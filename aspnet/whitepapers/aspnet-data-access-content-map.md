---
uid: whitepapers/aspnet-data-access-content-map
title: Доступ к данным ASP.NET — Рекомендуемые ресурсы | Документация Майкрософт
author: rick-anderson
description: В этом разделе содержатся ссылки на ресурсы документации о том, как получить доступ к данным в веб-приложениях ASP.NET, в первую очередь, с помощью Entity Framework и SQL SE...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513972"
---
# <a name="aspnet-data-access---recommended-resources"></a>Доступ к данным ASP.NET. Рекомендуемые ресурсы

> В этом разделе приводятся ссылки на ресурсы документации о том, как получить доступ к данным в веб-приложениях ASP.NET, в основном с помощью Entity Framework и SQL Server.
> 
> Если вы знакомы с отличной записью блога, потоком [StackOverflow](http://stackoverflow.com) или любой другой ссылкой, которая будет полезной, [отправьте нам сообщение электронной почты](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) со ссылкой.
> 
> Последнее обновление 4/3/2014

В нем содержатся следующие подразделы:

- [Начало работы с доступом к данным в ASP.NET](#gettingstarted)
- [Использование Entity Framework](#ef)

    - [Использование Entity Framework Code First](#cf)
    - [Использование Entity Framework Code First Migrations](#efcfmigrations)
    - [Использование Entity Framework Database First или Model First (конструктор EF)](#efdbf)
    - [Загрузка связанных данных в Entity Framework (отложенная загрузка, упреждающая загрузка и явная загрузка)](#efrelateddata)
    - [Оптимизация производительности Entity Framework](#optimizingef)
    - [Обработка параллелизма в приложении Entity Framework](#efconcurrency)
    - [Книги о Entity Framework](#efbooks)
    - [Дополнительные ресурсы Entity Framework](#otherefresources)
- [Привязка данных в приложениях веб-форм ASP.NET](#wfdatabinding)

    - [Использование привязки модели веб-форм](#wfmodelbinding)
    - [Использование элементов управления источниками данных веб-форм](#wfdsc)
    - [Использование элементов управления, привязанных к данным и выражений привязки данных веб-форм](#wfdbc)
- [Работа с базами данных SQL Server](#sqlserver)

    - [Работа с SQL Server Express базами данных LocalDB](#sslocaldb)
    - [Работа с базами данных SQL Server Express](#sse)
    - [Работа с базой данных SQL Windows Azure](#ssdb)
    - [Выбор между SQL Server и базой данных SQL Windows Azure](#ssdbchoosing)
- [Работа с системами управления базами данных NoSQL](#nosql)
- [Использование запросов LINQ в приложениях ASP.NET](#linq)
- [Использование платформа динамических данных формирования шаблонов](#dd)
- [Защита доступа к данным](#securing)
- [Оптимизация производительности доступа к данным](#optimizingdataaccess)
- [Развертывание базы данных](#deploying)
- [Доступ к данным через веб-службу](#webservice)
- [Дополнительные ресурсы](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>Начало работы с доступом к данным в ASP.NET

- [Варианты хранения данных (создание облачных приложений в реальном мире с помощью Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). Глава электронной книги о разработке для облака. Введение в базы данных NoSQL в качестве альтернативы, которую многие разработчики знакомы с реляционными базами данных, как правило, не заменять. Содержит рекомендации по выбору реляционных или NoSQL или выбору конкретной платформы.
- [Параметры доступа к данным ASP.NET](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). Общие сведения о параметрах доступа к данным для ASP.NET и рекомендации по выбору платформ и методов доступа, подходящих для вашего сценария.
- [Реляционная база данных](http://en.wikipedia.org/wiki/Relational_database). Википедии). Если вы еще не работали с реляционными базами данных, ознакомьтесь с этой страницей, чтобы ознакомиться с терминологией и понятиями реляционной базы данных. Общие сведения о SQL Server в конкретном разделе см. в разделе [Работа с SQL Serverными базами данных](#sqlserver) далее в этой статье.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Использование Entity Framework

- [Entity Framework подходов к разработке](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Рекомендации по выбору подхода к разработке Entity Framework Database First, Model First или Code First.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Использование Entity Framework Code First

Следующие учебники содержат загружаемые примеры приложений:

- [Начало работы с EF 6 с использованием MVC 5](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Охватывает широкий спектр Entity Framework Code First сценариев, включая миграцию и функции EF 6, такие как устойчивость подключений, перехват команд и асинхронные. Это обновленная версия [серии EF 5/MVC 4](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Предыдущий ряд содержит учебник по репозиторию и шаблонам единиц работы, которые не включены в новый ряд.
- [Введение в ASP.NET MVC 5](../mvc/overview/getting-started/introduction/getting-started.md). В этой статье рассматривается более узкий спектр Entity Framework Code First сценариев, но в нем представлено более исчерпывающее описание функций MVC.
- [Привязка модели и веб-формы](https://go.microsoft.com/fwlink/?LinkId=286117). Использует Code First в приложении веб-форм.
- [Начало работы с веб-формами ASP.NET 4,5](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Введение в веб-формы с определенным объемом Code First. Использует привязку модели.
- [Музыкальное хранилище MVC](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). Использует Code First в приложении MVC 3 для электронной коммерции, которое также реализует членство и авторизацию. Используемая здесь версия MVC и ASP.NET членства (проверка подлинности и авторизация); Дополнительные сведения о членстве в ASP.NET см. в разделе [https://asp.net/identity](https://asp.net/identity).

Другие ресурсы:

- [Entity Framework — Code First существующей базе данных](https://msdn.microsoft.com/data/jj200620). MSDN. Видео и пошаговое руководство, в котором показано, как использовать Code First с существующей базой данных.
- [Центр разработчиков данных — Entity Framework](https://msdn.microsoft.com/data/ef). MSDN. Руководство по Entity Framework документации, созданной и обслуживаемой группой Entity Framework, приведена по ссылке [Приступая к работе](https://msdn.microsoft.com/data/ee712907) .

См. также [книги о Entity Framework](#efbooks) и [дополнительных ресурсах Entity Framework](#otherefresources) далее в этом разделе.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Использование Entity Framework Code First Migrations

Большинство руководств по Code First, перечисленных выше, охватывают миграцию. См. также следующие ресурсы.

- [Веб-развертывание ASP.NET с помощью Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). Серия учебников из 2 частей, демонстрирующих использование Code First Migrations для развертывания базы данных.
- [Развертывание безопасного приложения ASP.NET MVC 5 с членством, OAuth и базой данных SQL на веб-сайте Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Microsoft Azure). Как использовать миграции для развертывания данных о членстве и приложениях в Azure.
- [Обзор веб-развертывания для Visual Studio и ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment). См. раздел **Настройка развертывания базы данных в Visual Studio** , в котором описано, как Code First migrations интегрирована в функции веб-развертывания Visual Studio.
- [Центр разработчиков данных — Code First migrations](https://msdn.microsoft.com/data/jj591621) (MSDN). Документация по миграции Entity Framework команды.
- [Серия презентаций для миграции](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). Блог EF). Три видео о дополнительных разделах Code First Migrations.
- [Code First migrations с веб-страницы ASP.NET сайтами](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites). Блог микесдотнеттинг). Показывает, как использовать Code First миграции с сайтом веб-страницы ASP.NET, поместив контекст данных в проект библиотеки классов Visual Studio.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Использование Entity Framework Database First или Model First (конструктор EF)

- [Начало работы с Entity Framework 6 Database First с помощью MVC 5](../mvc/overview/getting-started/database-first-development/setting-up-database.md). Запустите сценарий в обозреватель сервера, чтобы создать базу данных, а затем используйте конструктор Entity Framework для создания модели данных. Показывает, как создавать простые веб-страницы CRUD, а для других функций обработки данных можно воспользоваться одним из Code First руководств, так как все рабочие процессы EF используют один и тот же API DbContext.

Следующие ресурсы являются устаревшими. Они полезны, если вы хотите использовать Entity Framework версии 4,0 и хотите использовать элемент управления источниками данных для привязки данных в приложении веб-форм.

- [Начало работы с Entity Framework 4,0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). Показывает, как использовать элемент управления **EntityDataSource** .
- [Продолжение работы с Entity Framework](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(показывает, как использовать элемент управления **ObjectDataSource** . Содержит руководство по обработке параллелизма, руководству по повышению производительности EF и учебнику о новых возможностях EF 4,0.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Обработка связанных данных в Entity Framework (отложенная загрузка, упреждающая загрузка и явная загрузка)

- [Чтение связанных данных с Entity Framework в приложении MVC ASP.NET](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First, пример приложения MVC. Показанные методы применяются также к привязке модели веб-форм и рабочему процессу Database First.
- [Центр разработчиков данных — Загрузка связанных сущностей](https://msdn.microsoft.com/data/jj574232) (MSDN). Документация команды Entity Framework о загрузке связанных данных.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Оптимизация производительности Entity Framework

- [Расширенные Entity Framework сценарии для приложения ASP.NET](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md). Показывает, как выполнять собственные инструкции SQL или вызывать собственные хранимые процедуры, как отключить обнаружение изменений и отключить проверку при сохранении изменений.
- [Рекомендации по производительности для Entity Framework 5](https://msdn.microsoft.com/data/hh949853) (MSDN).
- [Вопросы производительности (Entity Framework)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [Максимальное повышение производительности с помощью Entity Framework в веб-приложении ASP.NET](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md). Применяется к Entity Framework 4,0.
- См. также [Оптимизация доступа к данным ASP.NET](#optimizingdataaccess) далее в этом разделе.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Обработка параллелизма в приложении Entity Framework

- [Обработка параллелизма с Entity Framework в приложении MVC ASP.NET](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First, API DbContext с использованием примера приложения MVC.
- [Центр разработчиков данных — шаблоны оптимистичного параллелизма](https://msdn.microsoft.com/data/jj592904) (MSDN). Документация по параллелизму группы Entity Framework.
- [Обработка параллелизма с помощью Entity Framework в веб-приложении ASP.NET](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). Применяется к Entity Framework 4,0. Database First, интерфейс ObjectContext, использующий пример приложения Web Forms.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Книги о Entity Framework

- [Программирование Entity Framework: DbContext](http://shop.oreilly.com/product/0636920022237.do) by Юлия Лерман и Роуэн Миллер.
- [Программирование Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) от Джулия Лерман и Роуэн Миллер.

Обе эти книги актуальны с использованием текущих рекомендуемых методов. Они предоставляют более полное представление о Entity Framework по сравнению с любым доступным в Интернете. Другой бюллетень, [программирование Entity Framework](http://shop.oreilly.com/product/9780596807252.do) от Юлия Лерман, больше и более исчерпывающий, но он более старый, и многие из методик, которые он охватывает, больше не являются рекомендуемым способом использования Entity Framework. См. также список книг, рекомендованных группой Entity Framework в [центре разработчиков данных — книги](https://msdn.microsoft.com/data/aa937716) на сайте MSDN.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>Другие ресурсы Entity Framework

- [Блог группы Entity Framework (ADO.NET)](https://blogs.msdn.com/b/adonet/). Один из лучших ресурсов для получения актуальных сведений и объявлений о новых улучшениях. Другие блоги, относящиеся к EF, см. в разделе Блоги at начало [работы с Entity Framework](https://msdn.microsoft.com/data/ee712907).
- [Журнал MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx). См. столбец **точки данных** , который часто относится к темам, связанным с Entity Framework.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>Привязка данных в приложениях веб-форм ASP.NET

- [ASP.NET параметры доступа к данным веб-форм](https://msdn.microsoft.com/library/jj822927.aspx) (<a id="wfmodelbinding"></a>MSDN).

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Использование привязки модели веб-форм

- [Привязка модели и веб-формы](https://go.microsoft.com/fwlink/?LinkId=286117). Серия руководств с использованием EF Code First.
- [Привязка модели Web Forms, часть 1. Выбор данных](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (блог Скотта Гатри (). В этих старых записях блога свойство, которое в настоящее время называется ItemType, называется ModelType, но в противном случае сведения, которые они содержат, являются допустимыми.
- [Привязка модели Web Forms, часть 2. Фильтрация данных](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (блог Скотта Гатри ().
- [Привязка модели веб-форм. часть 3. обновление и проверка](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (блог Скотта Гатри ().
- [Привязка модели веб-форм ASP.NET 4,5](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md). (видео).
- [Привязка модели, часть 1. Выбор данных](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (видео).
- [Привязка модели, часть 2 — Фильтрация](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (видео).
- [Начало работы с веб-формами ASP.NET 4,5 — Отображение элементов данных и сведений о них](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Использование элементов управления источниками данных веб-форм

- [Веб-серверные элементы управления "источник данных](https://msdn.microsoft.com/library/ms247258.aspx) " (MSDN).
- [Объявление о выпуске поставщика платформа динамических данных и элемента управления EntityDataSource для Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) (блог веб-разработки Майкрософт).

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Использование элементов управления, привязанных к данным и выражений привязки данных веб-форм

- [Привязка модели и веб-формы](https://go.microsoft.com/fwlink/?LinkId=286117). Серия руководств, использующая EF Code First.
- [Начало работы с веб-формами ASP.NET 4,5 — Отображение элементов данных и сведений о них](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).
- [Строго типизированные элементы управления данными](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (блог Скотта Гатри ().
- [Строго типизированные элементы управления данными](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (видео).
- [ASP.NET 4,5. веб Forms строго типизированные элементы управления данными](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (видео).
- [Веб-серверные элементы управления с привязкой к данным](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN).
- [Общие сведения о выражениях привязки данных](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). Эта страница охватывает только **eval** и **BIND**. Он не был обновлен для включения **Item** и **биндитем**.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>Работа с базами данных SQL Server

- [Функции базы данных SQL Server](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). Общие сведения о широком спектре SQL Serverых разделов см. в подразделах этой статьи в ОГЛАВЛЕНИи.
- [Выпуски SQL Server](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). Сводка доступных выпусков SQL Server со ссылками на дополнительные сведения о каждой из них.)
- [SQL Server строки подключения для веб-приложений ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Использование SQL Server Compact для веб-приложений ASP.NET](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN).
- [Microsoft SQL Server: образцы продуктов базы данных](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Примеры баз данных AdventureWorks.
- [Установка образцов баз данных](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). В дополнение к методам, показанным здесь, можно также скачать один из примеров MDF-файлов в папку данных приложения\_, преобразовать базу данных в LocalDB и создать строку подключения LocalDB. Сведения о том, как это сделать, см. [в разделе инструкции. обновление до LocalDB](https://msdn.microsoft.com/library/hh873188.aspx).

См. также следующие разделы по работе с SQL Server Express и LocalDB и выбором между SQL Server и базой данных SQL.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>Работа с SQL Server Express базами данных LocalDB

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). Официальное введение MSDN в LocalDB.
- [SQL Server строки подключения для веб-приложений ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Руководство. обновление до LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN). Как перенести MDF файл из более ранней версии SQL Server Express в LocalDB. Этот процесс также необходимо выполнить, если загрузить один из [образцов баз данных SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=117483).
- [Знакомство с LocalDB — УЛУЧШЕННЫЙ SQL Express](https://go.microsoft.com/fwlink/?LinkId=234375) (SQL Server Express блог). Содержит дополнительные сведения о том, почему создан LocalDB, чем входит в MSDN.
- [LocalDB: где находится моя база данных?](https://go.microsoft.com/fwlink/?LinkId=234376) (Блог SQL Server Express). Сведения о том, где создаются файлы базы данных LocalDB.
- [Использование LocalDB с полным IIS, часть 1: профиль пользователя](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express блога). LocalDB не предназначен для работы с IIS. В этой серии записей блога объясняются проблемы и некоторые обходные пути.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>Работа с базами данных SQL Server Express

- [SQL Server строки подключения для веб-приложений ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN). Если вы используете параметр строки подключения AttachDBFileName с SQL Server Express, см. раздел, в частности, в разделе Пользовательский экземпляр этой страницы.
- [Как стать владельцем локальной SQL Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (блог SQL Server Express). Распространенная проблема не способна работать с SQL Server Expressными базами данных, так как вы не являетесь администратором экземпляра SQL Server Express. По умолчанию только пользователь, установивший SQL Server Express, является администратором. В этом блоге объясняется, как сделать себя администратором SQL Server Express, если вы являетесь администратором компьютера.
- [Может ли веб-приложение ASP.NET использовать базу данных SQL Server Express в рабочей среде?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Работа с базой данных SQL Windows Azure

- [Развертывание безопасного приложения MVC ASP.NET с членством, OAuth и базой данных SQL на веб-сайте Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (Microsoft Azure сайте).
- [Базы данных SQL](https://docs.microsoft.com/azure/sql-database/) (Microsoft Azure сайт). Руководства и инструкции по началу работы.
- [База данных SQL Windows Azure](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). Узел верхнего уровня оглавления базы данных SQL в библиотеке MSDN.
- [Индекс вики-статей TechNet по базе данных SQL Windows Azure](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (сайт Microsoft TechNet).
- [Блок приложения обработки временной ошибки](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). Платформа, которая позволяет управлять временными сетевыми сбоями и ошибками подключения, возникающими в результате регулирования. Доступно в пакете NuGet: [Корпоративная библиотека 5,0 — блок приложения обработки временной ошибки](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling).
- [Начало работы с базой данных SQL и Entity Framework](https://msdn.microsoft.com/data/jj556244) (MSDN).
- [Комплект обучающих материалов по Windows Azure](https://www.microsoft.com/download/details.aspx?id=8396) (центр загрузки Майкрософт). Включает практические занятия по базе данных SQL.
- [Форум сообщества по базам данных SQL Windows Azure](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Переход в базу данных SQL Windows Azure](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN). Одна глава полного комплексного сценария группы шаблонов и практических рекомендаций корпорации Майкрософт. Описывает, почему может потребоваться выполнить миграцию, и как выполнить миграцию из SQL Server в базу данных SQL.
- [Миграция баз данных SQL Server в базу данных SQL Windows Azure](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).
- [Мастер миграции баз данных SQL](http://sqlazuremw.codeplex.com/). Средство с открытым исходным кодом для переноса баз данных в базу данных SQL и из нее.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>Выбор между SQL Server и базой данных SQL Windows Azure

- [Сравните SQL Server с базой данных SQL Windows Azure](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (сайт Microsoft TechNet).
- [Перенос данных в базу данных SQL Windows Azure: средства и методики](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). Включает разделы, которые сравнивают SQL Server с базой данных SQL и предоставляют рекомендации по переходу с SQL Server на базу данных SQL.
- [Инструкции по доставке базы данных SQL Windows Azure](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (сайт Microsoft TechNet).
- [Ограничения функций SQL Server (база данных SQL Windows Azure)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Хранилище таблиц Windows Azure и база данных SQL Windows Azure — сравнение и различия](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Для приложения, развертываемого в Windows Azure, хранилище таблиц Windows Azure может быть альтернативой базе данных SQL Windows Azure. Этот раздел поможет вам выбрать один из вариантов.
- [База данных SQL Windows Azure](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [Рекомендации и ограничения (база данных SQL Windows Azure)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>Работа с системами управления базами данных NoSQL

- [Службы данных Windows Azure](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure сайт). Ознакомьтесь с [руководством по функциям службы таблиц](https://docs.microsoft.com/azure/) и разделом **больших данных** на странице.
- [ASP.NET многоуровневое приложение с использованием таблиц хранилища, очередей и больших двоичных объектов](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure сайте). Полное руководство с загружаемым примером приложения, которое использует таблицы NoSQL хранилища Windows Azure.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>Использование запросов LINQ в приложениях ASP.NET

- [Параметры доступа к данным ASP.NET](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). Содержит введение в LINQ.
- [Обучающие видеоматериалы по LINQ](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (блог Джо Stagner)).
- [Поток форума ASP.NET со ссылками на динамические ресурсы LINQ](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq).

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Использование платформа динамических данных формирования шаблонов

- [Шаблоны проектов платформа динамических данных](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN). Рекомендации по использованию платформа динамических данных проектов.
- [Платформа динамических данных ASP.NET](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>Защита доступа к данным

- [Защита доступа к данным в ASP.NET](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN).
- [Вопросы безопасности (Entity Framework)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- [Как защитить строки подключения при использовании элементов управления источниками данных](https://msdn.microsoft.com/library/ms178372.aspx) (MSDN).

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>Оптимизация производительности доступа к данным

- [Обзор производительности ASP.NET](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [Кэширование ASP.NET](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [Повышение производительности ASP.NET](https://msdn.microsoft.com/library/ff647787) (MSDN). В верхней части этой страницы отображается предупреждение "содержимое с снято с учета", но большая часть информации по-прежнему актуальна и отсутствует совместимый обновленный ресурс.
- [Повышение производительности SQL Server](https://msdn.microsoft.com/library/ff647793) (MSDN). Тот же комментарий, что и предыдущая ссылка.

См. также [Оптимизация производительности Entity Framework](#optimizingef) выше в этом разделе.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>Развертывание базы данных

- [Веб-развертывание ASP.NET — Рекомендуемые ресурсы](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Доступ к данным через веб-службу

- [Доступ к данным через веб-службу](https://msdn.microsoft.com/library/ms178359.aspx#webservice) (MSDN). Рекомендации по использованию веб-API и WCF.
- [Начало работы с веб-API ASP.NET](../web-api/index.md).
- [WCF Data Services](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Часто задаваемые вопросы о доступе к данным ASP.NET](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [Учебники по веб-формам ASP.NET — данные](../web-forms/overview/data-access/index.md). Большинство из этих руководств относительно старые. Убедитесь, что вы прочитали [варианты доступа к данным ASP.NET](https://msdn.microsoft.com/library/ms178359.aspx) и [возможности хранения данных (создание облачных приложений в реальном времени с помощью Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) , чтобы вы не слишком посмотрели метод доступа к данным, который не подходит для вашего сценария.
- [ASP.NET карту содержимого MVC](../mvc/overview/getting-started/recommended-resources-for-mvc.md).
- [Учебники по веб-страницы ASP.NET — данные](../web-pages/overview/data/index.md).
- [Доступ к данным в Visual Studio](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN). Содержит список ссылок, схожих с этой картой содержимого, но с фокусом на Visual Studio, а не с ASP.NET.
