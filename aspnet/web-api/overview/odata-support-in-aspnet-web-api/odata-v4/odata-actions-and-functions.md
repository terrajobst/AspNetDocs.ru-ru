---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: Действия и функции в OData v4 с использованием веб-API ASP.NET 2,2 | Документация Майкрософт
author: MikeWasson
description: В OData действия и функции позволяют добавлять поведений на стороне сервера, которые не просто определяются как операции CRUD для сущностей. В этом руководстве показано, как...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448062"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="70553-104">Действия и функции в OData v4 с использованием веб-API ASP.NET 2,2</span><span class="sxs-lookup"><span data-stu-id="70553-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="70553-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="70553-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="70553-106">В OData действия и функции позволяют добавлять поведений на стороне сервера, которые не просто определяются как операции CRUD для сущностей.</span><span class="sxs-lookup"><span data-stu-id="70553-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="70553-107">В этом руководстве показано, как добавлять действия и функции в конечную точку OData v4 с помощью веб-API 2,2.</span><span class="sxs-lookup"><span data-stu-id="70553-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="70553-108">Руководство по построению в учебнике [Создание конечной точки OData v4 с помощью веб-API ASP.NET 2](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="70553-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="70553-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="70553-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="70553-110">Веб-API 2,2</span><span class="sxs-lookup"><span data-stu-id="70553-110">Web API 2.2</span></span>
> - <span data-ttu-id="70553-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="70553-111">OData v4</span></span>
> - <span data-ttu-id="70553-112">Visual Studio 2013 (Скачайте Visual Studio 2017 [здесь](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="70553-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="70553-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="70553-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="70553-114">Учебные версии</span><span class="sxs-lookup"><span data-stu-id="70553-114">Tutorial versions</span></span>
>
> <span data-ttu-id="70553-115">Сведения для OData версии 3 см. [в разделе действия OData в веб-API ASP.NET 2](../odata-v3/odata-actions.md).</span><span class="sxs-lookup"><span data-stu-id="70553-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="70553-116">Различие между *действиями* и *функциями* заключается в том, что действия могут иметь побочные эффекты, а функции — нет.</span><span class="sxs-lookup"><span data-stu-id="70553-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="70553-117">Действия и функции могут возвращать данные.</span><span class="sxs-lookup"><span data-stu-id="70553-117">Both actions and functions can return data.</span></span> <span data-ttu-id="70553-118">Ниже перечислены некоторые способы использования действий.</span><span class="sxs-lookup"><span data-stu-id="70553-118">Some uses for actions include:</span></span>

- <span data-ttu-id="70553-119">Сложные транзакции.</span><span class="sxs-lookup"><span data-stu-id="70553-119">Complex transactions.</span></span>
- <span data-ttu-id="70553-120">Одновременное управление несколькими сущностями.</span><span class="sxs-lookup"><span data-stu-id="70553-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="70553-121">Разрешение обновления только для определенных свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="70553-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="70553-122">Отправка данных, которые не являются сущностями.</span><span class="sxs-lookup"><span data-stu-id="70553-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="70553-123">Функции полезны для возврата сведений, которые не соответствуют непосредственно сущности или коллекции.</span><span class="sxs-lookup"><span data-stu-id="70553-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="70553-124">Действие (или функция) может ориентироваться на одну сущность или коллекцию.</span><span class="sxs-lookup"><span data-stu-id="70553-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="70553-125">В терминологии OData это *Привязка*.</span><span class="sxs-lookup"><span data-stu-id="70553-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="70553-126">Можно также иметь &quot;непривязанные&quot; действия или функции, которые вызываются как статические операции в службе.</span><span class="sxs-lookup"><span data-stu-id="70553-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="70553-127">Пример. Добавление действия</span><span class="sxs-lookup"><span data-stu-id="70553-127">Example: Adding an Action</span></span>

<span data-ttu-id="70553-128">Давайте определим действие для расчета частоты продукта.</span><span class="sxs-lookup"><span data-stu-id="70553-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="70553-129">В этом руководстве описано, [как создать конечную точку OData v4 с помощью веб-API ASP.NET 2](create-an-odata-v4-endpoint.md) .</span><span class="sxs-lookup"><span data-stu-id="70553-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="70553-130">Сначала добавьте модель `ProductRating` для представления оценок.</span><span class="sxs-lookup"><span data-stu-id="70553-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="70553-131">Также добавьте **DbSet** в класс `ProductsContext`, чтобы EF создаст таблицу оценок в базе данных.</span><span class="sxs-lookup"><span data-stu-id="70553-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="70553-132">Добавление действия в модель EDM</span><span class="sxs-lookup"><span data-stu-id="70553-132">Add the Action to the EDM</span></span>

<span data-ttu-id="70553-133">В WebApiConfig.cs добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="70553-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="70553-134">Метод **ентититипеконфигуратион. Action** добавляет действие в модель EDM.</span><span class="sxs-lookup"><span data-stu-id="70553-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="70553-135">Метод **Parameter** задает типизированный параметр для действия.</span><span class="sxs-lookup"><span data-stu-id="70553-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="70553-136">Этот код также задает пространство имен для модели EDM.</span><span class="sxs-lookup"><span data-stu-id="70553-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="70553-137">Пространство имен имеет значение, так как универсальный код ресурса (URI) действия включает полное имя действия:</span><span class="sxs-lookup"><span data-stu-id="70553-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="70553-138">В типичной конфигурации IIS точка в этом URL-адресе приведет к возврату ошибки 404.</span><span class="sxs-lookup"><span data-stu-id="70553-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="70553-139">Это можно разрешить, добавив следующий раздел в файл Web. config:</span><span class="sxs-lookup"><span data-stu-id="70553-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="70553-140">Добавление метода контроллера для действия</span><span class="sxs-lookup"><span data-stu-id="70553-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="70553-141">Чтобы включить&quot; &quot;Rate, добавьте следующий метод для `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="70553-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="70553-142">Обратите внимание, что имя метода совпадает с именем действия.</span><span class="sxs-lookup"><span data-stu-id="70553-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="70553-143">Атрибут **[HttpPost]** указывает, что метод является методом HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="70553-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="70553-144">Чтобы вызвать действие, клиент отправляет запрос HTTP POST, подобный следующему:</span><span class="sxs-lookup"><span data-stu-id="70553-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="70553-145">Действие&quot; Rate &quot;привязано к экземплярам продукта, поэтому универсальный код ресурса (URI) для действия — это полное имя действия, добавляемое к универсальному коду ресурса (URI) сущности.</span><span class="sxs-lookup"><span data-stu-id="70553-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="70553-146">(Помните, что мы устанавливаем пространство имен EDM &quot;Продуктсервице&quot;, поэтому полное имя действия — &quot;Продуктсервице. rate&quot;.)</span><span class="sxs-lookup"><span data-stu-id="70553-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="70553-147">Текст запроса содержит параметры действия в виде полезных данных JSON.</span><span class="sxs-lookup"><span data-stu-id="70553-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="70553-148">Веб-API автоматически преобразует полезные данные JSON в объект **одатаактионпараметерс** , который представляет собой просто словарь значений параметров.</span><span class="sxs-lookup"><span data-stu-id="70553-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="70553-149">Используйте этот словарь для доступа к параметрам в методе контроллера.</span><span class="sxs-lookup"><span data-stu-id="70553-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="70553-150">Если клиент отправляет параметры действия в неправильном формате, значение **ModelState. IsValid** равно false.</span><span class="sxs-lookup"><span data-stu-id="70553-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="70553-151">Установите этот флаг в метод контроллера и верните ошибку, если параметр **IsValid** имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="70553-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="70553-152">Пример. Добавление функции</span><span class="sxs-lookup"><span data-stu-id="70553-152">Example: Adding a Function</span></span>

<span data-ttu-id="70553-153">Теперь добавим функцию OData, которая возвращает самый ресурсоемкий продукт.</span><span class="sxs-lookup"><span data-stu-id="70553-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="70553-154">Как и раньше, первым шагом является добавление функции в EDM.</span><span class="sxs-lookup"><span data-stu-id="70553-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="70553-155">В WebApiConfig.cs добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="70553-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="70553-156">В этом случае функция привязана к коллекции Products, а не к отдельным экземплярам продукта.</span><span class="sxs-lookup"><span data-stu-id="70553-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="70553-157">Клиенты вызывают функцию, отправив запрос GET:</span><span class="sxs-lookup"><span data-stu-id="70553-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="70553-158">Ниже приведен метод контроллера для этой функции.</span><span class="sxs-lookup"><span data-stu-id="70553-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="70553-159">Обратите внимание, что имя метода совпадает с именем функции.</span><span class="sxs-lookup"><span data-stu-id="70553-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="70553-160">Атрибут **[HttpGet]** указывает, что метод является методом HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="70553-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="70553-161">Ответ HTTP:</span><span class="sxs-lookup"><span data-stu-id="70553-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="70553-162">Пример. Добавление непривязанной функции</span><span class="sxs-lookup"><span data-stu-id="70553-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="70553-163">Предыдущий пример — функция, привязанная к коллекции.</span><span class="sxs-lookup"><span data-stu-id="70553-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="70553-164">В следующем примере мы создадим *несвязанную* функцию.</span><span class="sxs-lookup"><span data-stu-id="70553-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="70553-165">Несвязанные функции вызываются как статические операции со службой.</span><span class="sxs-lookup"><span data-stu-id="70553-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="70553-166">Функция в этом примере будет возвращать налог на продажу для данного почтового индекса.</span><span class="sxs-lookup"><span data-stu-id="70553-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="70553-167">В файле WebApiConfig добавьте функцию в модель EDM:</span><span class="sxs-lookup"><span data-stu-id="70553-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="70553-168">Обратите внимание, что **функция** вызывается непосредственно в **одатамоделбуилдер**, а не в типе сущности или коллекции.</span><span class="sxs-lookup"><span data-stu-id="70553-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="70553-169">Это указывает построителю моделей, что функция не привязана.</span><span class="sxs-lookup"><span data-stu-id="70553-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="70553-170">Ниже приведен метод контроллера, реализующий функцию:</span><span class="sxs-lookup"><span data-stu-id="70553-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="70553-171">Не имеет значения, какой контроллер веб-API будет размещен в.</span><span class="sxs-lookup"><span data-stu-id="70553-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="70553-172">Его можно разместить в `ProductsController`или определить отдельный контроллер.</span><span class="sxs-lookup"><span data-stu-id="70553-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="70553-173">Атрибут **[одатарауте]** определяет шаблон URI для функции.</span><span class="sxs-lookup"><span data-stu-id="70553-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="70553-174">Вот пример запроса клиента:</span><span class="sxs-lookup"><span data-stu-id="70553-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="70553-175">HTTP-ответ:</span><span class="sxs-lookup"><span data-stu-id="70553-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
