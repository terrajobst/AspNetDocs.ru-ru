---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
title: Пользовательское форматирование на основе данных (VB) | Документация Майкрософт
author: rick-anderson
description: Настройка формата элементов управления GridView, DetailsView или FormView в зависимости от привязанных к ним данных может быть выполнена несколькими способами. В этом учебнике мы будем l...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: df5a1525-386f-4632-972c-57b199870bc3
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 268dc763ef6954903f721a3015daaf10bf9bccb1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74613062"
---
# <a name="custom-formatting-based-upon-data-vb"></a>Пользовательское форматирование на основе данных (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe) или [Загрузка PDF-файла](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)

> Настройка формата элементов управления GridView, DetailsView или FormView в зависимости от привязанных к ним данных может быть выполнена несколькими способами. В этом учебнике мы рассмотрим, как выполнять форматирование с привязкой данных с помощью обработчиков событий DataBound и RowDataBound.

## <a name="introduction"></a>Введение

Внешний вид элементов управления GridView, DetailsView и FormView можно настроить с помощью множества свойств, связанных со стилем. Кроме прочего, такие свойства, как `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`и `Height`, определяют общий внешний вид элемента управления, готового для просмотра. Свойства, включая `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`и другие, позволяют применять эти же параметры стиля к определенным разделам. Аналогичным образом эти параметры стиля можно применить на уровне полей.

Во многих случаях требования к форматированию зависят от значения отображаемых данных. Например, чтобы привлечь внимание к небольшим запасным продуктам, отчет, перечисляющий сведения о продукте, может установить желтый цвет фона для тех продуктов, чьи `UnitsInStock` и `UnitsOnOrder` поля равны 0. Чтобы выделить более ресурсоемкие продукты, нам может потребоваться отобразить цены на эти продукты более $75,00 полужирным шрифтом.

Настройка формата элементов управления GridView, DetailsView или FormView в зависимости от привязанных к ним данных может быть выполнена несколькими способами. В этом учебнике мы рассмотрим, как выполнять форматирование с привязкой к данным с помощью обработчиков событий `DataBound` и `RowDataBound`. В следующем учебном курсе мы рассмотрим альтернативный подход.

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>Использование обработчика событий`DataBound`элемента управления DetailsView

Если данные привязаны к элементу DetailsView из элемента управления источника данных или путем программного назначения данных свойству `DataSource` элемента управления и вызова метода `DataBind()`, выполняются следующие действия.

1. Срабатывает событие `DataBinding` веб-элемента управления данными.
2. Данные привязаны к веб-элементу управления данными.
3. Срабатывает событие `DataBound` веб-элемента управления данными.

Пользовательскую логику можно внедрить сразу после шагов 1 и 3 с помощью обработчика событий. Создав обработчик событий для `DataBound` события, можно программно определить данные, привязанные к веб-элементу управления данными, и настроить форматирование по мере необходимости. Чтобы проиллюстрировать это, создадим элемент DetailsView, который будет выводить общие сведения о продукте, но будет отображать `UnitPrice` значение ***полужирным шрифтом курсивом,*** если оно превышает $75,00.

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>Шаг 1. Отображение сведений о продукте в элементе DetailsView

Откройте страницу `CustomColors.aspx` в папке `CustomFormatting`, перетащите элемент управления DetailsView с панели инструментов в конструктор, задайте для его свойства `ID` значение `ExpensiveProductsPriceInBoldItalic`и привяжите его к новому элементу управления ObjectDataSource, который вызывает метод `ProductsBLL` класса `GetProducts()`. Подробные инструкции по выполнению этой задачи приведены здесь, так как мы подробно рассмотрели их в предыдущих руководствах.

После привязки элемента управления ObjectDataSource к элементу DetailsView извлеките список полей. Я выбрал удаление `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`и `Discontinued` BoundFields, а также переименование и повторное форматирование оставшихся BoundFields. Я также очистил параметры `Width` и `Height`. Так как DetailsView отображает только одну запись, необходимо включить разбиение на страницы, чтобы позволить конечному пользователю просматривать все продукты. Для этого установите флажок Включить разбиение по страницам в смарт-теге DetailsView.

