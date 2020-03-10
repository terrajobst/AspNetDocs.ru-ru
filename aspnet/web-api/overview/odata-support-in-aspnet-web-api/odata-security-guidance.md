---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Руководство по безопасности для веб-API ASP.NET 2 OData-ASP.NET 4. x
author: MikeWasson
description: Описывает вопросы безопасности, которые следует учитывать при предоставлении набора данных через OData для веб-API ASP.NET 2 на ASP.NET 4. x.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448296"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="b57fa-103">Руководство по безопасности для веб-API ASP.NET 2 OData</span><span class="sxs-lookup"><span data-stu-id="b57fa-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="b57fa-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b57fa-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b57fa-105">В этом разделе описываются некоторые проблемы безопасности, которые следует учитывать при предоставлении набора данных через OData для веб-API ASP.NET 2 на ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="b57fa-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="b57fa-106">Безопасность EDM</span><span class="sxs-lookup"><span data-stu-id="b57fa-106">EDM Security</span></span>

<span data-ttu-id="b57fa-107">Семантика запросов основана на модели EDM, а не на базовых типах моделей.</span><span class="sxs-lookup"><span data-stu-id="b57fa-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="b57fa-108">Вы можете исключить свойство из модели EDM, и оно не будет видимо для запроса.</span><span class="sxs-lookup"><span data-stu-id="b57fa-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="b57fa-109">Например, предположим, что модель включает тип сотрудника со свойством оклада.</span><span class="sxs-lookup"><span data-stu-id="b57fa-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="b57fa-110">Может потребоваться исключить это свойство из EDM, чтобы скрыть его от клиентов.</span><span class="sxs-lookup"><span data-stu-id="b57fa-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="b57fa-111">Существует два способа исключить свойство из EDM.</span><span class="sxs-lookup"><span data-stu-id="b57fa-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="b57fa-112">Вы можете задать атрибут **[игноредатамембер]** для свойства в классе Model:</span><span class="sxs-lookup"><span data-stu-id="b57fa-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="b57fa-113">Также можно удалить свойство из модели EDM программным способом:</span><span class="sxs-lookup"><span data-stu-id="b57fa-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="b57fa-114">Безопасность запросов</span><span class="sxs-lookup"><span data-stu-id="b57fa-114">Query Security</span></span>

