---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
title: Использование шаблонов FormView (C#) | Документация Майкрософт
author: rick-anderson
description: В отличие от DetailsView, FormView не состоит из полей. Вместо этого FormView отображается с помощью шаблонов. В этом учебнике мы рассмотрим использование F...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d3f062af-88cf-426d-af44-e41f32c41672
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
msc.type: authoredcontent
ms.openlocfilehash: 013c6878aad1a2277b0a334c096ff16ed84a95f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78426618"
---
# <a name="using-the-formviews-templates-c"></a>Использование шаблонов FormView (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_14_CS.exe) или [Загрузка PDF-файла](using-the-formview-s-templates-cs/_static/datatutorial14cs1.pdf)

> В отличие от DetailsView, FormView не состоит из полей. Вместо этого FormView отображается с помощью шаблонов. В этом учебнике мы рассмотрим использование элемента управления FormView для предоставления менее строгого отображения данных.

## <a name="introduction"></a>Введение

В последних двух учебных курсах мы увидели, как настроить выходы элементов управления GridView и DetailsView с помощью полей TemplateField. Полей TemplateField позволяют строго настраивать содержимое определенного поля, но в итоге, как GridView, так и DetailsView имеют угловат внешний вид, похожий на сетку. Во многих сценариях такой макет является идеальным, но в то же время требуется более гибкое, менее жесткое отображение. При отображении одной записи такой жидкий макет можно использовать с помощью элемента управления FormView.

В отличие от DetailsView, FormView не состоит из полей. Нельзя добавить BoundField или TemplateField в FormView. Вместо этого FormView отображается с помощью шаблонов. Рассматривайте FormView как элемент управления DetailsView, который содержит один TemplateField. FormView поддерживает следующие шаблоны:

- `ItemTemplate`, используемый для отображения конкретной записи, отображаемой в элементе FormView
- `HeaderTemplate`, используемое для указания необязательной строки заголовка
- `FooterTemplate`, используемое для указания необязательной строки нижнего колонтитула
- `EmptyDataTemplate`, когда `DataSource` FormView не имеет записей, `EmptyDataTemplate` используется вместо `ItemTemplate` для отрисовки разметки элемента управления.
- `PagerTemplate` можно использовать для настройки интерфейса разбиения на страницы для FormView, для которых включено разбиение на страницы
- `EditItemTemplate` / `InsertItemTemplate` используется для настройки интерфейса правки или вставки интерфейса для FormView, которые поддерживают такие функции.

В этом учебнике мы рассмотрим использование элемента управления FormView для предоставления менее строгого отображения продуктов. Вместо того чтобы использовать поля для имени, категории, поставщика и т. д., `ItemTemplate` FormView будет отображать эти значения, используя сочетание элемента Header и `<table>` (см. рис. 1).

[![FormView выходит из макета сетки, как видно в элементе DetailsView](using-the-formview-s-templates-cs/_static/image2.png)](using-the-formview-s-templates-cs/_static/image1.png)

**Рис. 1**. элемент FormView разбивается на макет, похожий на сетку, видимый в элементе DetailsView ([щелкните, чтобы просмотреть изображение с полным размером](using-the-formview-s-templates-cs/_static/image3.png))

## <a name="step-1-binding-the-data-to-the-formview"></a>Шаг 1. Привязка данных к FormView

Откройте страницу `FormView.aspx` и перетащите элемент FormView из области элементов в конструктор. При первом добавлении FormView отображается в виде серого поля, что дает нам указание о необходимости `ItemTemplate`.

[![FormView нельзя визуализировать в конструкторе, пока не будет предоставлен ItemTemplate](using-the-formview-s-templates-cs/_static/image5.png)](using-the-formview-s-templates-cs/_static/image4.png)

**Рис. 2**. невозможно отобразить FormView в конструкторе, пока не будет предоставлен `ItemTemplate` ([щелкните, чтобы просмотреть изображение с полным размером](using-the-formview-s-templates-cs/_static/image6.png))

`ItemTemplate` можно создать вручную (с помощью декларативного синтаксиса) или можно создать самостоятельно, привязывая FormView к элементу управления источником данных через конструктор. Эта созданная `ItemTemplate` содержит HTML-код, в котором перечислены имена всех полей и элементы управления Label, свойства `Text` которых привязаны к значению поля. Этот подход также автоматически создает `InsertItemTemplate` и `EditItemTemplate`, которые заполняются элементами управления вводом для каждого поля данных, возвращаемого элементом управления источника данных.

Если вы хотите автоматически создать шаблон, из смарт-тега FormView добавьте новый элемент управления ObjectDataSource, который вызывает метод `GetProducts()` класса `ProductsBLL`. Будет создан элемент FormView с `ItemTemplate`, `InsertItemTemplate`и `EditItemTemplate`. Из представления исходного кода удалите `InsertItemTemplate` и `EditItemTemplate`, так как мы не заинтересованы в создании элемента FormView, поддерживающего редактирование или вставку еще. Затем очистите разметку в `ItemTemplate`, чтобы у нас была чистая работа.

Если вы создаете `ItemTemplate` вручную, можно добавить и настроить ObjectDataSource, перетащив его из панели элементов в конструктор. Однако не задавайте источник данных FormView из конструктора. Вместо этого перейдите в представление исходного кода и вручную установите свойство `DataSourceID` FormView в значение `ID` элемента ObjectDataSource. Затем вручную добавьте `ItemTemplate`.

Независимо от того, какой подход вы решили предпринять, декларативная разметка FormView должна выглядеть следующим образом:

[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample1.aspx)]

