---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
title: Общие сведения о вставке, обновлении и удалении данных (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы рассмотрим, как сопоставлять методы вставки (), Update () и Delete () ObjectDataSource с методами классов BLL, а также как конфигу...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 35b40b8f-2ca8-4ab3-9c19-f361a91a3647
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 79491118ba1cbbc8c1b67ca9646a817d941f17ba
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74630928"
---
# <a name="an-overview-of-inserting-updating-and-deleting-data-vb"></a>Общие сведения о вставке, обновлении и удалении данных (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_VB.exe) или [Загрузка PDF-файла](an-overview-of-inserting-updating-and-deleting-data-vb/_static/datatutorial16vb1.pdf)

> В этом учебнике мы рассмотрим, как сопоставлять методы вставки (), Update () и Delete () ObjectDataSource с методами классов BLL, а также как настроить элементы управления GridView, DetailsView и FormView для предоставления возможностей изменения данных.

## <a name="introduction"></a>Введение

В нескольких прошлых учебных курсах мы рассмотрели, как отображать данные на странице ASP.NET с помощью элементов управления GridView, DetailsView и FormView. Эти элементы управления просто работают с предоставляемыми им данными. Как правило, эти элементы управления обращаются к данным с помощью элемента управления источниками данных, например ObjectDataSource. Мы увидели, как элемент управления ObjectDataSource выступает в качестве прокси-сервера между страницей ASP.NET и базовыми данными. Когда GridView необходимо отображать данные, он вызывает метод `Select()` ObjectDataSource, который, в свою очередь, вызывает метод из уровня бизнес-логики (BLL), который вызывает метод в соответствующем адаптере (DAL) уровня доступа к данным, который, в свою очередь, отправляет запрос `SELECT` в базу данных Northwind.

Вспомним, что при создании TableAdapters в DAL в [первом учебном курсе](../introduction/creating-a-data-access-layer-cs.md)Visual Studio автоматически добавила методы для вставки, обновления и удаления данных из базовой таблицы базы данных. Более того, при [создании уровня бизнес-логики](../introduction/creating-a-business-logic-layer-vb.md) мы разработали в BLL методы, которые вызывали эти методы DAL по изменению данных.

В дополнение к методу `Select()`, ObjectDataSource также имеет методы `Insert()`, `Update()`и `Delete()`. Как и метод `Select()`, эти три метода можно сопоставить с методами в базовом объекте. При настройке для вставки, обновления или удаления данных элементы управления GridView, DetailsView и FormView предоставляют пользовательский интерфейс для изменения базовых данных. Этот пользовательский интерфейс вызывает методы `Insert()`, `Update()`и `Delete()` ObjectDataSource, которые затем вызывают связанные с ним методы базового объекта (см. рис. 1).

[![методы вставки (), обновления () и удаления () ObjectDataSource являются прокси-сервером в BLL](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image1.png)

**Рис. 1**. методы `Insert()`, `Update()`и `Delete()` ObjectDataSource являются прокси-сервером в BLL ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image3.png))

В этом учебнике мы рассмотрим, как сопоставлять методы `Insert()`, `Update()`и `Delete()` ObjectDataSource с методами классов в BLL, а также как настроить элементы управления GridView, DetailsView и FormView для предоставления возможностей изменения данных.

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>Шаг 1. Создание веб-страниц учебников по вставке, обновлению и удалению

Прежде чем начать изучение вставки, обновления и удаления данных, давайте сначала создадим страницы ASP.NET в нашем проекте веб-сайта, которые понадобятся для работы с этим руководством и следующих нескольких. Для начала добавьте новую папку с именем `EditInsertDelete`. Затем добавьте в эту папку следующие страницы ASP.NET, чтобы связать каждую страницу с главной страницей `Site.master`:

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![Добавление страниц ASP.NET для руководств, связанных с изменением данных](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image4.png)

**Рис. 2**. добавление страниц ASP.NET для руководств, связанных с изменением данных

Как и в других папках, `Default.aspx` в папке `EditInsertDelete` будут перечислены учебники в разделе. Вспомним, что `SectionLevelTutorialListing.ascx` пользовательский элемент управления предоставляет эти функции. Таким образом, добавьте этот пользовательский элемент управления в `Default.aspx`, перетащив его из обозреватель решений на представление конструирования страницы.

[![добавить пользовательский элемент управления SectionLevelTutorialListing. ascx в Default. aspx](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image5.png)

**Рис. 3**. Добавление пользовательского элемента управления `SectionLevelTutorialListing.ascx` в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image7.png))

Наконец, добавьте страницы в качестве записей в файл `Web.sitemap`. В частности, добавьте следующую разметку после настраиваемого `<siteMapNode>`форматирования:

[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample1.xml)]

После обновления `Web.sitemap`просмотрите веб-сайт учебников в браузере. В меню слева теперь содержатся элементы для учебников по редактированию, вставке и удалению.

![На карте веб-узла теперь есть записи для учебников по редактированию, вставке и удалению.](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image8.png)

**Рис. 4**. схема узла теперь включает в себя записи для руководства по редактированию, вставке и удалению

## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>Шаг 2. Добавление и настройка элемента управления ObjectDataSource

