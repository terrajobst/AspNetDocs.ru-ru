---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: Согласование содержимого в веб-API ASP.NET ASP.NET 4. x
author: MikeWasson
description: Описывает, как веб-API ASP.NET реализует согласование содержимого HTTP для ASP.NET 4. x.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504660"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="bb282-103">Согласование содержимого в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bb282-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="bb282-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bb282-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bb282-105">В этой статье описывается, как веб-API ASP.NET реализует согласование содержимого для ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="bb282-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="bb282-106">Спецификация HTTP (RFC 2616) определяет согласование содержимого как "процесс выбора наилучшего представления для данного ответа, если доступно несколько представлений".</span><span class="sxs-lookup"><span data-stu-id="bb282-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="bb282-107">Основным механизмом согласования содержимого в HTTP являются следующие заголовки запросов:</span><span class="sxs-lookup"><span data-stu-id="bb282-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="bb282-108">**Принять:** Типы мультимедиа, приемлемые для ответа, такие как "Application/JSON", "Application/XML", или пользовательский тип мультимедиа, например &quot;application/vnd. example + XML&quot;</span><span class="sxs-lookup"><span data-stu-id="bb282-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="bb282-109">**Accept-Charset:** Допустимые наборы символов, такие как UTF-8 или ISO 8859-1.</span><span class="sxs-lookup"><span data-stu-id="bb282-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="bb282-110">**Accept — кодировка:** Допустимые кодировки содержимого, например gzip.</span><span class="sxs-lookup"><span data-stu-id="bb282-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="bb282-111">**Accept — Language:** Предпочтительный естественный язык, например "en-US".</span><span class="sxs-lookup"><span data-stu-id="bb282-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="bb282-112">Сервер также может просматривать другие части HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="bb282-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="bb282-113">Например, если запрос содержит заголовок X-Request-with, указывающий на запрос AJAX, то сервер может по умолчанию использовать JSON, если заголовок Accept отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bb282-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="bb282-114">В этой статье мы рассмотрим, как веб-API использует заголовки Accept и Accept-CharSet.</span><span class="sxs-lookup"><span data-stu-id="bb282-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="bb282-115">(В настоящее время отсутствует встроенная поддержка Accept-Encoding или Accept-Language.)</span><span class="sxs-lookup"><span data-stu-id="bb282-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="bb282-116">Сериализация</span><span class="sxs-lookup"><span data-stu-id="bb282-116">Serialization</span></span>

