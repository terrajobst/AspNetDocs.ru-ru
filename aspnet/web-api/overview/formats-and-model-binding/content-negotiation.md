---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: Содержимое согласование в ASP.NET Web API — ASP.NET 4.x
author: MikeWasson
description: Описывает, как веб-API ASP.NET реализует согласования содержимого HTTP для ASP.NET 4.x.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59380165"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="1debe-103">Согласование содержимого в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1debe-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="1debe-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1debe-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1debe-105">В этой статье описывается, как веб-API ASP.NET реализует согласование содержимого для ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="1debe-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="1debe-106">Спецификация HTTP (RFC 2616) определяет согласование содержимого, как «процесс выбора наиболее представлением ответ на запрос, когда доступны несколько представлений».</span><span class="sxs-lookup"><span data-stu-id="1debe-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="1debe-107">Основной механизм согласования содержимого по протоколу HTTP, эти заголовки запроса:</span><span class="sxs-lookup"><span data-stu-id="1debe-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="1debe-108">**Примите:** Типы мультимедиа, допустимые для ответа, например «application/json», «application/xml», или тип пользовательского носитель, такой как &quot;application/vnd.example+xml&quot;</span><span class="sxs-lookup"><span data-stu-id="1debe-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="1debe-109">**Accept-Charset:** Какие наборы символов допустимы, например UTF-8 или ISO-8859-1.</span><span class="sxs-lookup"><span data-stu-id="1debe-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="1debe-110">**Приемлемой кодировкой:** Какие кодировки содержимого являются допустимыми, таких как gzip.</span><span class="sxs-lookup"><span data-stu-id="1debe-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="1debe-111">**Примите язык:** Предпочтительный естественного языка, такие как «en-us».</span><span class="sxs-lookup"><span data-stu-id="1debe-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="1debe-112">Сервер также можно просмотреть другие части HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="1debe-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="1debe-113">Например если запрос содержит заголовок X-Requested-With, указывающее, является AJAX-запрос, сервер может по умолчанию JSON Если отсутствует заголовок Accept.</span><span class="sxs-lookup"><span data-stu-id="1debe-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="1debe-114">В этой статье мы рассмотрим, как веб-API использует заголовки Accept "и" Accept-Charset.</span><span class="sxs-lookup"><span data-stu-id="1debe-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="1debe-115">(В настоящее время не поддерживается встроенная Accept-Encoding "или" Accept-Language.)</span><span class="sxs-lookup"><span data-stu-id="1debe-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="1debe-116">Сериализация</span><span class="sxs-lookup"><span data-stu-id="1debe-116">Serialization</span></span>

