---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
title: Вставка, обновление и удаление данных с помощью элемента SqlDataSource (VB) | Документация Майкрософт
author: rick-anderson
description: В предыдущих руководствах мы узнали, как элемент управления ObjectDataSource допускает вставку, обновление и удаление данных. Элемент управления SqlDataSource поддерживает t...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9673bef3-892c-45ba-a7d8-0da3d6f48ec5
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 4f7b282b09769272df8ff3a32aa4c509c8917481
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508338"
---
# <a name="inserting-updating-and-deleting-data-with-the-sqldatasource-vb"></a>Вставка, обновление и удаление данных с помощью элемента управления SqlDataSource (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_VB.exe) или [Загрузка PDF-файла](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/datatutorial49vb1.pdf)

> В предыдущих руководствах мы узнали, как элемент управления ObjectDataSource допускает вставку, обновление и удаление данных. Элемент управления SqlDataSource поддерживает те же операции, но подход отличается, и в этом руководстве показано, как настроить SqlDataSource для вставки, обновления и удаления данных.

## <a name="introduction"></a>Введение

Как обсуждалось в [обзоре вставки, обновления и удаления](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md), элемент управления GridView предоставляет встроенные возможности обновления и удаления, а элементы управления DetailsView и FormView включают поддержку вставки вместе с функциями редактирования и удаления. Эти возможности изменения данных могут быть подключены непосредственно к элементу управления источника данных без необходимости написания строки кода. [Общие сведения о вставке, обновлении и удалении](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) , проверенном с помощью ObjectDataSource, для упрощения вставки, обновления и удаления элементов управления GridView, DetailsView и FormView. Кроме того, можно использовать SqlDataSource вместо ObjectDataSource.

Вспомним, что для поддержки вставки, обновления и удаления с помощью ObjectDataSource нам требовалось указать методы уровня объектов, которые нужно вызвать для выполнения операции вставки, обновления или удаления. С помощью SqlDataSource необходимо предоставить для выполнения `INSERT`, `UPDATE`и `DELETE` инструкции SQL (или хранимые процедуры). Как будет показано в этом учебнике, эти инструкции можно создать вручную или автоматически создать с помощью мастера настройки источника данных SqlDataSource s.

> [!NOTE]
> Поскольку мы уже обсуждали возможности вставки, правки и удаления элементов управления GridView, DetailsView и FormView, в этом учебнике основное внимание уделяется настройке элемента управления SqlDataSource для поддержки этих операций. Если вам нужно придерживаться реализации этих функций в GridView, DetailsView и FormView, вернитесь к учебникам по редактированию, вставке и удалению данных, начиная с [обзора вставки, обновления и удаления](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md).

## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>Шаг 1. Указание`INSERT`,`UPDATE`и инструкций`DELETE`

Как мы видели в прошлых двух учебниках, для получения данных из элемента управления SqlDataSource необходимо задать два свойства:

1. `ConnectionString`, указывающий базу данных, в которую отправляется запрос, и
2. `SelectCommand`, указывающий нерегламентированную инструкцию SQL или имя хранимой процедуры, которую необходимо выполнить для возврата результатов.

Для `SelectCommand` значений с параметрами значения параметров задаются с помощью коллекции SqlDataSource s `SelectParameters` и могут включать жестко запрограммированные значения, общие значения источника параметров (поля строки запроса, переменные сеанса, значения веб-элементов управления и т. д.), а также могут быть назначены программно. Когда метод `Select()` элемента управления SqlDataSource вызывается программно или автоматически из веб-элемента управления данными, устанавливается соединение с базой данных, значения параметров присваиваются запросу, а команда переключается в базу данных. Затем результаты возвращаются как набор данных или DataReader, в зависимости от значения свойства `DataSourceMode` управления.

