---
uid: signalr/overview/security/hub-authorization
title: Проверка подлинности и авторизация для концентраторов SignalR | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как ограничить доступ пользователей или ролей к методам концентратора. Версии программного обеспечения, используемые в этом разделе Visual Studio 2013 .NET 4,5 SignalR...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467514"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="b987e-104">Проверка подлинности и авторизация для концентраторов SignalR</span><span class="sxs-lookup"><span data-stu-id="b987e-104">Authentication and Authorization for SignalR Hubs</span></span>

<span data-ttu-id="b987e-105">[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b987e-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="b987e-106">В этом разделе описывается, как ограничить доступ пользователей или ролей к методам концентратора.</span><span class="sxs-lookup"><span data-stu-id="b987e-106">This topic describes how to restrict which users or roles can access hub methods.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="b987e-107">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="b987e-107">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="b987e-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b987e-108">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="b987e-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b987e-109">.NET 4.5</span></span>
> - <span data-ttu-id="b987e-110">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="b987e-110">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="b987e-111">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="b987e-111">Previous versions of this topic</span></span>
>
> <span data-ttu-id="b987e-112">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="b987e-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="b987e-113">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="b987e-113">Questions and comments</span></span>
>
> <span data-ttu-id="b987e-114">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b987e-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b987e-115">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="b987e-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="b987e-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="b987e-116">Overview</span></span>

<span data-ttu-id="b987e-117">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="b987e-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="b987e-118">Авторизовать атрибут</span><span class="sxs-lookup"><span data-stu-id="b987e-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="b987e-119">Требовать проверку подлинности для всех концентраторов</span><span class="sxs-lookup"><span data-stu-id="b987e-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="b987e-120">Настроенная авторизация</span><span class="sxs-lookup"><span data-stu-id="b987e-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="b987e-121">Передача сведений о проверке подлинности клиентам</span><span class="sxs-lookup"><span data-stu-id="b987e-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="b987e-122">Параметры проверки подлинности для клиентов .NET</span><span class="sxs-lookup"><span data-stu-id="b987e-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="b987e-123">Файл cookie с проверкой подлинности на формах</span><span class="sxs-lookup"><span data-stu-id="b987e-123">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="b987e-124">Проверка подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="b987e-124">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="b987e-125">Заголовок подключения</span><span class="sxs-lookup"><span data-stu-id="b987e-125">Connection header</span></span>](#header)
    - [<span data-ttu-id="b987e-126">Сертификат</span><span class="sxs-lookup"><span data-stu-id="b987e-126">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="b987e-127">Авторизовать атрибут</span><span class="sxs-lookup"><span data-stu-id="b987e-127">Authorize attribute</span></span>

<span data-ttu-id="b987e-128">SignalR предоставляет атрибут [авторизации](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) , чтобы указать, какие пользователи или роли имеют доступ к концентратору или методу.</span><span class="sxs-lookup"><span data-stu-id="b987e-128">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="b987e-129">Этот атрибут находится в пространстве имен `Microsoft.AspNet.SignalR`.</span><span class="sxs-lookup"><span data-stu-id="b987e-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="b987e-130">Атрибут `Authorize` применяется к концентратору или определенным методам в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="b987e-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="b987e-131">При применении атрибута `Authorize` к классу Hub указанные требования к авторизации применяются ко всем методам в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="b987e-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="b987e-132">В этом разделе приводятся примеры различных типов требований к авторизации, которые можно применять.</span><span class="sxs-lookup"><span data-stu-id="b987e-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="b987e-133">Без атрибута `Authorize` подключенный клиент может получить доступ к любому открытому методу в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="b987e-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="b987e-134">Если в веб-приложении определена роль с именем "admin", можно указать, что только пользователи с этой ролью могут получить доступ к концентратору со следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="b987e-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="b987e-135">Также можно указать, что центр содержит один метод, доступный всем пользователям, и второй метод, который доступен только для пользователей, прошедших проверку подлинности, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b987e-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="b987e-136">В следующих примерах разрешаться различные сценарии авторизации:</span><span class="sxs-lookup"><span data-stu-id="b987e-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="b987e-137">`[Authorize]` — только пользователи, прошедшие проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="b987e-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="b987e-138">`[Authorize(Roles = "Admin,Manager")]` — только пользователи, прошедшие проверку подлинности в указанных ролях</span><span class="sxs-lookup"><span data-stu-id="b987e-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="b987e-139">`[Authorize(Users = "user1,user2")]` — только пользователи, прошедшие проверку подлинности с указанными именами пользователей</span><span class="sxs-lookup"><span data-stu-id="b987e-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="b987e-140">`[Authorize(RequireOutgoing=false)]` — только пользователи, прошедшие проверку подлинности, могут вызывать концентратор, но вызовы от сервера к клиентам не ограничиваются авторизацией, например, когда только определенные пользователи могут отправлять сообщения, но все остальные могут получать это сообщение.</span><span class="sxs-lookup"><span data-stu-id="b987e-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="b987e-141">Свойство Рекуиреаутгоинг может применяться только ко всему концентратору, а не к отдельным методам в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="b987e-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="b987e-142">Если для Рекуиреаутгоинг не задано значение false, с сервера вызываются только пользователи, соответствующие требованию к авторизации.</span><span class="sxs-lookup"><span data-stu-id="b987e-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="b987e-143">Требовать проверку подлинности для всех концентраторов</span><span class="sxs-lookup"><span data-stu-id="b987e-143">Require authentication for all hubs</span></span>

<span data-ttu-id="b987e-144">Можно потребовать проверку подлинности для всех концентраторов и методов концентратора в приложении, вызвав метод [рекуиреаусентикатион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="b987e-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="b987e-145">Этот метод можно использовать, если у вас есть несколько концентраторов и необходимо обеспечить требование проверки подлинности для всех из них.</span><span class="sxs-lookup"><span data-stu-id="b987e-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="b987e-146">С помощью этого метода нельзя указать требования для роли, пользователя или исходящей авторизации.</span><span class="sxs-lookup"><span data-stu-id="b987e-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="b987e-147">Можно указать, чтобы доступ к методам концентратора был разрешен только пользователям, прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b987e-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="b987e-148">Однако вы по-прежнему можете применить атрибут авторизации к концентраторам или методам, чтобы указать дополнительные требования.</span><span class="sxs-lookup"><span data-stu-id="b987e-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="b987e-149">Все требования, указанные в атрибуте, добавляются к базовому требованию проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b987e-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="b987e-150">В следующем примере показан файл запуска, который разрешает всем методам концентратора проходить проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="b987e-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="b987e-151">При вызове метода `RequireAuthentication()` после обработки запроса SignalR SignalR выдаст исключение `InvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="b987e-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="b987e-152">SignalR создает это исключение, так как вы не можете добавить модуль в Хубпипелине после вызова конвейера.</span><span class="sxs-lookup"><span data-stu-id="b987e-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="b987e-153">В предыдущем примере показан вызов метода `RequireAuthentication` в методе `Configuration`, который выполняется один раз перед обработкой первого запроса.</span><span class="sxs-lookup"><span data-stu-id="b987e-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="b987e-154">Настроенная авторизация</span><span class="sxs-lookup"><span data-stu-id="b987e-154">Customized authorization</span></span>

<span data-ttu-id="b987e-155">Если необходимо настроить авторизацию, можно создать класс, производный от `AuthorizeAttribute` и переопределить метод [усераусоризед](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="b987e-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="b987e-156">Для каждого запроса SignalR вызывает этот метод, чтобы определить, имеет ли пользователь разрешение на завершение запроса.</span><span class="sxs-lookup"><span data-stu-id="b987e-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="b987e-157">В переопределенном методе вы предоставляете необходимую логику для вашего сценария авторизации.</span><span class="sxs-lookup"><span data-stu-id="b987e-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="b987e-158">В следующем примере показано, как обеспечить авторизацию с помощью удостоверения на основе утверждений.</span><span class="sxs-lookup"><span data-stu-id="b987e-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="b987e-159">Передача сведений о проверке подлинности клиентам</span><span class="sxs-lookup"><span data-stu-id="b987e-159">Pass authentication information to clients</span></span>

<span data-ttu-id="b987e-160">Может потребоваться использовать данные проверки подлинности в коде, который выполняется на клиенте.</span><span class="sxs-lookup"><span data-stu-id="b987e-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="b987e-161">Необходимо передать необходимые сведения при вызове методов на клиенте.</span><span class="sxs-lookup"><span data-stu-id="b987e-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="b987e-162">Например, метод приложения разговора может передавать в качестве параметра имя пользователя, публикующий сообщение, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b987e-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="b987e-163">Или можно создать объект для представления сведений о проверке подлинности и передать этот объект в качестве параметра, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b987e-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="b987e-164">Никогда не следует передавать идентификаторы подключения одного клиента другим клиентам, так как пользователь-злоумышленник может использовать его для имитации запроса от этого клиента.</span><span class="sxs-lookup"><span data-stu-id="b987e-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="b987e-165">Параметры проверки подлинности для клиентов .NET</span><span class="sxs-lookup"><span data-stu-id="b987e-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="b987e-166">Если у вас есть клиент .NET, например консольное приложение, взаимодействующее с концентратором, который ограничен пользователями, прошедшими проверку подлинности, можно передать учетные данные для проверки подлинности в файл cookie, заголовок соединения или сертификат.</span><span class="sxs-lookup"><span data-stu-id="b987e-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="b987e-167">В примерах этого раздела показано, как использовать различные методы для проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="b987e-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="b987e-168">Они не являются полнофункциональными приложениями SignalR.</span><span class="sxs-lookup"><span data-stu-id="b987e-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="b987e-169">Дополнительные сведения о клиентах .NET с помощью SignalR см. в статье [Путеводитель по API концентраторов — клиент .NET](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="b987e-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="b987e-170">Куки-файл</span><span class="sxs-lookup"><span data-stu-id="b987e-170">Cookie</span></span>

<span data-ttu-id="b987e-171">Когда клиент .NET взаимодействует с концентратором, использующим проверку подлинности ASP.NET Forms, необходимо вручную задать файл cookie проверки подлинности для соединения.</span><span class="sxs-lookup"><span data-stu-id="b987e-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="b987e-172">Файл cookie добавляется в свойство `CookieContainer` объекта [хубконнектион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="b987e-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="b987e-173">В следующем примере показано консольное приложение, которое получает файл cookie проверки подлинности с веб-страницы и добавляет этот файл cookie к соединению.</span><span class="sxs-lookup"><span data-stu-id="b987e-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="b987e-174">Консольное приложение отправляет учетные данные в <strong>www.contoso.com/RemoteLogin</strong> , которые могут ссылаться на пустую страницу, содержащую следующий файл кода программной части.</span><span class="sxs-lookup"><span data-stu-id="b987e-174">The console app posts the credentials to <strong>www.contoso.com/RemoteLogin</strong> which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="b987e-175">Проверка подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="b987e-175">Windows authentication</span></span>

<span data-ttu-id="b987e-176">При использовании проверки подлинности Windows можно передать учетные данные текущего пользователя с помощью свойства [дефаулткредентиалс](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b987e-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="b987e-177">Вы задаете учетные данные для соединения со значением Дефаулткредентиалс.</span><span class="sxs-lookup"><span data-stu-id="b987e-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="b987e-178">Заголовок подключения</span><span class="sxs-lookup"><span data-stu-id="b987e-178">Connection header</span></span>

<span data-ttu-id="b987e-179">Если приложение не использует файлы cookie, можно передать сведения о пользователе в заголовке соединения.</span><span class="sxs-lookup"><span data-stu-id="b987e-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="b987e-180">Например, можно передать маркер в заголовок Connection.</span><span class="sxs-lookup"><span data-stu-id="b987e-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="b987e-181">Затем в центре можно проверить маркер пользователя.</span><span class="sxs-lookup"><span data-stu-id="b987e-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="b987e-182">Сертификат</span><span class="sxs-lookup"><span data-stu-id="b987e-182">Certificate</span></span>

<span data-ttu-id="b987e-183">Сертификат клиента можно передать для проверки пользователя.</span><span class="sxs-lookup"><span data-stu-id="b987e-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="b987e-184">Сертификат добавляется при создании соединения.</span><span class="sxs-lookup"><span data-stu-id="b987e-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="b987e-185">В следующем примере показано, как добавить сертификат клиента в соединение. в нем не отображается полное консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="b987e-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="b987e-186">Он использует класс [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) , который предоставляет несколько различных способов создания сертификата.</span><span class="sxs-lookup"><span data-stu-id="b987e-186">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
