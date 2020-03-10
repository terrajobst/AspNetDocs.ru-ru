---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
title: Отображение данных с помощью ObjectDataSource (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике рассматривается элемент управления ObjectDataSource, использующий этот элемент управления. Вы можете привязать данные, полученные из BLL, созданного в предыдущем руководстве, без Хави...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d62c3a63-0940-4019-874e-4a4047df0c1c
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 754188352cbfb08e610027f5b7890a32bd88ae26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483054"
---
# <a name="displaying-data-with-the-objectdatasource-vb"></a>Отображение данных с помощью элемента управления ObjectDataSource (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_4_VB.exe) или [Загрузка PDF-файла](displaying-data-with-the-objectdatasource-vb/_static/datatutorial04vb1.pdf)

> В этом учебнике рассматривается элемент управления ObjectDataSource, использующий этот элемент управления. Вы можете привязать данные, полученные из BLL, созданного в предыдущем учебном курсе, без необходимости писать строчку кода!

## <a name="introduction"></a>Введение

Теперь, когда архитектура приложения и макет страницы веб-сайта завершены, мы готовы приступить к изучению способов выполнения разнообразных задач, связанных с данными и отчетами. В предыдущих руководствах мы рассмотрели, как программно привязывать данные из DAL и BLL к веб-элементу управления данными на странице ASP.NET. Этот синтаксис назначает свойство `DataSource` веб-элемента управления данными для отображаемых данных, а затем вызывает метод `DataBind()` элемента управления в качестве шаблона, используемого в приложениях ASP.NET 1. x, и может продолжать использовать в приложениях 2,0. Однако новые элементы управления источниками данных ASP.NET 2.0 обеспечивают декларативный способ работы с данными. С помощью этих элементов управления можно привязывать данные, полученные из BLL, созданного в предыдущем учебном курсе, без написания кода!

ASP.NET 2,0 поставляется с пятью встроенными элементами управления источниками данных: [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)и [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx) , хотя при необходимости можно создавать собственные [пользовательские элементы управления источниками данных](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp). Поскольку мы разработали архитектуру для нашего учебного приложения, мы будем использовать ObjectDataSource для наших классов BLL.

![ASP.NET 2,0 включает пять встроенных элементов управления источниками данных](displaying-data-with-the-objectdatasource-vb/_static/image1.png)

**Рис. 1**. ASP.NET 2,0 включает пять встроенных элементов управления источниками данных

Элемент управления ObjectDataSource выступает в качестве прокси-сервера для работы с другим объектом. Чтобы настроить ObjectDataSource, мы указываем этот базовый объект и как его методы сопоставляются с методами `Select`, `Insert`, `Update`и `Delete` ObjectDataSource. После указания этого базового объекта и его методов, сопоставленных с ObjectDataSource, можно привязать ObjectDataSource к веб-элементу управления данными. ASP.NET поставляется с множеством веб-элементов управления данными, включая GridView, DetailsView, RadioButtonList и DropDownList, среди прочих. Во время жизненного цикла страницы для веб-элемента управления данными может потребоваться доступ к данным, к которым он привязан, что достигается путем вызова метода `Select` элемента ObjectDataSource. Если веб-элемент управления данными поддерживает вставку, обновление или удаление, то могут выполняться вызовы методов `Insert`, `Update`или `Delete` ObjectDataSource. Затем эти вызовы направляются ObjectDataSource в соответствующие методы базового объекта, как показано на следующей схеме.

[![элемент управления ObjectDataSource выступает в качестве прокси-сервера](displaying-data-with-the-objectdatasource-vb/_static/image3.png)](displaying-data-with-the-objectdatasource-vb/_static/image2.png)

**Рис. 2**. элемент управления ObjectDataSource выступает в качестве учетной записи-посредника ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image4.png))

Хотя ObjectDataSource можно использовать для вызова методов для вставки, обновления или удаления данных, давайте просто рассмотрим возврат данных. в следующих учебных курсах рассматривается использование веб-элементов управления ObjectDataSource и Data, изменяющих данные.

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>Шаг 1. Добавление и настройка элемента управления ObjectDataSource

