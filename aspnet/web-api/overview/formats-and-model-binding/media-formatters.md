---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: Модули форматирования мультимедиа в ASP.NET Web API 2 — ASP.NET 4.x
author: MikeWasson
description: Показано, как для поддержки дополнительных носителей форматов в ASP.NET Web API для ASP.NET 4.x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418772"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="3e219-103">Модули форматирования мультимедиа в ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="3e219-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="3e219-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3e219-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3e219-105">Этом руководстве показано, как обеспечить поддержку дополнительных носителей форматов в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3e219-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="3e219-106">Типов мультимедиа для Интернета</span><span class="sxs-lookup"><span data-stu-id="3e219-106">Internet Media Types</span></span>

<span data-ttu-id="3e219-107">Тип носителя, также называемый MIME-тип, определяет формат фрагмента данных.</span><span class="sxs-lookup"><span data-stu-id="3e219-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="3e219-108">В HTTP типы мультимедиа описывают формат тела сообщения.</span><span class="sxs-lookup"><span data-stu-id="3e219-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="3e219-109">Тип носителя состоит из двух строк, тип и подтип.</span><span class="sxs-lookup"><span data-stu-id="3e219-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="3e219-110">Пример:</span><span class="sxs-lookup"><span data-stu-id="3e219-110">For example:</span></span>

- <span data-ttu-id="3e219-111">text/html</span><span class="sxs-lookup"><span data-stu-id="3e219-111">text/html</span></span>
- <span data-ttu-id="3e219-112">изображение/png</span><span class="sxs-lookup"><span data-stu-id="3e219-112">image/png</span></span>
- <span data-ttu-id="3e219-113">application/json</span><span class="sxs-lookup"><span data-stu-id="3e219-113">application/json</span></span>

