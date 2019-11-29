---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
title: Пользовательские кнопки в DataList и Repeater (C#) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы создадим интерфейс, который использует Repeater для перечисления категорий в системе, где каждая категория предоставляет кнопку для отображения ее ассоЦи...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 1f42e332-78dc-438b-9e35-0c97aa0ad929
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: e8cb1054068327c25e057b6df1cc7506feec8d37
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74601761"
---
# <a name="custom-buttons-in-the-datalist-and-repeater-c"></a>Настраиваемые кнопки в элементах управления DataList и Repeater (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_CS.exe) или [Загрузка PDF-файла](custom-buttons-in-the-datalist-and-repeater-cs/_static/datatutorial46cs1.pdf)

> В этом учебнике мы создадим интерфейс, который использует Repeater для перечисления категорий в системе, где каждая категория предоставляет кнопку для отображения связанных с ней продуктов с помощью элемента управления маркированного списка.

## <a name="introduction"></a>Введение

В течение прошлых учебников по DataList и Repeater мы создали как примеры для чтения, так и изменения и удаления примеров. Чтобы упростить редактирование и удаление возможностей в DataList, мы добавили кнопки в элементы DataList `ItemTemplate`, которые при нажатии вызвали обратную передачу и вызвали событие DataList, соответствующее свойству `CommandName` Button. Например, Добавление кнопки в `ItemTemplate` с `CommandName`ным значением свойства Edit приводит к срабатыванию `EditCommand` DataList s при обратной передаче. один с `CommandName` удаления вызывает `DeleteCommand`.

Помимо кнопок "Правка" и "Удалить", элементы управления DataList и Repeater могут также включать кнопки, LinkButton или Имажебуттонс, которые при нажатии выполняют некоторую пользовательскую логику на стороне сервера. В этом учебнике мы создадим интерфейс, который использует Repeater для перечисления категорий в системе. Для каждой категории Repeater будет содержать кнопку для отображения связанных с категориями продуктов, использующих элемент управления «Маркированный список» (см. рис. 1).

[![щелкнув ссылку Показать продукты, вы увидите продукты категории в маркированном списке.](custom-buttons-in-the-datalist-and-repeater-cs/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image1.png)

**Рис. 1**. Если щелкнуть ссылку Показать продукты, отображаются продукты категории в маркированном списке ([щелкните, чтобы просмотреть изображение с полным размером](custom-buttons-in-the-datalist-and-repeater-cs/_static/image3.png))

## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>Шаг 1. Добавление веб-страниц учебника по настраиваемым кнопкам

Прежде чем мы посмотрим, как добавить пользовательскую кнопку, давайте сначала создадим страницы ASP.NET в нашем проекте веб-сайта, которые понадобятся для работы с этим руководством. Для начала добавьте новую папку с именем `CustomButtonsDataListRepeater`. Затем добавьте следующие две страницы ASP.NET в эту папку, чтобы связать каждую страницу с главной страницей `Site.master`:

- `Default.aspx`
- `CustomButtons.aspx`

![Добавление страниц ASP.NET для руководств, связанных с пользовательскими кнопками](custom-buttons-in-the-datalist-and-repeater-cs/_static/image4.png)

**Рис. 2**. добавление страниц ASP.NET для руководств, связанных с пользовательскими кнопками

Как и в других папках, `Default.aspx` в папке `CustomButtonsDataListRepeater` будут перечислены учебники в разделе. Вспомним, что `SectionLevelTutorialListing.ascx` пользовательский элемент управления предоставляет эти функции. Добавьте этот пользовательский элемент управления в `Default.aspx`, перетащив его из обозреватель решений на страницу s представление конструирования.

[![добавить пользовательский элемент управления SectionLevelTutorialListing. ascx в Default. aspx](custom-buttons-in-the-datalist-and-repeater-cs/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image5.png)

**Рис. 3**. Добавление пользовательского элемента управления `SectionLevelTutorialListing.ascx` в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](custom-buttons-in-the-datalist-and-repeater-cs/_static/image7.png))

Наконец, добавьте страницы в качестве записей в файл `Web.sitemap`. В частности, добавьте следующую разметку после разбиения по страницам и сортировку с помощью элементов управления DataList и Repeater `<siteMapNode>`:

[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample1.xml)]

После обновления `Web.sitemap`просмотрите веб-сайт учебников в браузере. В меню слева теперь содержатся элементы для учебников по редактированию, вставке и удалению.

![На карте узла теперь есть запись для учебника по настраиваемым кнопкам](custom-buttons-in-the-datalist-and-repeater-cs/_static/image8.png)

**Рис. 4**. в карте узла теперь есть запись для учебника по настраиваемым кнопкам

## <a name="step-2-adding-the-list-of-categories"></a>Шаг 2. Добавление списка категорий

