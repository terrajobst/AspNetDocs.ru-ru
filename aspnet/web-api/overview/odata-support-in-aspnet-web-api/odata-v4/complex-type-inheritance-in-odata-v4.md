---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Наследование сложного типа в OData v4 с веб-API ASP.NET | Документация Майкрософт
author: microsoft
description: Согласно спецификации OData v4 сложный тип может наследовать от другого сложного типа. (Сложный тип является структурированного типа без ключа). Веб-API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 76db6325b8528af5b82ca3ea4e34284ca470ff6e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59378605"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="becdb-104">Наследование сложного типа в OData v4 с веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="becdb-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="becdb-105">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="becdb-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="becdb-106">В соответствии с OData v4 [спецификации](http://www.odata.org/documentation/odata-version-4-0/), сложный тип может наследовать от другого сложного типа.</span><span class="sxs-lookup"><span data-stu-id="becdb-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="becdb-107">(Объект *сложных* тип является типом структурированных без ключа.) Веб-API OData 5.3 поддерживает наследование сложного типа.</span><span class="sxs-lookup"><span data-stu-id="becdb-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="becdb-108">В этом разделе описывается создание entity data model (EDM) наследование сложных типов.</span><span class="sxs-lookup"><span data-stu-id="becdb-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="becdb-109">Полный исходный код, см. в разделе [OData сложный тип наследования пример](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="becdb-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="becdb-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="becdb-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="becdb-111">Веб-API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="becdb-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="becdb-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="becdb-112">OData v4</span></span>


## <a name="model-hierarchy"></a><span data-ttu-id="becdb-113">Иерархия модели</span><span class="sxs-lookup"><span data-stu-id="becdb-113">Model Hierarchy</span></span>

<span data-ttu-id="becdb-114">Чтобы продемонстрировать наследование сложного типа, мы будем использовать следующие иерархии классов.</span><span class="sxs-lookup"><span data-stu-id="becdb-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape` <span data-ttu-id="becdb-115">— Это абстрактный сложный тип.</span><span class="sxs-lookup"><span data-stu-id="becdb-115">is an abstract complex type.</span></span> `Rectangle`<span data-ttu-id="becdb-116">, `Triangle`, и `Circle` сложные типы являются производными от `Shape`, и `RoundRectangle` является производным от `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="becdb-116">, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> `Window` <span data-ttu-id="becdb-117">является типом сущности и содержит `Shape` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="becdb-117">is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="becdb-118">Ниже приведены классы CLR, которые определяют эти типы.</span><span class="sxs-lookup"><span data-stu-id="becdb-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="becdb-119">Создание модели EDM</span><span class="sxs-lookup"><span data-stu-id="becdb-119">Build the EDM Model</span></span>

<span data-ttu-id="becdb-120">Чтобы создать модель EDM, можно использовать **ODataConventionModelBuilder**, который выводит связи наследования из типов среды CLR.</span><span class="sxs-lookup"><span data-stu-id="becdb-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="becdb-121">Вы также можете создавать модели EDM явно, с помощью **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="becdb-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="becdb-122">Это занимает больше кода, но дает больший контроль над модели EDM.</span><span class="sxs-lookup"><span data-stu-id="becdb-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="becdb-123">Эти два примера создайте одну и ту же схему модели EDM.</span><span class="sxs-lookup"><span data-stu-id="becdb-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="becdb-124">Документ метаданных</span><span class="sxs-lookup"><span data-stu-id="becdb-124">Metadata Document</span></span>

<span data-ttu-id="becdb-125">Ниже приведен документ метаданных OData, показывающая наследование сложного типа.</span><span class="sxs-lookup"><span data-stu-id="becdb-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="becdb-126">Из документа метаданных можно увидеть, что:</span><span class="sxs-lookup"><span data-stu-id="becdb-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="becdb-127">`Shape` Сложный тип является абстрактным.</span><span class="sxs-lookup"><span data-stu-id="becdb-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="becdb-128">`Rectangle`, `Triangle`, И `Circle` сложный тип имеет базовый тип `Shape`.</span><span class="sxs-lookup"><span data-stu-id="becdb-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="becdb-129">`RoundRectangle` Тип имеет базовый тип `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="becdb-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="becdb-130">Приведение сложные типы</span><span class="sxs-lookup"><span data-stu-id="becdb-130">Casting Complex Types</span></span>

<span data-ttu-id="becdb-131">Теперь поддерживается приведение для сложных типов.</span><span class="sxs-lookup"><span data-stu-id="becdb-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="becdb-132">Например, следующий запрос приведения `Shape` для `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="becdb-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="becdb-133">Ниже приведен полезных данных ответа.</span><span class="sxs-lookup"><span data-stu-id="becdb-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
