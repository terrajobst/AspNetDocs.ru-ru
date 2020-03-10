---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: Проверка подлинности и авторизация для постоянных подключений SignalR (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается принудительное применение авторизации для постоянного подключения. Общие сведения об интеграции безопасности в приложение SignalR,...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431190"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="ec763-104">Проверка подлинности и авторизация для постоянных подключений SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="ec763-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>

<span data-ttu-id="ec763-105">[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ec763-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ec763-106">В этом разделе описывается принудительное применение авторизации для постоянного подключения.</span><span class="sxs-lookup"><span data-stu-id="ec763-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="ec763-107">Общие сведения о интеграции безопасности в приложение SignalR см. [в статье Введение в безопасность](index.md).</span><span class="sxs-lookup"><span data-stu-id="ec763-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="ec763-108">Принудительная авторизация</span><span class="sxs-lookup"><span data-stu-id="ec763-108">Enforce authorization</span></span>

<span data-ttu-id="ec763-109">Чтобы применить правила авторизации при использовании [персистентконнектион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , необходимо переопределить метод `AuthorizeRequest`.</span><span class="sxs-lookup"><span data-stu-id="ec763-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="ec763-110">Нельзя использовать атрибут `Authorize` с постоянными соединениями.</span><span class="sxs-lookup"><span data-stu-id="ec763-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="ec763-111">Метод `AuthorizeRequest` вызывается платформой SignalR перед каждым запросом, чтобы убедиться, что пользователь имеет право выполнять запрошенное действие.</span><span class="sxs-lookup"><span data-stu-id="ec763-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="ec763-112">Метод `AuthorizeRequest` не вызывается из клиента; Вместо этого выполняется проверка подлинности пользователя с помощью стандартного механизма проверки подлинности приложения.</span><span class="sxs-lookup"><span data-stu-id="ec763-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="ec763-113">В приведенном ниже примере показано, как ограничить запросы для пользователей, прошедших проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="ec763-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="ec763-114">В метод AuthorizeRequest можно добавить любую настраиваемую логику авторизации. Например, проверка принадлежности пользователя к определенной роли.</span><span class="sxs-lookup"><span data-stu-id="ec763-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