Поскольку GridView, DetailsView и FormView имеют разные возможности изменения данных и макет, давайте рассмотрим каждый из них по отдельности. Однако, вместо того, чтобы каждый элемент управления использовал собственный объект ObjectDataSource, давайте создадим только один объект ObjectDataSource, который может совместно использоваться всеми тремя примерами элементов управления.

Откройте страницу `Basics.aspx`, перетащите элемент управления ObjectDataSource из области элементов в конструктор и щелкните ссылку Настроить источник данных из своего смарт-тега. Поскольку `ProductsBLL` является единственным классом BLL, предоставляющим методы редактирования, вставки и удаления, настройте ObjectDataSource для использования этого класса.

[![настроить ObjectDataSource для использования класса ProductsBLL](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image9.png)

**Рис. 5**. Настройка ObjectDataSource для использования класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image11.png))

На следующем экране можно указать, какие методы класса `ProductsBLL` сопоставляются `Select()`, `Insert()`, `Update()`и `Delete()` ObjectDataSource, выбрав соответствующую вкладку и выбрав метод из раскрывающегося списка. Рис. 6, который должен выглядеть знакомым, теперь сопоставляет метод `Select()` ObjectDataSource с методом `GetProducts()` класса `ProductsBLL`. Методы `Insert()`, `Update()`и `Delete()` можно настроить, выбрав соответствующую вкладку в верхней части списка.

[![, что ObjectDataSource возвращает все продукты](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image12.png)

**Рис. 6**. возвращение всех продуктов с помощью ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image14.png))

На рисунках 7, 8 и 9 показаны вкладки обновления, вставки и удаления элемента управления ObjectDataSource. Настройте эти вкладки таким образом, чтобы методы `Insert()`, `Update()`и `Delete()` вызывали методы `UpdateProduct`, `AddProduct`и `DeleteProduct` класса `ProductsBLL` соответственно.

[![привяжите метод Update () ObjectDataSource к методу UpdateProduct класса Продуктблл](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image15.png)

**Рис. 7**. сопоставьте метод `Update()` ObjectDataSource с методом `UpdateProduct` класса `ProductBLL` ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image17.png))

[![сопоставлять метод вставки () ObjectDataSource с методом AddProduct класса Продуктблл](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image18.png)

**Рис. 8**. привязка метода `Insert()` ObjectDataSource к методу Add `Product` класса `ProductBLL` ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image20.png))

[![соотнести метод Delete () ObjectDataSource с методом DeleteProduct класса Продуктблл](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image21.png)

**Рис. 9**. сопоставьте метод `Delete()` ObjectDataSource с методом `DeleteProduct` класса `ProductBLL` ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image23.png))

Возможно, вы заметили, что в раскрывающихся списках на вкладках обновления, вставки и удаления уже были выбраны эти методы. Это спасибо за использование `DataObjectMethodAttribute`, которые оформляют методы `ProductsBLL`. Например, метод DeleteProduct имеет следующую сигнатуру:

[!code-vb[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample2.vb)]

Атрибут `DataObjectMethodAttribute` указывает назначение каждого метода — выбор, вставка, обновление или удаление, а также значение по умолчанию. Если эти атрибуты пропущены при создании классов BLL, необходимо вручную выбрать эти методы на вкладках обновление, вставка и удаление.

Убедившись, что соответствующие методы `ProductsBLL` сопоставляются с методами `Insert()`, `Update()`и `Delete()` ObjectDataSource, нажмите кнопку Готово, чтобы завершить работу мастера.

## <a name="examining-the-objectdatasources-markup"></a>Проверка разметки ObjectDataSource

После настройки ObjectDataSource с помощью мастера перейдите к представлению исходного кода, чтобы проверить созданную декларативную разметку. Тег `<asp:ObjectDataSource>` указывает базовый объект и методы для вызова. Кроме того, существуют `DeleteParameters`, `UpdateParameters`и `InsertParameters`, которые сопоставляются с входными параметрами для методов `AddProduct`, `UpdateProduct`и `DeleteProduct` класса `ProductsBLL`:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample3.aspx)]

ObjectDataSource включает параметр для каждого из входных параметров для связанных с ним методов, так же как список `SelectParameter` s присутствует, когда ObjectDataSource настроен для вызова метода Select, ожидающего входного параметра (например, `GetProductsByCategoryID(categoryID)`). Как скоро будет видно, значения этих `DeleteParameters`, `UpdateParameters`и `InsertParameters` задаются автоматически с помощью элементов управления GridView, DetailsView и FormView перед вызовом метода `Insert()`, `Update()`или `Delete()` ObjectDataSource. Эти значения также можно задать программным способом, как описано в следующем учебном курсе.

Одним из побочных эффектов использования мастера для настройки ObjectDataSource является то, что Visual Studio устанавливает для [свойства OldValuesParameterFormatString](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx) значение `original_{0}`. Это значение свойства используется для включения исходных значений изменяемых данных и полезно в двух сценариях:

- Если при редактировании записи пользователь может изменить значение первичного ключа. В этом случае необходимо предоставить новое значение первичного ключа и исходное значение первичного ключа, чтобы можно было найти запись с исходным значением первичного ключа и соответствующим образом обновить его значение.
- При использовании оптимистичного параллелизма. Оптимистическая блокировка — это метод, гарантирующий, что два одновременно работающих пользователя не перезапишут изменения, и это раздел для будущего руководства.

