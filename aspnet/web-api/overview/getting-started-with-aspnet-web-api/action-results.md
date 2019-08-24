---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Результаты действия в веб-API 2 — ASP.NET 4. x
author: MikeWasson
description: Описывает, как веб-API ASP.NET преобразует возвращаемое значение из действия контроллера в ответное сообщение HTTP в ASP.NET 4. x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 1eaaf8e87168096683212fa66d3ddf415ad6b22b
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000721"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="2b82d-103">Результаты действий в веб-API 2</span><span class="sxs-lookup"><span data-stu-id="2b82d-103">Action Results in Web API 2</span></span>

<span data-ttu-id="2b82d-104">В этом разделе описано, как веб-API ASP.NET преобразует возвращаемое значение из действия контроллера в сообщение ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b82d-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="2b82d-105">Действие контроллера веб-API может возвращать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="2b82d-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="2b82d-106">void</span><span class="sxs-lookup"><span data-stu-id="2b82d-106">void</span></span>
2. <span data-ttu-id="2b82d-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="2b82d-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="2b82d-108">**ихттпактионресулт**</span><span class="sxs-lookup"><span data-stu-id="2b82d-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="2b82d-109">Другой тип</span><span class="sxs-lookup"><span data-stu-id="2b82d-109">Some other type</span></span>

<span data-ttu-id="2b82d-110">В зависимости от того, какое из этих данных возвращается, веб-API использует другой механизм для создания ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b82d-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="2b82d-111">Возвращаемый тип</span><span class="sxs-lookup"><span data-stu-id="2b82d-111">Return type</span></span> | <span data-ttu-id="2b82d-112">Как веб-API создает ответ</span><span class="sxs-lookup"><span data-stu-id="2b82d-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="2b82d-113">void</span><span class="sxs-lookup"><span data-stu-id="2b82d-113">void</span></span> | <span data-ttu-id="2b82d-114">Возврат пустого значения 204 (без содержимого)</span><span class="sxs-lookup"><span data-stu-id="2b82d-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="2b82d-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="2b82d-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="2b82d-116">Преобразование непосредственно в ответное сообщение HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b82d-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="2b82d-117">**ихттпактионресулт**</span><span class="sxs-lookup"><span data-stu-id="2b82d-117">**IHttpActionResult**</span></span> | <span data-ttu-id="2b82d-118">Вызовите **ExecuteAsync** , чтобы создать **HttpResponseMessage**, а затем преобразуйте его в ответное сообщение HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b82d-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="2b82d-119">Другой тип</span><span class="sxs-lookup"><span data-stu-id="2b82d-119">Other type</span></span> | <span data-ttu-id="2b82d-120">Запишите сериализованное возвращаемое значение в текст ответа. Возвращает 200 (ОК).</span><span class="sxs-lookup"><span data-stu-id="2b82d-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="2b82d-121">В оставшейся части этого раздела каждый параметр описан более подробно.</span><span class="sxs-lookup"><span data-stu-id="2b82d-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="2b82d-122">void</span><span class="sxs-lookup"><span data-stu-id="2b82d-122">void</span></span>

<span data-ttu-id="2b82d-123">Если возвращаемый тип — `void`, веб-API просто возвращает пустой ответ HTTP с кодом состояния 204 (нет содержимого).</span><span class="sxs-lookup"><span data-stu-id="2b82d-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="2b82d-124">Пример контроллера:</span><span class="sxs-lookup"><span data-stu-id="2b82d-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="2b82d-125">HTTP-ответ:</span><span class="sxs-lookup"><span data-stu-id="2b82d-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="2b82d-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="2b82d-126">HttpResponseMessage</span></span>

