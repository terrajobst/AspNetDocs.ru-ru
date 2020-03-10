---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: Введение в ASP.NET MVC | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Создание простого веб-приложения, считывающего и записывающего данные из базы данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469800"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="55a34-104">Введение в ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="55a34-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="55a34-105">по [Скотт Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="55a34-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="55a34-106">Обновленная версия, если этот учебник доступен [здесь](../../getting-started/introduction/getting-started.md) с помощью [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span><span class="sxs-lookup"><span data-stu-id="55a34-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="55a34-107">В новом руководстве используется ASP.NET MVC 5, который обеспечивает множество улучшений в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="55a34-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="55a34-108">Это руководство для начинающих, в котором представлены основы ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="55a34-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="55a34-109">Вы создадите простое веб-приложение, считывающее и записывающее данные из базы данных.</span><span class="sxs-lookup"><span data-stu-id="55a34-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="55a34-110">Посетите [центр обучения ASP.NET MVC](../../../index.md) , чтобы найти другие руководства и примеры для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="55a34-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="55a34-111">Давайте создадим наше первое веб-приложение ASP.NET MVC с помощью [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span><span class="sxs-lookup"><span data-stu-id="55a34-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="55a34-112">Мы создадим небольшое приложение со списком фильмов, которое позволит нам создавать и перечислять фильмы.</span><span class="sxs-lookup"><span data-stu-id="55a34-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="55a34-113">Что вы создадите</span><span class="sxs-lookup"><span data-stu-id="55a34-113">What You'll Build</span></span>

<span data-ttu-id="55a34-114">Ниже приведено два снимка экрана создаваемого приложения.</span><span class="sxs-lookup"><span data-stu-id="55a34-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="55a34-115">Вы получите простую таблицу фильмов с различными столбцами.</span><span class="sxs-lookup"><span data-stu-id="55a34-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="55a34-116">[Список фильмов ![— Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="55a34-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="55a34-117">И у вас будет форма создания, чтобы мы могли добавлять в список фильмы.</span><span class="sxs-lookup"><span data-stu-id="55a34-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="55a34-118">[![создания фильма — Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="55a34-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="55a34-119">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="55a34-119">Skills You'll Learn</span></span>

<span data-ttu-id="55a34-120">В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55a34-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="55a34-121">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="55a34-121">You'll learn:</span></span>

- <span data-ttu-id="55a34-122">Создание нового проекта MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="55a34-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="55a34-123">Создание новой базы данных с помощью SQL Server</span><span class="sxs-lookup"><span data-stu-id="55a34-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="55a34-124">Создание контроллеров и представлений MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="55a34-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="55a34-125">Получение и отображение данных</span><span class="sxs-lookup"><span data-stu-id="55a34-125">How to retrieve and display data</span></span>
- <span data-ttu-id="55a34-126">Как изменить данные и включить проверку данных</span><span class="sxs-lookup"><span data-stu-id="55a34-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="55a34-127">Обновление схемы базы данных</span><span class="sxs-lookup"><span data-stu-id="55a34-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="55a34-128">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="55a34-128">Get Started</span></span>

<span data-ttu-id="55a34-129">Начните с запуска Visual Web Developer 2010 Express (теперь я называю его «VWD») и на начальном экране выберите пункт Создать проект.</span><span class="sxs-lookup"><span data-stu-id="55a34-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="55a34-130">Visual Web Developer — интегрированная среда разработки или интегрированная среда разработки.</span><span class="sxs-lookup"><span data-stu-id="55a34-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="55a34-131">Как и при использовании Microsoft Word для написания документов, для создания приложений используется интегрированная среда разработки.</span><span class="sxs-lookup"><span data-stu-id="55a34-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="55a34-132">В верхней части панели инструментов представлены различные доступные параметры, а также меню, которое можно было бы использовать для выбора файла | Новый проект.</span><span class="sxs-lookup"><span data-stu-id="55a34-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="55a34-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="55a34-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="55a34-134">Создание первого приложения</span><span class="sxs-lookup"><span data-stu-id="55a34-134">Creating Your First Application</span></span>

<span data-ttu-id="55a34-135">Приложения можно создавать с помощью Visual Basic или Visual C#.</span><span class="sxs-lookup"><span data-stu-id="55a34-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="55a34-136">Пока выберите элемент Visual C# слева, а затем — веб-приложение ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="55a34-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="55a34-137">Присвойте проекту имя "фильмы" и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="55a34-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="55a34-138">[![новый проект](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="55a34-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="55a34-139">В правой части обозреватель решений показаны все файлы и папки в приложении.</span><span class="sxs-lookup"><span data-stu-id="55a34-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="55a34-140">В среднем окно находится в том месте, где вы редактируете код и тратите большую часть времени.</span><span class="sxs-lookup"><span data-stu-id="55a34-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="55a34-141">Visual Studio использовала шаблон по умолчанию для только что созданного проекта MVC ASP.NET, поэтому у вас есть рабочее приложение, не делая ничего.</span><span class="sxs-lookup"><span data-stu-id="55a34-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="55a34-142">Это простой "Hello World!</span><span class="sxs-lookup"><span data-stu-id="55a34-142">This is a simple "Hello World!</span></span> <span data-ttu-id="55a34-143">и это хорошее место для начала работы с нашим приложением.</span><span class="sxs-lookup"><span data-stu-id="55a34-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="55a34-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="55a34-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="55a34-145">Нажмите кнопку "Воспроизведение" на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="55a34-145">Select the "play" button to the toolbar.</span></span>

![Начать отладку](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="55a34-147">Это зеленая стрелка, указывающая вправо, которая будет компилировать программу и запускать приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="55a34-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="55a34-148">*Примечание. Вы можете нажать клавишу F5 на клавиатуре или выбрать Отладка-&gt;начать отладку в меню "Отладка".*</span><span class="sxs-lookup"><span data-stu-id="55a34-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="55a34-149">Это приведет к тому, что Visual Web Developer запустит веб-сервер разработки и запустит наше веб-приложение (для этого не требуется настройка или действия, выполняемые вручную).</span><span class="sxs-lookup"><span data-stu-id="55a34-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="55a34-150">Затем он запускает браузер и настраивает его для просмотра домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="55a34-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="55a34-151">Обратите внимание, что в адресной строке браузера указано "localhost", а не что-то вроде example.com.</span><span class="sxs-lookup"><span data-stu-id="55a34-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="55a34-152">Это связано с тем, что localhost всегда указывает на локальный компьютер, который в данном случае выполняет только что созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="55a34-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="55a34-153">[Домашняя страница ![](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="55a34-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="55a34-154">Этот шаблон по умолчанию предоставляет две страницы для посещения и базовую страницу входа.</span><span class="sxs-lookup"><span data-stu-id="55a34-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="55a34-155">Давайте изменим, как работает это приложение, и немного изучите ASP.NET MVC в процессе.</span><span class="sxs-lookup"><span data-stu-id="55a34-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="55a34-156">Закройте браузер и измените код.</span><span class="sxs-lookup"><span data-stu-id="55a34-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="55a34-157">Дальше</span><span class="sxs-lookup"><span data-stu-id="55a34-157">Next</span></span>](getting-started-with-mvc-part2.md)
