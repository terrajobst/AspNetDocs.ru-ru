---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
title: Общие сведения о маршрутизации ASP.NETC#MVC () | Документация Майкрософт
author: StephenWalther
description: В этом руководстве Стивен Вальтер показывает, как платформа ASP.NET MVC сопоставляет запросы браузера с действиями контроллера.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 5b39d2d5-4bf9-4d04-94c7-81b84dfeeb31
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 5e1155ca676e7a25b5bfc63e251c6387a010eb34
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437706"
---
# <a name="aspnet-mvc-routing-overview-c"></a><span data-ttu-id="5e36a-103">Общие сведения о маршрутизации в ASP.NET MVC (C#)</span><span class="sxs-lookup"><span data-stu-id="5e36a-103">ASP.NET MVC Routing Overview (C#)</span></span>

<span data-ttu-id="5e36a-104">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="5e36a-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="5e36a-105">В этом руководстве Стивен Вальтер показывает, как платформа ASP.NET MVC сопоставляет запросы браузера с действиями контроллера.</span><span class="sxs-lookup"><span data-stu-id="5e36a-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>

<span data-ttu-id="5e36a-106">В этом учебнике вы предоставили важную возможность для каждого приложения ASP.NET MVC, именуемого *маршрутизацией ASP.NET*.</span><span class="sxs-lookup"><span data-stu-id="5e36a-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="5e36a-107">Модуль маршрутизации ASP.NET отвечает за сопоставление входящих запросов браузера определенным действиям контроллера MVC.</span><span class="sxs-lookup"><span data-stu-id="5e36a-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="5e36a-108">По завершении работы с этим руководством вы узнаете, как стандартная таблица маршрутов сопоставляет запросы действиям контроллера.</span><span class="sxs-lookup"><span data-stu-id="5e36a-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="5e36a-109">Использование таблицы маршрутов по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5e36a-109">Using the Default Route Table</span></span>

<span data-ttu-id="5e36a-110">При создании нового приложения ASP.NET MVC приложение уже настроено для использования маршрутизации ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5e36a-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="5e36a-111">Маршрутизация ASP.NET выполняется в двух местах.</span><span class="sxs-lookup"><span data-stu-id="5e36a-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="5e36a-112">Сначала в файле веб-конфигурации приложения (файл Web. config) включена маршрутизация ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5e36a-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="5e36a-113">В файле конфигурации есть четыре раздела, относящиеся к маршрутизации: раздел System. Web. httpModules, раздел System. Web. httpHandlers, раздел System. веб Server. modules и System. веб Server. обработчики.</span><span class="sxs-lookup"><span data-stu-id="5e36a-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="5e36a-114">Будьте внимательны и не удаляйте эти разделы, так как в этом случае маршрутизация больше не будет работать.</span><span class="sxs-lookup"><span data-stu-id="5e36a-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="5e36a-115">Во-вторых, и, что более важно, таблица маршрутов создается в файле Global. asax приложения.</span><span class="sxs-lookup"><span data-stu-id="5e36a-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="5e36a-116">Файл Global. asax — это специальный файл, содержащий обработчики событий для событий жизненного цикла приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5e36a-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="5e36a-117">Таблица маршрутов создается во время события запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="5e36a-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="5e36a-118">Файл в листинге 1 содержит файл Global. asax по умолчанию для приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="5e36a-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="5e36a-119">**Листинг 1. Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="5e36a-119">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample1.cs)]

<span data-ttu-id="5e36a-120">При первом запуске приложения MVC вызывается метод Application\_Start ().</span><span class="sxs-lookup"><span data-stu-id="5e36a-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="5e36a-121">Этот метод, в свою очередь, вызывает метод Регистерраутес ().</span><span class="sxs-lookup"><span data-stu-id="5e36a-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="5e36a-122">Метод Регистерраутес () создает таблицу маршрутов.</span><span class="sxs-lookup"><span data-stu-id="5e36a-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="5e36a-123">Таблица маршрутов по умолчанию содержит один маршрут (с именем по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="5e36a-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="5e36a-124">Маршрут по умолчанию сопоставляет первый сегмент URL-адреса с именем контроллера, второй сегмент URL-адреса действия контроллера и третий сегмент с именем параметра **ID**.</span><span class="sxs-lookup"><span data-stu-id="5e36a-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="5e36a-125">Представьте, что в адресную строку браузера введен следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="5e36a-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="5e36a-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="5e36a-126">/Home/Index/3</span></span>

<span data-ttu-id="5e36a-127">Маршрут по умолчанию сопоставляет этот URL-адрес со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="5e36a-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="5e36a-128">контроллер = Главная</span><span class="sxs-lookup"><span data-stu-id="5e36a-128">controller = Home</span></span>

- <span data-ttu-id="5e36a-129">действие = индекс</span><span class="sxs-lookup"><span data-stu-id="5e36a-129">action = Index</span></span>

- <span data-ttu-id="5e36a-130">ИД = 3</span><span class="sxs-lookup"><span data-stu-id="5e36a-130">id = 3</span></span>

<span data-ttu-id="5e36a-131">При запросе URL-адреса/Home/Index/3 выполняется следующий код:</span><span class="sxs-lookup"><span data-stu-id="5e36a-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="5e36a-132">HomeController. индекс (3)</span><span class="sxs-lookup"><span data-stu-id="5e36a-132">HomeController.Index(3)</span></span>

