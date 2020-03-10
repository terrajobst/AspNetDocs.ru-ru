---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: Сопоставление пользователей SignalR с подключениями | Документация Майкрософт
author: bradygaster
description: В этом разделе показано, как хранить сведения о пользователях и их подключениях. Патрик Флетчера помогло написать этот раздел. Версии программного обеспечения, используемые в этом разделе...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431394"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="1e210-105">Сопоставление пользователей SignalR с подключениями</span><span class="sxs-lookup"><span data-stu-id="1e210-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="1e210-106">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1e210-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="1e210-107">В этом разделе показано, как хранить сведения о пользователях и их подключениях.</span><span class="sxs-lookup"><span data-stu-id="1e210-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="1e210-108">Патрик Флетчера помогло написать этот раздел.</span><span class="sxs-lookup"><span data-stu-id="1e210-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="1e210-109">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="1e210-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="1e210-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="1e210-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="1e210-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="1e210-111">.NET 4.5</span></span>
> - <span data-ttu-id="1e210-112">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="1e210-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="1e210-113">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="1e210-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="1e210-114">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="1e210-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="1e210-115">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="1e210-115">Questions and comments</span></span>
>
> <span data-ttu-id="1e210-116">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="1e210-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="1e210-117">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="1e210-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="1e210-118">Введение</span><span class="sxs-lookup"><span data-stu-id="1e210-118">Introduction</span></span>

