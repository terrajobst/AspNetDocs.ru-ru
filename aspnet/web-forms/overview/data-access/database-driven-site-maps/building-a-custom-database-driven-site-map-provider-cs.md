---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-cs
title: Создание пользовательского поставщика карт сайтов, управляемого базой данныхC#() | Документация Майкрософт
author: rick-anderson
description: Поставщик карт узла по умолчанию в ASP.NET 2,0 извлекает свои данные из статического XML-файла. Хотя поставщик на основе XML подходит для многих малых и средних СИЗ...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 04b7591d-106f-4f05-87e9-d416cb65a8a6
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-cs
msc.type: authoredcontent
ms.openlocfilehash: a3e27b37703b12c9796e8516f0d805aef1fdf8d8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636919"
---
# <a name="building-a-custom-database-driven-site-map-provider-c"></a>Создание пользовательского поставщика карт сайтов, управляемых базами данных (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_CS.zip) или [скачать PDF](building-a-custom-database-driven-site-map-provider-cs/_static/datatutorial62cs1.pdf)

> Поставщик карт узла по умолчанию в ASP.NET 2,0 извлекает свои данные из статического XML-файла. Хотя поставщик на основе XML подходит для многих малых и средних веб-сайтов, для больших веб-приложений требуется более динамическая схема узла. В этом учебнике мы создадим пользовательский поставщик карт узла, который получает свои данные из уровня бизнес-логики, который, в свою очередь, извлекает данные из базы данных.

## <a name="introduction"></a>Введение

Функция Map ASP.NET 2,0 s позволяет разработчику страниц определять карту веб-узла Web Application на некоторых постоянных носителях, например в XML-файле. После определения доступ к данным карт узла можно получить программно с помощью [класса`SiteMap`](https://msdn.microsoft.com/library/system.web.sitemap.aspx) в [пространстве имен`System.Web`](https://msdn.microsoft.com/library/system.web.aspx) или с помощью различных веб-элементов управления навигацией, таких как SiteMapPath, меню и элементы управления TreeView. Система карт узла использует [модель поставщика](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) , чтобы различные реализации сериализации карт веб-узла можно было создать и подключить к веб-приложению. Поставщик карт узла по умолчанию, который поставляется с ASP.NET 2,0, сохраняет структуру карт узла в XML-файле. Вернувшись на [главные страницы и руководство по переходу на сайт](../introduction/master-pages-and-site-navigation-cs.md) , мы создали файл с именем `Web.sitemap`, содержащий эту структуру, и обновили его XML-код с помощью каждого нового раздела учебника.

Поставщик схемы сайта на основе XML по умолчанию работает правильно, если структура схемы узла является довольно статической, например для этих учебников. Однако во многих сценариях требуется более динамическая схема узла. Рассмотрим карту узла, показанную на рис. 1, где каждая категория и продукт отображаются в виде разделов в структуре веб-сайта. При использовании этой схемы сайта на веб-странице, соответствующей корневому узлу, могут сопоставлены все категории, в то время как на веб-странице с определенной категорией указано, что товары категории и просмотр определенной веб-страницы продукта покажут сведения о продукте.

[![категорий и продуктов, описывающего структуру узла](building-a-custom-database-driven-site-map-provider-cs/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image1.png)

**Рис. 1**. категории и продукты, описывающего структуру узла s ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image2.png))

Хотя эта структура на основе категорий и продуктов может быть жестко запрограммирована в `Web.sitemap` файле, необходимо обновить файл при каждом добавлении, удалении или переименовании категории или продукта. Следовательно, обслуживание карт узла было бы значительно упрощено, если его структура была получена из базы данных, или, в идеале, от уровня бизнес-логики архитектуры приложения. Таким образом, по мере добавления, переименования или удаления продуктов и категорий схема узла будет автоматически обновляться в соответствии с этими изменениями.

Так как сериализация карт узла ASP.NET 2,0 s основана на модели поставщика, мы можем создать собственный поставщик карт узла, который извлекает свои данные из альтернативного хранилища данных, такого как база данных или архитектура. В этом учебнике мы создадим настраиваемый поставщик, который извлекает свои данные из BLL. Давайте приступим к работе!

> [!NOTE]
> Пользовательский поставщик карт узла, созданный в этом руководстве, тесно связан с архитектурой приложения и моделью данных. Джефф Просайз [сохраняет карты сайтов в SQL Server](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) и [поставщик карты узла SQL, который вы](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) сохранили, ожидают, что статьи проверяют обобщенный подход к хранению данных карты узла в SQL Server.

## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>Шаг 1. Создание пользовательских веб-страниц поставщика карт сайта

