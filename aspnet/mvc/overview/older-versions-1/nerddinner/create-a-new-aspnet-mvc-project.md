---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Создание нового проекта MVC ASP.NET | Документация Майкрософт
author: microsoft
description: На шаге 1 показано, как разместить базовую структуру приложения NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469242"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="5c9c1-103">Создание проекта ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="5c9c1-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="5c9c1-104">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5c9c1-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="5c9c1-105">Скачать в формате PDF</span><span class="sxs-lookup"><span data-stu-id="5c9c1-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="5c9c1-106">Это шаг 1 бесплатного [учебника по приложению "NerdDinner"](introducing-the-nerddinner-tutorial.md) , в котором рассматривается создание небольшого, но полного веб-приложения с использованием ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="5c9c1-107">На шаге 1 показано, как разместить базовую структуру приложения NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="5c9c1-108">Если вы используете ASP.NET MVC 3, мы рекомендуем следовать руководствам по [Начало работы в MVC 3 или в приложении для](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [музыкального магазина MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="5c9c1-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="5c9c1-109">NerdDinner шаг 1. файл&gt;новый проект</span><span class="sxs-lookup"><span data-stu-id="5c9c1-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="5c9c1-110">Мы начнем наше приложение NerdDinner, выбрав пункт меню **файл-&gt;новый проект** в visual Studio 2008 или бесплатно Visual Web Developer 2008 Express.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="5c9c1-111">Откроется диалоговое окно "новый проект".</span><span class="sxs-lookup"><span data-stu-id="5c9c1-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="5c9c1-112">Чтобы создать новое приложение ASP.NET MVC, мы выберем узел "Web" в левой части диалогового окна, а затем выбираем шаблон проекта "веб-приложение ASP.NET MVC" справа:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="5c9c1-113">*Важно! убедитесь, что вы скачали и установили ASP.NET MVC. в противном случае она не будет отображаться в диалоговом окне "новый проект". Вы можете использовать версию 2 [установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx) если вы еще не установили ее (ASP.NET MVC доступен в разделе "веб-платформа — платформы&gt;и среды выполнения").*</span><span class="sxs-lookup"><span data-stu-id="5c9c1-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="5c9c1-114">Мы назовем новый проект, который мы создадим «NerdDinner», и нажмите кнопку «ОК», чтобы создать его.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="5c9c1-115">Если нажать кнопку "ОК", Visual Studio отобразит дополнительное диалоговое окно, предлагающее создать проект модульного теста для нового приложения.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="5c9c1-116">Этот проект модульных тестов позволяет создавать автоматические тесты, которые проверяют функциональность и поведение нашего приложения (что мы будем рассматривать как дальше в этом руководстве).</span><span class="sxs-lookup"><span data-stu-id="5c9c1-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="5c9c1-117">Раскрывающийся список Test Framework (тестовая платформа) в приведенном выше диалоговом окне заполняется всеми доступными шаблонами проектов модульных тестов MVC ASP.NET, установленными на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="5c9c1-118">Версии могут быть скачаны для NUnit, MBUnit и XUnit.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="5c9c1-119">Также поддерживается встроенная платформа модульного тестирования Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="5c9c1-120">*Примечание. Платформа модульного тестирования Visual Studio доступна только в Visual Studio 2008 Professional и более поздних версиях. Если вы используете VS 2008 Standard Edition или Visual Web Developer 2008 Express, для отображения этого диалогового окна необходимо загрузить и установить расширения NUnit, MBUnit или XUnit для ASP.NET MVC. Диалоговое окно не будет отображаться, если не установлены какие-либо платформы тестирования.*</span><span class="sxs-lookup"><span data-stu-id="5c9c1-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="5c9c1-121">Мы будем использовать имя по умолчанию "NerdDinner. Tests" для создаваемого тестового проекта и использовать параметр платформы "модульный тест Visual Studio".</span><span class="sxs-lookup"><span data-stu-id="5c9c1-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="5c9c1-122">При нажатии кнопки "ОК" Visual Studio создаст решение для нас с двумя проектами в нем — один для нашего веб-приложения, а другой — для наших модульных тестов:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="5c9c1-123">Анализ структуры каталогов NerdDinner</span><span class="sxs-lookup"><span data-stu-id="5c9c1-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="5c9c1-124">При создании нового приложения ASP.NET MVC с помощью Visual Studio оно автоматически добавляет в проект несколько файлов и каталогов:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="5c9c1-125">Проекты ASP.NET MVC по умолчанию имеют шесть каталогов верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="5c9c1-126">**Каталог**</span><span class="sxs-lookup"><span data-stu-id="5c9c1-126">**Directory**</span></span> | <span data-ttu-id="5c9c1-127">**Назначение**</span><span class="sxs-lookup"><span data-stu-id="5c9c1-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9c1-128">**/контроллерс**</span><span class="sxs-lookup"><span data-stu-id="5c9c1-128">**/Controllers**</span></span> | <span data-ttu-id="5c9c1-129">Размещение классов контроллеров, обрабатывающих запросы URL-адресов</span><span class="sxs-lookup"><span data-stu-id="5c9c1-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="5c9c1-130">**/моделс**</span><span class="sxs-lookup"><span data-stu-id="5c9c1-130">**/Models**</span></span> | <span data-ttu-id="5c9c1-131">Размещение классов, представляющих данные и манипулирующих ими</span><span class="sxs-lookup"><span data-stu-id="5c9c1-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="5c9c1-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="5c9c1-132">**/Views**</span></span> | <span data-ttu-id="5c9c1-133">Место размещения файлов шаблонов пользовательского интерфейса, отвечающих за отрисовку выходных данных</span><span class="sxs-lookup"><span data-stu-id="5c9c1-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="5c9c1-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="5c9c1-134">**/Scripts**</span></span> | <span data-ttu-id="5c9c1-135">Места размещения файлов библиотек JavaScript и скрипты (.js)</span><span class="sxs-lookup"><span data-stu-id="5c9c1-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="5c9c1-136">**/контент**</span><span class="sxs-lookup"><span data-stu-id="5c9c1-136">**/Content**</span></span> | <span data-ttu-id="5c9c1-137">Место размещения файлов CSS и изображений, а также другого содержимого, не являющегося динамическим или не относящимся к JavaScript</span><span class="sxs-lookup"><span data-stu-id="5c9c1-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="5c9c1-138">**/АПП\_данных**</span><span class="sxs-lookup"><span data-stu-id="5c9c1-138">**/App\_Data**</span></span> | <span data-ttu-id="5c9c1-139">Где хранятся файлы данных, предназначенные для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="5c9c1-140">ASP.NET MVC не требует этой структуры.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="5c9c1-141">На самом деле, разработчики, работающие над крупными приложениями, обычно разделяют приложение на несколько проектов, чтобы сделать его более управляемым (например, классы модели данных часто находятся в отдельном проекте библиотеки классов из веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="5c9c1-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="5c9c1-142">Однако структура проекта по умолчанию предоставляет хорошее соглашение о каталогах по умолчанию, которое можно использовать для очистки наших приложений.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="5c9c1-143">Развернув каталог/Контроллерс, мы найдем, что Visual Studio добавила в проект два класса контроллера — HomeController и AccountController — по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="5c9c1-144">Развернув каталог/views, мы найдем три вложенных каталога:/Home,/Account и/Shared, а также несколько файлов шаблонов в них по умолчанию были добавлены в проект.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="5c9c1-145">Развернув каталоги/контент и/Scripts, мы найдем файл Site. CSS, который используется для стиля всех HTML-документов на сайте, а также библиотеки JavaScript, которые могут включить поддержку ASP.NET AJAX и jQuery в приложении:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="5c9c1-146">Развернув проект NerdDinner. Tests, мы найдем два класса, которые содержат модульные тесты для наших классов контроллеров:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="5c9c1-147">Эти файлы по умолчанию, добавленные Visual Studio, предоставляют нам базовую структуру для рабочего приложения — полный с домашней страницей, страницей входа в систему, выходом из системы и регистрацией, а также необработанной страницей ошибки (все проводные и интерактивные окна).</span><span class="sxs-lookup"><span data-stu-id="5c9c1-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="5c9c1-148">Запуск приложения NerdDinner</span><span class="sxs-lookup"><span data-stu-id="5c9c1-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="5c9c1-149">Чтобы запустить проект, выберите пункт меню **Отладка-&gt;начать отладку** или **отладка —&gt;запуск без отладки** .</span><span class="sxs-lookup"><span data-stu-id="5c9c1-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="5c9c1-150">Это приведет к запуску встроенного веб-сервера ASP.NET, поставляемого вместе с Visual Studio, и запуску нашего приложения:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="5c9c1-151">Ниже приведена Домашняя страница для нашего нового проекта (URL-адрес: "/") при запуске:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="5c9c1-152">При выборе вкладки "о программе" отображается страница "о программе" (URL-адрес: "/Хоме/абаут"):</span><span class="sxs-lookup"><span data-stu-id="5c9c1-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="5c9c1-153">Щелкнув ссылку "вход" в правом верхнем углу, можно перейти на страницу входа (URL-адрес: "/аккаунт/Логон").</span><span class="sxs-lookup"><span data-stu-id="5c9c1-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="5c9c1-154">Если у нас нет учетной записи входа, можно щелкнуть ссылку Register (URL: "/аккаунт/регистер"), чтобы создать ее.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="5c9c1-155">Код, реализующий описанные выше функции Home, About и Logout/Register, был добавлен по умолчанию при создании нового проекта.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="5c9c1-156">Мы будем использовать его в качестве отправной точки нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="5c9c1-157">Тестирование приложения NerdDinner</span><span class="sxs-lookup"><span data-stu-id="5c9c1-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="5c9c1-158">Если используется выпуск Professional или более поздней версии Visual Studio 2008, мы можем использовать встроенную поддержку интегрированной среды разработки модульного тестирования в Visual Studio для тестирования проекта:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="5c9c1-159">Если выбрать один из указанных выше параметров, откроется панель "результаты теста" в интегрированной среде разработки и вы получите состояние "успех/сбой" для 27 модульных тестов, включенных в наш новый проект, охватывающие встроенные функции:</span><span class="sxs-lookup"><span data-stu-id="5c9c1-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="5c9c1-160">Далее в этом учебнике мы поговорим о автоматизированном тестировании и добавим дополнительные модульные тесты, охватывающие реализуемую функциональность приложения.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="5c9c1-161">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="5c9c1-161">Next Step</span></span>

<span data-ttu-id="5c9c1-162">Теперь у нас есть базовая структура приложения.</span><span class="sxs-lookup"><span data-stu-id="5c9c1-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="5c9c1-163">Теперь создадим [базу данных для хранения данных приложения](create-a-database.md).</span><span class="sxs-lookup"><span data-stu-id="5c9c1-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5c9c1-164">[Назад](introducing-the-nerddinner-tutorial.md)
> [Вперед](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="5c9c1-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
