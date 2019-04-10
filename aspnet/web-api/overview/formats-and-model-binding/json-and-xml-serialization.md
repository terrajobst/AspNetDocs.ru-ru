---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: Сериализация JSON и XML в ASP.NET Web API - ASP.NET 4.x
author: MikeWasson
description: Описывает модули форматирования JSON и XML в ASP.NET Web API для ASP.NET 4.x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: a9e7ed63a55c146976e0221214e722f3a2292fee
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408281"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="b55e9-103">Сериализация JSON и XML в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b55e9-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="b55e9-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b55e9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b55e9-105">В этой статье описывается модули форматирования JSON и XML в ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="b55e9-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="b55e9-106">В веб-API ASP.NET *форматирования типа мультимедиа* — это объект, который может:</span><span class="sxs-lookup"><span data-stu-id="b55e9-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="b55e9-107">Тело сообщения объектов среды CLR для чтения из HTTP</span><span class="sxs-lookup"><span data-stu-id="b55e9-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="b55e9-108">Запись объектов среды CLR в основную часть сообщения HTTP</span><span class="sxs-lookup"><span data-stu-id="b55e9-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="b55e9-109">Веб-API предоставляет модулей форматирования типа мультимедиа для JSON и XML.</span><span class="sxs-lookup"><span data-stu-id="b55e9-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="b55e9-110">Платформа вставляет эти модули форматирования в конвейер по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b55e9-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="b55e9-111">Клиенты могут запрашивать JSON или XML в заголовке Accept HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="b55e9-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="b55e9-112">Описание</span><span class="sxs-lookup"><span data-stu-id="b55e9-112">Contents</span></span>

