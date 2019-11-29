---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs
title: "\"Основной/подробности\" с помощью маркированного списка главных записей с элементом управления DataListC#() | Документация Майкрософт"
author: rick-anderson
description: В этом учебнике мы будем сжимать отчет «основной/подробности» из предыдущего руководства на одну страницу, отображая маркированный список имен категорий на t...
ms.author: riande
ms.date: 10/17/2006
ms.assetid: c727bb73-7b59-41a1-8dc3-623c6d69e7c2
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 4549ab8e64599b09c300c158bedfd5d85efafc4d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591872"
---
# <a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-c"></a>Отчет "Основной/подробности" с использованием маркированного списка основных записей с элементом управления DataList для подробных сведений (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_CS.exe) или [Загрузка PDF-файла](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/datatutorial35cs1.pdf)

> В этом учебнике мы будем сжимать отчет «основной/подробности» из предыдущего руководства на одну страницу, отображая маркированный список имен категорий в левой части экрана и продукты выбранной категории в правой части экрана.

## <a name="introduction"></a>Введение

В [предыдущем учебном курсе](master-detail-filtering-acess-two-pages-datalist-cs.md) мы рассматривали разделение отчета «основной/подробности» на две страницы. На главной странице мы использовали элемент управления Repeater для отображения маркированного списка категорий. Имя каждой категории было гиперссылкой, при щелчке которого пользователь перейдет на страницу сведений, где в DataList отображались продукты, принадлежащие выбранной категории.

В этом учебнике мы будем сжимать учебник с двумя страницами на одной странице, отображая маркированный список имен категорий в левой части экрана с именами категорий, отображаемыми как LinkButton. Щелкнув одну из категорий LinkButton, можно выполнить обратную передачу и привязать продукты выбранной категории к элементу DataList с двумя столбцами справа от экрана. В дополнение к отображению каждого имени категории, в элементе Repeater слева отображается общее количество продуктов для данной категории (см. рис. 1).

[![имя категории s и общее количество продуктов отображаются слева](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image1.png)

**Рис. 1**. имя категории и общее количество продуктов отображаются слева ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image3.png))

## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>Шаг 1. Отображение элемента Repeater в левой части экрана

Для работы с этим руководством необходимо, чтобы маркированный список категорий отображался слева от выбранных продуктов категории s. Содержимое на веб-странице может быть размещено с помощью стандартных тегов абзацев, неразрывных пробелов, `<table>` s и т. д. или с помощью методов каскадной таблицы стилей (CSS). Во всех наших руководствах мы использовали методы CSS для позиционирования. При построении пользовательского интерфейса навигации на главной странице в учебном курсе [главные страницы и Навигация по сайту](../introduction/master-pages-and-site-navigation-cs.md) было использовано *абсолютное позиционирование*, указывающее точное смещение пикселя для списка переходов и основное содержимое. Кроме того, CSS можно использовать для размещения одного элемента справа или слева от другого до *плавающего*. Можно отобразить маркированный список категорий слева от выбранных продуктов категории s, перечисляя элемент управления Repeater слева от элемента управления DataList.

Откройте страницу `CategoriesAndProducts.aspx` из папки `DataListRepeaterFiltering` и добавьте ее на страницу a Repeater и DataList. Задайте для параметра Repeater s `ID` значение `Categories`, а для элемента DataList s — значение `CategoryProducts`. Перейдите в представление исходного кода и помещайте элементы управления Repeater и DataList в свои элементы `<div>`. То есть сначала заключите элемент управления Repeater внутрь элемента `<div>`, а затем элемент управления DataList в своем собственном элементе `<div>` непосредственно после элемента управления Repeater. Разметка на этом этапе должна выглядеть следующим образом:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample1.aspx)]

Чтобы переместить элемент управления Repeater на левую часть DataList, необходимо использовать атрибут стиля CSS `float`, вот так:

[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample2.html)]

