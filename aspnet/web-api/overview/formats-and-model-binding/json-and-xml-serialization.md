---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: Сериализация JSON и XML в веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: Описывает модули форматирования JSON и XML в веб-API ASP.NET ASP.NET 4. x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449130"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="2e620-103">Сериализация JSON и XML в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2e620-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="2e620-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2e620-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2e620-105">В этой статье описываются модули форматирования JSON и XML в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2e620-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="2e620-106">В веб-API ASP.NET *модуль форматирования типа мультимедиа* — это объект, который может:</span><span class="sxs-lookup"><span data-stu-id="2e620-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="2e620-107">Чтение объектов CLR из текста HTTP-сообщения</span><span class="sxs-lookup"><span data-stu-id="2e620-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="2e620-108">Запись объектов среды CLR в текст сообщения HTTP</span><span class="sxs-lookup"><span data-stu-id="2e620-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="2e620-109">Веб-API предоставляет модули форматирования типа мультимедиа для JSON и XML.</span><span class="sxs-lookup"><span data-stu-id="2e620-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="2e620-110">По умолчанию платформа вставляет эти модули форматирования в конвейер.</span><span class="sxs-lookup"><span data-stu-id="2e620-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="2e620-111">Клиенты могут запрашивать JSON или XML в заголовке Accept HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="2e620-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="2e620-112">Содержимое</span><span class="sxs-lookup"><span data-stu-id="2e620-112">Contents</span></span>

