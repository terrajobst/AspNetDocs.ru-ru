---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
title: Ограничение функциональных возможностей изменения данных на основе пользователя (C#) | Документация Майкрософт
author: rick-anderson
description: В веб-приложении, позволяющем пользователям изменять данные, различные учетные записи пользователей могут иметь разные права на редактирование данных. В этом учебнике мы рассмотрим, как t...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 2b251c82-77cf-4e36-baa9-b648eddaa394
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
msc.type: authoredcontent
ms.openlocfilehash: c3cacaddb7e9b493ba39718f41dcaab360d36fd9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78478428"
---
# <a name="limiting-data-modification-functionality-based-on-the-user-c"></a>Ограничение функций изменения данных в зависимости от пользователя (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_CS.exe) или [Загрузка PDF-файла](limiting-data-modification-functionality-based-on-the-user-cs/_static/datatutorial23cs1.pdf)

> В веб-приложении, позволяющем пользователям изменять данные, различные учетные записи пользователей могут иметь разные права на редактирование данных. В этом учебнике мы рассмотрим, как динамически настраивать возможности изменения данных на основе посещения пользователя.

## <a name="introduction"></a>Введение

Ряд веб-приложений поддерживает учетные записи пользователей и предоставляет различные возможности, отчеты и функциональные возможности на основе вошедшего в систему пользователя. Например, в наших руководствах мы хотим разрешить пользователям из компаний-поставщиков входить на сайт и обновлять общую информацию о своих продуктах — их название и количество на единицу, возможно, вместе с информацией о поставщике, например названием компании. адрес, сведения о контактном лице и т. д. Кроме того, может потребоваться включить некоторые учетные записи пользователей из нашей компании, чтобы они могли входить в систему и обновлять информацию о продуктах, например единицы на акции, на уровне переупорядочения и т. д. Наше веб-приложение может также разрешить посещение анонимных пользователей (тех, кто не вошел в систему), но ограничит их только просмотром данных. Используя такую систему учетных записей пользователей, мы хотим, чтобы веб-элементы управления данными на страницах ASP.NET предлагали возможности вставки, правки и удаления, соответствующие текущему пользователю, вошедшему в систему.

В этом учебнике мы рассмотрим, как динамически настраивать возможности изменения данных на основе посещения пользователя. В частности, мы создадим страницу, отображающую сведения о поставщиках в редактируемой DetailsView вместе с GridView, в котором перечислены продукты, предоставляемые поставщиком. Если пользователь посещает страницу из нашей компании, он может: просматривать любые сведения о поставщиках; Измените адрес. и изменяют информацию для любого продукта, предоставленного поставщиком. Однако если пользователь принадлежит определенной компании, он может только просматривать и изменять свои сведения об адресе и изменять только те продукты, которые не были помечены как снятые.

[![пользователь из нашей компании может изменять любые сведения о поставщиках](limiting-data-modification-functionality-based-on-the-user-cs/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image1.png)

**Рис. 1**. пользователь из нашей компании может изменять любые сведения о поставщиках ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image3.png)).

[![пользователь определенного поставщика может только просматривать и изменять сведения](limiting-data-modification-functionality-based-on-the-user-cs/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image4.png)

**Рис. 2**. пользователь конкретного поставщика может только просматривать и изменять сведения ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image6.png))

Давайте приступим к работе!

> [!NOTE]
> Система членства ASP.NET 2,0 предоставляет стандартизированную, расширяемую платформу для создания и проверки учетных записей пользователей, а также управления ими. Поскольку исследование системы членства выходит за рамки этих руководств, в этом учебнике рассматривается «имитация» членства, позволяя анонимным посетителям выбирать, принадлежат ли они конкретному поставщику или нашей компании. Дополнительные сведения о членстве см. в статье [исследование членства, ролей и профилей в ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx) .

## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>Шаг 1. Разрешение пользователю на указание прав доступа

В реальном веб-приложении сведения об учетной записи пользователя могут указывать, работали ли они для нашей компании или для конкретного поставщика, и эта информация будет программно доступна из наших страниц ASP.NET после входа пользователя на сайт. Эта информация может быть захвачена с помощью системы ролей ASP.NET 2,0, как данные учетной записи на уровне пользователя через систему профилей, или через некоторые пользовательские средства.