`float: left;` перемещает первый элемент `<div>` влево от второго. Параметры `width` и `padding-right` указывают первый `<div>` `width` и то, сколько дополнений добавляется между содержимым `<div>` элемента и его правым полем. Дополнительные сведения об плавающих элементах CSS см. в [флоатуториал](http://css.maxdesign.com.au/floatutorial/).

Вместо того, чтобы задавать стиль непосредственно через первый `<p>` элемент `style` атрибут, давайте создадим новый класс CSS в `Styles.css` с именем `FloatLeft`:

[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample3.css)]

Затем можно заменить `<div>` `<div class="FloatLeft">`.

После добавления класса CSS и настройки разметки на странице `CategoriesAndProducts.aspx` перейдите в конструктор. Элемент управления Repeater должен быть плавающим слева от элемента управления DataList (хотя теперь он отображается серым цветом, так как мы еще не настроили их источники данных или шаблоны).

[![элемент управления Repeater находится слева от DataList](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image4.png)

**Рис. 2**. элемент управления Repeater находится слева от элемента управления DataList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image6.png))

## <a name="step-2-determining-the-number-of-products-for-each-category"></a>Шаг 2. Определение количества продуктов для каждой категории

После завершения разметки Repeater и DataList мы повторно готовы привязать данные категорий к элементу управления Repeater. Однако, как показано в маркированном списке категорий на рис. 1, в дополнение к именам категорий s также необходимо отобразить количество продуктов, связанных с категорией. Чтобы получить доступ к этим сведениям, можно выполнить одно из следующих действий:

- **Определите эти сведения на основе класса кода программной части ASP.NET Page s.** Учитывая конкретную *`categoryID`* мы можем определить количество связанных продуктов, вызвав метод `ProductsBLL` класса s `GetProductsByCategoryID(categoryID)`. Этот метод возвращает объект `ProductsDataTable`, свойство `Count` которого показывает, сколько `ProductsRow` существует, что представляет собой количество продуктов для указанного *`categoryID`* . Можно создать обработчик событий `ItemDataBound` для элемента Repeater, который для каждой категории, привязанной к элементу Repeater, вызывает метод `ProductsBLL` класса s `GetProductsByCategoryID(categoryID)` и включает его количество в выходных данных.
- **Обновите `CategoriesDataTable` в типизированном наборе данных, чтобы включить столбец `NumberOfProducts`.** Затем можно обновить метод `GetCategories()` в `CategoriesDataTable`, чтобы включить эти сведения, или же оставить `GetCategories()` "как есть" и создать новый метод `CategoriesDataTable` с именем `GetCategoriesAndNumberOfProducts()`.

Давайте рассмотрим оба этих метода. Первый подход проще реализовать, так как нам не нужно обновлять уровень доступа к данным. Однако для этого требуется больше связи с базой данных. Вызов метода `ProductsBLL` класса `GetProductsByCategoryID(categoryID)` в обработчике событий `ItemDataBound` добавляет дополнительный вызов базы данных для каждой категории, отображаемой в элементе Repeater. При использовании этого метода существует *n* + 1 вызовов баз данных, где *n* — число категорий, отображаемых в элементе Repeater. При втором подходе возвращается число продуктов со сведениями о каждой категории из метода `CategoriesBLL` класса s `GetCategories()` (или `GetCategoriesAndNumberOfProducts()`), что приводит к простому обращению к базе данных.

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>Определение количества продуктов в обработчике событий ItemDataBound

Для определения количества продуктов для каждой категории в обработчике событий Repeater `ItemDataBound` не требуется вносить изменения в имеющийся уровень доступа к данным. Все изменения можно вносить непосредственно на странице `CategoriesAndProducts.aspx`. Начните с добавления нового элемента управления ObjectDataSource с именем `CategoriesDataSource` через смарт-тег Repeater s. Затем настройте `CategoriesDataSource` ObjectDataSource таким образом, чтобы он получал свои данные из метода `CategoriesBLL` класса s `GetCategories()`.

[![настроить ObjectDataSource для использования метода класса CategoriesBLL-Categories ()](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image7.png)

**Рис. 3**. Настройка ObjectDataSource для использования метода `GetCategories()` `CategoriesBLL` классов ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image9.png))