<span data-ttu-id="2b82d-127">Если действие возвращает [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), веб-API преобразует возвращаемое значение непосредственно в ответное сообщение HTTP, используя свойства объекта **HttpResponseMessage** для заполнения ответа.</span><span class="sxs-lookup"><span data-stu-id="2b82d-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="2b82d-128">Этот параметр обеспечивает большой контроль над ответным сообщением.</span><span class="sxs-lookup"><span data-stu-id="2b82d-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="2b82d-129">Например, следующее действие контроллера задает заголовок Cache-Control.</span><span class="sxs-lookup"><span data-stu-id="2b82d-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="2b82d-130">Ответ</span><span class="sxs-lookup"><span data-stu-id="2b82d-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="2b82d-131">При передаче модели предметной области в метод **Креатереспонсе** веб-API использует [модуль форматирования мультимедиа](../formats-and-model-binding/media-formatters.md) для записи сериализованной модели в текст ответа.</span><span class="sxs-lookup"><span data-stu-id="2b82d-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="2b82d-132">Веб-API использует заголовок Accept в запросе для выбора модуля форматирования.</span><span class="sxs-lookup"><span data-stu-id="2b82d-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="2b82d-133">Дополнительные сведения см. в разделе [Согласование содержимого](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="2b82d-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="2b82d-134">ихттпактионресулт</span><span class="sxs-lookup"><span data-stu-id="2b82d-134">IHttpActionResult</span></span>

<span data-ttu-id="2b82d-135">Интерфейс **ихттпактионресулт** появился в веб-API 2.</span><span class="sxs-lookup"><span data-stu-id="2b82d-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="2b82d-136">По сути, он определяет фабрику **HttpResponseMessage** .</span><span class="sxs-lookup"><span data-stu-id="2b82d-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="2b82d-137">Ниже приведены некоторые преимущества использования интерфейса **ихттпактионресулт** .</span><span class="sxs-lookup"><span data-stu-id="2b82d-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="2b82d-138">Упрощает [модульное тестирование](../testing-and-debugging/unit-testing-controllers-in-web-api.md) контроллеров.</span><span class="sxs-lookup"><span data-stu-id="2b82d-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="2b82d-139">Перемещает общую логику для создания HTTP-ответов в отдельные классы.</span><span class="sxs-lookup"><span data-stu-id="2b82d-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="2b82d-140">Делает цель действия контроллера более четкой, скрывая низкоуровневые сведения о создании ответа.</span><span class="sxs-lookup"><span data-stu-id="2b82d-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="2b82d-141">**Ихттпактионресулт** содержит единственный метод **ExecuteAsync**, который асинхронно создает экземпляр **HttpResponseMessage** .</span><span class="sxs-lookup"><span data-stu-id="2b82d-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="2b82d-142">Если действие контроллера возвращает **ихттпактионресулт**, веб-API вызывает метод **ExecuteAsync** для создания **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="2b82d-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="2b82d-143">Затем он преобразует **HttpResponseMessage** в сообщение HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="2b82d-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="2b82d-144">Ниже приведена простая реализация **ихттпактионресулт** , которая создает ответ в виде обычного текста:</span><span class="sxs-lookup"><span data-stu-id="2b82d-144">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="2b82d-145">Пример действия контроллера:</span><span class="sxs-lookup"><span data-stu-id="2b82d-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="2b82d-146">Ответ</span><span class="sxs-lookup"><span data-stu-id="2b82d-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="2b82d-147">Чаще всего используются реализации **ихттпактионресулт** , определенные в пространстве имен **[System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="2b82d-147">More often, you use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="2b82d-148">Класс **ApiController** определяет вспомогательные методы, которые возвращают эти встроенные результаты действия.</span><span class="sxs-lookup"><span data-stu-id="2b82d-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="2b82d-149">В следующем примере, если запрос не соответствует существующему ИДЕНТИФИКАТОРу продукта, контроллер вызывает [ApiController. NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) для создания ответа 404 (не найдено).</span><span class="sxs-lookup"><span data-stu-id="2b82d-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="2b82d-150">В противном случае контроллер вызывает [ApiController. ОК](https://msdn.microsoft.com/library/dn314591.aspx), который создает ответ 200 (ОК), содержащий продукт.</span><span class="sxs-lookup"><span data-stu-id="2b82d-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="2b82d-151">Другие типы возвращаемых значения</span><span class="sxs-lookup"><span data-stu-id="2b82d-151">Other Return Types</span></span>

<span data-ttu-id="2b82d-152">Для всех остальных возвращаемых типов веб-API использует [модуль форматирования мультимедиа](../formats-and-model-binding/media-formatters.md) для сериализации возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="2b82d-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="2b82d-153">Веб-API записывает сериализованное значение в текст ответа.</span><span class="sxs-lookup"><span data-stu-id="2b82d-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="2b82d-154">Код состояния отклика — 200 (ОК).</span><span class="sxs-lookup"><span data-stu-id="2b82d-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="2b82d-155">Недостаток этого подхода заключается в том, что нельзя напрямую возвращать код ошибки, например 404.</span><span class="sxs-lookup"><span data-stu-id="2b82d-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="2b82d-156">Однако можно создать **хттпреспонсиксцептион** для кодов ошибок.</span><span class="sxs-lookup"><span data-stu-id="2b82d-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="2b82d-157">Дополнительные сведения см. [в разделе Обработка исключений в веб-API ASP.NET](../error-handling/exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="2b82d-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="2b82d-158">Веб-API использует заголовок Accept в запросе для выбора модуля форматирования.</span><span class="sxs-lookup"><span data-stu-id="2b82d-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="2b82d-159">Дополнительные сведения см. в разделе [Согласование содержимого](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="2b82d-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="2b82d-160">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="2b82d-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="2b82d-161">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="2b82d-161">Example response</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