[![рис. 1. Установите флажок Включить разбиение по страницам в смарт-теге DetailsView.](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)

**Рис. 1**. рисунок 1. Установите флажок Включить разбиение по страницам в смарт-теге DetailsView ([щелкните, чтобы просмотреть изображение с полным размером](custom-formatting-based-upon-data-vb/_static/image3.png)).

После этих изменений разметка DetailsView будет выглядеть следующим образом:

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample1.aspx)]

Уделите время для проверки этой страницы в браузере.

[![элемент управления DetailsView отображает по одному продукту за раз](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)

**Рис. 2**. элемент управления DetailsView отображает по одному продукту за раз ([щелкните, чтобы просмотреть изображение с полным размером](custom-formatting-based-upon-data-vb/_static/image6.png))

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>Шаг 2. Программное определение значения данных в обработчике событий DataBound

Чтобы отобразить цену с полужирным шрифтом, курсивом для тех продуктов, значение которых `UnitPrice` превышает $75,00, необходимо сначала получить возможность программно определить `UnitPrice` значение. Для элемента DetailsView это можно сделать в обработчике событий `DataBound`. Чтобы создать обработчик событий, щелкните элемент DetailsView в конструкторе, а затем перейдите к окно свойств. Нажмите клавишу F4, чтобы отобразить ее, если она не видна, или перейдите в меню Вид и выберите пункт меню окно "Свойства". В окно свойств щелкните значок с молнией, чтобы получить список событий DetailsView. Затем дважды щелкните событие `DataBound` или введите имя создаваемого обработчика событий.

![Создание обработчика событий для события DataBound](custom-formatting-based-upon-data-vb/_static/image7.png)

**Рис. 3**. Создание обработчика событий для `DataBound` события

> [!NOTE]
> Вы также можете создать обработчик событий из части кода страницы ASP.NET. В верхней части страницы вы найдете два раскрывающихся списка. Выберите объект из левого раскрывающегося списка и событие, для которого нужно создать обработчик, из раскрывающегося списка справа, и Visual Studio автоматически создаст соответствующий обработчик событий.

Это позволит автоматически создать обработчик событий и перейти к части кода, в которой он был добавлен. На этом этапе вы увидите:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample2.vb)]

Доступ к данным, привязанным к элементу DetailsView, можно получить с помощью свойства `DataItem`. Вспомним, что мы привязывая наши элементы управления к строго типизированной таблице данных DataTable, которая состоит из коллекции строго типизированных экземпляров DataRow. Когда объект DataTable привязан к элементу DetailsView, первый объект DataRow в объекте DataTable назначается свойству `DataItem` DetailsView. В частности, свойству `DataItem` присваивается объект `DataRowView`. Можно использовать свойство `Row` `DataRowView`, чтобы получить доступ к базовому объекту DataRow, который фактически является экземпляром `ProductsRow`. Когда у нас есть этот `ProductsRow` экземпляр, мы можем принять решение, просто проверив значения свойств объекта.

В следующем коде показано, как определить, имеет ли значение `UnitPrice`, привязанное к элементу управления DetailsView, больше $75,00:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample3.vb)]

> [!NOTE]
> Поскольку `UnitPrice` может иметь `NULL` значение в базе данных, сначала убедитесь, что мы не работаем с `NULL` значением, прежде чем обращаться к свойству `UnitPrice` `ProductsRow`. Эта проверка важна, поскольку при попытке получить доступ к свойству `UnitPrice` при наличии `NULL` значения объект `ProductsRow` выдаст [исключение StrongTypingException](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).

## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>Шаг 3. Форматирование значения UnitPrice в элементе DetailsView

На этом этапе можно определить, имеет ли значение `UnitPrice`, привязанное к элементу DetailsView, значение, превышающее $75,00, но мы еще не видели, как программно настроить форматирование DetailsView соответственно. Чтобы изменить форматирование целой строки в элементе DetailsView, программным способом получить доступ к строке с помощью `DetailsViewID.Rows(index)`; чтобы изменить конкретную ячейку, используйте `DetailsViewID.Rows(index).Cells(index)`. После получения ссылки на строку или ячейку можно изменить ее внешний вид, задав свойства, связанные со стилем.