Установите флажок Включить разбиение по страницам в смарт-теге FormView. При этом в декларативный синтаксис FormView будет добавлен атрибут `AllowPaging="True"`. Также присвойте свойству `EnableViewState` значение false.

## <a name="step-2-defining-theitemtemplates-markup"></a>Шаг 2. Определение разметки`ItemTemplate`

С помощью элемента FormView, привязанного к элементу управления ObjectDataSource и настроенного для поддержки разбиения на страницы, можно указать содержимое для `ItemTemplate`. В этом руководстве мы добавим название продукта в заголовок `<h3>`. Далее мы используем HTML-`<table>` для просмотра оставшихся свойств продукта в таблице из четырех столбцов, где в первом и третьем столбцах перечислены имена свойств, а во втором и четвертом списках их значения.

Эту разметку можно указать в интерфейсе редактирования шаблона FormView в конструкторе или указать вручную с помощью декларативного синтаксиса. При работе с шаблонами я обычно быстрее работает с декларативным синтаксисом, но вы можете использовать любой из наиболее удобных методик.

В следующей разметке показана декларативная разметка FormView после завершения структуры `ItemTemplate`.

[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample2.aspx)]

Обратите внимание, что синтаксис привязки данных — `<%# Eval("ProductName") %>`, например, может быть вставлен непосредственно в выходные данные шаблона. То есть его не нужно назначать свойству `Text` элемента управления Label. Например, у нас есть `ProductName` значение, отображаемое в элементе `<h3>` с помощью `<h3><%# Eval("ProductName") %></h3>`, который для продукта Chai будет отображаться как `<h3>Chai</h3>`.

Классы `ProductPropertyLabel` и `ProductPropertyValue` CSS используются для указания стиля имен и значений свойств продукта в `<table>`. Эти классы CSS определяются в `Styles.css` и приводят к выделению имен свойств полужирным и выровненным по правому краю и добавляют правое дополнение к значениям свойств.

Так как в FormView нет Чеккбоксфиелдс, чтобы отобразить значение `Discontinued` в качестве флажка, необходимо добавить собственный элемент управления CheckBox. Свойству `Enabled` присвоено значение false, делая его доступным только для чтения, а свойство `Checked` CheckBox привязано к значению поля данных `Discontinued`.

По завершении `ItemTemplate` сведения о продукте отображаются гораздо более динамичным способом. Сравните выходные данные DetailsView из последнего учебного курса (рис. 3) с выходными данными, созданными в элементе FormView в этом учебнике (рис. 4).

[![жесткая выводимые данные DetailsView](using-the-formview-s-templates-cs/_static/image8.png)](using-the-formview-s-templates-cs/_static/image7.png)

**Рис. 3**. Нежесткое вывод DetailsView ([щелкните, чтобы просмотреть изображение с полным размером](using-the-formview-s-templates-cs/_static/image9.png))

[![данных о жидких элементах FormView](using-the-formview-s-templates-cs/_static/image11.png)](using-the-formview-s-templates-cs/_static/image10.png)

**Рис. 4**. Выходное представление FormView ([щелкните, чтобы просмотреть изображение с полным размером](using-the-formview-s-templates-cs/_static/image12.png))

## <a name="summary"></a>Сводка

Хотя элементы управления GridView и DetailsView могут иметь свои выходные данные, настроенные с помощью полей TemplateField, они по-прежнему представляют данные в формате угловат, похожем на Grid. В тех случаях, когда одна запись должна быть показана с использованием менее жесткого макета, элемент FormView является идеальным выбором. Как и DetailsView, элемент FormView визуализирует одну запись из `DataSource`, но в отличие от DetailsView она состоит только из шаблонов и не поддерживает поля.

Как было показано в этом учебнике, FormView обеспечивает более гибкий макет при отображении одной записи. В следующих учебных курсах мы рассмотрим элементы управления DataList и Repeater, которые обеспечивают тот же уровень гибкости, что и Формсвиев, но могут отображать несколько записей (например, GridView).

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. В ходе работы с этим руководством был Е.Р. Гилморе. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](using-templatefields-in-the-detailsview-control-cs.md)
> [Вперед](displaying-summary-information-in-the-gridview-s-footer-cs.md)
