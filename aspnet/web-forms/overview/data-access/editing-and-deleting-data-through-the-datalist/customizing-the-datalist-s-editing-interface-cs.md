---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
title: Настройка интерфейса правки элемента управления DataList (C#) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы создадим расширенный интерфейс редактирования для DataList, включающий элементов управления DropDownList и CheckBox.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: a5d13067-ddfb-4c36-8209-0f69fd40e45c
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 81f5a7f6737f544f577447f263dbd37dbc8279d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78480546"
---
# <a name="customizing-the-datalists-editing-interface-c"></a>Настройка интерфейса правки элемента управления DataList (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_CS.exe) или [Загрузка PDF-файла](customizing-the-datalist-s-editing-interface-cs/_static/datatutorial40cs1.pdf)

> В этом учебнике мы создадим расширенный интерфейс редактирования для DataList, включающий элементов управления DropDownList и CheckBox.

## <a name="introduction"></a>Введение

Разметка и веб-элементы управления в DataList `EditItemTemplate` определяют его изменяемый интерфейс. Во всех изменяемых примерах DataList, которые мы уже рассматривали ранее, редактируемый интерфейс состоит из веб-элементов управления TextBox. В [предыдущем учебном курсе](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md) мы улучшили взаимодействие с пользователем во время редактирования, добавив элементы управления проверки.

`EditItemTemplate` можно дополнительно расширить для включения веб-элементов управления, отличных от текстового поля, например элементов управления DropDownList, RadioButtonList, Calendars и т. д. Как и в случае с текстовыми полями, при настройке интерфейса редактирования для включения других веб-элементов управления выполните следующие действия.

1. Добавьте веб-элемент управления в `EditItemTemplate`.
2. Используйте синтаксис DataBinding, чтобы присвоить соответствующее значение полю данных соответствующему свойству.
3. В обработчике `UpdateCommand` событий получите программный доступ к значению веб-элемента управления и передайте его в соответствующий метод BLL.

В этом учебнике мы создадим расширенный интерфейс редактирования для DataList, включающий элементов управления DropDownList и CheckBox. В частности, мы создадим элемент управления DataList, содержащий сведения о продукте, и допускает обновление названия продукта, поставщика, категории и состояния "снято с производства" (см. рис. 1).

[![интерфейс редактирования включает текстовое поле, два элементов управления DropDownList и флажок.](customizing-the-datalist-s-editing-interface-cs/_static/image2.png)](customizing-the-datalist-s-editing-interface-cs/_static/image1.png)

**Рис. 1**. интерфейс редактирования включает текстовое поле, два элементов управления DropDownList и флажок ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image3.png)).

## <a name="step-1-displaying-product-information"></a>Шаг 1. Отображение сведений о продукте

Прежде чем можно будет создать интерфейс для редактирования DataList s, сначала необходимо создать интерфейс только для чтения. Для начала откройте страницу `CustomizedUI.aspx` из папки `EditDeleteDataList` и в конструкторе добавьте на страницу элемент управления DataList, установив для свойства `ID` значение `Products`. Из смарт-тега DataList создайте новый элемент управления ObjectDataSource. Назовите этот новый элемент ObjectDataSource `ProductsDataSource` и настройте его для получения данных из метода `ProductsBLL` класса s `GetProducts`. Как и в предыдущих руководствах по DataList, мы будем обновлять измененные сведения о продуктах, переполняя их непосредственно на уровень бизнес-логики. Соответственно, установите в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет).

[![установить в раскрывающихся списках "обновление", "вставить" и "Удалить" значение (нет)](customizing-the-datalist-s-editing-interface-cs/_static/image5.png)](customizing-the-datalist-s-editing-interface-cs/_static/image4.png)

**Рис. 2**. Установка в раскрывающихся СПИСКАХ «обновление», «вставка» и «удаление» (нет) ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image6.png))

После настройки ObjectDataSource Visual Studio создаст `ItemTemplate` по умолчанию для элемента управления DataList, в котором будет указано имя и значение для каждого возвращаемого поля данных. Измените `ItemTemplate` таким образом, чтобы шаблон выводит название продукта в элементе `<h4>`, а также имя категории, имя поставщика, Цена и состояние неподдерживаемого состояния. Более того, добавьте кнопку Edit (изменить), убедившись, что ее свойство `CommandName` имеет значение Edit. Декларативная разметка для My `ItemTemplate` выглядит следующим образом:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