Помимо выбора данных, элемент управления SqlDataSource можно использовать для вставки, обновления и удаления данных путем предоставления `INSERT`, `UPDATE`и `DELETE` инструкций SQL точно так же. Просто назначьте `InsertCommand`, `UpdateCommand`и `DeleteCommand` свойства `INSERT`, `UPDATE`и `DELETE` инструкций SQL для выполнения. Если инструкции имеют параметры (как правило, они всегда будут), включите их в коллекции `InsertParameters`, `UpdateParameters`и `DeleteParameters`.

После того как было задано значение `InsertCommand`, `UpdateCommand`или `DeleteCommand`, будет доступен параметр Разрешить вставку, включение редактирования или Включение удаления в соответствующем смарт-теге веб-элемента управления данными. Чтобы проиллюстрировать это, давайте возьмем пример на странице `Querying.aspx`, созданной в [запросах данных, с помощью учебника по элементу управления SqlDataSource](querying-data-with-the-sqldatasource-control-vb.md) и дополнить его для включения возможностей удаления.

Для начала откройте `InsertUpdateDelete.aspx` и `Querying.aspx` страницы из папки `SqlDataSource`. В конструкторе на странице `Querying.aspx` выберите SqlDataSource и GridView из первого примера (элементы управления `ProductsDataSource` и `GridView1`). Выбрав два элемента управления, перейдите в меню Правка и выберите команду Копировать (или просто нажмите клавиши CTRL + C). Затем перейдите в конструктор `InsertUpdateDelete.aspx` и вставьте элементы управления. После перемещения этих двух элементов управления на `InsertUpdateDelete.aspx`протестируйте страницу в браузере. Должны отобразиться значения столбцов `ProductID`, `ProductName`и `UnitPrice` для всех записей в таблице `Products` базы данных.

[![перечислены все продукты, упорядоченные по ProductID](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.png)

**Рис. 1**. перечисляются все продукты, упорядоченные по `ProductID` ([щелкните, чтобы просмотреть изображение с полным размером](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.png))

## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>Добавление свойств SqlDataSource`DeleteCommand`и`DeleteParameters`

На этом этапе у нас есть средство SqlDataSource, которое просто возвращает все записи из таблицы `Products` и GridView, которое визуализирует эти данные. Наша цель — расширить этот пример, чтобы позволить пользователю удалять продукты с помощью GridView. Для этого необходимо указать значения для параметров управления SqlDataSource `DeleteCommand` и `DeleteParameters`, а затем настроить GridView для поддержки удаления.

Свойства `DeleteCommand` и `DeleteParameters` можно указать несколькими способами.

- С помощью декларативного синтаксиса
- Из окно свойств в конструкторе
- На экране Укажите пользовательскую инструкцию SQL или хранимую процедуру в мастере настройки источника данных
- С помощью кнопки Дополнительно в диалоговом окне укажите столбцы из таблицы представления в мастере настройки источника данных, который автоматически создает инструкцию SQL `DELETE` и коллекцию параметров, используемую в свойствах `DeleteCommand` и `DeleteParameters`

Мы рассмотрим, как автоматически создать инструкцию `DELETE`, созданную на шаге 2. Теперь давайте используем окно свойств в конструкторе, несмотря на то, что мастер настройки источника данных или декларативный синтаксис также работает.

В конструкторе в `InsertUpdateDelete.aspx`щелкните `ProductsDataSource` SqlDataSource, а затем откройте окно свойств (в меню Вид выберите пункт окно свойств или просто нажмите клавишу F4). Выберите свойство Делетекуери, которое будет выделять набор эллипсов.

![Выберите свойство Делетекуери в окне "Свойства".](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.gif)

**Рис. 2**. Выбор свойства Делетекуери в окне "Свойства"

> [!NOTE]
> В SqlDataSource отсутствует свойство Делетекуери. Вместо этого Делетекуери является сочетанием свойств `DeleteCommand` и `DeleteParameters` и отображается только в окно свойств при просмотре окна с помощью конструктора. Если вы просматриваете окно свойств в представлении исходного кода, вместо этого можно найти свойство `DeleteCommand`.

Нажмите кнопку с многоточием в свойстве Делетекуери, чтобы открыть диалоговое окно Редактор параметров и команд (см. рис. 3). В этом диалоговом окне можно указать `DELETE` инструкции SQL и указать параметры. Введите следующий запрос в текстовое поле `DELETE` команда (вручную или с помощью конструктор запросов, если вы предпочитаете):

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample1.sql)]

