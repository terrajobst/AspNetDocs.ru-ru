---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: Общие сведения о масштабировании в SignalR 1.x | Документация Майкрософт
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 04/29/2013
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 78e53c38ec760334cecee0431d52d993a657b908
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065541"
---
<a name="introduction-to-scaleout-in-signalr-1x"></a><span data-ttu-id="db1ea-102">Общие сведения о масштабировании в SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="db1ea-102">Introduction to Scaleout in SignalR 1.x</span></span>
====================
<span data-ttu-id="db1ea-103">по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="db1ea-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="db1ea-104">Вообще говоря, существует два способа масштабировать веб-приложения: *масштаба* и *горизонтальное масштабирование*.</span><span class="sxs-lookup"><span data-stu-id="db1ea-104">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="db1ea-105">Увеличить масштаб означает использование на больший сервер (или большего размера виртуальной Машины) с более ОЗУ, ЦП и т. д.</span><span class="sxs-lookup"><span data-stu-id="db1ea-105">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="db1ea-106">Горизонтальное масштабирование означает добавление дополнительных серверов для обработки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="db1ea-106">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="db1ea-107">Проблема с масштабированием в том, поспешно нажал ли ограничение на размер машины.</span><span class="sxs-lookup"><span data-stu-id="db1ea-107">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="db1ea-108">Кроме этого вам нужно масштабировать. Тем не менее при масштабировании, клиенты могут перенаправляться на разных серверах.</span><span class="sxs-lookup"><span data-stu-id="db1ea-108">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="db1ea-109">Клиент, который подключен к одному серверу не будет получать сообщения, отправленные с другого сервера.</span><span class="sxs-lookup"><span data-stu-id="db1ea-109">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="db1ea-110">Одним из решений является пересылки сообщений между серверами, используя компонент, называемый *объединительной платы*.</span><span class="sxs-lookup"><span data-stu-id="db1ea-110">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="db1ea-111">С задней панели, который включен каждый экземпляр приложения отправляет сообщения объединительной плате и задней панели перенаправляет их в другие экземпляры приложения.</span><span class="sxs-lookup"><span data-stu-id="db1ea-111">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="db1ea-112">(В области электроники, объединительной платы является группой parallel соединителей.</span><span class="sxs-lookup"><span data-stu-id="db1ea-112">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="db1ea-113">Используя аналогию объединительной панели SignalR подключает несколько серверов.)</span><span class="sxs-lookup"><span data-stu-id="db1ea-113">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="db1ea-114">SignalR в настоящее время предоставляет три расширения:</span><span class="sxs-lookup"><span data-stu-id="db1ea-114">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="db1ea-115">**Служебная шина Azure**.</span><span class="sxs-lookup"><span data-stu-id="db1ea-115">**Azure Service Bus**.</span></span> <span data-ttu-id="db1ea-116">Служебная шина — это инфраструктура обмена сообщениями, которая позволяет компонентам для отправки сообщений в слабо связанным образом.</span><span class="sxs-lookup"><span data-stu-id="db1ea-116">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="db1ea-117">**Redis**.</span><span class="sxs-lookup"><span data-stu-id="db1ea-117">**Redis**.</span></span> <span data-ttu-id="db1ea-118">Redis — это хранилище ключ значение в памяти.</span><span class="sxs-lookup"><span data-stu-id="db1ea-118">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="db1ea-119">Redis поддерживает шаблона публикации/подписки («pub/sub») для отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="db1ea-119">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="db1ea-120">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="db1ea-120">**SQL Server**.</span></span> <span data-ttu-id="db1ea-121">На задней стороне SQL Server записывает сообщения в таблицы SQL.</span><span class="sxs-lookup"><span data-stu-id="db1ea-121">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="db1ea-122">Задняя панель с компонентом Service Broker для эффективного обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="db1ea-122">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="db1ea-123">Тем не менее она также работает, если не включен компонент Service Broker.</span><span class="sxs-lookup"><span data-stu-id="db1ea-123">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="db1ea-124">Если вы развернете приложение в Azure, рассмотрите возможность использования на задней стороне служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="db1ea-124">If you deploy your application on Azure, consider using the Azure Service Bus backplane.</span></span> <span data-ttu-id="db1ea-125">Если развертываются на ферме серверов, рассмотрите возможность SQL Server или Redis соединительных панелях.</span><span class="sxs-lookup"><span data-stu-id="db1ea-125">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="db1ea-126">В следующих разделах содержатся пошаговые учебники по каждой объединительной платы:</span><span class="sxs-lookup"><span data-stu-id="db1ea-126">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="db1ea-127">Масштабирование SignalR с помощью служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="db1ea-127">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="db1ea-128">Масштабирование SignalR с помощью Redis</span><span class="sxs-lookup"><span data-stu-id="db1ea-128">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="db1ea-129">Масштабирование SignalR с помощью SQL Server</span><span class="sxs-lookup"><span data-stu-id="db1ea-129">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="db1ea-130">Реализация</span><span class="sxs-lookup"><span data-stu-id="db1ea-130">Implementation</span></span>

