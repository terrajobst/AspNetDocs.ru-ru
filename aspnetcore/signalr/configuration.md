---
title: Конфигурация ASP.NET Core SignalR
author: bradygaster
description: Сведения о настройке приложения ASP.NET Core SignalR.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 02/07/2019
uid: signalr/configuration
ms.openlocfilehash: f5449a15743c1f38c550fe30945bdc19f069e3f5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038191"
---
# <a name="aspnet-core-signalr-configuration"></a><span data-ttu-id="7d6c0-103">Конфигурация ASP.NET Core SignalR</span><span class="sxs-lookup"><span data-stu-id="7d6c0-103">ASP.NET Core SignalR configuration</span></span>

## <a name="jsonmessagepack-serialization-options"></a><span data-ttu-id="7d6c0-104">Параметры сериализации JSON/MessagePack</span><span class="sxs-lookup"><span data-stu-id="7d6c0-104">JSON/MessagePack serialization options</span></span>

<span data-ttu-id="7d6c0-105">ASP.NET Core SignalR поддерживает два протокола для кодировки сообщений: [JSON](https://www.json.org/) и [MessagePack](https://msgpack.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-105">ASP.NET Core SignalR supports two protocols for encoding messages: [JSON](https://www.json.org/) and [MessagePack](https://msgpack.org/index.html).</span></span> <span data-ttu-id="7d6c0-106">Каждый протокол имеет параметры конфигурации для сериализации.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-106">Each protocol has serialization configuration options.</span></span>

<span data-ttu-id="7d6c0-107">Сериализация JSON можно настроить на сервере, используя [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) метод расширения, которую можно добавить после [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) в вашей `Startup.ConfigureServices` метод.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-107">JSON serialization can be configured on the server using the [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) extension method, which can be added after [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in your `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="7d6c0-108">`AddJsonProtocol` Метод принимает делегат, который получает `options` объекта.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-108">The `AddJsonProtocol` method takes a delegate that receives an `options` object.</span></span> <span data-ttu-id="7d6c0-109">[PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) свойство на этот объект является JSON.NET `JsonSerializerSettings` объект, который может использоваться для настройки сериализации аргументов и возвращаемых значений.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-109">The [PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) property on that object is a JSON.NET `JsonSerializerSettings` object that can be used to configure serialization of arguments and return values.</span></span> <span data-ttu-id="7d6c0-110">См. в разделе [документации по JSON.NET](https://www.newtonsoft.com/json/help/html/Introduction.htm) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-110">See the [JSON.NET Documentation](https://www.newtonsoft.com/json/help/html/Introduction.htm) for more details.</span></span>

<span data-ttu-id="7d6c0-111">Например чтобы настроить сериализатор, используемый имена свойств «PascalCase», а не имена «camelCase» по умолчанию, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-111">As an example, to configure the serializer to use "PascalCase" property names, instead of the default "camelCase" names, use the following code:</span></span>

```csharp
services.AddSignalR()
    .AddJsonProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

<span data-ttu-id="7d6c0-112">В клиента .NET, так же `AddJsonProtocol` метод расширения существует на [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-112">In the .NET client, the same `AddJsonProtocol` extension method exists on [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span></span> <span data-ttu-id="7d6c0-113">`Microsoft.Extensions.DependencyInjection` Пространства имен должны импортироваться разрешить метод расширения:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-113">The `Microsoft.Extensions.DependencyInjection` namespace must be imported to resolve the extension method:</span></span>

```csharp
// At the top of the file:
using Microsoft.Extensions.DependencyInjection;

// When constructing your connection:
var connection = new HubConnectionBuilder()
    .AddJsonProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
            new DefaultContractResolver();
    })
    .Build();
