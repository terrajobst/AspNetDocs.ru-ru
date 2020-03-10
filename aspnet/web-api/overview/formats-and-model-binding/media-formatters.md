---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: Модули форматирования мультимедиа в веб-API ASP.NET 2 — ASP.NET 4. x
author: MikeWasson
description: Описание поддержки дополнительных форматов мультимедиа в веб-API ASP.NET для ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448944"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="a49ec-103">Модули форматирования мультимедиа в веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="a49ec-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="a49ec-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a49ec-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a49ec-105">В этом руководстве показано, как поддерживать дополнительные форматы мультимедиа в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a49ec-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="a49ec-106">Типы медиа Интернета</span><span class="sxs-lookup"><span data-stu-id="a49ec-106">Internet Media Types</span></span>

<span data-ttu-id="a49ec-107">Тип носителя, также называемый типом MIME, определяет формат фрагмента данных.</span><span class="sxs-lookup"><span data-stu-id="a49ec-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="a49ec-108">В протоколе HTTP типы носителей описывают формат текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="a49ec-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="a49ec-109">Тип мультимедиа состоит из двух строк: типа и подтипа.</span><span class="sxs-lookup"><span data-stu-id="a49ec-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="a49ec-110">Пример:</span><span class="sxs-lookup"><span data-stu-id="a49ec-110">For example:</span></span>

- <span data-ttu-id="a49ec-111">text/html</span><span class="sxs-lookup"><span data-stu-id="a49ec-111">text/html</span></span>
- <span data-ttu-id="a49ec-112">image/png</span><span class="sxs-lookup"><span data-stu-id="a49ec-112">image/png</span></span>
- <span data-ttu-id="a49ec-113">приложение/json</span><span class="sxs-lookup"><span data-stu-id="a49ec-113">application/json</span></span>

