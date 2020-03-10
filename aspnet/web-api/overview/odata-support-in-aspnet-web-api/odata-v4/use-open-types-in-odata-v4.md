---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Открытие типов в OData v4 с помощью веб-API ASP.NET | Документация Майкрософт
author: microsoft
description: В OData v4 открытый тип — это структурированный тип, который содержит динамические свойства в дополнение к любым свойствам, объявленным в определении типа. Открыть...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504582"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="0619e-104">Открытие типов в OData v4 с веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0619e-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="0619e-105">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0619e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0619e-106">В OData v4 *открытый тип* — это структурированный тип, который содержит динамические свойства в дополнение к любым свойствам, объявленным в определении типа.</span><span class="sxs-lookup"><span data-stu-id="0619e-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="0619e-107">Открытые типы позволяют повысить гибкость моделей данных.</span><span class="sxs-lookup"><span data-stu-id="0619e-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="0619e-108">В этом руководстве показано, как использовать открытые типы в веб-API ASP.NET OData.</span><span class="sxs-lookup"><span data-stu-id="0619e-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="0619e-109">В этом учебнике предполагается, что вы уже умеете создавать конечную точку OData в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0619e-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="0619e-110">Если это не так, начните с чтения сначала [Создайте конечную точку OData v4](create-an-odata-v4-endpoint.md) .</span><span class="sxs-lookup"><span data-stu-id="0619e-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0619e-111">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="0619e-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0619e-112">Веб-API OData 5,3</span><span class="sxs-lookup"><span data-stu-id="0619e-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="0619e-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="0619e-113">OData v4</span></span>

<span data-ttu-id="0619e-114">Во первых, некоторые термины OData:</span><span class="sxs-lookup"><span data-stu-id="0619e-114">First, some OData terminology:</span></span>

- <span data-ttu-id="0619e-115">Тип сущности — структурированный тип с ключом.</span><span class="sxs-lookup"><span data-stu-id="0619e-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="0619e-116">Сложный тип: структурированный тип без ключа.</span><span class="sxs-lookup"><span data-stu-id="0619e-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="0619e-117">Открыть тип: тип с динамическими свойствами.</span><span class="sxs-lookup"><span data-stu-id="0619e-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="0619e-118">Можно открыть как типы сущностей, так и сложные типы.</span><span class="sxs-lookup"><span data-stu-id="0619e-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="0619e-119">Значением динамического свойства может быть тип-примитив, сложный тип или тип перечисления. или коллекция любого из этих типов.</span><span class="sxs-lookup"><span data-stu-id="0619e-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="0619e-120">Дополнительные сведения об открытых типах см. в [спецификации OData v4](http://www.odata.org/documentation/odata-version-4-0/).</span><span class="sxs-lookup"><span data-stu-id="0619e-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="0619e-121">Установка библиотек веб-OData</span><span class="sxs-lookup"><span data-stu-id="0619e-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="0619e-122">Используйте диспетчер пакетов NuGet для установки последних библиотек веб-API OData.</span><span class="sxs-lookup"><span data-stu-id="0619e-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="0619e-123">В окне консоли диспетчера пакетов выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0619e-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="0619e-124">Определение типов CLR</span><span class="sxs-lookup"><span data-stu-id="0619e-124">Define the CLR Types</span></span>

<span data-ttu-id="0619e-125">Начните с определения моделей EDM в качестве типов CLR.</span><span class="sxs-lookup"><span data-stu-id="0619e-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="0619e-126">При создании EDM (EDM)</span><span class="sxs-lookup"><span data-stu-id="0619e-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="0619e-127">`Category` является типом перечисления.</span><span class="sxs-lookup"><span data-stu-id="0619e-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="0619e-128">`Address` является сложным типом.</span><span class="sxs-lookup"><span data-stu-id="0619e-128">`Address` is a complex type.</span></span> <span data-ttu-id="0619e-129">(У него нет ключа, поэтому он не является типом сущности.)</span><span class="sxs-lookup"><span data-stu-id="0619e-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="0619e-130">`Customer` является типом сущности.</span><span class="sxs-lookup"><span data-stu-id="0619e-130">`Customer` is an entity type.</span></span> <span data-ttu-id="0619e-131">(У него есть ключ.)</span><span class="sxs-lookup"><span data-stu-id="0619e-131">(It has a key.)</span></span>
- <span data-ttu-id="0619e-132">`Press` является открытым сложным типом.</span><span class="sxs-lookup"><span data-stu-id="0619e-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="0619e-133">`Book` является открытым типом сущности.</span><span class="sxs-lookup"><span data-stu-id="0619e-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="0619e-134">Для создания открытого типа тип CLR должен иметь свойство типа `IDictionary<string, object>`, которое содержит динамические свойства.</span><span class="sxs-lookup"><span data-stu-id="0619e-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="0619e-135">Построение модели EDM</span><span class="sxs-lookup"><span data-stu-id="0619e-135">Build the EDM Model</span></span>