```

> [!NOTE]
> <span data-ttu-id="7d6c0-114">Не поддерживается для настройки сериализации JSON в клиенте JavaScript в данный момент.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-114">It's not possible to configure JSON serialization in the JavaScript client at this time.</span></span>

### <a name="messagepack-serialization-options"></a><span data-ttu-id="7d6c0-115">Параметры сериализации MessagePack</span><span class="sxs-lookup"><span data-stu-id="7d6c0-115">MessagePack serialization options</span></span>

<span data-ttu-id="7d6c0-116">MessagePack сериализации можно настроить, предоставьте делегат для [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) вызова.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-116">MessagePack serialization can be configured by providing a delegate to the [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) call.</span></span> <span data-ttu-id="7d6c0-117">См. в разделе [MessagePack в SignalR](xref:signalr/messagepackhubprotocol) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-117">See [MessagePack in SignalR](xref:signalr/messagepackhubprotocol) for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="7d6c0-118">Не поддерживается для настройки сериализации MessagePack в клиенте JavaScript в данный момент.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-118">It's not possible to configure MessagePack serialization in the JavaScript client at this time.</span></span>

## <a name="configure-server-options"></a><span data-ttu-id="7d6c0-119">Настройка параметров сервера</span><span class="sxs-lookup"><span data-stu-id="7d6c0-119">Configure server options</span></span>

<span data-ttu-id="7d6c0-120">В следующей таблице описаны параметры для настройки концентраторов SignalR:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-120">The following table describes options for configuring SignalR hubs:</span></span>

| <span data-ttu-id="7d6c0-121">Параметр</span><span class="sxs-lookup"><span data-stu-id="7d6c0-121">Option</span></span> | <span data-ttu-id="7d6c0-122">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7d6c0-122">Default Value</span></span> | <span data-ttu-id="7d6c0-123">Описание:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-123">Description</span></span> |
| ------ | ------------- | ----------- |
| `ClientTimeoutInterval` | <span data-ttu-id="7d6c0-124">30 секунд</span><span class="sxs-lookup"><span data-stu-id="7d6c0-124">30 seconds</span></span> | <span data-ttu-id="7d6c0-125">Сервер будет рассматривать клиента отключен, если он еще не получил сообщение (включая keep-alive) в этом интервале.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-125">The server will consider the client disconnected if it hasn't received a message (including keep-alive) in this interval.</span></span> <span data-ttu-id="7d6c0-126">Может занять больше времени, чем этот интервал времени ожидания для клиента, фактически помечается как отключенный, из-за, как это реализовано.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-126">It could take longer than this timeout interval for the client to actually be marked disconnected, due to how this is implemented.</span></span> <span data-ttu-id="7d6c0-127">Рекомендуемое значение — double `KeepAliveInterval` значение.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-127">The recommended value is double the `KeepAliveInterval` value.</span></span>|
| `HandshakeTimeout` | <span data-ttu-id="7d6c0-128">15 секунд</span><span class="sxs-lookup"><span data-stu-id="7d6c0-128">15 seconds</span></span> | <span data-ttu-id="7d6c0-129">Если клиент не отправляет сообщение первоначального подтверждения в течение этого времени интервала, соединение закрывается.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-129">If the client doesn't send an initial handshake message within this time interval, the connection is closed.</span></span> <span data-ttu-id="7d6c0-130">Это расширенный параметр, который может изменяться только если из-за серьезных сетевой задержки происходят ошибки времени ожидания подтверждения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-130">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="7d6c0-131">Подробности, касающиеся процесса подтверждения, см. в разделе [спецификации протокола концентратора SignalR](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-131">For more detail on the handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |
| `KeepAliveInterval` | <span data-ttu-id="7d6c0-132">15 секунд</span><span class="sxs-lookup"><span data-stu-id="7d6c0-132">15 seconds</span></span> | <span data-ttu-id="7d6c0-133">Если сервер не отправил сообщение в течение этого интервала, автоматически отправляется сообщение ping необходимо сохранить открытым подключение.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-133">If the server hasn't sent a message within this interval, a ping message is sent automatically to keep the connection open.</span></span> <span data-ttu-id="7d6c0-134">При изменении `KeepAliveInterval`, изменить `ServerTimeout` / `serverTimeoutInMilliseconds` параметр на клиенте.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-134">When changing `KeepAliveInterval`, change the `ServerTimeout`/`serverTimeoutInMilliseconds` setting on the client.</span></span> <span data-ttu-id="7d6c0-135">Минимальная рекомендуемая `ServerTimeout` / `serverTimeoutInMilliseconds` значение double `KeepAliveInterval` значение.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-135">The recommended `ServerTimeout`/`serverTimeoutInMilliseconds` value is double the `KeepAliveInterval` value.</span></span>  |
| `SupportedProtocols` | <span data-ttu-id="7d6c0-136">Все установленные протоколы</span><span class="sxs-lookup"><span data-stu-id="7d6c0-136">All installed protocols</span></span> | <span data-ttu-id="7d6c0-137">Протоколы, поддерживаемые этого концентратора.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-137">Protocols supported by this hub.</span></span> <span data-ttu-id="7d6c0-138">По умолчанию разрешены все протоколы, которые зарегистрированы на сервере, но протоколы можно удалить из списка, чтобы отключить специальные протоколы для отдельных концентраторов.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-138">By default, all protocols registered on the server are allowed, but protocols can be removed from this list to disable specific protocols for individual hubs.</span></span> |
| `EnableDetailedErrors` | `false` | <span data-ttu-id="7d6c0-139">Если `true`подробные сообщения об исключениях возвращаются клиентам, когда исключение в методе концентратора.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-139">If `true`, detailed exception messages are returned to clients when an exception is thrown in a Hub method.</span></span> <span data-ttu-id="7d6c0-140">По умолчанию используется `false`, как эти сообщения об исключениях могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-140">The default is `false`, as these exception messages can contain sensitive information.</span></span> |

<span data-ttu-id="7d6c0-141">Можно настроить параметры для всех концентраторов, предоставляя делегат параметры для `AddSignalR` вызов в `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-141">Options can be configured for all hubs by providing an options delegate to the `AddSignalR` call in `Startup.ConfigureServices`.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSignalR(hubOptions =>
    {
        hubOptions.EnableDetailedErrors = true;
        hubOptions.KeepAliveInterval = TimeSpan.FromMinutes(1);
    });
}
```

<span data-ttu-id="7d6c0-142">Параметры для одного центра переопределить глобальные параметры, указанные на `AddSignalR` и могут настраиваться с помощью [AddHubOptions\<T >](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span><span class="sxs-lookup"><span data-stu-id="7d6c0-142">Options for a single hub override the global options provided in `AddSignalR` and can be configured using [AddHubOptions\<T>](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span></span>

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
});
```