Приведенная выше разметка размещает сведения о продукте, используя заголовок &lt;H4&gt; для названия продукта и `<table>` четыре столбца для остальных полей. Классы `ProductPropertyLabel` и `ProductPropertyValue` CSS, определенные в `Styles.css`, были рассмотрены в предыдущих руководствах. На рис. 3 показан ход выполнения при просмотре в браузере.

[![имя, поставщик, категория, неподдерживаемое состояние и цена каждого продукта.](customizing-the-datalist-s-editing-interface-cs/_static/image8.png)](customizing-the-datalist-s-editing-interface-cs/_static/image7.png)

**Рис. 3**. Отображение имени, поставщика, категории, неподдерживаемого состояния и цены каждого продукта ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image9.png))

## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>Шаг 2. Добавление веб-элементов управления в интерфейс правки

Первым шагом в создании настраиваемого интерфейса редактирования DataList является добавление необходимых веб-элементов управления в `EditItemTemplate`. В частности, нам нужен элемент DropDownList для категории, другой для поставщика, а флажок для состояния "снят с учета". Так как в этом примере цена продукта недоступна для редактирования, можно продолжить ее отображение с помощью веб-элемента управления Label.

Чтобы настроить интерфейс редактирования, щелкните ссылку Edit Templates (изменить шаблоны) в смарт-теге DataList и выберите параметр `EditItemTemplate` из раскрывающегося списка. Добавьте элемент DropDownList в `EditItemTemplate` и задайте для его `ID` значение `Categories`.

[![добавить DropDownList для категорий](customizing-the-datalist-s-editing-interface-cs/_static/image11.png)](customizing-the-datalist-s-editing-interface-cs/_static/image10.png)

**Рис. 4**. Добавление DropDownList для категорий ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image12.png))

Затем в смарт-теге DropDownList выберите вариант Выбор источника данных и создайте новый элемент ObjectDataSource с именем `CategoriesDataSource`. Настройте этот элемент ObjectDataSource для использования метода `GetCategories()` `CategoriesBLL` классов (см. рис. 5). Затем мастер настройки источника данных DropDownList s запрашивает поля данных для каждого `ListItem` s `Text` и `Value` свойств. В DropDownList отобразится поле данных `CategoryName` и используйте `CategoryID` в качестве значения, как показано на рис. 6.

[![создать новый элемент управления ObjectDataSource с именем CategoriesDataSource](customizing-the-datalist-s-editing-interface-cs/_static/image14.png)](customizing-the-datalist-s-editing-interface-cs/_static/image13.png)

