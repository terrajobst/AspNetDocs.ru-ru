---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: Путеводитель по API концентраторов SignalR ASP.NET — клиент JavaScript | Документация Майкрософт
author: bradygaster
description: В этом документе содержатся общие сведения об использовании API концентраторов для SignalR версии 2 в клиентах JavaScript, таких как браузеры и магазин Windows (WinJS) аппликат...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431292"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="5cb3b-103">Путеводитель по API концентраторов SignalR ASP.NET — клиент JavaScript</span><span class="sxs-lookup"><span data-stu-id="5cb3b-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5cb3b-104">В этом документе содержатся общие сведения об использовании API концентраторов для SignalR версии 2 в клиентах JavaScript, таких как браузеры и приложения Магазина Windows (WinJS).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="5cb3b-105">API концентраторов SignalR позволяет выполнять удаленные вызовы процедур (RPC) с сервера на подключенные клиенты и с клиентов на сервер.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="5cb3b-106">В серверном коде определяются методы, которые могут вызываться клиентами, и вызываются методы, которые выполняются на клиенте.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="5cb3b-107">В клиентском коде определяются методы, которые могут быть вызваны с сервера, а также вызываются методы, которые выполняются на сервере.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="5cb3b-108">Этот механизм отвечает за все клиентские коммуникации.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="5cb3b-109">SignalR также предлагает интерфейс API более низкого уровня, называемый постоянными подключениями.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="5cb3b-110">Общие сведения о SignalR, концентраторах и постоянных подключениях см. [в статье Общие сведения о SignalR](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="5cb3b-111">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="5cb3b-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="5cb3b-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="5cb3b-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="5cb3b-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5cb3b-113">.NET 4.5</span></span>
> - <span data-ttu-id="5cb3b-114">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="5cb3b-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="5cb3b-115">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="5cb3b-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="5cb3b-116">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="5cb3b-117">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="5cb3b-117">Questions and comments</span></span>
>
> <span data-ttu-id="5cb3b-118">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5cb3b-119">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="5cb3b-120">Обзор</span><span class="sxs-lookup"><span data-stu-id="5cb3b-120">Overview</span></span>

