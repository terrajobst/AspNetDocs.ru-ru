---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
title: Создание новых хранимых процедур для адаптеров таблиц TableAdapter типизированногоC#набора данных () | Документация Майкрософт
author: rick-anderson
description: В предыдущих учебных курсах мы создали в нашем коде инструкции SQL и передали инструкции в базу данных для выполнения. Альтернативный подход заключается в использовании s...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 751282ca-5870-4d66-84e4-6cefae23eb4a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
msc.type: authoredcontent
ms.openlocfilehash: db0d83a0fd1f1f175001d20844b298be0cf7e1cd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74609217"
---
# <a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-c"></a>Создание хранимых процедур для адаптеров таблиц TableAdapter типизированного DataSet (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_CS.zip) или [скачать PDF](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/datatutorial67cs1.pdf)

> В предыдущих учебных курсах мы создали в нашем коде инструкции SQL и передали инструкции в базу данных для выполнения. Альтернативный подход заключается в использовании хранимых процедур, в которых инструкции SQL предварительно определены в базе данных. В этом учебнике описано, как мастер TableAdapter создает новые хранимые процедуры для нас.

## <a name="introduction"></a>Введение

Уровень доступа к данным (DAL) для этих учебников использует типизированные наборы данных. Как обсуждалось в учебнике [Создание уровня доступа к данным](../introduction/creating-a-data-access-layer-cs.md) , типизированные наборы данных состоят из строго типизированных таблиц DataTable и TableAdapter. Объекты DataTable представляют логические сущности в системе, в то время как адаптеры таблиц TableAdapter с базовой базой данных выполняют работу с доступом к данным. Это включает в себя заполнение таблиц данных, исполнение запросов, возвращающих скалярные данные, а также вставку, обновление и удаление записей из базы данных.

Команды SQL, выполняемые TableAdapter, могут быть либо специальными инструкциями SQL, например `SELECT columnList FROM TableName`, либо хранимыми процедурами. Адаптеры таблиц в нашей архитектуре используют специальные инструкции SQL. Однако многие разработчики и администраторы баз данных предпочитают использовать хранимые процедуры для специальных инструкций SQL в целях обеспечения безопасности, удобства обслуживания и обновления. Другие ардентли предпочитают специальные инструкции SQL для своей гибкости. В моей собственной работе я использую хранимые процедуры для специальных инструкций SQL, но решил использовать специальные инструкции SQL для упрощения предыдущих руководств.

При определении TableAdapter или добавлении новых методов мастер адаптеров TableAdapter упрощает создание новых хранимых процедур или использование существующих хранимых процедур, так как он использует специальные инструкции SQL. В этом учебнике мы рассмотрим, как мастер TableAdapter s автоматически создает хранимые процедуры. В следующем учебном курсе мы рассмотрим, как настроить методы TableAdapter s для использования существующих или созданных вручную хранимых процедур.

> [!NOTE]
> Ознакомьтесь с записью блога Вадима в блоге о том, что хранимые [процедуры еще не используются?](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/) и [Франс Баума](https://weblogs.asp.net/fbouma/) s [. хранимые процедуры являются неправильными, M Кэй?](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx) для живом споров по преимуществам и недостаткам хранимых процедур и Специального SQL.

## <a name="stored-procedure-basics"></a>Основы хранимых процедур

Функции представляют собой конструкцию, общую для всех языков программирования. Функция — это коллекция инструкций, которые выполняются при вызове функции. Функции могут принимать входные параметры и при необходимости возвращать значение. *[Хранимые процедуры](http://en.wikipedia.org/wiki/Stored_procedure)* — это конструкции баз данных, которые обладают многими сходствами с функциями в языках программирования. Хранимая процедура состоит из набора инструкций T-SQL, которые выполняются при вызове хранимой процедуры. Хранимая процедура может принимать от нуля до многих входных параметров и может возвращать скалярные значения, выходные параметры или наиболее часто результирующие наборы из `SELECT` запросов.

> [!NOTE]
> Хранимые процедуры часто называются sprocs или SPs.

Хранимые процедуры создаются с помощью [`CREATE PROCEDURE`](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) инструкции t-SQL. Например, следующий скрипт T-SQL создает хранимую процедуру с именем `GetProductsByCategoryID`, которая принимает один параметр с именем `@CategoryID` и возвращает поля `ProductID`, `ProductName`, `UnitPrice`и `Discontinued` этих столбцов в `Products` таблице, имеющих совпадающее значение `CategoryID`:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample1.sql)]