Для начала откройте страницу `SimpleDisplay.aspx` в папке `BasicReporting`, переключитесь на представление конструирования, а затем перетащите элемент управления ObjectDataSource с панели элементов на область конструктора страницы. Элемент управления ObjectDataSource отображается в области конструктора в виде серого прямоугольника, так как он не создает никакой разметки. Он просто обращается к данным, вызывая метод из указанного объекта. Данные, возвращаемые ObjectDataSource, могут отображаться веб-элементом управления данными, таким как GridView, DetailsView, FormView и т. д.

> [!NOTE]
> Кроме того, можно сначала добавить веб-элемент управления данными на страницу, а затем из смарт-тега выбрать параметр &lt;создать источник данных&gt; из раскрывающегося списка.

Чтобы указать базовый объект ObjectDataSource и способ его соответствия методам объекта ObjectDataSource, щелкните ссылку Настроить источник данных из смарт-тега ObjectDataSource.

[![щелкните ссылку Настройка источника данных из смарт-тега.](displaying-data-with-the-objectdatasource-vb/_static/image6.png)](displaying-data-with-the-objectdatasource-vb/_static/image5.png)

**Рис. 3**. Щелкните ссылку Настройка источника данных из смарт-тега ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image7.png))

Откроется мастер настройки источника данных. Сначала необходимо указать объект, с которым будет работать элемент управления ObjectDataSource. Если установлен флажок "Показывать только компоненты данных", раскрывающийся список на этом экране содержит только те объекты, которые были дополнены атрибутом `DataObject`. В настоящее время наш список включает адаптеры таблиц в типизированном наборе данных и классы BLL, созданные в предыдущем руководстве. Если вы забыли добавить атрибут `DataObject` к классам уровня бизнес-логики, они не будут отображаться в этом списке. В этом случае снимите флажок "Показывать только компоненты данных", чтобы просмотреть все объекты, которые должны содержать классы BLL (вместе с другими классами в типизированном наборе DataSet, DataTables, DataRow и т. д.).

На первом экране выберите класс `ProductsBLL` из раскрывающегося списка и нажмите кнопку Далее.

[![указать объект для использования с элементом управления ObjectDataSource](displaying-data-with-the-objectdatasource-vb/_static/image9.png)](displaying-data-with-the-objectdatasource-vb/_static/image8.png)

**Рис. 4**. Указание объекта для использования с элементом управления ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image10.png))

На следующем экране мастера появится запрос на выбор метода, который должен вызывать элемент управления ObjectDataSource. Раскрывающийся список содержит методы, возвращающие данные в объекте, выбранном на предыдущем экране. Здесь мы видим `GetProductByProductID`, `GetProducts`, `GetProductsByCategoryID`и `GetProductsBySupplierID`. Выберите метод `GetProducts` из раскрывающегося списка и нажмите кнопку "Готово" (если вы добавили `DataObjectMethodAttribute` в методы `ProductBLL`, как показано в предыдущем руководстве, этот параметр будет выбран по умолчанию).

[![выбор метода возврата данных на вкладке «Выбор»](displaying-data-with-the-objectdatasource-vb/_static/image12.png)](displaying-data-with-the-objectdatasource-vb/_static/image11.png)

**Рис. 5**. Выбор метода возврата данных на вкладке "выбор" ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image13.png))

## <a name="configure-the-objectdatasource-manually"></a>Настройка ObjectDataSource вручную

Мастер настройки источников данных ObjectDataSource позволяет быстро указать используемый объект и определить, какие методы объекта вызываются. Однако можно настроить ObjectDataSource с помощью его свойств либо с помощью окно свойств, либо непосредственно в декларативной разметке. Просто задайте для свойства `TypeName` тип используемого базового объекта, а `SelectMethod` методу, который будет вызываться при извлечении данных.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample1.aspx)]

