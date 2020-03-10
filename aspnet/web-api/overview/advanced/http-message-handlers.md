---
uid: web-api/overview/advanced/http-message-handlers
title: Обработчики сообщений HTTP в веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: Обзор обработчиков сообщений HTTP в веб-API ASP.NET для ASP.NET 4. x
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504930"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="63396-103">Обработчики сообщений HTTP в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="63396-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="63396-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="63396-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="63396-105">*Обработчик сообщений* — это класс, который получает HTTP-запрос и ВОЗВРАЩАЕТ ответ HTTP.</span><span class="sxs-lookup"><span data-stu-id="63396-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="63396-106">Обработчики сообщений являются производными от абстрактного класса **HttpMessageHandler** .</span><span class="sxs-lookup"><span data-stu-id="63396-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="63396-107">Как правило, ряд обработчиков сообщений объединяется в цепочку.</span><span class="sxs-lookup"><span data-stu-id="63396-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="63396-108">Первый обработчик получает HTTP-запрос, выполняет некоторую обработку и передает запрос следующему обработчику.</span><span class="sxs-lookup"><span data-stu-id="63396-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="63396-109">В какой-то момент ответ создается и помещается в резервную копию цепочки.</span><span class="sxs-lookup"><span data-stu-id="63396-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="63396-110">Этот шаблон называется *делегированным* обработчиком.</span><span class="sxs-lookup"><span data-stu-id="63396-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="63396-111">Обработчики сообщений на стороне сервера</span><span class="sxs-lookup"><span data-stu-id="63396-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="63396-112">На стороне сервера конвейер веб-API использует некоторые встроенные обработчики сообщений:</span><span class="sxs-lookup"><span data-stu-id="63396-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="63396-113">**HttpServer** получает запрос от узла.</span><span class="sxs-lookup"><span data-stu-id="63396-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="63396-114">**Хттпраутингдиспатчер** отправляет запрос на основе маршрута.</span><span class="sxs-lookup"><span data-stu-id="63396-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="63396-115">**Хттпконтроллердиспатчер** отправляет запрос в контроллер веб-API.</span><span class="sxs-lookup"><span data-stu-id="63396-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="63396-116">К конвейеру можно добавить пользовательские обработчики.</span><span class="sxs-lookup"><span data-stu-id="63396-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="63396-117">Обработчики сообщений хорошо подходят для проблем с пересечением, которые работают на уровне HTTP-сообщений (а не действий контроллера).</span><span class="sxs-lookup"><span data-stu-id="63396-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="63396-118">Например, обработчик сообщений может:</span><span class="sxs-lookup"><span data-stu-id="63396-118">For example, a message handler might:</span></span>

- <span data-ttu-id="63396-119">Чтение или изменение заголовков запросов.</span><span class="sxs-lookup"><span data-stu-id="63396-119">Read or modify request headers.</span></span>
- <span data-ttu-id="63396-120">Добавление заголовка ответа в ответы.</span><span class="sxs-lookup"><span data-stu-id="63396-120">Add a response header to responses.</span></span>
- <span data-ttu-id="63396-121">Проверка запросов перед достижением контроллера.</span><span class="sxs-lookup"><span data-stu-id="63396-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="63396-122">На этой схеме показаны два пользовательских обработчика, вставленных в конвейер:</span><span class="sxs-lookup"><span data-stu-id="63396-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="63396-123">На стороне клиента HttpClient также использует обработчики сообщений.</span><span class="sxs-lookup"><span data-stu-id="63396-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="63396-124">Дополнительные сведения см. в разделе [обработчики сообщений HttpClient](httpclient-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="63396-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="63396-125">Пользовательские обработчики сообщений</span><span class="sxs-lookup"><span data-stu-id="63396-125">Custom Message Handlers</span></span>

<span data-ttu-id="63396-126">Для написания пользовательского обработчика сообщений следует использовать класс **System .NET. http. DelegatingHandler** и переопределить метод **SendAsync** .</span><span class="sxs-lookup"><span data-stu-id="63396-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="63396-127">Этот метод имеет следующую сигнатуру:</span><span class="sxs-lookup"><span data-stu-id="63396-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="63396-128">Метод принимает **HttpRequestMessage** в качестве входных данных и асинхронно возвращает **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="63396-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="63396-129">Типичная реализация выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="63396-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="63396-130">Обработать сообщение запроса.</span><span class="sxs-lookup"><span data-stu-id="63396-130">Process the request message.</span></span>
2. <span data-ttu-id="63396-131">Вызовите `base.SendAsync`, чтобы отправить запрос внутреннему обработчику.</span><span class="sxs-lookup"><span data-stu-id="63396-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="63396-132">Внутренний обработчик возвращает ответное сообщение.</span><span class="sxs-lookup"><span data-stu-id="63396-132">The inner handler returns a response message.</span></span> <span data-ttu-id="63396-133">(Этот шаг является асинхронным.)</span><span class="sxs-lookup"><span data-stu-id="63396-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="63396-134">Обработайте ответ и верните его вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="63396-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="63396-135">Ниже приведен простой пример.</span><span class="sxs-lookup"><span data-stu-id="63396-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="63396-136">Вызов к `base.SendAsync` выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="63396-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="63396-137">Если после этого вызова обработчик выполняет любую работу, используйте ключевое слово **await** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="63396-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>