После создания этой хранимой процедуры ее можно вызвать с помощью следующего синтаксиса:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample2.sql)]

> [!NOTE]
> В следующем учебном курсе мы рассмотрим создание хранимых процедур с помощью интегрированной среды разработки Visual Studio. Однако в этом руководстве мастер TableAdapter автоматически создает хранимые процедуры для нас.

Кроме простого возврата данных, хранимые процедуры часто используются для выполнения нескольких команд базы данных в рамках одной транзакции. Например, хранимая процедура с именем `DeleteCategory`может принимать в `@CategoryID` параметре и выполнять две инструкции `DELETE`: First, один для удаления связанных продуктов, а второй — для удаления указанной категории. Несколько инструкций в хранимой процедуре *не* упаковываются автоматически в транзакцию. Необходимо выполнить дополнительные команды T-SQL, чтобы гарантировать, что хранимые процедуры с несколькими командами рассматриваются как атомарные операции. В следующем руководстве мы посмотрим, как обернуть команды хранимых процедур в область действия транзакции.

При использовании хранимых процедур в архитектуре методы уровня доступа к данным вызывают определенную хранимую процедуру вместо того, чтобы выдавать Специальный оператор SQL. Это централизует расположение выполняемых инструкций SQL (в базе данных), а не определено в архитектуре приложения. Такая централизованность, вероятно, упрощает поиск, анализ и настройку запросов и предоставляет гораздо более четкое изображение, где и как используется база данных.

Дополнительные сведения об основных принципах хранимых процедур см. в разделе Дополнительные материалы в конце этого руководства.

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>Шаг 1. Создание веб-страниц сценариев расширенного уровня доступа к данным

