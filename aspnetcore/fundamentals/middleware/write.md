---
title: Написание пользовательского ПО промежуточного слоя ASP.NET Core
author: rick-anderson
description: Узнайте, как написать пользовательское ПО промежуточного слоя ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 02/14/2019
uid: fundamentals/middleware/write
ms.openlocfilehash: 2c5577394a10370d92c8a83f9d806b63f3245c8b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046241"
---
# <a name="write-custom-aspnet-core-middleware"></a><span data-ttu-id="e4782-103">Написание пользовательского ПО промежуточного слоя ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e4782-103">Write custom ASP.NET Core middleware</span></span>

<span data-ttu-id="e4782-104">Авторы: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson) и [Стив Смит](https://ardalis.com/) (Steve Smith)</span><span class="sxs-lookup"><span data-stu-id="e4782-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="e4782-105">ПО промежуточного слоя — это программное обеспечение, выстраиваемое в виде конвейера приложения для обработки запросов и откликов.</span><span class="sxs-lookup"><span data-stu-id="e4782-105">Middleware is software that's assembled into an app pipeline to handle requests and responses.</span></span> <span data-ttu-id="e4782-106">ASP.NET Core предоставляет широкий набор встроенных компонентов ПО промежуточного слоя, но в некоторых случаях может потребоваться написать пользовательское ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="e4782-106">ASP.NET Core provides a rich set of built-in middleware components, but in some scenarios you might want to write a custom middleware.</span></span>

## <a name="middleware-class"></a><span data-ttu-id="e4782-107">Класс ПО промежуточного слоя</span><span class="sxs-lookup"><span data-stu-id="e4782-107">Middleware class</span></span>

<span data-ttu-id="e4782-108">ПО промежуточного слоя обычно инкапсулируется в класс и предоставляется с помощью метода расширения.</span><span class="sxs-lookup"><span data-stu-id="e4782-108">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="e4782-109">Рассмотрим следующее ПО промежуточного слоя, которое задает язык и региональные параметры для текущего запроса из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="e4782-109">Consider the following middleware, which sets the culture for the current request from a query string:</span></span>

[!code-csharp[](index/snapshot/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="e4782-110">Приведенный выше пример кода демонстрирует создание компонента промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="e4782-110">The preceding sample code is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="e4782-111">Дополнительные сведения о встроенной поддержке локализации в ASP.NET Core см. в разделе <xref:fundamentals/localization>.</span><span class="sxs-lookup"><span data-stu-id="e4782-111">For ASP.NET Core's built-in localization support, see <xref:fundamentals/localization>.</span></span>

<span data-ttu-id="e4782-112">Это ПО промежуточного слоя можно проверить, передав язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="e4782-112">You can test the middleware by passing in the culture.</span></span> <span data-ttu-id="e4782-113">Например, `http://localhost:7997/?culture=no`.</span><span class="sxs-lookup"><span data-stu-id="e4782-113">For example, `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="e4782-114">Следующий код перемещает делегат ПО промежуточного слоя в класс.</span><span class="sxs-lookup"><span data-stu-id="e4782-114">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddleware.cs)]

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e4782-115">Метод ПО промежуточного слоя `Task` должен иметь имя `Invoke`.</span><span class="sxs-lookup"><span data-stu-id="e4782-115">The middleware `Task` method's name must be `Invoke`.</span></span> <span data-ttu-id="e4782-116">В ASP.NET Core 2.0 и более поздних версиях имя может быть `Invoke` или `InvokeAsync`.</span><span class="sxs-lookup"><span data-stu-id="e4782-116">In ASP.NET Core 2.0 or later, the name can be either `Invoke` or `InvokeAsync`.</span></span>

::: moniker-end

## <a name="middleware-extension-method"></a><span data-ttu-id="e4782-117">Метод расширения ПО промежуточного слоя</span><span class="sxs-lookup"><span data-stu-id="e4782-117">Middleware extension method</span></span>

<span data-ttu-id="e4782-118">Следующий метод расширения предоставляет ПО промежуточного слоя посредством <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>:</span><span class="sxs-lookup"><span data-stu-id="e4782-118">The following extension method exposes the middleware through <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="e4782-119">Следующий код вызывает ПО промежуточного слоя из `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="e4782-119">The following code calls the middleware from `Startup.Configure`:</span></span>

[!code-csharp[](index/snapshot/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="e4782-120">ПО промежуточного слоя должно соответствовать [принципу явных зависимостей](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies), предоставляя свои зависимости в своем конструкторе.</span><span class="sxs-lookup"><span data-stu-id="e4782-120">Middleware should follow the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="e4782-121">ПО промежуточного слоя создается один раз за *время существования приложения*.</span><span class="sxs-lookup"><span data-stu-id="e4782-121">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="e4782-122">В разделе [Зависимости отдельных запросов](#per-request-dependencies) приведены сведения о том, как использовать службы совместно с ПО промежуточного слоя внутри запроса.</span><span class="sxs-lookup"><span data-stu-id="e4782-122">See the [Per-request dependencies](#per-request-dependencies) section if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="e4782-123">Компоненты промежуточного слоя могут разрешать свои зависимости, возникшие в результате [внедрения зависимостей](xref:fundamentals/dependency-injection), за счет параметров конструктора.</span><span class="sxs-lookup"><span data-stu-id="e4782-123">Middleware components can resolve their dependencies from [dependency injection (DI)](xref:fundamentals/dependency-injection) through constructor parameters.</span></span> <span data-ttu-id="e4782-124">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___) также может принимать дополнительные параметры напрямую.</span><span class="sxs-lookup"><span data-stu-id="e4782-124">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___) can also accept additional parameters directly.</span></span>

## <a name="per-request-dependencies"></a><span data-ttu-id="e4782-125">Зависимости отдельных запросов</span><span class="sxs-lookup"><span data-stu-id="e4782-125">Per-request dependencies</span></span>

<span data-ttu-id="e4782-126">Так как ПО промежуточного слоя создается при запуске приложения, а не для отдельных запросов, службы времени существования *scoped*, используемые конструкторами ПО промежуточного слоя, не являются общими с другими типами, возникшими в результате внедрения зависимостей, в каждом из запросов.</span><span class="sxs-lookup"><span data-stu-id="e4782-126">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors aren't shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="e4782-127">Если необходимо предоставить службу *scoped* для совместного использования ПО промежуточного слоя и другими типами, добавьте ее в сигнатуру метода `Invoke`.</span><span class="sxs-lookup"><span data-stu-id="e4782-127">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="e4782-128">Метод `Invoke` может принимать дополнительные параметры, заполняемые при внедрении зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e4782-128">The `Invoke` method can accept additional parameters that are populated by DI:</span></span>

```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    // IMyScopedService is injected into Invoke
    public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
    {
        svc.MyProperty = 1000;
        await _next(httpContext);
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="e4782-129">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e4782-129">Additional resources</span></span>

* <xref:fundamentals/middleware/index>
* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>