<span data-ttu-id="b57fa-115">Вредоносный или упрощенный клиент может создать запрос, выполнение которого занимает очень много времени.</span><span class="sxs-lookup"><span data-stu-id="b57fa-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="b57fa-116">В худшем случае это может нарушить доступ к службе.</span><span class="sxs-lookup"><span data-stu-id="b57fa-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="b57fa-117">Атрибут **[с поддержкой запроса]** — это фильтр действий, который анализирует, проверяет и применяет запрос.</span><span class="sxs-lookup"><span data-stu-id="b57fa-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="b57fa-118">Фильтр преобразует параметры запроса в выражение LINQ.</span><span class="sxs-lookup"><span data-stu-id="b57fa-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="b57fa-119">Когда контроллер OData возвращает тип **IQueryable** , поставщик **IQueryable** LINQ преобразует выражение LINQ в запрос.</span><span class="sxs-lookup"><span data-stu-id="b57fa-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="b57fa-120">Таким образом, производительность зависит от используемого поставщика LINQ, а также от конкретных характеристик набора данных или схемы базы данных.</span><span class="sxs-lookup"><span data-stu-id="b57fa-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="b57fa-121">Дополнительные сведения об использовании параметров запросов OData в веб-API ASP.NET см. в разделе [Поддержка параметров запросов OData](supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="b57fa-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="b57fa-122">Если известно, что все клиенты являются доверенными (например, в корпоративной среде) или если набор данных является небольшим, производительность запросов может быть не проблемой.</span><span class="sxs-lookup"><span data-stu-id="b57fa-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="b57fa-123">В противном случае следует принять во внимание следующие рекомендации.</span><span class="sxs-lookup"><span data-stu-id="b57fa-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="b57fa-124">Протестируйте службу с различными запросами и проверяйте базу данных.</span><span class="sxs-lookup"><span data-stu-id="b57fa-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="b57fa-125">Включите серверную подкачку, чтобы избежать возвращения большого набора данных в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="b57fa-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="b57fa-126">Дополнительные сведения см. в разделе [подкачка, управляемая сервером](supporting-odata-query-options.md#server-paging).</span><span class="sxs-lookup"><span data-stu-id="b57fa-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="b57fa-127">Требуется $filter и $orderby?</span><span class="sxs-lookup"><span data-stu-id="b57fa-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="b57fa-128">Некоторые приложения могут разрешать подкачку клиента с помощью $top и $skip, но отключать другие параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="b57fa-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="b57fa-129">Рекомендуется ограничивать $orderby свойствами в кластеризованном индексе.</span><span class="sxs-lookup"><span data-stu-id="b57fa-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="b57fa-130">Сортировка больших данных без кластеризованного индекса выполняется слишком долго.</span><span class="sxs-lookup"><span data-stu-id="b57fa-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="b57fa-131">Максимальное число узлов: свойство **макснодекаунт** в **[запрашиваемое]** задает максимальное число узлов, допустимых в дереве синтаксиса $Filter.</span><span class="sxs-lookup"><span data-stu-id="b57fa-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="b57fa-132">Значение по умолчанию — 100, но может потребоваться задать меньшее значение, так как большое количество узлов может замедляться для компиляции.</span><span class="sxs-lookup"><span data-stu-id="b57fa-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="b57fa-133">Это особенно справедливо при использовании LINQ to Objects (т. е. запросов LINQ к коллекции в памяти без использования промежуточного поставщика LINQ).</span><span class="sxs-lookup"><span data-stu-id="b57fa-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="b57fa-134">Рассмотрите возможность отключения функций Any () и All (), так как они могут быть слишком длительными.</span><span class="sxs-lookup"><span data-stu-id="b57fa-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="b57fa-135">Если какие-либо строковые свойства&#8212;содержат большие строки, например, описание продукта или запись&#8212;в блоге, попробуйте отключить строковые функции.</span><span class="sxs-lookup"><span data-stu-id="b57fa-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="b57fa-136">Рассмотрите возможность запрета фильтрации по свойствам навигации.</span><span class="sxs-lookup"><span data-stu-id="b57fa-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="b57fa-137">Фильтрация по свойствам навигации может привести к созданию объединения, которое может быть заработано в зависимости от схемы базы данных.</span><span class="sxs-lookup"><span data-stu-id="b57fa-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="b57fa-138">В следующем коде показан проверяющий элемент управления, который предотвращает фильтрацию свойств навигации.</span><span class="sxs-lookup"><span data-stu-id="b57fa-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="b57fa-139">Дополнительные сведения о средствах проверки запросов см. в разделе [Проверка запросов](supporting-odata-query-options.md#query-validation).</span><span class="sxs-lookup"><span data-stu-id="b57fa-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="b57fa-140">Рассмотрите возможность ограничивать $filter запросы, написав проверяющий элемент управления, настроенный для базы данных.</span><span class="sxs-lookup"><span data-stu-id="b57fa-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="b57fa-141">Например, рассмотрим следующие два запроса:</span><span class="sxs-lookup"><span data-stu-id="b57fa-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="b57fa-142">Все фильмы с субъектами, фамилии которых начинаются с "A".</span><span class="sxs-lookup"><span data-stu-id="b57fa-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="b57fa-143">Все фильмы, выпущенные в 1994.</span><span class="sxs-lookup"><span data-stu-id="b57fa-143">All movies released in 1994.</span></span>

    <span data-ttu-id="b57fa-144">Если фильмы не индексируются субъектами, для первого запроса может потребоваться, чтобы ядро СУБД проверяло весь список фильмов.</span><span class="sxs-lookup"><span data-stu-id="b57fa-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="b57fa-145">В то время как второй запрос может быть приемлемым, при условии, что фильмы индексируются по году выпуска.</span><span class="sxs-lookup"><span data-stu-id="b57fa-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="b57fa-146">В следующем коде показан проверяющий элемент управления, позволяющий фильтровать свойства "Релеасэйеар" и "Title", но не другие свойства.</span><span class="sxs-lookup"><span data-stu-id="b57fa-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="b57fa-147">Как правило, определите, какие функции $filter вам нужны.</span><span class="sxs-lookup"><span data-stu-id="b57fa-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="b57fa-148">Если клиентам не требуется полное выразительность $filter, можно ограничить разрешенные функции.</span><span class="sxs-lookup"><span data-stu-id="b57fa-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
