---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs
title: Отображение данных с помощью элементов управления DataList и Repeater (C#) | Документация Майкрософт
author: rick-anderson
description: В предыдущих руководствах мы использовали элемент управления GridView для вывода данных. Начиная с этого руководства мы рассмотрим создание общих шаблонов отчетов с помощью...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 0591cacc-b34b-4cf6-885e-2c9953bb0946
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 09d3faf811f21a66bb5c234f71d77b2552ae6516
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78495750"
---
# <a name="displaying-data-with-the-datalist-and-repeater-controls-c"></a>Отображение данных с помощью элементов управления DataList и Repeater (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_CS.exe) или [Загрузка PDF-файла](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/datatutorial29cs1.pdf)

> В предыдущих руководствах мы использовали элемент управления GridView для вывода данных. Начиная с этого руководства мы рассмотрим создание общих шаблонов отчетов с помощью элементов управления DataList и Repeater, начиная с основ отображения данных с помощью этих элементов управления.

## <a name="introduction"></a>Введение

Во всех примерах за последние 28 учебников, если нам требовалось отобразить несколько записей из источника данных, который мы включили в элемент управления GridView. Элемент управления GridView отображает строку для каждой записи в источнике данных, отображая поля данных записей в столбцах. Хотя GridView делает его привязкой для отображения, постраничного просмотра, сортировки, редактирования и удаления данных, его внешний вид является угловат. Кроме того, разметка, ответственная за структуру GridView s, является фиксированной, она включает HTML-`<table>` со строкой таблицы (`<tr>`) для каждой записи и ячейку таблицы (`<td>`) для каждого поля.

Чтобы обеспечить большую степень настройки в виде и визуализации разметки при отображении нескольких записей, ASP.NET 2,0 предлагает элементы управления DataList и Repeater (оба из них также доступны в ASP.NET версии 1. x). Элементы управления DataList и Repeater визуализируют свое содержимое с помощью шаблонов, а не BoundFields, Чеккбоксфиелдс, Буттонфиелдс и т. д. Как и GridView, DataList отображается как HTML-`<table>`, но позволяет отображать несколько записей источников данных для каждой строки таблицы. С другой стороны, элемент управления Repeater не отображает дополнительную разметку, чем то, что вы явно указали, и является идеальным кандидатом, когда требуется точный контроль над порожденной разметкой.

В течение следующих десятков материалов или инструкций мы рассмотрим создание общих шаблонов отчетов с помощью элементов управления DataList и Repeater, начиная с основ отображения данных с помощью этих шаблонов элементов управления. Мы покажем, как форматировать эти элементы управления, изменять макет записей источников данных в DataList, общие сценарии с основными и подробными сведениями, способы изменения и удаления данных, пролистывать записи и т. д.

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>Шаг 1. Добавление веб-страниц учебника по DataList и Repeater

Прежде чем приступить к работе с этим руководством, давайте сначала добавим страницы ASP.NET, которые понадобятся для работы с этим руководством, и несколько руководств, посвященных отображению данных с помощью элементов управления DataList и Repeater. Начните с создания новой папки в проекте с именем `DataListRepeaterBasics`. Затем добавьте в эту папку следующие пять страниц ASP.NET, чтобы все они были настроены для использования главной страницы `Site.master`:

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`

![Создание папки DataListRepeaterBasics и добавление страниц Tutorial ASP.NET](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image1.png)

**Рис. 1**. Создание `DataListRepeaterBasics` папки и добавление страниц Tutorial ASP.NET

Откройте страницу `Default.aspx` и перетащите `SectionLevelTutorialListing.ascx` пользовательский элемент управления из папки `UserControls` в область конструктора. Этот пользовательский элемент управления, созданный в учебнике « [главные страницы и Навигация по узлу](../introduction/master-pages-and-site-navigation-cs.md) », перечисляет карту узла и отображает учебники из текущего раздела в маркированном списке.

[![добавить пользовательский элемент управления SectionLevelTutorialListing. ascx в Default. aspx](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image2.png)

**Рис. 2**. Добавление пользовательского элемента управления `SectionLevelTutorialListing.ascx` в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image4.png))

Чтобы в маркированном списке отображались учебники по DataList и Repeater, которые будут созданы, необходимо добавить их на карту узла. Откройте файл `Web.sitemap` и добавьте следующую разметку после разметки узла карт узла "Добавление настраиваемых кнопок":

[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample1.xml)]

![Обновление схемы узла для включения новых страниц ASP.NET](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image5.png)

**Рис. 3**. обновление схемы узла для включения новых страниц ASP.NET

## <a name="step-2-displaying-product-information-with-the-datalist"></a>Шаг 2. Отображение сведений о продукте с помощью элемента управления DataList

Как и в FormView, выходные данные элемента управления DataList зависят от шаблонов, а не от BoundFields, Чеккбоксфиелдс и т. д. В отличие от FormView, DataList предназначен для показа набора записей, а не одиночные. Давайте начнем с этого руководства и взглянем на то, как привязать сведения о продукте к DataList. Для начала откройте страницу `Basics.aspx` в папке `DataListRepeaterBasics`. Затем перетащите элемент управления DataList с панели элементов в конструктор. Как показано на рис. 4, прежде чем указывать шаблоны DataList, конструктор отображает его в виде серого прямоугольника.

[![перетащить элемент управления DataList с панели элементов в конструктор](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image6.png)

**Рис. 4**. Перетаскивание элемента управления DataList из панели элементов в конструктор ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image8.png))

Из смарт-тега DataList добавьте новый элемент ObjectDataSource и настройте его на использование метода `GetProducts` `ProductsBLL` класса. Так как в этом руководстве мы воссоздадим список DataList только для чтения, установите в раскрывающемся списке значение (нет) на вкладках Вставка, обновление и удаление мастера.

[![выбрать создание нового элемента управления ObjectDataSource](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image9.png)

**Рис. 5**. Создание нового элемента управления ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image11.png))

[![настроить ObjectDataSource для использования класса ProductsBLL](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image12.png)

**Рис. 6**. Настройка ObjectDataSource для использования класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image14.png))

[![получить сведения обо всех продуктах с помощью метода Products](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image15.png)

**Рис. 7**. Получение сведений обо всех продуктах с помощью метода `GetProducts` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image17.png))

После настройки ObjectDataSource и связывания его с элементом управления DataList через его смарт-тег Visual Studio автоматически создаст в DataList `ItemTemplate`, отображающий имя и значение каждого поля данных, возвращаемого источником данных (см. разметку ниже). Этот вид `ItemTemplate` по умолчанию аналогичен шаблонам, автоматически создаваемым при привязке источника данных к FormView через конструктор.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample2.aspx)]

> [!NOTE]
> Помните, что при привязке источника данных к элементу управления FormView через смарт-тег FormView s Visual Studio создает `ItemTemplate`, `InsertItemTemplate`и `EditItemTemplate`. Однако с элементом управления DataList создается только `ItemTemplate`. Это связано с тем, что элемент управления DataList не имеет такой же встроенной поддержки правки и вставки, которая предоставляется FormView. Элемент управления DataList содержит события, связанные с редактированием и удалением, а также поддержку редактирования и удаления, которую можно добавить с помощью фрагмента кода, но нет простой встроенной поддержки, как в элементе управления FormView. В следующем учебнике мы покажем, как включить поддержку редактирования и удаления элементов управления DataList.

Подождите немного, чтобы улучшить внешний вид этого шаблона. Вместо того чтобы отображать все поля данных, добавим в s только название продукта, поставщик, категорию, количество на единицу и цену за единицу. Кроме того, давайте отображаем имя в заголовке `<h4>` и разметьте оставшиеся поля, используя `<table>` под заголовком.

Чтобы внести эти изменения, можно использовать функции редактирования шаблонов в конструкторе из смарт-тега DataList, щелкнуть ссылку изменить шаблоны или изменить шаблон вручную с помощью декларативного синтаксиса Pages. При использовании параметра изменить шаблоны в конструкторе полученная разметка может не соответствовать следующей разметке точно, но при просмотре в браузере он очень похож на снимок экрана, показанный на рис. 8.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample3.aspx)]

> [!NOTE]
> В приведенном выше примере используются элементы управления Label, которым свойству `Text` присвоено значение синтаксиса DataBinding. Кроме того, можно полностью опустить метки, вводя только синтаксис привязки данных. То есть вместо использования `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />` можно было бы использовать декларативный синтаксис `<%# Eval("CategoryName") %>`.

Однако при этом в веб-элементах управления Label предусмотрено два преимущества. Во первых, он предоставляет более простые средства для форматирования данных на основе данных, как будет показано в следующем руководстве. Во-вторых, параметр Edit Templates (редактирование шаблонов) в конструкторе не отображает декларативный синтаксис привязки данных, который появляется за пределами определенного элемента управления. Вместо этого интерфейс Edit Templates разработан для упрощения работы со статической разметкой и веб-элементами управления и предполагает, что все привязки данных будут выполняться с помощью диалогового окна Изменение привязок, доступного из смарт-тегов Web Controls.

Таким образом, при работе с элементом управления DataList, который предоставляет возможность редактирования шаблонов с помощью конструктора, я предпочитаю использовать элементы Web Controls Label, чтобы содержимое было доступно через интерфейс редактирование шаблонов. Как мы увидим чуть ниже, Repeater требует, чтобы содержимое шаблона было изменено из представления исходного кода. Следовательно, при создании шаблонов Repeater мы часто будем опускать метки Web Controls, если не знать, что нужно отформатировать текст, привязанный к данным, на основе программной логики.

[![каждый из выходных данных продукта отображается с помощью DataList s ItemTemplate](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image18.png)

**Рис. 8**. выходные данные каждого продукта отображаются с помощью `ItemTemplate` DataList s ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image20.png))