Прежде чем приступить к созданию пользовательского поставщика карт узла, давайте сначала добавим страницы ASP.NET, необходимые для работы с этим руководством. Для начала добавьте новую папку с именем `SiteMapProvider`. Затем добавьте в эту папку следующие страницы ASP.NET, чтобы связать каждую страницу с главной страницей `Site.master`:

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

Также добавьте вложенную папку `CustomProviders` в папку `App_Code`.

![Добавление страниц ASP.NET для руководств, связанных с поставщиками карт узла](building-a-custom-database-driven-site-map-provider-cs/_static/image2.gif)

**Рис. 2**. добавление страниц ASP.NET для руководств, связанных с поставщиками карт узла

Так как в этом разделе есть только один учебник, нам не нужно `Default.aspx`, чтобы перечислить учебники по разделам. Вместо этого `Default.aspx` будут отображать категории в элементе управления GridView. Мы обсудим это на шаге 2.

Затем обновите `Web.sitemap`, чтобы включить ссылку на страницу `Default.aspx`. В частности, добавьте следующую разметку после `<siteMapNode>`кэширования:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample1.xml)]

После обновления `Web.sitemap`просмотрите веб-сайт учебников в браузере. В меню слева теперь содержится элемент для единственного учебника по поставщику карт узла.

![Схема узла теперь включает в себя запись для учебника по поставщику карт узла.](building-a-custom-database-driven-site-map-provider-cs/_static/image3.gif)

**Рис. 3**. схема узла теперь включает в себя запись для учебника по поставщику карт узла

В этом учебнике основное внимание уделяется созданию пользовательского поставщика карт узла и настройке веб-приложения для использования этого поставщика. В частности, мы создадим поставщик, возвращающий карту узла, которая включает корневой узел и узел для каждой категории и продукта, как показано на рис. 1. Как правило, каждый узел в карте узла может указывать URL-адрес. Для нашей схемы узла URL-адрес корневого узла s будет `~/SiteMapProvider/Default.aspx`, в котором будут перечислены все категории в базе данных. Каждый узел категории на карте узла будет иметь URL-адрес, указывающий на `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`, в котором будут перечислены все продукты указанного *CategoryID*. Наконец, каждый узел схемы узла продукта будет указывать на `~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`, в котором будут отображаться сведения о конкретном продукте.

Для начала необходимо создать `Default.aspx`, `ProductsByCategory.aspx`и `ProductDetails.aspx` страницы. Эти страницы выполняются в шагах 2, 3 и 4 соответственно. Так как креативность этого учебника посвящены поставщикам карт веб-узлов, и, поскольку в прошлых учебных курсах были рассмотрены создание таких видов многостраничных отчетов «основной/подробности», мы спешите с шагами 2 – 4. Если вам требуется Обновитель для создания отчетов «основной/подробности», охватывающих несколько страниц, ознакомьтесь с руководством « [основной/подробности фильтрация на двух страницах](../masterdetail/master-detail-filtering-across-two-pages-cs.md) ».

## <a name="step-2-displaying-a-list-of-categories"></a>Шаг 2. Отображение списка категорий

Откройте страницу `Default.aspx` в папке `SiteMapProvider` и перетащите элемент управления GridView с панели инструментов в конструктор, установив для его `ID` значение `Categories`. Из смарт-тега GridView s привяжите его к новому ObjectDataSource с именем `CategoriesDataSource` и настройте его таким образом, чтобы он получал свои данные с помощью метода `CategoriesBLL` класса s `GetCategories`. Поскольку в этом элементе управления GridView просто отображаются категории и не предусмотрены возможности изменения данных, установите в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет).

[![настроить ObjectDataSource для возврата категорий с помощью метода Categories](building-a-custom-database-driven-site-map-provider-cs/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image3.png)

**Рис. 4**. Настройка элемента управления ObjectDataSource для возврата категорий с помощью метода `GetCategories` ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image4.png))

[![установить в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет)](building-a-custom-database-driven-site-map-provider-cs/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image5.png)

**Рис. 5**. Установка раскрывающихся списков на вкладках обновления, вставки и удаления в (нет) ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image6.png))

После завершения работы мастера настройки источника данных Visual Studio добавит BoundField для `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`и `BrochurePath`. Измените элемент GridView таким образом, чтобы он содержал только `CategoryName` и `Description` BoundFields, и обновите свойство `HeaderText` `CategoryName` BoundField на Category.

Затем добавьте HyperLinkField и поместите его в крайнее левое поле. Задайте для свойства `DataNavigateUrlFields` значение `CategoryID` а свойству `DataNavigateUrlFormatString` — значение `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`. Задайте свойство `Text` для просмотра продуктов.

![Добавление HyperLinkField к категории GridView](building-a-custom-database-driven-site-map-provider-cs/_static/image6.gif)

**Рис. 6**. Добавление HyperLinkField в `Categories` GridView

