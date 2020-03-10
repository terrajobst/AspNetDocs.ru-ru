---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: Включение трассировки SignalR | Документация Майкрософт
author: bradygaster
description: В этом документе описано, как включить и настроить трассировку для серверов и клиентов SignalR. Трассировка позволяет просматривать диагностические сведения о событиях...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467442"
---
# <a name="enabling-signalr-tracing"></a><span data-ttu-id="a9948-104">Включение трассировки SignalR</span><span class="sxs-lookup"><span data-stu-id="a9948-104">Enabling SignalR Tracing</span></span>

<span data-ttu-id="a9948-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a9948-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="a9948-106">В этом документе описано, как включить и настроить трассировку для серверов и клиентов SignalR.</span><span class="sxs-lookup"><span data-stu-id="a9948-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="a9948-107">Трассировка позволяет просматривать диагностические сведения о событиях в приложении SignalR.</span><span class="sxs-lookup"><span data-stu-id="a9948-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
>
> <span data-ttu-id="a9948-108">Этот раздел изначально был написан с помощью Патрик Флетчера.</span><span class="sxs-lookup"><span data-stu-id="a9948-108">This topic was originally written by Patrick Fletcher.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a9948-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="a9948-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="a9948-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a9948-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="a9948-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="a9948-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="a9948-112">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="a9948-112">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="a9948-113">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="a9948-113">Questions and comments</span></span>
>
> <span data-ttu-id="a9948-114">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a9948-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="a9948-115">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="a9948-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="a9948-116">Когда трассировка включена, приложение SignalR создает записи журнала для событий.</span><span class="sxs-lookup"><span data-stu-id="a9948-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="a9948-117">События можно регистрировать как из клиента, так и с сервера.</span><span class="sxs-lookup"><span data-stu-id="a9948-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="a9948-118">Трассировка на сервере регистрирует соединение, масштабируемый поставщик и события шины сообщений.</span><span class="sxs-lookup"><span data-stu-id="a9948-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="a9948-119">Трассировка на клиенте регистрирует события соединения.</span><span class="sxs-lookup"><span data-stu-id="a9948-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="a9948-120">В SignalR 2,1 и более поздних версиях трассировка на клиенте записывает в журнал полное содержимое сообщений о вызовах концентратора.</span><span class="sxs-lookup"><span data-stu-id="a9948-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="a9948-121">Содержимое</span><span class="sxs-lookup"><span data-stu-id="a9948-121">Contents</span></span>