Каждый элемент в `Categories` Repeater должен быть щелчком мыши, и при нажатии `CategoryProducts` DataList отображает эти продукты для выбранной категории. Это можно сделать, сделав каждую категорию гиперссылкой, связав ее с той же страницей (`CategoriesAndProducts.aspx`), но передавая `CategoryID` через строку запроса, как показано в предыдущем руководстве. Преимуществом этого подхода является то, что страница, отображающая определенные продукты категории, может быть помечена и проиндексирована поисковой системой.

Кроме того, можно создать каждую категорию с помощью элемента LinkButton, который мы будем использовать для работы с этим руководством. Элемент LinkButton отображается в браузере User s как гиперссылка, но при щелчке вызывает обратную передачу; при обратной передаче необходимо обновить элемент управления DataList, чтобы отобразить продукты, принадлежащие выбранной категории. В этом учебнике использование гиперссылки имеет больше смысла, чем использование элемента LinkButton; Однако могут существовать и другие сценарии, в которых использование элемента LinkButton является более выгодным. Хотя подход гиперссылки идеально подходит для этого примера, давайте рассмотрим использование LinkButton. Как мы увидим, использование LinkButton вводит некоторые проблемы, которые в противном случае не будут возникать с гиперссылкой. Поэтому использование элемента LinkButton в этом учебнике выделит эти проблемы и предоставит решения для тех сценариев, в которых вместо гиперссылки может потребоваться использовать элемент LinkButton.

> [!NOTE]
> Рекомендуется повторить этот учебник, используя элемент управления HyperLink или элемент `<a>` вместо элемента LinkButton.

В следующей разметке показан декларативный синтаксис для элемента управления Repeater и ObjectDataSource. Обратите внимание, что шаблоны Repeater дорабатывают маркированный список с каждым элементом как LinkButton:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample4.aspx)]

> [!NOTE]
> В этом учебнике для элемента Repeater должно быть включено состояние просмотра (Обратите внимание на упущение `EnableViewState="False"` из декларативного синтаксиса Repeater). На этапе 3 мы создадим обработчик событий для события Repeater `ItemCommand`, в котором мы будем обновлять коллекцию коллекций ObjectDataSource s `SelectParameters`. Однако `ItemCommand`Repeater не будет срабатывать, если состояние представления отключено. Дополнительные сведения о том, почему должно быть включено состояние просмотра `ItemCommand` для запуска события Repeater, см. [в разделе головоломка ASP.NET вопроса](http://scottonwriting.net/sowblog/posts/1263.aspx) и [его решения](http://scottonwriting.net/sowBlog/posts/1268.aspx) .

Свойство LinkButton со значением свойства `ID` `ViewCategory` не имеет установленного свойства `Text`. Если бы было просто отображалось имя категории, свойство Text было бы задано декларативно с помощью синтаксиса DataBinding следующим образом:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample5.aspx)]

Однако мы хотим отобразить как имя категории, так *и* число продуктов, принадлежащих этой категории. Эти сведения можно получить из обработчика событий Repeater `ItemDataBound`, сделав вызов метода `ProductBLL` класса s `GetCategoriesByProductID(categoryID)` и определив, сколько записей возвращается в результате `ProductsDataTable`, как показано в следующем коде:

[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample6.cs)]

Начнем с того, что мы работаем над тем, чтобы мы переработали элемент данных (один из которых `ItemType` `Item` или `AlternatingItem`), а затем сослаться на экземпляр `CategoriesRow`, который только что был привязан к текущему `RepeaterItem`. Далее мы определяем количество продуктов для этой категории путем создания экземпляра класса `ProductsBLL`, вызова его метода `GetCategoriesByProductID(categoryID)` и определения количества записей, возвращаемых с помощью свойства `Count`. Наконец, `ViewCategory` LinkButton в ItemTemplate является ссылкой, а свойство `Text` имеет значение *CategoryName* (*нумберофпродуктсинкатегори*), где *нумберофпродуктсинкатегори* отформатировано как число с нулевыми десятичными разрядами.

