---
uid: signalr/overview/performance/signalr-performance
title: Производительность SignalR | Документация Майкрософт
author: bradygaster
description: Производительность SignalR
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449862"
---
# <a name="signalr-performance"></a><span data-ttu-id="329a1-103">Производительность SignalR</span><span class="sxs-lookup"><span data-stu-id="329a1-103">SignalR Performance</span></span>

<span data-ttu-id="329a1-104">по [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="329a1-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="329a1-105">В этом разделе описывается разработка, измерение и повышение производительности в приложении SignalR.</span><span class="sxs-lookup"><span data-stu-id="329a1-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="329a1-106">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="329a1-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="329a1-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="329a1-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="329a1-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="329a1-108">.NET 4.5</span></span>
> - <span data-ttu-id="329a1-109">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="329a1-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="329a1-110">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="329a1-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="329a1-111">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="329a1-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="329a1-112">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="329a1-112">Questions and comments</span></span>
>
> <span data-ttu-id="329a1-113">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="329a1-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="329a1-114">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="329a1-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="329a1-115">Последние сведения о производительности и масштабировании SignalR см. в статье [масштабирование веб-сайта в режиме реального времени с помощью ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="329a1-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="329a1-116">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="329a1-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="329a1-117">Рекомендации по проектированию</span><span class="sxs-lookup"><span data-stu-id="329a1-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="329a1-118">Настройка сервера SignalR для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="329a1-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="329a1-119">Устранение проблем с производительностью</span><span class="sxs-lookup"><span data-stu-id="329a1-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="329a1-120">Использование счетчиков производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="329a1-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="329a1-121">Использование других счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="329a1-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="329a1-122">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="329a1-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="329a1-123">Рекомендации по проектированию</span><span class="sxs-lookup"><span data-stu-id="329a1-123">Design considerations</span></span>

<span data-ttu-id="329a1-124">В этом разделе описываются шаблоны, которые могут быть реализованы во время разработки приложения SignalR, чтобы избежать снижения производительности, создавая ненужный сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="329a1-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="329a1-125">Частота сообщений регулирования</span><span class="sxs-lookup"><span data-stu-id="329a1-125">Throttling message frequency</span></span>

<span data-ttu-id="329a1-126">Даже в приложении, которое отправляет сообщения с высокой частотой (например, с игровым приложением реального времени), большинству приложений не требуется отправлять в секунду несколько сообщений.</span><span class="sxs-lookup"><span data-stu-id="329a1-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="329a1-127">Чтобы уменьшить объем трафика, создаваемого каждым клиентом, можно реализовать цикл обработки сообщений, который помещает очереди и отправляет сообщения не чаще, чем фиксированная скорость (то есть до определенного числа сообщений будет отправляться каждую секунду, если в это время есть сообщения в тервал для отправки).</span><span class="sxs-lookup"><span data-stu-id="329a1-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="329a1-128">Пример приложения, который регулирует сообщения до определенной скорости (от клиента и сервера), см. в разделе [Высокая частота в реальном времени с SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="329a1-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="329a1-129">Уменьшение размера сообщения</span><span class="sxs-lookup"><span data-stu-id="329a1-129">Reducing message size</span></span>

<span data-ttu-id="329a1-130">Можно уменьшить размер сообщения SignalR, уменьшив размер сериализованных объектов.</span><span class="sxs-lookup"><span data-stu-id="329a1-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="329a1-131">В серверном коде при отправке объекта, содержащего свойства, которые не требуется передавать, запретите сериализацию этих свойств с помощью атрибута `JsonIgnore`.</span><span class="sxs-lookup"><span data-stu-id="329a1-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="329a1-132">Имена свойств также хранятся в сообщении. имена свойств можно сократить с помощью атрибута `JsonProperty`.</span><span class="sxs-lookup"><span data-stu-id="329a1-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="329a1-133">В следующем примере кода показано, как исключить свойство из отправки клиенту и как сократить имена свойств:</span><span class="sxs-lookup"><span data-stu-id="329a1-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="329a1-134">**Серверный код .NET, демонстрирующий атрибут Жсонигноре для исключения данных из отправки клиенту, а атрибут JsonProperty — для уменьшения размера сообщения.**</span><span class="sxs-lookup"><span data-stu-id="329a1-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="329a1-135">Чтобы сохранить удобочитаемость и удобство сопровождения в клиентском коде, сокращенные имена свойств можно повторно сопоставить с понятными именами после получения сообщения.</span><span class="sxs-lookup"><span data-stu-id="329a1-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="329a1-136">В следующем примере кода демонстрируется один из возможных способов повторного сопоставления сокращенных имен с более длинными, путем определения контракта сообщения (сопоставления) и использования функции `reMap` для применения контракта к оптимизированному классу сообщений:</span><span class="sxs-lookup"><span data-stu-id="329a1-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="329a1-137">**Код JavaScript на стороне клиента, который повторно сопоставляет сокращенные имена свойств с понятными для человека именами.**</span><span class="sxs-lookup"><span data-stu-id="329a1-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="329a1-138">Имена можно также сократить в сообщениях от клиента на сервере, используя тот же метод.</span><span class="sxs-lookup"><span data-stu-id="329a1-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="329a1-139">Уменьшение объема памяти (т. е. объема памяти, используемого для сообщения) объекта Message также может повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="329a1-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="329a1-140">Например, если полный диапазон `int` не требуется, вместо него можно использовать `short` или `byte`.</span><span class="sxs-lookup"><span data-stu-id="329a1-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="329a1-141">Так как сообщения хранятся в памяти сервера в шине сообщений, уменьшение размера сообщений может также привести к проблемам с памятью сервера.</span><span class="sxs-lookup"><span data-stu-id="329a1-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="329a1-142">Настройка сервера SignalR для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="329a1-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="329a1-143">Следующие параметры конфигурации можно использовать для настройки сервера для повышения производительности в приложении SignalR.</span><span class="sxs-lookup"><span data-stu-id="329a1-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="329a1-144">Общие сведения о том, как повысить производительность приложения ASP.NET, см. в разделе [улучшение производительности ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="329a1-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="329a1-145">**Параметры конфигурации SignalR**</span><span class="sxs-lookup"><span data-stu-id="329a1-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="329a1-146">**Дефаултмессажебуфферсизе**: по умолчанию signalr поддерживает 1000 сообщений в памяти на каждый концентратор на каждое соединение.</span><span class="sxs-lookup"><span data-stu-id="329a1-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="329a1-147">Если используются большие сообщения, это может привести к возникновению проблем с памятью, которые можно сократить, уменьшив это значение.</span><span class="sxs-lookup"><span data-stu-id="329a1-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="329a1-148">Этот параметр можно задать в обработчике `Application_Start` событий в приложении ASP.NET или в методе `Configuration` класса запуска OWIN в собственном приложении.</span><span class="sxs-lookup"><span data-stu-id="329a1-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="329a1-149">В следующем примере показано, как уменьшить это значение, чтобы уменьшить объем памяти, занимаемый приложением, чтобы сократить используемую память сервера:</span><span class="sxs-lookup"><span data-stu-id="329a1-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="329a1-150">**Серверный код .NET в Startup.cs для уменьшения размера буфера сообщений по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="329a1-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="329a1-151">**Параметры конфигурации IIS**</span><span class="sxs-lookup"><span data-stu-id="329a1-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="329a1-152">**Максимальное число одновременных запросов на приложение**: увеличение числа одновременных запросов IIS увеличит количество ресурсов сервера, доступных для обслуживания запросов.</span><span class="sxs-lookup"><span data-stu-id="329a1-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="329a1-153">Значение по умолчанию — 5000; чтобы увеличить этот параметр, выполните следующие команды в командной строке с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="329a1-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="329a1-154">**ApplicationPool QueueLength**. это максимальное число запросов, которые очереди HTTP. sys для пула приложений.</span><span class="sxs-lookup"><span data-stu-id="329a1-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="329a1-155">Когда очередь заполнена, новые запросы получают ответ 503 "Служба недоступна".</span><span class="sxs-lookup"><span data-stu-id="329a1-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="329a1-156">Значение по умолчанию ― 1000.</span><span class="sxs-lookup"><span data-stu-id="329a1-156">The default value is 1000.</span></span>

    <span data-ttu-id="329a1-157">Сокращение длины очереди рабочего процесса в пуле приложений, в котором размещается приложение, приведет к экономии ресурсов памяти.</span><span class="sxs-lookup"><span data-stu-id="329a1-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="329a1-158">Дополнительные сведения см. в разделе [Управление, Настройка и настройка пулов приложений](https://technet.microsoft.com/library/cc745955.aspx).</span><span class="sxs-lookup"><span data-stu-id="329a1-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="329a1-159">**Параметры конфигурации ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="329a1-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="329a1-160">В этом разделе содержатся параметры конфигурации, которые можно задать в файле `aspnet.config`.</span><span class="sxs-lookup"><span data-stu-id="329a1-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="329a1-161">Этот файл находится в одном из двух расположений в зависимости от платформы:</span><span class="sxs-lookup"><span data-stu-id="329a1-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="329a1-162">Параметры ASP.NET, которые могут улучшить производительность SignalR, включают следующее:</span><span class="sxs-lookup"><span data-stu-id="329a1-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="329a1-163">**Максимальное число одновременных запросов на ЦП**: увеличение этого значения может привести к снижению узких мест производительности.</span><span class="sxs-lookup"><span data-stu-id="329a1-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="329a1-164">Чтобы увеличить этот параметр, добавьте следующий параметр конфигурации в файл `aspnet.config`:</span><span class="sxs-lookup"><span data-stu-id="329a1-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="329a1-165">**Ограничение очереди запросов**: Если общее число соединений превышает значение параметра `maxConcurrentRequestsPerCPU`, ASP.NET начнет регулирование запросов с помощью очереди.</span><span class="sxs-lookup"><span data-stu-id="329a1-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="329a1-166">Чтобы увеличить размер очереди, можно увеличить значение параметра `requestQueueLimit`.</span><span class="sxs-lookup"><span data-stu-id="329a1-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="329a1-167">Для этого добавьте следующий параметр конфигурации в узел `processModel` в `config/machine.config` (а не `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="329a1-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="329a1-168">Устранение проблем с производительностью</span><span class="sxs-lookup"><span data-stu-id="329a1-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="329a1-169">В этом разделе описываются способы поиска узких мест производительности в приложении.</span><span class="sxs-lookup"><span data-stu-id="329a1-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="329a1-170">Проверка использования WebSocket</span><span class="sxs-lookup"><span data-stu-id="329a1-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="329a1-171">Хотя SignalR может использовать разнообразные транспорты для обмена данными между клиентом и сервером, WebSocket обеспечивает значительное преимущество в производительности и следует использовать, если клиент и сервер его поддерживают.</span><span class="sxs-lookup"><span data-stu-id="329a1-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="329a1-172">Чтобы определить, соответствуют ли клиент и сервер требованиям WebSocket, см. раздел [транспорты и резервные](../getting-started/introduction-to-signalr.md#transports)серверы.</span><span class="sxs-lookup"><span data-stu-id="329a1-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="329a1-173">Чтобы определить, какой транспорт используется в приложении, можно использовать средства разработчика браузера и просмотреть журналы, чтобы узнать, какой транспорт используется для подключения.</span><span class="sxs-lookup"><span data-stu-id="329a1-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="329a1-174">Сведения об использовании средств разработки браузеров в Internet Explorer и Chrome см. в статье [транспорты и резервные стратегии](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="329a1-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="329a1-175">Использование счетчиков производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="329a1-175">Using SignalR performance counters</span></span>

<span data-ttu-id="329a1-176">В этом разделе описывается включение и использование счетчиков производительности SignalR, найденных в пакете `Microsoft.AspNet.SignalR.Utils`.</span><span class="sxs-lookup"><span data-stu-id="329a1-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="329a1-177">Установка SignalR. exe</span><span class="sxs-lookup"><span data-stu-id="329a1-177">Installing signalr.exe</span></span>

<span data-ttu-id="329a1-178">Счетчики производительности можно добавить на сервер с помощью служебной программы SignalR. exe.</span><span class="sxs-lookup"><span data-stu-id="329a1-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="329a1-179">Чтобы установить эту программу, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="329a1-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="329a1-180">В Visual Studio выберите **инструменты** > **диспетчер пакетов NuGet** > **Управление пакетами NuGet для решения**</span><span class="sxs-lookup"><span data-stu-id="329a1-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="329a1-181">Найдите **SignalR. utils**и нажмите кнопку установить.</span><span class="sxs-lookup"><span data-stu-id="329a1-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="329a1-182">Примите условия лицензионного соглашения, чтобы установить пакет.</span><span class="sxs-lookup"><span data-stu-id="329a1-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="329a1-183">SignalR. exe будет установлен для `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span><span class="sxs-lookup"><span data-stu-id="329a1-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="329a1-184">Установка счетчиков производительности с помощью SignalR. exe</span><span class="sxs-lookup"><span data-stu-id="329a1-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="329a1-185">Чтобы установить счетчики производительности SignalR, запустите SignalR. exe в командной строке с повышенными привилегиями со следующим параметром:</span><span class="sxs-lookup"><span data-stu-id="329a1-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="329a1-186">Чтобы удалить счетчики производительности SignalR, запустите SignalR. exe в командной строке с повышенными привилегиями со следующим параметром:</span><span class="sxs-lookup"><span data-stu-id="329a1-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="329a1-187">Счетчики производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="329a1-187">SignalR Performance counters</span></span>

<span data-ttu-id="329a1-188">Пакет служебных программ устанавливает следующие счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="329a1-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="329a1-189">Счетчик "всего" измеряет количество событий, произошедших с момента последнего перезапуска сервера или пула приложений.</span><span class="sxs-lookup"><span data-stu-id="329a1-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="329a1-190">**Метрики подключения**</span><span class="sxs-lookup"><span data-stu-id="329a1-190">**Connection metrics**</span></span>

<span data-ttu-id="329a1-191">Следующие метрики измеряют происходящие события времени существования соединения.</span><span class="sxs-lookup"><span data-stu-id="329a1-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="329a1-192">Дополнительные сведения см. в разделе [Основные сведения и обработка событий времени жизни соединения](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="329a1-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="329a1-193">**Подключено подключений**</span><span class="sxs-lookup"><span data-stu-id="329a1-193">**Connections Connected**</span></span>
- <span data-ttu-id="329a1-194">**Подключения повторно подключены**</span><span class="sxs-lookup"><span data-stu-id="329a1-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="329a1-195">**Подключения отключены**</span><span class="sxs-lookup"><span data-stu-id="329a1-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="329a1-196">**Текущих подключений**</span><span class="sxs-lookup"><span data-stu-id="329a1-196">**Connections Current**</span></span>

<span data-ttu-id="329a1-197">**Метрики сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-197">**Message metrics**</span></span>

<span data-ttu-id="329a1-198">Следующие метрики измеряют трафик сообщений, создаваемый SignalR.</span><span class="sxs-lookup"><span data-stu-id="329a1-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="329a1-199">**Всего получено сообщений подключения**</span><span class="sxs-lookup"><span data-stu-id="329a1-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="329a1-200">**Всего Отправлено сообщений подключения**</span><span class="sxs-lookup"><span data-stu-id="329a1-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="329a1-201">**Получено сообщений о соединении/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="329a1-202">**Отправлено сообщений о соединении/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="329a1-203">**Метрики шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-203">**Message bus metrics**</span></span>

<span data-ttu-id="329a1-204">Следующие метрики измеряют трафик через внутреннюю шину сообщений SignalR, очередь, в которой размещаются все входящие и исходящие сообщения SignalR.</span><span class="sxs-lookup"><span data-stu-id="329a1-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="329a1-205">Сообщение **публикуется** во время отправки или вещания.</span><span class="sxs-lookup"><span data-stu-id="329a1-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="329a1-206">**Подписчик** в этом контексте является подпиской на канале сообщений; Это число должно равняться числу клиентов плюс сам сервер.</span><span class="sxs-lookup"><span data-stu-id="329a1-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="329a1-207">**Выделенный рабочий процесс** — это компонент, который отправляет данные в активные соединения; **занятая рабочая роль** — это одна из них, которая активно отправляет сообщение.</span><span class="sxs-lookup"><span data-stu-id="329a1-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="329a1-208">**Всего получено сообщений в шине сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="329a1-209">**Получено сообщений в шине сообщений/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="329a1-210">**Всего опубликованных сообщений в шине сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="329a1-211">**Опубликовано сообщений в шине сообщений/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="329a1-212">**Текущие подписчики шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="329a1-213">**Всего подписчиков на шину сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="329a1-214">**Подписчиков шины сообщений/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="329a1-215">**Выделенные рабочие процессы шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="329a1-216">**Рабочие процессы, занятые шиной сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="329a1-217">**Актуальные разделы шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="329a1-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="329a1-218">**Метрики ошибок**</span><span class="sxs-lookup"><span data-stu-id="329a1-218">**Error metrics**</span></span>

<span data-ttu-id="329a1-219">Следующие метрики измеряют ошибки, создаваемые трафиком сообщений SignalR.</span><span class="sxs-lookup"><span data-stu-id="329a1-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="329a1-220">Ошибки **разрешения концентратора** возникают, когда не удается разрешить концентратор или метод концентратора.</span><span class="sxs-lookup"><span data-stu-id="329a1-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="329a1-221">Ошибки **вызова концентратора** — это исключения, возникающие при вызове метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="329a1-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="329a1-222">Ошибки **транспорта** — это ошибки соединения, возникающие во время HTTP-запроса или ответа.</span><span class="sxs-lookup"><span data-stu-id="329a1-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="329a1-223">**Ошибки: все итоги**</span><span class="sxs-lookup"><span data-stu-id="329a1-223">**Errors: All Total**</span></span>
- <span data-ttu-id="329a1-224">**Ошибок: "всего/с"**</span><span class="sxs-lookup"><span data-stu-id="329a1-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="329a1-225">**Ошибки: общее разрешение концентратора**</span><span class="sxs-lookup"><span data-stu-id="329a1-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="329a1-226">**Ошибки: разрешение концентратора/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="329a1-227">**Ошибки: всего вызовов концентратора**</span><span class="sxs-lookup"><span data-stu-id="329a1-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="329a1-228">**Ошибки: вызов концентратора/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="329a1-229">**Ошибки: всего транспортных**</span><span class="sxs-lookup"><span data-stu-id="329a1-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="329a1-230">**Ошибки: транспорт/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="329a1-231">**Метрики масштабирования**</span><span class="sxs-lookup"><span data-stu-id="329a1-231">**Scaleout metrics**</span></span>

<span data-ttu-id="329a1-232">Следующие метрики измеряют трафик и ошибки, созданные поставщиком масштабирования.</span><span class="sxs-lookup"><span data-stu-id="329a1-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="329a1-233">**Поток** в этом контексте — это единица масштабирования, используемая поставщиком масштабирования; Это таблица, если используется SQL Server, раздел, если используется служебная шина, и подписка, если используется Redis.</span><span class="sxs-lookup"><span data-stu-id="329a1-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="329a1-234">Каждый поток обеспечивает упорядоченные операции чтения и записи; один поток является потенциальным узким местом в масштабе, поэтому количество потоков можно увеличить, чтобы снизить эту узкие места.</span><span class="sxs-lookup"><span data-stu-id="329a1-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="329a1-235">Если используется несколько потоков, SignalR автоматически распределяет сообщения (сегменты) по этим потокам таким образом, чтобы сообщения, отправленные из любого подключения, были в порядке.</span><span class="sxs-lookup"><span data-stu-id="329a1-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="329a1-236">Параметр [макскуеуеленгс](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) управляет длиной очереди отправки scaleing, обслуживаемой SignalR.</span><span class="sxs-lookup"><span data-stu-id="329a1-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="329a1-237">Если задать для него значение больше 0, все сообщения в очереди отправки будут отправляться по одному в настроенную объединительную плату обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="329a1-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="329a1-238">Если размер очереди превышает заданную длину, последующие вызовы Send немедленно завершаются сбоем с исключением [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) , пока число сообщений в очереди не станет меньше значения параметра.</span><span class="sxs-lookup"><span data-stu-id="329a1-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="329a1-239">Очередь по умолчанию отключена, так как реализованные объединительные платы обычно имеют собственные очереди или управление потоком.</span><span class="sxs-lookup"><span data-stu-id="329a1-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="329a1-240">В случае SQL Server пул соединений эффективно ограничивает количество отправок, которые будут отправляться в любое время.</span><span class="sxs-lookup"><span data-stu-id="329a1-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="329a1-241">По умолчанию для SQL Server и Redis используется только один поток, пять потоков используются для служебной шины, а очередь отключается, но эти параметры можно изменить с помощью настройки в SQL Server и служебной шине:</span><span class="sxs-lookup"><span data-stu-id="329a1-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="329a1-242">**Серверный код .NET для настройки числа таблиц и длины очереди для SQL Serverной объединительной платы**</span><span class="sxs-lookup"><span data-stu-id="329a1-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="329a1-243">**Серверный код .NET для настройки числа разделов и длины очереди для объединительной платы служебной шины**</span><span class="sxs-lookup"><span data-stu-id="329a1-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="329a1-244">Поток **буферизации** — это тот, который перешел в состояние сбоя. Если поток находится в состоянии сбоя, все сообщения, отправленные на объединительную плату, будут завершаться сбоем сразу, пока поток не завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="329a1-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="329a1-245">**Длина очереди отправки** — это количество сообщений, которые были отправлены, но еще не отправлены.</span><span class="sxs-lookup"><span data-stu-id="329a1-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="329a1-246">**Получено сообщений в канале масштабирования сообщений в секунду**</span><span class="sxs-lookup"><span data-stu-id="329a1-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="329a1-247">**Всего потоков масштабирования**</span><span class="sxs-lookup"><span data-stu-id="329a1-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="329a1-248">**Открытие потоков масштабирования**</span><span class="sxs-lookup"><span data-stu-id="329a1-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="329a1-249">**Буферизация потоков с масштабированием**</span><span class="sxs-lookup"><span data-stu-id="329a1-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="329a1-250">**Всего ошибок масштабирования**</span><span class="sxs-lookup"><span data-stu-id="329a1-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="329a1-251">**Ошибок масштабирования/с**</span><span class="sxs-lookup"><span data-stu-id="329a1-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="329a1-252">**Длина очереди отправки при увеличении**</span><span class="sxs-lookup"><span data-stu-id="329a1-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="329a1-253">Дополнительные сведения об измерении этих счетчиков см. в разделе [масштабирование SignalR с помощью служебной шины Azure](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="329a1-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="329a1-254">Использование других счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="329a1-254">Using other performance counters</span></span>

<span data-ttu-id="329a1-255">Следующие счетчики производительности также могут быть полезны при наблюдении за производительностью приложения.</span><span class="sxs-lookup"><span data-stu-id="329a1-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="329a1-256">**Память**</span><span class="sxs-lookup"><span data-stu-id="329a1-256">**Memory**</span></span>

- <span data-ttu-id="329a1-257">Память CLR .NET\\байт во всех кучах (для w3wp)</span><span class="sxs-lookup"><span data-stu-id="329a1-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="329a1-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="329a1-258">**ASP.NET**</span></span>

- <span data-ttu-id="329a1-259">Текущий ASP. NET \ запросов</span><span class="sxs-lookup"><span data-stu-id="329a1-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="329a1-260">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="329a1-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="329a1-261">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="329a1-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="329a1-262">**ЦП**</span><span class="sxs-lookup"><span data-stu-id="329a1-262">**CPU**</span></span>

- <span data-ttu-id="329a1-263">Время Информатион\процессор процессора</span><span class="sxs-lookup"><span data-stu-id="329a1-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="329a1-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="329a1-264">**TCP/IP**</span></span>

- <span data-ttu-id="329a1-265">TCPv6/подключения установлены</span><span class="sxs-lookup"><span data-stu-id="329a1-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="329a1-266">TCPv4/подключения установлены</span><span class="sxs-lookup"><span data-stu-id="329a1-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="329a1-267">**Веб-служба**</span><span class="sxs-lookup"><span data-stu-id="329a1-267">**Web Service**</span></span>

- <span data-ttu-id="329a1-268">Подключения к веб-служба \ текущих</span><span class="sxs-lookup"><span data-stu-id="329a1-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="329a1-269">Подключения к веб-Сервице\максимум</span><span class="sxs-lookup"><span data-stu-id="329a1-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="329a1-270">**Работа с потоками**</span><span class="sxs-lookup"><span data-stu-id="329a1-270">**Threading**</span></span>

- <span data-ttu-id="329a1-271">Блокировки CLR .NET и потоки\\число текущих логических потоков</span><span class="sxs-lookup"><span data-stu-id="329a1-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="329a1-272">Блокировки CLR .NET и потоки\\количество текущих физических потоков</span><span class="sxs-lookup"><span data-stu-id="329a1-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="329a1-273">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="329a1-273">Other Resources</span></span>

<span data-ttu-id="329a1-274">Дополнительные сведения о мониторинге производительности ASP.NET и настройке см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="329a1-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="329a1-275">[Общие сведения о производительности ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="329a1-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="329a1-276">Использование потоков ASP.NET в IIS 7,5, IIS 7,0 и IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="329a1-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="329a1-277">Элемент &lt;applicationPool&gt; (веб-параметры)</span><span class="sxs-lookup"><span data-stu-id="329a1-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
