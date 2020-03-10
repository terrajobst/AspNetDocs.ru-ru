---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Наследование сложных типов в OData v4 с помощью веб-API ASP.NET | Документация Майкрософт
author: microsoft
description: В соответствии со спецификацией OData версии 4 сложный тип может наследовать от другого сложного типа. (Сложный тип — это структурированный тип без ключа.) Веб-API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448134"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="e683d-104">Наследование сложных типов в OData v4 с веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e683d-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="e683d-105">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e683d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e683d-106">В соответствии со [спецификацией](http://www.odata.org/documentation/odata-version-4-0/)OData версии 4 сложный тип может наследовать от другого сложного типа.</span><span class="sxs-lookup"><span data-stu-id="e683d-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="e683d-107">( *Сложный* тип — это структурированный тип без ключа.) Веб-API OData 5,3 поддерживает наследование сложного типа.</span><span class="sxs-lookup"><span data-stu-id="e683d-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="e683d-108">В этом разделе показано, как создать модель EDM со сложными типами наследования.</span><span class="sxs-lookup"><span data-stu-id="e683d-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="e683d-109">Полный исходный код см. в разделе [Пример наследования сложных типов OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="e683d-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e683d-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="e683d-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e683d-111">Веб-API OData 5,3</span><span class="sxs-lookup"><span data-stu-id="e683d-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="e683d-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="e683d-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="e683d-113">Иерархия модели</span><span class="sxs-lookup"><span data-stu-id="e683d-113">Model Hierarchy</span></span>

<span data-ttu-id="e683d-114">Чтобы продемонстрировать наследование сложного типа, мы будем использовать следующую иерархию классов.</span><span class="sxs-lookup"><span data-stu-id="e683d-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="e683d-115">`Shape` является абстрактным сложным типом.</span><span class="sxs-lookup"><span data-stu-id="e683d-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="e683d-116">`Rectangle`, `Triangle`и `Circle` являются сложными типами, производными от `Shape`, а `RoundRectangle` является производным от `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="e683d-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="e683d-117">`Window` является типом сущности и содержит экземпляр `Shape`.</span><span class="sxs-lookup"><span data-stu-id="e683d-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="e683d-118">Ниже приведены классы CLR, определяющие эти типы.</span><span class="sxs-lookup"><span data-stu-id="e683d-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="e683d-119">Построение модели EDM</span><span class="sxs-lookup"><span data-stu-id="e683d-119">Build the EDM Model</span></span>

<span data-ttu-id="e683d-120">Чтобы создать EDM, можно использовать **одатаконвентионмоделбуилдер**, который выводит отношения наследования от типов CLR.</span><span class="sxs-lookup"><span data-stu-id="e683d-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="e683d-121">Вы также можете создать EDM явным образом с помощью **одатамоделбуилдер**.</span><span class="sxs-lookup"><span data-stu-id="e683d-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="e683d-122">Это занимает больше кода, но обеспечивает более полный контроль над EDM.</span><span class="sxs-lookup"><span data-stu-id="e683d-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="e683d-123">Эти два примера создают одну и ту же схему EDM.</span><span class="sxs-lookup"><span data-stu-id="e683d-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="e683d-124">Документ метаданных</span><span class="sxs-lookup"><span data-stu-id="e683d-124">Metadata Document</span></span>

<span data-ttu-id="e683d-125">Ниже приведен документ метаданных OData, демонстрирующий наследование сложного типа.</span><span class="sxs-lookup"><span data-stu-id="e683d-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="e683d-126">Из документа метаданных можно увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="e683d-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="e683d-127">Сложный тип `Shape` является абстрактным.</span><span class="sxs-lookup"><span data-stu-id="e683d-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="e683d-128">`Rectangle`, `Triangle`и `Circle` сложного типа имеют базовый тип `Shape`.</span><span class="sxs-lookup"><span data-stu-id="e683d-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="e683d-129">Тип `RoundRectangle` имеет `Rectangle`базового типа.</span><span class="sxs-lookup"><span data-stu-id="e683d-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="e683d-130">Приведение сложных типов</span><span class="sxs-lookup"><span data-stu-id="e683d-130">Casting Complex Types</span></span>

<span data-ttu-id="e683d-131">Приведение типов в сложных типах теперь поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e683d-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="e683d-132">Например, следующий запрос приводит `Shape` к `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="e683d-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="e683d-133">Ниже приведены полезные данные ответа:</span><span class="sxs-lookup"><span data-stu-id="e683d-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
