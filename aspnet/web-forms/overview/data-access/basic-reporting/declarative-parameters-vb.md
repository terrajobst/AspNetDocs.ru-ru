---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
title: Декларативные параметры (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы продемонстрируем, как использовать набор параметров в жестко запрограммированное значение для выбора данных, отображаемых в элементе управления DetailsView.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: dc1234a3-114f-4c9a-8d25-50ca03cc8e8e
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
msc.type: authoredcontent
ms.openlocfilehash: cdc42752fc78d18366af037a81fe4ebe5a1646ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74612901"
---
# <a name="declarative-parameters-vb"></a>Декларативные параметры (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_5_VB.exe) или [Загрузка PDF-файла](declarative-parameters-vb/_static/datatutorial05vb1.pdf)

> В этом учебнике мы продемонстрируем, как использовать набор параметров в жестко запрограммированное значение для выбора данных, отображаемых в элементе управления DetailsView.

## <a name="introduction"></a>Введение

В [последнем учебном курсе](displaying-data-with-the-objectdatasource-vb.md) мы рассматривали отображение данных с элементами управления GridView, DetailsView и FormView, привязанными к элементу управления ObjectDataSource, вызвавшему метод `GetProducts()` из класса `ProductsBLL`. Метод `GetProducts()` возвращает строго типизированный объект DataTable, заполненный всеми записями из таблицы `Products` базы данных Northwind. Класс `ProductsBLL` содержит дополнительные методы для возврата только подмножества продуктов — `GetProductByProductID(productID)`, `GetProductsByCategoryID(categoryID)`и `GetProductsBySupplierID(supplierID)`. Эти три метода предполагают входной параметр, указывающий, как отфильтровать возвращенные сведения о продукте.

ObjectDataSource можно использовать для вызова методов, которые предполагают входные параметры, но для этого необходимо указать, откуда берутся значения этих параметров. Значения параметров могут быть жестко запрограммированы или могут поступать из различных динамических источников, включая значения QueryString, переменные сеанса, значение свойства веб-элемента управления на странице или другие.

В этом руководстве начнем с демонстрации того, как использовать набор параметров для жестко запрограммированного значения. В частности, мы рассмотрим добавление элемента DetailsView на страницу, на котором отображаются сведения о конкретном продукте, а именно Chef Anton's Gumbo, который имеет `ProductID` 5. Далее мы посмотрим, как задать значение параметра на основе веб-элемента управления. В частности, мы будем использовать текстовое поле для ввода пользователя в страну, после чего она может нажать кнопку, чтобы просмотреть список поставщиков, находящихся в этой стране.

## <a name="using-a-hard-coded-parameter-value"></a>Использование жестко запрограммированного значения параметра

Для первого примера Начните с добавления элемента управления DetailsView на страницу `DeclarativeParams.aspx` в папке `BasicReporting`. Из смарт-тега DetailsView выберите &lt;создать источник данных&gt; из раскрывающегося списка и выберите Добавление элемента управления ObjectDataSource.

[![добавить элемент управления ObjectDataSource на страницу](declarative-parameters-vb/_static/image2.png)](declarative-parameters-vb/_static/image1.png)

**Рис. 1**. Добавление элемента управления ObjectDataSource на страницу ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image3.png))

Будет автоматически запущен мастер выбора источника данных элемента управления ObjectDataSource. Выберите класс `ProductsBLL` на первом экране мастера.

[![выберите класс ProductsBLL](declarative-parameters-vb/_static/image5.png)](declarative-parameters-vb/_static/image4.png)

**Рис. 2**. выбор класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image6.png))

Так как нам нужно отобразить сведения о конкретном продукте, мы хотим использовать метод `GetProductByProductID(productID)`.

[![выбрать метод Жетпродуктбипродуктид (productID)](declarative-parameters-vb/_static/image8.png)](declarative-parameters-vb/_static/image7.png)

**Рис. 3**. выбор метода `GetProductByProductID(productID)` ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image9.png))

Так как выбранный метод включает параметр, в мастере есть еще один экран, где вам будет предложено определить значение, которое будет использоваться для параметра. В списке слева отображаются все параметры для выбранного метода. Для `GetProductByProductID(productID)` существует только один `productID`. Справа можно указать значение для выбранного параметра. Раскрывающийся список Источник параметра перечисляет различные возможные источники для значения параметра. Так как нам нужно указать жестко заданное значение 5 для параметра `productID`, оставьте Источник параметра как нет и введите 5 в текстовое поле DefaultValue.

[![жестко запрограммированное значение параметра, равное 5, будет использоваться для параметра productID.](declarative-parameters-vb/_static/image11.png)](declarative-parameters-vb/_static/image10.png)