- [<span data-ttu-id="b55e9-113">Модуль форматирования типа мультимедиа JSON</span><span class="sxs-lookup"><span data-stu-id="b55e9-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="b55e9-114">Свойства только для чтения</span><span class="sxs-lookup"><span data-stu-id="b55e9-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="b55e9-115">Даты</span><span class="sxs-lookup"><span data-stu-id="b55e9-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="b55e9-116">Отступы</span><span class="sxs-lookup"><span data-stu-id="b55e9-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="b55e9-117">Смешанный регистр знаков</span><span class="sxs-lookup"><span data-stu-id="b55e9-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="b55e9-118">Анонимные и слабо типизированных объектов</span><span class="sxs-lookup"><span data-stu-id="b55e9-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="b55e9-119">Модуль форматирования типа мультимедиа XML</span><span class="sxs-lookup"><span data-stu-id="b55e9-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="b55e9-120">Свойства только для чтения</span><span class="sxs-lookup"><span data-stu-id="b55e9-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="b55e9-121">Даты</span><span class="sxs-lookup"><span data-stu-id="b55e9-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="b55e9-122">Отступы</span><span class="sxs-lookup"><span data-stu-id="b55e9-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="b55e9-123">Сериализаторы XML для типа параметра</span><span class="sxs-lookup"><span data-stu-id="b55e9-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="b55e9-124">Модуль форматирования XML или JSON</span><span class="sxs-lookup"><span data-stu-id="b55e9-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="b55e9-125">Обработка циклические ссылки объекта</span><span class="sxs-lookup"><span data-stu-id="b55e9-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="b55e9-126">Тестирование сериализация объектов</span><span class="sxs-lookup"><span data-stu-id="b55e9-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="b55e9-127">Модуль форматирования типа мультимедиа JSON</span><span class="sxs-lookup"><span data-stu-id="b55e9-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="b55e9-128">Форматирование обеспечивается **JsonMediaTypeFormatter** класса.</span><span class="sxs-lookup"><span data-stu-id="b55e9-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="b55e9-129">По умолчанию **JsonMediaTypeFormatter** использует [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) библиотеку для выполнения сериализации.</span><span class="sxs-lookup"><span data-stu-id="b55e9-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="b55e9-130">Json.NET — это проект с открытым кодом независимых производителей.</span><span class="sxs-lookup"><span data-stu-id="b55e9-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="b55e9-131">При желании можно настроить **JsonMediaTypeFormatter** класс для использования **DataContractJsonSerializer** вместо Json.NET.</span><span class="sxs-lookup"><span data-stu-id="b55e9-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="b55e9-132">Чтобы сделать это, установите **UseDataContractJsonSerializer** свойства **true**:</span><span class="sxs-lookup"><span data-stu-id="b55e9-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="b55e9-133">Сериализация JSON</span><span class="sxs-lookup"><span data-stu-id="b55e9-133">JSON Serialization</span></span>

<span data-ttu-id="b55e9-134">В этом разделе описываются некоторые конкретные режимы модуль форматирования JSON, используя значение по умолчанию [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) сериализатор.</span><span class="sxs-lookup"><span data-stu-id="b55e9-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="b55e9-135">Это не должно быть полную документацию по библиотеке Json.NET. Дополнительные сведения см. в разделе [документации по Json.NET](http://james.newtonking.com/projects/json/help/).</span><span class="sxs-lookup"><span data-stu-id="b55e9-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="b55e9-136">Что был сериализован?</span><span class="sxs-lookup"><span data-stu-id="b55e9-136">What Gets Serialized?</span></span>

<span data-ttu-id="b55e9-137">По умолчанию все открытые свойства и поля включаются в сериализованном формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b55e9-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="b55e9-138">Чтобы опустить свойство или поле, декорировать его **JsonIgnore** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="b55e9-139">Если вы предпочитаете &quot;согласиться&quot; подход, установите для класса **DataContract** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="b55e9-140">Если этот атрибут присутствует, элементы учитываются, если они не имеют **DataMember**.</span><span class="sxs-lookup"><span data-stu-id="b55e9-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="b55e9-141">Можно также использовать **DataMember** для сериализации закрытых членов.</span><span class="sxs-lookup"><span data-stu-id="b55e9-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="b55e9-142">Свойства только для чтения</span><span class="sxs-lookup"><span data-stu-id="b55e9-142">Read-Only Properties</span></span>

<span data-ttu-id="b55e9-143">Только для чтения свойства сериализуются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b55e9-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="b55e9-144">Даты</span><span class="sxs-lookup"><span data-stu-id="b55e9-144">Dates</span></span>

<span data-ttu-id="b55e9-145">По умолчанию Json.NET записывает даты [ISO 8601](http://www.w3.org/TR/NOTE-datetime) формат.</span><span class="sxs-lookup"><span data-stu-id="b55e9-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="b55e9-146">Даты в формате UTC (время по Гринвичу) записываются с суффиксом «Z».</span><span class="sxs-lookup"><span data-stu-id="b55e9-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="b55e9-147">Даты в формате местного времени включают смещение часового пояса.</span><span class="sxs-lookup"><span data-stu-id="b55e9-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="b55e9-148">Пример:</span><span class="sxs-lookup"><span data-stu-id="b55e9-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="b55e9-149">По умолчанию Json.NET сохраняет часовой пояс.</span><span class="sxs-lookup"><span data-stu-id="b55e9-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="b55e9-150">Это можно переопределить, задав свойство DateTimeZoneHandling:</span><span class="sxs-lookup"><span data-stu-id="b55e9-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="b55e9-151">Если вы предпочитаете использовать [формат даты Microsoft JSON](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) вместо ISO 8601, задать **DateFormatHandling** свойство параметры сериализатора:</span><span class="sxs-lookup"><span data-stu-id="b55e9-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="b55e9-152">Отступы</span><span class="sxs-lookup"><span data-stu-id="b55e9-152">Indenting</span></span>

<span data-ttu-id="b55e9-153">Чтобы записать с отступом JSON, задайте **форматирование** присвоить **Formatting.Indented**:</span><span class="sxs-lookup"><span data-stu-id="b55e9-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="b55e9-154">Смешанный регистр знаков</span><span class="sxs-lookup"><span data-stu-id="b55e9-154">Camel Casing</span></span>

<span data-ttu-id="b55e9-155">Чтобы записать имена свойств JSON с смешанный регистр знаков, без изменения модели данных, задайте **CamelCasePropertyNamesContractResolver** на сериализатора:</span><span class="sxs-lookup"><span data-stu-id="b55e9-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="b55e9-156">Анонимные и слабо типизированных объектов</span><span class="sxs-lookup"><span data-stu-id="b55e9-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="b55e9-157">Метод действия может вернуть анонимный объект и выполнить его сериализацию в JSON.</span><span class="sxs-lookup"><span data-stu-id="b55e9-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="b55e9-158">Пример:</span><span class="sxs-lookup"><span data-stu-id="b55e9-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="b55e9-159">Текст ответа будет содержать следующий JSON:</span><span class="sxs-lookup"><span data-stu-id="b55e9-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="b55e9-160">Если веб-API получает слабо структурированных объектов JSON от клиентов, может выполнить десериализацию текста запроса для **Newtonsoft.Json.Linq.JObject** типа.</span><span class="sxs-lookup"><span data-stu-id="b55e9-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="b55e9-161">Тем не менее обычно лучше использовать строго типизированных объектов данных.</span><span class="sxs-lookup"><span data-stu-id="b55e9-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="b55e9-162">Затем нужно проанализировать данные самостоятельно, и вы получаете преимущества проверки модели.</span><span class="sxs-lookup"><span data-stu-id="b55e9-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="b55e9-163">XML-сериализатор не поддерживает анонимные типы или **JObject** экземпляров.</span><span class="sxs-lookup"><span data-stu-id="b55e9-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="b55e9-164">Если вы используете эти функции для данных JSON, следует удалить модуль форматирования XML из конвейера, как описано далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b55e9-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="b55e9-165">Модуль форматирования типа мультимедиа XML</span><span class="sxs-lookup"><span data-stu-id="b55e9-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="b55e9-166">Форматирование XML-кода обеспечивается **XmlMediaTypeFormatter** класса.</span><span class="sxs-lookup"><span data-stu-id="b55e9-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="b55e9-167">По умолчанию **XmlMediaTypeFormatter** использует **DataContractSerializer** классом для выполнения сериализации.</span><span class="sxs-lookup"><span data-stu-id="b55e9-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="b55e9-168">При желании можно настроить **XmlMediaTypeFormatter** использовать **XmlSerializer** вместо **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="b55e9-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="b55e9-169">Чтобы сделать это, установите **UseXmlSerializer** свойства **true**:</span><span class="sxs-lookup"><span data-stu-id="b55e9-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="b55e9-170">**XmlSerializer** класс поддерживает более узкий набор типов, чем **DataContractSerializer**, но дает больший контроль над получаемый код XML.</span><span class="sxs-lookup"><span data-stu-id="b55e9-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="b55e9-171">Рассмотрите возможность использования **XmlSerializer** Если вам необходимо соответствовать существующей схемы XML.</span><span class="sxs-lookup"><span data-stu-id="b55e9-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="b55e9-172">XML-сериализация</span><span class="sxs-lookup"><span data-stu-id="b55e9-172">XML Serialization</span></span>

<span data-ttu-id="b55e9-173">В этом разделе описываются некоторые конкретные поведения данного модуля форматирования XML, используя значение по умолчанию **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="b55e9-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="b55e9-174">По умолчанию DataContractSerializer ведет себя следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b55e9-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="b55e9-175">Сериализуются все свойства чтения/записи и поля.</span><span class="sxs-lookup"><span data-stu-id="b55e9-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="b55e9-176">Чтобы опустить свойство или поле, декорировать его **IgnoreDataMember** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="b55e9-177">Закрытые и защищенные члены не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="b55e9-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="b55e9-178">Свойства только для чтения не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="b55e9-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="b55e9-179">(Тем не менее, содержимое свойства только для чтения коллекции сериализуются.)</span><span class="sxs-lookup"><span data-stu-id="b55e9-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="b55e9-180">Имена классов и членов записываются в формате XML, так же, как в объявлении класса.</span><span class="sxs-lookup"><span data-stu-id="b55e9-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="b55e9-181">Пространство имен XML по умолчанию используется.</span><span class="sxs-lookup"><span data-stu-id="b55e9-181">A default XML namespace is used.</span></span>

<span data-ttu-id="b55e9-182">Если вам требуется больший контроль над сериализацией, вы можете декорировать класс с **DataContract** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="b55e9-183">Если этот атрибут присутствует, класс сериализуется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b55e9-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="b55e9-184">&quot;Согласиться&quot; подход: Свойства и поля не сериализуются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b55e9-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="b55e9-185">Чтобы сериализовать свойство или поле, декорировать его **DataMember** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="b55e9-186">Чтобы сериализовать закрытому или защищенному члену, декорировать его **DataMember** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="b55e9-187">Свойства только для чтения не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="b55e9-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="b55e9-188">Чтобы изменить, как отображается имя класса в XML, установите *имя* параметр в **DataContract** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="b55e9-189">Чтобы изменить, как имя члена отображается в XML, установите *имя* параметр в **DataMember** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="b55e9-190">Чтобы изменить пространство имен XML, установите *пространства имен* параметр в **DataContract** класса.</span><span class="sxs-lookup"><span data-stu-id="b55e9-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="b55e9-191">Свойства только для чтения</span><span class="sxs-lookup"><span data-stu-id="b55e9-191">Read-Only Properties</span></span>

<span data-ttu-id="b55e9-192">Свойства только для чтения не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="b55e9-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="b55e9-193">Если свойство только для чтения имеет закрытое резервное поле, можно пометить закрытое поле с **DataMember** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b55e9-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="b55e9-194">Этот подход требует **DataContract** атрибут класса.</span><span class="sxs-lookup"><span data-stu-id="b55e9-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="b55e9-195">Даты</span><span class="sxs-lookup"><span data-stu-id="b55e9-195">Dates</span></span>

<span data-ttu-id="b55e9-196">Даты записываются в формате ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="b55e9-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="b55e9-197">Например &quot;2012-05-23T20:21:37.9116538Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="b55e9-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="b55e9-198">Отступы</span><span class="sxs-lookup"><span data-stu-id="b55e9-198">Indenting</span></span>

<span data-ttu-id="b55e9-199">Чтобы записать Отступами, задайте **отступ** свойства **true**:</span><span class="sxs-lookup"><span data-stu-id="b55e9-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="b55e9-200">Сериализаторы XML для типа параметра</span><span class="sxs-lookup"><span data-stu-id="b55e9-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="b55e9-201">Можно задать разные сериализаторы XML для различных типов среды CLR.</span><span class="sxs-lookup"><span data-stu-id="b55e9-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="b55e9-202">Например, возможно, объекта данных, который требует **XmlSerializer** для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="b55e9-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="b55e9-203">Можно использовать **XmlSerializer** для данного объекта и продолжать использовать **DataContractSerializer** для других типов.</span><span class="sxs-lookup"><span data-stu-id="b55e9-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="b55e9-204">Чтобы задать XML-сериализатор для определенного типа, вызовите **SetSerializer**.</span><span class="sxs-lookup"><span data-stu-id="b55e9-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="b55e9-205">Можно указать **XmlSerializer** или любой объект, который является производным от **XmlObjectSerializer**.</span><span class="sxs-lookup"><span data-stu-id="b55e9-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="b55e9-206">Модуль форматирования XML или JSON</span><span class="sxs-lookup"><span data-stu-id="b55e9-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="b55e9-207">Модуль форматирования JSON или модуль форматирования XML можно удалить из списка модулей форматирования, если вы не хотите их использовать.</span><span class="sxs-lookup"><span data-stu-id="b55e9-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="b55e9-208">Ниже приведены основные причины этого.</span><span class="sxs-lookup"><span data-stu-id="b55e9-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="b55e9-209">Чтобы ограничить ваши ответы веб-API с определенным типом носителя.</span><span class="sxs-lookup"><span data-stu-id="b55e9-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="b55e9-210">Например можно на поддержку только для ответов JSON и удалить модуль форматирования XML.</span><span class="sxs-lookup"><span data-stu-id="b55e9-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="b55e9-211">Чтобы заменить модуль форматирования по умолчанию пользовательского модуля форматирования.</span><span class="sxs-lookup"><span data-stu-id="b55e9-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="b55e9-212">Например можно заменить модуль форматирования JSON с собственную реализацию модуля форматирования JSON.</span><span class="sxs-lookup"><span data-stu-id="b55e9-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="b55e9-213">Ниже показано, как удалить модули форматирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b55e9-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="b55e9-214">Вызывать его из вашей **приложения\_запустить** метод, определенный в файле Global.asax.</span><span class="sxs-lookup"><span data-stu-id="b55e9-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="b55e9-215">Обработка циклические ссылки объекта</span><span class="sxs-lookup"><span data-stu-id="b55e9-215">Handling Circular Object References</span></span>

<span data-ttu-id="b55e9-216">По умолчанию модули форматирования JSON и XML запись всех объектов в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="b55e9-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="b55e9-217">Если два свойства относятся к одному объекту, или тот же объект в коллекцию дважды, модуль форматирования будет сериализовать объект дважды.</span><span class="sxs-lookup"><span data-stu-id="b55e9-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="b55e9-218">Это обусловлено конкретной проблемы, если объект графа содержит циклы, сериализатор приведет к возникновению исключения при обнаружении цикл в графе.</span><span class="sxs-lookup"><span data-stu-id="b55e9-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="b55e9-219">Рассмотрим следующие объектные модели и контроллера.</span><span class="sxs-lookup"><span data-stu-id="b55e9-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="b55e9-220">Вызов это действие приводит к модулю форматирования генерации исключения, который преобразуется ответа кода состояния 500 (Внутренняя ошибка сервера) для клиента.</span><span class="sxs-lookup"><span data-stu-id="b55e9-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="b55e9-221">Для сохранения ссылок на объекты в формате JSON, добавьте следующий код, чтобы **приложения\_запустить** метод в файле Global.asax:</span><span class="sxs-lookup"><span data-stu-id="b55e9-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="b55e9-222">Теперь действие контроллера возвращает JSON, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b55e9-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="b55e9-223">Обратите внимание, что сериализатор добавляет &quot;$id&quot; свойства обоих объектов.</span><span class="sxs-lookup"><span data-stu-id="b55e9-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="b55e9-224">Кроме того, он обнаруживает, что свойство Employee.Department создает цикл, поэтому он заменяет значение ссылки на объект: {&quot;$ref&quot;:&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="b55e9-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="b55e9-225">Ссылки на объекты не являются стандартными в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b55e9-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="b55e9-226">Прежде чем использовать эту функцию, учитывать ли ваши клиенты смогут проанализировать результаты.</span><span class="sxs-lookup"><span data-stu-id="b55e9-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="b55e9-227">Возможно, лучше просто удалить циклов с диаграммы.</span><span class="sxs-lookup"><span data-stu-id="b55e9-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="b55e9-228">Например в ссылке из сотрудников отдела в этом примере требуется не действительно.</span><span class="sxs-lookup"><span data-stu-id="b55e9-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>


<span data-ttu-id="b55e9-229">Для сохранения ссылок на объекты в формате XML, можно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="b55e9-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="b55e9-230">Более простой способ — добавить `[DataContract(IsReference=true)]` к классу модели.</span><span class="sxs-lookup"><span data-stu-id="b55e9-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="b55e9-231">*IsReference* параметр включает ссылки на объекты.</span><span class="sxs-lookup"><span data-stu-id="b55e9-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="b55e9-232">Помните, что **DataContract** делает сериализации согласиться, поэтому также необходимо будет добавить **DataMember** атрибуты к свойствам:</span><span class="sxs-lookup"><span data-stu-id="b55e9-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="b55e9-233">Теперь модуль форматирования создает код XML, аналогичный следующее:</span><span class="sxs-lookup"><span data-stu-id="b55e9-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="b55e9-234">Если вы хотите избежать атрибуты в классе модели, есть еще один вариант: Создание нового конкретного типа **DataContractSerializer** экземпляр и задайте *פכאדמל* для **true** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="b55e9-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="b55e9-235">Установите этот экземпляр как сериализатор для типа модуля форматирования типа мультимедиа XML.</span><span class="sxs-lookup"><span data-stu-id="b55e9-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="b55e9-236">Следующий код показывает, как это сделать:</span><span class="sxs-lookup"><span data-stu-id="b55e9-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="b55e9-237">Тестирование сериализация объектов</span><span class="sxs-lookup"><span data-stu-id="b55e9-237">Testing Object Serialization</span></span>

<span data-ttu-id="b55e9-238">При разработке веб-API, полезно проверить, как будет сериализовать объекты данных.</span><span class="sxs-lookup"><span data-stu-id="b55e9-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="b55e9-239">Это можно сделать без создания контроллера или вызов действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="b55e9-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
