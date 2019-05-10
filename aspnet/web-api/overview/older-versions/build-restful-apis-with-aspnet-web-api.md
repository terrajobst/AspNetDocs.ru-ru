---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: Создание API-интерфейсов RESTful с помощью ASP.NET Web API — ASP.NET 4.x
author: rick-anderson
description: Практическое лабораторное занятие. Использование веб-API в ASP.NET 4.x, создать простой API REST для приложения диспетчера контактов.
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132265"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="02089-103">Создание API-интерфейсов RESTful с помощью веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="02089-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="02089-104">по [Web Слышатся Team](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="02089-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="02089-105">Практическое лабораторное занятие. Использование веб-API в ASP.NET 4.x, создать простой API REST для приложения диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="02089-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="02089-106">Вы также создадите клиента для использования API.</span><span class="sxs-lookup"><span data-stu-id="02089-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="02089-107">В последние годы стало clear, что HTTP не только для подготовки HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="02089-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="02089-108">Это также мощную платформу для построения веб-API, такие как с помощью несколько команд (GET, POST и т. д.) плюс несколько простых концепции *идентификаторы URI* и *заголовки*.</span><span class="sxs-lookup"><span data-stu-id="02089-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="02089-109">Веб-API ASP.NET — это набор компонентов, которые упрощают программирование HTTP.</span><span class="sxs-lookup"><span data-stu-id="02089-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="02089-110">Так как она построена на основе среды выполнения ASP.NET MVC, веб-API автоматически обрабатывает сведения низкого уровня транспорта протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="02089-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="02089-111">В то же время веб-API, естественным образом, предоставляет модель программирования HTTP.</span><span class="sxs-lookup"><span data-stu-id="02089-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="02089-112">На самом деле, одна из целей веб-API — *не* абстрагировании от реальности HTTP.</span><span class="sxs-lookup"><span data-stu-id="02089-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="02089-113">Таким образом веб-API, гибкие и легко расширяется.</span><span class="sxs-lookup"><span data-stu-id="02089-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="02089-114">Архитектурный стиль REST оказалось эффективным способом использовать HTTP -, несмотря на то, что это, конечно, единственным допустимым подход к HTTP.</span><span class="sxs-lookup"><span data-stu-id="02089-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="02089-115">Диспетчер контактов будет предоставлять RESTful для списка, добавление и удаление контактов, среди прочего.</span><span class="sxs-lookup"><span data-stu-id="02089-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="02089-116">Это лабораторное занятие требует понимания HTTP, REST и предполагается, что вы имеете базовые знания рабочий HTML, JavaScript и jQuery.</span><span class="sxs-lookup"><span data-stu-id="02089-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="02089-117">Веб-узла ASP.NET имеет выделенный в веб-API ASP.NET Framework в область [ https://asp.net/web-api ](https://asp.net/web-api).</span><span class="sxs-lookup"><span data-stu-id="02089-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="02089-118">Этот сайт будет продолжать последние сведения, примеры и новостей, относящихся к веб-API, поэтому она регулярно проверяйте Если вы хотите более подробно рассмотрим искусством создания пользовательского веб-API, доступных для framework практически с любого устройства или разработки.</span><span class="sxs-lookup"><span data-stu-id="02089-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="02089-119">Веб-API, аналогичную ASP.NET MVC 4 ASP.NET имеет большую гибкость с точки зрения отделение слой служб от контроллеров, позволяя использовать несколько доступных платформ внедрения зависимостей довольно просто.</span><span class="sxs-lookup"><span data-stu-id="02089-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="02089-120">В MSDN, показывающий, как использовать Ninject для внедрения зависимостей в проекте веб-API ASP.NET, его можно загрузить из есть хороший пример [здесь](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span><span class="sxs-lookup"><span data-stu-id="02089-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="02089-121">Все примеры кода и фрагменты кода включены в Web лагеря комплект обучающих материалов, доступных в [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="02089-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="02089-122">Цели</span><span class="sxs-lookup"><span data-stu-id="02089-122">Objectives</span></span>

<span data-ttu-id="02089-123">В этой практической работу вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="02089-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="02089-124">Реализации веб-API RESTful</span><span class="sxs-lookup"><span data-stu-id="02089-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="02089-125">Для вызова API из HTML-клиента</span><span class="sxs-lookup"><span data-stu-id="02089-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="02089-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="02089-126">Prerequisites</span></span>

<span data-ttu-id="02089-127">Для завершения этой практической работу требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="02089-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="02089-128">[Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или руководителя (чтение [приложении Б](#AppendixB) инструкции по его установке).</span><span class="sxs-lookup"><span data-stu-id="02089-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="02089-129">Установка</span><span class="sxs-lookup"><span data-stu-id="02089-129">Setup</span></span>

<span data-ttu-id="02089-130">**Установка фрагменты кода**</span><span class="sxs-lookup"><span data-stu-id="02089-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="02089-131">Для удобства большая часть кода, который вы планируете управлять вдоль этой лаборатории доступен как фрагменты кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02089-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="02089-132">Чтобы установить фрагменты кода запуска **.\Source\Setup\CodeSnippets.vsi** файла.</span><span class="sxs-lookup"><span data-stu-id="02089-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="02089-133">Если вы не знакомы с фрагменты кода Visual Studio и хотите научиться использовать их, можно ссылаться в приложение из этого документа &quot; [приложении a. Фрагменты кода](#AppendixA)&quot;.</span><span class="sxs-lookup"><span data-stu-id="02089-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="02089-134">Упражнения</span><span class="sxs-lookup"><span data-stu-id="02089-134">Exercises</span></span>

<span data-ttu-id="02089-135">Это Практическое занятие включает в себя следующие упражнения:</span><span class="sxs-lookup"><span data-stu-id="02089-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="02089-136">Упражнение 1. Создание только для чтения веб-API</span><span class="sxs-lookup"><span data-stu-id="02089-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="02089-137">Упражнение 2. Создание чтения и записи веб-API</span><span class="sxs-lookup"><span data-stu-id="02089-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="02089-138">Упражнение 3. Использовать веб-API из HTML-клиента</span><span class="sxs-lookup"><span data-stu-id="02089-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="02089-139">Каждого упражнения сопровождается **окончания** папку, содержащую полученное решение, должен быть получен после завершения упражнения.</span><span class="sxs-lookup"><span data-stu-id="02089-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="02089-140">Это решение можно использовать как руководство, если вам нужна дополнительная помощь при работе с примерами.</span><span class="sxs-lookup"><span data-stu-id="02089-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="02089-141">Предполагаемое время для выполнения этого лабораторного: **60 минут**.</span><span class="sxs-lookup"><span data-stu-id="02089-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="02089-142">Упражнение 1. Создание только для чтения веб-API</span><span class="sxs-lookup"><span data-stu-id="02089-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="02089-143">В этом упражнении вы реализуете методы GET только для чтения для диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="02089-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="02089-144">Задача 1 - Создание проекта API</span><span class="sxs-lookup"><span data-stu-id="02089-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="02089-145">В этой задаче будет использовать новые шаблоны веб-проектов ASP.NET для создания веб-приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="02089-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="02089-146">Запустите **Visual Studio 2012 Express для Web**, для этого перейдите к **запустить** и тип **VS Express для Web** нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="02089-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="02089-147">Из **файл** меню, выберите **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="02089-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="02089-148">Выберите **Visual C# | Web** тип в представлении дерева проекта типа проекта, а затем выберите **веб-приложение ASP.NET MVC 4** тип проекта.</span><span class="sxs-lookup"><span data-stu-id="02089-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="02089-149">Установите проект **имя** для *ContactManager* и **имя решения** для *начать*, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="02089-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="02089-150">![Создание нового ASP.NET MVC 4.0 проект веб-приложения](build-restful-apis-with-aspnet-web-api/_static/image1.png "Создание нового ASP.NET MVC 4.0 проект веб-приложения")</span><span class="sxs-lookup"><span data-stu-id="02089-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="02089-151">*Создание нового ASP.NET MVC 4.0 проект веб-приложения*</span><span class="sxs-lookup"><span data-stu-id="02089-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="02089-152">В диалоговом окне типа проекта ASP.NET MVC 4, выберите **веб-API** тип проекта.</span><span class="sxs-lookup"><span data-stu-id="02089-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="02089-153">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="02089-153">Click **OK**.</span></span>

    <span data-ttu-id="02089-154">![Указывает тип проекта веб-API](build-restful-apis-with-aspnet-web-api/_static/image2.png "указывает тип проекта веб-API")</span><span class="sxs-lookup"><span data-stu-id="02089-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="02089-155">*Указывает тип проекта веб-API*</span><span class="sxs-lookup"><span data-stu-id="02089-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="02089-156">Задача 2 - Создание контроллеров API диспетчера контактов</span><span class="sxs-lookup"><span data-stu-id="02089-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="02089-157">В этой задаче вы создадите классы контроллера, в которых будет находиться методов API.</span><span class="sxs-lookup"><span data-stu-id="02089-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="02089-158">Удалите файл с именем **ValuesController.cs** в **контроллеров** папку из проекта.</span><span class="sxs-lookup"><span data-stu-id="02089-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="02089-159">Щелкните правой кнопкой мыши **контроллеров** папки в проект и выберите **Add | Контроллер** в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="02089-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="02089-160">![Добавление в проект новый контроллер](build-restful-apis-with-aspnet-web-api/_static/image3.png "добавлении нового контроллера в проект")</span><span class="sxs-lookup"><span data-stu-id="02089-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="02089-161">*Добавление в проект новый контроллер*</span><span class="sxs-lookup"><span data-stu-id="02089-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="02089-162">В **Добавление контроллера** появившемся диалоговом окне выберите **пустой контроллер API** меню шаблон.</span><span class="sxs-lookup"><span data-stu-id="02089-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="02089-163">Имя класса контроллера **ContactController**.</span><span class="sxs-lookup"><span data-stu-id="02089-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="02089-164">Щелкните **Add.**</span><span class="sxs-lookup"><span data-stu-id="02089-164">Then, click **Add.**</span></span>

    <span data-ttu-id="02089-165">![Используя диалоговое окно добавления контроллера для создания нового контроллера веб-API](build-restful-apis-with-aspnet-web-api/_static/image4.png "используя диалоговое окно добавления контроллера для создания нового контроллера веб-API")</span><span class="sxs-lookup"><span data-stu-id="02089-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="02089-166">*Используя диалоговое окно добавления контроллера для создания нового контроллера веб-API*</span><span class="sxs-lookup"><span data-stu-id="02089-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="02089-167">Добавьте следующий код, чтобы **ContactController**.</span><span class="sxs-lookup"><span data-stu-id="02089-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="02089-168">(Code Snippet - *метод API Get лаборатории API веб - Ex01 -*)</span><span class="sxs-lookup"><span data-stu-id="02089-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="02089-169">Нажмите клавишу **F5** для отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="02089-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="02089-170">Откроется домашняя страница по умолчанию для проекта веб-API.</span><span class="sxs-lookup"><span data-stu-id="02089-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="02089-171">![Домашняя страница по умолчанию приложения веб-API ASP.NET](build-restful-apis-with-aspnet-web-api/_static/image5.png "Домашняя страница по умолчанию приложения веб-API ASP.NET")</span><span class="sxs-lookup"><span data-stu-id="02089-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="02089-172">*Домашняя страница по умолчанию приложения веб-API ASP.NET*</span><span class="sxs-lookup"><span data-stu-id="02089-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="02089-173">В окне Internet Explorer, нажмите клавишу **F12** клавишу, чтобы открыть **средств разработчика** окна.</span><span class="sxs-lookup"><span data-stu-id="02089-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="02089-174">Нажмите кнопку **сети** , а затем щелкните **начать захват** кнопку, чтобы начать отслеживать сетевой трафик в окно.</span><span class="sxs-lookup"><span data-stu-id="02089-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="02089-175">![Открыв вкладку "Сеть" и затем запускать сбор по сети](build-restful-apis-with-aspnet-web-api/_static/image6.png "открыв вкладку \"Сеть\" и затем запускать сбор по сети")</span><span class="sxs-lookup"><span data-stu-id="02089-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="02089-176">*Открыв вкладку "Сеть" и затем запускать сбор данных о сети*</span><span class="sxs-lookup"><span data-stu-id="02089-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="02089-177">Добавьте URL-адрес в адресной строке браузера с **/api/contact** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="02089-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="02089-178">В окне записи сети отображаются сведения передачи.</span><span class="sxs-lookup"><span data-stu-id="02089-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="02089-179">Обратите внимание, что в ответе тип MIME **application/json**.</span><span class="sxs-lookup"><span data-stu-id="02089-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="02089-180">Это показывает, как формат выходных данных по умолчанию — JSON.</span><span class="sxs-lookup"><span data-stu-id="02089-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="02089-181">![Просмотр выходных данных запроса веб-API в представлении сети](build-restful-apis-with-aspnet-web-api/_static/image7.png "просмотр выходных данных запроса веб-API в представлении сети")</span><span class="sxs-lookup"><span data-stu-id="02089-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="02089-182">*Просмотр выходных данных запроса веб-API в представлении сети*</span><span class="sxs-lookup"><span data-stu-id="02089-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="02089-183">Поведение по умолчанию Internet Explorer 10 на этом этапе следует задавать, если пользователь хочет сохранить или открыть поток, полученный из вызова веб-API.</span><span class="sxs-lookup"><span data-stu-id="02089-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="02089-184">Выходные данные будут текстовый файл, содержащий результат JSON вызова URL-адрес API.</span><span class="sxs-lookup"><span data-stu-id="02089-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="02089-185">Не отменять диалогового окна, чтобы иметь возможность просматривать содержимое ответа через окно инструментов для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="02089-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="02089-186">Нажмите кнопку **перейдите к представлению подробные** кнопки для просмотра дополнительных сведений об ответе этот вызов API.</span><span class="sxs-lookup"><span data-stu-id="02089-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="02089-187">![Переключиться в подробное представление](build-restful-apis-with-aspnet-web-api/_static/image8.png "переключитесь в представление сведений")</span><span class="sxs-lookup"><span data-stu-id="02089-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="02089-188">*Переключиться в подробное представление*</span><span class="sxs-lookup"><span data-stu-id="02089-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="02089-189">Нажмите кнопку **текст ответа** вкладку, чтобы просмотреть фактический текст ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="02089-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="02089-190">![Просмотр JSON вывода текста в сетевом мониторе](build-restful-apis-with-aspnet-web-api/_static/image9.png "просмотра JSON вывода текста в сетевом мониторе")</span><span class="sxs-lookup"><span data-stu-id="02089-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="02089-191">*Просмотр выходного текста JSON в сетевом мониторе*</span><span class="sxs-lookup"><span data-stu-id="02089-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="02089-192">Задача 3 - Создание связи моделей и дополнять контактные контроллера</span><span class="sxs-lookup"><span data-stu-id="02089-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="02089-193">В этой задаче вы создадите классы контроллера, в которых будет находиться методов API.</span><span class="sxs-lookup"><span data-stu-id="02089-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="02089-194">Щелкните правой кнопкой мыши **моделей** папку и выберите **Add | Класс...**  в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="02089-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="02089-195">![Добавление новой модели в веб-приложение](build-restful-apis-with-aspnet-web-api/_static/image10.png "Добавление новой модели в веб-приложение")</span><span class="sxs-lookup"><span data-stu-id="02089-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="02089-196">*Добавление новой модели в веб-приложение*</span><span class="sxs-lookup"><span data-stu-id="02089-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="02089-197">В **Добавление нового элемента** диалоговое окно, назовите новый файл **Contact.cs** и нажмите кнопку **Add.**</span><span class="sxs-lookup"><span data-stu-id="02089-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="02089-198">![Создание нового файла класса контакта](build-restful-apis-with-aspnet-web-api/_static/image11.png "Создание новый файл класса контакта")</span><span class="sxs-lookup"><span data-stu-id="02089-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="02089-199">*Создание нового файла класса контакта*</span><span class="sxs-lookup"><span data-stu-id="02089-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="02089-200">Добавьте следующий выделенный код, который **контакт** класса.</span><span class="sxs-lookup"><span data-stu-id="02089-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="02089-201">(Code Snippet - *веб-API лаборатории - Ex01 - класса контакта*)</span><span class="sxs-lookup"><span data-stu-id="02089-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="02089-202">В **ContactController** выберите слово **строка** в определение метода **получить** метод и введите слово *контакт*.</span><span class="sxs-lookup"><span data-stu-id="02089-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="02089-203">После слово вводится в, индикатора будет отображаться в начале слова **контакт**.</span><span class="sxs-lookup"><span data-stu-id="02089-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="02089-204">Либо удерживайте **Ctrl** ключа и нажмите клавишу точки (.) или щелкните значок с помощью мыши, чтобы открыть диалоговое окно помощника в редакторе кода, чтобы автоматически заполнять **с помощью** директив для моделей пространство имен.</span><span class="sxs-lookup"><span data-stu-id="02089-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![С помощью Intellisense помощь для деклараций пространств имен](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="02089-206">*С помощью Intellisense помощь для деклараций пространств имен*</span><span class="sxs-lookup"><span data-stu-id="02089-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="02089-207">Изменение кода для **получить** метод, возвращающий массив экземпляров модели контакта.</span><span class="sxs-lookup"><span data-stu-id="02089-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="02089-208">(Code Snippet - *лаборатории API веб - Ex01 - Возврат списка контактов*)</span><span class="sxs-lookup"><span data-stu-id="02089-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="02089-209">Нажмите клавишу **F5** для отладки веб-приложения в браузере.</span><span class="sxs-lookup"><span data-stu-id="02089-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="02089-210">Чтобы просмотреть изменения, внесенные в выходные данные ответа API, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="02089-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="02089-211">После того, как браузер откроется, нажмите **F12** средств разработчика еще не открытым.</span><span class="sxs-lookup"><span data-stu-id="02089-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="02089-212">Нажмите кнопку **сети** вкладки.</span><span class="sxs-lookup"><span data-stu-id="02089-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="02089-213">Нажмите клавишу **начать захват** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02089-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="02089-214">Добавьте суффикс URL-адрес **/api/contact** на URL-адрес в адресной строке и нажмите клавишу **ввод** ключ.</span><span class="sxs-lookup"><span data-stu-id="02089-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="02089-215">Нажмите клавишу **перейдите к представлению подробные** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02089-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="02089-216">Выберите **текст ответа** вкладки. Вы должны увидеть строку JSON, представляющая сериализованную форму массива экземпляров контакта.</span><span class="sxs-lookup"><span data-stu-id="02089-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="02089-217">![JSON-сериализованных выходных данных вызова метода веб-API, сложных](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON сериализованных выходных данных сложные вызова метода веб-API")</span><span class="sxs-lookup"><span data-stu-id="02089-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="02089-218">*Выходные данные сериализации JSON сложных вызова метода веб-API*</span><span class="sxs-lookup"><span data-stu-id="02089-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="02089-219">Задача 4 - извлечения функции в слой служб</span><span class="sxs-lookup"><span data-stu-id="02089-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="02089-220">Эта задача будет показано, как для извлечения функции в слой служб, что упрощает для разработчиков для разделения их функциональность службы от уровня контроллера, тем самым позволяя возможность многократного использования служб, которые фактически выполняющие работу.</span><span class="sxs-lookup"><span data-stu-id="02089-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="02089-221">Создайте новую папку в корневом каталоге решения и назовите его **служб**.</span><span class="sxs-lookup"><span data-stu-id="02089-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="02089-222">Чтобы сделать это, щелкните правой кнопкой мыши **ContactManager** проекта, выберите **добавить** | **новую папку**, назовите его *служб*.</span><span class="sxs-lookup"><span data-stu-id="02089-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="02089-223">![Папка служб создание](build-restful-apis-with-aspnet-web-api/_static/image14.png "папку создание служб")</span><span class="sxs-lookup"><span data-stu-id="02089-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="02089-224">*Создание папки служб*</span><span class="sxs-lookup"><span data-stu-id="02089-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="02089-225">Щелкните правой кнопкой мыши **служб** папку и выберите **Add | Класс...**  в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="02089-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="02089-226">![Добавление нового класса в папку службы](build-restful-apis-with-aspnet-web-api/_static/image15.png "Добавление нового класса в папку «службы»")</span><span class="sxs-lookup"><span data-stu-id="02089-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="02089-227">*Добавление нового класса в папку «службы»*</span><span class="sxs-lookup"><span data-stu-id="02089-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="02089-228">Когда **Добавление нового элемента** откроется диалоговое окно, назовите новый класс **ContactRepository** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="02089-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="02089-229">![Создание класса файл, содержащий код для уровня службы репозитория обратитесь к](build-restful-apis-with-aspnet-web-api/_static/image16.png "создания файла класса должен содержать код для уровня службы репозитория контактов")</span><span class="sxs-lookup"><span data-stu-id="02089-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="02089-230">*Создание класса файл, содержащий код для уровня службы репозитория контактов*</span><span class="sxs-lookup"><span data-stu-id="02089-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="02089-231">Добавить с помощью директивы **ContactRepository.cs** файл, чтобы включить пространство имен модели.</span><span class="sxs-lookup"><span data-stu-id="02089-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="02089-232">Добавьте следующий выделенный код, который **ContactRepository.cs** файл для реализации метода GetAllContacts.</span><span class="sxs-lookup"><span data-stu-id="02089-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="02089-233">(Code Snippet - *веб-API лаборатории - Ex01 - репозиторий контактов*)</span><span class="sxs-lookup"><span data-stu-id="02089-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="02089-234">Откройте **ContactController.cs** файла, если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="02089-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="02089-235">Добавьте следующий код с помощью инструкции в раздел объявлений пространства имен файла.</span><span class="sxs-lookup"><span data-stu-id="02089-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="02089-236">Добавьте следующий выделенный код, который **ContactController.cs** класса добавьте закрытое поле для представления экземпляра репозитория, таким образом, чтобы использовать rest членам класса реализации службы.</span><span class="sxs-lookup"><span data-stu-id="02089-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="02089-237">(Code Snippet - *лаборатории API - Ex01 - контактные контроллер веб-*)</span><span class="sxs-lookup"><span data-stu-id="02089-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="02089-238">Изменение **получить** метод, поэтому она позволяет использовать службы репозитория контактов.</span><span class="sxs-lookup"><span data-stu-id="02089-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="02089-239">(Code Snippet - *лаборатории API веб - Ex01 - Возврат списка контактов с помощью репозитория*)</span><span class="sxs-lookup"><span data-stu-id="02089-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="02089-240">Установите точку останова на **ContactController** **получить** определение метода.</span><span class="sxs-lookup"><span data-stu-id="02089-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="02089-241">![Добавление точек останова к контроллеру контактные](build-restful-apis-with-aspnet-web-api/_static/image17.png "Добавление точек останова к контроллеру контакта")</span><span class="sxs-lookup"><span data-stu-id="02089-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="02089-242">*Добавление точек останова к контроллеру контакта*</span><span class="sxs-lookup"><span data-stu-id="02089-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="02089-243">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="02089-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="02089-244">Когда откроется браузер, нажмите клавишу **F12** открытие средств разработчика.</span><span class="sxs-lookup"><span data-stu-id="02089-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="02089-245">Нажмите кнопку **сети** вкладки.</span><span class="sxs-lookup"><span data-stu-id="02089-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="02089-246">Нажмите кнопку **начать захват** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02089-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="02089-247">Добавьте URL-адрес в адресной строке с суффиксом **/api/contact** и нажмите клавишу **ввод** загрузить контроллер API.</span><span class="sxs-lookup"><span data-stu-id="02089-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="02089-248">Visual Studio 2012 следует останов **получить** начинается выполнение метода.</span><span class="sxs-lookup"><span data-stu-id="02089-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="02089-249">![Критические в метод Get](build-restful-apis-with-aspnet-web-api/_static/image18.png "критические в метод Get")</span><span class="sxs-lookup"><span data-stu-id="02089-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="02089-250">*Критические в метод Get*</span><span class="sxs-lookup"><span data-stu-id="02089-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="02089-251">Чтобы продолжить выполнение, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="02089-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="02089-252">Вернуться назад в Internet Explorer, если он еще не находится в фокусе.</span><span class="sxs-lookup"><span data-stu-id="02089-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="02089-253">Обратите внимание, окно записи сетевых данных.</span><span class="sxs-lookup"><span data-stu-id="02089-253">Note the network capture window.</span></span>

    <span data-ttu-id="02089-254">![В обозревателе Internet Explorer, отображая результаты вызова веб-API сети](build-restful-apis-with-aspnet-web-api/_static/image19.png "сети в обозревателе Internet Explorer, отображая результаты вызова веб-API")</span><span class="sxs-lookup"><span data-stu-id="02089-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="02089-255">*Представление сети в Internet Explorer, отображая результаты вызова веб-API*</span><span class="sxs-lookup"><span data-stu-id="02089-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="02089-256">Нажмите кнопку **перейдите к представлению подробные** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02089-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="02089-257">Нажмите кнопку **текст ответа** вкладки. Обратите внимание, выходные данные JSON в вызове API, и как он представляет два контакта, полученный на уровне службы.</span><span class="sxs-lookup"><span data-stu-id="02089-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="02089-258">![Просмотр выходных данных JSON из веб-API в окне средств разработчика](build-restful-apis-with-aspnet-web-api/_static/image20.png "просмотр выходных данных JSON из веб-API в окне средств разработчика")</span><span class="sxs-lookup"><span data-stu-id="02089-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="02089-259">*Просмотр выходных данных JSON из веб-API в окне средств разработчика*</span><span class="sxs-lookup"><span data-stu-id="02089-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="02089-260">Упражнение 2. Создание чтения и записи веб-API</span><span class="sxs-lookup"><span data-stu-id="02089-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="02089-261">В этом упражнении вы реализуете POST и PUT методы для диспетчера контактов включить его с помощью функции редактирования данных.</span><span class="sxs-lookup"><span data-stu-id="02089-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="02089-262">Задача 1 - Открытие проекта веб-API</span><span class="sxs-lookup"><span data-stu-id="02089-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="02089-263">В этой задаче будет подготовлена для улучшения проект веб-API, созданный в упражнении 1, таким образом, он может принимать ввод данных пользователем.</span><span class="sxs-lookup"><span data-stu-id="02089-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="02089-264">Запустите **Visual Studio 2012 Express для Web**, для этого перейдите к **запустить** и тип **VS Express для Web** нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="02089-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="02089-265">Откройте **начать** решений, расположенный **источника/Ex02-ReadWriteWebAPI/начало/** папки.</span><span class="sxs-lookup"><span data-stu-id="02089-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="02089-266">В противном случае можно продолжить использование **окончания** решение получен путем выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="02089-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="02089-267">Если вы открыли предоставленный **начать** решение, необходимо будет загрузить некоторые отсутствующие пакеты NuGet прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="02089-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="02089-268">Чтобы сделать это, нажмите кнопку **проекта** меню и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="02089-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="02089-269">В **управление пакетами NuGet** диалоговое окно, нажмите кнопку **восстановить** чтобы скачивать отсутствующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="02089-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="02089-270">Наконец, постройте решение, нажав кнопку **построения** | **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="02089-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="02089-271">Одним из преимуществ использования NuGet является отсутствие поставлять все библиотеки в проекте, уменьшив размер проекта.</span><span class="sxs-lookup"><span data-stu-id="02089-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="02089-272">С помощью NuGet Power Tools путем указания версий пакета в файле Packages.config можно для скачивания всех необходимых библиотек при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="02089-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="02089-273">Вот почему необходимо выполните описанные выше действия, после открытия существующего решения из этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="02089-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="02089-274">Откройте **Services/ContactRepository.cs** файла.</span><span class="sxs-lookup"><span data-stu-id="02089-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="02089-275">Задача 2 - Добавление функций сохраняемости данных, к реализации репозиторий контактов</span><span class="sxs-lookup"><span data-stu-id="02089-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="02089-276">В этой задаче будет расширить класс ContactRepository проекта веб-API, созданного в упражнении 1, чтобы его можно сохранить и принимать ввод данных пользователем и новые экземпляры обратитесь в службу.</span><span class="sxs-lookup"><span data-stu-id="02089-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="02089-277">Добавьте следующую константу для **ContactRepository** класс, представляющий имя имя веб-сервера кэш элемент ключа позже в этом упражнении.</span><span class="sxs-lookup"><span data-stu-id="02089-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="02089-278">Добавьте конструктор для **ContactRepository** содержит следующий код.</span><span class="sxs-lookup"><span data-stu-id="02089-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="02089-279">(Code Snippet - *веб-API лаборатории - Ex02 - репозиторий контактов конструктор*)</span><span class="sxs-lookup"><span data-stu-id="02089-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="02089-280">Изменение кода для **GetAllContacts** метод, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="02089-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="02089-281">(Code Snippet - *лаборатории API веб - Ex02 - получить все контакты*)</span><span class="sxs-lookup"><span data-stu-id="02089-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="02089-282">В этом примере осуществляется для демонстрационных целей и будет использовать кэш веб сервера как на носителе, чтобы значения будут доступны для нескольких клиентов одновременно, а не использовать механизм хранения сеанса или времени жизни запроса хранилища.</span><span class="sxs-lookup"><span data-stu-id="02089-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="02089-283">Можно было использовать Entity Framework, XML-хранилища или любые другие различные вместо кэше веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="02089-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="02089-284">Реализуйте новый метод с именем **SaveContact** для **ContactRepository** класс для работа по сохранению контакта.</span><span class="sxs-lookup"><span data-stu-id="02089-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="02089-285">**SaveContact** метод должен принимать один **контакт** и возвращают логическое значение, указывающее успех или неудачу.</span><span class="sxs-lookup"><span data-stu-id="02089-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="02089-286">(Code Snippet - *веб-API лаборатории - Ex02 - реализация метода SaveContact*)</span><span class="sxs-lookup"><span data-stu-id="02089-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="02089-287">Упражнение 3. Использовать веб-API из HTML-клиента</span><span class="sxs-lookup"><span data-stu-id="02089-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="02089-288">В этом упражнении вы создадите HTML-клиента для вызова веб-API.</span><span class="sxs-lookup"><span data-stu-id="02089-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="02089-289">Этот клиент будет упростить обмен данными с веб-API с помощью JavaScript и отображает результаты в браузере с помощью разметки HTML.</span><span class="sxs-lookup"><span data-stu-id="02089-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="02089-290">Задача 1 - Изменение представления индекса для предоставляют графический интерфейс пользователя для отображения контактов</span><span class="sxs-lookup"><span data-stu-id="02089-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="02089-291">В этой задаче будет изменено представление индекса по умолчанию веб-приложения для поддержки требования отображения списка существующих контактов в HTML-браузером.</span><span class="sxs-lookup"><span data-stu-id="02089-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="02089-292">Откройте **Visual Studio 2012 Express для Web** если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="02089-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="02089-293">Откройте **начать** решений, расположенный **источника/Ex03-ConsumingWebAPI/начало/** папки.</span><span class="sxs-lookup"><span data-stu-id="02089-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="02089-294">В противном случае можно продолжить использование **окончания** решение получен путем выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="02089-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="02089-295">Если вы открыли предоставленный **начать** решение, необходимо будет загрузить некоторые отсутствующие пакеты NuGet прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="02089-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="02089-296">Чтобы сделать это, нажмите кнопку **проекта** меню и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="02089-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="02089-297">В **управление пакетами NuGet** диалоговое окно, нажмите кнопку **восстановить** чтобы скачивать отсутствующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="02089-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="02089-298">Наконец, постройте решение, нажав кнопку **построения** | **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="02089-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="02089-299">Одним из преимуществ использования NuGet является отсутствие поставлять все библиотеки в проекте, уменьшив размер проекта.</span><span class="sxs-lookup"><span data-stu-id="02089-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="02089-300">С помощью NuGet Power Tools путем указания версий пакета в файле Packages.config можно для скачивания всех необходимых библиотек при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="02089-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="02089-301">Вот почему необходимо выполните описанные выше действия, после открытия существующего решения из этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="02089-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="02089-302">Откройте **Index.cshtml** файл, расположенный в **Views/Home** папки.</span><span class="sxs-lookup"><span data-stu-id="02089-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="02089-303">Замените код HTML в элемент div с идентификатором **текст** , чтобы он выглядел как следующий код.</span><span class="sxs-lookup"><span data-stu-id="02089-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="02089-304">Добавьте следующий код Javascript в нижней части файла для выполнения запроса HTTP для веб-API.</span><span class="sxs-lookup"><span data-stu-id="02089-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="02089-305">Откройте **ContactController.cs** файла, если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="02089-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="02089-306">Поместите точку останова на **получить** метод **ContactController** класса.</span><span class="sxs-lookup"><span data-stu-id="02089-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="02089-307">![Установив точку останова в методе Get контроллера API](build-restful-apis-with-aspnet-web-api/_static/image21.png "установив точку останова в методе Get контроллера API")</span><span class="sxs-lookup"><span data-stu-id="02089-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="02089-308">*Установив точку останова в методе Get контроллера API*</span><span class="sxs-lookup"><span data-stu-id="02089-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="02089-309">Нажмите клавишу **F5**, чтобы запустить проект.</span><span class="sxs-lookup"><span data-stu-id="02089-309">Press **F5** to run the project.</span></span> <span data-ttu-id="02089-310">Обозреватель загрузит HTML-документа.</span><span class="sxs-lookup"><span data-stu-id="02089-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="02089-311">Убедитесь, что вы подключаетесь к корневой URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="02089-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="02089-312">После загрузки страницы и выполняет код JavaScript, точка останова будет достигнута и выполнение кода будет приостановлено в контроллере.</span><span class="sxs-lookup"><span data-stu-id="02089-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="02089-313">![Отладка в вызовы веб-API, с помощью VS Express для Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "отладки в вызовы веб-API, с помощью VS Express для Web")</span><span class="sxs-lookup"><span data-stu-id="02089-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="02089-314">*Отладка в вызов веб-API, с помощью Visual Studio 2012 Express для Web*</span><span class="sxs-lookup"><span data-stu-id="02089-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="02089-315">Удалите точку останова и нажмите клавишу **F5** или панель инструментов отладки **Продолжить** кнопку, чтобы продолжить загрузку представление в браузере.</span><span class="sxs-lookup"><span data-stu-id="02089-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="02089-316">После завершения вызова веб-API должно отобразиться контактов, возвращенных веб-API вызывать отобразить в виде элементов списка в браузере.</span><span class="sxs-lookup"><span data-stu-id="02089-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="02089-317">![Результаты вызова API, отображаются в браузере в виде элементов списка](build-restful-apis-with-aspnet-web-api/_static/image23.png "результаты вызова API, отображаются в браузере в виде элементов списка")</span><span class="sxs-lookup"><span data-stu-id="02089-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="02089-318">*Результаты вызова API, отображаются в браузере в виде элементов списка*</span><span class="sxs-lookup"><span data-stu-id="02089-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="02089-319">Остановите отладку.</span><span class="sxs-lookup"><span data-stu-id="02089-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="02089-320">Задача 2 - изменение представления индекса обеспечивает графический интерфейс пользователя для создания контактов</span><span class="sxs-lookup"><span data-stu-id="02089-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="02089-321">В этой задаче будет продолжать Изменение представления индекса приложения MVC.</span><span class="sxs-lookup"><span data-stu-id="02089-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="02089-322">Формы будут добавляться на HTML-страницу, которая будет ввод данных и отправлять их в веб-API для создания нового контакта, и будет создан новый метод контроллера веб-API для сбора даты из графического интерфейса пользователя.</span><span class="sxs-lookup"><span data-stu-id="02089-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="02089-323">Откройте **ContactController.cs** файла.</span><span class="sxs-lookup"><span data-stu-id="02089-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="02089-324">Добавьте новый метод в класс контроллера с именем **Post** как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="02089-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="02089-325">(Code Snippet - *веб-метода Post лаборатории API - Ex03 -*)</span><span class="sxs-lookup"><span data-stu-id="02089-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="02089-326">Откройте **Index.cshtml** файла в Visual Studio, если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="02089-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="02089-327">Добавьте приведенный ниже код HTML в файл сразу после неупорядоченного списка, добавленного в предыдущей задаче.</span><span class="sxs-lookup"><span data-stu-id="02089-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="02089-328">В элементе скрипта, в нижней части документа добавьте выделенный ниже код для обработки события нажатия кнопки, которые будет отправлять данные веб-API с помощью вызова HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="02089-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="02089-329">В **ContactController.cs**, поместите точку останова на **Post** метод.</span><span class="sxs-lookup"><span data-stu-id="02089-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="02089-330">Нажмите клавишу **F5** для запуска приложения в браузере.</span><span class="sxs-lookup"><span data-stu-id="02089-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="02089-331">После загрузки страницы в браузере, введите имя нового контакта и идентификатор и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02089-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="02089-332">![Загружен документ клиента HTML в браузере](build-restful-apis-with-aspnet-web-api/_static/image24.png "загружен документ клиента HTML в браузере")</span><span class="sxs-lookup"><span data-stu-id="02089-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="02089-333">*Клиент HTML-документа, загруженной в браузере*</span><span class="sxs-lookup"><span data-stu-id="02089-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="02089-334">Когда в окне отладчика прерывается **Post** метод, просмотр свойств **обратитесь в службу** параметра.</span><span class="sxs-lookup"><span data-stu-id="02089-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="02089-335">Значения должны соответствовать данные, введенные в форме.</span><span class="sxs-lookup"><span data-stu-id="02089-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="02089-336">![Объект контакт, отправляются в веб-API из клиента](build-restful-apis-with-aspnet-web-api/_static/image25.png "объектов Contact, отправляемых веб-API из клиента")</span><span class="sxs-lookup"><span data-stu-id="02089-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="02089-337">*Объект контакт, отправляются в веб-API из клиента*</span><span class="sxs-lookup"><span data-stu-id="02089-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="02089-338">Шаг при помощи метода отладчик до **ответа** переменная создана.</span><span class="sxs-lookup"><span data-stu-id="02089-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="02089-339">После проверки в **"Локальные"** окно в отладчике, вы увидите что заданы все свойства.</span><span class="sxs-lookup"><span data-stu-id="02089-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="02089-340">![После создания в отладчике ответ](build-restful-apis-with-aspnet-web-api/_static/image26.png "ответа, после создания в отладчике")</span><span class="sxs-lookup"><span data-stu-id="02089-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="02089-341">*Ответ после создания в отладчике*</span><span class="sxs-lookup"><span data-stu-id="02089-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="02089-342">Если нажать клавишу **F5** или нажмите кнопку **Продолжить** в отладчике запрос будет выполнен.</span><span class="sxs-lookup"><span data-stu-id="02089-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="02089-343">После переключения обратно в браузер, новый контакт был добавлен в список контактов, хранящихся в **ContactRepository** реализации.</span><span class="sxs-lookup"><span data-stu-id="02089-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="02089-344">![Браузер отражает успешного создания нового экземпляра контактные](build-restful-apis-with-aspnet-web-api/_static/image27.png "браузер отражает успешного создания нового экземпляра контакта")</span><span class="sxs-lookup"><span data-stu-id="02089-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="02089-345">*Браузер отражает успешного создания нового экземпляра контакта*</span><span class="sxs-lookup"><span data-stu-id="02089-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="02089-346">Кроме того, можно развернуть это приложение для Azure следующих [приложение в: Публикация приложения ASP.NET MVC 4 с помощью веб-развертывания](#AppendixC).</span><span class="sxs-lookup"><span data-stu-id="02089-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="02089-347">Сводка</span><span class="sxs-lookup"><span data-stu-id="02089-347">Summary</span></span>

<span data-ttu-id="02089-348">Это лабораторное занятие был представлен на новую платформу веб-API ASP.NET и реализации Web API-интерфейсов RESTful с помощью платформы.</span><span class="sxs-lookup"><span data-stu-id="02089-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="02089-349">На этой странице можно создать новый репозиторий, который обеспечивает сохраняемость данных, используя любое количество механизмы и привязывания этой службы вместо того, простой, приведено в качестве примера в этой лабораторной работе.</span><span class="sxs-lookup"><span data-stu-id="02089-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="02089-350">Веб-API поддерживает несколько дополнительных функций, таких как включение подключения от клиентов отличающийся от HTML, написанных на любом языке, поддерживающем HTTP и JSON или XML.</span><span class="sxs-lookup"><span data-stu-id="02089-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="02089-351">Возможность размещения веб-API за пределами типичный веб-приложения можно также, а также является возможность создавать собственные форматы сериализации.</span><span class="sxs-lookup"><span data-stu-id="02089-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="02089-352">Веб-узла ASP.NET имеет выделенный в веб-API ASP.NET Framework в область [ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api).</span><span class="sxs-lookup"><span data-stu-id="02089-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="02089-353">Этот сайт будет продолжать последние сведения, примеры и новостей, относящихся к веб-API, поэтому она регулярно проверяйте Если вы хотите более подробно рассмотрим искусством создания пользовательского веб-API, доступных для framework практически с любого устройства или разработки.</span><span class="sxs-lookup"><span data-stu-id="02089-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="02089-354">Приложение а. Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="02089-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="02089-355">С помощью фрагментов кода у вас есть весь код, который требуется в вашем распоряжении.</span><span class="sxs-lookup"><span data-stu-id="02089-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="02089-356">Лаборатории документ поможет определить точно при их использовании, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="02089-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="02089-357">![Фрагменты кода Visual Studio, чтобы вставить код в проект](build-restful-apis-with-aspnet-web-api/_static/image28.png "фрагменты кода с помощью Visual Studio, чтобы вставить код в проект")</span><span class="sxs-lookup"><span data-stu-id="02089-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="02089-358">*Фрагменты кода Visual Studio, чтобы вставить код в проект*</span><span class="sxs-lookup"><span data-stu-id="02089-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="02089-359">Чтобы добавить фрагмент кода, с помощью клавиатуры (только C#)</span><span class="sxs-lookup"><span data-stu-id="02089-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="02089-360">Поместите курсор в место вставки кода.</span><span class="sxs-lookup"><span data-stu-id="02089-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="02089-361">Начните вводить имя фрагмента (без пробелов и дефисов).</span><span class="sxs-lookup"><span data-stu-id="02089-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="02089-362">Посмотрите, как IntelliSense отображает, совпадающие с именами фрагменты.</span><span class="sxs-lookup"><span data-stu-id="02089-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="02089-363">Выберите правильный фрагмент (или продолжите ввод, пока не будет выделен весь фрагмент имени).</span><span class="sxs-lookup"><span data-stu-id="02089-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="02089-364">Нажмите клавишу Tab дважды, чтобы вставить фрагмент в положении курсора.</span><span class="sxs-lookup"><span data-stu-id="02089-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="02089-365">![Начните вводить имя фрагмента](build-restful-apis-with-aspnet-web-api/_static/image29.png "начните вводить имя фрагмента")</span><span class="sxs-lookup"><span data-stu-id="02089-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="02089-366">*Начните вводить имя фрагмента*</span><span class="sxs-lookup"><span data-stu-id="02089-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="02089-367">![Нажмите клавишу Tab, чтобы выделить фрагмент в выделенный](build-restful-apis-with-aspnet-web-api/_static/image30.png "нажмите клавишу Tab, чтобы выделить выделенный фрагмент")</span><span class="sxs-lookup"><span data-stu-id="02089-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="02089-368">*Нажмите клавишу Tab, чтобы выделить выделенный фрагмент*</span><span class="sxs-lookup"><span data-stu-id="02089-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="02089-369">![Снова нажмите клавишу Tab и фрагмент будет расширяться](build-restful-apis-with-aspnet-web-api/_static/image31.png "еще раз нажмите клавишу Tab и фрагмент будет расширяться")</span><span class="sxs-lookup"><span data-stu-id="02089-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="02089-370">*Снова нажмите клавишу Tab и фрагмент будет расширяться*</span><span class="sxs-lookup"><span data-stu-id="02089-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="02089-371">Чтобы добавить фрагмент кода, с помощью мыши (C#, Visual Basic и XML)</span><span class="sxs-lookup"><span data-stu-id="02089-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="02089-372">Щелкните правой кнопкой мыши место для вставки фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="02089-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="02089-373">Выберите **вставить фрагмент** следуют **Мои фрагменты кода**.</span><span class="sxs-lookup"><span data-stu-id="02089-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="02089-374">Выберите соответствующий фрагмент из списка, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="02089-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="02089-375">![Щелкните правой кнопкой мыши, где необходимо вставить фрагмент кода и выберите Вставить фрагмент](build-restful-apis-with-aspnet-web-api/_static/image32.png "щелкните правой кнопкой мыши, где необходимо вставить фрагмент кода и выберите Вставить фрагмент")</span><span class="sxs-lookup"><span data-stu-id="02089-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="02089-376">*Щелкните правой кнопкой мыши место для вставки фрагмента кода и выберите Вставить фрагмент*</span><span class="sxs-lookup"><span data-stu-id="02089-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="02089-377">![Выберите соответствующий фрагмент из списка, щелкнув по ней](build-restful-apis-with-aspnet-web-api/_static/image33.png "выбрать соответствующий фрагмент из списка, щелкнув по ней")</span><span class="sxs-lookup"><span data-stu-id="02089-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="02089-378">*Выберите соответствующий фрагмент из списка, щелкнув по ней*</span><span class="sxs-lookup"><span data-stu-id="02089-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="02089-379">Приложение б. Установка Visual Studio Express 2012 для Web</span><span class="sxs-lookup"><span data-stu-id="02089-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="02089-380">Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версию с помощью **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="02089-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="02089-381">Приведенные ниже инструкции описывают действия, необходимые для установки *Visual studio Express 2012 для Web* с помощью *Microsoft Web Platform Installer*.</span><span class="sxs-lookup"><span data-stu-id="02089-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="02089-382">Перейдите к [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="02089-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="02089-383">Кроме того, если вы уже установили установщика веб-платформы, можно открыть его и выполните поиск продукта &quot; <em>Visual Studio Express 2012 для Web с пакетом Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="02089-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="02089-384">Щелкните **установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="02089-384">Click on **Install Now**.</span></span> <span data-ttu-id="02089-385">Если у вас нет **установщика веб-платформы** вы будете перенаправлены к сначала загрузить и установить его.</span><span class="sxs-lookup"><span data-stu-id="02089-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="02089-386">Один раз **установщика веб-платформы** открыт, нажмите кнопку **установить** для запуска программы установки.</span><span class="sxs-lookup"><span data-stu-id="02089-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="02089-387">![Установка Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "установка Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="02089-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="02089-388">*Установка Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="02089-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="02089-389">Прочтите лицензии и условия все продукты и нажмите кнопку **я принимаю** для продолжения.</span><span class="sxs-lookup"><span data-stu-id="02089-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Принятие условий лицензии](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="02089-391">*Принятие условий лицензии*</span><span class="sxs-lookup"><span data-stu-id="02089-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="02089-392">Подождите, пока не завершится процесс загрузки и установки.</span><span class="sxs-lookup"><span data-stu-id="02089-392">Wait until the downloading and installation process completes.</span></span>

    ![Ход установки](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="02089-394">*Ход выполнения установки*</span><span class="sxs-lookup"><span data-stu-id="02089-394">*Installation progress*</span></span>
6. <span data-ttu-id="02089-395">После завершения установки нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="02089-395">When the installation completes, click **Finish**.</span></span>

    ![Установка завершена](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="02089-397">*Установка завершена*</span><span class="sxs-lookup"><span data-stu-id="02089-397">*Installation completed*</span></span>
7. <span data-ttu-id="02089-398">Нажмите кнопку **выхода** закрыть установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="02089-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="02089-399">Чтобы открыть Visual Studio Express для Web, перейдите к **запустить** экрана и Займитесь написанием &quot; **VS Express**&quot;, нажмите кнопку на **VS Express для Web** Плитка.</span><span class="sxs-lookup"><span data-stu-id="02089-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express для Web плитки](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="02089-401">*VS Express для Web плитки*</span><span class="sxs-lookup"><span data-stu-id="02089-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="02089-402">Приложение c. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывания</span><span class="sxs-lookup"><span data-stu-id="02089-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="02089-403">В этом приложении показано, как создать новый веб-сайт на портале Azure и опубликовать приложение, полученный после лаборатории, используя преимущества компонентов публикации веб-развертывания, предоставляемые Azure.</span><span class="sxs-lookup"><span data-stu-id="02089-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="02089-404">Задача 1 - Создание нового веб-сайта с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="02089-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="02089-405">Перейдите к [портала управления Azure](https://manage.windowsazure.com/) и войдите с использованием учетных данных Майкрософт, связанную с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="02089-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="02089-406">С помощью Azure можно бесплатное размещение 10 веб-сайтов ASP.NET и затем масштабировать по мере увеличения объема трафика.</span><span class="sxs-lookup"><span data-stu-id="02089-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="02089-407">Вы можете зарегистрироваться [здесь](https://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="02089-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="02089-408">![Войдите на портал Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image39.png "Войдите на портал Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="02089-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="02089-409">*Войдите на портал*</span><span class="sxs-lookup"><span data-stu-id="02089-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="02089-410">Нажмите кнопку **New** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="02089-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="02089-411">![Создание нового веб-сайта](build-restful-apis-with-aspnet-web-api/_static/image40.png "создания нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="02089-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="02089-412">*Создание нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="02089-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="02089-413">Нажмите кнопку **вычислений** | **веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="02089-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="02089-414">Затем выберите **быстрое создание** параметр.</span><span class="sxs-lookup"><span data-stu-id="02089-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="02089-415">Укажите URL-адрес доступен для нового веб-сайта и нажмите кнопку **создать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="02089-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="02089-416">Azure является узлом для веб-приложение, работающее в облаке, вы можете управлять.</span><span class="sxs-lookup"><span data-stu-id="02089-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="02089-417">Быстрое создание позволяет развернуть завершенное веб-приложения в Azure из вне портала.</span><span class="sxs-lookup"><span data-stu-id="02089-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="02089-418">Он не включает действия по настройке базы данных.</span><span class="sxs-lookup"><span data-stu-id="02089-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="02089-419">![Создание нового веб-сайта, с помощью быстрого создания](build-restful-apis-with-aspnet-web-api/_static/image41.png "создания нового веб-сайта, с помощью быстрого создания")</span><span class="sxs-lookup"><span data-stu-id="02089-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="02089-420">*Создание нового веб-сайта, с помощью быстрого создания*</span><span class="sxs-lookup"><span data-stu-id="02089-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="02089-421">Подождите, пока новый **веб-сайт** создается.</span><span class="sxs-lookup"><span data-stu-id="02089-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="02089-422">После создания веб-сайт, щелкните ссылку под **URL-адрес** столбца.</span><span class="sxs-lookup"><span data-stu-id="02089-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="02089-423">Проверьте, что новый веб-сайт работает.</span><span class="sxs-lookup"><span data-stu-id="02089-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="02089-424">![Выбрав новый веб-сайт](build-restful-apis-with-aspnet-web-api/_static/image42.png "просмотра на новый веб-сайт")</span><span class="sxs-lookup"><span data-stu-id="02089-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="02089-425">*Выбрав новый веб-сайт*</span><span class="sxs-lookup"><span data-stu-id="02089-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="02089-426">![Веб-сайт работал](build-restful-apis-with-aspnet-web-api/_static/image43.png "веб-узлом")</span><span class="sxs-lookup"><span data-stu-id="02089-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="02089-427">*Веб-сайт под управлением*</span><span class="sxs-lookup"><span data-stu-id="02089-427">*Web site running*</span></span>
6. <span data-ttu-id="02089-428">Вернитесь на портал и щелкните имя веб-сайт в **имя** столбец для отображения страницы управления.</span><span class="sxs-lookup"><span data-stu-id="02089-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="02089-429">![Открытие страницы управления веб-сайт](build-restful-apis-with-aspnet-web-api/_static/image44.png "Открытие страницы управления веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="02089-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="02089-430">*Открытие страницы управления веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="02089-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="02089-431">В **панели мониторинга** раздела **быстрый обзор** щелкните **загрузить профиль публикации** ссылку.</span><span class="sxs-lookup"><span data-stu-id="02089-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="02089-432">*Профиль публикации* содержит все сведения, необходимые для публикации веб-приложения в Azure для каждого разрешенного метода публикации.</span><span class="sxs-lookup"><span data-stu-id="02089-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="02089-433">Профиль публикации содержит URL-адреса, учетные данные пользователя и строк базы данных, необходимых для подключения и проверку подлинности в каждой из конечных точек, для которых включена метода публикации.</span><span class="sxs-lookup"><span data-stu-id="02089-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="02089-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express для Web** и **Microsoft Visual Studio 2012** поддерживают чтение профилей публикации для автоматизации настройки из этих программ для Публикация веб-приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="02089-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="02089-435">![Профиль публикации веб-сайт загрузки](build-restful-apis-with-aspnet-web-api/_static/image45.png "профиль публикации веб-сайта загрузки")</span><span class="sxs-lookup"><span data-stu-id="02089-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="02089-436">*Профиль публикации веб-сайта загрузки*</span><span class="sxs-lookup"><span data-stu-id="02089-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="02089-437">Скачайте файл профиля публикации в известном месте.</span><span class="sxs-lookup"><span data-stu-id="02089-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="02089-438">Далее в этом упражнении показано, как использовать этот файл для публикации веб-приложения в Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02089-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="02089-439">![Сохранение файла профиля публикации](build-restful-apis-with-aspnet-web-api/_static/image46.png "Сохранение профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="02089-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="02089-440">*Сохранение файла профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="02089-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="02089-441">Задача 2 - Настройка сервера базы данных</span><span class="sxs-lookup"><span data-stu-id="02089-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="02089-442">Если приложение использует SQL Server, баз данных, необходимо будет создать сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="02089-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="02089-443">Эту задачу может пропустить, если вы хотите развернуть простое приложение, которое не использует SQL Server.</span><span class="sxs-lookup"><span data-stu-id="02089-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="02089-444">Вам потребуется сервер базы данных SQL для хранения базы данных приложения.</span><span class="sxs-lookup"><span data-stu-id="02089-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="02089-445">Серверы баз данных SQL можно просмотреть в своей подписке на портале управления Azure на **баз данных Sql** | **серверы** | **мониторинга сервера**.</span><span class="sxs-lookup"><span data-stu-id="02089-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="02089-446">Если у вас на сервер, созданный, можно создать его, используя **добавить** кнопки на панели команд.</span><span class="sxs-lookup"><span data-stu-id="02089-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="02089-447">Запишите **имя сервера и URL-адрес, имя входа администратора и пароль**, как их использование в следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="02089-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="02089-448">Не создавайте базы данных, так как он будет создан в более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="02089-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="02089-449">![Панель мониторинга базы данных SQL Server](build-restful-apis-with-aspnet-web-api/_static/image47.png "панель мониторинга базы данных SQL Server")</span><span class="sxs-lookup"><span data-stu-id="02089-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="02089-450">*Панель мониторинга базы данных SQL Server*</span><span class="sxs-lookup"><span data-stu-id="02089-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="02089-451">В следующей задаче вы проверите подключения к базе данных из Visual Studio по этой причине необходимо включить IP-адрес локального сервера списка **разрешенные IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="02089-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="02089-452">Чтобы сделать это, нажмите кнопку **Настройка**, выберите IP-адрес из **текущий IP-адрес клиента** и вставьте его на **начальный IP-адрес** и **конечный IP-адрес** текстовые поля и нажмите кнопку ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) кнопки.</span><span class="sxs-lookup"><span data-stu-id="02089-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![Добавление IP-адрес клиента](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="02089-454">*Добавление IP-адрес клиента*</span><span class="sxs-lookup"><span data-stu-id="02089-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="02089-455">Один раз **IP-адрес клиента** добавляется разрешенных IP-адресов выберите на **Сохранить** для подтверждения изменения.</span><span class="sxs-lookup"><span data-stu-id="02089-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Подтверждение изменений](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="02089-457">*Подтверждение изменений*</span><span class="sxs-lookup"><span data-stu-id="02089-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="02089-458">Задача 3 - публикация приложения ASP.NET MVC 4 с помощью веб-развертывания</span><span class="sxs-lookup"><span data-stu-id="02089-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="02089-459">Вернитесь к решению для ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="02089-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="02089-460">В **обозревателе решений**, щелкните правой кнопкой мыши проект веб-сайта и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="02089-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="02089-461">![Публикация приложения](build-restful-apis-with-aspnet-web-api/_static/image51.png "публикации приложения")</span><span class="sxs-lookup"><span data-stu-id="02089-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="02089-462">*Публикация веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="02089-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="02089-463">Импортируйте профиль публикации, сохраненный в первой задаче.</span><span class="sxs-lookup"><span data-stu-id="02089-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="02089-464">![Импорт профиля публикации](build-restful-apis-with-aspnet-web-api/_static/image52.png "Импорт профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="02089-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="02089-465">*Импорт профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="02089-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="02089-466">Нажмите кнопку **Проверка подключения**.</span><span class="sxs-lookup"><span data-stu-id="02089-466">Click **Validate Connection**.</span></span> <span data-ttu-id="02089-467">После завершения проверки нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="02089-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="02089-468">Проверка будет завершена, как только вы увидите зеленый флажок отображаться рядом с кнопкой проверить подключение.</span><span class="sxs-lookup"><span data-stu-id="02089-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="02089-469">![Проверка подключения](build-restful-apis-with-aspnet-web-api/_static/image53.png "Проверка подключения")</span><span class="sxs-lookup"><span data-stu-id="02089-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="02089-470">*Проверка подключения*</span><span class="sxs-lookup"><span data-stu-id="02089-470">*Validating connection*</span></span>
4. <span data-ttu-id="02089-471">В **параметры** раздела **баз данных** нажмите кнопку рядом с текстовое поле подключения к базе данных (т. е. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="02089-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="02089-472">![Конфигурация веб-развертывания](build-restful-apis-with-aspnet-web-api/_static/image54.png "конфигурация веб-развертывания")</span><span class="sxs-lookup"><span data-stu-id="02089-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="02089-473">*Конфигурация веб-развертывания*</span><span class="sxs-lookup"><span data-stu-id="02089-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="02089-474">Настройте подключение к базе данных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="02089-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="02089-475">В **имя_сервера** введите URL-адреса серверу базы данных SQL с помощью *tcp:* префикс.</span><span class="sxs-lookup"><span data-stu-id="02089-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="02089-476">В **имя пользователя** введите имя входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="02089-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="02089-477">В **пароль** введите пароль входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="02089-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="02089-478">Введите новое имя базы данных, например: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="02089-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="02089-479">![Настройка строки подключения назначения](build-restful-apis-with-aspnet-web-api/_static/image55.png "Настройка строка соединения с назначением")</span><span class="sxs-lookup"><span data-stu-id="02089-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="02089-480">*Настройка строки подключения назначения*</span><span class="sxs-lookup"><span data-stu-id="02089-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="02089-481">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="02089-481">Then click **OK**.</span></span> <span data-ttu-id="02089-482">При появлении запроса на создание базы данных нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="02089-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="02089-483">![Создание базы данных](build-restful-apis-with-aspnet-web-api/_static/image56.png "Создание строки базы данных")</span><span class="sxs-lookup"><span data-stu-id="02089-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="02089-484">*Создание базы данных*</span><span class="sxs-lookup"><span data-stu-id="02089-484">*Creating the database*</span></span>
7. <span data-ttu-id="02089-485">В текстовое поле подключение по умолчанию отображается строка подключения, который будет использоваться для подключения к базе данных SQL в Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="02089-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="02089-486">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="02089-486">Then click **Next**.</span></span>

    <span data-ttu-id="02089-487">![Строка подключения, указывающий на базу данных SQL](build-restful-apis-with-aspnet-web-api/_static/image57.png "строку подключения, указывающий на базу данных SQL")</span><span class="sxs-lookup"><span data-stu-id="02089-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="02089-488">*Строка подключения, указывающий на базу данных SQL*</span><span class="sxs-lookup"><span data-stu-id="02089-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="02089-489">В **предварительной версии** щелкните **публикации**.</span><span class="sxs-lookup"><span data-stu-id="02089-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="02089-490">![Публикация веб-приложения](build-restful-apis-with-aspnet-web-api/_static/image58.png "публикации веб-приложения")</span><span class="sxs-lookup"><span data-stu-id="02089-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="02089-491">*Публикация веб-приложения*</span><span class="sxs-lookup"><span data-stu-id="02089-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="02089-492">После завершения процесса публикации в браузере по умолчанию откроется опубликованного веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="02089-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="02089-493">![Приложение опубликовано в Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "публикации приложения в Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="02089-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="02089-494">*Приложение будет публиковаться в Azure*</span><span class="sxs-lookup"><span data-stu-id="02089-494">*Application published to Azure*</span></span>