- [<span data-ttu-id="a9948-122">Включение трассировки на сервере</span><span class="sxs-lookup"><span data-stu-id="a9948-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="a9948-123">Ведение журнала событий сервера в текстовые файлы</span><span class="sxs-lookup"><span data-stu-id="a9948-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="a9948-124">Ведение журнала событий сервера в журнале событий</span><span class="sxs-lookup"><span data-stu-id="a9948-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="a9948-125">Включение трассировки в клиенте .NET (классическое приложение для Windows)</span><span class="sxs-lookup"><span data-stu-id="a9948-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="a9948-126">Запись событий клиента настольных систем в консоль</span><span class="sxs-lookup"><span data-stu-id="a9948-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="a9948-127">Запись событий клиента рабочего стола в текстовый файл</span><span class="sxs-lookup"><span data-stu-id="a9948-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="a9948-128">Включение трассировки в клиентах Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="a9948-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="a9948-129">Ведение журнала Windows Phone событий клиента в пользовательском интерфейсе</span><span class="sxs-lookup"><span data-stu-id="a9948-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="a9948-130">Запись событий клиента Windows Phone в консоль отладки</span><span class="sxs-lookup"><span data-stu-id="a9948-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="a9948-131">Включение трассировки в клиенте JavaScript</span><span class="sxs-lookup"><span data-stu-id="a9948-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="a9948-132">Включение трассировки на сервере</span><span class="sxs-lookup"><span data-stu-id="a9948-132">Enabling tracing on the server</span></span>

<span data-ttu-id="a9948-133">Трассировка включается на сервере в файле конфигурации приложения (файл App. config или Web. config в зависимости от типа проекта). Укажите категории событий, которые необходимо заносить в журнал.</span><span class="sxs-lookup"><span data-stu-id="a9948-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="a9948-134">В файле конфигурации также указывается, следует ли записывать события в текстовый файл, в журнал событий Windows или в пользовательский журнал, используя реализацию [прослушивателя TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="a9948-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="a9948-135">К категориям событий сервера относятся следующие виды сообщений:</span><span class="sxs-lookup"><span data-stu-id="a9948-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="a9948-136">Источник</span><span class="sxs-lookup"><span data-stu-id="a9948-136">Source</span></span> | <span data-ttu-id="a9948-137">Сообщения</span><span class="sxs-lookup"><span data-stu-id="a9948-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="a9948-138">SignalR. Склмессажебус</span><span class="sxs-lookup"><span data-stu-id="a9948-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="a9948-139">Установка поставщика масштабирования шины сообщений SQL, события базы данных, ошибки и время ожидания</span><span class="sxs-lookup"><span data-stu-id="a9948-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="a9948-140">SignalR.ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="a9948-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="a9948-141">Создание раздела поставщика масштабирования служебной шины и события подписки, ошибок и сообщений</span><span class="sxs-lookup"><span data-stu-id="a9948-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="a9948-142">SignalR. Редисмессажебус</span><span class="sxs-lookup"><span data-stu-id="a9948-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="a9948-143">Redis, отключение и события ошибок для поставщика масштабирования.</span><span class="sxs-lookup"><span data-stu-id="a9948-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="a9948-144">SignalR. Скалеаутмессажебус</span><span class="sxs-lookup"><span data-stu-id="a9948-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="a9948-145">Масштабирование событий обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a9948-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="a9948-146">SignalR. транспорт. Вебсоккеттранспорт</span><span class="sxs-lookup"><span data-stu-id="a9948-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="a9948-147">Транспортное соединение WebSocket, отключение, Обмен сообщениями и события ошибок</span><span class="sxs-lookup"><span data-stu-id="a9948-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="a9948-148">SignalR. транспорт. Серверсентевентстранспорт</span><span class="sxs-lookup"><span data-stu-id="a9948-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="a9948-149">Серверсентевентс транспортное соединение, отключение, Обмен сообщениями и события ошибок</span><span class="sxs-lookup"><span data-stu-id="a9948-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="a9948-150">SignalR. транспорт. Фореверфраметранспорт</span><span class="sxs-lookup"><span data-stu-id="a9948-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="a9948-151">Фореверфраме транспортное соединение, отключение, Обмен сообщениями и события ошибок</span><span class="sxs-lookup"><span data-stu-id="a9948-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="a9948-152">SignalR.Transports.LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="a9948-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="a9948-153">Лонгполлинг транспортное соединение, отключение, Обмен сообщениями и события ошибок</span><span class="sxs-lookup"><span data-stu-id="a9948-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="a9948-154">SignalR.Transports.TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="a9948-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="a9948-155">Транспортные подключения, отключение и события KeepAlive</span><span class="sxs-lookup"><span data-stu-id="a9948-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="a9948-156">SignalR. Рефлектедхубдескрипторпровидер</span><span class="sxs-lookup"><span data-stu-id="a9948-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="a9948-157">События обнаружения концентратора</span><span class="sxs-lookup"><span data-stu-id="a9948-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="a9948-158">Ведение журнала событий сервера в текстовые файлы</span><span class="sxs-lookup"><span data-stu-id="a9948-158">Logging server events to text files</span></span>

<span data-ttu-id="a9948-159">В следующем коде показано, как включить трассировку для каждой категории события.</span><span class="sxs-lookup"><span data-stu-id="a9948-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="a9948-160">Этот пример настраивает приложение для записи событий в текстовые файлы.</span><span class="sxs-lookup"><span data-stu-id="a9948-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="a9948-161">**Код XML-сервера для включения трассировки**</span><span class="sxs-lookup"><span data-stu-id="a9948-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="a9948-162">В приведенном выше коде запись `SignalRSwitch` указывает значение [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) , используемое для событий, отправляемых в указанный журнал.</span><span class="sxs-lookup"><span data-stu-id="a9948-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="a9948-163">В этом случае для него задается значение `Verbose` что означает, что все сообщения отладки и трассировки записываются в журнал.</span><span class="sxs-lookup"><span data-stu-id="a9948-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="a9948-164">Следующие выходные данные показывают записи из файла `transports.log.txt` для приложения, в котором используется указанный выше файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a9948-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="a9948-165">В нем отображается новое подключение, удаленное подключение и события пульса передачи.</span><span class="sxs-lookup"><span data-stu-id="a9948-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="a9948-166">Ведение журнала событий сервера в журнале событий</span><span class="sxs-lookup"><span data-stu-id="a9948-166">Logging server events to the event log</span></span>

<span data-ttu-id="a9948-167">Чтобы регистрировать события в журнале событий, а не в текстовом файле, измените значения записей в узле `sharedListeners`.</span><span class="sxs-lookup"><span data-stu-id="a9948-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="a9948-168">В следующем коде показано, как регистрировать события сервера в журнале событий:</span><span class="sxs-lookup"><span data-stu-id="a9948-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="a9948-169">**Код XML-сервера для ведения журнала событий в журнале событий**</span><span class="sxs-lookup"><span data-stu-id="a9948-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="a9948-170">События регистрируются в журнале приложений и доступны через Просмотр событий, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="a9948-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![Просмотр событий отображения журналов SignalR](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="a9948-172">При использовании журнала событий установите для параметра **TraceLevel** значение **Error** , чтобы поддерживать Управление числом сообщений.</span><span class="sxs-lookup"><span data-stu-id="a9948-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="a9948-173">Включение трассировки в клиенте .NET (классическое приложение для Windows)</span><span class="sxs-lookup"><span data-stu-id="a9948-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="a9948-174">Клиент .NET может регистрировать события в консоли, текстовом файле или пользовательском журнале с помощью реализации [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9948-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="a9948-175">Чтобы включить ведение журнала в клиенте .NET, задайте для свойства `TraceLevel` соединения значение [трацелевелс](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) , а свойству `TraceWriter` — допустимый экземпляр [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a9948-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="a9948-176">Запись событий клиента настольных систем в консоль</span><span class="sxs-lookup"><span data-stu-id="a9948-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="a9948-177">В следующем C# коде показано, как регистрировать события в клиенте .NET на консоли.</span><span class="sxs-lookup"><span data-stu-id="a9948-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="a9948-178">Запись событий клиента рабочего стола в текстовый файл</span><span class="sxs-lookup"><span data-stu-id="a9948-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="a9948-179">В следующем C# коде показано, как регистрировать события в клиенте .NET в текстовом файле.</span><span class="sxs-lookup"><span data-stu-id="a9948-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="a9948-180">Следующие выходные данные показывают записи из файла `ClientLog.txt` для приложения, в котором используется указанный выше файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a9948-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="a9948-181">В нем отображается клиент, подключающийся к серверу, а в концентраторе вызывается клиентский метод с именем `addMessage`:</span><span class="sxs-lookup"><span data-stu-id="a9948-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="a9948-182">Включение трассировки в клиентах Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="a9948-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="a9948-183">Приложения SignalR для Windows Phoneных приложений используют один и тот же клиент .NET в качестве классических приложений, но [консоль. out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) и запись в файл с помощью [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) недоступны.</span><span class="sxs-lookup"><span data-stu-id="a9948-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="a9948-184">Вместо этого необходимо создать пользовательскую реализацию [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) для трассировки.</span><span class="sxs-lookup"><span data-stu-id="a9948-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span>

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="a9948-185">Ведение журнала Windows Phone событий клиента в пользовательском интерфейсе</span><span class="sxs-lookup"><span data-stu-id="a9948-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="a9948-186">[База кода SignalR](https://github.com/SignalR/SignalR/archive/master.zip) содержит Windows Phone пример, который записывает выходные данные трассировки в [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) с помощью пользовательской реализации [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) , именуемой `TextBlockWriter`.</span><span class="sxs-lookup"><span data-stu-id="a9948-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="a9948-187">Этот класс можно найти в проекте **Samples/Microsoft. AspNet. SignalR. Client. WP8. Samples** .</span><span class="sxs-lookup"><span data-stu-id="a9948-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="a9948-188">При создании экземпляра `TextBlockWriter`передайте текущий [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)и [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) , где будет создан [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) , используемый для вывода трассировки:</span><span class="sxs-lookup"><span data-stu-id="a9948-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="a9948-189">Затем выходные данные трассировки будут записаны в новый [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) , созданный в переданном [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a9948-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="a9948-190">Запись событий клиента Windows Phone в консоль отладки</span><span class="sxs-lookup"><span data-stu-id="a9948-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="a9948-191">Чтобы отправить выходные данные в консоль отладки, а не в пользовательский интерфейс, создайте реализацию [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) , которая выполняет запись в окно отладки, и назначьте ее свойству [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) соединения:</span><span class="sxs-lookup"><span data-stu-id="a9948-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="a9948-192">Данные трассировки будут записаны в окно отладки в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a9948-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="a9948-193">Включение трассировки в клиенте JavaScript</span><span class="sxs-lookup"><span data-stu-id="a9948-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="a9948-194">Чтобы включить ведение журнала на стороне клиента для соединения, задайте свойство `logging` объекта соединения перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="a9948-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="a9948-195">**Клиентский код JavaScript для включения трассировки в консоль браузера (с созданным прокси-сервером)**</span><span class="sxs-lookup"><span data-stu-id="a9948-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="a9948-196">**Клиентский код JavaScript для включения трассировки в консоль браузера (без созданного прокси-сервера)**</span><span class="sxs-lookup"><span data-stu-id="a9948-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="a9948-197">Когда трассировка включена, клиент JavaScript регистрирует события в консоли браузера.</span><span class="sxs-lookup"><span data-stu-id="a9948-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="a9948-198">Сведения о доступе к консоли браузера см. в разделе [мониторинг транспортов](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span><span class="sxs-lookup"><span data-stu-id="a9948-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="a9948-199">На следующем снимке экрана показан клиент на JavaScript SignalR с включенной трассировкой.</span><span class="sxs-lookup"><span data-stu-id="a9948-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="a9948-200">В консоли браузера отображаются события вызова подключения и концентратора:</span><span class="sxs-lookup"><span data-stu-id="a9948-200">It shows connection and hub invocation events in the browser console:</span></span>

![События трассировки SignalR в консоли браузера](enabling-signalr-tracing/_static/image4.png)
