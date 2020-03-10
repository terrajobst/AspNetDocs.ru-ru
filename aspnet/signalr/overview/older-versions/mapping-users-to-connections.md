---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: Сопоставление пользователей SignalR с подключениями в SignalR 1. x | Документация Майкрософт
author: bradygaster
description: В этом разделе показано, как хранить сведения о пользователях и их подключениях.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9d948495e9b8821fcb465611b6926603c3756a19
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450000"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="ff7d5-103">Сопоставление пользователей SignalR с подключениями в SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="ff7d5-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>

<span data-ttu-id="ff7d5-104">[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ff7d5-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ff7d5-105">В этом разделе показано, как хранить сведения о пользователях и их подключениях.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-105">This topic shows how to retain information about users and their connections.</span></span>

## <a name="introduction"></a><span data-ttu-id="ff7d5-106">Введение</span><span class="sxs-lookup"><span data-stu-id="ff7d5-106">Introduction</span></span>

<span data-ttu-id="ff7d5-107">Каждый клиент, подключающийся к концентратору, передает уникальный идентификатор соединения. Это значение можно получить в свойстве `Context.ConnectionId` контекста концентратора.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="ff7d5-108">Если приложению необходимо сопоставить пользователя с идентификатором подключения и сохранить это сопоставление, можно использовать один из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="ff7d5-109">[Хранилище в памяти](#inmemory), например словарь</span><span class="sxs-lookup"><span data-stu-id="ff7d5-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="ff7d5-110">Группа SignalR для каждого пользователя</span><span class="sxs-lookup"><span data-stu-id="ff7d5-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="ff7d5-111">[Постоянное внешнее хранилище](#database), например таблица базы данных или хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="ff7d5-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="ff7d5-112">Каждая из этих реализаций показана в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="ff7d5-113">Для наблюдения за состоянием подключения пользователя используются методы `OnConnected`, `OnDisconnected`и `OnReconnected` класса `Hub`.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="ff7d5-114">Оптимальный подход для вашего приложения зависит от следующих факторов.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="ff7d5-115">Число веб-серверов, на которых размещено приложение.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="ff7d5-116">Требуется ли получить список подключенных в данный момент пользователей.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="ff7d5-117">Необходимость сохранения сведений о группах и пользователях при перезапуске приложения или сервера.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="ff7d5-118">Является ли причиной проблемы задержка вызова внешнего сервера.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="ff7d5-119">В следующей таблице показано, какой подход подходит для этих вопросов.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="ff7d5-120">Более одного сервера</span><span class="sxs-lookup"><span data-stu-id="ff7d5-120">More than one server</span></span> | <span data-ttu-id="ff7d5-121">Получение списка подключенных в данный момент пользователей</span><span class="sxs-lookup"><span data-stu-id="ff7d5-121">Get list of currently connected users</span></span> | <span data-ttu-id="ff7d5-122">Сохранять сведения после перезагрузки</span><span class="sxs-lookup"><span data-stu-id="ff7d5-122">Persist information after restarts</span></span> | <span data-ttu-id="ff7d5-123">Оптимальная производительность</span><span class="sxs-lookup"><span data-stu-id="ff7d5-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ff7d5-124">В памяти</span><span class="sxs-lookup"><span data-stu-id="ff7d5-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="ff7d5-125">Группы с одним пользователем</span><span class="sxs-lookup"><span data-stu-id="ff7d5-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="ff7d5-126">Постоянный, внешний</span><span class="sxs-lookup"><span data-stu-id="ff7d5-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="ff7d5-127">Хранилище в памяти</span><span class="sxs-lookup"><span data-stu-id="ff7d5-127">In-memory storage</span></span>

<span data-ttu-id="ff7d5-128">В следующих примерах показано, как сохранить данные соединения и пользователя в словаре, который хранится в памяти.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="ff7d5-129">Словарь использует `HashSet` для хранения идентификатора соединения. В любой момент времени у пользователя может быть несколько подключений к приложению SignalR.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="ff7d5-130">Например, пользователь, который подключен через несколько устройств или несколько вкладок браузера, может иметь несколько идентификаторов подключения.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="ff7d5-131">Если приложение завершает работу, вся информация теряется, но будет повторно заполнена при повторной установке подключений пользователями.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="ff7d5-132">Хранилище в памяти не работает, если в вашей среде имеется несколько веб-серверов, поскольку каждый сервер будет иметь отдельную коллекцию подключений.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="ff7d5-133">В первом примере показан класс, который управляет сопоставлением пользователей с соединениями.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="ff7d5-134">Ключом для хэширования будет имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="ff7d5-135">В следующем примере показано, как использовать класс сопоставления соединения из концентратора.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="ff7d5-136">Экземпляр класса хранится в имени переменной `_connections`.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="ff7d5-137">Группы с одним пользователем</span><span class="sxs-lookup"><span data-stu-id="ff7d5-137">Single-user groups</span></span>

<span data-ttu-id="ff7d5-138">Вы можете создать группу для каждого пользователя, а затем отправить сообщение в эту группу, когда хотите обратиться только к этому пользователю.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="ff7d5-139">Имя каждой группы является именем пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="ff7d5-140">Если пользователь имеет более одного подключения, каждый идентификатор подключения добавляется в группу пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="ff7d5-141">Не следует удалять вручную пользователя из группы при отключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="ff7d5-142">Это действие автоматически выполняется платформой SignalR.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="ff7d5-143">В следующем примере показано, как реализовать однопользовательскую группу.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="ff7d5-144">Постоянное внешнее хранилище</span><span class="sxs-lookup"><span data-stu-id="ff7d5-144">Permanent, external storage</span></span>

<span data-ttu-id="ff7d5-145">В этом разделе показано, как использовать базу данных или хранилище таблиц Azure для хранения сведений о соединении.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="ff7d5-146">Этот подход работает при наличии нескольких веб-серверов, поскольку каждый веб-сервер может взаимодействовать с одним и тем же репозиторием данных.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="ff7d5-147">Если веб-серверы не работают или приложение перезапускается, метод `OnDisconnected` не вызывается.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="ff7d5-148">Таким образом, в репозитории данных могут быть записи для идентификаторов соединений, которые больше не действительны.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="ff7d5-149">Чтобы очистить эти потерянные записи, может потребоваться сделать недействительным любое подключение, созданное за пределами времени, относящегося к вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="ff7d5-150">Примеры в этом разделе включают значение для отслеживания при создании соединения, но не показывают, как очищать старые записи, так как это может потребоваться в качестве фонового процесса.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="ff7d5-151">База данных</span><span class="sxs-lookup"><span data-stu-id="ff7d5-151">Database</span></span>

<span data-ttu-id="ff7d5-152">В следующих примерах показано, как хранить соединения и сведения о пользователях в базе данных.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="ff7d5-153">Можно использовать любую технологию доступа к данным. Однако в приведенном ниже примере показано, как определить модели с помощью Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="ff7d5-154">Эти модели сущностей соответствуют таблицам и полям базы данных.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="ff7d5-155">Структура данных может значительно варьироваться в зависимости от требований приложения.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="ff7d5-156">В первом примере показано, как определить сущность пользователя, которая может быть связана с множеством сущностей соединения.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="ff7d5-157">Затем из центра можно отвести отслеживание состояния каждого подключения с помощью приведенного ниже кода.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="ff7d5-158">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="ff7d5-158">Azure table storage</span></span>

<span data-ttu-id="ff7d5-159">Следующий пример хранилища таблиц Azure похож на пример базы данных.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="ff7d5-160">Она не включает все сведения, необходимые для начала работы со службой хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="ff7d5-161">Дополнительные сведения см. [в статье Использование табличного хранилища из .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="ff7d5-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="ff7d5-162">В следующем примере показана сущность таблицы для хранения сведений о соединении.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="ff7d5-163">Он разделяет данные по имени пользователя и определяет каждую сущность по идентификатору соединения, чтобы пользователь мог в любое время иметь несколько подключений.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="ff7d5-164">В центре вы следите за состоянием подключения каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff7d5-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