<span data-ttu-id="63396-138">Делегирующий обработчик также может пропустить внутренний обработчик и создать ответ напрямую:</span><span class="sxs-lookup"><span data-stu-id="63396-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="63396-139">Если делегирующий обработчик создает ответ без вызова `base.SendAsync`, запрос пропускает оставшуюся часть конвейера.</span><span class="sxs-lookup"><span data-stu-id="63396-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="63396-140">Это может быть полезно для обработчика, который проверяет запрос (создает ответ об ошибке).</span><span class="sxs-lookup"><span data-stu-id="63396-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="63396-141">Добавление обработчика в конвейер</span><span class="sxs-lookup"><span data-stu-id="63396-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="63396-142">Чтобы добавить обработчик сообщений на стороне сервера, добавьте обработчик в коллекцию **HttpConfiguration. мессажехандлерс** .</span><span class="sxs-lookup"><span data-stu-id="63396-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="63396-143">Если для создания проекта использовался шаблон "веб-приложение ASP.NET MVC 4", это можно сделать в классе **WebApiConfig** :</span><span class="sxs-lookup"><span data-stu-id="63396-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="63396-144">Обработчики сообщений вызываются в том же порядке, в котором они отображаются в коллекции **мессажехандлерс** .</span><span class="sxs-lookup"><span data-stu-id="63396-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="63396-145">Так как они вложены, ответное сообщение перемещается в другое направление.</span><span class="sxs-lookup"><span data-stu-id="63396-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="63396-146">То есть последний обработчик является первым, чтобы получить ответное сообщение.</span><span class="sxs-lookup"><span data-stu-id="63396-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="63396-147">Обратите внимание, что не нужно задавать внутренние обработчики; платформа веб-API автоматически подключает обработчики сообщений.</span><span class="sxs-lookup"><span data-stu-id="63396-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="63396-148">При [размещении на собственном узле](../older-versions/self-host-a-web-api.md)создайте экземпляр класса **хттпселфхостконфигуратион** и добавьте обработчики в коллекцию **мессажехандлерс** .</span><span class="sxs-lookup"><span data-stu-id="63396-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="63396-149">Теперь рассмотрим некоторые примеры пользовательских обработчиков сообщений.</span><span class="sxs-lookup"><span data-stu-id="63396-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="63396-150">Пример: X-HTTP-Method-override</span><span class="sxs-lookup"><span data-stu-id="63396-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="63396-151">Переопределение X-HTTP-Method-override не является стандартным заголовком HTTP.</span><span class="sxs-lookup"><span data-stu-id="63396-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="63396-152">Он предназначен для клиентов, которые не могут отправлять определенные типы HTTP-запросов, такие как "поместить" или "Удалить".</span><span class="sxs-lookup"><span data-stu-id="63396-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="63396-153">Вместо этого клиент отправляет запрос POST и задает для заголовка X-HTTP-Method-override нужный метод.</span><span class="sxs-lookup"><span data-stu-id="63396-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="63396-154">Пример:</span><span class="sxs-lookup"><span data-stu-id="63396-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="63396-155">Ниже приведен обработчик сообщений, который добавляет поддержку для переопределения X-HTTP-Method:</span><span class="sxs-lookup"><span data-stu-id="63396-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="63396-156">В методе **SendAsync** обработчик проверяет, является ли сообщение запроса запросом POST, и содержит ли он заголовок X-HTTP-Method-override.</span><span class="sxs-lookup"><span data-stu-id="63396-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="63396-157">Если да, то он проверяет значение заголовка, а затем изменяет метод запроса.</span><span class="sxs-lookup"><span data-stu-id="63396-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="63396-158">Наконец, обработчик вызывает `base.SendAsync`, чтобы передать сообщение следующему обработчику.</span><span class="sxs-lookup"><span data-stu-id="63396-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="63396-159">Когда запрос достигает класса **хттпконтроллердиспатчер** , **хттпконтроллердиспатчер** направит запрос на основе обновленного метода запроса.</span><span class="sxs-lookup"><span data-stu-id="63396-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="63396-160">Пример. Добавление пользовательского заголовка ответа</span><span class="sxs-lookup"><span data-stu-id="63396-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="63396-161">Ниже приведен обработчик сообщений, который добавляет пользовательский заголовок к каждому ответному сообщению:</span><span class="sxs-lookup"><span data-stu-id="63396-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="63396-162">Сначала обработчик вызывает `base.SendAsync`, чтобы передать запрос обработчику внутреннего сообщения.</span><span class="sxs-lookup"><span data-stu-id="63396-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="63396-163">Внутренний обработчик возвращает ответное сообщение, но асинхронно использует **задачу&lt;t&gt;** объект.</span><span class="sxs-lookup"><span data-stu-id="63396-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="63396-164">Ответное сообщение недоступно, пока `base.SendAsync` не завершится асинхронно.</span><span class="sxs-lookup"><span data-stu-id="63396-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="63396-165">В этом примере ключевое слово **await** используется для выполнения работы в асинхронном режиме после завершения `SendAsync`.</span><span class="sxs-lookup"><span data-stu-id="63396-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="63396-166">Если вы нацеливание на .NET Framework 4,0, используйте&gt;**Task**&lt;t **. Метод ContinueWith** :</span><span class="sxs-lookup"><span data-stu-id="63396-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="63396-167">Пример. Проверка ключа API</span><span class="sxs-lookup"><span data-stu-id="63396-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="63396-168">Некоторые веб-службы требует, чтобы клиенты включали ключ API в свой запрос.</span><span class="sxs-lookup"><span data-stu-id="63396-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="63396-169">В следующем примере показано, как обработчик сообщений может проверить запросы на наличие допустимого ключа API:</span><span class="sxs-lookup"><span data-stu-id="63396-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="63396-170">Этот обработчик выполняет поиск ключа API в строке запроса URI.</span><span class="sxs-lookup"><span data-stu-id="63396-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="63396-171">(В этом примере предполагается, что ключ является статической строкой.</span><span class="sxs-lookup"><span data-stu-id="63396-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="63396-172">Реальная реализация, вероятно, будет использовать более сложную проверку.) Если строка запроса содержит ключ, обработчик передает запрос внутреннему обработчику.</span><span class="sxs-lookup"><span data-stu-id="63396-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="63396-173">Если у запроса нет допустимого ключа, обработчик создает ответное сообщение с состоянием 403, запрещено.</span><span class="sxs-lookup"><span data-stu-id="63396-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="63396-174">В этом случае обработчик не вызывает `base.SendAsync`, поэтому внутренний обработчик никогда не получает запрос и не выполняет контроллер.</span><span class="sxs-lookup"><span data-stu-id="63396-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="63396-175">Таким образом, контроллер может предположить, что все входящие запросы имеют действительный ключ API.</span><span class="sxs-lookup"><span data-stu-id="63396-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="63396-176">Если ключ API применяется только к определенным действиям контроллера, рассмотрите возможность использования фильтра действий вместо обработчика сообщений.</span><span class="sxs-lookup"><span data-stu-id="63396-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="63396-177">Фильтры действий выполняются после выполнения маршрутизации URI.</span><span class="sxs-lookup"><span data-stu-id="63396-177">Action filters run after URI routing is performed.</span></span>

