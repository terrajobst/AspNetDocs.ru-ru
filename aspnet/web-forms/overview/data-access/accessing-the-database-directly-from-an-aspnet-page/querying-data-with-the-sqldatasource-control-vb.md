---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
title: Запрос данных с помощью элемента управления SqlDataSource (VB) | Документация Майкрософт
author: rick-anderson
description: В предыдущих учебных курсах мы использовали элемент управления ObjectDataSource, чтобы полностью отделить уровень представления от уровня доступа к данным. Начиная с этого учебного...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: b12f752d-3502-40a4-b695-fc7b7d08cfd3
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 199ddb46e877c3a0937672d33241a240660684da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430062"
---
# <a name="querying-data-with-the-sqldatasource-control-vb"></a>Запрос данных с помощью элемента управления SqlDataSource (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_VB.exe) или [Загрузка PDF-файла](querying-data-with-the-sqldatasource-control-vb/_static/datatutorial47vb1.pdf)

> В предыдущих учебных курсах мы использовали элемент управления ObjectDataSource, чтобы полностью отделить уровень представления от уровня доступа к данным. Начиная с этого руководства мы рассмотрим, как можно использовать элемент управления SqlDataSource для простых приложений, не требующих такого четкого разделения представления и доступа к данным.

## <a name="introduction"></a>Введение

Все учебные курсы, которые мы рассматривали ранее, использовали многоуровневую архитектуру, состоящую из уровней представления, бизнес-логики и доступа к данным. Уровень доступа к данным (DAL) был создан в первом учебнике ([Создание уровня доступа к данным](../introduction/creating-a-data-access-layer-vb.md)) и на уровне бизнес-логики во втором ([Создание уровня бизнес-логики](../introduction/creating-a-business-logic-layer-vb.md)). В начале [отображения данных с помощью учебника по ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) мы увидели, как использовать новый элемент управления objectdatasource ASP.NET 2,0, чтобы декларативно взаимодействовать с архитектурой из уровня представления.

Хотя все руководства на данный момент использовали архитектуру для работы с данными, можно также получать доступ к данным, вставлять, обновлять и удалять данные базы данных непосредственно из страницы ASP.NET, минуя архитектуру. Это позволяет разместит определенные запросы к базе данных и бизнес-логику непосредственно на веб-странице. Для достаточно больших или сложных приложений разработка, реализация и использование многоуровневой архитектуры жизненно важна для успешного, обновляемого и обслуживаемого приложения. Однако разработка надежной архитектуры может быть ненужной при создании более простых, одноразовых приложений.

ASP.NET 2,0 предоставляет пять встроенных элементов управления источниками данных: [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)и [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx). SqlDataSource можно использовать для доступа к данным и их изменения непосредственно из реляционной базы данных, включая Microsoft SQL Server, Microsoft Access, Oracle, MySQL и др. В этом руководстве и трех следующих примерах мы рассмотрим работу с элементом управления SqlDataSource, просмотрев запросы и фильтрацию данных базы данных, а также как использовать SqlDataSource для вставки, обновления и удаления данных.

![ASP.NET 2,0 включает пять встроенных элементов управления источниками данных](querying-data-with-the-sqldatasource-control-vb/_static/image1.gif)

**Рис. 1**. ASP.NET 2,0 включает пять встроенных элементов управления источниками данных

## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>Сравнение ObjectDataSource и SqlDataSource

По сути, элементы управления ObjectDataSource и SqlDataSource просто являются прокси-объектами для данных. Как обсуждалось в руководстве по [отображению данных с помощью элемента управления ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) , у ObjectDataSource есть свойства, указывающие тип объекта, который предоставляет данные, и методы, вызываемые для выбора, вставки, обновления и удаления данных из базового типа объекта. После настройки свойств ObjectDataSource s веб-элемент управления данными, например GridView, DetailsView или DataList, может быть привязан к элементу управления с помощью методов ObjectDataSource `Select()`, `Insert()`, `Delete()`и `Update()` для взаимодействия с базовой архитектурой.

