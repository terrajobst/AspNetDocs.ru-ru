---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Создание единственного элемента в OData v4 с помощью веб-API 2,2 | Документация Майкрософт
author: rick-anderson
description: В этом разделе показано, как определить одноэлементный экземпляр в конечной точке OData в веб-API 2,2.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504504"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="225d2-103">Создание единственного элемента в OData v4 с помощью веб-API 2,2</span><span class="sxs-lookup"><span data-stu-id="225d2-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="225d2-104">по Зое Луо</span><span class="sxs-lookup"><span data-stu-id="225d2-104">by Zoe Luo</span></span>

> <span data-ttu-id="225d2-105">Обычно доступ к сущности можно получить только в том случае, если она была инкапсулирована в набор сущностей.</span><span class="sxs-lookup"><span data-stu-id="225d2-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="225d2-106">Но OData v4 предоставляет два дополнительных параметра: Singleton и Contain, которые поддерживаются WebAPI 2,2.</span><span class="sxs-lookup"><span data-stu-id="225d2-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="225d2-107">В этой статье показано, как определить одноэлементный экземпляр в конечной точке OData в веб-API 2,2.</span><span class="sxs-lookup"><span data-stu-id="225d2-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="225d2-108">Сведения о том, что такое одноэлементное и в чем преимущества его использования, см. в разделе [Использование одноэлементного набора для определения особой сущности](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span><span class="sxs-lookup"><span data-stu-id="225d2-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="225d2-109">Чтобы создать конечную точку OData v4 в веб-API, см. раздел [Создание конечной точки OData v4 с помощью веб-API ASP.NET 2,2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="225d2-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="225d2-110">Мы создадим одноэлементный экземпляр в проекте веб-API, используя следующую модель данных:</span><span class="sxs-lookup"><span data-stu-id="225d2-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![Модель данных](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="225d2-112">Одноэлементное имя с именем `Umbrella` будет определено на основе типа `Company`, а набор сущностей с именем `Employees` будет определяться на основе типа `Employee`.</span><span class="sxs-lookup"><span data-stu-id="225d2-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="225d2-113">Решение, используемое в этом руководстве, можно скачать на [сайте CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span><span class="sxs-lookup"><span data-stu-id="225d2-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="225d2-114">Определение модели данных</span><span class="sxs-lookup"><span data-stu-id="225d2-114">Define the data model</span></span>

1. <span data-ttu-id="225d2-115">Определите типы CLR.</span><span class="sxs-lookup"><span data-stu-id="225d2-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="225d2-116">Создание модели EDM на основе типов CLR.</span><span class="sxs-lookup"><span data-stu-id="225d2-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="225d2-117">Здесь `builder.Singleton<Company>("Umbrella")` указывает построителю моделей создать одноэлементное множество с именем `Umbrella` в модели EDM.</span><span class="sxs-lookup"><span data-stu-id="225d2-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="225d2-118">Созданные метаданные будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="225d2-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="225d2-119">Из метаданных можно увидеть, что свойство навигации, `Company` в наборе сущностей `Employees`, привязано к `Umbrella`Singleton.</span><span class="sxs-lookup"><span data-stu-id="225d2-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="225d2-120">Привязка выполняется автоматически `ODataConventionModelBuilder`, так как только `Umbrella` имеет тип `Company`.</span><span class="sxs-lookup"><span data-stu-id="225d2-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="225d2-121">Если в модели имеется какая-либо неоднозначность, можно использовать `HasSingletonBinding`, чтобы явно привязать свойство навигации к одноэлементному экземпляру. `HasSingletonBinding` действует так же, как и атрибут `Singleton` в определении типа CLR:</span><span class="sxs-lookup"><span data-stu-id="225d2-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="225d2-122">Определение одноэлементного контроллера</span><span class="sxs-lookup"><span data-stu-id="225d2-122">Define the singleton controller</span></span>

<span data-ttu-id="225d2-123">Как и контроллер EntitySet, одноэлементный контроллер наследуется от `ODataController`, а имя одноэлементного контроллера должно быть `[singletonName]Controller`.</span><span class="sxs-lookup"><span data-stu-id="225d2-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="225d2-124">Для обработки различных типов запросов действия должны быть предварительно определены в контроллере.</span><span class="sxs-lookup"><span data-stu-id="225d2-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="225d2-125">**Маршрутизация атрибутов** включена по умолчанию в WebApi 2,2.</span><span class="sxs-lookup"><span data-stu-id="225d2-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="225d2-126">Например, чтобы определить действие по обработке запросов `Revenue` от `Company` с помощью маршрутизации атрибутов, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="225d2-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="225d2-127">Если вы не хотите определять атрибуты для каждого действия, просто определите действия, следующие за [соглашениями о маршрутизации OData](../odata-routing-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="225d2-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="225d2-128">Поскольку ключ не требуется для запроса одноэлементного экземпляра, действия, определенные в контроллере Singleton, немного отличаются от действий, определенных в контроллере EntitySet.</span><span class="sxs-lookup"><span data-stu-id="225d2-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="225d2-129">Для справки сигнатуры методов для каждого определения действия в одноэлементном контроллере перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="225d2-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="225d2-130">По сути, это все, что нужно сделать на стороне службы.</span><span class="sxs-lookup"><span data-stu-id="225d2-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="225d2-131">[Пример проекта](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) содержит весь код для решения и клиента OData, который показывает, как использовать Singleton.</span><span class="sxs-lookup"><span data-stu-id="225d2-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="225d2-132">Клиент создается, выполнив действия, описанные в разделе [Создание клиентского приложения OData для версии 4](create-an-odata-v4-client-app.md).</span><span class="sxs-lookup"><span data-stu-id="225d2-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="225d2-133">.</span><span class="sxs-lookup"><span data-stu-id="225d2-133">.</span></span> 

<span data-ttu-id="225d2-134">*Благодарим вас за первоначальное содержимое этой статьи, Leo Hu.*</span><span class="sxs-lookup"><span data-stu-id="225d2-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