**Рис. 4**. жестко запрограммированное значение параметра, равное 5, будет использоваться для параметра `productID` ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image12.png))

После завершения работы мастера настройки источника данных декларативная разметка элемента управления ObjectDataSource включает объект `Parameter` в коллекцию `SelectParameters` для каждого входного параметра, ожидаемого методом, определенным в свойстве `SelectMethod`. Так как метод, который мы используем в этом примере, принимает только один входной параметр, `parameterID`, здесь есть только одна запись. Коллекция `SelectParameters` может содержать любой класс, производный от класса `Parameter` в пространстве имен `System.Web.UI.WebControls`. Для жестко запрограммированных значений параметров используется базовый класс `Parameter`, но для других параметров источника параметра используется производный `Parameter` класс. При необходимости можно также создать собственные [пользовательские типы параметров](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11).

[!code-aspx[Main](declarative-parameters-vb/samples/sample1.aspx)]

> [!NOTE]
> Если вы используете собственный компьютер, декларативная разметка, отображаемая на этом этапе, может включать значения свойств `InsertMethod`, `UpdateMethod`и `DeleteMethod`, а также `DeleteParameters`. Мастер выбора источника данных ObjectDataSource автоматически задает методы из `ProductBLL`, которые будут использоваться для вставки, обновления и удаления, поэтому, если вы явно не сняли их, они будут добавлены в разметку выше.

При посещении этой страницы веб-элемент управления данными будет вызывать метод `Select` ObjectDataSource, который будет вызывать метод `GetProductByProductID(productID)` класса `ProductsBLL`, используя жестко заданное значение 5 для входного параметра `productID`. Метод возвратит строго типизированный `ProductDataTable` объект, содержащий одну строку со сведениями о Gumbo Anton's Chef (продукт с `ProductID` 5).

[![сведения о наборе Gumbo Anton's Chef](declarative-parameters-vb/_static/image14.png)](declarative-parameters-vb/_static/image13.png)

**Рис. 5**. отображаются сведения о наборе Gumbo Chef Anton's ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image15.png))

## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>Присвоение параметру значения свойства веб-элемента управления

Значения параметров ObjectDataSource также могут быть заданы на основе значения веб-элемента управления на странице. Чтобы проиллюстрировать это, рассмотрим элемент управления GridView, в котором перечислены все поставщики, расположенные в стране, указанной пользователем. Чтобы сделать это, добавьте на страницу текстовое поле, в которое пользователь может ввести название страны. Присвойте свойству `ID` этого элемента управления TextBox значение `CountryName`. Также добавьте веб-элемент управления Button.

[![добавить текстовое поле на страницу с ИДЕНТИФИКАТОРом CountryName](declarative-parameters-vb/_static/image17.png)](declarative-parameters-vb/_static/image16.png)

**Рис. 6**. Добавление на страницу текстового поля с `ID` `CountryName` ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image18.png))

Затем добавьте элемент управления GridView на страницу и в смарт-теге выберите Добавление нового элемента ObjectDataSource. Так как мы хотим отобразить сведения о поставщиках, выберите класс `SuppliersBLL` на первом экране мастера. На втором экране выберите метод `GetSuppliersByCountry(country)`.

[![выбрать метод Жетсупплиерсбикаунтри (Country)](declarative-parameters-vb/_static/image20.png)](declarative-parameters-vb/_static/image19.png)

**Рис. 7**. выбор метода `GetSuppliersByCountry(country)` ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image21.png))

Так как метод `GetSuppliersByCountry(country)` имеет входной параметр, мастер снова включает в себя окончательный экран для выбора значения параметра. На этот раз задайте источнику параметров значение Control. При этом раскрывающийся список ControlID будет заполнен именами элементов управления на странице. Выберите элемент управления `CountryName` из списка. При первом посещении страницы текстовое поле `CountryName` будет пустым, поэтому результаты не будут возвращены и ничего не отобразится. Если требуется отобразить некоторые результаты по умолчанию, задайте соответствующее текстовое поле DefaultValue.

[![присвоить параметру значение элемента управления CountryName](declarative-parameters-vb/_static/image23.png)](declarative-parameters-vb/_static/image22.png)

**Рис. 8**. Присвоение параметру значения элемента управления `CountryName` ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image24.png))