Функция SqlDataSource предоставляет те же функциональные возможности, но работает с реляционной базой данных, а не с библиотекой объектов. С помощью SqlDataSource необходимо указать строку подключения к базе данных и нерегламентированные запросы SQL или хранимые процедуры, которые будут выполняться для вставки, обновления, удаления и получения данных. Методы SqlDataSource `Select()`, `Insert()`, `Update()`и `Delete()` при вызове подключаются к указанной базе данных и выдают соответствующий запрос SQL. Как показано на следующей схеме, эти методы выполняют grunt работу по подключению к базе данных, выполняя запрос и возвращают результаты.

![SqlDataSource выступает в качестве прокси-сервера для базы данных](querying-data-with-the-sqldatasource-control-vb/_static/image2.gif)

**Рис. 2**. SqlDataSource выступает в качестве прокси-сервера для базы данных

> [!NOTE]
> В этом учебнике основное внимание уделяется извлечению данных из базы данных. В руководстве по [вставке, обновлению и удалению данных с помощью элемента управления SqlDataSource](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md) будет показано, как настроить SqlDataSource для поддержки вставки, обновления и удаления.

## <a name="the-sqldatasource-and-accessdatasource-controls"></a>Элементы управления SqlDataSource и AccessDataSource

Помимо элемента управления SqlDataSource, ASP.NET 2,0 также включает элемент управления AccessDataSource. Эти два разных элемента управления ведут к тому, что многие разработчики впервые ASP.NET 2,0, что элемент управления AccessDataSource предназначен исключительно для работы с Microsoft Access с элементом управления SqlDataSource, предназначенным для работы исключительно с Microsoft SQL Server. Хотя AccessDataSource предназначен для работы непосредственно с Microsoft Access, элемент управления SqlDataSource работает с *любой* реляционной базой данных, доступ к которой можно получить с помощью .NET. Сюда входят все хранилища данных, совместимые с OleDb или ODBC, такие как Microsoft SQL Server, Microsoft Access, Oracle, Informix, MySQL и PostgreSQL, а также многие другие.

Единственное различие между элементами управления AccessDataSource и SqlDataSource заключается в том, как указываются сведения о подключении к базе данных. Элементу управления AccessDataSource требуется только путь к файлу базы данных Access. С другой стороны, для SqlDataSource требуется полная строка подключения.

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>Шаг 1. Создание веб-страниц SqlDataSource

