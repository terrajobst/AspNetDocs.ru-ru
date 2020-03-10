---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: Фильтрация "основной/подробности" с помощью DropDownList (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике показано, как отобразить отчеты "основной/подробности" на одной веб-странице с помощью элементов управления DropDownList, чтобы отобразить записи "Master" и DataList для отображения...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 537f8e76bc0cbfa759a014b63ae5f68b5d3ca64d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78491088"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>Фильтрация "Основной/подробности" с помощью элемента управления DropDownList (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe) или [Загрузка PDF-файла](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)

> В этом учебнике показано, как отображать отчеты «основной/подробности» на одной веб-странице с помощью элементов управления DropDownList для отображения «главных» записей и элементов управления DataList для отображения «сведений».

## <a name="introduction"></a>Введение

Отчет "основной/подробности", который сначала был создан с помощью GridView в предыдущей [фильтрации "основной/подробности" с помощью DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) , начинается с отображения некоторого набора "основных" записей. Затем пользователь может выполнить детализацию до одной из основных записей, тем самым просмотрев сведения о главной записи. Отчеты «основной/подробности» являются идеальным выбором для визуализации связей «один-ко-многим» и для отображения подробных сведений из особенно «широких» таблиц (тех, которые содержат большое количество столбцов). Мы изучили, как реализовать отчеты «основной/подробности» с помощью элементов управления GridView и DetailsView в предыдущих руководствах. В этом руководстве и двух следующих примерах мы будем пересмотреть эти концепции, но сосредоточиться на использовании элементов управления DataList и Repeater.

В этом учебнике мы рассмотрим использование DropDownList для размещения записей «Master» с записями «Details», отображаемыми в DataList.

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>Шаг 1. Добавление веб-страниц учебника "основной/подробности"

Прежде чем приступить к работе с этим руководством, сначала нужно добавить папку и ASP.NET страницы, которые понадобятся для работы с этим руководством, и два следующих действия с отчетами «основной/подробности» с помощью элементов управления DataList и Repeater. Начните с создания новой папки в проекте с именем `DataListRepeaterFiltering`. Затем добавьте в эту папку следующие пять страниц ASP.NET, чтобы все они были настроены для использования главной страницы `Site.master`:

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`

![Создание папки DataListRepeaterFiltering и добавление страниц Tutorial ASP.NET](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

**Рис. 1**. Создание `DataListRepeaterFiltering` папки и добавление страниц Tutorial ASP.NET

Затем откройте страницу `Default.aspx` и перетащите `SectionLevelTutorialListing.ascx` пользовательский элемент управления из папки `UserControls` в область конструктора. Этот пользовательский элемент управления, созданный в учебнике « [главные страницы и Навигация по узлу](../introduction/master-pages-and-site-navigation-vb.md) », перечисляет карту узла и отображает учебники из текущего раздела в маркированном списке.

[![добавить пользовательский элемент управления SectionLevelTutorialListing. ascx в Default. aspx](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)

**Рис. 2**. Добавление пользовательского элемента управления `SectionLevelTutorialListing.ascx` в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))

Чтобы в маркированном списке отображались основные и подробные учебники, которые будут созданы, необходимо добавить их на карту узла. Откройте файл `Web.sitemap` и добавьте следующую разметку после разметки узла "Отображение данных с помощью DataList и Repeater".

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]

![Обновление схемы узла для включения новых страниц ASP.NET](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

**Рис. 3**. обновление схемы узла для включения новых страниц ASP.NET

## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>Шаг 2. Отображение категорий в DropDownList

В нашем отчете «основной/подробности» будут перечислены категории в DropDownList, а продукты выбранного элемента списка отображаются на странице в элементе управления DataList. Первая задача, предшествующая нам, заключается в том, чтобы отобразить категории в DropDownList. Для начала откройте страницу `FilterByDropDownList.aspx` в папке `DataListRepeaterFiltering` и перетащите DropDownList с панели элементов на конструктор страницы. Затем присвойте свойству `ID` DropDownList значение `Categories`. Щелкните ссылку Выбор источника данных из смарт-тега DropDownList и создайте новый элемент управления ObjectDataSource с именем `CategoriesDataSource`.

[![добавить новый элемент управления ObjectDataSource с именем CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)

**Рис. 4**. Добавление нового элемента управления ObjectDataSource с именем `CategoriesDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))