Свойство `OldValuesParameterFormatString` указывает имя входных параметров в методах Update и DELETE базового объекта для исходных значений. Мы обсудим это свойство и его назначение более подробно при рассмотрении оптимистичного параллелизма. Однако я выберу его сейчас, так как методы BLL не предполагают исходные значения, поэтому важно удалить это свойство. Если для свойства `OldValuesParameterFormatString` задано значение, отличное от значения по умолчанию (`{0}`), то при попытке веб-элемента управления данными вызвать методы `Update()` или `Delete()` будет возникать ошибка, так как ObjectDataSource попытается передать как `UpdateParameters`, так и `DeleteParameters`, как и исходные параметры значения.

Если это не совсем понятно в этом присоединении ке, не беспокойтесь, мы рассмотрим это свойство и его служебную программу в следующем учебном курсе. Сейчас нужно просто удалить это объявление свойства целиком из декларативного синтаксиса или установить значение по умолчанию ({0}).

> [!NOTE]
> Если вы просто удаляете значение свойства `OldValuesParameterFormatString` из окно свойств в представление конструирования, оно по-прежнему будет существовать в декларативном синтаксисе, но должно быть задано как пустая строка. Это, увы, по-прежнему приведет к возникновению описанной выше проблемы. Поэтому либо удалите свойство из декларативного синтаксиса, либо из окно свойств, установите значение по умолчанию `{0}`.

## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>Шаг 3. Добавление веб-элемента управления данными и его настройка для изменения данных

После того как ObjectDataSource добавлен на страницу и настроен, мы готовы к добавлению веб-элементов управления данными на страницу, чтобы отобразить данные и предоставить пользователю возможность изменить их. Мы будем просматривать GridView, DetailsView и FormView отдельно, так как эти веб-элементы управления данными отличаются возможностями и конфигурацией изменения данных.

Как мы увидим в оставшейся части этой статьи, Добавление базовой поддержки редактирования, вставки и удаления с помощью элементов управления GridView, DetailsView и FormView — это так же просто, как проверка нескольких флажков. В реальной среде существует множество тонкостей и пограничных вариантов, которые обеспечивают более функциональную функциональность, чем просто наpointсь и щелкая. Тем не менее, в этом учебнике основное внимание уделяется исключительно упрощению возможностей изменения данных. В следующих учебных курсах будут рассмотрены проблемы, которые, как нереальности, будут возникать в реальных параметрах.

## <a name="deleting-data-from-the-gridview"></a>Удаление данных из GridView

Начните с перетаскивания элемента управления GridView с панели инструментов в конструктор. Затем привяжите ObjectDataSource к GridView, выбрав его из раскрывающегося списка в смарт-теге GridView. На этом этапе декларативная разметка GridView будет выглядеть следующим образом:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample4.aspx)]

Привязка элемента управления GridView к ObjectDataSource через его смарт-тег имеет два преимущества:

- BoundFields и Чеккбоксфиелдс создаются автоматически для каждого поля, возвращаемого ObjectDataSource. Более того, свойства BoundField и CheckBoxField задаются на основе метаданных базового поля. Например, поля `ProductID`, `CategoryName`и `SupplierName` помечаются как доступные только для чтения в `ProductsDataTable` и поэтому не должны обновляться при редактировании. Для этого [свойства ReadOnly](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx) BoundFields имеют значение `True`.
- [Свойству DataKeyNames](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx) присваивается поле первичного ключа базового объекта. Это важно при использовании элемента управления GridView для редактирования или удаления данных, так как это свойство указывает поле (или набор полей), уникально идентифицирующее каждую запись. Дополнительные сведения о свойстве `DataKeyNames` см. в разделе " [основной/подробности" с помощью выбираемого справочника по GridView с подробным](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) руководством по DetailView.

Хотя GridView можно привязать к ObjectDataSource через окно свойств или декларативный синтаксис, это требует ручного добавления соответствующей разметки BoundField и `DataKeyNames`.

Элемент управления GridView обеспечивает встроенную поддержку редактирования и удаления на уровне строк. Настройка GridView для поддержки удаления добавляет столбец кнопок удаления. Когда пользователь нажимает кнопку Удалить для определенной строки, выполняется обратная передача, и GridView выполняет следующие действия:

1. Значения `DeleteParameters` ObjectDataSource назначены
2. Вызывается метод `Delete()` ObjectDataSource, удаляя указанную запись
3. Элемент управления GridView повторно привязывается к ObjectDataSource, вызывая метод `Select()`

Значения, присваиваемые `DeleteParameters`, являются значениями полей `DataKeyNames` строки, для которых была нажата кнопка Delete. Поэтому крайне важно, чтобы свойство `DataKeyNames` GridView было правильно установлено. Если он отсутствует, `DeleteParameters` будет присвоено значение `Nothing` на шаге 1, что, в свою очередь, не приведет к удалению записей на шаге 2.

