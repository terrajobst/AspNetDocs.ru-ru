---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Примеры Katana | Документация Майкрософт
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472350"
---
# <a name="katana-samples"></a><span data-ttu-id="a2c39-102">Примеры Katana</span><span class="sxs-lookup"><span data-stu-id="a2c39-102">Katana Samples</span></span>

<span data-ttu-id="a2c39-103">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a2c39-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="a2c39-104">Примеры Katana</span><span class="sxs-lookup"><span data-stu-id="a2c39-104">Katana Samples</span></span>

<span data-ttu-id="a2c39-105">Пример [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes) | **маршрутов ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="a2c39-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="a2c39-106">В некоторых приложениях необходимо подключать компоненты OWIN в таблице маршрутизации Asp.Net параллельно с компонентами, отличными от OWIN.</span><span class="sxs-lookup"><span data-stu-id="a2c39-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="a2c39-107">В этом примере показано, как использовать методы расширения RouteCollection Маповинпас и Маповинрауте, предоставляемые Microsoft. Owin. host. SystemWeb.</span><span class="sxs-lookup"><span data-stu-id="a2c39-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="a2c39-108">**Пример конвейеров ветвления** | [исходном коде](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="a2c39-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="a2c39-109">Конвейеры обработки запросов OWIN не должны быть линейными, они могут быть разветвлены для обработки запросов различными способами.</span><span class="sxs-lookup"><span data-stu-id="a2c39-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="a2c39-110">В этом примере показано, как создать конвейер ветвления на основе путей запросов или других данных запроса, таких как заголовки.</span><span class="sxs-lookup"><span data-stu-id="a2c39-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="a2c39-111">Эти компоненты доступны в пакете NuGet Microsoft. Owin. mapping.</span><span class="sxs-lookup"><span data-stu-id="a2c39-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="a2c39-112">**Пользовательский пример** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) сервера </span><span class="sxs-lookup"><span data-stu-id="a2c39-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="a2c39-113">Показывает, как использовать пользовательский сервер OWIN при размещении OWIN.</span><span class="sxs-lookup"><span data-stu-id="a2c39-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="a2c39-114">**Внедренный пример** [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded) | </span><span class="sxs-lookup"><span data-stu-id="a2c39-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="a2c39-115">Некоторые серверы OWIN можно запускать в собственном процессе (&quot;локально размещенном&quot;).</span><span class="sxs-lookup"><span data-stu-id="a2c39-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="a2c39-116">В этом примере показано, как запустить приложение OWIN с помощью средств, предоставляемых пакетом NuGet Microsoft. Owin. Hosting.</span><span class="sxs-lookup"><span data-stu-id="a2c39-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="a2c39-117">**HelloWorld** . пример [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld) | </span><span class="sxs-lookup"><span data-stu-id="a2c39-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="a2c39-118">OWIN — это абстракция API HTTP-сервера, обеспечивающая переносимость приложений на различных серверах.</span><span class="sxs-lookup"><span data-stu-id="a2c39-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="a2c39-119">В этом образце показано, как написать приложение Hello World с помощью **простых оболочек** , связанных с необработанной абстракцией OWIN, и запустить ее на веб-сервере, например ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a2c39-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="a2c39-120">**Hello World необработанного примера** [ИСХОДНОГО кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin) | OWIN</span><span class="sxs-lookup"><span data-stu-id="a2c39-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="a2c39-121">В этом примере показано, как написать приложение Hello World с помощью **необработанной** абстракции OWIN и запустить его на веб-сервере, например ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a2c39-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="a2c39-122">**Пример** [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR) SignalR | </span><span class="sxs-lookup"><span data-stu-id="a2c39-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="a2c39-123">Показывает, как самостоятельно размещать SignalR с помощью OWIN/Katana.</span><span class="sxs-lookup"><span data-stu-id="a2c39-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="a2c39-124">Дополнительные сведения о самостоятельном размещении SignalR см. в разделе [учебник. Саморазмещение SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="a2c39-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="a2c39-125">**Статический файл пример** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="a2c39-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="a2c39-126">Показывает, как поддерживать HTTP-запросы для статических файлов с помощью OWIN/Katana.</span><span class="sxs-lookup"><span data-stu-id="a2c39-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="a2c39-127">[Исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) | **веб-API** </span><span class="sxs-lookup"><span data-stu-id="a2c39-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="a2c39-128">В этом примере показано, как разместить OWIN в IIS и добавить веб-API в конвейер OWIN.</span><span class="sxs-lookup"><span data-stu-id="a2c39-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="a2c39-129">Пример [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) **веб-сокета** |  </span><span class="sxs-lookup"><span data-stu-id="a2c39-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="a2c39-130">Показывает, как поддерживать веб-сокеты в OWIN с помощью класса [System .NET. WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) .</span><span class="sxs-lookup"><span data-stu-id="a2c39-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