<span data-ttu-id="0619e-136">Если для создания модели EDM используется **одатаконвентионмоделбуилдер** , то `Press` и `Book` автоматически добавляются как открытые типы в зависимости от наличия свойства `IDictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="0619e-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="0619e-137">Вы также можете создать EDM явным образом с помощью **одатамоделбуилдер**.</span><span class="sxs-lookup"><span data-stu-id="0619e-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="0619e-138">Добавление контроллера OData</span><span class="sxs-lookup"><span data-stu-id="0619e-138">Add an OData Controller</span></span>

<span data-ttu-id="0619e-139">Затем добавьте контроллер OData.</span><span class="sxs-lookup"><span data-stu-id="0619e-139">Next, add an OData controller.</span></span> <span data-ttu-id="0619e-140">В этом руководстве мы будем использовать упрощенный контроллер, который только поддерживает запросы GET и POST, и использует список в памяти для хранения сущностей.</span><span class="sxs-lookup"><span data-stu-id="0619e-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="0619e-141">Обратите внимание, что первый экземпляр `Book` не имеет динамических свойств.</span><span class="sxs-lookup"><span data-stu-id="0619e-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="0619e-142">Второй экземпляр `Book` имеет следующие динамические свойства:</span><span class="sxs-lookup"><span data-stu-id="0619e-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="0619e-143">"Published": тип-примитив</span><span class="sxs-lookup"><span data-stu-id="0619e-143">"Published": Primitive type</span></span>
- <span data-ttu-id="0619e-144">"Authors": Коллекция типов-примитивов</span><span class="sxs-lookup"><span data-stu-id="0619e-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="0619e-145">"Осеркатегориес": Коллекция типов перечисления.</span><span class="sxs-lookup"><span data-stu-id="0619e-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="0619e-146">Кроме того, свойство `Press` этого экземпляра `Book` имеет следующие динамические свойства:</span><span class="sxs-lookup"><span data-stu-id="0619e-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="0619e-147">"Блог": тип-примитив</span><span class="sxs-lookup"><span data-stu-id="0619e-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="0619e-148">"Address": сложный тип</span><span class="sxs-lookup"><span data-stu-id="0619e-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="0619e-149">Запрос метаданных</span><span class="sxs-lookup"><span data-stu-id="0619e-149">Query the Metadata</span></span>

<span data-ttu-id="0619e-150">Чтобы получить документ метаданных OData, отправьте запрос GET в `~/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="0619e-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="0619e-151">Текст ответа должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0619e-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="0619e-152">Из документа метаданных можно увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="0619e-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="0619e-153">Для типов `Book` и `Press` значение атрибута `OpenType` равно true.</span><span class="sxs-lookup"><span data-stu-id="0619e-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="0619e-154">Типы `Customer` и `Address` не имеют этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="0619e-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="0619e-155">Тип сущности `Book` имеет три объявленных свойства: ISBN, Title и Press.</span><span class="sxs-lookup"><span data-stu-id="0619e-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="0619e-156">Метаданные OData не включают свойство `Book.Properties` из класса CLR.</span><span class="sxs-lookup"><span data-stu-id="0619e-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="0619e-157">Аналогичным образом, `Press` сложного типа имеет только два объявленных свойства: Name и category.</span><span class="sxs-lookup"><span data-stu-id="0619e-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="0619e-158">Метаданные не включают свойство `Press.DynamicProperties` из класса CLR.</span><span class="sxs-lookup"><span data-stu-id="0619e-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="0619e-159">Запрос сущности</span><span class="sxs-lookup"><span data-stu-id="0619e-159">Query an Entity</span></span>

<span data-ttu-id="0619e-160">Чтобы получить книгу с ISBN-значением, равным "978-0-7356-7942-9", отправьте запрос GET в `~/Books('978-0-7356-7942-9')`.</span><span class="sxs-lookup"><span data-stu-id="0619e-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="0619e-161">Текст ответа должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0619e-161">The response body should look similar to the following.</span></span> <span data-ttu-id="0619e-162">(С отступом, чтобы сделать его более удобочитаемым.)</span><span class="sxs-lookup"><span data-stu-id="0619e-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="0619e-163">Обратите внимание, что динамические свойства включаются в строку с объявленными свойствами.</span><span class="sxs-lookup"><span data-stu-id="0619e-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="0619e-164">Публикация сущности</span><span class="sxs-lookup"><span data-stu-id="0619e-164">POST an Entity</span></span>

<span data-ttu-id="0619e-165">Чтобы добавить сущность Book, отправьте запрос POST в `~/Books`.</span><span class="sxs-lookup"><span data-stu-id="0619e-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="0619e-166">Клиент может задавать динамические свойства в полезных данных запроса.</span><span class="sxs-lookup"><span data-stu-id="0619e-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="0619e-167">Ниже приведен пример запроса.</span><span class="sxs-lookup"><span data-stu-id="0619e-167">Here is an example request.</span></span> <span data-ttu-id="0619e-168">Обратите внимание на свойства Price и published.</span><span class="sxs-lookup"><span data-stu-id="0619e-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="0619e-169">Если задать точку останова в методе контроллера, можно увидеть, что веб-API добавил эти свойства в словарь `Properties`.</span><span class="sxs-lookup"><span data-stu-id="0619e-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="0619e-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0619e-170">Additional Resources</span></span>

[<span data-ttu-id="0619e-171">Пример открытого типа OData</span><span class="sxs-lookup"><span data-stu-id="0619e-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