> [!NOTE]
> Коллекция `DataKeys` хранится в состоянии управления GridView s, что означает, что `DataKeys` значения будут сохраняться в обратной передаче, даже если состояние представления GridView s было отключено. Однако очень важно, чтобы состояние представления оставалось включенным для элементов управления GridView, поддерживающих редактирование или удаление (поведение по умолчанию). Если для свойства `EnableViewState` GridView s задано значение `false`, то поведение редактирования и удаления будет работать для одного пользователя, но при наличии одновременных пользователей удаление данных существует вероятность того, что эти одновременные пользователи могут случайно удалить или изменить записи, которые им не планировалось. См. мою запись блога, [Предупреждение: проблемы параллелизма с ASP.NET 2,0 gridviews/DetailsView/FormView, которые поддерживают редактирование и (или) удаление, а состояние представления — отключено](http://scottonwriting.net/sowblog/posts/10054.aspx), для получения дополнительных сведений.

Это же предупреждение также относится к DetailsView и FormView.

Чтобы добавить возможности удаления в GridView, просто перейдите к смарт-тегу и установите флажок Включить удаление.

![Установите флажок "включить удаление".](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image24.png)

**Рис. 10**. Установка флажка "включить удаление"

Установка флажка "включить удаление" из смарт-тега добавляет CommandField в GridView. CommandField визуализирует столбец в GridView с кнопками для выполнения одной или нескольких следующих задач: Выбор записи, изменение записи и удаление записи. Ранее мы видели CommandField в действии с выбором записей в [главной и подробной среде с помощью выбираемого главного элемента управления GridView с учебником Details DetailView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) .

CommandField содержит ряд свойств `ShowXButton`, которые указывают, какие ряды кнопок отображаются в CommandField. Установив флажок Enable (включить удаление) CommandField, свойство `ShowDeleteButton` которого `True`, было добавлено в коллекцию Columns GridView.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample5.aspx)]

На этом этапе вы считаете, что он или нет, мы сделали Добавление поддержки удаления в GridView! Как показано на рис. 11, при посещении этой страницы через браузер имеется столбец с кнопками «удалить».

[![CommandField добавляет столбец кнопок удаления](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image25.png)

**Рис. 11**. CommandField добавляет столбец кнопок удаления ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image27.png))

Если вы создаете этот учебник с нуля самостоятельно, при тестировании этой страницы нажатие кнопки удалить вызовет исключение. Продолжайте чтение, чтобы узнать, почему были вызваны эти исключения и как их исправить.

> [!NOTE]
> Если вы используете загрузку, прилагаемую к этому учебнику, эти проблемы уже были внесены в учетную запись. Однако я рекомендую ознакомиться с приведенными ниже сведениями, чтобы определить проблемы, которые могут возникнуть и подходящие решения.

Если при попытке удалить продукт вы получаете исключение, сообщение о котором похоже на "*ObjectDataSource ' ObjectDataSource1 ' не может найти неуниверсальный метод ' DeleteProduct ', имеющий параметры: ProductID, original\_ProductID*, вероятно, вы забыли удалить свойство `OldValuesParameterFormatString` из ObjectDataSource. Если указано свойство `OldValuesParameterFormatString`, ObjectDataSource пытается передать в метод `DeleteProduct` `productID` и `original_ProductID` входные параметры. Однако `DeleteProduct`принимает только один входной параметр, поэтому это исключение. Удаление свойства `OldValuesParameterFormatString` (или присвоение ему значения `{0}`) заставляет ObjectDataSource не пытаться передать исходный входной параметр.

[![убедитесь, что свойство OldValuesParameterFormatString было удалено.](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image28.png)

**Рис. 12**. Убедитесь, что свойство `OldValuesParameterFormatString` было удалено ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image30.png))

Даже если вы удалили свойство `OldValuesParameterFormatString`, по-прежнему возникает исключение при попытке удалить продукт с сообщением: "*инструкция DELETE конфликтует с ссылочным ограничением FK\_Order\_details\_Products"* . База данных Northwind содержит ограничение внешнего ключа между `Order Details` и `Products` таблицей, что означает, что продукт нельзя удалить из системы, если для него есть одна или несколько записей в таблице `Order Details`. Так как каждый продукт в базе данных Northwind имеет по крайней мере одну запись в `Order Details`, мы не можем удалить какие бы то ни было продукты, пока не удалим соответствующие записи о заказах продукта.

[![ограничение внешнего ключа запрещает удаление продуктов](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image31.png)

**Рис. 13**. ограничение внешнего ключа запрещает удаление продуктов ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image33.png))

В нашем руководстве мы просто удалим все записи из таблицы `Order Details`. В реальном приложении необходимо выполнить одно из следующих действий:

- Наличие другого экрана для управления сведениями о заказах
- Расширение метода `DeleteProduct` для включения логики для удаления указанных сведений о заказе продукта
- Изменение SQL запроса, используемого TableAdapter для включения удаления указанных сведений о заказе продукта

Просто удалим все записи из таблицы `Order Details`, чтобы обойти ограничение внешнего ключа. Перейдите в обозреватель сервера в Visual Studio, щелкните правой кнопкой мыши узел `NORTHWND.MDF` и выберите команду Создать запрос. Затем в окне запроса выполните следующую инструкцию SQL: `DELETE FROM [Order Details]`

[![удалить все записи из таблицы Order Details](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image34.png)

**Рис. 14**. Удаление всех записей из таблицы `Order Details` ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image36.png))