Для программного доступа к строке необходимо, чтобы вы знали индекс строки, который начинается с 0. `UnitPrice` строка представляет собой пятую строку в элементе DetailsView, которая предоставляет ей индекс 4 и делает его программно доступным с помощью `ExpensiveProductsPriceInBoldItalic.Rows(4)`. На этом этапе содержимое строки целиком можно отобразить полужирным шрифтом курсивом, используя следующий код:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample4.vb)]

Тем не менее, это *сделает метку* (Price) и значение полужирным и курсивом. Если нужно сделать только значение полужирным и курсивом, необходимо применить это форматирование ко второй ячейке в строке, что можно сделать с помощью следующего:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample5.vb)]

Так как в наших руководствах использовались таблицы стилей для аккуратного разделения отображаемой разметки и сведений, относящихся к стилю, вместо задания свойств конкретного стиля, как показано выше, вместо этого следует использовать класс CSS. Откройте таблицу стилей `Styles.css` и добавьте новый класс CSS с именем `ExpensivePriceEmphasis` со следующим определением:

[!code-css[Main](custom-formatting-based-upon-data-vb/samples/sample6.css)]

Затем в обработчике событий `DataBound` задайте для свойства `CssClass` ячейки значение `ExpensivePriceEmphasis`. В следующем коде показан полностью `DataBound` обработчик событий:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample7.vb)]

При просмотре продукта Chai, стоимость которого меньше $75,00, Цена отображается обычным шрифтом (см. рис. 4). Однако при просмотре посетитель Кобе Нику с ценой $97,00 Цена выводится полужирным шрифтом курсивом (см. рис. 5).

[![цены меньше $75,00 отображаются обычным шрифтом.](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)

**Рис. 4**. цены меньше $75,00 отображаются обычным шрифтом ([щелкните, чтобы просмотреть изображение с полным размером](custom-formatting-based-upon-data-vb/_static/image10.png))

[Цены на ![дорогостоящих продуктов отображаются полужирным шрифтом курсивом](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)

**Рис. 5**. цены на дорогостоящие продукты отображаются полужирным шрифтом курсивом ([щелкните, чтобы просмотреть изображение с полным размером](custom-formatting-based-upon-data-vb/_static/image13.png))

## <a name="using-the-formview-controlsdataboundevent-handler"></a>Использование обработчика событий`DataBound`элемента управления FormView

Шаги по определению базовых данных, привязанных к элементу FormView, идентичны тем, что относятся к элементу управления DetailsView создание `DataBound` обработчика событий, приведение `DataItem` свойства к соответствующему типу объекта, привязанному к нему, и определение способа продолжения. Однако FormView и DetailsView различаются при обновлении внешнего вида пользовательского интерфейса.

Элемент FormView не содержит никаких BoundFields, поэтому коллекция `Rows` отсутствует. Вместо этого FormView состоит из шаблонов, которые могут содержать сочетание статического кода HTML, веб-элементов управления и синтаксиса привязки данных. Настройка стиля FormView обычно включает в себя настройку стиля одного или нескольких веб-элементов управления в шаблонах FormView.

Чтобы проиллюстрировать это, давайте будем использовать элемент FormView для перечисления продуктов, как в предыдущем примере, но на этот раз выводится только название продукта и единицы склада с единицами склада в виде красного шрифта, если он меньше или равен 10.

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>Шаг 4. Отображение сведений о продукте в элементе FormView

Добавьте элемент FormView на страницу `CustomColors.aspx` под элементом DetailsView и задайте для свойства `ID` значение `LowStockedProductsInRed`. Привяжите FormView к элементу управления ObjectDataSource, созданному на предыдущем шаге. Это приведет к созданию `ItemTemplate`, `EditItemTemplate`и `InsertItemTemplate` для FormView. Удалите `EditItemTemplate` и `InsertItemTemplate` и упростите `ItemTemplate`, чтобы включить только значения `ProductName` и `UnitsInStock`, каждый из которых имеет свои собственные элементы управления Label с соответствующими именами. Как и в элементе DetailsView из предыдущего примера, также установите флажок Включить разбиение по страницам в смарт-теге FormView.

После этих изменений разметка FormView должна выглядеть следующим образом:

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample8.aspx)]

