---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Действие приводит к веб-API 2 — ASP.NET 4.x
author: MikeWasson
description: Описывает преобразование возвращаемое значение из действия контроллера в ответное сообщение HTTP в ASP.NET веб-API ASP.NET 4.x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 87f71938a5c5f38d3a456ba9339540f67e236e1a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400897"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="f88c7-103">Результаты действий в веб-API 2</span><span class="sxs-lookup"><span data-stu-id="f88c7-103">Action Results in Web API 2</span></span>

<span data-ttu-id="f88c7-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f88c7-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="f88c7-105">Здесь описывается, как веб-API ASP.NET преобразует возвращаемое значение из действия контроллера в ответное сообщение HTTP.</span><span class="sxs-lookup"><span data-stu-id="f88c7-105">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="f88c7-106">Действие контроллера веб-API может возвращать одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="f88c7-106">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="f88c7-107">void</span><span class="sxs-lookup"><span data-stu-id="f88c7-107">void</span></span>
2. <span data-ttu-id="f88c7-108">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="f88c7-108">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="f88c7-109">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="f88c7-109">**IHttpActionResult**</span></span>
4. <span data-ttu-id="f88c7-110">Какое-либо иное</span><span class="sxs-lookup"><span data-stu-id="f88c7-110">Some other type</span></span>

<span data-ttu-id="f88c7-111">В зависимости от их возвращается, веб-API использует другой механизм для создания HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="f88c7-111">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="f88c7-112">Возвращаемый тип</span><span class="sxs-lookup"><span data-stu-id="f88c7-112">Return type</span></span> | <span data-ttu-id="f88c7-113">Как веб-API создает ответ</span><span class="sxs-lookup"><span data-stu-id="f88c7-113">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="f88c7-114">void</span><span class="sxs-lookup"><span data-stu-id="f88c7-114">void</span></span> | <span data-ttu-id="f88c7-115">Возвращает пустой 204 (нет содержимого)</span><span class="sxs-lookup"><span data-stu-id="f88c7-115">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="f88c7-116">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="f88c7-116">**HttpResponseMessage**</span></span> | <span data-ttu-id="f88c7-117">Преобразуйте непосредственно в сообщение ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="f88c7-117">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="f88c7-118">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="f88c7-118">**IHttpActionResult**</span></span> | <span data-ttu-id="f88c7-119">Вызовите **ExecuteAsync** для создания **HttpResponseMessage**, затем преобразовать сообщение ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="f88c7-119">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="f88c7-120">Другой тип</span><span class="sxs-lookup"><span data-stu-id="f88c7-120">Other type</span></span> | <span data-ttu-id="f88c7-121">Записи сериализованного возвращаемое значение в тексте ответа; возвращать ответ 200 (ОК).</span><span class="sxs-lookup"><span data-stu-id="f88c7-121">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="f88c7-122">В остальной части этого раздела описаны все параметры более подробно.</span><span class="sxs-lookup"><span data-stu-id="f88c7-122">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="f88c7-123">void</span><span class="sxs-lookup"><span data-stu-id="f88c7-123">void</span></span>

<span data-ttu-id="f88c7-124">Если возвращаемый тип — `void`, веб-API просто возвращает пустой ответ HTTP с кодом состояния 204 (нет содержимого).</span><span class="sxs-lookup"><span data-stu-id="f88c7-124">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="f88c7-125">Пример контроллера:</span><span class="sxs-lookup"><span data-stu-id="f88c7-125">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="f88c7-126">HTTP-ответа:</span><span class="sxs-lookup"><span data-stu-id="f88c7-126">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="f88c7-127">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="f88c7-127">HttpResponseMessage</span></span>