Поскольку целью этого учебника является демонстрация настройки возможностей модификации данных на основе вошедшего в систему пользователя и не предназначенного для демонстрации членства, ролей и систем профилей ASP.NET 2,0, мы будем использовать очень простой механизм для определения возможности для пользователя, который посещает страницу — DropDownList, с помощью которого пользователь может просматривать и редактировать сведения о поставщиках, или, Кроме того, сведения о конкретных поставщиках, которые они могут просматривать и изменять. Если пользователь указывает, что он может просматривать и редактировать все сведения о поставщике (по умолчанию), он может пролистывать всех поставщиков, изменять сведения об адресах поставщиков и изменять имя и количество единиц для любого продукта, предоставленного выбранным поставщиком. Однако если пользователь указывает, что он может только просматривать и редактировать конкретного поставщика, он может только просматривать сведения и продукты для этого поставщика, а также обновлять только сведения об имени и количестве на единицу для тех продуктов, которые больше *не* поддерживаются.

Первым шагом в этом руководстве является создание этого DropDownList и заполнение его поставщиками в системе. Откройте страницу `UserLevelAccess.aspx` в папке `EditInsertDelete`, добавьте элемент управления DropDownList, свойство `ID` которого имеет значение `Suppliers`, и свяжите этот элемент управления DropDownList с новым ObjectDataSource с именем `AllSuppliersDataSource`.