Даже если вы предпочитаете Мастер настройки источников данных, может возникнуть необходимость ручной настройки ObjectDataSource, так как мастер отображает только классы, созданные разработчиком. Если необходимо привязать ObjectDataSource к классу в .NET Framework например, в [классе членства](https://msdn.microsoft.com/library/system.web.security.membership.aspx), для доступа к сведениям об учетной записи пользователя или к [классу каталога](https://msdn.microsoft.com/library/system.io.directory.aspx) для работы со сведениями файловой системы, необходимо вручную задать свойства ObjectDataSource.

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>Шаг 2. Добавление веб-элемента управления данными и его привязка к ObjectDataSource

После того как ObjectDataSource добавлен на страницу и настроен, мы готовы к добавлению веб-элементов управления данными на страницу для вывода данных, возвращаемых методом `Select` ObjectDataSource. Любой веб-элемент управления данными может быть привязан к элементу ObjectDataSource; Рассмотрим отображение данных ObjectDataSource в элементе управления GridView, DetailsView и FormView.

## <a name="binding-a-gridview-to-the-objectdatasource"></a>Привязка элемента управления GridView к элементу управления ObjectDataSource

Добавление элемента управления GridView из панели элементов в область конструктора `SimpleDisplay.aspx`. В смарт-теге GridView выберите элемент управления ObjectDataSource, добавленный на шаге 1. Это автоматически создаст BoundField в GridView для каждого свойства, возвращаемого данными из метода `Select` ObjectDataSource (а именно, свойства, определенные в таблице Products.).

[![элемент GridView добавлен на страницу и привязан к элементу управления ObjectDataSource](displaying-data-with-the-objectdatasource-vb/_static/image15.png)](displaying-data-with-the-objectdatasource-vb/_static/image14.png)

**Рис. 6**. элемент управления GridView добавлен на страницу и привязан к элементу ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image16.png))

Затем можно настроить, изменить или удалить BoundFields GridView, щелкнув параметр Edit Columns (изменить столбцы) в смарт-теге.

[![управления BoundFields GridView с помощью диалогового окна "изменение столбцов"](displaying-data-with-the-objectdatasource-vb/_static/image18.png)](displaying-data-with-the-objectdatasource-vb/_static/image17.png)

**Рис. 7**. Управление BoundFields GridView с помощью диалогового окна "изменение столбцов" ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image19.png))

