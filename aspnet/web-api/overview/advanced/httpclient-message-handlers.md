---
uid: web-api/overview/advanced/httpclient-message-handlers
title: Обработчики сообщений HttpClient в веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: Создание пользовательских обработчиков сообщений для веб-API ASP.NET в ASP.NET 4. x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449280"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="b0a98-103">Обработчики сообщений HttpClient в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b0a98-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="b0a98-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b0a98-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b0a98-105">*Обработчик сообщений* — это класс, который получает HTTP-запрос и ВОЗВРАЩАЕТ ответ HTTP.</span><span class="sxs-lookup"><span data-stu-id="b0a98-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="b0a98-106">Как правило, ряд обработчиков сообщений объединяется в цепочку.</span><span class="sxs-lookup"><span data-stu-id="b0a98-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="b0a98-107">Первый обработчик получает HTTP-запрос, выполняет некоторую обработку и передает запрос следующему обработчику.</span><span class="sxs-lookup"><span data-stu-id="b0a98-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="b0a98-108">В какой-то момент ответ создается и помещается в резервную копию цепочки.</span><span class="sxs-lookup"><span data-stu-id="b0a98-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="b0a98-109">Этот шаблон называется *делегированным* обработчиком.</span><span class="sxs-lookup"><span data-stu-id="b0a98-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="b0a98-110">На стороне клиента класс **HttpClient** использует обработчик сообщений для обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="b0a98-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="b0a98-111">Обработчик по умолчанию — **HttpClientHandler**, который отправляет запрос по сети и получает ответ от сервера.</span><span class="sxs-lookup"><span data-stu-id="b0a98-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="b0a98-112">В клиентский конвейер можно вставлять пользовательские обработчики сообщений:</span><span class="sxs-lookup"><span data-stu-id="b0a98-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="b0a98-113">Веб-API ASP.NET также использует обработчики сообщений на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="b0a98-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="b0a98-114">Дополнительные сведения см. в разделе [обработчики сообщений HTTP](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="b0a98-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="b0a98-115">Пользовательские обработчики сообщений</span><span class="sxs-lookup"><span data-stu-id="b0a98-115">Custom Message Handlers</span></span>

<span data-ttu-id="b0a98-116">Для написания пользовательского обработчика сообщений следует использовать класс **System .NET. http. DelegatingHandler** и переопределить метод **SendAsync** .</span><span class="sxs-lookup"><span data-stu-id="b0a98-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="b0a98-117">Вот так выглядит подпись метода.</span><span class="sxs-lookup"><span data-stu-id="b0a98-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="b0a98-118">Метод принимает **HttpRequestMessage** в качестве входных данных и асинхронно возвращает **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="b0a98-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="b0a98-119">Типичная реализация выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b0a98-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="b0a98-120">Обработать сообщение запроса.</span><span class="sxs-lookup"><span data-stu-id="b0a98-120">Process the request message.</span></span>
2. <span data-ttu-id="b0a98-121">Вызовите `base.SendAsync`, чтобы отправить запрос внутреннему обработчику.</span><span class="sxs-lookup"><span data-stu-id="b0a98-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="b0a98-122">Внутренний обработчик возвращает ответное сообщение.</span><span class="sxs-lookup"><span data-stu-id="b0a98-122">The inner handler returns a response message.</span></span> <span data-ttu-id="b0a98-123">(Этот шаг является асинхронным.)</span><span class="sxs-lookup"><span data-stu-id="b0a98-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="b0a98-124">Обработайте ответ и верните его вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="b0a98-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="b0a98-125">В следующем примере показан обработчик сообщений, который добавляет пользовательский заголовок к исходящему запросу:</span><span class="sxs-lookup"><span data-stu-id="b0a98-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="b0a98-126">Вызов к `base.SendAsync` выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="b0a98-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="b0a98-127">Если после этого вызова обработчик выполняет какие – либо действия, используйте ключевое слово **await** , чтобы возобновить выполнение после завершения метода.</span><span class="sxs-lookup"><span data-stu-id="b0a98-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="b0a98-128">В следующем примере показан обработчик, который записывает коды ошибок.</span><span class="sxs-lookup"><span data-stu-id="b0a98-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="b0a98-129">Сам журнал не очень интересен, но в примере показано, как получить ответ внутри обработчика.</span><span class="sxs-lookup"><span data-stu-id="b0a98-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="b0a98-130">Добавление обработчиков сообщений в клиентский конвейер</span><span class="sxs-lookup"><span data-stu-id="b0a98-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="b0a98-131">Чтобы добавить пользовательские обработчики в **HttpClient**, используйте метод **хттпклиентфактори. Create** :</span><span class="sxs-lookup"><span data-stu-id="b0a98-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="b0a98-132">Обработчики сообщений вызываются в том порядке, в котором они передаются в метод **CREATE** .</span><span class="sxs-lookup"><span data-stu-id="b0a98-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="b0a98-133">Так как обработчики являются вложенными, ответное сообщение перемещается в другое направление.</span><span class="sxs-lookup"><span data-stu-id="b0a98-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="b0a98-134">То есть последний обработчик является первым, чтобы получить ответное сообщение.</span><span class="sxs-lookup"><span data-stu-id="b0a98-134">That is, the last handler is the first to get the response message.</span></span>