Обратите внимание, что `ItemTemplate` содержит:

- **Статический HTML** — текст "Product:" и "Units in бирж:" вместе с элементами `<br />` и `<b>`.
- **Веб-элементы управления** имеют два элемента управления Label: `ProductNameLabel` и `UnitsInStockLabel`.
- **Синтаксис привязки данных** синтаксис `<%# Bind("ProductName") %>` и `<%# Bind("UnitsInStock") %>`, который присваивает значения из этих полей свойствам элемента управления Label "`Text`".

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>Шаг 5. Программное определение значения данных в обработчике событий с привязкой к данным

После завершения разметки FormView, следующим шагом является программное определение того, является ли значение `UnitsInStock` меньше или равным 10. Это выполняется точно так же, как и FormView, как и в DetailsView. Начните с создания обработчика событий для события `DataBound` FormView.

![Создание обработчика событий DataBound](custom-formatting-based-upon-data-vb/_static/image14.png)

**Рис. 6**. Создание обработчика событий `DataBound`

В обработчике событий приведите свойство `DataItem` FormView к экземпляру `ProductsRow` и определите, является ли значение `UnitsInPrice` таким, что нужно отобразить его красным шрифтом.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample9.vb)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>Шаг 6. Форматирование элемента управления метки Унитсинстокклабел в ItemTemplate объекта FormView

Последний шаг — форматирование отображаемого `UnitsInStock`ного значения красным шрифтом, если значение равно 10 или меньше. Для этого необходимо программно получить доступ к элементу управления `UnitsInStockLabel` в `ItemTemplate` и задать его свойства стиля, чтобы текст отображался красным цветом. Чтобы получить доступ к веб-элементу управления в шаблоне, используйте метод `FindControl("controlID")` следующим образом:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample10.vb)]

Для нашего примера мы хотим получить доступ к элементу управления Label, значение `ID` которого равно `UnitsInStockLabel`, поэтому мы будем использовать:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample11.vb)]

После получения программной ссылки на веб-элемент управления можно изменить его свойства, связанные со стилем, по мере необходимости. Как и в предыдущем примере, я создал класс CSS в `Styles.css` с именем `LowUnitsInStockEmphasis`. Чтобы применить этот стиль к веб-элементу управления Label, задайте соответствующее свойство `CssClass`.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample12.vb)]

> [!NOTE]
> Синтаксис форматирования шаблона программным образом обращается к веб-элементу управления с помощью `FindControl("controlID")`, а затем при использовании [полей TemplateField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) в элементах управления DetailsView или GridView также можно использовать свойства, связанные со стилем. В следующем руководстве мы рассмотрим полей TemplateField.

На рисунках 7 отображается элемент FormView при просмотре продукта, значение `UnitsInStock` которого больше 10, а в продукте на рис. 8 — значение меньше 10.