Для работы с этим руководством необходимо создать элемент Repeater со списком всех категорий вместе с элементом «Показать продукты», который при щелчке отображает связанные продукты категории в маркированном списке. Давайте сначала создадим простой элемент Repeater, содержащий категории в системе. Для начала откройте страницу `CustomButtons.aspx` в папке `CustomButtonsDataListRepeater`. Перетащите элемент Repeater из панели элементов в конструктор и задайте для его свойства `ID` значение `Categories`. Затем создайте новый элемент управления источниками данных из смарт-тега Repeater s. В частности, создайте новый элемент управления ObjectDataSource с именем `CategoriesDataSource`, выбирающий его данные из метода `CategoriesBLL` класса s `GetCategories()`.

[![настроить ObjectDataSource для использования метода класса CategoriesBLL-Categories ()](custom-buttons-in-the-datalist-and-repeater-cs/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image9.png)

**Рис. 5**. Настройка ObjectDataSource для использования метода `GetCategories()` `CategoriesBLL` Class ([щелкните, чтобы просмотреть изображение с полным размером](custom-buttons-in-the-datalist-and-repeater-cs/_static/image11.png))

В отличие от элемента управления DataList, для которого Visual Studio создает `ItemTemplate` по умолчанию на основе источника данных, шаблоны Repeater необходимо определять вручную. Более того, шаблоны Repeater должны создаваться и редактироваться декларативно (то есть в смарт-теге Repeater s нет параметра "изменить шаблоны").

Щелкните вкладку Source (источник) в левом нижнем углу и добавьте `ItemTemplate`, отображающий имя категории в элементе `<h3>` и его описание в теге абзаца. Включите `SeparatorTemplate`, отображающий горизонтальное правило (`<hr />`) между каждой категорией. Также добавьте элемент LinkButton со свойством `Text`, имеющим значение отображать продукты. После выполнения этих действий декларативная разметка страницы должна выглядеть следующим образом:

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample2.aspx)]

На рис. 6 показана страница при просмотре в браузере. В списке указаны имя и описание каждой категории. Кнопка "показывать продукты" при нажатии вызывает обратную передачу, но еще не выполняет никаких действий.

[![отображается имя и описание каждой категории, а также элемент Показать продукты LinkButton.](custom-buttons-in-the-datalist-and-repeater-cs/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image12.png)

**Рис. 6**. отображается имя и описание каждой категории, а также элемент "Показать продукты" ([щелкните, чтобы просмотреть изображение с полным размером](custom-buttons-in-the-datalist-and-repeater-cs/_static/image14.png))

## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>Шаг 3. исполнение логики на стороне сервера при нажатии кнопки "отобразить продукты"

При нажатии кнопки, LinkButton или ImageButton в шаблоне в элементе управления DataList или Repeater происходит обратная передача, а также порождается событие `ItemCommand` DataList или Repeater s. В дополнение к событию `ItemCommand` элемент управления DataList может также вызвать другое, более конкретное событие, если свойство Button `CommandName` имеет значение одной из зарезервированных строк (Delete, Правка, отменить, обновить или выбрать), но событие `ItemCommand` *всегда* срабатывает.

При нажатии кнопки в элементе управления DataList или Repeater часто нам нужно передать нажатую кнопку (в случае, если в элементе есть несколько кнопок, таких как кнопка "Изменить" и "Удалить") и, возможно, некоторые дополнительные сведения (например, значение первичного ключа элемента, кнопка которого была нажата. Кнопки, LinkButton и ImageButton предоставляют два свойства, значения которых передаются в обработчик событий `ItemCommand`:

- `CommandName` строку, обычно используемую для поиска каждой кнопки в шаблоне
- `CommandArgument` обычно используется для хранения значения некоторого поля данных, например значения первичного ключа.

В этом примере задайте свойству `CommandName` LinkButton s значение Шовпродуктс и привяжите `CategoryID` значения первичного ключа текущей записи к свойству `CommandArgument` с помощью синтаксиса привязки данных `CategoryArgument='<%# Eval("CategoryID") %>'`. После указания этих двух свойств декларативный синтаксис LinkButton s должен выглядеть следующим образом:

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample3.aspx)]

При нажатии кнопки происходит обратная передача и вызывается событие DataList или Repeater s `ItemCommand`. Обработчику событий передается кнопка s `CommandName` и `CommandArgument` значения.

Создайте обработчик событий для события Repeater `ItemCommand` и обратите внимание на второй параметр, передаваемый в обработчик событий (с именем `e`). Второй параметр имеет тип [`RepeaterCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) и имеет следующие четыре свойства:

- `CommandArgument` значение свойства `CommandArgument` нажатой кнопки
- `CommandName` значение свойства кнопки `CommandName`
- `CommandSource` ссылку на элемент управления Button, который был нажат
- `Item` ссылку на [`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx) , содержащую кнопку, которая была нажата. Каждая запись, привязанная к элементу Repeater, является `RepeaterItem`

