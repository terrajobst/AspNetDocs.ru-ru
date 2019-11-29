---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-vb
title: Фильтрация "основной/подробности" на двух страницах (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике рассматривается разделение отчета «основной/подробности» на две страницы. На странице "Главная" мы используем элемент управления Repeater для отображения списка катег...
ms.author: riande
ms.date: 10/30/2010
ms.assetid: f1a1be2c-6fd9-4a09-916e-aa1b98d5cf17
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 037e5f47efff88bfcbec57b11efa4fec04f9542d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591498"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>Фильтрация "Основной/подробности" на двух страницах (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_VB.exe) или [Загрузка PDF-файла](master-detail-filtering-acess-two-pages-datalist-vb/_static/datatutorial34vb1.pdf)

> В этом учебнике рассматривается разделение отчета «основной/подробности» на две страницы. На главной странице мы используем элемент управления Repeater для отображения списка категорий, при щелчке которого пользователь перейдет на страницу "сведения", где в DataList в двух столбцах отображаются продукты, принадлежащие выбранной категории.

## <a name="introduction"></a>Введение

В учебнике « [основной/подробности» в двух страницах](../masterdetail/master-detail-filtering-across-two-pages-vb.md) мы рассматривали этот шаблон с помощью элемента управления GridView для отображения всех поставщиков в системе. Этот GridView включал в себя HyperLinkField, который отображается в виде ссылки на вторую страницу, передавая `SupplierID` в строке запроса. На второй странице используется GridView для перечисления продуктов, предоставляемых выбранным поставщиком.

Такие Многостраничные отчеты «основной/подробности» могут быть выполнены также с помощью элементов управления DataList и Repeater. Единственное отличие заключается в том, что ни DataList, ни Repeater не поддерживают элемент управления HyperLinkField. Вместо этого необходимо добавить веб-элемент управления HyperLink или элемент HTML Anchor (`<a>`) в `ItemTemplate`элемента управления. Затем можно настроить свойство `NavigateUrl` гиперссылки или атрибут `href` привязки с помощью декларативных или программных подходов.

В этом учебнике мы рассмотрим пример, который перечисляет категории в маркированном списке на одной странице с помощью элемента управления Repeater. Каждый элемент списка будет включать имя и описание категории, а имя категории отображается как ссылка на вторую страницу. Если щелкнуть эту ссылку, пользователь перенесет на вторую страницу, где в DataList будут показаны продукты, принадлежащие к выбранной категории.

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>Шаг 1. Отображение категорий в маркированном списке

Первый шаг при создании отчета «основной/подробности» начинается с отображения «главных» записей. Поэтому нашей первой задачей является отображение категорий на странице «Главная». Откройте страницу `CategoryListMaster.aspx` в папке `DataListRepeaterFiltering`, добавьте элемент управления Repeater и в смарт-теге выберите Добавить новый объект ObjectDataSource. Настройте новый элемент ObjectDataSource таким образом, чтобы он обращается к своим данным из метода `GetCategories` класса `CategoriesBLL` (см. рис. 1).

[![настроить ObjectDataSource для использования метода Categories класса CategoriesBLL](master-detail-filtering-acess-two-pages-datalist-vb/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image1.png)

**Рис. 1**. Настройка ObjectDataSource для использования метода `GetCategories` класса `CategoriesBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image3.png))

Затем определите шаблоны Repeater таким образом, чтобы имя и описание каждой категории отображались как элемент в маркированном списке. Давайте еще не будем беспокоиться о том, что каждая категория имеет ссылку на страницу сведений. Ниже показана декларативная разметка для элемента управления Repeater и ObjectDataSource:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample1.aspx)]

После завершения этой разметки уделите время для просмотра хода выполнения через браузер. Как показано на рис. 2, элемент Repeater отображается в виде маркированного списка, в котором указаны имя и описание каждой категории.

[![каждая категория отображается как маркированный элемент списка](master-detail-filtering-acess-two-pages-datalist-vb/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image4.png)

**Рис. 2**. Каждая категория отображается как маркированный элемент списка ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image6.png))

## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>Шаг 2. преобразование имени категории в ссылку на страницу сведений

Чтобы разрешить пользователю отображать сведения об определенной категории, необходимо добавить ссылку на каждый маркированный список, при щелчке которого пользователь перейдет на вторую страницу (`ProductsForCategoryDetails.aspx`). На этой второй странице будут отображаться продукты для выбранной категории с помощью DataList. Чтобы определить категорию, для которой была нажата ссылка, необходимо передать `CategoryID` на вторую страницу с помощью какого-либо механизма. Самый простой и простой способ переносить скалярные данные с одной страницы на другую — через строку запроса, которая является вариантом, который мы будем использовать в этом учебнике. В частности, на странице `ProductsForCategoryDetails.aspx` будет считаться, что выбранное *`categoryID`* значение передается через поле QueryString с именем `CategoryID`. Например, чтобы просмотреть продукты для категории «напитки» с `CategoryID` 1, пользователь будет посещать `ProductsForCategoryDetails.aspx?CategoryID=1`.

Чтобы создать гиперссылку для каждого элемента маркированного списка в элементе управления Repeater, необходимо добавить в `ItemTemplate`элемент Web Control HyperLink или HTML Anchor (`<a>`). В сценариях, где гиперссылка отображается одинаково для каждой строки, любой из этих подходов будет достаточно. Для повторяющихся элементов я предпочитаю использовать элемент Anchor. Чтобы использовать элемент Anchor, обновите ItemTemplate элемента Repeater на:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample2.aspx)]

Обратите внимание, что `CategoryID` можно внедрить непосредственно в атрибут `href` элемента привязки. Тем не менее, для этого необходимо ограничить значение `href` атрибута апострофами (и кавычками), так как метод `Eval` в атрибуте `href` отделяет строку (`"CategoryID"`) кавычками. Вместо этого можно использовать веб-элемент управления HyperLink:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample3.aspx)]

Обратите внимание на то, как статическая часть URL-адреса — `ProductsForCategoryDetails.aspx?CategoryID` — добавляется к результату `Eval("CategoryID")` непосредственно в синтаксисе привязки данных с помощью сцепления строк.

Одним из преимуществ использования элемента управления HyperLink является возможность программного доступа к нему из обработчика `ItemDataBound` событий Repeater, если это необходимо. Например, можно отобразить имя категории как текст, а не как ссылку для категорий без связанных продуктов. Такую проверку можно выполнить программно в обработчике событий `ItemDataBound`. для категорий без связанных продуктов в свойстве `NavigateUrl` гиперссылки может быть задана пустая строка, что приводит к отображению конкретного имени категории в виде обычного текста (а не в виде ссылки). Дополнительные сведения о форматировании содержимого DataList и Repeater на основе программной логики с помощью обработчика событий `ItemDataBound` см. в статье Форматирование элементов управления DataList [и Repeater на основе данных](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md) .

Если вы выполняете следующие функции, вы можете использовать на странице подход к элементу привязки или элементу управления HyperLink. Независимо от подхода при просмотре страницы в браузере каждое имя категории должно быть отображено в виде ссылки на `ProductsForCategoryDetails.aspx`, передавая соответствующее значение `CategoryID` (см. рис. 3).

[![имена категорий теперь можно связать с ProductsForCategoryDetails. aspx](master-detail-filtering-acess-two-pages-datalist-vb/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image7.png)

**Рис. 3**. имена категорий теперь связаны с `ProductsForCategoryDetails.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image9.png))

## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>Шаг 3. Перечисление продуктов, относящихся к выбранной категории

По завершении страницы `CategoryListMaster.aspx` все готово к внедрению страницы "сведения", `ProductsForCategoryDetails.aspx`. Откройте эту страницу, перетащите элемент управления DataList с панели инструментов в конструктор и задайте для его свойства `ID` значение `ProductsInCategory`. Затем в смарт-теге DataList выберите Добавить на страницу новый элемент управления ObjectDataSource, назвав его `ProductsInCategoryDataSource`. Настройте его таким способом, чтобы он вызывал метод `GetProductsByCategoryID(categoryID)` класса `ProductsBLL`; Задайте для раскрывающихся списков на вкладках Вставка, обновление и удаление значение (нет).

[![настроить ObjectDataSource для использования метода GetProductsByCategoryID (categoryID) класса ProductsBLL](master-detail-filtering-acess-two-pages-datalist-vb/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image10.png)

**Рис. 4**. Настройка ObjectDataSource для использования метода `GetProductsByCategoryID(categoryID)` класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image12.png))

Поскольку метод `GetProductsByCategoryID(categoryID)` принимает входной параметр ( *`categoryID`* ), мастер выбора источника данных предлагает нам возможность указать источник параметра. Задайте в качестве источника параметра значение QueryString с помощью `CategoryID`QueryStringField.

[![использовать поле строки кода CategoryID в качестве источника параметра](master-detail-filtering-acess-two-pages-datalist-vb/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image13.png)

**Рис. 5**. Использование поля QueryString `CategoryID` в качестве источника параметра ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image15.png))

