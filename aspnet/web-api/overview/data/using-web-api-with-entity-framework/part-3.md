---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Использовать Code First Migrations для заполнения базы данных | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449118"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="bba42-102">Использование Code First Migrations для заполнения базы данных</span><span class="sxs-lookup"><span data-stu-id="bba42-102">Use Code First Migrations to Seed the Database</span></span>

<span data-ttu-id="bba42-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bba42-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="bba42-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="bba42-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="bba42-105">В этом разделе вы будете использовать [Code First migrations](https://msdn.microsoft.com/data/jj591621) в EF для заполнения базы данных тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="bba42-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="bba42-106">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="bba42-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="bba42-107">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bba42-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="bba42-108">Эта команда добавляет папку с именем миграции в проект и файл кода с именем Configuration.cs в папке migrations.</span><span class="sxs-lookup"><span data-stu-id="bba42-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="bba42-109">Откройте файл Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="bba42-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="bba42-110">Добавьте следующую инструкцию **using** .</span><span class="sxs-lookup"><span data-stu-id="bba42-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="bba42-111">Затем добавьте следующий код в метод **Configuration. SEED** :</span><span class="sxs-lookup"><span data-stu-id="bba42-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="bba42-112">В окне консоли диспетчера пакетов введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="bba42-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="bba42-113">Первая команда создает код, создающий базу данных, а вторая команда выполняет этот код.</span><span class="sxs-lookup"><span data-stu-id="bba42-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="bba42-114">База данных создается локально с помощью [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span><span class="sxs-lookup"><span data-stu-id="bba42-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="bba42-115">Изучение API (необязательно)</span><span class="sxs-lookup"><span data-stu-id="bba42-115">Explore the API (Optional)</span></span>

<span data-ttu-id="bba42-116">Нажмите F5, чтобы выполнить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="bba42-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="bba42-117">Visual Studio запускает IIS Express и запускает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="bba42-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="bba42-118">Затем Visual Studio запустит браузер и откроет домашнюю страницу приложения.</span><span class="sxs-lookup"><span data-stu-id="bba42-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="bba42-119">Когда Visual Studio выполняет веб-проект, он назначает номер порта.</span><span class="sxs-lookup"><span data-stu-id="bba42-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="bba42-120">На рисунке ниже показан номер порта 50524.</span><span class="sxs-lookup"><span data-stu-id="bba42-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="bba42-121">При запуске приложения вы увидите другой номер порта.</span><span class="sxs-lookup"><span data-stu-id="bba42-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="bba42-122">Домашняя страница реализуется с помощью ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="bba42-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="bba42-123">В верхней части страницы есть ссылка с текстом "API".</span><span class="sxs-lookup"><span data-stu-id="bba42-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="bba42-124">Эта ссылка позволяет получить автоматически созданную страницу справки для веб-API.</span><span class="sxs-lookup"><span data-stu-id="bba42-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="bba42-125">(Дополнительные сведения о создании этой страницы справки и о том, как добавить собственную документацию на страницу, см. в разделе [Создание страниц справки для веб-API ASP.NET](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) Можно щелкнуть ссылку на страницу справки, чтобы просмотреть сведения об API, включая формат запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="bba42-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="bba42-126">API включает операции CRUD в базе данных.</span><span class="sxs-lookup"><span data-stu-id="bba42-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="bba42-127">Ниже приведена сводка по API.</span><span class="sxs-lookup"><span data-stu-id="bba42-127">The following summarizes the API.</span></span>

| <span data-ttu-id="bba42-128">Авторы</span><span class="sxs-lookup"><span data-stu-id="bba42-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="bba42-129">GET api/authors</span><span class="sxs-lookup"><span data-stu-id="bba42-129">GET api/authors</span></span> | <span data-ttu-id="bba42-130">Получение всех авторов.</span><span class="sxs-lookup"><span data-stu-id="bba42-130">Get all authors.</span></span> |
| <span data-ttu-id="bba42-131">GET api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="bba42-131">GET api/authors/{id}</span></span> | <span data-ttu-id="bba42-132">Получить автора по ИДЕНТИФИКАТОРу.</span><span class="sxs-lookup"><span data-stu-id="bba42-132">Get an author by ID.</span></span> |
| <span data-ttu-id="bba42-133">POST /api/authors</span><span class="sxs-lookup"><span data-stu-id="bba42-133">POST /api/authors</span></span> | <span data-ttu-id="bba42-134">Создайте нового автора.</span><span class="sxs-lookup"><span data-stu-id="bba42-134">Create a new author.</span></span> |
| <span data-ttu-id="bba42-135">PUT /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="bba42-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="bba42-136">Обновление существующего автора.</span><span class="sxs-lookup"><span data-stu-id="bba42-136">Update an existing author.</span></span> |
| <span data-ttu-id="bba42-137">DELETE /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="bba42-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="bba42-138">Удаление автора.</span><span class="sxs-lookup"><span data-stu-id="bba42-138">Delete an author.</span></span> |

