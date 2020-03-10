---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Основные сведения о процессе выполнения ASP.NET MVC | Документация Майкрософт
author: microsoft
description: Узнайте, как инфраструктура MVC ASP.NET обрабатывает пошаговые инструкции в браузере.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435456"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="38c5c-103">Общие сведения о процессе выполнения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="38c5c-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="38c5c-104">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="38c5c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="38c5c-105">Узнайте, как инфраструктура MVC ASP.NET обрабатывает пошаговые инструкции в браузере.</span><span class="sxs-lookup"><span data-stu-id="38c5c-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="38c5c-106">Запросы к веб-приложению на основе MVC ASP.NET сначала проходят через объект **UrlRoutingModule** , который является HTTP-модулем.</span><span class="sxs-lookup"><span data-stu-id="38c5c-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="38c5c-107">Этот модуль анализирует запрос и выбирает маршрут.</span><span class="sxs-lookup"><span data-stu-id="38c5c-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="38c5c-108">Объект **UrlRoutingModule** выбирает первый объект Route, соответствующий текущему запросу.</span><span class="sxs-lookup"><span data-stu-id="38c5c-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="38c5c-109">(Объект маршрута — это класс, реализующий **раутебасе**, который обычно является экземпляром класса **Route** .) Если маршруты не совпадают, объект **UrlRoutingModule** ничего не делает и позволяет выполнить запрос к обычной обработке запросов ASP.NET или IIS.</span><span class="sxs-lookup"><span data-stu-id="38c5c-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="38c5c-110">Из выбранного объекта **маршрута** объект **UrlRoutingModule** получает объект **IRouteHandler** , связанный с объектом **Route** .</span><span class="sxs-lookup"><span data-stu-id="38c5c-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="38c5c-111">Как правило, в приложении MVC это будет экземпляр **мвкраутехандлер**.</span><span class="sxs-lookup"><span data-stu-id="38c5c-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="38c5c-112">Экземпляр **IRouteHandler** создает объект **IHttpHandler** и передает его в объект **ихттпконтекст** .</span><span class="sxs-lookup"><span data-stu-id="38c5c-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="38c5c-113">По умолчанию экземпляром **IHttpHandler** для MVC является объект **мвчандлер** .</span><span class="sxs-lookup"><span data-stu-id="38c5c-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="38c5c-114">Затем объект **мвчандлер** выбирает контроллер, который в конечном итоге будет обрабатывать запрос.</span><span class="sxs-lookup"><span data-stu-id="38c5c-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="38c5c-115">Если веб-приложение ASP.NET на базе MVC запускается в IIS 7.0, для проектов MVC не требуется расширение имени файла.</span><span class="sxs-lookup"><span data-stu-id="38c5c-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="38c5c-116">В IIS 6.0 для обработки необходимо, чтобы расширение имени файла MVC было связано с библиотекой DLL ISAPI ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="38c5c-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="38c5c-117">Модуль и обработчик являются точками входа для платформы MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="38c5c-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="38c5c-118">Они отвечают за следующее:</span><span class="sxs-lookup"><span data-stu-id="38c5c-118">They perform the following actions:</span></span>

- <span data-ttu-id="38c5c-119">Выбор нужного контроллера в веб-приложении MVC.</span><span class="sxs-lookup"><span data-stu-id="38c5c-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="38c5c-120">Получение отдельного экземпляра контроллера.</span><span class="sxs-lookup"><span data-stu-id="38c5c-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="38c5c-121">Вызовите метод **EXECUTE** контроллера.</span><span class="sxs-lookup"><span data-stu-id="38c5c-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="38c5c-122">Ниже перечислены этапы выполнения веб-проекта MVC.</span><span class="sxs-lookup"><span data-stu-id="38c5c-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="38c5c-123">Получение первого запроса к приложению.</span><span class="sxs-lookup"><span data-stu-id="38c5c-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="38c5c-124">В файле Global. asax объекты **Route** добавляются в объект **RouteTable** .</span><span class="sxs-lookup"><span data-stu-id="38c5c-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="38c5c-125">Выполнение маршрутизации</span><span class="sxs-lookup"><span data-stu-id="38c5c-125">Perform routing</span></span> 

    - <span data-ttu-id="38c5c-126">Модуль **UrlRoutingModule** использует первый совпадающий объект **Route** в коллекции **RouteTable** для создания объекта **RouteData** , который затем используется для создания объекта **RequestContext** (**ихттпконтекст**).</span><span class="sxs-lookup"><span data-stu-id="38c5c-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="38c5c-127">Создание обработчика запроса MVC</span><span class="sxs-lookup"><span data-stu-id="38c5c-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="38c5c-128">Объект **мвкраутехандлер** создает экземпляр класса **мвчандлер** и передает его экземпляру **RequestContext** .</span><span class="sxs-lookup"><span data-stu-id="38c5c-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="38c5c-129">Создание контроллера</span><span class="sxs-lookup"><span data-stu-id="38c5c-129">Create controller</span></span> 

    - <span data-ttu-id="38c5c-130">Объект **мвчандлер** использует экземпляр **RequestContext** для задания объекта **иконтроллерфактори** (обычно это экземпляр класса **дефаултконтроллерфактори** ) для создания экземпляра контроллера с помощью.</span><span class="sxs-lookup"><span data-stu-id="38c5c-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="38c5c-131">Выполнение контроллера — экземпляр **мвчандлер** вызывает метод **EXECUTE** контроллера s.</span><span class="sxs-lookup"><span data-stu-id="38c5c-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="38c5c-132">Вызов действия</span><span class="sxs-lookup"><span data-stu-id="38c5c-132">Invoke action</span></span> 

    - <span data-ttu-id="38c5c-133">Большинство контроллеров наследуются от базового класса **контроллера** .</span><span class="sxs-lookup"><span data-stu-id="38c5c-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="38c5c-134">Для контроллеров, которые делают это, объект **ControllerActionInvoker** , связанный с контроллером, определяет, какой метод действия класса контроллера нужно вызвать, а затем вызывает этот метод.</span><span class="sxs-lookup"><span data-stu-id="38c5c-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="38c5c-135">Выполнение результата</span><span class="sxs-lookup"><span data-stu-id="38c5c-135">Execute result</span></span> 

    - <span data-ttu-id="38c5c-136">Типичный метод действия может получить ввод данных пользователем, подготовить соответствующие данные ответа, а затем выполнить результат, возвращая тип результата.</span><span class="sxs-lookup"><span data-stu-id="38c5c-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="38c5c-137">К встроенным типам результатов, которые могут быть выполнены, относятся следующие: **виевресулт** (который визуализирует представление и является наиболее часто используемым типом результата), **редиректтораутересулт**, **редиректресулт**, **контентресулт**, **JsonResult**и **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="38c5c-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
