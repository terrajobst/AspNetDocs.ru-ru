---
uid: signalr/overview/older-versions/hub-authorization
title: Проверка подлинности и авторизация для концентраторов SignalR (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как ограничить доступ пользователей или ролей к методам концентратора.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450042"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="35418-103">Проверка подлинности и авторизация для концентраторов SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="35418-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>

<span data-ttu-id="35418-104">[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="35418-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="35418-105">В этом разделе описывается, как ограничить доступ пользователей или ролей к методам концентратора.</span><span class="sxs-lookup"><span data-stu-id="35418-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>

## <a name="overview"></a><span data-ttu-id="35418-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="35418-106">Overview</span></span>

<span data-ttu-id="35418-107">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="35418-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="35418-108">Авторизовать атрибут</span><span class="sxs-lookup"><span data-stu-id="35418-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="35418-109">Требовать проверку подлинности для всех концентраторов</span><span class="sxs-lookup"><span data-stu-id="35418-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="35418-110">Настроенная авторизация</span><span class="sxs-lookup"><span data-stu-id="35418-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="35418-111">Передача сведений о проверке подлинности клиентам</span><span class="sxs-lookup"><span data-stu-id="35418-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="35418-112">Параметры проверки подлинности для клиентов .NET</span><span class="sxs-lookup"><span data-stu-id="35418-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="35418-113">Файл cookie с проверкой подлинности на формах</span><span class="sxs-lookup"><span data-stu-id="35418-113">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="35418-114">Проверка подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="35418-114">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="35418-115">Заголовок подключения</span><span class="sxs-lookup"><span data-stu-id="35418-115">Connection header</span></span>](#header)
    - [<span data-ttu-id="35418-116">Сертификат</span><span class="sxs-lookup"><span data-stu-id="35418-116">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="35418-117">Авторизовать атрибут</span><span class="sxs-lookup"><span data-stu-id="35418-117">Authorize attribute</span></span>

<span data-ttu-id="35418-118">SignalR предоставляет атрибут [авторизации](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) , чтобы указать, какие пользователи или роли имеют доступ к концентратору или методу.</span><span class="sxs-lookup"><span data-stu-id="35418-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="35418-119">Этот атрибут находится в пространстве имен `Microsoft.AspNet.SignalR`.</span><span class="sxs-lookup"><span data-stu-id="35418-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="35418-120">Атрибут `Authorize` применяется к концентратору или определенным методам в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="35418-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="35418-121">При применении атрибута `Authorize` к классу Hub указанные требования к авторизации применяются ко всем методам в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="35418-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="35418-122">Ниже приведены различные типы требований к авторизации, которые можно применять.</span><span class="sxs-lookup"><span data-stu-id="35418-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="35418-123">Без атрибута `Authorize` все открытые методы в концентраторе доступны для клиента, подключенного к концентратору.</span><span class="sxs-lookup"><span data-stu-id="35418-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="35418-124">Если в веб-приложении определена роль с именем "admin", можно указать, что только пользователи с этой ролью могут получить доступ к концентратору со следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="35418-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="35418-125">Также можно указать, что центр содержит один метод, доступный всем пользователям, и второй метод, который доступен только для пользователей, прошедших проверку подлинности, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="35418-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="35418-126">В следующих примерах разрешаться различные сценарии авторизации:</span><span class="sxs-lookup"><span data-stu-id="35418-126">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="35418-127">`[Authorize]` — только пользователи, прошедшие проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="35418-127">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="35418-128">`[Authorize(Roles = "Admin,Manager")]` — только пользователи, прошедшие проверку подлинности в указанных ролях</span><span class="sxs-lookup"><span data-stu-id="35418-128">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="35418-129">`[Authorize(Users = "user1,user2")]` — только пользователи, прошедшие проверку подлинности с указанными именами пользователей</span><span class="sxs-lookup"><span data-stu-id="35418-129">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="35418-130">`[Authorize(RequireOutgoing=false)]` — только пользователи, прошедшие проверку подлинности, могут вызывать концентратор, но вызовы от сервера к клиентам не ограничиваются авторизацией, например, когда только определенные пользователи могут отправлять сообщения, но все остальные могут получать это сообщение.</span><span class="sxs-lookup"><span data-stu-id="35418-130">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="35418-131">Свойство Рекуиреаутгоинг может применяться только ко всему концентратору, а не к отдельным методам в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="35418-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="35418-132">Если для Рекуиреаутгоинг не задано значение false, с сервера вызываются только пользователи, соответствующие требованию к авторизации.</span><span class="sxs-lookup"><span data-stu-id="35418-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="35418-133">Требовать проверку подлинности для всех концентраторов</span><span class="sxs-lookup"><span data-stu-id="35418-133">Require authentication for all hubs</span></span>

<span data-ttu-id="35418-134">Можно потребовать проверку подлинности для всех концентраторов и методов концентратора в приложении, вызвав метод [рекуиреаусентикатион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="35418-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="35418-135">Этот метод можно использовать, если у вас есть несколько концентраторов и необходимо обеспечить требование проверки подлинности для всех из них.</span><span class="sxs-lookup"><span data-stu-id="35418-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="35418-136">С помощью этого метода нельзя указать роль, пользователя или исходящую авторизацию.</span><span class="sxs-lookup"><span data-stu-id="35418-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="35418-137">Можно указать, чтобы доступ к методам концентратора был разрешен только пользователям, прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="35418-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="35418-138">Однако вы по-прежнему можете применить атрибут авторизации к концентраторам или методам, чтобы указать дополнительные требования.</span><span class="sxs-lookup"><span data-stu-id="35418-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="35418-139">Все требования, указываемые в атрибутах, применяются в дополнение к базовому требованию проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="35418-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="35418-140">В следующем примере показан файл Global. asax, который запрещает всем методам центра проходить проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="35418-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="35418-141">При вызове метода `RequireAuthentication()` после обработки запроса SignalR SignalR выдаст исключение `InvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="35418-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="35418-142">Это исключение возникает, поскольку невозможно добавить модуль в Хубпипелине после вызова конвейера.</span><span class="sxs-lookup"><span data-stu-id="35418-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="35418-143">В предыдущем примере показан вызов метода `RequireAuthentication` в методе `Application_Start`, который выполняется один раз перед обработкой первого запроса.</span><span class="sxs-lookup"><span data-stu-id="35418-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="35418-144">Настроенная авторизация</span><span class="sxs-lookup"><span data-stu-id="35418-144">Customized authorization</span></span>

<span data-ttu-id="35418-145">Если необходимо настроить авторизацию, можно создать класс, производный от `AuthorizeAttribute` и переопределить метод [усераусоризед](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="35418-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="35418-146">Этот метод вызывается для каждого запроса, чтобы определить, имеет ли пользователь разрешение на завершение запроса.</span><span class="sxs-lookup"><span data-stu-id="35418-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="35418-147">В переопределенном методе вы предоставляете необходимую логику для вашего сценария авторизации.</span><span class="sxs-lookup"><span data-stu-id="35418-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="35418-148">В следующем примере показано, как обеспечить авторизацию с помощью удостоверения на основе утверждений.</span><span class="sxs-lookup"><span data-stu-id="35418-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="35418-149">Передача сведений о проверке подлинности клиентам</span><span class="sxs-lookup"><span data-stu-id="35418-149">Pass authentication information to clients</span></span>

<span data-ttu-id="35418-150">Может потребоваться использовать данные проверки подлинности в коде, который выполняется на клиенте.</span><span class="sxs-lookup"><span data-stu-id="35418-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="35418-151">Необходимо передать необходимые сведения при вызове методов на клиенте.</span><span class="sxs-lookup"><span data-stu-id="35418-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="35418-152">Например, метод приложения разговора может передавать в качестве параметра имя пользователя, публикующий сообщение, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="35418-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="35418-153">Или можно создать объект для представления сведений о проверке подлинности и передать этот объект в качестве параметра, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="35418-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="35418-154">Никогда не следует передавать идентификаторы подключения одного клиента другим клиентам, так как пользователь-злоумышленник может использовать его для имитации запроса от этого клиента.</span><span class="sxs-lookup"><span data-stu-id="35418-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="35418-155">Параметры проверки подлинности для клиентов .NET</span><span class="sxs-lookup"><span data-stu-id="35418-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="35418-156">Если у вас есть клиент .NET, например консольное приложение, взаимодействующее с концентратором, который ограничен пользователями, прошедшими проверку подлинности, можно передать учетные данные для проверки подлинности в файл cookie, заголовок соединения или сертификат.</span><span class="sxs-lookup"><span data-stu-id="35418-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="35418-157">В примерах этого раздела показано, как использовать различные методы для проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="35418-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="35418-158">Они не являются полнофункциональными приложениями SignalR.</span><span class="sxs-lookup"><span data-stu-id="35418-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="35418-159">Дополнительные сведения о клиентах .NET с помощью SignalR см. в статье [Путеводитель по API концентраторов — клиент .NET](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="35418-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="35418-160">Куки-файл</span><span class="sxs-lookup"><span data-stu-id="35418-160">Cookie</span></span>

<span data-ttu-id="35418-161">Когда клиент .NET взаимодействует с концентратором, использующим проверку подлинности ASP.NET Forms, необходимо вручную задать файл cookie проверки подлинности для соединения.</span><span class="sxs-lookup"><span data-stu-id="35418-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="35418-162">Файл cookie добавляется в свойство `CookieContainer` объекта [хубконнектион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="35418-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="35418-163">В следующем примере показано консольное приложение, которое получает файл cookie проверки подлинности с веб-страницы и добавляет этот файл cookie к соединению.</span><span class="sxs-lookup"><span data-stu-id="35418-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="35418-164">URL-адрес `https://www.contoso.com/RemoteLogin` в примере указывает на веб-страницу, которую необходимо создать.</span><span class="sxs-lookup"><span data-stu-id="35418-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="35418-165">Страница будет получать опубликованные имя пользователя и пароль, а также пытаться войти в систему пользователя с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="35418-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="35418-166">Консольное приложение отправляет учетные данные в www.contoso.com/RemoteLogin, которые могут ссылаться на пустую страницу, содержащую следующий файл кода программной части.</span><span class="sxs-lookup"><span data-stu-id="35418-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="35418-167">Проверка подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="35418-167">Windows authentication</span></span>

<span data-ttu-id="35418-168">При использовании проверки подлинности Windows можно передать учетные данные текущего пользователя с помощью свойства [дефаулткредентиалс](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) .</span><span class="sxs-lookup"><span data-stu-id="35418-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="35418-169">Вы задаете учетные данные для соединения со значением Дефаулткредентиалс.</span><span class="sxs-lookup"><span data-stu-id="35418-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="35418-170">Заголовок подключения</span><span class="sxs-lookup"><span data-stu-id="35418-170">Connection header</span></span>

<span data-ttu-id="35418-171">Если приложение не использует файлы cookie, можно передать сведения о пользователе в заголовке соединения.</span><span class="sxs-lookup"><span data-stu-id="35418-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="35418-172">Например, можно передать маркер в заголовок Connection.</span><span class="sxs-lookup"><span data-stu-id="35418-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="35418-173">Затем в центре можно проверить маркер пользователя.</span><span class="sxs-lookup"><span data-stu-id="35418-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="35418-174">Сертификат</span><span class="sxs-lookup"><span data-stu-id="35418-174">Certificate</span></span>

<span data-ttu-id="35418-175">Сертификат клиента можно передать для проверки пользователя.</span><span class="sxs-lookup"><span data-stu-id="35418-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="35418-176">Сертификат добавляется при создании соединения.</span><span class="sxs-lookup"><span data-stu-id="35418-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="35418-177">В следующем примере показано, как добавить сертификат клиента в соединение. в нем не отображается полное консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="35418-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="35418-178">Он использует класс [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) , который предоставляет несколько различных способов создания сертификата.</span><span class="sxs-lookup"><span data-stu-id="35418-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