[![для продуктов с достаточно большим количеством единиц в запасах, пользовательское форматирование не применяется.](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)

**Рис. 7**. для продуктов с достаточно большим количеством единиц на бумаге не применяется настраиваемое форматирование ([щелкните, чтобы просмотреть изображение с полным размером](custom-formatting-based-upon-data-vb/_static/image17.png))

[![единицы складского номера отображаются красным цветом для продуктов со значениями 10 или меньше](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)

**Рис. 8**. единицы складского номера показаны красным цветом для продуктов со значениями 10 или меньше ([щелкните, чтобы просмотреть изображение с полным размером](custom-formatting-based-upon-data-vb/_static/image20.png))

## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>Форматирование с помощью события`RowDataBound`GridView

Ранее мы рассматривали последовательность шагов, выполняемых элементами управления DetailsView и FormView во время привязки данных. Давайте вернемся к этим шагам снова в качестве обновления.

1. Срабатывает событие `DataBinding` веб-элемента управления данными.
2. Данные привязаны к веб-элементу управления данными.
3. Срабатывает событие `DataBound` веб-элемента управления данными.

Эти три простых шага достаточно для элемента DetailsView и FormView, так как они отображают только одну запись. Для GridView, в котором отображаются *все* записи, привязанные к нему (а не только первый), шаг 2 немного сложнее.

На шаге 2 GridView перечисляет источник данных, а для каждой записи создает экземпляр `GridViewRow` и привязывает к нему текущую запись. Для каждого `GridViewRow`, добавляемого в GridView, вызываются два события:

- **`RowCreated`** срабатывает после создания `GridViewRow`
- **`RowDataBound`** срабатывает после привязки текущей записи к `GridViewRow`.

Для GridView привязка данных более точно описывается следующей последовательностью действий:

1. Вызывается событие `DataBinding` GridView.
2. Данные привязаны к GridView.   
  
   Для каждой записи в источнике данных 

    1. Создание объекта `GridViewRow`
    2. Запустить событие `RowCreated`
    3. Привязка записи к `GridViewRow`
    4. Запустить событие `RowDataBound`
    5. Добавление `GridViewRow` в коллекцию `Rows`
3. Вызывается событие `DataBound` GridView.

Чтобы настроить формат отдельных записей GridView, необходимо создать обработчик событий для события `RowDataBound`. Чтобы проиллюстрировать это, давайте добавим GridView на страницу `CustomColors.aspx`, в которой отображается имя, Категория и цена для каждого продукта, в котором выделены продукты, цена которых меньше $10,00 с желтым цветом фона.

## <a name="step-7-displaying-product-information-in-a-gridview"></a>Шаг 7. Отображение сведений о продукте в элементе управления GridView

Добавьте элемент управления GridView под элементом FormView из предыдущего примера и задайте для его свойства `ID` значение `HighlightCheapProducts`. Так как у нас уже есть элемент управления ObjectDataSource, который возвращает все продукты на странице, привяжите к нему GridView. Наконец, измените BoundFields GridView, чтобы включить только названия продуктов, категории и цены. После этих изменений разметка GridView должна выглядеть следующим образом:

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample13.aspx)]

На рис. 9 показан ход выполнения этой точки при просмотре в браузере.

[![GridView содержит имя, категорию и цену для каждого продукта.](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)

**Рис. 9**. Отображение имени, категории и цены каждого продукта в элементе управления GridView ([щелкните, чтобы просмотреть изображение с полным размером](custom-formatting-based-upon-data-vb/_static/image23.png))

## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>Шаг 8. Программное определение значения данных в обработчике событий RowDataBound

Если `ProductsDataTable` привязан к GridView, его `ProductsRow` экземпляры перечисляются и для каждого `ProductsRow` создается `GridViewRow`. Свойству `DataItem` `GridViewRow`присваивается определенный `ProductRow`, после чего вызывается обработчик событий `RowDataBound` GridView. Чтобы определить `UnitPrice` значение для каждого продукта, привязанного к GridView, необходимо создать обработчик событий для события `RowDataBound` GridView. В этом обработчике событий можно проверить значение `UnitPrice` для текущего `GridViewRow` и принять решение о форматировании для этой строки.

Этот обработчик событий можно создать с помощью той же серии шагов, что и в элементе FormView и DetailsView.

![Создание обработчика событий для события RowDataBound GridView](custom-formatting-based-upon-data-vb/_static/image24.png)

**Рис. 10**. Создание обработчика событий для `RowDataBound` события GridView

Создание обработчика событий таким образом приведет к автоматическому добавлению следующего кода в часть кода страницы ASP.NET:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample14.vb)]

При срабатывании события `RowDataBound` обработчик событий передается в качестве второго параметра объектом типа `GridViewRowEventArgs`, у которого есть свойство с именем `Row`. Это свойство возвращает ссылку на `GridViewRow`, которая была только что привязана к данным. Для доступа к экземпляру `ProductsRow`, привязанному к `GridViewRow` мы используем свойство `DataItem` следующим образом:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample15.vb)]

При работе с обработчиком событий `RowDataBound` важно помнить, что GridView состоит из различных типов строк и что это событие срабатывает для *всех* типов строк. Тип `GridViewRow`может быть определен свойством `RowType` и может иметь одно из возможных значений:

- `DataRow` строки, привязанной к записи из `DataSource` GridView
- `EmptyDataRow` строку, отображаемую, если `DataSource` GridView пуста
- `Footer` строку нижнего колонтитула; отображается, если свойство `ShowFooter` GridView имеет значение `True`
- `Header` строку заголовка; отображается, если свойство Шовхеадер элемента GridView имеет значение `True` (по умолчанию)
- `Pager` для элемента GridView, который реализует разбиение на страницы, строка, отображающая интерфейс разбиения на страницы
- `Separator` не используется для GridView, но используются свойствами `RowType` для элементов управления DataList и Repeater, два веб-элемента управления данными будут обсуждаться в следующих учебных курсах.

Поскольку строки `EmptyDataRow`, `Header`, `Footer`и `Pager` не связаны с записью `DataSource`, они всегда будут иметь значение `Nothing` для их свойства `DataItem`. По этой причине, прежде чем пытаться работать с свойством `DataItem` текущего `GridViewRow`, сначала необходимо убедиться, что мы работаем с `DataRow`. Это можно сделать, проверив свойство `RowType` `GridViewRow`следующим образом:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample16.vb)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>Шаг 9. выделение строки желтого, если значение UnitPrice меньше $10,00

Последний шаг — программное выделение всей `GridViewRow`, если значение `UnitPrice` для этой строки меньше $10,00. Синтаксис для доступа к строкам или ячейкам GridView совпадает со `GridViewID.Rows(index)`ом DetailsView для доступа ко всей строке, `GridViewID.Rows(index).Cells(index)` для доступа к определенной ячейке. Однако когда обработчик событий `RowDataBound` запускает привязку к данным `GridViewRow` еще не добавлена в коллекцию `Rows` GridView. Таким образом, невозможно получить доступ к текущему экземпляру `GridViewRow` из обработчика событий `RowDataBound` с помощью коллекции Rows.

Вместо `GridViewID.Rows(index)`мы можем ссылаться на текущий экземпляр `GridViewRow` в обработчике событий `RowDataBound` с помощью `e.Row`. То есть, чтобы выделить текущий экземпляр `GridViewRow` из обработчика `RowDataBound` событий, который мы будем использовать:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample17.vb)]

Вместо того, чтобы устанавливать свойство `BackColor` `GridViewRow`напрямую, придерживайтесь использования классов CSS. Я создал класс CSS с именем `AffordablePriceEmphasis`, который устанавливает желтый цвет фона. Завершенный `RowDataBound` обработчик событий выглядит следующим образом:

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample18.vb)]

[![самые недорогие продукты выделены желтым цветом](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)

**Рис. 11**. наиболее доступные продукты выделены желтым цветом ([щелкните, чтобы просмотреть изображение с полным размером](custom-formatting-based-upon-data-vb/_static/image27.png))

## <a name="summary"></a>Сводка

В этом учебнике мы увидели, как форматировать элементы GridView, DetailsView и FormView на основе данных, привязанных к элементу управления. Для этого мы создали обработчик событий для событий `DataBound` или `RowDataBound`, где базовые данные были проверены вместе с изменением форматирования, если это необходимо. Для доступа к данным, привязанным к DetailsView или FormView, мы используем свойство `DataItem` в обработчике событий `DataBound`. для элемента управления GridView каждое свойство `DataItem` экземпляра `GridViewRow` содержит данные, привязанные к этой строке, которая доступна в обработчике событий `RowDataBound`.

Синтаксис программной настройки форматирования веб-элемента управления данными зависит от веб-элемента управления и способа отображения данных для форматирования. Для элементов управления DetailsView и GridView доступ к строкам и ячейкам можно получить по порядковому индексу. Для FormView, в котором используются шаблоны, метод `FindControl("controlID")` обычно используется для нахождение веб-элемента управления в шаблоне.

В следующем учебном курсе мы рассмотрим, как использовать шаблоны с GridView и DetailsView. Кроме того, мы увидим еще один способ настройки форматирования на основе базовых данных.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого учебника были Е.Р. Гилморе, Деннис Patterson и "+ + + Jagers). Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](displaying-summary-information-in-the-gridview-s-footer-cs.md)
> [Вперед](using-templatefields-in-the-gridview-control-vb.md)