## <a name="step-3-improving-the-appearance-of-the-datalist"></a>Шаг 3. улучшение внешнего вида элемента управления DataList

Как и GridView, DataList предлагает ряд свойств, связанных со стилем, таких как `Font`, `ForeColor`, `BackColor`, `CssClass`, `ItemStyle`, `AlternatingItemStyle`, `SelectedItemStyle`и т. д. При работе с элементами управления GridView и DetailsView мы создали файлы обложки в теме `DataWebControls`, в которой заранее определены свойства `CssClass` для этих двух элементов управления и свойство `CssClass` для некоторых их вложенных свойств (`RowStyle`, `HeaderStyle`и т. д.). Позвольте s сделать то же самое для DataList.

Как обсуждалось в разделе [Отображение данных с помощью элемента управления ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) , в файле обложки задаются свойства, связанные с внешним видом по умолчанию для веб-элемента. Тема — это коллекция файлов Skin, CSS, Image и JavaScript, которые определяют конкретный внешний вид веб-сайта. При *отображении данных с помощью* учебника по ObjectDataSource мы создали тему `DataWebControls` (которая реализована в виде папки в папке `App_Themes`), в которой в настоящее время есть два файла обложки — `GridView.skin` и `DetailsView.skin`. Добавим третий файл обложки, чтобы указать предварительно определенные параметры стиля для DataList.