> [!NOTE]
> Кроме того, мы могли бы добавить *функцию форматирования* в класс кода программной части ASP.NET Page s, который принимает категории s `CategoryName` и `CategoryID` значения и возвращает `CategoryName` сцепление с числом продуктов в категории (как определено вызовом метода `GetCategoriesByProductID(categoryID)`). Результаты такой функции форматирования можно декларативно назначить свойству "текст" в LinkButton, заменив потребность в обработчике событий `ItemDataBound`. Дополнительные сведения об использовании функций форматирования см. в разделе [Использование полей TemplateField в элементе управления GridView](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) или при [форматировании элементов DataList и Repeater на основе](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md) учебников по работе с данными.

После добавления этого обработчика событий протестируйте страницу в браузере. Обратите внимание, что каждая категория указана в маркированном списке, отображая название категории s и число продуктов, связанных с категорией (см. рис. 4).

[![отображаются имена и количество продуктов категории s](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image10.png)

**Рис. 4**. отображаются имена и количество продуктов каждой категории ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image12.png)).

## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>Обновление`CategoriesDataTable`и`CategoriesTableAdapter`для включения числа продуктов для каждой категории

Вместо того чтобы определять количество продуктов для каждой категории в качестве привязки к Repeater, мы можем упростить этот процесс, настроив `CategoriesDataTable` и `CategoriesTableAdapter` на уровне доступа к данным, чтобы включить эти сведения в исходный код. Для этого необходимо добавить новый столбец для `CategoriesDataTable` для хранения количества связанных продуктов. Чтобы добавить новый столбец к DataTable, откройте типизированный набор данных (`App_Code\DAL\Northwind.xsd`), щелкните правой кнопкой мыши таблицу данных, которую нужно изменить, и выберите Добавить/столбец. Добавьте новый столбец в `CategoriesDataTable` (см. рис. 5).