[![создать новый элемент управления ObjectDataSource с именем Аллсупплиерсдатасаурце](limiting-data-modification-functionality-based-on-the-user-cs/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image7.png)

**Рис. 3**. Создание нового элемента управления ObjectDataSource с именем `AllSuppliersDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image9.png))

Так как в DropDownList требуется включить все поставщики, настройте ObjectDataSource для вызова метода `GetSuppliers()` класса `SuppliersBLL`. Также убедитесь, что метод ObjectDataSource `Update()` сопоставлен с методом `SuppliersBLL` класса s `UpdateSupplierAddress`, так как этот элемент управления ObjectDataSource также будет использоваться элементом управления DetailsView, который будет добавлен на шаге 2.

После завершения работы мастера ObjectDataSource выполните действия, настроив `Suppliers` DropDownList таким образом, чтобы в нем было указано `CompanyName` поле данных и в качестве значения для каждого `ListItem`используется поле `SupplierID` данных.

[![настроить в DropDownList поставщиков поля данных CompanyName и КодПоставщика.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image10.png)

**Рис. 4**. Настройка `Suppliers` DropDownList для использования полей данных `CompanyName` и `SupplierID` ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image12.png))

На этом этапе DropDownList перечисляет названия компаний поставщиков в базе данных. Однако в DropDownList также необходимо включить параметр "показывать/изменить все поставщики". Для этого присвойте свойству `Suppliers` DropDownList `AppendDataBoundItems` значение `true`, а затем добавьте `ListItem`, свойство `Text` которых имеет значение "отобразить/изменить всех поставщиков", а — `-1`. Это можно добавить непосредственно в декларативной разметке или в конструкторе, перейдя к окно свойств и щелкнув многоточие в свойстве DropDownList s `Items`.

> [!NOTE]
> Дополнительные сведения о добавлении элемента «выделить все» в элемент DropDownList с привязкой к данным см. в статье [*Фильтрация "основной/подробности*](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) " в разделе "учебник по DropDownList".

После установки свойства `AppendDataBoundItems` и добавления `ListItem` декларативная разметка DropDownList должна выглядеть следующим образом:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample1.aspx)]

На рис. 5 показан снимок экрана текущего хода выполнения при просмотре в браузере.

[![список «поставщики» содержит элемент «отображать все ListItem», а по одному для каждого поставщика](limiting-data-modification-functionality-based-on-the-user-cs/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image13.png)

**Рис. 5**. `Suppliers` DropDownList содержит показ всех `ListItem`и по одному для каждого поставщика ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image15.png)).

Так как мы хотим обновить пользовательский интерфейс сразу после того, как пользователь изменил свой выбор, задайте для свойства `Suppliers` DropDownList `AutoPostBack` значение `true`. На шаге 2 мы создадим элемент управления DetailsView, который будет отображать сведения для поставщиков на основе выбора DropDownList. Затем на шаге 3 мы создадим обработчик событий для этого события DropDownList `SelectedIndexChanged`, в котором мы добавим код, который привязывает соответствующую информацию о поставщике к элементу DetailsView на основе выбранного поставщика.

## <a name="step-2-adding-a-detailsview-control"></a>Шаг 2. Добавление элемента управления DetailsView

Разрешите использовать DetailsView для отображения сведений о поставщике. Для пользователя, который может просматривать и изменять всех поставщиков, элемент DetailsView поддерживает разбиение на страницы, позволяя пользователю пошагово прокручивать данные поставщика по одной записи за раз. Однако если пользователь работает с определенным поставщиком, то DetailsView покажет только эту конкретную информацию о поставщике и не будет включать интерфейс разбиения по страницам. В любом случае элемент DetailsView должен разрешить пользователю изменять поля адрес, город и страна поставщика.

Добавьте элемент DetailsView на страницу под `Suppliers` DropDownList, установите для свойства `ID` значение `SupplierDetails`и привяжите его к `AllSuppliersDataSource` ObjectDataSource, созданному на предыдущем шаге. Затем установите флажки Включить разбиение по страницам и включить редактирование из смарт-тега DetailsView s.

> [!NOTE]
> Если вы не видите параметр Enable Edit в смарт-теге DetailsView s, так как вы не сопоставляли метод ObjectDataSource `Update()` в метод `SuppliersBLL` класса s `UpdateSupplierAddress`. Уделите немного времени, чтобы вернуться к этому изменению конфигурации, после чего в смарт-теге DetailsView s должен появиться параметр Включить изменение.

Поскольку метод `SuppliersBLL` классов `UpdateSupplierAddress` принимает только четыре параметра — `supplierID`, `address`, `city`и `country` — измените BoundFields DetailsView s таким образом, чтобы `CompanyName` и `Phone` BoundFields были доступны только для чтения. Кроме того, полностью удалите `SupplierID` BoundField. Наконец, у `AllSuppliersDataSource` ObjectDataSource в данный момент свойство `OldValuesParameterFormatString` имеет значение `original_{0}`. Уделите немного времени, чтобы полностью удалить этот параметр свойства из декларативного синтаксиса, или присвоить ему значение по умолчанию `{0}`.

После настройки `SupplierDetails` DetailsView и `AllSuppliersDataSource` ObjectDataSource у нас будет следующая декларативная разметка:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample2.aspx)]

На этом этапе DetailsView можно пролистывать, а выбранные сведения об адресе поставщика могут быть обновлены независимо от выбора, сделанного в `Suppliers` DropDownList (см. рис. 6).

[![просмотреть сведения о поставщиках, и его адрес будет обновлен.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image16.png)

**Рис. 6**. Просмотр сведений о поставщиках и его адрес в обновленном[виде (щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image18.png))

## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>Шаг 3. Отображение только выбранных сведений о поставщике

В настоящее время наша страница отображает сведения обо всех поставщиках независимо от того, был ли выбран конкретный поставщик из `Suppliers` DropDownList. Чтобы отобразить только сведения о поставщике для выбранного поставщика, необходимо добавить на нашу страницу еще один элемент управления ObjectDataSource, который получает сведения о конкретном поставщике.

Добавьте на страницу новый элемент управления ObjectDataSource, назвав его `SingleSupplierDataSource`. В смарт-теге щелкните ссылку Configure Data Source (настроить источник данных) и используйте метод `SuppliersBLL` класса s `GetSupplierBySupplierID(supplierID)`. Как и в случае с `AllSuppliersDataSource` ObjectDataSource, `SingleSupplierDataSource` ObjectDataSource s `Update()` метод, сопоставленный с методом `SuppliersBLL` Class s `UpdateSupplierAddress`.

[![настроить ObjectDataSource Синглесупплиердатасаурце для использования метода Жетсупплиербисупплиерид (КодПоставщика)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image19.png)

**Рис. 7**. Настройка `SingleSupplierDataSource` ObjectDataSource для использования метода `GetSupplierBySupplierID(supplierID)` ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image21.png))

Далее мы восиспользуем запрос на указание источника параметра для `GetSupplierBySupplierID(supplierID)` метода s `supplierID` входного параметра. Так как мы хотим отобразить сведения о поставщике, выбранном из DropDownList, используйте свойство `Suppliers` DropDownList s `SelectedValue` в качестве источника параметра.

[![использовать DropDownList "поставщики" в качестве источника параметра "КодПоставщика"](limiting-data-modification-functionality-based-on-the-user-cs/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image22.png)

**Рис. 8**. Использование `Suppliers` DropDownList в качестве источника параметра `supplierID` ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image24.png))

Даже при добавлении второго элемента ObjectDataSource элемент управления DetailsView в настоящее время настроен так, чтобы всегда использовать `AllSuppliersDataSource` ObjectDataSource. Необходимо добавить логику для корректировки источника данных, используемого DetailsView в зависимости от выбранного элемента DropDownList `Suppliers`. Чтобы сделать это, создайте обработчик событий `SelectedIndexChanged` для DropDownList поставщиков. Это можно легко создать, дважды щелкнув элемент DropDownList в конструкторе. Этот обработчик событий должен определить, какой источник данных следует использовать, и повторно привязать данные к элементу DetailsView. Это выполняется с помощью следующего кода:

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample3.cs)]

Обработчик событий начинает с определения того, был ли выбран параметр «Показывать или изменять всех поставщиков». Если это так, `SupplierDetails` DetailsView `DataSourceID` `AllSuppliersDataSource` и вернет пользователя к первой записи в наборе поставщиков, установив для свойства `PageIndex` значение 0. Однако если пользователь выбрал конкретного поставщика из DropDownList, то `DataSourceID` DetailsView s назначается `SingleSuppliersDataSource`. Независимо от используемого источника данных, режим `SuppliersDetails` возвращается к режиму только для чтения, а данные повторно привязываются к элементу DetailsView с помощью вызова метода `SuppliersDetails` Control s `DataBind()`.

После выполнения этого обработчика событий элемент управления DetailsView теперь показывает выбранного поставщика, если не выбран параметр "Показать/изменить всех поставщиков". в этом случае все поставщики можно просматривать через интерфейс разбиения по страницам. На рис. 9 показана страница с выбранным параметром "Показать/изменить всех поставщиков". Обратите внимание, что имеется интерфейс разбиения по страницам, позволяющий пользователю посетить и обновить любого поставщика. На рис. 10 показана страница с выбранным поставщиком MA Маисон. В этом случае доступна только информация MA Маисон s.

[![все сведения о поставщиках можно просмотреть и изменить.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image25.png)

**Рис. 9**. можно просмотреть и изменить все сведения о поставщиках ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image27.png))

[![просмотреть и изменить можно только выбранные сведения о поставщике](limiting-data-modification-functionality-based-on-the-user-cs/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image28.png)

**Рис. 10**. просматривать и изменять можно только выбранные сведения о поставщиках ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image30.png))

> [!NOTE]
> В этом учебнике для элементов управления DropDownList и DetailsView `EnableViewState` должно быть задано значение `true` (по умолчанию), так как элементы DropDownList s `SelectedIndex` и свойства `DataSourceID` DetailsView s должны быть сохранены во всех обратных передачах.

## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>Шаг 4. Перечисление продуктов поставщиков в редактируемом элементе управления GridView

Теперь, когда элемент DetailsView завершен, наш следующий шаг заключается в включении редактируемого элемента управления GridView, содержащего список продуктов, предоставленных выбранным поставщиком. Этот элемент GridView должен допускать изменения только для полей `ProductName` и `QuantityPerUnit`. Более того, если пользователь посещает страницу от конкретного поставщика, он должен допускать обновления только тех продуктов, которые *не* будут прекращены. Для этого необходимо сначала добавить перегрузку метода `ProductsBLL` класса `UpdateProducts`, который принимает в качестве входных данных только поля `ProductID`, `ProductName`и `QuantityPerUnit`. Мы подробно проведем этот процесс в многочисленных учебных курсах, так что давайте просто взглянем на код, который следует добавить в `ProductsBLL`:

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample4.cs)]

После создания этой перегрузки мы повторно готовы к добавлению элемента управления GridView и связанного с ним ObjectDataSource. Добавьте на страницу новый элемент управления GridView, задайте для его свойства `ID` значение `ProductsBySupplier`и настройте его для использования нового элемента управления ObjectDataSource с именем `ProductsBySupplierDataSource`. Так как мы хотим, чтобы этот элемент управления GridView перечислит эти продукты выбранным поставщиком, используйте метод `ProductsBLL` класса s `GetProductsBySupplierID(supplierID)`. Также сопоставьте метод `Update()` с новой перегрузкой `UpdateProduct`, которую мы только что создали.

[![настроить ObjectDataSource для использования только что созданной перегрузки UpdateProduct](limiting-data-modification-functionality-based-on-the-user-cs/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image31.png)

**Рис. 11**. Настройка ObjectDataSource для использования только что созданной перегрузки `UpdateProduct` ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image33.png))

Мы повторно предлагаем вам выбрать источник параметра для `GetProductsBySupplierID(supplierID)` метода s `supplierID` входного параметра. Так как мы хотим отобразить продукты для поставщика, выбранного в DetailsView, используйте свойство `SuppliersDetails` DetailsView Control s `SelectedValue` в качестве источника параметра.

[![использовать свойство SelectedValue Супплиерсдетаилс DetailsView в качестве источника параметра](limiting-data-modification-functionality-based-on-the-user-cs/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image34.png)

**Рис. 12**. использование свойства `SelectedValue` `SuppliersDetails` DetailsView s в качестве источника параметра ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image36.png))

После возврата в GridView удалите все поля GridView, за исключением `ProductName`, `QuantityPerUnit`и `Discontinued`, помечая `Discontinued` CheckBoxField как доступное только для чтения. Также установите флажок Включить правку в смарт-теге GridView s. После внесения этих изменений декларативная разметка для GridView и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample5.aspx)]

Как и в предыдущих элементах ObjectDataSource, это свойство `OldValuesParameterFormatString` имеет значение `original_{0}`, что вызовет проблемы при попытке обновить имя или количество продукта на единицу. Удалите это свойство из декларативного синтаксиса или задайте для него значение по умолчанию `{0}`.

После завершения этой настройки на нашей странице будут перечислены продукты, предоставленные поставщиком, выбранным в GridView (см. рис. 13). В настоящее время можно обновить *любое* имя или количество продуктов на единицу. Однако нам нужно обновить логику страницы таким образом, чтобы такая функциональность была запрещена для неподдерживаемых продуктов для пользователей, связанных с определенным поставщиком. Мы обсудим эту последнюю часть на шаге 5.

[![отображаются продукты, предоставленные выбранным поставщиком.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image37.png)

**Рис. 13**. отображаются продукты, предоставленные выбранным поставщиком ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image39.png))

> [!NOTE]
> Добавление этого редактируемого элемента управления GridView позволяет обновить обработчик событий `Suppliers` DropDownList s `SelectedIndexChanged`, чтобы вернуть GridView к состоянию только для чтения. В противном случае при выборе другого поставщика в процессе редактирования сведений о продукте соответствующий индекс в GridView для нового поставщика также будет доступен для редактирования. Чтобы избежать этого, просто установите для свойства `EditIndex` GridView s значение `-1` в обработчике событий `SelectedIndexChanged`.

Также помните, что необходимо включить состояние представления GridView s (поведение по умолчанию). Если для свойства `EnableViewState` GridView s задано значение `false`, возникает риск непреднамеренного удаления или изменения записей одновременно выполняющимися пользователями. См. [Предупреждение: ошибка параллелизма с ASP.NET 2,0 gridviews/DetailsView/FormView, которые поддерживают редактирование и (или) удаление, а состояние представления — "отключено](http://scottonwriting.net/sowblog/posts/10054.aspx) " для получения дополнительных сведений.

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>Шаг 5. Запрет изменения для неподдерживаемых продуктов, если не выбран параметр "отображать или изменять всех поставщиков"

Хотя `ProductsBySupplier` GridView полностью работоспособен, он предоставляет слишком большой доступ пользователям, которые относятся к определенному поставщику. В соответствии с бизнес-правилами такие пользователи не должны иметь возможности обновлять Неподдерживаемые продукты. Для этого можно скрыть (или отключить) кнопку "Изменить" в этих строках GridView с неподдерживаемыми продуктами, когда пользователь посещает страницу от поставщика.

Создайте обработчик событий для события `RowDataBound` GridView s. В этом обработчике событий необходимо определить, связан ли пользователь с определенным поставщиком, что, для этого руководства, можно определить, установив флажок поставщики DropDownList `SelectedValue` свойство. Если оно отличается от-1, то пользователь связан с определенным поставщиком. Для таких пользователей необходимо определить, прекращен ли продукт. Можно взять ссылку на фактический экземпляр `ProductRow`, привязанный к строке GridView, через свойство `e.Row.DataItem`, как описано в разделе [*Отображение сводных данных в этом*](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md) руководстве. Если продукт прекращен, мы можем получить программную ссылку на кнопку Edit (изменить) в элементе управления GridView s CommandField, используя методики, описанные в предыдущем руководстве, [*добавив подтверждение на стороне клиента при удалении*](adding-client-side-confirmation-when-deleting-cs.md). После получения ссылки можно скрыть или отключить кнопку.

[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample6.cs)]

При использовании этого обработчика событий при посещении этой страницы в качестве пользователя от конкретного поставщика недоступные продукты не редактируются, так как кнопка Изменить скрыта для этих продуктов. Например, Chef Anton's s Gumbo Mix — это неподдерживаемый продукт для нового поставщика Orleans Cajun light. При посещении страницы этого конкретного поставщика кнопка Изменить для этого продукта скрыта (см. рис. 14). Однако при посещении с помощью команды "Показать/изменить всех поставщиков" доступна кнопка "Изменить" (см. рис. 15).

[![для пользователей, зависящих от поставщика, кнопка Изменить для Chef Anton's s Gumbo смесь скрыта.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image40.png)

**Рис. 14**. для пользователей, связанных с конкретными поставщиками, кнопка Изменить для Chef Anton's s Gumbo Mix скрыта ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image42.png))

[![для отображения или изменения всех пользователей-поставщиков отображается кнопка Изменить для Chef Anton's s Gumbo Mix.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image43.png)

**Рис. 15**. для отображения или изменения всех пользователей-поставщиков отображается кнопка Изменить для Chef Anton's s Gumbo Mix ([щелкните, чтобы просмотреть изображение с полным размером](limiting-data-modification-functionality-based-on-the-user-cs/_static/image45.png)).

## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>Проверка прав доступа на уровне бизнес-логики

В этом руководстве страница ASP.NET обрабатывает всю логику с учетом информации, которую может видеть пользователь, и продуктов, которые он может обновить. В идеале эта логика также будет присутствовать на уровне бизнес-логики. Например, метод `SuppliersBLL` классов `GetSuppliers()` (который возвращает все поставщики) может включать проверку, чтобы убедиться, что вошедший в систему пользователь *не* связан с конкретным поставщиком. Аналогичным образом, метод `UpdateSupplierAddress` может включать проверку, чтобы убедиться, что вошедший в систему пользователь работал в нашей компании (и, следовательно, может обновить все сведения об адресе поставщиков) или связан с поставщиком, чьи данные обновляются.

Я не включил такие проверки уровня BLL, так как в нашем руководстве права пользователя определяются DropDownList на странице, к которому не удается получить доступ классы BLL. При использовании системы членства или одной из встроенных схем проверки подлинности, предоставляемых ASP.NET (например, проверка подлинности Windows), сведения о пользователях и ролях, вошедшие в систему, можно получить из BLL, делая таким образом такой доступ. проверки прав на уровне представления и слоя BLL.

## <a name="summary"></a>Сводка

Большинство сайтов, предоставляющих учетные записи пользователей, должны настраивать интерфейс изменения данных на основе вошедшего в систему пользователя. Пользователи с правами администратора могут удалять и изменять любые записи, в то время как пользователи, не являющиеся администраторами, могут быть ограничены только обновлением или удалением созданных ими записей. Независимо от ситуации, классы веб-элементов управления данными, ObjectDataSource и Business Logic могут быть расширены для добавления или отмены определенных функций на основе вошедшего в систему пользователя. В этом учебнике мы увидели, как ограничить доступные для просмотра и редактируемые данные в зависимости от того, связан ли пользователь с конкретным поставщиком или работал ли он с нашей компанией.

Этот учебник завершает изучение вставки, обновления и удаления данных с помощью элементов управления GridView, DetailsView и FormView. Начиная со следующего руководства мы соберем, как добавить поддержку разбиения по страницам и сортировки.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Назад](adding-client-side-confirmation-when-deleting-cs.md)
> [Вперед](an-overview-of-inserting-updating-and-deleting-data-vb.md)