После очистки `Order Details` таблице нажатие кнопки удалить приведет к удалению продукта без ошибок. Если нажатие кнопки удалить не приводит к удалению продукта, убедитесь, что для свойства `DataKeyNames` GridView установлено значение поля первичный ключ (`ProductID`).

> [!NOTE]
> При нажатии кнопки "Удалить" происходит обратная передача, и запись удаляется. Это может быть опасно, поскольку несложно случайно нажать кнопку "Удалить" в неверной строке. В следующем учебном курсе мы покажем, как добавить подтверждение на стороне клиента при удалении записи.

## <a name="editing-data-with-the-gridview"></a>Изменение данных с помощью GridView

Вместе с удалением элемент управления GridView также предоставляет встроенную поддержку редактирования на уровне строк. Настройка элемента управления GridView для поддержки редактирования добавляет столбец кнопок редактирования. С точки зрения конечного пользователя нажатие кнопки Правка строки приводит к тому, что эта строка становится редактируемой, а ячейки переходят в текстовые поля, содержащие существующие значения, и заменяют кнопку изменить кнопками обновления и отмены. После внесения необходимых изменений конечный пользователь может нажать кнопку обновить, чтобы сохранить изменения, или кнопку Отмена, чтобы отменить их. В любом случае после нажатия кнопки Обновить или отмена GridView возвращается в состояние предварительного редактирования.

С нашей точки зрения разработчик страницы, когда пользователь нажимает кнопку "Изменить" для определенной строки, выполняется обратная передача, и GridView выполняет следующие действия:

1. Свойство `EditItemIndex` GridView присвоено индексу строки, для которой была нажата кнопка "Изменить"
2. Элемент управления GridView повторно привязывается к ObjectDataSource, вызывая метод `Select()`
3. Индекс строки, соответствующий `EditItemIndex`, подготавливается к просмотру в режиме правки. В этом режиме кнопка "Изменить" заменяется кнопками обновления и отмены и BoundFields, свойства `ReadOnly` которых имеют значение false (по умолчанию), отображаются как веб-элементы управления TextBox, `Text` свойства которых присваиваются значениям полей данных.

На этом этапе в браузер возвращается разметка, позволяющая конечному пользователю вносить любые изменения в данные строки. Когда пользователь нажимает кнопку "Обновить", происходит обратная передача, и GridView выполняет следующие действия:

1. `UpdateParameters` значениям ObjectDataSource присваиваются значения, вводимых конечным пользователем в интерфейс редактирования GridView.
2. Вызывается метод `Update()` ObjectDataSource, который обновляет указанную запись
3. Элемент управления GridView повторно привязывается к ObjectDataSource, вызывая метод `Select()`

Значения первичного ключа, назначенные `UpdateParameters` на шаге 1, берутся из значений, указанных в свойстве `DataKeyNames`, тогда как значения непервичного ключа берутся из текста в веб-элементах управления TextBox для редактируемой строки. Как и при удалении, крайне важно, чтобы свойство `DataKeyNames` GridView было правильно установлено. Если он отсутствует, `UpdateParameters` значение первичного ключа будет присвоено значение `Nothing` на шаге 1, что, в свою очередь, не приведет к обновлению записей на шаге 2.

Функциональность редактирования можно активировать, просто установив флажок Включить редактирование в смарт-теге GridView.

![Установите флажок Enable Edit (включить редактирование).](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image37.png)

**Рис. 15**. Установка флажка "включить редактирование"

Установка флажка Enable Edit (включить редактирование) добавит CommandField (при необходимости) и присвойте свойству `ShowEditButton` значение `True`. Как мы видели ранее, CommandField содержит ряд свойств `ShowXButton`, которые указывают, какие серии кнопок отображаются в CommandField. Установив флажок Enable Edit (включить редактирование), вы добавите свойство `ShowEditButton` к существующему CommandField:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample6.aspx)]

Это все, что необходимо для добавления поддержки элементарного редактирования. Как показано в Figure16, интерфейс правки грубый каждый BoundField, свойство `ReadOnly` которого имеет значение `False` (значение по умолчанию) подготавливается к просмотру как текстовое поле. Сюда входят такие поля, как `CategoryID` и `SupplierID`, которые являются ключами к другим таблицам.

[![нажатии кнопки "Изменить" в списке Chai s отображает строку в режиме редактирования](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image38.png)

**Рис. 16**. нажатие кнопки "Изменить" в списке Chai s отображает строку в режиме редактирования ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image40.png))

Помимо предоставления пользователям возможности изменять значения внешних ключей напрямую, интерфейс интерфейса правки не имеет следующих отличий.

- Если пользователь вводит `CategoryID` или `SupplierID`, которых нет в базе данных, `UPDATE` будет нарушать ограничение внешнего ключа, что приведет к возникновению исключения.
- Интерфейс редактирования не включает проверку. Если не указано требуемое значение (например, `ProductName`) или введите строковое значение, в котором ожидается числовое значение (например, введите "слишком много!"). в текстовое поле `UnitPrice`) будет создано исключение. В следующем учебнике будет рассмотрено Добавление элементов управления проверки в пользовательский интерфейс редактирования.
- Сейчас *все* поля продуктов, которые не предназначены только для чтения, должны быть включены в GridView. Если бы было необходимо удалить поле из GridView, скажем `UnitPrice`, при обновлении данных GridView не задаст значение `UnitPrice` `UpdateParameters`, что привело бы к изменению `UnitPrice` записи базы данных на `NULL` значение. Аналогичным образом, если обязательное поле, например `ProductName`, удаляется из GridView, обновление завершится ошибкой с тем же «*Column ' ProductName ' не допускает значения NULL*», упомянутого выше.
- Форматирование интерфейса редактирования оставляет массу необходимости. `UnitPrice` отображается с четырьмя десятичными точками. В идеале значения `CategoryID` и `SupplierID` будут содержать элементов управления DropDownList, в которых перечислены категории и поставщики в системе.