**Рис. 5**. Создание нового элемента управления ObjectDataSource с именем `CategoriesDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image15.png))

[![настройке полей вывода и значений DropDownList](customizing-the-datalist-s-editing-interface-cs/_static/image17.png)](customizing-the-datalist-s-editing-interface-cs/_static/image16.png)

**Рис. 6**. Настройка полей отображения и значений DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image18.png))

Повторите эту последовательность действий, чтобы создать DropDownList для поставщиков. Задайте `ID` для этого DropDownList, чтобы `Suppliers` и присвоить имя `SuppliersDataSource`ObjectDataSource.

После добавления двух элементов управления DropDownList добавьте флажок для неподдерживаемого состояния и текстовое поле для имени продукта. Задайте `ID` s для CheckBox и текстового поля, чтобы `Discontinued` и `ProductName`соответственно. Добавьте RequiredFieldValidator, чтобы гарантировать, что пользователь предоставит значение для имени продукта.

Наконец, добавьте кнопки обновления и отмены. Помните, что для этих двух кнопок необходимо, чтобы свойства `CommandName` были настроены на обновление и отмену соответственно.

Вы можете создать макет интерфейса редактирования, но вам нравится. Я решил использовать тот же макет `<table>` четырех столбцов из интерфейса только для чтения, так как следующий декларативный синтаксис и снимок экрана иллюстрирует:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample2.aspx)]

[![интерфейс редактирования располагается как интерфейс только для чтения.](customizing-the-datalist-s-editing-interface-cs/_static/image20.png)](customizing-the-datalist-s-editing-interface-cs/_static/image19.png)

**Рис. 7**. интерфейс редактирования располагается как интерфейс только для чтения ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image21.png))

## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>Шаг 3. Создание обработчиков событий Едиткомманд и CancelCommand

В настоящее время в `EditItemTemplate` нет синтаксиса привязки данных (за исключением `UnitPriceLabel`, который был скопирован с `ItemTemplate`). Мы добавим синтаксис DataBinding мгновенно, но сначала создадим обработчики событий для `EditCommand` и `CancelCommand` событий DataList. Помните, что ответственность за `EditCommand` обработчика событий заключается в отображении интерфейса правки для элемента DataList, для которого была нажата кнопка Edit, в то время как задание `CancelCommand` s — возврат элемента управления DataList к состоянию до его предварительного редактирования.

Создайте эти два обработчика событий и используйте следующий код:

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample3.cs)]

При наличии этих двух обработчиков событий при нажатии кнопки «изменить» отображается интерфейс редактирования, а при нажатии кнопки «Отмена» отредактированный элемент возвращается в режим «только для чтения». На рис. 8 показан элемент управления DataList после нажатия кнопки Edit (изменить) Gumbo Chef Anton's s. Так как мы еще не добавили синтаксис привязки данных к интерфейсу правки, текстовое поле `ProductName` пусто, флажок `Discontinued` не установлен и первые элементы, выбранные из `Categories` и `Suppliers` элементов управления DropDownList.

[![нажатии кнопки "Изменить" отображается интерфейс редактирования](customizing-the-datalist-s-editing-interface-cs/_static/image23.png)](customizing-the-datalist-s-editing-interface-cs/_static/image22.png)

**Рис. 8**. при нажатии кнопки "Изменить" отображается интерфейс редактирования ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image24.png))

## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>Шаг 4. Добавление синтаксиса привязки данных в интерфейс правки

Чтобы интерфейс правки отображал значения текущих продуктов, необходимо использовать синтаксис DataBinding, чтобы присвоить значения полей данных соответствующим значениям веб-элемента управления. Синтаксис DataBinding можно применить в конструкторе, перейдя к экрану изменение шаблонов и выбрав ссылку изменить привязки данных в смарт-тегах элемента управления Web Controls. Кроме того, синтаксис DataBinding можно добавить непосредственно в декларативную разметку.

Присвойте значение поля `ProductName` данных `Text` свойству `ProductName` текстовое поле s, `CategoryID` и `SupplierID` значения полей данных `Categories` и `Suppliers` элементов управления DropDownList `SelectedValue` свойства, а значение поля данных `Discontinued` `Discontinued` свойству `Checked`. После внесения этих изменений либо с помощью конструктора, либо непосредственно через декларативную разметку снова откройте страницу в браузере и нажмите кнопку изменить для Chef Anton's s Gumbo Mix. Как показано на рис. 9, синтаксис DataBinding добавил текущие значения в TextBox, элементов управления DropDownList и CheckBox.

[![нажатии кнопки "Изменить" отображается интерфейс редактирования](customizing-the-datalist-s-editing-interface-cs/_static/image26.png)](customizing-the-datalist-s-editing-interface-cs/_static/image25.png)

**Рис. 9**. при нажатии кнопки "Изменить" отображается интерфейс редактирования ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image27.png))

## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>Шаг 5. Сохранение изменений пользователя в обработчике событий UpdateCommand

Когда пользователь редактирует продукт и нажимает кнопку "Обновить", происходит обратная передача и вызывается событие DataList `UpdateCommand`. В обработчике событий необходимо считывать значения из веб-элементов управления в `EditItemTemplate` и взаимодействовать с BLL для обновления продукта в базе данных. Как мы видели в предыдущих учебных курсах, `ProductID` обновленного продукта можно получить с помощью коллекции `DataKeys`. Доступ к пользовательским полям осуществляется путем программной ссылки на веб-элементы управления с помощью `FindControl("controlID")`, как показано в следующем коде:

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample4.cs)]

Код начинает с помощью свойства `Page.IsValid`, чтобы убедиться, что все элементы управления проверки на странице являются допустимыми. Если `Page.IsValid` `True`, то измененное значение `ProductID`ного продукта считывается из коллекции `DataKeys` и веб-элементы управления вводом данных в `EditItemTemplate` программными ссылками. Затем значения из этих веб-элементов управления считываются в переменные, которые затем передаются в соответствующую перегрузку `UpdateProduct`. После обновления данных элемент управления DataList возвращается в состояние предварительного редактирования.

> [!NOTE]
> Я не пропустил логику обработки исключений, добавленную в учебнике [обработка исключений BLL и DAL](handling-bll-and-dal-level-exceptions-cs.md) , чтобы сохранить код и этот пример. В качестве упражнения добавьте эту функцию после завершения работы с этим руководством.

## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>Шаг 6. Обработка значений ненулевого CategoryID и КодПоставщика

База данных Northwind позволяет `NULL` значения для `Products` таблицы s `CategoryID` и `SupplierID` столбцы. Однако наш интерфейс правки в настоящее время не поддерживает `NULL` значений. При попытке изменить продукт, имеющий `NULL` значение для столбцов `CategoryID` или `SupplierID`, мы получаем `ArgumentOutOfRangeException` с сообщением об ошибке следующего вида: *"Categories" имеет SelectedValue, который является недопустимым, так как он не существует в списке элементов.* Кроме того, в настоящее время нет возможности изменить категорию продукта или значение поставщика с не`NULL`ного значения на `NULL` одно.

Для поддержки `NULL` значений категории и поставщика элементов управления DropDownList необходимо добавить дополнительный `ListItem`. Я решил использовать (None) в качестве значения `Text` для этого `ListItem`, но вы можете изменить его на другое (например, пустую строку), если вы d. Наконец, не забудьте установить `AppendDataBoundItems` элементов управления DropDownList в `True`; Если вы забыли это сделать, категории и поставщики, привязанные к DropDownList, будут перезаписывать статически добавленные `ListItem`.

После внесения этих изменений разметка элементов управления DropDownList в DataList s `EditItemTemplate` должна выглядеть следующим образом:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample5.aspx)]

> [!NOTE]
> Статические `ListItem` s можно добавить в элемент DropDownList через конструктор или напрямую с помощью декларативного синтаксиса. При добавлении элемента DropDownList для представления `NULL` значения базы данных не забудьте добавить `ListItem` с помощью декларативного синтаксиса. При использовании редактора коллекции `ListItem` в конструкторе созданный декларативный синтаксис будет полностью опускать параметр `Value` при присвоении пустой строки, создавая декларативную разметку, например: `<asp:ListItem>(None)</asp:ListItem>`. Хотя это может показаться безобидным, отсутствующий `Value` заставляет DropDownList использовать значение свойства `Text`. Это означает, что если выбран этот `NULL` `ListItem`, то будет предпринята попытка назначения значения (None) полю данных продукта (`CategoryID` или `SupplierID`в этом руководстве), что приведет к возникновению исключения. При явном задании `Value=""`для поля данных продукта будет присвоено значение `NULL` при выборе `NULL` `ListItem`.

Уделите время для просмотра хода выполнения в браузере. При редактировании продукта Обратите внимание, что `Categories` и `Suppliers` элементов управления DropDownList имеют параметр (нет) в начале DropDownList.

[![категории и поставщики элементов управления DropDownList включить параметр (None)](customizing-the-datalist-s-editing-interface-cs/_static/image29.png)](customizing-the-datalist-s-editing-interface-cs/_static/image28.png)

**Рис. 10**. `Categories` и `Suppliers` элементов управления DropDownList включают параметр (None) ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-datalist-s-editing-interface-cs/_static/image30.png))

Чтобы сохранить параметр (None) в качестве значения `NULL` базы данных, необходимо вернуться к обработчику событий `UpdateCommand`. Измените `categoryIDValue` и `supplierIDValue` переменные так, чтобы они допускали значение NULL целыми числами, и назначьте им значения, отличные от `Nothing` только в том случае, если `SelectedValue` DropDownList не является пустой строкой:

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample6.cs)]

После этого изменения значение `Nothing` будет передано в метод `UpdateProduct` BLL, если пользователь выбрал параметр (нет) в любом из раскрывающихся списков, который соответствует значению `NULL` базы данных.

## <a name="summary"></a>Сводка

В этом учебнике мы увидели, как создать более сложный интерфейс редактирования DataList, включающий в себя три различных входных веб-элемента управления TextBox, два элементов управления DropDownList и флажок вместе с элементами управления проверки. При создании интерфейса редактирования шаги одинаковы, независимо от используемых веб-элементов управления: Начните с добавления веб-элементов управления в DataList s `EditItemTemplate`; Используйте синтаксис DataBinding, чтобы присвоить соответствующие значения полей данных соответствующим свойствам веб-элемента управления. и в обработчике событий `UpdateCommand` программным способом получить доступ к веб-элементам управления и их соответствующим свойствам, передав их значения в BLL.

При создании интерфейса редактирования, состоящего из текстовых полей или коллекции различных веб-элементов управления, обязательно правильно обрабатывать значения `NULL` базы данных. При использовании учета для `NULL` необходимо не только правильно отобразить существующее значение `NULL` в интерфейсе редактирования, но и предоставить возможность пометить значение как `NULL`. Для элементов управления DropDownList в списках данных это обычно означает Добавление статического `ListItem`, для свойства `Value` которого явно задана пустая строка (`Value=""`), и Добавление фрагмента кода в обработчик событий `UpdateCommand`, чтобы определить, выбран ли `NULL``ListItem`.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого учебника были Деннис Patterson, Дэвид суру и Рэнди Шмидт. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)
> [Вперед](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