Настройте новый элемент ObjectDataSource таким способом, чтобы он вызывал метод `GetCategories()` класса `CategoriesBLL`. После настройки ObjectDataSource необходимо указать поле источника данных, которое должно быть отображено в элементе управления DropDownList, а также связать его со значением для каждого элемента списка. По`CategoryName` поле в качестве отображаемого и `CategoryID` в качестве значения для каждого элемента списка.

[![отображать поле CategoryName и использовать CategoryID в качестве значения](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)

**Рис. 5**. отображение поля `CategoryName` в DropDownList и использование `CategoryID` в качестве значения ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))

На этом этапе у нас есть элемент управления DropDownList, который заполняется записями из таблицы `Categories` (все это выполняется около шести секунд). На рис. 6 показан ход работы в браузере.

[![раскрывающийся список с текущими категориями](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)

**Рис. 6**. раскрывающийся список с текущими категориями ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))

## <a name="step-2-adding-the-products-datalist"></a>Шаг 2. Добавление элемента управления DataList для продуктов

Последним шагом в нашем отчете «основной/подробности» является отображение списка продуктов, связанных с выбранной категорией. Для этого добавьте на страницу элемент управления DataList и создайте новый элемент ObjectDataSource с именем `ProductsByCategoryDataSource`. Элементы управления `ProductsByCategoryDataSource` извлекают свои данные из метода `GetProductsByCategoryID(categoryID)` класса `ProductsBLL`. Поскольку этот отчет «основной/подробности» доступен только для чтения, выберите параметр (нет) на вкладках Вставка, обновление и удаление.

[![выбрать метод GetProductsByCategoryID (КодТипа)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)

**Рис. 7**. выбор метода `GetProductsByCategoryID(categoryID)` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))

После нажатия кнопки Далее мастер ObjectDataSource запрашивает источник значения для параметра *`categoryID`* метода `GetProductsByCategoryID(categoryID)`. Чтобы использовать значение выбранного элемента DropDownList `categories`, установите источник параметра в значение Control, а для ControlID — значение `Categories`.

[![задать для параметра categoryID значение элемента DropDownList категорий](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)

**Рис. 8**. Установка для параметра *`categoryID`* значения `Categories` DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png))

После завершения работы мастера настройки источника данных Visual Studio автоматически создаст `ItemTemplate` для элемента управления DataList, отображающего имя и значение каждого поля данных. Попробуем вместо этого использовать `ItemTemplate`, отображающий только название продукта, категорию, поставщика, количество на единицу и цену, а также `SeparatorTemplate`, которая вставляет элемент `<hr>` между каждым элементом. Я буду использовать `ItemTemplate` из примера в руководстве по [отображению данных с помощью элементов управления DataList и Repeater](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md) , но вы можете использовать любую разметку шаблона, которая наиболее наглядна.

После внесения этих изменений элемент управления DataList и его разметка ObjectDataSource должны выглядеть следующим образом:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

Уделите немного времени для проверки хода выполнения в браузере. При первом посещении страницы отображаются продукты, принадлежащие выбранной категории (напитки) (как показано на рис. 9), но изменение DropDownList не приводит к обновлению данных. Это связано с тем, что для обновления элемента управления DataList должна быть выполнена обратная передача. Для этого можно либо присвоить свойству `AutoPostBack` DropDownList значение `true`, либо добавить на страницу веб-элемент управления Button. В этом руководстве я решил установить для свойства `AutoPostBack` DropDownList значение `true`.

На рисунках 9 и 10 показан отчет «основной/подробности» в действии.

[![при первом посещении страницы отображаются продукты напитков](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)

**Рис. 9**. при первом посещении страницы отображаются продукты напитков ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png)).

