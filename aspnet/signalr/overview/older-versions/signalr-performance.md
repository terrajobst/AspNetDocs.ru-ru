---
uid: signalr/overview/older-versions/signalr-performance
title: Производительность SignalR (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: Производительность SignalR
ms.author: bradyg
ms.date: 07/03/2013
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 915fd822caae9bbcb0a688c6dd7a5b2bda12c9df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468108"
---
# <a name="signalr-performance-signalr-1x"></a><span data-ttu-id="34e7f-103">Производительность SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="34e7f-103">SignalR Performance (SignalR 1.x)</span></span>

<span data-ttu-id="34e7f-104">по [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="34e7f-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="34e7f-105">В этом разделе описывается разработка, измерение и повышение производительности в приложении SignalR.</span><span class="sxs-lookup"><span data-stu-id="34e7f-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>

<span data-ttu-id="34e7f-106">Последние сведения о производительности и масштабировании SignalR см. в статье [масштабирование веб-сайта в режиме реального времени с помощью ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="34e7f-106">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="34e7f-107">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="34e7f-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="34e7f-108">Рекомендации по проектированию</span><span class="sxs-lookup"><span data-stu-id="34e7f-108">Design considerations</span></span>](#design)
- [<span data-ttu-id="34e7f-109">Настройка сервера SignalR для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="34e7f-109">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="34e7f-110">Устранение проблем с производительностью</span><span class="sxs-lookup"><span data-stu-id="34e7f-110">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="34e7f-111">Использование счетчиков производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="34e7f-111">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="34e7f-112">Использование других счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="34e7f-112">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="34e7f-113">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="34e7f-113">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="34e7f-114">Рекомендации по проектированию</span><span class="sxs-lookup"><span data-stu-id="34e7f-114">Design considerations</span></span>

<span data-ttu-id="34e7f-115">В этом разделе описываются шаблоны, которые могут быть реализованы во время разработки приложения SignalR, чтобы избежать снижения производительности, создавая ненужный сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="34e7f-115">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="34e7f-116">Частота сообщений регулирования</span><span class="sxs-lookup"><span data-stu-id="34e7f-116">Throttling message frequency</span></span>

<span data-ttu-id="34e7f-117">Даже в приложении, которое отправляет сообщения с высокой частотой (например, с игровым приложением реального времени), большинству приложений не требуется отправлять в секунду несколько сообщений.</span><span class="sxs-lookup"><span data-stu-id="34e7f-117">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="34e7f-118">Чтобы уменьшить объем трафика, создаваемого каждым клиентом, можно реализовать цикл обработки сообщений, который помещает очереди и отправляет сообщения не чаще, чем фиксированная скорость (то есть до определенного числа сообщений будет отправляться каждую секунду, если в это время есть сообщения в тервал для отправки).</span><span class="sxs-lookup"><span data-stu-id="34e7f-118">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="34e7f-119">Пример приложения, который регулирует сообщения до определенной скорости (от клиента и сервера), см. в разделе [Высокая частота в реальном времени с SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="34e7f-119">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="34e7f-120">Уменьшение размера сообщения</span><span class="sxs-lookup"><span data-stu-id="34e7f-120">Reducing message size</span></span>

<span data-ttu-id="34e7f-121">Можно уменьшить размер сообщения SignalR, уменьшив размер сериализованных объектов.</span><span class="sxs-lookup"><span data-stu-id="34e7f-121">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="34e7f-122">В серверном коде при отправке объекта, содержащего свойства, которые не требуется передавать, запретите сериализацию этих свойств с помощью атрибута `JsonIgnore`.</span><span class="sxs-lookup"><span data-stu-id="34e7f-122">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="34e7f-123">Имена свойств также хранятся в сообщении. имена свойств можно сократить с помощью атрибута `JsonProperty`.</span><span class="sxs-lookup"><span data-stu-id="34e7f-123">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="34e7f-124">В следующем примере кода показано, как исключить свойство из отправки клиенту и как сократить имена свойств:</span><span class="sxs-lookup"><span data-stu-id="34e7f-124">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="34e7f-125">**Серверный код .NET, демонстрирующий атрибут Жсонигноре для исключения данных из отправки клиенту, а атрибут JsonProperty — для уменьшения размера сообщения.**</span><span class="sxs-lookup"><span data-stu-id="34e7f-125">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="34e7f-126">Чтобы сохранить удобочитаемость и удобство сопровождения в клиентском коде, сокращенные имена свойств можно повторно сопоставить с понятными именами после получения сообщения.</span><span class="sxs-lookup"><span data-stu-id="34e7f-126">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="34e7f-127">В следующем примере кода демонстрируется один из возможных способов повторного сопоставления сокращенных имен с более длинными, путем определения контракта сообщения (сопоставления) и использования функции `reMap` для применения контракта к оптимизированному классу сообщений:</span><span class="sxs-lookup"><span data-stu-id="34e7f-127">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="34e7f-128">**Код JavaScript на стороне клиента, который повторно сопоставляет сокращенные имена свойств с понятными для человека именами.**</span><span class="sxs-lookup"><span data-stu-id="34e7f-128">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="34e7f-129">Имена можно также сократить в сообщениях от клиента на сервере, используя тот же метод.</span><span class="sxs-lookup"><span data-stu-id="34e7f-129">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="34e7f-130">Уменьшение объема памяти (т. е. объема памяти, используемого для сообщения) объекта Message также может повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="34e7f-130">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="34e7f-131">Например, если полный диапазон `int` не требуется, вместо него можно использовать `short` или `byte`.</span><span class="sxs-lookup"><span data-stu-id="34e7f-131">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="34e7f-132">Так как сообщения хранятся в памяти сервера в шине сообщений, уменьшение размера сообщений может также привести к проблемам с памятью сервера.</span><span class="sxs-lookup"><span data-stu-id="34e7f-132">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="34e7f-133">Настройка сервера SignalR для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="34e7f-133">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="34e7f-134">Следующие параметры конфигурации можно использовать для настройки сервера для повышения производительности в приложении SignalR.</span><span class="sxs-lookup"><span data-stu-id="34e7f-134">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="34e7f-135">Общие сведения о том, как повысить производительность приложения ASP.NET, см. в разделе [улучшение производительности ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="34e7f-135">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="34e7f-136">**Параметры конфигурации SignalR**</span><span class="sxs-lookup"><span data-stu-id="34e7f-136">**SignalR configuration settings**</span></span>

- <span data-ttu-id="34e7f-137">**Дефаултмессажебуфферсизе**: по умолчанию signalr поддерживает 1000 сообщений в памяти на каждый концентратор на каждое соединение.</span><span class="sxs-lookup"><span data-stu-id="34e7f-137">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="34e7f-138">Если используются большие сообщения, это может привести к возникновению проблем с памятью, которые можно сократить, уменьшив это значение.</span><span class="sxs-lookup"><span data-stu-id="34e7f-138">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="34e7f-139">Этот параметр можно задать в обработчике `Application_Start` событий в приложении ASP.NET или в методе `Configuration` класса запуска OWIN в собственном приложении.</span><span class="sxs-lookup"><span data-stu-id="34e7f-139">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="34e7f-140">В следующем примере показано, как уменьшить это значение, чтобы уменьшить объем памяти, занимаемый приложением, чтобы сократить используемую память сервера:</span><span class="sxs-lookup"><span data-stu-id="34e7f-140">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="34e7f-141">**Код сервера .NET в Global. asax для уменьшения размера буфера сообщений по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="34e7f-141">**.NET server code in Global.asax for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="34e7f-142">**Параметры конфигурации IIS**</span><span class="sxs-lookup"><span data-stu-id="34e7f-142">**IIS configuration settings**</span></span>

- <span data-ttu-id="34e7f-143">**Максимальное число одновременных запросов на приложение**: увеличение числа одновременных запросов IIS увеличит количество ресурсов сервера, доступных для обслуживания запросов.</span><span class="sxs-lookup"><span data-stu-id="34e7f-143">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="34e7f-144">Значение по умолчанию — 5000; чтобы увеличить этот параметр, выполните следующие команды в командной строке с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="34e7f-144">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

<span data-ttu-id="34e7f-145">**Параметры конфигурации ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="34e7f-145">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="34e7f-146">В этом разделе содержатся параметры конфигурации, которые можно задать в файле `aspnet.config`.</span><span class="sxs-lookup"><span data-stu-id="34e7f-146">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="34e7f-147">Этот файл находится в одном из двух расположений в зависимости от платформы:</span><span class="sxs-lookup"><span data-stu-id="34e7f-147">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="34e7f-148">Параметры ASP.NET, которые могут улучшить производительность SignalR, включают следующее:</span><span class="sxs-lookup"><span data-stu-id="34e7f-148">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="34e7f-149">**Максимальное число одновременных запросов на ЦП**: увеличение этого значения может привести к снижению узких мест производительности.</span><span class="sxs-lookup"><span data-stu-id="34e7f-149">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="34e7f-150">Чтобы увеличить этот параметр, добавьте следующий параметр конфигурации в файл `aspnet.config`:</span><span class="sxs-lookup"><span data-stu-id="34e7f-150">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="34e7f-151">**Ограничение очереди запросов**: Если общее число соединений превышает значение параметра `maxConcurrentRequestsPerCPU`, ASP.NET начнет регулирование запросов с помощью очереди.</span><span class="sxs-lookup"><span data-stu-id="34e7f-151">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="34e7f-152">Чтобы увеличить размер очереди, можно увеличить значение параметра `requestQueueLimit`.</span><span class="sxs-lookup"><span data-stu-id="34e7f-152">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="34e7f-153">Для этого добавьте следующий параметр конфигурации в узел `processModel` в `config/machine.config` (а не `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="34e7f-153">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="34e7f-154">Устранение проблем с производительностью</span><span class="sxs-lookup"><span data-stu-id="34e7f-154">Troubleshooting performance issues</span></span>

<span data-ttu-id="34e7f-155">В этом разделе описываются способы поиска узких мест производительности в приложении.</span><span class="sxs-lookup"><span data-stu-id="34e7f-155">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="34e7f-156">Проверка использования WebSocket</span><span class="sxs-lookup"><span data-stu-id="34e7f-156">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="34e7f-157">Хотя SignalR может использовать разнообразные транспорты для обмена данными между клиентом и сервером, WebSocket обеспечивает значительное преимущество в производительности и следует использовать, если клиент и сервер его поддерживают.</span><span class="sxs-lookup"><span data-stu-id="34e7f-157">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="34e7f-158">Чтобы определить, соответствуют ли клиент и сервер требованиям WebSocket, см. раздел [транспорты и резервные](../getting-started/introduction-to-signalr.md#transports)серверы.</span><span class="sxs-lookup"><span data-stu-id="34e7f-158">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="34e7f-159">Чтобы определить, какой транспорт используется в приложении, можно использовать средства разработчика браузера и просмотреть журналы, чтобы узнать, какой транспорт используется для подключения.</span><span class="sxs-lookup"><span data-stu-id="34e7f-159">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="34e7f-160">Сведения об использовании средств разработки браузеров в Internet Explorer и Chrome см. в статье [транспорты и резервные стратегии](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="34e7f-160">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="34e7f-161">Использование счетчиков производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="34e7f-161">Using SignalR performance counters</span></span>

<span data-ttu-id="34e7f-162">В этом разделе описывается включение и использование счетчиков производительности SignalR, найденных в пакете `Microsoft.AspNet.SignalR.Utils`.</span><span class="sxs-lookup"><span data-stu-id="34e7f-162">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="34e7f-163">Установка SignalR. exe</span><span class="sxs-lookup"><span data-stu-id="34e7f-163">Installing signalr.exe</span></span>

<span data-ttu-id="34e7f-164">Счетчики производительности можно добавить на сервер с помощью служебной программы SignalR. exe.</span><span class="sxs-lookup"><span data-stu-id="34e7f-164">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="34e7f-165">Чтобы установить эту программу, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="34e7f-165">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="34e7f-166">В Visual Studio выберите **инструменты** > **диспетчер пакетов NuGet** > **Управление пакетами NuGet для решения**</span><span class="sxs-lookup"><span data-stu-id="34e7f-166">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="34e7f-167">Найдите **SignalR. utils**и нажмите кнопку установить.</span><span class="sxs-lookup"><span data-stu-id="34e7f-167">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="34e7f-168">Примите условия лицензионного соглашения, чтобы установить пакет.</span><span class="sxs-lookup"><span data-stu-id="34e7f-168">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="34e7f-169">SignalR. exe будет установлен для `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span><span class="sxs-lookup"><span data-stu-id="34e7f-169">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="34e7f-170">Установка счетчиков производительности с помощью SignalR. exe</span><span class="sxs-lookup"><span data-stu-id="34e7f-170">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="34e7f-171">Чтобы установить счетчики производительности SignalR, запустите SignalR. exe в командной строке с повышенными привилегиями со следующим параметром:</span><span class="sxs-lookup"><span data-stu-id="34e7f-171">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="34e7f-172">Чтобы удалить счетчики производительности SignalR, запустите SignalR. exe в командной строке с повышенными привилегиями со следующим параметром:</span><span class="sxs-lookup"><span data-stu-id="34e7f-172">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="34e7f-173">Счетчики производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="34e7f-173">SignalR Performance counters</span></span>

<span data-ttu-id="34e7f-174">Пакет служебных программ устанавливает следующие счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="34e7f-174">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="34e7f-175">Счетчик "всего" измеряет количество событий, произошедших с момента последнего перезапуска сервера или пула приложений.</span><span class="sxs-lookup"><span data-stu-id="34e7f-175">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="34e7f-176">**Метрики подключения**</span><span class="sxs-lookup"><span data-stu-id="34e7f-176">**Connection metrics**</span></span>

<span data-ttu-id="34e7f-177">Следующие метрики измеряют происходящие события времени существования соединения.</span><span class="sxs-lookup"><span data-stu-id="34e7f-177">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="34e7f-178">Дополнительные сведения см. в разделе [Основные сведения и обработка событий времени жизни соединения](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="34e7f-178">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="34e7f-179">**Подключено подключений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-179">**Connections Connected**</span></span>
- <span data-ttu-id="34e7f-180">**Подключения повторно подключены**</span><span class="sxs-lookup"><span data-stu-id="34e7f-180">**Connections Reconnected**</span></span>
- <span data-ttu-id="34e7f-181">**Подключения отключены**</span><span class="sxs-lookup"><span data-stu-id="34e7f-181">**Connections Disconnected**</span></span>
- <span data-ttu-id="34e7f-182">**Текущих подключений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-182">**Connections Current**</span></span>

<span data-ttu-id="34e7f-183">**Метрики сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-183">**Message metrics**</span></span>

<span data-ttu-id="34e7f-184">Следующие метрики измеряют трафик сообщений, создаваемый SignalR.</span><span class="sxs-lookup"><span data-stu-id="34e7f-184">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="34e7f-185">**Всего получено сообщений подключения**</span><span class="sxs-lookup"><span data-stu-id="34e7f-185">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="34e7f-186">**Всего Отправлено сообщений подключения**</span><span class="sxs-lookup"><span data-stu-id="34e7f-186">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="34e7f-187">**Получено сообщений о соединении/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-187">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="34e7f-188">**Отправлено сообщений о соединении/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-188">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="34e7f-189">**Метрики шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-189">**Message bus metrics**</span></span>

<span data-ttu-id="34e7f-190">Следующие метрики измеряют трафик через внутреннюю шину сообщений SignalR, очередь, в которой размещаются все входящие и исходящие сообщения SignalR.</span><span class="sxs-lookup"><span data-stu-id="34e7f-190">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="34e7f-191">Сообщение **публикуется** во время отправки или вещания.</span><span class="sxs-lookup"><span data-stu-id="34e7f-191">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="34e7f-192">**Подписчик** в этом контексте является подпиской на канале сообщений; Это число должно равняться числу клиентов плюс сам сервер.</span><span class="sxs-lookup"><span data-stu-id="34e7f-192">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="34e7f-193">**Выделенный рабочий процесс** — это компонент, который отправляет данные в активные соединения; **занятая рабочая роль** — это одна из них, которая активно отправляет сообщение.</span><span class="sxs-lookup"><span data-stu-id="34e7f-193">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="34e7f-194">**Всего получено сообщений в шине сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-194">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="34e7f-195">**Получено сообщений в шине сообщений/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-195">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="34e7f-196">**Всего опубликованных сообщений в шине сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-196">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="34e7f-197">**Опубликовано сообщений в шине сообщений/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-197">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="34e7f-198">**Текущие подписчики шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-198">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="34e7f-199">**Всего подписчиков на шину сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-199">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="34e7f-200">**Подписчиков шины сообщений/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-200">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="34e7f-201">**Выделенные рабочие процессы шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-201">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="34e7f-202">**Рабочие процессы, занятые шиной сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-202">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="34e7f-203">**Актуальные разделы шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="34e7f-203">**Message Bus Topics Current**</span></span>

<span data-ttu-id="34e7f-204">**Метрики ошибок**</span><span class="sxs-lookup"><span data-stu-id="34e7f-204">**Error metrics**</span></span>

<span data-ttu-id="34e7f-205">Следующие метрики измеряют ошибки, создаваемые трафиком сообщений SignalR.</span><span class="sxs-lookup"><span data-stu-id="34e7f-205">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="34e7f-206">Ошибки **разрешения концентратора** возникают, когда не удается разрешить концентратор или метод концентратора.</span><span class="sxs-lookup"><span data-stu-id="34e7f-206">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="34e7f-207">Ошибки **вызова концентратора** — это исключения, возникающие при вызове метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="34e7f-207">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="34e7f-208">Ошибки **транспорта** — это ошибки соединения, возникающие во время HTTP-запроса или ответа.</span><span class="sxs-lookup"><span data-stu-id="34e7f-208">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="34e7f-209">**Ошибки: все итоги**</span><span class="sxs-lookup"><span data-stu-id="34e7f-209">**Errors: All Total**</span></span>
- <span data-ttu-id="34e7f-210">**Ошибок: "всего/с"**</span><span class="sxs-lookup"><span data-stu-id="34e7f-210">**Errors: All/Sec**</span></span>
- <span data-ttu-id="34e7f-211">**Ошибки: общее разрешение концентратора**</span><span class="sxs-lookup"><span data-stu-id="34e7f-211">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="34e7f-212">**Ошибки: разрешение концентратора/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-212">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="34e7f-213">**Ошибки: всего вызовов концентратора**</span><span class="sxs-lookup"><span data-stu-id="34e7f-213">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="34e7f-214">**Ошибки: вызов концентратора/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-214">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="34e7f-215">**Ошибки: всего транспортных**</span><span class="sxs-lookup"><span data-stu-id="34e7f-215">**Errors: Transport Total**</span></span>
- <span data-ttu-id="34e7f-216">**Ошибки: транспорт/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-216">**Errors: Transport/Sec**</span></span>

<span data-ttu-id="34e7f-217">**Метрики масштабирования**</span><span class="sxs-lookup"><span data-stu-id="34e7f-217">**Scaleout metrics**</span></span>

<span data-ttu-id="34e7f-218">Следующие метрики измеряют трафик и ошибки, созданные поставщиком масштабирования.</span><span class="sxs-lookup"><span data-stu-id="34e7f-218">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="34e7f-219">**Поток** в этом контексте — это единица масштабирования, используемая поставщиком масштабирования; Это таблица, если используется SQL Server, раздел, если используется служебная шина, и подписка, если используется Redis.</span><span class="sxs-lookup"><span data-stu-id="34e7f-219">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="34e7f-220">По умолчанию используется только один поток, но его можно увеличить с помощью настройки SQL Server и служебной шины.</span><span class="sxs-lookup"><span data-stu-id="34e7f-220">By default, only one stream is used, but this can be increased through configuration on SQL Server and Service Bus.</span></span> <span data-ttu-id="34e7f-221">Поток **буферизации** — это тот, который перешел в состояние сбоя. Если поток находится в состоянии сбоя, все сообщения, отправленные на объединительную плату, будут завершаться сбоем сразу, пока поток не завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="34e7f-221">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="34e7f-222">**Длина очереди отправки** — это количество сообщений, которые были отправлены, но еще не отправлены.</span><span class="sxs-lookup"><span data-stu-id="34e7f-222">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="34e7f-223">**Получено сообщений в канале масштабирования сообщений в секунду**</span><span class="sxs-lookup"><span data-stu-id="34e7f-223">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="34e7f-224">**Всего потоков масштабирования**</span><span class="sxs-lookup"><span data-stu-id="34e7f-224">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="34e7f-225">**Открытие потоков масштабирования**</span><span class="sxs-lookup"><span data-stu-id="34e7f-225">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="34e7f-226">**Буферизация потоков с масштабированием**</span><span class="sxs-lookup"><span data-stu-id="34e7f-226">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="34e7f-227">**Всего ошибок масштабирования**</span><span class="sxs-lookup"><span data-stu-id="34e7f-227">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="34e7f-228">**Ошибок масштабирования/с**</span><span class="sxs-lookup"><span data-stu-id="34e7f-228">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="34e7f-229">**Длина очереди отправки при увеличении**</span><span class="sxs-lookup"><span data-stu-id="34e7f-229">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="34e7f-230">Дополнительные сведения об измерении этих счетчиков см. в разделе [масштабирование SignalR с помощью служебной шины Azure](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="34e7f-230">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="34e7f-231">Использование других счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="34e7f-231">Using other performance counters</span></span>

<span data-ttu-id="34e7f-232">Следующие счетчики производительности также могут быть полезны при наблюдении за производительностью приложения.</span><span class="sxs-lookup"><span data-stu-id="34e7f-232">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="34e7f-233">**Память**</span><span class="sxs-lookup"><span data-stu-id="34e7f-233">**Memory**</span></span>

- <span data-ttu-id="34e7f-234">Память CLR .NET байт во всех кучах (для w3wp)</span><span class="sxs-lookup"><span data-stu-id="34e7f-234">.NET CLR Memory# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="34e7f-235">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="34e7f-235">**ASP.NET**</span></span>

- <span data-ttu-id="34e7f-236">Текущий ASP. NET \ запросов</span><span class="sxs-lookup"><span data-stu-id="34e7f-236">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="34e7f-237">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="34e7f-237">ASP.NET\Queued</span></span>
- <span data-ttu-id="34e7f-238">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="34e7f-238">ASP.NET\Rejected</span></span>

<span data-ttu-id="34e7f-239">**ЦП**</span><span class="sxs-lookup"><span data-stu-id="34e7f-239">**CPU**</span></span>

- <span data-ttu-id="34e7f-240">Время Информатион\процессор процессора</span><span class="sxs-lookup"><span data-stu-id="34e7f-240">Processor Information\Processor Time</span></span>

<span data-ttu-id="34e7f-241">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="34e7f-241">**TCP/IP**</span></span>

- <span data-ttu-id="34e7f-242">TCPv6/подключения установлены</span><span class="sxs-lookup"><span data-stu-id="34e7f-242">TCPv6/Connections Established</span></span>
- <span data-ttu-id="34e7f-243">TCPv4/подключения установлены</span><span class="sxs-lookup"><span data-stu-id="34e7f-243">TCPv4/Connections Established</span></span>

<span data-ttu-id="34e7f-244">**Веб-служба**</span><span class="sxs-lookup"><span data-stu-id="34e7f-244">**Web Service**</span></span>

- <span data-ttu-id="34e7f-245">Подключения к веб-служба \ текущих</span><span class="sxs-lookup"><span data-stu-id="34e7f-245">Web Service\Current Connections</span></span>
- <span data-ttu-id="34e7f-246">Подключения к веб-Сервице\максимум</span><span class="sxs-lookup"><span data-stu-id="34e7f-246">Web Service\Maximum Connections</span></span>

<span data-ttu-id="34e7f-247">**Работа с потоками**</span><span class="sxs-lookup"><span data-stu-id="34e7f-247">**Threading**</span></span>

- <span data-ttu-id="34e7f-248">LocksAndThreads CLR .NET\# из текущих логических потоков</span><span class="sxs-lookup"><span data-stu-id="34e7f-248">.NET CLR LocksAndThreads\# of current logical Threads</span></span>
- <span data-ttu-id="34e7f-249">Потоки Локксанд CLR .NET\# из текущих физических потоков</span><span class="sxs-lookup"><span data-stu-id="34e7f-249">.NET CLR LocksAnd Threads\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="34e7f-250">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="34e7f-250">Other Resources</span></span>

<span data-ttu-id="34e7f-251">Дополнительные сведения о мониторинге производительности ASP.NET и настройке см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="34e7f-251">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="34e7f-252">[Общие сведения о производительности ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="34e7f-252">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="34e7f-253">Использование потоков ASP.NET в IIS 7,5, IIS 7,0 и IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="34e7f-253">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="34e7f-254">Элемент &lt;applicationPool&gt; (веб-параметры)</span><span class="sxs-lookup"><span data-stu-id="34e7f-254">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
