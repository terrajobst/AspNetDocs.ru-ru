---
title: Типы возвращаемых значений действий контроллера в веб-API ASP.NET Core
author: scottaddie
description: Сведения об использовании различных типов возвращаемых значений методов действий контроллера в веб-API ASP.NET Core.
ms.author: scaddie
ms.custom: mvc
ms.date: 01/04/2019
uid: web-api/action-return-types
ms.openlocfilehash: 98d70e0379d353cff98a6d7a13f2dd00eb4da206
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047501"
---
# <a name="controller-action-return-types-in-aspnet-core-web-api"></a><span data-ttu-id="23289-103">Типы возвращаемых значений действий контроллера в веб-API ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="23289-103">Controller action return types in ASP.NET Core Web API</span></span>

<span data-ttu-id="23289-104">Автор: [Скотт Адди](https://github.com/scottaddie) (Scott Addie)</span><span class="sxs-lookup"><span data-stu-id="23289-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="23289-105">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/action-return-types/samples) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="23289-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/action-return-types/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="23289-106">ASP.NET Core предоставляет следующие параметры для типов возвращаемых значений действий контроллера веб-API:</span><span class="sxs-lookup"><span data-stu-id="23289-106">ASP.NET Core offers the following options for Web API controller action return types:</span></span>

::: moniker range=">= aspnetcore-2.1"

* [<span data-ttu-id="23289-107">Определенный тип</span><span class="sxs-lookup"><span data-stu-id="23289-107">Specific type</span></span>](#specific-type)
* [<span data-ttu-id="23289-108">IActionResult</span><span class="sxs-lookup"><span data-stu-id="23289-108">IActionResult</span></span>](#iactionresult-type)
* [<span data-ttu-id="23289-109">ActionResult\<T></span><span class="sxs-lookup"><span data-stu-id="23289-109">ActionResult\<T></span></span>](#actionresultt-type)

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

* [<span data-ttu-id="23289-110">Определенный тип</span><span class="sxs-lookup"><span data-stu-id="23289-110">Specific type</span></span>](#specific-type)
* [<span data-ttu-id="23289-111">IActionResult</span><span class="sxs-lookup"><span data-stu-id="23289-111">IActionResult</span></span>](#iactionresult-type)

::: moniker-end

<span data-ttu-id="23289-112">В этом документе объясняется, когда лучше использовать каждый тип возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="23289-112">This document explains when it's most appropriate to use each return type.</span></span>

## <a name="specific-type"></a><span data-ttu-id="23289-113">Определенный тип</span><span class="sxs-lookup"><span data-stu-id="23289-113">Specific type</span></span>

<span data-ttu-id="23289-114">Простейшее действие возвращает элементарный или сложный тип данных (например, `string` или пользовательский тип объекта).</span><span class="sxs-lookup"><span data-stu-id="23289-114">The simplest action returns a primitive or complex data type (for example, `string` or a custom object type).</span></span> <span data-ttu-id="23289-115">Рассмотрим следующее действие, которое возвращает коллекцию пользовательских объектов `Product`:</span><span class="sxs-lookup"><span data-stu-id="23289-115">Consider the following action, which returns a collection of custom `Product` objects:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_Get)]

<span data-ttu-id="23289-116">Если не известны условия, которые необходимо соблюдать при выполнении действия, конкретного типа будет достаточно.</span><span class="sxs-lookup"><span data-stu-id="23289-116">Without known conditions to safeguard against during action execution, returning a specific type could suffice.</span></span> <span data-ttu-id="23289-117">Предыдущее действие не принимает параметры, поэтому проверка ограничений параметров не требуется.</span><span class="sxs-lookup"><span data-stu-id="23289-117">The preceding action accepts no parameters, so parameter constraints validation isn't needed.</span></span>

<span data-ttu-id="23289-118">Если в действии необходимо учитывать известные условия, используется несколько путей возврата.</span><span class="sxs-lookup"><span data-stu-id="23289-118">When known conditions need to be accounted for in an action, multiple return paths are introduced.</span></span> <span data-ttu-id="23289-119">В этом случае рекомендуется комбинировать тип возвращаемого значения [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) с элементарным или сложным типом возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="23289-119">In such a case, it's common to mix an [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) return type with the primitive or complex return type.</span></span> <span data-ttu-id="23289-120">Для этого типа действия требуется [IActionResult](#iactionresult-type) или [ActionResult\<T >](#actionresultt-type).</span><span class="sxs-lookup"><span data-stu-id="23289-120">Either [IActionResult](#iactionresult-type) or [ActionResult\<T>](#actionresultt-type) are necessary to accommodate this type of action.</span></span>

## <a name="iactionresult-type"></a><span data-ttu-id="23289-121">Тип IActionResult</span><span class="sxs-lookup"><span data-stu-id="23289-121">IActionResult type</span></span>

<span data-ttu-id="23289-122">Тип возвращаемого значения [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult) можно использовать, если в действии возможно несколько типов возвращаемого значения [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult).</span><span class="sxs-lookup"><span data-stu-id="23289-122">The [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult) return type is appropriate when multiple [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) return types are possible in an action.</span></span> <span data-ttu-id="23289-123">Типы `ActionResult` представляют различные коды состояния HTTP.</span><span class="sxs-lookup"><span data-stu-id="23289-123">The `ActionResult` types represent various HTTP status codes.</span></span> <span data-ttu-id="23289-124">Некоторые наиболее распространенные типы возвращаемых значений из этой категории: [BadRequestResult](/dotnet/api/microsoft.aspnetcore.mvc.badrequestresult) (400) [NotFoundResult](/dotnet/api/microsoft.aspnetcore.mvc.notfoundresult) (404) и [OkObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.okobjectresult) (200).</span><span class="sxs-lookup"><span data-stu-id="23289-124">Some common return types falling into this category are [BadRequestResult](/dotnet/api/microsoft.aspnetcore.mvc.badrequestresult) (400), [NotFoundResult](/dotnet/api/microsoft.aspnetcore.mvc.notfoundresult) (404), and [OkObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.okobjectresult) (200).</span></span>

<span data-ttu-id="23289-125">Поскольку в действии есть несколько типов возвращаемого значения и путей, необходимо использовать атрибут [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute.-ctor).</span><span class="sxs-lookup"><span data-stu-id="23289-125">Because there are multiple return types and paths in the action, liberal use of the [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute.-ctor) attribute is necessary.</span></span> <span data-ttu-id="23289-126">Этот атрибут создает более описательные сведения об ответе для страниц справки API, создаваемых такими инструментами, как [Swagger](/aspnet/core/tutorials/web-api-help-pages-using-swagger).</span><span class="sxs-lookup"><span data-stu-id="23289-126">This attribute produces more descriptive response details for API help pages generated by tools like [Swagger](/aspnet/core/tutorials/web-api-help-pages-using-swagger).</span></span> <span data-ttu-id="23289-127">`[ProducesResponseType]` указывает известные типы и коды состояния HTTP, возвращаемые действием.</span><span class="sxs-lookup"><span data-stu-id="23289-127">`[ProducesResponseType]` indicates the known types and HTTP status codes to be returned by the action.</span></span>

### <a name="synchronous-action"></a><span data-ttu-id="23289-128">Синхронное действие</span><span class="sxs-lookup"><span data-stu-id="23289-128">Synchronous action</span></span>

<span data-ttu-id="23289-129">Рассмотрим следующее синхронное действие, в котором возможны два типа возвращаемых значений:</span><span class="sxs-lookup"><span data-stu-id="23289-129">Consider the following synchronous action in which there are two possible return types:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.Pre21/Controllers/ProductsController.cs?name=snippet_GetById&highlight=8,11)]

<span data-ttu-id="23289-130">В предыдущем действии возвращается код состояния 404, если продукт, представленный `id`, не существует в базовом хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="23289-130">In the preceding action, a 404 status code is returned when the product represented by `id` doesn't exist in the underlying data store.</span></span> <span data-ttu-id="23289-131">Вспомогательный метод [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) вызывается в качестве ярлыка для `return new NotFoundResult();`.</span><span class="sxs-lookup"><span data-stu-id="23289-131">The [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) helper method is invoked as a shortcut to `return new NotFoundResult();`.</span></span> <span data-ttu-id="23289-132">Если продукт существует, объект `Product`, представляющий полезные данные, возвращается с кодом состояния 200.</span><span class="sxs-lookup"><span data-stu-id="23289-132">If the product does exist, a `Product` object representing the payload is returned with a 200 status code.</span></span> <span data-ttu-id="23289-133">Вспомогательный метод [ОК](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) вызывается в качестве краткой формы `return new OkObjectResult(product);`.</span><span class="sxs-lookup"><span data-stu-id="23289-133">The [Ok](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) helper method is invoked as the shorthand form of `return new OkObjectResult(product);`.</span></span>

### <a name="asynchronous-action"></a><span data-ttu-id="23289-134">Асинхронное действие</span><span class="sxs-lookup"><span data-stu-id="23289-134">Asynchronous action</span></span>

<span data-ttu-id="23289-135">Рассмотрим следующее асинхронное действие, в котором возможны два типа возвращаемых значений:</span><span class="sxs-lookup"><span data-stu-id="23289-135">Consider the following asynchronous action in which there are two possible return types:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.Pre21/Controllers/ProductsController.cs?name=snippet_CreateAsync&highlight=8,13)]

