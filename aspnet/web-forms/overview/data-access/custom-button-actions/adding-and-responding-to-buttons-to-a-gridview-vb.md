---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
title: Добавление кнопок в GridView (VB) и реагирование на них | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы рассмотрим, как добавить настраиваемые кнопки как в шаблон, так и в поля элемента управления GridView или DetailsView. В частности, мы буи...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 06c6bbd2-4bdc-435b-87a3-df2c868f4baa
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
msc.type: authoredcontent
ms.openlocfilehash: 8727d8faead02340d223c75845bf29f63d1a0834
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74601352"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-vb"></a>Добавление кнопок и ответов на них к GridView (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_VB.exe) или [Загрузка PDF-файла](adding-and-responding-to-buttons-to-a-gridview-vb/_static/datatutorial28vb1.pdf)

> В этом учебнике мы рассмотрим, как добавить настраиваемые кнопки как в шаблон, так и в поля элемента управления GridView или DetailsView. В частности, мы создадим интерфейс с FormView, который позволяет пользователю пролистывать поставщиков.

## <a name="introduction"></a>Введение

Несмотря на то, что многие сценарии составления отчетов включают доступ только для чтения к данным отчета, в отчетах не часто встречаются возможности выполнения действий на основе отображаемых данных. Обычно это связано с добавлением веб-элемента управления Button, LinkButton или ImageButton с каждой отображаемой в отчете записью, которая при нажатии вызывает обратную передачу и вызывает некоторый код на стороне сервера. Наиболее распространенным примером является изменение и удаление данных на основе записи. На самом деле, как было показано, начиная с [обзора вставки, обновления и удаления данных учебник по вставке, обновлению](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) и удалению является настолько распространенным, что элементы управления GridView, DetailsView и FormView могут поддерживать такую функциональность без необходимости написания одной строки кода.

В дополнение к кнопкам "Правка" и "Удалить" элементы управления GridView, DetailsView и FormView могут также включать кнопки, LinkButton или Имажебуттонс, которые при нажатии выполняют некоторую пользовательскую логику на стороне сервера. В этом учебнике мы рассмотрим, как добавить настраиваемые кнопки как в шаблон, так и в поля элемента управления GridView или DetailsView. В частности, мы создадим интерфейс с FormView, который позволяет пользователю пролистывать поставщиков. Для данного поставщика FormView будет показывать сведения о поставщике вместе с веб-элементом управления "Кнопка", при нажатии которого все связанные с ним продукты будут помечены как снятые с работы. Кроме того, GridView перечисляет продукты, предоставляемые выбранным поставщиком, с каждой строкой, содержащей кнопки увеличения цены и скидки, которые при нажатии увеличивают или уменьшают продукт `UnitPrice` на 10% (см. рис. 1).

[![как FormView, так и GridView содержат кнопки, выполняющие настраиваемые действия](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image1.png)

**Рис. 1**. как FormView, так и GridView содержат кнопки для выполнения настраиваемых действий ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image3.png)).

## <a name="step-1-adding-the-button-tutorial-web-pages"></a>Шаг 1. Добавление веб-страниц учебника по кнопкам

Прежде чем мы посмотрим, как добавлять пользовательские кнопки, давайте сначала создадим страницы ASP.NET в нашем проекте веб-сайта, которые понадобятся для работы с этим руководством. Для начала добавьте новую папку с именем `CustomButtons`. Затем добавьте следующие две страницы ASP.NET в эту папку, чтобы связать каждую страницу с главной страницей `Site.master`:

- `Default.aspx`
- `CustomButtons.aspx`

![Добавление страниц ASP.NET для руководств, связанных с пользовательскими кнопками](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image4.png)

**Рис. 2**. добавление страниц ASP.NET для руководств, связанных с пользовательскими кнопками

Как и в других папках, `Default.aspx` в папке `CustomButtons` будут перечислены учебники в разделе. Вспомним, что `SectionLevelTutorialListing.ascx` пользовательский элемент управления предоставляет эти функции. Таким образом, добавьте этот пользовательский элемент управления в `Default.aspx`, перетащив его из обозреватель решений на страницу s представление конструирования.