<span data-ttu-id="f88c7-128">Если действие возвращает [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), веб-API преобразует возвращаемое значение непосредственно в ответное сообщение HTTP с помощью свойств **HttpResponseMessage** объекта для заполнения ответ.</span><span class="sxs-lookup"><span data-stu-id="f88c7-128">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="f88c7-129">Этот параметр обеспечивает большую контроля над ответного сообщения.</span><span class="sxs-lookup"><span data-stu-id="f88c7-129">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="f88c7-130">Например следующее действие контроллера задает заголовок Cache-Control.</span><span class="sxs-lookup"><span data-stu-id="f88c7-130">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="f88c7-131">Ответ</span><span class="sxs-lookup"><span data-stu-id="f88c7-131">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="f88c7-132">Если передать модель домена, чтобы **CreateResponse** метод, веб-API использует [форматирования мультимедиа](../formats-and-model-binding/media-formatters.md) для записи сериализованной модели в тексте ответа.</span><span class="sxs-lookup"><span data-stu-id="f88c7-132">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="f88c7-133">Веб-API использует заголовок Accept в запросе для выбора модуля форматирования.</span><span class="sxs-lookup"><span data-stu-id="f88c7-133">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="f88c7-134">Дополнительные сведения см. в разделе [согласование содержимого](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="f88c7-134">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="f88c7-135">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="f88c7-135">IHttpActionResult</span></span>

<span data-ttu-id="f88c7-136">**IHttpActionResult** в веб-API 2 был представлен интерфейс.</span><span class="sxs-lookup"><span data-stu-id="f88c7-136">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="f88c7-137">По сути, он определяет **HttpResponseMessage** фабрики.</span><span class="sxs-lookup"><span data-stu-id="f88c7-137">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="f88c7-138">Ниже приведены некоторые преимущества использования **IHttpActionResult** интерфейса:</span><span class="sxs-lookup"><span data-stu-id="f88c7-138">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="f88c7-139">Упрощает [модульное тестирование](../testing-and-debugging/unit-testing-controllers-in-web-api.md) контроллеров.</span><span class="sxs-lookup"><span data-stu-id="f88c7-139">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="f88c7-140">Перемещает общую логику для создания HTTP-ответов в отдельные классы.</span><span class="sxs-lookup"><span data-stu-id="f88c7-140">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="f88c7-141">Делает цель более понятным, действие контроллера, скрывая низкоуровневые сведения о создании ответа.</span><span class="sxs-lookup"><span data-stu-id="f88c7-141">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="f88c7-142">**IHttpActionResult** содержит один метод, **ExecuteAsync**, которая асинхронно создает **HttpResponseMessage** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="f88c7-142">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="f88c7-143">Возвращает действие контроллера **IHttpActionResult**, вызывает веб-API **ExecuteAsync** метод для создания **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="f88c7-143">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="f88c7-144">То она преобразует **HttpResponseMessage** в ответное сообщение HTTP.</span><span class="sxs-lookup"><span data-stu-id="f88c7-144">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="f88c7-145">Вот простая реализация **IHttpActionResult** , создающий формат ответа:</span><span class="sxs-lookup"><span data-stu-id="f88c7-145">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="f88c7-146">Пример действия контроллера:</span><span class="sxs-lookup"><span data-stu-id="f88c7-146">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="f88c7-147">Ответ</span><span class="sxs-lookup"><span data-stu-id="f88c7-147">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="f88c7-148">Более часто, вы воспользуетесь **IHttpActionResult** реализации, определенных в **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** пространства имен.</span><span class="sxs-lookup"><span data-stu-id="f88c7-148">More often, you will use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="f88c7-149">**ApiController** класс определяет вспомогательные методы, которые возвращают результаты этих встроенных действий.</span><span class="sxs-lookup"><span data-stu-id="f88c7-149">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="f88c7-150">В следующем примере, если запрос не совпадает с Идентификатором существующего продукта, контроллер вызывает [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) для создания ответа 404 (не найдено).</span><span class="sxs-lookup"><span data-stu-id="f88c7-150">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="f88c7-151">В противном случае вызывает контроллер [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), который создает ответ 200 (ОК), содержащий продукта.</span><span class="sxs-lookup"><span data-stu-id="f88c7-151">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="f88c7-152">Другие типы возвращаемого значения</span><span class="sxs-lookup"><span data-stu-id="f88c7-152">Other Return Types</span></span>

<span data-ttu-id="f88c7-153">Для всех других типов возвращаемого значения, веб-API использует [форматирования мультимедиа](../formats-and-model-binding/media-formatters.md) для сериализации возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="f88c7-153">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="f88c7-154">Веб-API записывает сериализованное значение в тексте ответа.</span><span class="sxs-lookup"><span data-stu-id="f88c7-154">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="f88c7-155">Код состояния ответа: 200 (ОК).</span><span class="sxs-lookup"><span data-stu-id="f88c7-155">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="f88c7-156">Недостаток этого подхода является то, что нельзя напрямую возвращать код ошибки, например 404.</span><span class="sxs-lookup"><span data-stu-id="f88c7-156">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="f88c7-157">Тем не менее, можно создавать **HttpResponseException** для кодов ошибок.</span><span class="sxs-lookup"><span data-stu-id="f88c7-157">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="f88c7-158">Дополнительные сведения см. в разделе [обработка исключений в веб-API ASP.NET](../error-handling/exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="f88c7-158">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="f88c7-159">Веб-API использует заголовок Accept в запросе для выбора модуля форматирования.</span><span class="sxs-lookup"><span data-stu-id="f88c7-159">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="f88c7-160">Дополнительные сведения см. в разделе [согласование содержимого](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="f88c7-160">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="f88c7-161">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="f88c7-161">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="f88c7-162">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="f88c7-162">Example response:</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