После создания ObjectDataSource и настройки полей GridView два элемента управления декларативная разметка будет выглядеть следующим образом:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample2.aspx)]

На рис. 7 показано, `Default.aspx` при просмотре в браузере. Щелкнув ссылку категории s View Products, вы перейдете к `ProductsByCategory.aspx?CategoryID=categoryID`, которая будет построена на шаге 3.

[![каждая категория указана вместе со ссылкой «Просмотр продуктов»](building-a-custom-database-driven-site-map-provider-cs/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image7.png)

**Рис. 7**. Каждая категория отображается вместе со ссылкой «Просмотр продуктов» ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image8.png)).

## <a name="step-3-listing-the-selected-category-s-products"></a>Шаг 3. перечисление выбранных продуктов категории

Откройте страницу `ProductsByCategory.aspx` и добавьте элемент GridView, назвав его `ProductsByCategory`. Из своего смарт-тега привяжите GridView к новому элементу ObjectDataSource с именем `ProductsByCategoryDataSource`. Настройте ObjectDataSource для использования метода `ProductsBLL` Class s `GetProductsByCategoryID(categoryID)` и задайте для раскрывающихся списков значение (нет) на вкладках обновление, вставка и удаление.

[![использовать метод GetProductsByCategoryID класса ProductsBLL (categoryID)](building-a-custom-database-driven-site-map-provider-cs/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image9.png)

**Рис. 8**. использование метода `GetProductsByCategoryID(categoryID)` `ProductsBLL` классов ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image10.png))

На последнем шаге мастера настройки источника данных запрашивается источник параметров для *CategoryID*. Так как эти сведения передаются через поле QueryString `CategoryID`, выберите строку запроса из раскрывающегося списка и введите CategoryID в текстовое поле QueryStringField, как показано на рис. 9. Чтобы завершить работу мастера, нажмите кнопку Готово.

[![использовать поле строки CategoryID для параметра categoryID](building-a-custom-database-driven-site-map-provider-cs/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image11.png)

**Рис. 9**. Использование поля QueryString `CategoryID` для параметра *CategoryID* ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image12.png))

После завершения работы мастера Visual Studio добавит соответствующие BoundFields и CheckBoxField в GridView для полей данных продукта. Удалите все, кроме `ProductName`, `UnitPrice`и `SupplierName` BoundFields. Настройте эти три свойства `HeaderText` BoundFields для чтения продукта, цены и поставщика соответственно. Отформатируйте `UnitPrice` BoundField как валюту.

Затем добавьте HyperLinkField и переместите его в крайнее левое положение. Задайте для свойства `Text` значение, чтобы просмотреть сведения, свойство `DataNavigateUrlFields` для `ProductID`, а для свойства `DataNavigateUrlFormatString` — значение `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`.

![Добавьте сведения о представлении HyperLinkField, указывающие на Продуктдетаилс. aspx](building-a-custom-database-driven-site-map-provider-cs/_static/image10.gif)

**Рис. 10**. Добавление сведений о представлении HyperLinkField, указывающих на `ProductDetails.aspx`

После выполнения этих настроек декларативная разметка GridView и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample3.aspx)]

Вернитесь к просмотру `Default.aspx` через браузер и щелкните ссылку Просмотреть продукты для напитков. Это приведет к `ProductsByCategory.aspx?CategoryID=1`, отображению имен, цен и поставщиков продуктов в базе данных Northwind, принадлежащих категории «напитки» (см. рис. 11). Вы можете еще больше усовершенствовать эту страницу, включив ссылку для возврата пользователей на страницу со списком категорий (`Default.aspx`) и элемент управления DetailsView или FormView, отображающий выбранную категорию имя и описание.

[![отображаются названия напитков, цены и поставщики](building-a-custom-database-driven-site-map-provider-cs/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image13.png)

**Рис. 11**. Отображение названий напитков, цен и поставщиков ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image14.png))

## <a name="step-4-showing-a-product-s-details"></a>Шаг 4. Отображение сведений о продукте

На последней странице `ProductDetails.aspx`отображаются сведения о выбранных продуктах. Откройте `ProductDetails.aspx` и перетащите элемент DetailsView с панели элементов на конструктор. Задайте свойству `ID` DetailsView s значение `ProductInfo` и удалите значения свойств `Height` и `Width`. Из своего смарт-тега свяжите DetailsView с новым ObjectDataSource с именем `ProductDataSource`, настроив ObjectDataSource на извлечение своих данных из `ProductsBLL` класса s `GetProductByProductID(productID)` метода. Как и в предыдущих веб-страницах, созданных в шагах 2 и 3, установите раскрывающиеся списки на вкладках обновление, вставка и удаление в значение (нет).