[![добавить пользовательский элемент управления SectionLevelTutorialListing. ascx в Default. aspx](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image5.png)

**Рис. 3**. Добавление пользовательского элемента управления `SectionLevelTutorialListing.ascx` в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image7.png))

Наконец, добавьте страницы в качестве записей в файл `Web.sitemap`. В частности, добавьте следующую разметку после разбиения на страницы и сортировки `<siteMapNode>`:

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample1.xml)]

После обновления `Web.sitemap`просмотрите веб-сайт учебников в браузере. В меню слева теперь содержатся элементы для учебников по редактированию, вставке и удалению.

![На карте узла теперь есть запись для учебника по настраиваемым кнопкам](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image8.png)

**Рис. 4**. в карте узла теперь есть запись для учебника по настраиваемым кнопкам

## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>Шаг 2. Добавление элемента FormView, содержащего список поставщиков

Давайте приступим к работе с этим руководством, добавив FormView, в котором перечислены поставщики. Как обсуждалось во введении, этот FormView позволит пользователю пролистывать поставщиков, отображая продукты, предоставленные поставщиком в GridView. Кроме того, в этот FormView будет включена кнопка, которая при нажатии пометит все продукты поставщика как снятые с работы. Прежде чем приступить к работе с добавлением пользовательской кнопки в FormView, давайте сначала создадим FormView, чтобы отобразить сведения о поставщике.

Для начала откройте страницу `CustomButtons.aspx` в папке `CustomButtons`. Добавьте элемент FormView на страницу, перетащив его с панели элементов в конструктор, и задайте для его свойства `ID` значение `Suppliers`. В смарт-теге FormView s выберите создать новый элемент управления ObjectDataSource с именем `SuppliersDataSource`.

[![создать новый элемент управления ObjectDataSource с именем Супплиерсдатасаурце](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image9.png)

**Рис. 5**. Создание нового элемента управления ObjectDataSource с именем `SuppliersDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image11.png))

Настройте этот новый элемент ObjectDataSource таким способом, чтобы он запрашивается из метода `GetSuppliers()` `SuppliersBLL` классов (см. рис. 6). Поскольку этот элемент FormView не предоставляет интерфейс для обновления сведений о поставщике, выберите параметр (нет) в раскрывающемся списке на вкладке обновление.

[![настроить источник данных для использования метода Супплиерсблл класса s ()](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image12.png)

**Рис. 6**. Настройка источника данных на использование метода `GetSuppliers()` `SuppliersBLL` классов ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image14.png))

После настройки ObjectDataSource Visual Studio создаст `InsertItemTemplate`, `EditItemTemplate`и `ItemTemplate` для FormView. Удалите `InsertItemTemplate` и `EditItemTemplate` и измените `ItemTemplate`, чтобы в нем отображалось только название компании поставщика и номер телефона. Наконец, включите поддержку разбиения по страницам для FormView, установив флажок Включить разбиение по страницам из своего смарт-тега (или задав для свойства `AllowPaging` значение `True`). После внесения этих изменений декларативная разметка страницы должна выглядеть следующим образом:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample2.aspx)]

На рис. 7 показана страница CustomButtons. aspx при просмотре в браузере.

[![FormView содержит поля CompanyName и Phone для текущего выбранного поставщика.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image15.png)

**Рис. 7**. список полей `CompanyName` и `Phone` из выбранного в данный момент поставщика ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image17.png))

## <a name="step-3-adding-a-gridview-that-lists-the-selected-supplier-s-products"></a>Шаг 3. Добавление элемента управления GridView, содержащего список выбранных продуктов поставщика

Прежде чем добавить кнопку "прекратить все продукты" к шаблону FormView, давайте сначала добавим элемент управления GridView под элементом FormView, в котором перечислены продукты, предоставляемые выбранным поставщиком. Для этого добавьте GridView на страницу, задайте для свойства `ID` значение `SuppliersProducts`и добавьте новый элемент управления ObjectDataSource с именем `SuppliersProductsDataSource`.

[![создать новый элемент управления ObjectDataSource с именем Супплиерспродуктсдатасаурце](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image18.png)

**Рис. 8**. Создание нового элемента управления ObjectDataSource с именем `SuppliersProductsDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image20.png))

