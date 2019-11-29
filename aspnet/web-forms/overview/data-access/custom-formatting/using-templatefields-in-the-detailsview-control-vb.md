---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
title: Использование полей TemplateField в элементе управления DetailsView (VB) | Документация Майкрософт
author: rick-anderson
description: Те же возможности полей TemplateField, которые доступны с GridView, также доступны в элементе управления DetailsView. В этом учебнике будет отображен один продукт...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0b91d5f8-127d-4f6a-b204-f2e2b35ef703
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
msc.type: authoredcontent
ms.openlocfilehash: e96f954c27ae1c8ccc18a9c40fe7e541b487c1cc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74625076"
---
# <a name="using-templatefields-in-the-detailsview-control-vb"></a>Использование TemplateField в элементе управления DetailsView (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_13_VB.exe) или [Загрузка PDF-файла](using-templatefields-in-the-detailsview-control-vb/_static/datatutorial13vb1.pdf)

> Те же возможности полей TemplateField, которые доступны с GridView, также доступны в элементе управления DetailsView. В этом учебнике мы будем отображать по одному продукту за раз с помощью элемента DetailsView, содержащего полей TemplateField.

## <a name="introduction"></a>Введение

TemplateField предлагает большую степень гибкости данных отрисовки, чем элементы управления BoundField, CheckBoxField, HyperLinkField и другие поля данных. В [предыдущем учебном курсе](using-templatefields-in-the-gridview-control-vb.md) мы рассматривали использование TemplateField в GridView для:

- Отображение нескольких значений полей данных в одном столбце. В частности, поля `FirstName` и `LastName` были объединены в один столбец GridView.
- Используйте альтернативный веб-элемент управления для выражения значения поля данных. Мы увидели, как показывать `HiredDate` значение с помощью элемента управления Calendar.
- Отображение сведений о состоянии на основе базовых данных. В то время как таблица `Employees` не содержит столбец, который возвращает количество дней, в течение которых сотрудник выполнял задание, мы смогли отобразить такую информацию в примере GridView из предыдущего руководства с использованием TemplateField и метода форматирования.

Те же возможности полей TemplateField, которые доступны с GridView, также доступны в элементе управления DetailsView. В этом учебнике мы будем отображать по одному продукту за раз с помощью элемента DetailsView, который содержит два полей TemplateField. Первый TemplateField будет сочетать поля данных `UnitPrice`, `UnitsInStock`и `UnitsOnOrder` в одну строку DetailsView. Второй TemplateField будет отображать значение поля `Discontinued`, но будет использовать метод форматирования для вывода значения "YES", если `Discontinued` `True`, и "нет" в противном случае.

[для настройки экрана используются ![две полей TemplateField](using-templatefields-in-the-detailsview-control-vb/_static/image2.png)](using-templatefields-in-the-detailsview-control-vb/_static/image1.png)

**Рис. 1**. Использование двух полей TemplateField для настройки отображения ([щелкните, чтобы просмотреть изображение в полном размере](using-templatefields-in-the-detailsview-control-vb/_static/image3.png))

Приступим к работе!

## <a name="step-1-binding-the-data-to-the-detailsview"></a>Шаг 1. Привязка данных к элементу DetailsView

Как обсуждалось в предыдущем руководстве, при работе с полей TemplateField зачастую проще всего начать с создания элемента управления DetailsView, который содержит только BoundFields, а затем добавить новый полей TemplateField или преобразовать существующий BoundFields в полей TemplateField по мере необходимости. . Поэтому начните с этого руководства, добавив DetailsView на страницу в конструкторе и привязывая его к элементу ObjectDataSource, который возвращает список продуктов. В результате выполнения этих действий будет создан элемент DetailsView с BoundFields для каждого из полей нелогического значения продукта и CheckBoxField для одного поля логического значения (снято с конца).

Откройте страницу `DetailsViewTemplateField.aspx` и перетащите элемент DetailsView с панели элементов на конструктор. В смарт-теге DetailsView выберите Добавление нового элемента управления ObjectDataSource, который вызывает метод `GetProducts()` класса `ProductsBLL`.

[![добавить новый элемент управления ObjectDataSource, вызывающий метод Products ()](using-templatefields-in-the-detailsview-control-vb/_static/image5.png)](using-templatefields-in-the-detailsview-control-vb/_static/image4.png)

**Рис. 2**. Добавление нового элемента управления ObjectDataSource, который вызывает метод `GetProducts()` ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image6.png))

