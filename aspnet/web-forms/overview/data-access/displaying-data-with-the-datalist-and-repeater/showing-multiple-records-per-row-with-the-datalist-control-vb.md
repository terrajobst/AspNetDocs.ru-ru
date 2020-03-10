---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-vb
title: Отображение нескольких записей в строке с помощью элемента управления DataList (VB) | Документация Майкрософт
author: rick-anderson
description: В этом кратком руководстве мы рассмотрим, как настроить макет DataList с помощью свойств RepeatColumns и RepeatDirection.
ms.author: riande
ms.date: 09/13/2006
ms.assetid: f555c531-bf33-4699-9987-42dbfef23c1f
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 17283dae192896fbaa48f1d7fe49afdbaf4c9a02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78495306"
---
# <a name="showing-multiple-records-per-row-with-the-datalist-control-vb"></a>Отображение нескольких записей в одной строке с помощью элемента управления DataList (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_VB.exe) или [Загрузка PDF-файла](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/datatutorial31vb1.pdf)

> В этом кратком руководстве мы рассмотрим, как настроить макет DataList с помощью свойств RepeatColumns и RepeatDirection.

## <a name="introduction"></a>Введение

Примеры DataList, представленные в прошлых двух учебниках, подготавливают каждую запись из источника данных в виде строки в HTML-`<table>`с одним столбцом. Хотя это поведение DataList по умолчанию, очень легко настроить отображение DataList таким образом, чтобы элементы источника данных были распределены по нескольким столбцам, многострочным таблицам. Более того, все элементы источника данных могут отображаться в однострочном DataList.

Макет DataList можно настроить с помощью свойств `RepeatColumns` и `RepeatDirection`, которые соответственно указывают количество отображаемых столбцов, а также расположение этих элементов по вертикали или по горизонтали. На рис. 1, например, отображается элемент управления DataList, отображающий сведения о продукте в таблице с тремя столбцами.

[![элемент управления DataList показывает три продукта в строке](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image1.png)

**Рисунок 1**. в DataList отображается три продукта на строку ([щелкните, чтобы просмотреть изображение с полным размером](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image3.png))

Показывая несколько элементов источника данных в каждой строке, элемент управления DataList может более эффективно использовать горизонтальное пространство экрана. В этом кратком учебнике мы рассмотрим эти два свойства DataList.

## <a name="step-1-displaying-product-information-in-a-datalist"></a>Шаг 1. Отображение сведений о продукте в элементе управления DataList

Прежде чем исследовать свойства `RepeatColumns` и `RepeatDirection`, давайте сначала создадим на нашей странице элемент управления DataList, содержащий сведения о продукте, используя стандартный многострочный макет таблицы с одним столбцом. В этом примере параметр s отображает название продукта, категорию и цену, используя следующую разметку:

[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-vb/samples/sample1.html)]

Мы узнали, как привязать данные к DataList в предыдущих примерах, так что я быстро перейдем к этим шагам. Для начала откройте страницу `RepeatColumnAndDirection.aspx` в папке `DataListRepeaterBasics` и перетащите элемент управления DataList с панели элементов в конструктор. Из смарт-тега DataList s выберите создать новый элемент ObjectDataSource и настройте его для извлечения данных из `GetProducts` метода `ProductsBLL` классов, выбрав параметр (нет) на вкладках Вставка, обновление и удаление мастера.

После создания и привязки нового элемента управления ObjectDataSource к DataList Visual Studio автоматически создаст `ItemTemplate`, отображающий имя и значение для каждого поля данных продукта. Измените `ItemTemplate` либо напрямую с помощью декларативной разметки, либо из параметра изменить шаблоны в смарт-теге DataList, чтобы использовать приведенную выше разметку, заменив *Название продукта*, *название категории*и текст *цены* на элементы управления метками, которые используют соответствующий синтаксис DataBinding для присвоения значений их свойствам `Text`. После обновления `ItemTemplate`декларативная разметка страницы должна выглядеть следующим образом:

[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-vb/samples/sample2.aspx)]

Обратите внимание, что я включил описатель формата в `Eval` синтаксис привязки данных для `UnitPrice`, отформатировать возвращаемое значение как денежную `Eval("UnitPrice", "{0:C}").`

Уделите время посещению страницы в браузере. Как показано на рис. 2, элемент управления DataList отображается как таблица с одним столбцом и несколькими строками продуктов.