Уделите немного времени, чтобы изменить BoundFields GridView, удалив `ProductID`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitsInStock`, `UnitsOnOrder`и `ReorderLevel` BoundFields. Просто выберите BoundField из списка в левом нижнем углу и нажмите кнопку Удалить (красный значок X), чтобы удалить их. Затем измените расположение BoundFields, чтобы `CategoryName` и `SupplierName` BoundFields предшествовать `UnitPrice` BoundField, выбрав эти BoundFields и щелкнув стрелку вверх. Задайте для свойств `HeaderText` оставшихся BoundFields значения `Products`, `Category`, `Supplier`и `Price`соответственно. Затем по`Price` BoundField в формате валюты, задав для свойства `HtmlEncode` BoundField значение false, а для свойства `DataFormatString` значение `{0:c}`. Наконец, выровняйте `Price` по правому краю и `Discontinued` флажок в центре через свойство `ItemStyle`/`HorizontalAlign`.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

[![были настроены BoundFields GridView](displaying-data-with-the-objectdatasource-vb/_static/image21.png)](displaying-data-with-the-objectdatasource-vb/_static/image20.png)

**Рис. 8**. BoundFields GridView были настроены ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image22.png))

## <a name="using-themes-for-a-consistent-look"></a>Использование тем для единообразного вида

Эти учебники посвящены удалению любых параметров стиля уровня элемента управления, вместо этого при необходимости можно использовать каскадные таблицы стилей, определенные во внешнем файле. Файл `Styles.css` содержит классы CSS `DataWebControlStyle`, `HeaderStyle`, `RowStyle`и `AlternatingRowStyle`, которые следует использовать для диктовки внешнего вида веб-элементов управления данными, используемых в этих учебниках. Для этого можно задать для свойства `CssClass` GridView значение `DataWebControlStyle`, а также свойства `HeaderStyle`, `RowStyle`и `AlternatingRowStyle` свойства `CssClass` соответственно.

Если установить эти `CssClass` свойства в веб-элементе управления, нам нужно не забывать явно задавать значения этих свойств для каждого и каждого веб-элемента управления данными, добавляемых в наши руководства. Более управляемый подход заключается в определении свойств, связанных с CSS по умолчанию для элементов управления GridView, DetailsView и FormView, с помощью темы. Тема — это коллекция параметров свойств уровня элементов управления, изображений и классов CSS, которые можно применить к страницам на сайте для обеспечения общего внешнего вида и поведения.

Наша тема не будет включать изображения или файлы CSS (мы будем оставлять таблицу стилей `Styles.css` "как есть", определенную в корневой папке веб-приложения), но будет содержать две обложки. Обложка — это файл, который определяет свойства по умолчанию для веб-элемента управления. В частности, у нас будет файл обложки для элементов управления GridView и DetailsView, указывающий свойства, связанные с `CssClass`по умолчанию.

Для начала добавьте новый файл обложки в проект с именем `GridView.skin`, щелкнув правой кнопкой мыши имя проекта в обозреватель решений и выбрав пункт Добавить новый элемент.

[![добавить файл обложки с именем GridView. Skin](displaying-data-with-the-objectdatasource-vb/_static/image24.png)](displaying-data-with-the-objectdatasource-vb/_static/image23.png)

**Рис. 9**. Добавление файла обложки с именем `GridView.skin` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image25.png))

Файлы обложки необходимо поместить в тему, расположенную в папке `App_Themes`. Так как у нас еще нет такой папки, Visual Studio будет предлагать создать ее для нас при добавлении нашей первой обложки. Нажмите кнопку Да, чтобы создать папку `App_Theme` и поместить в нее новый файл `GridView.skin`.

[![позволить Visual Studio создать App_Theme папку](displaying-data-with-the-objectdatasource-vb/_static/image27.png)](displaying-data-with-the-objectdatasource-vb/_static/image26.png)

**Рис. 10**. Разрешите Visual Studio создать папку `App_Theme` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image28.png))

Будет создана новая тема в папке `App_Themes` с именем GridView с файлом обложки `GridView.skin`.

![Тема GridView добавлена в папку App_Theme](displaying-data-with-the-objectdatasource-vb/_static/image29.png)

**Рис. 11**. Тема GridView добавлена в папку `App_Theme`

Переименуйте тему GridView в WebControl (щелкните правой кнопкой мыши папку GridView в папке `App_Theme` и выберите пункт Переименовать). Затем введите в файл `GridView.skin` следующую разметку:

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample3.aspx)]

Это определяет свойства по умолчанию для свойств, связанных с `CssClass`, для любого элемента управления GridView на любой странице, использующей тему WebControl. Давайте добавим еще одну обложку DetailsView, веб-элемент управления данными, который скоро будет использоваться. Добавьте новую обложку в тему WebControl с именем `DetailsView.skin` и добавьте следующую разметку:

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample4.aspx)]

После определения темы последним шагом является применение темы к нашей ASP.NET странице. Тему можно применять к отдельным страницам или ко всем страницам на веб-сайте. Давайте будем использовать эту тему для всех страниц на веб-сайте. Для этого добавьте следующую разметку в раздел `<system.web>` `Web.config`:

[!code-xml[Main](displaying-data-with-the-objectdatasource-vb/samples/sample5.xml)]

Это все. Параметр `styleSheetTheme` указывает, что свойства, заданные в теме, *не* должны переопределять свойства, заданные на уровне элемента управления. Чтобы указать, что параметры темы должны закозырить параметры управления, вместо `styleSheetTheme`используйте `theme` атрибут. к сожалению, параметры темы не отображаются в представление конструирования Visual Studio. Дополнительные сведения о темах и обложках см. в разделе [Общие сведения о темах и обложках ASP.NET](https://msdn.microsoft.com/library/ykzx33wh.aspx) и [стили на стороне сервера с помощью тем](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx) . Дополнительные сведения о настройке страницы для использования темы см. [в разделе Практические руководства. применение ASP.NET тем](https://msdn.microsoft.com/library/0yy5hxdk%28VS.80%29.aspx) .

[![элементе GridView отображаются название продукта, категория, поставщик, Цена и неподдерживаемые сведения.](displaying-data-with-the-objectdatasource-vb/_static/image31.png)](displaying-data-with-the-objectdatasource-vb/_static/image30.png)

**Рис. 12**. Отображение имени продукта, категории, поставщика, цены и неподдерживаемой информации в элементе GridView ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image32.png))

## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>Отображение одной записи за раз в элементе DetailsView

Элемент GridView отображает по одной строке для каждой записи, возвращенной элементом управления источником данных, к которому он привязан. Однако бывают ситуации, когда нам нужно отобразить единственную запись или только одну запись за раз. [Элемент управления DetailsView](https://msdn.microsoft.com/library/s3w1w7t4.aspx) предлагает эту функцию, который готовится к просмотру как HTML-`<table>` с двумя столбцами и одной строкой для каждого столбца или свойства, привязанного к элементу управления. Можно представить DetailsView как GridView с одной записью, повернутой на 90 градусов.

Начните с добавления элемента управления DetailsView *над* GridView в `SimpleDisplay.aspx`. Затем привяжите его к тому же элементу управления ObjectDataSource, что и GridView. Как и в GridView, BoundField будет добавлен к элементу DetailsView для каждого свойства в объекте, возвращаемом методом `Select` ObjectDataSource. Единственное отличие заключается в том, что BoundFields DetailsView располагаются горизонтально, а не вертикально.

[![добавить элемент DetailsView на страницу и привязать его к элементу управления ObjectDataSource](displaying-data-with-the-objectdatasource-vb/_static/image34.png)](displaying-data-with-the-objectdatasource-vb/_static/image33.png)

**Рис. 13**. Добавление элемента DetailsView на страницу и привязка его к ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image35.png))

Как и GridView, BoundFields элемента DetailsView можно настроить таким образом, чтобы обеспечить более настраиваемое отображение данных, возвращаемых ObjectDataSource. На рис. 14 показана DetailsView после того, как свойства BoundFields и `CssClass` были настроены таким образом, чтобы его внешний вид был похож на пример GridView.

[![элемент DetailsView показывает одну запись](displaying-data-with-the-objectdatasource-vb/_static/image37.png)](displaying-data-with-the-objectdatasource-vb/_static/image36.png)

**Рис. 14**. элемент DetailsView отображает одну запись ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image38.png))

Обратите внимание, что элемент DetailsView отображает только первую запись, возвращенную ее источником данных. Чтобы разрешить пользователю выполнять все записи по отдельности, необходимо включить разбиение по страницам DetailsView. Для этого вернитесь в Visual Studio и установите флажок Включить разбиение по страницам в смарт-теге DetailsView.

[![включить разбиение по страницам в элементе управления DetailsView](displaying-data-with-the-objectdatasource-vb/_static/image40.png)](displaying-data-with-the-objectdatasource-vb/_static/image39.png)

**Рис. 15**. Включение разбиения по страницам в элементе управления DetailsView ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image41.png))

[![с включенным разбиением на страницы DetailsView позволяет пользователю просматривать любой из продуктов.](displaying-data-with-the-objectdatasource-vb/_static/image43.png)](displaying-data-with-the-objectdatasource-vb/_static/image42.png)

**Рис. 16**. при включенном разбиении по страницам DetailsView позволяет пользователю просматривать любой из продуктов ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image44.png)).

Дополнительные сведения о разбиении на страницы см. в следующих руководствах.

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>Более гибкий макет для отображения одной записи за раз

Элемент DetailsView очень жестко показывает, как он отображает каждую запись, возвращенную из ObjectDataSource. Нам может потребоваться более гибкое представление данных. Например, вместо отображения названия продукта, категории, поставщика, цены и сведений о неподдерживаемой информации в отдельной строке нам может потребоваться показать название и цену продукта в заголовке `<h4>`, а сведения о категории и поставщике отображаются под названием и ценой меньшего размера шрифта. И мы можем не позаботиться о названиях свойств (продукт, Категория и т. д.) рядом со значениями.

[Элемент управления FormView](https://msdn.microsoft.com/library/fyf1dk77.aspx) обеспечивает этот уровень настройки. Вместо использования полей (таких как GridView и DetailsView), FormView использует шаблоны, которые позволяют использовать сочетание веб-элементов управления, статического HTML и [синтаксиса привязки данных](http://www.15seconds.com/issue/040630.htm). Если вы знакомы с элементом управления Repeater из ASP.NET 1. x, вы можете представить FormView как Repeater для отображения одной записи.

Добавление элемента управления FormView в рабочую область конструктора `SimpleDisplay.aspx` страницы. Изначально FormView отображается в виде серого блока, что информирует нас о том, что необходимо предоставить, как минимум, `ItemTemplate`элемента управления.

[![FormView должен включать ItemTemplate](displaying-data-with-the-objectdatasource-vb/_static/image46.png)](displaying-data-with-the-objectdatasource-vb/_static/image45.png)

**Рис. 17**. элемент FormView должен включать `ItemTemplate` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image47.png))

Можно привязать FormView непосредственно к элементу управления источника данных с помощью смарт-тега FormView, который автоматически создает `ItemTemplate` по умолчанию (вместе с `EditItemTemplate` и `InsertItemTemplate`, если заданы свойства `InsertMethod` и `UpdateMethod` элемента управления ObjectDataSource). Однако в этом примере мы выполним привязку данных к FormView и указываем его `ItemTemplate` вручную. Начните с установки свойства `DataSourceID` FormView в `ID` элемента управления ObjectDataSource `ObjectDataSource1`. Затем создайте `ItemTemplate` таким образом, чтобы он отображал название и цену продукта в `<h4>` элементе, а названия категорий и грузоотправителей под меньшим размером шрифта.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample6.aspx)]

[![первый продукт (Chai) отображается в пользовательском формате](displaying-data-with-the-objectdatasource-vb/_static/image49.png)](displaying-data-with-the-objectdatasource-vb/_static/image48.png)

**Рис. 18**. первый продукт (Chai) отображается в настраиваемом формате ([щелкните, чтобы просмотреть изображение с полным размером](displaying-data-with-the-objectdatasource-vb/_static/image50.png))

`<%# Eval(propertyName) %>` является синтаксисом привязки данных. Метод `Eval` возвращает значение указанного свойства для текущего объекта, привязанного к элементу управления FormView. Ознакомьтесь со статьей об [упрощенном и расширенном синтаксисе привязки данных в ASP.NET 2,0](http://www.15seconds.com/issue/040630.htm) , чтобы получить дополнительные сведения о Homer данных.