Для этого отчета удалите `ProductID`, `SupplierID`, `CategoryID`и `ReorderLevel` BoundFields. Затем Переупорядочивайте BoundFields, чтобы `CategoryName` и `SupplierName` BoundFields отображались сразу после `ProductName` BoundField. Вы можете настроить свойства `HeaderText` и свойства форматирования для BoundFields, как вы видите. Как и в случае с GridView, эти изменения уровня BoundField можно выполнить в диалоговом окне поля (доступно, щелкнув ссылку изменить поля в смарт-теге DetailsView) или декларативный синтаксис. Наконец, очистите значения свойств `Height` и `Width` DetailsView, чтобы разрешить расширять элемент управления DetailsView в зависимости от отображаемых данных, и установите флажок Включить разбиение по страницам в смарт-теге.

После внесения этих изменений декларативная разметка элемента управления DetailsView должна выглядеть следующим образом:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample1.aspx)]

Уделите время просмотру страницы в браузере. На этом этапе вы должны увидеть один продукт в списке (Chai) со строками, содержащими название продукта, категорию, поставщика, цену, единицы склада, единицы в заказе и состояние прекращения.

[![сведения о продукте показаны с помощью серии BoundFields](using-templatefields-in-the-detailsview-control-vb/_static/image8.png)](using-templatefields-in-the-detailsview-control-vb/_static/image7.png)

**Рис. 3**. сведения о продукте показаны с помощью серии BoundFields ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image9.png))

## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>Шаг 2. объединение цены, единиц склада и единиц измерения по заказу в одну строку

DetailsView содержит строку для полей `UnitPrice`, `UnitsInStock`и `UnitsOnOrder`. Эти поля данных можно объединить в одну строку с TemplateField либо путем добавления нового TemplateField, либо путем преобразования одного из существующих `UnitPrice`, `UnitsInStock`и `UnitsOnOrder` BoundFields в TemplateField. Хотя я предпочитаю преобразовывать существующие BoundFields, давайте попробуем добавить новый TemplateField.

Сначала щелкните ссылку Edit Fields (изменить поля) в смарт-теге DetailsView, чтобы открыть диалоговое окно поля. Затем добавьте новый TemplateField и задайте для его свойства `HeaderText` значение "Цена и Инвентаризация" и переместите новый TemplateField, чтобы он был расположен над `UnitPrice` BoundField.

[![добавить новый TemplateField в элемент управления DetailsView](using-templatefields-in-the-detailsview-control-vb/_static/image11.png)](using-templatefields-in-the-detailsview-control-vb/_static/image10.png)

**Рис. 4**. Добавление нового TemplateField к элементу управления DetailsView ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image12.png))

Так как этот новый TemplateField будет содержать значения, которые в настоящее время отображаются в `UnitPrice`, `UnitsInStock`и `UnitsOnOrder` BoundFields, давайте удалим их.

Последняя задача этого шага — определение `ItemTemplate` разметки для цены и инвентаризации TemplateField, которую можно выполнить с помощью интерфейса редактирования шаблона DetailsView в конструкторе или вручную с помощью декларативного синтаксиса элемента управления. Как и в случае с GridView, можно получить доступ к интерфейсу редактирования шаблонов DetailsView, щелкнув ссылку изменить шаблоны в смарт-теге. Здесь можно выбрать шаблон для редактирования из раскрывающегося списка, а затем добавить все веб-элементы управления из панели элементов.

Для работы с этим руководством Начните с добавления элемента управления Label в `ItemTemplate`Price и Inventory TemplateField. Затем щелкните ссылку Edit DataBindings (Правка привязок) в смарт-теге Label Web Control и привяжите свойство `Text` к полю `UnitPrice`.

[![привязать свойство Text метки к полю данных UnitPrice](using-templatefields-in-the-detailsview-control-vb/_static/image14.png)](using-templatefields-in-the-detailsview-control-vb/_static/image13.png)

**Рис. 5**. привязка свойства `Text` метки к полю данных `UnitPrice` ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image15.png))

## <a name="formatting-the-price-as-a-currency"></a>Форматирование цены в виде валюты

Благодаря этому добавлению метки Web Control Price и Inventory TemplateField теперь будут отображаться только цены на выбранный продукт. На рис. 6 показан снимок экрана с ходом выполнения, который был на данный момент просмотрен в браузере.