<span data-ttu-id="1e210-119">Каждый клиент, подключающийся к концентратору, передает уникальный идентификатор соединения. Это значение можно получить в свойстве `Context.ConnectionId` контекста концентратора.</span><span class="sxs-lookup"><span data-stu-id="1e210-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="1e210-120">Если приложению необходимо сопоставить пользователя с идентификатором подключения и сохранить это сопоставление, можно использовать один из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="1e210-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="1e210-121">Поставщик ИДЕНТИФИКАТОРов пользователей (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="1e210-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="1e210-122">[Хранилище в памяти](#inmemory), например словарь</span><span class="sxs-lookup"><span data-stu-id="1e210-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="1e210-123">Группа SignalR для каждого пользователя</span><span class="sxs-lookup"><span data-stu-id="1e210-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="1e210-124">[Постоянное внешнее хранилище](#database), например таблица базы данных или хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="1e210-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="1e210-125">Каждая из этих реализаций показана в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="1e210-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="1e210-126">Для наблюдения за состоянием подключения пользователя используются методы `OnConnected`, `OnDisconnected`и `OnReconnected` класса `Hub`.</span><span class="sxs-lookup"><span data-stu-id="1e210-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="1e210-127">Оптимальный подход для вашего приложения зависит от следующих факторов.</span><span class="sxs-lookup"><span data-stu-id="1e210-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="1e210-128">Число веб-серверов, на которых размещено приложение.</span><span class="sxs-lookup"><span data-stu-id="1e210-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="1e210-129">Требуется ли получить список подключенных в данный момент пользователей.</span><span class="sxs-lookup"><span data-stu-id="1e210-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="1e210-130">Необходимость сохранения сведений о группах и пользователях при перезапуске приложения или сервера.</span><span class="sxs-lookup"><span data-stu-id="1e210-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="1e210-131">Является ли причиной проблемы задержка вызова внешнего сервера.</span><span class="sxs-lookup"><span data-stu-id="1e210-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="1e210-132">В следующей таблице показано, какой подход подходит для этих вопросов.</span><span class="sxs-lookup"><span data-stu-id="1e210-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="1e210-133">Более одного сервера</span><span class="sxs-lookup"><span data-stu-id="1e210-133">More than one server</span></span> | <span data-ttu-id="1e210-134">Получение списка подключенных в данный момент пользователей</span><span class="sxs-lookup"><span data-stu-id="1e210-134">Get list of currently connected users</span></span> | <span data-ttu-id="1e210-135">Сохранять сведения после перезагрузки</span><span class="sxs-lookup"><span data-stu-id="1e210-135">Persist information after restarts</span></span> | <span data-ttu-id="1e210-136">Оптимальная производительность</span><span class="sxs-lookup"><span data-stu-id="1e210-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="1e210-137">Поставщик UserID</span><span class="sxs-lookup"><span data-stu-id="1e210-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="1e210-138">В памяти</span><span class="sxs-lookup"><span data-stu-id="1e210-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="1e210-139">Группы с одним пользователем</span><span class="sxs-lookup"><span data-stu-id="1e210-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="1e210-140">Постоянный, внешний</span><span class="sxs-lookup"><span data-stu-id="1e210-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="1e210-141">Поставщик Иусерид</span><span class="sxs-lookup"><span data-stu-id="1e210-141">IUserID provider</span></span>

<span data-ttu-id="1e210-142">Эта функция позволяет пользователям указать, какой идентификатор userId основан на IRequest с помощью нового интерфейса Иусеридпровидер.</span><span class="sxs-lookup"><span data-stu-id="1e210-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="1e210-143">**Иусеридпровидер**</span><span class="sxs-lookup"><span data-stu-id="1e210-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="1e210-144">По умолчанию будет использоваться реализация, которая использует `IPrincipal.Identity.Name` пользователя в качестве имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e210-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="1e210-145">Чтобы изменить это, зарегистрируйте свою реализацию `IUserIdProvider` с помощью глобального узла при запуске приложения:</span><span class="sxs-lookup"><span data-stu-id="1e210-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="1e210-146">В центре вы сможете отправить сообщения этим пользователям через следующий API:</span><span class="sxs-lookup"><span data-stu-id="1e210-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="1e210-147">**Отправка сообщения определенному пользователю**</span><span class="sxs-lookup"><span data-stu-id="1e210-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="1e210-148">Хранилище в памяти</span><span class="sxs-lookup"><span data-stu-id="1e210-148">In-memory storage</span></span>

<span data-ttu-id="1e210-149">В следующих примерах показано, как сохранить данные соединения и пользователя в словаре, который хранится в памяти.</span><span class="sxs-lookup"><span data-stu-id="1e210-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="1e210-150">Словарь использует `HashSet` для хранения идентификатора соединения. В любой момент времени у пользователя может быть несколько подключений к приложению SignalR.</span><span class="sxs-lookup"><span data-stu-id="1e210-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="1e210-151">Например, пользователь, который подключен через несколько устройств или несколько вкладок браузера, может иметь несколько идентификаторов подключения.</span><span class="sxs-lookup"><span data-stu-id="1e210-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="1e210-152">Если приложение завершает работу, вся информация теряется, но будет повторно заполнена при повторной установке подключений пользователями.</span><span class="sxs-lookup"><span data-stu-id="1e210-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="1e210-153">Хранилище в памяти не работает, если в вашей среде имеется несколько веб-серверов, поскольку каждый сервер будет иметь отдельную коллекцию подключений.</span><span class="sxs-lookup"><span data-stu-id="1e210-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="1e210-154">В первом примере показан класс, который управляет сопоставлением пользователей с соединениями.</span><span class="sxs-lookup"><span data-stu-id="1e210-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="1e210-155">Ключом для хэширования будет имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e210-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="1e210-156">В следующем примере показано, как использовать класс сопоставления соединения из концентратора.</span><span class="sxs-lookup"><span data-stu-id="1e210-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="1e210-157">Экземпляр класса хранится в имени переменной `_connections`.</span><span class="sxs-lookup"><span data-stu-id="1e210-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="1e210-158">Группы с одним пользователем</span><span class="sxs-lookup"><span data-stu-id="1e210-158">Single-user groups</span></span>

<span data-ttu-id="1e210-159">Вы можете создать группу для каждого пользователя, а затем отправить сообщение в эту группу, когда хотите обратиться только к этому пользователю.</span><span class="sxs-lookup"><span data-stu-id="1e210-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="1e210-160">Имя каждой группы является именем пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e210-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="1e210-161">Если пользователь имеет более одного подключения, каждый идентификатор подключения добавляется в группу пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e210-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="1e210-162">Не следует удалять вручную пользователя из группы при отключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e210-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="1e210-163">Это действие автоматически выполняется платформой SignalR.</span><span class="sxs-lookup"><span data-stu-id="1e210-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="1e210-164">В следующем примере показано, как реализовать однопользовательскую группу.</span><span class="sxs-lookup"><span data-stu-id="1e210-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="1e210-165">Постоянное внешнее хранилище</span><span class="sxs-lookup"><span data-stu-id="1e210-165">Permanent, external storage</span></span>

<span data-ttu-id="1e210-166">В этом разделе показано, как использовать базу данных или хранилище таблиц Azure для хранения сведений о соединении.</span><span class="sxs-lookup"><span data-stu-id="1e210-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="1e210-167">Этот подход работает при наличии нескольких веб-серверов, поскольку каждый веб-сервер может взаимодействовать с одним и тем же репозиторием данных.</span><span class="sxs-lookup"><span data-stu-id="1e210-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="1e210-168">Если веб-серверы не работают или приложение перезапускается, метод `OnDisconnected` не вызывается.</span><span class="sxs-lookup"><span data-stu-id="1e210-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="1e210-169">Таким образом, в репозитории данных могут быть записи для идентификаторов соединений, которые больше не действительны.</span><span class="sxs-lookup"><span data-stu-id="1e210-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="1e210-170">Чтобы очистить эти потерянные записи, может потребоваться сделать недействительным любое подключение, созданное за пределами времени, относящегося к вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="1e210-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="1e210-171">Примеры в этом разделе включают значение для отслеживания при создании соединения, но не показывают, как очищать старые записи, так как это может потребоваться в качестве фонового процесса.</span><span class="sxs-lookup"><span data-stu-id="1e210-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="1e210-172">База данных</span><span class="sxs-lookup"><span data-stu-id="1e210-172">Database</span></span>

<span data-ttu-id="1e210-173">В следующих примерах показано, как хранить соединения и сведения о пользователях в базе данных.</span><span class="sxs-lookup"><span data-stu-id="1e210-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="1e210-174">Можно использовать любую технологию доступа к данным. Однако в приведенном ниже примере показано, как определить модели с помощью Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="1e210-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="1e210-175">Эти модели сущностей соответствуют таблицам и полям базы данных.</span><span class="sxs-lookup"><span data-stu-id="1e210-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="1e210-176">Структура данных может значительно варьироваться в зависимости от требований приложения.</span><span class="sxs-lookup"><span data-stu-id="1e210-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="1e210-177">В первом примере показано, как определить сущность пользователя, которая может быть связана с множеством сущностей соединения.</span><span class="sxs-lookup"><span data-stu-id="1e210-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="1e210-178">Затем из центра можно отвести отслеживание состояния каждого подключения с помощью приведенного ниже кода.</span><span class="sxs-lookup"><span data-stu-id="1e210-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="1e210-179">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="1e210-179">Azure table storage</span></span>

<span data-ttu-id="1e210-180">Следующий пример хранилища таблиц Azure похож на пример базы данных.</span><span class="sxs-lookup"><span data-stu-id="1e210-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="1e210-181">Она не включает все сведения, необходимые для начала работы со службой хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="1e210-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="1e210-182">Дополнительные сведения см. [в статье Использование табличного хранилища из .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="1e210-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="1e210-183">В следующем примере показана сущность таблицы для хранения сведений о соединении.</span><span class="sxs-lookup"><span data-stu-id="1e210-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="1e210-184">Он разделяет данные по имени пользователя и определяет каждую сущность по идентификатору соединения, чтобы пользователь мог в любое время иметь несколько подключений.</span><span class="sxs-lookup"><span data-stu-id="1e210-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="1e210-185">В центре вы следите за состоянием подключения каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e210-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