Как и DetailsView, FormView показывает только первую запись, возвращенную из ObjectDataSource. Можно включить разбиение по страницам в FormView, чтобы посетители могли пошагово прокручивать продукты по одному за раз.

## <a name="summary"></a>Сводка

Доступ к данным уровня бизнес-логики и их отображение могут осуществляться без написания строки кода благодаря элементу управления ObjectDataSource в ASP.NET 2.0. ObjectDataSource вызывает указанный метод класса и возвращает результаты. Эти результаты могут отображаться в веб-элементе управления данными, привязанном к ObjectDataSource. В этом учебнике мы рассматривали привязку элементов управления GridView, DetailsView и FormView к элементу ObjectDataSource.

До сих пор мы видели, как использовать ObjectDataSource для вызова метода без параметров, но что если бы мы хотим вызвать метод, который предполагает ввод входных параметров, например `GetProductsByCategoryID(categoryID)`класса `ProductBLL`? Чтобы вызвать метод, который ожидает один или несколько параметров, необходимо настроить ObjectDataSource для указания значений этих параметров. Мы посмотрим, как это сделать в [следующем руководстве](declarative-parameters-vb.md).

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные материалы

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Создание собственных элементов управления источниками данных](https://msdn.microsoft.com/library/ms364049.aspx)
- [Примеры GridView для ASP.NET 2,0](https://msdn.microsoft.com/library/aa479339.aspx)
- [Упрощенный и расширенный синтаксис привязки данных в ASP.NET 2,0](http://www.15seconds.com/issue/040630.htm)
- [Темы в ASP.NET 2,0](http://www.odetocode.com/Articles/423.aspx)
- [Стили на стороне сервера, использующие темы](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [Как программно применить темы ASP.NET](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Хилтон Гизнау. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
> [Вперед](declarative-parameters-vb.md)
