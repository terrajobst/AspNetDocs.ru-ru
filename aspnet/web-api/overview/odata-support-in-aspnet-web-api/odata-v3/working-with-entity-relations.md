---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: Поддержка отношений сущностей в OData v3 с веб-API 2 | Документация Майкрософт
author: MikeWasson
description: 'Большинство наборов данных определяют связи между сущностями: у клиентов есть заказы. книги имеют авторов; продукты имеют поставщики. С помощью OData клиенты могут перемещаться по...'
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484506"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="54866-104">Поддержка отношений сущностей в OData v3 с веб-API 2</span><span class="sxs-lookup"><span data-stu-id="54866-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>

<span data-ttu-id="54866-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="54866-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="54866-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="54866-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="54866-107">Большинство наборов данных определяют связи между сущностями: у клиентов есть заказы. книги имеют авторов; продукты имеют поставщики.</span><span class="sxs-lookup"><span data-stu-id="54866-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="54866-108">С помощью OData клиенты могут перемещаться по связям сущностей.</span><span class="sxs-lookup"><span data-stu-id="54866-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="54866-109">С учетом продукта можно найти поставщика.</span><span class="sxs-lookup"><span data-stu-id="54866-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="54866-110">Также можно создавать и удалять связи.</span><span class="sxs-lookup"><span data-stu-id="54866-110">You can also create or remove relationships.</span></span> <span data-ttu-id="54866-111">Например, можно задать поставщика для продукта.</span><span class="sxs-lookup"><span data-stu-id="54866-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="54866-112">В этом руководстве показано, как поддерживать эти операции в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="54866-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="54866-113">Руководство строится на руководстве по [созданию конечной точки OData v3 с веб-API 2](creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="54866-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="54866-114">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="54866-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="54866-115">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="54866-115">Web API 2</span></span>
> - <span data-ttu-id="54866-116">OData версии 3</span><span class="sxs-lookup"><span data-stu-id="54866-116">OData Version 3</span></span>
> - <span data-ttu-id="54866-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="54866-117">Entity Framework 6</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="54866-118">Добавление сущности поставщика</span><span class="sxs-lookup"><span data-stu-id="54866-118">Add a Supplier Entity</span></span>

<span data-ttu-id="54866-119">Сначала необходимо добавить новый тип сущности в наш веб-канал OData.</span><span class="sxs-lookup"><span data-stu-id="54866-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="54866-120">Мы добавим класс `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="54866-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="54866-121">Этот класс использует строку для ключа сущности.</span><span class="sxs-lookup"><span data-stu-id="54866-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="54866-122">На практике это может быть менее распространенным, чем использование целочисленного ключа.</span><span class="sxs-lookup"><span data-stu-id="54866-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="54866-123">Но стоит рассмотреть, как OData обрабатывает другие типы ключей помимо целых чисел.</span><span class="sxs-lookup"><span data-stu-id="54866-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="54866-124">Далее мы создадим отношение, добавив свойство `Supplier` к классу `Product`:</span><span class="sxs-lookup"><span data-stu-id="54866-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="54866-125">Добавьте новый **DbSet** в класс `ProductServiceContext`, чтобы Entity Framework включала в базу данных таблицу `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="54866-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="54866-126">В WebApiConfig.cs добавьте сущность «поставщики» в модель EDM:</span><span class="sxs-lookup"><span data-stu-id="54866-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="54866-127">Свойства навигации</span><span class="sxs-lookup"><span data-stu-id="54866-127">Navigation Properties</span></span>

<span data-ttu-id="54866-128">Чтобы получить поставщик для продукта, клиент отправляет запрос GET:</span><span class="sxs-lookup"><span data-stu-id="54866-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="54866-129">Здесь "поставщик" — это свойство навигации типа `Product`.</span><span class="sxs-lookup"><span data-stu-id="54866-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="54866-130">В этом случае `Supplier` ссылается на один элемент, но свойство навигации также может возвращать коллекцию (связь «один ко многим» или «многие ко многим»).</span><span class="sxs-lookup"><span data-stu-id="54866-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="54866-131">Для поддержки этого запроса добавьте в класс `ProductsController` следующий метод:</span><span class="sxs-lookup"><span data-stu-id="54866-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="54866-132">*Ключевым* параметром является ключ продукта.</span><span class="sxs-lookup"><span data-stu-id="54866-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="54866-133">Метод возвращает связанную сущность&#8212;в данном случае — экземпляр `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="54866-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="54866-134">Имя метода и имя параметра являются важными.</span><span class="sxs-lookup"><span data-stu-id="54866-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="54866-135">В общем случае, если свойство навигации имеет имя «X», необходимо добавить метод с именем «Жеткс».</span><span class="sxs-lookup"><span data-stu-id="54866-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="54866-136">Метод должен принимать параметр с именем*Key*, соответствующий типу данных родительского ключа.</span><span class="sxs-lookup"><span data-stu-id="54866-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="54866-137">Также важно включить атрибут **[фромодатаури]** в параметр *Key* .</span><span class="sxs-lookup"><span data-stu-id="54866-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="54866-138">Этот атрибут указывает, что веб-API будет использовать правила синтаксиса OData при анализе ключа из URI запроса.</span><span class="sxs-lookup"><span data-stu-id="54866-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="54866-139">Создание и удаление ссылок</span><span class="sxs-lookup"><span data-stu-id="54866-139">Creating and Deleting Links</span></span>

