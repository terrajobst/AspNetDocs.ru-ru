---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: Отношения сущностей в OData v4 с использованием веб-API ASP.NET 2,2 | Документация Майкрософт
author: MikeWasson
description: 'Большинство наборов данных определяют связи между сущностями: у клиентов есть заказы. книги имеют авторов; продукты имеют поставщики. С помощью OData клиенты могут перемещаться по...'
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484464"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="b36c7-104">Отношения сущностей в OData v4 с использованием веб-API ASP.NET 2,2</span><span class="sxs-lookup"><span data-stu-id="b36c7-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="b36c7-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b36c7-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="b36c7-106">Большинство наборов данных определяют связи между сущностями: у клиентов есть заказы. книги имеют авторов; продукты имеют поставщики.</span><span class="sxs-lookup"><span data-stu-id="b36c7-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="b36c7-107">С помощью OData клиенты могут перемещаться по связям сущностей.</span><span class="sxs-lookup"><span data-stu-id="b36c7-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="b36c7-108">С учетом продукта можно найти поставщика.</span><span class="sxs-lookup"><span data-stu-id="b36c7-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="b36c7-109">Также можно создавать и удалять связи.</span><span class="sxs-lookup"><span data-stu-id="b36c7-109">You can also create or remove relationships.</span></span> <span data-ttu-id="b36c7-110">Например, можно задать поставщика для продукта.</span><span class="sxs-lookup"><span data-stu-id="b36c7-110">For example, you can set the supplier for a product.</span></span>
>
> <span data-ttu-id="b36c7-111">В этом руководстве показано, как поддерживать эти операции в OData v4 с помощью веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b36c7-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="b36c7-112">Руководство по построению в руководстве по [созданию конечной точки OData v4 с помощью веб-API ASP.NET 2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b36c7-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b36c7-113">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="b36c7-113">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="b36c7-114">Веб-API 2,1</span><span class="sxs-lookup"><span data-stu-id="b36c7-114">Web API 2.1</span></span>
> - <span data-ttu-id="b36c7-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="b36c7-115">OData v4</span></span>
> - <span data-ttu-id="b36c7-116">Visual Studio 2013 (Скачайте Visual Studio 2017 [здесь](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="b36c7-116">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="b36c7-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="b36c7-117">Entity Framework 6</span></span>
> - <span data-ttu-id="b36c7-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b36c7-118">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="b36c7-119">Учебные версии</span><span class="sxs-lookup"><span data-stu-id="b36c7-119">Tutorial versions</span></span>
>
> <span data-ttu-id="b36c7-120">Сведения для OData версии 3 см. [в разделе Поддержка связей сущностей в OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span><span class="sxs-lookup"><span data-stu-id="b36c7-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="b36c7-121">Добавление сущности поставщика</span><span class="sxs-lookup"><span data-stu-id="b36c7-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="b36c7-122">Руководство по построению в руководстве по [созданию конечной точки OData v4 с помощью веб-API ASP.NET 2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b36c7-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="b36c7-123">Во-первых, нам нужна связанная сущность.</span><span class="sxs-lookup"><span data-stu-id="b36c7-123">First, we need a related entity.</span></span> <span data-ttu-id="b36c7-124">Добавьте класс с именем `Supplier` в папку Models.</span><span class="sxs-lookup"><span data-stu-id="b36c7-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="b36c7-125">Добавьте свойство навигации в класс `Product`:</span><span class="sxs-lookup"><span data-stu-id="b36c7-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="b36c7-126">Добавьте новый **DbSet** в класс `ProductsContext`, чтобы Entity Framework включала таблицу поставщика в базе данных.</span><span class="sxs-lookup"><span data-stu-id="b36c7-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="b36c7-127">В WebApiConfig.cs добавьте поставщики &quot;&quot; набор сущностей в модель EDM:</span><span class="sxs-lookup"><span data-stu-id="b36c7-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="b36c7-128">Добавление контроллера поставщиков</span><span class="sxs-lookup"><span data-stu-id="b36c7-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="b36c7-129">Добавьте класс `SuppliersController` в папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="b36c7-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="b36c7-130">Я не буду показывать, как добавить операции CRUD для этого контроллера.</span><span class="sxs-lookup"><span data-stu-id="b36c7-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="b36c7-131">Эти шаги те же, что и для контроллера Products (см. раздел [Создание конечной точки OData v4](create-an-odata-v4-endpoint.md)).</span><span class="sxs-lookup"><span data-stu-id="b36c7-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="b36c7-132">Получение связанных сущностей</span><span class="sxs-lookup"><span data-stu-id="b36c7-132">Getting Related Entities</span></span>

<span data-ttu-id="b36c7-133">Чтобы получить поставщик для продукта, клиент отправляет запрос GET:</span><span class="sxs-lookup"><span data-stu-id="b36c7-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="b36c7-134">Для поддержки этого запроса добавьте в класс `ProductsController` следующий метод:</span><span class="sxs-lookup"><span data-stu-id="b36c7-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="b36c7-135">Этот метод использует соглашение об именовании по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b36c7-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="b36c7-136">Имя метода: Жеткс, где X — это свойство навигации.</span><span class="sxs-lookup"><span data-stu-id="b36c7-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="b36c7-137">Имя параметра: *ключ*</span><span class="sxs-lookup"><span data-stu-id="b36c7-137">Parameter name: *key*</span></span>

<span data-ttu-id="b36c7-138">Если следовать этому соглашению об именовании, веб-API автоматически сопоставляет запрос HTTP методу контроллера.</span><span class="sxs-lookup"><span data-stu-id="b36c7-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="b36c7-139">Пример HTTP-запроса:</span><span class="sxs-lookup"><span data-stu-id="b36c7-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="b36c7-140">Пример HTTP-ответа:</span><span class="sxs-lookup"><span data-stu-id="b36c7-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="b36c7-141">Получение связанной коллекции</span><span class="sxs-lookup"><span data-stu-id="b36c7-141">Getting a related collection</span></span>

<span data-ttu-id="b36c7-142">В предыдущем примере продукт имеет одного поставщика.</span><span class="sxs-lookup"><span data-stu-id="b36c7-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="b36c7-143">Свойство навигации также может возвращать коллекцию.</span><span class="sxs-lookup"><span data-stu-id="b36c7-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="b36c7-144">Следующий код получает продукты для поставщика:</span><span class="sxs-lookup"><span data-stu-id="b36c7-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="b36c7-145">В этом случае метод возвращает **IQueryable** , а не **синглересулт&lt;t&gt;**</span><span class="sxs-lookup"><span data-stu-id="b36c7-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="b36c7-146">Пример HTTP-запроса:</span><span class="sxs-lookup"><span data-stu-id="b36c7-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="b36c7-147">Пример HTTP-ответа:</span><span class="sxs-lookup"><span data-stu-id="b36c7-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="b36c7-148">Создание связи между сущностями</span><span class="sxs-lookup"><span data-stu-id="b36c7-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="b36c7-149">OData поддерживает создание или удаление связей между двумя существующими сущностями.</span><span class="sxs-lookup"><span data-stu-id="b36c7-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="b36c7-150">В терминологии OData версии 4 отношение является &quot;ссылкой&quot;.</span><span class="sxs-lookup"><span data-stu-id="b36c7-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="b36c7-151">(В OData v3 связь называлась *ссылкой*.</span><span class="sxs-lookup"><span data-stu-id="b36c7-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="b36c7-152">Различия в протоколе не важны для работы с этим руководством.)</span><span class="sxs-lookup"><span data-stu-id="b36c7-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="b36c7-153">Ссылка имеет собственный URI с формой `/Entity/NavigationProperty/$ref`.</span><span class="sxs-lookup"><span data-stu-id="b36c7-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="b36c7-154">Например, ниже приведен URI для обращения к ссылке между продуктом и его поставщиком.</span><span class="sxs-lookup"><span data-stu-id="b36c7-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="b36c7-155">Чтобы добавить связь, клиент отправляет запрос POST или помещается по этому адресу.</span><span class="sxs-lookup"><span data-stu-id="b36c7-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="b36c7-156">Помещайте, если свойство навигации является одной сущностью, например `Product.Supplier`.</span><span class="sxs-lookup"><span data-stu-id="b36c7-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="b36c7-157">POST, если свойство навигации является коллекцией, например `Supplier.Products`.</span><span class="sxs-lookup"><span data-stu-id="b36c7-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="b36c7-158">Текст запроса содержит URI другой сущности в отношении.</span><span class="sxs-lookup"><span data-stu-id="b36c7-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="b36c7-159">Ниже приведен пример запроса:</span><span class="sxs-lookup"><span data-stu-id="b36c7-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="b36c7-160">В этом примере клиент отправляет запрос на размещение в `/Products(6)/Supplier/$ref`, который является $ref URI для `Supplier` продукта с ИДЕНТИФИКАТОРом 6.</span><span class="sxs-lookup"><span data-stu-id="b36c7-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="b36c7-161">Если запрос выполнен, сервер отправляет ответ 204 (без содержимого):</span><span class="sxs-lookup"><span data-stu-id="b36c7-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="b36c7-162">Ниже приведен метод контроллера для добавления отношения к `Product`.</span><span class="sxs-lookup"><span data-stu-id="b36c7-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="b36c7-163">Параметр *navigationProperty* указывает, какую связь следует задать.</span><span class="sxs-lookup"><span data-stu-id="b36c7-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="b36c7-164">(Если в сущности имеется более одного свойства навигации, можно добавить дополнительные операторы `case`.)</span><span class="sxs-lookup"><span data-stu-id="b36c7-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="b36c7-165">Параметр *Link* содержит универсальный код ресурса (URI) поставщика.</span><span class="sxs-lookup"><span data-stu-id="b36c7-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="b36c7-166">Веб-API автоматически анализирует текст запроса, чтобы получить значение для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="b36c7-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="b36c7-167">Для поиска поставщика требуется идентификатор (или ключ), который является частью параметра *Link* .</span><span class="sxs-lookup"><span data-stu-id="b36c7-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="b36c7-168">Для этого используйте следующий вспомогательный метод:</span><span class="sxs-lookup"><span data-stu-id="b36c7-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="b36c7-169">По сути, этот метод использует библиотеку OData для разделения пути URI на сегменты, поиска сегмента, содержащего ключ, и преобразования ключа в правильный тип.</span><span class="sxs-lookup"><span data-stu-id="b36c7-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="b36c7-170">Удаление связи между сущностями</span><span class="sxs-lookup"><span data-stu-id="b36c7-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="b36c7-171">Чтобы удалить связь, клиент отправляет запрос HTTP DELETE в URI $ref:</span><span class="sxs-lookup"><span data-stu-id="b36c7-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="b36c7-172">Ниже приведен метод контроллера для удаления связи между продуктом и поставщиком.</span><span class="sxs-lookup"><span data-stu-id="b36c7-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="b36c7-173">В этом случае `Product.Supplier` является &quot;1&quot; окончании отношения «один ко многим», поэтому связь можно удалить, просто установив `Product.Supplier` в `null`.</span><span class="sxs-lookup"><span data-stu-id="b36c7-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="b36c7-174">В &quot;многих&quot; конец связи, клиент должен указать, какую связанную сущность следует удалить.</span><span class="sxs-lookup"><span data-stu-id="b36c7-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="b36c7-175">Для этого клиент отправляет универсальный код ресурса (URI) связанной сущности в строке запроса запроса.</span><span class="sxs-lookup"><span data-stu-id="b36c7-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="b36c7-176">Например, чтобы удалить «Product 1» из «поставщика 1»:</span><span class="sxs-lookup"><span data-stu-id="b36c7-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="b36c7-177">Для поддержки этой функции в веб-API необходимо включить дополнительный параметр в метод `DeleteRef`.</span><span class="sxs-lookup"><span data-stu-id="b36c7-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="b36c7-178">Ниже приведен метод контроллера для удаления продукта из отношения `Supplier.Products`.</span><span class="sxs-lookup"><span data-stu-id="b36c7-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="b36c7-179">Ключевым *параметром* является ключ для поставщика, а параметр *релатедкэй* — ключ продукта, который удаляется из связи `Products`.</span><span class="sxs-lookup"><span data-stu-id="b36c7-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="b36c7-180">Обратите внимание, что веб-API автоматически получает ключ из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="b36c7-180">Note that Web API automatically gets the key from the query string.</span></span>