Настройте этот элемент ObjectDataSource для использования метода `GetProductsBySupplierID(supplierID)` класса ProductsBLL (см. рис. 9). Хотя этот элемент GridView позволяет корректировать цену продукта, он не будет использовать встроенные функции редактирования или удаления из GridView. Поэтому в раскрывающемся списке можно задать значение (нет) для вкладок «обновление», «вставка» и «удаление».

[![настроить источник данных для использования метода Жетпродуктсбисупплиерид класса ProductsBLL (КодПоставщика)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image21.png)

**Рис. 9**. Настройка источника данных на использование метода `GetProductsBySupplierID(supplierID)` `ProductsBLL` классов ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image23.png))

Так как метод `GetProductsBySupplierID(supplierID)` принимает входной параметр, мастер ObjectDataSource предлагает нам указать источник этого значения параметра. Чтобы передать значение `SupplierID` из FormView, в раскрывающемся списке Источник параметра выберите элемент Управление, а в раскрывающемся списке ControlID — значение `Suppliers` (идентификатор элемента FormView, созданного на шаге 2).

[![указать, что параметр «КодПоставщика» должен поступать от элемента управления FormView «поставщики»](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image24.png)

**Рис. 10**. Указание того, что параметр *`supplierID`* должен поступать из `Suppliers` элемента управления FormView ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image26.png))

После завершения работы мастера ObjectDataSource элемент управления GridView будет содержать BoundField или CheckBoxField для каждого из полей данных Products. Разрежьте его так, чтобы отображались только `ProductName` и `UnitPrice` BoundFields вместе с `Discontinued` CheckBoxField; Кроме того, давайте отформатировать `UnitPrice` BoundField таким образом, чтобы его текст был отформатирован как денежная единица. Декларативная разметка GridView и `SuppliersProductsDataSource` ObjectDataSource s должна выглядеть примерно так, как показано в следующей разметке:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample3.aspx)]

На этом этапе в нашем учебном курсе отображается отчет «основной/подробности», позволяющий пользователю выбрать поставщика из FormView в верхней части экрана и просмотреть продукты, предоставленные этим поставщиком, с помощью элемента управления GridView внизу. На рис. 11 показан снимок экрана этой страницы при выборе поставщика компании Токио из FormView.

[![выбранные продукты поставщика отображаются в GridView](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image27.png)

**Рис. 11**. выбранные продукты поставщика отображаются в элементе управления GridView ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image29.png))

## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>Шаг 4. Создание методов DAL и BLL для прекращения всех продуктов для поставщика

Прежде чем можно будет добавить кнопку в FormView, которая при нажатии отменяет все продукты поставщика, сначала необходимо добавить метод в DAL и BLL, выполняющие это действие. В частности, этот метод будет называться `DiscontinueAllProductsForSupplier(supplierID)`. При нажатии кнопки FormView s Этот метод будет вызываться на уровне бизнес-логики, передавая выбранному поставщику `SupplierID`. затем BLL обращается к соответствующему методу уровня доступа к данным, который будет выдавать инструкцию `UPDATE` базе данных, которая прекращает работу указанных продуктов поставщика.

Как мы сделали в предыдущих руководствах, мы будем использовать подход снизу вверх, начиная с создания метода DAL, затем метод BLL и заканчивая реализацией функций на странице ASP.NET. Откройте `Northwind.xsd` типизированный набор данных в папке `App_Code/DAL` и добавьте новый метод в `ProductsTableAdapter` (щелкните правой кнопкой мыши `ProductsTableAdapter` и выберите команду Добавить запрос). При этом откроется мастер настройки запросов адаптера таблицы TableAdapter, который познакомит нас с процессом добавления нового метода. Начните с указания того, что наш метод DAL будет использовать специальный оператор SQL.

[![создания метода DAL с помощью специального оператора SQL](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image30.png)

**Рис. 12**. Создание метода DAL с помощью специального оператора SQL ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image32.png))

