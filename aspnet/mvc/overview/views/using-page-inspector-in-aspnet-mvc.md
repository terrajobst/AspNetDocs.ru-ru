---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: Использование Инспектор страниц в ASP.NET MVC | Документация Майкрософт
author: rick-anderson
description: Инспектор страниц в Visual Studio 2012 — это средство веб-разработки с интегрированным браузером. Выберите любой элемент в интегрированном браузере и Инспектор страниц i...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432456"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="9175c-104">Использование инспектора страниц в ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="9175c-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="9175c-105">по Тим Амманн</span><span class="sxs-lookup"><span data-stu-id="9175c-105">by Tim Ammann</span></span>

> <span data-ttu-id="9175c-106">Инспектор страниц в Visual Studio 2012 — это средство веб-разработки с интегрированным браузером.</span><span class="sxs-lookup"><span data-stu-id="9175c-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="9175c-107">Выберите любой элемент в интегрированном браузере, и Инспектор страниц мгновенно заподсвечивает источник элемента и CSS.</span><span class="sxs-lookup"><span data-stu-id="9175c-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="9175c-108">Можно просматривать любое представление MVC, быстро находить источники отображаемой разметки и использовать средства браузера непосредственно в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9175c-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="9175c-109">Просмотр видео</span><span class="sxs-lookup"><span data-stu-id="9175c-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="9175c-110">В этом руководстве показано, как включить режим проверки, а затем быстро находить и редактировать разметку и CSS в веб-проекте.</span><span class="sxs-lookup"><span data-stu-id="9175c-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="9175c-111">В этом руководстве используется проект MVC, но можно также использовать Инспектор страниц для [веб-форм](https://go.microsoft.com/?linkid=9802001) и других приложений ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9175c-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="9175c-112">Учебник содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="9175c-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="9175c-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9175c-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="9175c-114">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9175c-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="9175c-115">Использование Инспектор страниц для перехода к представлению</span><span class="sxs-lookup"><span data-stu-id="9175c-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="9175c-116">Включить режим проверки</span><span class="sxs-lookup"><span data-stu-id="9175c-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="9175c-117">Использование Инспектор страниц для внесения изменений в разметку</span><span class="sxs-lookup"><span data-stu-id="9175c-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="9175c-118">режим проверки и окно HTML</span><span class="sxs-lookup"><span data-stu-id="9175c-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - [<span data-ttu-id="9175c-119">Предварительный просмотр изменений CSS в окне "стили"</span><span class="sxs-lookup"><span data-stu-id="9175c-119">Preview CSS Changes in the Styles window</span></span>](#_7_previewing_css)
> - [<span data-ttu-id="9175c-120">Автоматическая синхронизация CSS</span><span class="sxs-lookup"><span data-stu-id="9175c-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="9175c-121">Использование выбора цвета CSS</span><span class="sxs-lookup"><span data-stu-id="9175c-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="9175c-122">Сопоставление динамических элементов страницы с JavaScript</span><span class="sxs-lookup"><span data-stu-id="9175c-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="9175c-123">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9175c-123">Prerequisites</span></span>

- <span data-ttu-id="9175c-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) или [Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="9175c-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="9175c-125">Чтобы получить последнюю версию Инспектор страниц, используйте [установщик веб-платформы](https://go.microsoft.com/fwlink/?LinkId=255386) для установки пакета Windows Azure SDK для .NET 2,0.</span><span class="sxs-lookup"><span data-stu-id="9175c-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="9175c-126">Инспектор страниц входит в состав инструменты разработчика Microsoft Web.</span><span class="sxs-lookup"><span data-stu-id="9175c-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="9175c-127">Последняя версия — 1,3.</span><span class="sxs-lookup"><span data-stu-id="9175c-127">The latest version is 1.3.</span></span> <span data-ttu-id="9175c-128">Чтобы проверить, какая версия установлена, запустите Visual Studio и выберите **о Microsoft Visual Studio** в меню " **Справка** ".</span><span class="sxs-lookup"><span data-stu-id="9175c-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="9175c-129">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9175c-129">Create a Web Application</span></span>

<span data-ttu-id="9175c-130">Сначала создайте веб-приложение, которое будет использоваться Инспектор страниц с.</span><span class="sxs-lookup"><span data-stu-id="9175c-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="9175c-131">В Visual Studio выберите **файл** &gt; **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="9175c-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="9175c-132">В левой части разверните узел **визуальный C#** элемент, выберите **веб**, а затем выберите **ASP.NET MVC4 веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="9175c-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![Новое приложение ASP.NET MVC](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="9175c-134">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9175c-134">Click **OK**.</span></span>

<span data-ttu-id="9175c-135">В диалоговом окне **Новый проект ASP.NET MVC 4** выберите **Интернет приложение**.</span><span class="sxs-lookup"><span data-stu-id="9175c-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="9175c-136">Оставьте **Razor** в качестве подсистемы представления по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9175c-136">Leave **Razor** as the default view engine.</span></span>

![Новый проект MVC ASP.NET — Интернет-приложение](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="9175c-138">Приложение откроется в представлении **исходного кода** .</span><span class="sxs-lookup"><span data-stu-id="9175c-138">The application opens in **Source** view.</span></span>

![Новое приложение ASP.NET MVC в представлении исходного кода](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="9175c-140">Теперь, когда у вас есть приложение для работы с, можно использовать Инспектор страниц для его анализа и изменения.</span><span class="sxs-lookup"><span data-stu-id="9175c-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="9175c-141">Использование Инспектор страниц для перехода к представлению</span><span class="sxs-lookup"><span data-stu-id="9175c-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="9175c-142">В Visual Studio 2012 можно щелкнуть правой кнопкой мыши любое представление проекта, выбрать пункт **Просмотреть в инспектор страниц**, а инспектор страниц будет вычислить маршрут и отобразить страницу.</span><span class="sxs-lookup"><span data-stu-id="9175c-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="9175c-143">В **Обозреватель решений**разверните папку **представления** , а затем — **корневую** папку.</span><span class="sxs-lookup"><span data-stu-id="9175c-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="9175c-144">Щелкните правой кнопкой мыши файл index. cshtml и выберите пункт **Просмотреть в инспектор страниц**.</span><span class="sxs-lookup"><span data-stu-id="9175c-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![Просмотр index. cshtml в Инспектор страниц](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="9175c-146">По умолчанию Инспектор страниц закрепляется как окно в левой части среды Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9175c-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="9175c-147">При желании вы можете закрепить его в любом расположении или отстыковать окно.</span><span class="sxs-lookup"><span data-stu-id="9175c-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="9175c-148">См. раздел [как упорядочивать и закреплять окна](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span><span class="sxs-lookup"><span data-stu-id="9175c-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="9175c-149">В верхней области окна Инспектор страниц отображается текущая страница в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="9175c-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="9175c-150">На нижней панели отображается страница в разметке HTML, а также некоторые вкладки, позволяющие проверять различные аспекты страницы.</span><span class="sxs-lookup"><span data-stu-id="9175c-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="9175c-151">Нижняя панель аналогична [средства для разработчикову F12](https://msdn.microsoft.com/ie/aa740478) в Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9175c-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![Приложение ASP.NET MVC в Инспектор страниц](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="9175c-153">В этом учебнике вы будете использовать вкладки **HTML** и **стили** для быстрой навигации и внесения изменений в приложение.</span><span class="sxs-lookup"><span data-stu-id="9175c-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="9175c-154">Режим Енаблеинспектион</span><span class="sxs-lookup"><span data-stu-id="9175c-154">EnableInspection Mode</span></span>

<span data-ttu-id="9175c-155">Чтобы вставить Инспектор страниц в режим проверки, нажмите кнопку **проверить** .</span><span class="sxs-lookup"><span data-stu-id="9175c-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="9175c-156">В режим проверки при наведении указателя мыши на любую часть отображаемой страницы выделяется соответствующая исходная разметка или код.</span><span class="sxs-lookup"><span data-stu-id="9175c-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![Переключить режим проверки](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="9175c-158">Теперь наведите указатель мыши на различные части страницы в Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="9175c-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="9175c-159">При этом указатель мыши превращается в большой знак «плюс», и элемент под ним выделяется.</span><span class="sxs-lookup"><span data-stu-id="9175c-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Наведение указателя мыши на div. Content-упаковщик](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="9175c-161">При перемещении указателя мыши Visual Studio выделяет соответствующие синтаксис Razor в исходном файле.</span><span class="sxs-lookup"><span data-stu-id="9175c-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="9175c-162">Если элемент HTML поступает из другого исходного файла, Visual Studio автоматически открывает этот файл.</span><span class="sxs-lookup"><span data-stu-id="9175c-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="9175c-163">В Инспектор страниц на вкладке **HTML** отображается HTML-код, созданный из синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="9175c-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="9175c-164">При перемещении указателя мыши элементы HTML выделяются.</span><span class="sxs-lookup"><span data-stu-id="9175c-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="9175c-165">На вкладке **стили** ОТОБРАЖАЮТСЯ правила CSS для элемента.</span><span class="sxs-lookup"><span data-stu-id="9175c-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="9175c-166">Использование Инспектор страниц для внесения изменений в разметку</span><span class="sxs-lookup"><span data-stu-id="9175c-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="9175c-167">Инспектор страниц позволяет найти разметку, расположение которой может быть неочевидным.</span><span class="sxs-lookup"><span data-stu-id="9175c-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="9175c-168">Затем можно изменить разметку и просмотреть итоговые изменения.</span><span class="sxs-lookup"><span data-stu-id="9175c-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="9175c-169">Чтобы увидеть это, щелкните **проверить** и прокрутите страницу вниз до нижней части страницы инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="9175c-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="9175c-170">При перемещении указателя мыши в область нижнего колонтитула Инспектор страниц открывает файл \_Layout. cshtml и выделяет раздел выбранной страницы макета.</span><span class="sxs-lookup"><span data-stu-id="9175c-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="9175c-171">Как видите, нижний колонтитул определяется в файле макета, а не в самом представлении.</span><span class="sxs-lookup"><span data-stu-id="9175c-171">As you can see, the footer are is defined in the layout file, and not the view itself.</span></span>

![Нижний колонтитул](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="9175c-173">Теперь наведите указатель мыши на строку с уведомлением об <a id="a"> </a>авторских правах.</span><span class="sxs-lookup"><span data-stu-id="9175c-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="9175c-174">На странице \_Layout. cshtml выделена соответствующая строка.</span><span class="sxs-lookup"><span data-stu-id="9175c-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![Выделенная строка авторских прав нижнего колонтитула](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="9175c-176">Добавьте текст в конец строки в файле \_Layout. cshtml.</span><span class="sxs-lookup"><span data-stu-id="9175c-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="9175c-177">&lt;p&gt;&amp;Copy; @DateTime.Now.Year-мой ASP.NET приложение MVC Rocks!&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="9175c-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="9175c-178">Теперь нажмите клавиши CTRL + ALT + ВВОД или щелкните панель обновления, чтобы просмотреть результаты в окне браузера Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="9175c-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![Мой ASP.NET приложение Rocks!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="9175c-180">Возможно, вы думали, что нижний колонтитул, определенный в index. cshtml, но он был в \_Layout. cshtml, и Инспектор страниц нашел его.</span><span class="sxs-lookup"><span data-stu-id="9175c-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="9175c-181">режим проверки и окно HTML</span><span class="sxs-lookup"><span data-stu-id="9175c-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="9175c-182">Теперь вы сможете быстро взглянуть на окно HTML и то, как оно сопоставляет элементы.</span><span class="sxs-lookup"><span data-stu-id="9175c-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="9175c-183">Нажмите кнопку **проверить** , чтобы перевести Инспектор страниц в режим проверки.</span><span class="sxs-lookup"><span data-stu-id="9175c-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="9175c-184">Щелкните верхнюю часть страницы с текстом "Ваша Эмблема".</span><span class="sxs-lookup"><span data-stu-id="9175c-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="9175c-185">Вы проведете анализ определенного элемента более подробно, поэтому отображение в окне браузера больше не изменяется при перемещении указателя мыши.</span><span class="sxs-lookup"><span data-stu-id="9175c-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="9175c-186">Теперь наведите указатель мыши на окно **HTML** .</span><span class="sxs-lookup"><span data-stu-id="9175c-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="9175c-187">При перемещении указателя мыши Инспектор страниц отображает элемент в окне **HTML** и выделяет соответствующий элемент в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="9175c-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![Окно HTML](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="9175c-189">Как и ранее, Инспектор страниц откроет файл \_Layout. cshtml на временной вкладке. Щелкните вкладку \_Layout. cshtml временная, и соответствующая разметка будет выделена в разделе&gt; заголовка &lt;.</span><span class="sxs-lookup"><span data-stu-id="9175c-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![Выделенная разметка](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="9175c-191">Предварительный просмотр изменений CSS в окне "стили"</span><span class="sxs-lookup"><span data-stu-id="9175c-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="9175c-192">Далее вы будете использовать окно **стили** инспектор страниц для предварительного просмотра изменений в CSS.</span><span class="sxs-lookup"><span data-stu-id="9175c-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="9175c-193">Нажмите кнопку **проверить** , чтобы перевести Инспектор страниц в режим проверки.</span><span class="sxs-lookup"><span data-stu-id="9175c-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="9175c-194">В окне браузера Инспектор страниц наведите указатель мыши на раздел "Домашняя страница", пока не появится метка **div. Content-упаковщик** .</span><span class="sxs-lookup"><span data-stu-id="9175c-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Наведение указателя мыши на div. Content-упаковщик](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="9175c-196">Щелкните один раз в разделе div. Content-оберток, а затем переместите указатель мыши в окно **стили** .</span><span class="sxs-lookup"><span data-stu-id="9175c-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="9175c-197">В окне **стили** отображаются все правила CSS для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="9175c-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="9175c-198">Прокрутите вниз, чтобы найти селектор класса. Избранное. Content-оберток.</span><span class="sxs-lookup"><span data-stu-id="9175c-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="9175c-199">Теперь снимите флажок для свойства цвет фона.</span><span class="sxs-lookup"><span data-stu-id="9175c-199">Now clear the checkbox for the background-color property.</span></span>

![Очистить цвет фона](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="9175c-201">Обратите внимание на то, как мгновенно просмотреть изменения в окне браузера Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="9175c-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="9175c-202">Снова установите флажок, затем дважды щелкните значение свойства и измените его на красный.</span><span class="sxs-lookup"><span data-stu-id="9175c-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="9175c-203">Это изменение показано немедленно:</span><span class="sxs-lookup"><span data-stu-id="9175c-203">The change shows immediately:</span></span>

![Красный цвет фона](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="9175c-205">Окно **стили** упрощает тестирование и предварительный просмотр изменений в CSS перед фиксацией изменений в самой таблице стилей.</span><span class="sxs-lookup"><span data-stu-id="9175c-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="9175c-206">Автоматическая синхронизация CSS</span><span class="sxs-lookup"><span data-stu-id="9175c-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="9175c-207">Для этой функции требуется версия 1,3 Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="9175c-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="9175c-208">Функция автоматической синхронизации CSS позволяет непосредственно редактировать CSS-файл и немедленно просматривать изменения в обозревателе Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="9175c-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="9175c-209">Нажмите кнопку **проверить** , чтобы перевести Инспектор страниц в режим проверки.</span><span class="sxs-lookup"><span data-stu-id="9175c-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="9175c-210">В браузере Инспектор страниц наведите указатель мыши на раздел "Домашняя страница", пока не появится метка **div. Content-упаковщик** .</span><span class="sxs-lookup"><span data-stu-id="9175c-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="9175c-211">Щелкните один раз, чтобы выбрать этот элемент.</span><span class="sxs-lookup"><span data-stu-id="9175c-211">Click once to select this element.</span></span>

<span data-ttu-id="9175c-212">В окне **стили** отображаются все правила CSS для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="9175c-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="9175c-213">Прокрутите вниз, чтобы найти селектор класса. Избранное. Content-оберток.</span><span class="sxs-lookup"><span data-stu-id="9175c-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="9175c-214">Щелкните ". Избранное. Content-упаковщик".</span><span class="sxs-lookup"><span data-stu-id="9175c-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="9175c-215">Инспектор страниц открывает CSS-файл, который определяет этот стиль (site. CSS) и выделяет соответствующий стиль CSS.</span><span class="sxs-lookup"><span data-stu-id="9175c-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="9175c-216">Теперь измените значение `background-color` на "Red".</span><span class="sxs-lookup"><span data-stu-id="9175c-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="9175c-217">Это изменение отображается сразу в Инспектор страниц браузере.</span><span class="sxs-lookup"><span data-stu-id="9175c-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="9175c-218">Использование выбора цвета CSS</span><span class="sxs-lookup"><span data-stu-id="9175c-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="9175c-219">Редактор CSS в Visual Studio 2012 имеет палитру цветов, которая позволяет легко выбирать и вставлять цвета.</span><span class="sxs-lookup"><span data-stu-id="9175c-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="9175c-220">Палитра цветов включает стандартную палитру цветов, поддерживает стандартные имена цветов, хэш-коды, RGB, RGBA, HSL и ХСЛА, а также поддерживает список цветов, использовавшихся в документе последними.</span><span class="sxs-lookup"><span data-stu-id="9175c-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="9175c-221">В предыдущем разделе вы изменили значение свойства `background-color`.</span><span class="sxs-lookup"><span data-stu-id="9175c-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="9175c-222">Чтобы вызвать палитру цветов, поместите точку вставки после имени свойства и введите **#** или **RGB (** .</span><span class="sxs-lookup"><span data-stu-id="9175c-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![Панель выбора цвета CSS](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="9175c-224">Щелкните цвет, чтобы выбрать его, или нажмите клавишу со стрелкой вниз, а затем используйте клавиши со стрелками влево и вправо для перемещения цветов.</span><span class="sxs-lookup"><span data-stu-id="9175c-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="9175c-225">При посещении цвета соответствующее шестнадцатеричное значение будет предварительно просмотрено:</span><span class="sxs-lookup"><span data-stu-id="9175c-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![Предварительный просмотр значения свойства цвета фона](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="9175c-227">Если цветовая шкала не имеет нужного цвета, можно использовать всплывающее окно палитры цветов.</span><span class="sxs-lookup"><span data-stu-id="9175c-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="9175c-228">Чтобы открыть его, щелкните значок шеврона в правой части цветовой шкалы или нажмите стрелку вниз один или два раза на клавиатуре.</span><span class="sxs-lookup"><span data-stu-id="9175c-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![Всплывающее окно выбора цвета CSS](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="9175c-230">Щелкните цвет на вертикальной панели справа.</span><span class="sxs-lookup"><span data-stu-id="9175c-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="9175c-231">Он показывает градиент для этого цвета в главном окне.</span><span class="sxs-lookup"><span data-stu-id="9175c-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="9175c-232">Выберите цвет непосредственно из вертикальной линии, нажав клавишу ВВОД, или щелкните любую точку в главном окне, чтобы выбрать с большей точностью.</span><span class="sxs-lookup"><span data-stu-id="9175c-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="9175c-233">Если на экране компьютера есть цвет, который вы хотите использовать (он не должен находиться в пользовательском интерфейсе Visual Studio), его значение можно записать с помощью инструмента "Пипетка" в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="9175c-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="9175c-234">Можно также изменить прозрачность цвета, переместив ползунок в нижней части палитры цветов.</span><span class="sxs-lookup"><span data-stu-id="9175c-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="9175c-235">При этом значения цвета изменяются на значения RGBA, так как формат RGBA может представлять непрозрачность.</span><span class="sxs-lookup"><span data-stu-id="9175c-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="9175c-236">После выбора цвета нажмите клавишу ВВОД, а затем введите точку с запятой, чтобы завершить запись в фоновом режиме в файле *site. CSS* .</span><span class="sxs-lookup"><span data-stu-id="9175c-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="9175c-237">Панель обновления Инспектор страниц</span><span class="sxs-lookup"><span data-stu-id="9175c-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="9175c-238">Инспектор страниц немедленно обнаруживает изменения в файле *site. CSS* и отображает оповещение на панели обновления.</span><span class="sxs-lookup"><span data-stu-id="9175c-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![Обновить панель](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="9175c-240">Чтобы сохранить все файлы и обновить обозреватель Инспектор страниц, нажмите клавиши CTRL + ALT + ВВОД или щелкните панель обновления.</span><span class="sxs-lookup"><span data-stu-id="9175c-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="9175c-241">Изменение цвета выделения отображается в браузере.</span><span class="sxs-lookup"><span data-stu-id="9175c-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="9175c-242">Сопоставление динамических элементов страницы с JavaScript</span><span class="sxs-lookup"><span data-stu-id="9175c-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="9175c-243">В современных веб-приложениях элементы страницы часто создаются динамически с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9175c-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="9175c-244">Это означает, что отсутствует статическая разметка (HTML или Razor), соответствующая этим элементам страницы.</span><span class="sxs-lookup"><span data-stu-id="9175c-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="9175c-245">В версии 1,3 Инспектор страниц теперь можно сопоставлять элементы, динамически добавленные на страницу, в соответствующий код JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9175c-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="9175c-246">Чтобы продемонстрировать эту функцию, мы будем использовать [шаблон одностраничного приложения (SPA)](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span><span class="sxs-lookup"><span data-stu-id="9175c-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9175c-247">Для шаблона SPA требуется обновление [ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650) .</span><span class="sxs-lookup"><span data-stu-id="9175c-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="9175c-248">В Visual Studio выберите **файл** &gt; **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="9175c-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="9175c-249">В левой части разверните узел **визуальный C#** элемент, выберите **веб**, а затем выберите **ASP.NET MVC4 веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="9175c-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="9175c-250">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9175c-250">Click **OK**.</span></span>

<span data-ttu-id="9175c-251">В диалоговом окне **Новый проект ASP.NET MVC 4** выберите **одностраничное приложение**.</span><span class="sxs-lookup"><span data-stu-id="9175c-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="9175c-252">В обозреватель решений разверните папку **представления** , а затем — **корневую** папку.</span><span class="sxs-lookup"><span data-stu-id="9175c-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="9175c-253">Щелкните правой кнопкой мыши файл index. cshtml и выберите пункт **Просмотреть в инспектор страниц**.</span><span class="sxs-lookup"><span data-stu-id="9175c-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="9175c-254">Первое, что отображается в Инспектор страниц браузере, является страницей входа.</span><span class="sxs-lookup"><span data-stu-id="9175c-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="9175c-255">Щелкните "зарегистрироваться" и создайте имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="9175c-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="9175c-256">После регистрации приложение войдет в систему и создаст список задач с примерами элементов.</span><span class="sxs-lookup"><span data-stu-id="9175c-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="9175c-257">Нажмите кнопку **проверить** , чтобы перевести Инспектор страниц в режим проверки.</span><span class="sxs-lookup"><span data-stu-id="9175c-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="9175c-258">В браузере Инспектор страниц щелкните один из элементов задач.</span><span class="sxs-lookup"><span data-stu-id="9175c-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="9175c-259">Обратите внимание, что вместо того, чтобы выделять синим цветом, элемент выделяется оранжевым цветом, а "JS" — рядом с именем элемента.</span><span class="sxs-lookup"><span data-stu-id="9175c-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="9175c-260">Это означает, что элемент был создан динамически с помощью скрипта.</span><span class="sxs-lookup"><span data-stu-id="9175c-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="9175c-261">Кроме того, на вкладке **Стек вызовов** появляется оранжевый подчеркивание. Это означает, что область **стека вызовов** содержит дополнительные сведения об элементе.</span><span class="sxs-lookup"><span data-stu-id="9175c-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="9175c-262">Перейдите на вкладку **Стек вызовов** . На панели **Стек вызовов** отображается стек вызовов для вызова JavaScript, который создал элемент.</span><span class="sxs-lookup"><span data-stu-id="9175c-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="9175c-263">Вызовы внешних библиотек, таких как jQuery, свернуты, что позволяет легко просматривать вызовы скрипта приложения.</span><span class="sxs-lookup"><span data-stu-id="9175c-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="9175c-264">Чтобы просмотреть полный стек, включая вызовы внешних библиотек, можно развернуть узлы с меткой "внешние библиотеки":</span><span class="sxs-lookup"><span data-stu-id="9175c-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="9175c-265">Если щелкнуть элемент в стеке вызовов, Visual Studio откроет файл кода и выполнит выделение соответствующего скрипта.</span><span class="sxs-lookup"><span data-stu-id="9175c-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="9175c-266">См. также:</span><span class="sxs-lookup"><span data-stu-id="9175c-266">See Also</span></span>

<span data-ttu-id="9175c-267">[Введение в ASP.NET MVC 4 с Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (веб-сайт ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9175c-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="9175c-268">[Знакомство с инспектор страниц](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (видео на канале 9)</span><span class="sxs-lookup"><span data-stu-id="9175c-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="9175c-269">[Инспектор страниц сообщения об ошибках](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="9175c-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
