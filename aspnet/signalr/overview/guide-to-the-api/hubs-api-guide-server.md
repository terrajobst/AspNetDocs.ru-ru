---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: Путеводитель по API концентраторов SignalR ASP.NET — серверC#() | Документация Майкрософт
author: bradygaster
description: В этом документе приводятся общие сведения о программировании на стороне сервера API концентраторов SignalR ASP.NET для SignalR версии 2 с примерами кода...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431370"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="5b999-103">Путеводитель по API концентраторов SignalR ASP.NET — серверC#()</span><span class="sxs-lookup"><span data-stu-id="5b999-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="5b999-104">[Патрик Флетчера](https://github.com/pfletcher), [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5b999-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5b999-105">В этом документе приводятся общие сведения о программировании на стороне сервера API концентраторов SignalR ASP.NET для SignalR версии 2 с примерами кода, демонстрирующими общие параметры.</span><span class="sxs-lookup"><span data-stu-id="5b999-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="5b999-106">API концентраторов SignalR позволяет выполнять удаленные вызовы процедур (RPC) с сервера на подключенные клиенты и с клиентов на сервер.</span><span class="sxs-lookup"><span data-stu-id="5b999-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="5b999-107">В серверном коде определяются методы, которые могут вызываться клиентами, и вызываются методы, которые выполняются на клиенте.</span><span class="sxs-lookup"><span data-stu-id="5b999-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="5b999-108">В клиентском коде определяются методы, которые могут быть вызваны с сервера, а также вызываются методы, которые выполняются на сервере.</span><span class="sxs-lookup"><span data-stu-id="5b999-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="5b999-109">Этот механизм отвечает за все клиентские коммуникации.</span><span class="sxs-lookup"><span data-stu-id="5b999-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="5b999-110">SignalR также предлагает интерфейс API более низкого уровня, называемый постоянными подключениями.</span><span class="sxs-lookup"><span data-stu-id="5b999-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="5b999-111">Общие сведения о SignalR, концентраторах и постоянных подключениях см. [в статье Введение в SignalR 2](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="5b999-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="5b999-112">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="5b999-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="5b999-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5b999-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="5b999-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5b999-114">.NET 4.5</span></span>
> - <span data-ttu-id="5b999-115">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="5b999-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="5b999-116">Версии разделов</span><span class="sxs-lookup"><span data-stu-id="5b999-116">Topic versions</span></span>
> 
> <span data-ttu-id="5b999-117">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="5b999-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="5b999-118">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="5b999-118">Questions and comments</span></span>
> 
> <span data-ttu-id="5b999-119">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5b999-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5b999-120">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="5b999-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="5b999-121">Обзор</span><span class="sxs-lookup"><span data-stu-id="5b999-121">Overview</span></span>

<span data-ttu-id="5b999-122">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="5b999-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="5b999-123">Регистрация по промежуточного слоя SignalR</span><span class="sxs-lookup"><span data-stu-id="5b999-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="5b999-124">URL-адрес/SignalR</span><span class="sxs-lookup"><span data-stu-id="5b999-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="5b999-125">Настройка параметров SignalR</span><span class="sxs-lookup"><span data-stu-id="5b999-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="5b999-126">Создание и использование классов концентратора</span><span class="sxs-lookup"><span data-stu-id="5b999-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="5b999-127">Время существования объекта концентратора</span><span class="sxs-lookup"><span data-stu-id="5b999-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="5b999-128">Неоднородный регистр имен концентраторов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="5b999-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="5b999-129">Несколько концентраторов</span><span class="sxs-lookup"><span data-stu-id="5b999-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="5b999-130">Строго типизированные концентраторы</span><span class="sxs-lookup"><span data-stu-id="5b999-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="5b999-131">Определение методов в классе Hub, которые могут вызываться клиентами</span><span class="sxs-lookup"><span data-stu-id="5b999-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="5b999-132">Неоднородный регистр имен методов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="5b999-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="5b999-133">Время асинхронного выполнения</span><span class="sxs-lookup"><span data-stu-id="5b999-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="5b999-134">Определение перегрузок</span><span class="sxs-lookup"><span data-stu-id="5b999-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="5b999-135">Отчет о ходе выполнения вызовов метода концентратора</span><span class="sxs-lookup"><span data-stu-id="5b999-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="5b999-136">Вызов клиентских методов из класса HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="5b999-137">Выбор клиентов, получающих RPC</span><span class="sxs-lookup"><span data-stu-id="5b999-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="5b999-138">Нет проверки во время компиляции для имен методов</span><span class="sxs-lookup"><span data-stu-id="5b999-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="5b999-139">Сопоставление имен методов без учета регистра</span><span class="sxs-lookup"><span data-stu-id="5b999-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="5b999-140">Асинхронное выполнение</span><span class="sxs-lookup"><span data-stu-id="5b999-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="5b999-141">Управление членством в группах из класса HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="5b999-142">Асинхронное выполнение методов Add и Remove</span><span class="sxs-lookup"><span data-stu-id="5b999-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="5b999-143">Сохранение членства в группах</span><span class="sxs-lookup"><span data-stu-id="5b999-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="5b999-144">Группы с одним пользователем</span><span class="sxs-lookup"><span data-stu-id="5b999-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="5b999-145">Как управлять событиями времени жизни соединения в классе HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="5b999-146">При вызове onconnected, OnDisconnection и Онреконнектед</span><span class="sxs-lookup"><span data-stu-id="5b999-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="5b999-147">Состояние вызывающего объекта не заполнено</span><span class="sxs-lookup"><span data-stu-id="5b999-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="5b999-148">Получение сведений о клиенте из свойства Context</span><span class="sxs-lookup"><span data-stu-id="5b999-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="5b999-149">Передача состояния между клиентами и классом HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="5b999-150">Как выполнять обработку ошибок в классе HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="5b999-151">Вызов клиентских методов и управление группами извне класса HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="5b999-152">Вызов методов клиента</span><span class="sxs-lookup"><span data-stu-id="5b999-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="5b999-153">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="5b999-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="5b999-154">Включение трассировки</span><span class="sxs-lookup"><span data-stu-id="5b999-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="5b999-155">Настройка конвейера концентраторов</span><span class="sxs-lookup"><span data-stu-id="5b999-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="5b999-156">Документацию по программированию клиентов см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="5b999-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="5b999-157">Путеводитель по API концентраторов SignalR — клиент JavaScript</span><span class="sxs-lookup"><span data-stu-id="5b999-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="5b999-158">Путеводитель по API концентраторов SignalR — клиент .NET</span><span class="sxs-lookup"><span data-stu-id="5b999-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="5b999-159">Серверные компоненты SignalR 2 доступны только в .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="5b999-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="5b999-160">Серверы, на которых работает .NET 4,0, должны использовать SignalR v1. x.</span><span class="sxs-lookup"><span data-stu-id="5b999-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="5b999-161">Регистрация по промежуточного слоя SignalR</span><span class="sxs-lookup"><span data-stu-id="5b999-161">How to register SignalR middleware</span></span>

<span data-ttu-id="5b999-162">Чтобы определить маршрут, который клиенты будут использовать для подключения к концентратору, вызовите метод `MapSignalR` при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="5b999-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="5b999-163">`MapSignalR` является [методом расширения](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) для класса `OwinExtensions`.</span><span class="sxs-lookup"><span data-stu-id="5b999-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="5b999-164">В следующем примере показано, как определить маршрут концентраторов SignalR с помощью класса Startup OWIN.</span><span class="sxs-lookup"><span data-stu-id="5b999-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="5b999-165">При добавлении функций SignalR в приложение ASP.NET MVC убедитесь, что маршрут SignalR добавлен перед другими маршрутами.</span><span class="sxs-lookup"><span data-stu-id="5b999-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="5b999-166">Дополнительные сведения см. в разделе [учебник. Начало работы с SignalR 2 и MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="5b999-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="5b999-167">URL-адрес/SignalR</span><span class="sxs-lookup"><span data-stu-id="5b999-167">The /signalr URL</span></span>

<span data-ttu-id="5b999-168">По умолчанию URL-адрес маршрута, который будет использоваться клиентами для подключения к концентратору, — "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="5b999-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="5b999-169">(Не путайте этот URL-адрес с URL-адресом "/сигналр/хубс", который предназначен для автоматически созданного файла JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5b999-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="5b999-170">Дополнительные сведения о созданном прокси-сервере см. в статье [Путеводитель по API концентраторов SignalR — клиент JavaScript — созданный прокси-сервер и его назначение](hubs-api-guide-javascript-client.md#genproxy).)</span><span class="sxs-lookup"><span data-stu-id="5b999-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="5b999-171">В некоторых случаях этот базовый URL-адрес не может использоваться для SignalR; Например, в проекте есть папка с именем *SignalR* , и вы не хотите изменять имя.</span><span class="sxs-lookup"><span data-stu-id="5b999-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="5b999-172">В этом случае можно изменить базовый URL-адрес, как показано в следующих примерах (замените "/SignalR" в примере кода на нужный URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="5b999-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="5b999-173">**Серверный код, указывающий URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5b999-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="5b999-174">**Клиентский код JavaScript, указывающий URL-адрес (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5b999-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="5b999-175">**Клиентский код JavaScript, указывающий URL-адрес (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5b999-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="5b999-176">**Клиентский код .NET, указывающий URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5b999-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="5b999-177">Настройка параметров SignalR</span><span class="sxs-lookup"><span data-stu-id="5b999-177">Configuring SignalR Options</span></span>

<span data-ttu-id="5b999-178">Перегрузки метода `MapSignalR` позволяют указать настраиваемый URL-адрес, Пользовательский сопоставитель зависимостей и следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="5b999-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="5b999-179">Включение междоменных вызовов с помощью CORS или JSONP от клиентов браузера.</span><span class="sxs-lookup"><span data-stu-id="5b999-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="5b999-180">Как правило, если браузер загружает страницу из `http://contoso.com`, то подключение SignalR находится в том же домене, в `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="5b999-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="5b999-181">Если страница из `http://contoso.com` устанавливает подключение к `http://fabrikam.com/signalr`, то есть подключение между доменами.</span><span class="sxs-lookup"><span data-stu-id="5b999-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="5b999-182">По соображениям безопасности междоменные соединения отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5b999-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="5b999-183">Дополнительные сведения см. в статье [руководство по API концентраторов signalr ASP.NET. клиент JavaScript — как установить междоменное подключение](hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="5b999-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="5b999-184">Включить подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="5b999-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="5b999-185">При возникновении ошибок поведение SignalR по умолчанию — отправить клиенту сообщение уведомления без подробностей о том, что произошло.</span><span class="sxs-lookup"><span data-stu-id="5b999-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="5b999-186">Отправка подробных сведений об ошибках клиентам не рекомендуется в рабочей среде, так как пользователи-злоумышленники могут использовать эти сведения в атаках приложения.</span><span class="sxs-lookup"><span data-stu-id="5b999-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="5b999-187">Для устранения неполадок можно использовать этот параметр, чтобы временно включить более информативные отчеты об ошибках.</span><span class="sxs-lookup"><span data-stu-id="5b999-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="5b999-188">Отключите автоматически создаваемые прокси-файлы JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5b999-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="5b999-189">По умолчанию файл JavaScript с прокси для классов концентратора создается в ответ на URL-адрес «/сигналр/хубс».</span><span class="sxs-lookup"><span data-stu-id="5b999-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="5b999-190">Если вы не хотите использовать прокси-серверы JavaScript или хотите создать этот файл вручную и ссылаться на физический файл в клиентах, можно использовать этот параметр, чтобы отключить создание прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="5b999-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="5b999-191">Дополнительные сведения см. в статье [руководство по API концентраторов SignalR — клиент JavaScript. Создание физического файла для прокси-сервера, созданного SignalR](hubs-api-guide-javascript-client.md#manualproxy).</span><span class="sxs-lookup"><span data-stu-id="5b999-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="5b999-192">В следующем примере показано, как указать URL-адрес подключения SignalR и эти параметры в вызове метода `MapSignalR`.</span><span class="sxs-lookup"><span data-stu-id="5b999-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="5b999-193">Чтобы указать пользовательский URL-адрес, замените "/SignalR" в примере на URL-адрес, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="5b999-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="5b999-194">Создание и использование классов концентратора</span><span class="sxs-lookup"><span data-stu-id="5b999-194">How to create and use Hub classes</span></span>

<span data-ttu-id="5b999-195">Чтобы создать концентратор, создайте класс, производный от [Microsoft. ASPNET. SignalR. Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="5b999-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="5b999-196">В следующем примере показан простой класс концентратора для приложения разговора.</span><span class="sxs-lookup"><span data-stu-id="5b999-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="5b999-197">В этом примере подключенный клиент может вызвать метод `NewContosoChatMessage`, а когда это происходит, полученные данные передаются на все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="5b999-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="5b999-198">Время существования объекта концентратора</span><span class="sxs-lookup"><span data-stu-id="5b999-198">Hub object lifetime</span></span>

<span data-ttu-id="5b999-199">Вы не создаете экземпляр класса HUB или вызываете его методы из собственного кода на сервере. Все это выполняется конвейером концентраторов SignalR.</span><span class="sxs-lookup"><span data-stu-id="5b999-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="5b999-200">SignalR создает новый экземпляр класса Hub каждый раз, когда ему требуется выполнять операции концентратора, например, когда клиент подключается, отключается или вызывает метод на сервере.</span><span class="sxs-lookup"><span data-stu-id="5b999-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="5b999-201">Поскольку экземпляры класса Hub являются временными, их нельзя использовать для поддержания состояния от одного вызова метода к следующему.</span><span class="sxs-lookup"><span data-stu-id="5b999-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="5b999-202">Каждый раз, когда сервер получает вызов метода от клиента, новый экземпляр класса Hub обрабатывает сообщение.</span><span class="sxs-lookup"><span data-stu-id="5b999-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="5b999-203">Чтобы сохранить состояние через несколько соединений и вызовов методов, используйте другой метод, например базу данных или статическую переменную в классе Hub, или другой класс, который не является производным от `Hub`.</span><span class="sxs-lookup"><span data-stu-id="5b999-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="5b999-204">При сохранении данных в памяти с помощью метода, такого как статическая переменная в классе Hub, данные будут потеряны при очистке домена приложения.</span><span class="sxs-lookup"><span data-stu-id="5b999-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="5b999-205">Если вы хотите отправить сообщения клиентам из собственного кода, который выполняется вне класса Hub, это невозможно сделать, создав экземпляр класса концентратора, но это можно сделать, получив ссылку на объект контекста SignalR для класса Hub.</span><span class="sxs-lookup"><span data-stu-id="5b999-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="5b999-206">Дополнительные сведения см. в разделе [как вызывать клиентские методы и управлять группами за пределами класса Hub](#callfromoutsidehub) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5b999-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="5b999-207">Неоднородный регистр имен концентраторов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="5b999-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="5b999-208">По умолчанию клиенты JavaScript ссылаются на концентраторы, используя версию имени класса в стиле Camel.</span><span class="sxs-lookup"><span data-stu-id="5b999-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="5b999-209">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать соглашениям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5b999-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="5b999-210">Предыдущий пример будет называться `contosoChatHub` в коде JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5b999-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="5b999-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="5b999-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="5b999-212">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="5b999-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="5b999-213">Если необходимо указать другое имя для использования клиентами, добавьте атрибут `HubName`.</span><span class="sxs-lookup"><span data-stu-id="5b999-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="5b999-214">При использовании атрибута `HubName` в клиентах JavaScript нет необходимости изменять имя на Camel.</span><span class="sxs-lookup"><span data-stu-id="5b999-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="5b999-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="5b999-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="5b999-216">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="5b999-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="5b999-217">Несколько концентраторов</span><span class="sxs-lookup"><span data-stu-id="5b999-217">Multiple Hubs</span></span>

<span data-ttu-id="5b999-218">В приложении можно определить несколько классов концентратора.</span><span class="sxs-lookup"><span data-stu-id="5b999-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="5b999-219">При этом соединение является общим, но группы являются отдельными:</span><span class="sxs-lookup"><span data-stu-id="5b999-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="5b999-220">Все клиенты будут использовать один и тот же URL-адрес для установления подключения SignalR со службой ("/SignalR" или настраиваемого URL-адреса, если он указан), и это соединение используется для всех центров, определенных службой.</span><span class="sxs-lookup"><span data-stu-id="5b999-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="5b999-221">По сравнению с определением всех функций концентратора в одном классе нет разницы в производительности для нескольких концентраторов.</span><span class="sxs-lookup"><span data-stu-id="5b999-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="5b999-222">Все концентраторы получают одинаковые сведения о запросе HTTP.</span><span class="sxs-lookup"><span data-stu-id="5b999-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="5b999-223">Так как все концентраторы используют одно и то же соединение, единственными данными HTTP-запроса, которые получает сервер, является исходный HTTP-запрос, который устанавливает подключение SignalR.</span><span class="sxs-lookup"><span data-stu-id="5b999-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="5b999-224">При использовании запроса на подключение для передачи информации от клиента на сервер путем указания строки запроса нельзя указывать разные строки запроса для разных концентраторов.</span><span class="sxs-lookup"><span data-stu-id="5b999-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="5b999-225">Все концентраторы получат одну и ту же информацию.</span><span class="sxs-lookup"><span data-stu-id="5b999-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="5b999-226">Созданный файл прокси-серверов JavaScript будет содержать учетные записи-посредники для всех концентраторов в одном файле.</span><span class="sxs-lookup"><span data-stu-id="5b999-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="5b999-227">Сведения о прокси-серверах JavaScript см. [в статье Путеводитель по API концентраторов SignalR — клиент JavaScript — созданный прокси-сервер и его назначение](hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="5b999-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="5b999-228">Группы определяются в центрах.</span><span class="sxs-lookup"><span data-stu-id="5b999-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="5b999-229">В SignalR вы можете определить именованные группы для широковещательной рассылки подмножествам подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="5b999-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="5b999-230">Группы обслуживаются отдельно для каждого концентратора.</span><span class="sxs-lookup"><span data-stu-id="5b999-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="5b999-231">Например, группа с именем "Администраторы" будет включать в себя один набор клиентов для `ContosoChatHub` класса, и одно и то же имя группы будет ссылаться на другой набор клиентов для класса `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="5b999-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="5b999-232">Строго типизированные концентраторы</span><span class="sxs-lookup"><span data-stu-id="5b999-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="5b999-233">Чтобы определить интерфейс для методов концентратора, на которые может ссылаться клиент (и включить IntelliSense в методах концентратора), выберете концентратор из `Hub<T>` (который появился в SignalR 2,1), а не `Hub`.</span><span class="sxs-lookup"><span data-stu-id="5b999-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="5b999-234">Определение методов в классе Hub, которые могут вызываться клиентами</span><span class="sxs-lookup"><span data-stu-id="5b999-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="5b999-235">Чтобы предоставить метод в концентраторе, который должен быть вызываемым из клиента, объявите открытый метод, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="5b999-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="5b999-236">Можно указать тип возвращаемого значения и параметры, включая сложные типы и массивы, как в любом C# методе.</span><span class="sxs-lookup"><span data-stu-id="5b999-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="5b999-237">Все данные, получаемые в параметрах или возвращаемые вызывающему объекту, передаются между клиентом и сервером с помощью JSON, а SignalR обрабатывает привязку сложных объектов и массивов объектов автоматически.</span><span class="sxs-lookup"><span data-stu-id="5b999-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="5b999-238">Неоднородный регистр имен методов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="5b999-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="5b999-239">По умолчанию клиенты JavaScript ссылаются на методы концентратора, используя версию имени метода в стиле Camel.</span><span class="sxs-lookup"><span data-stu-id="5b999-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="5b999-240">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать соглашениям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5b999-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="5b999-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="5b999-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="5b999-242">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="5b999-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="5b999-243">Если необходимо указать другое имя для использования клиентами, добавьте атрибут `HubMethodName`.</span><span class="sxs-lookup"><span data-stu-id="5b999-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="5b999-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="5b999-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="5b999-245">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="5b999-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="5b999-246">Время асинхронного выполнения</span><span class="sxs-lookup"><span data-stu-id="5b999-246">When to execute asynchronously</span></span>

<span data-ttu-id="5b999-247">Если метод будет длительно выполнен или должен выполнить работу, которая будет заключаться в ожидании (например, при поиске базы данных или вызове веб-службы), сделайте метод концентратора асинхронным, возвращая [задачу](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (вместо `void` Return) или [Task&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) объект (вместо `T`ного типа).</span><span class="sxs-lookup"><span data-stu-id="5b999-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="5b999-248">Когда вы возвращаете объект `Task` из метода, SignalR ожидает завершения `Task`, а затем отправляет неупакованный результат обратно клиенту, поэтому нет никакой разницы в способе кодирования вызова метода в клиенте.</span><span class="sxs-lookup"><span data-stu-id="5b999-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="5b999-249">Создание метода концентратора асинхронно позволяет избежать блокировки соединения при использовании транспорта WebSocket.</span><span class="sxs-lookup"><span data-stu-id="5b999-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="5b999-250">Если метод концентратора выполняется синхронно, а транспорт — WebSocket, последующие вызовы методов в концентраторе от одного клиента блокируются до завершения метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="5b999-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="5b999-251">В следующем примере показан тот же метод, закодированный для синхронного или асинхронного выполнения, за которым следует код клиента JavaScript, который работает для вызова любой версии.</span><span class="sxs-lookup"><span data-stu-id="5b999-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="5b999-252">**Рабатывают**</span><span class="sxs-lookup"><span data-stu-id="5b999-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="5b999-253">**Асинхронной**</span><span class="sxs-lookup"><span data-stu-id="5b999-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="5b999-254">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="5b999-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="5b999-255">Дополнительные сведения об использовании асинхронных методов в ASP.NET 4,5 см. в разделе [Использование асинхронных методов в ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="5b999-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="5b999-256">Определение перегрузок</span><span class="sxs-lookup"><span data-stu-id="5b999-256">Defining Overloads</span></span>

<span data-ttu-id="5b999-257">Если требуется определить перегрузки для метода, количество параметров в каждой перегрузке должно отличаться.</span><span class="sxs-lookup"><span data-stu-id="5b999-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="5b999-258">Если вы отличаете перегрузку только путем указания других типов параметров, класс Hub будет компилироваться, но служба SignalR выдаст исключение во время выполнения, когда клиенты пытаются вызвать одну из перегрузок.</span><span class="sxs-lookup"><span data-stu-id="5b999-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="5b999-259">Отчет о ходе выполнения вызовов метода концентратора</span><span class="sxs-lookup"><span data-stu-id="5b999-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="5b999-260">SignalR 2,1 добавляет поддержку [шаблона отчетов о ходе выполнения](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) , представленного в .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="5b999-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="5b999-261">Чтобы реализовать отчеты о ходе выполнения, определите параметр `IProgress<T>` для метода концентратора, к которому клиент имеет доступ.</span><span class="sxs-lookup"><span data-stu-id="5b999-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="5b999-262">При написании длительно выполняемого сервера важно использовать асинхронный шаблон программирования, такой как async/await, а не блокировать поток концентратора.</span><span class="sxs-lookup"><span data-stu-id="5b999-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="5b999-263">Вызов клиентских методов из класса HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="5b999-264">Чтобы вызывать клиентские методы с сервера, используйте свойство `Clients` в методе в классе Hub.</span><span class="sxs-lookup"><span data-stu-id="5b999-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="5b999-265">В следующем примере показан серверный код, который вызывает `addNewMessageToPage` на всех подключенных клиентах, и клиентский код, определяющий метод в клиенте JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5b999-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="5b999-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="5b999-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="5b999-267">Вызов клиентского метода является асинхронной операцией и возвращает `Task`.</span><span class="sxs-lookup"><span data-stu-id="5b999-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="5b999-268">Используйте `await` в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="5b999-268">Use `await`:</span></span>

* <span data-ttu-id="5b999-269">Чтобы убедиться, что сообщение отправлено без ошибок.</span><span class="sxs-lookup"><span data-stu-id="5b999-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="5b999-270">Для включения перехвата и обработки ошибок в блоке try-catch.</span><span class="sxs-lookup"><span data-stu-id="5b999-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="5b999-271">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="5b999-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="5b999-272">Невозможно получить возвращаемое значение из клиентского метода. такой синтаксис, как `int x = Clients.All.add(1,1)`, не работает.</span><span class="sxs-lookup"><span data-stu-id="5b999-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="5b999-273">Для параметров можно указать сложные типы и массивы.</span><span class="sxs-lookup"><span data-stu-id="5b999-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="5b999-274">В следующем примере сложный тип передается клиенту в параметре метода.</span><span class="sxs-lookup"><span data-stu-id="5b999-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="5b999-275">**Серверный код, вызывающий клиентский метод с помощью сложного объекта**</span><span class="sxs-lookup"><span data-stu-id="5b999-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="5b999-276">**Серверный код, определяющий сложный объект**</span><span class="sxs-lookup"><span data-stu-id="5b999-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="5b999-277">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="5b999-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="5b999-278">Выбор клиентов, получающих RPC</span><span class="sxs-lookup"><span data-stu-id="5b999-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="5b999-279">Свойство Clients возвращает объект [хубконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) , который предоставляет несколько параметров для указания клиентов, которые будут принимать RPC:</span><span class="sxs-lookup"><span data-stu-id="5b999-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="5b999-280">Все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="5b999-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="5b999-281">Только вызывающий клиент.</span><span class="sxs-lookup"><span data-stu-id="5b999-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="5b999-282">Все клиенты, кроме вызывающего клиента.</span><span class="sxs-lookup"><span data-stu-id="5b999-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="5b999-283">Конкретный клиент, идентифицируемый по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="5b999-284">В этом примере вызывается `addContosoChatMessageToPage` на вызывающем клиенте и действует тот же результат, что и при использовании `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="5b999-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="5b999-285">Все подключенные клиенты, за исключением указанных клиентов, идентифицируемые по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="5b999-286">Все подключенные клиенты в указанной группе.</span><span class="sxs-lookup"><span data-stu-id="5b999-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="5b999-287">Все подключенные клиенты в указанной группе, за исключением указанных клиентов, идентифицируемые по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="5b999-288">Все подключенные клиенты в указанной группе, кроме вызывающего клиента.</span><span class="sxs-lookup"><span data-stu-id="5b999-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="5b999-289">Конкретный пользователь, идентифицируемый userId.</span><span class="sxs-lookup"><span data-stu-id="5b999-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="5b999-290">По умолчанию это `IPrincipal.Identity.Name`, но его можно изменить, [зарегистрировав реализацию иусеридпровидер с глобальным узлом](mapping-users-to-connections.md#IUserIdProvider).</span><span class="sxs-lookup"><span data-stu-id="5b999-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="5b999-291">Все клиенты и группы в списке идентификаторов подключений.</span><span class="sxs-lookup"><span data-stu-id="5b999-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="5b999-292">Список групп.</span><span class="sxs-lookup"><span data-stu-id="5b999-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="5b999-293">Пользователь по имени.</span><span class="sxs-lookup"><span data-stu-id="5b999-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="5b999-294">Список имен пользователей (введенных в SignalR 2,1).</span><span class="sxs-lookup"><span data-stu-id="5b999-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="5b999-295">Нет проверки во время компиляции для имен методов</span><span class="sxs-lookup"><span data-stu-id="5b999-295">No compile-time validation for method names</span></span>

<span data-ttu-id="5b999-296">Указанное имя метода интерпретируется как динамический объект, что означает отсутствие в нем IntelliSense или проверку во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="5b999-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="5b999-297">Выражение вычисляется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5b999-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="5b999-298">При вызове метода SignalR отправляет клиенту имя метода и значения параметров, а если клиент имеет метод, совпадающий с именем, вызывается метод и ему передаются значения параметров.</span><span class="sxs-lookup"><span data-stu-id="5b999-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="5b999-299">Если на клиенте не найден соответствующий метод, ошибка не возникает.</span><span class="sxs-lookup"><span data-stu-id="5b999-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="5b999-300">Сведения о формате данных, которые SignalR передает клиенту в фоновом режиме при вызове клиентского метода, см. [в разделе Общие](../getting-started/introduction-to-signalr.md)сведения о SignalR.</span><span class="sxs-lookup"><span data-stu-id="5b999-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="5b999-301">Сопоставление имен методов без учета регистра</span><span class="sxs-lookup"><span data-stu-id="5b999-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="5b999-302">Сопоставление имен методов не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="5b999-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="5b999-303">Например, `Clients.All.addContosoChatMessageToPage` на сервере будет выполнять `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`или `addContosoChatMessageToPage` на клиенте.</span><span class="sxs-lookup"><span data-stu-id="5b999-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="5b999-304">Асинхронное выполнение</span><span class="sxs-lookup"><span data-stu-id="5b999-304">Asynchronous execution</span></span>

<span data-ttu-id="5b999-305">Вызываемый метод выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="5b999-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="5b999-306">Любой код, который поступает после вызова метода клиенту, будет выполняться немедленно, не дожидаясь завершения передачи данных для клиентов SignalR, если не указать, что последующие строки кода должны ожидать завершения метода.</span><span class="sxs-lookup"><span data-stu-id="5b999-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="5b999-307">В следующем примере кода показано, как выполнять два метода клиента последовательно.</span><span class="sxs-lookup"><span data-stu-id="5b999-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="5b999-308">**Использование await (.NET 4,5)**</span><span class="sxs-lookup"><span data-stu-id="5b999-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="5b999-309">Если вы используете `await`, чтобы дождаться завершения клиентского метода до выполнения следующей строки кода, это не означает, что клиенты фактически получат сообщение перед выполнением следующей строки кода.</span><span class="sxs-lookup"><span data-stu-id="5b999-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="5b999-310">"Завершение" вызова клиентского метода означает только то, что SignalR выполнил все необходимое для отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="5b999-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="5b999-311">Если требуется проверка того, что клиенты получили сообщение, необходимо программировать механизм самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="5b999-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="5b999-312">Например, можно закодировать метод `MessageReceived` в концентраторе, а в методе `addContosoChatMessageToPage` на клиенте можно вызвать `MessageReceived` после выполнения любой работы, которую необходимо выполнить на клиенте.</span><span class="sxs-lookup"><span data-stu-id="5b999-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="5b999-313">В `MessageReceived` в центре можно выполнять любые действия, зависящие от фактического приема и обработки исходного вызова метода.</span><span class="sxs-lookup"><span data-stu-id="5b999-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="5b999-314">Использование строковой переменной в качестве имени метода</span><span class="sxs-lookup"><span data-stu-id="5b999-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="5b999-315">Если вы хотите вызвать клиентский метод, используя строковую переменную в качестве имени метода, приведите `Clients.All` (или `Clients.Others`, `Clients.Caller`и т. д.) `IClientProxy`, а затем вызовите [Invoke (имя_метода, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="5b999-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="5b999-316">Управление членством в группах из класса HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="5b999-317">Группы в SignalR предоставляют метод для вещания сообщений в указанные подмножества подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="5b999-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="5b999-318">Группа может иметь любое количество клиентов, а клиент может быть членом любого числа групп.</span><span class="sxs-lookup"><span data-stu-id="5b999-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="5b999-319">Для управления членством в группе используйте методы [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) и [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) , предоставляемые свойством `Groups` класса Hub.</span><span class="sxs-lookup"><span data-stu-id="5b999-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="5b999-320">В следующем примере показаны методы `Groups.Add` и `Groups.Remove`, используемые в методах концентратора, которые вызываются клиентским кодом, а затем — клиентский код JavaScript, который вызывает их.</span><span class="sxs-lookup"><span data-stu-id="5b999-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="5b999-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="5b999-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="5b999-322">**Клиент JavaScript, использующий созданный прокси-сервер**</span><span class="sxs-lookup"><span data-stu-id="5b999-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="5b999-323">Вам не нужно явно создавать группы.</span><span class="sxs-lookup"><span data-stu-id="5b999-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="5b999-324">Фактически группа создается автоматически при первом указании имени в вызове `Groups.Add`и удаляется при удалении последнего подключения из членства в нем.</span><span class="sxs-lookup"><span data-stu-id="5b999-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="5b999-325">Отсутствует API для получения списка членства в группе или списка групп.</span><span class="sxs-lookup"><span data-stu-id="5b999-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="5b999-326">SignalR отправляет сообщения клиентам и группам, основанным на [модели публикации и подтипа](http://en.wikipedia.org/wiki/Publish/subscribe), а сервер не поддерживает списки групп или членства в группах.</span><span class="sxs-lookup"><span data-stu-id="5b999-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="5b999-327">Это обеспечивает максимальную масштабируемость, так как при добавлении узла в веб-ферму любое состояние, которое обслуживает SignalR, должно быть распространено на новый узел.</span><span class="sxs-lookup"><span data-stu-id="5b999-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="5b999-328">Асинхронное выполнение методов Add и Remove</span><span class="sxs-lookup"><span data-stu-id="5b999-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="5b999-329">Методы `Groups.Add` и `Groups.Remove` выполняются асинхронно.</span><span class="sxs-lookup"><span data-stu-id="5b999-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="5b999-330">Если вы хотите добавить клиент в группу и сразу же отправить сообщение клиенту с помощью группы, необходимо убедиться в том, что метод `Groups.Add` завершается первым.</span><span class="sxs-lookup"><span data-stu-id="5b999-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="5b999-331">В следующем примере кода показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="5b999-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="5b999-332">**Добавление клиента в группу и последующее переобмен сообщениями от клиента**</span><span class="sxs-lookup"><span data-stu-id="5b999-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="5b999-333">Сохранение членства в группах</span><span class="sxs-lookup"><span data-stu-id="5b999-333">Group membership persistence</span></span>

<span data-ttu-id="5b999-334">SignalR отслеживает соединения, а не пользователей, поэтому, если требуется, чтобы пользователь настроился в одной группе каждый раз, когда пользователь устанавливает соединение, необходимо вызывать `Groups.Add` каждый раз, когда пользователь устанавливает новое соединение.</span><span class="sxs-lookup"><span data-stu-id="5b999-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="5b999-335">После временной потери подключения иногда SignalR может автоматически восстановить подключение.</span><span class="sxs-lookup"><span data-stu-id="5b999-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="5b999-336">В этом случае SignalR восстанавливает одно и то же подключение, не устанавливая новое подключение, поэтому членство в группе клиента автоматически восстанавливается.</span><span class="sxs-lookup"><span data-stu-id="5b999-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="5b999-337">Это возможно даже в том случае, если временный перерыв является результатом перезагрузки или сбоя сервера, так как состояние подключения для каждого клиента, включая членство в группах, передается клиенту.</span><span class="sxs-lookup"><span data-stu-id="5b999-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="5b999-338">Если сервер выходит из строя и заменяется новым сервером до истечения времени ожидания подключения, клиент может автоматически подключиться к новому серверу и повторно зарегистрировать в группах, членом которых он является.</span><span class="sxs-lookup"><span data-stu-id="5b999-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="5b999-339">Если подключение не может быть восстановлено автоматически после потери подключения или истечения времени ожидания соединения или когда клиент отключается (например, когда браузер переходит на новую страницу), членство в группах теряется.</span><span class="sxs-lookup"><span data-stu-id="5b999-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="5b999-340">При следующем подключении пользователя будет установлено новое подключение.</span><span class="sxs-lookup"><span data-stu-id="5b999-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="5b999-341">Чтобы обеспечить членство в группах, когда один и тот же пользователь устанавливает новое подключение, приложение должно отслеживание взаимосвязей между пользователями и группами и восстанавливать членство в группах каждый раз, когда пользователь устанавливает новое подключение.</span><span class="sxs-lookup"><span data-stu-id="5b999-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="5b999-342">Дополнительные сведения о подключениях и повторном подключении см. в разделе [как управлять событиями времени существования соединения в классе Hub](#connectionlifetime) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5b999-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="5b999-343">Группы с одним пользователем</span><span class="sxs-lookup"><span data-stu-id="5b999-343">Single-user groups</span></span>

<span data-ttu-id="5b999-344">Приложения, использующие SignalR, обычно должны вести отслеживание взаимосвязей между пользователями и соединениями, чтобы узнать, какой пользователь отправил сообщение и какие пользователи должны получать сообщение.</span><span class="sxs-lookup"><span data-stu-id="5b999-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="5b999-345">Группы используются в одном из двух часто используемых шаблонов.</span><span class="sxs-lookup"><span data-stu-id="5b999-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="5b999-346">Группы с одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="5b999-346">Single-user groups.</span></span>

    <span data-ttu-id="5b999-347">Можно указать имя пользователя в качестве имени группы и добавить текущий идентификатор подключения в группу при каждом подключении или повторном подключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="5b999-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="5b999-348">Для отправки сообщений пользователю, который отправляется в группу.</span><span class="sxs-lookup"><span data-stu-id="5b999-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="5b999-349">Недостаток этого метода заключается в том, что группа не дает вам способа выяснить, находится ли пользователь в сети или в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="5b999-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="5b999-350">Следите за связями между именами пользователей и идентификаторами подключений.</span><span class="sxs-lookup"><span data-stu-id="5b999-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="5b999-351">Можно сохранить связь между именем пользователя и одним или несколькими идентификаторами соединения в словаре или базе данных, а также обновлять сохраненные данные при каждом подключении или отключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="5b999-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="5b999-352">Чтобы отправить сообщения пользователю, укажите идентификаторы соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="5b999-353">Недостаток этого метода заключается в том, что он занимает больше памяти.</span><span class="sxs-lookup"><span data-stu-id="5b999-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="5b999-354">Как управлять событиями времени жизни соединения в классе HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="5b999-355">Типичными причинами обработки событий времени существования соединения являются отслеживание того, подключено ли пользователь, а также отслеживается связь между именами пользователей и идентификаторами подключений.</span><span class="sxs-lookup"><span data-stu-id="5b999-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="5b999-356">Чтобы запустить собственный код при подключении или отключении клиентов, переопределите `OnConnected`, `OnDisconnected`и `OnReconnected` виртуальные методы класса Hub, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="5b999-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="5b999-357">При вызове onconnected, OnDisconnection и Онреконнектед</span><span class="sxs-lookup"><span data-stu-id="5b999-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="5b999-358">Каждый раз, когда браузер переходит на новую страницу, необходимо установить новое соединение, означающее, что SignalR выполнит метод `OnDisconnected`, а затем метод `OnConnected`.</span><span class="sxs-lookup"><span data-stu-id="5b999-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="5b999-359">SignalR всегда создает новый идентификатор подключения при установлении нового соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="5b999-360">Метод `OnReconnected` вызывается при временном разрыве соединения, при котором SignalR может автоматически восстановиться из, например при временном отключении и повторном подключении кабеля до истечения времени ожидания соединения. Метод `OnDisconnected` вызывается, когда клиент отключается, и SignalR не может автоматически подключиться, например, когда браузер переходит на новую страницу.</span><span class="sxs-lookup"><span data-stu-id="5b999-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="5b999-361">Таким образом, возможная последовательность событий для данного клиента — `OnConnected`, `OnReconnected`, `OnDisconnected`; или `OnConnected``OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="5b999-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="5b999-362">Вы не увидите последовательность `OnConnected`, `OnDisconnected``OnReconnected` для данного подключения.</span><span class="sxs-lookup"><span data-stu-id="5b999-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="5b999-363">Метод `OnDisconnected` не вызывается в некоторых сценариях, например при отключении сервера или при перезапуске домена приложения.</span><span class="sxs-lookup"><span data-stu-id="5b999-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="5b999-364">Когда другой сервер поступает в сети или домен приложения завершает свой перезапуск, некоторые клиенты могут повторно подключиться и запустить событие `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="5b999-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="5b999-365">Дополнительные сведения см. [в разделе Основные сведения и обработка событий времени жизни подключения в SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="5b999-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="5b999-366">Состояние вызывающего объекта не заполнено</span><span class="sxs-lookup"><span data-stu-id="5b999-366">Caller state not populated</span></span>

<span data-ttu-id="5b999-367">Методы обработчика событий времени жизни соединения вызываются с сервера. Это означает, что любое состояние, помещаемое в объект `state` на клиенте, не будет заполнено в свойстве `Caller` на сервере.</span><span class="sxs-lookup"><span data-stu-id="5b999-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="5b999-368">Дополнительные сведения об объекте `state` и свойстве `Caller` см. в разделе [Передача состояния между клиентами и классом Hub](#passstate) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5b999-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="5b999-369">Получение сведений о клиенте из свойства Context</span><span class="sxs-lookup"><span data-stu-id="5b999-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="5b999-370">Чтобы получить сведения о клиенте, используйте свойство `Context` класса Hub.</span><span class="sxs-lookup"><span data-stu-id="5b999-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="5b999-371">Свойство `Context` возвращает объект [хубкаллерконтекст](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) , который предоставляет доступ к следующим сведениям:</span><span class="sxs-lookup"><span data-stu-id="5b999-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="5b999-372">Идентификатор подключения вызывающего клиента.</span><span class="sxs-lookup"><span data-stu-id="5b999-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="5b999-373">Идентификатор подключения — это идентификатор GUID, назначенный SignalR (вы не можете указать значение в своем коде).</span><span class="sxs-lookup"><span data-stu-id="5b999-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="5b999-374">Для каждого подключения существует один идентификатор подключения, и один и тот же идентификатор подключения используется всеми концентраторами, если в приложении имеется несколько концентраторов.</span><span class="sxs-lookup"><span data-stu-id="5b999-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="5b999-375">Данные заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="5b999-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="5b999-376">Также можно получить заголовки HTTP из `Context.Headers`.</span><span class="sxs-lookup"><span data-stu-id="5b999-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="5b999-377">Причиной нескольких ссылок на одно и то же самое является то, что `Context.Headers` был создан первым, свойство `Context.Request` было добавлено позже и `Context.Headers` было сохранено для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="5b999-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="5b999-378">Данные строки запроса.</span><span class="sxs-lookup"><span data-stu-id="5b999-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="5b999-379">Можно также получить данные строки запроса из `Context.QueryString`.</span><span class="sxs-lookup"><span data-stu-id="5b999-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="5b999-380">Строка запроса, полученная в этом свойстве, используется с HTTP-запросом, который установил подключение SignalR.</span><span class="sxs-lookup"><span data-stu-id="5b999-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="5b999-381">Можно добавить параметры строки запроса в клиент, настроив соединение, что является удобным способом передачи данных о клиенте с клиента на сервер.</span><span class="sxs-lookup"><span data-stu-id="5b999-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="5b999-382">В следующем примере показан один из способов добавления строки запроса в клиент JavaScript при использовании созданного прокси.</span><span class="sxs-lookup"><span data-stu-id="5b999-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="5b999-383">Дополнительные сведения о настройке параметров строки запроса см. в руководствах по API для клиентов [JavaScript](hubs-api-guide-javascript-client.md) и [.NET](hubs-api-guide-net-client.md) .</span><span class="sxs-lookup"><span data-stu-id="5b999-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="5b999-384">Метод перевозки, используемый для соединения, можно найти в данных строки запроса, а также с другими внутренними значениями, используемыми SignalR:</span><span class="sxs-lookup"><span data-stu-id="5b999-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="5b999-385">Значение `transportMethod` будет равно "WebSockets", "Серверсентевентс", "Фореверфраме" или "Лонгполлинг".</span><span class="sxs-lookup"><span data-stu-id="5b999-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="5b999-386">Обратите внимание, что если проверить это значение в методе обработчика событий `OnConnected`, то в некоторых сценариях можно изначально получить значение транспорта, которое не является окончательным согласованным транспортным методом для соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="5b999-387">В этом случае метод выдаст исключение и будет вызван позже, когда будет установлен окончательный метод транспортировки.</span><span class="sxs-lookup"><span data-stu-id="5b999-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="5b999-388">Сеанс.</span><span class="sxs-lookup"><span data-stu-id="5b999-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="5b999-389">Вы также можете получать файлы cookie из `Context.RequestCookies`.</span><span class="sxs-lookup"><span data-stu-id="5b999-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="5b999-390">сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="5b999-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="5b999-391">Объект HttpContext для запроса:</span><span class="sxs-lookup"><span data-stu-id="5b999-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="5b999-392">Используйте этот метод вместо получения `HttpContext.Current` для получения объекта `HttpContext` для подключения SignalR.</span><span class="sxs-lookup"><span data-stu-id="5b999-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="5b999-393">Передача состояния между клиентами и классом HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="5b999-394">Прокси клиента предоставляет объект `state`, в котором можно хранить данные, которые необходимо передать на сервер при каждом вызове метода.</span><span class="sxs-lookup"><span data-stu-id="5b999-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="5b999-395">На сервере эти данные можно получить в свойстве `Clients.Caller` в методах концентратора, которые вызываются клиентами.</span><span class="sxs-lookup"><span data-stu-id="5b999-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="5b999-396">Свойство `Clients.Caller` не заполняется методами обработчика событий времени жизни соединения `OnConnected`, `OnDisconnected`и `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="5b999-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="5b999-397">Создание или обновление данных в объекте `state`, а свойство `Clients.Caller` работает в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="5b999-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="5b999-398">Можно обновить значения на сервере и передать их обратно клиенту.</span><span class="sxs-lookup"><span data-stu-id="5b999-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="5b999-399">В следующем примере показан код клиента JavaScript, который сохраняет состояние для передачи на сервер при каждом вызове метода.</span><span class="sxs-lookup"><span data-stu-id="5b999-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="5b999-400">В следующем примере показан эквивалентный код в клиенте .NET.</span><span class="sxs-lookup"><span data-stu-id="5b999-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="5b999-401">В классе Hub можно получить доступ к этим данным в свойстве `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="5b999-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="5b999-402">В следующем примере показан код, который извлекает состояние, на которое ссылается предыдущий пример.</span><span class="sxs-lookup"><span data-stu-id="5b999-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="5b999-403">Этот механизм для сохранения состояния не предназначен для больших объемов данных, так как все, что вы поместили в `state` или `Clients.Caller` свойство, обложились с помощью каждого вызова метода.</span><span class="sxs-lookup"><span data-stu-id="5b999-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="5b999-404">Это удобно для небольших элементов, таких как имена пользователей или счетчики.</span><span class="sxs-lookup"><span data-stu-id="5b999-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="5b999-405">В VB.NET или в концентраторе со строгой типизацией объект состояния вызывающего объекта не может быть доступен через `Clients.Caller`; Вместо этого используйте `Clients.CallerState` (появилось в SignalR 2,1):</span><span class="sxs-lookup"><span data-stu-id="5b999-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="5b999-406">**Использование Каллерстате вC#**</span><span class="sxs-lookup"><span data-stu-id="5b999-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="5b999-407">**Использование Каллерстате в Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="5b999-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="5b999-408">Как выполнять обработку ошибок в классе HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="5b999-409">Чтобы обрабатывались ошибки, возникающие в методах класса Hub, сначала убедитесь, что все исключения из асинхронных операций (например, вызов методов клиента) используются `await`.</span><span class="sxs-lookup"><span data-stu-id="5b999-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="5b999-410">Затем используйте один или несколько следующих методов.</span><span class="sxs-lookup"><span data-stu-id="5b999-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="5b999-411">Заключите код метода в блоки try-catch и заносите в журнал объект исключения.</span><span class="sxs-lookup"><span data-stu-id="5b999-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="5b999-412">В целях отладки можно отправить исключение клиенту, но в целях безопасности не рекомендуется отправлять подробные сведения клиентам в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5b999-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="5b999-413">Создайте модуль конвейера концентраторов, который обрабатывает метод [онинкоминжеррор](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="5b999-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="5b999-414">В следующем примере показан модуль конвейера, в котором регистрируются ошибки, а затем код в Startup.cs, который внедряет модуль в конвейер концентраторов.</span><span class="sxs-lookup"><span data-stu-id="5b999-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="5b999-415">Используйте класс `HubException` (представленный в SignalR 2).</span><span class="sxs-lookup"><span data-stu-id="5b999-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="5b999-416">Эта ошибка может быть вызвана любым вызовом концентратора.</span><span class="sxs-lookup"><span data-stu-id="5b999-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="5b999-417">Конструктор `HubError` принимает строковое сообщение и объект для хранения дополнительных данных об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5b999-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="5b999-418">SignalR выполнит автоматическую сериализацию исключения и отправит его клиенту, где он будет использоваться для отклонения или отказа в вызове метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="5b999-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="5b999-419">В следующих примерах кода показано, как создавать `HubException` во время вызова концентратора, а также как управлять исключениями на клиентах JavaScript и .NET.</span><span class="sxs-lookup"><span data-stu-id="5b999-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="5b999-420">**Серверный код, демонстрирующий класс Хубексцептион**</span><span class="sxs-lookup"><span data-stu-id="5b999-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="5b999-421">**Клиентский код JavaScript, демонстрирующий ответ на создание Хубексцептион в концентраторе**</span><span class="sxs-lookup"><span data-stu-id="5b999-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="5b999-422">**Клиентский код .NET, демонстрирующий ответ на создание Хубексцептион в концентраторе**</span><span class="sxs-lookup"><span data-stu-id="5b999-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="5b999-423">Дополнительные сведения о модулях конвейера концентратора см. в подразделе [Настройка конвейера](#hubpipeline) концентраторов далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5b999-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="5b999-424">Включение трассировки</span><span class="sxs-lookup"><span data-stu-id="5b999-424">How to enable tracing</span></span>

<span data-ttu-id="5b999-425">Чтобы включить трассировку на стороне сервера, добавьте элемент System. Diagnostics в файл Web. config, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="5b999-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="5b999-426">При запуске приложения в Visual Studio журналы можно просмотреть в окне **вывод** .</span><span class="sxs-lookup"><span data-stu-id="5b999-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="5b999-427">Вызов клиентских методов и управление группами извне класса HUB</span><span class="sxs-lookup"><span data-stu-id="5b999-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="5b999-428">Чтобы вызвать клиентские методы из другого класса, чем класс Hub, получите ссылку на объект контекста SignalR для концентратора и используйте его для вызова методов в клиенте или для управления группами.</span><span class="sxs-lookup"><span data-stu-id="5b999-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="5b999-429">Следующий пример `StockTicker` класс получает объект контекста, сохраняет его в экземпляре класса, сохраняет экземпляр класса в статическом свойстве и использует контекст из экземпляра одноэлементного класса для вызова метода `updateStockPrice` на клиентах, подключенных к концентратору с именем `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="5b999-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="5b999-430">Если необходимо использовать контекст несколько раз в долгосрочном объекте, получите ссылку один раз и сохраните его вместо того, чтобы повторно получать его каждый раз.</span><span class="sxs-lookup"><span data-stu-id="5b999-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="5b999-431">Получение контекста однократно гарантирует, что SignalR отправляет сообщения клиентам в той же последовательности, в которой методы концентратора выполняют вызовы клиентских методов.</span><span class="sxs-lookup"><span data-stu-id="5b999-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="5b999-432">Руководство, в котором показано, как использовать контекст SignalR для концентратора, см. в разделе [серверное вещание с помощью ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="5b999-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="5b999-433">Вызов методов клиента</span><span class="sxs-lookup"><span data-stu-id="5b999-433">Calling client methods</span></span>

<span data-ttu-id="5b999-434">Вы можете указать, какие клиенты будут принимать RPC, но при этом у вас будет меньше параметров, чем при вызове из класса Hub.</span><span class="sxs-lookup"><span data-stu-id="5b999-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="5b999-435">Причина в том, что контекст не связан с определенным вызовом от клиента, поэтому все методы, которым требуются знания о текущем ИДЕНТИФИКАТОРе соединения, такие как `Clients.Others`или `Clients.Caller`или `Clients.OthersInGroup`, недоступны.</span><span class="sxs-lookup"><span data-stu-id="5b999-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="5b999-436">Доступны следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="5b999-436">The following options are available:</span></span>

- <span data-ttu-id="5b999-437">Все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="5b999-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="5b999-438">Конкретный клиент, идентифицируемый по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="5b999-439">Все подключенные клиенты, за исключением указанных клиентов, идентифицируемые по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="5b999-440">Все подключенные клиенты в указанной группе.</span><span class="sxs-lookup"><span data-stu-id="5b999-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="5b999-441">Все подключенные клиенты в указанной группе, за исключением указанных клиентов, идентифицируемые по ИДЕНТИФИКАТОРу соединения.</span><span class="sxs-lookup"><span data-stu-id="5b999-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="5b999-442">При вызове класса, не являющегося концентратором, из методов класса Hub можно передать текущий идентификатор соединения и использовать его с `Clients.Client`, `Clients.AllExcept`или `Clients.Group` для имитации `Clients.Caller`, `Clients.Others`или `Clients.OthersInGroup`.</span><span class="sxs-lookup"><span data-stu-id="5b999-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="5b999-443">В следующем примере класс `MoveShapeHub` передает идентификатор подключения классу `Broadcaster`, чтобы класс `Broadcaster` мог имитировать `Clients.Others`.</span><span class="sxs-lookup"><span data-stu-id="5b999-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="5b999-444">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="5b999-444">Managing group membership</span></span>

<span data-ttu-id="5b999-445">Для управления группами доступны те же параметры, что и в классе Hub.</span><span class="sxs-lookup"><span data-stu-id="5b999-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="5b999-446">Добавление клиента в группу</span><span class="sxs-lookup"><span data-stu-id="5b999-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="5b999-447">Удаление клиента из группы</span><span class="sxs-lookup"><span data-stu-id="5b999-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="5b999-448">Настройка конвейера концентраторов</span><span class="sxs-lookup"><span data-stu-id="5b999-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="5b999-449">SignalR позволяет внедрять собственный код в конвейер концентратора.</span><span class="sxs-lookup"><span data-stu-id="5b999-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="5b999-450">В следующем примере показан пользовательский модуль конвейера концентратора, который регистрирует каждый входящий вызов метода, полученный от клиента, и вызов исходящего метода, вызываемого на клиенте:</span><span class="sxs-lookup"><span data-stu-id="5b999-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="5b999-451">Следующий код в файле *Startup.CS* регистрирует модуль для запуска в конвейере концентратора:</span><span class="sxs-lookup"><span data-stu-id="5b999-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="5b999-452">Существует множество различных методов, которые можно переопределить.</span><span class="sxs-lookup"><span data-stu-id="5b999-452">There are many different methods that you can override.</span></span> <span data-ttu-id="5b999-453">Полный список см. в разделе [методы хубпипелинемодуле](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="5b999-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