<span data-ttu-id="bb282-117">Если контроллер веб-API возвращает ресурс как тип CLR, конвейер сериализует возвращаемое значение и записывает его в текст ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="bb282-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="bb282-118">Например, рассмотрим следующее действие контроллера:</span><span class="sxs-lookup"><span data-stu-id="bb282-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="bb282-119">Клиент может отправить этот HTTP-запрос:</span><span class="sxs-lookup"><span data-stu-id="bb282-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="bb282-120">В ответ сервер может отправить следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="bb282-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="bb282-121">В этом примере клиент запросил либо JSON, JavaScript, либо "что угодно" (\*/\*).</span><span class="sxs-lookup"><span data-stu-id="bb282-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="bb282-122">Сервер ответил с помощью JSON-представления объекта `Product`.</span><span class="sxs-lookup"><span data-stu-id="bb282-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="bb282-123">Обратите внимание, что заголовок Content-Type в ответе имеет значение &quot;Application/JSON&quot;.</span><span class="sxs-lookup"><span data-stu-id="bb282-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="bb282-124">Контроллер также может возвращать объект **HttpResponseMessage** .</span><span class="sxs-lookup"><span data-stu-id="bb282-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="bb282-125">Чтобы указать объект CLR для текста ответа, вызовите метод расширения **креатереспонсе** :</span><span class="sxs-lookup"><span data-stu-id="bb282-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="bb282-126">Этот параметр обеспечивает более полный контроль над данными ответа.</span><span class="sxs-lookup"><span data-stu-id="bb282-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="bb282-127">Можно задать код состояния, добавить заголовки HTTP и т. д.</span><span class="sxs-lookup"><span data-stu-id="bb282-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="bb282-128">Объект, который сериализует ресурс, называется *модулем форматирования мультимедиа*.</span><span class="sxs-lookup"><span data-stu-id="bb282-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="bb282-129">Модули форматирования мультимедиа являются производными от класса **MediaTypeFormatter** .</span><span class="sxs-lookup"><span data-stu-id="bb282-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="bb282-130">Веб-API предоставляет средства форматирования мультимедиа для XML и JSON, а также позволяет создавать пользовательские модули форматирования для поддержки других типов мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="bb282-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="bb282-131">Сведения о написании пользовательского модуля форматирования см. в разделе [модули форматирования мультимедиа](media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="bb282-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="bb282-132">Как работает согласование содержимого</span><span class="sxs-lookup"><span data-stu-id="bb282-132">How Content Negotiation Works</span></span>

<span data-ttu-id="bb282-133">Сначала конвейер получает службу **иконтентнеготиатор** из объекта **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="bb282-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="bb282-134">Он также получает список модулей форматирования мультимедиа из коллекции **HttpConfiguration. Formatter** .</span><span class="sxs-lookup"><span data-stu-id="bb282-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="bb282-135">Затем конвейер вызывает **иконтентнеготиатор. Negotiate**, передавая:</span><span class="sxs-lookup"><span data-stu-id="bb282-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="bb282-136">Тип объекта для сериализации</span><span class="sxs-lookup"><span data-stu-id="bb282-136">The type of object to serialize</span></span>
- <span data-ttu-id="bb282-137">Коллекция модулей форматирования мультимедиа</span><span class="sxs-lookup"><span data-stu-id="bb282-137">The collection of media formatters</span></span>
- <span data-ttu-id="bb282-138">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="bb282-138">The HTTP request</span></span>

<span data-ttu-id="bb282-139">Метод **Negotiate** возвращает два фрагмента информации:</span><span class="sxs-lookup"><span data-stu-id="bb282-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="bb282-140">Используемый модуль форматирования</span><span class="sxs-lookup"><span data-stu-id="bb282-140">Which formatter to use</span></span>
- <span data-ttu-id="bb282-141">Тип носителя для ответа</span><span class="sxs-lookup"><span data-stu-id="bb282-141">The media type for the response</span></span>

<span data-ttu-id="bb282-142">Если модуль форматирования не найден, метод **Negotiate** возвращает **значение NULL**, и клиент получает ошибку HTTP 406 (неприемлемо).</span><span class="sxs-lookup"><span data-stu-id="bb282-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="bb282-143">В следующем коде показано, как контроллер может напрямую вызывать согласование содержимого:</span><span class="sxs-lookup"><span data-stu-id="bb282-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="bb282-144">Этот код эквивалентен тому, что делает конвейер автоматическим.</span><span class="sxs-lookup"><span data-stu-id="bb282-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="bb282-145">Negotiator содержимого по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bb282-145">Default Content Negotiator</span></span>

<span data-ttu-id="bb282-146">Класс **дефаултконтентнеготиатор** предоставляет реализацию **иконтентнеготиатор**по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bb282-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="bb282-147">Для выбора модуля форматирования используется несколько критериев.</span><span class="sxs-lookup"><span data-stu-id="bb282-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="bb282-148">Во первых, модуль форматирования должен иметь возможность сериализовать тип.</span><span class="sxs-lookup"><span data-stu-id="bb282-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="bb282-149">Это проверяется путем вызова **MediaTypeFormatter. канвритетипе**.</span><span class="sxs-lookup"><span data-stu-id="bb282-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="bb282-150">Затем Negotiator содержимого просматривает каждый модуль форматирования и оценивает, насколько хорошо он соответствует HTTP-запросу.</span><span class="sxs-lookup"><span data-stu-id="bb282-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="bb282-151">Чтобы оценить соответствие, Negotiator содержимого просматривает два объекта модуля форматирования:</span><span class="sxs-lookup"><span data-stu-id="bb282-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="bb282-152">Коллекция **суппортедмедиатипес** , которая содержит список поддерживаемых типов носителей.</span><span class="sxs-lookup"><span data-stu-id="bb282-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="bb282-153">Negotiator содержимого пытается сопоставить этот список с заголовком запроса Accept.</span><span class="sxs-lookup"><span data-stu-id="bb282-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="bb282-154">Обратите внимание, что заголовок Accept может включать диапазоны.</span><span class="sxs-lookup"><span data-stu-id="bb282-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="bb282-155">Например, "text/plain" — это совпадение для Text/\* или \*/\*.</span><span class="sxs-lookup"><span data-stu-id="bb282-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="bb282-156">Коллекция **медиатипемаппингс** , которая содержит список объектов **медиатипемаппинг** .</span><span class="sxs-lookup"><span data-stu-id="bb282-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="bb282-157">Класс **медиатипемаппинг** предоставляет универсальный способ сопоставления HTTP-запросов с типами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="bb282-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="bb282-158">Например, он может сопоставлять пользовательский заголовок HTTP с определенным типом носителя.</span><span class="sxs-lookup"><span data-stu-id="bb282-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="bb282-159">Если существует несколько совпадений, то сопоставление с наивысшим коэффициентом качества — WINS.</span><span class="sxs-lookup"><span data-stu-id="bb282-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="bb282-160">Пример:</span><span class="sxs-lookup"><span data-stu-id="bb282-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="bb282-161">В этом примере приложение/JSON имеет неявный фактор качества 1,0, поэтому он предпочтительнее приложения или XML.</span><span class="sxs-lookup"><span data-stu-id="bb282-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="bb282-162">Если совпадения не найдены, содержимое Negotiator пытается сопоставить тип носителя текста запроса, если таковой имеется.</span><span class="sxs-lookup"><span data-stu-id="bb282-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="bb282-163">Например, если запрос содержит данные JSON, Negotiator содержимого ищет модуль форматирования JSON.</span><span class="sxs-lookup"><span data-stu-id="bb282-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="bb282-164">Если совпадений по-прежнему нет, Negotiator содержимого просто выбирает первый модуль форматирования, который может сериализовать тип.</span><span class="sxs-lookup"><span data-stu-id="bb282-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="bb282-165">Выбор кодировки символов</span><span class="sxs-lookup"><span data-stu-id="bb282-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="bb282-166">После выбора модуля форматирования содержимого Negotiator выбирает наилучшую кодировку символов, просмотрев свойство **суппортеденкодингс** в модуле форматирования и сопоставляя его с заголовком Accept-Charset в запросе (если есть).</span><span class="sxs-lookup"><span data-stu-id="bb282-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