[![выборе нового продукта (фрукты) автоматически вызывает обратную передачу, обновляя элемент управления DataList.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)

**Рис. 10**. Выбор нового продукта (фрукты) автоматически вызывает обратную передачу, обновляя элемент управления DataList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png))

## <a name="adding-a----choose-a-category----list-item"></a>Добавление элемента списка "--выберите категорию--"

При первом посещении страницы `FilterByDropDownList.aspx` по умолчанию выбирается первый элемент списка элемента управления DropDownList, отображая продукты категории «напитки» в DataList. В *фильтрации "основной/подробности" с помощью элемента DropDownList* мы добавили в DropDownList параметр "--выберите категорию--", который был выбран по умолчанию, и при выборе этого параметра отображаются *все* продукты в базе данных. Такой подход был бы управляемым при перечислении продуктов в GridView, так как каждая строка продукта занимала небольшой объем экранного пространства. Однако при использовании элемента управления DataList каждый продукт использует гораздо больший фрагмент экрана. Давайте по-прежнему добавим параметр "--выбрать категорию--", и он будет выбран по умолчанию, но вместо того, чтобы отображать все продукты при выборе, давайте настроим его таким образом, чтобы он не отображал продукты.

Чтобы добавить новый элемент списка в DropDownList, перейдите к окно свойств и щелкните многоточие в свойстве `Items`. Добавьте новый элемент списка с `Text` "--выберите категорию--" и `0``Value`.

![Добавить](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

**Рис. 11**. Добавление элемента списка «--выберите категорию--»

Кроме того, можно добавить элемент списка, добавив в DropDownList следующую разметку:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

Кроме того, необходимо присвоить `AppendDataBoundItems`у элемента управления DropDownList `true`, так как если он имеет значение `false` (значение по умолчанию), то при привязке категорий к DropDownList из ObjectDataSource они будут перезаписывать элементы списка, добавленные вручную.

![Присвойте свойству Аппенддатабаундитемс значение true.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

**Рис. 12**. установка свойства `AppendDataBoundItems` в значение true

Причина, по которой мы выбрали значение `0` для элемента списка "--выберите категорию--", заключается в том, что в системе нет категорий со значением `0`, поэтому при выборе элемента списка "--выберите категорию--" не будут возвращаться никакие записи о продукте. Чтобы подтвердить это, уделите время посетить страницу в браузере. Как показано на рис. 13, при первом просмотре страницы выбирается элемент списка «--выберите категорию--», и продукты не отображаются.

[![, когда](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)

**Рис. 13**. при выборе элемента списка "--выберите категорию--" продукты не отображаются ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png))

Если вы предпочитаете отображать *все* продукты, если выбран параметр "--выбрать категорию--", используйте вместо этого значение `-1`. Читатель внимательный будет отзывать его в фильтрации " *основной/подробности" с помощью DropDownList* . Мы обновили метод `GetProductsByCategoryID(categoryID)` класса `ProductsBLL`, чтобы при передаче *`categoryID`* значения `-1` были возвращены все записи продуктов.

## <a name="summary"></a>Сводка

При отображении иерархически связанных данных часто бывает удобно представлять данные с помощью отчетов «основной/подробности», из которых пользователь может начать изучение данных из верхней части иерархии и детализировать подробные сведения. В этом учебнике мы рассмотрели создание простого отчета «основной/подробности», в котором отображаются продукты выбранной категории. Это было выполнено с помощью DropDownList для списка категорий и DataList для продуктов, принадлежащих выбранной категории.

В следующем учебном курсе мы рассмотрим отделение основных и подробных записей на двух страницах. На первой странице будет отображен список записей «Master» со ссылкой для просмотра сведений. Щелкнув ссылку, вы перенесет пользователя на вторую страницу, где будут отображаться сведения о выбранной главной записи.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Особая благодарность...

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Рэнди Шмидт. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
> [Вперед](master-detail-filtering-acess-two-pages-datalist-vb.md)