Затем мастер запрашивает тип создаваемого запроса. Так как методу `DiscontinueAllProductsForSupplier(supplierID)` потребуется обновить таблицу `Products` базы данных, задав для поля `Discontinued` значение 1 для всех продуктов, предоставленных указанным *`supplierID`* , необходимо создать запрос, обновляющий данные.

[![выбрать тип запроса обновления](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image33.png)

**Рис. 13**. Выбор типа запроса на обновление ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image35.png))

Следующий экран мастера предоставляет существующую инструкцию `UPDATE` TableAdapter, которая обновляет каждое из полей, определенных в `Products` DataTable. Замените текст запроса следующей инструкцией:

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample4.sql)]

После ввода этого запроса и нажатия кнопки "Далее" на последнем экране мастера запрашивается имя нового метода. Используйте `DiscontinueAllProductsForSupplier`. Завершите работу мастера, нажав кнопку Готово. При возврате в конструктор наборов данных вы должны увидеть новый метод в `ProductsTableAdapter` с именем `DiscontinueAllProductsForSupplier(@SupplierID)`.

[![назовите новый метод DAL Дисконтинуеаллпродуктсфорсупплиер](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image36.png)

**Рис. 14**. Именование нового метода DAL `DiscontinueAllProductsForSupplier` ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image38.png))

С помощью метода `DiscontinueAllProductsForSupplier(supplierID)`, созданного на уровне доступа к данным, наша следующая задача — создать метод `DiscontinueAllProductsForSupplier(supplierID)` на уровне бизнес-логики. Для этого откройте файл `ProductsBLL` класса и добавьте следующее:

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample5.vb)]

Этот метод просто вызывает метод `DiscontinueAllProductsForSupplier(supplierID)` в DAL, передавая предоставленное значение параметра *`supplierID`* . Если существовали бизнес-правила, которые позволили бы больше не поддерживать продукты поставщика при определенных обстоятельствах, эти правила должны быть реализованы в BLL.

> [!NOTE]
> В отличие от перегрузок `UpdateProduct` в классе `ProductsBLL`, сигнатура метода `DiscontinueAllProductsForSupplier(supplierID)` не включает атрибут `DataObjectMethodAttribute` (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`). Это исключает возможность `DiscontinueAllProductsForSupplier(supplierID)` метода из раскрывающегося списка мастера настройки источника данных на вкладке обновление. Этот атрибут опущен, так как мы будем вызывать метод `DiscontinueAllProductsForSupplier(supplierID)` непосредственно из обработчика событий на нашей странице ASP.NET.

## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>Шаг 5. Добавление кнопки "прекратить все продукты" в FormView

При завершении метода `DiscontinueAllProductsForSupplier(supplierID)` в BLL и DAL последним шагом добавить возможность прекращения всех продуктов для выбранного поставщика является добавление веб-элемента управления Button в `ItemTemplate`FormView. Добавим такую кнопку под номером телефона поставщика с текстом кнопки, прекратить все продукты и `ID` значение свойства `DiscontinueAllProductsForSupplier`. Этот веб-элемент управления этой кнопки можно добавить через конструктор, щелкнув ссылку Edit Templates (изменить шаблоны) в смарт-теге FormView (см. рис. 15) или напрямую с помощью декларативного синтаксиса.

[![добавить веб-элемент управления "прекратить все продукты" для кнопки FormView s ItemTemplate](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image39.png)

**Рис. 15**. Добавление веб-элемента управления "прекратить все продукты" в `ItemTemplate` FormView s ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image41.png))

При нажатии кнопки пользователем происходит обратная передача, и срабатывает [событие`ItemCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx) FormView. Для выполнения пользовательского кода в ответ на нажатие этой кнопки можно создать обработчик событий для этого события. Однако следует понимать, что событие `ItemCommand` срабатывает при щелчке элемента управления FormView *любой* кнопки, LinkButton или ImageButton. Это означает, что при переходе пользователя с одной страницы на другую в FormView возникает событие `ItemCommand`. то же самое, когда пользователь нажимает кнопку "создать", "Изменить" или "Удалить" в элементе FormView, поддерживающем вставку, обновление или удаление.