Декларативная разметка ObjectDataSource немного отличается от нашего первого примера с использованием [ControlParameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx) вместо стандартного объекта `Parameter`. У `ControlParameter` есть дополнительные свойства, позволяющие указать `ID` веб-элемента управления и значение свойства, которое будет использоваться для параметра (`PropertyName`). Мастер настройки источника данных был достаточно интеллектуальным, чтобы определить, что для текстового поля, скорее всего, потребуется использовать свойство `Text` для значения параметра. Однако если вы хотите использовать другое значение свойства из веб-элемента управления, можно изменить значение `PropertyName` здесь или щелкнув ссылку "Показывать дополнительные свойства" в мастере.

[!code-aspx[Main](declarative-parameters-vb/samples/sample2.aspx)]

При первом посещении страницы в первый раз `CountryName` TextBox пуст. Метод `Select` ObjectDataSource по-прежнему вызывается GridView, но значение `Nothing` передается в метод `GetSuppliersByCountry(country)`. TableAdapter преобразует `Nothing` в базу данных `NULL` значение (`DBNull.Value`), но запрос, используемый методом `GetSuppliersByCountry(country)`, записывается таким способом, что он не возвращает никаких значений, если для параметра `NULL` указано значение `@CategoryID`. Вкратце, поставщики не возвращаются.

Однако после того, как посетитель введет в страну и нажимает кнопку «Показывать поставщиков», чтобы вызвать обратную передачу, повторно запрашивается метод `Select` ObjectDataSource, передающий значение `Text` элемента управления TextBox в качестве параметра `country`.

[Отображаются ![поставщиков из Канады](declarative-parameters-vb/_static/image26.png)](declarative-parameters-vb/_static/image25.png)

**Рис. 9**. показаны поставщики из Канады ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image27.png))

## <a name="showing-all-suppliers-by-default"></a>Отображение всех поставщиков по умолчанию

Вместо того чтобы показывать ни одного из поставщиков при первом просмотре страницы, может потребоваться сначала отобразить *всех* поставщиков, чтобы пользователь мог немного очистить вниз по списку, введя название страны в текстовом поле. Если текстовое поле пусто, метод `GetSuppliersByCountry(country)` `SuppliersBLL` класса передается в `Nothing` для его входного параметра *`country`* . Это `Nothing` значение затем передается в метод `GetSupplierByCountry(country)` DAL, где он преобразуется в базу данных `NULL` значение параметра `@Country` в следующем запросе:

[!code-sql[Main](declarative-parameters-vb/samples/sample3.sql)]

Выражение `Country = NULL` всегда возвращает значение false, даже для записей, у которых `Country` столбец имеет `NULL` значение. Поэтому записи не возвращаются.

Чтобы получить *список всех* поставщиков, если текстовое поле Country (страна) пустое, можно дополнить метод `GetSuppliersByCountry(country)` в BLL, чтобы вызвать метод `GetSuppliers()`, если параметр Country имеет значение `Nothing` и вызывать метод `GetSuppliersByCountry(country)` DAL в противном случае. Это приведет к возврату всех поставщиков, если не указана страна и соответствующее подмножество поставщиков при включении параметра Country.

Измените метод `GetSuppliersByCountry(country)` в классе `SuppliersBLL` на следующий:

[!code-vb[Main](declarative-parameters-vb/samples/sample4.vb)]

После этого изменения `DeclarativeParams.aspx` страница отображает всех поставщиков при первом посещении (или при пустом текстовом поле `CountryName`).

[![все поставщики теперь отображаются по умолчанию](declarative-parameters-vb/_static/image29.png)](declarative-parameters-vb/_static/image28.png)

**Рис. 10**. все поставщики теперь отображаются по умолчанию ([щелкните, чтобы просмотреть изображение с полным размером](declarative-parameters-vb/_static/image30.png))

## <a name="summary"></a>Сводка

Чтобы использовать методы с входными параметрами, необходимо указать значения для параметров в коллекции `SelectParameters` ObjectDataSource. Различные типы параметров позволяют получить значение параметра из различных источников. Тип параметра по умолчанию использует жестко заданное значение, но так же просто (и без строки кода) значения параметров можно получить из строки запроса, переменных сеанса, файлов cookie и даже введенных пользователем значений из веб-элементов управления на странице.

В примерах, рассмотренных в этом учебнике, показано, как использовать значения декларативных параметров. Однако могут возникнуть ситуации, когда нам нужно использовать недоступный источник параметра, например текущую дату и время, или, если наш сайт использовал членство, идентификатор пользователя посетителя. Для таких сценариев мы можем задать значения параметров программным способом до того, как ObjectDataSource вызовет метод базового объекта. Мы посмотрим, как это сделать в [следующем руководстве](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md).

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Хилтон Гизнау. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](displaying-data-with-the-objectdatasource-vb.md)
> [Вперед](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)
