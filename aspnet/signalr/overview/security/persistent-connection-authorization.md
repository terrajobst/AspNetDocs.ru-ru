---
uid: signalr/overview/security/persistent-connection-authorization
title: Проверка подлинности и авторизация для постоянных подключений SignalR | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается принудительное применение авторизации для постоянного подключения. Общие сведения об интеграции безопасности в приложение SignalR,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467478"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="4a185-104">Проверка подлинности и авторизация для постоянных подключений SignalR</span><span class="sxs-lookup"><span data-stu-id="4a185-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="4a185-105">[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4a185-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4a185-106">В этом разделе описывается принудительное применение авторизации для постоянного подключения.</span><span class="sxs-lookup"><span data-stu-id="4a185-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="4a185-107">Общие сведения о интеграции безопасности в приложение SignalR см. [в статье Введение в безопасность](introduction-to-security.md).</span><span class="sxs-lookup"><span data-stu-id="4a185-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="4a185-108">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="4a185-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="4a185-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4a185-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="4a185-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="4a185-110">.NET 4.5</span></span>
> - <span data-ttu-id="4a185-111">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="4a185-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="4a185-112">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="4a185-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="4a185-113">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="4a185-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="4a185-114">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="4a185-114">Questions and comments</span></span>
>
> <span data-ttu-id="4a185-115">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="4a185-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="4a185-116">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="4a185-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="4a185-117">Принудительная авторизация</span><span class="sxs-lookup"><span data-stu-id="4a185-117">Enforce authorization</span></span>

<span data-ttu-id="4a185-118">Чтобы применить правила авторизации при использовании [персистентконнектион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , необходимо переопределить метод `AuthorizeRequest`.</span><span class="sxs-lookup"><span data-stu-id="4a185-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="4a185-119">Нельзя использовать атрибут `Authorize` с постоянными соединениями.</span><span class="sxs-lookup"><span data-stu-id="4a185-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="4a185-120">Метод `AuthorizeRequest` вызывается платформой SignalR перед каждым запросом, чтобы убедиться, что пользователь имеет право выполнять запрошенное действие.</span><span class="sxs-lookup"><span data-stu-id="4a185-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="4a185-121">Метод `AuthorizeRequest` не вызывается из клиента; Вместо этого выполняется проверка подлинности пользователя с помощью стандартного механизма проверки подлинности приложения.</span><span class="sxs-lookup"><span data-stu-id="4a185-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="4a185-122">В приведенном ниже примере показано, как ограничить запросы для пользователей, прошедших проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="4a185-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="4a185-123">В метод AuthorizeRequest можно добавить любую настраиваемую логику авторизации. Например, проверка принадлежности пользователя к определенной роли.</span><span class="sxs-lookup"><span data-stu-id="4a185-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