Поскольку `ItemCommand` срабатывает независимо от того, какая кнопка нажата, в обработчике событий требуется способ определить, была ли нажата кнопка «прекратить все продукты» или была ли другая кнопка. Для этого можно присвоить свойству `CommandName` веб-элемента управления "Button" определенное идентифицирующее значение. При нажатии кнопки это `CommandName` значение передается в обработчик событий `ItemCommand`, что позволяет нам определить, была ли нажата кнопка «прекратить все продукты». Установите для свойства `CommandName` "прекратить все продукты" значение "Дисконтинуепродуктс".

Наконец, давайте попробуем использовать диалоговое окно подтверждения на стороне клиента, чтобы убедиться, что пользователь действительно хочет прекратить работу выбранных продуктов поставщика. Как было показано в статье [Добавление подтверждения на стороне клиента при удалении](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb.md) учебника, это можно сделать с помощью нескольких сценариев JavaScript. В частности, задайте для свойства OnClientClick элемента управления "Кнопка" значение `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');`

После внесения этих изменений декларативный синтаксис FormView s должен выглядеть следующим образом:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample6.aspx)]

Затем создайте обработчик событий для события `ItemCommand` FormView. В этом обработчике событий необходимо сначала определить, была ли нажата кнопка "прекратить все продукты". Если да, необходимо создать экземпляр класса `ProductsBLL` и вызвать его метод `DiscontinueAllProductsForSupplier(supplierID)`, передав `SupplierID` выбранного FormView:

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample7.vb)]

Обратите внимание, что `SupplierID` текущего выбранного поставщика в FormView можно получить с помощью [свойства`SelectedValue`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)FormView. Свойство `SelectedValue` возвращает первое значение ключа данных для записи, отображаемой в FormView. [Свойство FormView`DataKeyNames`](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx), которое указывает поля данных, из которых извлекаются значения ключей данных, автоматически задается `SupplierID` в Visual Studio при привязке ObjectDataSource к элементу управления FormView на шаге 2.

После создания обработчика событий `ItemCommand` уделите время на тестирование страницы. Перейдите к поставщику Cooperativa de Quesos "Лас Кабрас" (он — это пятый поставщик в FormView для меня). Этот поставщик предоставляет два продукта: Queso Cabrales и Queso Manchego La Pastore, которые больше *не* поддерживаются.

Представьте, что Cooperativa де Quesos ' Лас Кабрас ' закончился в бизнесе, поэтому его продукты будут прекращены. Нажмите кнопку "прекратить все продукты". Отобразится диалоговое окно подтверждения на стороне клиента (см. рис. 16).

[![Cooperativa de Quesos Лас Кабрас предоставляет два активных продукта](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image42.png)

**Рис. 16**. Cooperativa de Quesos Лас Кабрас предоставляет два активных продукта ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image44.png))

Если нажать кнопку ОК в диалоговом окне Подтверждение на стороне клиента, отправка формы будет продолжена, что вызовет обратную передачу, в которой будет срабатывать событие `ItemCommand` FormView. Созданный обработчик событий, который затем будет выполнен, вызывает метод `DiscontinueAllProductsForSupplier(supplierID)` и прекращает работу продуктов Queso Cabrales и Queso Manchego La Pastore.

Если вы отключили состояние представления GridView s, элемент управления GridView повторно привязан к базовому хранилищу данных при каждой обратной передаче, и поэтому будет немедленно обновлен, чтобы отразить, что эти два продукта теперь недоступны (см. рис. 17). Однако если вы не отключили состояние представления в GridView, после внесения этого изменения необходимо будет вручную выполнить повторную привязку данных к GridView. Для этого просто выполните вызов метода `DataBind()` GridView s сразу же после вызова метода `DiscontinueAllProductsForSupplier(supplierID)`.

[![после нажатия кнопки "прекратить все продукты" продукты поставщика обновляются соответствующим образом](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image45.png)

**Рис. 17**. После нажатия кнопки "прекратить все продукты" продукты поставщика обновляются соответствующим образом ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image47.png))

## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-product-s-price"></a>Шаг 6. Создание перегрузки UpdateProduct на уровне бизнес-логики для корректировки цены продукта

