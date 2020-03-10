---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: Введение в ASP.NET MVC 3 (C#) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1)...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434730"
---
# <a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="5d86d-103">Введение в ASP.NET MVC 3 (C#)</span><span class="sxs-lookup"><span data-stu-id="5d86d-103">Intro to ASP.NET MVC 3 (C#)</span></span>

<span data-ttu-id="5d86d-104">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5d86d-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="5d86d-105">Обновленная версия этого учебника доступна [здесь](../../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="5d86d-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="5d86d-106">Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="5d86d-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="5d86d-107">В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d86d-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="5d86d-108">Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="5d86d-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="5d86d-109">Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="5d86d-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="5d86d-110">Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:</span><span class="sxs-lookup"><span data-stu-id="5d86d-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="5d86d-111">Предварительные требования для Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="5d86d-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="5d86d-112">Обновление инструментов ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="5d86d-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="5d86d-113">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)</span><span class="sxs-lookup"><span data-stu-id="5d86d-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="5d86d-114">Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="5d86d-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="5d86d-115">Для этого раздела доступен проект Visual C# Web Developer с исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="5d86d-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="5d86d-116">[Скачайте C# версию](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="5d86d-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="5d86d-117">Если вы предпочитаете Visual Basic, переключитесь на [Visual Basic версию](../vb/intro-to-aspnet-mvc-3.md) этого учебника.</span><span class="sxs-lookup"><span data-stu-id="5d86d-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="5d86d-118">Что вы создадите</span><span class="sxs-lookup"><span data-stu-id="5d86d-118">What You'll Build</span></span>

<span data-ttu-id="5d86d-119">Вы реализуете простое приложение с перечнем фильмов, которое поддерживает создание, изменение и перечисление фильмов из базы данных.</span><span class="sxs-lookup"><span data-stu-id="5d86d-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="5d86d-120">Ниже приведены два снимка экрана создаваемого приложения.</span><span class="sxs-lookup"><span data-stu-id="5d86d-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="5d86d-121">Он содержит страницу, на которой отображается список фильмов из базы данных:</span><span class="sxs-lookup"><span data-stu-id="5d86d-121">It includes a page that displays a list of movies from a database:</span></span>

![мовиесвисвариауссм](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="5d86d-123">Кроме того, приложение позволяет добавлять, изменять и удалять фильмы, а также просматривать сведения о них.</span><span class="sxs-lookup"><span data-stu-id="5d86d-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="5d86d-124">Все сценарии ввода данных включают проверку, чтобы убедиться, что данные, хранящиеся в базе данных, верны.</span><span class="sxs-lookup"><span data-stu-id="5d86d-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="5d86d-125">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="5d86d-125">Skills You'll Learn</span></span>

<span data-ttu-id="5d86d-126">В этом учебнике вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="5d86d-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="5d86d-127">Создание нового проекта MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5d86d-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="5d86d-128">Создание контроллеров и представлений MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5d86d-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="5d86d-129">Создание новой базы данных с помощью Entity Framework парадигмы Code First.</span><span class="sxs-lookup"><span data-stu-id="5d86d-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="5d86d-130">Получение и отображение данных.</span><span class="sxs-lookup"><span data-stu-id="5d86d-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="5d86d-131">Как изменить данные и включить проверку данных.</span><span class="sxs-lookup"><span data-stu-id="5d86d-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5d86d-132">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="5d86d-132">Getting Started</span></span>

<span data-ttu-id="5d86d-133">Начните с запуска Visual Web Developer 2010 Express («Visual Web Developer») и выберите пункт **создать проект** на **начальной** странице.</span><span class="sxs-lookup"><span data-stu-id="5d86d-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="5d86d-134">Visual Web Developer — это интегрированная среда разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="5d86d-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="5d86d-135">Как и при использовании Microsoft Word для написания документов, для создания приложений используется интегрированная среда разработки.</span><span class="sxs-lookup"><span data-stu-id="5d86d-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="5d86d-136">В Visual Web Developer есть панель инструментов, в верхней части которой показаны различные доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="5d86d-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="5d86d-137">Также есть меню, предоставляющее еще один способ выполнения задач в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="5d86d-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="5d86d-138">(Например, вместо выбора **нового проекта** на **начальной** странице можно использовать меню и выбрать **файл** &gt; **Новый проект**).</span><span class="sxs-lookup"><span data-stu-id="5d86d-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="5d86d-139">Создание первого приложения</span><span class="sxs-lookup"><span data-stu-id="5d86d-139">Creating Your First Application</span></span>

<span data-ttu-id="5d86d-140">Приложения можно создавать с помощью Visual Basic или визуального C# элемента в качестве языка программирования.</span><span class="sxs-lookup"><span data-stu-id="5d86d-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="5d86d-141">Выберите элемент C# Visual слева, а затем выберите **ASP.NET MVC 3 веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="5d86d-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="5d86d-142">Присвойте проекту имя "MvcMovie" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5d86d-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="5d86d-143">(Если вы предпочитаете Visual Basic, переключитесь на [Visual Basic версию](../vb/intro-to-aspnet-mvc-3.md) этого учебника.)</span><span class="sxs-lookup"><span data-stu-id="5d86d-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="5d86d-144">В диалоговом окне **Новый проект ASP.NET MVC 3** выберите **Интернет приложение**.</span><span class="sxs-lookup"><span data-stu-id="5d86d-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="5d86d-145">Установите флажок **использовать разметку HTML5** и оставьте **Razor** в качестве ядра представления по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5d86d-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="5d86d-146">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5d86d-146">Click **OK**.</span></span> <span data-ttu-id="5d86d-147">Visual Web Developer использовал шаблон по умолчанию для только что созданного проекта MVC ASP.NET, так что у вас уже есть рабочее приложение, не делая ничего.</span><span class="sxs-lookup"><span data-stu-id="5d86d-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="5d86d-148">Это простой "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="5d86d-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="5d86d-149">и это хорошее место для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="5d86d-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="5d86d-150">В меню **Отладка** выберите пункт **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="5d86d-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="5d86d-151">Обратите внимание, что для начала отладки используется сочетание клавиш F5.</span><span class="sxs-lookup"><span data-stu-id="5d86d-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="5d86d-152">F5 заставляет Visual Web Developer запустить веб-сервер разработки и запустить веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="5d86d-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="5d86d-153">Visual Web Developer запускает браузер и открывает домашнюю страницу приложения.</span><span class="sxs-lookup"><span data-stu-id="5d86d-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="5d86d-154">Обратите внимание, что в адресной строке браузера указано `localhost` и не что-то вроде `example.com`.</span><span class="sxs-lookup"><span data-stu-id="5d86d-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="5d86d-155">Это связано с тем, что `localhost` всегда указывает на локальный компьютер, который в данном случае выполняет только что созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="5d86d-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="5d86d-156">Когда Visual Web Developer запускает веб-проект, для веб-сервера используется случайный порт.</span><span class="sxs-lookup"><span data-stu-id="5d86d-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="5d86d-157">На приведенном ниже рисунке случайным номером порта является 43246.</span><span class="sxs-lookup"><span data-stu-id="5d86d-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="5d86d-158">При запуске приложения вы, вероятно, увидите другой номер порта.</span><span class="sxs-lookup"><span data-stu-id="5d86d-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="5d86d-159">Сразу после этого шаблон по умолчанию предоставляет две страницы для посещения и базовую страницу входа.</span><span class="sxs-lookup"><span data-stu-id="5d86d-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="5d86d-160">Следующим шагом является изменение того, как это приложение работает, и немного изучите ASP.NET MVC в процессе.</span><span class="sxs-lookup"><span data-stu-id="5d86d-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="5d86d-161">Закройте браузер и измените код.</span><span class="sxs-lookup"><span data-stu-id="5d86d-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5d86d-162">Дальше</span><span class="sxs-lookup"><span data-stu-id="5d86d-162">Next</span></span>](adding-a-controller.md)