<span data-ttu-id="5e36a-133">Маршрут по умолчанию включает значения по умолчанию для всех трех параметров.</span><span class="sxs-lookup"><span data-stu-id="5e36a-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="5e36a-134">Если контроллер не указан, параметр контроллера по умолчанию имеет значение **Home**.</span><span class="sxs-lookup"><span data-stu-id="5e36a-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="5e36a-135">Если действие не указано, для параметра Action по умолчанию используется значение **index**.</span><span class="sxs-lookup"><span data-stu-id="5e36a-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="5e36a-136">Наконец, если идентификатор не указан, параметр ID по умолчанию имеет пустую строку.</span><span class="sxs-lookup"><span data-stu-id="5e36a-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="5e36a-137">Рассмотрим несколько примеров того, как маршрут по умолчанию сопоставляет URL-адреса действиям контроллера.</span><span class="sxs-lookup"><span data-stu-id="5e36a-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="5e36a-138">Представьте, что в адресную строку браузера введен следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="5e36a-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="5e36a-139">/Home</span><span class="sxs-lookup"><span data-stu-id="5e36a-139">/Home</span></span>

<span data-ttu-id="5e36a-140">По умолчанию при вводе этого URL-адреса вызывается метод Index () класса HomeController в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="5e36a-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="5e36a-141">**Листинг 2. HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="5e36a-141">**Listing 2 - HomeController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample2.cs)]

<span data-ttu-id="5e36a-142">В листинге 2 класс HomeController включает метод с именем index (), который принимает один параметр с именем ID. /Home URL вызывает вызов метода index () с пустой строкой в качестве значения параметра ID.</span><span class="sxs-lookup"><span data-stu-id="5e36a-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with an empty string as the value of the Id parameter.</span></span>

<span data-ttu-id="5e36a-143">Поскольку платформа MVC вызывает действия контроллера, URL-адрес/Home также соответствует методу index () класса HomeController в листинге 3.</span><span class="sxs-lookup"><span data-stu-id="5e36a-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="5e36a-144">**Листинг 3 — HomeController.cs (действие с индексом без параметра)**</span><span class="sxs-lookup"><span data-stu-id="5e36a-144">**Listing 3 - HomeController.cs (Index action with no parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample3.cs)]

<span data-ttu-id="5e36a-145">Метод Index () в листинге 3 не принимает никаких параметров.</span><span class="sxs-lookup"><span data-stu-id="5e36a-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="5e36a-146">URL-адрес/Home приведет к вызову этого метода index ().</span><span class="sxs-lookup"><span data-stu-id="5e36a-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="5e36a-147">URL-адрес/Home/Index/3 также вызывает этот метод (идентификатор игнорируется).</span><span class="sxs-lookup"><span data-stu-id="5e36a-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="5e36a-148">URL-адрес/Home также соответствует методу index () класса HomeController в листинге 4.</span><span class="sxs-lookup"><span data-stu-id="5e36a-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="5e36a-149">**Листинг 4 — HomeController.cs (действие индекса с параметром, допускающим значение null)**</span><span class="sxs-lookup"><span data-stu-id="5e36a-149">**Listing 4 - HomeController.cs (Index action with nullable parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample4.cs)]

<span data-ttu-id="5e36a-150">В листинге 4 метод Index () имеет один целочисленный параметр.</span><span class="sxs-lookup"><span data-stu-id="5e36a-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="5e36a-151">Поскольку параметр является параметром, допускающим значения NULL (может иметь значение null), индекс () может быть вызван без возникновения ошибки.</span><span class="sxs-lookup"><span data-stu-id="5e36a-151">Because the parameter is a nullable parameter (can have the value Null), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="5e36a-152">Наконец, вызов метода index () в листинге 5 с URL-адресом/Home вызывает исключение, так как параметр ID *не* является параметром, допускающим значение null.</span><span class="sxs-lookup"><span data-stu-id="5e36a-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="5e36a-153">При попытке вызвать метод Index () появится сообщение об ошибке, показанное на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="5e36a-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="5e36a-154">**Листинг 5 — HomeController.cs (действие индекса с параметром ID)**</span><span class="sxs-lookup"><span data-stu-id="5e36a-154">**Listing 5 - HomeController.cs (Index action with Id parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample5.cs)]

<span data-ttu-id="5e36a-155">[![вызова действия контроллера, ожидающего значения параметра](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5e36a-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)</span></span>

<span data-ttu-id="5e36a-156">**Рис. 01**. вызов действия контроллера, ожидающего значения параметра ([щелкните, чтобы просмотреть изображение с полным размером](asp-net-mvc-routing-overview-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5e36a-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-cs/_static/image2.png))</span></span>

<span data-ttu-id="5e36a-157">URL-адрес/Home/Index/3, с другой стороны, работает точно так же, как и действие контроллера индекса в листинге 5.</span><span class="sxs-lookup"><span data-stu-id="5e36a-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="5e36a-158">/Home/Index/3 запроса вызывает метод Index () с параметром ID, имеющим значение 3.</span><span class="sxs-lookup"><span data-stu-id="5e36a-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="5e36a-159">Сводка</span><span class="sxs-lookup"><span data-stu-id="5e36a-159">Summary</span></span>

<span data-ttu-id="5e36a-160">Цель этого учебника — предоставить краткое введение в маршрутизацию ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5e36a-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="5e36a-161">Мы рассматривали таблицу маршрутов по умолчанию, полученную с помощью нового приложения MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5e36a-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="5e36a-162">Вы узнали, как маршрут по умолчанию сопоставляет URL-адреса действиям контроллера.</span><span class="sxs-lookup"><span data-stu-id="5e36a-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5e36a-163">Дальше</span><span class="sxs-lookup"><span data-stu-id="5e36a-163">Next</span></span>](understanding-action-filters-cs.md)
