---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: Привязка параметра в веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: Описывает, как веб-API привязывает параметры и как настроить процесс привязки в ASP.NET 4. x.
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 464cb9b45dc0b62c4da38b7cf612934808854d32
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074908"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="24d96-103">Привязка параметра в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24d96-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="24d96-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="24d96-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="24d96-105">В этой статье описывается, как веб-API привязывает параметры и как можно настроить процесс привязки.</span><span class="sxs-lookup"><span data-stu-id="24d96-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="24d96-106">Когда веб-API вызывает метод на контроллере, он должен задать значения для параметров — процесс, называемый *Binding*.</span><span class="sxs-lookup"><span data-stu-id="24d96-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span>

<span data-ttu-id="24d96-107">По умолчанию для привязки параметров веб-API использует следующие правила:</span><span class="sxs-lookup"><span data-stu-id="24d96-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="24d96-108">Если параметр имеет тип Simple, веб-API пытается получить значение из универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="24d96-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="24d96-109">Простые типы включают в себя [примитивные типы](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) .NET (**int**, **bool**, **Double**и т. д.), а также **TimeSpan**, **DateTime**, **GUID**, **Decimal**и **String** *, а также любой тип* с преобразователем типов, который может выполнять преобразование из строки.</span><span class="sxs-lookup"><span data-stu-id="24d96-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="24d96-110">(Дополнительные сведения о преобразователях типов см. ниже.)</span><span class="sxs-lookup"><span data-stu-id="24d96-110">(More about type converters later.)</span></span>
- <span data-ttu-id="24d96-111">Для сложных типов веб-API пытается считать значение из текста сообщения с помощью [модуля форматирования типа мультимедиа](media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="24d96-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="24d96-112">Например, ниже приведен типичный метод контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="24d96-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="24d96-113">Параметр *ID* — это &quot;простой тип&quot;, поэтому веб-API пытается получить значение из универсального кода ресурса (URI) запроса.</span><span class="sxs-lookup"><span data-stu-id="24d96-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="24d96-114">Параметр *Item* является сложным типом, поэтому веб-API использует модуль форматирования типа мультимедиа для считывания значения из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="24d96-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="24d96-115">Чтобы получить значение из универсального кода ресурса (URI), веб-API ищет данные маршрута и строку запроса URI.</span><span class="sxs-lookup"><span data-stu-id="24d96-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="24d96-116">Данные маршрута заполняются, когда система маршрутизации анализирует URI и сопоставляет его с маршрутом.</span><span class="sxs-lookup"><span data-stu-id="24d96-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="24d96-117">Дополнительные сведения см. в разделе [Маршрутизация и выбор действий](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="24d96-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="24d96-118">В оставшейся части этой статьи я покажу, как можно настроить процесс привязки модели.</span><span class="sxs-lookup"><span data-stu-id="24d96-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="24d96-119">Однако для сложных типов рекомендуется использовать модули форматирования типа мультимедиа везде, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="24d96-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="24d96-120">Ключевым принципом протокола HTTP является то, что ресурсы отправляются в тексте сообщения с помощью согласования содержимого для указания представления ресурса.</span><span class="sxs-lookup"><span data-stu-id="24d96-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="24d96-121">Модули форматирования типа мультимедиа предназначены именно для этой цели.</span><span class="sxs-lookup"><span data-stu-id="24d96-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="24d96-122">Использование [Фромури]</span><span class="sxs-lookup"><span data-stu-id="24d96-122">Using [FromUri]</span></span>

<span data-ttu-id="24d96-123">Чтобы заставить веб-API считывать сложный тип из универсального кода ресурса (URI), добавьте атрибут **[фромури]** в параметр.</span><span class="sxs-lookup"><span data-stu-id="24d96-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="24d96-124">В следующем примере определяется тип `GeoPoint`, а также метод контроллера, который получает `GeoPoint` из универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="24d96-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="24d96-125">Клиент может разместить значения широты и долготы в строке запроса, а веб-API будет использовать их для создания `GeoPoint`.</span><span class="sxs-lookup"><span data-stu-id="24d96-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="24d96-126">Например:</span><span class="sxs-lookup"><span data-stu-id="24d96-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="24d96-127">Использование [FromBody]</span><span class="sxs-lookup"><span data-stu-id="24d96-127">Using [FromBody]</span></span>

<span data-ttu-id="24d96-128">Чтобы заставить веб-API считывать простой тип из текста запроса, добавьте атрибут **[FromBody]** в параметр:</span><span class="sxs-lookup"><span data-stu-id="24d96-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="24d96-129">В этом примере веб-API будет использовать модуль форматирования типа мультимедиа для считывания значения *имени* из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="24d96-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="24d96-130">Ниже приведен пример клиентского запроса.</span><span class="sxs-lookup"><span data-stu-id="24d96-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="24d96-131">Если параметр имеет значение [FromBody], веб-API использует заголовок Content-Type для выбора модуля форматирования.</span><span class="sxs-lookup"><span data-stu-id="24d96-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="24d96-132">В этом примере тип содержимого — &quot;Application/JSON&quot;, а текст запроса — необработанная строка JSON (не объект JSON).</span><span class="sxs-lookup"><span data-stu-id="24d96-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="24d96-133">Для чтения текста сообщения может быть не более одного параметра.</span><span class="sxs-lookup"><span data-stu-id="24d96-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="24d96-134">Поэтому это не будет работать:</span><span class="sxs-lookup"><span data-stu-id="24d96-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="24d96-135">Причина этого правила заключается в том, что текст запроса может храниться в небуферизованном потоке, который может быть считан только один раз.</span><span class="sxs-lookup"><span data-stu-id="24d96-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="24d96-136">Преобразователи типов</span><span class="sxs-lookup"><span data-stu-id="24d96-136">Type Converters</span></span>

<span data-ttu-id="24d96-137">Веб-API может рассматривать класс как простой тип (поэтому веб-API будет пытаться привязать его из универсального кода ресурса (URI)), создав **TypeConverter** и добавив преобразование строки.</span><span class="sxs-lookup"><span data-stu-id="24d96-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="24d96-138">В следующем коде показан класс `GeoPoint`, представляющий географическую точку, а также **TypeConverter** , который преобразует строки в `GeoPoint` экземпляры.</span><span class="sxs-lookup"><span data-stu-id="24d96-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="24d96-139">Класс `GeoPoint` снабжен атрибутом **[TypeConverter]** для указания преобразователя типов.</span><span class="sxs-lookup"><span data-stu-id="24d96-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="24d96-140">(Этот пример был связан с записью блога Mike в блоге [о том, как выполнить привязку к пользовательским объектам в сигнатурах действий в MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span><span class="sxs-lookup"><span data-stu-id="24d96-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="24d96-141">Теперь веб-API будет обрабатывать `GeoPoint` как простой тип, то есть будет пытаться привязать `GeoPoint` параметры из универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="24d96-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="24d96-142">В параметре не нужно включать **[фромури]** .</span><span class="sxs-lookup"><span data-stu-id="24d96-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="24d96-143">Клиент может вызвать метод с URI следующим образом:</span><span class="sxs-lookup"><span data-stu-id="24d96-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="24d96-144">Привязки моделей</span><span class="sxs-lookup"><span data-stu-id="24d96-144">Model Binders</span></span>

<span data-ttu-id="24d96-145">Более гибкий вариант, чем преобразователь типов, заключается в создании пользовательского связывателя модели.</span><span class="sxs-lookup"><span data-stu-id="24d96-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="24d96-146">При использовании связывателя модели у вас есть доступ к таким средствам, как HTTP-запрос, описание действия и необработанные значения из данных маршрута.</span><span class="sxs-lookup"><span data-stu-id="24d96-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="24d96-147">Чтобы создать связыватель модели, реализуйте интерфейс **имоделбиндер** .</span><span class="sxs-lookup"><span data-stu-id="24d96-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="24d96-148">Этот интерфейс определяет единственный метод **биндмодел**:</span><span class="sxs-lookup"><span data-stu-id="24d96-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="24d96-149">Ниже приведен связыватель модели для `GeoPoint` объектов.</span><span class="sxs-lookup"><span data-stu-id="24d96-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="24d96-150">Связыватель модели получает необработанные входные значения от *поставщика значений*.</span><span class="sxs-lookup"><span data-stu-id="24d96-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="24d96-151">Этот проект разделяет две отдельные функции:</span><span class="sxs-lookup"><span data-stu-id="24d96-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="24d96-152">Поставщик значений принимает HTTP-запрос и заполняет словарь пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="24d96-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="24d96-153">Связыватель модели использует этот словарь для заполнения модели.</span><span class="sxs-lookup"><span data-stu-id="24d96-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="24d96-154">Поставщик значений по умолчанию в веб-API получает значения из данных маршрута и строки запроса.</span><span class="sxs-lookup"><span data-stu-id="24d96-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="24d96-155">Например, если универсальный код ресурса (URI) `http://localhost/api/values/1?location=48,-122`, поставщик значений создает следующие пары "ключ-значение":</span><span class="sxs-lookup"><span data-stu-id="24d96-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="24d96-156">ID = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="24d96-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="24d96-157">Расположение = &quot;48 122&quot;</span><span class="sxs-lookup"><span data-stu-id="24d96-157">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="24d96-158">(Предполагается, что используется шаблон маршрута по умолчанию, который &quot;API/{Controller}/{ID}&quot;.)</span><span class="sxs-lookup"><span data-stu-id="24d96-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="24d96-159">Имя параметра для привязки хранится в свойстве **моделбиндингконтекст. ModelName** .</span><span class="sxs-lookup"><span data-stu-id="24d96-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="24d96-160">Связыватель модели ищет ключ с этим значением в словаре.</span><span class="sxs-lookup"><span data-stu-id="24d96-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="24d96-161">Если значение существует и может быть преобразовано в `GeoPoint`, связыватель модели присваивает связанное значение свойству **моделбиндингконтекст. Model** .</span><span class="sxs-lookup"><span data-stu-id="24d96-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="24d96-162">Обратите внимание, что связыватель модели не ограничивается простым преобразованием типов.</span><span class="sxs-lookup"><span data-stu-id="24d96-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="24d96-163">В этом примере связыватель модели сначала выполняет поиск в таблице известных расположений, и в случае сбоя он использует преобразование типов.</span><span class="sxs-lookup"><span data-stu-id="24d96-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="24d96-164">**Настройка связывателя модели**</span><span class="sxs-lookup"><span data-stu-id="24d96-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="24d96-165">Существует несколько способов задать связыватель модели.</span><span class="sxs-lookup"><span data-stu-id="24d96-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="24d96-166">Во-первых, в параметр можно добавить атрибут **[моделбиндер]** .</span><span class="sxs-lookup"><span data-stu-id="24d96-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="24d96-167">К типу можно также добавить атрибут **[моделбиндер]** .</span><span class="sxs-lookup"><span data-stu-id="24d96-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="24d96-168">Веб-API будет использовать указанный связыватель модели для всех параметров этого типа.</span><span class="sxs-lookup"><span data-stu-id="24d96-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="24d96-169">Наконец, можно добавить поставщик привязки модели в **HttpConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="24d96-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="24d96-170">Поставщик привязки модели — это просто класс фабрики, который создает связыватель модели.</span><span class="sxs-lookup"><span data-stu-id="24d96-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="24d96-171">Поставщик можно создать, создав производный от класса [моделбиндерпровидер](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) .</span><span class="sxs-lookup"><span data-stu-id="24d96-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="24d96-172">Однако если связыватель модели обрабатывает один тип, проще использовать встроенный **симплемоделбиндерпровидер**, который предназначен для этой цели.</span><span class="sxs-lookup"><span data-stu-id="24d96-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="24d96-173">В следующем примере кода показано, как это сделать:</span><span class="sxs-lookup"><span data-stu-id="24d96-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="24d96-174">При использовании поставщика привязки модели по-прежнему необходимо добавить атрибут **[моделбиндер]** в параметр, чтобы сообщить веб-API, что он должен использовать связыватель модели, а не модуль форматирования типа мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="24d96-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="24d96-175">Но теперь не нужно указывать тип связывателя модели в атрибуте:</span><span class="sxs-lookup"><span data-stu-id="24d96-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="24d96-176">Поставщики значений</span><span class="sxs-lookup"><span data-stu-id="24d96-176">Value Providers</span></span>

<span data-ttu-id="24d96-177">Я упомянул, что связыватель модели получает значения от поставщика значений.</span><span class="sxs-lookup"><span data-stu-id="24d96-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="24d96-178">Чтобы написать поставщик настраиваемого значения, реализуйте интерфейс **ивалуепровидер** .</span><span class="sxs-lookup"><span data-stu-id="24d96-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="24d96-179">Ниже приведен пример, который извлекает значения из файлов cookie в запросе:</span><span class="sxs-lookup"><span data-stu-id="24d96-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="24d96-180">Кроме того, необходимо создать фабрику поставщика значений, производная от класса **валуепровидерфактори** .</span><span class="sxs-lookup"><span data-stu-id="24d96-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="24d96-181">Добавьте фабрику поставщика значений в **HttpConfiguration** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="24d96-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="24d96-182">Веб-API формирует все поставщики значений, поэтому когда связыватель модели вызывает **значение valueprovider. GetValue**, связыватель модели получает значение от первого поставщика значений, который может его создать.</span><span class="sxs-lookup"><span data-stu-id="24d96-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="24d96-183">Кроме того, можно задать фабрику поставщика значений на уровне параметров с помощью атрибута **значение valueprovider** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="24d96-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="24d96-184">Это указывает веб-API использовать привязку модели с заданной фабрикой поставщика значений, а не использовать другие зарегистрированные поставщики значений.</span><span class="sxs-lookup"><span data-stu-id="24d96-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="24d96-185">хттппараметербиндинг</span><span class="sxs-lookup"><span data-stu-id="24d96-185">HttpParameterBinding</span></span>

<span data-ttu-id="24d96-186">Связыватели моделей — это конкретный экземпляр более общего механизма.</span><span class="sxs-lookup"><span data-stu-id="24d96-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="24d96-187">Если взглянуть на атрибут **[моделбиндер]** , вы увидите, что он является производным от абстрактного класса **параметербиндингаттрибуте** .</span><span class="sxs-lookup"><span data-stu-id="24d96-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="24d96-188">Этот класс определяет единственный метод- **Binding**, который возвращает объект **хттппараметербиндинг** :</span><span class="sxs-lookup"><span data-stu-id="24d96-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="24d96-189">**Хттппараметербиндинг** отвечает за привязку параметра к значению.</span><span class="sxs-lookup"><span data-stu-id="24d96-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="24d96-190">В случае **[моделбиндер]** атрибут возвращает реализацию **хттппараметербиндинг** , которая использует **имоделбиндер** для выполнения фактической привязки.</span><span class="sxs-lookup"><span data-stu-id="24d96-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="24d96-191">Вы также можете реализовать собственный **хттппараметербиндинг**.</span><span class="sxs-lookup"><span data-stu-id="24d96-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="24d96-192">Например, предположим, что необходимо получить ETag из `if-match` и `if-none-match` заголовков в запросе.</span><span class="sxs-lookup"><span data-stu-id="24d96-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="24d96-193">Начнем с определения класса для представления ETag.</span><span class="sxs-lookup"><span data-stu-id="24d96-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="24d96-194">Также будет определено перечисление, указывающее, следует ли получить ETag из заголовка `if-match` или `if-none-match`.</span><span class="sxs-lookup"><span data-stu-id="24d96-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="24d96-195">Вот **хттппараметербиндинг** , который получает eTag из нужного заголовка и привязывает его к параметру типа ETag:</span><span class="sxs-lookup"><span data-stu-id="24d96-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="24d96-196">Метод **ексекутебиндингасинк** выполняет привязку.</span><span class="sxs-lookup"><span data-stu-id="24d96-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="24d96-197">В этом методе добавьте связанное значение параметра в словарь **актионаргумент** в **хттпактионконтекст**.</span><span class="sxs-lookup"><span data-stu-id="24d96-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="24d96-198">Если метод **ексекутебиндингасинк** считывает текст сообщения запроса, переопределите свойство **виллреадбоди** , чтобы оно возвращало значение true.</span><span class="sxs-lookup"><span data-stu-id="24d96-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="24d96-199">Тело запроса может быть небуферизованным потоком, который может быть считан только один раз, поэтому веб-API принудительно применяет правило, которое может считывать только одна привязка к тексту сообщения.</span><span class="sxs-lookup"><span data-stu-id="24d96-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>

<span data-ttu-id="24d96-200">Чтобы применить пользовательский **хттппараметербиндинг**, можно определить атрибут, производный от **параметербиндингаттрибуте**.</span><span class="sxs-lookup"><span data-stu-id="24d96-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="24d96-201">Для `ETagParameterBinding`мы определим два атрибута: один для `if-match` заголовков и один для `if-none-match` заголовков.</span><span class="sxs-lookup"><span data-stu-id="24d96-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="24d96-202">Оба являются производными от абстрактного базового класса.</span><span class="sxs-lookup"><span data-stu-id="24d96-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="24d96-203">Ниже приведен метод контроллера, использующий атрибут `[IfNoneMatch]`.</span><span class="sxs-lookup"><span data-stu-id="24d96-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="24d96-204">Помимо **параметербиндингаттрибуте**, существует еще один обработчик для добавления пользовательского **хттппараметербиндинг**.</span><span class="sxs-lookup"><span data-stu-id="24d96-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="24d96-205">В объекте **HttpConfiguration** свойство **параметербиндингрулес** является коллекцией анонимных функций типа (**хттппараметердескриптор** -&gt; **хттппараметербиндинг**).</span><span class="sxs-lookup"><span data-stu-id="24d96-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="24d96-206">Например, можно добавить правило, которое любой параметр ETag в методе GET использует `ETagParameterBinding` с `if-none-match`:</span><span class="sxs-lookup"><span data-stu-id="24d96-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="24d96-207">Функция должна возвращать `null` для параметров, в которых привязка неприменима.</span><span class="sxs-lookup"><span data-stu-id="24d96-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="24d96-208">иактионвалуебиндер</span><span class="sxs-lookup"><span data-stu-id="24d96-208">IActionValueBinder</span></span>

<span data-ttu-id="24d96-209">Весь процесс привязки параметров управляется подключаемой службой **иактионвалуебиндер**.</span><span class="sxs-lookup"><span data-stu-id="24d96-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="24d96-210">Реализация **иактионвалуебиндер** по умолчанию выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="24d96-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="24d96-211">Найдите **параметербиндингаттрибуте** в параметре.</span><span class="sxs-lookup"><span data-stu-id="24d96-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="24d96-212">К ним относятся **[FromBody]** , **[фромури]** и **[моделбиндер]** , а также настраиваемые атрибуты.</span><span class="sxs-lookup"><span data-stu-id="24d96-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="24d96-213">В противном случае найдите в **HttpConfiguration. параметербиндингрулес** функцию, которая возвращает значение **хттппараметербиндинг**, отличное от NULL.</span><span class="sxs-lookup"><span data-stu-id="24d96-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="24d96-214">В противном случае используйте правила по умолчанию, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="24d96-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="24d96-215">Если параметр имеет тип "Simple" или имеет преобразователь типов, выполните привязку из универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="24d96-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="24d96-216">Это эквивалентно размещению атрибута **[фромури]** в параметре.</span><span class="sxs-lookup"><span data-stu-id="24d96-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="24d96-217">В противном случае попробуйте прочитать параметр из текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="24d96-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="24d96-218">Это эквивалентно размещению **[FromBody]** в параметре.</span><span class="sxs-lookup"><span data-stu-id="24d96-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="24d96-219">При необходимости можно заменить всю службу **иактионвалуебиндер** собственной реализацией.</span><span class="sxs-lookup"><span data-stu-id="24d96-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24d96-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="24d96-220">Additional Resources</span></span>

[<span data-ttu-id="24d96-221">Пример пользовательской привязки параметра</span><span class="sxs-lookup"><span data-stu-id="24d96-221">Custom Parameter Binding Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

<span data-ttu-id="24d96-222">Майк записал хорошие серии записей блога о привязке параметров веб-API:</span><span class="sxs-lookup"><span data-stu-id="24d96-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="24d96-223">Как веб-API выполняет привязку параметров</span><span class="sxs-lookup"><span data-stu-id="24d96-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="24d96-224">Привязка параметра стиля MVC для веб-API</span><span class="sxs-lookup"><span data-stu-id="24d96-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="24d96-225">Привязка к пользовательским объектам в сигнатурах действий в MVC и веб-API</span><span class="sxs-lookup"><span data-stu-id="24d96-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="24d96-226">Создание пользовательского поставщика значений в веб-API</span><span class="sxs-lookup"><span data-stu-id="24d96-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="24d96-227">Привязка параметра веб-API в невнутреннем режиме</span><span class="sxs-lookup"><span data-stu-id="24d96-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