<span data-ttu-id="5cb3b-121">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="5cb3b-122">Созданный прокси-сервер и его назначение</span><span class="sxs-lookup"><span data-stu-id="5cb3b-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="5cb3b-123">Когда следует использовать созданный прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="5cb3b-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="5cb3b-124">Установка клиента</span><span class="sxs-lookup"><span data-stu-id="5cb3b-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="5cb3b-125">Как ссылаться на динамически создаваемый прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="5cb3b-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="5cb3b-126">Создание физического файла для прокси-сервера, созданного SignalR</span><span class="sxs-lookup"><span data-stu-id="5cb3b-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="5cb3b-127">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="5cb3b-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="5cb3b-128">$. Connection. Hub — это тот же объект, который создает $. Хубконнектион ()</span><span class="sxs-lookup"><span data-stu-id="5cb3b-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="5cb3b-129">Асинхронное выполнение метода Start</span><span class="sxs-lookup"><span data-stu-id="5cb3b-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="5cb3b-130">Как установить междоменное подключение</span><span class="sxs-lookup"><span data-stu-id="5cb3b-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="5cb3b-131">Настройка подключения</span><span class="sxs-lookup"><span data-stu-id="5cb3b-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="5cb3b-132">Указание параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="5cb3b-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="5cb3b-133">Как указать метод перевозки</span><span class="sxs-lookup"><span data-stu-id="5cb3b-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="5cb3b-134">Как получить учетную запись-посредник для класса HUB</span><span class="sxs-lookup"><span data-stu-id="5cb3b-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="5cb3b-135">Определение методов на клиенте, который может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="5cb3b-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="5cb3b-136">Вызов методов сервера из клиента</span><span class="sxs-lookup"><span data-stu-id="5cb3b-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="5cb3b-137">Как работать с событиями времени жизни соединения</span><span class="sxs-lookup"><span data-stu-id="5cb3b-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="5cb3b-138">Как обрабатывались ошибки</span><span class="sxs-lookup"><span data-stu-id="5cb3b-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="5cb3b-139">Как включить ведение журнала на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="5cb3b-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="5cb3b-140">Документацию по программированию клиентов сервера или .NET см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="5cb3b-141">Путеводитель по API концентраторов SignalR — сервер</span><span class="sxs-lookup"><span data-stu-id="5cb3b-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="5cb3b-142">Путеводитель по API концентраторов SignalR — клиент .NET</span><span class="sxs-lookup"><span data-stu-id="5cb3b-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="5cb3b-143">Серверный компонент SignalR 2 доступен только в .NET 4,5 (хотя существует клиент .NET для SignalR 2 в .NET 4,0).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="5cb3b-144">Созданный прокси-сервер и его назначение</span><span class="sxs-lookup"><span data-stu-id="5cb3b-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="5cb3b-145">Вы можете программировать клиент JavaScript для взаимодействия со службой SignalR с прокси-сервером, который генерирует SignalR, или без него.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="5cb3b-146">То, что делает прокси-сервер, упрощает синтаксис кода, используемого для соединения, создания методов, которые сервер вызывает, и вызова методов на сервере.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="5cb3b-147">При написании кода для вызова методов сервера созданный прокси-сервер позволяет использовать синтаксис, который выглядит так, как если бы выполнялась локальная функция: можно написать `serverMethod(arg1, arg2)` вместо `invoke('serverMethod', arg1, arg2)`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="5cb3b-148">Сформированный синтаксис прокси-сервера также позволяет немедленно и расшифровать ошибку на стороне клиента при ошибочном вводе имени метода сервера.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="5cb3b-149">Если вы вручную создаете файл, который определяет прокси-серверы, можно также получить поддержку IntelliSense для написания кода, который вызывает методы сервера.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="5cb3b-150">Например, предположим, что на сервере имеется следующий класс концентратора:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="5cb3b-151">В следующих примерах кода показано, как выглядит код JavaScript для вызова метода `NewContosoChatMessage` на сервере и получения вызовов метода `addContosoChatMessageToPage` с сервера.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="5cb3b-152">**С созданным прокси-сервером**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="5cb3b-153">**Без созданного прокси-сервера**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="5cb3b-154">Когда следует использовать созданный прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="5cb3b-154">When to use the generated proxy</span></span>

<span data-ttu-id="5cb3b-155">Если требуется зарегистрировать несколько обработчиков событий для клиентского метода, который вызывается сервером, то созданный прокси-сервер использовать нельзя.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="5cb3b-156">В противном случае можно выбрать использование созданного прокси-сервера или не в зависимости от предпочтений в коде.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="5cb3b-157">Если вы решили не использовать его, не нужно ссылаться на URL-адрес "SignalR/Hubs" в элементе `script` в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="5cb3b-158">Настройка клиента</span><span class="sxs-lookup"><span data-stu-id="5cb3b-158">Client setup</span></span>

