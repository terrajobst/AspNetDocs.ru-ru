---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Маршрутизация атрибутов в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447000"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="05ee0-102">Маршрутизация атрибутов в веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="05ee0-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="05ee0-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="05ee0-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="05ee0-104">*Маршрутизация* — это то, как веб-API сопоставляет URI с действием.</span><span class="sxs-lookup"><span data-stu-id="05ee0-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="05ee0-105">Веб-API 2 поддерживает новый тип маршрутизации, называемый *маршрутизацией атрибутов*.</span><span class="sxs-lookup"><span data-stu-id="05ee0-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="05ee0-106">Как следует из названия, маршрутизация атрибутов использует атрибуты для определения маршрутов.</span><span class="sxs-lookup"><span data-stu-id="05ee0-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="05ee0-107">Маршрутизация атрибутов обеспечивает более полный контроль над URI в веб-API.</span><span class="sxs-lookup"><span data-stu-id="05ee0-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="05ee0-108">Например, можно легко создать URI, описывающие иерархии ресурсов.</span><span class="sxs-lookup"><span data-stu-id="05ee0-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="05ee0-109">Более ранний стиль маршрутизации, называемый маршрутизацией на основе соглашений, по-прежнему поддерживается полностью.</span><span class="sxs-lookup"><span data-stu-id="05ee0-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="05ee0-110">На самом деле можно сочетать оба метода в одном проекте.</span><span class="sxs-lookup"><span data-stu-id="05ee0-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="05ee0-111">В этом разделе показано, как включить маршрутизацию атрибутов и приводятся различные параметры маршрутизации атрибутов.</span><span class="sxs-lookup"><span data-stu-id="05ee0-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="05ee0-112">Полное руководство, в котором используется маршрутизация атрибутов, см. в разделе [создание REST API с маршрутизацией атрибутов в веб-API 2](create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="05ee0-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05ee0-113">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="05ee0-113">Prerequisites</span></span>

<span data-ttu-id="05ee0-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional или Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="05ee0-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="05ee0-115">Кроме того, можно использовать диспетчер пакетов NuGet для установки необходимых пакетов.</span><span class="sxs-lookup"><span data-stu-id="05ee0-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="05ee0-116">В меню **Сервис** в Visual Studio выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="05ee0-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="05ee0-117">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="05ee0-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="05ee0-118">Зачем нужна маршрутизация атрибутов?</span><span class="sxs-lookup"><span data-stu-id="05ee0-118">Why Attribute Routing?</span></span>

<span data-ttu-id="05ee0-119">Первый выпуск веб-API использовал маршрутизацию *на основе соглашений* .</span><span class="sxs-lookup"><span data-stu-id="05ee0-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="05ee0-120">В этом типе маршрутизации определяется один или несколько шаблонов маршрутов, которые по сути являются параметризованными строками.</span><span class="sxs-lookup"><span data-stu-id="05ee0-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="05ee0-121">Когда платформа получает запрос, она сопоставляет URI с шаблоном маршрута.</span><span class="sxs-lookup"><span data-stu-id="05ee0-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="05ee0-122">(Дополнительные сведения о маршрутизации на основе соглашений см. [в разделе Маршрутизация в веб-API ASP.NET](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="05ee0-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="05ee0-123">Одним из преимуществ маршрутизации на основе соглашений является то, что шаблоны определяются в одном месте, а правила маршрутизации применяются одинаково ко всем контроллерам.</span><span class="sxs-lookup"><span data-stu-id="05ee0-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="05ee0-124">К сожалению, маршрутизация на основе соглашений делает несложным поддержку определенных шаблонов URI, общих для интерфейсов API RESTFUL.</span><span class="sxs-lookup"><span data-stu-id="05ee0-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="05ee0-125">Например, ресурсы часто содержат дочерние ресурсы: у клиентов есть заказы, у них есть актеры, авторы книг и т. д.</span><span class="sxs-lookup"><span data-stu-id="05ee0-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="05ee0-126">Естественно создать универсальные коды ресурса (URI), отражающие эти отношения:</span><span class="sxs-lookup"><span data-stu-id="05ee0-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="05ee0-127">Этот тип URI трудно создать с помощью маршрутизации на основе соглашений.</span><span class="sxs-lookup"><span data-stu-id="05ee0-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="05ee0-128">Хотя это и может быть сделано, результаты не масштабируются, если имеется много контроллеров или типов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="05ee0-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="05ee0-129">С помощью маршрутизации атрибутов можно просто определить маршрут для этого URI.</span><span class="sxs-lookup"><span data-stu-id="05ee0-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="05ee0-130">Просто добавьте атрибут к действию контроллера:</span><span class="sxs-lookup"><span data-stu-id="05ee0-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="05ee0-131">Ниже приведены некоторые другие шаблоны, которые упрощают маршрутизацию атрибутов.</span><span class="sxs-lookup"><span data-stu-id="05ee0-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="05ee0-132">**Управление версиями API**</span><span class="sxs-lookup"><span data-stu-id="05ee0-132">**API versioning**</span></span>

<span data-ttu-id="05ee0-133">В этом примере "/API/V1/Products" будет направляться на другой контроллер, чем "/API/v2/Products".</span><span class="sxs-lookup"><span data-stu-id="05ee0-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="05ee0-134">**Перегруженные сегменты URI**</span><span class="sxs-lookup"><span data-stu-id="05ee0-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="05ee0-135">В этом примере "1" — номер заказа, но "ожидание" сопоставляется с коллекцией.</span><span class="sxs-lookup"><span data-stu-id="05ee0-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="05ee0-136">**Несколько типов параметров**</span><span class="sxs-lookup"><span data-stu-id="05ee0-136">**Multiple parameter types**</span></span>

<span data-ttu-id="05ee0-137">В этом примере "1" — номер заказа, но "2013/06/16" указывает дату.</span><span class="sxs-lookup"><span data-stu-id="05ee0-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="05ee0-138">Включение маршрутизации атрибутов</span><span class="sxs-lookup"><span data-stu-id="05ee0-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="05ee0-139">Чтобы включить маршрутизацию атрибутов, вызовите **мафттпаттрибутераутес** во время настройки.</span><span class="sxs-lookup"><span data-stu-id="05ee0-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="05ee0-140">Этот метод расширения определен в классе **System. Web. http. хттпконфигуратионекстенсионс** .</span><span class="sxs-lookup"><span data-stu-id="05ee0-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="05ee0-141">Маршрутизацию атрибутов можно сочетать с маршрутизацией [на основе соглашения](routing-in-aspnet-web-api.md) .</span><span class="sxs-lookup"><span data-stu-id="05ee0-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="05ee0-142">Чтобы определить маршруты на основе соглашения, вызовите метод **мафттпрауте** .</span><span class="sxs-lookup"><span data-stu-id="05ee0-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="05ee0-143">Дополнительные сведения о настройке веб-API см. в разделе [настройка веб-API ASP.NET 2](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="05ee0-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="05ee0-144">Примечание. Переход с веб-API 1</span><span class="sxs-lookup"><span data-stu-id="05ee0-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="05ee0-145">До веб-API 2 шаблоны проектов веб-API создавали код следующим образом:</span><span class="sxs-lookup"><span data-stu-id="05ee0-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="05ee0-146">Если включена маршрутизация атрибутов, этот код вызовет исключение.</span><span class="sxs-lookup"><span data-stu-id="05ee0-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="05ee0-147">При обновлении существующего проекта веб-API для использования маршрутизации атрибутов обязательно обновите этот код конфигурации следующим образом:</span><span class="sxs-lookup"><span data-stu-id="05ee0-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="05ee0-148">Дополнительные сведения см. [в разделе Настройка веб-API с ASP.NET размещением](../advanced/configuring-aspnet-web-api.md#webhost).</span><span class="sxs-lookup"><span data-stu-id="05ee0-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="05ee0-149">Добавление атрибутов маршрута</span><span class="sxs-lookup"><span data-stu-id="05ee0-149">Adding Route Attributes</span></span>

<span data-ttu-id="05ee0-150">Ниже приведен пример маршрута, определенного с помощью атрибута.</span><span class="sxs-lookup"><span data-stu-id="05ee0-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="05ee0-151">Строка &quot;Customers/{customerId}/Orders&quot; является шаблоном универсального кода ресурса (URI) для маршрута.</span><span class="sxs-lookup"><span data-stu-id="05ee0-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="05ee0-152">Веб-API пытается сопоставить универсальный код ресурса (URI) запроса с шаблоном.</span><span class="sxs-lookup"><span data-stu-id="05ee0-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="05ee0-153">В этом примере "Customers" и "Orders" являются сегментами литералов, а "{customerId}" является параметром переменной.</span><span class="sxs-lookup"><span data-stu-id="05ee0-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="05ee0-154">Следующий URI будет соответствовать этому шаблону:</span><span class="sxs-lookup"><span data-stu-id="05ee0-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="05ee0-155">Сопоставление можно ограничить с помощью [ограничений](#constraints), описанных далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="05ee0-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="05ee0-156">Обратите внимание, что параметр &quot;{customerId}&quot; в шаблоне маршрута соответствует имени параметра *customerId* в методе.</span><span class="sxs-lookup"><span data-stu-id="05ee0-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="05ee0-157">Когда веб-API вызывает действие контроллера, он пытается привязать параметры маршрута.</span><span class="sxs-lookup"><span data-stu-id="05ee0-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="05ee0-158">Например, если URI `http://example.com/customers/1/orders`, веб-API пытается привязать значение "1" к параметру *customerId* в действии.</span><span class="sxs-lookup"><span data-stu-id="05ee0-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="05ee0-159">Шаблон URI может иметь несколько параметров:</span><span class="sxs-lookup"><span data-stu-id="05ee0-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="05ee0-160">Все методы контроллера, не имеющие атрибута Route, используют маршрутизацию на основе соглашений.</span><span class="sxs-lookup"><span data-stu-id="05ee0-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="05ee0-161">Таким образом, можно объединить оба типа маршрутизации в одном проекте.</span><span class="sxs-lookup"><span data-stu-id="05ee0-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="05ee0-162">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="05ee0-162">HTTP Methods</span></span>

<span data-ttu-id="05ee0-163">Веб-API также выбирает действия на основе метода HTTP запроса (GET, POST и т. д.).</span><span class="sxs-lookup"><span data-stu-id="05ee0-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="05ee0-164">По умолчанию веб-API ищет совпадение без учета регистра с началом имени метода контроллера.</span><span class="sxs-lookup"><span data-stu-id="05ee0-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="05ee0-165">Например, метод контроллера с именем `PutCustomers` соответствует запросу HTTP-размещения.</span><span class="sxs-lookup"><span data-stu-id="05ee0-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="05ee0-166">Это соглашение можно переопределить, добавив метод с помощью следующих атрибутов:</span><span class="sxs-lookup"><span data-stu-id="05ee0-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="05ee0-167">**[Хттпделете]**</span><span class="sxs-lookup"><span data-stu-id="05ee0-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="05ee0-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="05ee0-168">**[HttpGet]**</span></span>
- <span data-ttu-id="05ee0-169">**[Хттфеад]**</span><span class="sxs-lookup"><span data-stu-id="05ee0-169">**[HttpHead]**</span></span>
- <span data-ttu-id="05ee0-170">**[Хттпоптионс]**</span><span class="sxs-lookup"><span data-stu-id="05ee0-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="05ee0-171">**[Хттппатч]**</span><span class="sxs-lookup"><span data-stu-id="05ee0-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="05ee0-172">**HttpPost**</span><span class="sxs-lookup"><span data-stu-id="05ee0-172">**[HttpPost]**</span></span>
- <span data-ttu-id="05ee0-173">**[Хттппут]**</span><span class="sxs-lookup"><span data-stu-id="05ee0-173">**[HttpPut]**</span></span>

<span data-ttu-id="05ee0-174">В следующем примере метод Креатебук сопоставляется с запросами HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="05ee0-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="05ee0-175">Для всех других методов HTTP, включая нестандартные методы, используйте атрибут **акцептвербс** , который принимает список методов HTTP.</span><span class="sxs-lookup"><span data-stu-id="05ee0-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="05ee0-176">Префиксы маршрутов</span><span class="sxs-lookup"><span data-stu-id="05ee0-176">Route Prefixes</span></span>

<span data-ttu-id="05ee0-177">Часто маршруты в контроллере начинаются с одного и того же префикса.</span><span class="sxs-lookup"><span data-stu-id="05ee0-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="05ee0-178">Пример:</span><span class="sxs-lookup"><span data-stu-id="05ee0-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="05ee0-179">Общий префикс для всего контроллера можно задать с помощью атрибута **[RoutePrefix]** :</span><span class="sxs-lookup"><span data-stu-id="05ee0-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="05ee0-180">Используйте тильду (~) в атрибуте Method, чтобы переопределить префикс маршрута:</span><span class="sxs-lookup"><span data-stu-id="05ee0-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="05ee0-181">Префикс маршрута может включать параметры:</span><span class="sxs-lookup"><span data-stu-id="05ee0-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="05ee0-182">Ограничения маршрута</span><span class="sxs-lookup"><span data-stu-id="05ee0-182">Route Constraints</span></span>

<span data-ttu-id="05ee0-183">Ограничения маршрутов позволяют ограничить способ сопоставления параметров в шаблоне маршрута.</span><span class="sxs-lookup"><span data-stu-id="05ee0-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="05ee0-184">Общий синтаксис — &quot;{параметр: Constraint}&quot;.</span><span class="sxs-lookup"><span data-stu-id="05ee0-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="05ee0-185">Пример:</span><span class="sxs-lookup"><span data-stu-id="05ee0-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="05ee0-186">В этом случае первый маршрут будет выбран, только если идентификатор &quot;&quot; сегмент URI является целым числом.</span><span class="sxs-lookup"><span data-stu-id="05ee0-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="05ee0-187">В противном случае будет выбран второй маршрут.</span><span class="sxs-lookup"><span data-stu-id="05ee0-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="05ee0-188">В следующей таблице перечислены поддерживаемые ограничения.</span><span class="sxs-lookup"><span data-stu-id="05ee0-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="05ee0-189">Ограничение</span><span class="sxs-lookup"><span data-stu-id="05ee0-189">Constraint</span></span> | <span data-ttu-id="05ee0-190">Description</span><span class="sxs-lookup"><span data-stu-id="05ee0-190">Description</span></span> | <span data-ttu-id="05ee0-191">Пример</span><span class="sxs-lookup"><span data-stu-id="05ee0-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05ee0-192">альфа</span><span class="sxs-lookup"><span data-stu-id="05ee0-192">alpha</span></span> | <span data-ttu-id="05ee0-193">Соответствует символам латинского алфавита в верхнем или нижнем регистре (a – z, A – Z)</span><span class="sxs-lookup"><span data-stu-id="05ee0-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="05ee0-194">{КС:Алфа}</span><span class="sxs-lookup"><span data-stu-id="05ee0-194">{x:alpha}</span></span> |
| <span data-ttu-id="05ee0-195">bool</span><span class="sxs-lookup"><span data-stu-id="05ee0-195">bool</span></span> | <span data-ttu-id="05ee0-196">Соответствует логическому значению.</span><span class="sxs-lookup"><span data-stu-id="05ee0-196">Matches a Boolean value.</span></span> | <span data-ttu-id="05ee0-197">{КС:бул}</span><span class="sxs-lookup"><span data-stu-id="05ee0-197">{x:bool}</span></span> |
| <span data-ttu-id="05ee0-198">DATETIME</span><span class="sxs-lookup"><span data-stu-id="05ee0-198">datetime</span></span> | <span data-ttu-id="05ee0-199">Соответствует значению **даты и времени** .</span><span class="sxs-lookup"><span data-stu-id="05ee0-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="05ee0-200">{КС:датетиме}</span><span class="sxs-lookup"><span data-stu-id="05ee0-200">{x:datetime}</span></span> |
| <span data-ttu-id="05ee0-201">Decimal</span><span class="sxs-lookup"><span data-stu-id="05ee0-201">decimal</span></span> | <span data-ttu-id="05ee0-202">Соответствует десятичному значению.</span><span class="sxs-lookup"><span data-stu-id="05ee0-202">Matches a decimal value.</span></span> | <span data-ttu-id="05ee0-203">{КС:деЦимал}</span><span class="sxs-lookup"><span data-stu-id="05ee0-203">{x:decimal}</span></span> |
| <span data-ttu-id="05ee0-204">double</span><span class="sxs-lookup"><span data-stu-id="05ee0-204">double</span></span> | <span data-ttu-id="05ee0-205">Соответствует 64-разрядному значению с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="05ee0-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="05ee0-206">{КС:даубле}</span><span class="sxs-lookup"><span data-stu-id="05ee0-206">{x:double}</span></span> |
| <span data-ttu-id="05ee0-207">FLOAT</span><span class="sxs-lookup"><span data-stu-id="05ee0-207">float</span></span> | <span data-ttu-id="05ee0-208">Соответствует 32-разрядному значению с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="05ee0-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="05ee0-209">{КС:флоат}</span><span class="sxs-lookup"><span data-stu-id="05ee0-209">{x:float}</span></span> |
| <span data-ttu-id="05ee0-210">guid</span><span class="sxs-lookup"><span data-stu-id="05ee0-210">guid</span></span> | <span data-ttu-id="05ee0-211">Соответствует значению GUID.</span><span class="sxs-lookup"><span data-stu-id="05ee0-211">Matches a GUID value.</span></span> | <span data-ttu-id="05ee0-212">{КС:гуид}</span><span class="sxs-lookup"><span data-stu-id="05ee0-212">{x:guid}</span></span> |
| <span data-ttu-id="05ee0-213">INT</span><span class="sxs-lookup"><span data-stu-id="05ee0-213">int</span></span> | <span data-ttu-id="05ee0-214">Соответствует 32-разрядному целому значению.</span><span class="sxs-lookup"><span data-stu-id="05ee0-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="05ee0-215">{КС:Инт}</span><span class="sxs-lookup"><span data-stu-id="05ee0-215">{x:int}</span></span> |
| <span data-ttu-id="05ee0-216">length</span><span class="sxs-lookup"><span data-stu-id="05ee0-216">length</span></span> | <span data-ttu-id="05ee0-217">Соответствует строке с указанной длиной или в пределах указанного диапазона длин.</span><span class="sxs-lookup"><span data-stu-id="05ee0-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="05ee0-218">{КС:ленгс (6)} {КС:ленгс (1, 20)}</span><span class="sxs-lookup"><span data-stu-id="05ee0-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="05ee0-219">long</span><span class="sxs-lookup"><span data-stu-id="05ee0-219">long</span></span> | <span data-ttu-id="05ee0-220">Соответствует 64-разрядному целому значению.</span><span class="sxs-lookup"><span data-stu-id="05ee0-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="05ee0-221">{КС:Лонг}</span><span class="sxs-lookup"><span data-stu-id="05ee0-221">{x:long}</span></span> |
| <span data-ttu-id="05ee0-222">max</span><span class="sxs-lookup"><span data-stu-id="05ee0-222">max</span></span> | <span data-ttu-id="05ee0-223">Соответствует целочисленному значению с максимальным значением.</span><span class="sxs-lookup"><span data-stu-id="05ee0-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="05ee0-224">{КС:Макс (10)}</span><span class="sxs-lookup"><span data-stu-id="05ee0-224">{x:max(10)}</span></span> |
| <span data-ttu-id="05ee0-225">MaxLength</span><span class="sxs-lookup"><span data-stu-id="05ee0-225">maxlength</span></span> | <span data-ttu-id="05ee0-226">Соответствует строке с максимальной длиной.</span><span class="sxs-lookup"><span data-stu-id="05ee0-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="05ee0-227">{КС:максленгс (10)}</span><span class="sxs-lookup"><span data-stu-id="05ee0-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="05ee0-228">Min</span><span class="sxs-lookup"><span data-stu-id="05ee0-228">min</span></span> | <span data-ttu-id="05ee0-229">Соответствует целочисленному значению с минимальным значением.</span><span class="sxs-lookup"><span data-stu-id="05ee0-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="05ee0-230">{КС:мин (10)}</span><span class="sxs-lookup"><span data-stu-id="05ee0-230">{x:min(10)}</span></span> |
| <span data-ttu-id="05ee0-231">MinLength</span><span class="sxs-lookup"><span data-stu-id="05ee0-231">minlength</span></span> | <span data-ttu-id="05ee0-232">Соответствует строке с минимальной длиной.</span><span class="sxs-lookup"><span data-stu-id="05ee0-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="05ee0-233">{КС:минленгс (10)}</span><span class="sxs-lookup"><span data-stu-id="05ee0-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="05ee0-234">range</span><span class="sxs-lookup"><span data-stu-id="05ee0-234">range</span></span> | <span data-ttu-id="05ee0-235">Соответствует целому числу в диапазоне значений.</span><span class="sxs-lookup"><span data-stu-id="05ee0-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="05ee0-236">{КС:ранже (10, 50)}</span><span class="sxs-lookup"><span data-stu-id="05ee0-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="05ee0-237">regex</span><span class="sxs-lookup"><span data-stu-id="05ee0-237">regex</span></span> | <span data-ttu-id="05ee0-238">Соответствует регулярному выражению.</span><span class="sxs-lookup"><span data-stu-id="05ee0-238">Matches a regular expression.</span></span> | <span data-ttu-id="05ee0-239">{КС:режекс (^ \d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="05ee0-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="05ee0-240">Обратите внимание, что некоторые ограничения, такие как &quot;min&quot;, принимают аргументы в круглых скобках.</span><span class="sxs-lookup"><span data-stu-id="05ee0-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="05ee0-241">К параметру можно применить несколько ограничений, разделенных двоеточием.</span><span class="sxs-lookup"><span data-stu-id="05ee0-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="05ee0-242">Пользовательские ограничения маршрутов</span><span class="sxs-lookup"><span data-stu-id="05ee0-242">Custom Route Constraints</span></span>

<span data-ttu-id="05ee0-243">Можно создать пользовательские ограничения маршрута, реализовав интерфейс **ихттпраутеконстраинт** .</span><span class="sxs-lookup"><span data-stu-id="05ee0-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="05ee0-244">Например, следующее ограничение ограничит параметр до ненулевого целочисленного значения.</span><span class="sxs-lookup"><span data-stu-id="05ee0-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="05ee0-245">В следующем коде показано, как зарегистрировать ограничение:</span><span class="sxs-lookup"><span data-stu-id="05ee0-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="05ee0-246">Теперь можно применить ограничение к маршрутам:</span><span class="sxs-lookup"><span data-stu-id="05ee0-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="05ee0-247">Также можно заменить весь класс **дефаултинлинеконстраинтресолвер** , реализовав интерфейс **иинлинеконстраинтресолвер** .</span><span class="sxs-lookup"><span data-stu-id="05ee0-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="05ee0-248">Это приведет к замене всех встроенных ограничений, если только реализация **иинлинеконстраинтресолвер** специально не добавит их.</span><span class="sxs-lookup"><span data-stu-id="05ee0-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="05ee0-249">Необязательные параметры URI и значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="05ee0-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="05ee0-250">Параметр URI можно сделать необязательным, добавив вопросительный знак в параметр Route.</span><span class="sxs-lookup"><span data-stu-id="05ee0-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="05ee0-251">Если параметр маршрута является необязательным, необходимо определить значение по умолчанию для параметра метода.</span><span class="sxs-lookup"><span data-stu-id="05ee0-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="05ee0-252">В этом примере `/api/books/locale/1033` и `/api/books/locale` возвращают один и тот же ресурс.</span><span class="sxs-lookup"><span data-stu-id="05ee0-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="05ee0-253">Кроме того, можно указать значение по умолчанию в шаблоне маршрута следующим образом:</span><span class="sxs-lookup"><span data-stu-id="05ee0-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="05ee0-254">Это почти так же, как в предыдущем примере, но при применении значения по умолчанию существует небольшая разница в поведении.</span><span class="sxs-lookup"><span data-stu-id="05ee0-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="05ee0-255">В первом примере ("{LCID: int?}") значение по умолчанию 1033 присваивается непосредственно параметру метода, поэтому параметр будет иметь это точное значение.</span><span class="sxs-lookup"><span data-stu-id="05ee0-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="05ee0-256">Во втором примере ("{LCID: int = 1033}") значение по умолчанию "1033" проходит процесс привязки модели.</span><span class="sxs-lookup"><span data-stu-id="05ee0-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="05ee0-257">Связыватель модели по умолчанию преобразует "1033" в числовое значение 1033.</span><span class="sxs-lookup"><span data-stu-id="05ee0-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="05ee0-258">Однако можно подключить пользовательский связыватель модели, который может сделать что-то другое.</span><span class="sxs-lookup"><span data-stu-id="05ee0-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="05ee0-259">(В большинстве случаев, если в конвейере нет пользовательских связывателей модели, эти две формы будут эквивалентны.)</span><span class="sxs-lookup"><span data-stu-id="05ee0-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="05ee0-260">Имена маршрутов</span><span class="sxs-lookup"><span data-stu-id="05ee0-260">Route Names</span></span>

<span data-ttu-id="05ee0-261">В веб-API у каждого маршрута есть имя.</span><span class="sxs-lookup"><span data-stu-id="05ee0-261">In Web API, every route has a name.</span></span> <span data-ttu-id="05ee0-262">Имена маршрутов удобно использовать для создания ссылок, чтобы можно было включить ссылку в HTTP-ответ.</span><span class="sxs-lookup"><span data-stu-id="05ee0-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="05ee0-263">Чтобы указать имя маршрута, задайте свойство **Name** атрибута.</span><span class="sxs-lookup"><span data-stu-id="05ee0-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="05ee0-264">В следующем примере показано, как задать имя маршрута, а также как использовать имя маршрута при создании ссылки.</span><span class="sxs-lookup"><span data-stu-id="05ee0-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="05ee0-265">Порядок маршрутов</span><span class="sxs-lookup"><span data-stu-id="05ee0-265">Route Order</span></span>

<span data-ttu-id="05ee0-266">Когда платформа пытается сопоставить URI с маршрутом, он оценивает маршруты в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="05ee0-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="05ee0-267">Чтобы указать порядок, задайте свойство **Order** для атрибута Route.</span><span class="sxs-lookup"><span data-stu-id="05ee0-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="05ee0-268">Значения меньшего уровня оцениваются первыми.</span><span class="sxs-lookup"><span data-stu-id="05ee0-268">Lower values are evaluated first.</span></span> <span data-ttu-id="05ee0-269">Значение порядка по умолчанию равно нулю.</span><span class="sxs-lookup"><span data-stu-id="05ee0-269">The default order value is zero.</span></span>

<span data-ttu-id="05ee0-270">Вот как определяется общее упорядочение:</span><span class="sxs-lookup"><span data-stu-id="05ee0-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="05ee0-271">Сравните свойство **Order** атрибута Route.</span><span class="sxs-lookup"><span data-stu-id="05ee0-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="05ee0-272">Взгляните на каждый сегмент URI в шаблоне маршрута.</span><span class="sxs-lookup"><span data-stu-id="05ee0-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="05ee0-273">Для каждого сегмента выполните следующий порядок:</span><span class="sxs-lookup"><span data-stu-id="05ee0-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="05ee0-274">Литеральные сегменты.</span><span class="sxs-lookup"><span data-stu-id="05ee0-274">Literal segments.</span></span>
    2. <span data-ttu-id="05ee0-275">Параметры маршрутизации с ограничениями.</span><span class="sxs-lookup"><span data-stu-id="05ee0-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="05ee0-276">Параметры маршрутизации без ограничений.</span><span class="sxs-lookup"><span data-stu-id="05ee0-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="05ee0-277">Сегменты параметра-шаблона с ограничениями.</span><span class="sxs-lookup"><span data-stu-id="05ee0-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="05ee0-278">Сегменты параметров с подстановочными знаками без ограничений.</span><span class="sxs-lookup"><span data-stu-id="05ee0-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="05ee0-279">В случае с привязкум маршруты упорядочиваются по порядковому номеру строки ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) шаблона маршрута без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="05ee0-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="05ee0-280">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="05ee0-280">Here is an example.</span></span> <span data-ttu-id="05ee0-281">Предположим, вы определили следующий контроллер:</span><span class="sxs-lookup"><span data-stu-id="05ee0-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="05ee0-282">Эти маршруты упорядочиваются следующим образом.</span><span class="sxs-lookup"><span data-stu-id="05ee0-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="05ee0-283">заказы/подробности</span><span class="sxs-lookup"><span data-stu-id="05ee0-283">orders/details</span></span>
2. <span data-ttu-id="05ee0-284">Orders/{ID}</span><span class="sxs-lookup"><span data-stu-id="05ee0-284">orders/{id}</span></span>
3. <span data-ttu-id="05ee0-285">Orders/{customerName}</span><span class="sxs-lookup"><span data-stu-id="05ee0-285">orders/{customerName}</span></span>
4. <span data-ttu-id="05ee0-286">Orders/{\*Date}</span><span class="sxs-lookup"><span data-stu-id="05ee0-286">orders/{\*date}</span></span>
5. <span data-ttu-id="05ee0-287">заказы/ожидание</span><span class="sxs-lookup"><span data-stu-id="05ee0-287">orders/pending</span></span>

<span data-ttu-id="05ee0-288">Обратите внимание, что «Details» — это литеральный сегмент, который отображается перед «{ID}», но «ожидание» отображается последним, так как свойство **Order** имеет значение 1.</span><span class="sxs-lookup"><span data-stu-id="05ee0-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="05ee0-289">(В этом примере предполагается, что клиенты с именами «Details» и «Pending» отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="05ee0-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="05ee0-290">Как правило, старайтесь не использовать неоднозначные маршруты.</span><span class="sxs-lookup"><span data-stu-id="05ee0-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="05ee0-291">В этом примере лучше использовать шаблон маршрута для `GetByCustomer` — "Customers/{customerName}").</span><span class="sxs-lookup"><span data-stu-id="05ee0-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