Прежде чем начать изучение работы с данными базы данных с помощью элемента управления SqlDataSource, давайте сначала создадим страницы ASP.NET в нашем проекте веб-сайта, которые понадобятся для работы с этим руководством и следующих трех. Для начала добавьте новую папку с именем `SqlDataSource`. Затем добавьте в эту папку следующие страницы ASP.NET, чтобы связать каждую страницу с главной страницей `Site.master`:

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`

![Добавление страниц ASP.NET для учебников, связанных с SqlDataSource](querying-data-with-the-sqldatasource-control-vb/_static/image3.gif)

**Рис. 3**. добавление страниц ASP.NET для учебников, связанных с SqlDataSource

Как и в других папках, `Default.aspx` в папке `SqlDataSource` будут перечислены учебники в разделе. Вспомним, что `SectionLevelTutorialListing.ascx` пользовательский элемент управления предоставляет эти функции. Таким образом, добавьте этот пользовательский элемент управления в `Default.aspx`, перетащив его из обозреватель решений на страницу s представление конструирования.

[![добавить пользовательский элемент управления SectionLevelTutorialListing. ascx в Default. aspx](querying-data-with-the-sqldatasource-control-vb/_static/image5.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image4.gif)

**Рис. 4**. Добавление пользовательского элемента управления `SectionLevelTutorialListing.ascx` в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](querying-data-with-the-sqldatasource-control-vb/_static/image6.gif))

Наконец, добавьте эти четыре страницы в качестве записей в файл `Web.sitemap`. В частности, добавьте следующую разметку после добавления пользовательских кнопок в DataList и Repeater `<siteMapNode>`:

[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample1.sql)]

После обновления `Web.sitemap`просмотрите веб-сайт учебников в браузере. В меню слева теперь содержатся элементы для учебников по редактированию, вставке и удалению.

![На карте веб-узла теперь есть записи для учебников по SqlDataSource.](querying-data-with-the-sqldatasource-control-vb/_static/image7.gif)

**Рис. 5**. схема узла теперь включает записи для учебников по SqlDataSource

## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>Шаг 2. Добавление и настройка элемента управления SqlDataSource

Для начала откройте страницу `Querying.aspx` в папке `SqlDataSource` и перейдите в представление конструирования. Перетащите элемент управления SqlDataSource из панели элементов в конструктор и задайте для его `ID` значение `ProductsDataSource`. Как и в случае с ObjectDataSource, SqlDataSource не создает выходные данные и, следовательно, отображается в виде серого прямоугольника в области конструктора. Чтобы настроить SqlDataSource, щелкните ссылку Настроить источник данных из смарт-тега SqlDataSource s.

![Щелкните ссылку Настройка источника данных из смарт-тега SqlDataSource s.](querying-data-with-the-sqldatasource-control-vb/_static/image8.gif)

**Рис. 6**. Щелкните ссылку Настройка источника данных из смарт-тега SqlDataSource s

Откроется мастер настройки источника данных SqlDataSource Control s. В то время как шаги мастера отличаются от элементов управления ObjectDataSource, конечная цель одинакова для предоставления сведений о том, как извлекать, вставлять, обновлять и удалять данные через источник данных. Для SqlDataSource это означает указание базовой базы данных для использования и предоставление специальных инструкций SQL или хранимых процедур.

Первый шаг мастера запрашивает у нас базу данных. В раскрывающемся списке содержатся базы данных, найденные в папке веб-приложения s `App_Data` и те, которые были добавлены в узел подключения к данным в обозреватель сервера. Так как мы уже добавили строку подключения для базы данных `NORTHWIND.MDF` в папке `App_Data` в `Web.config`ном файле Project s, раскрывающийся список содержит ссылку на эту строку подключения `NORTHWINDConnectionString`. Выберите этот элемент в раскрывающемся списке и нажмите кнопку Далее.

![Выберите NORTHWINDConnectionString из раскрывающегося списка.](querying-data-with-the-sqldatasource-control-vb/_static/image9.gif)

**Рис. 7**. Выбор `NORTHWINDConnectionString` из раскрывающегося списка

После выбора базы данных мастер запросит запрос на возврат данных. Можно указать столбцы таблицы или представления, которые должны быть возвращены или могут ввести пользовательскую инструкцию SQL или указать хранимую процедуру. Можно переключаться между этими вариантами с помощью параметра указать пользовательскую инструкцию SQL или хранимую процедуру и указать столбцы из переключателя таблицы или представления.

> [!NOTE]
> Для этого первого примера позвольте использовать параметр указать столбцы из таблицы или представления. Далее в этом руководстве мы вернемся к мастеру и изучим параметр указать пользовательскую инструкцию SQL или хранимую процедуру.

На рис. 8 показан экран Настройка инструкции SELECT, когда выбран переключатель Укажите столбцы из таблицы или представления. Раскрывающийся список содержит набор таблиц и представлений в базе данных Northwind с выбранными столбцами таблица или представление s, отображенными в списке ниже. В этом примере пусть s возвращает `ProductID`, `ProductName`и `UnitPrice` столбцы из таблицы `Products`. Как показано на рис. 8, после выполнения этих выбора мастер показывает результирующую инструкцию SQL `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`.

![Возврат данных из таблицы Products](querying-data-with-the-sqldatasource-control-vb/_static/image10.gif)

**Рис. 8**. Возвращение данных из таблицы `Products`

После настройки мастера для возврата `ProductID`, `ProductName`и `UnitPrice` столбцов из таблицы `Products` нажмите кнопку Далее. На этом последнем экране можно просмотреть результаты запроса, настроенного на предыдущем шаге. Нажатие кнопки Проверить запрос выполняет настроенную инструкцию `SELECT` и отображает результаты в виде сетки.

![Нажмите кнопку проверить запрос, чтобы проверить запрос SELECT.](querying-data-with-the-sqldatasource-control-vb/_static/image11.gif)

**Рис. 9**. нажатие кнопки "проверить запрос" для просмотра `SELECT` запроса

Чтобы завершить работу мастера, нажмите кнопку Готово.

Как и в случае с ObjectDataSource, мастер SqlDataSource s просто присваивает значения свойствам Control s, а именно [`ConnectionString`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx) и [`SelectCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx) свойства. После завершения работы мастера декларативная разметка элемента управления SqlDataSource должна выглядеть следующим образом:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample2.aspx)]