### <a name="advanced-http-configuration-options"></a><span data-ttu-id="7d6c0-143">Дополнительные параметры конфигурации HTTP</span><span class="sxs-lookup"><span data-stu-id="7d6c0-143">Advanced HTTP configuration options</span></span>

<span data-ttu-id="7d6c0-144">Используйте `HttpConnectionDispatcherOptions` для расширенной настройки, относящиеся к транспортов и управление буфером памяти.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-144">Use `HttpConnectionDispatcherOptions` to configure advanced settings related to transports and memory buffer management.</span></span> <span data-ttu-id="7d6c0-145">Эти параметры настраиваются путем передачи делегата для [MapHub\<T >](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub) в `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-145">These options are configured by passing a delegate to [MapHub\<T>](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub) in `Startup.Configure`.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseSignalR((configure) => 
    {
        var desiredTransports = 
            HttpTransportType.WebSockets |
            HttpTransportType.LongPolling;

        configure.MapHub<MyHub>("/myhub", (options) => 
        {
            options.Transports = desiredTransports;
        });
    });
}
```

<span data-ttu-id="7d6c0-146">В следующей таблице описаны параметры для настройки дополнительных параметров HTTP ASP.NET Core SignalR:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-146">The following table describes options for configuring ASP.NET Core SignalR's advanced HTTP options:</span></span>

| <span data-ttu-id="7d6c0-147">Параметр</span><span class="sxs-lookup"><span data-stu-id="7d6c0-147">Option</span></span> | <span data-ttu-id="7d6c0-148">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7d6c0-148">Default Value</span></span> | <span data-ttu-id="7d6c0-149">Описание:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-149">Description</span></span> |
| ------ | ------------- | ----------- |
| `ApplicationMaxBufferSize` | <span data-ttu-id="7d6c0-150">32 КБ</span><span class="sxs-lookup"><span data-stu-id="7d6c0-150">32 KB</span></span> | <span data-ttu-id="7d6c0-151">Максимальное число байтов, полученных от клиента, буферы сервера.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-151">The maximum number of bytes received from the client that the server buffers.</span></span> <span data-ttu-id="7d6c0-152">Увеличение этого значения позволяет серверу для получения сообщения большего размера, но может отрицательно повлиять на потребление памяти.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-152">Increasing this value allows the server to receive larger messages, but can negatively impact memory consumption.</span></span> |
| `AuthorizationData` | <span data-ttu-id="7d6c0-153">Данные, собранные из автоматически `Authorize` атрибутов, примененных к классу Hub.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-153">Data automatically gathered from the `Authorize` attributes applied to the Hub class.</span></span> | <span data-ttu-id="7d6c0-154">Список [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) объекты, используемые для определения того, если клиенту разрешено подключаться к концентратору.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-154">A list of [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) objects used to determine if a client is authorized to connect to the hub.</span></span> |
| `TransportMaxBufferSize` | <span data-ttu-id="7d6c0-155">32 КБ</span><span class="sxs-lookup"><span data-stu-id="7d6c0-155">32 KB</span></span> | <span data-ttu-id="7d6c0-156">Максимальное число байтов, отправленных в приложение, буферы сервера.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-156">The maximum number of bytes sent by the app that the server buffers.</span></span> <span data-ttu-id="7d6c0-157">Увеличение этого значения позволяет серверу для отправки сообщения большего размера, но может отрицательно повлиять на потребление памяти.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-157">Increasing this value allows the server to send larger messages, but can negatively impact memory consumption.</span></span> |
| `Transports` | <span data-ttu-id="7d6c0-158">Включены все транспорты.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-158">All Transports are enabled.</span></span> | <span data-ttu-id="7d6c0-159">Битовая маска `HttpTransportType` значения, которые можно ограничить транспорты, которые клиент может использовать для подключения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-159">A bitmask of `HttpTransportType` values that can restrict the transports a client can use to connect.</span></span> |
| `LongPolling` | <span data-ttu-id="7d6c0-160">См. ниже.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-160">See below.</span></span> | <span data-ttu-id="7d6c0-161">Дополнительные параметры, характерные для транспорта длинный опрос.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-161">Additional options specific to the Long Polling transport.</span></span> |
| `WebSockets` | <span data-ttu-id="7d6c0-162">См. ниже.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-162">See below.</span></span> | <span data-ttu-id="7d6c0-163">Дополнительные параметры, характерные для транспорта WebSockets.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-163">Additional options specific to the WebSockets transport.</span></span> |

<span data-ttu-id="7d6c0-164">Транспорт длинный опрос имеет дополнительные параметры, которые могут быть настроены с помощью `LongPolling` свойство:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-164">The Long Polling transport has additional options that can be configured using the `LongPolling` property:</span></span>

| <span data-ttu-id="7d6c0-165">Параметр</span><span class="sxs-lookup"><span data-stu-id="7d6c0-165">Option</span></span> | <span data-ttu-id="7d6c0-166">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7d6c0-166">Default Value</span></span> | <span data-ttu-id="7d6c0-167">Описание</span><span class="sxs-lookup"><span data-stu-id="7d6c0-167">Description</span></span> |
| ------ | ------------- | ----------- |
| `PollTimeout` | <span data-ttu-id="7d6c0-168">90 секунд</span><span class="sxs-lookup"><span data-stu-id="7d6c0-168">90 seconds</span></span> | <span data-ttu-id="7d6c0-169">Максимальное время ожидания сервером ответа сообщение, отправляемое клиенту перед завершением работы запрос на единый опроса.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-169">The maximum amount of time the server waits for a message to send to the client before terminating a single poll request.</span></span> <span data-ttu-id="7d6c0-170">Уменьшение этого значения приводит к клиентам выполнять чаще, новые запросы опроса.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-170">Decreasing this value causes the client to issue new poll requests more frequently.</span></span> |

<span data-ttu-id="7d6c0-171">Транспорт WebSocket имеет дополнительные параметры, которые могут быть настроены с помощью `WebSockets` свойство:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-171">The WebSocket transport has additional options that can be configured using the `WebSockets` property:</span></span>

| <span data-ttu-id="7d6c0-172">Параметр</span><span class="sxs-lookup"><span data-stu-id="7d6c0-172">Option</span></span> | <span data-ttu-id="7d6c0-173">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7d6c0-173">Default Value</span></span> | <span data-ttu-id="7d6c0-174">Описание</span><span class="sxs-lookup"><span data-stu-id="7d6c0-174">Description</span></span> |
| ------ | ------------- | ----------- |
| `CloseTimeout` | <span data-ttu-id="7d6c0-175">5 секунд</span><span class="sxs-lookup"><span data-stu-id="7d6c0-175">5 seconds</span></span> | <span data-ttu-id="7d6c0-176">После завершения работы сервера, если клиенту не удается закрыть в течение этого времени интервала, соединение будет разорвано.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-176">After the server closes, if the client fails to close within this time interval, the connection is terminated.</span></span> |
| `SubProtocolSelector` | `null` | <span data-ttu-id="7d6c0-177">Делегат, который может использоваться для задания `Sec-WebSocket-Protocol` заголовок пользовательское значение.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-177">A delegate that can be used to set the `Sec-WebSocket-Protocol` header to a custom value.</span></span> <span data-ttu-id="7d6c0-178">Делегат получает значения, запрошенной клиентом в качестве входных данных и должен возвращать необходимое значение.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-178">The delegate receives the values requested by the client as input and is expected to return the desired value.</span></span> |

## <a name="configure-client-options"></a><span data-ttu-id="7d6c0-179">Настройка параметров клиента</span><span class="sxs-lookup"><span data-stu-id="7d6c0-179">Configure client options</span></span>

<span data-ttu-id="7d6c0-180">Можно настроить параметры клиента на `HubConnectionBuilder` тип (доступна в клиентах .NET и JavaScript), а также в `HubConnection` сам.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-180">Client options can be configured on the `HubConnectionBuilder` type (available in both .NET and JavaScript clients), as well as on the `HubConnection` itself.</span></span>

### <a name="configure-logging"></a><span data-ttu-id="7d6c0-181">Настройка ведения журнала</span><span class="sxs-lookup"><span data-stu-id="7d6c0-181">Configure logging</span></span>

<span data-ttu-id="7d6c0-182">Настроить ведение журнала с помощью клиента .NET `ConfigureLogging` метод.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-182">Logging is configured in the .NET Client using the `ConfigureLogging` method.</span></span> <span data-ttu-id="7d6c0-183">Ведение журнала, поставщики и фильтры могут быть зарегистрированы в так же как при работе на сервере.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-183">Logging providers and filters can be registered in the same way as they are on the server.</span></span> <span data-ttu-id="7d6c0-184">См. в разделе [ведения журналов в ASP.NET Core](xref:fundamentals/logging/index) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-184">See the [Logging in ASP.NET Core](xref:fundamentals/logging/index) documentation for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="7d6c0-185">Чтобы зарегистрировать поставщики ведения журналов, необходимо установить необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-185">In order to register Logging providers, you must install the necessary packages.</span></span> <span data-ttu-id="7d6c0-186">См. в разделе [встроенные поставщики ведения журналов](xref:fundamentals/logging/index#built-in-logging-providers) разделе документы с полным списком.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-186">See the [Built-in logging providers](xref:fundamentals/logging/index#built-in-logging-providers) section of the docs for a full list.</span></span>

<span data-ttu-id="7d6c0-187">Например, чтобы включить ведение журнала консоли, установить `Microsoft.Extensions.Logging.Console` пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-187">For example, to enable Console logging, install the `Microsoft.Extensions.Logging.Console` NuGet package.</span></span> <span data-ttu-id="7d6c0-188">Вызовите `AddConsole` метод расширения:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-188">Call the `AddConsole` extension method:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

<span data-ttu-id="7d6c0-189">В клиенте JavaScript, аналогичное `configureLogging` метод существует.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-189">In the JavaScript client, a similar `configureLogging` method exists.</span></span> <span data-ttu-id="7d6c0-190">Укажите `LogLevel` значение, указывающее минимальный уровень журнала сообщений для получения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-190">Provide a `LogLevel` value indicating the minimum level of log messages to produce.</span></span> <span data-ttu-id="7d6c0-191">Журналы записываются в окно консоли браузера.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-191">Logs are written to the browser console window.</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> <span data-ttu-id="7d6c0-192">Чтобы отключить ведение журнала полностью, укажите `signalR.LogLevel.None` в `configureLogging` метод.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-192">To disable logging entirely, specify `signalR.LogLevel.None` in the `configureLogging` method.</span></span>

<span data-ttu-id="7d6c0-193">Ниже перечислены уровни ведения журнала, доступные для клиента JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-193">Log levels available to the JavaScript client are listed below.</span></span> <span data-ttu-id="7d6c0-194">Установка уровня журнала в одно из следующих значений включает ведение журнала сообщений в **или более поздней версии** этого уровня.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-194">Setting the log level to one of these values enables logging of messages at **or above** that level.</span></span>

| <span data-ttu-id="7d6c0-195">Уровень</span><span class="sxs-lookup"><span data-stu-id="7d6c0-195">Level</span></span> | <span data-ttu-id="7d6c0-196">Описание:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-196">Description</span></span> |
| ----- | ----------- |
| `None` | <span data-ttu-id="7d6c0-197">Сообщения не регистрируются.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-197">No messages are logged.</span></span> |
| `Critical` | <span data-ttu-id="7d6c0-198">Сообщения, которые означают сбой всего приложения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-198">Messages that indicate a failure in the entire app.</span></span> |
| `Error` | <span data-ttu-id="7d6c0-199">Сообщения, которые указывают на сбой в текущей операции.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-199">Messages that indicate a failure in the current operation.</span></span> |
| `Warning` | <span data-ttu-id="7d6c0-200">Сообщения, которые указывают на проблему, не являющиеся неустранимыми.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-200">Messages that indicate a non-fatal problem.</span></span> |
| `Information` | <span data-ttu-id="7d6c0-201">Информационные сообщения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-201">Informational messages.</span></span> |
| `Debug` | <span data-ttu-id="7d6c0-202">Диагностические сообщения, полезны для отладки.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-202">Diagnostic messages useful for debugging.</span></span> |
| `Trace` | <span data-ttu-id="7d6c0-203">Очень подробные диагностические сообщения, предназначены для диагностики конкретных проблем.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-203">Very detailed diagnostic messages designed for diagnosing specific issues.</span></span> |

### <a name="configure-allowed-transports"></a><span data-ttu-id="7d6c0-204">Настройка разрешенных транспортов</span><span class="sxs-lookup"><span data-stu-id="7d6c0-204">Configure allowed transports</span></span>

<span data-ttu-id="7d6c0-205">Можно настроить транспорт, используемый с SignalR в `WithUrl` вызова (`withUrl` в JavaScript).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-205">The transports used by SignalR can be configured in the `WithUrl` call (`withUrl` in JavaScript).</span></span> <span data-ttu-id="7d6c0-206">Побитовое или-значения `HttpTransportType` может использоваться для ограничения клиента на использование только указанного транспорта.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-206">A bitwise-OR of the values of `HttpTransportType` can be used to restrict the client to only use the specified transports.</span></span> <span data-ttu-id="7d6c0-207">Все транспорты включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-207">All transports are enabled by default.</span></span>

<span data-ttu-id="7d6c0-208">Например чтобы отключить события Server-Sent транспорта, но подключений WebSockets и длинный опрос:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-208">For example, to disable the Server-Sent Events transport, but allow WebSockets and Long Polling connections:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

<span data-ttu-id="7d6c0-209">В клиенте JavaScript транспортов настраиваются, задав `transport` на объект параметры, передаваемые `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-209">In the JavaScript client, transports are configured by setting the `transport` field on the options object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a><span data-ttu-id="7d6c0-210">Настройка проверки подлинности носителя</span><span class="sxs-lookup"><span data-stu-id="7d6c0-210">Configure bearer authentication</span></span>

