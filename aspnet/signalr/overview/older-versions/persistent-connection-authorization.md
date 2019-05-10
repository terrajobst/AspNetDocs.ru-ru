---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: Проверка подлинности и авторизация для постоянных подключений SignalR (SignalR 1.x) | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как требовать принудительной авторизации на постоянное подключение. Общие сведения об интеграции безопасности в приложении SignalR...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117045"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="81a89-104">Проверка подлинности и авторизация для постоянных подключений SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="81a89-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>

<span data-ttu-id="81a89-105">по [Флетчера Патрик](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="81a89-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="81a89-106">В этом разделе описывается, как требовать принудительной авторизации на постоянное подключение.</span><span class="sxs-lookup"><span data-stu-id="81a89-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="81a89-107">Общие сведения об интеграции безопасности в приложении SignalR, см. в разделе [Общие сведения о безопасности](index.md).</span><span class="sxs-lookup"><span data-stu-id="81a89-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="81a89-108">Требовать принудительной авторизации</span><span class="sxs-lookup"><span data-stu-id="81a89-108">Enforce authorization</span></span>

<span data-ttu-id="81a89-109">Для принудительного выполнения правил авторизации, при использовании [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) необходимо переопределить `AuthorizeRequest` метод.</span><span class="sxs-lookup"><span data-stu-id="81a89-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="81a89-110">Нельзя использовать `Authorize` атрибута с постоянные подключения.</span><span class="sxs-lookup"><span data-stu-id="81a89-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="81a89-111">`AuthorizeRequest` Метод вызывается инфраструктурой SignalR перед каждым запросом, чтобы убедиться, что пользователь авторизован для выполнения запрошенного действия.</span><span class="sxs-lookup"><span data-stu-id="81a89-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="81a89-112">`AuthorizeRequest` Метод не вызывается из клиента; вместо этого проверки подлинности пользователя через механизм стандартной проверки подлинности приложения.</span><span class="sxs-lookup"><span data-stu-id="81a89-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="81a89-113">В приведенном ниже примере показано, как ограничить запросы пользователям, прошедшим проверку.</span><span class="sxs-lookup"><span data-stu-id="81a89-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="81a89-114">Можно добавить логику настраиваемой авторизации в методе AuthorizeRequest; например проверка, принадлежит ли пользователь к определенной роли.</span><span class="sxs-lookup"><span data-stu-id="81a89-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