[![добавить новый столбец в CategoriesDataSource](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image13.png)

**Рис. 5**. Добавление нового столбца в `CategoriesDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image15.png))

При этом будет добавлен новый столбец с именем `Column1`, который можно изменить, просто введя другое имя. Переименуйте этот новый столбец в `NumberOfProducts`. Далее необходимо настроить свойства этого столбца. Щелкните новый столбец и перейдите к окно свойств. Измените свойство `DataType` столбцов с `System.String` на `System.Int32` и задайте для свойства `ReadOnly` значение `True`, как показано на рис. 6.

![Установка свойств DataType и ReadOnly нового столбца](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image16.png)

**Рис. 6**. задание свойств `DataType` и `ReadOnly` нового столбца

Хотя `CategoriesDataTable` теперь содержит столбец `NumberOfProducts`, его значение не задается ни одним из запросов TableAdapter s. Мы можем обновить метод `GetCategories()`, чтобы получить эти сведения, если требуется, чтобы эти сведения возвращались при каждой получении сведений о категории. Однако в редких случаях нам нужно только извлечь количество связанных продуктов для категорий (например, просто для этого руководства), а затем оставить `GetCategories()` "как есть" и создать новый метод, возвращающий эту информацию. Давайте будем использовать этот подход, создавая новый метод с именем `GetCategoriesAndNumberOfProducts()`.

Чтобы добавить этот новый метод `GetCategoriesAndNumberOfProducts()`, щелкните правой кнопкой мыши `CategoriesTableAdapter` и выберите Создать запрос. Откроется мастер настройки запросов адаптера таблицы TableAdapter, который мы использовали несколько раз в предыдущих руководствах. Для этого метода запустите мастер, указав, что запрос использует специальный оператор SQL, возвращающий строки.

[![создать метод с помощью специального оператора SQL](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image17.png)

**Рис. 7**. Создание метода с помощью специального оператора SQL ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image19.png))

[![инструкция SQL возвращает строки](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image20.png)

**Рис. 8**. Инструкция SQL возвращает строки ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image22.png))

На следующем экране мастера запрашивается запрос на использование. Чтобы вернуть каждую категорию `CategoryID`, `CategoryName`и `Description` полей, а также число продуктов, связанных с категорией, используйте следующую инструкцию `SELECT`:

[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample7.sql)]

[![указать используемый запрос](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image23.png)

**Рис. 9**. Указание используемого запроса ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image25.png))

Обратите внимание, что вложенный запрос, вычисляющий количество продуктов, связанных с категорией, имеет псевдоним в виде `NumberOfProducts`. Такое сопоставление имен приводит к тому, что значение, возвращаемое этим вложенным запросом, связывается со столбцом `CategoriesDataTable` s `NumberOfProducts`.

После ввода этого запроса последним шагом является выбор имени для нового метода. Используйте `FillWithNumberOfProducts` и `GetCategoriesAndNumberOfProducts` для заполнения DataTable и возврата шаблонов DataTable соответственно.

[![назовите новые методы TableAdapter s Филлвиснумберофпродуктс и GetCategoriesAndNumberOfProducts.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image26.png)

**Рис. 10**. именование новых методов адаптера таблицы `FillWithNumberOfProducts` и `GetCategoriesAndNumberOfProducts` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image28.png))

На этом этапе уровень доступа к данным был расширен и включает число продуктов для каждой категории. Так как весь уровень представления направляет все вызовы DAL через отдельный уровень бизнес-логики, необходимо добавить соответствующий метод `GetCategoriesAndNumberOfProducts` в класс `CategoriesBLL`:

[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample8.cs)]

После выполнения DAL и BLL мы повторно готовы привязать эти данные к `Categories` Repeater в `CategoriesAndProducts.aspx`! Если вы уже создали элемент управления ObjectDataSource для элемента управления Repeater от определения числа продуктов в разделе обработчика событий `ItemDataBound`, удалите этот элемент ObjectDataSource и удалите параметр свойства Repeater s `DataSourceID`. Кроме того, не следует развязать событие Repeater `ItemDataBound` из обработчика событий, удалив синтаксис `Handles Categories.OnItemDataBound` в классе кода программной части ASP.NET.

После возврата к исходному состоянию Repeater добавьте новый объект ObjectDataSource с именем `CategoriesDataSource` через смарт-тег Repeater s. Настройте ObjectDataSource для использования класса `CategoriesBLL`, но вместо того, чтобы он использовал метод `GetCategories()`, он должен использовать `GetCategoriesAndNumberOfProducts()` вместо него (см. рис. 11).

[![настроить ObjectDataSource для использования метода GetCategoriesAndNumberOfProducts](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image29.png)

**Рис. 11**. Настройка ObjectDataSource для использования метода `GetCategoriesAndNumberOfProducts` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image31.png))

Затем обновите `ItemTemplate` таким образом, чтобы свойство LinkButton `Text` было декларативно назначено с помощью синтаксиса DataBinding и включало поля данных `CategoryName` и `NumberOfProducts`. Полная декларативная разметка для элемента управления Repeater и `CategoriesDataSource` ObjectDataSource соблюдается:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample9.aspx)]

Выходные данные, отображаемые путем обновления DAL для включения `NumberOfProducts` столбца, аналогичны тому, как используется `ItemDataBound`ный метод обработчика событий (см. рис. 4 для просмотра снимка экрана с именами категорий и количеством продуктов).

## <a name="step-3-displaying-the-selected-category-s-products"></a>Шаг 3. Отображение выбранных продуктов категории

На этом этапе у нас есть `Categories` Repeater, отображающий список категорий вместе с количеством продуктов в каждой категории. Элемент управления Repeater использует элемент управления LinkButton для каждой категории, которая при нажатии вызывает обратную передачу, после чего необходимо отобразить эти продукты для выбранной категории в `CategoryProducts` DataList.

Одна из проблем заключается в том, как разместить в DataList только те продукты для выбранной категории. В базе данных " [основной/подробности" с помощью выбираемого главного элемента управления GridView с](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) руководством по DetailsView мы увидели, как создать элемент управления GridView, строки которого могли быть выбраны, а сведения о выбранных строках отображаются в элементе DetailsView на той же странице. Элемент управления GridView возвращает сведения обо всех продуктах, используя метод `ProductsBLL` s `GetProducts()`, а элемент ObjectDataSource DetailsView извлекает сведения о выбранном продукте с помощью метода `GetProductsByProductID(productID)`. Значение параметра *`productID`* было предоставлено декларативно путем связывания его со значением свойства GridView s `SelectedValue`. К сожалению, у элемента Repeater нет свойства `SelectedValue` и он не может выступать в качестве источника параметра.

> [!NOTE]
> Это одна из проблем, которые появляются при использовании LinkButton в элементе Repeater. Если бы мы использовали гиперссылку для передачи `CategoryID` через строку запроса, мы могли бы использовать это поле QueryString в качестве источника для значения параметра s.

Прежде чем беспокоиться о недостатке свойства `SelectedValue` для элемента управления Repeater, позвольте s сначала привязать элемент управления DataList к элементу ObjectDataSource и указать его `ItemTemplate`.

В смарт-теге DataList добавьте новый элемент ObjectDataSource с именем `CategoryProductsDataSource` и настройте его для использования метода `ProductsBLL` класса s `GetProductsByCategoryID(categoryID)`. Поскольку элемент управления DataList в этом учебнике предоставляет интерфейс только для чтения, вы можете установить в раскрывающихся списках на вкладках Вставка, обновление и удалить значение (нет).

[![настроить ObjectDataSource для использования метода GetProductsByCategoryID класса ProductsBLL (КодТипа)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image32.png)

**Рис. 12**. Настройка ObjectDataSource для использования метода `ProductsBLL` Class s `GetProductsByCategoryID(categoryID)` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image34.png))

Так как метод `GetProductsByCategoryID(categoryID)` принимает входной параметр ( *`categoryID`* ), мастер настройки источника данных позволяет указать источник параметра s. Если категории были перечислены в элементе управления GridView или DataList, мы устанавливаем раскрывающийся список источника параметров для управления, а параметр ControlID — `ID` веб-элемента. Однако поскольку у элемента Repeater отсутствует свойство `SelectedValue` его нельзя использовать в качестве источника параметра. Если флажок установлен, то раскрывающийся список ControlID будет содержать только один элемент управления `ID``CategoryProducts`, `ID` DataList.

Пока установите в раскрывающемся списке Источник параметра значение нет. В итоге мы будем программно назначать значение этого параметра при щелчке элемента LinkButton в элементе Repeater.

[![не указывать источник параметра для параметра categoryID](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image35.png)

**Рис. 13**. не указывайте источник параметра для параметра *`categoryID`* ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image37.png))

После завершения работы мастера настройки источника данных Visual Studio создает `ItemTemplate`DataList. Замените этот `ItemTemplate` по умолчанию шаблоном, который использовался в предыдущем руководстве. также задайте для свойства `RepeatColumns` DataList s значение 2. После внесения этих изменений декларативная разметка для элемента управления DataList и связанный с ней объект ObjectDataSource должны выглядеть следующим образом:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample10.aspx)]

В настоящее время параметр *`categoryID`* `CategoryProductsDataSource` ObjectDataSource s не задан, поэтому при просмотре страницы продукты не отображаются. Для этого нужно задать значение этого параметра на основе `CategoryID` категории, нажатой в элементе Repeater. Это приводит к двум задачам: сначала, как определить, когда была нажата кнопка LinkButton в элементе Repeater s `ItemTemplate`; и во вторых, как можно определить `CategoryID` соответствующей категории, которую щелкнули LinkButton?

Элемент управления LinkButton, такой как Button и ImageButton, имеет событие `Click` и [событие`Command`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx). Событие `Click` предназначено для того, чтобы просто отметить, что была нажата кнопка LinkButton. Однако иногда в дополнение к тому, что была нажата кнопка LinkButton, нам также нужно передать некоторую дополнительную информацию в обработчик событий. В этом случае эти дополнительные сведения могут быть назначены свойствам LinkButton [`CommandName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx) и [`CommandArgument`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx) . Затем при нажатии элемента LinkButton срабатывает ее `Command` событие (вместо события `Click`), и обработчику событий передаются значения свойств `CommandName` и `CommandArgument`.