Как и кнопка "прекратить все продукты" в FormView, чтобы добавить кнопки для увеличения и уменьшения цены на продукт в GridView, необходимо сначала добавить соответствующий уровень доступа к данным и методы уровня бизнес-логики. Поскольку у нас уже есть метод, который обновляет одну строку продукта в DAL, мы можем предоставить такую функциональность, создав новую перегрузку для метода `UpdateProduct` в BLL.

Наши предыдущие `UpdateProduct` перегрузки производят некоторые сочетания полей продукта в качестве скалярных входных значений и затем обновляют только поля для указанного продукта. Для этой перегрузки мы немного изменяем этот стандарт и передаем `ProductID` продукта и процентную долю, на которую нужно настроить `UnitPrice` (в отличие от передачи нового, скорректированного `UnitPrice`). Этот подход упростит код, который нам нужно написать в классе ASP.NET Page, поскольку нам не нужно беспокоиться о том, чтобы определить текущий продукт `UnitPrice`.

Перегрузка `UpdateProduct` для этого учебника показана ниже:

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample8.vb)]

Эта перегрузка извлекает сведения об указанном продукте через метод DAL s `GetProductByProductID(productID)`. Затем он проверяет, присвоено ли продукту `UnitPrice` `NULL` значение базы данных. Если это так, Цена остается без изменений. Однако при наличии значения `UnitPrice`, не являющегося`NULL`, метод обновляет продукт с `UnitPrice` на указанный процент (`unitPriceAdjustmentPercent`).

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>Шаг 7. Добавление кнопок увеличения и уменьшения в GridView