<span data-ttu-id="23289-136">В приведенном выше коде:</span><span class="sxs-lookup"><span data-stu-id="23289-136">In the preceding code:</span></span>

* <span data-ttu-id="23289-137">Код состояния 400 ([BadRequest](xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest*)) возвращается средой выполнения ASP.NET Core, когда описание продукта содержит XYZ Widget.</span><span class="sxs-lookup"><span data-stu-id="23289-137">A 400 status code ([BadRequest](xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest*)) is returned by the ASP.NET Core runtime when the product description contains "XYZ Widget".</span></span>
* <span data-ttu-id="23289-138">Код состояния 201 генерируется методом [CreatedAtAction](xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction*) при создании продукта.</span><span class="sxs-lookup"><span data-stu-id="23289-138">A 201 status code is generated by the [CreatedAtAction](xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction*) method when a product is created.</span></span> <span data-ttu-id="23289-139">В этой ветви кода возвращается объект `Product`.</span><span class="sxs-lookup"><span data-stu-id="23289-139">In this code path, the `Product` object is returned.</span></span>

<span data-ttu-id="23289-140">Например, следующая модель указывает на то, что запросы должны включать свойства `Name` и `Description`.</span><span class="sxs-lookup"><span data-stu-id="23289-140">For example, the following model indicates that requests must include the `Name` and `Description` properties.</span></span> <span data-ttu-id="23289-141">Таким образом, если невозможно указать `Name` и `Description` в запросе, происходит сбой проверки модели.</span><span class="sxs-lookup"><span data-stu-id="23289-141">Therefore, failure to provide `Name` and `Description` in the request causes model validation to fail.</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.DataAccess/Models/Product.cs?name=snippet_ProductClass&highlight=5-6,8-9)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="23289-142">Если атрибут [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) применяется в ASP.NET Core версии 2.1 и выше, ошибки при проверке модели приводят к генерации кода состояния 400.</span><span class="sxs-lookup"><span data-stu-id="23289-142">If the [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) attribute in ASP.NET Core 2.1 or later  is applied, model validation errors result in a 400 status code.</span></span> <span data-ttu-id="23289-143">Дополнительные сведения см. в разделе [Автоматические отклики HTTP 400](xref:web-api/index#automatic-http-400-responses).</span><span class="sxs-lookup"><span data-stu-id="23289-143">For more information, see [Automatic HTTP 400 responses](xref:web-api/index#automatic-http-400-responses).</span></span>

## <a name="actionresultt-type"></a><span data-ttu-id="23289-144">Тип ActionResult\<T></span><span class="sxs-lookup"><span data-stu-id="23289-144">ActionResult\<T> type</span></span>

<span data-ttu-id="23289-145">ASP.NET Core 2.1 предоставляет тип возвращаемого значения [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1) для действий контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="23289-145">ASP.NET Core 2.1 introduces the [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1) return type for Web API controller actions.</span></span> <span data-ttu-id="23289-146">Он позволяет возвращать тип, производный от [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult), или [определенный тип](#specific-type).</span><span class="sxs-lookup"><span data-stu-id="23289-146">It enables you to return a type deriving from [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) or return a [specific type](#specific-type).</span></span> <span data-ttu-id="23289-147">`ActionResult<T>` имеет следующие преимущества по сравнению с [типом IActionResult](#iactionresult-type):</span><span class="sxs-lookup"><span data-stu-id="23289-147">`ActionResult<T>` offers the following benefits over the [IActionResult type](#iactionresult-type):</span></span>

* <span data-ttu-id="23289-148">Свойство `Type` атрибута [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute) можно исключить.</span><span class="sxs-lookup"><span data-stu-id="23289-148">The [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute) attribute's `Type` property can be excluded.</span></span> <span data-ttu-id="23289-149">Например, `[ProducesResponseType(200, Type = typeof(Product))]` упрощается до `[ProducesResponseType(200)]`.</span><span class="sxs-lookup"><span data-stu-id="23289-149">For example, `[ProducesResponseType(200, Type = typeof(Product))]` is simplified to `[ProducesResponseType(200)]`.</span></span> <span data-ttu-id="23289-150">Ожидаемый тип возвращаемого значения действия вместо этого выводится из `T` в `ActionResult<T>`.</span><span class="sxs-lookup"><span data-stu-id="23289-150">The action's expected return type is instead inferred from the `T` in `ActionResult<T>`.</span></span>
* <span data-ttu-id="23289-151">[Операторы неявного приведения](/dotnet/csharp/language-reference/keywords/implicit) поддерживают преобразование `T` и `ActionResult` в `ActionResult<T>`.</span><span class="sxs-lookup"><span data-stu-id="23289-151">[Implicit cast operators](/dotnet/csharp/language-reference/keywords/implicit) support the conversion of both `T` and `ActionResult` to `ActionResult<T>`.</span></span> <span data-ttu-id="23289-152">`T` преобразуется в [ObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.objectresult), то есть `return new ObjectResult(T);` упрощается до `return T;`.</span><span class="sxs-lookup"><span data-stu-id="23289-152">`T` converts to [ObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.objectresult), which means `return new ObjectResult(T);` is simplified to `return T;`.</span></span>

<span data-ttu-id="23289-153">C# не поддерживает операторы неявных приведений в интерфейсах.</span><span class="sxs-lookup"><span data-stu-id="23289-153">C# doesn't support implicit cast operators on interfaces.</span></span> <span data-ttu-id="23289-154">Следовательно, для преобразования в конкретный тип необходимо использовать `ActionResult<T>`.</span><span class="sxs-lookup"><span data-stu-id="23289-154">Consequently, conversion of the interface to a concrete type is necessary to use `ActionResult<T>`.</span></span> <span data-ttu-id="23289-155">Например, использование `IEnumerable` не работает в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="23289-155">For example, use of `IEnumerable` in the following example doesn't work:</span></span>

```csharp
[HttpGet]
public ActionResult<IEnumerable<Product>> Get()
{
    return _repository.GetProducts();
}
```

<span data-ttu-id="23289-156">Один из способов исправить приведенный выше код — возвратить `_repository.GetProducts().ToList();`.</span><span class="sxs-lookup"><span data-stu-id="23289-156">One option to fix the preceding code is to return `_repository.GetProducts().ToList();`.</span></span>

<span data-ttu-id="23289-157">Большинство действий имеют тип возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="23289-157">Most actions have a specific return type.</span></span> <span data-ttu-id="23289-158">При выполнении действия могут возникнуть непредвиденные условия, и в этом случае определенный тип не возвращается.</span><span class="sxs-lookup"><span data-stu-id="23289-158">Unexpected conditions can occur during action execution, in which case the specific type isn't returned.</span></span> <span data-ttu-id="23289-159">Например, входной параметр действия может не пройти проверку модели.</span><span class="sxs-lookup"><span data-stu-id="23289-159">For example, an action's input parameter may fail model validation.</span></span> <span data-ttu-id="23289-160">В этом случае обычно возвращается подходящий тип `ActionResult` вместо конкретного типа.</span><span class="sxs-lookup"><span data-stu-id="23289-160">In such a case, it's common to return the appropriate `ActionResult` type instead of the specific type.</span></span>

### <a name="synchronous-action"></a><span data-ttu-id="23289-161">Синхронное действие</span><span class="sxs-lookup"><span data-stu-id="23289-161">Synchronous action</span></span>

<span data-ttu-id="23289-162">Рассмотрим синхронное действие, в котором возможны два типа возвращаемых значений:</span><span class="sxs-lookup"><span data-stu-id="23289-162">Consider a synchronous action in which there are two possible return types:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_GetById&highlight=8,11)]

