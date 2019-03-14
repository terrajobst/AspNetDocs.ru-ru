---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Использовать Code First Migrations заполнить базу данных | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 733b1c343d774e5fa8757808be07a9ae67481d84
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065501"
---
<a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="7ef51-102">Использовать Code First Migrations заполнить базу данных</span><span class="sxs-lookup"><span data-stu-id="7ef51-102">Use Code First Migrations to Seed the Database</span></span>
====================
<span data-ttu-id="7ef51-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7ef51-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7ef51-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="7ef51-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="7ef51-105">В этом разделе вы воспользуетесь [Code First Migrations](https://msdn.microsoft.com/data/jj591621) в EF для заполнения базы тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="7ef51-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="7ef51-106">Из **средства** меню, выберите **диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="7ef51-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7ef51-107">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ef51-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="7ef51-108">Эта команда добавляет папку с именем миграции в проект, а также файл кода с именем Configuration.cs в папку Migrations.</span><span class="sxs-lookup"><span data-stu-id="7ef51-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="7ef51-109">Откройте файл Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="7ef51-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="7ef51-110">Добавьте следующий **с помощью** инструкции.</span><span class="sxs-lookup"><span data-stu-id="7ef51-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="7ef51-111">Затем добавьте следующий код, чтобы **Configuration.Seed** метод:</span><span class="sxs-lookup"><span data-stu-id="7ef51-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="7ef51-112">В окне консоли диспетчера пакетов введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="7ef51-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="7ef51-113">Первая команда создает код, который создает базу данных, а вторая команда выполняет этот код.</span><span class="sxs-lookup"><span data-stu-id="7ef51-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="7ef51-114">База данных создается локально, с помощью [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ef51-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="7ef51-115">Изучить API (необязательно)</span><span class="sxs-lookup"><span data-stu-id="7ef51-115">Explore the API (Optional)</span></span>

<span data-ttu-id="7ef51-116">Нажмите клавишу F5, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="7ef51-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="7ef51-117">Visual Studio запускает IIS Express и запускает веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7ef51-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="7ef51-118">Затем Visual Studio запустит браузер и откроется домашняя страница приложения.</span><span class="sxs-lookup"><span data-stu-id="7ef51-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="7ef51-119">При запуске веб-проекта в Visual Studio, он назначает номер порта.</span><span class="sxs-lookup"><span data-stu-id="7ef51-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="7ef51-120">На рисунке ниже номер порта — 50524.</span><span class="sxs-lookup"><span data-stu-id="7ef51-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="7ef51-121">При запуске приложения вы увидите другой номер порта.</span><span class="sxs-lookup"><span data-stu-id="7ef51-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="7ef51-122">На домашней странице реализуется с помощью ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="7ef51-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="7ef51-123">В верхней части страницы есть ссылка с текстом «API».</span><span class="sxs-lookup"><span data-stu-id="7ef51-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="7ef51-124">Эта ссылка позволяет открыть страницу автоматически созданную справку для веб-API.</span><span class="sxs-lookup"><span data-stu-id="7ef51-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="7ef51-125">(Чтобы узнать, как создается Эта страница справки, и как можно добавить вашу собственную документацию на страницу, см. в разделе [Создание страницы справки для веб-API ASP.NET](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) Можно щелкнуть справки странице приведены ссылки, чтобы просмотреть сведения об API, включая формат запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="7ef51-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="7ef51-126">API-Интерфейс позволяет операции CRUD в базе данных.</span><span class="sxs-lookup"><span data-stu-id="7ef51-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="7ef51-127">В следующей таблице показаны API.</span><span class="sxs-lookup"><span data-stu-id="7ef51-127">The following summarizes the API.</span></span>

| <span data-ttu-id="7ef51-128">Authors</span><span class="sxs-lookup"><span data-stu-id="7ef51-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="7ef51-129">Получение api/authors</span><span class="sxs-lookup"><span data-stu-id="7ef51-129">GET api/authors</span></span> | <span data-ttu-id="7ef51-130">Получение всех авторов.</span><span class="sxs-lookup"><span data-stu-id="7ef51-130">Get all authors.</span></span> |
| <span data-ttu-id="7ef51-131">GET api/authors / {id}</span><span class="sxs-lookup"><span data-stu-id="7ef51-131">GET api/authors/{id}</span></span> | <span data-ttu-id="7ef51-132">Получить автора по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="7ef51-132">Get an author by ID.</span></span> |
| <span data-ttu-id="7ef51-133">POST/api/authors</span><span class="sxs-lookup"><span data-stu-id="7ef51-133">POST /api/authors</span></span> | <span data-ttu-id="7ef51-134">Создание нового автора.</span><span class="sxs-lookup"><span data-stu-id="7ef51-134">Create a new author.</span></span> |
| <span data-ttu-id="7ef51-135">PUT/API/authors / {id}</span><span class="sxs-lookup"><span data-stu-id="7ef51-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="7ef51-136">Обновите существующие автора.</span><span class="sxs-lookup"><span data-stu-id="7ef51-136">Update an existing author.</span></span> |
| <span data-ttu-id="7ef51-137">DELETE/API/authors / {id}</span><span class="sxs-lookup"><span data-stu-id="7ef51-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="7ef51-138">Удалите автора.</span><span class="sxs-lookup"><span data-stu-id="7ef51-138">Delete an author.</span></span> |

| <span data-ttu-id="7ef51-139">Books</span><span class="sxs-lookup"><span data-stu-id="7ef51-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="7ef51-140">ПОЛУЧИТЬ /api/books</span><span class="sxs-lookup"><span data-stu-id="7ef51-140">GET /api/books</span></span> | <span data-ttu-id="7ef51-141">Получите все книги.</span><span class="sxs-lookup"><span data-stu-id="7ef51-141">Get all books.</span></span> |
| <span data-ttu-id="7ef51-142">GET/API/books / {id}</span><span class="sxs-lookup"><span data-stu-id="7ef51-142">GET /api/books/{id}</span></span> | <span data-ttu-id="7ef51-143">Получите книгу по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="7ef51-143">Get a book by ID.</span></span> |
| <span data-ttu-id="7ef51-144">POST/api/книг</span><span class="sxs-lookup"><span data-stu-id="7ef51-144">POST /api/books</span></span> | <span data-ttu-id="7ef51-145">Создайте новую книгу.</span><span class="sxs-lookup"><span data-stu-id="7ef51-145">Create a new book.</span></span> |
| <span data-ttu-id="7ef51-146">PUT/API/books / {id}</span><span class="sxs-lookup"><span data-stu-id="7ef51-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="7ef51-147">Обновите существующую книгу.</span><span class="sxs-lookup"><span data-stu-id="7ef51-147">Update an existing book.</span></span> |
| <span data-ttu-id="7ef51-148">DELETE/API/books / {id}</span><span class="sxs-lookup"><span data-stu-id="7ef51-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="7ef51-149">Удалите книгу.</span><span class="sxs-lookup"><span data-stu-id="7ef51-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="7ef51-150">Представление базы данных (необязательно)</span><span class="sxs-lookup"><span data-stu-id="7ef51-150">View the Database (Optional)</span></span>

<span data-ttu-id="7ef51-151">При выполнении команды Update-Database, EF создает базу данных и вызывается `Seed` метод.</span><span class="sxs-lookup"><span data-stu-id="7ef51-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="7ef51-152">При локальном запуске приложения EF использует [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ef51-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="7ef51-153">Базы данных можно просмотреть в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ef51-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="7ef51-154">Из **представление** меню, выберите **обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7ef51-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="7ef51-155">В **соединение с сервером** диалоговое окно, в **имя_сервера** поле ввода, введите «(localdb) \v11.0».</span><span class="sxs-lookup"><span data-stu-id="7ef51-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="7ef51-156">Оставьте **проверки подлинности** для параметра «Проверка подлинности Windows».</span><span class="sxs-lookup"><span data-stu-id="7ef51-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="7ef51-157">Нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="7ef51-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="7ef51-158">Visual Studio подключается к LocalDB и отображает существующие базы данных в окне обозревателя объектов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7ef51-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="7ef51-159">Можно развернуть узлы для просмотра таблиц, которые созданы EF.</span><span class="sxs-lookup"><span data-stu-id="7ef51-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="7ef51-160">Чтобы просмотреть данные, щелкните правой кнопкой мыши таблицу и выберите **данные представления**.</span><span class="sxs-lookup"><span data-stu-id="7ef51-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="7ef51-161">На следующем рисунке показан результаты в электронной таблице.</span><span class="sxs-lookup"><span data-stu-id="7ef51-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="7ef51-162">Обратите внимание на то, что EF заполняет базу данных начального значения, а таблица содержит внешний ключ к таблице Authors.</span><span class="sxs-lookup"><span data-stu-id="7ef51-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="7ef51-163">[Назад](part-2.md)
> [Вперед](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="7ef51-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
