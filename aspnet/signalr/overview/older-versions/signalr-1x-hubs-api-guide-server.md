---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: Путеводитель по API концентраторов SignalR ASP.NET-Server (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: В этом документе содержатся общие сведения о программировании на стороне сервера API концентраторов SignalR ASP.NET для SignalR версии 1,1 с примерами кода, демонстрирующими...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468132"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a><span data-ttu-id="23fd2-103">Путеводитель по API концентраторов SignalR ASP.NET-Server (SignalR 1. x)</span><span class="sxs-lookup"><span data-stu-id="23fd2-103">ASP.NET SignalR Hubs API Guide - Server (SignalR 1.x)</span></span>

<span data-ttu-id="23fd2-104">[Патрик Флетчера](https://github.com/pfletcher), [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="23fd2-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="23fd2-105">В этом документе приводятся общие сведения о программировании на стороне сервера API концентраторов SignalR ASP.NET для SignalR версии 1,1 с примерами кода, демонстрирующими общие параметры.</span><span class="sxs-lookup"><span data-stu-id="23fd2-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 1.1, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="23fd2-106">API концентраторов SignalR позволяет выполнять удаленные вызовы процедур (RPC) с сервера на подключенные клиенты и с клиентов на сервер.</span><span class="sxs-lookup"><span data-stu-id="23fd2-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="23fd2-107">В серверном коде определяются методы, которые могут вызываться клиентами, и вызываются методы, которые выполняются на клиенте.</span><span class="sxs-lookup"><span data-stu-id="23fd2-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="23fd2-108">В клиентском коде определяются методы, которые могут быть вызваны с сервера, а также вызываются методы, которые выполняются на сервере.</span><span class="sxs-lookup"><span data-stu-id="23fd2-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="23fd2-109">Этот механизм отвечает за все клиентские коммуникации.</span><span class="sxs-lookup"><span data-stu-id="23fd2-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="23fd2-110">SignalR также предлагает интерфейс API более низкого уровня, называемый постоянными подключениями.</span><span class="sxs-lookup"><span data-stu-id="23fd2-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="23fd2-111">Общие сведения о SignalR, концентраторах и постоянных подключениях, а также руководство, в котором показано, как создать полноценное приложение SignalR, см. в разделе [SignalR-начало работы](index.md).</span><span class="sxs-lookup"><span data-stu-id="23fd2-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="23fd2-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="23fd2-112">Overview</span></span>

<span data-ttu-id="23fd2-113">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="23fd2-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="23fd2-114">Как зарегистрировать маршрут SignalR и настроить параметры SignalR</span><span class="sxs-lookup"><span data-stu-id="23fd2-114">How to register the SignalR route and configure SignalR options</span></span>](#route)

    - [<span data-ttu-id="23fd2-115">URL-адрес/SignalR</span><span class="sxs-lookup"><span data-stu-id="23fd2-115">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="23fd2-116">Настройка параметров SignalR</span><span class="sxs-lookup"><span data-stu-id="23fd2-116">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="23fd2-117">Создание и использование классов концентратора</span><span class="sxs-lookup"><span data-stu-id="23fd2-117">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="23fd2-118">Время существования объекта концентратора</span><span class="sxs-lookup"><span data-stu-id="23fd2-118">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="23fd2-119">Неоднородный регистр имен концентраторов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="23fd2-119">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="23fd2-120">Несколько концентраторов</span><span class="sxs-lookup"><span data-stu-id="23fd2-120">Multiple Hubs</span></span>](#multiplehubs)
- [<span data-ttu-id="23fd2-121">Определение методов в классе Hub, которые могут вызываться клиентами</span><span class="sxs-lookup"><span data-stu-id="23fd2-121">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="23fd2-122">Неоднородный регистр имен методов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="23fd2-122">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="23fd2-123">Время асинхронного выполнения</span><span class="sxs-lookup"><span data-stu-id="23fd2-123">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="23fd2-124">Определение перегрузок</span><span class="sxs-lookup"><span data-stu-id="23fd2-124">Defining overloads</span></span>](#overloads)
- [<span data-ttu-id="23fd2-125">Вызов клиентских методов из класса HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-125">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="23fd2-126">Выбор клиентов, получающих RPC</span><span class="sxs-lookup"><span data-stu-id="23fd2-126">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="23fd2-127">Нет проверки во время компиляции для имен методов</span><span class="sxs-lookup"><span data-stu-id="23fd2-127">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="23fd2-128">Сопоставление имен методов без учета регистра</span><span class="sxs-lookup"><span data-stu-id="23fd2-128">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="23fd2-129">Асинхронное выполнение</span><span class="sxs-lookup"><span data-stu-id="23fd2-129">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="23fd2-130">Управление членством в группах из класса HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-130">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="23fd2-131">Асинхронное выполнение методов Add и Remove</span><span class="sxs-lookup"><span data-stu-id="23fd2-131">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="23fd2-132">Сохранение членства в группах</span><span class="sxs-lookup"><span data-stu-id="23fd2-132">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="23fd2-133">Группы с одним пользователем</span><span class="sxs-lookup"><span data-stu-id="23fd2-133">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="23fd2-134">Как управлять событиями времени жизни соединения в классе HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-134">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="23fd2-135">При вызове onconnected, OnDisconnection и Онреконнектед</span><span class="sxs-lookup"><span data-stu-id="23fd2-135">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="23fd2-136">Состояние вызывающего объекта не заполнено</span><span class="sxs-lookup"><span data-stu-id="23fd2-136">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="23fd2-137">Получение сведений о клиенте из свойства Context</span><span class="sxs-lookup"><span data-stu-id="23fd2-137">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="23fd2-138">Передача состояния между клиентами и классом HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-138">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="23fd2-139">Как выполнять обработку ошибок в классе HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-139">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="23fd2-140">Вызов клиентских методов и управление группами извне класса HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-140">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="23fd2-141">Вызов методов клиента</span><span class="sxs-lookup"><span data-stu-id="23fd2-141">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="23fd2-142">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="23fd2-142">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="23fd2-143">Включение трассировки</span><span class="sxs-lookup"><span data-stu-id="23fd2-143">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="23fd2-144">Настройка конвейера концентраторов</span><span class="sxs-lookup"><span data-stu-id="23fd2-144">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="23fd2-145">Документацию по программированию клиентов см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="23fd2-145">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="23fd2-146">Путеводитель по API концентраторов SignalR — клиент JavaScript</span><span class="sxs-lookup"><span data-stu-id="23fd2-146">SignalR Hubs API Guide - JavaScript Client</span></span>](index.md)
- [<span data-ttu-id="23fd2-147">Путеводитель по API концентраторов SignalR — клиент .NET</span><span class="sxs-lookup"><span data-stu-id="23fd2-147">SignalR Hubs API Guide - .NET Client</span></span>](index.md)

<span data-ttu-id="23fd2-148">Ссылки на справочные статьи по API относятся к версии .NET 4,5 API.</span><span class="sxs-lookup"><span data-stu-id="23fd2-148">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="23fd2-149">Если вы используете .NET 4, см. [статьи с описанием API для .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="23fd2-149">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a><span data-ttu-id="23fd2-150">Как зарегистрировать маршрут SignalR и настроить параметры SignalR</span><span class="sxs-lookup"><span data-stu-id="23fd2-150">How to register the SignalR route and configure SignalR options</span></span>

<span data-ttu-id="23fd2-151">Чтобы определить маршрут, который клиенты будут использовать для подключения к концентратору, вызовите метод [мафубс](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-151">To define the route that clients will use to connect to your Hub, call the [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="23fd2-152">`MapHubs` является [методом расширения](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) для класса `System.Web.Routing.RouteCollection`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-152">`MapHubs` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `System.Web.Routing.RouteCollection` class.</span></span> <span data-ttu-id="23fd2-153">В следующем примере показано, как определить маршрут концентраторов SignalR в файле *Global. asax* .</span><span class="sxs-lookup"><span data-stu-id="23fd2-153">The following example shows how to define the SignalR Hubs route in the *Global.asax* file.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

<span data-ttu-id="23fd2-154">При добавлении функций SignalR в приложение ASP.NET MVC убедитесь, что маршрут SignalR добавлен перед другими маршрутами.</span><span class="sxs-lookup"><span data-stu-id="23fd2-154">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="23fd2-155">Дополнительные сведения см. [в разделе Учебник. Начало работы с SignalR и MVC 4](index.md).</span><span class="sxs-lookup"><span data-stu-id="23fd2-155">For more information, see [Tutorial: Getting Started with SignalR and MVC 4](index.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="23fd2-156">URL-адрес/SignalR</span><span class="sxs-lookup"><span data-stu-id="23fd2-156">The /signalr URL</span></span>

<span data-ttu-id="23fd2-157">По умолчанию URL-адрес маршрута, который будет использоваться клиентами для подключения к концентратору, — "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="23fd2-157">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="23fd2-158">(Не путайте этот URL-адрес с URL-адресом "/сигналр/хубс", который предназначен для автоматически созданного файла JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23fd2-158">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="23fd2-159">Дополнительные сведения о созданном прокси-сервере см. в статье [Путеводитель по API концентраторов SignalR — клиент JavaScript — созданный прокси-сервер и его назначение](index.md).)</span><span class="sxs-lookup"><span data-stu-id="23fd2-159">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).)</span></span>

<span data-ttu-id="23fd2-160">В некоторых случаях этот базовый URL-адрес не может использоваться для SignalR; Например, в проекте есть папка с именем *SignalR* , и вы не хотите изменять имя.</span><span class="sxs-lookup"><span data-stu-id="23fd2-160">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="23fd2-161">В этом случае можно изменить базовый URL-адрес, как показано в следующих примерах (замените "/SignalR" в примере кода на нужный URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="23fd2-161">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="23fd2-162">**Серверный код, указывающий URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="23fd2-162">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

<span data-ttu-id="23fd2-163">**Клиентский код JavaScript, указывающий URL-адрес (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="23fd2-163">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="23fd2-164">**Клиентский код JavaScript, указывающий URL-адрес (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="23fd2-164">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

<span data-ttu-id="23fd2-165">**Клиентский код .NET, указывающий URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="23fd2-165">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="23fd2-166">Настройка параметров SignalR</span><span class="sxs-lookup"><span data-stu-id="23fd2-166">Configuring SignalR Options</span></span>

<span data-ttu-id="23fd2-167">Перегрузки метода `MapHubs` позволяют указать настраиваемый URL-адрес, Пользовательский сопоставитель зависимостей и следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="23fd2-167">Overloads of the `MapHubs` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="23fd2-168">Включение междоменных вызовов из клиентов браузера.</span><span class="sxs-lookup"><span data-stu-id="23fd2-168">Enable cross-domain calls from browser clients.</span></span>

    <span data-ttu-id="23fd2-169">Как правило, если браузер загружает страницу из `http://contoso.com`, то подключение SignalR находится в том же домене, в `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-169">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="23fd2-170">Если страница из `http://contoso.com` устанавливает подключение к `http://fabrikam.com/signalr`, то есть подключение между доменами.</span><span class="sxs-lookup"><span data-stu-id="23fd2-170">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="23fd2-171">По соображениям безопасности междоменные соединения отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="23fd2-171">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="23fd2-172">Дополнительные сведения см. в статье [руководство по API концентраторов signalr ASP.NET. клиент JavaScript — как установить междоменное подключение](index.md).</span><span class="sxs-lookup"><span data-stu-id="23fd2-172">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](index.md).</span></span>
- <span data-ttu-id="23fd2-173">Включить подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="23fd2-173">Enable detailed error messages.</span></span>

    <span data-ttu-id="23fd2-174">При возникновении ошибок поведение SignalR по умолчанию — отправить клиенту сообщение уведомления без подробностей о том, что произошло.</span><span class="sxs-lookup"><span data-stu-id="23fd2-174">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="23fd2-175">Отправка подробных сведений об ошибках клиентам не рекомендуется в рабочей среде, так как пользователи-злоумышленники могут использовать эти сведения в атаках приложения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-175">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="23fd2-176">Для устранения неполадок можно использовать этот параметр, чтобы временно включить более информативные отчеты об ошибках.</span><span class="sxs-lookup"><span data-stu-id="23fd2-176">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="23fd2-177">Отключите автоматически создаваемые прокси-файлы JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23fd2-177">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="23fd2-178">По умолчанию файл JavaScript с прокси для классов концентратора создается в ответ на URL-адрес «/сигналр/хубс».</span><span class="sxs-lookup"><span data-stu-id="23fd2-178">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="23fd2-179">Если вы не хотите использовать прокси-серверы JavaScript или хотите создать этот файл вручную и ссылаться на физический файл в клиентах, можно использовать этот параметр, чтобы отключить создание прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="23fd2-179">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="23fd2-180">Дополнительные сведения см. в статье [руководство по API концентраторов SignalR — клиент JavaScript. Создание физического файла для прокси-сервера, созданного SignalR](index.md).</span><span class="sxs-lookup"><span data-stu-id="23fd2-180">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](index.md).</span></span>

<span data-ttu-id="23fd2-181">В следующем примере показано, как указать URL-адрес подключения SignalR и эти параметры в вызове метода `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-181">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapHubs` method.</span></span> <span data-ttu-id="23fd2-182">Чтобы указать пользовательский URL-адрес, замените "/SignalR" в примере на URL-адрес, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="23fd2-182">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="23fd2-183">Создание и использование классов концентратора</span><span class="sxs-lookup"><span data-stu-id="23fd2-183">How to create and use Hub classes</span></span>

<span data-ttu-id="23fd2-184">Чтобы создать концентратор, создайте класс, производный от [Microsoft. ASPNET. SignalR. Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="23fd2-184">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="23fd2-185">В следующем примере показан простой класс концентратора для приложения разговора.</span><span class="sxs-lookup"><span data-stu-id="23fd2-185">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

<span data-ttu-id="23fd2-186">В этом примере подключенный клиент может вызвать метод `NewContosoChatMessage`, а когда это происходит, полученные данные передаются на все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="23fd2-186">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="23fd2-187">Время существования объекта концентратора</span><span class="sxs-lookup"><span data-stu-id="23fd2-187">Hub object lifetime</span></span>

<span data-ttu-id="23fd2-188">Вы не создаете экземпляр класса HUB или вызываете его методы из собственного кода на сервере. Все это выполняется конвейером концентраторов SignalR.</span><span class="sxs-lookup"><span data-stu-id="23fd2-188">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="23fd2-189">SignalR создает новый экземпляр класса Hub каждый раз, когда ему требуется выполнять операции концентратора, например, когда клиент подключается, отключается или вызывает метод на сервере.</span><span class="sxs-lookup"><span data-stu-id="23fd2-189">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="23fd2-190">Поскольку экземпляры класса Hub являются временными, их нельзя использовать для поддержания состояния от одного вызова метода к следующему.</span><span class="sxs-lookup"><span data-stu-id="23fd2-190">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="23fd2-191">Каждый раз, когда сервер получает вызов метода от клиента, новый экземпляр класса Hub обрабатывает сообщение.</span><span class="sxs-lookup"><span data-stu-id="23fd2-191">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="23fd2-192">Чтобы сохранить состояние через несколько соединений и вызовов методов, используйте другой метод, например базу данных или статическую переменную в классе Hub, или другой класс, который не является производным от `Hub`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-192">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="23fd2-193">При сохранении данных в памяти с помощью метода, такого как статическая переменная в классе Hub, данные будут потеряны при очистке домена приложения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-193">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="23fd2-194">Если вы хотите отправить сообщения клиентам из собственного кода, который выполняется вне класса Hub, это невозможно сделать, создав экземпляр класса концентратора, но это можно сделать, получив ссылку на объект контекста SignalR для класса Hub.</span><span class="sxs-lookup"><span data-stu-id="23fd2-194">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="23fd2-195">Дополнительные сведения см. в разделе [как вызывать клиентские методы и управлять группами за пределами класса Hub](#callfromoutsidehub) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="23fd2-195">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="23fd2-196">Неоднородный регистр имен концентраторов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="23fd2-196">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="23fd2-197">По умолчанию клиенты JavaScript ссылаются на концентраторы, используя версию имени класса в стиле Camel.</span><span class="sxs-lookup"><span data-stu-id="23fd2-197">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="23fd2-198">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать соглашениям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23fd2-198">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="23fd2-199">Предыдущий пример будет называться `contosoChatHub` в коде JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23fd2-199">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="23fd2-200">**Server**</span><span class="sxs-lookup"><span data-stu-id="23fd2-200">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

<span data-ttu-id="23fd2-201">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="23fd2-201">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

<span data-ttu-id="23fd2-202">Если необходимо указать другое имя для использования клиентами, добавьте атрибут `HubName`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-202">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="23fd2-203">При использовании атрибута `HubName` в клиентах JavaScript нет необходимости изменять имя на Camel.</span><span class="sxs-lookup"><span data-stu-id="23fd2-203">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="23fd2-204">**Server**</span><span class="sxs-lookup"><span data-stu-id="23fd2-204">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

<span data-ttu-id="23fd2-205">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="23fd2-205">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="23fd2-206">Несколько концентраторов</span><span class="sxs-lookup"><span data-stu-id="23fd2-206">Multiple Hubs</span></span>

<span data-ttu-id="23fd2-207">В приложении можно определить несколько классов концентратора.</span><span class="sxs-lookup"><span data-stu-id="23fd2-207">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="23fd2-208">При этом соединение является общим, но группы являются отдельными:</span><span class="sxs-lookup"><span data-stu-id="23fd2-208">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="23fd2-209">Все клиенты будут использовать один и тот же URL-адрес для установления подключения SignalR со службой ("/SignalR" или настраиваемого URL-адреса, если он указан), и это соединение используется для всех центров, определенных службой.</span><span class="sxs-lookup"><span data-stu-id="23fd2-209">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="23fd2-210">По сравнению с определением всех функций концентратора в одном классе нет разницы в производительности для нескольких концентраторов.</span><span class="sxs-lookup"><span data-stu-id="23fd2-210">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="23fd2-211">Все концентраторы получают одинаковые сведения о запросе HTTP.</span><span class="sxs-lookup"><span data-stu-id="23fd2-211">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="23fd2-212">Так как все концентраторы используют одно и то же соединение, единственными данными HTTP-запроса, которые получает сервер, является исходный HTTP-запрос, который устанавливает подключение SignalR.</span><span class="sxs-lookup"><span data-stu-id="23fd2-212">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="23fd2-213">При использовании запроса на подключение для передачи информации от клиента на сервер путем указания строки запроса нельзя указывать разные строки запроса для разных концентраторов.</span><span class="sxs-lookup"><span data-stu-id="23fd2-213">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="23fd2-214">Все концентраторы получат одну и ту же информацию.</span><span class="sxs-lookup"><span data-stu-id="23fd2-214">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="23fd2-215">Созданный файл прокси-серверов JavaScript будет содержать учетные записи-посредники для всех концентраторов в одном файле.</span><span class="sxs-lookup"><span data-stu-id="23fd2-215">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="23fd2-216">Сведения о прокси-серверах JavaScript см. [в статье Путеводитель по API концентраторов SignalR — клиент JavaScript — созданный прокси-сервер и его назначение](index.md).</span><span class="sxs-lookup"><span data-stu-id="23fd2-216">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).</span></span>
- <span data-ttu-id="23fd2-217">Группы определяются в центрах.</span><span class="sxs-lookup"><span data-stu-id="23fd2-217">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="23fd2-218">В SignalR вы можете определить именованные группы для широковещательной рассылки подмножествам подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="23fd2-218">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="23fd2-219">Группы обслуживаются отдельно для каждого концентратора.</span><span class="sxs-lookup"><span data-stu-id="23fd2-219">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="23fd2-220">Например, группа с именем "Администраторы" будет включать в себя один набор клиентов для `ContosoChatHub` класса, и одно и то же имя группы будет ссылаться на другой набор клиентов для класса `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-220">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="23fd2-221">Определение методов в классе Hub, которые могут вызываться клиентами</span><span class="sxs-lookup"><span data-stu-id="23fd2-221">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="23fd2-222">Чтобы предоставить метод в концентраторе, который должен быть вызываемым из клиента, объявите открытый метод, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="23fd2-222">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="23fd2-223">Можно указать тип возвращаемого значения и параметры, включая сложные типы и массивы, как в любом C# методе.</span><span class="sxs-lookup"><span data-stu-id="23fd2-223">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="23fd2-224">Все данные, получаемые в параметрах или возвращаемые вызывающему объекту, передаются между клиентом и сервером с помощью JSON, а SignalR обрабатывает привязку сложных объектов и массивов объектов автоматически.</span><span class="sxs-lookup"><span data-stu-id="23fd2-224">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="23fd2-225">Неоднородный регистр имен методов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="23fd2-225">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="23fd2-226">По умолчанию клиенты JavaScript ссылаются на методы концентратора, используя версию имени метода в стиле Camel.</span><span class="sxs-lookup"><span data-stu-id="23fd2-226">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="23fd2-227">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать соглашениям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23fd2-227">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="23fd2-228">**Server**</span><span class="sxs-lookup"><span data-stu-id="23fd2-228">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="23fd2-229">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="23fd2-229">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="23fd2-230">Если необходимо указать другое имя для использования клиентами, добавьте атрибут `HubMethodName`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-230">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="23fd2-231">**Server**</span><span class="sxs-lookup"><span data-stu-id="23fd2-231">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="23fd2-232">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="23fd2-232">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="23fd2-233">Время асинхронного выполнения</span><span class="sxs-lookup"><span data-stu-id="23fd2-233">When to execute asynchronously</span></span>

<span data-ttu-id="23fd2-234">Если метод будет длительно выполнен или должен выполнить работу, которая будет заключаться в ожидании (например, при поиске базы данных или вызове веб-службы), сделайте метод концентратора асинхронным, возвращая [задачу](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (вместо `void` Return) или [Task&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) объект (вместо `T`ного типа).</span><span class="sxs-lookup"><span data-stu-id="23fd2-234">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="23fd2-235">Когда вы возвращаете объект `Task` из метода, SignalR ожидает завершения `Task`, а затем отправляет неупакованный результат обратно клиенту, поэтому нет никакой разницы в способе кодирования вызова метода в клиенте.</span><span class="sxs-lookup"><span data-stu-id="23fd2-235">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="23fd2-236">Создание метода концентратора асинхронно позволяет избежать блокировки соединения при использовании транспорта WebSocket.</span><span class="sxs-lookup"><span data-stu-id="23fd2-236">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="23fd2-237">Если метод концентратора выполняется синхронно, а транспорт — WebSocket, последующие вызовы методов в концентраторе от одного клиента блокируются до завершения метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="23fd2-237">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="23fd2-238">В следующем примере показан тот же метод, закодированный для синхронного или асинхронного выполнения, за которым следует код клиента JavaScript, который работает для вызова любой версии.</span><span class="sxs-lookup"><span data-stu-id="23fd2-238">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="23fd2-239">**Рабатывают**</span><span class="sxs-lookup"><span data-stu-id="23fd2-239">**Synchronous**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="23fd2-240">**Асинхронный — ASP.NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="23fd2-240">**Asynchronous - ASP.NET 4.5**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="23fd2-241">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="23fd2-241">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="23fd2-242">Дополнительные сведения об использовании асинхронных методов в ASP.NET 4,5 см. в разделе [Использование асинхронных методов в ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="23fd2-242">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="23fd2-243">Определение перегрузок</span><span class="sxs-lookup"><span data-stu-id="23fd2-243">Defining Overloads</span></span>

<span data-ttu-id="23fd2-244">Если требуется определить перегрузки для метода, количество параметров в каждой перегрузке должно отличаться.</span><span class="sxs-lookup"><span data-stu-id="23fd2-244">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="23fd2-245">Если вы отличаете перегрузку только путем указания других типов параметров, класс Hub будет компилироваться, но служба SignalR выдаст исключение во время выполнения, когда клиенты пытаются вызвать одну из перегрузок.</span><span class="sxs-lookup"><span data-stu-id="23fd2-245">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="23fd2-246">Вызов клиентских методов из класса HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-246">How to call client methods from the Hub class</span></span>

<span data-ttu-id="23fd2-247">Чтобы вызывать клиентские методы с сервера, используйте свойство `Clients` в методе в классе Hub.</span><span class="sxs-lookup"><span data-stu-id="23fd2-247">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="23fd2-248">В следующем примере показан серверный код, который вызывает `addNewMessageToPage` на всех подключенных клиентах, и клиентский код, определяющий метод в клиенте JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23fd2-248">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="23fd2-249">**Server**</span><span class="sxs-lookup"><span data-stu-id="23fd2-249">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

<span data-ttu-id="23fd2-250">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="23fd2-250">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

<span data-ttu-id="23fd2-251">Невозможно получить возвращаемое значение из клиентского метода. такой синтаксис, как `int x = Clients.All.add(1,1)`, не работает.</span><span class="sxs-lookup"><span data-stu-id="23fd2-251">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="23fd2-252">Для параметров можно указать сложные типы и массивы.</span><span class="sxs-lookup"><span data-stu-id="23fd2-252">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="23fd2-253">В следующем примере сложный тип передается клиенту в параметре метода.</span><span class="sxs-lookup"><span data-stu-id="23fd2-253">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="23fd2-254">**Серверный код, вызывающий клиентский метод с помощью сложного объекта**</span><span class="sxs-lookup"><span data-stu-id="23fd2-254">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

<span data-ttu-id="23fd2-255">**Серверный код, определяющий сложный объект**</span><span class="sxs-lookup"><span data-stu-id="23fd2-255">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

<span data-ttu-id="23fd2-256">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="23fd2-256">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="23fd2-257">Выбор клиентов, получающих RPC</span><span class="sxs-lookup"><span data-stu-id="23fd2-257">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="23fd2-258">Свойство Clients возвращает объект [хубконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) , который предоставляет несколько параметров для указания клиентов, которые будут принимать RPC:</span><span class="sxs-lookup"><span data-stu-id="23fd2-258">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="23fd2-259">Все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="23fd2-259">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- <span data-ttu-id="23fd2-260">Только вызывающий клиент.</span><span class="sxs-lookup"><span data-stu-id="23fd2-260">Only the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="23fd2-261">Все клиенты, кроме вызывающего клиента.</span><span class="sxs-lookup"><span data-stu-id="23fd2-261">All clients except the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="23fd2-262">Конкретный клиент, идентифицируемый по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-262">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    <span data-ttu-id="23fd2-263">В этом примере вызывается `addContosoChatMessageToPage` на вызывающем клиенте и действует тот же результат, что и при использовании `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-263">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="23fd2-264">Все подключенные клиенты, за исключением указанных клиентов, идентифицируемые по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-264">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- <span data-ttu-id="23fd2-265">Все подключенные клиенты в указанной группе.</span><span class="sxs-lookup"><span data-stu-id="23fd2-265">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- <span data-ttu-id="23fd2-266">Все подключенные клиенты в указанной группе, за исключением указанных клиентов, идентифицируемые по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-266">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- <span data-ttu-id="23fd2-267">Все подключенные клиенты в указанной группе, кроме вызывающего клиента.</span><span class="sxs-lookup"><span data-stu-id="23fd2-267">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="23fd2-268">Нет проверки во время компиляции для имен методов</span><span class="sxs-lookup"><span data-stu-id="23fd2-268">No compile-time validation for method names</span></span>

<span data-ttu-id="23fd2-269">Указанное имя метода интерпретируется как динамический объект, что означает отсутствие в нем IntelliSense или проверку во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="23fd2-269">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="23fd2-270">Выражение вычисляется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-270">The expression is evaluated at run time.</span></span> <span data-ttu-id="23fd2-271">При вызове метода SignalR отправляет клиенту имя метода и значения параметров, а если клиент имеет метод, совпадающий с именем, вызывается метод и ему передаются значения параметров.</span><span class="sxs-lookup"><span data-stu-id="23fd2-271">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="23fd2-272">Если на клиенте не найден соответствующий метод, ошибка не возникает.</span><span class="sxs-lookup"><span data-stu-id="23fd2-272">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="23fd2-273">Сведения о формате данных, которые SignalR передает клиенту в фоновом режиме при вызове клиентского метода, см. [в разделе Общие](index.md)сведения о SignalR.</span><span class="sxs-lookup"><span data-stu-id="23fd2-273">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](index.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="23fd2-274">Сопоставление имен методов без учета регистра</span><span class="sxs-lookup"><span data-stu-id="23fd2-274">Case-insensitive method name matching</span></span>

<span data-ttu-id="23fd2-275">Сопоставление имен методов не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="23fd2-275">Method name matching is case-insensitive.</span></span> <span data-ttu-id="23fd2-276">Например, `Clients.All.addContosoChatMessageToPage` на сервере будет выполнять `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`или `addContosoChatMessageToPage` на клиенте.</span><span class="sxs-lookup"><span data-stu-id="23fd2-276">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="23fd2-277">Асинхронное выполнение</span><span class="sxs-lookup"><span data-stu-id="23fd2-277">Asynchronous execution</span></span>

<span data-ttu-id="23fd2-278">Вызываемый метод выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="23fd2-278">The method that you call executes asynchronously.</span></span> <span data-ttu-id="23fd2-279">Любой код, который поступает после вызова метода клиенту, будет выполняться немедленно, не дожидаясь завершения передачи данных для клиентов SignalR, если не указать, что последующие строки кода должны ожидать завершения метода.</span><span class="sxs-lookup"><span data-stu-id="23fd2-279">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="23fd2-280">В следующих примерах кода показано, как последовательно выполнить два метода клиента: один использует код, который работает в .NET 4,5, и один с кодом, который работает в .NET 4.</span><span class="sxs-lookup"><span data-stu-id="23fd2-280">The following code examples show how to execute two client methods sequentially, one using code that works in .NET 4.5, and one using code that works in .NET 4.</span></span>

<span data-ttu-id="23fd2-281">**Пример .NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="23fd2-281">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

<span data-ttu-id="23fd2-282">**Пример .NET 4**</span><span class="sxs-lookup"><span data-stu-id="23fd2-282">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

<span data-ttu-id="23fd2-283">Если вы используете `await` или `ContinueWith`, чтобы дождаться завершения клиентского метода до выполнения следующей строки кода, это не означает, что клиенты фактически получат сообщение перед выполнением следующей строки кода.</span><span class="sxs-lookup"><span data-stu-id="23fd2-283">If you use `await` or `ContinueWith` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="23fd2-284">"Завершение" вызова клиентского метода означает только то, что SignalR выполнил все необходимое для отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-284">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="23fd2-285">Если требуется проверка того, что клиенты получили сообщение, необходимо программировать механизм самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="23fd2-285">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="23fd2-286">Например, можно закодировать метод `MessageReceived` в концентраторе, а в методе `addContosoChatMessageToPage` на клиенте можно вызвать `MessageReceived` после выполнения любой работы, которую необходимо выполнить на клиенте.</span><span class="sxs-lookup"><span data-stu-id="23fd2-286">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="23fd2-287">В `MessageReceived` в центре можно выполнять любые действия, зависящие от фактического приема и обработки исходного вызова метода.</span><span class="sxs-lookup"><span data-stu-id="23fd2-287">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="23fd2-288">Использование строковой переменной в качестве имени метода</span><span class="sxs-lookup"><span data-stu-id="23fd2-288">How to use a string variable as the method name</span></span>

<span data-ttu-id="23fd2-289">Если вы хотите вызвать клиентский метод, используя строковую переменную в качестве имени метода, приведите `Clients.All` (или `Clients.Others`, `Clients.Caller`и т. д.) `IClientProxy`, а затем вызовите [Invoke (имя_метода, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="23fd2-289">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="23fd2-290">Управление членством в группах из класса HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-290">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="23fd2-291">Группы в SignalR предоставляют метод для вещания сообщений в указанные подмножества подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="23fd2-291">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="23fd2-292">Группа может иметь любое количество клиентов, а клиент может быть членом любого числа групп.</span><span class="sxs-lookup"><span data-stu-id="23fd2-292">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="23fd2-293">Для управления членством в группе используйте методы [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) и [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) , предоставляемые свойством `Groups` класса Hub.</span><span class="sxs-lookup"><span data-stu-id="23fd2-293">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="23fd2-294">В следующем примере показаны методы `Groups.Add` и `Groups.Remove`, используемые в методах концентратора, которые вызываются клиентским кодом, а затем — клиентский код JavaScript, который вызывает их.</span><span class="sxs-lookup"><span data-stu-id="23fd2-294">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="23fd2-295">**Server**</span><span class="sxs-lookup"><span data-stu-id="23fd2-295">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

<span data-ttu-id="23fd2-296">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="23fd2-296">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

<span data-ttu-id="23fd2-297">Вам не нужно явно создавать группы.</span><span class="sxs-lookup"><span data-stu-id="23fd2-297">You don't have to explicitly create groups.</span></span> <span data-ttu-id="23fd2-298">Фактически группа создается автоматически при первом указании имени в вызове `Groups.Add`и удаляется при удалении последнего подключения из членства в нем.</span><span class="sxs-lookup"><span data-stu-id="23fd2-298">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="23fd2-299">Отсутствует API для получения списка членства в группе или списка групп.</span><span class="sxs-lookup"><span data-stu-id="23fd2-299">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="23fd2-300">SignalR отправляет сообщения клиентам и группам, основанным на [модели публикации и подтипа](http://en.wikipedia.org/wiki/Publish/subscribe), а сервер не поддерживает списки групп или членства в группах.</span><span class="sxs-lookup"><span data-stu-id="23fd2-300">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="23fd2-301">Это обеспечивает максимальную масштабируемость, так как при добавлении узла в веб-ферму любое состояние, которое обслуживает SignalR, должно быть распространено на новый узел.</span><span class="sxs-lookup"><span data-stu-id="23fd2-301">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="23fd2-302">Асинхронное выполнение методов Add и Remove</span><span class="sxs-lookup"><span data-stu-id="23fd2-302">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="23fd2-303">Методы `Groups.Add` и `Groups.Remove` выполняются асинхронно.</span><span class="sxs-lookup"><span data-stu-id="23fd2-303">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="23fd2-304">Если вы хотите добавить клиент в группу и сразу же отправить сообщение клиенту с помощью группы, необходимо убедиться в том, что метод `Groups.Add` завершается первым.</span><span class="sxs-lookup"><span data-stu-id="23fd2-304">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="23fd2-305">В следующих примерах кода показано, как это сделать, с помощью кода, который работает в .NET 4,5, а другой — с помощью кода, который работает в .NET 4.</span><span class="sxs-lookup"><span data-stu-id="23fd2-305">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4</span></span>

<span data-ttu-id="23fd2-306">**Пример .NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="23fd2-306">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="23fd2-307">**Пример .NET 4**</span><span class="sxs-lookup"><span data-stu-id="23fd2-307">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="23fd2-308">Сохранение членства в группах</span><span class="sxs-lookup"><span data-stu-id="23fd2-308">Group membership persistence</span></span>

<span data-ttu-id="23fd2-309">SignalR отслеживает соединения, а не пользователей, поэтому, если требуется, чтобы пользователь настроился в одной группе каждый раз, когда пользователь устанавливает соединение, необходимо вызывать `Groups.Add` каждый раз, когда пользователь устанавливает новое соединение.</span><span class="sxs-lookup"><span data-stu-id="23fd2-309">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="23fd2-310">После временной потери подключения иногда SignalR может автоматически восстановить подключение.</span><span class="sxs-lookup"><span data-stu-id="23fd2-310">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="23fd2-311">В этом случае SignalR восстанавливает одно и то же подключение, не устанавливая новое подключение, поэтому членство в группе клиента автоматически восстанавливается.</span><span class="sxs-lookup"><span data-stu-id="23fd2-311">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="23fd2-312">Это возможно даже в том случае, если временный перерыв является результатом перезагрузки или сбоя сервера, так как состояние подключения для каждого клиента, включая членство в группах, передается клиенту.</span><span class="sxs-lookup"><span data-stu-id="23fd2-312">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="23fd2-313">Если сервер выходит из строя и заменяется новым сервером до истечения времени ожидания подключения, клиент может автоматически подключиться к новому серверу и повторно зарегистрировать в группах, членом которых он является.</span><span class="sxs-lookup"><span data-stu-id="23fd2-313">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="23fd2-314">Если подключение не может быть восстановлено автоматически после потери подключения или истечения времени ожидания соединения или когда клиент отключается (например, когда браузер переходит на новую страницу), членство в группах теряется.</span><span class="sxs-lookup"><span data-stu-id="23fd2-314">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="23fd2-315">При следующем подключении пользователя будет установлено новое подключение.</span><span class="sxs-lookup"><span data-stu-id="23fd2-315">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="23fd2-316">Чтобы обеспечить членство в группах, когда один и тот же пользователь устанавливает новое подключение, приложение должно отслеживание взаимосвязей между пользователями и группами и восстанавливать членство в группах каждый раз, когда пользователь устанавливает новое подключение.</span><span class="sxs-lookup"><span data-stu-id="23fd2-316">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="23fd2-317">Дополнительные сведения о подключениях и повторном подключении см. в разделе [как управлять событиями времени существования соединения в классе Hub](#connectionlifetime) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="23fd2-317">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="23fd2-318">Группы с одним пользователем</span><span class="sxs-lookup"><span data-stu-id="23fd2-318">Single-user groups</span></span>

<span data-ttu-id="23fd2-319">Приложения, использующие SignalR, обычно должны вести отслеживание взаимосвязей между пользователями и соединениями, чтобы узнать, какой пользователь отправил сообщение и какие пользователи должны получать сообщение.</span><span class="sxs-lookup"><span data-stu-id="23fd2-319">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="23fd2-320">Группы используются в одном из двух часто используемых шаблонов.</span><span class="sxs-lookup"><span data-stu-id="23fd2-320">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="23fd2-321">Группы с одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="23fd2-321">Single-user groups.</span></span>

    <span data-ttu-id="23fd2-322">Можно указать имя пользователя в качестве имени группы и добавить текущий идентификатор подключения в группу при каждом подключении или повторном подключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="23fd2-322">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="23fd2-323">Для отправки сообщений пользователю, который отправляется в группу.</span><span class="sxs-lookup"><span data-stu-id="23fd2-323">To send messages to the user you send to the group.</span></span> <span data-ttu-id="23fd2-324">Недостаток этого метода заключается в том, что группа не дает вам способа выяснить, находится ли пользователь в сети или в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="23fd2-324">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="23fd2-325">Следите за связями между именами пользователей и идентификаторами подключений.</span><span class="sxs-lookup"><span data-stu-id="23fd2-325">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="23fd2-326">Можно сохранить связь между именем пользователя и одним или несколькими идентификаторами соединения в словаре или базе данных, а также обновлять сохраненные данные при каждом подключении или отключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="23fd2-326">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="23fd2-327">Чтобы отправить сообщения пользователю, укажите идентификаторы соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-327">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="23fd2-328">Недостаток этого метода заключается в том, что он занимает больше памяти.</span><span class="sxs-lookup"><span data-stu-id="23fd2-328">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="23fd2-329">Как управлять событиями времени жизни соединения в классе HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-329">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="23fd2-330">Типичными причинами обработки событий времени существования соединения являются отслеживание того, подключено ли пользователь, а также отслеживается связь между именами пользователей и идентификаторами подключений.</span><span class="sxs-lookup"><span data-stu-id="23fd2-330">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="23fd2-331">Чтобы запустить собственный код при подключении или отключении клиентов, переопределите `OnConnected`, `OnDisconnected`и `OnReconnected` виртуальные методы класса Hub, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="23fd2-331">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="23fd2-332">При вызове onconnected, OnDisconnection и Онреконнектед</span><span class="sxs-lookup"><span data-stu-id="23fd2-332">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="23fd2-333">Каждый раз, когда браузер переходит на новую страницу, необходимо установить новое соединение, означающее, что SignalR выполнит метод `OnDisconnected`, а затем метод `OnConnected`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-333">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="23fd2-334">SignalR всегда создает новый идентификатор подключения при установлении нового соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-334">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="23fd2-335">Метод `OnReconnected` вызывается при временном разрыве соединения, при котором SignalR может автоматически восстановиться из, например при временном отключении и повторном подключении кабеля до истечения времени ожидания соединения. Метод `OnDisconnected` вызывается, когда клиент отключается, и SignalR не может автоматически подключиться, например, когда браузер переходит на новую страницу.</span><span class="sxs-lookup"><span data-stu-id="23fd2-335">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="23fd2-336">Таким образом, возможная последовательность событий для данного клиента — `OnConnected`, `OnReconnected`, `OnDisconnected`; или `OnConnected``OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-336">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="23fd2-337">Вы не увидите последовательность `OnConnected`, `OnDisconnected``OnReconnected` для данного подключения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-337">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="23fd2-338">Метод `OnDisconnected` не вызывается в некоторых сценариях, например при отключении сервера или при перезапуске домена приложения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-338">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="23fd2-339">Когда другой сервер поступает в сети или домен приложения завершает свой перезапуск, некоторые клиенты могут повторно подключиться и запустить событие `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-339">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="23fd2-340">Дополнительные сведения см. [в разделе Основные сведения и обработка событий времени жизни подключения в SignalR](index.md).</span><span class="sxs-lookup"><span data-stu-id="23fd2-340">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="23fd2-341">Состояние вызывающего объекта не заполнено</span><span class="sxs-lookup"><span data-stu-id="23fd2-341">Caller state not populated</span></span>

<span data-ttu-id="23fd2-342">Методы обработчика событий времени жизни соединения вызываются с сервера. Это означает, что любое состояние, помещаемое в объект `state` на клиенте, не будет заполнено в свойстве `Caller` на сервере.</span><span class="sxs-lookup"><span data-stu-id="23fd2-342">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="23fd2-343">Дополнительные сведения об объекте `state` и свойстве `Caller` см. в разделе [Передача состояния между клиентами и классом Hub](#passstate) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="23fd2-343">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="23fd2-344">Получение сведений о клиенте из свойства Context</span><span class="sxs-lookup"><span data-stu-id="23fd2-344">How to get information about the client from the Context property</span></span>

<span data-ttu-id="23fd2-345">Чтобы получить сведения о клиенте, используйте свойство `Context` класса Hub.</span><span class="sxs-lookup"><span data-stu-id="23fd2-345">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="23fd2-346">Свойство `Context` возвращает объект [хубкаллерконтекст](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) , который предоставляет доступ к следующим сведениям:</span><span class="sxs-lookup"><span data-stu-id="23fd2-346">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="23fd2-347">Идентификатор подключения вызывающего клиента.</span><span class="sxs-lookup"><span data-stu-id="23fd2-347">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    <span data-ttu-id="23fd2-348">Идентификатор подключения — это идентификатор GUID, назначенный SignalR (вы не можете указать значение в своем коде).</span><span class="sxs-lookup"><span data-stu-id="23fd2-348">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="23fd2-349">Для каждого подключения существует один идентификатор подключения, и один и тот же идентификатор подключения используется всеми концентраторами, если в приложении имеется несколько концентраторов.</span><span class="sxs-lookup"><span data-stu-id="23fd2-349">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="23fd2-350">Данные заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="23fd2-350">HTTP header data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    <span data-ttu-id="23fd2-351">Также можно получить заголовки HTTP из `Context.Headers`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-351">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="23fd2-352">Причиной нескольких ссылок на одно и то же самое является то, что `Context.Headers` был создан первым, свойство `Context.Request` было добавлено позже и `Context.Headers` было сохранено для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="23fd2-352">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="23fd2-353">Данные строки запроса.</span><span class="sxs-lookup"><span data-stu-id="23fd2-353">Query string data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    <span data-ttu-id="23fd2-354">Можно также получить данные строки запроса из `Context.QueryString`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-354">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="23fd2-355">Строка запроса, полученная в этом свойстве, используется с HTTP-запросом, который установил подключение SignalR.</span><span class="sxs-lookup"><span data-stu-id="23fd2-355">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="23fd2-356">Можно добавить параметры строки запроса в клиент, настроив соединение, что является удобным способом передачи данных о клиенте с клиента на сервер.</span><span class="sxs-lookup"><span data-stu-id="23fd2-356">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="23fd2-357">В следующем примере показан один из способов добавления строки запроса в клиент JavaScript при использовании созданного прокси.</span><span class="sxs-lookup"><span data-stu-id="23fd2-357">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    <span data-ttu-id="23fd2-358">Дополнительные сведения о настройке параметров строки запроса см. в руководствах по API для клиентов [JavaScript](index.md) и [.NET](index.md) .</span><span class="sxs-lookup"><span data-stu-id="23fd2-358">For more information about setting query string parameters, see the API guides for the [JavaScript](index.md) and [.NET](index.md) clients.</span></span>

    <span data-ttu-id="23fd2-359">Метод перевозки, используемый для соединения, можно найти в данных строки запроса, а также с другими внутренними значениями, используемыми SignalR:</span><span class="sxs-lookup"><span data-stu-id="23fd2-359">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    <span data-ttu-id="23fd2-360">Значение `transportMethod` будет равно "WebSockets", "Серверсентевентс", "Фореверфраме" или "Лонгполлинг".</span><span class="sxs-lookup"><span data-stu-id="23fd2-360">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="23fd2-361">Обратите внимание, что если проверить это значение в методе обработчика событий `OnConnected`, то в некоторых сценариях можно изначально получить значение транспорта, которое не является окончательным согласованным транспортным методом для соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-361">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="23fd2-362">В этом случае метод выдаст исключение и будет вызван позже, когда будет установлен окончательный метод транспортировки.</span><span class="sxs-lookup"><span data-stu-id="23fd2-362">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="23fd2-363">Сеанс.</span><span class="sxs-lookup"><span data-stu-id="23fd2-363">Cookies.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="23fd2-364">Вы также можете получать файлы cookie из `Context.RequestCookies`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-364">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="23fd2-365">сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="23fd2-365">User information.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- <span data-ttu-id="23fd2-366">Объект HttpContext для запроса:</span><span class="sxs-lookup"><span data-stu-id="23fd2-366">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    <span data-ttu-id="23fd2-367">Используйте этот метод вместо получения `HttpContext.Current` для получения объекта `HttpContext` для подключения SignalR.</span><span class="sxs-lookup"><span data-stu-id="23fd2-367">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="23fd2-368">Передача состояния между клиентами и классом HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-368">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="23fd2-369">Прокси клиента предоставляет объект `state`, в котором можно хранить данные, которые необходимо передать на сервер при каждом вызове метода.</span><span class="sxs-lookup"><span data-stu-id="23fd2-369">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="23fd2-370">На сервере эти данные можно получить в свойстве `Clients.Caller` в методах концентратора, которые вызываются клиентами.</span><span class="sxs-lookup"><span data-stu-id="23fd2-370">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="23fd2-371">Свойство `Clients.Caller` не заполняется методами обработчика событий времени жизни соединения `OnConnected`, `OnDisconnected`и `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-371">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="23fd2-372">Создание или обновление данных в объекте `state`, а свойство `Clients.Caller` работает в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="23fd2-372">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="23fd2-373">Можно обновить значения на сервере и передать их обратно клиенту.</span><span class="sxs-lookup"><span data-stu-id="23fd2-373">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="23fd2-374">В следующем примере показан код клиента JavaScript, который сохраняет состояние для передачи на сервер при каждом вызове метода.</span><span class="sxs-lookup"><span data-stu-id="23fd2-374">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

<span data-ttu-id="23fd2-375">В следующем примере показан эквивалентный код в клиенте .NET.</span><span class="sxs-lookup"><span data-stu-id="23fd2-375">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

<span data-ttu-id="23fd2-376">В классе Hub можно получить доступ к этим данным в свойстве `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-376">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="23fd2-377">В следующем примере показан код, который извлекает состояние, на которое ссылается предыдущий пример.</span><span class="sxs-lookup"><span data-stu-id="23fd2-377">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="23fd2-378">Этот механизм для сохранения состояния не предназначен для больших объемов данных, так как все, что вы поместили в `state` или `Clients.Caller` свойство, обложились с помощью каждого вызова метода.</span><span class="sxs-lookup"><span data-stu-id="23fd2-378">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="23fd2-379">Это удобно для небольших элементов, таких как имена пользователей или счетчики.</span><span class="sxs-lookup"><span data-stu-id="23fd2-379">It's useful for smaller items such as user names or counters.</span></span>

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="23fd2-380">Как выполнять обработку ошибок в классе HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-380">How to handle errors in the Hub class</span></span>

<span data-ttu-id="23fd2-381">Чтобы обрабатывались ошибки, возникающие в методах класса Hub, используйте один или оба следующих метода.</span><span class="sxs-lookup"><span data-stu-id="23fd2-381">To handle errors that occur in your Hub class methods, use one or both of the following methods:</span></span>

- <span data-ttu-id="23fd2-382">Заключите код метода в блоки try-catch и заносите в журнал объект исключения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-382">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="23fd2-383">В целях отладки можно отправить исключение клиенту, но в целях безопасности не рекомендуется отправлять подробные сведения клиентам в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="23fd2-383">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="23fd2-384">Создайте модуль конвейера концентраторов, который обрабатывает метод [онинкоминжеррор](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="23fd2-384">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="23fd2-385">В следующем примере показан модуль конвейера, в котором регистрируются ошибки, за которым следует код в Global. asax, который внедряет модуль в конвейер концентраторов.</span><span class="sxs-lookup"><span data-stu-id="23fd2-385">The following example shows a pipeline module that logs errors, followed by code in Global.asax that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

<span data-ttu-id="23fd2-386">Дополнительные сведения о модулях конвейера концентратора см. в подразделе [Настройка конвейера](#hubpipeline) концентраторов далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="23fd2-386">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="23fd2-387">Включение трассировки</span><span class="sxs-lookup"><span data-stu-id="23fd2-387">How to enable tracing</span></span>

<span data-ttu-id="23fd2-388">Чтобы включить трассировку на стороне сервера, добавьте элемент System. Diagnostics в файл Web. config, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="23fd2-388">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

<span data-ttu-id="23fd2-389">При запуске приложения в Visual Studio журналы можно просмотреть в окне **вывод** .</span><span class="sxs-lookup"><span data-stu-id="23fd2-389">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="23fd2-390">Вызов клиентских методов и управление группами извне класса HUB</span><span class="sxs-lookup"><span data-stu-id="23fd2-390">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="23fd2-391">Чтобы вызвать клиентские методы из другого класса, чем класс Hub, получите ссылку на объект контекста SignalR для концентратора и используйте его для вызова методов в клиенте или для управления группами.</span><span class="sxs-lookup"><span data-stu-id="23fd2-391">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="23fd2-392">Следующий пример `StockTicker` класс получает объект контекста, сохраняет его в экземпляре класса, сохраняет экземпляр класса в статическом свойстве и использует контекст из экземпляра одноэлементного класса для вызова метода `updateStockPrice` на клиентах, подключенных к концентратору с именем `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-392">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

<span data-ttu-id="23fd2-393">Если необходимо использовать контекст несколько раз в долгосрочном объекте, получите ссылку один раз и сохраните его вместо того, чтобы повторно получать его каждый раз.</span><span class="sxs-lookup"><span data-stu-id="23fd2-393">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="23fd2-394">Получение контекста однократно гарантирует, что SignalR отправляет сообщения клиентам в той же последовательности, в которой методы концентратора выполняют вызовы клиентских методов.</span><span class="sxs-lookup"><span data-stu-id="23fd2-394">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="23fd2-395">Руководство, в котором показано, как использовать контекст SignalR для концентратора, см. в разделе [серверное вещание с помощью ASP.NET SignalR](index.md).</span><span class="sxs-lookup"><span data-stu-id="23fd2-395">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](index.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="23fd2-396">Вызов методов клиента</span><span class="sxs-lookup"><span data-stu-id="23fd2-396">Calling client methods</span></span>

<span data-ttu-id="23fd2-397">Вы можете указать, какие клиенты будут принимать RPC, но при этом у вас будет меньше параметров, чем при вызове из класса Hub.</span><span class="sxs-lookup"><span data-stu-id="23fd2-397">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="23fd2-398">Причина в том, что контекст не связан с определенным вызовом от клиента, поэтому все методы, которым требуются знания о текущем ИДЕНТИФИКАТОРе соединения, такие как `Clients.Others`или `Clients.Caller`или `Clients.OthersInGroup`, недоступны.</span><span class="sxs-lookup"><span data-stu-id="23fd2-398">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="23fd2-399">Доступны следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="23fd2-399">The following options are available:</span></span>

- <span data-ttu-id="23fd2-400">Все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="23fd2-400">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- <span data-ttu-id="23fd2-401">Конкретный клиент, идентифицируемый по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-401">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- <span data-ttu-id="23fd2-402">Все подключенные клиенты, за исключением указанных клиентов, идентифицируемые по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-402">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- <span data-ttu-id="23fd2-403">Все подключенные клиенты в указанной группе.</span><span class="sxs-lookup"><span data-stu-id="23fd2-403">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- <span data-ttu-id="23fd2-404">Все подключенные клиенты в указанной группе, за исключением указанных клиентов, идентифицируемые по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="23fd2-404">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

<span data-ttu-id="23fd2-405">При вызове класса, не являющегося концентратором, из методов класса Hub можно передать текущий идентификатор соединения и использовать его с `Clients.Client`, `Clients.AllExcept`или `Clients.Group` для имитации `Clients.Caller`, `Clients.Others`или `Clients.OthersInGroup`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-405">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="23fd2-406">В следующем примере класс `MoveShapeHub` передает идентификатор подключения классу `Broadcaster`, чтобы класс `Broadcaster` мог имитировать `Clients.Others`.</span><span class="sxs-lookup"><span data-stu-id="23fd2-406">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="23fd2-407">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="23fd2-407">Managing group membership</span></span>

<span data-ttu-id="23fd2-408">Для управления группами доступны те же параметры, что и в классе Hub.</span><span class="sxs-lookup"><span data-stu-id="23fd2-408">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="23fd2-409">Добавление клиента в группу</span><span class="sxs-lookup"><span data-stu-id="23fd2-409">Add a client to a group</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- <span data-ttu-id="23fd2-410">Удаление клиента из группы</span><span class="sxs-lookup"><span data-stu-id="23fd2-410">Remove a client from a group</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="23fd2-411">Настройка конвейера концентраторов</span><span class="sxs-lookup"><span data-stu-id="23fd2-411">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="23fd2-412">SignalR позволяет внедрять собственный код в конвейер концентратора.</span><span class="sxs-lookup"><span data-stu-id="23fd2-412">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="23fd2-413">В следующем примере показан пользовательский модуль конвейера концентратора, который регистрирует каждый входящий вызов метода, полученный от клиента, и вызов исходящего метода, вызываемого на клиенте:</span><span class="sxs-lookup"><span data-stu-id="23fd2-413">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

<span data-ttu-id="23fd2-414">Следующий код в файле *Global. asax* регистрирует модуль для запуска в конвейере концентратора:</span><span class="sxs-lookup"><span data-stu-id="23fd2-414">The following code in the *Global.asax* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

<span data-ttu-id="23fd2-415">Существует множество различных методов, которые можно переопределить.</span><span class="sxs-lookup"><span data-stu-id="23fd2-415">There are many different methods that you can override.</span></span> <span data-ttu-id="23fd2-416">Полный список см. в разделе [методы хубпипелинемодуле](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="23fd2-416">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