Свойство `ConnectionString` предоставляет сведения о том, как подключиться к базе данных. Этому свойству можно присвоить полное жестко заданное значение строки подключения или указать строку подключения в `Web.config`. Для ссылки на значение строки подключения в файле Web. config используйте синтаксис `<%$ expressionPrefix:expressionValue %>`. Обычно *експрессионпрефикс* — это ConnectionString, а *експрессионвалуе* — имя строки подключения в [разделе `Web.config``<connectionStrings>`](https://msdn.microsoft.com/library/bf7sd233.aspx). Однако синтаксис можно использовать для ссылки на `<appSettings>` элементы или содержимое из файлов ресурсов. Подробнее об этом синтаксисе см. в разделе [Общие сведения о выражениях ASP.NET](https://msdn.microsoft.com/library/d5bd1tad.aspx) .

Свойство `SelectCommand` указывает нерегламентированную инструкцию SQL или хранимую процедуру, которую необходимо выполнить для возврата данных.

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>Шаг 3. Добавление веб-элемента управления данными и его привязка к SqlDataSource

После настройки SqlDataSource его можно привязать к веб-элементу управления данными, например GridView или DetailsView. В этом руководстве мы будем отображать данные в элементе управления GridView. Перетащите элемент управления GridView с панели элементов на страницу и привяжите его к `ProductsDataSource` SqlDataSource, выбрав источник данных из раскрывающегося списка в смарт-теге GridView s.

[![добавить GridView и привязать его к элементу управления SqlDataSource](querying-data-with-the-sqldatasource-control-vb/_static/image13.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image12.gif)

**Рис. 10**. Добавление GridView и привязка его к элементу управления SqlDataSource ([щелкните, чтобы просмотреть изображение с полным размером](querying-data-with-the-sqldatasource-control-vb/_static/image14.gif))

После выбора элемента управления SqlDataSource из раскрывающегося списка в смарт-теге GridView s Visual Studio автоматически добавит BoundField или CheckBoxField в GridView для каждого столбца, возвращаемого элементом управления источника данных. Так как SqlDataSource возвращает три столбца базы данных `ProductID`, `ProductName`и `UnitPrice` в GridView есть три поля.

Уделите несколько минут настройке трех BoundFields в GridView s. Измените `ProductName` поля `HeaderText` свойства на имя продукта и на `UnitPrice` поле s на Price. Также Отформатируйте поле `UnitPrice` как валюту. После внесения этих изменений декларативная разметка GridView s должна выглядеть следующим образом:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample3.aspx)]

Посетите эту страницу в браузере. Как показано на рис. 11, в элементе GridView перечислены `ProductID`, `ProductName`и `UnitPrice` значения.