Затем нажмите кнопку обновить параметры, чтобы добавить параметр `@ProductID` в список параметров ниже.

[![выберите свойство Делетекуери в окне "Свойства".](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.png)

**Рис. 3**. Выбор свойства Делетекуери в окне "Свойства" ([щелкните, чтобы просмотреть изображение с полным размером](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.png))

*Не* указывайте значение для этого параметра (оставьте его источник параметров без изменений). Когда мы добавим поддержку удаления в GridView, GridView автоматически предоставит значение этого параметра, используя значение его `DataKeys` коллекции для строки, для которой была нажата кнопка Delete (удалить).

> [!NOTE]
> Имя параметра, используемое в запросе `DELETE`, *должно* совпадать с именем `DataKeyNames` значения в GridView, DetailsView или FormView. Это значит, что параметр в операторе `DELETE` намеренно с именем `@ProductID` (вместо, скажем, `@ID`), так как имя первичного ключевого столбца в таблице Products (и, следовательно, значение DataKeyNames в GridView) `ProductID`.

Если имя параметра и значение `DataKeyNames` не совпадают, GridView не может автоматически присвоить параметру значение из коллекции `DataKeys`.

После ввода сведений об удалении в диалоговом окне Редактор параметров и команд нажмите кнопку ОК и перейдите к представлению исходного кода, чтобы просмотреть полученную декларативную разметку.

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample2.aspx)]

Обратите внимание на добавление свойства `DeleteCommand`, а также раздела `<DeleteParameters>` и объекта параметра с именем `productID`.

## <a name="configuring-the-gridview-for-deleting"></a>Настройка элемента GridView для удаления

После добавления свойства `DeleteCommand` смарт-тег GridView s теперь содержит параметр Включить удаление. Установите этот флажок. Как обсуждалось в [обзоре вставки, обновления и удаления](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md), GridView добавляет CommandField со свойством `ShowDeleteButton`, имеющим значение `True`. Как показано на рис. 4, при посещении страницы через браузер включается кнопка Удалить. Протестируйте эту страницу, удалив некоторые продукты.