<span data-ttu-id="54866-140">OData поддерживает создание или удаление связей между двумя сущностями.</span><span class="sxs-lookup"><span data-stu-id="54866-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="54866-141">В терминологии OData связь является "связью".</span><span class="sxs-lookup"><span data-stu-id="54866-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="54866-142">Каждая ссылка имеет универсальный код ресурса (URI) с формой *Entity*/$Links или*Entity*.</span><span class="sxs-lookup"><span data-stu-id="54866-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="54866-143">Например, ссылка от Product к поставщику выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="54866-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="54866-144">Чтобы создать новую ссылку, клиент отправляет запрос POST в URI ссылки.</span><span class="sxs-lookup"><span data-stu-id="54866-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="54866-145">Тело запроса — это URI целевой сущности.</span><span class="sxs-lookup"><span data-stu-id="54866-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="54866-146">Например, предположим, что имеется поставщик с ключом «КТСО».</span><span class="sxs-lookup"><span data-stu-id="54866-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="54866-147">Чтобы создать ссылку с "Product (1)" на "поставщик (" КТСО ")", клиент отправляет запрос, подобный следующему:</span><span class="sxs-lookup"><span data-stu-id="54866-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="54866-148">Чтобы удалить ссылку, клиент отправляет запрос на удаление в URI ссылки.</span><span class="sxs-lookup"><span data-stu-id="54866-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="54866-149">**Создание ссылок**</span><span class="sxs-lookup"><span data-stu-id="54866-149">**Creating Links**</span></span>

<span data-ttu-id="54866-150">Чтобы разрешить клиенту создавать связи продуктов и поставщиков, добавьте следующий код в класс `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="54866-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="54866-151">Этот метод принимает три параметра:</span><span class="sxs-lookup"><span data-stu-id="54866-151">This method takes three parameters:</span></span>

- <span data-ttu-id="54866-152">*ключ*: ключ к родительской сущности (продукт).</span><span class="sxs-lookup"><span data-stu-id="54866-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="54866-153">*navigationProperty*: имя свойства навигации.</span><span class="sxs-lookup"><span data-stu-id="54866-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="54866-154">В этом примере единственным допустимым свойством навигации является «поставщик».</span><span class="sxs-lookup"><span data-stu-id="54866-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="54866-155">*ссылка*: URI OData связанной сущности.</span><span class="sxs-lookup"><span data-stu-id="54866-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="54866-156">Это значение берется из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="54866-156">This value is taken from the request body.</span></span> <span data-ttu-id="54866-157">Например, URI ссылки может быть "`http://localhost/odata/Suppliers('CTSO')`, то есть поставщик с ИДЕНТИФИКАТОРом" КТСО ".</span><span class="sxs-lookup"><span data-stu-id="54866-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="54866-158">Метод использует ссылку для поиска поставщика.</span><span class="sxs-lookup"><span data-stu-id="54866-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="54866-159">Если найден соответствующий поставщик, метод задает свойство `Product.Supplier` и сохраняет результат в базе данных.</span><span class="sxs-lookup"><span data-stu-id="54866-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="54866-160">Самая сложная часть — это анализ универсального кода ресурса (URI) ссылки.</span><span class="sxs-lookup"><span data-stu-id="54866-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="54866-161">По сути, необходимо имитировать результат отправки запроса GET на этот универсальный код ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="54866-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="54866-162">В следующем вспомогательном методе показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="54866-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="54866-163">Метод вызывает процесс маршрутизации веб-API и возвращает экземпляр **ODataPath** , представляющий проанализированный путь OData.</span><span class="sxs-lookup"><span data-stu-id="54866-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="54866-164">Для URI ссылки один из сегментов должен быть ключом сущности.</span><span class="sxs-lookup"><span data-stu-id="54866-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="54866-165">(Если нет, клиент отправил некорректный URI.)</span><span class="sxs-lookup"><span data-stu-id="54866-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="54866-166">**Удаление ссылок**</span><span class="sxs-lookup"><span data-stu-id="54866-166">**Deleting Links**</span></span>

<span data-ttu-id="54866-167">Чтобы удалить ссылку, добавьте следующий код в класс `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="54866-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="54866-168">В этом примере свойство навигации является одной сущностью `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="54866-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="54866-169">Если свойство навигации является коллекцией, URI для удаления ссылки должен включать ключ для связанной сущности.</span><span class="sxs-lookup"><span data-stu-id="54866-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="54866-170">Пример:</span><span class="sxs-lookup"><span data-stu-id="54866-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="54866-171">Этот запрос удаляет заказ 1 из клиента 1.</span><span class="sxs-lookup"><span data-stu-id="54866-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="54866-172">В этом случае метод Делетелинк будет иметь следующую сигнатуру:</span><span class="sxs-lookup"><span data-stu-id="54866-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="54866-173">Параметр *релатедкэй* предоставляет ключ для связанной сущности.</span><span class="sxs-lookup"><span data-stu-id="54866-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="54866-174">Поэтому в методе `DeleteLink` найдите основную сущность по *ключевому* параметру, найдите связанную сущность с помощью параметра *релатедкэй* , а затем удалите связь.</span><span class="sxs-lookup"><span data-stu-id="54866-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="54866-175">В зависимости от модели данных может потребоваться реализовать обе версии `DeleteLink`.</span><span class="sxs-lookup"><span data-stu-id="54866-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="54866-176">Веб-API будет вызывать правильную версию на основе URI запроса.</span><span class="sxs-lookup"><span data-stu-id="54866-176">Web API will call the correct version based on the request URI.</span></span>