Это все недостатки, с которыми мы будем жить сейчас, но они будут рассмотрены в следующих руководствах.

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>Вставка, изменение и удаление данных с помощью элемента DetailsView

Как мы видели в предыдущих учебных курсах, элемент управления DetailsView отображает по одной записи за раз и, как GridView, позволяет изменять и удалять отображаемую в данный момент запись. Опыт конечного пользователя, редактирующий и удаляющий элементы из элемента DetailsView и рабочего процесса из ASP.NET, идентичен элементу GridView. Если элемент DetailsView отличается от GridView, он также предоставляет встроенную поддержку вставки.

Чтобы продемонстрировать возможности изменения данных GridView, начните с добавления элемента DetailsView на страницу `Basics.aspx` над существующим элементом управления GridView и привяжите его к существующему ObjectDataSource через смарт-тег DetailsView. Затем очистите свойства `Height` и `Width` DetailsView, а также установите флажок Включить разбиение по страницам в смарт-теге. Чтобы включить поддержку редактирования, вставки и удаления, просто установите флажки Включить редактирование, включить вставку и включить удаление в смарт-теге.

![Настройка элемента DetailsView для поддержки редактирования, вставки и удаления](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image41.png)

**Рис. 17**. Настройка DetailsView для поддержки редактирования, вставки и удаления

Как и в случае с GridView, Добавление поддержки правки, вставки или удаления добавляет CommandField к элементу DetailsView, как показано в следующем декларативном синтаксисе:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample7.aspx)]

Обратите внимание, что для DetailsView CommandField по умолчанию отображается в конце коллекции Columns. Поскольку поля DetailsView подготавливаются к просмотру как строки, CommandField отображается в виде строки с кнопками вставки, правки и удаления в нижней части элемента DetailsView.

[![настроить DetailsView для поддержки редактирования, вставки и удаления](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image42.png)

**Рис. 18**. Настройка элемента DetailsView для поддержки редактирования, вставки и удаления ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image44.png))

При нажатии кнопки "Удалить" начинается та же последовательность событий, что и для GridView: обратная передача. после чего элемент управления DetailsView заполняет `DeleteParameters` на основе значений `DataKeyNames`; и завершился с вызовом метода `Delete()` ObjectDataSource, который фактически удаляет продукт из базы данных. Редактирование в DetailsView также работает точно так же, как GridView.

Для вставки конечного пользователя отображается новая кнопка, которая при нажатии отображает DetailsView в режиме вставки. При использовании "режима вставки" Новая кнопка заменяется кнопками вставки и отмены и только те BoundFields, для которых свойство `InsertVisible` имеет значение `True` (по умолчанию). Эти поля данных, идентифицируемые как поля автоприращения, такие как `ProductID`, имеют [свойство инсертвисибле](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx) со значением `False` при привязке элемента DetailsView к источнику данных через смарт-тег.

При привязке источника данных к элементу DetailsView через смарт-тег Visual Studio устанавливает свойство `InsertVisible` в значение `False` только для полей автоприращения. Поля, предназначенные только для чтения, такие как `CategoryName` и `SupplierName`, будут отображаться в пользовательском интерфейсе "режим вставки", если только для свойства `InsertVisible` явно не задано значение `False`. Потратьте немного времени, чтобы задать для этих двух полей `InsertVisible` свойства `False`, с помощью декларативного синтаксиса DetailsView или ссылки Edit Fields (изменить поля) в смарт-теге. На рис. 19 показано, как задать свойства `InsertVisible` для `False`, щелкнув ссылку Edit Fields (изменить поля).

[![Northwind Traders теперь предлагает ACME чай](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image45.png)

**Рис. 19**. Теперь компания Northwind Traders предлагает ACME-чай ([щелкните, чтобы просмотреть изображение полного размера](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image47.png))

После задания свойств `InsertVisible` просмотрите страницу `Basics.aspx` в браузере и нажмите кнопку Создать. На рис. 20 показана DetailsView при добавлении нового напитков, Acme чай в нашу линейку продуктов.

[![Northwind Traders теперь предлагает ACME чай](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image48.png)

**Рис. 20**. Теперь компания Northwind Traders предлагает ACME чай ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image50.png))

После ввода сведений для «Acme» и нажатия кнопки «Вставить» происходит обратная передача, а новая запись добавляется в таблицу базы данных `Products`. Так как эта DetailsView перечисляет продукты в порядке, в котором они существуют в таблице базы данных, для просмотра нового продукта необходимо выполнить страницу до последнего продукта.

[![сведения о чай](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image51.png)

**Рисунок 21**. сведения для «Acme» ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image53.png))

