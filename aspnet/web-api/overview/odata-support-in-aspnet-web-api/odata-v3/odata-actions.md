---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: Поддержка действий OData в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: 'В OData действия — это способ добавления поведений на стороне сервера, которые не просто определяются как операции CRUD с сущностями. К некоторым действиям относятся: реализация...'
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448176"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="90424-104">Поддержка действий OData в веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="90424-104">Supporting OData Actions in ASP.NET Web API 2</span></span>

<span data-ttu-id="90424-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="90424-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="90424-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="90424-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="90424-107">В OData *действия* — это способ добавления поведений на стороне сервера, которые не просто определяются как операции CRUD с сущностями.</span><span class="sxs-lookup"><span data-stu-id="90424-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="90424-108">Ниже перечислены некоторые способы использования действий.</span><span class="sxs-lookup"><span data-stu-id="90424-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="90424-109">Реализация сложных транзакций.</span><span class="sxs-lookup"><span data-stu-id="90424-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="90424-110">Одновременное управление несколькими сущностями.</span><span class="sxs-lookup"><span data-stu-id="90424-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="90424-111">Разрешение обновления только для определенных свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="90424-112">Отправка данных на сервер, не определенный в сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="90424-113">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="90424-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="90424-114">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="90424-114">Web API 2</span></span>
> - <span data-ttu-id="90424-115">OData версии 3</span><span class="sxs-lookup"><span data-stu-id="90424-115">OData Version 3</span></span>
> - <span data-ttu-id="90424-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="90424-116">Entity Framework 6</span></span>

## <a name="example-rating-a-product"></a><span data-ttu-id="90424-117">Пример: Оценка продукта</span><span class="sxs-lookup"><span data-stu-id="90424-117">Example: Rating a Product</span></span>

<span data-ttu-id="90424-118">В этом примере мы хотим разрешить пользователям оценивать продукты, а затем предоставлять среднюю оценку для каждого продукта.</span><span class="sxs-lookup"><span data-stu-id="90424-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="90424-119">В базе данных будет сохранен список оценок с ключом Products.</span><span class="sxs-lookup"><span data-stu-id="90424-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="90424-120">Ниже приведена модель, которую можно использовать для представления оценок в Entity Framework:</span><span class="sxs-lookup"><span data-stu-id="90424-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="90424-121">Но мы не хотим, чтобы клиенты пере`ProductRating` объект в коллекцию "оценки".</span><span class="sxs-lookup"><span data-stu-id="90424-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="90424-122">Интуитивно, оценка связана с коллекцией Products, и клиенту нужно только опубликовать значение рейтинга.</span><span class="sxs-lookup"><span data-stu-id="90424-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="90424-123">Таким образом, вместо обычных операций CRUD мы определим действие, которое клиент может вызывать для продукта.</span><span class="sxs-lookup"><span data-stu-id="90424-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="90424-124">В терминологии OData действие *привязано* к сущностям Product.</span><span class="sxs-lookup"><span data-stu-id="90424-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="90424-125">Действия имеют побочные эффекты на сервере.</span><span class="sxs-lookup"><span data-stu-id="90424-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="90424-126">По этой причине они вызываются с помощью HTTP-запросов POST.</span><span class="sxs-lookup"><span data-stu-id="90424-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="90424-127">Действия могут иметь параметры и возвращаемые типы, которые описаны в метаданных службы.</span><span class="sxs-lookup"><span data-stu-id="90424-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="90424-128">Клиент отправляет параметры в тексте запроса, а сервер отправляет возвращаемое значение в тексте ответа.</span><span class="sxs-lookup"><span data-stu-id="90424-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="90424-129">Чтобы вызвать действие "оценить продукт", клиент отправляет POST в URI, как в следующем:</span><span class="sxs-lookup"><span data-stu-id="90424-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="90424-130">Данные в запросе POST — это просто Оценка продукта:</span><span class="sxs-lookup"><span data-stu-id="90424-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="90424-131">Объявите действие в EDM</span><span class="sxs-lookup"><span data-stu-id="90424-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="90424-132">В конфигурации веб-API добавьте действие в модель EDM:</span><span class="sxs-lookup"><span data-stu-id="90424-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="90424-133">Этот код определяет "Ратепродукт" как действие, которое может быть выполнено с сущностями продукта.</span><span class="sxs-lookup"><span data-stu-id="90424-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="90424-134">Он также объявляет, что действие принимает параметр **int** с именем "Оценка" и **возвращает целочисленное значение.**</span><span class="sxs-lookup"><span data-stu-id="90424-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="90424-135">Добавление действия в контроллер</span><span class="sxs-lookup"><span data-stu-id="90424-135">Add the Action to the Controller</span></span>