<span data-ttu-id="1debe-117">Если контроллер Web API возвращает ресурс как тип CLR, конвейер сериализует возвращаемое значение и записывает его в тексте ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="1debe-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="1debe-118">Например рассмотрим следующее действие контроллера:</span><span class="sxs-lookup"><span data-stu-id="1debe-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="1debe-119">Клиент может передавать этого HTTP-запроса:</span><span class="sxs-lookup"><span data-stu-id="1debe-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="1debe-120">Сервер может отправить в ответ:</span><span class="sxs-lookup"><span data-stu-id="1debe-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="1debe-121">В этом примере клиент запросил JSON, Javascript или «все», что (\*/\*).</span><span class="sxs-lookup"><span data-stu-id="1debe-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="1debe-122">Сервер вернул JSON-представление `Product` объекта.</span><span class="sxs-lookup"><span data-stu-id="1debe-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="1debe-123">Обратите внимание, что имеет значение заголовка Content-Type в ответе &quot;application/json&quot;.</span><span class="sxs-lookup"><span data-stu-id="1debe-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="1debe-124">Контроллер также может возвращать **HttpResponseMessage** объекта.</span><span class="sxs-lookup"><span data-stu-id="1debe-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="1debe-125">Чтобы указать объект среды CLR, текст ответа, вызовите **CreateResponse** метод расширения:</span><span class="sxs-lookup"><span data-stu-id="1debe-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="1debe-126">Этот параметр обеспечивает больший контроль над сведения об ответе.</span><span class="sxs-lookup"><span data-stu-id="1debe-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="1debe-127">Можно задать код состояния, добавьте HTTP-заголовков и т. д.</span><span class="sxs-lookup"><span data-stu-id="1debe-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="1debe-128">Объект, который выполняет сериализацию ресурс называется *форматирования мультимедиа*.</span><span class="sxs-lookup"><span data-stu-id="1debe-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="1debe-129">Модули форматирования мультимедиа являются производными от **MediaTypeFormatter** класса.</span><span class="sxs-lookup"><span data-stu-id="1debe-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="1debe-130">Веб-API предоставляет модули форматирования мультимедиа для XML и JSON, и можно создать пользовательские модули форматирования для поддержки других типов мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="1debe-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="1debe-131">Сведения о написании пользовательского модуля форматирования, см. в разделе [модули форматирования мультимедиа](media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="1debe-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="1debe-132">Как содержимого Works согласования</span><span class="sxs-lookup"><span data-stu-id="1debe-132">How Content Negotiation Works</span></span>

<span data-ttu-id="1debe-133">Во-первых, конвейер получает **IContentNegotiator** службы из **HttpConfiguration** объекта.</span><span class="sxs-lookup"><span data-stu-id="1debe-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="1debe-134">Он также возвращает список модулей форматирования мультимедиа из **HttpConfiguration.Formatters** коллекции.</span><span class="sxs-lookup"><span data-stu-id="1debe-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="1debe-135">Затем конвейер вызывает **IContentNegotiator.Negotiate**, передавая:</span><span class="sxs-lookup"><span data-stu-id="1debe-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="1debe-136">Тип объекта для сериализации</span><span class="sxs-lookup"><span data-stu-id="1debe-136">The type of object to serialize</span></span>
- <span data-ttu-id="1debe-137">Коллекция модулей форматирования мультимедиа</span><span class="sxs-lookup"><span data-stu-id="1debe-137">The collection of media formatters</span></span>
- <span data-ttu-id="1debe-138">HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="1debe-138">The HTTP request</span></span>

<span data-ttu-id="1debe-139">**Negotiate** метод возвращает два фрагмента информации:</span><span class="sxs-lookup"><span data-stu-id="1debe-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="1debe-140">Какой модуль форматирования</span><span class="sxs-lookup"><span data-stu-id="1debe-140">Which formatter to use</span></span>
- <span data-ttu-id="1debe-141">Тип носителя для ответа</span><span class="sxs-lookup"><span data-stu-id="1debe-141">The media type for the response</span></span>

<span data-ttu-id="1debe-142">Если модуль форматирования не найден, **Negotiate** возвращает **null**, и клиент получает ошибки HTTP 406 (неприемлемо).</span><span class="sxs-lookup"><span data-stu-id="1debe-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="1debe-143">В следующем коде показано, как контроллер может напрямую вызывать согласование содержимого:</span><span class="sxs-lookup"><span data-stu-id="1debe-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="1debe-144">Этот код эквивалентен на то, что конвейер выполняет автоматически.</span><span class="sxs-lookup"><span data-stu-id="1debe-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="1debe-145">Согласователь содержимого по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1debe-145">Default Content Negotiator</span></span>

<span data-ttu-id="1debe-146">**DefaultContentNegotiator** класс предоставляет реализацию по умолчанию **IContentNegotiator**.</span><span class="sxs-lookup"><span data-stu-id="1debe-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="1debe-147">Она использует несколько критериев для выбора модуля форматирования.</span><span class="sxs-lookup"><span data-stu-id="1debe-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="1debe-148">Во-первых модуль форматирования должен иметь возможность сериализовать тип.</span><span class="sxs-lookup"><span data-stu-id="1debe-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="1debe-149">Проверка пройдена, вызвав **MediaTypeFormatter.CanWriteType**.</span><span class="sxs-lookup"><span data-stu-id="1debe-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="1debe-150">Согласователь содержимого просматривает каждый модуль форматирования затем оценивает, насколько хорошо она соответствует HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="1debe-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="1debe-151">Чтобы оценить соответствие, согласователь содержимого проверяет две вещи в модуль форматирования:</span><span class="sxs-lookup"><span data-stu-id="1debe-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="1debe-152">**SupportedMediaTypes** коллекции, которая содержит список типов носителей, поддерживаемых.</span><span class="sxs-lookup"><span data-stu-id="1debe-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="1debe-153">Согласователь содержимого предпринимается попытка этот список для запроса заголовок Accept.</span><span class="sxs-lookup"><span data-stu-id="1debe-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="1debe-154">Обратите внимание, что заголовок Accept может содержать диапазонов.</span><span class="sxs-lookup"><span data-stu-id="1debe-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="1debe-155">Например, «text/plain» — соответствие для текста /\* или \* / \*.</span><span class="sxs-lookup"><span data-stu-id="1debe-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="1debe-156">**MediaTypeMappings** коллекции, которая содержит список **MediaTypeMapping** объектов.</span><span class="sxs-lookup"><span data-stu-id="1debe-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="1debe-157">**MediaTypeMapping** класс предоставляет универсальный способ для сопоставления HTTP-запросов с типами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="1debe-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="1debe-158">Например он может сопоставить HTTP-заголовка для определенного типа носителя.</span><span class="sxs-lookup"><span data-stu-id="1debe-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="1debe-159">При наличии нескольких совпадает, совпадение с наивысшим wins коэффициент качества.</span><span class="sxs-lookup"><span data-stu-id="1debe-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="1debe-160">Пример:</span><span class="sxs-lookup"><span data-stu-id="1debe-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="1debe-161">В этом примере application/json имеет коэффициент подразумеваемых качества, 1.0, поэтому она предпочтительнее, чем application/xml.</span><span class="sxs-lookup"><span data-stu-id="1debe-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="1debe-162">Если соответствий не найдено, согласователь содержимого пытается сопоставить с типом мультимедиа тела запроса, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="1debe-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="1debe-163">Например если запрос содержит данные JSON, согласователь содержимого ищет модуль форматирования JSON.</span><span class="sxs-lookup"><span data-stu-id="1debe-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="1debe-164">Если по-прежнему нет совпадений, согласователь содержимого просто выбирает первый модуль форматирования, который может сериализовать тип.</span><span class="sxs-lookup"><span data-stu-id="1debe-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="1debe-165">Выбрать кодировку</span><span class="sxs-lookup"><span data-stu-id="1debe-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="1debe-166">После выбора модуля форматирования согласователь содержимого выбирает лучшую кодировку символов, просмотрев **SupportedEncodings** свойству в модуль форматирования и ее противопоставления заголовок Accept-Charset в запросе (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="1debe-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
