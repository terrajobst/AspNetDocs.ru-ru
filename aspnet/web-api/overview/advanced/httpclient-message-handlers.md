---
uid: web-api/overview/advanced/httpclient-message-handlers
title: Обработчики сообщений HttpClient в ASP.NET Web API — ASP.NET 4.x
author: MikeWasson
description: Создание обработчиков пользовательских сообщений для веб-API ASP.NET в ASP.NET 4.x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: bd52396064cd7007ee17705ba86b02aaf27cb4f0
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59401729"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="eaf24-103">Обработчики сообщений HttpClient в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="eaf24-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="eaf24-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="eaf24-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="eaf24-105">Объект *обработчик сообщений* — это класс, который получает HTTP-запрос и возвращает ответ HTTP.</span><span class="sxs-lookup"><span data-stu-id="eaf24-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="eaf24-106">Как правило ряд обработчиков сообщений соединяются друг с другом.</span><span class="sxs-lookup"><span data-stu-id="eaf24-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="eaf24-107">Первый обработчик получает запрос HTTP, обрабатывает и предоставляет запрос к следующий обработчик.</span><span class="sxs-lookup"><span data-stu-id="eaf24-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="eaf24-108">Рано или поздно ответа создается и возвращается в цепочке.</span><span class="sxs-lookup"><span data-stu-id="eaf24-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="eaf24-109">Такая модель называется *делегирование* обработчика.</span><span class="sxs-lookup"><span data-stu-id="eaf24-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="eaf24-110">На стороне клиента **HttpClient** класс использует обработчик сообщений для обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="eaf24-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="eaf24-111">Обработчик по умолчанию является **HttpClientHandler**, который отправляет запрос по сети и получает ответ от сервера.</span><span class="sxs-lookup"><span data-stu-id="eaf24-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="eaf24-112">Вы можете вставить обработчики пользовательских сообщений в конвейер клиента:</span><span class="sxs-lookup"><span data-stu-id="eaf24-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="eaf24-113">Веб-API ASP.NET также использует обработчики сообщений на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="eaf24-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="eaf24-114">Дополнительные сведения см. в разделе [обработчиков сообщений HTTP](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="eaf24-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="eaf24-115">Обработчики пользовательских сообщений</span><span class="sxs-lookup"><span data-stu-id="eaf24-115">Custom Message Handlers</span></span>

<span data-ttu-id="eaf24-116">Чтобы написать обработчик пользовательского сообщения, являются производными от **System.Net.Http.DelegatingHandler** и переопределить **SendAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="eaf24-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="eaf24-117">Ниже представлена подпись метода:</span><span class="sxs-lookup"><span data-stu-id="eaf24-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="eaf24-118">Этот метод принимает **HttpRequestMessage** как входных данных и асинхронно возвращает **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="eaf24-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="eaf24-119">Типичной реализации выполняет следующие функции:</span><span class="sxs-lookup"><span data-stu-id="eaf24-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="eaf24-120">Процесс сообщения запроса.</span><span class="sxs-lookup"><span data-stu-id="eaf24-120">Process the request message.</span></span>
2. <span data-ttu-id="eaf24-121">Вызовите `base.SendAsync` для отправки запроса на внутренний обработчик.</span><span class="sxs-lookup"><span data-stu-id="eaf24-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="eaf24-122">Внутренний обработчик возвращает ответное сообщение.</span><span class="sxs-lookup"><span data-stu-id="eaf24-122">The inner handler returns a response message.</span></span> <span data-ttu-id="eaf24-123">(Этот шаг выполняется асинхронно).</span><span class="sxs-lookup"><span data-stu-id="eaf24-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="eaf24-124">Обработать ответ и вернуть его вызывающей стороне.</span><span class="sxs-lookup"><span data-stu-id="eaf24-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="eaf24-125">В следующем примере обработчик сообщений, который добавляет пользовательский заголовок исходящего запроса:</span><span class="sxs-lookup"><span data-stu-id="eaf24-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="eaf24-126">Вызов `base.SendAsync` является асинхронным.</span><span class="sxs-lookup"><span data-stu-id="eaf24-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="eaf24-127">Если обработчик не выполняет никакой работы после этого вызова, используйте **await** ключевое слово для возобновления выполнения после завершения работы метода.</span><span class="sxs-lookup"><span data-stu-id="eaf24-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="eaf24-128">Пример обработчика, который регистрирует коды ошибок.</span><span class="sxs-lookup"><span data-stu-id="eaf24-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="eaf24-129">Ведение журнала, сам не очень интересно, но примере показано, как получить в ответ внутри обработчика.</span><span class="sxs-lookup"><span data-stu-id="eaf24-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="eaf24-130">Добавление обработчиков сообщений в конвейер, клиент</span><span class="sxs-lookup"><span data-stu-id="eaf24-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="eaf24-131">Добавление пользовательских обработчиков для **HttpClient**, использовать **HttpClientFactory.Create** метод:</span><span class="sxs-lookup"><span data-stu-id="eaf24-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="eaf24-132">Обработчики сообщений вызываются в порядке, который можно передать их в **создать** метод.</span><span class="sxs-lookup"><span data-stu-id="eaf24-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="eaf24-133">Так как обработчики являются вложенными, ответное сообщение перемещается в обратном направлении.</span><span class="sxs-lookup"><span data-stu-id="eaf24-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="eaf24-134">Последним обработчиком является первым ответного сообщения.</span><span class="sxs-lookup"><span data-stu-id="eaf24-134">That is, the last handler is the first to get the response message.</span></span>
