---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: Использование Инспектор страниц для Visual Studio 2012 в веб-формах ASP.NET | Документация Майкрософт
author: rick-anderson
description: Инспектор страниц для Visual Studio 2012 — это средство веб-разработки с интегрированным браузером. Выберите любой элемент в интегрированном браузере и Инспектор страниц...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464946"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="a0e84-104">Использование инспектора страниц для Visual Studio 2012 в веб-формах ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a0e84-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>

<span data-ttu-id="a0e84-105">по Тим Амманн</span><span class="sxs-lookup"><span data-stu-id="a0e84-105">by Tim Ammann</span></span>

> <span data-ttu-id="a0e84-106">Инспектор страниц для Visual Studio 2012 — это средство веб-разработки с интегрированным браузером.</span><span class="sxs-lookup"><span data-stu-id="a0e84-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="a0e84-107">Выберите любой элемент в интегрированном браузере, и Инспектор страниц мгновенно заподсвечивает источник элемента и CSS.</span><span class="sxs-lookup"><span data-stu-id="a0e84-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="a0e84-108">Можно просматривать любую страницу в приложении, быстро находить источники отображаемой разметки и использовать средства браузера непосредственно в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0e84-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="a0e84-109">В этом учебнике показано, как включить режим проверки, а затем быстро находить и редактировать правила CSS и текст в веб-проекте.</span><span class="sxs-lookup"><span data-stu-id="a0e84-109">This tutorial shows how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="a0e84-110">В этом учебнике используется проект приложения Web Forms, но можно также использовать Инспектор страниц для проектов веб-сайтов и приложений [MVC](https://go.microsoft.com/?linkid=9802002) .</span><span class="sxs-lookup"><span data-stu-id="a0e84-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="a0e84-111">Учебник содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="a0e84-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="a0e84-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a0e84-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="a0e84-113">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a0e84-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="a0e84-114">Использование Инспектор страниц для просмотра приложения</span><span class="sxs-lookup"><span data-stu-id="a0e84-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="a0e84-115">Включить режим проверки</span><span class="sxs-lookup"><span data-stu-id="a0e84-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="a0e84-116">Использование Инспектор страниц для внесения изменений в разметку</span><span class="sxs-lookup"><span data-stu-id="a0e84-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="a0e84-117">режим проверки и окно HTML</span><span class="sxs-lookup"><span data-stu-id="a0e84-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> [<span data-ttu-id="a0e84-118">Предварительный просмотр изменений CSS в окне "стили"</span><span class="sxs-lookup"><span data-stu-id="a0e84-118">Preview CSS Changes in the Styles Window</span></span>](#_7_previewing_css)
> 
> [<span data-ttu-id="a0e84-119">Автоматическая синхронизация CSS</span><span class="sxs-lookup"><span data-stu-id="a0e84-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="a0e84-120">Использование выбора цвета CSS</span><span class="sxs-lookup"><span data-stu-id="a0e84-120">Using the CSS Color Picker</span></span>](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="a0e84-121">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a0e84-121">Prerequisites</span></span>

- <span data-ttu-id="a0e84-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) или [Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="a0e84-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="a0e84-123">Чтобы получить последнюю версию Инспектор страниц, используйте [установщик веб-платформы](https://go.microsoft.com/fwlink/?LinkId=255386) для установки пакета Azure SDK для .NET 2,0.</span><span class="sxs-lookup"><span data-stu-id="a0e84-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="a0e84-124">Инспектор страниц входит в состав инструменты разработчика Microsoft Web.</span><span class="sxs-lookup"><span data-stu-id="a0e84-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="a0e84-125">Последняя версия — 1,3.</span><span class="sxs-lookup"><span data-stu-id="a0e84-125">The latest version is 1.3.</span></span> <span data-ttu-id="a0e84-126">Чтобы проверить, какая версия установлена, запустите Visual Studio и выберите **о Microsoft Visual Studio** в меню " **Справка** ".</span><span class="sxs-lookup"><span data-stu-id="a0e84-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="a0e84-127">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a0e84-127">Create a Web Application</span></span>

<span data-ttu-id="a0e84-128">Сначала необходимо создать веб-приложение, которое будет использоваться Инспектор страниц с.</span><span class="sxs-lookup"><span data-stu-id="a0e84-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="a0e84-129">В Visual Studio выберите **файл** &gt; **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="a0e84-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="a0e84-130">В левой части разверните узел **визуальный C#** элемент, выберите **веб**, а затем выберите **приложение ASP.NET Web Forms**.</span><span class="sxs-lookup"><span data-stu-id="a0e84-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![Новое приложение веб-форм](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="a0e84-132">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a0e84-132">Click **OK**.</span></span>

<span data-ttu-id="a0e84-133">Приложение откроется в представлении **исходного кода** .</span><span class="sxs-lookup"><span data-stu-id="a0e84-133">The application opens in **Source** view.</span></span>

![Новое приложение Web Forms в представлении исходного кода](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="a0e84-135">Теперь, когда у вас есть приложение для работы с, можно использовать Инспектор страниц для его анализа и изменения.</span><span class="sxs-lookup"><span data-stu-id="a0e84-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="a0e84-136">Использование Инспектор страниц для просмотра приложения</span><span class="sxs-lookup"><span data-stu-id="a0e84-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="a0e84-137">Теперь приложение будет просматриваться с Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="a0e84-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="a0e84-138">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите пункт **Просмотреть в инспектор страниц**.</span><span class="sxs-lookup"><span data-stu-id="a0e84-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![Просмотреть в инспекторе страниц](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="a0e84-140">По умолчанию при первом запуске Инспектор страниц он закрепляется в виде узких окон в левой части среды Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0e84-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="a0e84-141">Оставьте закрепленный с левой стороны и задайте для него ширину, удобную для вас, или закрепите ее в одной из областей, расположенных в верхней, нижней или правой части окна.</span><span class="sxs-lookup"><span data-stu-id="a0e84-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![Инспектор страниц позиции закрепления](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="a0e84-143">Если вы открепите Инспектор страниц окно, его можно поместить за пределы Visual Studio или даже на втором мониторе, если таковой имеется.</span><span class="sxs-lookup"><span data-stu-id="a0e84-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="a0e84-144">Однако, чтобы ALT + TAB между Инспектор страниц и Visual Studio, когда Инспектор страниц окно не закреплено, последовательно выберите пункты **сервис** &gt; **параметры** &gt; **Среда** &gt; **вкладки и окна**, а **также**снимите флажок **плавающие окна инструментов всегда находятся поверх главного окна**:</span><span class="sxs-lookup"><span data-stu-id="a0e84-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![Снимите флажок плавающие окна инструментов, чтобы ALT + TAB между Visual Studio и незакрепленным Инспектор страниц окном.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="a0e84-146">В верхней области окна Инспектор страниц отображается текущая страница в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="a0e84-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="a0e84-147">В нижней области отображается страница в разметке HTML слева, а также некоторые вкладки справа, позволяющие проверять различные аспекты страницы.</span><span class="sxs-lookup"><span data-stu-id="a0e84-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="a0e84-148">Нижняя панель аналогична [средства для разработчикову F12](https://msdn.microsoft.com/ie/aa740478) в Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="a0e84-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="a0e84-149">(Однако, в отличие от средств разработчика, вы можете использовать Инспектор страниц прямо в Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="a0e84-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![Инспектор страниц](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="a0e84-151">В этом руководстве вы будете использовать панель браузера Инспектор страниц, а также вкладки **HTML** и **стили** , помогающие быстро перемещаться в приложение и вносить в него изменения.</span><span class="sxs-lookup"><span data-stu-id="a0e84-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="a0e84-152">Включить режим проверки</span><span class="sxs-lookup"><span data-stu-id="a0e84-152">Enable Inspection Mode</span></span>

<span data-ttu-id="a0e84-153">Далее вы узнаете, как работает режим проверки Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="a0e84-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="a0e84-154">В окне Инспектор страниц нажмите кнопку **проверить** .</span><span class="sxs-lookup"><span data-stu-id="a0e84-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![Проверить элемент](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="a0e84-156">Чтобы увидеть режим проверки в действии, наведите указатель мыши на различные части страницы в Инспектор страниц окне браузера.</span><span class="sxs-lookup"><span data-stu-id="a0e84-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="a0e84-157">При этом указатель мыши превращается в большой знак «плюс», и элемент под ним выделяется.</span><span class="sxs-lookup"><span data-stu-id="a0e84-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Наведение указателя мыши на div. Content-упаковщик](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="a0e84-159">При перемещении указателя мыши Обратите внимание на то, что</span><span class="sxs-lookup"><span data-stu-id="a0e84-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="a0e84-160">Содержимое в представлении **исходного кода** изменяется для отображения разметки, соответствующей выбранному элементу на странице.</span><span class="sxs-lookup"><span data-stu-id="a0e84-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="a0e84-161">Соответствующая разметка выделена.</span><span class="sxs-lookup"><span data-stu-id="a0e84-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="a0e84-162">Если источник находится в другом файле, этот файл открывается в представлении исходного кода с выделенной подходящим разметкой.</span><span class="sxs-lookup"><span data-stu-id="a0e84-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="a0e84-163">Разметка, отображаемая на вкладке **HTML** в инспектор страниц, также изменяется в соответствии с выбранным элементом на странице.</span><span class="sxs-lookup"><span data-stu-id="a0e84-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="a0e84-164">На вкладке **HTML** соответствующая разметка обтроена.</span><span class="sxs-lookup"><span data-stu-id="a0e84-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="a0e84-165">На вкладке **стили** ОТОБРАЖАЮТСЯ правила CSS, относящиеся к текущему выделению.</span><span class="sxs-lookup"><span data-stu-id="a0e84-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="a0e84-166">Использование Инспектор страниц для внесения изменений в разметку</span><span class="sxs-lookup"><span data-stu-id="a0e84-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="a0e84-167">Теперь вы увидите, как можно использовать Инспектор страниц для поиска и внесения изменений в разметку или текст, расположение которого может быть не сразу очевидным.</span><span class="sxs-lookup"><span data-stu-id="a0e84-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="a0e84-168">Поставьте Инспектор страниц в режим проверки и прокрутите домашнюю страницу вниз.</span><span class="sxs-lookup"><span data-stu-id="a0e84-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="a0e84-169">После ввода нижнего колонтитула Инспектор страниц открывает файл макета *site. master* в представлении **исходного кода** во временной вкладке справа от других вкладок и выделяет выбранный раздел главной страницы.</span><span class="sxs-lookup"><span data-stu-id="a0e84-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="a0e84-170">В этом примере показано, как Инспектор страниц может находить и отображать содержимое на странице, которая может быть взята из файла, отличного от того, который был изначально открыт.</span><span class="sxs-lookup"><span data-stu-id="a0e84-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![Выделение нижнего колонтитула в режим проверки](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="a0e84-172">В окне браузера Инспектор страниц наведите указатель мыши на строку с уведомлением об авторских <a id="a"> </a>правах.</span><span class="sxs-lookup"><span data-stu-id="a0e84-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="a0e84-173">На странице *site. master* выделена соответствующая строка.</span><span class="sxs-lookup"><span data-stu-id="a0e84-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![Выделенная строка авторских прав нижнего колонтитула](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="a0e84-175">Добавьте текст в конец строки в файле *site. master* .</span><span class="sxs-lookup"><span data-stu-id="a0e84-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="a0e84-176">&lt;p&gt;&amp;Copy; &lt;%: DateTime. Now. Year%&gt;-мой ASP.NET приложение Rocks!&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="a0e84-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="a0e84-177">Теперь нажмите клавиши CTRL + ALT + ВВОД или щелкните панель обновления, чтобы просмотреть результаты в окне браузера Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="a0e84-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![Мой ASP.NET приложение Rocks!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="a0e84-179">Возможно, вы считали, что нижний колонтитул был на странице *Default. aspx* , но он был на странице макета образца и инспектор страниц его найти.</span><span class="sxs-lookup"><span data-stu-id="a0e84-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="a0e84-180">режим проверки и окно HTML</span><span class="sxs-lookup"><span data-stu-id="a0e84-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="a0e84-181">Теперь вы сможете быстро взглянуть на окно HTML и то, как оно сопоставляет элементы.</span><span class="sxs-lookup"><span data-stu-id="a0e84-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="a0e84-182">Поставьте Инспектор страниц в режим проверки.</span><span class="sxs-lookup"><span data-stu-id="a0e84-182">Put Page Inspector in Inspection Mode.</span></span>

![Проверить элемент](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="a0e84-184">Щелкните верхнюю часть страницы с текстом "Ваша Эмблема".</span><span class="sxs-lookup"><span data-stu-id="a0e84-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="a0e84-185">Вы проведете анализ определенного элемента более подробно, поэтому отображение в окне браузера больше не изменяется при перемещении указателя мыши.</span><span class="sxs-lookup"><span data-stu-id="a0e84-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="a0e84-186">Теперь наведите указатель мыши на окно **HTML** .</span><span class="sxs-lookup"><span data-stu-id="a0e84-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="a0e84-187">При перемещении указателя мыши Инспектор страниц отображает элемент в окне **HTML** и выделяет соответствующий элемент в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="a0e84-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![Окно HTML](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="a0e84-189">Как и ранее, Инспектор страниц открывает файл *site. master* на временной вкладке. Перейдите на вкладку site. master, и соответствующая разметка выделяется в заголовке &lt;&gt; разделе:</span><span class="sxs-lookup"><span data-stu-id="a0e84-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![Выделенная разметка](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="a0e84-191">Предварительный просмотр изменений CSS в окне "стили"</span><span class="sxs-lookup"><span data-stu-id="a0e84-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="a0e84-192">Далее вы узнаете, как можно использовать окно **стили** инспектор страниц для предварительного просмотра изменений в CSS.</span><span class="sxs-lookup"><span data-stu-id="a0e84-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="a0e84-193">Нажмите кнопку " **проверить** ", чтобы добавить Инспектор страниц в режим проверки.</span><span class="sxs-lookup"><span data-stu-id="a0e84-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="a0e84-194">В окне браузера Инспектор страниц наведите указатель мыши на раздел "Домашняя страница", пока не появится метка **div. Content-упаковщик** .</span><span class="sxs-lookup"><span data-stu-id="a0e84-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Наведение указателя мыши на элементы](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="a0e84-196">Щелкните один раз в разделе div. Content-оберток, а затем переместите указатель мыши в окно **стили** .</span><span class="sxs-lookup"><span data-stu-id="a0e84-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="a0e84-197">В селекторе класса. популярное. Content-оберток снимите флажок и установите флажок для свойства цвет фона.</span><span class="sxs-lookup"><span data-stu-id="a0e84-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![Очистить цвет фона](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="a0e84-199">Обратите внимание на то, как мгновенно просмотреть изменения в окне браузера Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="a0e84-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="a0e84-200">Снова установите флажок, затем дважды щелкните значение свойства и измените его на `red`.</span><span class="sxs-lookup"><span data-stu-id="a0e84-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="a0e84-201">Это изменение показано немедленно:</span><span class="sxs-lookup"><span data-stu-id="a0e84-201">The change shows immediately:</span></span>

![Красный цвет фона](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="a0e84-203">Окно **стили** упрощает тестирование и предварительный просмотр изменений в CSS перед фиксацией изменений в самой таблице стилей.</span><span class="sxs-lookup"><span data-stu-id="a0e84-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="a0e84-204">Автоматическая синхронизация CSS</span><span class="sxs-lookup"><span data-stu-id="a0e84-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="a0e84-205">Для этой функции требуется версия 1,3 Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="a0e84-205">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="a0e84-206">Функция автоматической синхронизации CSS позволяет непосредственно редактировать CSS-файл и немедленно просматривать изменения в обозревателе Инспектор страниц.</span><span class="sxs-lookup"><span data-stu-id="a0e84-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="a0e84-207">Нажмите кнопку **проверить** , чтобы перевести Инспектор страниц в режим проверки.</span><span class="sxs-lookup"><span data-stu-id="a0e84-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="a0e84-208">В браузере Инспектор страниц наведите указатель мыши на раздел "Домашняя страница", пока не появится метка **div. Content-упаковщик** .</span><span class="sxs-lookup"><span data-stu-id="a0e84-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="a0e84-209">Щелкните один раз, чтобы выбрать этот элемент.</span><span class="sxs-lookup"><span data-stu-id="a0e84-209">Click once to select this element.</span></span>

<span data-ttu-id="a0e84-210">В окне **стили** отображаются все правила CSS для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="a0e84-210">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="a0e84-211">Прокрутите вниз, чтобы найти селектор класса. Избранное. Content-оберток.</span><span class="sxs-lookup"><span data-stu-id="a0e84-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="a0e84-212">Щелкните ". Избранное. Content-упаковщик".</span><span class="sxs-lookup"><span data-stu-id="a0e84-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="a0e84-213">Инспектор страниц открывает CSS-файл, который определяет этот стиль (site. CSS) и выделяет соответствующий стиль CSS.</span><span class="sxs-lookup"><span data-stu-id="a0e84-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![Файл CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="a0e84-215">Теперь измените значение `background-color` на "Red".</span><span class="sxs-lookup"><span data-stu-id="a0e84-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="a0e84-216">Это изменение отображается сразу в Инспектор страниц браузере.</span><span class="sxs-lookup"><span data-stu-id="a0e84-216">The change appears immediately in the Page Inspector browser.</span></span>

![Браузер Инспектор страниц](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="a0e84-218">Использование выбора цвета CSS</span><span class="sxs-lookup"><span data-stu-id="a0e84-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="a0e84-219">Далее вы узнаете, как использовать Инспектор страниц для быстрого поиска и изменения CSS для выделенного текста в приложении по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a0e84-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="a0e84-220">В этом примере вы решили, что вы не нравится синему выделению и хотите изменить его на другой цвет.</span><span class="sxs-lookup"><span data-stu-id="a0e84-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="a0e84-221">Нажмите кнопку **проверить** .</span><span class="sxs-lookup"><span data-stu-id="a0e84-221">Click the **Inspect** button.</span></span>

![Проверить элемент](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="a0e84-223">В окне браузера Инспектор страниц наведите указатель мыши на выделенный текст "видео, учебники и примеры", чтобы появилась метка CSS "марка".</span><span class="sxs-lookup"><span data-stu-id="a0e84-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![Наведение указателя мыши на элемент Mark](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="a0e84-225">Щелкните текст, чтобы выбрать его.</span><span class="sxs-lookup"><span data-stu-id="a0e84-225">Click the text to select it.</span></span> <span data-ttu-id="a0e84-226">В нижней части окна **стили** появится соответствующий селектор CSS.</span><span class="sxs-lookup"><span data-stu-id="a0e84-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![Выбор метки в окне "стили"](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="a0e84-228">Щелкните элемент выбора метки.</span><span class="sxs-lookup"><span data-stu-id="a0e84-228">Click the mark selector.</span></span> <span data-ttu-id="a0e84-229">Откроется файл *site. CSS* для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a0e84-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="a0e84-230">Перейдите на вкладку site. CSS, и соответствующие CSS для селектора выделяются:</span><span class="sxs-lookup"><span data-stu-id="a0e84-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![пометить селектор в таблице стилей](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="a0e84-232">Выберите и удалите линию со свойством цвет фона.</span><span class="sxs-lookup"><span data-stu-id="a0e84-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="a0e84-233">Теперь вы будете использовать новое средство выбора цвета CSS Visual Studio 2012, чтобы выбрать новый цвет для свойства **метки** фона.</span><span class="sxs-lookup"><span data-stu-id="a0e84-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="a0e84-234">Использование средства выбора цвета CSS в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a0e84-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="a0e84-235">Редактор CSS в Visual Studio 2012 имеет палитру цветов, которая позволяет легко выбирать и вставлять цвета.</span><span class="sxs-lookup"><span data-stu-id="a0e84-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="a0e84-236">Он имеет простую цветовую полоску и «всплывающий элемент выбора», предлагающий более точный контроль.</span><span class="sxs-lookup"><span data-stu-id="a0e84-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="a0e84-237">Палитра цветов включает стандартную палитру цветов, поддерживает стандартные имена цветов, хэш-коды, RGB, RGBA, HSL и ХСЛА, а также поддерживает список цветов, использовавшихся в документе последними.</span><span class="sxs-lookup"><span data-stu-id="a0e84-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="a0e84-238">В строке со свойством цвет фона введите BC и нажмите клавишу Стрелка вниз.</span><span class="sxs-lookup"><span data-stu-id="a0e84-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="a0e84-239">При вводе первого символа каждого слова в свойстве, разделенном дефисом, например "Background-Color", IntelliSense фильтрует список для отображения только тех свойств, которые соответствуют:</span><span class="sxs-lookup"><span data-stu-id="a0e84-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![Отфильтрованные значения IntelliSense](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="a0e84-241">Теперь введите двоеточие.</span><span class="sxs-lookup"><span data-stu-id="a0e84-241">Now type a colon.</span></span> <span data-ttu-id="a0e84-242">При этом вставляется полное имя свойства цвета фона.</span><span class="sxs-lookup"><span data-stu-id="a0e84-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="a0e84-243">Введите **#** или **RGB (** , и появится панель выбора цвета:</span><span class="sxs-lookup"><span data-stu-id="a0e84-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![Панель выбора цвета CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="a0e84-245">Чтобы увидеть, как работает панель выбора цвета, щелкните ее цвета с помощью указателя мыши или нажмите клавишу Стрелка вниз, а затем используйте клавиши со стрелками влево и вправо для перемещения по цветам.</span><span class="sxs-lookup"><span data-stu-id="a0e84-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="a0e84-246">При посещении цвета отображается соответствующее значение для свойства цвет фона:</span><span class="sxs-lookup"><span data-stu-id="a0e84-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![Предварительный просмотр значения свойства цвета фона](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="a0e84-248">На этом этапе можно нажать клавишу ВВОД, чтобы выбрать значение, а затем точку с запятой (;) для завершения записи CSS.</span><span class="sxs-lookup"><span data-stu-id="a0e84-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="a0e84-249">Сейчас перейдите к следующему разделу, чтобы увидеть, как работает всплывающее окно палитры цветов.</span><span class="sxs-lookup"><span data-stu-id="a0e84-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="a0e84-250">Использование всплывающего окна «Палитра цветов»</span><span class="sxs-lookup"><span data-stu-id="a0e84-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="a0e84-251">Если цветовая шкала не имеет точного цвета, которую вы ищете, можно использовать всплывающее окно палитры цветов.</span><span class="sxs-lookup"><span data-stu-id="a0e84-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="a0e84-252">Чтобы открыть его, щелкните значок шеврона в правой части цветовой шкалы или нажмите стрелку вниз один или два раза на клавиатуре.</span><span class="sxs-lookup"><span data-stu-id="a0e84-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![Всплывающее окно выбора цвета CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="a0e84-254">Щелкните цвет на вертикальной панели справа.</span><span class="sxs-lookup"><span data-stu-id="a0e84-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="a0e84-255">Он показывает градиент для этого цвета в главном окне.</span><span class="sxs-lookup"><span data-stu-id="a0e84-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="a0e84-256">Выберите цвет непосредственно из вертикальной линии, нажав клавишу ВВОД, или щелкните любую точку в главном окне, чтобы выбрать с большей точностью.</span><span class="sxs-lookup"><span data-stu-id="a0e84-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="a0e84-257">Если на экране компьютера есть цвет, который вы хотите использовать (он не должен находиться в пользовательском интерфейсе Visual Studio), его значение можно записать с помощью инструмента "Пипетка" в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="a0e84-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="a0e84-258">Можно также изменить прозрачность цвета, переместив ползунок в нижней части палитры цветов.</span><span class="sxs-lookup"><span data-stu-id="a0e84-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="a0e84-259">При этом значения цвета изменяются на значения RGBA, поскольку формат RGBA может представлять непрозрачность.</span><span class="sxs-lookup"><span data-stu-id="a0e84-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="a0e84-260">После выбора цвета нажмите клавишу ВВОД, а затем введите точку с запятой, чтобы завершить запись в фоновом режиме в файле *site. CSS* .</span><span class="sxs-lookup"><span data-stu-id="a0e84-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="a0e84-261">Панель обновления Инспектор страниц</span><span class="sxs-lookup"><span data-stu-id="a0e84-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="a0e84-262">Инспектор страниц немедленно обнаруживает изменение файла *site. CSS* (или любого файла в приложении) и отображает предупреждение на панели обновления.</span><span class="sxs-lookup"><span data-stu-id="a0e84-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![Обновить панель](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="a0e84-264">Чтобы сохранить все файлы и обновить обозреватель Инспектор страниц, нажмите клавиши CTRL + ALT + ВВОД или щелкните панель обновления.</span><span class="sxs-lookup"><span data-stu-id="a0e84-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="a0e84-265">Изменение цвета выделения отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="a0e84-265">The change in the highlight color appears in the browser:</span></span>

![Цвет выделения изменен](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="a0e84-267">Обратите внимание, что вы легко обновляете Инспектор страниц браузере прямо в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0e84-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="a0e84-268">Использование Инспектор страниц вместо внешнего браузера позволяет остаться в редакторе при разработке веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="a0e84-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="a0e84-269">См. также:</span><span class="sxs-lookup"><span data-stu-id="a0e84-269">See Also</span></span>

<span data-ttu-id="a0e84-270">[Знакомство с инспектор страниц](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (видео на канале 9)</span><span class="sxs-lookup"><span data-stu-id="a0e84-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="a0e84-271">[Инспектор страниц сообщения об ошибках](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="a0e84-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