Как мы видели в предыдущих руководствах, после завершения работы с мастером выбор источника данных Visual Studio автоматически создает `ItemTemplate` для элемента управления DataList, в котором перечислены имена и значения полей данных. Замените этот шаблон на тот, который содержит только название продукта, поставщика и цену. Также задайте для свойства `RepeatColumns` элемента управления DataList значение 2. После этих изменений декларативная разметка DataList и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample4.aspx)]

Чтобы просмотреть эту страницу в действии, начните со страницы `CategoryListMaster.aspx`. затем щелкните ссылку в маркированном списке категории. В этом случае вы перейдете к `ProductsForCategoryDetails.aspx`, передав `CategoryID` через строку запроса. `ProductsInCategoryDataSource` ObjectDataSource в `ProductsForCategoryDetails.aspx` будет получать только продукты для указанной категории и отображать их в DataList, который отображает два продукта в строке. На рис. 6 показан снимок экрана `ProductsForCategoryDetails.aspx` при просмотре напитков.

[![отображаются напитки, по две строки](master-detail-filtering-acess-two-pages-datalist-vb/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image16.png)

**Рис. 6**. отображаются напитки, две на строку ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image18.png)).

## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>Шаг 4. Отображение сведений о категории в ProductsForCategoryDetails. aspx

Когда пользователь щелкает категорию в `CategoryListMaster.aspx`, он предпринимается для `ProductsForCategoryDetails.aspx` и отображения продуктов, принадлежащих выбранной категории. Однако в `ProductsForCategoryDetails.aspx` нет визуальных подсказок относительно выбранной категории. Пользователь, который выбрал элемент напитки, но случайно щелкнул «специи», не имеет возможности выпустить свою ошибку после достижения `ProductsForCategoryDetails.aspx`. Чтобы решить эту потенциальную проблему, можно отобразить сведения о выбранной категории — ее имя и описание — в верхней части страницы `ProductsForCategoryDetails.aspx`.

Для этого добавьте элемент FormView над элементом управления Repeater в `ProductsForCategoryDetails.aspx`. Затем добавьте новый элемент управления ObjectDataSource на страницу из смарт-тега FormView с именем `CategoryDataSource` и настройте его для использования метода `GetCategoryByCategoryID(categoryID)` класса `CategoriesBLL`.