[![GridView отображает значения ProductID, ProductName и UnitPrice для каждого продукта.](querying-data-with-the-sqldatasource-control-vb/_static/image16.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image15.gif)

**Рис. 11**. Отображение каждого продукта с `ProductID`, `ProductName`и `UnitPrice` значений (щелкните,[чтобы просмотреть изображение с полным размером](querying-data-with-the-sqldatasource-control-vb/_static/image17.gif))

При посещении страницы GridView вызывает метод `Select()` управления источниками данных. При использовании элемента управления ObjectDataSource это вызывало метод `ProductsBLL` Class s `GetProducts()`. Однако с помощью SqlDataSource метод `Select()` устанавливает соединение с указанной базой данных и выдает `SelectCommand` (в этом примере —`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`). Функция SqlDataSource возвращает свои результаты, которые затем выполняет перечисление GridView, создавая строку в GridView для каждой возвращенной записи базы данных.

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>Встроенные функции веб-элементов управления данными и элемент управления SqlDataSource

В целом, функции, присущие веб-элементам управления данными, сортируются, редактируют, удаляют, вставляют и т. д., относятся к веб-элементу управления данными и не зависят от используемого элемента управления источниками данных. Это значит, что GridView может использовать встроенную подкачку, сортировку, редактирование и удаление, связан ли он с ObjectDataSource или SqlDataSource. Однако некоторые функции веб-элементов управления данными чувствительны к используемому элементу управления источником данных или к конфигурации системы управления источниками данных.

Например, в [рамках эффективного постраничного обмена большими объемами данных](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) мы обсуждали, как по умолчанию логика разбиения по страницам для веб-элементов управления данными сильно возвращает *все* записи из базового источника данных, а затем отображает только соответствующее подмножество записей, учитывая текущий индекс страницы, и число записей, отображаемых на странице. Эта модель очень неэффективна при разбиении на страницы достаточно большого набора результирующих наборов. К счастью, элемент управления ObjectDataSource можно настроить для поддержки пользовательского разбиения на страницы, возвращающего только точное подмножество отображаемых записей. Однако в элементе управления SqlDataSource отсутствуют свойства для реализации пользовательского разбиения на страницы.

Другая тонкость, связанная с разбиением по страницам и сортировкой, возникает с помощью SqlDataSource. По умолчанию данные, возвращаемые из SqlDataSource, можно пролистывать или сортировать с помощью элемента управления GridView. Чтобы продемонстрировать это, установите флажок Включить разбиение на страницы и включить параметры сортировки в смарт-теге GridView s в `Querying.aspx` и убедитесь, что это работает правильно.

Сортировка и разбиение на страницы работают, поскольку SqlDataSource извлекает данные из базы данных в слабо типизированный набор данных. Общее число записей, возвращенных запросом, является важным аспектом реализации разбиения на страницы из набора данных. Кроме того, результаты набора данных можно отсортировать через объект DataView. Эти возможности автоматически используются средством SqlDataSource, когда GridView запрашивает страницы или отсортированные данные.

С помощью элемента SqlDataSource можно настроить возврат объекта DataReader вместо набора данных, изменив его [свойство`DataSourceMode`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx) с `DataSet` (по умолчанию) на `DataReader`. Использование DataReader может оказаться предпочтительным в ситуациях, когда передает результаты SqlDataSource в существующий код, который ждет DataReader. Более того, поскольку объекты DataReader являются значительно более простыми объектами, чем наборы данных, они обеспечивают лучшую производительность. Однако при внесении этого изменения веб-элемент управления данными не может ни выполнять сортировку, ни страницу, так как SqlDataSource не может определить, сколько записей возвращается запросом, а DataReader не предлагает никаких методов для сортировки возвращаемых данных.

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>Шаг 4. Использование пользовательской инструкции SQL или хранимой процедуры

При настройке элемента управления SqlDataSource запрос, используемый для возврата данных, может быть указан в одном из двух подходов в качестве пользовательской инструкции SQL или хранимой процедуры или в виде столбцов из существующей таблицы или представления. На шаге 2 мы рассмотрели выбор столбцов из таблицы `Products`. Давайте посмотрим на использование пользовательской инструкции SQL.

Добавьте еще один элемент управления GridView на страницу `Querying.aspx` и выберите Создание нового источника данных из раскрывающегося списка в смарт-теге. Затем укажите, что данные будут извлечены из базы данных. при этом будет создан новый элемент управления SqlDataSource. Присвойте элементу управления имя `ProductsWithCategoryInfoDataSource`.

![Создание нового элемента управления SqlDataSource с именем Продуктсвискатегоринфодатасаурце](querying-data-with-the-sqldatasource-control-vb/_static/image18.gif)

**Рис. 12**. Создание нового элемента управления SqlDataSource с именем `ProductsWithCategoryInfoDataSource`

На следующем экране будет предложено указать базу данных. Как мы делали на рис. 7, выберите `NORTHWINDConnectionString` из раскрывающегося списка и нажмите кнопку Далее. На экране Настройка инструкции Select выберите переключатель задать пользовательскую инструкцию SQL или хранимую процедуру и нажмите кнопку Далее. Откроется экран определение пользовательских инструкций или хранимых процедур, в котором будут представлены вкладки с метками SELECT, UPDATE, INSERT и DELETE. На каждой вкладке можно ввести пользовательскую инструкцию SQL в текстовое поле или выбрать хранимую процедуру из раскрывающегося списка. В этом учебнике рассматривается ввод пользовательской инструкции SQL. в следующем учебнике содержится пример, в котором используется хранимая процедура.

![Введите пользовательскую инструкцию SQL или выберите хранимую процедуру](querying-data-with-the-sqldatasource-control-vb/_static/image19.gif)

**Рис. 13**. Ввод пользовательской инструкции SQL или выбор хранимой процедуры

Пользовательская инструкция SQL может быть передана вручную в текстовое поле или может быть построена графически путем нажатия кнопки конструктор запросов. В конструктор запросов или в текстовом поле используйте следующий запрос, чтобы вернуть поля `ProductID` и `ProductName` из таблицы `Products` с помощью `JOIN` для получения `CategoryName` продуктов из таблицы `Categories`.

[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample4.sql)]