[![по умолчанию DataList отображается как таблица с одним столбцом и несколькими строками.](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image4.png)

**Рис. 2**. по умолчанию DataList отображается в виде таблицы с одним столбцом и несколькими строками ([щелкните, чтобы просмотреть изображение с полным размером](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image6.png))

## <a name="step-2-changing-the-datalist-s-layout-direction"></a>Шаг 2. изменение направления макета в DataList

Хотя поведение элемента управления DataList по умолчанию заключается в разметке элементов по вертикали в таблице с одним столбцом и несколькими строками, это поведение можно легко изменить с помощью [свойства`RepeatDirection`](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)DataList. Свойство `RepeatDirection` может принимать одно из двух возможных значений: `Horizontal` или `Vertical` (значение по умолчанию).

Изменив свойство `RepeatDirection` с `Vertical` на `Horizontal`, DataList отрисовывает свои записи в одной строке, создавая по одному столбцу для каждого элемента источника данных. Чтобы проиллюстрировать этот эффект, щелкните элемент управления DataList в конструкторе, а затем в окно свойств измените свойство `RepeatDirection` с `Vertical` на `Horizontal`. Сразу же после этого конструктор корректирует макет DataList, создавая многострочный интерфейс с несколькими столбцами (см. рис. 3).

[![свойство RepeatDirection определяет направление расположения элементов DataList](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image7.png)

**Рис. 3**. свойство `RepeatDirection` определяет направление расположения элементов DataList ([щелкните, чтобы просмотреть изображение с полным размером](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image9.png))

При отображении небольших объемов данных таблица с одной строкой и несколькими столбцами может быть идеальным средством для максимального увеличения объема экрана. Однако для больших объемов данных одна строка потребует много столбцов, при этом элементы, которые можно заменять на экране, перемещаются вправо. На рис. 4 показаны продукты при подготовке к просмотру в DataList с одной строкой. Так как существует множество продуктов (свыше 80), пользователю придется прокручивать направо, чтобы просмотреть сведения о каждом из этих продуктов.

[![для достаточно больших источников данных, для одного столбца DataList потребуется горизонтальная прокрутка](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image10.png)

**Рис. 4**. для достаточно больших источников данных для одного столбца DataList потребуется горизонтальная прокрутка ([щелкните, чтобы просмотреть изображение с полным размером](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image12.png))

## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>Шаг 3. Отображение данных в многоколоночном, многострочном столбце

Для создания многостолбцового DataList с несколькими строками необходимо задать для [свойства`RepeatColumns`](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx) число отображаемых столбцов. По умолчанию свойство `RepeatColumns` имеет значение 0, которое приведет к отображению всех элементов DataList в одной строке или столбце (в зависимости от значения свойства `RepeatDirection`).

В нашем примере пусть для каждой строки таблицы отображается три продукта. Поэтому присвойте свойству `RepeatColumns` значение 3. После внесения этого изменения просмотрите результаты в браузере. Как показано на рис. 5, продукты теперь перечислены в таблице с тремя столбцами и несколькими строками.

[![для каждой строки отображаются три продукта](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image13.png)

**Рис. 5**. Отображение трех продуктов для каждой строки ([щелкните, чтобы просмотреть изображение с полным размером](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image15.png))

Свойство `RepeatDirection` влияет на расположение элементов в DataList. На рис. 5 показаны результаты со свойством `RepeatDirection`, для которого задано значение `Horizontal`. Обратите внимание, что первые три продукта Chai, меня и Анисид сируп располагаются слева направо, сверху вниз. Следующие три продукта (начиная с Chef Anton's s Cajun) отображаются в строке под первыми тремя. При изменении свойства `RepeatDirection` обратно на `Vertical`эти продукты размещается сверху вниз, слева направо, как показано на рис. 6.

[![здесь продукты располагаются вертикально](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image16.png)

**Рис. 6**. здесь продукты располагаются вертикально ([щелкните, чтобы просмотреть изображение с полным размером](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image18.png)).

Количество строк, отображаемых в результирующей таблице, зависит от количества записей, привязанных к DataList. Точно то же самое — от общего числа элементов источника данных, деленного на значение свойства `RepeatColumns`. Так как в настоящее время таблица `Products` содержит продукты 84, которые делятся на 3, количество строк составляет 28. Если количество элементов в источнике данных и значение свойства `RepeatColumns` не являются кратными, то последняя строка или столбец будет содержать пустые ячейки. Если `RepeatDirection` имеет значение `Vertical`, то последний столбец будет содержать пустые ячейки. Если `RepeatDirection` `Horizontal`, то в последней строке будут сонаходиться пустые ячейки.

## <a name="summary"></a>Сводка

Элемент управления DataList по умолчанию перечисляет свои элементы в таблице с одним столбцом и несколькими строками, которая имитирует макет элемента управления GridView с одним TemplateField. Хотя этот макет по умолчанию приемлем, можно максимально увеличить масштаб экрана, отображая несколько элементов источника данных в каждой строке. Для этого достаточно установить свойство `RepeatColumns` DataList s в число отображаемых столбцов в каждой строке. Кроме того, свойство DataList `RepeatDirection` можно использовать для указания того, следует ли располагать содержимое многостолбцовой таблицы, многострочной, горизонтально и сверху вниз или вертикально сверху вниз, слева направо.

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Джон суру. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
> [Вперед](nested-data-web-controls-vb.md)