[![настроить ObjectDataSource для использования метода Жетпродуктбипродуктид (productID)](building-a-custom-database-driven-site-map-provider-cs/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image15.png)

**Рис. 12**. Настройка ObjectDataSource для использования метода `GetProductByProductID(productID)` ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image16.png))

На последнем шаге мастера настройки источника данных запрашивается источник параметра *ProductID* . Так как эти данные поступают через поле QueryString `ProductID`, задайте для раскрывающегося списка значение QueryString, а в текстовом поле QueryStringField — ProductID. Наконец, нажмите кнопку "Готово", чтобы завершить работу мастера.

[![настроить параметр productID для извлечения его значения из поля строки запроса ProductID](building-a-custom-database-driven-site-map-provider-cs/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image17.png)

**Рис. 13**. Настройка параметра *ProductID* для извлечения его значения из поля `ProductID` QueryString ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image18.png))

После завершения работы мастера настройки источника данных Visual Studio создаст соответствующие BoundFields и CheckBoxField в DetailsView для полей данных продукта. Удалите `ProductID`, `SupplierID`и `CategoryID` BoundFields и настройте оставшиеся поля по своему усмотрению. После нескольких конфигураций Aesthetic декларативная разметка DetailsView и ObjectDataSource выглядит следующим образом:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample4.aspx)]

Чтобы протестировать эту страницу, вернитесь в `Default.aspx` и щелкните Просмотр продуктов для категории "напитки". В списке продуктов напитков щелкните ссылку Просмотреть сведения для Чай Chai. Откроется `ProductDetails.aspx?ProductID=1`, в котором отображаются сведения о Чай Chai (см. рис. 14).

[Отображается ![поставщика Chai, категория, Цена и другие сведения.](building-a-custom-database-driven-site-map-provider-cs/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image19.png)

**Рис. 14**. отображается поставщик, категория, Цена и другие сведения, отображаемые в списке Chai ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image20.png))

## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>Шаг 5. Основные сведения о внутренних принципах работы поставщика карт веб-сайтов

Схема узла представлена в памяти веб-сервера как коллекция `SiteMapNode` экземпляров, образующих иерархию. Должно быть ровно один корень, все некорневые узлы должны иметь ровно один родительский узел, а все узлы могут иметь произвольное число дочерних элементов. Каждый объект `SiteMapNode` представляет раздел в структуре веб-сайта. в этих разделах обычно есть соответствующая веб-страница. Следовательно, [класс`SiteMapNode`](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) имеет такие свойства, как `Title`, `Url`и `Description`, которые предоставляют сведения для раздела, который представляет `SiteMapNode`. Существует также свойство `Key`, которое однозначно определяет каждую `SiteMapNode` в иерархии, а также свойства, используемые для создания иерархии `ChildNodes`, `ParentNode`, `NextSibling`, `PreviousSibling`и т. д.

На рис. 15 показана общая структура карт узла на рис. 1, но при этом детали реализации набросаны более подробно.

[![каждый SiteMapNode имеет такие свойства, как Title, URL-адрес, ключ и т. д.](building-a-custom-database-driven-site-map-provider-cs/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image15.gif)

**Рис. 15**. Каждый `SiteMapNode` имеет такие свойства, как `Title`, `Url`, `Key`и т. д. ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image17.gif))