GridView (и DetailsView) состоят из набора полей. В дополнение к BoundFields, Чеккбоксфиелдс и полей TemplateField, ASP.NET включает в себя Буттонфиелд, который, как предполагает его название, отображается как столбец с кнопкой, LinkButton или ImageButton для каждой строки. Аналогично элементу FormView, нажатию *любой* кнопки в кнопках мыши GridView, кнопках изменить или удалить, кнопки сортировки и т. д. вызывает обратную передачу и вызывает [событие GridView`RowCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx).

Буттонфиелд имеет свойство `CommandName`, которое назначает указанное значение каждой из его кнопок `CommandName` свойства. Как и в FormView, `CommandName` значение используется обработчиком событий `RowCommand`, чтобы определить, какая кнопка была нажата.

Добавим в GridView два новых Буттонфиелдс, один — с ценой текста кнопки + 10%, а другой — с текстом Price-10%. Чтобы добавить эти Буттонфиелдс, щелкните ссылку Edit Columns (изменить столбцы) в смарт-теге GridView s, выберите тип поля Буттонфиелд из списка в левом верхнем углу и нажмите кнопку Добавить.

![Добавление двух Буттонфиелдс в GridView](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image48.png)

**Рис. 18**. Добавление двух Буттонфиелдс в GridView

Переместите два Буттонфиелдс, чтобы они отображались в качестве первых двух полей GridView. Затем задайте для свойств `Text` этих двух Буттонфиелдс значения Price + 10% и Price-10%, а свойства `CommandName` — Инкреасеприце и Декреасеприце соответственно. По умолчанию Буттонфиелд отображает свой столбец кнопок как LinkButton. Однако это можно изменить с помощью [свойства`ButtonType`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)буттонфиелд s. Пусть эти два Буттонфиелдс отображаются как обычные кнопки отправки. Поэтому присвойте свойству `ButtonType` значение `Button`. На рис. 19 показано диалоговое окно «поля» после внесения этих изменений. Ниже приведена декларативная разметка GridView s.

![Настройка свойств Text, CommandName и ButtonType Буттонфиелдс](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image49.png)

**Рис. 19**. настройка свойств `Text`, `CommandName`и `ButtonType` буттонфиелдс

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample9.aspx)]

После создания этих Буттонфиелдс на завершающем этапе создается обработчик событий для события `RowCommand` GridView s. Этот обработчик событий, если он срабатывает из-за нажатия кнопок Price + 10% или Price – 10%, необходимо определить `ProductID` для строки, нажатой кнопкой, а затем вызвать метод `ProductsBLL` Class s `UpdateProduct`, передав соответствующую коррекцию `UnitPrice` процентных значений вместе с `ProductID`. Следующий код выполняет следующие задачи:

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample10.vb)]

Чтобы определить `ProductID` для строки, для которой была нажата кнопка Цена + 10% или Price-10%, необходимо обратиться к коллекции GridView s `DataKeys`. Эта коллекция содержит значения полей, указанных в свойстве `DataKeyNames` для каждой строки GridView. Так как при привязке ObjectDataSource к GridView в Visual Studio свойству `DataKeyNames` GridView s присвоено значение ProductID, `DataKeys(rowIndex).Value` предоставляет `ProductID` для указанного значения *rowIndex*.

Буттонфиелд автоматически передает значение *rowIndex* строки, нажатой с помощью параметра `e.CommandArgument`. Таким образом, чтобы определить `ProductID` для строки, для которой была нажата кнопка Цена + 10% или Price-10%, мы используем: `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`.

Как и при нажатии кнопки "прекратить все продукты", если состояние представления GridView s отключено, элемент управления GridView повторно привязан к базовому хранилищу данных при каждой обратной передаче и, следовательно, будет обновлен, чтобы отразить изменение цены, которое происходит после нажатия кнопки Любая из кнопок. Однако если вы не отключили состояние представления в GridView, после внесения этого изменения необходимо будет вручную выполнить повторную привязку данных к GridView. Для этого просто выполните вызов метода `DataBind()` GridView s сразу же после вызова метода `UpdateProduct`.

На рис. 20 показана страница при просмотре продуктов, предоставляемых Хоместеад Келли бабушка. На рис. 21 показаны результаты после нажатия кнопки Цена + 10% для разворота бабушка Бойсенберри и кнопки Price-10% один раз для Норсвудс Кранберри.

[![GridView включает кнопки Цена + 10% и Price-10%](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image50.png)

**Рис. 20**. элемент GridView включает кнопки Price + 10% и Price-10% ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image52.png))

[![цены на первый и третий продукты были обновлены с помощью кнопок Цена + 10% и цена-10%.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image53.png)

**Рис. 21**. цены на первый и третий продукты были обновлены с помощью кнопок Цена + 10% и цена-10% ([щелкните, чтобы просмотреть изображение с полным размером](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image55.png)).

> [!NOTE]
> GridView (и DetailsView) также может содержать кнопки, LinkButton или Имажебуттонс, добавленные в их полей TemplateField. Как и в случае с BoundField, эти кнопки при нажатии будут вызывать обратную передачу, позывая событие `RowCommand` GridView s. Однако при добавлении кнопок в TemplateField кнопка s `CommandArgument` не задается автоматически индексом строки, как при использовании Буттонфиелдс. Если необходимо определить индекс строки кнопки, которая была нажата в обработчике событий `RowCommand`, необходимо вручную задать свойство Button `CommandArgument` в его декларативном синтаксисе в TemplateField, используя следующий код:  
> `<asp:Button runat="server" ... CommandArgument='<%# CType(Container, GridViewRow).RowIndex %>' />`.

## <a name="summary"></a>Сводка

Элементы управления GridView, DetailsView и FormView могут включать кнопки, LinkButton или Имажебуттонс. Такие кнопки, при щелчке, вызывают обратную передачу и вызывают событие `ItemCommand` в элементах управления FormView и DetailsView и событие `RowCommand` в GridView. Эти веб-элементы управления данными имеют встроенные функции для обработки общих действий, связанных с командами, таких как удаление или изменение записей. Однако можно также использовать кнопки, которые при щелчке мыши реагируют на исполнение собственного кода.

Для этого необходимо создать обработчик событий для события `ItemCommand` или `RowCommand`. В этом обработчике событий сначала проверяется значение входящего `CommandName`, чтобы определить, какая кнопка была нажата, а затем выполнить соответствующее настраиваемое действие. В этом учебнике мы увидели, как использовать кнопки и Буттонфиелдс для прекращения использования всех продуктов для указанного поставщика или увеличения или уменьшения цены на определенный продукт на 10%.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Назад](adding-and-responding-to-buttons-to-a-gridview-cs.md)