<span data-ttu-id="90424-136">Действие "Ратепродукт" привязано к сущностям продукта.</span><span class="sxs-lookup"><span data-stu-id="90424-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="90424-137">Чтобы реализовать действие, добавьте метод с именем `RateProduct` в контроллер Products:</span><span class="sxs-lookup"><span data-stu-id="90424-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="90424-138">Обратите внимание, что имя метода совпадает с именем действия в модели EDM.</span><span class="sxs-lookup"><span data-stu-id="90424-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="90424-139">Метод имеет два параметра:</span><span class="sxs-lookup"><span data-stu-id="90424-139">The method has two parameters:</span></span>

- <span data-ttu-id="90424-140">*ключ*: ключ продукта для ставки.</span><span class="sxs-lookup"><span data-stu-id="90424-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="90424-141">*Parameters*— словарь значений параметров действия.</span><span class="sxs-lookup"><span data-stu-id="90424-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="90424-142">Если используются соглашения о маршрутизации по умолчанию, параметр key должен иметь имя Key.</span><span class="sxs-lookup"><span data-stu-id="90424-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="90424-143">Также важно включить атрибут **[фромодатаури]** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="90424-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="90424-144">Этот атрибут указывает, что веб-API будет использовать правила синтаксиса OData при анализе ключа из URI запроса.</span><span class="sxs-lookup"><span data-stu-id="90424-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="90424-145">Чтобы получить параметры действия, используйте словарь *параметров* :</span><span class="sxs-lookup"><span data-stu-id="90424-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="90424-146">Если клиент отправляет параметры действия в правильном формате, значение **ModelState. IsValid** равно true.</span><span class="sxs-lookup"><span data-stu-id="90424-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="90424-147">В этом случае можно использовать словарь **одатаактионпараметерс** для получения значений параметров.</span><span class="sxs-lookup"><span data-stu-id="90424-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="90424-148">В этом примере действие `RateProduct` принимает один параметр с именем "Оценка".</span><span class="sxs-lookup"><span data-stu-id="90424-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="90424-149">Метаданные действия</span><span class="sxs-lookup"><span data-stu-id="90424-149">Action Metadata</span></span>

<span data-ttu-id="90424-150">Чтобы просмотреть метаданные службы, отправьте запрос GET в/одата/$metadata.</span><span class="sxs-lookup"><span data-stu-id="90424-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="90424-151">Ниже приведена часть метаданных, объявляющая действие `RateProduct`:</span><span class="sxs-lookup"><span data-stu-id="90424-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="90424-152">Элемент **FunctionImport** объявляет действие.</span><span class="sxs-lookup"><span data-stu-id="90424-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="90424-153">Большинство полей говорят сами за себя, но два стоит отметить:</span><span class="sxs-lookup"><span data-stu-id="90424-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="90424-154">**Подшивка** означает, что действие может быть вызвано в целевой сущности, по крайней мере в некоторый момент времени.</span><span class="sxs-lookup"><span data-stu-id="90424-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="90424-155">**IsAlwaysBindable** означает, что действие всегда может вызываться в целевой сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="90424-156">Разница заключается в том, что некоторые действия всегда доступны клиентам, но другие действия могут зависеть от состояния сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="90424-157">Например, предположим, что вы определили действие "Покупка".</span><span class="sxs-lookup"><span data-stu-id="90424-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="90424-158">Вы можете приобрести только тот товар, который находится на бирже.</span><span class="sxs-lookup"><span data-stu-id="90424-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="90424-159">Если товар находится за пределами склада, клиент не может вызвать это действие.</span><span class="sxs-lookup"><span data-stu-id="90424-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="90424-160">При определении модели EDM метод **действия** создает действие Always-BIND:</span><span class="sxs-lookup"><span data-stu-id="90424-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="90424-161">Далее в этом разделе я расскажу о действиях, которые не всегда являются связываемыми (также называются *временными* действиями).</span><span class="sxs-lookup"><span data-stu-id="90424-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="90424-162">Вызов действия</span><span class="sxs-lookup"><span data-stu-id="90424-162">Invoking the Action</span></span>