- [<span data-ttu-id="2e620-113">Модуль форматирования JSON-типов</span><span class="sxs-lookup"><span data-stu-id="2e620-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="2e620-114">Свойства только для чтения</span><span class="sxs-lookup"><span data-stu-id="2e620-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="2e620-115">Дату</span><span class="sxs-lookup"><span data-stu-id="2e620-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="2e620-116">Отступов</span><span class="sxs-lookup"><span data-stu-id="2e620-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="2e620-117">Регистр в стиле Camel</span><span class="sxs-lookup"><span data-stu-id="2e620-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="2e620-118">Анонимные и слабо типизированные объекты</span><span class="sxs-lookup"><span data-stu-id="2e620-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="2e620-119">Модуль форматирования мультимедиа типа XML</span><span class="sxs-lookup"><span data-stu-id="2e620-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="2e620-120">Свойства только для чтения</span><span class="sxs-lookup"><span data-stu-id="2e620-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="2e620-121">Дату</span><span class="sxs-lookup"><span data-stu-id="2e620-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="2e620-122">Отступов</span><span class="sxs-lookup"><span data-stu-id="2e620-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="2e620-123">Установка XML-сериализаторов для каждого типа</span><span class="sxs-lookup"><span data-stu-id="2e620-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="2e620-124">Удаление модуля форматирования JSON или XML</span><span class="sxs-lookup"><span data-stu-id="2e620-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="2e620-125">Обработка циклических ссылок на объекты</span><span class="sxs-lookup"><span data-stu-id="2e620-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="2e620-126">Проверка сериализации объектов</span><span class="sxs-lookup"><span data-stu-id="2e620-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="2e620-127">Модуль форматирования JSON-типов</span><span class="sxs-lookup"><span data-stu-id="2e620-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="2e620-128">Форматирование JSON предоставляется классом **жсонмедиатипеформаттер** .</span><span class="sxs-lookup"><span data-stu-id="2e620-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="2e620-129">По умолчанию **жсонмедиатипеформаттер** использует библиотеку [JSON.NET](https://github.com/JamesNK/Newtonsoft.Json) для выполнения сериализации.</span><span class="sxs-lookup"><span data-stu-id="2e620-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="2e620-130">Json.NET — сторонний проект с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="2e620-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="2e620-131">При желании можно настроить класс **жсонмедиатипеформаттер** для использования **DataContractJsonSerializer** вместо JSON.NET.</span><span class="sxs-lookup"><span data-stu-id="2e620-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="2e620-132">Для этого задайте для свойства **уседатаконтрактжсонсериализер** **значение true**:</span><span class="sxs-lookup"><span data-stu-id="2e620-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="2e620-133">Сериализация JSON</span><span class="sxs-lookup"><span data-stu-id="2e620-133">JSON Serialization</span></span>

<span data-ttu-id="2e620-134">В этом разделе описываются некоторые особенности поведения модуля форматирования JSON с использованием сериализатора [JSON.NET](https://github.com/JamesNK/Newtonsoft.Json) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2e620-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="2e620-135">Это не предназначено для полной документации по библиотеке Json.NET. Дополнительные сведения см. в [документации по JSON.NET](http://james.newtonking.com/projects/json/help/).</span><span class="sxs-lookup"><span data-stu-id="2e620-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="2e620-136">Что сериализуется?</span><span class="sxs-lookup"><span data-stu-id="2e620-136">What Gets Serialized?</span></span>

<span data-ttu-id="2e620-137">По умолчанию все открытые свойства и поля включаются в сериализованный код JSON.</span><span class="sxs-lookup"><span data-stu-id="2e620-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="2e620-138">Чтобы опустить свойство или поле, необходимо снабдить его атрибутом **жсонигноре** .</span><span class="sxs-lookup"><span data-stu-id="2e620-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="2e620-139">Если вы предпочитаете &quot;согласие&quot;, добавьте класс с атрибутом **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="2e620-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="2e620-140">Если этот атрибут существует, элементы игнорируются, если только они не имеют **DataMember**.</span><span class="sxs-lookup"><span data-stu-id="2e620-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="2e620-141">Можно также использовать **DataMember** для сериализации закрытых членов.</span><span class="sxs-lookup"><span data-stu-id="2e620-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="2e620-142">Свойства только для чтения</span><span class="sxs-lookup"><span data-stu-id="2e620-142">Read-Only Properties</span></span>

<span data-ttu-id="2e620-143">Свойства, доступные только для чтения, сериализуются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2e620-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="2e620-144">даты.</span><span class="sxs-lookup"><span data-stu-id="2e620-144">Dates</span></span>

<span data-ttu-id="2e620-145">По умолчанию Json.NET записывает даты в формате [ISO 8601](http://www.w3.org/TR/NOTE-datetime) .</span><span class="sxs-lookup"><span data-stu-id="2e620-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="2e620-146">Даты в формате UTC (всемирное время) записываются с суффиксом "Z".</span><span class="sxs-lookup"><span data-stu-id="2e620-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="2e620-147">Даты в местном времени включают смещение часового пояса.</span><span class="sxs-lookup"><span data-stu-id="2e620-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="2e620-148">Пример:</span><span class="sxs-lookup"><span data-stu-id="2e620-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="2e620-149">По умолчанию Json.NET сохраняет часовой пояс.</span><span class="sxs-lookup"><span data-stu-id="2e620-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="2e620-150">Это можно переопределить, задав свойство Датетимезонехандлинг:</span><span class="sxs-lookup"><span data-stu-id="2e620-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="2e620-151">Если вы предпочитаете использовать [Формат даты Microsoft JSON](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) вместо ISO 8601, задайте свойство **датеформасандлинг** в параметрах сериализатора:</span><span class="sxs-lookup"><span data-stu-id="2e620-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="2e620-152">Отступы</span><span class="sxs-lookup"><span data-stu-id="2e620-152">Indenting</span></span>

<span data-ttu-id="2e620-153">Чтобы написать код JSON с отступом, задайте для параметра **форматирования** значение **Форматирование. отступ**:</span><span class="sxs-lookup"><span data-stu-id="2e620-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="2e620-154">Регистр в стиле Camel</span><span class="sxs-lookup"><span data-stu-id="2e620-154">Camel Casing</span></span>

<span data-ttu-id="2e620-155">Чтобы записать имена свойств JSON с использованием прописных букв, не изменяя модель данных, задайте **камелкасепропертинамесконтрактресолвер** для сериализатора:</span><span class="sxs-lookup"><span data-stu-id="2e620-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="2e620-156">Анонимные и слабо типизированные объекты</span><span class="sxs-lookup"><span data-stu-id="2e620-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="2e620-157">Метод действия может возвращать анонимный объект и сериализовать его в JSON.</span><span class="sxs-lookup"><span data-stu-id="2e620-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="2e620-158">Пример:</span><span class="sxs-lookup"><span data-stu-id="2e620-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="2e620-159">Текст ответного сообщения будет содержать следующий код JSON:</span><span class="sxs-lookup"><span data-stu-id="2e620-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="2e620-160">Если веб-API получает слабо структурированные объекты JSON от клиентов, текст запроса можно десериализовать в тип **Newtonsoft. JSON. LINQ. JObject** .</span><span class="sxs-lookup"><span data-stu-id="2e620-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="2e620-161">Однако обычно лучше использовать строго типизированные объекты данных.</span><span class="sxs-lookup"><span data-stu-id="2e620-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="2e620-162">Затем вам не нужно самостоятельно анализировать данные, и вы получаете преимущества проверки модели.</span><span class="sxs-lookup"><span data-stu-id="2e620-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="2e620-163">XML-сериализатор не поддерживает анонимные типы или экземпляры **JObject** .</span><span class="sxs-lookup"><span data-stu-id="2e620-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="2e620-164">При использовании этих функций для данных JSON следует удалить модуль форматирования XML из конвейера, как описано далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="2e620-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="2e620-165">Модуль форматирования мультимедиа типа XML</span><span class="sxs-lookup"><span data-stu-id="2e620-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="2e620-166">Форматирование XML предоставляется классом **ксмлмедиатипеформаттер** .</span><span class="sxs-lookup"><span data-stu-id="2e620-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="2e620-167">По умолчанию **ксмлмедиатипеформаттер** использует класс **DataContractSerializer** для выполнения сериализации.</span><span class="sxs-lookup"><span data-stu-id="2e620-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="2e620-168">При желании можно настроить **ксмлмедиатипеформаттер** для использования **XmlSerializer** вместо **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="2e620-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="2e620-169">Для этого задайте для свойства **усексмлсериализер** **значение true**:</span><span class="sxs-lookup"><span data-stu-id="2e620-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="2e620-170">Класс **XmlSerializer** поддерживает более узкий набор типов, чем **DataContractSerializer**, но предоставляет больший контроль над результирующим XML.</span><span class="sxs-lookup"><span data-stu-id="2e620-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="2e620-171">Если необходимо сопоставить существующую схему XML, рассмотрите возможность использования **XmlSerializer** .</span><span class="sxs-lookup"><span data-stu-id="2e620-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="2e620-172">Сериализация XML</span><span class="sxs-lookup"><span data-stu-id="2e620-172">XML Serialization</span></span>

<span data-ttu-id="2e620-173">В этом разделе описываются некоторые особенности поведения модуля форматирования XML с использованием **DataContractSerializer**по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2e620-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="2e620-174">По умолчанию DataContractSerializer ведет себя следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e620-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="2e620-175">Все открытые свойства и поля для чтения и записи сериализуются.</span><span class="sxs-lookup"><span data-stu-id="2e620-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="2e620-176">Чтобы опустить свойство или поле, необходимо снабдить его атрибутом **игноредатамембер** .</span><span class="sxs-lookup"><span data-stu-id="2e620-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="2e620-177">Закрытые и защищенные члены не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="2e620-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="2e620-178">Свойства, доступные только для чтения, не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="2e620-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="2e620-179">(Однако содержимое свойства коллекции, доступного только для чтения, сериализуется.)</span><span class="sxs-lookup"><span data-stu-id="2e620-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="2e620-180">Имена классов и членов записываются в XML-коде точно так же, как они отображаются в объявлении класса.</span><span class="sxs-lookup"><span data-stu-id="2e620-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="2e620-181">Используется пространство имен XML по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2e620-181">A default XML namespace is used.</span></span>

<span data-ttu-id="2e620-182">Если требуется больший контроль над сериализацией, можно снабдить класс атрибутом **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="2e620-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="2e620-183">При наличии этого атрибута класс сериализуется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e620-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="2e620-184">&quot;согласие&quot;. свойства и поля не сериализуются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2e620-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="2e620-185">Чтобы сериализовать свойство или поле, добавьте к нему атрибут **DataMember** .</span><span class="sxs-lookup"><span data-stu-id="2e620-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="2e620-186">Чтобы сериализовать закрытый или защищенный член, добавьте его в атрибут **DataMember** .</span><span class="sxs-lookup"><span data-stu-id="2e620-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="2e620-187">Свойства, доступные только для чтения, не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="2e620-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="2e620-188">Чтобы изменить способ отображения имени класса в XML, задайте параметр *Name* в атрибуте **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="2e620-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="2e620-189">Чтобы изменить способ отображения имени члена в XML, задайте параметр *Name* в атрибуте **DataMember** .</span><span class="sxs-lookup"><span data-stu-id="2e620-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="2e620-190">Чтобы изменить пространство имен XML, задайте параметр *Namespace* в классе **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="2e620-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="2e620-191">Свойства только для чтения</span><span class="sxs-lookup"><span data-stu-id="2e620-191">Read-Only Properties</span></span>

<span data-ttu-id="2e620-192">Свойства, доступные только для чтения, не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="2e620-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="2e620-193">Если свойство только для чтения имеет резервное закрытое поле, можно пометить частное поле атрибутом **DataMember** .</span><span class="sxs-lookup"><span data-stu-id="2e620-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="2e620-194">Этот подход требует наличия атрибута **DataContract** в классе.</span><span class="sxs-lookup"><span data-stu-id="2e620-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="2e620-195">даты.</span><span class="sxs-lookup"><span data-stu-id="2e620-195">Dates</span></span>

<span data-ttu-id="2e620-196">Даты записываются в формате ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="2e620-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="2e620-197">Например, &quot;2012-05-23T20:21:37.9116538 Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="2e620-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="2e620-198">Отступы</span><span class="sxs-lookup"><span data-stu-id="2e620-198">Indenting</span></span>

<span data-ttu-id="2e620-199">Чтобы написать XML с отступом, задайте для свойства **Indent** значение **true**:</span><span class="sxs-lookup"><span data-stu-id="2e620-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="2e620-200">Установка XML-сериализаторов для каждого типа</span><span class="sxs-lookup"><span data-stu-id="2e620-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="2e620-201">Можно задать различные XML-сериализаторы для разных типов CLR.</span><span class="sxs-lookup"><span data-stu-id="2e620-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="2e620-202">Например, у вас может быть определенный объект данных, для обеспечения обратной совместимости которого требуется **XmlSerializer** .</span><span class="sxs-lookup"><span data-stu-id="2e620-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="2e620-203">Для этого объекта можно использовать **XmlSerializer** и продолжить использовать **DataContractSerializer** для других типов.</span><span class="sxs-lookup"><span data-stu-id="2e620-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="2e620-204">Чтобы задать сериализатор XML для определенного типа, вызовите **сетсериализер**.</span><span class="sxs-lookup"><span data-stu-id="2e620-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="2e620-205">Можно указать **XmlSerializer** или любой объект, производный от **XmlObjectSerializer**.</span><span class="sxs-lookup"><span data-stu-id="2e620-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="2e620-206">Удаление модуля форматирования JSON или XML</span><span class="sxs-lookup"><span data-stu-id="2e620-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="2e620-207">Вы можете удалить модуль форматирования JSON или модуль форматирования XML из списка модулей форматирования, если вы не хотите их использовать.</span><span class="sxs-lookup"><span data-stu-id="2e620-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="2e620-208">Вот основные причины этого:</span><span class="sxs-lookup"><span data-stu-id="2e620-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="2e620-209">Для ограничения ответов веб-API на определенный тип носителя.</span><span class="sxs-lookup"><span data-stu-id="2e620-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="2e620-210">Например, можно выбрать поддержку только ответов JSON и удалить модуль форматирования XML.</span><span class="sxs-lookup"><span data-stu-id="2e620-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="2e620-211">Для замены модуля форматирования по умолчанию пользовательским модулем форматирования.</span><span class="sxs-lookup"><span data-stu-id="2e620-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="2e620-212">Например, можно заменить модуль форматирования JSON собственной пользовательской реализацией модуля форматирования JSON.</span><span class="sxs-lookup"><span data-stu-id="2e620-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="2e620-213">В следующем коде показано, как удалить модули форматирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2e620-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="2e620-214">Вызовите его из **приложения\_метод Start** , определенный в Global. asax.</span><span class="sxs-lookup"><span data-stu-id="2e620-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="2e620-215">Обработка циклических ссылок на объекты</span><span class="sxs-lookup"><span data-stu-id="2e620-215">Handling Circular Object References</span></span>

<span data-ttu-id="2e620-216">По умолчанию модули форматирования JSON и XML записывают все объекты в виде значений.</span><span class="sxs-lookup"><span data-stu-id="2e620-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="2e620-217">Если два свойства ссылаются на один объект или один объект встречается дважды в коллекции, модуль форматирования сериализует объект дважды.</span><span class="sxs-lookup"><span data-stu-id="2e620-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="2e620-218">Это конкретная проблема, если граф объектов содержит циклы, так как сериализатор выдаст исключение при обнаружении цикла в графе.</span><span class="sxs-lookup"><span data-stu-id="2e620-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="2e620-219">Рассмотрим следующие модели объектов и контроллер.</span><span class="sxs-lookup"><span data-stu-id="2e620-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="2e620-220">Вызов этого действия приведет к тому, что модуль форматирования создаст исключение, которое преобразуется в ответ на клиентский код состояния 500 (внутренняя ошибка сервера).</span><span class="sxs-lookup"><span data-stu-id="2e620-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="2e620-221">Чтобы сохранить ссылки на объекты в JSON, добавьте следующий код в **приложение\_запуск** метода в файле Global. asax:</span><span class="sxs-lookup"><span data-stu-id="2e620-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="2e620-222">Теперь действие контроллера вернет JSON, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e620-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="2e620-223">Обратите внимание, что сериализатор добавляет к обоим объектам свойство &quot;$id&quot;.</span><span class="sxs-lookup"><span data-stu-id="2e620-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="2e620-224">Кроме того, он обнаруживает, что свойство Employee. Department создает цикл, поэтому оно заменяет значение ссылкой на объект: {&quot;$ref&quot;:&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="2e620-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="2e620-225">Ссылки на объекты не являются стандартными в JSON.</span><span class="sxs-lookup"><span data-stu-id="2e620-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="2e620-226">Прежде чем использовать эту функцию, определите, будут ли клиенты иметь возможность анализировать результаты.</span><span class="sxs-lookup"><span data-stu-id="2e620-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="2e620-227">Возможно, лучше просто удалить циклы из графа.</span><span class="sxs-lookup"><span data-stu-id="2e620-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="2e620-228">Например, в этом примере нет необходимости в связи между сотрудниками и Отделом.</span><span class="sxs-lookup"><span data-stu-id="2e620-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="2e620-229">Для сохранения ссылок на объекты в XML существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="2e620-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="2e620-230">Более простой вариант заключается в добавлении `[DataContract(IsReference=true)]` в класс модели.</span><span class="sxs-lookup"><span data-stu-id="2e620-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="2e620-231">Параметр *IsReference* включает ссылки на объекты.</span><span class="sxs-lookup"><span data-stu-id="2e620-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="2e620-232">Помните, что **контракт DataContract** выполняет явный вход, поэтому также необходимо добавить атрибуты **DataMember** в свойства:</span><span class="sxs-lookup"><span data-stu-id="2e620-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="2e620-233">Теперь модуль форматирования создаст XML-код следующего вида:</span><span class="sxs-lookup"><span data-stu-id="2e620-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="2e620-234">Если вы хотите избежать атрибутов в классе модели, существует еще один вариант: создать новый экземпляр **DataContractSerializer** конкретного типа и установить для *пресервеобжектреференцес* **значение true** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="2e620-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="2e620-235">Затем установите этот экземпляр в качестве сериализатора для каждого типа на модуль форматирования мультимедиа типа XML.</span><span class="sxs-lookup"><span data-stu-id="2e620-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="2e620-236">В следующем коде показано, как это сделать:</span><span class="sxs-lookup"><span data-stu-id="2e620-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="2e620-237">Проверка сериализации объектов</span><span class="sxs-lookup"><span data-stu-id="2e620-237">Testing Object Serialization</span></span>

<span data-ttu-id="2e620-238">При проектировании веб-API полезно проверить, как будут сериализованы объекты данных.</span><span class="sxs-lookup"><span data-stu-id="2e620-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="2e620-239">Это можно сделать без создания контроллера или вызова действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2e620-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
