---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: Поддержка параметров запроса OData в ASP.NET Web API 2 — ASP.NET 4.x
author: MikeWasson
description: Обзор с примерами кода показаны поддержки параметров запроса OData в веб-API ASP.NET 2 для ASP.NET 4.x.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 428e4942e42436585049c1e84cd7b07a4a79c0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59411570"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="a5455-103">Поддержка параметров запроса OData в веб-API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a5455-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="a5455-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a5455-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a5455-105">В этом обзоре с примерами кода демонстрируется поддержки параметров запроса OData в веб-API ASP.NET 2 для ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="a5455-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="a5455-106">OData определяет параметры, которые можно использовать для изменения запроса OData.</span><span class="sxs-lookup"><span data-stu-id="a5455-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="a5455-107">Клиент отправляет эти параметры в строке запроса URI запроса.</span><span class="sxs-lookup"><span data-stu-id="a5455-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="a5455-108">Например чтобы отсортировать результаты, клиент использует параметр $orderby:</span><span class="sxs-lookup"><span data-stu-id="a5455-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="a5455-109">Спецификации протокола OData вызывает эти параметры *параметры запроса*.</span><span class="sxs-lookup"><span data-stu-id="a5455-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="a5455-110">Вы можете включить параметры запроса OData для любого контроллера веб-API в вашем проекте &#8212; контроллера не должны быть конечной точкой OData.</span><span class="sxs-lookup"><span data-stu-id="a5455-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="a5455-111">Это позволяет легко добавить функции, такие как фильтрация и сортировка в любое приложение веб-API.</span><span class="sxs-lookup"><span data-stu-id="a5455-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="a5455-112">Прежде чем включать параметры запроса, см. в статье в разделе [рекомендации по безопасности OData](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="a5455-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="a5455-113">Включение параметров запроса OData</span><span class="sxs-lookup"><span data-stu-id="a5455-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="a5455-114">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="a5455-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="a5455-115">Server-Driven Paging</span><span class="sxs-lookup"><span data-stu-id="a5455-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="a5455-116">Ограничение параметры запроса</span><span class="sxs-lookup"><span data-stu-id="a5455-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="a5455-117">Вызов непосредственно параметры запроса</span><span class="sxs-lookup"><span data-stu-id="a5455-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="a5455-118">Проверка запроса</span><span class="sxs-lookup"><span data-stu-id="a5455-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="a5455-119">Включение параметров запроса OData</span><span class="sxs-lookup"><span data-stu-id="a5455-119">Enabling OData Query Options</span></span>

<span data-ttu-id="a5455-120">Веб-API поддерживает следующие параметры запроса OData:</span><span class="sxs-lookup"><span data-stu-id="a5455-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="a5455-121">Параметр</span><span class="sxs-lookup"><span data-stu-id="a5455-121">Option</span></span> | <span data-ttu-id="a5455-122">Описание</span><span class="sxs-lookup"><span data-stu-id="a5455-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5455-123">$expand</span><span class="sxs-lookup"><span data-stu-id="a5455-123">$expand</span></span> | <span data-ttu-id="a5455-124">При развертывании встроенного связанных сущностей.</span><span class="sxs-lookup"><span data-stu-id="a5455-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="a5455-125">$filter</span><span class="sxs-lookup"><span data-stu-id="a5455-125">$filter</span></span> | <span data-ttu-id="a5455-126">Фильтрует результаты, на основе логического условия.</span><span class="sxs-lookup"><span data-stu-id="a5455-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="a5455-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="a5455-127">$inlinecount</span></span> | <span data-ttu-id="a5455-128">Указывает, что сервер для включения общее число соответствующих сущностей в ответе.</span><span class="sxs-lookup"><span data-stu-id="a5455-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="a5455-129">(Полезно для серверное разбиение по страницам).</span><span class="sxs-lookup"><span data-stu-id="a5455-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="a5455-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="a5455-130">$orderby</span></span> | <span data-ttu-id="a5455-131">Сортирует результаты.</span><span class="sxs-lookup"><span data-stu-id="a5455-131">Sorts the results.</span></span> |
| <span data-ttu-id="a5455-132">$select</span><span class="sxs-lookup"><span data-stu-id="a5455-132">$select</span></span> | <span data-ttu-id="a5455-133">Выбирает, какие свойства будут включены в ответе.</span><span class="sxs-lookup"><span data-stu-id="a5455-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="a5455-134">$skip</span><span class="sxs-lookup"><span data-stu-id="a5455-134">$skip</span></span> | <span data-ttu-id="a5455-135">Пропускает первые n результатов.</span><span class="sxs-lookup"><span data-stu-id="a5455-135">Skips the first n results.</span></span> |
| <span data-ttu-id="a5455-136">$top</span><span class="sxs-lookup"><span data-stu-id="a5455-136">$top</span></span> | <span data-ttu-id="a5455-137">Возвращает только первые n результатов.</span><span class="sxs-lookup"><span data-stu-id="a5455-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="a5455-138">Чтобы использовать параметры запроса OData, необходимо включить их явным образом.</span><span class="sxs-lookup"><span data-stu-id="a5455-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="a5455-139">Можно включить глобально для всего приложения или включить их для определенных контроллеров и определенные действия.</span><span class="sxs-lookup"><span data-stu-id="a5455-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="a5455-140">Чтобы включить параметры запроса OData глобально, вызовите **EnableQuerySupport** на **HttpConfiguration** класса во время запуска:</span><span class="sxs-lookup"><span data-stu-id="a5455-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="a5455-141">**EnableQuerySupport** метод включает параметры запроса для любого действия контроллера, который возвращает **IQueryable** типа.</span><span class="sxs-lookup"><span data-stu-id="a5455-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="a5455-142">Если вы не хотите параметры запросов, которые включены для всего приложения, вы можете включить их для действий определенного контроллера, добавив **[Queryable]** атрибут к методу действия.</span><span class="sxs-lookup"><span data-stu-id="a5455-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="a5455-143">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="a5455-143">Example Queries</span></span>

