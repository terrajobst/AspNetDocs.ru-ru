---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: Поддержка BSON в веб-API ASP.NET 2,1-ASP.NET 4. x
author: MikeWasson
description: показывает, как использовать BSON в контроллере веб-API (на стороне сервера) и в клиентском приложении .NET для ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: ccbc0372120301b1cd8d4cdc86bd9fba9404d8ae
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519338"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="43274-103">Поддержка BSON в веб-API ASP.NET 2,1</span><span class="sxs-lookup"><span data-stu-id="43274-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="43274-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="43274-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="43274-105">В этом разделе показано, как использовать BSON в контроллере веб-API (на стороне сервера) и в клиентском приложении .NET.</span><span class="sxs-lookup"><span data-stu-id="43274-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="43274-106">В веб-API 2,1 введена поддержка BSON.</span><span class="sxs-lookup"><span data-stu-id="43274-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="43274-107">Что такое BSON?</span><span class="sxs-lookup"><span data-stu-id="43274-107">What is BSON?</span></span>

<span data-ttu-id="43274-108">[BSON](http://bsonspec.org/) — это формат двоичной сериализации.</span><span class="sxs-lookup"><span data-stu-id="43274-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="43274-109">"BSON" означает "двоичный JSON", но BSON и JSON сериализуются совершенно иначе.</span><span class="sxs-lookup"><span data-stu-id="43274-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="43274-110">BSON — это «JSON-Like», поскольку объекты представлены как пары «имя-значение», аналогичные формату JSON.</span><span class="sxs-lookup"><span data-stu-id="43274-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="43274-111">В отличие от JSON, числовые типы данных хранятся в виде байтов, а не строк.</span><span class="sxs-lookup"><span data-stu-id="43274-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="43274-112">BSON был разработан для упрощения, легкого сканирования и быстрого кодирования и декодирования.</span><span class="sxs-lookup"><span data-stu-id="43274-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="43274-113">BSON сравним по размеру с JSON.</span><span class="sxs-lookup"><span data-stu-id="43274-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="43274-114">В зависимости от конкретных данных полезные данные BSON могут занять меньше или больше пространства, чем полезные данные JSON.</span><span class="sxs-lookup"><span data-stu-id="43274-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="43274-115">Для сериализации двоичных данных, таких как файл изображения, BSON меньше JSON, так как двоичные данные не кодируются в Base64.</span><span class="sxs-lookup"><span data-stu-id="43274-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="43274-116">Документы BSON легко сканировать, поскольку элементы имеют префикс поля длины, поэтому средство синтаксического анализа может пропускать элементы без их декодирования.</span><span class="sxs-lookup"><span data-stu-id="43274-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="43274-117">Кодирование и декодирование являются эффективными, так как числовые типы данных хранятся в виде чисел, а не строк.</span><span class="sxs-lookup"><span data-stu-id="43274-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="43274-118">Собственные клиенты, такие как клиентские приложения .NET, могут воспользоваться преимуществами BSON вместо текстовых форматов, таких как JSON или XML.</span><span class="sxs-lookup"><span data-stu-id="43274-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="43274-119">Для клиентов браузеров, вероятно, потребуется использовать JSON, так как JavaScript может напрямую преобразовывать полезные данные JSON.</span><span class="sxs-lookup"><span data-stu-id="43274-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="43274-120">К счастью, веб-API использует [Согласование содержимого](content-negotiation.md), поэтому API может поддерживать оба формата и позволить клиенту выбрать.</span><span class="sxs-lookup"><span data-stu-id="43274-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="43274-121">Включение BSON на сервере</span><span class="sxs-lookup"><span data-stu-id="43274-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="43274-122">В конфигурации веб-API добавьте **бсонмедиатипеформаттер** в коллекцию форматеров.</span><span class="sxs-lookup"><span data-stu-id="43274-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="43274-123">Теперь, если клиент запрашивает "Application/BSON", веб-API будет использовать модуль форматирования BSON.</span><span class="sxs-lookup"><span data-stu-id="43274-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="43274-124">Чтобы связать BSON с другими типами мультимедиа, добавьте их в коллекцию Суппортедмедиатипес.</span><span class="sxs-lookup"><span data-stu-id="43274-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="43274-125">Следующий код добавляет "application/vnd. contoso" к поддерживаемым типам носителей:</span><span class="sxs-lookup"><span data-stu-id="43274-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="43274-126">Пример сеанса HTTP</span><span class="sxs-lookup"><span data-stu-id="43274-126">Example HTTP Session</span></span>

<span data-ttu-id="43274-127">В этом примере мы будем использовать следующий класс Model и простой контроллер веб-API:</span><span class="sxs-lookup"><span data-stu-id="43274-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="43274-128">Клиент может отправить следующий HTTP-запрос:</span><span class="sxs-lookup"><span data-stu-id="43274-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="43274-129">Ответ:</span><span class="sxs-lookup"><span data-stu-id="43274-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="43274-130">Здесь я заменил двоичные данные на &quot;.&quot; символов.</span><span class="sxs-lookup"><span data-stu-id="43274-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="43274-131">На следующем снимке экрана из Fiddler показаны необработанные шестнадцатеричные значения.</span><span class="sxs-lookup"><span data-stu-id="43274-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="43274-132">Использование BSON с HttpClient</span><span class="sxs-lookup"><span data-stu-id="43274-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="43274-133">Клиентские приложения .NET могут использовать модуль форматирования BSON с **HttpClient**.</span><span class="sxs-lookup"><span data-stu-id="43274-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="43274-134">Дополнительные сведения о **HttpClient**см. в разделе [вызов веб-API из клиента .NET](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="43274-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="43274-135">Следующий код отправляет запрос GET, который принимает BSON, а затем десериализует полезные данные BSON в ответе.</span><span class="sxs-lookup"><span data-stu-id="43274-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="43274-136">Чтобы запросить BSON с сервера, задайте для заголовка Accept значение "Application/BSON":</span><span class="sxs-lookup"><span data-stu-id="43274-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="43274-137">Чтобы десериализовать текст ответа, используйте **бсонмедиатипеформаттер**.</span><span class="sxs-lookup"><span data-stu-id="43274-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="43274-138">Этот модуль форматирования не находится в коллекции модулей форматирования по умолчанию, поэтому его необходимо указать при чтении текста ответа:</span><span class="sxs-lookup"><span data-stu-id="43274-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="43274-139">В следующем примере показано, как отправить запрос POST, содержащий BSON.</span><span class="sxs-lookup"><span data-stu-id="43274-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="43274-140">Большая часть этого кода аналогична предыдущему примеру.</span><span class="sxs-lookup"><span data-stu-id="43274-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="43274-141">Но в методе **Async** укажите **бсонмедиатипеформаттер** в качестве модуля форматирования:</span><span class="sxs-lookup"><span data-stu-id="43274-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="43274-142">Сериализация примитивных типов верхнего уровня</span><span class="sxs-lookup"><span data-stu-id="43274-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="43274-143">Каждый документ BSON представляет собой список пар «ключ-значение». Спецификация BSON не определяет синтаксис для сериализации одного необработанного значения, такого как целое число или строка.</span><span class="sxs-lookup"><span data-stu-id="43274-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="43274-144">Чтобы обойти это ограничение, **бсонмедиатипеформаттер** рассматривает примитивные типы как особый случай.</span><span class="sxs-lookup"><span data-stu-id="43274-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="43274-145">Перед сериализацией он преобразует значение в пару "ключ-значение" с ключом "value".</span><span class="sxs-lookup"><span data-stu-id="43274-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="43274-146">Например, предположим, что контроллер API возвращает целое число:</span><span class="sxs-lookup"><span data-stu-id="43274-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="43274-147">Перед сериализацией модуль форматирования BSON преобразует его в следующую пару "ключ-значение":</span><span class="sxs-lookup"><span data-stu-id="43274-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="43274-148">При десериализации модуль форматирования преобразует данные обратно в исходное значение.</span><span class="sxs-lookup"><span data-stu-id="43274-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="43274-149">Однако клиенты, использующие другое средство синтаксического анализа BSON, должны обработать этот случай, если ваш веб-API возвращает необработанные значения.</span><span class="sxs-lookup"><span data-stu-id="43274-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="43274-150">Как правило, рекомендуется возвращать структурированные данные, а не необработанные значения.</span><span class="sxs-lookup"><span data-stu-id="43274-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43274-151">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="43274-151">Additional Resources</span></span>

[<span data-ttu-id="43274-152">Пример BSON веб-API</span><span class="sxs-lookup"><span data-stu-id="43274-152">Web API BSON Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[<span data-ttu-id="43274-153">Модули форматирования мультимедиа</span><span class="sxs-lookup"><span data-stu-id="43274-153">Media Formatters</span></span>](media-formatters.md)