| <span data-ttu-id="bba42-139">Книги</span><span class="sxs-lookup"><span data-stu-id="bba42-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="bba42-140">GET /api/books</span><span class="sxs-lookup"><span data-stu-id="bba42-140">GET /api/books</span></span> | <span data-ttu-id="bba42-141">Получить все книги.</span><span class="sxs-lookup"><span data-stu-id="bba42-141">Get all books.</span></span> |
| <span data-ttu-id="bba42-142">GET /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="bba42-142">GET /api/books/{id}</span></span> | <span data-ttu-id="bba42-143">Получение книги по ИДЕНТИФИКАТОРу.</span><span class="sxs-lookup"><span data-stu-id="bba42-143">Get a book by ID.</span></span> |
| <span data-ttu-id="bba42-144">POST /api/books</span><span class="sxs-lookup"><span data-stu-id="bba42-144">POST /api/books</span></span> | <span data-ttu-id="bba42-145">Создайте новую книгу.</span><span class="sxs-lookup"><span data-stu-id="bba42-145">Create a new book.</span></span> |
| <span data-ttu-id="bba42-146">PUT /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="bba42-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="bba42-147">Обновление существующей книги.</span><span class="sxs-lookup"><span data-stu-id="bba42-147">Update an existing book.</span></span> |
| <span data-ttu-id="bba42-148">DELETE /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="bba42-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="bba42-149">Удаление книги.</span><span class="sxs-lookup"><span data-stu-id="bba42-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="bba42-150">Просмотр базы данных (необязательно)</span><span class="sxs-lookup"><span data-stu-id="bba42-150">View the Database (Optional)</span></span>

<span data-ttu-id="bba42-151">При выполнении команды Update-Database EF создал базу данных и вызвала метод `Seed`.</span><span class="sxs-lookup"><span data-stu-id="bba42-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="bba42-152">При локальном запуске приложения EF использует [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span><span class="sxs-lookup"><span data-stu-id="bba42-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="bba42-153">Вы можете просмотреть базу данных в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bba42-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="bba42-154">В меню **Представление** выберите **Обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="bba42-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="bba42-155">В диалоговом окне **соединение с сервером** в поле ввода **имя сервера** введите "(LocalDB) \v11.0".</span><span class="sxs-lookup"><span data-stu-id="bba42-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="bba42-156">Оставьте параметр **проверки подлинности** "Проверка подлинности Windows".</span><span class="sxs-lookup"><span data-stu-id="bba42-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="bba42-157">Нажмите кнопку **Соединить**.</span><span class="sxs-lookup"><span data-stu-id="bba42-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="bba42-158">Visual Studio подключается к LocalDB и отображает существующие базы данных в окне обозреватель объектов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bba42-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="bba42-159">Можно развернуть узлы, чтобы просмотреть таблицы, созданные EF.</span><span class="sxs-lookup"><span data-stu-id="bba42-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="bba42-160">Чтобы просмотреть данные, щелкните правой кнопкой мыши таблицу и выберите **Просмотреть данные**.</span><span class="sxs-lookup"><span data-stu-id="bba42-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="bba42-161">На следующем снимке экрана показаны результаты для таблицы Books.</span><span class="sxs-lookup"><span data-stu-id="bba42-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="bba42-162">Обратите внимание, что EF заполняет базу данных начальными данными, а таблица содержит внешний ключ для таблицы authors.</span><span class="sxs-lookup"><span data-stu-id="bba42-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="bba42-163">[Назад](part-2.md)
> [Вперед](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="bba42-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