Чтобы добавить файл обложки, щелкните правой кнопкой мыши папку `App_Themes/DataWebControls`, выберите пункт Добавить новый элемент и выберите в списке параметр файл обложки. Назовите файл `DataList.skin`.

[![создать новый файл обложки с именем DataList. Skin](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image21.png)

**Рис. 9**. Создание нового файла обложки с именем `DataList.skin` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image23.png))

Используйте следующую разметку для файла `DataList.skin`:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample4.aspx)]

Эти параметры применяют те же классы CSS к соответствующим свойствам DataList, что использовались с элементами управления GridView и DetailsView. Используемые здесь классы CSS `DataWebControlStyle`, `AlternatingRowStyle`, `RowStyle`и т. д. определяются в файле `Styles.css` и были добавлены в предыдущих учебных курсах.

При добавлении этого файла обложки внешний вид DataList обновляется в конструкторе (для просмотра эффектов нового файла обложки может потребоваться обновить представление конструктора). в меню "вид" выберите команду "Обновить". Как показано на рис. 10, каждый чередующийся продукт имеет светло-розовый цвет фона.

[![создать новый файл обложки с именем DataList. Skin](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image24.png)

**Рис. 10**. Создание нового файла обложки с именем `DataList.skin` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image26.png))

## <a name="step-4-exploring-the-datalist-s-other-templates"></a>Шаг 4. изучение DataList s другие шаблоны

