---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: Выбор маршрутизации и действий в веб-API ASP.NET | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446916"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="a5f3e-102">Выбор маршрутизации и действий в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a5f3e-102">Routing and Action Selection in ASP.NET Web API</span></span>

<span data-ttu-id="a5f3e-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a5f3e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a5f3e-104">В этой статье описывается, как веб-API ASP.NET направляет HTTP-запрос к определенному действию на контроллере.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="a5f3e-105">Общий обзор маршрутизации см. [в разделе Маршрутизация в веб-API ASP.NET](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="a5f3e-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="a5f3e-106">В этой статье рассматриваются сведения о процессе маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="a5f3e-107">Если вы создадите проект веб-API и обнаружите, что некоторые запросы не направляются должным образом, надеюсь, эта статья поможет вам.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="a5f3e-108">Маршрутизация включает три основных этапа:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="a5f3e-109">Сопоставление URI с шаблоном маршрута.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="a5f3e-110">Выбор контроллера.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-110">Selecting a controller.</span></span>
3. <span data-ttu-id="a5f3e-111">Выбор действия.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-111">Selecting an action.</span></span>

<span data-ttu-id="a5f3e-112">Некоторые части процесса можно заменить собственными пользовательским поведением.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="a5f3e-113">В этой статье я опишу поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="a5f3e-114">В конце я занимаю места, где можно настроить поведение.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="a5f3e-115">Шаблоны маршрутов</span><span class="sxs-lookup"><span data-stu-id="a5f3e-115">Route Templates</span></span>

<span data-ttu-id="a5f3e-116">Шаблон маршрута похож на путь URI, но может содержать значения заполнителей, обозначенные фигурными скобками:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="a5f3e-117">При создании маршрута можно указать значения по умолчанию для некоторых или всех заполнителей:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="a5f3e-118">Можно также предоставить ограничения, ограничивающие соответствие сегмента URI заполнительу.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="a5f3e-119">Платформа пытается сопоставить сегменты в пути URI с шаблоном.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="a5f3e-120">Литералы в шаблоне должны точно совпадать.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="a5f3e-121">Заполнитель соответствует любому значению, если только не указаны ограничения.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="a5f3e-122">Платформа не соответствует другим частям URI, таким как имя узла или параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="a5f3e-123">Платформа выбирает первый маршрут в таблице маршрутов, соответствующий универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="a5f3e-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="a5f3e-124">Есть два специальных заполнителя: "{Controller}" и "{Action}".</span><span class="sxs-lookup"><span data-stu-id="a5f3e-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="a5f3e-125">"{Controller}" — имя контроллера.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="a5f3e-126">"{Action}" предоставляет имя действия.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="a5f3e-127">В веб-API обычным соглашением является пропуск "{Action}".</span><span class="sxs-lookup"><span data-stu-id="a5f3e-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="a5f3e-128">Умолчания;</span><span class="sxs-lookup"><span data-stu-id="a5f3e-128">Defaults</span></span>

<span data-ttu-id="a5f3e-129">Если указать значения по умолчанию, маршрут будет соответствовать URI, в котором отсутствуют эти сегменты.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="a5f3e-130">Пример:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="a5f3e-131">URI `http://localhost/api/products/all` и `http://localhost/api/products` соответствуют предыдущему маршруту.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="a5f3e-132">В последнем URI отсутствует сегмент `{category}` присваивается значение по умолчанию `all`.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="a5f3e-133">Словарь маршрутов</span><span class="sxs-lookup"><span data-stu-id="a5f3e-133">Route Dictionary</span></span>

<span data-ttu-id="a5f3e-134">Если платформа находит совпадение для URI, создается словарь, содержащий значение для каждого заполнителя.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="a5f3e-135">Ключи — это имена заполнителей, не включая фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="a5f3e-136">Значения берутся из пути URI или из значений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="a5f3e-137">Словарь хранится в объекте **ихттпраутедата** .</span><span class="sxs-lookup"><span data-stu-id="a5f3e-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="a5f3e-138">Во время этой фазы сопоставления маршрутов специальные заполнители "{Controller}" и "{Action}" обрабатываются точно так же, как и другие заполнители.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="a5f3e-139">Они просто хранятся в словаре с другими значениями.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="a5f3e-140">Значение по умолчанию может быть специальным значением **раутепараметер. Optional**.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="a5f3e-141">Если заполнитель назначает это значение, это значение не добавляется в словарь маршрутов.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="a5f3e-142">Пример:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="a5f3e-143">Для пути URI "API/Products" словарь маршрутов будет содержать:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="a5f3e-144">Controller: "Products"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-144">controller: "products"</span></span>
- <span data-ttu-id="a5f3e-145">Категория: "все"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-145">category: "all"</span></span>

<span data-ttu-id="a5f3e-146">Однако для «API/Products/Toys/123» словарь маршрутов будет содержать:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="a5f3e-147">Controller: "Products"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-147">controller: "products"</span></span>
- <span data-ttu-id="a5f3e-148">Категория: "Toys"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-148">category: "toys"</span></span>
- <span data-ttu-id="a5f3e-149">Идентификатор: "123"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-149">id: "123"</span></span>

<span data-ttu-id="a5f3e-150">Значения по умолчанию также могут включать значение, которое не отображается в любом месте шаблона маршрута.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="a5f3e-151">Если маршрут совпадает, это значение сохраняется в словаре.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="a5f3e-152">Пример:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="a5f3e-153">Если путь URI имеет значение "API/root/8", словарь будет содержать два значения:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="a5f3e-154">контроллер: "клиенты"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-154">controller: "customers"</span></span>
- <span data-ttu-id="a5f3e-155">Идентификатор: "8"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="a5f3e-156">Выбор контроллера</span><span class="sxs-lookup"><span data-stu-id="a5f3e-156">Selecting a Controller</span></span>

<span data-ttu-id="a5f3e-157">Выбор контроллера обрабатывается методом **ихттпконтроллерселектор. селектконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="a5f3e-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="a5f3e-158">Этот метод принимает экземпляр **HttpRequestMessage** и возвращает **хттпконтроллердескриптор**.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="a5f3e-159">Реализация по умолчанию предоставляется классом **дефаулсттпконтроллерселектор** .</span><span class="sxs-lookup"><span data-stu-id="a5f3e-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="a5f3e-160">Этот класс использует простой алгоритм:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="a5f3e-161">Просмотрите словарь маршрутов для ключа "контроллер".</span><span class="sxs-lookup"><span data-stu-id="a5f3e-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="a5f3e-162">Примите значение для этого ключа и добавьте строку "Controller", чтобы получить имя типа контроллера.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="a5f3e-163">Найдите контроллер веб-API с этим именем типа.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="a5f3e-164">Например, если словарь маршрутов содержит пару "ключ-значение" "Controller" = "Products", то тип контроллера — "Продуктсконтроллер".</span><span class="sxs-lookup"><span data-stu-id="a5f3e-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="a5f3e-165">При отсутствии соответствующего типа или нескольких совпадений платформа возвращает клиенту ошибку.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="a5f3e-166">В шаге 3 **дефаулсттпконтроллерселектор** использует интерфейс **ихттпконтроллертипересолвер** для получения списка типов контроллеров веб-API.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="a5f3e-167">Реализация **ихттпконтроллертипересолвер** по умолчанию возвращает все открытые классы, которые (a) реализуют **ихттпконтроллер**, (b) не являются абстрактными, а (c) имеют имя, заканчивающееся на "Controller".</span><span class="sxs-lookup"><span data-stu-id="a5f3e-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="a5f3e-168">Выбор действия</span><span class="sxs-lookup"><span data-stu-id="a5f3e-168">Action Selection</span></span>

<span data-ttu-id="a5f3e-169">После выбора контроллера платформа выбирает действие, вызывая метод **ихттпактионселектор. селектактион** .</span><span class="sxs-lookup"><span data-stu-id="a5f3e-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="a5f3e-170">Этот метод принимает **HttpControllerContext** и возвращает **хттпактиондескриптор**.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="a5f3e-171">Реализация по умолчанию предоставляется классом **апиконтроллерактионселектор** .</span><span class="sxs-lookup"><span data-stu-id="a5f3e-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="a5f3e-172">Чтобы выбрать действие, оно будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="a5f3e-173">Метод HTTP, используемый для запроса.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="a5f3e-174">Заполнитель "{Action}" в шаблоне маршрута, если он есть.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="a5f3e-175">Параметры действий на контроллере.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="a5f3e-176">Прежде чем взглянуть на алгоритм выбора, необходимо понять некоторые моменты, связанные с действиями контроллера.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="a5f3e-177">**Какие методы в контроллере считаются "действиями"?**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="a5f3e-178">При выборе действия платформа проверяет только открытые методы экземпляра на контроллере.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="a5f3e-179">Кроме того, в нем исключены методы ["специального имени"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) (конструкторы, события, перегрузки операторов и т. д.) и методы, унаследованные от класса **ApiController** .</span><span class="sxs-lookup"><span data-stu-id="a5f3e-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="a5f3e-180">**Методы HTTP.**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-180">**HTTP Methods.**</span></span> <span data-ttu-id="a5f3e-181">Платформа выбирает только те действия, которые соответствуют HTTP-методу запроса, определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="a5f3e-182">Метод HTTP можно указать с помощью атрибута: **акцептвербс**, **хттпделете**, **HttpGet**, **хттфеад**, **хттпоптионс**, **хттппатч**, **HttpPost**или **хттппут**.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="a5f3e-183">В противном случае, если имя метода контроллера начинается с «Get», «POST», «WHERE», «DELETE», «Head», «Options» или «patch», то по соглашению действие поддерживает этот метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="a5f3e-184">Если ни один из вышеперечисленных методов не указан, метод поддерживает POST.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="a5f3e-185">**Привязки параметров.**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-185">**Parameter Bindings.**</span></span> <span data-ttu-id="a5f3e-186">Привязка параметра — это то, как веб-API создает значение для параметра.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="a5f3e-187">Ниже приведено правило по умолчанию для привязки параметров.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="a5f3e-188">Простые типы берутся из универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="a5f3e-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="a5f3e-189">Сложные типы берутся из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="a5f3e-190">Простые типы включают все [.NET Framework примитивные типы](https://msdn.microsoft.com/library/system.type.isprimitive), а также **DateTime**, **Decimal**, **GUID**, **String**и **TimeSpan**.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="a5f3e-191">Для каждого действия не более одного параметра может считывать текст запроса.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="a5f3e-192">Можно переопределить правила привязки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="a5f3e-193">См. раздел [Привязка параметра WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5f3e-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>

<span data-ttu-id="a5f3e-194">В этом примере используется алгоритм выбора действий.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="a5f3e-195">Создайте список всех действий на контроллере, которые соответствуют методу HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="a5f3e-196">Если словарь маршрутов содержит запись Action, удалите действия, имя которых не соответствует этому значению.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="a5f3e-197">Попробуйте сопоставить параметры действия с URI следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="a5f3e-198">Для каждого действия получите список параметров, которые являются простым типом, где привязка получает параметр из универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="a5f3e-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="a5f3e-199">Исключите необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="a5f3e-200">В этом списке попытайтесь найти совпадение для каждого имени параметра либо в словаре маршрутов, либо в строке запроса URI.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="a5f3e-201">Совпадения не учитывают регистр и не зависят от порядка параметров.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="a5f3e-202">Выберите действие, в котором каждый параметр в списке имеет совпадение в URI.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="a5f3e-203">Если одно действие соответствует этим критериям, выберите его с наибольшим совпадением параметров.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="a5f3e-204">Пропускать действия с атрибутом **[unaction]** .</span><span class="sxs-lookup"><span data-stu-id="a5f3e-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="a5f3e-205">Действие #3, вероятно, является самым запутанным.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="a5f3e-206">Основная идея состоит в том, что параметр может получить свое значение из универсального кода ресурса (URI), из тела запроса или из пользовательской привязки.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="a5f3e-207">Для параметров, полученных из универсального кода ресурса (URI), мы хотим убедиться, что универсальный код ресурса (URI) действительно содержит значение для этого параметра либо в пути (через словарь маршрутов), либо в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="a5f3e-208">Например, рассмотрим следующее действие:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="a5f3e-209">Параметр *ID* привязывается к универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="a5f3e-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="a5f3e-210">Таким образом, это действие может совпадать только с URI, содержащим значение для "ID", в словаре маршрутов или в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="a5f3e-211">Необязательные параметры являются исключением, так как они являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="a5f3e-212">Для необязательного параметра, если привязка не может получить значение из универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="a5f3e-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="a5f3e-213">Сложные типы являются исключением по другой причине.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="a5f3e-214">Сложный тип может быть привязан только к URI через пользовательскую привязку.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="a5f3e-215">Но в этом случае платформа не может заранее определить, будет ли параметр привязан к конкретному универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="a5f3e-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="a5f3e-216">Чтобы выяснить это, необходимо вызвать привязку.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="a5f3e-217">Цель алгоритма выбора заключается в выборе действия из статического описания перед вызовом любых привязок.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="a5f3e-218">Поэтому сложные типы исключаются из алгоритма сопоставления.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="a5f3e-219">После выбора действия вызываются все привязки параметров.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="a5f3e-220">Сводка.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-220">Summary:</span></span>

- <span data-ttu-id="a5f3e-221">Действие должно соответствовать методу HTTP запроса.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="a5f3e-222">Имя действия должно соответствовать записи "Action" в словаре маршрутов, если он есть.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="a5f3e-223">При каждом параметре действия, если параметр берется из универсального кода ресурса (URI), имя параметра должно быть найдено либо в словаре маршрутов, либо в строке запроса URI.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="a5f3e-224">(Необязательные параметры и параметры со сложными типами исключаются.)</span><span class="sxs-lookup"><span data-stu-id="a5f3e-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="a5f3e-225">Попробуйте сопоставить наибольшее количество параметров.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="a5f3e-226">Лучшим совпадением может быть метод без параметров.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="a5f3e-227">Расширенный пример</span><span class="sxs-lookup"><span data-stu-id="a5f3e-227">Extended Example</span></span>

<span data-ttu-id="a5f3e-228">Маршрутизации</span><span class="sxs-lookup"><span data-stu-id="a5f3e-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="a5f3e-229">Контроллер:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="a5f3e-230">HTTP-запрос:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="a5f3e-231">Сопоставление маршрутов</span><span class="sxs-lookup"><span data-stu-id="a5f3e-231">Route Matching</span></span>

<span data-ttu-id="a5f3e-232">Универсальный код ресурса (URI) соответствует маршруту с именем «Дефаултапи».</span><span class="sxs-lookup"><span data-stu-id="a5f3e-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="a5f3e-233">Словарь маршрутов содержит следующие записи:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="a5f3e-234">Controller: "Products"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-234">controller: "products"</span></span>
- <span data-ttu-id="a5f3e-235">Идентификатор: "1"</span><span class="sxs-lookup"><span data-stu-id="a5f3e-235">id: "1"</span></span>

<span data-ttu-id="a5f3e-236">Словарь маршрутов не содержит параметров строки запроса "Version" и "Details", но они по-прежнему будут учитываться во время выбора действия.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="a5f3e-237">Выбор контроллера</span><span class="sxs-lookup"><span data-stu-id="a5f3e-237">Controller Selection</span></span>

<span data-ttu-id="a5f3e-238">Из записи контроллера в словаре маршрутов типом контроллера является `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="a5f3e-239">Выбор действия</span><span class="sxs-lookup"><span data-stu-id="a5f3e-239">Action Selection</span></span>

<span data-ttu-id="a5f3e-240">HTTP-запрос является запросом GET.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="a5f3e-241">Действия контроллера, поддерживающие GET, — это `GetAll`, `GetById`и `FindProductsByName`.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="a5f3e-242">Словарь маршрутов не содержит записи для "Action", поэтому не нужно сопоставлять имя действия.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="a5f3e-243">Затем мы пытаемся сопоставить имена параметров для действий, просмотрев только действия GET.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="a5f3e-244">Действие</span><span class="sxs-lookup"><span data-stu-id="a5f3e-244">Action</span></span> | <span data-ttu-id="a5f3e-245">Параметры для сопоставления</span><span class="sxs-lookup"><span data-stu-id="a5f3e-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="a5f3e-246">none</span><span class="sxs-lookup"><span data-stu-id="a5f3e-246">none</span></span> |
| `GetById` | <span data-ttu-id="a5f3e-247">идентификатор</span><span class="sxs-lookup"><span data-stu-id="a5f3e-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="a5f3e-248">безымян</span><span class="sxs-lookup"><span data-stu-id="a5f3e-248">"name"</span></span> |

<span data-ttu-id="a5f3e-249">Обратите внимание, что параметр *версии* `GetById` не рассматривается, так как это необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="a5f3e-250">Метод `GetAll` соответствует тривиальному.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="a5f3e-251">Метод `GetById` также соответствует, так как словарь маршрутов содержит "ID".</span><span class="sxs-lookup"><span data-stu-id="a5f3e-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="a5f3e-252">Метод `FindProductsByName` не соответствует.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="a5f3e-253">Метод `GetById` WINS, так как он соответствует одному параметру и не имеет параметров для `GetAll`.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="a5f3e-254">Метод вызывается со следующими значениями параметров:</span><span class="sxs-lookup"><span data-stu-id="a5f3e-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="a5f3e-255">*ИД* = 1</span><span class="sxs-lookup"><span data-stu-id="a5f3e-255">*id* = 1</span></span>
- <span data-ttu-id="a5f3e-256">*версия* = 1,5</span><span class="sxs-lookup"><span data-stu-id="a5f3e-256">*version* = 1.5</span></span>

<span data-ttu-id="a5f3e-257">Обратите внимание, что несмотря на то, что *версия* не использовалась в алгоритме выбора, значение параметра берется из строки запроса URI.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="a5f3e-258">Точки расширения</span><span class="sxs-lookup"><span data-stu-id="a5f3e-258">Extension Points</span></span>

<span data-ttu-id="a5f3e-259">Веб-API предоставляет точки расширения для некоторых частей процесса маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="a5f3e-260">Интерфейс</span><span class="sxs-lookup"><span data-stu-id="a5f3e-260">Interface</span></span> | <span data-ttu-id="a5f3e-261">Description</span><span class="sxs-lookup"><span data-stu-id="a5f3e-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5f3e-262">**ихттпконтроллерселектор**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="a5f3e-263">Выбирает контроллер.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-263">Selects the controller.</span></span> |
| <span data-ttu-id="a5f3e-264">**ихттпконтроллертипересолвер**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="a5f3e-265">Возвращает список типов контроллеров.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-265">Gets the list of controller types.</span></span> <span data-ttu-id="a5f3e-266">**Дефаулсттпконтроллерселектор** выбирает тип контроллера из этого списка.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="a5f3e-267">**иассемблиесресолвер**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="a5f3e-268">Возвращает список сборок проекта.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="a5f3e-269">Интерфейс **ихттпконтроллертипересолвер** использует этот список для поиска типов контроллеров.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="a5f3e-270">**ихттпконтроллерактиватор**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="a5f3e-271">Создает новые экземпляры контроллера.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="a5f3e-272">**ихттпактионселектор**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="a5f3e-273">Выбирает действие.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-273">Selects the action.</span></span> |
| <span data-ttu-id="a5f3e-274">**ихттпактионинвокер**</span><span class="sxs-lookup"><span data-stu-id="a5f3e-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="a5f3e-275">Вызывает действие.</span><span class="sxs-lookup"><span data-stu-id="a5f3e-275">Invokes the action.</span></span> |

<span data-ttu-id="a5f3e-276">Чтобы предоставить собственную реализацию для любого из этих интерфейсов, используйте коллекцию **Services** для объекта **HttpConfiguration** :</span><span class="sxs-lookup"><span data-stu-id="a5f3e-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