<span data-ttu-id="7d6c0-211">Чтобы указать данные проверки подлинности, а также SignalR запросов, используйте `AccessTokenProvider` параметр (`accessTokenFactory` в JavaScript) для указания функция, которая возвращает маркер необходимый тип доступа.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-211">To provide authentication data along with SignalR requests, use the `AccessTokenProvider` option (`accessTokenFactory` in JavaScript) to specify a function that returns the desired access token.</span></span> <span data-ttu-id="7d6c0-212">В клиенте .NET, этот маркер передается как HTTP «Проверки подлинности носителя» токена (с помощью `Authorization` заголовка с типом `Bearer`).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-212">In the .NET Client, this access token is passed in as an HTTP "Bearer Authentication" token (Using the `Authorization` header with a type of `Bearer`).</span></span> <span data-ttu-id="7d6c0-213">В клиенте JavaScript используется маркер доступа в качестве токена носителя, **за исключением** в некоторых случаях, где обозреватель API-интерфейсы ограничить возможность применения заголовки (в частности, в запросы событий Server-Sent и WebSockets).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-213">In the JavaScript client, the access token is used as a Bearer token, **except** in a few cases where browser APIs restrict the ability to apply headers (specifically, in Server-Sent Events and WebSockets requests).</span></span> <span data-ttu-id="7d6c0-214">В этих случаях маркер доступа предоставляется как значение строки запроса `access_token`.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-214">In these cases, the access token is provided as a query string value `access_token`.</span></span>