[![доступ к сведениям о категории с помощью метода Жеткатегорибикатегорид (categoryID) класса CategoriesBLL](master-detail-filtering-acess-two-pages-datalist-vb/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image19.png)

**Рис. 7**. доступ к сведениям о категории с помощью метода `GetCategoryByCategoryID(categoryID)` класса `CategoriesBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image21.png))

Как и в случае с `ProductsInCategoryDataSource` ObjectDataSource, добавленным на шаге 3, мастер настройки источника данных `CategoryDataSource`запрашивает источник для входного параметра метода `GetCategoryByCategoryID(categoryID)`. Используйте те же параметры, что и ранее, установив для источника параметра значение QueryString, а для значения QueryStringField — `CategoryID` (см. рис. 5).

После завершения работы мастера Visual Studio автоматически создает `ItemTemplate`, `EditItemTemplate`и `InsertItemTemplate` для FormView. Так как мы предоставляем интерфейс только для чтения, вы можете удалить `EditItemTemplate` и `InsertItemTemplate`. Кроме того, вы можете настроить `ItemTemplate`FormView. После удаления лишних шаблонов и настройки ItemTemplate декларативная разметка FormView и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample5.aspx)]

На рис. 8 показан снимок экрана при просмотре этой страницы в браузере.

> [!NOTE]
> Помимо FormView, я также добавил элемент управления HyperLink над FormView, который вернет пользователя в список категорий (`CategoryListMaster.aspx`). Вы можете поместить эту ссылку в другое место или полностью опустить ее.

[Сведения о категории ![теперь отображаются в верхней части страницы](master-detail-filtering-acess-two-pages-datalist-vb/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image22.png)

**Рис. 8**. Теперь сведения о категориях отображаются в верхней части страницы ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image24.png))

## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>Шаг 5. Отображение сообщения, если продукты не относятся к выбранной категории

На `CategoryListMaster.aspx` странице перечислены все категории в системе, независимо от наличия связанных с ними продуктов. Если пользователь щелкает категорию без связанных продуктов, элемент управления DataList в `ProductsForCategoryDetails.aspx` не будет подготовлен, так как его источник данных не будет содержать никаких элементов. Как мы видели в прошлых учебных курсах, GridView предоставляет свойство `EmptyDataText`, которое можно использовать для указания текстового сообщения, которое должно отображаться, если в его источнике данных нет записей. Увы, ни элемент управления DataList, ни Repeater не имеют такого свойства.

Чтобы отобразить сообщение о том, что для выбранной категории нет соответствующих продуктов, необходимо добавить на страницу элемент управления Label, для которого в свойстве `Text` назначено сообщение, которое будет отображаться в случае отсутствия соответствующих продуктов. Затем необходимо программно задать свойство `Visible` в зависимости от того, содержит ли DataList какие либо элементы.

Чтобы сделать это, начните с добавления метки под элементом управления DataList. Присвойте свойству `ID` `NoProductsMessage` и его свойству `Text` значение "отсутствуют продукты для выбранной категории..." Далее необходимо программно задать свойство `Visible` этой метки в зависимости от того, были ли данные привязаны к `ProductsInCategory` DataList. Это назначение должно быть выполнено после привязки данных к DataList. Для элементов GridView, DetailsView и FormView можно создать обработчик событий для события `DataBound` элемента управления, которое срабатывает после завершения привязки данных. Однако ни элемент управления DataList, ни Repeater не имеют доступного `DataBound` события.

В этом конкретном примере можно назначить свойство `Visible` метки в обработчике событий `Page_Load`, поскольку данные будут назначены элементу управления DataList до события `Load` страницы. Однако этот подход не будет работать в общем случае, так как данные из ObjectDataSource могут быть привязаны к DataList позже в жизненном цикле страницы. Например, если отображаемые данные основаны на значении в другом элементе управления, например при отображении отчета «основной/подробности» с помощью DropDownList для хранения «основных» записей, данные могут быть не привязаны к веб-элементу управления данными до тех пор, пока не будет `PreRender` этапа жизненного цикла страницы.

Одним из решений, которые будут работать во всех случаях, является присвоение свойству `Visible` `False` в обработчике событий `ItemDataBound` (или `ItemCreated`) DataList при привязке типа элемента `Item` или `AlternatingItem`. В этом случае мы понимаем, что в источнике данных есть хотя бы один элемент данных, и поэтому может скрыть `NoProductsMessage` метку. В дополнение к этому обработчику событий нам также нужен обработчик событий `DataBinding` элемента управления DataList, в котором мы инициализируем свойство `Visible` метки для `True`. Так как событие `DataBinding` срабатывает до `ItemDataBound` событий, для свойства `Visible` метки первоначально устанавливается значение `True`. Однако если имеются какие бы то ни было элементы данных, для них будет задано значение `False`. Следующий код реализует эту логику:

[!code-vb[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample6.vb)]

Все категории в базе данных Northwind связаны с одним или несколькими продуктами. Чтобы протестировать эту функцию, я вручную настроил базу данных Northwind для этого руководства, переназначит все продукты, связанные с категорией создания (`CategoryID` = 7), в категорию Seafood (`CategoryID` = 8). Это можно сделать в обозреватель сервера, выбрав Создать запрос и используя следующую инструкцию `UPDATE`:

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample7.sql)]

После обновления базы данных вернитесь на страницу `CategoryListMaster.aspx` и щелкните ссылку Создать. Поскольку больше нет продуктов, принадлежащих категории создать, вы должны увидеть "продукты для выбранной категории отсутствуют..." сообщение, как показано на рис. 9.

[![отображается сообщение, если нет продуктов, принадлежащих к выбранной категории](master-detail-filtering-acess-two-pages-datalist-vb/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image25.png)

**Рис. 9**. сообщение отображается, если нет продуктов, принадлежащих к выбранной категории ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-acess-two-pages-datalist-vb/_static/image27.png))

## <a name="summary"></a>Сводка

В то время как отчеты «основной/подробности» могут отображать как основные, так и подробные записи на одной странице, во многих веб-сайтах они разделяются на две веб-страницы. В этом учебнике мы рассмотрели, как реализовать такой отчет «основной/подробности», используя категории, перечисленные в маркированном списке, с помощью повторителя на главной веб-странице и связанных продуктов, перечисленных на странице «сведения». Каждый элемент списка на главной веб-странице содержал ссылку на страницу сведений, переданную по значению `CategoryID` строки.

На странице сведений получение этих продуктов для указанного поставщика осуществлялось с помощью метода `GetProductsByCategoryID(categoryID)` класса `ProductsBLL`. Значение параметра *`categoryID`* было указано декларативно с использованием значения `CategoryID` QueryString в качестве источника параметра. Мы также рассмотрели, как отобразить сведения о категории на странице сведений с помощью FormView и как отобразить сообщение, если нет продуктов, принадлежащих к выбранной категории.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Особая благодарность...

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальным рецензентам для этого учебника были Зак Jones и основными рецензентами. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](master-detail-filtering-with-a-dropdownlist-datalist-vb.md)
> [Вперед](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)