Помимо `ItemTemplate`, DataList поддерживает шесть других необязательных шаблонов:

- `HeaderTemplate` если указано, добавляет строку заголовка к выходным данным и используется для визуализации этой строки.
- `AlternatingItemTemplate`, используемый для визуализации чередующихся элементов
- `SelectedItemTemplate`, используемый для отрисовки выбранного элемента; выбранный элемент является элементом, индекс которого соответствует [свойству`SelectedIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx) DataList s
- `EditItemTemplate`, используемый для визуализации редактируемого элемента
- `SeparatorTemplate`, если он указан, добавляет разделитель между каждым элементом и используется для отображения этого разделителя.
- `FooterTemplate` — если предоставлено, добавляет к выходу строку нижнего колонтитула и используется для визуализации этой строки.

При указании `HeaderTemplate` или `FooterTemplate`DataList добавляет дополнительную строку верхнего или нижнего колонтитула в отображаемые выходные данные. Как и в случае с заголовками и нижними колонтитулами GridView s, верхний и нижний колонтитулы в DataList не привязаны к данным. Таким образом, любой синтаксис привязки данных в `HeaderTemplate` или `FooterTemplate`, пытающийся получить доступ к привязанным данным, вернет пустую строку.

> [!NOTE]
> Как было показано в статье [Отображение сводных данных в нижнем колонтитуле GridView s](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md) , в то время как строки верхнего и нижнего колонтитула не поддерживают синтаксис привязки данных, сведения, относящиеся к данным, могут быть добавлены непосредственно в эти строки из обработчика `RowDataBound` GridView s. Этот метод можно использовать для вычисления текущих итогов или другой информации из данных, привязанных к элементу управления, а также для назначения этих сведений нижнему колонтитулу. Эта же концепция может применяться к элементам управления DataList и Repeater; Единственное различие заключается в том, что для элементов управления DataList и Repeater создается обработчик событий `ItemDataBound` события (вместо события `RowDataBound`).

В нашем примере пусть в верхней части списка DataList отображаются сведения о продукте, заголовком `<h3>`. Для этого добавьте `HeaderTemplate` с соответствующей разметкой. В конструкторе это можно сделать, щелкнув ссылку изменить шаблоны в смарт-теге DataList, выбрав шаблон заголовка из раскрывающегося списка и введя текст в раскрывающемся списке стиль (см. рис. 11).

[![добавить HeaderTemplate с текстовыми сведениями о продукте](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image27.png)

**Рис. 11**. Добавление `HeaderTemplate` со сведениями о продукте ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image29.png))

Кроме того, это можно добавить декларативно, введя следующую разметку в теги `<asp:DataList>`:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample5.html)]

Чтобы добавить в список продуктов несколько пробелов, добавим `SeparatorTemplate`, включающую линию между каждым разделом. Тег горизонтального правила (`<hr>`) добавляет такой разделитель. Создайте `SeparatorTemplate` так, чтобы он наработал следующую разметку:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample6.html)]

> [!NOTE]
> Как и `HeaderTemplate` и `FooterTemplates`, `SeparatorTemplate` не привязана к какой-либо записи из источника данных и поэтому не может напрямую обращаться к записям источников данных, привязанным к DataList.

После выполнения этого сложения при просмотре страницы в браузере она должна выглядеть примерно так, как показано на рис. 12. Обратите внимание на строку заголовка и строку между каждым списком продуктов.

[![DataList включает строку заголовка и горизонтальное правило между каждым списком продуктов.](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image30.png)

**Рис. 12**. элемент управления DataList содержит строку заголовка и горизонтальное правило между каждым списком продуктов ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image32.png)).

## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>Шаг 5. отрисовка определенной разметки с помощью элемента управления Repeater

Если вы выполняете представление или источник из браузера при просмотре примера DataList на рис. 12, вы увидите, что DataList выдает `<table>` HTML, содержащий строку таблицы (`<tr>`) с одной ячейкой таблицы (`<td>`) для каждого элемента, привязанного к DataList. На самом деле эти выходные данные идентичны тому, что получится из GridView с одним TemplateField. Как можно будет увидеть в следующем учебном курсе, DataList допускает дальнейшую настройку выходных данных, позволяя нам отображать несколько записей источников данных в каждой строке таблицы.

Но если вы не хотите создавать HTML-`<table>`? Для общего и полного управления разметкой, создаваемой веб-элементом управления данными, необходимо использовать элемент управления Repeater. Как и в DataList, элемент управления Repeater создается на основе шаблонов. Однако Repeater предлагает только следующие пять шаблонов:

- `HeaderTemplate` если предоставлено, добавляет указанную разметку перед элементами.
- `ItemTemplate`, используемые для отрисовки элементов
- `AlternatingItemTemplate`, если он задан, используется для визуализации чередующихся элементов
- `SeparatorTemplate`, если оно предоставлено, добавляет указанную разметку между каждым элементом.
- `FooterTemplate` — если предоставлено, добавляет указанную разметку после элементов.

В ASP.NET 1. x элемент управления Repeater обычно использовался для вывода маркированного списка, данные которого получены из источника данных. В этом случае `HeaderTemplate` и `FooterTemplates` будут содержать открывающие и закрывающие теги `<ul>` соответственно, а `ItemTemplate` будет содержать элементы `<li>` с синтаксисом DataBinding. Этот подход по-прежнему можно использовать в ASP.NET 2,0, как мы видели в двух примерах на [главных страницах и](../introduction/master-pages-and-site-navigation-cs.md) в учебнике по переходу на сайт.

- На главной странице `Site.master` используется Repeater для отображения маркированного списка содержимого карт узла верхнего уровня (базовый отчет, фильтрация отчетов, настраиваемое форматирование и т. д.). другой вложенный элемент Repeater использовался для вывода дочерних разделов разделов верхнего уровня.
- В `SectionLevelTutorialListing.ascx`для отображения маркированного списка дочерних разделов текущего раздела схемы веб-узла используется элемент Repeater.

> [!NOTE]
> В ASP.NET 2,0 появился новый [элемент управления "маркированный](https://msdn.microsoft.com/library/ms228101.aspx)", который можно привязать к элементу управления источником данных, чтобы отобразить простой маркированный список. При использовании элемента управления маркированными списками не нужно указывать ни один из HTML-страниц, связанных со списком; Вместо этого мы просто обозначаем поле данных, которое будет отображаться как текст для каждого элемента списка.

Repeater служит в качестве веб-элемента управления для перехвата всех данных. Если существующего элемента управления, создающего необходимую разметку, не существует, можно использовать элемент управления Repeater. Чтобы проиллюстрировать использование элемента управления Repeater, давайте, чтобы список категорий отображался над элементом управления DataList, созданным на шаге 2. В частности, пусть категории отображаются в HTML-`<table>` одной строки с каждой категорией, отображаемой в виде столбца в таблице.

Чтобы сделать это, начните с перетаскивания элемента управления Repeater с панели инструментов в конструктор над элементом DataList сведений о продукте. Как и в элементе управления DataList, элемент управления Repeater первоначально отображается как серый прямоугольник, пока его шаблоны не определены.

[![Добавление элемента Repeater в конструктор](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image33.png)

**Рис. 13**. Добавление элемента Repeater в конструктор ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image35.png))

В смарт-теге Repeater s есть только один параметр: выберите источник данных. Необходимо создать новый элемент ObjectDataSource и настроить его для использования метода `GetCategories` `CategoriesBLL` класса.

[![создать новый элемент управления ObjectDataSource](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image36.png)

**Рис. 14**. Создание нового элемента управления ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image38.png))

[![настроить ObjectDataSource для использования класса CategoriesBLL](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image39.png)

**Рис. 15**. Настройка ObjectDataSource для использования класса `CategoriesBLL` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image41.png))

[![получить сведения обо всех категориях с помощью метода Categories](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image42.png)

**Рис. 16**. Получение сведений обо всех категориях с помощью метода `GetCategories` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image44.png))

В отличие от DataList, Visual Studio не создает ItemTemplate автоматически для элемента управления Repeater после его привязки к источнику данных. Более того, шаблоны Repeater не могут быть настроены с помощью конструктора и должны быть заданы декларативно.

Чтобы отобразить категории в виде однострочного `<table>` со столбцом для каждой категории, нам нужен элемент Repeater для создания разметки, аналогичной следующей:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample7.html)]

Так как текст `<td>Category X</td>` — это повторяющаяся часть, она появится в элементе Repeater s ItemTemplate. Разметка, которая появляется перед `<table><tr>`, будет помещена в `HeaderTemplate`, а конечная разметка `</tr></table>` — помещается в `FooterTemplate`. Чтобы ввести эти параметры шаблона, перейдите к декларативной части страницы ASP.NET, нажав кнопку Источник в левом нижнем углу и введя следующий синтаксис:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample8.aspx)]

Элемент Repeater создает точную разметку, указанную в шаблонах, ничего больше, ничего не меньше. На рис. 17 показан вывод данных Repeater при просмотре в браузере.

[![&lt;таблице HTML с одной строкой&gt; список каждой категории в отдельном столбце](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image45.png)

**Рис. 17**. HTML-`<table>` одной строки содержит каждую категорию в отдельном столбце ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image47.png))

## <a name="step-6-improving-the-appearance-of-the-repeater"></a>Шаг 6. улучшение внешнего вида элемента Repeater

Так как Repeater создает точную разметку, указанную в шаблонах, она должна не задуматься о том, что для Repeater нет свойств, связанных с стилем. Чтобы изменить внешний вид содержимого, созданного Repeater, необходимо вручную добавить требуемое содержимое HTML или CSS непосредственно в шаблоны Repeater s.

В нашем примере пусть столбцы категории имеют альтернативные цвета фона, например с чередованием строк в DataList. Для этого необходимо присвоить `RowStyle` классу CSS каждому элементу Repeater и классу `AlternatingRowStyle` CSS к каждому альтернативному элементу Repeater с помощью шаблонов `ItemTemplate` и `AlternatingItemTemplate`, вот так:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample9.aspx)]

Давайте также добавим к выходу строку заголовка с использованием текстовых категорий продуктов. Поскольку мы не понимаем, сколько столбцов будет состоять в итоговой `<table>`, самый простой способ создать строку заголовка, которая гарантированно охватывает все столбцы, — использовать *две* `<table>` s. Первая `<table>` будет содержать две строки заголовка и строку, которая будет содержать вторую однострочную `<table>` со столбцом для каждой категории в системе. То есть мы хотим создать следующую разметку:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample10.html)]

Следующие `HeaderTemplate` и `FooterTemplate` приводят к желаемой разметке:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample11.aspx)]

На рис. 18 показан элемент Repeater после внесения этих изменений.

[![столбцы категорий в альтернативном цвете и включает строку заголовка](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image48.png)

**Рис. 18**. столбцы категорий, которые относятся к цвету фона и включают строку заголовка ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image50.png))

## <a name="summary"></a>Сводка

Хотя элемент управления GridView упрощает отображение, изменение, удаление, сортировку и детализацию данных, внешний вид является очень угловатным и в виде сетки. Чтобы лучше контролировать внешний вид, необходимо включить элементы управления DataList или Repeater. Оба этих элемента управления отображают набор записей с помощью шаблонов вместо BoundFields, Чеккбоксфиелдс и т. д.

Элемент управления DataList готовится к просмотру как `<table>` HTML, который по умолчанию отображает каждую запись источника данных в одной строке таблицы, как и GridView с одним TemplateField. Как мы увидим в следующем учебном курсе, элемент управления DataList позволяет отображать несколько записей в каждой строке таблицы. С другой стороны, Repeater строго создает разметку, указанную в ее шаблонах. Он не добавляет дополнительную разметку и, таким образом, обычно используется для вывода данных в HTML-элементах, отличных от `<table>` (например, в маркированном списке).

Хотя элементы управления DataList и Repeater обеспечивают большую гибкость в отображаемых выходных данных, у них нет многих встроенных функций, имеющихся в GridView. Как мы рассмотрим в предстоящих руководствах, некоторые из этих функций могут быть подключены обратно, не требуя слишком больших усилий, но при этом следует помнить, что использование DataList или Repeater вместо GridView ограничивает возможности, которые можно использовать без реализации этих функций. степень.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого руководства: Яааков yaakov Ellis), основными рецензентами, Рэнди Шмидт и Стейси парк. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Дальше](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
