---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: Доступ к данным модели из контроллера | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Создание простого веб-приложения, считывающего и записывающего данные из базы данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437370"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="c1444-104">Доступ к данным модели из контроллера</span><span class="sxs-lookup"><span data-stu-id="c1444-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="c1444-105">по [Скотт Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="c1444-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="c1444-106">Это руководство для начинающих, в котором представлены основы ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c1444-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="c1444-107">Вы создадите простое веб-приложение, считывающее и записывающее данные из базы данных.</span><span class="sxs-lookup"><span data-stu-id="c1444-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="c1444-108">Посетите [центр обучения ASP.NET MVC](../../../index.md) , чтобы найти другие руководства и примеры для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c1444-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="c1444-109">В этом разделе мы создадим новый класс MoviesController и запишем код, который извлекает наши данные фильмов и отображает его обратно в браузере с помощью шаблона представления.</span><span class="sxs-lookup"><span data-stu-id="c1444-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="c1444-110">Щелкните правой кнопкой мыши папку Controllers и создайте новый MoviesController.</span><span class="sxs-lookup"><span data-stu-id="c1444-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="c1444-111">[![добавить контроллер](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c1444-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="c1444-112">Будет создан новый файл "MoviesController.cs" в папке \Controllers в нашем проекте.</span><span class="sxs-lookup"><span data-stu-id="c1444-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="c1444-113">Обновите Мовиеконтроллер, чтобы получить список фильмов из новой заполненной базы данных.</span><span class="sxs-lookup"><span data-stu-id="c1444-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="c1444-114">Мы выполняем запрос LINQ, поэтому мы получаем только фильмы, выпущенные после лета 1984.</span><span class="sxs-lookup"><span data-stu-id="c1444-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="c1444-115">Для отображения этого списка фильмов потребуется шаблон представления, поэтому щелкните метод правой кнопкой мыши и выберите Добавить представление, чтобы создать его.</span><span class="sxs-lookup"><span data-stu-id="c1444-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="c1444-116">В диалоговом окне Добавление представления указывается, что мы передаем список&lt;фильмов. Models. Movie&gt; в наш шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="c1444-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="c1444-117">В отличие от предыдущих случаев, когда мы использовали диалоговое окно Добавление представления и решили создать пустой шаблон, на этот раз мы будем указывать, что Visual Studio автоматически «Template» — шаблон представления для нас с содержимым по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c1444-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="c1444-118">Для этого нужно выбрать элемент "список" в раскрывающемся меню "Просмотр содержимого".</span><span class="sxs-lookup"><span data-stu-id="c1444-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="c1444-119">Помните, что при создании нового класса необходимо скомпилировать приложение, чтобы оно отображалось в диалоговом окне Добавление представления.</span><span class="sxs-lookup"><span data-stu-id="c1444-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![Добавить представление](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="c1444-121">Нажмите кнопку Добавить, и система автоматически создаст код для представления для нас, в котором отображается наш список фильмов.</span><span class="sxs-lookup"><span data-stu-id="c1444-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="c1444-122">Самое время, чтобы изменить заголовок &lt;H2&gt; на нечто вроде «мой список фильмов», как было сделано ранее в представлении «Hello World».</span><span class="sxs-lookup"><span data-stu-id="c1444-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="c1444-123">[![фильмов — Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c1444-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="c1444-124">Запустите приложение и перейдите по адресу/Movies в адресной строке.</span><span class="sxs-lookup"><span data-stu-id="c1444-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="c1444-125">Теперь мы извлекаем данные из базы данных с помощью базового запроса в контроллере и возвращали данные в представление, которое знает о фильмах.</span><span class="sxs-lookup"><span data-stu-id="c1444-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="c1444-126">Затем это представление просматривает список фильмов и создает таблицу данных для нас.</span><span class="sxs-lookup"><span data-stu-id="c1444-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="c1444-127">[Список фильмов ![— Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="c1444-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="c1444-128">Мы не будем реализовывать функции правки, детализации и удаления с помощью этого приложения, поэтому нам не нужны ссылки по умолчанию, созданные шаблоном шаблонов для нас.</span><span class="sxs-lookup"><span data-stu-id="c1444-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="c1444-129">Откройте файл/Мовиес/индекс.аспкс и удалите его.</span><span class="sxs-lookup"><span data-stu-id="c1444-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="c1444-130">Ниже приведен исходный код для того, как будет выглядеть обновленный шаблон представления после внесения этих изменений:</span><span class="sxs-lookup"><span data-stu-id="c1444-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="c1444-131">Он создает ссылки, которые нам не понадобятся, поэтому мы удалим их для этого примера.</span><span class="sxs-lookup"><span data-stu-id="c1444-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="c1444-132">Мы будем размещать нашу новую ссылку «Создать», как это дальше!</span><span class="sxs-lookup"><span data-stu-id="c1444-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="c1444-133">Вот как выглядит наше приложение при удалении этого столбца.</span><span class="sxs-lookup"><span data-stu-id="c1444-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="c1444-134">[Список фильмов ![— Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="c1444-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="c1444-135">Теперь у нас есть простой список данных о фильме.</span><span class="sxs-lookup"><span data-stu-id="c1444-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="c1444-136">Однако если щелкнуть ссылку "создать", будет выведено сообщение об ошибке, так как оно не подключено!</span><span class="sxs-lookup"><span data-stu-id="c1444-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="c1444-137">Давайте реализуем метод создания действия и позволяем пользователю вводить новые фильмы в нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="c1444-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c1444-138">[Назад](getting-started-with-mvc-part4.md)
> [Вперед](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="c1444-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
