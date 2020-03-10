---
uid: signalr/overview/older-versions/working-with-groups
title: Работа с группами в SignalR 1. x | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как сохранять сведения о членстве в группах с помощью API концентратора.
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467898"
---
# <a name="working-with-groups-in-signalr-1x"></a><span data-ttu-id="3081e-103">Работа с группами в SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="3081e-103">Working with Groups in SignalR 1.x</span></span>

<span data-ttu-id="3081e-104">[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3081e-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="3081e-105">В этом разделе описывается добавление пользователей в группы и сохранение сведений о членстве в группах.</span><span class="sxs-lookup"><span data-stu-id="3081e-105">This topic describes how to add users to groups and persist group membership information.</span></span>

## <a name="overview"></a><span data-ttu-id="3081e-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="3081e-106">Overview</span></span>

<span data-ttu-id="3081e-107">Группы в SignalR предоставляют метод для вещания сообщений в указанные подмножества подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="3081e-107">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="3081e-108">Группа может иметь любое количество клиентов, а клиент может быть членом любого числа групп.</span><span class="sxs-lookup"><span data-stu-id="3081e-108">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="3081e-109">Вам не нужно явно создавать группы.</span><span class="sxs-lookup"><span data-stu-id="3081e-109">You don't have to explicitly create groups.</span></span> <span data-ttu-id="3081e-110">По сути, группа создается автоматически при первом указании имени в вызове Groups. Add и удаляется при удалении последнего подключения из членства в нем.</span><span class="sxs-lookup"><span data-stu-id="3081e-110">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="3081e-111">Общие сведения об использовании групп см. в разделе [Управление членством в группах из класса Hub](index.md) руководства по API концентраторов.</span><span class="sxs-lookup"><span data-stu-id="3081e-111">For an introduction to using groups, see [How to manage group membership from the Hub class](index.md) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="3081e-112">Отсутствует API для получения списка членства в группе или списка групп.</span><span class="sxs-lookup"><span data-stu-id="3081e-112">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="3081e-113">SignalR отправляет сообщения клиентам и группам, основанным на модели публикации и подтипа, а сервер не поддерживает списки групп или членства в группах.</span><span class="sxs-lookup"><span data-stu-id="3081e-113">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="3081e-114">Это обеспечивает максимальную масштабируемость, так как при добавлении узла в веб-ферму любое состояние, которое обслуживает SignalR, должно быть распространено на новый узел.</span><span class="sxs-lookup"><span data-stu-id="3081e-114">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="3081e-115">При добавлении пользователя в группу с помощью метода `Groups.Add` пользователь получает сообщения, направленные в эту группу, на время текущего соединения, но членство пользователя в этой группе не сохраняется за пределами текущего соединения.</span><span class="sxs-lookup"><span data-stu-id="3081e-115">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="3081e-116">Если вы хотите постоянно сохранять сведения о группах и членстве в группах, эти данные необходимо хранить в репозитории, например в базе данных или в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="3081e-116">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="3081e-117">Затем каждый раз, когда пользователь подключается к вашему приложению, вы получаете из репозитория, в который входит пользователь, и вручную добавляете этого пользователя в эти группы.</span><span class="sxs-lookup"><span data-stu-id="3081e-117">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="3081e-118">При повторном подключении после временного перерыва пользователь автоматически повторно присоединяется к ранее назначенным группам.</span><span class="sxs-lookup"><span data-stu-id="3081e-118">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="3081e-119">Автоматическое пересоединение группы применяется только при повторном подключении, а не при установке нового соединения.</span><span class="sxs-lookup"><span data-stu-id="3081e-119">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="3081e-120">Маркер с цифровой подписью передается из клиента, содержащего список ранее назначенных групп.</span><span class="sxs-lookup"><span data-stu-id="3081e-120">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="3081e-121">Если необходимо проверить, относится ли пользователь к запрошенным группам, можно переопределить поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3081e-121">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="3081e-122">Этот раздел включает следующие подразделы:</span><span class="sxs-lookup"><span data-stu-id="3081e-122">This topic includes the following sections:</span></span>

- [<span data-ttu-id="3081e-123">Добавление и удаление пользователей</span><span class="sxs-lookup"><span data-stu-id="3081e-123">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="3081e-124">Вызов членов группы</span><span class="sxs-lookup"><span data-stu-id="3081e-124">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="3081e-125">Хранение членства в группе в базе данных</span><span class="sxs-lookup"><span data-stu-id="3081e-125">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="3081e-126">Хранение членства в группах в хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="3081e-126">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="3081e-127">Проверка членства в группе при повторном подключении</span><span class="sxs-lookup"><span data-stu-id="3081e-127">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="3081e-128">Добавление и удаление пользователей</span><span class="sxs-lookup"><span data-stu-id="3081e-128">Adding and removing users</span></span>

<span data-ttu-id="3081e-129">Чтобы добавить или удалить пользователей из группы, вызовите методы [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) или [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) и передайте в качестве параметров идентификатор подключения пользователя и имя группы.</span><span class="sxs-lookup"><span data-stu-id="3081e-129">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="3081e-130">При завершении соединения не требуется вручную удалять пользователя из группы.</span><span class="sxs-lookup"><span data-stu-id="3081e-130">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="3081e-131">В следующем примере показаны методы `Groups.Add` и `Groups.Remove`, используемые в методах концентратора.</span><span class="sxs-lookup"><span data-stu-id="3081e-131">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="3081e-132">Методы `Groups.Add` и `Groups.Remove` выполняются асинхронно.</span><span class="sxs-lookup"><span data-stu-id="3081e-132">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="3081e-133">Если вы хотите добавить клиент в группу и сразу же отправить сообщение клиенту с помощью группы, необходимо убедиться в том, что метод Groups. Add завершается первым.</span><span class="sxs-lookup"><span data-stu-id="3081e-133">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="3081e-134">В следующих примерах кода показано, как это сделать, используя код, который работает в .NET 4,5, а другой — с помощью кода, который работает в .NET 4.</span><span class="sxs-lookup"><span data-stu-id="3081e-134">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4.</span></span>

#### <a name="asynchronous-net-45-example"></a><span data-ttu-id="3081e-135">Пример асинхронного .NET 4,5</span><span class="sxs-lookup"><span data-stu-id="3081e-135">Asynchronous .NET 4.5 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a><span data-ttu-id="3081e-136">Пример асинхронного .NET 4</span><span class="sxs-lookup"><span data-stu-id="3081e-136">Asynchronous .NET 4 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

<span data-ttu-id="3081e-137">В общем случае не следует включать `await` при вызове метода `Groups.Remove`, так как идентификатор подключения, который вы пытаетесь удалить, может больше не быть доступен.</span><span class="sxs-lookup"><span data-stu-id="3081e-137">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="3081e-138">В этом случае `TaskCanceledException` создается после истечения времени ожидания запроса. Если приложение должно гарантировать, что пользователь был удален из группы перед отправкой сообщения в группу, можно добавить `await` перед группами. Удалите, а затем перехватите исключение `TaskCanceledException`, которое может быть выдано.</span><span class="sxs-lookup"><span data-stu-id="3081e-138">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before Groups.Remove, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="3081e-139">Вызов членов группы</span><span class="sxs-lookup"><span data-stu-id="3081e-139">Calling members of a group</span></span>

<span data-ttu-id="3081e-140">Можно отправить сообщения всем членам группы или только указанным членам группы, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="3081e-140">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="3081e-141">**Все** подключенные клиенты в указанной группе.</span><span class="sxs-lookup"><span data-stu-id="3081e-141">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- <span data-ttu-id="3081e-142">Все подключенные клиенты в указанной группе, **за исключением указанных клиентов**, идентифицируемые по идентификатору соединения.</span><span class="sxs-lookup"><span data-stu-id="3081e-142">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- <span data-ttu-id="3081e-143">Все подключенные клиенты в указанной группе, **Кроме вызывающего клиента**.</span><span class="sxs-lookup"><span data-stu-id="3081e-143">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="3081e-144">Хранение членства в группе в базе данных</span><span class="sxs-lookup"><span data-stu-id="3081e-144">Storing group membership in a database</span></span>

<span data-ttu-id="3081e-145">В следующих примерах показано, как хранить сведения о группах и пользователях в базе данных.</span><span class="sxs-lookup"><span data-stu-id="3081e-145">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="3081e-146">Можно использовать любую технологию доступа к данным. Однако в приведенном ниже примере показано, как определить модели с помощью Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="3081e-146">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="3081e-147">Эти модели сущностей соответствуют таблицам и полям базы данных.</span><span class="sxs-lookup"><span data-stu-id="3081e-147">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="3081e-148">Структура данных может значительно варьироваться в зависимости от требований приложения.</span><span class="sxs-lookup"><span data-stu-id="3081e-148">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="3081e-149">Этот пример включает класс с именем `ConversationRoom`, который будет уникальным для приложения, позволяющего пользователям присоединяться к беседам по различным темам, таким как спорт или садом.</span><span class="sxs-lookup"><span data-stu-id="3081e-149">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="3081e-150">Этот пример также включает класс для соединений.</span><span class="sxs-lookup"><span data-stu-id="3081e-150">This example also includes a class for the connections.</span></span> <span data-ttu-id="3081e-151">Класс Connection не является абсолютно необходимым для отслеживания членства в группах, но часто является частью надежного решения для отслеживания пользователей.</span><span class="sxs-lookup"><span data-stu-id="3081e-151">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<span data-ttu-id="3081e-152">Затем в центре можно получить сведения о группах и пользователях из базы данных и вручную добавить пользователя в соответствующие группы.</span><span class="sxs-lookup"><span data-stu-id="3081e-152">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="3081e-153">В примере не содержится код для отслеживания пользовательских соединений.</span><span class="sxs-lookup"><span data-stu-id="3081e-153">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="3081e-154">В этом примере ключевое слово `await` не применяется перед `Groups.Add`, так как сообщение не отправляется сразу членам группы.</span><span class="sxs-lookup"><span data-stu-id="3081e-154">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="3081e-155">Если вы хотите отправить сообщение всем членам группы сразу после добавления нового члена, необходимо применить ключевое слово `await`, чтобы убедиться, что асинхронная операция завершена.</span><span class="sxs-lookup"><span data-stu-id="3081e-155">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="3081e-156">Хранение членства в группах в хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="3081e-156">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="3081e-157">Использование хранилища таблиц Azure для хранения данных группы и пользователя аналогично использованию базы данных.</span><span class="sxs-lookup"><span data-stu-id="3081e-157">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="3081e-158">В следующем примере показана сущность таблицы, в которой хранится имя пользователя и имя группы.</span><span class="sxs-lookup"><span data-stu-id="3081e-158">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<span data-ttu-id="3081e-159">В центре вы получаете назначенные группы при подключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="3081e-159">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="3081e-160">Проверка членства в группе при повторном подключении</span><span class="sxs-lookup"><span data-stu-id="3081e-160">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="3081e-161">По умолчанию SignalR автоматически переназначит пользователя соответствующим группам при повторном подключении из временного перерыва, например при удалении и повторном установлении соединения до истечения времени ожидания соединения. Сведения о группе пользователя передаются в токене при повторном подключении, и этот маркер проверяется на сервере.</span><span class="sxs-lookup"><span data-stu-id="3081e-161">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="3081e-162">Сведения о процедуре проверки повторного присоединения пользователей к группам см. в разделе [повторное присоединение групп при восстановлении](index.md)соединения.</span><span class="sxs-lookup"><span data-stu-id="3081e-162">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](index.md).</span></span>

<span data-ttu-id="3081e-163">В общем случае следует использовать поведение по умолчанию автоматического повторного присоединения групп при восстановлении соединения.</span><span class="sxs-lookup"><span data-stu-id="3081e-163">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="3081e-164">Группы SignalR не предназначены для обеспечения безопасности при ограничении доступа к конфиденциальным данным.</span><span class="sxs-lookup"><span data-stu-id="3081e-164">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="3081e-165">Однако если приложение должно проверить членство пользователя в группе при повторном подключении, можно переопределить поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3081e-165">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="3081e-166">Изменение поведения по умолчанию может добавить нагрузку в базу данных, так как членство пользователя в группе необходимо получить для каждого повторного подключения, а не только при подключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="3081e-166">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="3081e-167">Если необходимо проверить членство в группе при повторном подключении, создайте новый модуль конвейера концентратора, который возвращает список назначенных групп, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3081e-167">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

<span data-ttu-id="3081e-168">Затем добавьте этот модуль в конвейер концентратора, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3081e-168">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