Так как выбранная категория s `CategoryID` передается через свойство `CommandArgument`, можно получить набор продуктов, связанных с выбранной категорией, в обработчике событий `ItemCommand`. Затем эти продукты можно привязать к элементу управления "маркированный" в `ItemTemplate` (который мы еще не добавили). Все, что остается, — это добавить маркированный список, ссылаться на него в обработчике событий `ItemCommand` и привязать к нему набор продуктов для выбранной категории, который мы рассмотрим на шаге 4.

> [!NOTE]
> Обработчику событий DataList `ItemCommand` передается объект типа [`DataListCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx), который предоставляет те же четыре свойства, что и класс `RepeaterCommandEventArgs`.

## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>Шаг 4. Отображение выбранных продуктов категории в маркированном списке

Выбранные продукты категории можно отобразить в элементе управления Repeater `ItemTemplate` с помощью любого числа элементов. Можно добавить еще один вложенный элемент управления Repeater, DataList, DropDownList, GridView и т. д. Так как мы хотим отобразить продукты в виде маркированного списка, мы будем использовать элемент управления «Маркированный список». После возврата к декларативной разметке страницы `CustomButtons.aspx` добавьте элемент управления "маркированный список" в `ItemTemplate` после элемента "отображать продукты LinkButton". Установите `ID` Буллетедлистс s в значение `ProductsInCategory`. Маркированный список отображает значение поля данных, указанного с помощью свойства `DataTextField`; так как этот элемент управления будет иметь привязанную к нему информацию о продукте, задайте для свойства `DataTextField` значение `ProductName`.

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample4.aspx)]

В обработчике событий `ItemCommand` сослаться на этот элемент управления с помощью `e.Item.FindControl("ProductsInCategory")` и привязать его к набору продуктов, связанных с выбранной категорией.

[!code-csharp[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample5.cs)]

Перед выполнением каких бы то ни было действий в обработчике событий `ItemCommand`, разумно сначала проверить значение входящего `CommandName`. Так как обработчик событий `ItemCommand` срабатывает при нажатии *любой* кнопки, если в шаблоне есть несколько кнопок, используется значение `CommandName`, чтобы определить, какое действие следует предпринять. Проверка `CommandName` здесь затеи, так как у нас есть только одна кнопка, но это хороший привычка для формирования. Затем `CategoryID` выбранной категории извлекается из свойства `CommandArgument`. Затем на элемент управления Маркированный список в шаблоне указываются и привязываются результаты метода `ProductsBLL` класса `GetProductsByCategoryID(categoryID)`.

В предыдущих руководствах, в которых использовались кнопки в DataList, например [Общие сведения об изменении и удалении данных в DataList](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md), мы определили значение первичного ключа данного элемента через коллекцию `DataKeys`. Хотя этот подход хорошо работает с элементом управления DataList, элемент управления Repeater не имеет свойства `DataKeys`. Вместо этого следует использовать альтернативный подход к предоставлению значения первичного ключа, например, с помощью кнопки `CommandArgument` свойство или назначив значение первичного ключа для веб-элемента управления скрытой метки в шаблоне и прочесть его значение обратно в обработчике событий `ItemCommand` с помощью `e.Item.FindControl("LabelID")`.

После завершения `ItemCommand` обработчика событий проверьте эту страницу в браузере. Как показано на рис. 7, щелчок ссылки Показать продукты вызывает обратную передачу и отображает продукты для выбранной категории в маркированном списке. Кроме того, обратите внимание, что эти сведения о продукте остаются, даже если щелкнуть другие категории, чтобы отобразить ссылки на продукты.

> [!NOTE]
> Если вы хотите изменить поведение этого отчета таким образом, чтобы в каждый момент времени была указана только одна категория продуктов категории, просто установите для свойства `EnableViewState` управления маркированными списками значение `False`.

[![для вывода продуктов выбранной категории используется маркированный список](custom-buttons-in-the-datalist-and-repeater-cs/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image15.png)

**Рис. 7**. для отображения продуктов выбранной категории используется маркированный список ([щелкните, чтобы просмотреть изображение с полным размером](custom-buttons-in-the-datalist-and-repeater-cs/_static/image17.png))

## <a name="summary"></a>Сводка

Элементы управления DataList и Repeater могут включать любое количество кнопок, LinkButton или Имажебуттонс в своих шаблонах. Такие кнопки при нажатии вызывают обратную передачу и вызывают событие `ItemCommand`. Чтобы связать пользовательское действие на стороне сервера с нажатой кнопкой, создайте обработчик событий для события `ItemCommand`. В этом обработчике событий сначала проверьте значение входящего `CommandName`, чтобы определить, какая кнопка была нажата. Дополнительные сведения можно дополнительно указать с помощью кнопки `CommandArgument` свойства.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Деннис Patterson. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Вперед](custom-buttons-in-the-datalist-and-repeater-vb.md)