<span data-ttu-id="a49ec-114">Если сообщение HTTP содержит текст сущности, заголовок Content-Type определяет формат текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="a49ec-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="a49ec-115">Это указывает получателю, как анализировать содержимое текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="a49ec-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="a49ec-116">Например, если HTTP-ответ содержит изображение PNG, то ответ может иметь следующие заголовки.</span><span class="sxs-lookup"><span data-stu-id="a49ec-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="a49ec-117">Когда клиент отправляет сообщение запроса, он может включать заголовок Accept.</span><span class="sxs-lookup"><span data-stu-id="a49ec-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="a49ec-118">Заголовок Accept сообщает серверу, какой тип носителя требуется клиенту с сервера.</span><span class="sxs-lookup"><span data-stu-id="a49ec-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="a49ec-119">Пример:</span><span class="sxs-lookup"><span data-stu-id="a49ec-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="a49ec-120">Этот заголовок сообщает серверу, что клиенту требуется HTML, XHTML или XML.</span><span class="sxs-lookup"><span data-stu-id="a49ec-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="a49ec-121">Тип носителя определяет, как веб-API сериализует и десериализует текст сообщения HTTP.</span><span class="sxs-lookup"><span data-stu-id="a49ec-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="a49ec-122">Веб-API имеет встроенную поддержку данных XML, JSON, BSON и Form-UrlEncoded, и вы можете поддерживать дополнительные типы мультимедиа, написав *модуль форматирования мультимедиа*.</span><span class="sxs-lookup"><span data-stu-id="a49ec-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="a49ec-123">Чтобы создать модуль форматирования мультимедиа, сделайте его производным от одного из следующих классов:</span><span class="sxs-lookup"><span data-stu-id="a49ec-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="a49ec-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="a49ec-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="a49ec-125">Этот класс использует асинхронные методы чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="a49ec-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="a49ec-126">[Буффередмедиатипеформаттер](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="a49ec-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="a49ec-127">Этот класс является производным от **MediaTypeFormatter** , но использует синхронные методы чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="a49ec-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="a49ec-128">Наследование от **буффередмедиатипеформаттер** проще, поскольку асинхронный код отсутствует, но это также означает, что вызывающий поток может блокироваться во время ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="a49ec-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="a49ec-129">Пример. Создание модуля форматирования мультимедиа CSV</span><span class="sxs-lookup"><span data-stu-id="a49ec-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="a49ec-130">В следующем примере показан модуль форматирования типа мультимедиа, который может сериализовать объект Product в формат значений с разделителями-запятыми (CSV).</span><span class="sxs-lookup"><span data-stu-id="a49ec-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="a49ec-131">В этом примере используется тип продукта, определенный в руководстве [Создание веб-API, поддерживающего операции CRUD](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a49ec-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="a49ec-132">Ниже приведено определение объекта Product:</span><span class="sxs-lookup"><span data-stu-id="a49ec-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="a49ec-133">Чтобы реализовать модуль форматирования CSV, определите класс, производный от **буффередмедиатипеформаттер**:</span><span class="sxs-lookup"><span data-stu-id="a49ec-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="a49ec-134">В конструкторе добавьте типы носителей, поддерживаемые модулем форматирования.</span><span class="sxs-lookup"><span data-stu-id="a49ec-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="a49ec-135">В этом примере модуль форматирования поддерживает один тип носителя, &quot;&quot;Text/CSV:</span><span class="sxs-lookup"><span data-stu-id="a49ec-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="a49ec-136">Переопределите метод **канвритетипе** , чтобы указать типы, которые модуль форматирования может сериализовать:</span><span class="sxs-lookup"><span data-stu-id="a49ec-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="a49ec-137">В этом примере модуль форматирования может сериализовать отдельные `Product`ные объекты, а также коллекции `Product` объектов.</span><span class="sxs-lookup"><span data-stu-id="a49ec-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="a49ec-138">Аналогичным образом Переопределите метод **канреадтипе** , чтобы указать типы, которые модуль форматирования может десериализовать.</span><span class="sxs-lookup"><span data-stu-id="a49ec-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="a49ec-139">В этом примере модуль форматирования не поддерживает десериализацию, поэтому метод просто возвращает **значение false**.</span><span class="sxs-lookup"><span data-stu-id="a49ec-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="a49ec-140">Наконец, переопределите метод **вритетостреам** .</span><span class="sxs-lookup"><span data-stu-id="a49ec-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="a49ec-141">Этот метод сериализует тип, записывая его в поток.</span><span class="sxs-lookup"><span data-stu-id="a49ec-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="a49ec-142">Если модуль форматирования поддерживает десериализацию, также следует переопределить метод **реадфромстреам** .</span><span class="sxs-lookup"><span data-stu-id="a49ec-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="a49ec-143">Добавление модуля форматирования мультимедиа в конвейер веб-API</span><span class="sxs-lookup"><span data-stu-id="a49ec-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="a49ec-144">Чтобы добавить модуль форматирования типов мультимедиа в конвейер веб-API, используйте свойство **форматеры** объекта **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="a49ec-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="a49ec-145">Кодировки символов</span><span class="sxs-lookup"><span data-stu-id="a49ec-145">Character Encodings</span></span>

<span data-ttu-id="a49ec-146">При необходимости модуль форматирования мультимедиа может поддерживать несколько кодировок символов, таких как UTF-8 или ISO 8859-1.</span><span class="sxs-lookup"><span data-stu-id="a49ec-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="a49ec-147">В конструкторе добавьте один или несколько типов [System. Text. Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) в коллекцию **суппортеденкодингс** .</span><span class="sxs-lookup"><span data-stu-id="a49ec-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="a49ec-148">Сначала укажите кодировку по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a49ec-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="a49ec-149">В методах **вритетостреам** и **Реадфромстреам** вызовите [MediaTypeFormatter. селектчарактеренкодинг](https://msdn.microsoft.com/library/hh969054.aspx) , чтобы выбрать предпочтительную кодировку символов.</span><span class="sxs-lookup"><span data-stu-id="a49ec-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="a49ec-150">Этот метод сопоставляет заголовки запроса со списком поддерживаемых кодировок.</span><span class="sxs-lookup"><span data-stu-id="a49ec-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="a49ec-151">Используйте возвращенную **кодировку** при чтении или записи из потока:</span><span class="sxs-lookup"><span data-stu-id="a49ec-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
