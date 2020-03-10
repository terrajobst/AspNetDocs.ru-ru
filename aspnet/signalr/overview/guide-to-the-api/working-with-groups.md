---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: Работа с группами в SignalR | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как сохранять сведения о членстве в группах с помощью API концентратора.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 46dd952fc4902b37c981a111dfa344dad79bb668
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450084"
---
# <a name="working-with-groups-in-signalr"></a><span data-ttu-id="2d7ea-103">Работа с группами в SignalR</span><span class="sxs-lookup"><span data-stu-id="2d7ea-103">Working with Groups in SignalR</span></span>

<span data-ttu-id="2d7ea-104">[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2d7ea-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="2d7ea-105">В этом разделе описывается добавление пользователей в группы и сохранение сведений о членстве в группах.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-105">This topic describes how to add users to groups and persist group membership information.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="2d7ea-106">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="2d7ea-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="2d7ea-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2d7ea-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2d7ea-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2d7ea-108">.NET 4.5</span></span>
> - <span data-ttu-id="2d7ea-109">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="2d7ea-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="2d7ea-110">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="2d7ea-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="2d7ea-111">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2d7ea-112">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="2d7ea-112">Questions and comments</span></span>
>
> <span data-ttu-id="2d7ea-113">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2d7ea-114">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="2d7ea-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="2d7ea-115">Обзор</span><span class="sxs-lookup"><span data-stu-id="2d7ea-115">Overview</span></span>

<span data-ttu-id="2d7ea-116">Группы в SignalR предоставляют метод для вещания сообщений в указанные подмножества подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-116">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="2d7ea-117">Группа может иметь любое количество клиентов, а клиент может быть членом любого числа групп.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-117">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="2d7ea-118">Вам не нужно явно создавать группы.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-118">You don't have to explicitly create groups.</span></span> <span data-ttu-id="2d7ea-119">По сути, группа создается автоматически при первом указании имени в вызове Groups. Add и удаляется при удалении последнего подключения из членства в нем.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-119">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="2d7ea-120">Общие сведения об использовании групп см. в разделе [Управление членством в группах из класса Hub](hubs-api-guide-server.md#groupsfromhub) руководства по API концентраторов.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-120">For an introduction to using groups, see [How to manage group membership from the Hub class](hubs-api-guide-server.md#groupsfromhub) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="2d7ea-121">Отсутствует API для получения списка членства в группе или списка групп.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-121">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="2d7ea-122">SignalR отправляет сообщения клиентам и группам, основанным на модели публикации и подтипа, а сервер не поддерживает списки групп или членства в группах.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-122">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="2d7ea-123">Это обеспечивает максимальную масштабируемость, так как при добавлении узла в веб-ферму любое состояние, которое обслуживает SignalR, должно быть распространено на новый узел.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-123">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="2d7ea-124">При добавлении пользователя в группу с помощью метода `Groups.Add` пользователь получает сообщения, направленные в эту группу, на время текущего соединения, но членство пользователя в этой группе не сохраняется за пределами текущего соединения.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-124">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="2d7ea-125">Если вы хотите постоянно сохранять сведения о группах и членстве в группах, эти данные необходимо хранить в репозитории, например в базе данных или в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-125">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="2d7ea-126">Затем каждый раз, когда пользователь подключается к вашему приложению, вы получаете из репозитория, в который входит пользователь, и вручную добавляете этого пользователя в эти группы.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-126">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="2d7ea-127">При повторном подключении после временного перерыва пользователь автоматически повторно присоединяется к ранее назначенным группам.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-127">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="2d7ea-128">Автоматическое пересоединение группы применяется только при повторном подключении, а не при установке нового соединения.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-128">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="2d7ea-129">Маркер с цифровой подписью передается из клиента, содержащего список ранее назначенных групп.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-129">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="2d7ea-130">Если необходимо проверить, относится ли пользователь к запрошенным группам, можно переопределить поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-130">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="2d7ea-131">Этот раздел включает следующие подразделы:</span><span class="sxs-lookup"><span data-stu-id="2d7ea-131">This topic includes the following sections:</span></span>

- [<span data-ttu-id="2d7ea-132">Добавление и удаление пользователей</span><span class="sxs-lookup"><span data-stu-id="2d7ea-132">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="2d7ea-133">Вызов членов группы</span><span class="sxs-lookup"><span data-stu-id="2d7ea-133">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="2d7ea-134">Хранение членства в группе в базе данных</span><span class="sxs-lookup"><span data-stu-id="2d7ea-134">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="2d7ea-135">Хранение членства в группах в хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="2d7ea-135">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="2d7ea-136">Проверка членства в группе при повторном подключении</span><span class="sxs-lookup"><span data-stu-id="2d7ea-136">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="2d7ea-137">Добавление и удаление пользователей</span><span class="sxs-lookup"><span data-stu-id="2d7ea-137">Adding and removing users</span></span>

<span data-ttu-id="2d7ea-138">Чтобы добавить или удалить пользователей из группы, вызовите методы [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) или [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) и передайте в качестве параметров идентификатор подключения пользователя и имя группы.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-138">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="2d7ea-139">При завершении соединения не требуется вручную удалять пользователя из группы.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-139">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="2d7ea-140">В следующем примере показаны методы `Groups.Add` и `Groups.Remove`, используемые в методах концентратора.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-140">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="2d7ea-141">Методы `Groups.Add` и `Groups.Remove` выполняются асинхронно.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-141">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="2d7ea-142">Если вы хотите добавить клиент в группу и сразу же отправить сообщение клиенту с помощью группы, необходимо убедиться в том, что метод Groups. Add завершается первым.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-142">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="2d7ea-143">В следующих примерах кода показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-143">The following code examples show how to do that.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

<span data-ttu-id="2d7ea-144">В общем случае не следует включать `await` при вызове метода `Groups.Remove`, так как идентификатор подключения, который вы пытаетесь удалить, может больше не быть доступен.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-144">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="2d7ea-145">В этом случае `TaskCanceledException` создается после истечения времени ожидания запроса. Если приложение должно гарантировать, что пользователь был удален из группы перед отправкой сообщения в группу, можно добавить `await` до `Groups.Remove`, а затем перехватить `TaskCanceledException` исключение, которое может быть выдано.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-145">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before `Groups.Remove`, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="2d7ea-146">Вызов членов группы</span><span class="sxs-lookup"><span data-stu-id="2d7ea-146">Calling members of a group</span></span>

<span data-ttu-id="2d7ea-147">Можно отправить сообщения всем членам группы или только указанным членам группы, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-147">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="2d7ea-148">**Все** подключенные клиенты в указанной группе.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-148">**All** connected clients in a specified group.</span></span>

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- <span data-ttu-id="2d7ea-149">Все подключенные клиенты в указанной группе, **за исключением указанных клиентов**, идентифицируемые по идентификатору соединения.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-149">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span>

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- <span data-ttu-id="2d7ea-150">Все подключенные клиенты в указанной группе, **Кроме вызывающего клиента**.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-150">All connected clients in a specified group **except the calling client**.</span></span>

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="2d7ea-151">Хранение членства в группе в базе данных</span><span class="sxs-lookup"><span data-stu-id="2d7ea-151">Storing group membership in a database</span></span>

<span data-ttu-id="2d7ea-152">В следующих примерах показано, как хранить сведения о группах и пользователях в базе данных.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-152">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="2d7ea-153">Можно использовать любую технологию доступа к данным. Однако в приведенном ниже примере показано, как определить модели с помощью Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="2d7ea-154">Эти модели сущностей соответствуют таблицам и полям базы данных.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="2d7ea-155">Структура данных может значительно варьироваться в зависимости от требований приложения.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-155">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="2d7ea-156">Этот пример включает класс с именем `ConversationRoom`, который будет уникальным для приложения, позволяющего пользователям присоединяться к беседам по различным темам, таким как спорт или садом.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-156">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="2d7ea-157">Этот пример также включает класс для соединений.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-157">This example also includes a class for the connections.</span></span> <span data-ttu-id="2d7ea-158">Класс Connection не является абсолютно необходимым для отслеживания членства в группах, но часто является частью надежного решения для отслеживания пользователей.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-158">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

<span data-ttu-id="2d7ea-159">Затем в центре можно получить сведения о группах и пользователях из базы данных и вручную добавить пользователя в соответствующие группы.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-159">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="2d7ea-160">В примере не содержится код для отслеживания пользовательских соединений.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-160">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="2d7ea-161">В этом примере ключевое слово `await` не применяется перед `Groups.Add`, так как сообщение не отправляется сразу членам группы.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-161">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="2d7ea-162">Если вы хотите отправить сообщение всем членам группы сразу после добавления нового члена, необходимо применить ключевое слово `await`, чтобы убедиться, что асинхронная операция завершена.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-162">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="2d7ea-163">Хранение членства в группах в хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="2d7ea-163">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="2d7ea-164">Использование хранилища таблиц Azure для хранения данных группы и пользователя аналогично использованию базы данных.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-164">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="2d7ea-165">В следующем примере показана сущность таблицы, в которой хранится имя пользователя и имя группы.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-165">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<span data-ttu-id="2d7ea-166">В центре вы получаете назначенные группы при подключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-166">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="2d7ea-167">Проверка членства в группе при повторном подключении</span><span class="sxs-lookup"><span data-stu-id="2d7ea-167">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="2d7ea-168">По умолчанию SignalR автоматически переназначит пользователя соответствующим группам при повторном подключении из временного перерыва, например при удалении и повторном установлении соединения до истечения времени ожидания соединения. Сведения о группе пользователя передаются в токене при повторном подключении, и этот маркер проверяется на сервере.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-168">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="2d7ea-169">Сведения о процедуре проверки повторного присоединения пользователей к группам см. в разделе [повторное присоединение групп при восстановлении](../security/introduction-to-security.md#rejoingroup)соединения.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-169">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](../security/introduction-to-security.md#rejoingroup).</span></span>

<span data-ttu-id="2d7ea-170">В общем случае следует использовать поведение по умолчанию автоматического повторного присоединения групп при восстановлении соединения.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-170">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="2d7ea-171">Группы SignalR не предназначены для обеспечения безопасности при ограничении доступа к конфиденциальным данным.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-171">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="2d7ea-172">Однако если приложение должно проверить членство пользователя в группе при повторном подключении, можно переопределить поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-172">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="2d7ea-173">Изменение поведения по умолчанию может добавить нагрузку в базу данных, так как членство пользователя в группе необходимо получить для каждого повторного подключения, а не только при подключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-173">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="2d7ea-174">Если необходимо проверить членство в группе при повторном подключении, создайте новый модуль конвейера концентратора, который возвращает список назначенных групп, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-174">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<span data-ttu-id="2d7ea-175">Затем добавьте этот модуль в конвейер концентратора, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2d7ea-175">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]