<span data-ttu-id="a5455-144">В этом разделе показаны типы запросов, которые возможно использует параметры запроса OData.</span><span class="sxs-lookup"><span data-stu-id="a5455-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="a5455-145">Конкретные сведения о параметрах запроса см. в документации по OData на [www.odata.org](http://www.odata.org/).</span><span class="sxs-lookup"><span data-stu-id="a5455-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="a5455-146">Сведения о $ разверните узел и $select, см. в разделе [использование $select, $expand и $value в OData веб-API ASP.NET](using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="a5455-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="a5455-147">**Разбиение на страницы клиента**</span><span class="sxs-lookup"><span data-stu-id="a5455-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="a5455-148">Для больших наборов сущностей клиент может потребоваться ограничить количество результатов.</span><span class="sxs-lookup"><span data-stu-id="a5455-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="a5455-149">Например клиент может показывать 10 записей одновременно, со ссылками «Далее» для получения следующей страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="a5455-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="a5455-150">Чтобы сделать это, клиент использует параметры $top и $skip.</span><span class="sxs-lookup"><span data-stu-id="a5455-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="a5455-151">Параметр $top дает максимальное количество возвращаемых записей, а параметр $skip дает число пропускаемых записей.</span><span class="sxs-lookup"><span data-stu-id="a5455-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="a5455-152">Предыдущий пример извлекает записи 21-30.</span><span class="sxs-lookup"><span data-stu-id="a5455-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="a5455-153">**Фильтрация**</span><span class="sxs-lookup"><span data-stu-id="a5455-153">**Filtering**</span></span>

<span data-ttu-id="a5455-154">Параметр $filter позволяет клиенту фильтрации результатов путем применения логического выражения.</span><span class="sxs-lookup"><span data-stu-id="a5455-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="a5455-155">Выражения фильтра весьма существенны; они включают логические операторы и арифметические операторы, строковые функции и функции даты.</span><span class="sxs-lookup"><span data-stu-id="a5455-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="a5455-156">Возвратить все продукты с категорией, равным «Toys».</span><span class="sxs-lookup"><span data-stu-id="a5455-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="a5455-157">`http://localhost/Products?$filter=Category` EQ «Toys»</span><span class="sxs-lookup"><span data-stu-id="a5455-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="a5455-158">Возвратить все продукты с ценой меньше 10.</span><span class="sxs-lookup"><span data-stu-id="a5455-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="a5455-159">`http://localhost/Products?$filter=Price` lt 10</span><span class="sxs-lookup"><span data-stu-id="a5455-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="a5455-160">Логические операторы Возвратить все продукты где цена > = 5 и цена < = 15.</span><span class="sxs-lookup"><span data-stu-id="a5455-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="a5455-161">`http://localhost/Products?$filter=Price` GE 5 и цена le 15</span><span class="sxs-lookup"><span data-stu-id="a5455-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="a5455-162">Строковые функции: Возвратить все продукты с «zz» в имени.</span><span class="sxs-lookup"><span data-stu-id="a5455-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="a5455-163">Функции даты: Возвратить все продукты с ReleaseDate за 2005.</span><span class="sxs-lookup"><span data-stu-id="a5455-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="a5455-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span><span class="sxs-lookup"><span data-stu-id="a5455-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="a5455-165">**Сортировка**</span><span class="sxs-lookup"><span data-stu-id="a5455-165">**Sorting**</span></span>

<span data-ttu-id="a5455-166">Чтобы отсортировать результаты, используйте фильтр $orderby.</span><span class="sxs-lookup"><span data-stu-id="a5455-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="a5455-167">Сортировка по цене.</span><span class="sxs-lookup"><span data-stu-id="a5455-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="a5455-168">Сортировка по цене в убывающем порядке (от большего к меньшему).</span><span class="sxs-lookup"><span data-stu-id="a5455-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="a5455-169">Сортировать по категориям, а затем отсортировать по цене в убывающем порядке в пределах их категорий.</span><span class="sxs-lookup"><span data-stu-id="a5455-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="a5455-170">Server-Driven Paging</span><span class="sxs-lookup"><span data-stu-id="a5455-170">Server-Driven Paging</span></span>

<span data-ttu-id="a5455-171">Если база данных содержит миллионы записей, вы не хотите отправлять их все в одной полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="a5455-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="a5455-172">Чтобы избежать этого, сервер может ограничить количество записей, отправляемых в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="a5455-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="a5455-173">Чтобы включить разбиение на страницы, задайте **PageSize** свойство в **Queryable** атрибута.</span><span class="sxs-lookup"><span data-stu-id="a5455-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="a5455-174">Значение — это максимальное число возвращаемых записей.</span><span class="sxs-lookup"><span data-stu-id="a5455-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="a5455-175">Если ваш контроллер возвращает формат OData, текст ответа будет содержать ссылку на следующую страницу данных:</span><span class="sxs-lookup"><span data-stu-id="a5455-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="a5455-176">Клиент может использовать эту ссылку для получения следующей страницы.</span><span class="sxs-lookup"><span data-stu-id="a5455-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="a5455-177">Чтобы узнать, общее число записей в результирующем наборе, клиент может задать параметра запроса $inlinecount со значением «allpages».</span><span class="sxs-lookup"><span data-stu-id="a5455-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="a5455-178">Значение «allpages» предписывает серверу включал полный счетчик в ответе:</span><span class="sxs-lookup"><span data-stu-id="a5455-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="a5455-179">Ссылки следующей страницы и встроенное количество требуется формат OData.</span><span class="sxs-lookup"><span data-stu-id="a5455-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="a5455-180">Причина в том, что OData определяет специальные поля в тексте ответа для размещения ссылки и count.</span><span class="sxs-lookup"><span data-stu-id="a5455-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>


<span data-ttu-id="a5455-181">Для форматов не OData, можно по-прежнему поддерживает счетчик ссылок и в строке следующей страницы, заключив результаты запроса в **PageResult&lt;T&gt;**  объекта.</span><span class="sxs-lookup"><span data-stu-id="a5455-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="a5455-182">Однако он требует немного больше кода.</span><span class="sxs-lookup"><span data-stu-id="a5455-182">However, it requires a bit more code.</span></span> <span data-ttu-id="a5455-183">Пример:</span><span class="sxs-lookup"><span data-stu-id="a5455-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="a5455-184">Ниже приведен пример ответа JSON:</span><span class="sxs-lookup"><span data-stu-id="a5455-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="a5455-185">Ограничение параметры запроса</span><span class="sxs-lookup"><span data-stu-id="a5455-185">Limiting the Query Options</span></span>

<span data-ttu-id="a5455-186">Параметры запроса предоставьте клиенту массу контроль над запроса, который выполняется на сервере.</span><span class="sxs-lookup"><span data-stu-id="a5455-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="a5455-187">В некоторых случаях может потребоваться ограничить доступные параметры для повышения производительности и безопасности.</span><span class="sxs-lookup"><span data-stu-id="a5455-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="a5455-188">**[Queryable]** атрибут некоторые встроенные свойства для этого.</span><span class="sxs-lookup"><span data-stu-id="a5455-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="a5455-189">Ниже приводятся некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="a5455-189">Here are some examples.</span></span>

<span data-ttu-id="a5455-190">Разрешить только $skip, $top, для поддержки разбиения по страницам и ничего более:</span><span class="sxs-lookup"><span data-stu-id="a5455-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="a5455-191">Разрешить упорядочение только с определенными свойствами запретить сортировку по свойствам, которые не индексируются в базе данных:</span><span class="sxs-lookup"><span data-stu-id="a5455-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="a5455-192">Разрешить использование логической функции «eq», но не другие логические функции:</span><span class="sxs-lookup"><span data-stu-id="a5455-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="a5455-193">Не разрешать все арифметические операторы:</span><span class="sxs-lookup"><span data-stu-id="a5455-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="a5455-194">Вы можете ограничить параметры глобально, создав **QueryableAttribute** экземпляра и передается командлету **EnableQuerySupport** функции:</span><span class="sxs-lookup"><span data-stu-id="a5455-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="a5455-195">Вызов непосредственно параметры запроса</span><span class="sxs-lookup"><span data-stu-id="a5455-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="a5455-196">Вместо использования **[Queryable]** атрибут, параметры запроса можно вызвать непосредственно в контроллере.</span><span class="sxs-lookup"><span data-stu-id="a5455-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="a5455-197">Чтобы сделать это, добавьте **ODataQueryOptions** параметр для метода контроллера.</span><span class="sxs-lookup"><span data-stu-id="a5455-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="a5455-198">В этом случае не требуется **[Queryable]** атрибута.</span><span class="sxs-lookup"><span data-stu-id="a5455-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="a5455-199">Заполняет веб-API **ODataQueryOptions** строка запроса из URI.</span><span class="sxs-lookup"><span data-stu-id="a5455-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="a5455-200">Чтобы применить запрос, передайте **IQueryable** для **ApplyTo** метод.</span><span class="sxs-lookup"><span data-stu-id="a5455-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="a5455-201">Этот метод возвращает другой **IQueryable**.</span><span class="sxs-lookup"><span data-stu-id="a5455-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="a5455-202">Для более сложных сценариев, если у вас нет **IQueryable** поставщик запросов, можно изучить **ODataQueryOptions** и преобразование параметров запроса в другой форме.</span><span class="sxs-lookup"><span data-stu-id="a5455-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="a5455-203">(Например, см. в разделе блога RaghuRam Nadiminti [запросов преобразования OData в HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), также включает [пример](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span><span class="sxs-lookup"><span data-stu-id="a5455-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="a5455-204">Проверка запроса</span><span class="sxs-lookup"><span data-stu-id="a5455-204">Query Validation</span></span>

<span data-ttu-id="a5455-205">**[Queryable]** атрибут проверяет запрос перед его выполнением.</span><span class="sxs-lookup"><span data-stu-id="a5455-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="a5455-206">Действие проверки выполняется в **QueryableAttribute.ValidateQuery** метод.</span><span class="sxs-lookup"><span data-stu-id="a5455-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="a5455-207">Можно также настроить процесс проверки.</span><span class="sxs-lookup"><span data-stu-id="a5455-207">You can also customize the validation process.</span></span>

<span data-ttu-id="a5455-208">Также см. в разделе [рекомендации по безопасности OData](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="a5455-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="a5455-209">Во-первых, переопределение одного модуля проверки классы, то есть определенные в **Web.Http.OData.Query.Validators** пространства имен.</span><span class="sxs-lookup"><span data-stu-id="a5455-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="a5455-210">Например следующий класс проверяющего элемента управления отключает параметр «desc» для параметра $orderby.</span><span class="sxs-lookup"><span data-stu-id="a5455-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="a5455-211">Подкласс **[Queryable]** атрибута для переопределения **ValidateQuery** метод.</span><span class="sxs-lookup"><span data-stu-id="a5455-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="a5455-212">Задайте пользовательский атрибут либо глобально или на контроллер:</span><span class="sxs-lookup"><span data-stu-id="a5455-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="a5455-213">Если вы используете **ODataQueryOptions** напрямую, установить проверяющий элемент управления о параметрах:</span><span class="sxs-lookup"><span data-stu-id="a5455-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
