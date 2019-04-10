---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: Использование $select, $expand и $value в ASP.NET Web API 2 OData - ASP.NET 4.x
author: MikeWasson
description: Общие сведения и примеры кода для $развернуть, $select, и параметры $value в OData веб-API 2 ASP.NET 4.x.
ms.author: riande
ms.date: 10/11/2013
ms.custom: seoapril2019
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: 8b5d3e87c679a31f1908aa648219ae5c6b701a1f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400702"
---
# <a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a><span data-ttu-id="1b872-103">Использование $select, $expand и $value в ASP.NET Web API 2 OData</span><span class="sxs-lookup"><span data-stu-id="1b872-103">Using $select, $expand, and $value in ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="1b872-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1b872-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1b872-105">Общие сведения и примеры кода для $развернуть, $select, и параметры $value в OData веб-API 2 ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="1b872-105">Overview and code samples for the $expand, $select, and $value options in OData Web API 2 for ASP.NET 4.x.</span></span> <span data-ttu-id="1b872-106">Эти параметры позволяют клиенту управлять представление, которое возвращается с сервера.</span><span class="sxs-lookup"><span data-stu-id="1b872-106">These options allow a client to control the representation that it gets back from the server.</span></span>

- <span data-ttu-id="1b872-107">**$expand** вызывает связанные сущности быть указаны в ответе.</span><span class="sxs-lookup"><span data-stu-id="1b872-107">**$expand** causes related entities to be included inline in the response.</span></span>
- <span data-ttu-id="1b872-108">**$select** выбирает подмножество свойств для включения в ответ.</span><span class="sxs-lookup"><span data-stu-id="1b872-108">**$select** selects a subset of properties to include in the response.</span></span>
- <span data-ttu-id="1b872-109">**$value** получает необработанное значение свойства.</span><span class="sxs-lookup"><span data-stu-id="1b872-109">**$value** gets the raw value of a property.</span></span>

## <a name="example-schema"></a><span data-ttu-id="1b872-110">Пример схемы</span><span class="sxs-lookup"><span data-stu-id="1b872-110">Example Schema</span></span>

<span data-ttu-id="1b872-111">В этой статье я буду использовать службы OData, определяющий три сущности: Продукта, поставщика и категории.</span><span class="sxs-lookup"><span data-stu-id="1b872-111">For this article, I'll use an OData service that defines three entities: Product, Supplier, and Category.</span></span> <span data-ttu-id="1b872-112">Каждый продукт состоит из одной категории и одного поставщика.</span><span class="sxs-lookup"><span data-stu-id="1b872-112">Each product has one category and one supplier.</span></span>

![](using-select-expand-and-value/_static/image1.png)

<span data-ttu-id="1b872-113">Ниже приведены классы C#, которые определяют модели сущностей.</span><span class="sxs-lookup"><span data-stu-id="1b872-113">Here are the C# classes that define the entity models:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

<span data-ttu-id="1b872-114">Обратите внимание, что `Product` класс определяет свойства навигации для `Supplier` и `Category`.</span><span class="sxs-lookup"><span data-stu-id="1b872-114">Notice that the `Product` class defines navigation properties for the `Supplier` and `Category`.</span></span> <span data-ttu-id="1b872-115">`Category` Класс определяет свойство навигации для продуктов в каждой категории.</span><span class="sxs-lookup"><span data-stu-id="1b872-115">The `Category` class defines a navigation property for the products in each category.</span></span>