<span data-ttu-id="90424-163">Теперь давайте посмотрим, как клиент вызовет это действие.</span><span class="sxs-lookup"><span data-stu-id="90424-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="90424-164">Предположим, клиент хочет получить оценку 2 для продукта с ИД = 4.</span><span class="sxs-lookup"><span data-stu-id="90424-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="90424-165">Ниже приведен пример сообщения запроса с использованием формата JSON для текста запроса:</span><span class="sxs-lookup"><span data-stu-id="90424-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="90424-166">Ответное сообщение:</span><span class="sxs-lookup"><span data-stu-id="90424-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="90424-167">Привязка действия к набору сущностей</span><span class="sxs-lookup"><span data-stu-id="90424-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="90424-168">В предыдущем примере действие привязано к одной сущности: Клиент оценивает один продукт.</span><span class="sxs-lookup"><span data-stu-id="90424-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="90424-169">Можно также привязать действие к коллекции сущностей.</span><span class="sxs-lookup"><span data-stu-id="90424-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="90424-170">Просто внесите следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="90424-170">Just make the following changes:</span></span>

<span data-ttu-id="90424-171">В EDM добавьте действие в свойство **коллекции** сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="90424-172">В методе контроллера опустите параметр *Key* .</span><span class="sxs-lookup"><span data-stu-id="90424-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="90424-173">Теперь клиент вызывает действие для набора сущностей Products:</span><span class="sxs-lookup"><span data-stu-id="90424-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="90424-174">Действия с параметрами коллекции</span><span class="sxs-lookup"><span data-stu-id="90424-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="90424-175">Действия могут иметь параметры, которые принимают коллекцию значений.</span><span class="sxs-lookup"><span data-stu-id="90424-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="90424-176">В модели EDM для объявления параметра используйте **коллектионпараметер&lt;t&gt;** .</span><span class="sxs-lookup"><span data-stu-id="90424-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="90424-177">Он объявляет параметр с именем "оценки", который принимает коллекцию значений **типа int** .</span><span class="sxs-lookup"><span data-stu-id="90424-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="90424-178">В методе контроллера вы по-прежнему получаете значение параметра из объекта **одатаактионпараметерс** , но теперь значением является **ICollection&lt;int&gt;** значение:</span><span class="sxs-lookup"><span data-stu-id="90424-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="90424-179">Временные действия</span><span class="sxs-lookup"><span data-stu-id="90424-179">Transient Actions</span></span>

<span data-ttu-id="90424-180">В примере "Ратепродукт" пользователи всегда могут оценивать продукт, поэтому действие всегда доступно.</span><span class="sxs-lookup"><span data-stu-id="90424-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="90424-181">Но некоторые действия зависят от состояния сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="90424-182">Например, в службе аренды видео действие "извлечение" не всегда доступно.</span><span class="sxs-lookup"><span data-stu-id="90424-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="90424-183">(Это зависит от того, доступна ли копия этого видео.) Этот тип действия называется *временным* действием.</span><span class="sxs-lookup"><span data-stu-id="90424-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="90424-184">В метаданных службы временное действие имеет значение **IsAlwaysBindable** , равное false.</span><span class="sxs-lookup"><span data-stu-id="90424-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="90424-185">Это действительно значение по умолчанию, поэтому метаданные будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="90424-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="90424-186">Вот почему это важно: Если действие является временным, сервер должен сообщить клиенту, когда действие будет доступно.</span><span class="sxs-lookup"><span data-stu-id="90424-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="90424-187">Это достигается путем включения ссылки на действие в сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="90424-188">Ниже приведен пример для сущности Movie:</span><span class="sxs-lookup"><span data-stu-id="90424-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="90424-189">Свойство "#CheckOut" содержит ссылку на действие извлечения.</span><span class="sxs-lookup"><span data-stu-id="90424-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="90424-190">Если действие недоступно, сервер опускает ссылку.</span><span class="sxs-lookup"><span data-stu-id="90424-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="90424-191">Чтобы объявить временное действие в модели EDM, вызовите метод **трансиентактион** :</span><span class="sxs-lookup"><span data-stu-id="90424-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="90424-192">Кроме того, необходимо предоставить функцию, которая возвращает ссылку на действие для данной сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="90424-193">Установите эту функцию, вызвав **хасактионлинк**.</span><span class="sxs-lookup"><span data-stu-id="90424-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="90424-194">Функцию можно написать в виде лямбда-выражения:</span><span class="sxs-lookup"><span data-stu-id="90424-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="90424-195">Если действие доступно, лямбда-выражение возвращает ссылку на действие.</span><span class="sxs-lookup"><span data-stu-id="90424-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="90424-196">Сериализатор OData включает эту ссылку при сериализации сущности.</span><span class="sxs-lookup"><span data-stu-id="90424-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="90424-197">Если действие недоступно, функция возвращает `null`.</span><span class="sxs-lookup"><span data-stu-id="90424-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90424-198">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="90424-198">Additional Resources</span></span>

[<span data-ttu-id="90424-199">Пример действий OData</span><span class="sxs-lookup"><span data-stu-id="90424-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