Карту узла доступны через [класс`SiteMap`](https://msdn.microsoft.com/library/system.web.sitemap.aspx) в [пространстве имен`System.Web`](https://msdn.microsoft.com/library/system.web.aspx). Это свойство `RootNode` классов возвращает корневой экземпляр `SiteMapNode` узла Map. `CurrentNode` возвращает `SiteMapNode`, свойство `Url` которого соответствует URL-адресу запрашиваемой в данный момент страницы. Этот класс используется внутри веб-элементов управления навигации ASP.NET 2,0.

При доступе к свойствам `SiteMap` классов необходимо сериализовать структуру карт узла из некоторого постоянного источника в память. Однако логика сериализации карт узла не жестко кодируется в класс `SiteMap`. Вместо этого во время выполнения класс `SiteMap` определяет, какой *поставщик* карт узла следует использовать для сериализации. По умолчанию используется [класс`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx) , который считывает структуру карт узла из правильно отформатированного XML-файла. Однако с небольшой наработкой мы можем создать собственный пользовательский поставщик карт узла.

Все поставщики карт веб-сайтов должны быть производными от [класса`SiteMapProvider`](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx), который включает в себя необходимые методы и свойства, необходимые для поставщиков карт сайта, но не содержит много деталей реализации. Второй класс, [`StaticSiteMapProvider`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx), расширяет класс `SiteMapProvider` и содержит более надежную реализацию необходимых функций. На внутреннем уровне `StaticSiteMapProvider` сохраняет экземпляры `SiteMapNode` карте узла в `Hashtable` и предоставляет такие методы, как `AddNode(child, parent)`, `RemoveNode(siteMapNode),` и `Clear()`, которые добавляют и удаляют `SiteMapNode` s во внутреннюю `Hashtable`. Класс `XmlSiteMapProvider` является производным от `StaticSiteMapProvider`.

При создании пользовательского поставщика карт узла, который расширяет `StaticSiteMapProvider`, необходимо переопределить два абстрактных метода: [`BuildSiteMap`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx) и [`GetRootNodeCore`](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx). `BuildSiteMap`, как и предполагает его название, отвечает за загрузку структуры карт узла из постоянного хранилища и ее конструирования в памяти. `GetRootNodeCore` возвращает корневой узел в карте сайта.

Прежде чем веб-приложение сможет использовать поставщик карт узла, его необходимо зарегистрировать в конфигурации приложения. По умолчанию класс `XmlSiteMapProvider` регистрируется с именем `AspNetXmlSiteMapProvider`. Чтобы зарегистрировать дополнительные поставщики карт веб-сайтов, добавьте следующую разметку в `Web.config`:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample5.xml)]

Значение *имени* присваивает поставщику понятное имя, а *тип* указывает полное имя типа для поставщика карт узла. После создания пользовательского поставщика карт веб-узла мы рассмотрим конкретные значения для значений *имени* и *типа* на шаге 7.

Экземпляр класса поставщика карт узла создается при первом доступе из класса `SiteMap` и остается в памяти в течение времени существования веб-приложения. Поскольку существует только один экземпляр поставщика карт узла, который может вызываться из нескольких одновременных посетителей веб-узла, крайне важно, чтобы методы поставщика были *потокобезопасными*.

В целях повышения производительности и масштабируемости важно, чтобы мы кэшировал структуру карт сайтов в памяти и возвращали эту кэшированную структуру, а не создавать ее каждый раз при вызове метода `BuildSiteMap`. `BuildSiteMap` может вызываться несколько раз для каждого запроса страницы на каждого пользователя в зависимости от используемых элементов управления навигацией на странице и глубины структуры карт узла. В любом случае, если не кэшировать структуру карт узла в `BuildSiteMap` тогда при каждом вызове потребуется повторно извлечь сведения о продукте и категории из архитектуры (что приведет к получению запроса к базе данных). Как обсуждалось в предыдущих руководствах по кэшированию, кэшированные данные могут устареть. Чтобы бороться с этим, можно использовать срок действия, основанный на зависимости времени или кэша SQL.

> [!NOTE]
> Поставщик карт узла может дополнительно переопределить [метод`Initialize`](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx). `Initialize` вызывается, когда сначала создается поставщик схемы узла и ему передаются пользовательские атрибуты, назначенные поставщику в `Web.config` элемента `<add>`, например: `<add name="name" type="type" customAttribute="value" />`. Это полезно, если необходимо разрешить разработчику страниц указывать различные параметры, связанные с поставщиком карт узла, без необходимости изменять код поставщика. Например, если мы прочитали данные категорий и продуктов непосредственно из базы данных, а не через архитектуру, мы, вероятно, хотели бы позволить разработчику страницы указать строку подключения к базе данных с помощью `Web.config` вместо использования жестко закодированного значения в коде поставщика s. Пользовательский поставщик карт узла, который будет построен на шаге 6, не переопределяет этот метод `Initialize`. Пример использования метода `Initialize` см. в статье об источнике " [Джефф Просайз](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) s" по [хранению карт сайтов в SQL Server](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) .

## <a name="step-6-creating-the-custom-site-map-provider"></a>Шаг 6. Создание пользовательского поставщика карт узла

Чтобы создать пользовательский поставщик карт узла, который строит карту узла из категорий и продуктов в базе данных Northwind, необходимо создать класс, расширяющий `StaticSiteMapProvider`. На шаге 1 я попросил добавить папку `CustomProviders` в папку `App_Code` — добавить новый класс в эту папку с именем `NorthwindSiteMapProvider`. Добавьте следующий код в класс `NorthwindSiteMapProvider` :

[!code-csharp[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample6.cs)]

Давайте начнем с изучения этого метода `BuildSiteMap` класса, который начинается с [оператора`lock`](https://msdn.microsoft.com/library/c5kehkcz.aspx). Оператор `lock` допускает вход только по одному потоку. Таким образом, он сериализует доступ к своему коду и предотвращает пошаговое выполнение двух параллельных потоков на одном другом наступал.

Переменная `SiteMapNode` уровня класса `root` используется для кэширования структуры карт узла. При создании схемы узла в первый раз или в первый раз после изменения базовых данных `root` будет `null` и структура схемы узла будет создана. Корневой узел узла Map s назначается `root` в процессе создания, поэтому при следующем вызове этого метода `root` не будет `null`. Таким образом, пока `root` не `null` структура схемы узла будет возвращена вызывающему объекту без необходимости ее повторного создания.

Если параметр root имеет значение `null`, структура схемы узла создается на основе сведений о продукте и категории. Схема узла строится путем создания `SiteMapNode` экземпляров и последующего формирования иерархии с помощью вызовов метода `StaticSiteMapProvider` класса s `AddNode`. `AddNode` выполняет внутренний бухгалтерский вход, сохраняя экземпляры `SiteMapNode` ассортимента в `Hashtable`. Прежде чем приступить к построению иерархии, начнем с вызова метода `Clear`, который удаляет элементы из внутреннего `Hashtable`. Затем метод `ProductsBLL` классов `GetProducts` и итоговые `ProductsDataTable` хранятся в локальных переменных.

Конструкция узла Map начинается с создания корневого узла и назначения его `root`. Для перегрузки [конструктора`SiteMapNode` s](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx) , используемого здесь и во всех остальных `BuildSiteMap`, передаются следующие сведения:

- Ссылка на поставщик карт узла (`this`).
- `Key``SiteMapNode`. Это обязательное значение должно быть уникальным для каждого `SiteMapNode`.
- `Url``SiteMapNode`. `Url` является необязательным, но если он указан, каждое значение `Url` `SiteMapNode` s должно быть уникальным.
- `Title``SiteMapNode`, который является обязательным.

Вызов метода `AddNode(root)` добавляет `SiteMapNode` `root` в карту узла в качестве корневого каталога. Далее перечисляются все `ProductRow` в `ProductsDataTable`. Если уже существует `SiteMapNode` для текущей категории Products, ссылка на которую имеется. В противном случае создается новый `SiteMapNode` для категории и добавляется как дочерний элемент `SiteMapNode``root` через вызов метода `AddNode(categoryNode, root)`. После того как найден или создан соответствующий узел категории `SiteMapNode`, создается `SiteMapNode` для текущего продукта и добавляется в качестве дочернего элемента категории `SiteMapNode` через `AddNode(productNode, categoryNode)`. Обратите внимание, что категория `SiteMapNode` s `Url` значение свойства `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`, а свойство Product `SiteMapNode` s `Url` назначается `~/SiteMapNode/ProductDetails.aspx?ProductID=productID`.

> [!NOTE]
> Эти продукты, имеющие `NULL` базы данных для своих `CategoryID`, группируются в категории, `SiteMapNode` свойство `Title` которого имеет значение None и для свойства `Url` задано пустая строка. Я решил присвоить `Url` пустой строке, так как метод `ProductBLL` класса s `GetProductsByCategory(categoryID)` в настоящее время не имеет возможности возвращать только те продукты, для которых `NULL` `CategoryID` значение. Кроме того, я хотел продемонстрировать, как элементы управления навигацией визуализируют `SiteMapNode`, в которой отсутствует значение для свойства `Url`. Я рекомендую расширить этот учебник таким образом, чтобы свойство None `SiteMapNode` s `Url` не указывало на `ProductsByCategory.aspx`, но только отображает продукты с `NULL` `CategoryID` значений.

После создания схемы узла произвольный объект добавляется в кэш данных с помощью зависимости кэша SQL для `Categories` и `Products` таблиц через объект `AggregateCacheDependency`. Мы изучили использование зависимостей кэша SQL в предыдущем руководстве, *используя зависимости кэша SQL*. Однако пользовательский поставщик карт узла использует перегрузку метода `Insert` кэша данных, который мы еще не просматривая. Эта перегрузка принимает в качестве окончательного входного параметра делегат, который вызывается при удалении объекта из кэша. В частности, мы передаем новый [делегат`CacheItemRemovedCallback`](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx) , указывающий на метод `OnSiteMapChanged`, определенный далее в классе `NorthwindSiteMapProvider`.

> [!NOTE]
> Представление схемы узла в памяти кэшируется с помощью переменной уровня класса `root`. Так как существует только один экземпляр пользовательского класса поставщика карт узла, и поскольку этот экземпляр является общим для всех потоков в веб-приложении, эта переменная класса выступает в качестве кэша. Метод `BuildSiteMap` также использует кэш данных, но только в качестве средства для получения уведомления при изменении данных базовой базы данных в `Categories` или в `Products` таблицах. Обратите внимание, что значение, помещаемое в кэш данных, — это только текущая дата и время. Фактические данные схемы узла *не* помещаются в кэш данных.

Метод `BuildSiteMap` завершается возвратом корневого узла схемы узла.

Остальные методы довольно просты. `GetRootNodeCore` отвечает за возврат корневого узла. Поскольку `BuildSiteMap` возвращает корень, `GetRootNodeCore` просто возвращает возвращаемое значение `BuildSiteMap` s. Метод `OnSiteMapChanged` задает `root` возвращаться к `null` при удалении элемента кэша. Если для параметра root задано значение `null`, то при следующем вызове `BuildSiteMap` будет перестроена структура схемы узла. Наконец, свойство `CachedDate` возвращает значение даты и времени, хранящееся в кэше данных, если такое значение существует. Это свойство может использоваться разработчиком страницы для определения времени последнего кэширования данных карт узла.

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>Шаг 7. Регистрация`NorthwindSiteMapProvider`

Чтобы веб-приложение использовало `NorthwindSiteMapProvider` поставщика карт узла, созданного на шаге 6, необходимо зарегистрировать его в разделе `<siteMap>` `Web.config`. В частности, добавьте следующую разметку в элемент `<system.web>` в `Web.config`:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample7.xml)]

Эта разметка состоит из двух вещей: во-первых, это означает, что встроенная `AspNetXmlSiteMapProvider` является поставщиком схемы сайта по умолчанию. Во-вторых, он регистрирует пользовательский поставщик карт узла, созданный на шаге 6, с понятным именем Northwind.

> [!NOTE]
> Для поставщиков карт веб-сайтов, расположенных в папке Application `App_Code`, значением атрибута `type` является просто имя класса. Кроме того, Пользовательский поставщик карт узла может быть создан в отдельном проекте библиотеки классов с скомпилированной сборкой, помещенной в каталог веб-приложений `/Bin` Directory. В этом случае значением атрибута `type` будет *пространство имен*. *ClassName*, *AssemblyName* .

После обновления `Web.config`Потратьте некоторое время на просмотр любой страницы из учебников в браузере. Обратите внимание, что в интерфейсе навигации слева по-прежнему отображаются разделы и учебники, определенные в `Web.sitemap`. Это связано с тем, что мы оставили `AspNetXmlSiteMapProvider` как поставщик по умолчанию. Чтобы создать элемент пользовательского интерфейса навигации, использующий `NorthwindSiteMapProvider`, необходимо явно указать, что должен использоваться поставщик карты сайта "Борей". Мы посмотрим, как это сделать на шаге 8.

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>Шаг 8. Отображение сведений о карте сайта с помощью пользовательского поставщика карт веб-узла

С помощью пользовательского поставщика карт узла, созданного и зарегистрированного в `Web.config`, мы повторно готовы к добавлению элементов управления навигацией на `Default.aspx`, `ProductsByCategory.aspx`и `ProductDetails.aspx` страниц в папке `SiteMapProvider`. Для начала откройте страницу `Default.aspx` и перетащите `SiteMapPath` из области элементов в конструктор. Элемент управления SiteMapPath находится в разделе навигации панели элементов.

[![добавить SiteMapPath в Default. aspx](building-a-custom-database-driven-site-map-provider-cs/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image18.gif)

**Рис. 16**. Добавление элемента SiteMapPath в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image20.gif))

Элемент управления SiteMapPath отображает навигатор, указывающий расположение текущей страницы в карте узла. Мы добавили SiteMapPath в верхнюю часть главной страницы в учебнике « *главные страницы» и «Навигация по сайту* ».

Уделите несколько минут для просмотра этой страницы в браузере. Для SiteMapPath, добавленной на рис. 16, используется поставщик карт сайта по умолчанию, который извлекает данные из `Web.sitemap`. Таким образом, Навигатор показывает домашнюю &gt; настроить карту узла, как в верхнем правом углу.

[![навигатор использует поставщик карт сайта по умолчанию](building-a-custom-database-driven-site-map-provider-cs/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image21.gif)

**Рис. 17**. Навигатор использует поставщик карт сайта по умолчанию ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image23.gif))

Чтобы добавить SiteMapPath на рис. 16, используйте настраиваемый поставщик карт узла, созданный на шаге 6, присвойте [свойству`SiteMapProvider`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx) значение Northwind, имя, которое мы присвоили `NorthwindSiteMapProvider` в `Web.config`. К сожалению, конструктор по умолчанию использует поставщик карт сайта, но если вы посещаете страницу через браузер после изменения этого свойства, вы увидите, что навигатор теперь использует пользовательский поставщик карт узла.

[![навигатор теперь использует пользовательский поставщик карт веб-узла Норсвиндситемаппровидер](building-a-custom-database-driven-site-map-provider-cs/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image24.gif)

**Рис. 18**. Теперь навигатор использует пользовательский поставщик карт веб-узла `NorthwindSiteMapProvider` ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image26.gif))

Элемент управления SiteMapPath отображает более функциональный пользовательский интерфейс на страницах `ProductsByCategory.aspx` и `ProductDetails.aspx`. Добавьте к этим страницам элемент SiteMapPath, установив для свойства `SiteMapProvider` в значение Northwind. В `Default.aspx` щелкните ссылку Просмотреть продукты для напитков, а затем щелкните ссылку Просмотреть сведения для Чай Chai. Как показано на рис. 19, Навигатор включает в себя текущий раздел схемы узла (Чай Chai) и его предков: напитки и все категории.

[![навигатор теперь использует пользовательский поставщик карт веб-узла Норсвиндситемаппровидер](building-a-custom-database-driven-site-map-provider-cs/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image21.png)

**Рис. 19**. Теперь навигатор использует пользовательский поставщик карт веб-узла `NorthwindSiteMapProvider` ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image22.png))

Другие элементы пользовательского интерфейса навигации можно использовать в дополнение к SiteMapPath, например к элементам управления Menu и TreeView. Страницы `Default.aspx`, `ProductsByCategory.aspx`и `ProductDetails.aspx` в загружаемом руководстве, например все элементы управления меню (см. рис. 20). Более подробные сведения о элементах управления навигацией и системе карт узла в ASP.NET 2,0 см. в разделе [изучение функций навигации по сайту ASP.NET 2,0 s](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) и раздела [Использование элементов управления навигацией по веб-сайту](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx) в [ASP.NET 2,0](https://quickstarts.asp.net/QuickStartv20/aspnet/) .

[![элемент управления Menu содержит список категорий и продуктов](building-a-custom-database-driven-site-map-provider-cs/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image28.gif)

**Рис. 20**. в элементе управления Menu перечислены категории и продукты ([щелкните, чтобы просмотреть изображение с полным размером](building-a-custom-database-driven-site-map-provider-cs/_static/image30.gif)).

Как упоминалось ранее в этом руководстве, структуру схемы узла можно получить программно с помощью класса `SiteMap`. Следующий код возвращает корневой `SiteMapNode` поставщика по умолчанию:

[!code-csharp[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample8.cs)]

Поскольку `AspNetXmlSiteMapProvider` является поставщиком по умолчанию для нашего приложения, приведенный выше код возвращает корневой узел, определенный в `Web.sitemap`. Для ссылки на поставщика карт узла, отличного от значения по умолчанию, используйте [свойство](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx) `SiteMap` классов`Providers` следующим образом:

[!code-csharp[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample9.cs)]

Где *Name* — имя пользовательского поставщика карт узла (Northwind для нашего веб-приложения).

Чтобы получить доступ к элементу, характерному для поставщика карт узла, используйте `SiteMap.Providers["name"]`, чтобы получить экземпляр поставщика, а затем приведите его к соответствующему типу. Например, чтобы отобразить свойство `NorthwindSiteMapProvider` s `CachedDate` на странице ASP.NET, используйте следующий код:

[!code-csharp[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample10.cs)]

> [!NOTE]
> Обязательно протестируйте функцию зависимости кэша SQL. После посещения страниц `Default.aspx`, `ProductsByCategory.aspx`и `ProductDetails.aspx` перейдите к одному из руководств в разделе Редактирование, вставка и удаление и измените имя категории или продукта. Затем вернитесь на одну из страниц в папке `SiteMapProvider`. Предполагая, что для механизма опроса было достаточно времени, чтобы отметить изменение базовой базы данных, необходимо обновить карту узла, чтобы отобразить имя нового продукта или категории.

## <a name="summary"></a>Сводка

ASP.NET 2,0 s Map Features включает класс `SiteMap`, ряд встроенных веб-элементов управления навигацией и поставщик карт узла по умолчанию, который предполагает сохранение сведений о карте узла в XML-файле. Чтобы использовать сведения о карте узла из другого источника, например из базы данных, архитектуры приложения или удаленной веб-службы, необходимо создать пользовательский поставщик карт узла. Это подразумевает создание класса, прямо или косвенно производного от класса `SiteMapProvider`.

В этом учебнике мы рассмотрели создание пользовательского поставщика карт узла, который основывается на карте узла на продуктах и категориях, исключающих из архитектуры приложения. Наш поставщик расширил класс `StaticSiteMapProvider` и, в своюмся, создает метод `BuildSiteMap`, который извлекает данные, разстроил иерархию карт узла и кэширует полученную структуру в переменной уровня класса. Мы использовали зависимость кэша SQL с функцией обратного вызова, чтобы сделать кэшированную структуру недействительной при изменении базовых `Categories` или `Products` данных.

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Хранение карт сайтов в SQL Server](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) и [поставщику карты узла SQL, который вы ожидаете](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)
- [Взгляд на модель поставщика ASP.NET 2,0 s](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [Набор средств поставщика](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [Изучение функций навигации по сайту ASP.NET 2,0 s](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого руководства: Дейв Гарднер, Зак Jones, Терезой Мерфи и Бернадетте Леигх. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Вперед](building-a-custom-database-driven-site-map-provider-vb.md)