Прежде чем приступить к обсуждению создания DAL с помощью хранимых процедур, давайте сначала создадим страницы ASP.NET в нашем проекте веб-сайта, которые понадобятся для этого и следующих нескольких руководств. Для начала добавьте новую папку с именем `AdvancedDAL`. Затем добавьте в эту папку следующие страницы ASP.NET, чтобы связать каждую страницу с главной страницей `Site.master`:

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`

![Добавление страниц ASP.NET для сценариев расширенного уровня доступа к данным учебников](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image1.png)

**Рис. 1**. добавление страниц ASP.NET для сценариев расширенного уровня доступа к данным учебников

Как и в других папках, `Default.aspx` в папке `AdvancedDAL` будут перечислены учебники в разделе. Вспомним, что `SectionLevelTutorialListing.ascx` пользовательский элемент управления предоставляет эти функции. Таким образом, добавьте этот пользовательский элемент управления в `Default.aspx`, перетащив его из обозреватель решений на страницу s представление конструирования.

[![добавить пользовательский элемент управления SectionLevelTutorialListing. ascx в Default. aspx](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image2.png)

**Рис. 2**. Добавление пользовательского элемента управления `SectionLevelTutorialListing.ascx` в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image4.png))

Наконец, добавьте эти страницы в качестве записей в файл `Web.sitemap`. В частности, добавьте следующую разметку после работы с пакетными данными `<siteMapNode>`.

[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample3.xml)]

После обновления `Web.sitemap`просмотрите веб-сайт учебников в браузере. Меню слева теперь включает элементы для учебников по расширенным сценариям DAL.

![На карте веб-узла теперь есть записи для учебников по расширенным сценариям DAL.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image5.png)

**Рис. 3**. схема узла теперь включает записи для учебников по расширенным СЦЕНАРИЯм DAL

## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>Шаг 2. Настройка адаптера таблицы для создания новых хранимых процедур

Чтобы продемонстрировать создание уровня доступа к данным, использующего хранимые процедуры вместо специальных инструкций SQL, давайте создадим новый типизированный набор данных в папке `~/App_Code/DAL` с именем `NorthwindWithSprocs.xsd`. Так как мы подробно обрабатывали этот процесс в предыдущих учебных курсах, мы будем быстро выполнить шаги, описанные здесь. Если вы пойдете в очередь или потребуете дальнейших пошаговых инструкций по созданию и настройке типизированного набора данных, см. Руководство по [созданию уровня доступа к данным](../introduction/creating-a-data-access-layer-cs.md) .

Добавьте новый набор данных в проект, щелкнув правой кнопкой мыши папку `DAL`, выбрав пункт Добавить новый элемент и выбрав шаблон набора данных, как показано на рис. 4.

[![добавить новый типизированный набор данных в проект с именем Норсвиндвисспрокс. xsd](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image6.png)

**Рис. 4**. Добавление нового типизированного набора данных в проект с именем `NorthwindWithSprocs.xsd` ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image8.png))

Будет создан новый типизированный набор данных, открыт его конструктор, создан новый адаптер таблицы и запущен мастер настройки адаптера таблицы. Первый шаг мастера настройки адаптера таблицы требует выбрать базу данных для работы. Строка подключения к базе данных Northwind должна быть указана в раскрывающемся списке. Выберите этот пункт и нажмите кнопку Далее.

На следующем экране можно выбрать способ доступа адаптера таблицы к базе данных. В предыдущих руководствах мы выбрали первый вариант, используя инструкции SQL. Для работы с этим руководством выберите второй параметр, создайте новые хранимые процедуры и нажмите кнопку Далее.

[![настроить TableAdapter для создания новых хранимых процедур](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image9.png)

**Рис. 5**. Указание адаптером TableAdapter создания новых хранимых процедур ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image11.png))

Как и при использовании специальных инструкций SQL, на следующем этапе мы попросят предоставить инструкцию `SELECT` для основного запроса TableAdapter s. Но вместо использования оператора `SELECT`, введенного здесь для прямого выполнения нерегламентированного запроса, мастер адаптеров таблиц TableAdapter создаст хранимую процедуру, содержащую этот `SELECT`ный запрос.

Используйте следующий `SELECT` запрос для этого адаптера таблицы:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample4.sql)]

[![ввести запрос SELECT](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image12.png)

**Рис. 6**. Ввод `SELECT` запроса ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image14.png))

> [!NOTE]
> Вышеприведенный запрос немного отличается от основного запроса `ProductsTableAdapter` в `Northwind` типизированном наборе данных. Помните, что `ProductsTableAdapter` в `Northwind` типизированном наборе данных содержит два коррелированных вложенных запроса, чтобы вернуть имя категории и название компании для каждой категории продуктов и поставщика. В следующем руководстве по [обновлению адаптера таблицы TableAdapter для использования соединений](updating-the-tableadapter-to-use-joins-cs.md) мы рассмотрим добавление этих связанных данных в этот TableAdapter.

Уделите несколько минут нажатию кнопки Дополнительные параметры. Здесь можно указать, должен ли мастер создавать инструкции INSERT, Update и DELETE для TableAdapter, следует ли использовать оптимистичный параллелизм и следует ли обновлять таблицу данных после вставок и обновлений. Параметр создать инструкции INSERT, Update и DELETE установлен по умолчанию. Оставьте флажок установленным. Для работы с этим руководством не устанавливайте флажок использовать оптимистичный параллелизм.

При автоматическом создании хранимых процедур мастером TableAdapter возникает, что параметр Обновить таблицу данных не учитывается. Независимо от того, установлен этот флажок, результирующие хранимые процедуры INSERT и Update извлекают только что вставленную или просто обновленную запись, как будет показано на шаге 3.

![Оставьте флажок Создать инструкции INSERT, Update и DELETE установленным.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image15.png)

**Рис. 7**. не устанавливайте флажок Создать инструкции INSERT, Update и DELETE

> [!NOTE]
> Если установлен флажок использовать оптимистичный параллелизм, мастер добавит дополнительные условия в предложение `WHERE`, которое предотвратит обновление данных в случае изменения в других полях. Дополнительные сведения об использовании встроенной функции управления оптимистичным параллелизмом TableAdapter см. в руководстве по [реализации](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) оптимистичного параллелизма.

После ввода `SELECT` запроса и подтверждения того, что установлен флажок Создать инструкции INSERT, Update и DELETE, нажмите кнопку Далее. Следующий экран, показанный на рис. 8, запрашивает имена хранимых процедур, которые будут созданы мастером для выбора, вставки, обновления и удаления данных. Измените имена этих хранимых процедур на `Products_Select`, `Products_Insert`, `Products_Update`и `Products_Delete`.

[![переименовать хранимые процедуры](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image16.png)

**Рис. 8**. Переименование хранимых процедур ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image18.png))

Чтобы просмотреть инструкции T-SQL, которые мастер TableAdapter будет использовать для создания четырех хранимых процедур, нажмите кнопку Предварительный просмотр скрипта SQL. В диалоговом окне «Предварительный просмотр скрипта SQL» можно сохранить скрипт в файл или скопировать его в буфер обмена.

![Предварительный просмотр скрипта SQL, используемого для создания хранимых процедур](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image19.png)

**Рис. 9**. Предварительный просмотр СКРИПТа SQL, используемого для создания хранимых процедур

После именования хранимых процедур нажмите кнопку Далее, чтобы назвать соответствующие методы TableAdapter. Как и при использовании специальных инструкций SQL, можно создавать методы, которые заполняют существующую таблицу данных или возвращают новую. Также можно указать, должен ли TableAdapter включать в себя шаблон DB-Direct для вставки, обновления и удаления записей. Оставьте все три флажка установленными, но переименуйте возвращаемый метод DataTable на `GetProducts` (как показано на рис. 10).

[![назовите методы Fill и Products.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image20.png)

**Рис. 10**. Именование методов `Fill` и `GetProducts` ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image22.png))

Нажмите кнопку Далее, чтобы просмотреть сводку действий, которые будут выполнены мастером. Завершите работу мастера, нажав кнопку Готово. После завершения работы мастера вы вернетесь к конструктору набора данных, который теперь должен включать `ProductsDataTable`.

[![конструктор наборов данных отображает только что добавленные Продуктсдататабле](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image23.png)

**Рис. 11**. Конструктор наборов данных отображает только что добавленные `ProductsDataTable` ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image25.png))

## <a name="step-3-examining-the-newly-created-stored-procedures"></a>Шаг 3. изучение вновь созданных хранимых процедур

Мастер TableAdapter, используемый на шаге 2, автоматически создал хранимые процедуры для выбора, вставки, обновления и удаления данных. Эти хранимые процедуры можно просмотреть или изменить в Visual Studio, перейдя к обозреватель сервера и выполнив детализацию в папке хранимых процедур базы данных s. Как показано на рис. 12, база данных Northwind содержит четыре новые хранимые процедуры: `Products_Delete`, `Products_Insert`, `Products_Select`и `Products_Update`.

![Четыре хранимые процедуры, созданные на шаге 2, можно найти в папке databases s хранимые процедуры.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image26.png)

**Рис. 12**. четыре хранимые процедуры, созданные на шаге 2, можно найти в папке хранимых процедур базы данных s

> [!NOTE]
> Если обозреватель сервера не отображается, перейдите в меню Вид и выберите параметр обозреватель сервера. Если вы не видите связанные с продуктом хранимые процедуры, добавленные на шаге 2, попробуйте щелкнуть правой кнопкой мыши папку Хранимые процедуры и выбрать команду Обновить.

Чтобы просмотреть или изменить хранимую процедуру, дважды щелкните ее имя в обозреватель сервера или же щелкните правой кнопкой мыши хранимую процедуру и выберите Открыть. На рис. 13 показана `Products_Delete` хранимая процедура при открытии.

[![хранимые процедуры можно открывать и изменять в Visual Studio.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image27.png)

**Рис. 13**. хранимые процедуры можно открывать и изменять в Visual Studio ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image29.png))

Содержимое хранимых процедур `Products_Delete` и `Products_Select` довольно просто. С другой стороны, `Products_Insert` и `Products_Update` хранимые процедуры предоставляют более тщательную проверку, так как они выполняют инструкцию `SELECT` после их `INSERT` и `UPDATE` инструкций. Например, следующий SQL создает `Products_Insert` хранимую процедуру:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample5.sql)]

Хранимая процедура принимает в качестве входных параметров `Products` столбцы, которые были возвращены запросом `SELECT`, указанным в мастере TableAdapter s, и эти значения используются в инструкции `INSERT`. После инструкции `INSERT` для получения значений столбцов `Products` (включая `ProductID`) только что добавленной записи используется запрос `SELECT`. Эта возможность обновления полезна при добавлении новой записи с помощью шаблона пакетного обновления, так как автоматически обновляет вновь добавленные `ProductRow` экземпляры `ProductID` свойства с автоматически увеличивающимися значениями, назначенными базой данных.

Эта функция показана в следующем коде. Он содержит `ProductsTableAdapter` и `ProductsDataTable`, созданные для `NorthwindWithSprocs` типизированного набора данных. Новый продукт добавляется в базу данных путем создания `ProductsRow` экземпляра, предоставления его значений и вызова метода `Update` TableAdapter, передавая `ProductsDataTable`. На внутреннем уровне метод `Update` TableAdapter перечисляет экземпляры `ProductsRow` в переданном DataTable (в этом примере только один добавленный) и выполняет соответствующую команду INSERT, UPDATE или DELETE. В этом случае выполняется хранимая процедура `Products_Insert`, которая добавляет новую запись в `Products` таблицу и возвращает сведения о вновь добавленной записи. После этого обновляется значение `ProductsRow` экземпляра `ProductID`. После завершения метода `Update` можно получить доступ к вновь добавленной записи `ProductID` значение с помощью свойства `ProductID` `ProductsRow` s.

[!code-csharp[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample6.cs)]

`Products_Update` хранимая процедура аналогичным образом включает инструкцию `SELECT` после ее оператора `UPDATE`.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample7.sql)]

Обратите внимание, что эта хранимая процедура включает два входных параметра для `ProductID`: `@Original_ProductID` и `@ProductID`. Эта функция позволяет использовать сценарии, в которых первичный ключ может быть изменен. Например, в базе данных сотрудников каждая запись сотрудника может использовать номер социального страхования Employee s в качестве первичного ключа. Чтобы изменить существующий номер социального страхования сотрудника, необходимо указать и новый номер социального страхования, и первоначальный. Для таблицы `Products` такие функции не требуются, так как столбец `ProductID` является столбцом `IDENTITY` и никогда не должен изменяться. На самом деле, инструкция `UPDATE` в хранимой процедуре `Products_Update` не включает столбец `ProductID` в список столбцов. Таким образом, хотя `@Original_ProductID` используется в предложении `UPDATE` `WHERE`, оно является избыточным для таблицы `Products` и может быть заменено параметром `@ProductID`. При изменении параметров хранимой процедуры важно, чтобы методы TableAdapter, которые используют эту хранимую процедуру, также были обновлены.

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>Шаг 4. изменение параметров хранимой процедуры и обновление адаптера таблицы TableAdapter

Поскольку параметр `@Original_ProductID` является излишним, можно полностью удалить его из хранимой процедуры `Products_Update`. Откройте `Products_Update` хранимую процедуру, удалите параметр `@Original_ProductID` и в предложении `WHERE` инструкции `UPDATE` измените имя параметра, используемое из `@Original_ProductID`, в `@ProductID`. После внесения этих изменений T-SQL внутри хранимой процедуры должен выглядеть следующим образом:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample8.sql)]

Чтобы сохранить эти изменения в базе данных, щелкните значок сохранить на панели инструментов или нажмите клавиши CTRL + S. На этом этапе хранимая процедура `Products_Update` не предполагала входного параметра `@Original_ProductID`, но TableAdapter настроен для передачи такого параметра. Вы можете просмотреть параметры, которые TableAdapter будет отсылать в `Products_Update` хранимой процедуре, выбрав TableAdapter в конструкторе наборов данных, перейдя к окно свойств и нажав кнопку с многоточием в коллекции `UpdateCommand` s `Parameters`. Откроется диалоговое окно Редактор коллекции параметров, показанное на рис. 14.

![В редакторе коллекции параметров перечисляются параметры, используемые для передачи Products_Update хранимой процедуре.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image30.png)

**Рис. 14**. Редактор коллекции параметров содержит список параметров, используемых в `Products_Update` хранимой процедуре

Вы можете удалить этот параметр отсюда, просто выбрав параметр `@Original_ProductID` из списка членов и нажав кнопку Удалить.

Кроме того, можно обновить параметры, используемые для всех методов, щелкнув правой кнопкой мыши TableAdapter в конструкторе и выбрав configure (настроить). Откроется мастер настройки адаптера таблицы, содержащий хранимые процедуры, используемые для выбора, вставки, обновления и удаления, а также параметры, которые должны быть получены хранимыми процедурами. Если щелкнуть раскрывающийся список обновление, можно увидеть `Products_Update` хранимые процедуры, ожидаемые входными параметрами, которые теперь больше не включают `@Original_ProductID` (см. рис. 15). Просто нажмите кнопку Готово, чтобы автоматически обновить коллекцию параметров, используемую TableAdapter.

[![можно также использовать мастер настройки TableAdapter s для обновления коллекций параметров методов](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image31.png)

**Рис. 15**. можно также использовать мастер настройки адаптера таблицы, чтобы обновить его методы коллекции параметров ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image33.png)).

## <a name="step-5-adding-additional-tableadapter-methods"></a>Шаг 5. Добавление дополнительных методов TableAdapter

Как показано на шаге 2, при создании нового адаптера таблицы можно легко создавать соответствующие хранимые процедуры. То же самое справедливо и при добавлении дополнительных методов в TableAdapter. Чтобы проиллюстрировать это, добавим метод `GetProductByProductID(productID)` в `ProductsTableAdapter`, созданный на шаге 2. Этот метод принимает в качестве входных данных `ProductID` значение и возвращает сведения об указанном продукте.

Для начала щелкните правой кнопкой мыши TableAdapter и выберите в контекстном меню команду Добавить запрос.

![Добавление нового запроса в TableAdapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image34.png)

**Рис. 16**. Добавление нового запроса в TableAdapter

Запустится мастер настройки запросов адаптера таблицы, который сначала запросит, как TableAdapter должен получить доступ к базе данных. Чтобы создать новую хранимую процедуру, выберите параметр создать новую хранимую процедуру и нажмите кнопку Далее.

[![выберите параметр создать новую хранимую процедуру.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image35.png)

**Рис. 17**. Выбор параметра "создать новую хранимую процедуру" ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image37.png))

На следующем экране будет предложено определить тип выполняемого запроса, возвращающего набор строк или одно скалярное значение, либо выполнить `UPDATE`, `INSERT`или инструкцию `DELETE`. Поскольку метод `GetProductByProductID(productID)` вернет строку, оставьте выбранным параметр выбрать, который возвращает строку и нажмите кнопку Далее.

[![выберите параметр выбрать, который возвращает строку.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image38.png)

**Рис. 18**. Выбор параметра выбор возвращающей строки ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image40.png))

На следующем экране отображается основной запрос TableAdapter s, в котором просто выводится имя хранимой процедуры (`dbo.Products_Select`). Замените имя хранимой процедуры следующей инструкцией `SELECT`, которая возвращает все поля продукта для указанного продукта:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample9.sql)]

[![заменить имя хранимой процедуры запросом SELECT](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image41.png)

**Рис. 19**. Замена имени хранимой процедуры `SELECT`ным запросом ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image43.png))

На следующем экране будет предложено указать имя создаваемой хранимой процедуры. Введите имя `Products_SelectByProductID` и нажмите кнопку Далее.

[![присвойте имя новой хранимой процедуре Products_SelectByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image44.png)

**Рис. 20**. присвойте новой хранимой процедуре имя `Products_SelectByProductID` ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image46.png))

Последний шаг мастера позволяет изменить имена методов, которые также указывают, следует ли использовать шаблон «заполнить таблицу данных», возвращать модель DataTable или и то, и другое. Для этого метода оставьте оба параметра установленными, но переименуйте методы в `FillByProductID` и `GetProductByProductID`. Нажмите кнопку Далее, чтобы просмотреть сводку действий, которые будут выполнены мастером, а затем нажмите кнопку Готово, чтобы завершить работу мастера.

[![переименование методов адаптера TableAdapter в Филлбипродуктид и Жетпродуктбипродуктид](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image47.png)

**Рис. 21**. Переименование методов TableAdapter s в `FillByProductID` и `GetProductByProductID` ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image49.png))

После завершения работы мастера в TableAdapter будет доступен новый метод, `GetProductByProductID(productID)` который при вызове выполняет хранимую процедуру `Products_SelectByProductID`, которая была только что создана. Просмотрите эту новую хранимую процедуру из обозреватель сервера, изменив папку хранимых процедур и открыв `Products_SelectByProductID` (если она не отображается, щелкните правой кнопкой мыши папку Хранимые процедуры и выберите команду Обновить).

Обратите внимание, что `SelectByProductID` хранимая процедура принимает `@ProductID` в качестве входного параметра и выполняет инструкцию `SELECT`, введенную в мастере.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>Шаг 6. Создание класса уровня бизнес-логики

В рамках серии руководств мы предоставили возможность поддерживать многоуровневую архитектуру, в которой уровень представления данных выполняет все свои вызовы уровня бизнес-логики (BLL). Чтобы придерживаться этого решения по проектированию, сначала необходимо создать класс BLL для нового типизированного набора данных, прежде чем получить доступ к данным продукта с уровня представления данных.

Создайте новый файл класса с именем `ProductsBLLWithSprocs.cs` в папке `~/App_Code/BLL` и добавьте в него следующий код:

[!code-csharp[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample11.cs)]

Этот класс имитирует семантику класса `ProductsBLL` из предыдущих руководств, но использует `ProductsTableAdapter` и `ProductsDataTable` объекты из набора данных `NorthwindWithSprocs`. Например, вместо выполнения инструкции `using NorthwindTableAdapters` в начале файла класса, как `ProductsBLL`, класс `ProductsBLLWithSprocs` использует `using NorthwindWithSprocsTableAdapters`. Аналогично, `ProductsDataTable` и `ProductsRow` объекты, используемые в этом классе, начинаются с пространства имен `NorthwindWithSprocs`. Класс `ProductsBLLWithSprocs` предоставляет два метода доступа к данным: `GetProducts` и `GetProductByProductID`, а также методы для добавления, обновления и удаления одного экземпляра продукта.

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>Шаг 7. Работа с набором данных`NorthwindWithSprocs`на уровне представления

На этом этапе мы создали DAL, который использует хранимые процедуры для доступа и изменения базовых данных базы данных. Мы также создали элементарный слой BLL с методами для получения всех продуктов или определенного продукта вместе с методами для добавления, обновления и удаления продуктов. Чтобы округлить этот учебник, давайте создадим страницу ASP.NET, использующую класс BLL `ProductsBLLWithSprocs` для отображения, обновления и удаления записей.

Откройте страницу `NewSprocs.aspx` в папке `AdvancedDAL` и перетащите элемент управления GridView из области элементов в конструктор, назвав его `Products`. В смарт-теге GridView s выберите привязку к новому ObjectDataSource с именем `ProductsDataSource`. Настройте ObjectDataSource для использования класса `ProductsBLLWithSprocs`, как показано на рис. 22.

[![настроить ObjectDataSource для использования класса Продуктсбллвисспрокс](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image50.png)

**Рис. 22**. Настройка ObjectDataSource для использования класса `ProductsBLLWithSprocs` ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image52.png))

Раскрывающийся список на вкладке Выбор имеет два параметра: `GetProducts` и `GetProductByProductID`. Так как нам нужно отобразить все продукты в GridView, выберите метод `GetProducts`. В раскрывающихся списках на вкладках обновления, вставки и удаления имеется только один метод. Убедитесь, что в каждом из раскрывающихся списков выбран соответствующий метод, и нажмите кнопку Готово.

После завершения работы мастера ObjectDataSource Visual Studio добавит BoundFields и CheckBoxField в GridView для полей данных продукта. Включите встроенные функции редактирования и удаления элементов управления GridView, установив флажки Включить редактирование и включить удаление в смарт-теге.

[![страница содержит элемент управления GridView с включенной поддержкой редактирования и удаления](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image53.png)

**Рис. 23**. страница содержит элемент управления GridView с включенной поддержкой редактирования и удаления ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image55.png))

Как мы говорили в предыдущих учебных курсах, при завершении работы мастера ObjectDataSource s Visual Studio присваивает свойству `OldValuesParameterFormatString` значение Original\_{0}. Необходимо вернуть значение по умолчанию {0}, чтобы функции изменения данных правильно работали с параметрами, ожидаемыми методами в BLL. Поэтому обязательно задайте для свойства `OldValuesParameterFormatString` значение {0} или удалите свойство из декларативного синтаксиса.

После завершения работы мастера настройки источника данных, включения поддержки редактирования и удаления в GridView и возврата свойства ObjectDataSource `OldValuesParameterFormatString` в значение по умолчанию декларативная разметка страницы должна выглядеть следующим образом:

[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample12.aspx)]

На этом этапе можно поместить GridView, настроив интерфейс правки для включения проверки, чтобы `CategoryID` и `SupplierID` столбцы отображались как элементов управления DropDownList и т. д. Также можно добавить подтверждение на стороне клиента к кнопке Delete, и я рекомендую принять время на реализацию этих улучшений. Так как эти разделы были рассмотрены в предыдущих руководствах, мы не будем перекрывать их здесь.

Независимо от того, улучшите ли вы элементы GridView или нет, протестируйте основные компоненты страницы в браузере. Как показано на рис. 24, на странице перечислены продукты в GridView, которые обеспечивают возможности редактирования и удаления отдельных строк.

[![можно просматривать, изменять и удалять продукты из GridView](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image56.png)

**Рис. 24**. продукты можно просматривать, изменять и удалять из GridView ([щелкните, чтобы просмотреть изображение с полным размером](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image58.png)).

## <a name="summary"></a>Сводка

TableAdapter в типизированном наборе данных может обращаться к данным из базы данных с помощью специальных инструкций SQL или хранимых процедур. При работе с хранимыми процедурами можно использовать либо существующие хранимые процедуры, либо мастер TableAdapter, позволяющий создавать новые хранимые процедуры на основе `SELECT` запроса. В этом учебнике мы изучили, как автоматически создавать хранимые процедуры для нас.

Хотя хранимые процедуры, созданные автоматически, помогают экономить время, в некоторых случаях, когда хранимая процедура, созданная мастером, не соответствует созданному нами. Одним из примеров является хранимая процедура `Products_Update`, которая предполагает, что `@Original_ProductID` и `@ProductID` входные параметры, даже если параметр `@Original_ProductID` был избыточным.

Во многих сценариях хранимые процедуры могут уже быть созданы, или может потребоваться создать их вручную, чтобы иметь более точное управление командами хранимых процедур. В любом случае мы хотим указать TableAdapter использовать существующие хранимые процедуры для своих методов. Мы увидим, как это сделать в следующем руководстве.

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Создание и обслуживание хранимых процедур](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [Получение скалярных данных из хранимой процедуры](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [Основные сведения о хранимых процедурах SQL Server](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [Общие сведения о хранимых процедурах](http://www.sqlteam.com/item.asp?ItemID=563)
- [Написание хранимой процедуры](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Хилтон Жеисенов. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Вперед](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