> [!NOTE]
> [Свойство куррентмоде](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx) элемента DetailsView указывает отображаемый интерфейс и может принимать одно из следующих значений: `Edit`, `Insert`или `ReadOnly`. [Свойство DefaultMode](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx) указывает режим, в который элемент DetailsView возвращает значение после завершения операции правки или вставки. он удобен для отображения элемента DetailsView, который постоянно находится в режиме правки или вставки.

Точка и щелчок функции вставки и правки элемента управления DetailsView пострадает от тех же ограничений, что и GridView: пользователь должен ввести существующие `CategoryID` и `SupplierID` значения через текстовое поле. в интерфейсе отсутствует логика проверки. все поля продуктов, которые не допускают `NULL` значений или не имеют значения по умолчанию, заданного на уровне базы данных, должны быть включены в интерфейс вставки и т. д.

Методы, которые мы рассмотрим для расширения и улучшения интерфейса редактирования GridView в будущих статьях, можно также применить к интерфейсам правки и вставки элемента управления DetailsView.

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>Использование элемента FormView для более гибкого пользовательского интерфейса изменения данных

FormView предлагает встроенную поддержку вставки, редактирования и удаления данных, но поскольку в ней используются шаблоны вместо полей, нет места для добавления BoundFields или CommandField, используемых элементами управления GridView и DetailsView для предоставления данных. интерфейс изменения. Вместо этого интерфейс веб-элементов управления для сбора вводимых пользователем данных при добавлении нового элемента или редактировании существующего объекта вместе с кнопками создать, изменить, удалить, вставить, обновить и отменить необходимо вручную добавить в соответствующие шаблоны. К счастью, Visual Studio автоматически создаст необходимый интерфейс при привязке элемента FormView к источнику данных с помощью раскрывающегося списка в смарт-теге.

Чтобы продемонстрировать эти методы, начните с добавления элемента управления FormView на страницу `Basics.aspx` и из смарт-тега FormView привяжите его к уже созданному ObjectDataSource. Это приведет к созданию `EditItemTemplate`, `InsertItemTemplate`и `ItemTemplate` для элемента управления FormView с TextBox для получения веб-элементов управления ввода и кнопок пользователя для кнопок создать, изменить, удалить, вставить, обновить и отменить. Кроме того, для свойства `DataKeyNames` FormView задается поле первичного ключа (`ProductID`) объекта, возвращаемого ObjectDataSource. Наконец, установите флажок Включить разбиение по страницам в смарт-теге FormView.

Ниже показана декларативная разметка для `ItemTemplate` FormView после привязки элемента управления FormView к ObjectDataSource. По умолчанию каждое поле продукта, не являющегося логическим значением, привязано к свойству `Text` элемента управления Label, тогда как каждое поле логического значения (`Discontinued`) привязано к свойству `Checked` отключенного веб-элемента управления CheckBox. Чтобы кнопки создания, изменения и удаления вызывали определенное поведение FormView при щелчке, необходимо установить для их `CommandName` значения `New`, `Edit`и `Delete`соответственно.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample8.aspx)]

На рис. 22 показано `ItemTemplate` FormView при просмотре в браузере. Каждое поле продукта отображается с кнопками создать, изменить и удалить внизу.

[![Дефаут FormView ItemTemplate содержит список всех полей продуктов, а также кнопки "создать", "Изменить" и "Удалить".](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image54.png)

**Рис. 22**. дефаут FormView `ItemTemplate` список всех полей продуктов вместе с кнопками "создать", "Изменить" и "Удалить" ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image56.png))

Как и в случае с GridView и DetailsView, нажатием кнопки удалить или любой кнопкой, LinkButton или ImageButton, свойство `CommandName` которого имеет значение Delete, вызывает обратную передачу, заполняет `DeleteParameters` ObjectDataSource на основе значения `DataKeyNames` FormView и вызывает метод `Delete()` ObjectDataSource.

При нажатии кнопки "Изменить" происходит обратная передача данных, и данные повторно привязываются к `EditItemTemplate`, которая отвечает за визуализацию интерфейса редактирования. Этот интерфейс включает веб-элементы управления для редактирования данных вместе с кнопками обновления и отмены. `EditItemTemplate` по умолчанию, создаваемая Visual Studio, содержит метку для всех полей автоприращения (`ProductID`), текстовое поле для каждого поля значения, не являющегося логическим, и флажок для каждого поля логического значения. Такое поведение очень похоже на автоматическое создание BoundFields в элементах управления GridView и DetailsView.

> [!NOTE]
> Одной из мелких проблем с автосозданием `EditItemTemplate` FormView является то, что она отображает веб-элементы управления TextBox для полей, доступных только для чтения, таких как `CategoryName` и `SupplierName`. В ближайшее время мы увидим, как это учитывать.

Элементы управления TextBox в `EditItemTemplate` имеют свойства `Text`, привязанные к значению соответствующего поля данных с помощью *двухсторонней привязки*. Двусторонняя привязка, обозначенная `<%# Bind("dataField") %>`, выполняет привязку данных как при привязке к шаблону, так и при заполнении параметров ObjectDataSource для вставки или изменения записей. То есть когда пользователь нажимает кнопку "Изменить" в `ItemTemplate`, метод `Bind()` возвращает указанное значение поля данных. После того как пользователь вносит изменения и нажимает кнопку обновить, значения, соответствующие полям данных, указанным с помощью `Bind()`, применяются к `UpdateParameters`у ObjectDataSource. Кроме того, односторонняя привязка, обозначающая `<%# Eval("dataField") %>`, извлекает значения полей данных только при привязке данных к шаблону и *не* возвращает значения, вводимых пользователем, в параметры источника данных при обратной передаче.

