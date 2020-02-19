---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: Доступ к данным модели из контроллера | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленная версия этого учебника доступна здесь, в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще в исполнении и демонстрации...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456170"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="2bfe9-104">Доступ к данным модели из контроллера</span><span class="sxs-lookup"><span data-stu-id="2bfe9-104">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="2bfe9-105">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2bfe9-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="2bfe9-106">Обновленная версия этого учебника доступна [здесь](../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="2bfe9-107">Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="2bfe9-108">В этом разделе вы создадите новый класс `MoviesController` и запишете код, который извлекает данные фильмов и отображает их в браузере с помощью шаблона представления.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="2bfe9-109">**Создайте приложение,** прежде чем переходить к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="2bfe9-110">Щелкните правой кнопкой мыши папку *Controllers* и создайте новый контроллер `MoviesController`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="2bfe9-111">Указанные ниже параметры не отображаются, пока не будет построено приложение.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="2bfe9-112">Выберите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-112">Select the following options:</span></span>

- <span data-ttu-id="2bfe9-113">Имя контроллера: **MoviesController**.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="2bfe9-114">(Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-114">(This is the default.</span></span> <span data-ttu-id="2bfe9-115">)</span><span class="sxs-lookup"><span data-stu-id="2bfe9-115">)</span></span>
- <span data-ttu-id="2bfe9-116">Шаблон: **контроллер MVC с действиями чтения и записи и представлениями с использованием Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="2bfe9-117">Класс модели: **Movie (MvcMovie. Models)** .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="2bfe9-118">Класс контекста данных: **мовиедбконтекст (MvcMovie. Models)** .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="2bfe9-119">Представления: **Razor (CSHTML)** .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="2bfe9-120">(Значение по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="2bfe9-120">(The default.)</span></span>

![аддскаффолдедмовиеконтроллер](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="2bfe9-122">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-122">Click **Add**.</span></span> <span data-ttu-id="2bfe9-123">Visual Studio Express создает следующие файлы и папки:</span><span class="sxs-lookup"><span data-stu-id="2bfe9-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="2bfe9-124">Файл *MoviesController.CS* в папке *Controllers* проекта.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="2bfe9-125">Папка *фильмов* в папке *views* проекта.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="2bfe9-126">В новой папке *Виевс\мовиес* *создаются. cshtml, DELETE. cshtml, Details. cshtml, Edit. cshtml*и *index. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="2bfe9-127">ASP.NET MVC 4 автоматически создал методы и представления действия CRUD (создание, чтение, обновление и удаление) для вас (автоматическое создание методов и представлений действий CRUD называется формированием шаблонов).</span><span class="sxs-lookup"><span data-stu-id="2bfe9-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="2bfe9-128">Теперь у вас есть полнофункциональное веб-приложение, которое позволяет создавать, перечислять, изменять и удалять записи фильмов.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="2bfe9-129">Запустите приложение и перейдите к контроллеру `Movies`, добавив */Movies* в URL-адрес в адресной строке браузера.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="2bfe9-130">Поскольку приложение полагается на маршрутизацию по умолчанию (определенную в файле *Global. asax* ), запрос браузера `http://localhost:xxxxx/Movies` направляется в метод действия `Index` по умолчанию контроллера `Movies`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="2bfe9-131">Иными словами, `http://localhost:xxxxx/Movies` запроса браузера фактически аналогичен `http://localhost:xxxxx/Movies/Index`запроса браузера.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="2bfe9-132">Результатом является пустой список фильмов, так как вы еще не добавили их.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="2bfe9-133">Создание фильма</span><span class="sxs-lookup"><span data-stu-id="2bfe9-133">Creating a Movie</span></span>

<span data-ttu-id="2bfe9-134">Щелкните ссылку **Create New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="2bfe9-134">Select the **Create New** link.</span></span> <span data-ttu-id="2bfe9-135">Введите некоторые сведения о фильме и нажмите кнопку **создать** .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="2bfe9-136">Нажатие кнопки **создать** приводит к тому, что форма будет отправлена на сервер, где сведения о фильме будут сохранены в базе данных.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="2bfe9-137">Затем вы перейдете на URL-адрес */Movies* , на котором можно увидеть созданный фильм в списке.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="2bfe9-138">![индексвхенхарримет](accessing-your-models-data-from-a-controller/_static/image4.png "индексвхенхарримет")</span><span class="sxs-lookup"><span data-stu-id="2bfe9-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="2bfe9-139">Создайте еще несколько записей фильмов.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-139">Create a couple more movie entries.</span></span> <span data-ttu-id="2bfe9-140">Попробуйте воспользоваться ссылками **Изменить**, **Сведения** и **Удалить** — все они работают.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="2bfe9-141">Проверка созданного кода</span><span class="sxs-lookup"><span data-stu-id="2bfe9-141">Examining the Generated Code</span></span>

<span data-ttu-id="2bfe9-142">Откройте файл *контроллерс\мовиесконтроллер.КС* и изучите созданный метод `Index`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="2bfe9-143">Ниже показана часть контроллера фильмов с методом `Index`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="2bfe9-144">Следующая строка из класса `MoviesController` создает экземпляр контекста базы данных Movie, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="2bfe9-145">Для запроса, изменения и удаления фильмов можно использовать контекст базы данных Movie.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="2bfe9-146">Запрос к контроллеру `Movies` возвращает все записи в таблице `Movies` базы данных фильмов, а затем передает результаты в представление `Index`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="2bfe9-147">Строго типизированные модели и ключевое слово @model</span><span class="sxs-lookup"><span data-stu-id="2bfe9-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="2bfe9-148">Ранее в этом руководстве вы узнали, как контроллер может передавать данные или объекты в шаблон представления с помощью объекта `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="2bfe9-149">`ViewBag` — это динамический объект, предоставляющий удобный способ для передачи сведений в представление.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="2bfe9-150">ASP.NET MVC также предоставляет возможность передавать строго типизированные данные или объекты в шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="2bfe9-151">Такой строго типизированный подход обеспечивает лучшую проверку кода во время компиляции и более широкие возможности IntelliSense в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="2bfe9-152">Механизм формирования шаблонов в Visual Studio использовал этот подход с классом `MoviesController` и шаблонами представления при создании методов и представлений.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="2bfe9-153">В файле *контроллерс\мовиесконтроллер.КС* изучите созданный метод `Details`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="2bfe9-154">Ниже показана часть контроллера фильмов с методом `Details`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="2bfe9-155">Если `Movie` найден, экземпляр модели `Movie` передается в представление Details.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="2bfe9-156">Изучите содержимое файла *виевс\мовиес\детаилс.кштмл* .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="2bfe9-157">Включив инструкцию `@model` в верхней части файла шаблона представления, можно указать тип объекта, который предполагается отобразить в представлении.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="2bfe9-158">При создании контроллера movie Visual Studio автоматически включает следующий оператор `@model` в начало файла *Details.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="2bfe9-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="2bfe9-159">Эта директива `@model` обеспечивает доступ к фильму, который контроллер передал в представление с использованием строго типизированного объекта `Model`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="2bfe9-160">Например, в шаблоне *Details. cshtml* код передает каждое поле movie в `DisplayNameFor` и [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) вспомогательные методы HTML с помощью строго типизированного объекта `Model`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="2bfe9-161">Методы Create и Edit и шаблоны представлений также передают объект модели фильма.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="2bfe9-162">Изучите шаблон представления *index. cshtml* и метод `Index` в файле *MoviesController.CS* .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="2bfe9-163">Обратите внимание, что код создает объект [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) при вызове вспомогательного метода `View` в методе `Index` действия.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="2bfe9-164">Затем код передает этот список `Movies` из контроллера в представление:</span><span class="sxs-lookup"><span data-stu-id="2bfe9-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="2bfe9-165">При создании контроллера Movie Visual Studio Express автоматически включил следующую инструкцию `@model` в начало файла *index. cshtml* :</span><span class="sxs-lookup"><span data-stu-id="2bfe9-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="2bfe9-166">Эта директива `@model` позволяет получить доступ к списку фильмов, переданных контроллером в представление, используя строго типизированный объект `Model`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="2bfe9-167">Например, в шаблоне *index. cshtml* код проходит через фильмы, выполняя инструкцию `foreach` для строго типизированного объекта `Model`:</span><span class="sxs-lookup"><span data-stu-id="2bfe9-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="2bfe9-168">Так как объект `Model` является строго типизированным (в виде объекта `IEnumerable<Movie>`), каждый объект `item` в цикле вводится как `Movie`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="2bfe9-169">Помимо прочих преимуществ это означает, что во время компиляции кода и полной поддержки IntelliSense в редакторе кода вы получаете проверку.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![моделинтеллисенсе](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="2bfe9-171">Работа с SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="2bfe9-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="2bfe9-172">Entity Framework Code First обнаружила, что предоставленная строка подключения к базе данных указывала на базу данных `Movies`, которая еще не существовала, поэтому Code First автоматически создавала базу данных.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="2bfe9-173">Чтобы убедиться, что он создан, найдите в папке *приложение\_данные* .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="2bfe9-174">Если файл *movies. mdf* не отображается, нажмите кнопку " **Показать все файлы** " на панели инструментов **Обозреватель решений** , нажмите кнопку " **Обновить** ", а затем разверните папку " *приложение\_данные* ".</span><span class="sxs-lookup"><span data-stu-id="2bfe9-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="2bfe9-175">Дважды щелкните *movies. mdf* , чтобы открыть **Обозреватель баз данных**, а затем разверните папку **таблицы** , чтобы просмотреть таблицу фильмов.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="2bfe9-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="2bfe9-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="2bfe9-177">Если обозреватель баз данных не отображается, в меню **Сервис** выберите **подключиться к базе данных**, а затем отменяет диалоговое окно **Выбор источника данных** .</span><span class="sxs-lookup"><span data-stu-id="2bfe9-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="2bfe9-178">Это приведет к принудительному открытию обозревателя баз данных.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-178">This will force open the database explorer.</span></span>

> [!NOTE]
> <span data-ttu-id="2bfe9-179">Если вы используете VWD или Visual Studio 2010 и получаете ошибку, похожую на одну из следующих:</span><span class="sxs-lookup"><span data-stu-id="2bfe9-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="2bfe9-180">База данных "C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_ДАТА\МОВИЕС. Невозможно открыть MDF, так как он имеет версию 706.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="2bfe9-181">Этот сервер поддерживает версию 655 и более ранние.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="2bfe9-182">Переход на предыдущую версию не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="2bfe9-183">&quot;исключение InvalidOperation не обработано пользовательским кодом&quot; в предоставленном объекте SqlConnection не указан исходный каталог.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="2bfe9-184">Необходимо установить [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) и [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span><span class="sxs-lookup"><span data-stu-id="2bfe9-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="2bfe9-185">Проверьте строку подключения `MovieDBContext`, указанную на предыдущей странице.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>

<span data-ttu-id="2bfe9-186">Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Показать данные таблицы** , чтобы просмотреть созданные данные.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="2bfe9-187">Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Open Table Definition (Открыть определение таблицы** ), чтобы увидеть структуру таблицы, которая Entity Framework Code First создана.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="2bfe9-188">Обратите внимание, что схема `Movies` таблицы сопоставляется с созданным ранее классом `Movie`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-188">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="2bfe9-189">Entity Framework Code First автоматически создали эту схему на основе класса `Movie`.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-189">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="2bfe9-190">По завершении закройте подключение, щелкнув правой кнопкой мыши *мовиедбконтекст* и выбрав **закрыть подключение**.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-190">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="2bfe9-191">(Если вы не закроете подключение, при следующем запуске проекта может появиться сообщение об ошибке).</span><span class="sxs-lookup"><span data-stu-id="2bfe9-191">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

<span data-ttu-id="2bfe9-192">Теперь у вас есть база данных и простая страница со списком для отображения содержимого из нее.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-192">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="2bfe9-193">В следующем руководстве мы рассмотрим оставшуюся часть кода с формированием шаблонов и добавим метод `SearchIndex` и представление `SearchIndex`, которое позволяет выполнять поиск фильмов в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="2bfe9-193">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2bfe9-194">[Назад](adding-a-model.md)
> [Вперед](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="2bfe9-194">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