<span data-ttu-id="23289-163">В приведенном выше коде возвращается код состояния 404, если произведение не существует в базе данных.</span><span class="sxs-lookup"><span data-stu-id="23289-163">In the preceding code, a 404 status code is returned when the product doesn't exist in the database.</span></span> <span data-ttu-id="23289-164">Если произведение существует, возвращается соответствующий объект `Product`.</span><span class="sxs-lookup"><span data-stu-id="23289-164">If the product does exist, the corresponding `Product` object is returned.</span></span> <span data-ttu-id="23289-165">До версии ASP.NET Core 2.1 строка `return product;` имела бы вид `return Ok(product);`.</span><span class="sxs-lookup"><span data-stu-id="23289-165">Before ASP.NET Core 2.1, the `return product;` line would have been `return Ok(product);`.</span></span>

> [!TIP]
> <span data-ttu-id="23289-166">В версии ASP.NET Core 2.1 включен вывод источника привязки параметра действия, когда класс контроллера дополнен атрибутом `[ApiController]`.</span><span class="sxs-lookup"><span data-stu-id="23289-166">As of ASP.NET Core 2.1, action parameter binding source inference is enabled when a controller class is decorated with the `[ApiController]` attribute.</span></span> <span data-ttu-id="23289-167">Имя параметра, соответствующее имени в шаблоне маршрута, автоматически привязывается с помощью данных запроса маршрута.</span><span class="sxs-lookup"><span data-stu-id="23289-167">A parameter name matching a name in the route template is automatically bound using the request route data.</span></span> <span data-ttu-id="23289-168">В результате параметр предыдущего действия `id` явным образом не помечен атрибутом [[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute).</span><span class="sxs-lookup"><span data-stu-id="23289-168">Consequently, the preceding action's `id` parameter isn't explicitly annotated with the [[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute) attribute.</span></span>

### <a name="asynchronous-action"></a><span data-ttu-id="23289-169">Асинхронное действие</span><span class="sxs-lookup"><span data-stu-id="23289-169">Asynchronous action</span></span>

<span data-ttu-id="23289-170">Рассмотрим асинхронное действие, в котором возможны два типа возвращаемых значений:</span><span class="sxs-lookup"><span data-stu-id="23289-170">Consider an asynchronous action in which there are two possible return types:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_CreateAsync&highlight=8,13)]