<span data-ttu-id="3e219-114">Если сообщение HTTP содержит тело сущности, заголовка Content-Type формат тела сообщения.</span><span class="sxs-lookup"><span data-stu-id="3e219-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="3e219-115">Это говорит получателю, как анализировать содержимое тела сообщения.</span><span class="sxs-lookup"><span data-stu-id="3e219-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="3e219-116">Например если ответ HTTP содержит изображения в формате PNG, ответ может содержать следующие заголовки.</span><span class="sxs-lookup"><span data-stu-id="3e219-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="3e219-117">Когда клиент отправляет сообщение-запрос, он может включать заголовок Accept.</span><span class="sxs-lookup"><span data-stu-id="3e219-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="3e219-118">Заголовок Accept говорит, что сервер мультимедиа типы клиент хочет с сервера.</span><span class="sxs-lookup"><span data-stu-id="3e219-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="3e219-119">Пример:</span><span class="sxs-lookup"><span data-stu-id="3e219-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="3e219-120">Этот заголовок указывает, что сервер, необходимый клиенту HTML, XHTML или XML.</span><span class="sxs-lookup"><span data-stu-id="3e219-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="3e219-121">Тип носителя определяет, как веб-API сериализует и десериализует текст сообщения HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e219-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="3e219-122">Веб-API имеет встроенную поддержку XML, JSON, BSON и формы urlencoded данных и может поддерживать дополнительные носители, написав *форматирования мультимедиа*.</span><span class="sxs-lookup"><span data-stu-id="3e219-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="3e219-123">Чтобы создать модуль форматирования мультимедиа, являются производными от одного из этих классов:</span><span class="sxs-lookup"><span data-stu-id="3e219-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="3e219-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e219-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="3e219-125">Этот класс использует асинхронное чтение и запись методы.</span><span class="sxs-lookup"><span data-stu-id="3e219-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="3e219-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e219-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="3e219-127">Этот класс является производным от **MediaTypeFormatter** , но использует методы синхронные чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="3e219-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="3e219-128">Наследование от **BufferedMediaTypeFormatter** проще использовать, так как нет асинхронного кода, но это также значит, можно блокировать вызывающий поток ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="3e219-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="3e219-129">Пример Создание CSV-ФАЙЛ форматирования мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3e219-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="3e219-130">В следующем примере показано форматирования типа мультимедиа, который может сериализовать объект Product в формат с разделителями-запятыми (CSV).</span><span class="sxs-lookup"><span data-stu-id="3e219-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="3e219-131">В этом примере используется тип продукта, определенный в этом руководстве [Создание веб-API, поддерживает операции CRUD](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3e219-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="3e219-132">Вот определение объекта продукта:</span><span class="sxs-lookup"><span data-stu-id="3e219-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="3e219-133">Чтобы реализовать модуль форматирования CSV, определите класс, который является производным от **BufferedMediaTypeFormatter**:</span><span class="sxs-lookup"><span data-stu-id="3e219-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="3e219-134">Добавьте в конструктор, типы объектов, которые поддерживает модуль форматирования.</span><span class="sxs-lookup"><span data-stu-id="3e219-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="3e219-135">В этом примере модуль форматирования поддерживает устройств одного типа, &quot;text/csv&quot;:</span><span class="sxs-lookup"><span data-stu-id="3e219-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="3e219-136">Переопределить **CanWriteType** метод, чтобы указать, какие типы форматирования можно сериализовать:</span><span class="sxs-lookup"><span data-stu-id="3e219-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="3e219-137">В этом примере модуль форматирования может сериализовать единый `Product` объекты, а также коллекции `Product` объектов.</span><span class="sxs-lookup"><span data-stu-id="3e219-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="3e219-138">Аналогичным образом переопределить **методов CanReadType** метод, чтобы указать, какие типы модуль форматирования может десериализовать.</span><span class="sxs-lookup"><span data-stu-id="3e219-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="3e219-139">В этом примере модуль форматирования не поддерживает десериализацию, поэтому метод просто возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="3e219-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="3e219-140">Наконец, переопределение **WriteToStream** метод.</span><span class="sxs-lookup"><span data-stu-id="3e219-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="3e219-141">Этот метод сериализует тип с помощью записи в поток.</span><span class="sxs-lookup"><span data-stu-id="3e219-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="3e219-142">Если модуль форматирования поддерживает десериализацию, также переопределить **ReadFromStream** метод.</span><span class="sxs-lookup"><span data-stu-id="3e219-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="3e219-143">Добавление форматирования мультимедиа в конвейер веб-API</span><span class="sxs-lookup"><span data-stu-id="3e219-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="3e219-144">Чтобы добавить тип мультимедиа модуля форматирования в конвейер веб-API, используйте **модули форматирования** свойство **HttpConfiguration** объекта.</span><span class="sxs-lookup"><span data-stu-id="3e219-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="3e219-145">Кодировки символов</span><span class="sxs-lookup"><span data-stu-id="3e219-145">Character Encodings</span></span>

<span data-ttu-id="3e219-146">Кроме того модуль форматирования мультимедиа может поддерживать несколько кодировок, например UTF-8 или ISO-8859-1.</span><span class="sxs-lookup"><span data-stu-id="3e219-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="3e219-147">В конструкторе, добавьте один или несколько [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) типов **SupportedEncodings** коллекции.</span><span class="sxs-lookup"><span data-stu-id="3e219-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="3e219-148">Поместите первый кодировку по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3e219-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="3e219-149">В **WriteToStream** и **ReadFromStream** вызывать методы, [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) выберите предпочитаемую кодировку символов.</span><span class="sxs-lookup"><span data-stu-id="3e219-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="3e219-150">Этот метод соответствует заголовки запроса со списком поддерживаемых кодировок.</span><span class="sxs-lookup"><span data-stu-id="3e219-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="3e219-151">Используйте возвращенный **кодировка** при чтении или записи из потока:</span><span class="sxs-lookup"><span data-stu-id="3e219-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
