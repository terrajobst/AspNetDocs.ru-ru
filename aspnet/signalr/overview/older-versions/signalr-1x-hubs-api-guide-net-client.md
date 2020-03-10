---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: Путеводитель по API концентраторов SignalR ASP.NET — клиент .NET (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: В этом документе приводятся общие сведения об использовании API концентраторов для SignalR версии 2 в клиентах .NET, таких как Магазин Windows (WinRT), WPF, Silverlight и недостатки...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 2b22b53c405a865f91b04e677f60b82dd46dbf9b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505974"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a><span data-ttu-id="77c32-103">Путеводитель по API концентраторов SignalR ASP.NET — клиент .NET (SignalR 1. x)</span><span class="sxs-lookup"><span data-stu-id="77c32-103">ASP.NET SignalR Hubs API Guide - .NET Client (SignalR 1.x)</span></span>

<span data-ttu-id="77c32-104">[Патрик Флетчера](https://github.com/pfletcher), [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="77c32-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="77c32-105">В этом документе содержатся общие сведения об использовании API концентраторов для SignalR версии 2 в клиентах .NET, таких как Магазин Windows (WinRT), WPF, Silverlight и консольные приложения.</span><span class="sxs-lookup"><span data-stu-id="77c32-105">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
> 
> <span data-ttu-id="77c32-106">API концентраторов SignalR позволяет выполнять удаленные вызовы процедур (RPC) с сервера на подключенные клиенты и с клиентов на сервер.</span><span class="sxs-lookup"><span data-stu-id="77c32-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="77c32-107">В серверном коде определяются методы, которые могут вызываться клиентами, и вызываются методы, которые выполняются на клиенте.</span><span class="sxs-lookup"><span data-stu-id="77c32-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="77c32-108">В клиентском коде определяются методы, которые могут быть вызваны с сервера, а также вызываются методы, которые выполняются на сервере.</span><span class="sxs-lookup"><span data-stu-id="77c32-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="77c32-109">Этот механизм отвечает за все клиентские коммуникации.</span><span class="sxs-lookup"><span data-stu-id="77c32-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="77c32-110">SignalR также предлагает интерфейс API более низкого уровня, называемый постоянными подключениями.</span><span class="sxs-lookup"><span data-stu-id="77c32-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="77c32-111">Общие сведения о SignalR, концентраторах и постоянных подключениях, а также руководство, в котором показано, как создать полноценное приложение SignalR, см. в разделе [SignalR-начало работы](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="77c32-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="77c32-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="77c32-112">Overview</span></span>

<span data-ttu-id="77c32-113">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="77c32-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="77c32-114">Установка клиента</span><span class="sxs-lookup"><span data-stu-id="77c32-114">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="77c32-115">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="77c32-115">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="77c32-116">Междоменные соединения от клиентов Silverlight</span><span class="sxs-lookup"><span data-stu-id="77c32-116">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="77c32-117">Настройка подключения</span><span class="sxs-lookup"><span data-stu-id="77c32-117">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="77c32-118">Установка максимального числа одновременных подключений в клиентах WPF</span><span class="sxs-lookup"><span data-stu-id="77c32-118">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="77c32-119">Указание параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="77c32-119">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="77c32-120">Как указать метод перевозки</span><span class="sxs-lookup"><span data-stu-id="77c32-120">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="77c32-121">Как указать заголовки HTTP</span><span class="sxs-lookup"><span data-stu-id="77c32-121">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="77c32-122">Как указать сертификаты клиента</span><span class="sxs-lookup"><span data-stu-id="77c32-122">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="77c32-123">Создание прокси-сервера концентратора</span><span class="sxs-lookup"><span data-stu-id="77c32-123">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="77c32-124">Определение методов на клиенте, который может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="77c32-124">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="77c32-125">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-125">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="77c32-126">Методы с параметрами, указание типов параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-126">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="77c32-127">Методы с параметрами, указание динамических объектов для параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-127">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="77c32-128">Удаление обработчика</span><span class="sxs-lookup"><span data-stu-id="77c32-128">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="77c32-129">Вызов методов сервера из клиента</span><span class="sxs-lookup"><span data-stu-id="77c32-129">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="77c32-130">Как работать с событиями времени жизни соединения</span><span class="sxs-lookup"><span data-stu-id="77c32-130">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="77c32-131">Как обрабатывались ошибки</span><span class="sxs-lookup"><span data-stu-id="77c32-131">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="77c32-132">Как включить ведение журнала на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="77c32-132">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="77c32-133">Примеры кода приложений WPF, Silverlight и консольного приложения для клиентских методов, которые может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="77c32-133">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="77c32-134">Примеры клиентских проектов .NET см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="77c32-134">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="77c32-135">[Густаво-Армента/SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) на GitHub.com (WinRT, Silverlight, примеры консольного приложения).</span><span class="sxs-lookup"><span data-stu-id="77c32-135">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="77c32-136">[Дамианедвардс/SignalR-мовешапедемо/мовешапе. Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) на GitHub.com (пример с WPF).</span><span class="sxs-lookup"><span data-stu-id="77c32-136">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="77c32-137">[SignalR/Microsoft. AspNet. SignalR. Client. Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (пример консольного приложения).</span><span class="sxs-lookup"><span data-stu-id="77c32-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="77c32-138">Документацию по программированию клиентов сервера или JavaScript см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="77c32-138">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="77c32-139">Путеводитель по API концентраторов SignalR — сервер</span><span class="sxs-lookup"><span data-stu-id="77c32-139">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="77c32-140">Путеводитель по API концентраторов SignalR — клиент JavaScript</span><span class="sxs-lookup"><span data-stu-id="77c32-140">SignalR Hubs API Guide - JavaScript Client</span></span>](../guide-to-the-api/hubs-api-guide-javascript-client.md)

<span data-ttu-id="77c32-141">Ссылки на справочные статьи по API относятся к версии .NET 4,5 API.</span><span class="sxs-lookup"><span data-stu-id="77c32-141">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="77c32-142">Если вы используете .NET 4, см. [статьи с описанием API для .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="77c32-142">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="77c32-143">Настройка клиента</span><span class="sxs-lookup"><span data-stu-id="77c32-143">Client setup</span></span>

<span data-ttu-id="77c32-144">Установите пакет NuGet [Microsoft. ASPNET. SignalR. Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) (не пакет [Microsoft. ASPNET. SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) ).</span><span class="sxs-lookup"><span data-stu-id="77c32-144">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="77c32-145">Этот пакет поддерживает клиентские приложения WinRT, Silverlight, WPF, консольное приложение и Windows Phone для .NET 4 и .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="77c32-145">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="77c32-146">Если версия SignalR, установленная на клиенте, отличается от версии на сервере, то SignalR часто может адаптироваться к разнице.</span><span class="sxs-lookup"><span data-stu-id="77c32-146">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="77c32-147">Например, когда выдается SignalR версии 2,0 и устанавливается на сервере, сервер будет поддерживать клиенты, на которых установлен выпуск 1.1. x, а также клиенты, на которых установлено 2,0.</span><span class="sxs-lookup"><span data-stu-id="77c32-147">For example, when SignalR version 2.0 is released and you install that on the server, the server will support clients that have 1.1.x installed as well as clients that have 2.0 installed.</span></span> <span data-ttu-id="77c32-148">Если разница между версией на сервере и версией на клиенте слишком велика, SignalR вызывает исключение `InvalidOperationException`, когда клиент пытается установить соединение.</span><span class="sxs-lookup"><span data-stu-id="77c32-148">If the difference between the version on the server and the version on the client is too great, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="77c32-149">Сообщение об ошибке: "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span><span class="sxs-lookup"><span data-stu-id="77c32-149">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="77c32-150">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="77c32-150">How to establish a connection</span></span>

<span data-ttu-id="77c32-151">Прежде чем установить соединение, необходимо создать объект `HubConnection` и создать прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="77c32-151">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="77c32-152">Чтобы установить соединение, вызовите метод `Start` для объекта `HubConnection`.</span><span class="sxs-lookup"><span data-stu-id="77c32-152">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="77c32-153">Для клиентов JavaScript необходимо зарегистрировать по крайней мере один обработчик событий перед вызовом метода `Start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="77c32-153">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="77c32-154">Это не является обязательным для клиентов .NET.</span><span class="sxs-lookup"><span data-stu-id="77c32-154">This is not necessary for .NET clients.</span></span> <span data-ttu-id="77c32-155">Для клиентов JavaScript созданный код прокси автоматически создает учетные записи-посредники для всех концентраторов, существующих на сервере, и регистрирует обработчик, чтобы указать, какие концентраторы клиент планирует использовать.</span><span class="sxs-lookup"><span data-stu-id="77c32-155">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="77c32-156">Но для клиента .NET вы создаете прокси-серверы концентратора вручную, поэтому SignalR предполагает, что вы будете использовать любой центр, для которого создается прокси.</span><span class="sxs-lookup"><span data-stu-id="77c32-156">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="77c32-157">В примере кода для подключения к службе SignalR используется URL-адрес по умолчанию "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="77c32-157">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="77c32-158">Сведения о том, как указать другой базовый URL-адрес, см. [в разделе ASP.NET SignalR Hub API Guide-Server-URL-адрес/SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="77c32-158">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="77c32-159">Метод `Start` выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="77c32-159">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="77c32-160">Чтобы следующие строки кода не выполнялись до тех пор, пока соединение не будет установлено, используйте `await` в асинхронном методе ASP.NET 4,5 или `.Wait()` в синхронном методе.</span><span class="sxs-lookup"><span data-stu-id="77c32-160">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="77c32-161">Не используйте `.Wait()` в клиенте WinRT.</span><span class="sxs-lookup"><span data-stu-id="77c32-161">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<span data-ttu-id="77c32-162">Класс `HubConnection` является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="77c32-162">The `HubConnection` class is thread-safe.</span></span>

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="77c32-163">Междоменные соединения от клиентов Silverlight</span><span class="sxs-lookup"><span data-stu-id="77c32-163">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="77c32-164">Сведения о том, как включить междоменные подключения от клиентов Silverlight, см. в разделе [обеспечение доступности службы через границы домена](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="77c32-164">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="77c32-165">Настройка подключения</span><span class="sxs-lookup"><span data-stu-id="77c32-165">How to configure the connection</span></span>

<span data-ttu-id="77c32-166">Прежде чем устанавливать соединение, можно указать любой из следующих параметров.</span><span class="sxs-lookup"><span data-stu-id="77c32-166">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="77c32-167">Ограничение количества одновременных подключений.</span><span class="sxs-lookup"><span data-stu-id="77c32-167">Concurrent connections limit.</span></span>
- <span data-ttu-id="77c32-168">Параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="77c32-168">Query string parameters.</span></span>
- <span data-ttu-id="77c32-169">Метод перевозки.</span><span class="sxs-lookup"><span data-stu-id="77c32-169">The transport method.</span></span>
- <span data-ttu-id="77c32-170">Заголовки HTTP.</span><span class="sxs-lookup"><span data-stu-id="77c32-170">HTTP headers.</span></span>
- <span data-ttu-id="77c32-171">Сертификаты клиента.</span><span class="sxs-lookup"><span data-stu-id="77c32-171">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="77c32-172">Установка максимального числа одновременных подключений в клиентах WPF</span><span class="sxs-lookup"><span data-stu-id="77c32-172">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="77c32-173">В клиентах WPF может потребоваться увеличить максимальное число одновременных подключений со значением по умолчанию 2.</span><span class="sxs-lookup"><span data-stu-id="77c32-173">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="77c32-174">Рекомендуемое значение — 10.</span><span class="sxs-lookup"><span data-stu-id="77c32-174">The recommended value is 10.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="77c32-175">Дополнительные сведения см. в разделе [ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="77c32-175">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="77c32-176">Указание параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="77c32-176">How to specify query string parameters</span></span>

<span data-ttu-id="77c32-177">Если требуется отправлять данные на сервер при подключении клиента, можно добавить параметры строки запроса в объект соединения.</span><span class="sxs-lookup"><span data-stu-id="77c32-177">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="77c32-178">В следующем примере показано, как задать параметр строки запроса в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="77c32-178">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="77c32-179">В следующем примере показано, как считать параметр строки запроса в серверном коде.</span><span class="sxs-lookup"><span data-stu-id="77c32-179">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="77c32-180">Как указать метод перевозки</span><span class="sxs-lookup"><span data-stu-id="77c32-180">How to specify the transport method</span></span>

<span data-ttu-id="77c32-181">В рамках процесса подключения клиент SignalR обычно согласовывается с сервером для определения наилучшего транспорта, поддерживаемого как сервером, так и клиентом.</span><span class="sxs-lookup"><span data-stu-id="77c32-181">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="77c32-182">Если вы уже уверены, какой транспорт вы хотите использовать, можно обойти этот процесс согласования.</span><span class="sxs-lookup"><span data-stu-id="77c32-182">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="77c32-183">Чтобы указать транспортный метод, передайте объект транспорта в метод Start.</span><span class="sxs-lookup"><span data-stu-id="77c32-183">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="77c32-184">В следующем примере показано, как указать метод перевозки в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="77c32-184">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="77c32-185">Пространство имен [Microsoft. AspNet. SignalR. Client.](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) Transports содержит следующие классы, которые можно использовать для указания транспорта.</span><span class="sxs-lookup"><span data-stu-id="77c32-185">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="77c32-186">[лонгполлингтранспорт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="77c32-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="77c32-187">[серверсентевентстранспорт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="77c32-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="77c32-188">[Вебсоккеттранспорт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (доступно, только если сервер и клиент используют .NET 4,5).</span><span class="sxs-lookup"><span data-stu-id="77c32-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="77c32-189">[Автотранспортировка](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (автоматически выбирает лучший транспорт, который поддерживается как клиентом, так и сервером.</span><span class="sxs-lookup"><span data-stu-id="77c32-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="77c32-190">Это транспорт по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="77c32-190">This is the default transport.</span></span> <span data-ttu-id="77c32-191">Передача этого метода в метод `Start` имеет тот же результат, что и не передает ничего.)</span><span class="sxs-lookup"><span data-stu-id="77c32-191">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="77c32-192">Транспорт Фореверфраме не включен в этот список, так как он используется только браузерами.</span><span class="sxs-lookup"><span data-stu-id="77c32-192">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="77c32-193">Сведения о том, как проверить транспортный метод в коде сервера, см. в разделе [ASP.NET SignalR Hub API Guide-Server-как получить сведения о клиенте из свойства Context](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="77c32-193">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="77c32-194">Дополнительные сведения о транспортировках и резервных запасах см. [в статье Введение в SignalR-транспорты и резервные стратегии](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="77c32-194">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="77c32-195">Как указать заголовки HTTP</span><span class="sxs-lookup"><span data-stu-id="77c32-195">How to specify HTTP headers</span></span>

<span data-ttu-id="77c32-196">Чтобы задать заголовки HTTP, используйте свойство `Headers` объекта Connection.</span><span class="sxs-lookup"><span data-stu-id="77c32-196">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="77c32-197">В следующем примере показано, как добавить заголовок HTTP.</span><span class="sxs-lookup"><span data-stu-id="77c32-197">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="77c32-198">Как указать сертификаты клиента</span><span class="sxs-lookup"><span data-stu-id="77c32-198">How to specify client certificates</span></span>

<span data-ttu-id="77c32-199">Чтобы добавить сертификаты клиента, используйте метод `AddClientCertificate` объекта Connection.</span><span class="sxs-lookup"><span data-stu-id="77c32-199">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="77c32-200">Создание прокси-сервера концентратора</span><span class="sxs-lookup"><span data-stu-id="77c32-200">How to create the Hub proxy</span></span>

<span data-ttu-id="77c32-201">Чтобы определить методы на клиенте, которые концентратор может вызывать с сервера, и вызывать методы в концентраторе на сервере, создайте прокси-сервер для концентратора, вызвав `CreateHubProxy` для объекта Connection.</span><span class="sxs-lookup"><span data-stu-id="77c32-201">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="77c32-202">Строка, которую вы передаете `CreateHubProxy`, является именем класса концентратора или именем, заданным атрибутом `HubName`, если он использовался на сервере.</span><span class="sxs-lookup"><span data-stu-id="77c32-202">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="77c32-203">Сопоставление имен не зависит от регистра.</span><span class="sxs-lookup"><span data-stu-id="77c32-203">Name matching is case-insensitive.</span></span>

<span data-ttu-id="77c32-204">**Класс Hub на сервере**</span><span class="sxs-lookup"><span data-stu-id="77c32-204">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="77c32-205">**Создание прокси клиента для класса HUB**</span><span class="sxs-lookup"><span data-stu-id="77c32-205">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="77c32-206">Если класс Hub дополнить атрибутом `HubName`, используйте это имя.</span><span class="sxs-lookup"><span data-stu-id="77c32-206">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="77c32-207">**Класс Hub на сервере**</span><span class="sxs-lookup"><span data-stu-id="77c32-207">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="77c32-208">**Создание прокси клиента для класса HUB**</span><span class="sxs-lookup"><span data-stu-id="77c32-208">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="77c32-209">Прокси-объект является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="77c32-209">The proxy object is thread-safe.</span></span> <span data-ttu-id="77c32-210">На самом деле, если вы вызываете `HubConnection.CreateHubProxy` несколько раз с одним и тем же `hubName`, вы получаете один кэшированный объект `IHubProxy`.</span><span class="sxs-lookup"><span data-stu-id="77c32-210">In fact, if you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="77c32-211">Определение методов на клиенте, который может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="77c32-211">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="77c32-212">Чтобы определить метод, который может вызвать сервер, используйте метод `On` прокси-сервера для регистрации обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="77c32-212">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="77c32-213">Сопоставление имен методов не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="77c32-213">Method name matching is case-insensitive.</span></span> <span data-ttu-id="77c32-214">Например, `Clients.All.UpdateStockPrice` на сервере будет выполнять `updateStockPrice`, `updatestockprice`или `UpdateStockPrice` на клиенте.</span><span class="sxs-lookup"><span data-stu-id="77c32-214">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="77c32-215">Разные клиентские платформы имеют разные требования к написанию кода метода для обновления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="77c32-215">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="77c32-216">Приведенные примеры предназначены для клиентов WinRT (Windows Store .NET).</span><span class="sxs-lookup"><span data-stu-id="77c32-216">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="77c32-217">Примеры приложений WPF, Silverlight и консольного приложения приведены в [отдельном разделе далее в этом разделе](#wpfsl).</span><span class="sxs-lookup"><span data-stu-id="77c32-217">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="77c32-218">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-218">Methods without parameters</span></span>

<span data-ttu-id="77c32-219">Если обрабатываемый метод не имеет параметров, используйте неуниверсальную перегрузку метода `On`:</span><span class="sxs-lookup"><span data-stu-id="77c32-219">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="77c32-220">**Код сервера, вызывающий клиентский метод без параметров**</span><span class="sxs-lookup"><span data-stu-id="77c32-220">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="77c32-221">**Клиентский код WinRT для метода, вызываемого с сервера без параметров ([см. примеры WPF и Silverlight далее в этом разделе](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="77c32-221">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="77c32-222">Методы с параметрами, указание типов параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-222">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="77c32-223">Если обрабатываемый метод имеет параметры, укажите типы параметров в качестве универсальных типов метода `On`.</span><span class="sxs-lookup"><span data-stu-id="77c32-223">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="77c32-224">Существуют универсальные перегрузки метода `On`, позволяющие указать до 8 параметров (4 в Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="77c32-224">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="77c32-225">В следующем примере один параметр отправляется в метод `UpdateStockPrice`.</span><span class="sxs-lookup"><span data-stu-id="77c32-225">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="77c32-226">**Серверный код, вызывающий клиентский метод с параметром**</span><span class="sxs-lookup"><span data-stu-id="77c32-226">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="77c32-227">**Класс акции, используемый для параметра**</span><span class="sxs-lookup"><span data-stu-id="77c32-227">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="77c32-228">**Клиентский код WinRT для метода, вызываемого с сервера с параметром ([см. примеры WPF и Silverlight далее в этом разделе](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="77c32-228">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="77c32-229">Методы с параметрами, указание динамических объектов для параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-229">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="77c32-230">В качестве альтернативы указанию параметров в качестве универсальных типов метода `On` можно указать параметры как динамические объекты:</span><span class="sxs-lookup"><span data-stu-id="77c32-230">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="77c32-231">**Серверный код, вызывающий клиентский метод с параметром**</span><span class="sxs-lookup"><span data-stu-id="77c32-231">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="77c32-232">**Класс акции, используемый для параметра**</span><span class="sxs-lookup"><span data-stu-id="77c32-232">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="77c32-233">**Клиентский код WinRT для метода, вызываемого с сервера с параметром, с использованием динамического объекта для параметра ([см. примеры WPF и Silverlight далее в этом разделе](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="77c32-233">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="77c32-234">Удаление обработчика</span><span class="sxs-lookup"><span data-stu-id="77c32-234">How to remove a handler</span></span>

<span data-ttu-id="77c32-235">Чтобы удалить обработчик, вызовите его метод `Dispose`.</span><span class="sxs-lookup"><span data-stu-id="77c32-235">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="77c32-236">**Клиентский код для метода, вызываемого с сервера**</span><span class="sxs-lookup"><span data-stu-id="77c32-236">**Client code for a method called from server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="77c32-237">**Код клиента для удаления обработчика**</span><span class="sxs-lookup"><span data-stu-id="77c32-237">**Client code to remove the handler**</span></span>

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="77c32-238">Вызов методов сервера из клиента</span><span class="sxs-lookup"><span data-stu-id="77c32-238">How to call server methods from the client</span></span>

<span data-ttu-id="77c32-239">Чтобы вызвать метод на сервере, используйте метод `Invoke` для прокси-сервера концентратора.</span><span class="sxs-lookup"><span data-stu-id="77c32-239">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="77c32-240">Если метод сервера не имеет возвращаемого значения, используйте неуниверсальную перегрузку метода `Invoke`.</span><span class="sxs-lookup"><span data-stu-id="77c32-240">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="77c32-241">**Серверный код для метода, не имеющего возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="77c32-241">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="77c32-242">**Клиентский код, вызывающий метод, не имеющий возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="77c32-242">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="77c32-243">Если метод сервера имеет возвращаемое значение, укажите тип возвращаемого значения в качестве универсального типа метода `Invoke`.</span><span class="sxs-lookup"><span data-stu-id="77c32-243">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="77c32-244">**Серверный код для метода, который имеет возвращаемое значение и принимает параметр сложного типа**</span><span class="sxs-lookup"><span data-stu-id="77c32-244">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="77c32-245">**Класс акции, используемый для параметра и возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="77c32-245">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="77c32-246">**Клиентский код, вызывающий метод с возвращаемым значением и принимающий параметр сложного типа в асинхронном методе ASP.NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="77c32-246">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="77c32-247">**Клиентский код, вызывающий метод с возвращаемым значением и принимающий параметр сложного типа в синхронном методе**</span><span class="sxs-lookup"><span data-stu-id="77c32-247">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="77c32-248">Метод `Invoke` выполняется асинхронно и возвращает объект `Task`.</span><span class="sxs-lookup"><span data-stu-id="77c32-248">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="77c32-249">Если не указать `await` или `.Wait()`, следующая строка кода будет выполняться до завершения выполнения метода, который вызывается.</span><span class="sxs-lookup"><span data-stu-id="77c32-249">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="77c32-250">Как работать с событиями времени жизни соединения</span><span class="sxs-lookup"><span data-stu-id="77c32-250">How to handle connection lifetime events</span></span>

<span data-ttu-id="77c32-251">SignalR предоставляет следующие события времени жизни подключения, которые можно выполнять:</span><span class="sxs-lookup"><span data-stu-id="77c32-251">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="77c32-252">`Received`: возникает, когда в соединении получены какие-либо данные.</span><span class="sxs-lookup"><span data-stu-id="77c32-252">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="77c32-253">Предоставляет полученные данные.</span><span class="sxs-lookup"><span data-stu-id="77c32-253">Provides the received data.</span></span>
- <span data-ttu-id="77c32-254">`ConnectionSlow`: возникает, когда клиент обнаруживает слишком большое или частое удаление соединения.</span><span class="sxs-lookup"><span data-stu-id="77c32-254">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="77c32-255">`Reconnecting`: возникает, когда начинается повторное подключение базового транспорта.</span><span class="sxs-lookup"><span data-stu-id="77c32-255">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="77c32-256">`Reconnected`: возникает при повторном подключении базового транспорта.</span><span class="sxs-lookup"><span data-stu-id="77c32-256">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="77c32-257">`StateChanged`: возникает при изменении состояния соединения.</span><span class="sxs-lookup"><span data-stu-id="77c32-257">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="77c32-258">Предоставляет старое состояние и новое состояние.</span><span class="sxs-lookup"><span data-stu-id="77c32-258">Provides the old state and the new state.</span></span> <span data-ttu-id="77c32-259">Сведения о значениях состояния соединения см. в разделе [перечисление ConnectionState](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="77c32-259">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="77c32-260">`Closed`: возникает при отключении соединения.</span><span class="sxs-lookup"><span data-stu-id="77c32-260">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="77c32-261">Например, если требуется отображать предупреждающие сообщения об ошибках, которые не являются критическими, но вызывают периодически возникающих проблем с подключением, например медленная работа или частым удалением соединения, обработайте событие `ConnectionSlow`.</span><span class="sxs-lookup"><span data-stu-id="77c32-261">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="77c32-262">Дополнительные сведения см. [в разделе Основные сведения и обработка событий времени жизни подключения в SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="77c32-262">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="77c32-263">Как обрабатывались ошибки</span><span class="sxs-lookup"><span data-stu-id="77c32-263">How to handle errors</span></span>

<span data-ttu-id="77c32-264">Если на сервере явно не включены подробные сообщения об ошибках, то объект исключения, возвращаемый SignalR после ошибки, содержит минимальные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="77c32-264">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="77c32-265">Например, если вызов `newContosoChatMessage` завершается ошибкой, сообщение об ошибке в объекте Error содержит "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Отправка подробных сообщений об ошибках клиентам в рабочей среде не рекомендуется по соображениям безопасности, но если вы хотите включить подробные сообщения об ошибках для устранения неполадок, используйте следующий код на сервере.</span><span class="sxs-lookup"><span data-stu-id="77c32-265">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="77c32-266">Для обработки ошибок, вызванных SignalR, можно добавить обработчик для события `Error` в объекте Connection.</span><span class="sxs-lookup"><span data-stu-id="77c32-266">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="77c32-267">Чтобы обрабатывались ошибки вызовов методов, заключите код в блок try-catch.</span><span class="sxs-lookup"><span data-stu-id="77c32-267">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="77c32-268">Как включить ведение журнала на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="77c32-268">How to enable client-side logging</span></span>

<span data-ttu-id="77c32-269">Чтобы включить ведение журнала на стороне клиента, задайте свойства `TraceLevel` и `TraceWriter` объекта соединения.</span><span class="sxs-lookup"><span data-stu-id="77c32-269">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="77c32-270">Примеры кода приложений WPF, Silverlight и консольного приложения для клиентских методов, которые может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="77c32-270">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="77c32-271">Примеры кода, показанные выше, для определения клиентских методов, которые сервер может вызывать для клиентов WinRT.</span><span class="sxs-lookup"><span data-stu-id="77c32-271">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="77c32-272">В следующих примерах показан эквивалентный код для клиентов WPF, Silverlight и консольных приложений.</span><span class="sxs-lookup"><span data-stu-id="77c32-272">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="77c32-273">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-273">Methods without parameters</span></span>

<span data-ttu-id="77c32-274">**Клиентский код WPF для метода, вызываемого с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="77c32-274">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="77c32-275">**Клиентский код Silverlight для метода, вызываемого с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="77c32-275">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="77c32-276">**Код клиента консольного приложения для метода, вызываемого с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="77c32-276">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="77c32-277">Методы с параметрами, указание типов параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-277">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="77c32-278">**Клиентский код WPF для метода, вызываемого с сервера с параметром**</span><span class="sxs-lookup"><span data-stu-id="77c32-278">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="77c32-279">**Клиентский код Silverlight для метода, вызываемого с сервера с параметром**</span><span class="sxs-lookup"><span data-stu-id="77c32-279">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="77c32-280">**Код клиента консольного приложения для метода, вызываемого с сервера с параметром**</span><span class="sxs-lookup"><span data-stu-id="77c32-280">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="77c32-281">Методы с параметрами, указание динамических объектов для параметров</span><span class="sxs-lookup"><span data-stu-id="77c32-281">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="77c32-282">**Клиентский код WPF для метода, вызываемого с сервера с параметром, с использованием динамического объекта для параметра**</span><span class="sxs-lookup"><span data-stu-id="77c32-282">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="77c32-283">**Клиентский код Silverlight для метода, вызываемого с сервера с параметром, с использованием динамического объекта для параметра**</span><span class="sxs-lookup"><span data-stu-id="77c32-283">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="77c32-284">**Код клиента консольного приложения для метода, вызываемого с сервера с параметром, с использованием динамического объекта для параметра**</span><span class="sxs-lookup"><span data-stu-id="77c32-284">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
