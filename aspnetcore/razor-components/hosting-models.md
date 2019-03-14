---
title: Компоненты Razor, размещения моделей
author: guardrex
description: Сведения о Blazor на стороне клиента и сервера ASP.NET Core Razor компоненты на стороне размещения моделей.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/hosting-models
ms.openlocfilehash: d1e0c472d7d10eeb4cef0da735cf703c98dd1645
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042441"
---
# <a name="razor-components-hosting-models"></a><span data-ttu-id="dba75-103">Компоненты Razor, размещения моделей</span><span class="sxs-lookup"><span data-stu-id="dba75-103">Razor Components hosting models</span></span>

<span data-ttu-id="dba75-104">По [Дэниэл рот](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="dba75-104">By [Daniel Roth](https://github.com/danroth27)</span></span>

<span data-ttu-id="dba75-105">Компоненты Razor — это веб-платформа, предназначен для запуска на стороне клиента в браузере в среде выполнения .NET на основе WebAssembly (*Blazor*) или на сервере в ASP.NET Core (*ASP.NET Core Razor компоненты*).</span><span class="sxs-lookup"><span data-stu-id="dba75-105">Razor Components is a web framework designed to run client-side in the browser on a WebAssembly-based .NET runtime (*Blazor*) or server-side in ASP.NET Core (*ASP.NET Core Razor Components*).</span></span> <span data-ttu-id="dba75-106">Независимо от модели размещения модель, приложения и компонента *остаются теми же*.</span><span class="sxs-lookup"><span data-stu-id="dba75-106">Regardless of the hosting model, the app and component models *remain the same*.</span></span> <span data-ttu-id="dba75-107">В этой статье рассматриваются доступные модели размещения.</span><span class="sxs-lookup"><span data-stu-id="dba75-107">This article discusses the available hosting models.</span></span>

## <a name="client-side-hosting-model"></a><span data-ttu-id="dba75-108">Модель размещения на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="dba75-108">Client-side hosting model</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="dba75-109">Основной модели размещения для Blazor — выполнение стороне клиента в браузере.</span><span class="sxs-lookup"><span data-stu-id="dba75-109">The principal hosting model for Blazor is running client-side in the browser.</span></span> <span data-ttu-id="dba75-110">В этой модели Blazor приложение, его зависимости и среды выполнения .NET, загружаются в браузер.</span><span class="sxs-lookup"><span data-stu-id="dba75-110">In this model, the Blazor app, its dependencies, and the .NET runtime are downloaded to the browser.</span></span> <span data-ttu-id="dba75-111">Приложение выполняется непосредственно в потоке пользовательского интерфейса браузера.</span><span class="sxs-lookup"><span data-stu-id="dba75-111">The app is executed directly on the browser UI thread.</span></span> <span data-ttu-id="dba75-112">Все обновления пользовательского интерфейса и обработка событий происходит в одном процессе.</span><span class="sxs-lookup"><span data-stu-id="dba75-112">All UI updates and event handling happens within the same process.</span></span> <span data-ttu-id="dba75-113">Ресурсы приложения можно развернуть в качестве статических файлов с помощью любого веб-сервера является предпочтительным (см. в разделе [узла и развертывать](xref:host-and-deploy/razor-components/index)).</span><span class="sxs-lookup"><span data-stu-id="dba75-113">The app assets can be deployed as static files using whatever web server is preferred (see [Host and deploy](xref:host-and-deploy/razor-components/index)).</span></span>

![Blazor со стороны клиента: Blazor приложение выполняется в потоке пользовательского интерфейса в браузере.](hosting-models/_static/client-side.png)

<span data-ttu-id="dba75-115">Чтобы создать приложение Blazor, используя модель размещения на стороне клиента, используйте **Blazor** или **Blazor (ASP.NET Core с размещением)** шаблоны проектов (`blazor` или `blazorhosted` шаблон при использовании [команды dotnet new](/dotnet/core/tools/dotnet-new) команду в командной строке).</span><span class="sxs-lookup"><span data-stu-id="dba75-115">To create a Blazor app using the client-side hosting model, use the **Blazor** or **Blazor (ASP.NET Core Hosted)** project templates (`blazor` or `blazorhosted` template when using the [dotnet new](/dotnet/core/tools/dotnet-new) command at a command prompt).</span></span> <span data-ttu-id="dba75-116">Включенные *blazor.webassembly.js* дескрипторы сценариев:</span><span class="sxs-lookup"><span data-stu-id="dba75-116">The included *blazor.webassembly.js* script handles:</span></span>

* <span data-ttu-id="dba75-117">Загрузка среды выполнения .NET, приложения и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="dba75-117">Downloading the .NET runtime, the app, and its dependencies.</span></span>
* <span data-ttu-id="dba75-118">Инициализация среды выполнения для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="dba75-118">Initialization of the runtime to run the app.</span></span>

<span data-ttu-id="dba75-119">Модель размещения клиентского обладает рядом преимуществ.</span><span class="sxs-lookup"><span data-stu-id="dba75-119">The client-side hosting model offers several benefits.</span></span> <span data-ttu-id="dba75-120">Blazor на стороне клиента:</span><span class="sxs-lookup"><span data-stu-id="dba75-120">Client-side Blazor:</span></span>

* <span data-ttu-id="dba75-121">Имеет не зависят от .NET на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="dba75-121">Has no .NET server-side dependency.</span></span>
* <span data-ttu-id="dba75-122">Имеет широкие возможности интерактивного пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="dba75-122">Has a rich interactive UI.</span></span>
* <span data-ttu-id="dba75-123">Полностью использует ресурсы клиента и функции.</span><span class="sxs-lookup"><span data-stu-id="dba75-123">Fully leverages client resources and capabilities.</span></span>
* <span data-ttu-id="dba75-124">Разгрузка работать с сервера клиенту.</span><span class="sxs-lookup"><span data-stu-id="dba75-124">Offloads work from the server to the client.</span></span>
* <span data-ttu-id="dba75-125">Поддерживает сценарии автономной работы.</span><span class="sxs-lookup"><span data-stu-id="dba75-125">Supports offline scenarios.</span></span>

<span data-ttu-id="dba75-126">Есть и недостатки, касающиеся размещения на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="dba75-126">There are downsides to client-side hosting.</span></span> <span data-ttu-id="dba75-127">Blazor на стороне клиента:</span><span class="sxs-lookup"><span data-stu-id="dba75-127">Client-side Blazor:</span></span>

* <span data-ttu-id="dba75-128">Ограничивает его возможности браузера.</span><span class="sxs-lookup"><span data-stu-id="dba75-128">Restricts the app to the capabilities of the browser.</span></span>
* <span data-ttu-id="dba75-129">Требуется клиент с поддержкой оборудования и программного обеспечения (например, WebAssembly поддержка).</span><span class="sxs-lookup"><span data-stu-id="dba75-129">Requires capable client hardware and software (for example, WebAssembly support).</span></span>
* <span data-ttu-id="dba75-130">Имеет больший размер загрузки и больше приложений время загрузки.</span><span class="sxs-lookup"><span data-stu-id="dba75-130">Has a larger download size and longer app load time.</span></span>
* <span data-ttu-id="dba75-131">Имеет меньше даже сложные среды выполнения .NET и средства поддержки (например, ограничения поддержки .NET Standard и отладки).</span><span class="sxs-lookup"><span data-stu-id="dba75-131">Has less mature .NET runtime and tooling support (for example, limitations in .NET Standard support and debugging).</span></span>

<span data-ttu-id="dba75-132">Visual Studio включает в себя **Blazor (ASP.NET Core размещенных)** шаблон проекта для создания приложения Blazor, которая выполняется на WebAssembly и размещается на сервере ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="dba75-132">Visual Studio includes the **Blazor (ASP.NET Core hosted)** project template for creating a Blazor app that runs on WebAssembly and is hosted on an ASP.NET Core server.</span></span> <span data-ttu-id="dba75-133">Приложение ASP.NET Core предоставляет Blazor приложение клиентам, но в противном случае — это отдельный процесс.</span><span class="sxs-lookup"><span data-stu-id="dba75-133">The ASP.NET Core app serves the Blazor app to clients but is otherwise a separate process.</span></span> <span data-ttu-id="dba75-134">Blazor клиентского приложения могут взаимодействовать с сервером по сети с помощью вызовов веб-API или подключениями SignalR.</span><span class="sxs-lookup"><span data-stu-id="dba75-134">The client-side Blazor app can interact with the server over the network using Web API calls or SignalR connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dba75-135">Если приложения на стороне клиента Blazor обслуживается приложение ASP.NET Core, размещенное как приложение sub IIS, отключите унаследованный обработчик из модуля ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="dba75-135">If a client-side Blazor app is served by an ASP.NET Core app hosted as an IIS sub-app, disable the inherited ASP.NET Core Module handler.</span></span> <span data-ttu-id="dba75-136">Задать базовый путь приложения в нем Blazor *index.html* файл псевдоним IIS, используемый при настройке дочернего приложения в IIS.</span><span class="sxs-lookup"><span data-stu-id="dba75-136">Set the app base path in the Blazor app's *index.html* file to the IIS alias used when configuring the sub-app in IIS.</span></span>
>
> <span data-ttu-id="dba75-137">Дополнительные сведения см. в разделе [основной путь приложения](xref:host-and-deploy/razor-components/index#app-base-path).</span><span class="sxs-lookup"><span data-stu-id="dba75-137">For more information, see [App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="server-side-hosting-model"></a><span data-ttu-id="dba75-138">Модель размещения на сервере</span><span class="sxs-lookup"><span data-stu-id="dba75-138">Server-side hosting model</span></span>

<span data-ttu-id="dba75-139">В модели размещения ASP.NET Core Razor компонентов на сервере приложение выполняется на сервере в приложение ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="dba75-139">In the ASP.NET Core Razor Components server-side hosting model, the app is executed on the server from within an ASP.NET Core app.</span></span> <span data-ttu-id="dba75-140">Обновление элементов пользовательского интерфейса, обработка событий и вызовы JavaScript обрабатываются через подключение SignalR.</span><span class="sxs-lookup"><span data-stu-id="dba75-140">UI updates, event handling, and JavaScript calls are handled over a SignalR connection.</span></span>

![ASP.NET Core Razor компонентов на сервере: Браузер взаимодействует с приложением (размещенный внутри приложения ASP.NET Core) на сервере подключения SignalR.](hosting-models/_static/server-side.png)

<span data-ttu-id="dba75-142">Чтобы создать приложение Razor компоненты, используя модель размещения на сервере, используйте **Blazor (на сервере в ASP.NET Core)** шаблона (`blazorserver` при использовании [команды dotnet new](/dotnet/core/tools/dotnet-new) в командной строке).</span><span class="sxs-lookup"><span data-stu-id="dba75-142">To create a Razor Components app using the server-side hosting model, use the **Blazor (Server-side in ASP.NET Core)** template (`blazorserver` when using [dotnet new](/dotnet/core/tools/dotnet-new) at a command prompt).</span></span> <span data-ttu-id="dba75-143">Приложения ASP.NET Core размещено приложение на сервере компонентов Razor и задает конечную точку SignalR, где клиенты подключаются.</span><span class="sxs-lookup"><span data-stu-id="dba75-143">An ASP.NET Core app hosts the Razor Components server-side app and sets up the SignalR endpoint where clients connect.</span></span> <span data-ttu-id="dba75-144">Приложение ASP.NET Core ссылается на приложения `Startup` добавляемый класс:</span><span class="sxs-lookup"><span data-stu-id="dba75-144">The ASP.NET Core app references the app's `Startup` class to add:</span></span>

* <span data-ttu-id="dba75-145">Службы компонентов Razor на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="dba75-145">Server-side Razor Components services.</span></span>
* <span data-ttu-id="dba75-146">Приложение, чтобы конвейер обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="dba75-146">The app to the request handling pipeline.</span></span>

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

<span data-ttu-id="dba75-147">*Blazor.server.js* скрипт&dagger; устанавливает соединение с клиентом.</span><span class="sxs-lookup"><span data-stu-id="dba75-147">The *blazor.server.js* script&dagger; establishes the client connection.</span></span> <span data-ttu-id="dba75-148">Это приложение отвечает за сохранение и восстановление состояние приложения при необходимости (например, в случае потери сетевого подключения).</span><span class="sxs-lookup"><span data-stu-id="dba75-148">It's the app's responsibility to persist and restore app state as required (for example, in the event of a lost network connection).</span></span>

<span data-ttu-id="dba75-149">Модель размещения на сервере имеет несколько преимуществ.</span><span class="sxs-lookup"><span data-stu-id="dba75-149">The server-side hosting model offers several benefits:</span></span>

* <span data-ttu-id="dba75-150">Позволяет разработчикам писать приложения целиком, с помощью .NET и C# с помощью модели компонентов.</span><span class="sxs-lookup"><span data-stu-id="dba75-150">Allows you to write your entire app with .NET and C# using the component model.</span></span>
* <span data-ttu-id="dba75-151">Обеспечивает широкие возможности интерактивный пользовательский интерфейс и избежать обновления ненужные страницы.</span><span class="sxs-lookup"><span data-stu-id="dba75-151">Provides a rich interactive feel and avoids unnecessary page refreshes.</span></span>
* <span data-ttu-id="dba75-152">Имеет значительно меньший размер приложения, чем Blazor приложения на стороне клиента и загружается гораздо быстрее.</span><span class="sxs-lookup"><span data-stu-id="dba75-152">Has a significantly smaller app size than a client-side Blazor app and loads much faster.</span></span>
* <span data-ttu-id="dba75-153">Логикой компонента можно использовать все возможности сервера, включая использование любого совместимых API .NET Core.</span><span class="sxs-lookup"><span data-stu-id="dba75-153">Component logic can take full advantage of server capabilities, including using any .NET Core compatible APIs.</span></span>
* <span data-ttu-id="dba75-154">Выполняется на .NET Core на сервере, поэтому существующие .NET, оборудование, например, отладка, работает правильно.</span><span class="sxs-lookup"><span data-stu-id="dba75-154">Runs on .NET Core on the server, so existing .NET tooling, such as debugging, works as expected.</span></span>
* <span data-ttu-id="dba75-155">Работает с тонкие клиенты (например, браузеры, которые не поддерживают WebAssembly и ресурсов ограничение устройств).</span><span class="sxs-lookup"><span data-stu-id="dba75-155">Works with thin clients (for example, browsers that don't support WebAssembly and resource constrained devices).</span></span>

<span data-ttu-id="dba75-156">Есть и недостатки, касающиеся размещения на сервере:</span><span class="sxs-lookup"><span data-stu-id="dba75-156">There are downsides to server-side hosting:</span></span>

* <span data-ttu-id="dba75-157">Имеет большее время задержки: Любое действие пользователя прыжок сети.</span><span class="sxs-lookup"><span data-stu-id="dba75-157">Has higher latency: Every user interaction involves a network hop.</span></span>
* <span data-ttu-id="dba75-158">Предоставляет не поддержку автономной работы. В случае сбоя подключения клиента, приложение перестает работать.</span><span class="sxs-lookup"><span data-stu-id="dba75-158">Offers no offline support: If the client connection fails, the app stops working.</span></span>
* <span data-ttu-id="dba75-159">Обладает уменьшенной масштабируемости: Сервер управления подключениями нескольких клиентов и обработки состояния клиента.</span><span class="sxs-lookup"><span data-stu-id="dba75-159">Has reduced scalability: The server must manage multiple client connections and handle client state.</span></span>
* <span data-ttu-id="dba75-160">Требуется ASP.NET Core сервер для обслуживания приложения.</span><span class="sxs-lookup"><span data-stu-id="dba75-160">Requires an ASP.NET Core server to serve the app.</span></span> <span data-ttu-id="dba75-161">Развертывание без сервера (например, из сети доставки Содержимого) невозможно.</span><span class="sxs-lookup"><span data-stu-id="dba75-161">Deployment without a server (for example, from a CDN) isn't possible.</span></span>

<span data-ttu-id="dba75-162">&dagger;*Blazor.server.js* скрипт публикуется по следующему пути: *bin / {Отладка | Выпуск} / {ЦЕЛЕВОЙ ПЛАТФОРМЫ} /publish/ {имя_приложения}. Приложения/dist/_платформа*.</span><span class="sxs-lookup"><span data-stu-id="dba75-162">&dagger;The *blazor.server.js* script is published to the following path: *bin/{Debug|Release}/{TARGET FRAMEWORK}/publish/{APPLICATION NAME}.App/dist/_framework*.</span></span>
