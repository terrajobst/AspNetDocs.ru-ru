---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: Создание строки подключения и работа с SQL Server LocalDB | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: d3c6e736c5dcf4a3615e3c72cfc033effc7cc8e6
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519314"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="45f31-102">Создание строки подключения и работа с SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="45f31-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="45f31-103">по [Рик Андерсон (]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="45f31-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="45f31-104">Создание строки подключения и работа с SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="45f31-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="45f31-105">Созданный класс `MovieDBContext` обрабатывает задачу подключения к базе данных и сопоставление объектов `Movie` с записями базы данных.</span><span class="sxs-lookup"><span data-stu-id="45f31-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="45f31-106">Одним из вопросов, которые вы можете спросить, является указание того, к какой базе данных будет подключаться.</span><span class="sxs-lookup"><span data-stu-id="45f31-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="45f31-107">На самом деле нет необходимости указывать, какую базу данных использовать, Entity Framework по умолчанию будет использовать [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="45f31-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="45f31-108">В этом разделе мы явно добавим строку подключения в файл *Web. config* приложения.</span><span class="sxs-lookup"><span data-stu-id="45f31-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="45f31-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="45f31-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="45f31-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) — это упрощенная версия SQL Server Express ядро СУБД, которая запускается по запросу и запускается в пользовательском режиме.</span><span class="sxs-lookup"><span data-stu-id="45f31-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="45f31-111">LocalDB выполняется в специальном режиме выполнения SQL Server Express, который позволяет работать с базами данных в виде *MDF* -файлов.</span><span class="sxs-lookup"><span data-stu-id="45f31-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="45f31-112">Как правило, файлы базы данных LocalDB хранятся в папке *приложения\_данных* веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="45f31-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="45f31-113">SQL Server Express не рекомендуется использовать в рабочих веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="45f31-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="45f31-114">LocalDB в частности не следует использовать для рабочей среды с веб-приложением, поскольку оно не предназначено для работы с IIS.</span><span class="sxs-lookup"><span data-stu-id="45f31-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="45f31-115">Однако базу данных LocalDB можно легко перенести в SQL Server или SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="45f31-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="45f31-116">В Visual Studio 2017 LocalDB устанавливается по умолчанию в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45f31-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="45f31-117">По умолчанию Entity Framework ищет строку подключения с именем, аналогичную классу контекста объекта (`MovieDBContext` для этого проекта).</span><span class="sxs-lookup"><span data-stu-id="45f31-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="45f31-118">Дополнительные сведения см. в разделе [SQL Server строки подключения для веб-приложений ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx).</span><span class="sxs-lookup"><span data-stu-id="45f31-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="45f31-119">Откройте корневой файл *Web. config* приложения, показанный ниже.</span><span class="sxs-lookup"><span data-stu-id="45f31-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="45f31-120">(Не файл *Web. config* в папке *views* .)</span><span class="sxs-lookup"><span data-stu-id="45f31-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="45f31-121">Найдите элемент `<connectionStrings>`:</span><span class="sxs-lookup"><span data-stu-id="45f31-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="45f31-122">Добавьте следующую строку подключения в элемент `<connectionStrings>` в файле *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="45f31-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="45f31-123">В следующем примере показана часть файла *Web. config* с добавленной новой строкой подключения:</span><span class="sxs-lookup"><span data-stu-id="45f31-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="45f31-124">Две строки подключения очень похожи.</span><span class="sxs-lookup"><span data-stu-id="45f31-124">The two connection strings are very similar.</span></span> <span data-ttu-id="45f31-125">Первая строка подключения называется `DefaultConnection` и используется для базы данных членства для управления доступом к приложению.</span><span class="sxs-lookup"><span data-stu-id="45f31-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="45f31-126">Добавленная строка подключения указывает базу данных LocalDB с именем *Movie. mdf* , расположенную в папке *приложения\_данных* .</span><span class="sxs-lookup"><span data-stu-id="45f31-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="45f31-127">Мы не будем использовать базу данных членства в этом руководстве. Дополнительные сведения о членстве, проверке подлинности и безопасности см. в моем руководстве [Создание приложения ASP.NET MVC с проверкой подлинности и базой данных SQL и развертывание в службе приложений Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="45f31-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="45f31-128">Имя строки подключения должно совпадать с именем класса [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) .</span><span class="sxs-lookup"><span data-stu-id="45f31-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="45f31-129">В действительности не нужно добавлять строку подключения `MovieDBContext`.</span><span class="sxs-lookup"><span data-stu-id="45f31-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="45f31-130">Если строка подключения не указана, Entity Framework создаст базу данных LocalDB в каталоге Users с полным именем класса [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) (в данном случае `MvcMovie.Models.MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="45f31-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="45f31-131">Вы можете присвоить базе данных любое имя, если оно имеет значение *. Суффикс MDF* .</span><span class="sxs-lookup"><span data-stu-id="45f31-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="45f31-132">Например, можно присвоить имя базе данных *мифилмс. mdf*.</span><span class="sxs-lookup"><span data-stu-id="45f31-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="45f31-133">Далее предстоит создать новый класс `MoviesController`, который можно использовать для отображения данных фильмов и предоставления пользователям возможности создавать новые списки фильмов.</span><span class="sxs-lookup"><span data-stu-id="45f31-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="45f31-134">[Назад](adding-a-model.md)
> [Вперед](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="45f31-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