[![каждая строка GridView теперь содержит кнопку "Удалить"](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.png)

**Рис. 4**. Теперь каждая строка GridView содержит кнопку «Удалить» ([щелкните, чтобы просмотреть изображение с полным размером](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.png)).

При нажатии кнопки удалить происходит обратная передача, GridView присваивает параметру `ProductID` значение `DataKeys` коллекции для строки, на которую была нажата кнопка Delete, и вызывает метод SqlDataSource `Delete()`. Затем элемент управления SqlDataSource подключается к базе данных и выполняет инструкцию `DELETE`. Затем GridView выполняет повторную привязку к SqlDataSource, получая и отображая текущий набор продуктов (который больше не включает в себя только что удаленную запись).

> [!NOTE]
> Поскольку GridView использует коллекцию `DataKeys` для заполнения параметров SqlDataSource, крайне важно, чтобы свойство GridView s `DataKeyNames` было установлено равным столбцам, составляющим первичный ключ, а в SqlDataSource s `SelectCommand` возвращать эти столбцы. Более того, важно, чтобы имя параметра в SqlDataSource s `DeleteCommand` было установлено в `@ProductID`. Если свойство `DataKeyNames` не задано или параметр не имеет имя `@ProductsID`, нажатие кнопки удалить вызовет обратную передачу, но фактически не удаляет записи.

На рис. 5 показано графическое взаимодействие. Дополнительные сведения о цепочке событий, связанных с вставкой, обновлением и удалением из веб-элемента управления данными, см. в статье [изучение событий, связанных с вставкой, обновлением и удалением](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) руководства.

![При нажатии кнопки "Удалить" в GridView вызывается метод SqlDataSource s Delete ().](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.gif)

**Рис. 5**. нажатие кнопки Delete в GridView вызывает метод SqlDataSource `Delete()`

## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>Шаг 2. Автоматическое создание`INSERT`,`UPDATE`и инструкций`DELETE`

На шаге 1 проверены, `INSERT`, `UPDATE`и `DELETE` инструкции SQL можно указать с помощью декларативного синтаксиса окно свойств или Control. Однако этот подход требует, чтобы вручную написать инструкции SQL, которые могут быть монотонную и подвержены ошибкам. К счастью, мастер настройки источников данных предоставляет возможность автоматического создания `INSERT`, `UPDATE`и `DELETE` инструкций при использовании окна указать столбцы из таблицы представления.

Давайте рассмотрим этот вариант автоматического создания. Добавьте элемент DetailsView в конструктор в `InsertUpdateDelete.aspx` и задайте для его свойства `ID` значение `ManageProducts`. Затем в смарт-теге DetailsView s выберите Создание нового источника данных и создание SqlDataSource с именем `ManageProductsDataSource`.

[![создать новый элемент SqlDataSource с именем Манажепродуктсдатасаурце](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.png)

**Рис. 6**. Создание нового SqlDataSource с именем `ManageProductsDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.png))

В мастере настройки источника данных выберите использовать строку подключения `NORTHWINDConnectionString` и нажмите кнопку Далее. На экране Настройка инструкции SELECT оставьте переключатель Укажите столбцы из таблицы или представления выбранным и выберите `Products` таблицу из раскрывающегося списка. Выберите столбцы `ProductID`, `ProductName`, `UnitPrice`и `Discontinued` из списка флажков.

[![использовании таблицы Products, возвращающей столбцы ProductID, ProductName, UnitPrice и неподдерживаемые](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.png)

**Рис. 7**. Использование `Products` таблицы для получения `ProductID`, `ProductName`, `UnitPrice`и `Discontinued` столбцов (щелкните,[чтобы просмотреть изображение с полным размером](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image10.png))

Чтобы автоматически создать инструкции `INSERT`, `UPDATE`и `DELETE` на основе выбранной таблицы и столбцов, нажмите кнопку Дополнительно и установите флажок Создать `INSERT`, `UPDATE`и инструкции `DELETE`.

![Установите флажок Создать инструкции INSERT, UPDATE и DELETE.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.gif)

**Рис. 8**. флажок создания инструкций `INSERT`, `UPDATE`и `DELETE`

Флажок Создать `INSERT`, `UPDATE`и `DELETE` будет доступен только в том случае, если выбранная таблица имеет первичный ключ, а столбец первичного ключа (или столбцы) включается в список возвращаемых столбцов. Флажок использовать оптимистичный параллелизм, который становится выбираемым после установки флажка создать `INSERT`, `UPDATE`и `DELETE`, дополняет предложения `WHERE` в результирующих `UPDATE` и инструкциях `DELETE` для обеспечения управления оптимистичным параллелизмом. Пока не устанавливайте этот флажок. в следующем руководстве мы рассмотрим оптимистичный параллелизм с помощью элемента управления SqlDataSource.

После установки флажка создать `INSERT`, `UPDATE`и `DELETE` нажмите кнопку ОК, чтобы вернуться на экран Настройка инструкции SELECT, затем нажмите кнопку Далее, а затем Готово, чтобы завершить работу мастера настройки источника данных. После завершения работы мастера Visual Studio добавит BoundFields в элемент DetailsView для столбцов `ProductID`, `ProductName`и `UnitPrice` и CheckBoxField для столбца `Discontinued`. В смарт-теге DetailsView s установите флажок Включить разбиение на страницы, чтобы пользователь, который посещает эту страницу, мог пошагово пройти по продуктам. Также очистите свойства `Width` и `Height` DetailsView.

Обратите внимание, что смарт-тег включает параметры Включить вставку, включить редактирование и разрешить удаление. Это обусловлено тем, что SqlDataSource содержит значения для его `InsertCommand`, `UpdateCommand`и `DeleteCommand`, как показано в следующем декларативном синтаксисе:

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample3.aspx)]

Обратите внимание, что значения элемента управления SqlDataSource автоматически задаются для свойств `InsertCommand`, `UpdateCommand`и `DeleteCommand`. Набор столбцов, упоминаемых в свойствах `InsertCommand` и `UpdateCommand`, основан на значениях в инструкции `SELECT`. То есть, вместо того чтобы *каждый* столбец Products в `InsertCommand` и `UpdateCommand`, были указаны только столбцы `SelectCommand` (меньше `ProductID`, что опускается, так как это [столбец`IDENTITY`](http://www.sqlteam.com/item.asp?ItemID=102), значение которого не может быть изменено при редактировании и которое автоматически назначается при вставке). Кроме того, для каждого параметра в свойствах `InsertCommand`, `UpdateCommand`и `DeleteCommand` существуют соответствующие параметры в коллекциях `InsertParameters`, `UpdateParameters`и `DeleteParameters`.

Чтобы включить функции изменения данных DetailsView, установите флажок Включить вставку, включить редактирование и включить параметры удаления в смарт-теге. При этом добавляется CommandField со свойствами `ShowInsertButton`, `ShowEditButton`и `ShowDeleteButton`, для которых задано значение `True`.

Откройте страницу в браузере и обратите внимание на кнопки Правка, удалить и новые, входящие в элемент DetailsView. При нажатии кнопки "Изменить" элемент DetailsView переводится в режим редактирования, в котором отображаются все BoundField, свойство `ReadOnly` которых имеет значение `False` (по умолчанию) в качестве текстового поля, а CheckBoxField — как CheckBox.

[![интерфейс редактирования по умолчанию DetailsView s](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image11.png)

**Рис. 9**. интерфейс редактирования по умолчанию DetailsView s ([щелкните, чтобы просмотреть изображение с полным размером](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image12.png))

Аналогичным образом можно удалить текущий выбранный продукт или добавить новый продукт в систему. Так как инструкция `InsertCommand` работает только с столбцами `ProductName`, `UnitPrice`и `Discontinued`, другие столбцы имеют либо `NULL`, либо значения по умолчанию, назначенные базой данных при вставке. Как и в случае с ObjectDataSource, если в `InsertCommand` отсутствуют столбцы таблицы базы данных, которые не позволяют `NULL` s и Дон t не имеют значения по умолчанию, то при попытке выполнить инструкцию `INSERT` произойдет ошибка SQL.

> [!NOTE]
> В интерфейсах вставки и редактирования DetailsView s отсутствует настройка или проверка. Чтобы добавить элементы управления проверки или настроить интерфейсы, необходимо преобразовать BoundFields в полей TemplateField. Дополнительные сведения см. в разделе [Добавление элементов управления проверки в интерфейсы правки и вставки](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) и настройка в учебниках по [интерфейсу изменения данных](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) .

Кроме того, обратите внимание, что для обновления и удаления элемент DetailsView использует текущее значение Product `DataKey`, которое имеется только в том случае, если настроено свойство `DataKeyNames`. Если изменение или удаление не оказывает никакого влияния, убедитесь, что задано свойство `DataKeyNames`.

## <a name="limitations-of-automatically-generating-sql-statements"></a>Ограничения автоматического создания инструкций SQL

Поскольку параметр Generate `INSERT`, `UPDATE`и `DELETE` доступен только при выборе столбцов из таблицы, для более сложных запросов необходимо написать собственные `INSERT`, `UPDATE`и инструкции `DELETE`, как в шаге 1. Как правило, инструкции SQL `SELECT` используют `JOIN` s для возврата данных из одной или нескольких таблиц подстановки в целях отображения (например, при возврате поля `Categories` таблицы с `CategoryName` при отображении сведений о продукте). В то же время может потребоваться разрешить пользователю изменять, обновлять или вставлять данные в основную таблицу (`Products`, в данном случае).

Хотя инструкции `INSERT`, `UPDATE`и `DELETE` можно указать вручную, рассмотрите следующий совет по экономии времени. Сначала настройте SqlDataSource таким образом, чтобы он запрашивает обратно данные только из таблицы `Products`. С помощью мастера настройки источника данных укажите столбцы из окна таблицы или представления, чтобы можно было автоматически создавать `INSERT`, `UPDATE`и операторы `DELETE`. После завершения работы мастера выберите настройку Селекткуери из окно свойств (или, Кроме того, вернитесь к мастеру настройки источника данных, но используйте параметр указать пользовательскую инструкцию SQL или хранимую процедуру). Затем обновите инструкцию `SELECT`, включив в нее синтаксис `JOIN`. Этот метод позволяет экономить время на основе автоматически создаваемых инструкций SQL и предоставляет более настраиваемую инструкцию `SELECT`.

Еще одно ограничение автоматического создания `INSERT`, `UPDATE`и `DELETE` инструкций заключается в том, что столбцы в инструкциях `INSERT` и `UPDATE` основаны на столбцах, возвращаемых инструкцией `SELECT`. Однако может потребоваться обновить или вставить больше или меньше полей. Например, в примере на шаге 2 может потребоваться, чтобы `UnitPrice` BoundField быть доступны только для чтения. В этом случае он не должен отображаться в `UpdateCommand`. Или нам может потребоваться задать значение поля таблицы, которое не отображается в GridView. Например, при добавлении новой записи может потребоваться задать для `QuantityPerUnit` значение TODO.

Если такие настройки необходимы, их необходимо сделать вручную либо с помощью окно свойств, в мастере Укажите настраиваемую инструкцию SQL или параметр хранимой процедуры или с помощью декларативного синтаксиса.

> [!NOTE]
> При добавлении параметров, не имеющих соответствующих полей в веб-элементе управления данными, помните, что значения этих параметров должны быть назначены определенным образом. Эти значения могут быть жестко запрограммированы непосредственно в `InsertCommand` или `UpdateCommand`; может поступать из некоторого заранее определенного источника (строки запроса, состояния сеанса, веб-элементов управления на странице и т. д.); или могут быть назначены программно, как было показано в предыдущем руководстве.

## <a name="summary"></a>Сводка

Чтобы веб-элементы управления данными могли использовать встроенные возможности вставки, редактирования и удаления, элемент управления источника данных, к которому они привязаны, должен предоставить такую функциональность. Для SqlDataSource это означает, что `INSERT`, `UPDATE`и `DELETE` инструкции SQL должны быть назначены свойствам `InsertCommand`, `UpdateCommand`и `DeleteCommand`. Эти свойства и соответствующие коллекции параметров можно добавить вручную или создать автоматически с помощью мастера настройки источника данных. В этом учебнике мы рассмотрели обе методики.

Мы рассматривали использование оптимистичного параллелизма с ObjectDataSource в учебнике [реализация оптимистичного параллелизма](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) . Элемент управления SqlDataSource также обеспечивает поддержку оптимистичного параллелизма. Как отмечалось на шаге 2, при автоматическом создании `INSERT`, `UPDATE`и инструкций `DELETE` мастер предлагает параметр использовать оптимистичный параллелизм. Как мы увидим в следующем руководстве, использование оптимистичного параллелизма с помощью SqlDataSource изменяет `WHERE`ные предложения в инструкциях `UPDATE` и `DELETE`, чтобы гарантировать, что значения других столбцов не изменялись с момента последнего отображения данных на странице.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Назад](using-parameterized-queries-with-the-sqldatasource-vb.md)
> [Вперед](implementing-optimistic-concurrency-with-the-sqldatasource-vb.md)