<span data-ttu-id="5cb3b-159">Клиенту JavaScript требуются ссылки на jQuery и основной файл JavaScript SignalR.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="5cb3b-160">Версия jQuery должна быть 1.6.4 или крупными более поздними версиями, такими как 1.7.2, 1.8.2 или 1.9.1.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="5cb3b-161">Если вы решили использовать созданный прокси-сервер, вам также потребуется ссылка на файл JavaScript, созданный SignalR.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="5cb3b-162">В следующем примере показано, как могут выглядеть ссылки на HTML-странице, использующей созданный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="5cb3b-163">Эти ссылки должны включаться в следующий порядок: jQuery First, SignalR Core после этого и, наконец, прокси-серверы SignalR.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="5cb3b-164">Как ссылаться на динамически создаваемый прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="5cb3b-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="5cb3b-165">В предыдущем примере ссылка на прокси-сервер, созданный SignalR, — это динамически созданный код JavaScript, а не физический файл.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="5cb3b-166">SignalR создает код JavaScript для прокси на лету и обслуживает его клиенту в ответ на URL-адрес "/сигналр/хубс".</span><span class="sxs-lookup"><span data-stu-id="5cb3b-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="5cb3b-167">Если вы указали другой базовый URL-адрес для соединений SignalR на сервере в методе `MapSignalR`, URL-адрес динамически создаваемого прокси-файла — это пользовательский URL-адрес, к которому добавляется "/хубс".</span><span class="sxs-lookup"><span data-stu-id="5cb3b-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="5cb3b-168">Для клиентов JavaScript Windows 8 (Windows Store) используйте файл физического прокси-сервера вместо динамически созданного.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="5cb3b-169">Дополнительные сведения см. в подразделе [Создание физического файла для прокси-сервера, созданного SignalR](#manualproxy) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="5cb3b-170">В представлении Razor ASP.NET 4 или 5 Используйте символ тильды для ссылки на корень приложения в ссылке на файл прокси-сервера:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="5cb3b-171">Дополнительные сведения об использовании SignalR в MVC 5 см. в разделе [Начало работы с SignalR и MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="5cb3b-172">В представлении Razor ASP.NET 3 Используйте `Url.Content` для ссылки на прокси-файл:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="5cb3b-173">В приложении ASP.NET Web Forms используйте `ResolveClientUrl` для доступа к файлу прокси-сервера или зарегистрируйте его через ScriptManager с помощью относительного пути к корню приложения (начиная с тильды):</span><span class="sxs-lookup"><span data-stu-id="5cb3b-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="5cb3b-174">Как правило, используйте тот же метод для указания URL-адреса "/сигналр/хубс", который используется для файлов CSS или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="5cb3b-175">Если вы указали URL-адрес без использования символа тильды, в некоторых сценариях приложение будет работать правильно при тестировании в Visual Studio с помощью IIS Express, но при развертывании в полной службе IIS произойдет ошибка 404.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="5cb3b-176">Дополнительные сведения см. в разделе **разрешение ссылок на ресурсы корневого уровня** на [веб-серверах в Visual Studio для веб-проектов ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="5cb3b-177">При запуске веб-проекта в Visual Studio 2017 в режиме отладки и при использовании Internet Explorer в качестве браузера можно просмотреть файл прокси-сервера в **Обозреватель решений** в разделе **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="5cb3b-178">Чтобы просмотреть содержимое файла, дважды щелкните элемент **концентраторы**.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="5cb3b-179">Если вы не используете Visual Studio 2012 или 2013 и Internet Explorer или если вы не в режиме отладки, можно также получить содержимое файла, перейдя по URL-адресу "/Сигналр/хубс".</span><span class="sxs-lookup"><span data-stu-id="5cb3b-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="5cb3b-180">Например, если сайт работает на `http://localhost:56699`, перейдите в раздел `http://localhost:56699/SignalR/hubs` в браузере.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="5cb3b-181">Создание физического файла для прокси-сервера, созданного SignalR</span><span class="sxs-lookup"><span data-stu-id="5cb3b-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="5cb3b-182">В качестве альтернативы динамически создаваемому прокси-серверу можно создать физический файл с кодом прокси-сервера и ссылаться на этот файл.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="5cb3b-183">Это может потребоваться для контроля над кэшированием или объединением, а также для получения IntelliSense при кодировании вызовов к методам сервера.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="5cb3b-184">Чтобы создать прокси-файл, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="5cb3b-185">Установите пакет NuGet [Microsoft. AspNet. SignalR. utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) .</span><span class="sxs-lookup"><span data-stu-id="5cb3b-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="5cb3b-186">Откройте командную строку и перейдите в папку *Tools* , содержащую файл SignalR. exe.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="5cb3b-187">Папка Tools находится в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="5cb3b-188">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="5cb3b-189">Путь к *DLL* -файлу обычно является папкой *bin* в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="5cb3b-190">Эта команда создает файл с именем *Server. js* в той же папке, что и *SignalR. exe*.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="5cb3b-191">Поместите файл *Server. js* в соответствующую папку в проекте, переименуйте его в соответствии с вашими приложениями и добавьте ссылку на него вместо ссылки "SignalR/Hubs".</span><span class="sxs-lookup"><span data-stu-id="5cb3b-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="5cb3b-192">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="5cb3b-192">How to establish a connection</span></span>

<span data-ttu-id="5cb3b-193">Прежде чем установить соединение, необходимо создать объект соединения, создать прокси-сервер и зарегистрировать обработчики событий для методов, которые могут быть вызваны с сервера.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="5cb3b-194">При настройке прокси-сервера и обработчиков событий установите соединение, вызвав метод `start`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="5cb3b-195">Если вы используете созданный прокси-сервер, то не нужно создавать объект подключения в собственном коде, поскольку созданный код прокси делает это автоматически.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="5cb3b-196">**Установить соединение (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="5cb3b-197">**Установить соединение (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="5cb3b-198">В примере кода для подключения к службе SignalR используется URL-адрес по умолчанию "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="5cb3b-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="5cb3b-199">Сведения о том, как указать другой базовый URL-адрес, см. [в разделе ASP.NET SignalR Hub API Guide-Server-URL-адрес/SignalR](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="5cb3b-200">По умолчанию расположением концентратора является текущий сервер. При подключении к другому серверу укажите URL-адрес перед вызовом метода `start`, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="5cb3b-201">Обычно обработчики событий регистрируются перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="5cb3b-202">Если вы хотите зарегистрировать некоторые обработчики событий после установления соединения, это можно сделать, но необходимо зарегистрировать по крайней мере один из обработчиков событий перед вызовом метода `start`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="5cb3b-203">Одна из причин этого заключается в том, что в приложении может быть много концентраторов, но не требуется запускать событие `OnConnected` на каждом концентраторе, если вы собираетесь использовать только один из них.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="5cb3b-204">Когда соединение установлено, присутствие клиентского метода на прокси-сервере концентратора сообщает SignalR о необходимости активировать событие `OnConnected`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="5cb3b-205">Если вы не зарегистрировали обработчики событий перед вызовом метода `start`, вы сможете вызывать методы в центре, но метод `OnConnected` центра не будет вызываться, а клиентские методы не будут вызываться с сервера.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="5cb3b-206">$. Connection. Hub — это тот же объект, который создает $. Хубконнектион ()</span><span class="sxs-lookup"><span data-stu-id="5cb3b-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="5cb3b-207">Как видно из примеров, при использовании созданного прокси-сервера `$.connection.hub` ссылается на объект Connection.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="5cb3b-208">Это тот же объект, который можно получить, вызвав `$.hubConnection()`, если не используется созданный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="5cb3b-209">Созданный код прокси создает подключение для вас, выполняя следующую инструкцию:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Создание подключения в созданном прокси-файле](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="5cb3b-211">При использовании созданного прокси-сервера можно выполнять любые действия с `$.connection.hub`, которые можно выполнять с помощью объекта соединения, если не используется созданный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="5cb3b-212">Асинхронное выполнение метода Start</span><span class="sxs-lookup"><span data-stu-id="5cb3b-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="5cb3b-213">Метод `start` выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="5cb3b-214">Он возвращает [отложенный объект jQuery](http://api.jquery.com/category/deferred-object/). Это означает, что можно добавлять функции обратного вызова, вызывая такие методы, как `pipe`, `done`и `fail`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="5cb3b-215">Если имеется код, который необходимо выполнить после установления соединения, например вызов метода сервера, вставьте этот код в функцию обратного вызова или вызовите его из функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="5cb3b-216">Метод обратного вызова `.done` выполняется после установления соединения и после завершения выполнения любого кода в `OnConnected` метода обработчика событий на сервере.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="5cb3b-217">Если перед `.done` вызовом метода `start` вы поместили оператор "Now Connected" из предыдущего примера в качестве следующей строки кода, то `console.log`ная строка будет выполнена до установки соединения, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Неправильный способ написания кода, который выполняется после установления соединения](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="5cb3b-219">Как установить междоменное подключение</span><span class="sxs-lookup"><span data-stu-id="5cb3b-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="5cb3b-220">Как правило, если браузер загружает страницу из `http://contoso.com`, то подключение SignalR находится в том же домене, в `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="5cb3b-221">Если страница из `http://contoso.com` устанавливает подключение к `http://fabrikam.com/signalr`, то есть подключение между доменами.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="5cb3b-222">По соображениям безопасности междоменные соединения отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="5cb3b-223">В SignalR 1. x запросы между доменами управляются одним флагом Енаблекроссдомаин.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="5cb3b-224">Этот флаг управляет запросами JSONP и CORS.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="5cb3b-225">Для большей гибкости вся поддержка CORS была удалена из серверного компонента SignalR (клиенты JavaScript по-прежнему используют CORS обычным образом, если обнаружено, что браузер поддерживает его), а новое по промежуточного слоя OWIN доступно для поддержки этих сценариев.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="5cb3b-226">Если для клиента требуется поддержка JSONP (для поддержки междоменных запросов в более старых браузерах), ее необходимо включить явным образом, установив `EnableJSONP` для объекта `HubConfiguration` в значение `true`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="5cb3b-227">JSONP по умолчанию отключен, так как он менее безопасен, чем CORS.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="5cb3b-228">**Добавление Microsoft. Owin. CORS в проект:** Чтобы установить эту библиотеку, выполните в консоли диспетчера пакетов следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="5cb3b-229">Эта команда добавит версию пакета 2.1.0 в проект.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="5cb3b-230">Вызов UseCors</span><span class="sxs-lookup"><span data-stu-id="5cb3b-230">Calling UseCors</span></span>

 <span data-ttu-id="5cb3b-231">В следующем фрагменте кода показано, как реализовать междоменные соединения в SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="5cb3b-232">**Реализация запросов между доменами в SignalR 2**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="5cb3b-233">В следующем коде показано, как включить CORS или JSONP в проекте SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="5cb3b-234">В этом примере кода используется `Map` и `RunSignalR` вместо `MapSignalR`, чтобы по промежуточного слоя CORS выполнялось только для запросов SignalR, требующих поддержки CORS (а не для всего трафика по пути, указанному в `MapSignalR`). Map можно также использовать для любого другого по промежуточного слоя, который должен выполняться для конкретного префикса URL-адреса, а не для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="5cb3b-235">Не устанавливайте в коде значение true для `jQuery.support.cors`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![Не устанавливайте jQuery. support. CORS в значение true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="5cb3b-237">SignalR обрабатывает использование CORS.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="5cb3b-238">Если присвоить параметру `jQuery.support.cors` значение true, JSONP отключается, так как в этом случае SignalR считает, что браузер поддерживает CORS.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="5cb3b-239">При подключении к URL-адресу localhost Internet Explorer 10 не будет считать его междоменным подключением, поэтому приложение будет работать локально с IE 10, даже если на сервере не включены междоменные соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="5cb3b-240">Сведения об использовании междоменных соединений с Internet Explorer 9 см. в [этом потоке StackOverflow](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="5cb3b-241">Сведения об использовании междоменных соединений с Chrome см. в [этом потоке StackOverflow](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="5cb3b-242">В примере кода для подключения к службе SignalR используется URL-адрес по умолчанию "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="5cb3b-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="5cb3b-243">Сведения о том, как указать другой базовый URL-адрес, см. [в разделе ASP.NET SignalR Hub API Guide-Server-URL-адрес/SignalR](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="5cb3b-244">Настройка подключения</span><span class="sxs-lookup"><span data-stu-id="5cb3b-244">How to configure the connection</span></span>

<span data-ttu-id="5cb3b-245">Прежде чем устанавливать соединение, можно указать параметры строки запроса или указать метод перевозки.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="5cb3b-246">Указание параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="5cb3b-246">How to specify query string parameters</span></span>

<span data-ttu-id="5cb3b-247">Если требуется отправлять данные на сервер при подключении клиента, можно добавить параметры строки запроса в объект соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="5cb3b-248">В следующих примерах показано, как задать параметр строки запроса в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="5cb3b-249">**Задать значение строки запроса перед вызовом метода Start (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="5cb3b-250">**Задать значение строки запроса перед вызовом метода Start (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="5cb3b-251">В следующем примере показано, как считать параметр строки запроса в серверном коде.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="5cb3b-252">Как указать метод перевозки</span><span class="sxs-lookup"><span data-stu-id="5cb3b-252">How to specify the transport method</span></span>

<span data-ttu-id="5cb3b-253">В рамках процесса подключения клиент SignalR обычно согласовывается с сервером для определения наилучшего транспорта, поддерживаемого как сервером, так и клиентом.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="5cb3b-254">Если вы уже уверены, какой транспорт вы хотите использовать, можно обойти этот процесс согласования, указав метод перевозки при вызове метода `start`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="5cb3b-255">**Клиентский код, указывающий транспортный метод (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="5cb3b-256">**Клиентский код, указывающий транспортный метод (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="5cb3b-257">В качестве альтернативы можно указать несколько методов транспорта в том порядке, в котором вы хотите, чтобы SignalR помогла их использовать.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="5cb3b-258">**Клиентский код, указывающий настраиваемую схему резервного транспорта (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="5cb3b-259">**Клиентский код, указывающий настраиваемую схему резервного транспорта (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="5cb3b-260">Для указания транспортного метода можно использовать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="5cb3b-261">WebSockets</span><span class="sxs-lookup"><span data-stu-id="5cb3b-261">"webSockets"</span></span>
- <span data-ttu-id="5cb3b-262">"Фореверфраме"</span><span class="sxs-lookup"><span data-stu-id="5cb3b-262">"foreverFrame"</span></span>
- <span data-ttu-id="5cb3b-263">"Серверсентевентс"</span><span class="sxs-lookup"><span data-stu-id="5cb3b-263">"serverSentEvents"</span></span>
- <span data-ttu-id="5cb3b-264">"Лонгполлинг"</span><span class="sxs-lookup"><span data-stu-id="5cb3b-264">"longPolling"</span></span>

<span data-ttu-id="5cb3b-265">В следующих примерах показано, как узнать, какой транспортный метод используется соединением.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="5cb3b-266">**Клиентский код, отображающий транспортный метод, используемый соединением (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="5cb3b-267">**Клиентский код, отображающий транспортный метод, используемый соединением (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="5cb3b-268">Сведения о том, как проверить транспортный метод в коде сервера, см. в разделе [ASP.NET SignalR Hub API Guide-Server-как получить сведения о клиенте из свойства Context](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="5cb3b-269">Дополнительные сведения о транспортировках и резервных запасах см. [в статье Введение в SignalR-транспорты и резервные стратегии](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="5cb3b-270">Как получить учетную запись-посредник для класса HUB</span><span class="sxs-lookup"><span data-stu-id="5cb3b-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="5cb3b-271">Каждый созданный объект соединения инкапсулирует сведения о соединении со службой SignalR, которая содержит один или несколько классов концентратора.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="5cb3b-272">Для взаимодействия с классом концентратора используется прокси-объект, создаваемый самостоятельно (если вы не используете созданный прокси) или который создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="5cb3b-273">На клиенте имя прокси-сервера — это версия имени класса концентратора в стиле Camel.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="5cb3b-274">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать соглашениям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="5cb3b-275">**Класс Hub на сервере**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="5cb3b-276">**Получение ссылки на созданный прокси клиента для концентратора**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="5cb3b-277">**Создание прокси клиента для класса Hub (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="5cb3b-278">Если класс Hub доменяется атрибутом `HubName`, используйте точное имя без изменения регистра.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="5cb3b-279">**Класс Hub на сервере с атрибутом HubName**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="5cb3b-280">**Получение ссылки на созданный прокси клиента для концентратора**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="5cb3b-281">**Создание прокси клиента для класса Hub (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="5cb3b-282">Определение методов на клиенте, который может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="5cb3b-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="5cb3b-283">Чтобы определить метод, который сервер может вызывать из концентратора, добавьте обработчик событий в прокси-сервер концентратора с помощью свойства `client` созданного прокси-сервера или вызовите метод `on`, если не используется созданный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="5cb3b-284">Параметры могут быть сложными объектами.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="5cb3b-285">Добавьте обработчик событий перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="5cb3b-286">(Если вы хотите добавить обработчики событий после вызова метода `start`, см. Примечание в статье [о том, как установить соединение](#establishconnection) ранее в этом документе, и используйте синтаксис, показанный для определения метода без использования созданного прокси-сервера.)</span><span class="sxs-lookup"><span data-stu-id="5cb3b-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="5cb3b-287">Сопоставление имен методов не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="5cb3b-288">Например, `Clients.All.addContosoChatMessageToPage` на сервере будет выполнять `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`или `addcontosochatmessagetopage` на клиенте.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="5cb3b-289">**Определение метода на клиенте (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="5cb3b-290">**Альтернативный способ определения метода на клиенте (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="5cb3b-291">**Определите метод на клиенте (без созданного прокси-сервера или при добавлении после вызова метода Start).**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="5cb3b-292">**Серверный код, вызывающий метод клиента**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="5cb3b-293">Следующие примеры включают сложный объект в качестве параметра метода.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="5cb3b-294">**Определите метод для клиента, который принимает сложный объект (с созданным прокси-сервером).**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="5cb3b-295">**Определите метод для клиента, который принимает сложный объект (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="5cb3b-296">**Серверный код, определяющий сложный объект**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="5cb3b-297">**Серверный код, вызывающий метод клиента с помощью сложного объекта**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="5cb3b-298">Вызов методов сервера из клиента</span><span class="sxs-lookup"><span data-stu-id="5cb3b-298">How to call server methods from the client</span></span>

<span data-ttu-id="5cb3b-299">Чтобы вызвать серверный метод из клиента, используйте свойство `server` созданного прокси-сервера или метод `invoke` на прокси-сервере концентратора, если не используется созданный прокси.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="5cb3b-300">Возвращаемое значение или параметры могут быть сложными объектами.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="5cb3b-301">Передайте в концентратор имя метода в стиле Camel.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="5cb3b-302">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать соглашениям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="5cb3b-303">В следующих примерах показано, как вызвать метод сервера, не имеющий возвращаемого значения, и как вызвать метод сервера, который имеет возвращаемое значение.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="5cb3b-304">**Серверный метод без атрибута Хубмесоднаме**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="5cb3b-305">**Серверный код, определяющий сложный объект, передаваемый в параметре**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="5cb3b-306">**Клиентский код, вызывающий метод сервера (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="5cb3b-307">**Клиентский код, вызывающий метод сервера (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="5cb3b-308">Если метод концентратора был дополнен атрибутом `HubMethodName`, используйте это имя без изменения регистра.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="5cb3b-309">**Серверный метод** с атрибутом хубмесоднаме</span><span class="sxs-lookup"><span data-stu-id="5cb3b-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="5cb3b-310">**Клиентский код, вызывающий метод сервера (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="5cb3b-311">**Клиентский код, вызывающий метод сервера (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="5cb3b-312">В предыдущих примерах показано, как вызвать метод сервера, не имеющий возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="5cb3b-313">В следующих примерах показано, как вызвать метод сервера, который имеет возвращаемое значение.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="5cb3b-314">**Серверный код для метода, имеющего возвращаемое значение**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="5cb3b-315">**Класс акции, используемый для** возвращаемого значения</span><span class="sxs-lookup"><span data-stu-id="5cb3b-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="5cb3b-316">**Клиентский код, вызывающий метод сервера (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="5cb3b-317">**Клиентский код, вызывающий метод сервера (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="5cb3b-318">Как работать с событиями времени жизни соединения</span><span class="sxs-lookup"><span data-stu-id="5cb3b-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="5cb3b-319">SignalR предоставляет следующие события времени жизни подключения, которые можно выполнять:</span><span class="sxs-lookup"><span data-stu-id="5cb3b-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="5cb3b-320">`starting`: возникает перед отправкой данных через соединение.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="5cb3b-321">`received`: возникает, когда в соединении получены какие-либо данные.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="5cb3b-322">Предоставляет полученные данные.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-322">Provides the received data.</span></span>
- <span data-ttu-id="5cb3b-323">`connectionSlow`: возникает, когда клиент обнаруживает слишком большое или частое удаление соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="5cb3b-324">`reconnecting`: возникает, когда начинается повторное подключение базового транспорта.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="5cb3b-325">`reconnected`: возникает при повторном подключении базового транспорта.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="5cb3b-326">`stateChanged`: возникает при изменении состояния соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="5cb3b-327">Обеспечивает старое состояние и новое состояние (подключение, подключение, повторное подключение или соединение разорвано).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="5cb3b-328">`disconnected`: возникает при отключении соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="5cb3b-329">Например, если вы хотите отображать предупреждающие сообщения при возникновении проблем с подключением, которые могут привести к заметным задержкам, обработайте событие `connectionSlow`.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="5cb3b-330">**Обрабатывает событие Коннектионслов (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="5cb3b-331">**Обрабатывает событие Коннектионслов (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="5cb3b-332">Дополнительные сведения см. [в разделе Основные сведения и обработка событий времени жизни подключения в SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="5cb3b-333">Как обрабатывались ошибки</span><span class="sxs-lookup"><span data-stu-id="5cb3b-333">How to handle errors</span></span>

<span data-ttu-id="5cb3b-334">Клиент JavaScript SignalR предоставляет `error` событие, для которого можно добавить обработчик.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="5cb3b-335">Также можно использовать метод Fail, чтобы добавить обработчик для ошибок, возникших в результате вызова метода сервера.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="5cb3b-336">Если на сервере явно не включены подробные сообщения об ошибках, то объект исключения, возвращаемый SignalR после ошибки, содержит минимальные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="5cb3b-337">Например, если вызов `newContosoChatMessage` завершается ошибкой, сообщение об ошибке в объекте Error содержит "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Отправка подробных сообщений об ошибках клиентам в рабочей среде не рекомендуется по соображениям безопасности, но если вы хотите включить подробные сообщения об ошибках для устранения неполадок, используйте следующий код на сервере.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="5cb3b-338">В следующем примере показано, как добавить обработчик для события ошибки.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="5cb3b-339">**Добавление обработчика ошибок (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="5cb3b-340">**Добавление обработчика ошибок (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="5cb3b-341">В следующем примере показано, как выполнить обработку ошибки из вызова метода.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="5cb3b-342">**Обрабатывает ошибку при вызове метода (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="5cb3b-343">**Обрабатывает ошибку при вызове метода (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="5cb3b-344">При сбое вызова метода также вызывается событие `error`, поэтому код в обработчике метода `error` и в обратном вызове метода `.fail` будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="5cb3b-345">Как включить ведение журнала на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="5cb3b-345">How to enable client-side logging</span></span>

<span data-ttu-id="5cb3b-346">Чтобы включить ведение журнала на стороне клиента для соединения, задайте свойство `logging` объекта соединения перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb3b-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="5cb3b-347">**Включить ведение журнала (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="5cb3b-348">**Включить ведение журнала (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="5cb3b-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="5cb3b-349">Чтобы просмотреть журналы, откройте средства разработчика в браузере и перейдите на вкладку "консоль". Руководство, в котором показаны пошаговые инструкции и снимки экрана, в которых показано, как это сделать, см. в разделе [серверное вещание с помощью ASP.NET SignalR. Включение ведения журнала](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span><span class="sxs-lookup"><span data-stu-id="5cb3b-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