## <a name="per-route-message-handlers"></a><span data-ttu-id="63396-178">Обработчики сообщений для каждого маршрута</span><span class="sxs-lookup"><span data-stu-id="63396-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="63396-179">Обработчики в коллекции **HttpConfiguration. мессажехандлерс** применяются глобально.</span><span class="sxs-lookup"><span data-stu-id="63396-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="63396-180">Кроме того, можно добавить обработчик сообщений к конкретному маршруту при определении маршрута:</span><span class="sxs-lookup"><span data-stu-id="63396-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="63396-181">В этом примере, если URI запроса соответствует "Route2", запрос отправляется в `MessageHandler2`.</span><span class="sxs-lookup"><span data-stu-id="63396-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="63396-182">На следующей схеме показан конвейер для этих двух маршрутов.</span><span class="sxs-lookup"><span data-stu-id="63396-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="63396-183">Обратите внимание, что `MessageHandler2` заменяет **хттпконтроллердиспатчер**по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="63396-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="63396-184">В этом примере `MessageHandler2` создает ответ, и запросы, соответствующие "Route2", никогда не переходят к контроллеру.</span><span class="sxs-lookup"><span data-stu-id="63396-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="63396-185">Это позволяет заменить весь механизм контроллера веб-API собственной пользовательской конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="63396-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="63396-186">Кроме того, обработчик сообщений для каждого маршрута может делегироваться **хттпконтроллердиспатчер**, который затем отправляется контроллеру.</span><span class="sxs-lookup"><span data-stu-id="63396-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="63396-187">В следующем примере кода показано, как настроить этот маршрут:</span><span class="sxs-lookup"><span data-stu-id="63396-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
