---
uid: single-page-application/overview/templates/hottowel-template
title: Шаблон Hot Товел | Документация Майкрософт
author: madskristensen
description: Шаблон Хоттовел
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467142"
---
# <a name="hot-towel-template"></a><span data-ttu-id="66793-103">Шаблон Hot Towel</span><span class="sxs-lookup"><span data-stu-id="66793-103">Hot Towel template</span></span>

<span data-ttu-id="66793-104">по [Мэдсом Кристенсеном](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="66793-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="66793-105">Шаблон "горячий Товел MVC" написан Джон Папа (</span><span class="sxs-lookup"><span data-stu-id="66793-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="66793-106">Выберите версию для загрузки:</span><span class="sxs-lookup"><span data-stu-id="66793-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="66793-107">Шаблон Товел MVC для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="66793-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="66793-108">Шаблон "горячий Товел MVC" для Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="66793-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="66793-109">Горячий Товел: так как вы не хотите переходить к SPA без участия!</span><span class="sxs-lookup"><span data-stu-id="66793-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>

<span data-ttu-id="66793-110">Хотите создать SPA, но не можете решить, где начать?</span><span class="sxs-lookup"><span data-stu-id="66793-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="66793-111">Используйте горячий Товел и, в секундах, вы получите SPA и все средства, которые должны быть созданы.</span><span class="sxs-lookup"><span data-stu-id="66793-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="66793-112">Горячий Товел создает отличную отправную точку для создания одностраничного приложения (SPA) с помощью ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="66793-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="66793-113">В этом случае вы предоставляете модульную структуру кода, навигацию по представлениям, привязку данных, широкие возможности управления данными, а также простые, но элегантные стили.</span><span class="sxs-lookup"><span data-stu-id="66793-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="66793-114">Горячий Товел предоставляет все необходимое для создания SPA, чтобы вы могли сосредоточиться на своем приложении, а не на связи.</span><span class="sxs-lookup"><span data-stu-id="66793-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="66793-115">Узнайте больше о создании SPA на основе [видеороликов, руководств и Pluralsight курсов Джон Папа (](http://johnpapa.net/spa?vsix).</span><span class="sxs-lookup"><span data-stu-id="66793-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>

## <a name="application-structure"></a><span data-ttu-id="66793-116">Структура приложений</span><span class="sxs-lookup"><span data-stu-id="66793-116">Application Structure</span></span>

<span data-ttu-id="66793-117">Горячий Товел SPA предоставляет папку приложения, в которой содержатся файлы JavaScript и HTML, определяющие приложение.</span><span class="sxs-lookup"><span data-stu-id="66793-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="66793-118">Внутри папки приложения:</span><span class="sxs-lookup"><span data-stu-id="66793-118">Inside the App folder:</span></span>

- <span data-ttu-id="66793-119">Durandal</span><span class="sxs-lookup"><span data-stu-id="66793-119">durandal</span></span>
- <span data-ttu-id="66793-120">services;</span><span class="sxs-lookup"><span data-stu-id="66793-120">services</span></span>
- <span data-ttu-id="66793-121">ViewModels</span><span class="sxs-lookup"><span data-stu-id="66793-121">viewmodels</span></span>
- <span data-ttu-id="66793-122">узел "Представления"</span><span class="sxs-lookup"><span data-stu-id="66793-122">views</span></span>

<span data-ttu-id="66793-123">Папка приложения содержит коллекцию модулей.</span><span class="sxs-lookup"><span data-stu-id="66793-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="66793-124">Эти модули инкапсулируют функциональность и объявляют зависимости от других модулей.</span><span class="sxs-lookup"><span data-stu-id="66793-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="66793-125">Папка Views содержит код HTML для вашего приложения, а папка ViewModels содержит логику представления для представлений (общий шаблон MVVM).</span><span class="sxs-lookup"><span data-stu-id="66793-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="66793-126">Папка Services идеально подходит для размещения любых общих служб, которые могут потребоваться вашему приложению, таких как получение данных HTTP или взаимодействие с локальным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="66793-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="66793-127">Часто несколько ViewModels используются для повторного использования кода из модулей служб.</span><span class="sxs-lookup"><span data-stu-id="66793-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="66793-128">Структура приложения ASP.NET MVC на стороне сервера</span><span class="sxs-lookup"><span data-stu-id="66793-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="66793-129">Горячий Товел построен на знакомой и мощной структуре ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="66793-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="66793-130">Запуск\_приложения</span><span class="sxs-lookup"><span data-stu-id="66793-130">App\_Start</span></span>
- <span data-ttu-id="66793-131">Содержимое</span><span class="sxs-lookup"><span data-stu-id="66793-131">Content</span></span>
- <span data-ttu-id="66793-132">Controllers;</span><span class="sxs-lookup"><span data-stu-id="66793-132">Controllers</span></span>
- <span data-ttu-id="66793-133">Модели</span><span class="sxs-lookup"><span data-stu-id="66793-133">Models</span></span>
- <span data-ttu-id="66793-134">Сценарии</span><span class="sxs-lookup"><span data-stu-id="66793-134">Scripts</span></span>
- <span data-ttu-id="66793-135">Представления</span><span class="sxs-lookup"><span data-stu-id="66793-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="66793-136">Избранные библиотеки</span><span class="sxs-lookup"><span data-stu-id="66793-136">Featured Libraries</span></span>

- <span data-ttu-id="66793-137">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="66793-137">ASP.NET MVC</span></span>
- <span data-ttu-id="66793-138">Веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="66793-138">ASP.NET Web API</span></span>
- <span data-ttu-id="66793-139">Веб-Оптимизация ASP.NET — объединение и минификации</span><span class="sxs-lookup"><span data-stu-id="66793-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="66793-140">Очень просто [. js](http://Breezejs.com) -расширенное управление данными</span><span class="sxs-lookup"><span data-stu-id="66793-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="66793-141">[Durandal. js](http://Durandaljs.com) — Навигация и просмотр структуры</span><span class="sxs-lookup"><span data-stu-id="66793-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="66793-142">[Выколачивание. js](http://Knockoutjs.com) — привязки данных</span><span class="sxs-lookup"><span data-stu-id="66793-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="66793-143">[Требовать. js](http://requirejs.org) -модуль с AMD и оптимизацией</span><span class="sxs-lookup"><span data-stu-id="66793-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="66793-144">Всплывающие окна всплывающих сообщений [. js](http://jpapa.me/c7toastr)</span><span class="sxs-lookup"><span data-stu-id="66793-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="66793-145">[Начальная загрузка Twitter](https://twitter.github.com/bootstrap/) — надежная СТИЛИЗАЦИя CSS</span><span class="sxs-lookup"><span data-stu-id="66793-145">[Twitter Bootstrap](https://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="66793-146">Установка с помощью шаблона горячий Товел SPA в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="66793-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="66793-147">Горячий Товел можно установить как шаблон Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="66793-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="66793-148">Просто щелкните `File` | `New Project` и выберите `ASP.NET MVC 4 Web Application`.</span><span class="sxs-lookup"><span data-stu-id="66793-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="66793-149">Затем выберите шаблон "горячее Товел одностраничное приложение" и выполните команду!</span><span class="sxs-lookup"><span data-stu-id="66793-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="66793-150">Установка с помощью пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="66793-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="66793-151">Горячий Товел также является пакетом NuGet, который дополняет существующий пустой проект ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="66793-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="66793-152">Просто установите с помощью NuGet, а затем запустите.</span><span class="sxs-lookup"><span data-stu-id="66793-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="66793-153">Как выполнить сборку с горячий Товел?</span><span class="sxs-lookup"><span data-stu-id="66793-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="66793-154">Просто начните добавлять код!</span><span class="sxs-lookup"><span data-stu-id="66793-154">Simply start adding code!</span></span>

1. <span data-ttu-id="66793-155">Добавьте собственный код на стороне сервера, предпочтительно Entity Framework и WebAPI (что, в действительности, очень просто с помощью простого. js)</span><span class="sxs-lookup"><span data-stu-id="66793-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="66793-156">Добавление представлений в папку `App/views`</span><span class="sxs-lookup"><span data-stu-id="66793-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="66793-157">Добавление ViewModels в папку `App/viewmodels`</span><span class="sxs-lookup"><span data-stu-id="66793-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="66793-158">Добавление привязок данных HTML и маскирования в новые представления</span><span class="sxs-lookup"><span data-stu-id="66793-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="66793-159">Обновление маршрутов навигации в `shell.js`</span><span class="sxs-lookup"><span data-stu-id="66793-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="66793-160">Пошаговое руководство по HTML/JavaScript</span><span class="sxs-lookup"><span data-stu-id="66793-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="66793-161">Views/Хоттовел/index. cshtml</span><span class="sxs-lookup"><span data-stu-id="66793-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="66793-162">index. cshtml — это начальный маршрут и представление для приложения MVC.</span><span class="sxs-lookup"><span data-stu-id="66793-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="66793-163">Он содержит все стандартные теги META, ссылки CSS и ссылки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="66793-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="66793-164">Текст содержит один `<div>`, где все содержимое (представления) будет помещено при запросе.</span><span class="sxs-lookup"><span data-stu-id="66793-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="66793-165">`@Scripts.Render` использует файл обязательно. js для запуска точки входа для кода приложения, который содержится в файле `main.js`.</span><span class="sxs-lookup"><span data-stu-id="66793-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="66793-166">Экран-заставка показывает, как создать экран-заставку во время загрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="66793-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="66793-167">App/Main. js</span><span class="sxs-lookup"><span data-stu-id="66793-167">App/main.js</span></span>

<span data-ttu-id="66793-168">Файл `main.js` содержит код, который будет выполняться сразу после загрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="66793-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="66793-169">Здесь вы хотите определить маршруты навигации, задать представления запуска и выполнить настройку или начальную загрузку, например подготовка данные вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="66793-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="66793-170">Файл `main.js` определяет несколько модулей Durandal, которые помогут запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="66793-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="66793-171">Инструкция define помогает разрешить зависимости модулей, чтобы они были доступны для функции.</span><span class="sxs-lookup"><span data-stu-id="66793-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="66793-172">Сначала сообщения отладки включены, которые отправляют сообщения о событиях, выполняемых приложением в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="66793-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="66793-173">Код App. Start сообщает Durandal Framework запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="66793-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="66793-174">Соглашения задаются таким образом, что Durandal знает все представления и ViewModels содержатся в одних и тех же именованных папках соответственно.</span><span class="sxs-lookup"><span data-stu-id="66793-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="66793-175">Наконец, `app.setRoot` запускает загрузку `shell` с помощью предопределенной `entrance` анимации.</span><span class="sxs-lookup"><span data-stu-id="66793-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="66793-176">Представления</span><span class="sxs-lookup"><span data-stu-id="66793-176">Views</span></span>

<span data-ttu-id="66793-177">Представления находятся в папке `App/views`.</span><span class="sxs-lookup"><span data-stu-id="66793-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="66793-178">Shell. HTML</span><span class="sxs-lookup"><span data-stu-id="66793-178">shell.html</span></span>

<span data-ttu-id="66793-179">`shell.html` содержит основной макет для HTML-кода.</span><span class="sxs-lookup"><span data-stu-id="66793-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="66793-180">Все остальные представления будут содержаться в любом месте в представлении `shell`.</span><span class="sxs-lookup"><span data-stu-id="66793-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="66793-181">Горячий Товел предоставляет `shell` с тремя такими регионами: заголовок, область содержимого и нижний колонтитул.</span><span class="sxs-lookup"><span data-stu-id="66793-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="66793-182">Каждый из этих регионов загружается вместе с содержимым в другие представления по запросу.</span><span class="sxs-lookup"><span data-stu-id="66793-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="66793-183">Привязки `compose` для верхнего и нижнего колонтитулов жестко закодированы в горячий Товел, чтобы они указывали на `nav` и `footer` представления соответственно.</span><span class="sxs-lookup"><span data-stu-id="66793-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="66793-184">Привязка создания для раздела `#content` привязана к активному элементу модуля `router`.</span><span class="sxs-lookup"><span data-stu-id="66793-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="66793-185">Иными словами, при щелчке ссылки навигации в этой области загружается соответствующее представление.</span><span class="sxs-lookup"><span data-stu-id="66793-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="66793-186">NAV. HTML</span><span class="sxs-lookup"><span data-stu-id="66793-186">nav.html</span></span>

<span data-ttu-id="66793-187">`nav.html` содержит ссылки навигации для SPA.</span><span class="sxs-lookup"><span data-stu-id="66793-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="66793-188">В этом случае можно разместить структуру меню, например.</span><span class="sxs-lookup"><span data-stu-id="66793-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="66793-189">Часто это происходит с привязкой данных (с использованием маскирования) к модулю `router` для просмотра навигации, определенной в `shell.js`.</span><span class="sxs-lookup"><span data-stu-id="66793-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="66793-190">Выколачивание ищет атрибуты привязки данных и привязывает их к `shell` ViewModel для отображения маршрутов навигации и отображения ProgressBar (с помощью начальной загрузки Twitter), если модуль `router` находится в процессе перехода от одного представления к другому (см. `router.isNavigating`).</span><span class="sxs-lookup"><span data-stu-id="66793-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="66793-191">Home. HTML и Details. HTML</span><span class="sxs-lookup"><span data-stu-id="66793-191">home.html and details.html</span></span>

<span data-ttu-id="66793-192">Эти представления содержат HTML для пользовательских представлений.</span><span class="sxs-lookup"><span data-stu-id="66793-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="66793-193">При нажатии ссылки `home` в меню представления `nav` представление `home` будет помещено в область содержимого представления `shell`.</span><span class="sxs-lookup"><span data-stu-id="66793-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="66793-194">Эти представления можно дополнить или заменить собственными пользовательскими представлениями.</span><span class="sxs-lookup"><span data-stu-id="66793-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="66793-195">Нижний колонтитул. HTML</span><span class="sxs-lookup"><span data-stu-id="66793-195">footer.html</span></span>

<span data-ttu-id="66793-196">`footer.html` содержит HTML-код, отображаемый в нижнем колонтитуле в нижней части представления `shell`.</span><span class="sxs-lookup"><span data-stu-id="66793-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="66793-197">Модели представлений</span><span class="sxs-lookup"><span data-stu-id="66793-197">ViewModels</span></span>

<span data-ttu-id="66793-198">ViewModels находятся в папке `App/viewmodels`.</span><span class="sxs-lookup"><span data-stu-id="66793-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="66793-199">Shell. js</span><span class="sxs-lookup"><span data-stu-id="66793-199">shell.js</span></span>

<span data-ttu-id="66793-200">`shell` ViewModel содержит свойства и функции, привязанные к представлению `shell`.</span><span class="sxs-lookup"><span data-stu-id="66793-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="66793-201">Часто это место, где обнаруживаются привязки навигации по меню (см. логику `router.mapNav`).</span><span class="sxs-lookup"><span data-stu-id="66793-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="66793-202">Home. js и Details. js</span><span class="sxs-lookup"><span data-stu-id="66793-202">home.js and details.js</span></span>

<span data-ttu-id="66793-203">Эти классы ViewModel содержат свойства и функции, привязанные к `home`ному представлению.</span><span class="sxs-lookup"><span data-stu-id="66793-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="66793-204">Он также содержит логику представления для представления и является связующим представлением между данными и представлением.</span><span class="sxs-lookup"><span data-stu-id="66793-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="66793-205">Службы</span><span class="sxs-lookup"><span data-stu-id="66793-205">Services</span></span>

<span data-ttu-id="66793-206">Службы находятся в папке App/Services.</span><span class="sxs-lookup"><span data-stu-id="66793-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="66793-207">В идеале для будущих служб, таких как модуль службы данных, который отвечает за получение и публикацию удаленных данных, может быть размещен.</span><span class="sxs-lookup"><span data-stu-id="66793-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="66793-208">Logger. js</span><span class="sxs-lookup"><span data-stu-id="66793-208">logger.js</span></span>

<span data-ttu-id="66793-209">Горячий Товел предоставляет модуль `logger` в папке "службы".</span><span class="sxs-lookup"><span data-stu-id="66793-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="66793-210">Модуль `logger` идеально подходит для ведения журнала сообщений в консоли и для пользователя во всплывающих уведомлениях.</span><span class="sxs-lookup"><span data-stu-id="66793-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