![Можно графически сформировать запрос с помощью конструктор запросов](querying-data-with-the-sqldatasource-control-vb/_static/image20.gif)

**Рис. 14**. Создание графического запроса с помощью конструктор запросов

После указания запроса нажмите кнопку Далее, чтобы перейти к экрану тестового запроса. Нажмите кнопку Готово, чтобы завершить работу мастера SqlDataSource.

После завершения работы мастера в GridView будет добавлено три BoundFields для отображения `ProductID`, `ProductName`и `CategoryName` столбцы, возвращаемые из запроса, и в результате чего будет получена следующая декларативная разметка:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample5.aspx)]

[![элементе GridView отображаются ИДЕНТИФИКАТОРы, имена и имена связанных категорий продуктов.](querying-data-with-the-sqldatasource-control-vb/_static/image22.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image21.gif)

**Рис. 15**. в элементе GRIDVIEW отображаются идентификаторы, имена и имена связанных категорий продуктов ([щелкните, чтобы просмотреть изображение с полным размером](querying-data-with-the-sqldatasource-control-vb/_static/image23.gif)).

## <a name="summary"></a>Сводка

В этом учебнике мы увидели, как запрашивать и отображать данные с помощью элемента управления SqlDataSource. Как и в случае с ObjectDataSource, SqlDataSource выступает в качестве прокси-сервера, предоставляя декларативный подход к доступу к данным. Его свойства указывают базу данных, к которой необходимо подключиться, а также запрос SQL `SELECT` для выполнения. их можно указать с помощью окно свойств или с помощью мастера настройки источника данных.

В `SELECT` примерах запросов, которые мы рассматривали в этом учебнике, были возвращены все записи из указанного запроса. Однако элемент управления SqlDataSource может содержать предложение `WHERE` с параметрами, значения которых назначаются программно или автоматически извлекаются из указанного источника. В следующем руководстве мы рассмотрим, как создавать и использовать параметризованные запросы.

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные материалы

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Доступ к данным реляционной базы данных](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [Общие сведения об элементе управления SqlDataSource](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [Краткие руководства по ASP.NET: элемент управления SqlDataSource](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Элемент `<connectionStrings>` Web. config](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [Ссылка на строку подключения к базе данных](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого руководства: Ирина Коннери, Бернадетте Леигх и Дэвид суру. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](implementing-optimistic-concurrency-with-the-sqldatasource-cs.md)
> [Вперед](using-parameterized-queries-with-the-sqldatasource-vb.md)