<span data-ttu-id="23289-171">В приведенном выше коде:</span><span class="sxs-lookup"><span data-stu-id="23289-171">In the preceding code:</span></span>

* <span data-ttu-id="23289-172">Код состояния 400 ([BadRequest](xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest*)) возвращается средой выполнения ASP.NET Core, когда:</span><span class="sxs-lookup"><span data-stu-id="23289-172">A 400 status code ([BadRequest](xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest*)) is returned by the ASP.NET Core runtime when:</span></span>
  * <span data-ttu-id="23289-173">Атрибут [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) был применен и проверка модели не пройдена.</span><span class="sxs-lookup"><span data-stu-id="23289-173">The [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) attribute has been applied and model validation fails.</span></span>
  * <span data-ttu-id="23289-174">Описание продукта содержит XYZ Widget.</span><span class="sxs-lookup"><span data-stu-id="23289-174">The product description contains "XYZ Widget".</span></span>
* <span data-ttu-id="23289-175">Код состояния 201 генерируется методом [CreatedAtAction](xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction*) при создании продукта.</span><span class="sxs-lookup"><span data-stu-id="23289-175">A 201 status code is generated by the [CreatedAtAction](xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction*) method when a product is created.</span></span> <span data-ttu-id="23289-176">В этой ветви кода возвращается объект `Product`.</span><span class="sxs-lookup"><span data-stu-id="23289-176">In this code path, the `Product` object is returned.</span></span>

> [!TIP]
> <span data-ttu-id="23289-177">В версии ASP.NET Core 2.1 включен вывод источника привязки параметра действия, когда класс контроллера дополнен атрибутом `[ApiController]`.</span><span class="sxs-lookup"><span data-stu-id="23289-177">As of ASP.NET Core 2.1, action parameter binding source inference is enabled when a controller class is decorated with the `[ApiController]` attribute.</span></span> <span data-ttu-id="23289-178">Параметры сложного типа связываются автоматически с помощью текста запроса.</span><span class="sxs-lookup"><span data-stu-id="23289-178">Complex type parameters are automatically bound using the request body.</span></span> <span data-ttu-id="23289-179">В результате параметр предыдущего действия `product` явным образом не помечен атрибутом [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute).</span><span class="sxs-lookup"><span data-stu-id="23289-179">Consequently, the preceding action's `product` parameter isn't explicitly annotated with the [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute.</span></span>

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="23289-180">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="23289-180">Additional resources</span></span>

* <xref:mvc/controllers/actions>
* <xref:mvc/models/validation>
* <xref:tutorials/web-api-help-pages-using-swagger>