[![цены и описи TemplateField показывает цену](using-templatefields-in-the-detailsview-control-vb/_static/image17.png)](using-templatefields-in-the-detailsview-control-vb/_static/image16.png)

**Рис. 6**. TemplateField цены и инвентаризации показывает цену ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image18.png)).

Обратите внимание, что цена продукта не отформатирована как денежная единица. С помощью BoundField форматирование возможно путем присвоения свойству `HtmlEncode` значения `False`, а свойству `DataFormatString` — значение `{0:formatSpecifier}`. Однако для TemplateField все инструкции форматирования должны быть указаны в синтаксисе DataBinding или с помощью метода форматирования, определенного где-либо в коде приложения (например, в классе кода программной части страницы ASP.NET).

Чтобы задать форматирование для синтаксиса DataBinding, используемого в веб-элементе управления Label, вернитесь в диалоговое окно привязки данных, щелкнув ссылку Edit Databindingss (изменить привязки к данным) в смарт-теге метки. Инструкции по форматированию можно ввести непосредственно в раскрывающемся списке Формат или выбрать одну из определенных строк формата. Как и в случае со свойством `DataFormatString` BoundField, форматирование задается с помощью `{0:formatSpecifier}`.

Для поля `UnitPrice` Используйте форматирование денежной единицы, указанное при выборе соответствующего значения раскрывающегося списка или введя в `{0:C}` вручную.

[![отформатировать цену как валюту](using-templatefields-in-the-detailsview-control-vb/_static/image20.png)](using-templatefields-in-the-detailsview-control-vb/_static/image19.png)

**Рис. 7**. форматирование цены в виде валюты ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image21.png))

Декларативно спецификация форматирования указывается как второй параметр в методах `Bind` или `Eval`. Параметры, только что сделанные в конструкторе, приводят к следующему выражению привязки данных в декларативной разметке:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>Добавление оставшихся полей данных в TemplateField

На этом этапе мы выделили и отправили поле данных `UnitPrice` в полях Price и Inventory TemplateField, но по-прежнему должны отображать `UnitsInStock` и `UnitsOnOrder` поля. Давайте попробуем отобразить их в строке под ценой и в круглых скобках. В интерфейсе редактирования шаблонов в конструкторе такую разметку можно добавить, разместив курсор внутри шаблона и просто введя текст, который будет отображаться. Кроме того, эту разметку можно указать непосредственно в декларативном синтаксисе.

Добавьте статическую разметку, пометка веб-элементов управления и синтаксис привязки данных таким образом, чтобы цены и инвентаризации TemplateField отображали сведения о ценах и запасах следующим образом:

*UnitPrice*  
(**В складе/по заказу:** *UnitsInStock* / *UnitsOnOrder*)

После выполнения этой задачи декларативная разметка DetailsView должна выглядеть следующим образом:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample3.aspx)]

С помощью этих изменений мы объединили цены и данные инвентаризации в одну строку DetailsView.

[![сведения о ценах и запасах отображаются в одной строке](using-templatefields-in-the-detailsview-control-vb/_static/image23.png)](using-templatefields-in-the-detailsview-control-vb/_static/image22.png)

**Рис. 8**. сведения о ценах и запасах отображаются в одной строке ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image24.png))

## <a name="step-3-customizing-the-discontinued-field-information"></a>Шаг 3. Настройка сведений о неподдерживаемом поле

Столбец `Discontinued` таблицы `Products` является битовым значением, указывающим, был ли продукт прекращен. При привязке элемента DetailsView (или GridView) к элементу управления источником данных поля с логическими значениями, такие как `Discontinued`, реализуются как Чеккбоксфиелдс, а Нелогические поля значений, такие как `ProductID`, `ProductName`и т. д., реализуются как BoundFields. CheckBoxField готовится к просмотру как отключенный флажок, который проверяется, если значение поля данных равно true, в противном случае — неустановленный.

Вместо того, чтобы отображать CheckBoxField, нам может потребоваться отобразить текст, указывающий, снят ли продукт с производства. Для этого можно удалить CheckBoxField из DetailsView, а затем добавить BoundField, для свойства `DataField` которого было задано значение `Discontinued`. Потратьте время на это. После этого изменения DetailsView отображает текст "true" для неподдерживаемых продуктов и "false" для продуктов, которые все еще активны.

[![строки true и false используются для отображения неподдерживаемого состояния](using-templatefields-in-the-detailsview-control-vb/_static/image26.png)](using-templatefields-in-the-detailsview-control-vb/_static/image25.png)

