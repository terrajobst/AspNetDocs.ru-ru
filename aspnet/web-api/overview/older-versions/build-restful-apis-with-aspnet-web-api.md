---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: Создание API-интерфейсов RESTFUL с помощью веб-API ASP.NET ASP.NET 4. x
author: rick-anderson
description: Практическое занятие. Используйте веб-API в ASP.NET 4. x для создания простого REST API для приложения диспетчера контактов.
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504270"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="9474f-103">Создание API-интерфейсов RESTFUL с помощью веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9474f-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="9474f-104">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="9474f-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="9474f-105">Практическое занятие. Используйте веб-API в ASP.NET 4. x для создания простого REST API для приложения диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="9474f-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="9474f-106">Кроме того, будет построен клиент для использования API.</span><span class="sxs-lookup"><span data-stu-id="9474f-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="9474f-107">В последние годы он стал ясно, что HTTP не только обслуживает HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="9474f-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="9474f-108">Она также является мощной платформой для создания веб-API, используя несколько глаголов (GET, POST и т. д.) и несколько простых концепций, таких как *URI* и *заголовки*.</span><span class="sxs-lookup"><span data-stu-id="9474f-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="9474f-109">Веб-API ASP.NET — это набор компонентов, упрощающих программирование HTTP.</span><span class="sxs-lookup"><span data-stu-id="9474f-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="9474f-110">Поскольку она построена на базе среды выполнения MVC ASP.NET, веб-API автоматически обрабатывает данные транспорта низкого уровня по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="9474f-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="9474f-111">В то же время веб-API естественным образом предоставляет модель программирования HTTP.</span><span class="sxs-lookup"><span data-stu-id="9474f-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="9474f-112">На самом деле, одна из целей веб-API заключается в том, чтобы *не* приойти к реальности HTTP.</span><span class="sxs-lookup"><span data-stu-id="9474f-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="9474f-113">В результате веб-API является гибким и простым в расширении.</span><span class="sxs-lookup"><span data-stu-id="9474f-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="9474f-114">Архитектурный стиль «ОСТАЛЬной» стал эффективным способом использования протокола HTTP, хотя он, безусловно, не является единственным допустимым подходом к HTTP.</span><span class="sxs-lookup"><span data-stu-id="9474f-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="9474f-115">Диспетчер контактов будет предоставлять все остальное для перечисления, добавления и удаления контактов.</span><span class="sxs-lookup"><span data-stu-id="9474f-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="9474f-116">В этом лабораторном занятии требуется базовое понимание протокола HTTP, а также предполагается, что у вас есть основные знания о HTML, JavaScript и jQuery.</span><span class="sxs-lookup"><span data-stu-id="9474f-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="9474f-117">На веб-сайте ASP.NET есть область, выделенная для веб-API ASP.NET Framework на [https://asp.net/web-api](https://asp.net/web-api).</span><span class="sxs-lookup"><span data-stu-id="9474f-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="9474f-118">Этот сайт продолжит предоставлять последние сведения, примеры и новости, связанные с веб-API, поэтому регулярно проверяйте его, если вы хотите глубже изучить создание настраиваемых веб-API, доступных практически для любого устройства или платформы разработки.</span><span class="sxs-lookup"><span data-stu-id="9474f-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="9474f-119">Веб-API ASP.NET, как и в случае с ASP.NET MVC 4, имеет большую гибкость в плане разделения уровня служб от контроллеров, что позволяет легко использовать несколько доступных платформ внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="9474f-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="9474f-120">В MSDN есть хороший пример, демонстрирующий использование Нинжект для внедрения зависимостей в проект веб-API ASP.NET, который можно скачать [отсюда](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span><span class="sxs-lookup"><span data-stu-id="9474f-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="9474f-121">Все примеры кода и фрагментов включены в комплект обучающих курсов Web Camp, доступный по адресу [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="9474f-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="9474f-122">Цели</span><span class="sxs-lookup"><span data-stu-id="9474f-122">Objectives</span></span>

<span data-ttu-id="9474f-123">В этой практической лабораторной работе вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="9474f-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="9474f-124">Реализация веб-API RESTFUL</span><span class="sxs-lookup"><span data-stu-id="9474f-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="9474f-125">Вызов API из HTML-клиента</span><span class="sxs-lookup"><span data-stu-id="9474f-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="9474f-126">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9474f-126">Prerequisites</span></span>

<span data-ttu-id="9474f-127">Для выполнения этой практической лабораторной работы требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="9474f-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="9474f-128">[Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или старше (см. [Приложение B](#AppendixB) для получения инструкций по его установке).</span><span class="sxs-lookup"><span data-stu-id="9474f-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="9474f-129">Настройка</span><span class="sxs-lookup"><span data-stu-id="9474f-129">Setup</span></span>

<span data-ttu-id="9474f-130">**Установка фрагментов кода**</span><span class="sxs-lookup"><span data-stu-id="9474f-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="9474f-131">Для удобства большая часть кода, который вы будете управлять в этой лаборатории, доступна в виде фрагментов кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9474f-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="9474f-132">Чтобы установить фрагменты кода, запустите файл **.\саурце\сетуп\кодесниппетс.ВСИ** .</span><span class="sxs-lookup"><span data-stu-id="9474f-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="9474f-133">Если вы не знакомы с фрагментами кода Visual Studio Code и хотите узнать, как их использовать, см. приложение из этого документа &quot;[приложении а. Использование фрагментов кода](#AppendixA)&quot;.</span><span class="sxs-lookup"><span data-stu-id="9474f-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="9474f-134">Полнят</span><span class="sxs-lookup"><span data-stu-id="9474f-134">Exercises</span></span>

<span data-ttu-id="9474f-135">Эта практическая лабораторная работа включает в себя следующее упражнение:</span><span class="sxs-lookup"><span data-stu-id="9474f-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="9474f-136">Упражнение 1. Создание веб-API только для чтения</span><span class="sxs-lookup"><span data-stu-id="9474f-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="9474f-137">Упражнение 2. Создание веб-API для чтения и записи</span><span class="sxs-lookup"><span data-stu-id="9474f-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="9474f-138">Упражнение 3. Использование веб-API из клиента HTML</span><span class="sxs-lookup"><span data-stu-id="9474f-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="9474f-139">Каждое упражнение сопровождается **конечной** папкой, содержащей итоговое решение, которое следует получить после завершения упражнений.</span><span class="sxs-lookup"><span data-stu-id="9474f-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="9474f-140">Это решение можно использовать в качестве инструкции, если вам нужна дополнительная помощь по работе с упражнениями.</span><span class="sxs-lookup"><span data-stu-id="9474f-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="9474f-141">Предполагаемое время выполнения этой лабораторной работы: **60 минут**.</span><span class="sxs-lookup"><span data-stu-id="9474f-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="9474f-142">Упражнение 1. Создание веб-API только для чтения</span><span class="sxs-lookup"><span data-stu-id="9474f-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="9474f-143">В этом упражнении будут реализованы методы GET, доступные только для чтения для диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="9474f-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="9474f-144">Задача 1. Создание проекта API</span><span class="sxs-lookup"><span data-stu-id="9474f-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="9474f-145">В этой задаче вы будете использовать новые шаблоны веб-проектов ASP.NET для создания веб-приложения API.</span><span class="sxs-lookup"><span data-stu-id="9474f-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="9474f-146">Запустите **Visual Studio 2012 Express для Web**. для этого перейдите в раздел **запуск** и введите **VS Express для Web** нажмите клавишу **Ввод**.</span><span class="sxs-lookup"><span data-stu-id="9474f-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="9474f-147">В меню **файл** выберите пункт **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="9474f-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="9474f-148">Выберите **визуальный C# элемент | Тип веб-** проекта из древовидного представления типа проекта, а затем выберите тип проекта **веб-приложение ASP.NET MVC 4** .</span><span class="sxs-lookup"><span data-stu-id="9474f-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="9474f-149">Задайте для проекта **имя** *ContactManager* , а для параметра **имя решения** — *Начало*, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9474f-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="9474f-150">![Создание нового проекта веб-приложения ASP.NET MVC 4,0](build-restful-apis-with-aspnet-web-api/_static/image1.png "Создание нового проекта веб-приложения ASP.NET MVC 4,0")</span><span class="sxs-lookup"><span data-stu-id="9474f-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="9474f-151">*Создание нового проекта веб-приложения ASP.NET MVC 4,0*</span><span class="sxs-lookup"><span data-stu-id="9474f-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="9474f-152">В диалоговом окне Тип проекта ASP.NET MVC 4 Выберите тип проекта **веб-API** .</span><span class="sxs-lookup"><span data-stu-id="9474f-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="9474f-153">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9474f-153">Click **OK**.</span></span>

    <span data-ttu-id="9474f-154">![Указание типа проекта веб-API](build-restful-apis-with-aspnet-web-api/_static/image2.png "Указание типа проекта веб-API")</span><span class="sxs-lookup"><span data-stu-id="9474f-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="9474f-155">*Указание типа проекта веб-API*</span><span class="sxs-lookup"><span data-stu-id="9474f-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="9474f-156">Задача 2. Создание контроллеров API диспетчера контактов</span><span class="sxs-lookup"><span data-stu-id="9474f-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="9474f-157">В этой задаче будут созданы классы контроллеров, в которых будут размещаться методы API.</span><span class="sxs-lookup"><span data-stu-id="9474f-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="9474f-158">Удалите файл с именем **ValuesController.CS** в папке **Controllers** из проекта.</span><span class="sxs-lookup"><span data-stu-id="9474f-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="9474f-159">Щелкните правой кнопкой мыши папку **Controllers** в проекте и выберите **Добавить | Контроллер** из контекстного меню.</span><span class="sxs-lookup"><span data-stu-id="9474f-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="9474f-160">![Добавление нового контроллера в проект](build-restful-apis-with-aspnet-web-api/_static/image3.png "Добавление нового контроллера в проект")</span><span class="sxs-lookup"><span data-stu-id="9474f-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="9474f-161">*Добавление нового контроллера в проект*</span><span class="sxs-lookup"><span data-stu-id="9474f-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="9474f-162">В появившемся диалоговом окне **Добавление контроллера** в меню шаблон выберите пункт **пустой контроллер API** .</span><span class="sxs-lookup"><span data-stu-id="9474f-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="9474f-163">Назовите класс контроллера **контактконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="9474f-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="9474f-164">Затем нажмите кнопку **Добавить.**</span><span class="sxs-lookup"><span data-stu-id="9474f-164">Then, click **Add.**</span></span>

    <span data-ttu-id="9474f-165">![Использование диалогового окна "Добавление контроллера" для создания нового контроллера веб-API](build-restful-apis-with-aspnet-web-api/_static/image4.png "Использование диалогового окна "Добавление контроллера" для создания нового контроллера веб-API")</span><span class="sxs-lookup"><span data-stu-id="9474f-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="9474f-166">*Использование диалогового окна "Добавление контроллера" для создания нового контроллера веб-API*</span><span class="sxs-lookup"><span data-stu-id="9474f-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="9474f-167">Добавьте следующий код в **контактконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="9474f-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="9474f-168">(Фрагмент кода — *веб-API Lab-Ex01-Get метод API*)</span><span class="sxs-lookup"><span data-stu-id="9474f-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="9474f-169">Нажмите клавишу **F5** для запуска отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="9474f-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="9474f-170">Должна отобразиться домашняя страница по умолчанию для проекта веб-API.</span><span class="sxs-lookup"><span data-stu-id="9474f-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="9474f-171">![Домашняя страница по умолчанию веб-API ASP.NET приложения](build-restful-apis-with-aspnet-web-api/_static/image5.png "Домашняя страница по умолчанию веб-API ASP.NET приложения")</span><span class="sxs-lookup"><span data-stu-id="9474f-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="9474f-172">*Домашняя страница по умолчанию веб-API ASP.NET приложения*</span><span class="sxs-lookup"><span data-stu-id="9474f-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="9474f-173">В окне Internet Explorer нажмите клавишу **F12** , чтобы открыть окно **средства для разработчиков** .</span><span class="sxs-lookup"><span data-stu-id="9474f-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="9474f-174">Перейдите на вкладку **сеть** и нажмите кнопку **Start захватить (начать запись** ), чтобы начать запись сетевого трафика в окно.</span><span class="sxs-lookup"><span data-stu-id="9474f-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="9474f-175">![Открытие вкладки "сеть" и инициация записи в сеть](build-restful-apis-with-aspnet-web-api/_static/image6.png "Открытие вкладки "сеть" и инициация записи в сеть")</span><span class="sxs-lookup"><span data-stu-id="9474f-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="9474f-176">*Открытие вкладки "сеть" и инициация записи в сеть*</span><span class="sxs-lookup"><span data-stu-id="9474f-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="9474f-177">Добавьте URL-адрес в адресную строку браузера с помощью **/АПИ/контакт** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="9474f-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="9474f-178">Сведения о передаче будут отображаться в окне "запись сети".</span><span class="sxs-lookup"><span data-stu-id="9474f-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="9474f-179">Обратите внимание, что тип MIME ответа — **Application/JSON**.</span><span class="sxs-lookup"><span data-stu-id="9474f-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="9474f-180">Это показывает, как формат вывода по умолчанию — JSON.</span><span class="sxs-lookup"><span data-stu-id="9474f-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="9474f-181">![Просмотр выходных данных запроса веб-API в представлении сети](build-restful-apis-with-aspnet-web-api/_static/image7.png "Просмотр выходных данных запроса веб-API в представлении сети")</span><span class="sxs-lookup"><span data-stu-id="9474f-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="9474f-182">*Просмотр выходных данных запроса веб-API в представлении сети*</span><span class="sxs-lookup"><span data-stu-id="9474f-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9474f-183">По умолчанию Internet Explorer 10 получит запрос на сохранение или открытие потока, полученного при вызове веб-API.</span><span class="sxs-lookup"><span data-stu-id="9474f-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="9474f-184">Выходные данные будут представлять собой текстовый файл, содержащий результат JSON вызова URL веб-API.</span><span class="sxs-lookup"><span data-stu-id="9474f-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="9474f-185">Не отменяйте диалоговое окно, чтобы иметь возможность просматривать содержимое ответа через окно инструментов разработчиков.</span><span class="sxs-lookup"><span data-stu-id="9474f-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="9474f-186">Нажмите кнопку " **Перейти к подробному просмотру** ", чтобы просмотреть дополнительные сведения о ответе этого вызова API.</span><span class="sxs-lookup"><span data-stu-id="9474f-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="9474f-187">![Переключиться в подробное представление](build-restful-apis-with-aspnet-web-api/_static/image8.png "Переключиться в представление сведений")</span><span class="sxs-lookup"><span data-stu-id="9474f-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="9474f-188">*Переключиться в подробное представление*</span><span class="sxs-lookup"><span data-stu-id="9474f-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="9474f-189">Щелкните вкладку **текст ответа** , чтобы просмотреть фактический текст ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="9474f-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="9474f-190">![Просмотр выходного текста JSON в сетевом мониторе](build-restful-apis-with-aspnet-web-api/_static/image9.png "Просмотр выходного текста JSON в сетевом мониторе")</span><span class="sxs-lookup"><span data-stu-id="9474f-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="9474f-191">*Просмотр выходного текста JSON в сетевом мониторе*</span><span class="sxs-lookup"><span data-stu-id="9474f-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="9474f-192">Задача 3. Создание моделей контактов и дополнение контактного контроллера</span><span class="sxs-lookup"><span data-stu-id="9474f-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="9474f-193">В этой задаче будут созданы классы контроллеров, в которых будут размещаться методы API.</span><span class="sxs-lookup"><span data-stu-id="9474f-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="9474f-194">Щелкните правой кнопкой мыши папку **модели** и выберите **Добавить | Класс...** в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="9474f-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="9474f-195">![Добавление новой модели в веб-приложение](build-restful-apis-with-aspnet-web-api/_static/image10.png "Добавление новой модели в веб-приложение")</span><span class="sxs-lookup"><span data-stu-id="9474f-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="9474f-196">*Добавление новой модели в веб-приложение*</span><span class="sxs-lookup"><span data-stu-id="9474f-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="9474f-197">В диалоговом окне **Добавление нового элемента** назовите новый файл **Contact.CS** и нажмите кнопку **Добавить.**</span><span class="sxs-lookup"><span data-stu-id="9474f-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="9474f-198">![Создание нового файла класса Contact](build-restful-apis-with-aspnet-web-api/_static/image11.png "Создание нового файла класса Contact")</span><span class="sxs-lookup"><span data-stu-id="9474f-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="9474f-199">*Создание нового файла класса Contact*</span><span class="sxs-lookup"><span data-stu-id="9474f-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="9474f-200">Добавьте выделенный ниже код в класс **Contact** .</span><span class="sxs-lookup"><span data-stu-id="9474f-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="9474f-201">(Фрагмент кода — *веб-API Lab — Ex01 — класс Contact*)</span><span class="sxs-lookup"><span data-stu-id="9474f-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="9474f-202">В классе **контактконтроллер** выберите слово **строка** в определении метода **Get** и введите слово *Contact*.</span><span class="sxs-lookup"><span data-stu-id="9474f-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="9474f-203">После того как слово введено, в начале **контакта**слова появится индикатор.</span><span class="sxs-lookup"><span data-stu-id="9474f-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="9474f-204">Либо удерживайте нажатой клавишу **CTRL** , либо нажмите клавишу точка (.) или щелкните значок с помощью мыши, чтобы открыть диалоговое окно помощи в редакторе кода, чтобы автоматически заполнить директиву **using** для пространства имен Models.</span><span class="sxs-lookup"><span data-stu-id="9474f-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![Использование справки IntelliSense для объявлений пространств имен](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="9474f-206">*Использование справки IntelliSense для объявлений пространств имен*</span><span class="sxs-lookup"><span data-stu-id="9474f-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="9474f-207">Измените код для метода **Get** таким образом, чтобы он возвращал массив экземпляров модели связи.</span><span class="sxs-lookup"><span data-stu-id="9474f-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="9474f-208">(Фрагмент кода — *веб-API Lab — Ex01 — Возврат списка контактов*)</span><span class="sxs-lookup"><span data-stu-id="9474f-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="9474f-209">Нажмите клавишу **F5** для отладки веб-приложения в браузере.</span><span class="sxs-lookup"><span data-stu-id="9474f-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="9474f-210">Чтобы просмотреть изменения, внесенные в выходные данные ответа API, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9474f-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="9474f-211">После открытия браузера нажмите клавишу **F12** , если средства разработчика еще не открыты.</span><span class="sxs-lookup"><span data-stu-id="9474f-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="9474f-212">Перейдите на вкладку **сеть** .</span><span class="sxs-lookup"><span data-stu-id="9474f-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="9474f-213">Нажмите кнопку **начать запись** .</span><span class="sxs-lookup"><span data-stu-id="9474f-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="9474f-214">Добавьте URL-суффикс **/АПИ/контакт** к URL-адресу в адресной строке и нажмите клавишу **Ввод** .</span><span class="sxs-lookup"><span data-stu-id="9474f-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="9474f-215">Нажмите кнопку **Перейти к подробному просмотру** .</span><span class="sxs-lookup"><span data-stu-id="9474f-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="9474f-216">Перейдите на вкладку **текст ответа** . Должна отобразиться строка JSON, представляющая сериализованную форму массива экземпляров контакта.</span><span class="sxs-lookup"><span data-stu-id="9474f-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="9474f-217">![Сериализованные выходные данные JSON вызова сложного метода веб-API](build-restful-apis-with-aspnet-web-api/_static/image13.png "Сериализованные выходные данные JSON вызова сложного метода веб-API")</span><span class="sxs-lookup"><span data-stu-id="9474f-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="9474f-218">*Сериализованные выходные данные JSON вызова сложного метода веб-API*</span><span class="sxs-lookup"><span data-stu-id="9474f-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="9474f-219">Задача 4. Извлечение функциональных возможностей в слой служб</span><span class="sxs-lookup"><span data-stu-id="9474f-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="9474f-220">В этой задаче будет продемонстрировано, как извлечь функциональные возможности в слой служб, чтобы разработчикам было проще отделить функциональность служб от уровня контроллера, таким образом обеспечивая возможность повторного использования служб, которые реально выполняют работу.</span><span class="sxs-lookup"><span data-stu-id="9474f-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="9474f-221">Создайте новую папку в корне решения и назовите ее **Services**.</span><span class="sxs-lookup"><span data-stu-id="9474f-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="9474f-222">Для этого щелкните правой кнопкой мыши проект **ContactManager** , выберите **Добавить** | **создать папку**, назовите *службы*.</span><span class="sxs-lookup"><span data-stu-id="9474f-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="9474f-223">![Создание папки служб](build-restful-apis-with-aspnet-web-api/_static/image14.png "Создание папки служб")</span><span class="sxs-lookup"><span data-stu-id="9474f-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="9474f-224">*Создание папки служб*</span><span class="sxs-lookup"><span data-stu-id="9474f-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="9474f-225">Щелкните правой кнопкой мыши папку **службы** и выберите команду **Добавить | Класс...** в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="9474f-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="9474f-226">![Добавление нового класса в папку "службы"](build-restful-apis-with-aspnet-web-api/_static/image15.png "Добавление нового класса в папку "службы"")</span><span class="sxs-lookup"><span data-stu-id="9474f-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="9474f-227">*Добавление нового класса в папку "службы"*</span><span class="sxs-lookup"><span data-stu-id="9474f-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="9474f-228">Когда появится диалоговое окно **Добавление нового элемента** , назовите новый класс **ContactRepository** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="9474f-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="9474f-229">![Создание файла класса, содержащего код для уровня службы репозитория контактов](build-restful-apis-with-aspnet-web-api/_static/image16.png "Создание файла класса, содержащего код для уровня службы репозитория контактов")</span><span class="sxs-lookup"><span data-stu-id="9474f-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="9474f-230">*Создание файла класса, содержащего код для уровня службы репозитория контактов*</span><span class="sxs-lookup"><span data-stu-id="9474f-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="9474f-231">Добавьте директиву using в файл **ContactRepository.CS** , чтобы включить пространство имен Models.</span><span class="sxs-lookup"><span data-stu-id="9474f-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="9474f-232">Добавьте следующий выделенный код в файл **ContactRepository.CS** для реализации метода жеталлконтактс.</span><span class="sxs-lookup"><span data-stu-id="9474f-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="9474f-233">(Фрагмент кода — *веб-API Lab — Ex01 — репозиторий контактов*)</span><span class="sxs-lookup"><span data-stu-id="9474f-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="9474f-234">Откройте файл **ContactController.CS** , если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="9474f-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="9474f-235">Добавьте следующий оператор using в раздел объявления пространства имен файла.</span><span class="sxs-lookup"><span data-stu-id="9474f-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="9474f-236">Добавьте следующий выделенный код в класс **ContactController.CS** , чтобы добавить закрытое поле для представления экземпляра репозитория, чтобы остальные члены класса могли использовать реализацию службы.</span><span class="sxs-lookup"><span data-stu-id="9474f-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="9474f-237">(Фрагмент кода — *веб-API Lab — Ex01 — контактный контроллер*)</span><span class="sxs-lookup"><span data-stu-id="9474f-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="9474f-238">Измените метод **Get** таким образом, чтобы он использовал службу репозитория контактов.</span><span class="sxs-lookup"><span data-stu-id="9474f-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="9474f-239">(Фрагмент кода — *веб-API Lab — Ex01 — Возврат списка контактов через репозиторий*)</span><span class="sxs-lookup"><span data-stu-id="9474f-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="9474f-240">Установите точку останова в определении метода **Get** **контактконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="9474f-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="9474f-241">![Добавление точек останова в контактный контроллер](build-restful-apis-with-aspnet-web-api/_static/image17.png "Добавление точек останова в контактный контроллер")</span><span class="sxs-lookup"><span data-stu-id="9474f-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="9474f-242">*Добавление точек останова в контактный контроллер*</span><span class="sxs-lookup"><span data-stu-id="9474f-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="9474f-243">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="9474f-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="9474f-244">Когда откроется браузер, нажмите клавишу **F12** , чтобы открыть средства разработчика.</span><span class="sxs-lookup"><span data-stu-id="9474f-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="9474f-245">Перейдите на вкладку **сеть** .</span><span class="sxs-lookup"><span data-stu-id="9474f-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="9474f-246">Нажмите кнопку **начать запись** .</span><span class="sxs-lookup"><span data-stu-id="9474f-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="9474f-247">Добавьте URL-адрес в адресную строку с суффиксом **/АПИ/контакт** и нажмите клавишу **Ввод** , чтобы загрузить контроллер API.</span><span class="sxs-lookup"><span data-stu-id="9474f-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="9474f-248">Visual Studio 2012 должна прерываться после начала выполнения метода **Get** .</span><span class="sxs-lookup"><span data-stu-id="9474f-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="9474f-249">![Прерывание в методе Get](build-restful-apis-with-aspnet-web-api/_static/image18.png "Прерывание в методе Get")</span><span class="sxs-lookup"><span data-stu-id="9474f-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="9474f-250">*Прерывание в методе Get*</span><span class="sxs-lookup"><span data-stu-id="9474f-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="9474f-251">Нажмите клавишу **F5**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="9474f-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="9474f-252">Вернитесь в Internet Explorer, если он еще не находится в фокусе.</span><span class="sxs-lookup"><span data-stu-id="9474f-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="9474f-253">Обратите внимание на окно записи в сеть.</span><span class="sxs-lookup"><span data-stu-id="9474f-253">Note the network capture window.</span></span>

    <span data-ttu-id="9474f-254">![Представление "сеть" в Internet Explorer, отображающее результаты вызова веб-API](build-restful-apis-with-aspnet-web-api/_static/image19.png "Представление "сеть" в Internet Explorer, отображающее результаты вызова веб-API")</span><span class="sxs-lookup"><span data-stu-id="9474f-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="9474f-255">*Представление "сеть" в Internet Explorer, отображающее результаты вызова веб-API*</span><span class="sxs-lookup"><span data-stu-id="9474f-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="9474f-256">Нажмите кнопку " **Перейти к подробному просмотру** ".</span><span class="sxs-lookup"><span data-stu-id="9474f-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="9474f-257">Перейдите на вкладку **текст ответа** . Обратите внимание на выходные данные JSON вызова API и на то, как он представляет два контакта, полученные слоем служб.</span><span class="sxs-lookup"><span data-stu-id="9474f-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="9474f-258">![Просмотр выходных данных JSON из веб-API в окне средств разработчика](build-restful-apis-with-aspnet-web-api/_static/image20.png "Просмотр выходных данных JSON из веб-API в окне средств разработчика")</span><span class="sxs-lookup"><span data-stu-id="9474f-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="9474f-259">*Просмотр выходных данных JSON из веб-API в окне средств разработчика*</span><span class="sxs-lookup"><span data-stu-id="9474f-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="9474f-260">Упражнение 2. Создание веб-API для чтения и записи</span><span class="sxs-lookup"><span data-stu-id="9474f-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="9474f-261">В этом упражнении будут реализованы методы POST и постановки для диспетчера контактов, чтобы включить его с помощью функций редактирования данных.</span><span class="sxs-lookup"><span data-stu-id="9474f-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="9474f-262">Задача 1. Открытие проекта веб-API</span><span class="sxs-lookup"><span data-stu-id="9474f-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="9474f-263">В этой задаче вы будете готовы усовершенствовать проект веб-API, созданный в упражнении 1, чтобы он мог принимать данные, вводимые пользователем.</span><span class="sxs-lookup"><span data-stu-id="9474f-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="9474f-264">Запустите **Visual Studio 2012 Express для Web**. для этого перейдите в раздел **запуск** и введите **VS Express для Web** нажмите клавишу **Ввод**.</span><span class="sxs-lookup"><span data-stu-id="9474f-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="9474f-265">Откройте **Начальное** решение, расположенное по адресу **Source/Ex02-реадвритевебапи/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="9474f-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="9474f-266">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="9474f-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="9474f-267">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="9474f-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="9474f-268">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9474f-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="9474f-269">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="9474f-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="9474f-270">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="9474f-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9474f-271">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="9474f-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="9474f-272">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="9474f-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="9474f-273">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9474f-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="9474f-274">Откройте файл **Services/ContactRepository. CS** .</span><span class="sxs-lookup"><span data-stu-id="9474f-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="9474f-275">Задача 2. Добавление функций сохраняемости данных в реализацию репозитория контактов</span><span class="sxs-lookup"><span data-stu-id="9474f-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="9474f-276">В этой задаче вы дополните класс ContactRepository проекта веб-API, созданного в упражнении 1, чтобы он мог сохранять и принимать введенные пользователем данные и новые экземпляры контактов.</span><span class="sxs-lookup"><span data-stu-id="9474f-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="9474f-277">Добавьте следующую константу в класс **ContactRepository** для представления имени ключа элемента кэша веб-сервера далее в этом упражнении.</span><span class="sxs-lookup"><span data-stu-id="9474f-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="9474f-278">Добавьте конструктор в **ContactRepository** , содержащий следующий код.</span><span class="sxs-lookup"><span data-stu-id="9474f-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="9474f-279">(Фрагмент кода — *веб-API Lab-Ex02-конструктор репозитория*)</span><span class="sxs-lookup"><span data-stu-id="9474f-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="9474f-280">Измените код метода **жеталлконтактс** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9474f-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="9474f-281">(Фрагмент кода — *веб-API Lab — Ex02 — получение всех контактов*)</span><span class="sxs-lookup"><span data-stu-id="9474f-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="9474f-282">Этот пример предназначен для демонстрационных целей и будет использовать кэш веб-сервера в качестве среды хранения, чтобы значения были доступны нескольким клиентам одновременно, вместо использования механизма хранения сеанса или времени существования хранилища запросов.</span><span class="sxs-lookup"><span data-stu-id="9474f-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="9474f-283">Можно использовать Entity Framework, хранилище XML или любые другие разнообразные вместо кэша веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="9474f-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="9474f-284">Реализуйте новый метод с именем **савеконтакт** для класса **ContactRepository** , чтобы выполнить действия по сохранению контакта.</span><span class="sxs-lookup"><span data-stu-id="9474f-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="9474f-285">Метод **савеконтакт** должен принимать один параметр **Contact** и возвращать логическое значение, указывающее на успешное выполнение или сбой.</span><span class="sxs-lookup"><span data-stu-id="9474f-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="9474f-286">(Фрагмент кода — *веб-API Lab-Ex02 — реализация метода савеконтакт*)</span><span class="sxs-lookup"><span data-stu-id="9474f-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="9474f-287">Упражнение 3. Использование веб-API из клиента HTML</span><span class="sxs-lookup"><span data-stu-id="9474f-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="9474f-288">В этом упражнении вам предстоит создать HTML-клиент для вызова Web API.</span><span class="sxs-lookup"><span data-stu-id="9474f-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="9474f-289">Этот клиент упрощает обмен данными с веб-API с помощью JavaScript и отображает результаты в веб-браузере с помощью разметки HTML.</span><span class="sxs-lookup"><span data-stu-id="9474f-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="9474f-290">Задача 1. изменение представления индекса для предоставления графического пользовательского интерфейса для отображения контактов</span><span class="sxs-lookup"><span data-stu-id="9474f-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="9474f-291">В этой задаче будет изменено представление индекса по умолчанию веб-приложения для поддержки требования отображения списка существующих контактов в HTML-браузере.</span><span class="sxs-lookup"><span data-stu-id="9474f-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="9474f-292">Откройте **Visual Studio 2012 Express для Web** , если она еще не открыта.</span><span class="sxs-lookup"><span data-stu-id="9474f-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="9474f-293">Откройте **Начальное** решение, расположенное по адресу **Source/Ex03-консумингвебапи/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="9474f-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="9474f-294">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="9474f-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="9474f-295">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="9474f-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="9474f-296">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9474f-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="9474f-297">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="9474f-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="9474f-298">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="9474f-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9474f-299">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="9474f-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="9474f-300">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="9474f-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="9474f-301">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9474f-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="9474f-302">Откройте файл **index. cshtml** , расположенный в папке **Views/Home** .</span><span class="sxs-lookup"><span data-stu-id="9474f-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="9474f-303">Замените код HTML в элементе div на **текст** идентификатора, чтобы он выглядел как следующий код.</span><span class="sxs-lookup"><span data-stu-id="9474f-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="9474f-304">Добавьте следующий код JavaScript в нижнюю часть файла, чтобы выполнить HTTP-запрос к Web API.</span><span class="sxs-lookup"><span data-stu-id="9474f-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="9474f-305">Откройте файл **ContactController.CS** , если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="9474f-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="9474f-306">Поместите точку останова в метод **Get** класса **контактконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="9474f-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="9474f-307">![Размещение точки останова в методе Get контроллера API](build-restful-apis-with-aspnet-web-api/_static/image21.png "Размещение точки останова в методе Get контроллера API")</span><span class="sxs-lookup"><span data-stu-id="9474f-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="9474f-308">*Размещение точки останова в методе Get контроллера API*</span><span class="sxs-lookup"><span data-stu-id="9474f-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="9474f-309">Нажмите клавишу **F5**, чтобы запустить проект.</span><span class="sxs-lookup"><span data-stu-id="9474f-309">Press **F5** to run the project.</span></span> <span data-ttu-id="9474f-310">Браузер загрузит HTML-документ.</span><span class="sxs-lookup"><span data-stu-id="9474f-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9474f-311">Убедитесь, что вы посещаете корневой URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="9474f-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="9474f-312">После загрузки страницы и выполнения JavaScript будет достигнута точка останова, и выполнение кода будет приостановлено в контроллере.</span><span class="sxs-lookup"><span data-stu-id="9474f-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="9474f-313">![Отладка в вызовах веб-API с помощью VS Express для Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Отладка в вызовах веб-API с помощью VS Express для Web")</span><span class="sxs-lookup"><span data-stu-id="9474f-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="9474f-314">*Отладка в вызове веб-API с помощью Visual Studio 2012 Express для Web*</span><span class="sxs-lookup"><span data-stu-id="9474f-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="9474f-315">Удалите точку останова и нажмите клавишу **F5** или кнопку **Continue** на панели инструментов отладки, чтобы продолжить загрузку представления в браузере.</span><span class="sxs-lookup"><span data-stu-id="9474f-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="9474f-316">После завершения вызова веб-API вы должны увидеть контакты, возвращенные из вызова веб-API, отображаемые как элементы списка в браузере.</span><span class="sxs-lookup"><span data-stu-id="9474f-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="9474f-317">![Результаты вызова API, отображаемого в браузере как элементы списка](build-restful-apis-with-aspnet-web-api/_static/image23.png "Результаты вызова API, отображаемого в браузере как элементы списка")</span><span class="sxs-lookup"><span data-stu-id="9474f-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="9474f-318">*Результаты вызова API, отображаемого в браузере как элементы списка*</span><span class="sxs-lookup"><span data-stu-id="9474f-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="9474f-319">Остановите отладку.</span><span class="sxs-lookup"><span data-stu-id="9474f-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="9474f-320">Задача 2. изменение представления индекса для предоставления графического пользовательского интерфейса для создания контактов</span><span class="sxs-lookup"><span data-stu-id="9474f-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="9474f-321">В этой задаче будет продолжаться изменение представления индекса приложения MVC.</span><span class="sxs-lookup"><span data-stu-id="9474f-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="9474f-322">На страницу HTML будет добавлена форма, которая будет записывать вводимые пользователем данные и передавать их в веб-API для создания нового контакта, и будет создан новый метод контроллера веб-API для сбора данных о дате из графического интерфейса пользователя.</span><span class="sxs-lookup"><span data-stu-id="9474f-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="9474f-323">Откройте файл **ContactController.CS** .</span><span class="sxs-lookup"><span data-stu-id="9474f-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="9474f-324">Добавьте новый метод в класс контроллера с именем **POST** , как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="9474f-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="9474f-325">(Фрагмент кода — *метод веб-API Lab-Ex03-POST*)</span><span class="sxs-lookup"><span data-stu-id="9474f-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="9474f-326">Откройте файл **index. cshtml** в Visual Studio, если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="9474f-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="9474f-327">Добавьте приведенный ниже код HTML в файл сразу после неупорядоченного списка, добавленного в предыдущей задаче.</span><span class="sxs-lookup"><span data-stu-id="9474f-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="9474f-328">В элементе script в нижней части документа добавьте следующий выделенный код для управления событиями нажатия кнопки, которые будут отправлять данные в веб-API с помощью вызова HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="9474f-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="9474f-329">В **ContactController.CS**разместите точку останова в методе **POST** .</span><span class="sxs-lookup"><span data-stu-id="9474f-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="9474f-330">Нажмите клавишу **F5** , чтобы запустить приложение в браузере.</span><span class="sxs-lookup"><span data-stu-id="9474f-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="9474f-331">После загрузки страницы в браузере введите новое имя и идентификатор контакта и нажмите кнопку **сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9474f-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="9474f-332">![Клиентский HTML-документ, загруженный в браузере](build-restful-apis-with-aspnet-web-api/_static/image24.png "Клиентский HTML-документ, загруженный в браузере")</span><span class="sxs-lookup"><span data-stu-id="9474f-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="9474f-333">*Клиентский HTML-документ, загруженный в браузере*</span><span class="sxs-lookup"><span data-stu-id="9474f-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="9474f-334">Когда окно отладчика останавливается в методе **POST** , просмотрите свойства параметра **Contact** .</span><span class="sxs-lookup"><span data-stu-id="9474f-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="9474f-335">Значения должны соответствовать данным, введенным в форме.</span><span class="sxs-lookup"><span data-stu-id="9474f-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="9474f-336">![Объект Contact, отправляемый в веб-API из клиента](build-restful-apis-with-aspnet-web-api/_static/image25.png "Объект Contact, отправляемый в веб-API из клиента")</span><span class="sxs-lookup"><span data-stu-id="9474f-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="9474f-337">*Объект Contact, отправляемый в веб-API из клиента*</span><span class="sxs-lookup"><span data-stu-id="9474f-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="9474f-338">Пошаговое выполнение метода в отладчике до создания переменной **ответа** .</span><span class="sxs-lookup"><span data-stu-id="9474f-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="9474f-339">После проверки в окне " **локальные** " отладчика вы увидите, что установлены все свойства.</span><span class="sxs-lookup"><span data-stu-id="9474f-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="9474f-340">![Ответ, следующий за созданием в отладчике](build-restful-apis-with-aspnet-web-api/_static/image26.png "Ответ, следующий за созданием в отладчике")</span><span class="sxs-lookup"><span data-stu-id="9474f-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="9474f-341">*Ответ, следующий за созданием в отладчике*</span><span class="sxs-lookup"><span data-stu-id="9474f-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="9474f-342">Если нажать клавишу **F5** или нажать кнопку **продолжить** в отладчике, запрос будет выполнен.</span><span class="sxs-lookup"><span data-stu-id="9474f-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="9474f-343">После переключения обратно в браузер новый контакт будет добавлен в список контактов, сохраненных реализацией **ContactRepository** .</span><span class="sxs-lookup"><span data-stu-id="9474f-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="9474f-344">![Браузер отражает успешное создание нового экземпляра контакта](build-restful-apis-with-aspnet-web-api/_static/image27.png "Браузер отражает успешное создание нового экземпляра контакта")</span><span class="sxs-lookup"><span data-stu-id="9474f-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="9474f-345">*Браузер отражает успешное создание нового экземпляра контакта*</span><span class="sxs-lookup"><span data-stu-id="9474f-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="9474f-346">Кроме того, это приложение можно развернуть в Azure в [приложении C: Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание](#AppendixC).</span><span class="sxs-lookup"><span data-stu-id="9474f-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="9474f-347">Сводка</span><span class="sxs-lookup"><span data-stu-id="9474f-347">Summary</span></span>

<span data-ttu-id="9474f-348">В этом лабораторном занятии введена новая платформа веб-API ASP.NET и реализация веб-API RESTFUL с помощью платформы.</span><span class="sxs-lookup"><span data-stu-id="9474f-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="9474f-349">Здесь можно создать новый репозиторий, который упрощает сохранение данных с помощью любого количества механизмов и сети, которые обслуживаются, а не простой, как в примере в этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="9474f-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="9474f-350">Веб-API поддерживает ряд дополнительных функций, таких как включение взаимодействия от клиентов, отличных от HTML, написанных на любом языке, поддерживающем HTTP и JSON или XML.</span><span class="sxs-lookup"><span data-stu-id="9474f-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="9474f-351">Возможность размещения веб-API за пределами обычного веб-приложения также возможна, а также позволяет создавать собственные форматы сериализации.</span><span class="sxs-lookup"><span data-stu-id="9474f-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="9474f-352">На веб-сайте ASP.NET есть область, выделенная для веб-API ASP.NET Framework на [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span><span class="sxs-lookup"><span data-stu-id="9474f-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="9474f-353">Этот сайт продолжит предоставлять последние сведения, примеры и новости, связанные с веб-API, поэтому регулярно проверяйте его, если вы хотите глубже изучить создание настраиваемых веб-API, доступных практически для любого устройства или платформы разработки.</span><span class="sxs-lookup"><span data-stu-id="9474f-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="9474f-354">Приложение а. Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="9474f-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="9474f-355">С помощью фрагментов кода вы можете получить все необходимые вам коды.</span><span class="sxs-lookup"><span data-stu-id="9474f-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="9474f-356">В лабораторном документе вы узнаете, когда можно использовать их, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="9474f-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="9474f-357">![Использование фрагментов кода Visual Studio для вставки кода в проект](build-restful-apis-with-aspnet-web-api/_static/image28.png "Использование фрагментов кода Visual Studio для вставки кода в проект")</span><span class="sxs-lookup"><span data-stu-id="9474f-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="9474f-358">*Использование фрагментов кода Visual Studio для вставки кода в проект*</span><span class="sxs-lookup"><span data-stu-id="9474f-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="9474f-359">Добавление фрагмента кода с помощью клавиатуры (C# только)</span><span class="sxs-lookup"><span data-stu-id="9474f-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="9474f-360">Поместите курсор в то место, куда вы хотите вставить код.</span><span class="sxs-lookup"><span data-stu-id="9474f-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="9474f-361">Начните вводить имя фрагмента (без пробелов или дефисов).</span><span class="sxs-lookup"><span data-stu-id="9474f-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="9474f-362">Посмотрите, как IntelliSense отображает соответствующие имена фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="9474f-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="9474f-363">Выберите правильный фрагмент кода (или вводите его, пока не будет выбрано имя всего фрагмента).</span><span class="sxs-lookup"><span data-stu-id="9474f-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="9474f-364">Дважды нажмите клавишу TAB, чтобы вставить фрагмент в позицию курсора.</span><span class="sxs-lookup"><span data-stu-id="9474f-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="9474f-365">![Начните вводить имя фрагмента](build-restful-apis-with-aspnet-web-api/_static/image29.png "Начните вводить имя фрагмента")</span><span class="sxs-lookup"><span data-stu-id="9474f-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="9474f-366">*Начните вводить имя фрагмента*</span><span class="sxs-lookup"><span data-stu-id="9474f-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="9474f-367">![Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.](build-restful-apis-with-aspnet-web-api/_static/image30.png "Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="9474f-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="9474f-368">*Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="9474f-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="9474f-369">![Снова нажмите клавишу TAB, и фрагмент развернется](build-restful-apis-with-aspnet-web-api/_static/image31.png "Снова нажмите клавишу TAB, и фрагмент развернется")</span><span class="sxs-lookup"><span data-stu-id="9474f-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="9474f-370">*Снова нажмите клавишу TAB, и фрагмент развернется*</span><span class="sxs-lookup"><span data-stu-id="9474f-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="9474f-371">Добавление фрагмента кода с помощью мыши (C#, Visual Basic и XML)</span><span class="sxs-lookup"><span data-stu-id="9474f-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="9474f-372">Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="9474f-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="9474f-373">Выберите **Вставить фрагмент** , за которым следуют **фрагменты кода**.</span><span class="sxs-lookup"><span data-stu-id="9474f-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="9474f-374">Выберите соответствующий фрагмент из списка, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="9474f-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="9474f-375">![Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.](build-restful-apis-with-aspnet-web-api/_static/image32.png "Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="9474f-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="9474f-376">*Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="9474f-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="9474f-377">![Выберите соответствующий фрагмент из списка, щелкнув его.](build-restful-apis-with-aspnet-web-api/_static/image33.png "Выберите соответствующий фрагмент из списка, щелкнув его.")</span><span class="sxs-lookup"><span data-stu-id="9474f-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="9474f-378">*Выберите соответствующий фрагмент из списка, щелкнув его.*</span><span class="sxs-lookup"><span data-stu-id="9474f-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="9474f-379">Приложение б. Установка Visual Studio Express 2012 для Web</span><span class="sxs-lookup"><span data-stu-id="9474f-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="9474f-380">Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версии с помощью **[установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="9474f-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="9474f-381">Следующие инструкции помогут вам выполнить действия, необходимые для установки *Visual Studio Express 2012 для Web* с помощью *установщик веб-платформы Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="9474f-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="9474f-382">Перейдите в [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="9474f-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="9474f-383">Кроме того, если у вас уже установлен установщик веб-платформы, вы можете открыть его и найти продукт &quot;<em>Visual Studio Express 2012 для Web с пакетом Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="9474f-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="9474f-384">Щелкните **Install Now (установить сейчас**).</span><span class="sxs-lookup"><span data-stu-id="9474f-384">Click on **Install Now**.</span></span> <span data-ttu-id="9474f-385">Если у вас нет **установщика веб-платформы** , вы будете сначала перенаправлены на загрузку и установку.</span><span class="sxs-lookup"><span data-stu-id="9474f-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="9474f-386">После открытия **установщика веб-платформы** нажмите кнопку **установить** , чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="9474f-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="9474f-387">![Установка Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Установка Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="9474f-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="9474f-388">*Установка Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="9474f-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="9474f-389">Прочитайте все лицензии и условия продуктов и нажмите кнопку " **принять** ", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="9474f-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Принятие условий лицензии](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="9474f-391">*Принятие условий лицензии*</span><span class="sxs-lookup"><span data-stu-id="9474f-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="9474f-392">Дождитесь завершения процесса загрузки и установки.</span><span class="sxs-lookup"><span data-stu-id="9474f-392">Wait until the downloading and installation process completes.</span></span>

    ![Ход установки](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="9474f-394">*Ход установки*</span><span class="sxs-lookup"><span data-stu-id="9474f-394">*Installation progress*</span></span>
6. <span data-ttu-id="9474f-395">После завершения установки нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="9474f-395">When the installation completes, click **Finish**.</span></span>

    ![Установка завершена](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="9474f-397">*Установка завершена*</span><span class="sxs-lookup"><span data-stu-id="9474f-397">*Installation completed*</span></span>
7. <span data-ttu-id="9474f-398">Нажмите кнопку **выход** , чтобы закрыть установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="9474f-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="9474f-399">Чтобы открыть Visual Studio Express для Интернета, перейдите на **начальный** экран и начните запись &quot;**VS Express**&quot;, а затем щелкните плитку **VS Express для Web** .</span><span class="sxs-lookup"><span data-stu-id="9474f-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Плитка VS Express для Web](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="9474f-401">*Плитка VS Express для Web*</span><span class="sxs-lookup"><span data-stu-id="9474f-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="9474f-402">Приложение в. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание</span><span class="sxs-lookup"><span data-stu-id="9474f-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="9474f-403">В этом приложении показано, как создать новый веб-сайт на портале Azure и опубликовать полученное приложение, выполнив следующие лабораторные занятия, используя возможности публикации веб-развертывание, предоставляемые Azure.</span><span class="sxs-lookup"><span data-stu-id="9474f-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="9474f-404">Задача 1. Создание нового веб-сайта на портале Azure</span><span class="sxs-lookup"><span data-stu-id="9474f-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="9474f-405">Перейдите в [портал управления Azure](https://manage.windowsazure.com/) и выполните вход с использованием учетных данных Майкрософт, связанных с подпиской.</span><span class="sxs-lookup"><span data-stu-id="9474f-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9474f-406">С помощью Azure вы можете бесплатно разместить 10 веб-сайтов ASP.NET, а затем масштабировать их по мере роста объема трафика.</span><span class="sxs-lookup"><span data-stu-id="9474f-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="9474f-407">Вы можете зарегистрироваться [здесь](https://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="9474f-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="9474f-408">![Вход в Windows портал Azure](build-restful-apis-with-aspnet-web-api/_static/image39.png "Вход в Windows портал Azure")</span><span class="sxs-lookup"><span data-stu-id="9474f-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="9474f-409">*Вход на портал*</span><span class="sxs-lookup"><span data-stu-id="9474f-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="9474f-410">На панели команд щелкните **создать** .</span><span class="sxs-lookup"><span data-stu-id="9474f-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="9474f-411">![Создание нового веб-сайта](build-restful-apis-with-aspnet-web-api/_static/image40.png "Создание нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="9474f-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="9474f-412">*Создание нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="9474f-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="9474f-413">Щелкните **Compute** | **веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="9474f-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="9474f-414">Затем выберите пункт **Быстрое создание** .</span><span class="sxs-lookup"><span data-stu-id="9474f-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="9474f-415">Предоставьте доступный URL-адрес для нового веб-сайта и щелкните **создать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="9474f-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9474f-416">Azure — это узел для веб-приложения, работающего в облаке, которое можно контролировать и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="9474f-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="9474f-417">Параметр Быстрое создание позволяет развернуть завершенное веб-приложение в Azure за пределами портала.</span><span class="sxs-lookup"><span data-stu-id="9474f-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="9474f-418">Он не включает шаги по настройке базы данных.</span><span class="sxs-lookup"><span data-stu-id="9474f-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="9474f-419">![Создание нового веб-сайта с помощью быстрого создания](build-restful-apis-with-aspnet-web-api/_static/image41.png "Создание нового веб-сайта с помощью быстрого создания")</span><span class="sxs-lookup"><span data-stu-id="9474f-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="9474f-420">*Создание нового веб-сайта с помощью быстрого создания*</span><span class="sxs-lookup"><span data-stu-id="9474f-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="9474f-421">Дождитесь создания нового **веб-сайта** .</span><span class="sxs-lookup"><span data-stu-id="9474f-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="9474f-422">После создания веб-сайта щелкните ссылку в столбце **URL-адрес** .</span><span class="sxs-lookup"><span data-stu-id="9474f-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="9474f-423">Убедитесь, что новый веб-сайт работает.</span><span class="sxs-lookup"><span data-stu-id="9474f-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="9474f-424">![Обзор нового веб-сайта](build-restful-apis-with-aspnet-web-api/_static/image42.png "Обзор нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="9474f-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="9474f-425">*Обзор нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="9474f-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="9474f-426">![Веб-сайт работает](build-restful-apis-with-aspnet-web-api/_static/image43.png "Веб-сайт работает")</span><span class="sxs-lookup"><span data-stu-id="9474f-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="9474f-427">*Веб-сайт работает*</span><span class="sxs-lookup"><span data-stu-id="9474f-427">*Web site running*</span></span>
6. <span data-ttu-id="9474f-428">Вернитесь на портал и щелкните имя веб-сайта в столбце **имя** , чтобы отобразить страницы управления.</span><span class="sxs-lookup"><span data-stu-id="9474f-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="9474f-429">![Открытие страниц управления веб-сайтом](build-restful-apis-with-aspnet-web-api/_static/image44.png "Открытие страниц управления веб-сайтом")</span><span class="sxs-lookup"><span data-stu-id="9474f-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="9474f-430">*Открытие страниц управления веб-сайтом*</span><span class="sxs-lookup"><span data-stu-id="9474f-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="9474f-431">На странице **панель мониторинга** в разделе **краткий обзор** щелкните ссылку **скачать профиль публикации** .</span><span class="sxs-lookup"><span data-stu-id="9474f-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9474f-432">*Профиль публикации* содержит все сведения, необходимые для публикации веб-приложения в Azure для каждого включенного метода публикации.</span><span class="sxs-lookup"><span data-stu-id="9474f-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="9474f-433">Профиль публикации содержит URL-адреса, учетные данные пользователей и строки для открытия базы данных, которые необходимы для проверки подлинности и подключения к каждой из конечных точек, соответствующей разрешенному методу публикации.</span><span class="sxs-lookup"><span data-stu-id="9474f-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="9474f-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express для Web** и **Microsoft Visual Studio 2012** поддерживают чтение профилей публикации для автоматизации настройки этих программ для публикации веб-приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="9474f-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="9474f-435">![Скачивание профиля публикации веб-сайта](build-restful-apis-with-aspnet-web-api/_static/image45.png "Скачивание профиля публикации веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="9474f-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="9474f-436">*Скачивание профиля публикации веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="9474f-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="9474f-437">Скачайте файл профиля публикации в известное расположение.</span><span class="sxs-lookup"><span data-stu-id="9474f-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="9474f-438">Далее в этом упражнении вы узнаете, как использовать этот файл для публикации веб-приложения в Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9474f-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="9474f-439">![Сохранение файла профиля публикации](build-restful-apis-with-aspnet-web-api/_static/image46.png "Сохранение профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="9474f-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="9474f-440">*Сохранение файла профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="9474f-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="9474f-441">Задача 2. Настройка сервера базы данных</span><span class="sxs-lookup"><span data-stu-id="9474f-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="9474f-442">Если приложение использует SQL Server базы данных, потребуется создать сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9474f-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="9474f-443">Если вы хотите развернуть простое приложение, которое не использует SQL Server вы можете пропустить эту задачу.</span><span class="sxs-lookup"><span data-stu-id="9474f-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="9474f-444">Для хранения базы данных приложения необходим сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9474f-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="9474f-445">Серверы базы данных SQL можно просмотреть в подписке на портале управления Azure в **базах данных sql** | **серверы** | **панели мониторинга сервера**.</span><span class="sxs-lookup"><span data-stu-id="9474f-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="9474f-446">Если сервер не создан, можно создать его с помощью кнопки **Добавить** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="9474f-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="9474f-447">Запишите **имя сервера и URL-адрес, имя для входа администратора и пароль**, так как они будут использоваться в следующих задачах.</span><span class="sxs-lookup"><span data-stu-id="9474f-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="9474f-448">Пока не создавайте базу данных, так как она будет создана на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="9474f-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="9474f-449">![Панель мониторинга сервера базы данных SQL](build-restful-apis-with-aspnet-web-api/_static/image47.png "Панель мониторинга сервера базы данных SQL")</span><span class="sxs-lookup"><span data-stu-id="9474f-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="9474f-450">*Панель мониторинга сервера базы данных SQL*</span><span class="sxs-lookup"><span data-stu-id="9474f-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="9474f-451">В следующей задаче вы проверите подключение к базе данных из Visual Studio. по этой причине необходимо включить локальный IP-адрес в список **разрешенных IP-адресов**сервера.</span><span class="sxs-lookup"><span data-stu-id="9474f-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="9474f-452">Для этого нажмите кнопку **настроить**, выберите IP-адрес из **текущего IP-адреса клиента** и вставьте его в текстовые поля **начальный IP-адрес** и **конечный IP** -адрес и нажмите кнопку ![добавить-клиент-IP – адрес-OK-кнопка](build-restful-apis-with-aspnet-web-api/_static/image48.png).</span><span class="sxs-lookup"><span data-stu-id="9474f-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![Добавление IP-адреса клиента](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="9474f-454">*Добавление IP-адреса клиента*</span><span class="sxs-lookup"><span data-stu-id="9474f-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="9474f-455">После добавления **IP-адреса клиента** в список Разрешенные IP-адреса нажмите кнопку **сохранить** , чтобы подтвердить изменения.</span><span class="sxs-lookup"><span data-stu-id="9474f-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Подтверждение изменений](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="9474f-457">*Подтверждение изменений*</span><span class="sxs-lookup"><span data-stu-id="9474f-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="9474f-458">Задача 3. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание</span><span class="sxs-lookup"><span data-stu-id="9474f-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="9474f-459">Вернитесь к решению ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="9474f-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="9474f-460">В **Обозреватель решений**щелкните правой кнопкой мыши проект веб-сайта и выберите **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="9474f-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="9474f-461">![Публикация приложения](build-restful-apis-with-aspnet-web-api/_static/image51.png "Публикация приложения")</span><span class="sxs-lookup"><span data-stu-id="9474f-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="9474f-462">*Публикация веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="9474f-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="9474f-463">Импортируйте профиль публикации, сохраненный в первой задаче.</span><span class="sxs-lookup"><span data-stu-id="9474f-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="9474f-464">![Импорт профиля публикации](build-restful-apis-with-aspnet-web-api/_static/image52.png "Импорт профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="9474f-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="9474f-465">*Импорт профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="9474f-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="9474f-466">Щелкните **проверить подключение**.</span><span class="sxs-lookup"><span data-stu-id="9474f-466">Click **Validate Connection**.</span></span> <span data-ttu-id="9474f-467">После завершения проверки нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9474f-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9474f-468">Проверка завершится, когда появится зеленая галочка рядом с кнопкой проверить подключение.</span><span class="sxs-lookup"><span data-stu-id="9474f-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="9474f-469">![Проверка подключения](build-restful-apis-with-aspnet-web-api/_static/image53.png "Проверка подключения")</span><span class="sxs-lookup"><span data-stu-id="9474f-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="9474f-470">*Проверка подключения*</span><span class="sxs-lookup"><span data-stu-id="9474f-470">*Validating connection*</span></span>
4. <span data-ttu-id="9474f-471">На странице **Параметры** в разделе **базы данных** нажмите кнопку рядом с текстовым полем подключения к базе данных (т. е. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="9474f-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="9474f-472">![Конфигурация веб-развертывания](build-restful-apis-with-aspnet-web-api/_static/image54.png "Конфигурация веб-развертывания")</span><span class="sxs-lookup"><span data-stu-id="9474f-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="9474f-473">*Конфигурация веб-развертывания*</span><span class="sxs-lookup"><span data-stu-id="9474f-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="9474f-474">Настройте подключение к базе данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9474f-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="9474f-475">В поле **имя сервера** введите URL-адрес сервера базы данных SQL с помощью префикса *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="9474f-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="9474f-476">В окне **имя пользователя** введите имя для входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="9474f-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="9474f-477">В окне **пароль** введите пароль для входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="9474f-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="9474f-478">Введите имя новой базы данных, например: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="9474f-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="9474f-479">![Настройка строки подключения к целевому объекту](build-restful-apis-with-aspnet-web-api/_static/image55.png "Настройка строки подключения к целевому объекту")</span><span class="sxs-lookup"><span data-stu-id="9474f-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="9474f-480">*Настройка строки подключения к целевому объекту*</span><span class="sxs-lookup"><span data-stu-id="9474f-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="9474f-481">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9474f-481">Then click **OK**.</span></span> <span data-ttu-id="9474f-482">При появлении запроса на создание базы данных нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="9474f-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="9474f-483">![Создание базы данных](build-restful-apis-with-aspnet-web-api/_static/image56.png "Создание строки базы данных")</span><span class="sxs-lookup"><span data-stu-id="9474f-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="9474f-484">*Создание базы данных*</span><span class="sxs-lookup"><span data-stu-id="9474f-484">*Creating the database*</span></span>
7. <span data-ttu-id="9474f-485">Строка подключения, которая будет использоваться для подключения к базе данных SQL в Windows Azure, отображается в текстовом поле подключения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9474f-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="9474f-486">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9474f-486">Then click **Next**.</span></span>

    <span data-ttu-id="9474f-487">![Строка подключения, указывающая на базу данных SQL](build-restful-apis-with-aspnet-web-api/_static/image57.png "Строка подключения, указывающая на базу данных SQL")</span><span class="sxs-lookup"><span data-stu-id="9474f-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="9474f-488">*Строка подключения, указывающая на базу данных SQL*</span><span class="sxs-lookup"><span data-stu-id="9474f-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="9474f-489">На странице **Предварительный просмотр** нажмите кнопку **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="9474f-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="9474f-490">![Публикация веб-приложения](build-restful-apis-with-aspnet-web-api/_static/image58.png "Публикация веб-приложения")</span><span class="sxs-lookup"><span data-stu-id="9474f-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="9474f-491">*Публикация веб-приложения*</span><span class="sxs-lookup"><span data-stu-id="9474f-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="9474f-492">По завершении процесса публикации браузер по умолчанию будет открывать опубликованный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="9474f-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="9474f-493">![Приложение, опубликованное в Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Приложение, опубликованное в Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="9474f-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="9474f-494">*Приложение Опубликовано в Azure*</span><span class="sxs-lookup"><span data-stu-id="9474f-494">*Application published to Azure*</span></span>