<span data-ttu-id="db1ea-131">В SignalR каждое сообщение отправляется через канал сообщений.</span><span class="sxs-lookup"><span data-stu-id="db1ea-131">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="db1ea-132">Реализует канал сообщений [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) интерфейс, который предоставляет абстракцию публикации/подписки.</span><span class="sxs-lookup"><span data-stu-id="db1ea-132">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="db1ea-133">Соединительных панелях работы, заменив значение по умолчанию **IMessageBus** с шиной предназначен для этой задней панели.</span><span class="sxs-lookup"><span data-stu-id="db1ea-133">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="db1ea-134">Например, канал сообщений для Redis является [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), и он использует Redis [pub/sub](http://redis.io/topics/pubsub) механизм для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="db1ea-134">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="db1ea-135">Каждый экземпляр сервера подключается к задней панели через шину.</span><span class="sxs-lookup"><span data-stu-id="db1ea-135">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="db1ea-136">При отправке сообщения, она переходит к задней панели и задней панели отправляет его на каждом сервере.</span><span class="sxs-lookup"><span data-stu-id="db1ea-136">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="db1ea-137">Если сервер получает сообщение от объединительной платы, он помещает сообщение в локальном кэше.</span><span class="sxs-lookup"><span data-stu-id="db1ea-137">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="db1ea-138">Затем сервер доставляет сообщения клиентам из своего локального кэша.</span><span class="sxs-lookup"><span data-stu-id="db1ea-138">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="db1ea-139">Для каждого клиентского соединения клиента выполняется в режиме чтения потока сообщений отслеживается с помощью курсора.</span><span class="sxs-lookup"><span data-stu-id="db1ea-139">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="db1ea-140">(Курсор представляет позицию в потоке сообщений). Если клиент отключается, а затем снова подключается, шина запрашивает все сообщения, полученные после значения курсора клиента.</span><span class="sxs-lookup"><span data-stu-id="db1ea-140">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="db1ea-141">То же самое происходит, когда соединение использует [долго опрашивающего](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="db1ea-141">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="db1ea-142">После выполнения запроса долгого опроса, клиент открывает новое подключение и запрашивает сообщения, полученные после курсора.</span><span class="sxs-lookup"><span data-stu-id="db1ea-142">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="db1ea-143">Работает механизм курсора, даже если клиент направляется на другой сервер, на переподключение.</span><span class="sxs-lookup"><span data-stu-id="db1ea-143">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="db1ea-144">Задняя панель учитывает всех серверов, и неважно, какой сервер, клиент подключается к.</span><span class="sxs-lookup"><span data-stu-id="db1ea-144">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="db1ea-145">Ограничения</span><span class="sxs-lookup"><span data-stu-id="db1ea-145">Limitations</span></span>

<span data-ttu-id="db1ea-146">Использование объединительной платы, пропускная способность максимальное сообщений является ниже, чем это, когда клиенты напрямую обмениваться данными с одного сервера узла.</span><span class="sxs-lookup"><span data-stu-id="db1ea-146">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="db1ea-147">Том, что задней панели перенаправляет каждое сообщение на каждый узел, поэтому задней панели может стать узким местом.</span><span class="sxs-lookup"><span data-stu-id="db1ea-147">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="db1ea-148">Является ли это ограничение проблемы зависит от приложения.</span><span class="sxs-lookup"><span data-stu-id="db1ea-148">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="db1ea-149">Например Вот несколько типичных сценариев, SignalR.</span><span class="sxs-lookup"><span data-stu-id="db1ea-149">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="db1ea-150">[Рассылка сервера](tutorial-server-broadcast-with-aspnet-signalr.md) (например, биржевые сводки): Соединительных панелях хорошо подходят для этого сценария, так как сервер определяет скорость, с которой отправляются сообщения.</span><span class="sxs-lookup"><span data-stu-id="db1ea-150">[Server broadcast](tutorial-server-broadcast-with-aspnet-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="db1ea-151">[Клиент клиент](tutorial-getting-started-with-signalr.md) (например, чат): В этом случае задней панели может быть узким местом, если количество сообщений, масштабируется с количеством клиентов; то есть если увеличивается число сообщений, присоединить пропорционально как можно большего числа клиентов.</span><span class="sxs-lookup"><span data-stu-id="db1ea-151">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="db1ea-152">[В реальном времени высокой частотой](tutorial-high-frequency-realtime-with-signalr.md) (например, в режиме реального времени игры): Задняя панель не рекомендуется для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="db1ea-152">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="db1ea-153">Включение трассировки для масштабирование SignalR</span><span class="sxs-lookup"><span data-stu-id="db1ea-153">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="db1ea-154">Чтобы включить трассировку для соединительных панелях, добавьте следующие разделы в файл web.config в корне **конфигурации** элемент:</span><span class="sxs-lookup"><span data-stu-id="db1ea-154">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]