**Рис. 9**. строки true и false используются для отображения неподдерживаемого состояния ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image27.png))

Представьте, что мы не хотим использовать строки "true" или "false", а не "Да" и "нет". Такая настройка может быть выполнена с помощью TemplateField и метода форматирования. Метод форматирования может принимать любое количество входных параметров, но должен возвращать HTML (в виде строки) для внедрения в шаблон.

Добавьте метод форматирования в класс кода программной части `DetailsViewTemplateField.aspx` страницы с именем `DisplayDiscontinuedAsYESorNO`, который принимает объект `Northwind.ProductsRow` в качестве входного параметра и возвращает строку. Как обсуждалось в предыдущем руководстве, этот метод *должен* быть помечен как `Protected` или `Public`, чтобы быть доступным из шаблона.

[!code-vb[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample4.vb)]

Этот метод проверяет входной параметр (`discontinued`) и возвращает значение "YES", если это `True`, в противном случае — "нет".

> [!NOTE]
> В методе форматирования, рассмотренном в предыдущем учебнике, помните, что мы передавали поле данных, которое может содержать `NULL` s и, следовательно, требовалось проверить, имел ли `HiredDate`ное значение свойства `NULL` базы данных перед доступом к свойству `HiredDate` `EmployeesRow`. Такая проверка не требуется, так как `Discontinued` столбцу не может быть назначено значение `NULL` базы данных. Более того, это объясняется тем, что метод может принимать логический входной параметр, а не принимать `ProductsRow` экземпляр или параметр типа `Object`.

По завершении этого метода форматирования все, что остается, — это вызов из `ItemTemplate`TemplateField. Чтобы создать TemplateField, удалите `Discontinued` BoundField и добавьте новый TemplateField или преобразуйте `Discontinued` BoundField в TemplateField. Затем из представления декларативной разметки измените TemplateField, чтобы он содержал только ItemTemplate, вызывающий метод `DisplayDiscontinuedAsYESorNO`, передав значение свойства `Discontinued` текущего экземпляра `ProductRow`. Доступ к этому можно получить с помощью метода `Eval`. В частности, разметка TemplateField должна выглядеть следующим образом:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample5.aspx)]

Это приведет к вызову метода `DisplayDiscontinuedAsYESorNO` при отрисовке DetailsView, передавая значение `Discontinued` экземпляра `ProductRow`. Так как метод `Eval` возвращает значение типа `Object`, но метод `DisplayDiscontinuedAsYESorNO` предполагает входной параметр типа `Boolean`, мы приводим возвращаемое значение методов `Eval` к `Boolean`. Затем метод `DisplayDiscontinuedAsYESorNO` возвратит значение "YES" или "NO" в зависимости от полученного значения. Возвращаемое значение — это то, что отображается в этой строке DetailsView (см. рис. 10).

[![да или не показывать значения в неподдерживаемой строке](using-templatefields-in-the-detailsview-control-vb/_static/image29.png)](using-templatefields-in-the-detailsview-control-vb/_static/image28.png)

**Рис. 10**. в неподдерживаемой строке теперь отображаются значения Да или нет ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-detailsview-control-vb/_static/image30.png))

## <a name="summary"></a>Сводка

TemplateField в элементе управления DetailsView обеспечивает большую степень гибкости отображения данных, чем доступно в других элементах управления полями и идеально подходит для ситуаций, в которых:

- Несколько полей данных должны отображаться в одном столбце GridView
- Данные лучше всего выражаются с помощью веб-элемента управления, а не обычного текста.
- Выходные данные зависят от базовых данных, таких как отображение метаданных или переформатирование данных.

Хотя полей TemplateField обеспечивает большую степень гибкости при отрисовке базовых данных DetailsView, вывод DetailsView по-прежнему имеет битовую угловат, так как каждое поле подготавливается к просмотру как строка в `<table>`HTML.

Элемент управления FormView обеспечивает большую степень гибкости при настройке отображаемых выходных данных. Элемент FormView не содержит полей, а только ряда шаблонов (`ItemTemplate`, `EditItemTemplate`, `HeaderTemplate`и т. д.). Мы посмотрим, как использовать FormView, чтобы еще больше контролировать макет, готовый для просмотра, в нашем следующем руководстве.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был «Jagers)». Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](using-templatefields-in-the-gridview-control-vb.md)
> [Вперед](using-the-formview-s-templates-vb.md)
