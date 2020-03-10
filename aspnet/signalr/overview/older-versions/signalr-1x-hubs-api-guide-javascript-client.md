---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: Путеводитель по API концентраторов SignalR 1. x — клиент JavaScript | Документация Майкрософт
author: bradygaster
description: В этом документе содержатся общие сведения об использовании API концентраторов для SignalR версии 1,1 в клиентах JavaScript, таких как браузеры и магазин Windows (WinJS) апплик...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 24850fe5229490bf600e09ad4718abb575a845fa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431106"
---
# <a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="1b4ad-103">Руководство по API концентраторов SignalR 1.x — клиент JavaScript</span><span class="sxs-lookup"><span data-stu-id="1b4ad-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>

<span data-ttu-id="1b4ad-104">[Патрик Флетчера](https://github.com/pfletcher), [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1b4ad-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="1b4ad-105">В этом документе содержатся общие сведения об использовании API концентраторов для SignalR версии 1,1 в клиентах JavaScript, таких как браузеры и приложения Магазина Windows (WinJS).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="1b4ad-106">API концентраторов SignalR позволяет выполнять удаленные вызовы процедур (RPC) с сервера на подключенные клиенты и с клиентов на сервер.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="1b4ad-107">В серверном коде определяются методы, которые могут вызываться клиентами, и вызываются методы, которые выполняются на клиенте.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="1b4ad-108">В клиентском коде определяются методы, которые могут быть вызваны с сервера, а также вызываются методы, которые выполняются на сервере.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="1b4ad-109">Этот механизм отвечает за все клиентские коммуникации.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="1b4ad-110">SignalR также предлагает интерфейс API более низкого уровня, называемый постоянными подключениями.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="1b4ad-111">Общие сведения о SignalR, концентраторах и постоянных подключениях, а также руководство, в котором показано, как создать полноценное приложение SignalR, см. в разделе [SignalR-начало работы](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="1b4ad-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="1b4ad-112">Overview</span></span>

<span data-ttu-id="1b4ad-113">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="1b4ad-114">Созданный прокси-сервер и его назначение</span><span class="sxs-lookup"><span data-stu-id="1b4ad-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="1b4ad-115">Когда следует использовать созданный прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="1b4ad-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="1b4ad-116">Установка клиента</span><span class="sxs-lookup"><span data-stu-id="1b4ad-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="1b4ad-117">Как ссылаться на динамически создаваемый прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="1b4ad-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="1b4ad-118">Создание физического файла для прокси-сервера, созданного SignalR</span><span class="sxs-lookup"><span data-stu-id="1b4ad-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="1b4ad-119">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="1b4ad-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="1b4ad-120">$. Connection. Hub — это тот же объект, который создает $. Хубконнектион ()</span><span class="sxs-lookup"><span data-stu-id="1b4ad-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="1b4ad-121">Асинхронное выполнение метода Start</span><span class="sxs-lookup"><span data-stu-id="1b4ad-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="1b4ad-122">Как установить междоменное подключение</span><span class="sxs-lookup"><span data-stu-id="1b4ad-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="1b4ad-123">Настройка подключения</span><span class="sxs-lookup"><span data-stu-id="1b4ad-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="1b4ad-124">Указание параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="1b4ad-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="1b4ad-125">Как указать метод перевозки</span><span class="sxs-lookup"><span data-stu-id="1b4ad-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="1b4ad-126">Как получить учетную запись-посредник для класса HUB</span><span class="sxs-lookup"><span data-stu-id="1b4ad-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="1b4ad-127">Определение методов на клиенте, который может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="1b4ad-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="1b4ad-128">Вызов методов сервера из клиента</span><span class="sxs-lookup"><span data-stu-id="1b4ad-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="1b4ad-129">Как работать с событиями времени жизни соединения</span><span class="sxs-lookup"><span data-stu-id="1b4ad-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="1b4ad-130">Как обрабатывались ошибки</span><span class="sxs-lookup"><span data-stu-id="1b4ad-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="1b4ad-131">Как включить ведение журнала на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="1b4ad-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="1b4ad-132">Документацию по программированию клиентов сервера или .NET см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="1b4ad-133">Путеводитель по API концентраторов SignalR — сервер</span><span class="sxs-lookup"><span data-stu-id="1b4ad-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="1b4ad-134">Путеводитель по API концентраторов SignalR — клиент .NET</span><span class="sxs-lookup"><span data-stu-id="1b4ad-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="1b4ad-135">Ссылки на справочные статьи по API относятся к версии .NET 4,5 API.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="1b4ad-136">Если вы используете .NET 4, см. [статьи с описанием API для .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="1b4ad-137">Созданный прокси-сервер и его назначение</span><span class="sxs-lookup"><span data-stu-id="1b4ad-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="1b4ad-138">Вы можете программировать клиент JavaScript для взаимодействия со службой SignalR с прокси-сервером, который генерирует SignalR, или без него.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="1b4ad-139">То, что делает прокси-сервер, упрощает синтаксис кода, используемого для соединения, создания методов, которые сервер вызывает, и вызова методов на сервере.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="1b4ad-140">При написании кода для вызова методов сервера созданный прокси-сервер позволяет использовать синтаксис, который выглядит так, как если бы выполнялась локальная функция: можно написать `serverMethod(arg1, arg2)` вместо `invoke('serverMethod', arg1, arg2)`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="1b4ad-141">Сформированный синтаксис прокси-сервера также позволяет немедленно и расшифровать ошибку на стороне клиента при ошибочном вводе имени метода сервера.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="1b4ad-142">Если вы вручную создаете файл, который определяет прокси-серверы, можно также получить поддержку IntelliSense для написания кода, который вызывает методы сервера.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="1b4ad-143">Например, предположим, что на сервере имеется следующий класс концентратора:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="1b4ad-144">В следующих примерах кода показано, как выглядит код JavaScript для вызова метода `NewContosoChatMessage` на сервере и получения вызовов метода `addContosoChatMessageToPage` с сервера.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="1b4ad-145">**С созданным прокси-сервером**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="1b4ad-146">**Без созданного прокси-сервера**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="1b4ad-147">Когда следует использовать созданный прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="1b4ad-147">When to use the generated proxy</span></span>

<span data-ttu-id="1b4ad-148">Если требуется зарегистрировать несколько обработчиков событий для клиентского метода, который вызывается сервером, то созданный прокси-сервер использовать нельзя.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="1b4ad-149">В противном случае можно выбрать использование созданного прокси-сервера или не в зависимости от предпочтений в коде.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="1b4ad-150">Если вы решили не использовать его, не нужно ссылаться на URL-адрес "SignalR/Hubs" в элементе `script` в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="1b4ad-151">Настройка клиента</span><span class="sxs-lookup"><span data-stu-id="1b4ad-151">Client setup</span></span>

<span data-ttu-id="1b4ad-152">Клиенту JavaScript требуются ссылки на jQuery и основной файл JavaScript SignalR.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="1b4ad-153">Версия jQuery должна быть 1.6.4 или крупными более поздними версиями, такими как 1.7.2, 1.8.2 или 1.9.1.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="1b4ad-154">Если вы решили использовать созданный прокси-сервер, вам также потребуется ссылка на файл JavaScript, созданный SignalR.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="1b4ad-155">В следующем примере показано, как могут выглядеть ссылки на HTML-странице, использующей созданный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="1b4ad-156">Эти ссылки должны включаться в следующий порядок: jQuery First, SignalR Core после этого и, наконец, прокси-серверы SignalR.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="1b4ad-157">Как ссылаться на динамически создаваемый прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="1b4ad-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="1b4ad-158">В предыдущем примере ссылка на прокси-сервер, созданный SignalR, — это динамически созданный код JavaScript, а не физический файл.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="1b4ad-159">SignalR создает код JavaScript для прокси на лету и обслуживает его клиенту в ответ на URL-адрес "/сигналр/хубс".</span><span class="sxs-lookup"><span data-stu-id="1b4ad-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="1b4ad-160">Если вы указали другой базовый URL-адрес для соединений SignalR на сервере в методе `MapHubs`, URL-адрес динамически создаваемого прокси-файла — это пользовательский URL-адрес, к которому добавляется "/хубс".</span><span class="sxs-lookup"><span data-stu-id="1b4ad-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="1b4ad-161">Для клиентов JavaScript Windows 8 (Windows Store) используйте файл физического прокси-сервера вместо динамически созданного.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="1b4ad-162">Дополнительные сведения см. в подразделе [Создание физического файла для прокси-сервера, созданного SignalR](#manualproxy) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="1b4ad-163">В представлении Razor ASP.NET MVC 4 Используйте символ тильды для ссылки на корень приложения в ссылке на файл прокси-сервера:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="1b4ad-164">Дополнительные сведения об использовании SignalR в MVC 4 см. в разделе [Начало работы с SignalR и MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="1b4ad-165">В представлении Razor ASP.NET 3 Используйте `Url.Content` для ссылки на прокси-файл:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="1b4ad-166">В приложении ASP.NET Web Forms используйте `ResolveClientUrl` для доступа к файлу прокси-сервера или зарегистрируйте его через ScriptManager с помощью относительного пути к корню приложения (начиная с тильды):</span><span class="sxs-lookup"><span data-stu-id="1b4ad-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="1b4ad-167">Как правило, используйте тот же метод для указания URL-адреса "/сигналр/хубс", который используется для файлов CSS или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="1b4ad-168">Если вы указали URL-адрес без использования символа тильды, в некоторых сценариях приложение будет работать правильно при тестировании в Visual Studio с помощью IIS Express, но при развертывании в полной службе IIS произойдет ошибка 404.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="1b4ad-169">Дополнительные сведения см. в разделе **разрешение ссылок на ресурсы корневого уровня** на [веб-серверах в Visual Studio для веб-проектов ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="1b4ad-170">При запуске веб-проекта в Visual Studio 2012 в режиме отладки и при использовании Internet Explorer в качестве браузера можно просмотреть файл прокси-сервера в **Обозреватель решений** в разделе **документы сценария**, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![Созданный JavaScript файл прокси в обозреватель решений](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="1b4ad-172">Чтобы просмотреть содержимое файла, дважды щелкните элемент **концентраторы**.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="1b4ad-173">Если вы не используете Visual Studio 2012 и Internet Explorer или если вы не в режиме отладки, можно также получить содержимое файла, перейдя по URL-адресу "/Сигналр/хубс".</span><span class="sxs-lookup"><span data-stu-id="1b4ad-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="1b4ad-174">Например, если сайт работает на `http://localhost:56699`, перейдите в раздел `http://localhost:56699/SignalR/hubs` в браузере.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="1b4ad-175">Создание физического файла для прокси-сервера, созданного SignalR</span><span class="sxs-lookup"><span data-stu-id="1b4ad-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="1b4ad-176">В качестве альтернативы динамически создаваемому прокси-серверу можно создать физический файл с кодом прокси-сервера и ссылаться на этот файл.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="1b4ad-177">Это может потребоваться для контроля над кэшированием или объединением, а также для получения IntelliSense при кодировании вызовов к методам сервера.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="1b4ad-178">Чтобы создать прокси-файл, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="1b4ad-179">Установите пакет NuGet [Microsoft. AspNet. SignalR. utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) .</span><span class="sxs-lookup"><span data-stu-id="1b4ad-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="1b4ad-180">Откройте командную строку и перейдите в папку *Tools* , содержащую файл SignalR. exe.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="1b4ad-181">Папка Tools находится в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="1b4ad-182">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="1b4ad-183">Путь к *DLL* -файлу обычно является папкой *bin* в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="1b4ad-184">Эта команда создает файл с именем *Server. js* в той же папке, что и *SignalR. exe*.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="1b4ad-185">Поместите файл *Server. js* в соответствующую папку в проекте, переименуйте его в соответствии с вашими приложениями и добавьте ссылку на него вместо ссылки "SignalR/Hubs".</span><span class="sxs-lookup"><span data-stu-id="1b4ad-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="1b4ad-186">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="1b4ad-186">How to establish a connection</span></span>

<span data-ttu-id="1b4ad-187">Прежде чем установить соединение, необходимо создать объект соединения, создать прокси-сервер и зарегистрировать обработчики событий для методов, которые могут быть вызваны с сервера.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="1b4ad-188">При настройке прокси-сервера и обработчиков событий установите соединение, вызвав метод `start`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="1b4ad-189">Если вы используете созданный прокси-сервер, то не нужно создавать объект подключения в собственном коде, поскольку созданный код прокси делает это автоматически.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="1b4ad-190">**Установить соединение (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="1b4ad-191">**Установить соединение (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="1b4ad-192">В примере кода для подключения к службе SignalR используется URL-адрес по умолчанию "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="1b4ad-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="1b4ad-193">Сведения о том, как указать другой базовый URL-адрес, см. [в разделе ASP.NET SignalR Hub API Guide-Server-URL-адрес/SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="1b4ad-194">Обычно обработчики событий регистрируются перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="1b4ad-195">Если вы хотите зарегистрировать некоторые обработчики событий после установления соединения, это можно сделать, но необходимо зарегистрировать по крайней мере один из обработчиков событий перед вызовом метода `start`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="1b4ad-196">Одна из причин этого заключается в том, что в приложении может быть много концентраторов, но не требуется запускать событие `OnConnected` на каждом концентраторе, если вы собираетесь использовать только один из них.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="1b4ad-197">Когда соединение установлено, присутствие клиентского метода на прокси-сервере концентратора сообщает SignalR о необходимости активировать событие `OnConnected`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="1b4ad-198">Если вы не зарегистрировали обработчики событий перед вызовом метода `start`, вы сможете вызывать методы в центре, но метод `OnConnected` центра не будет вызываться, а клиентские методы не будут вызываться с сервера.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="1b4ad-199">$. Connection. Hub — это тот же объект, который создает $. Хубконнектион ()</span><span class="sxs-lookup"><span data-stu-id="1b4ad-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="1b4ad-200">Как видно из примеров, при использовании созданного прокси-сервера `$.connection.hub` ссылается на объект Connection.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="1b4ad-201">Это тот же объект, который можно получить, вызвав `$.hubConnection()`, если не используется созданный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="1b4ad-202">Созданный код прокси создает подключение для вас, выполняя следующую инструкцию:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Создание подключения в созданном прокси-файле](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="1b4ad-204">При использовании созданного прокси-сервера можно выполнять любые действия с `$.connection.hub`, которые можно выполнять с помощью объекта соединения, если не используется созданный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="1b4ad-205">Асинхронное выполнение метода Start</span><span class="sxs-lookup"><span data-stu-id="1b4ad-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="1b4ad-206">Метод `start` выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="1b4ad-207">Он возвращает [отложенный объект jQuery](http://api.jquery.com/category/deferred-object/). Это означает, что можно добавлять функции обратного вызова, вызывая такие методы, как `pipe`, `done`и `fail`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="1b4ad-208">Если имеется код, который необходимо выполнить после установления соединения, например вызов метода сервера, вставьте этот код в функцию обратного вызова или вызовите его из функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="1b4ad-209">Метод обратного вызова `.done` выполняется после установления соединения и после завершения выполнения любого кода в `OnConnected` метода обработчика событий на сервере.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="1b4ad-210">Если перед `.done` вызовом метода `start` вы поместили оператор "Now Connected" из предыдущего примера в качестве следующей строки кода, то `console.log`ная строка будет выполнена до установки соединения, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Неправильный способ написания кода, который выполняется после установления соединения](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="1b4ad-212">Как установить междоменное подключение</span><span class="sxs-lookup"><span data-stu-id="1b4ad-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="1b4ad-213">Как правило, если браузер загружает страницу из `http://contoso.com`, то подключение SignalR находится в том же домене, в `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="1b4ad-214">Если страница из `http://contoso.com` устанавливает подключение к `http://fabrikam.com/signalr`, то есть подключение между доменами.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="1b4ad-215">По соображениям безопасности междоменные соединения отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="1b4ad-216">Чтобы установить междоменное подключение, убедитесь, что на сервере включены междоменные соединения, и укажите URL-адрес соединения при создании объекта соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="1b4ad-217">SignalR будет использовать соответствующую технологию для междоменных подключений, таких как [JSONP](http://en.wikipedia.org/wiki/JSONP) или [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="1b4ad-218">На сервере включите междоменные соединения, выбрав этот параметр при вызове метода `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="1b4ad-219">На клиенте укажите URL-адрес при создании объекта соединения (без созданного прокси-сервера) или перед вызовом метода Start (с созданным прокси-сервером).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="1b4ad-220">**Клиентский код, указывающий междоменное соединение (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="1b4ad-221">**Клиентский код, указывающий междоменное соединение (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="1b4ad-222">При использовании конструктора `$.hubConnection` не нужно включать `signalr` в URL-адрес, так как он добавляется автоматически (если не указано `useDefaultUrl` как `false`).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="1b4ad-223">Можно создать несколько подключений к разным конечным точкам.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="1b4ad-224">Не устанавливайте в коде значение true для `jQuery.support.cors`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![Не устанавливайте jQuery. support. CORS в значение true](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="1b4ad-226">SignalR обрабатывает использование JSONP или CORS.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="1b4ad-227">Если присвоить параметру `jQuery.support.cors` значение true, JSONP отключается, так как в этом случае SignalR считает, что браузер поддерживает CORS.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="1b4ad-228">При подключении к URL-адресу localhost Internet Explorer 10 не будет считать его междоменным подключением, поэтому приложение будет работать локально с IE 10, даже если на сервере не включены междоменные соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="1b4ad-229">Сведения об использовании междоменных соединений с Internet Explorer 9 см. в [этом потоке StackOverflow](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="1b4ad-230">Сведения об использовании междоменных соединений с Chrome см. в [этом потоке StackOverflow](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="1b4ad-231">В примере кода для подключения к службе SignalR используется URL-адрес по умолчанию "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="1b4ad-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="1b4ad-232">Сведения о том, как указать другой базовый URL-адрес, см. [в разделе ASP.NET SignalR Hub API Guide-Server-URL-адрес/SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="1b4ad-233">Настройка подключения</span><span class="sxs-lookup"><span data-stu-id="1b4ad-233">How to configure the connection</span></span>

<span data-ttu-id="1b4ad-234">Прежде чем устанавливать соединение, можно указать параметры строки запроса или указать метод перевозки.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="1b4ad-235">Указание параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="1b4ad-235">How to specify query string parameters</span></span>

<span data-ttu-id="1b4ad-236">Если требуется отправлять данные на сервер при подключении клиента, можно добавить параметры строки запроса в объект соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="1b4ad-237">В следующих примерах показано, как задать параметр строки запроса в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="1b4ad-238">**Задать значение строки запроса перед вызовом метода Start (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="1b4ad-239">**Задать значение строки запроса перед вызовом метода Start (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="1b4ad-240">В следующем примере показано, как считать параметр строки запроса в серверном коде.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="1b4ad-241">Как указать метод перевозки</span><span class="sxs-lookup"><span data-stu-id="1b4ad-241">How to specify the transport method</span></span>

<span data-ttu-id="1b4ad-242">В рамках процесса подключения клиент SignalR обычно согласовывается с сервером для определения наилучшего транспорта, поддерживаемого как сервером, так и клиентом.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="1b4ad-243">Если вы уже уверены, какой транспорт вы хотите использовать, можно обойти этот процесс согласования, указав метод перевозки при вызове метода `start`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="1b4ad-244">**Клиентский код, указывающий транспортный метод (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="1b4ad-245">**Клиентский код, указывающий транспортный метод (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="1b4ad-246">В качестве альтернативы можно указать несколько методов транспорта в том порядке, в котором вы хотите, чтобы SignalR помогла их использовать.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="1b4ad-247">**Клиентский код, указывающий настраиваемую схему резервного транспорта (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="1b4ad-248">**Клиентский код, указывающий настраиваемую схему резервного транспорта (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="1b4ad-249">Для указания транспортного метода можно использовать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="1b4ad-250">WebSockets</span><span class="sxs-lookup"><span data-stu-id="1b4ad-250">"webSockets"</span></span>
- <span data-ttu-id="1b4ad-251">"Фореверфраме"</span><span class="sxs-lookup"><span data-stu-id="1b4ad-251">"foreverFrame"</span></span>
- <span data-ttu-id="1b4ad-252">"Серверсентевентс"</span><span class="sxs-lookup"><span data-stu-id="1b4ad-252">"serverSentEvents"</span></span>
- <span data-ttu-id="1b4ad-253">"Лонгполлинг"</span><span class="sxs-lookup"><span data-stu-id="1b4ad-253">"longPolling"</span></span>

<span data-ttu-id="1b4ad-254">В следующих примерах показано, как узнать, какой транспортный метод используется соединением.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="1b4ad-255">**Клиентский код, отображающий транспортный метод, используемый соединением (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="1b4ad-256">**Клиентский код, отображающий транспортный метод, используемый соединением (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="1b4ad-257">Сведения о том, как проверить транспортный метод в коде сервера, см. в разделе [ASP.NET SignalR Hub API Guide-Server-как получить сведения о клиенте из свойства Context](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="1b4ad-258">Дополнительные сведения о транспортировках и резервных запасах см. [в статье Введение в SignalR-транспорты и резервные стратегии](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="1b4ad-259">Как получить учетную запись-посредник для класса HUB</span><span class="sxs-lookup"><span data-stu-id="1b4ad-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="1b4ad-260">Каждый созданный объект соединения инкапсулирует сведения о соединении со службой SignalR, которая содержит один или несколько классов концентратора.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="1b4ad-261">Для взаимодействия с классом концентратора используется прокси-объект, создаваемый самостоятельно (если вы не используете созданный прокси) или который создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="1b4ad-262">На клиенте имя прокси-сервера — это версия имени класса концентратора в стиле Camel.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="1b4ad-263">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать соглашениям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="1b4ad-264">**Класс Hub на сервере**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="1b4ad-265">**Получение ссылки на созданный прокси клиента для концентратора**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="1b4ad-266">**Создание прокси клиента для класса Hub (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="1b4ad-267">Если класс Hub доменяется атрибутом `HubName`, используйте точное имя без изменения регистра.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="1b4ad-268">**Класс Hub на сервере с атрибутом HubName**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="1b4ad-269">**Получение ссылки на созданный прокси клиента для концентратора**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="1b4ad-270">**Создание прокси клиента для класса Hub (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="1b4ad-271">Определение методов на клиенте, который может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="1b4ad-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="1b4ad-272">Чтобы определить метод, который сервер может вызывать из концентратора, добавьте обработчик событий в прокси-сервер концентратора с помощью свойства `client` созданного прокси-сервера или вызовите метод `on`, если не используется созданный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="1b4ad-273">Параметры могут быть сложными объектами.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="1b4ad-274">Добавьте обработчик событий перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="1b4ad-275">(Если вы хотите добавить обработчики событий после вызова метода `start`, см. Примечание в статье [о том, как установить соединение](#establishconnection) ранее в этом документе, и используйте синтаксис, показанный для определения метода без использования созданного прокси-сервера.)</span><span class="sxs-lookup"><span data-stu-id="1b4ad-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="1b4ad-276">Сопоставление имен методов не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="1b4ad-277">Например, `Clients.All.addContosoChatMessageToPage` на сервере будет выполнять `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`или `addcontosochatmessagetopage` на клиенте.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="1b4ad-278">**Определение метода на клиенте (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="1b4ad-279">**Альтернативный способ определения метода на клиенте (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="1b4ad-280">**Определите метод на клиенте (без созданного прокси-сервера или при добавлении после вызова метода Start).**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="1b4ad-281">**Серверный код, вызывающий метод клиента**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="1b4ad-282">Следующие примеры включают сложный объект в качестве параметра метода.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="1b4ad-283">**Определите метод для клиента, который принимает сложный объект (с созданным прокси-сервером).**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="1b4ad-284">**Определите метод для клиента, который принимает сложный объект (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="1b4ad-285">**Серверный код, определяющий сложный объект**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="1b4ad-286">**Серверный код, вызывающий метод клиента с помощью сложного объекта**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="1b4ad-287">Вызов методов сервера из клиента</span><span class="sxs-lookup"><span data-stu-id="1b4ad-287">How to call server methods from the client</span></span>

<span data-ttu-id="1b4ad-288">Чтобы вызвать серверный метод из клиента, используйте свойство `server` созданного прокси-сервера или метод `invoke` на прокси-сервере концентратора, если не используется созданный прокси.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="1b4ad-289">Возвращаемое значение или параметры могут быть сложными объектами.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="1b4ad-290">Передайте в концентратор имя метода в стиле Camel.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="1b4ad-291">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать соглашениям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="1b4ad-292">В следующих примерах показано, как вызвать метод сервера, не имеющий возвращаемого значения, и как вызвать метод сервера, который имеет возвращаемое значение.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="1b4ad-293">**Серверный метод без атрибута Хубмесоднаме**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="1b4ad-294">**Серверный код, определяющий сложный объект, передаваемый в параметре**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="1b4ad-295">**Клиентский код, вызывающий метод сервера (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="1b4ad-296">**Клиентский код, вызывающий метод сервера (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="1b4ad-297">Если метод концентратора был дополнен атрибутом `HubMethodName`, используйте это имя без изменения регистра.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="1b4ad-298">**Серверный метод** с атрибутом хубмесоднаме</span><span class="sxs-lookup"><span data-stu-id="1b4ad-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="1b4ad-299">**Клиентский код, вызывающий метод сервера (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="1b4ad-300">**Клиентский код, вызывающий метод сервера (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="1b4ad-301">В предыдущих примерах показано, как вызвать метод сервера, не имеющий возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="1b4ad-302">В следующих примерах показано, как вызвать метод сервера, который имеет возвращаемое значение.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="1b4ad-303">**Серверный код для метода, имеющего возвращаемое значение**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="1b4ad-304">**Класс акции, используемый для** возвращаемого значения</span><span class="sxs-lookup"><span data-stu-id="1b4ad-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="1b4ad-305">**Клиентский код, вызывающий метод сервера (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="1b4ad-306">**Клиентский код, вызывающий метод сервера (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="1b4ad-307">Как работать с событиями времени жизни соединения</span><span class="sxs-lookup"><span data-stu-id="1b4ad-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="1b4ad-308">SignalR предоставляет следующие события времени жизни подключения, которые можно выполнять:</span><span class="sxs-lookup"><span data-stu-id="1b4ad-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="1b4ad-309">`starting`: возникает перед отправкой данных через соединение.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="1b4ad-310">`received`: возникает, когда в соединении получены какие-либо данные.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="1b4ad-311">Предоставляет полученные данные.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-311">Provides the received data.</span></span>
- <span data-ttu-id="1b4ad-312">`connectionSlow`: возникает, когда клиент обнаруживает слишком большое или частое удаление соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="1b4ad-313">`reconnecting`: возникает, когда начинается повторное подключение базового транспорта.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="1b4ad-314">`reconnected`: возникает при повторном подключении базового транспорта.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="1b4ad-315">`stateChanged`: возникает при изменении состояния соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="1b4ad-316">Обеспечивает старое состояние и новое состояние (подключение, подключение, повторное подключение или соединение разорвано).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="1b4ad-317">`disconnected`: возникает при отключении соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="1b4ad-318">Например, если вы хотите отображать предупреждающие сообщения при возникновении проблем с подключением, которые могут привести к заметным задержкам, обработайте событие `connectionSlow`.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="1b4ad-319">**Обрабатывает событие Коннектионслов (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="1b4ad-320">**Обрабатывает событие Коннектионслов (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="1b4ad-321">Дополнительные сведения см. [в разделе Основные сведения и обработка событий времени жизни подключения в SignalR](index.md).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="1b4ad-322">Как обрабатывались ошибки</span><span class="sxs-lookup"><span data-stu-id="1b4ad-322">How to handle errors</span></span>

<span data-ttu-id="1b4ad-323">Клиент JavaScript SignalR предоставляет `error` событие, для которого можно добавить обработчик.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="1b4ad-324">Также можно использовать метод Fail, чтобы добавить обработчик для ошибок, возникших в результате вызова метода сервера.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="1b4ad-325">Если на сервере явно не включены подробные сообщения об ошибках, то объект исключения, возвращаемый SignalR после ошибки, содержит минимальные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="1b4ad-326">Например, если вызов `newContosoChatMessage` завершается ошибкой, сообщение об ошибке в объекте Error содержит "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Отправка подробных сообщений об ошибках клиентам в рабочей среде не рекомендуется по соображениям безопасности, но если вы хотите включить подробные сообщения об ошибках для устранения неполадок, используйте следующий код на сервере.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="1b4ad-327">В следующем примере показано, как добавить обработчик для события ошибки.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="1b4ad-328">**Добавление обработчика ошибок (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="1b4ad-329">**Добавление обработчика ошибок (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="1b4ad-330">В следующем примере показано, как выполнить обработку ошибки из вызова метода.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="1b4ad-331">**Обрабатывает ошибку при вызове метода (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="1b4ad-332">**Обрабатывает ошибку при вызове метода (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="1b4ad-333">При сбое вызова метода также вызывается событие `error`, поэтому код в обработчике метода `error` и в обратном вызове метода `.fail` будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="1b4ad-334">Как включить ведение журнала на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="1b4ad-334">How to enable client-side logging</span></span>

<span data-ttu-id="1b4ad-335">Чтобы включить ведение журнала на стороне клиента для соединения, задайте свойство `logging` объекта соединения перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="1b4ad-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="1b4ad-336">**Включить ведение журнала (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="1b4ad-337">**Включить ведение журнала (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="1b4ad-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="1b4ad-338">Чтобы просмотреть журналы, откройте средства разработчика в браузере и перейдите на вкладку "консоль". Руководство, в котором показаны пошаговые инструкции и снимки экрана, в которых показано, как это сделать, см. в разделе [серверное вещание с помощью ASP.NET SignalR. Включение ведения журнала](index.md).</span><span class="sxs-lookup"><span data-stu-id="1b4ad-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