<span data-ttu-id="7d6c0-215">В клиенте .NET `AccessTokenProvider` параметр может быть указан с помощью делегата параметры в `WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-215">In the .NET client, the `AccessTokenProvider` option can be specified using the options delegate in `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        };
    })
    .Build();
```

<span data-ttu-id="7d6c0-216">В клиенте JavaScript настроен маркер доступа, задав `accessTokenFactory` на объект параметров в `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-216">In the JavaScript client, the access token is configured by setting the `accessTokenFactory` field on the options object in `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        accessTokenFactory: () => {
            // Get and return the access token.
            // This function can return a JavaScript Promise if asynchronous
            // logic is required to retrieve the access token.
        }
    })
    .build();
```

### <a name="configure-timeout-and-keep-alive-options"></a><span data-ttu-id="7d6c0-217">Настройка времени ожидания и параметры проверки активности</span><span class="sxs-lookup"><span data-stu-id="7d6c0-217">Configure timeout and keep-alive options</span></span>

<span data-ttu-id="7d6c0-218">Доступны дополнительные параметры для настройки времени ожидания и поведение активности на `HubConnection` сам объект:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-218">Additional options for configuring timeout and keep-alive behavior are available on the `HubConnection` object itself:</span></span>

| <span data-ttu-id="7d6c0-219">Параметр .NET</span><span class="sxs-lookup"><span data-stu-id="7d6c0-219">.NET Option</span></span> | <span data-ttu-id="7d6c0-220">Параметр JavaScript</span><span class="sxs-lookup"><span data-stu-id="7d6c0-220">JavaScript Option</span></span> | <span data-ttu-id="7d6c0-221">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7d6c0-221">Default Value</span></span> | <span data-ttu-id="7d6c0-222">Описание:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-222">Description</span></span> |
| ----------- | ----------------- | ------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | <span data-ttu-id="7d6c0-223">30 секунд (30 000 миллисекунд)</span><span class="sxs-lookup"><span data-stu-id="7d6c0-223">30 seconds (30,000 milliseconds)</span></span> | <span data-ttu-id="7d6c0-224">Время ожидания активности сервера.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-224">Timeout for server activity.</span></span> <span data-ttu-id="7d6c0-225">Если сервер не отправил сообщение в этом интервале, клиент считает, что сервер отключен и триггеры `Closed` событий (`onclose` в JavaScript).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-225">If the server hasn't sent a message in this interval, the client considers the server disconnected and triggers the `Closed` event (`onclose` in JavaScript).</span></span> <span data-ttu-id="7d6c0-226">Это значение должно быть достаточно большим для получения сообщения ping, отправляемых с сервера **и** полученные клиентом в течение времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-226">This value must be large enough for a ping message to be sent from the server **and** received by the client within the timeout interval.</span></span> <span data-ttu-id="7d6c0-227">Рекомендуемое значение — номера по крайней мере двойное server `KeepAliveInterval` значение, чтобы выделить время для проверки связи для получения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-227">The recommended value is a number at least double the server's `KeepAliveInterval` value, to allow time for pings to arrive.</span></span> |
| `HandshakeTimeout` | <span data-ttu-id="7d6c0-228">Недоступно для настройки</span><span class="sxs-lookup"><span data-stu-id="7d6c0-228">Not configurable</span></span> | <span data-ttu-id="7d6c0-229">15 секунд</span><span class="sxs-lookup"><span data-stu-id="7d6c0-229">15 seconds</span></span> | <span data-ttu-id="7d6c0-230">Время ожидания подтверждения исходным сервером.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-230">Timeout for initial server handshake.</span></span> <span data-ttu-id="7d6c0-231">Если сервер не отправляет ответ подтверждения в этом интервале, клиент отменяет подтверждения и триггеры `Closed` событий (`onclose` в JavaScript).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-231">If the server doesn't send a handshake response in this interval, the client cancels the handshake and triggers the `Closed` event (`onclose` in JavaScript).</span></span> <span data-ttu-id="7d6c0-232">Это расширенный параметр, который может изменяться только если из-за серьезных сетевой задержки происходят ошибки времени ожидания подтверждения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-232">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="7d6c0-233">Подробности, касающиеся процесса подтверждения, см. в разделе [спецификации протокола концентратора SignalR](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="7d6c0-233">For more detail on the Handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |

<span data-ttu-id="7d6c0-234">В клиенте .NET, значения времени ожидания задаются в виде `TimeSpan` значения.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-234">In the .NET Client, timeout values are specified as `TimeSpan` values.</span></span> <span data-ttu-id="7d6c0-235">В клиенте JavaScript значения времени ожидания задаются как число, указывающее длительность в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-235">In the JavaScript client, timeout values are specified as a number indicating the duration in milliseconds.</span></span>

### <a name="configure-additional-options"></a><span data-ttu-id="7d6c0-236">Настройка дополнительных параметров</span><span class="sxs-lookup"><span data-stu-id="7d6c0-236">Configure additional options</span></span>

<span data-ttu-id="7d6c0-237">Дополнительные параметры можно настроить в `WithUrl` (`withUrl` в JavaScript) метод `HubConnectionBuilder`:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-237">Additional options can be configured in the `WithUrl` (`withUrl` in JavaScript) method on `HubConnectionBuilder`:</span></span>

| <span data-ttu-id="7d6c0-238">Параметр .NET</span><span class="sxs-lookup"><span data-stu-id="7d6c0-238">.NET Option</span></span> | <span data-ttu-id="7d6c0-239">Параметр JavaScript</span><span class="sxs-lookup"><span data-stu-id="7d6c0-239">JavaScript Option</span></span> | <span data-ttu-id="7d6c0-240">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7d6c0-240">Default Value</span></span> | <span data-ttu-id="7d6c0-241">Описание:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-241">Description</span></span> |
| ----------- | ----------------- | ------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | `null` | <span data-ttu-id="7d6c0-242">Функция, возвращающая строку, которая предоставляется как токен проверки подлинности носителя в HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-242">A function returning a string that is provided as a Bearer authentication token in HTTP requests.</span></span> |
| `SkipNegotiation` | `skipNegotiation` | `false` | <span data-ttu-id="7d6c0-243">Задайте значение `true` пропустить шаг согласования.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-243">Set this to `true` to skip the negotiation step.</span></span> <span data-ttu-id="7d6c0-244">**Поддерживается только при передаче WebSockets только транспорта включена**.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-244">**Only supported when the WebSockets transport is the only enabled transport**.</span></span> <span data-ttu-id="7d6c0-245">Этот параметр не может быть включен, при использовании служба Azure SignalR.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-245">This setting can't be enabled when using the Azure SignalR Service.</span></span> |
| `ClientCertificates` | <span data-ttu-id="7d6c0-246">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-246">Not configurable \*</span></span> | <span data-ttu-id="7d6c0-247">Empty</span><span class="sxs-lookup"><span data-stu-id="7d6c0-247">Empty</span></span> | <span data-ttu-id="7d6c0-248">Коллекция TLS-сертификатов, отправляемых для проверки подлинности запросов.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-248">A collection of TLS certificates to send to authenticate requests.</span></span> |
| `Cookies` | <span data-ttu-id="7d6c0-249">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-249">Not configurable \*</span></span> | <span data-ttu-id="7d6c0-250">Empty</span><span class="sxs-lookup"><span data-stu-id="7d6c0-250">Empty</span></span> | <span data-ttu-id="7d6c0-251">Коллекция файлов cookie HTTP для отправки с каждым запросом HTTP.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-251">A collection of HTTP cookies to send with every HTTP request.</span></span> |
| `Credentials` | <span data-ttu-id="7d6c0-252">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-252">Not configurable \*</span></span> | <span data-ttu-id="7d6c0-253">Empty</span><span class="sxs-lookup"><span data-stu-id="7d6c0-253">Empty</span></span> | <span data-ttu-id="7d6c0-254">Учетные данные для отправки с каждым запросом HTTP.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-254">Credentials to send with every HTTP request.</span></span> |
| `CloseTimeout` | <span data-ttu-id="7d6c0-255">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-255">Not configurable \*</span></span> | <span data-ttu-id="7d6c0-256">5 секунд</span><span class="sxs-lookup"><span data-stu-id="7d6c0-256">5 seconds</span></span> | <span data-ttu-id="7d6c0-257">WebSockets.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-257">WebSockets only.</span></span> <span data-ttu-id="7d6c0-258">Максимальное количество времени, клиент ожидает после закрывающего тега для сервера подтвердить запрос на закрытие.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-258">The maximum amount of time the client waits after closing for the server to acknowledge the close request.</span></span> <span data-ttu-id="7d6c0-259">Если сервер не подтвердил закрытия в течение этого времени, клиент отключается.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-259">If the server doesn't acknowledge the close within this time, the client disconnects.</span></span> |
| `Headers` | <span data-ttu-id="7d6c0-260">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-260">Not configurable \*</span></span> | <span data-ttu-id="7d6c0-261">Empty</span><span class="sxs-lookup"><span data-stu-id="7d6c0-261">Empty</span></span> | <span data-ttu-id="7d6c0-262">Словарь дополнительных HTTP-заголовков для отправки с каждым запросом HTTP.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-262">A dictionary of additional HTTP headers to send with every HTTP request.</span></span> |
| `HttpMessageHandlerFactory` | <span data-ttu-id="7d6c0-263">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-263">Not configurable \*</span></span> | `null` | <span data-ttu-id="7d6c0-264">Делегат, который может использоваться для настройки или замените `HttpMessageHandler` используется для отправки запросов HTTP.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-264">A delegate that can be used to configure or replace the `HttpMessageHandler` used to send HTTP requests.</span></span> <span data-ttu-id="7d6c0-265">Не используется для соединений WebSocket.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-265">Not used for WebSocket connections.</span></span> <span data-ttu-id="7d6c0-266">Этот делегат должен возвращать значение отличное от null, и он получает значение по умолчанию в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-266">This delegate must return a non-null value, and it receives the default value as a parameter.</span></span> <span data-ttu-id="7d6c0-267">Измените параметры на это значение по умолчанию и вернуть его или возвращают новый `HttpMessageHandler` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-267">Either modify settings on that default value and return it, or return a new `HttpMessageHandler` instance.</span></span> <span data-ttu-id="7d6c0-268">**Если заменить обработчик обязательно скопируйте параметры, которые вы хотите сохранить из обработчика, в противном случае настроенные параметры (например, файлы cookie и заголовки) нельзя применить новый обработчик.**</span><span class="sxs-lookup"><span data-stu-id="7d6c0-268">**When replacing the handler make sure to copy the settings you want to keep from the provided handler, otherwise, the configured options (such as Cookies and Headers) won't apply to the new handler.**</span></span> |
| `Proxy` | <span data-ttu-id="7d6c0-269">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-269">Not configurable \*</span></span> | `null` | <span data-ttu-id="7d6c0-270">HTTP-прокси для использования при отправке HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-270">An HTTP proxy to use when sending HTTP requests.</span></span> |
| `UseDefaultCredentials` | <span data-ttu-id="7d6c0-271">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-271">Not configurable \*</span></span> | `false` | <span data-ttu-id="7d6c0-272">Задает это значение типа boolean для отправки учетных данных по умолчанию для запросов HTTP и WebSockets.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-272">Set this boolean to send the default credentials for HTTP and WebSockets requests.</span></span> <span data-ttu-id="7d6c0-273">Это позволяет использовать проверку подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-273">This enables the use of Windows authentication.</span></span> |
| `WebSocketConfiguration` | <span data-ttu-id="7d6c0-274">Недоступно для настройки \*</span><span class="sxs-lookup"><span data-stu-id="7d6c0-274">Not configurable \*</span></span> | `null` | <span data-ttu-id="7d6c0-275">Делегат, который может использоваться для настройки дополнительных параметров WebSocket.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-275">A delegate that can be used to configure additional WebSocket options.</span></span> <span data-ttu-id="7d6c0-276">Получает экземпляр класса [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) , можно использовать для настройки параметров.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-276">Receives an instance of [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) that can be used to configure the options.</span></span> |

<span data-ttu-id="7d6c0-277">Параметры, отмеченные звездочкой (\*) не может быть настроено в клиенте JavaScript из-за ограничений в браузере API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="7d6c0-277">Options marked with an asterisk (\*) aren't configurable in the JavaScript client, due to limitations in browser APIs.</span></span>

<span data-ttu-id="7d6c0-278">В клиенте .NET эти параметры можно изменить параметры делегат для `WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-278">In the .NET Client, these options can be modified by the options delegate provided to `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

<span data-ttu-id="7d6c0-279">В клиенте JavaScript, эти параметры могут быть предоставлены в JavaScript объект, предоставляемый для `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="7d6c0-279">In the JavaScript Client, these options can be provided in a JavaScript object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    })
    .build();
```

## <a name="additional-resources"></a><span data-ttu-id="7d6c0-280">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7d6c0-280">Additional resources</span></span>

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