При возникновении события `Command` в шаблоне в элементе Repeater возникает [событие repeater`ItemCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx) , и ему передается `CommandName` и `CommandArgument` значения нажатия элемента LinkButton (или кнопки или ImageButton). Таким образом, чтобы определить, когда была нажата Категория LinkButton в элементе Repeater, необходимо выполнить следующие действия.

1. Задайте для свойства `CommandName` элемента LinkButton в элементе Repeater `ItemTemplate` какое-то значение (я использовал Листпродуктс). Если задать это `CommandName`, то при нажатии кнопки LinkButton возникает событие `Command` LinkButton.
2. Присвойте свойству `CommandArgument` LinkButton s значение текущего элемента `CategoryID`.
3. Создайте обработчик событий для события Repeater `ItemCommand`. В обработчике событий задайте для параметра `CategoryProductsDataSource` ObjectDataSource s `CategoryID` значение переданного `CommandArgument`.

Следующая `ItemTemplate` разметка для повторяющихся категорий, реализует шаги 1 и 2. Обратите внимание, что `CommandArgument` значение присваивается элементам данных `CategoryID` с помощью синтаксиса DataBinding:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample11.aspx)]

При создании обработчика `ItemCommand` событий рекомендуется всегда сначала проверять значение входящего `CommandName`, так как *любое* событие `Command`, вызванное *любой* кнопкой, LinkButton или ImageButton в элементе Repeater, приведет к срабатыванию события `ItemCommand`. Хотя сейчас у нас есть только одна такая LinkButton, в будущем мы (или другой разработчик в нашей группе) могут добавить в Repeater дополнительные веб-элементы управления для кнопок, которые при нажатии вызывают тот же `ItemCommand` обработчик событий. Поэтому рекомендуется всегда проверять свойство `CommandName` и продолжать только программную логику, если она соответствует ожидаемому значению.

Убедившись, что переданное `CommandName` значение равно Листпродуктс, обработчик событий присваивает `CategoryProductsDataSource` ObjectDataSource s `CategoryID` параметру переданного `CommandArgument`. Это изменение в ObjectDataSource `SelectParameters` автоматически приводит к повторной привязке элемента управления DataList к источнику данных, отображая продукты для вновь выбранной категории.

[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample12.cs)]

С этими дополнениями наш учебник завершен. Уделите немного времени для тестирования в браузере. На рис. 14 показан экран при первом посещении страницы. Поскольку Категория еще не выбрана, продукты не отображаются. Щелкнув категорию, например создать, вы увидите эти продукты в категории продуктов в представлении с двумя столбцами (см. рис. 15).

[![при первом посещении страницы продукты не отображаются](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image38.png)

**Рис. 14**. при первом посещении страницы продукты не отображаются ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image40.png))

[![щелкнув категорию создать, вы выведете список соответствующих продуктов справа.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image41.png)

**Рис. 15**. Если щелкнуть категорию создать, выводится список соответствующих продуктов справа ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image43.png)).

## <a name="summary"></a>Сводка

Как было показано в этом учебнике, а также на предыдущем, отчеты «основной/подробности» могут быть распределены между двумя страницами или объединены по одной. При отображении отчета «основной/подробности» на одной странице приводятся некоторые трудности, связанные с тем, как лучше разрешать макеты основных и подробных записей на странице. В *главной и подробной среде с помощью выбираемого главного элемента управления GridView с руководством по DetailsView подробные* записи отображаются над главными записями. в этом учебнике мы использовали методы CSS, чтобы записи главной таблицы настроились слева от сведений.

Вместе с отображением отчетов «основной/подробности» у нас также была возможность исследовать, как получить количество продуктов, связанных с каждой категорией, а также как выполнять логику на стороне сервера при щелчке элемента LinkButton (или кнопки или ImageButton) в элементе Repeater.

Этот учебник завершает исследование отчетов «основной/подробности» с помощью элементов управления DataList и Repeater. В следующем наборе руководств показано, как добавить возможности редактирования и удаления элементов управления DataList.

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Флоатуториал](http://css.maxdesign.com.au/floatutorial/) учебник по плавающим элементам CSS с помощью CSS
- [Размещение CSS](http://www.brainjar.com/css/positioning/) дополнительные сведения о размещении элементов с помощью CSS
- Размещение [содержимого с HTML](http://www.w3schools.com/html/html_layout.asp) с помощью `<table>` s и других HTML-элементов для позиционирования

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалистом по интересу для этого учебника был Зак Джонс. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](master-detail-filtering-acess-two-pages-datalist-cs.md)
> [Вперед](master-detail-filtering-with-a-dropdownlist-datalist-vb.md)