В следующей декларативной разметке показано `EditItemTemplate`FormView. Обратите внимание, что метод `Bind()` используется в синтаксисе привязки данных, и для веб-элементов управления "обновление" и "Отмена" заданы соответствующие свойства `CommandName`.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample9.aspx)]

На этом этапе наш `EditItemTemplate`вызовет исключение при попытке использовать его. Проблема заключается в том, что поля `CategoryName` и `SupplierName` отображаются как веб-элементы управления TextBox в `EditItemTemplate`. Необходимо изменить эти текстовые поля на метки или полностью удалить их. Давайте просто удалим их полностью из `EditItemTemplate`.

На рис. 23 показан элемент FormView в браузере после нажатия кнопки Edit (изменить) для Chai. Обратите внимание, что поля `SupplierName` и `CategoryName`, показанные в `ItemTemplate`, больше не существуют, так как они были удалены из `EditItemTemplate`. При нажатии кнопки "перейти" FormView выполняет ту же последовательность шагов, что и элементы управления GridView и DetailsView.

[![по умолчанию в EditItemTemplate показывается каждое редактируемое поле продукта в виде текстового поля или флажка](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image57.png)

**Рис. 23**. по умолчанию в `EditItemTemplate` отображаются все редактируемые поля продуктов в виде текстового поля или флажка ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image59.png)).

Когда вы нащелкнули кнопку "вставить", `ItemTemplate` подается обратная передача. Однако данные не привязаны к элементу FormView, так как добавляется новая запись. Интерфейс `InsertItemTemplate` включает веб-элементы управления для добавления новой записи вместе с кнопками вставки и отмены. `InsertItemTemplate` по умолчанию, создаваемая Visual Studio, содержит текстовое поле для каждого поля значения, не являющегося логическим, и флажок для каждого поля логического значения, аналогично автоматически созданному интерфейсу `EditItemTemplate`. Элементы управления TextBox имеют свойство `Text`, привязанное к значению соответствующего поля данных, используя двустороннюю привязку данных.

В следующей декларативной разметке показано `InsertItemTemplate`FormView. Обратите внимание, что метод `Bind()` используется в синтаксисе привязки данных, и для веб-элементов управления "Вставка" и "Отмена" заданы соответствующие свойства `CommandName`.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample10.aspx)]

Существует тонкость автоматического создания `InsertItemTemplate`в FormView. В частности, веб-элементы управления TextBox создаются даже для тех полей, которые доступны только для чтения, например `CategoryName` и `SupplierName`. Как и в случае с `EditItemTemplate`, необходимо удалить эти текстовые поля из `InsertItemTemplate`.

На рис. 24 показан элемент FormView в браузере при добавлении нового продукта, Acme кофе. Обратите внимание, что поля `SupplierName` и `CategoryName`, показанные в `ItemTemplate`, больше не существуют, так как они были удалены. При нажатии кнопки «Вставить» FormView выполняет ту же последовательность шагов, что и элемент управления DetailsView, добавляя новую запись в таблицу `Products`. На рис. 25 показаны сведения о продукте ACME кофе в элементе FormView после его вставки.

[![InsertItemTemplate определяет интерфейс вставки FormView](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image60.png)

**Рис. 24**. `InsertItemTemplate` определяет интерфейс вставки FormView ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image62.png))

[![сведения о новом продукте, Acme кофе, отображаются в элементе FormView.](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image63.png)

**Рис. 25**. сведения о новом продукте, Acme кофе, отображаются в элементе FormView ([щелкните, чтобы просмотреть изображение с полным размером](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image65.png)).

Разделив интерфейсы только для чтения, редактирования и вставки на три отдельных шаблона, FormView обеспечивает более тонкую степень контроля над этими интерфейсами, чем DetailsView и GridView.

> [!NOTE]
> Как и DetailsView, свойство `CurrentMode` FormView указывает отображаемый интерфейс, а его свойство `DefaultMode` указывает режим, в который функция FormView возвращает значение после завершения операции редактирования или вставки.

## <a name="summary"></a>Сводка

В этом учебнике мы рассмотрели основы вставки, редактирования и удаления данных с помощью элементов управления GridView, DetailsView и FormView. Все три этих элемента управления предоставляют определенный уровень встроенных возможностей изменения данных, которые можно использовать без написания единой строки кода на странице ASP.NET благодаря веб-элементам управления данными и ObjectDataSource. Однако простые методы Point и Click отображают довольно фраил и наивный пользовательский интерфейс изменения данных. Чтобы обеспечить проверку, внедрять программные значения, корректно обрабатывать исключения, настраивать пользовательский интерфейс и т. д., необходимо полагаться на множество методов, которые будут обсуждаться в следующих нескольких руководствах.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Назад](limiting-data-modification-functionality-based-on-the-user-cs.md)
> [Вперед](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