<span data-ttu-id="1b872-116">Чтобы создать конечную точку OData для этой схемы, использовать формирование шаблонов Visual Studio 2013, как описано в разделе [Создание конечной точки OData в веб-API ASP.NET](odata-v3/creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="1b872-116">To create an OData endpoint for this schema, use the Visual Studio 2013 scaffolding, as described in [Creating an OData Endpoint in ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span></span> <span data-ttu-id="1b872-117">Добавьте отдельные контроллеры для продукта, категорию и поставщика.</span><span class="sxs-lookup"><span data-stu-id="1b872-117">Add separate controllers for Product, Category, and Supplier.</span></span>

## <a name="enabling-expand-and-select"></a><span data-ttu-id="1b872-118">Включение $разверните и $select</span><span class="sxs-lookup"><span data-stu-id="1b872-118">Enabling $expand and $select</span></span>

<span data-ttu-id="1b872-119">В Visual Studio 2013 формирование шаблонов веб-API OData создает контроллер, автоматически поддерживает $expand и $select.</span><span class="sxs-lookup"><span data-stu-id="1b872-119">In Visual Studio 2013, the Web API OData scaffolding creates a controller that automatically supports $expand and $select.</span></span> <span data-ttu-id="1b872-120">Для справки ниже приведены, разверните узел требования для поддержки $ и $select в контроллере.</span><span class="sxs-lookup"><span data-stu-id="1b872-120">For reference, here are the requirements to support $expand and $select in a controller.</span></span>

<span data-ttu-id="1b872-121">Для коллекций, контроллер `Get` метод должен возвращать **IQueryable**.</span><span class="sxs-lookup"><span data-stu-id="1b872-121">For collections, the controller's `Get` method must return an **IQueryable**.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

<span data-ttu-id="1b872-122">Для одной сущности, возвращаемого **— SingleResult&lt;T&gt;**, где T — **IQueryable** , содержащая более одной сущности.</span><span class="sxs-lookup"><span data-stu-id="1b872-122">For single entities, return a **SingleResult&lt;T&gt;**, where T is an **IQueryable** that contains zero or one entities.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

<span data-ttu-id="1b872-123">Кроме того, снабдить вашего `Get` методы с **[Queryable]** атрибута, как показано в предыдущих фрагментах кода.</span><span class="sxs-lookup"><span data-stu-id="1b872-123">Also, decorate your `Get` methods with the **[Queryable]** attribute, as shown in the previous code snippets.</span></span> <span data-ttu-id="1b872-124">Кроме того, вызвать **EnableQuerySupport** на **HttpConfiguration** объекта во время запуска.</span><span class="sxs-lookup"><span data-stu-id="1b872-124">Alternatively, call **EnableQuerySupport** on the **HttpConfiguration** object at startup.</span></span> <span data-ttu-id="1b872-125">(Дополнительные сведения см. в разделе [включения параметров запроса OData](supporting-odata-query-options.md#enable).)</span><span class="sxs-lookup"><span data-stu-id="1b872-125">(For more information, see [Enabling OData Query Options](supporting-odata-query-options.md#enable).)</span></span>

## <a name="using-expand"></a><span data-ttu-id="1b872-126">Разверните узел с помощью $</span><span class="sxs-lookup"><span data-stu-id="1b872-126">Using $expand</span></span>

<span data-ttu-id="1b872-127">При запросе OData сущность или коллекцию, ответ по умолчанию не включает связанных сущностей.</span><span class="sxs-lookup"><span data-stu-id="1b872-127">When you query an OData entity or collection, the default response does not include related entities.</span></span> <span data-ttu-id="1b872-128">Например вот ответ по умолчанию для набора сущностей категории:</span><span class="sxs-lookup"><span data-stu-id="1b872-128">For example, here is the default response for the Categories entity set:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

<span data-ttu-id="1b872-129">Как вы видите, ответ не включает все продукты, несмотря на то, что сущность «Категория» содержит ссылку перехода продуктов.</span><span class="sxs-lookup"><span data-stu-id="1b872-129">As you can see, the response does not include any products, even though the Category entity has a Products navigation link.</span></span> <span data-ttu-id="1b872-130">Тем не менее, клиент может использовать $разверните, чтобы получить список продуктов для каждой категории.</span><span class="sxs-lookup"><span data-stu-id="1b872-130">However, the client can use $expand to get the list of products for each category.</span></span> <span data-ttu-id="1b872-131">Параметр expand $ переходит в строке запроса:</span><span class="sxs-lookup"><span data-stu-id="1b872-131">The $expand option goes in the query string of the request:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

<span data-ttu-id="1b872-132">Теперь сервер будет включать продукты для каждой категории, встроенные с категориями.</span><span class="sxs-lookup"><span data-stu-id="1b872-132">Now the server will include the products for each category, inline with the categories.</span></span> <span data-ttu-id="1b872-133">Ниже приведен полезных данных ответа.</span><span class="sxs-lookup"><span data-stu-id="1b872-133">Here is the response payload:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

<span data-ttu-id="1b872-134">Обратите внимание на то, что каждая запись в массиве «значение» со списком продуктов.</span><span class="sxs-lookup"><span data-stu-id="1b872-134">Notice that each entry in the "value" array contains a Products list.</span></span>

<span data-ttu-id="1b872-135">$Expand параметр принимает разделенный запятыми список свойств навигации для развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b872-135">The $expand option takes a comma-separated list of navigation properties to expand.</span></span> <span data-ttu-id="1b872-136">Следующий запрос расширяет категорию и поставщика для продукта.</span><span class="sxs-lookup"><span data-stu-id="1b872-136">The following request expands both the category and the supplier for a product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

<span data-ttu-id="1b872-137">Ниже приведен текст ответа:</span><span class="sxs-lookup"><span data-stu-id="1b872-137">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

<span data-ttu-id="1b872-138">Вы можете развернуть более одного уровня свойства навигации.</span><span class="sxs-lookup"><span data-stu-id="1b872-138">You can expand more than one level of navigation property.</span></span> <span data-ttu-id="1b872-139">Следующий пример включает все продукты для категории, а также поставщика для каждого продукта.</span><span class="sxs-lookup"><span data-stu-id="1b872-139">The following example includes all the products for a category and also the supplier for each product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

<span data-ttu-id="1b872-140">Ниже приведен текст ответа:</span><span class="sxs-lookup"><span data-stu-id="1b872-140">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

<span data-ttu-id="1b872-141">По умолчанию веб-API ограничивает максимальное расширения глубина до 2.</span><span class="sxs-lookup"><span data-stu-id="1b872-141">By default, Web API limits the maximum expansion depth to 2.</span></span> <span data-ttu-id="1b872-142">Не позволяет клиенту отправлять сложных запросов, например `$expand=Orders/OrderDetails/Product/Supplier/Region`, который может быть неэффективным для запроса и создание больших ответов.</span><span class="sxs-lookup"><span data-stu-id="1b872-142">That prevents the client from sending complex requests like `$expand=Orders/OrderDetails/Product/Supplier/Region`, which might be inefficient to query and create large responses.</span></span> <span data-ttu-id="1b872-143">Чтобы переопределить значение по умолчанию, задайте **MaxExpansionDepth** свойство **[Queryable]** атрибута.</span><span class="sxs-lookup"><span data-stu-id="1b872-143">To override the default, set the **MaxExpansionDepth** property on the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

<span data-ttu-id="1b872-144">Дополнительные сведения о $разверните параметр, см. в разделе [системный параметр запроса ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) в официальной документации OData.</span><span class="sxs-lookup"><span data-stu-id="1b872-144">For more information about the $expand option, see [Expand System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) in the official OData documentation.</span></span>

## <a name="using-select"></a><span data-ttu-id="1b872-145">Использование $select</span><span class="sxs-lookup"><span data-stu-id="1b872-145">Using $select</span></span>

<span data-ttu-id="1b872-146">Параметр $select определяет подмножество свойств для включения в тексте ответа.</span><span class="sxs-lookup"><span data-stu-id="1b872-146">The $select option specifies a subset of properties to include in the response body.</span></span> <span data-ttu-id="1b872-147">Например чтобы получить только название и цену каждого продукта, используйте следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="1b872-147">For example, to get only the name and price of each product, use the following query:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

<span data-ttu-id="1b872-148">Ниже приведен текст ответа:</span><span class="sxs-lookup"><span data-stu-id="1b872-148">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

<span data-ttu-id="1b872-149">Вы можете объединить $select и $expand в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="1b872-149">You can combine $select and $expand in the same query.</span></span> <span data-ttu-id="1b872-150">Не забудьте включить расширенное свойство в параметра $select.</span><span class="sxs-lookup"><span data-stu-id="1b872-150">Make sure to include the expanded property in the $select option.</span></span> <span data-ttu-id="1b872-151">Например следующий запрос возвращает имя продукта и поставщика.</span><span class="sxs-lookup"><span data-stu-id="1b872-151">For example, the following request gets the product name and supplier.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

<span data-ttu-id="1b872-152">Ниже приведен текст ответа:</span><span class="sxs-lookup"><span data-stu-id="1b872-152">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

<span data-ttu-id="1b872-153">Можно также выбрать свойства, используемые в расширенное свойство.</span><span class="sxs-lookup"><span data-stu-id="1b872-153">You can also select the properties within an expanded property.</span></span> <span data-ttu-id="1b872-154">Следующий запрос расширяет продуктов и выбирает имя категории, а также название продукта.</span><span class="sxs-lookup"><span data-stu-id="1b872-154">The following request expands Products and selects category name plus product name.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

<span data-ttu-id="1b872-155">Ниже приведен текст ответа:</span><span class="sxs-lookup"><span data-stu-id="1b872-155">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

<span data-ttu-id="1b872-156">Дополнительные сведения о параметра $select, см. в разделе [параметр системного запроса выбора ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) в официальной документации OData.</span><span class="sxs-lookup"><span data-stu-id="1b872-156">For more information about the $select option, see [Select System Query Option ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) in the official OData documentation.</span></span>

## <a name="getting-individual-properties-of-an-entity-value"></a><span data-ttu-id="1b872-157">Получение отдельных свойств сущности ($value)</span><span class="sxs-lookup"><span data-stu-id="1b872-157">Getting Individual Properties of an Entity ($value)</span></span>

<span data-ttu-id="1b872-158">Существует два способа для клиента OData для получения отдельного свойства из сущности.</span><span class="sxs-lookup"><span data-stu-id="1b872-158">There are two ways for an OData client to get an individual property from an entity.</span></span> <span data-ttu-id="1b872-159">Клиента можно получить значение в формате OData или получить необработанное значение свойства.</span><span class="sxs-lookup"><span data-stu-id="1b872-159">The client can either get the value in OData format, or get the raw value of the property.</span></span>

<span data-ttu-id="1b872-160">Следующий запрос возвращает свойство в формате OData.</span><span class="sxs-lookup"><span data-stu-id="1b872-160">The following request gets a property in OData format.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

<span data-ttu-id="1b872-161">Ниже приведен пример ответа в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="1b872-161">Here is an example response in JSON format:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

<span data-ttu-id="1b872-162">Чтобы получить необработанное значение свойства, добавьте $value к URI.</span><span class="sxs-lookup"><span data-stu-id="1b872-162">To get the raw value of the property, append $value to the URI:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

<span data-ttu-id="1b872-163">Вот ответ.</span><span class="sxs-lookup"><span data-stu-id="1b872-163">Here is the response.</span></span> <span data-ttu-id="1b872-164">Обратите внимание на то, что тип содержимого «text/plain», не является JSON.</span><span class="sxs-lookup"><span data-stu-id="1b872-164">Notice that the content type is "text/plain", not JSON.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

<span data-ttu-id="1b872-165">Поддерживает эти запросы в контроллере OData, добавьте метод с именем `GetProperty`, где `Property` — это имя свойства.</span><span class="sxs-lookup"><span data-stu-id="1b872-165">To support these queries in your OData controller, add a method named `GetProperty`, where `Property` is the name of the property.</span></span> <span data-ttu-id="1b872-166">Например, будет иметь имя метода для получения имени свойства `GetName`.</span><span class="sxs-lookup"><span data-stu-id="1b872-166">For example, the method to get the Name property would be named `GetName`.</span></span> <span data-ttu-id="1b872-167">Метод должен вернуть значение этого свойства:</span><span class="sxs-lookup"><span data-stu-id="1b872-167">The method should return the value of that property:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
