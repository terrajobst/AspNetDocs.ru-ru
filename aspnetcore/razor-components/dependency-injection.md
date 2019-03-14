---
title: Внедрение зависимостей компонентов Razor
author: guardrex
description: См. в разделе, как Blazor и Razor компоненты приложения могут использовать встроенные службы, внедряя их в компоненты.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/dependency-injection
ms.openlocfilehash: 6ce8fa74f20145f48797d267c20ef2593368b941
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042431"
---
# <a name="razor-components-dependency-injection"></a><span data-ttu-id="2ec90-103">Внедрение зависимостей компонентов Razor</span><span class="sxs-lookup"><span data-stu-id="2ec90-103">Razor Components dependency injection</span></span>

<span data-ttu-id="2ec90-104">По [Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="2ec90-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="2ec90-105">[Внедрение зависимостей (DI)](/aspnet/core/fundamentals/dependency-injection) является встроенной функцией.</span><span class="sxs-lookup"><span data-stu-id="2ec90-105">[Dependency injection (DI)](/aspnet/core/fundamentals/dependency-injection) is built-in.</span></span> <span data-ttu-id="2ec90-106">Приложения могут использовать встроенные службы, внедряя их в компоненты.</span><span class="sxs-lookup"><span data-stu-id="2ec90-106">Apps can use built-in services by having them injected into components.</span></span> <span data-ttu-id="2ec90-107">Приложения также можно определять пользовательские службы и сделать их доступными через внедрение Зависимостей.</span><span class="sxs-lookup"><span data-stu-id="2ec90-107">Apps can also define custom services and make them available via DI.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="2ec90-108">Внедрение зависимостей</span><span class="sxs-lookup"><span data-stu-id="2ec90-108">Dependency injection</span></span>

<span data-ttu-id="2ec90-109">Внедрение Зависимостей — это способ для доступа к службам, настроенным в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="2ec90-109">DI is a technique for accessing services configured in a central location.</span></span> <span data-ttu-id="2ec90-110">Это может быть полезно для:</span><span class="sxs-lookup"><span data-stu-id="2ec90-110">This can be useful to:</span></span>

* <span data-ttu-id="2ec90-111">Использовать один экземпляр класса службы многих компонентов (известный как *одноэлементный* службы).</span><span class="sxs-lookup"><span data-stu-id="2ec90-111">Share a single instance of a service class across many components (known as a *singleton* service).</span></span>
* <span data-ttu-id="2ec90-112">Отделять компоненты от конкретной службы конкретных классов и ссылаться только на абстракции.</span><span class="sxs-lookup"><span data-stu-id="2ec90-112">Decouple components from particular concrete service classes and only reference abstractions.</span></span> <span data-ttu-id="2ec90-113">Например, интерфейс `IDataAccess` реализуется конкретный класс `DataAccess`.</span><span class="sxs-lookup"><span data-stu-id="2ec90-113">For example, an interface `IDataAccess` is implemented by a concrete class `DataAccess`.</span></span> <span data-ttu-id="2ec90-114">Когда компонент использует внедрения Зависимостей для получения `IDataAccess` реализации, компонент не связан с конкретным типом.</span><span class="sxs-lookup"><span data-stu-id="2ec90-114">When a component uses DI to receive an `IDataAccess` implementation, the component isn't coupled to the concrete type.</span></span> <span data-ttu-id="2ec90-115">Реализацию можно переключать, возможно для реализации макетов в модульных тестах.</span><span class="sxs-lookup"><span data-stu-id="2ec90-115">The implementation can be swapped, perhaps to a mock implementation in unit tests.</span></span>

<span data-ttu-id="2ec90-116">В системе внедрения Зависимостей отвечает за предоставление экземпляров служб компонентов.</span><span class="sxs-lookup"><span data-stu-id="2ec90-116">The DI system is responsible for supplying instances of services to components.</span></span> <span data-ttu-id="2ec90-117">Внедрение Зависимостей также позволяет устранить зависимости рекурсивно сами службы может зависеть от дополнительной службы.</span><span class="sxs-lookup"><span data-stu-id="2ec90-117">DI also resolves dependencies recursively so that services themselves can depend on further services.</span></span> <span data-ttu-id="2ec90-118">DI настраивается во время запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="2ec90-118">DI is configured during startup of the app.</span></span> <span data-ttu-id="2ec90-119">Пример показан далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="2ec90-119">An example is shown later in this topic.</span></span>

## <a name="add-services-to-di"></a><span data-ttu-id="2ec90-120">Добавление служб для внедрения Зависимостей</span><span class="sxs-lookup"><span data-stu-id="2ec90-120">Add services to DI</span></span>

<span data-ttu-id="2ec90-121">После создания нового приложения, изучите `Startup.ConfigureServices` метод:</span><span class="sxs-lookup"><span data-stu-id="2ec90-121">After creating a new app, examine the `Startup.ConfigureServices` method:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

<span data-ttu-id="2ec90-122">`ConfigureServices` Методу передается [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), являющимся списком объектов дескриптора службы ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span><span class="sxs-lookup"><span data-stu-id="2ec90-122">The `ConfigureServices` method is passed an [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), which is a list of service descriptor objects ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span></span> <span data-ttu-id="2ec90-123">Службы добавляются, предоставляя дескрипторов службы для службы коллекции.</span><span class="sxs-lookup"><span data-stu-id="2ec90-123">Services are added by providing service descriptors to the service collection.</span></span> <span data-ttu-id="2ec90-124">В следующем образце кода показано концепции:</span><span class="sxs-lookup"><span data-stu-id="2ec90-124">The following code sample demonstrates the concept:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

<span data-ttu-id="2ec90-125">Службы можно настроить следующие параметры времени существования:</span><span class="sxs-lookup"><span data-stu-id="2ec90-125">Services can be configured with the following lifetimes:</span></span>

| <span data-ttu-id="2ec90-126">Метод</span><span class="sxs-lookup"><span data-stu-id="2ec90-126">Method</span></span>      | <span data-ttu-id="2ec90-127">Описание</span><span class="sxs-lookup"><span data-stu-id="2ec90-127">Description</span></span> |
| ----------- | ----------- |
| [<span data-ttu-id="2ec90-128">Одноэлементные</span><span class="sxs-lookup"><span data-stu-id="2ec90-128">Singleton</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | <span data-ttu-id="2ec90-129">Создает DI *единственных* службы.</span><span class="sxs-lookup"><span data-stu-id="2ec90-129">DI creates a *single instance* of the service.</span></span> <span data-ttu-id="2ec90-130">Все компоненты, требующие эта служба получена ссылка на этот экземпляр.</span><span class="sxs-lookup"><span data-stu-id="2ec90-130">All components requiring this service receive a reference to this instance.</span></span> |
| [<span data-ttu-id="2ec90-131">Временный</span><span class="sxs-lookup"><span data-stu-id="2ec90-131">Transient</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | <span data-ttu-id="2ec90-132">Каждый раз, когда эта служба необходима для компонента, он получает *новый экземпляр* службы.</span><span class="sxs-lookup"><span data-stu-id="2ec90-132">Whenever a component requires this service, it receives a *new instance* of the service.</span></span> |
| [<span data-ttu-id="2ec90-133">Ограниченный областью</span><span class="sxs-lookup"><span data-stu-id="2ec90-133">Scoped</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | <span data-ttu-id="2ec90-134">В настоящее время понятие областей внедрения Зависимостей не имеет Blazor на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="2ec90-134">Client-side Blazor doesn't currently have the concept of DI scopes.</span></span> <span data-ttu-id="2ec90-135">`Scoped` ведет себя как `Singleton`.</span><span class="sxs-lookup"><span data-stu-id="2ec90-135">`Scoped` behaves like `Singleton`.</span></span> <span data-ttu-id="2ec90-136">Тем не менее, ASP.NET Core Razor компоненты поддерживают `Scoped` времени существования.</span><span class="sxs-lookup"><span data-stu-id="2ec90-136">However, ASP.NET Core Razor Components support the `Scoped` lifetime.</span></span> <span data-ttu-id="2ec90-137">В компоненте Razor регистрация службы с заданной областью, ограничиваются соединения.</span><span class="sxs-lookup"><span data-stu-id="2ec90-137">In a Razor Component, a scoped service registration is scoped to the connection.</span></span> <span data-ttu-id="2ec90-138">По этой причине использование ограниченных служб является предпочтительным для служб, которые должны быть привязаны к текущему пользователю (даже если текущий предполагается выполняемых на стороне клиента в браузере).</span><span class="sxs-lookup"><span data-stu-id="2ec90-138">For this reason, using scoped services is preferred for services that should be scoped to the current user (even if the current intent is to run client-side in the browser).</span></span> |

<span data-ttu-id="2ec90-139">DI система основана на системе внедрения Зависимостей в ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2ec90-139">The DI system is based on the DI system in ASP.NET Core.</span></span> <span data-ttu-id="2ec90-140">Дополнительные сведения см. в разделе [внедрение зависимостей в ASP.NET Core](/aspnet/core/fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="2ec90-140">For more information, see [Dependency injection in ASP.NET Core](/aspnet/core/fundamentals/dependency-injection).</span></span>

## <a name="default-services"></a><span data-ttu-id="2ec90-141">Службы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2ec90-141">Default services</span></span>

<span data-ttu-id="2ec90-142">Службы по умолчанию автоматически добавляются в коллекцию службы приложения.</span><span class="sxs-lookup"><span data-stu-id="2ec90-142">Default services are automatically added to the service collection of an app.</span></span> <span data-ttu-id="2ec90-143">Ниже приведены некоторые полезные значения по умолчанию служб, предоставляемых.</span><span class="sxs-lookup"><span data-stu-id="2ec90-143">The following table shows some of the useful default services provided.</span></span>

| <span data-ttu-id="2ec90-144">Метод</span><span class="sxs-lookup"><span data-stu-id="2ec90-144">Method</span></span>       | <span data-ttu-id="2ec90-145">Описание:</span><span class="sxs-lookup"><span data-stu-id="2ec90-145">Description</span></span> |
| ------------ | ----------- |
| [<span data-ttu-id="2ec90-146">HttpClient</span><span class="sxs-lookup"><span data-stu-id="2ec90-146">HttpClient</span></span>](/dotnet/api/system.net.http.httpclient) | <span data-ttu-id="2ec90-147">Предоставляет методы для отправки HTTP-запросов и получения HTTP-ответов от ресурса с заданным URI (единственного экземпляра).</span><span class="sxs-lookup"><span data-stu-id="2ec90-147">Provides methods for sending HTTP requests and receiving HTTP responses from a resource identified by a URI (singleton).</span></span> <span data-ttu-id="2ec90-148">Обратите внимание, что этот экземпляр `HttpClient` использует браузер для обработки трафика HTTP в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="2ec90-148">Note that this instance of `HttpClient` uses the browser for handling the HTTP traffic in the background.</span></span> <span data-ttu-id="2ec90-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) автоматически присваивается базовый префикс URI приложения.</span><span class="sxs-lookup"><span data-stu-id="2ec90-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) is automatically set to the base URI prefix of the app.</span></span> <span data-ttu-id="2ec90-150">`HttpClient` предоставляется только для приложений Blazor на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="2ec90-150">`HttpClient` is only provided to client-side Blazor apps.</span></span> |
| `IJSRuntime` | <span data-ttu-id="2ec90-151">Представляет экземпляр среды выполнения JavaScript, на который может быть отправлен вызовов.</span><span class="sxs-lookup"><span data-stu-id="2ec90-151">Represents an instance of a JavaScript runtime to which calls may be dispatched.</span></span> <span data-ttu-id="2ec90-152">Дополнительные сведения см. в разделе <xref:razor-components/javascript-interop>.</span><span class="sxs-lookup"><span data-stu-id="2ec90-152">For more information, see <xref:razor-components/javascript-interop>.</span></span> |
| `IUriHelper` | <span data-ttu-id="2ec90-153">Вспомогательные функции для работы с состоянием URI и навигации (единственного экземпляра).</span><span class="sxs-lookup"><span data-stu-id="2ec90-153">Helpers for working with URIs and navigation state (singleton).</span></span> <span data-ttu-id="2ec90-154">`IUriHelper` предоставляется клиентских Blazor и ASP.NET Core Razor компонентов приложений.</span><span class="sxs-lookup"><span data-stu-id="2ec90-154">`IUriHelper` is provided to both client-side Blazor and ASP.NET Core Razor Components apps.</span></span> |

<span data-ttu-id="2ec90-155">Обратите внимание, что можно использовать поставщик пользовательских служб вместо поставщика службы по умолчанию, который добавляется с помощью шаблона по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2ec90-155">Note that it is possible to use a custom services provider instead of the default service provider that's added by the default template.</span></span> <span data-ttu-id="2ec90-156">Поставщик пользовательская служба не предоставляет автоматически службы по умолчанию, перечисленных в таблице.</span><span class="sxs-lookup"><span data-stu-id="2ec90-156">A custom service provider doesn't automatically provide the default services listed in the table.</span></span> <span data-ttu-id="2ec90-157">Эти службы необходимо явно добавить нового поставщика служб.</span><span class="sxs-lookup"><span data-stu-id="2ec90-157">Those services must be added to the new service provider explicitly.</span></span>

## <a name="request-a-service-in-a-component"></a><span data-ttu-id="2ec90-158">Запрос службы в компоненте</span><span class="sxs-lookup"><span data-stu-id="2ec90-158">Request a service in a component</span></span>

<span data-ttu-id="2ec90-159">Когда службы добавляются в коллекцию служб, они могут внедряться в шаблоны Razor компонентов с помощью `@inject` директивы Razor.</span><span class="sxs-lookup"><span data-stu-id="2ec90-159">Once services are added to the service collection, they can be injected into the components' Razor templates using the `@inject` Razor directive.</span></span> <span data-ttu-id="2ec90-160">`@inject` имеет два параметра:</span><span class="sxs-lookup"><span data-stu-id="2ec90-160">`@inject` has two parameters:</span></span>

* <span data-ttu-id="2ec90-161">Имя типа: Тип службы для вставки.</span><span class="sxs-lookup"><span data-stu-id="2ec90-161">Type name: The type of the service to inject.</span></span>
* <span data-ttu-id="2ec90-162">Имя свойства: Имя свойства, получение внедренного приложения службы.</span><span class="sxs-lookup"><span data-stu-id="2ec90-162">Property name: The name of the property receiving the injected app service.</span></span> <span data-ttu-id="2ec90-163">Обратите внимание на то, что свойство не требует создания вручную.</span><span class="sxs-lookup"><span data-stu-id="2ec90-163">Note that the property doesn't require manual creation.</span></span> <span data-ttu-id="2ec90-164">Компилятор создает свойства.</span><span class="sxs-lookup"><span data-stu-id="2ec90-164">The compiler creates the property.</span></span>

<span data-ttu-id="2ec90-165">Несколько `@inject` операторы могут использоваться для добавления различных служб.</span><span class="sxs-lookup"><span data-stu-id="2ec90-165">Multiple `@inject` statements can be used to inject different services.</span></span>

<span data-ttu-id="2ec90-166">В следующем примере показано, как использовать `@inject`.</span><span class="sxs-lookup"><span data-stu-id="2ec90-166">The following example shows how to use `@inject`.</span></span> <span data-ttu-id="2ec90-167">Реализация службы `Services.IDataAccess` вставляется в свойство компонента `DataRepository`.</span><span class="sxs-lookup"><span data-stu-id="2ec90-167">The service implementing `Services.IDataAccess` is injected into the component's property `DataRepository`.</span></span> <span data-ttu-id="2ec90-168">Обратите внимание на то, как код использует только `IDataAccess` абстракции:</span><span class="sxs-lookup"><span data-stu-id="2ec90-168">Note how the code is only using the `IDataAccess` abstraction:</span></span>

```csharp
@page "/customer-list"
@using Services
@inject IDataAccess DataRepository

<ul>
    @if (Customers != null)
    {
        @foreach (var customer in Customers)
        {
            <li>@customer.FirstName @customer.LastName</li>
        }
    }
</ul>

@functions {
    private IReadOnlyList<Customer> Customers;

    protected override async Task OnInitAsync()
    {
        // The property DataRepository received an implementation
        // of IDataAccess through dependency injection. Use 
        // DataRepository to obtain data from the server.
        Customers = await DataRepository.GetAllCustomersAsync();
    }
}
```

<span data-ttu-id="2ec90-169">На внутреннем уровне созданное свойство (`DataRepository`) снабжен `InjectAttribute` атрибута.</span><span class="sxs-lookup"><span data-stu-id="2ec90-169">Internally, the generated property (`DataRepository`) is decorated with the `InjectAttribute` attribute.</span></span> <span data-ttu-id="2ec90-170">Как правило этот атрибут не используется напрямую.</span><span class="sxs-lookup"><span data-stu-id="2ec90-170">Typically, this attribute isn't used directly.</span></span> <span data-ttu-id="2ec90-171">Если базовый класс является обязательным для компонентов и внедренного свойства также требуются для базового класса, `InjectAttribute` можно добавлять вручную:</span><span class="sxs-lookup"><span data-stu-id="2ec90-171">If a base class is required for components and injected properties are also required for the base class, `InjectAttribute` can be manually added:</span></span>

```csharp
public class ComponentBase : BlazorComponent
{
    // Dependency injection works even if using the
    // InjectAttribute in a component's base class.
    [Inject]
    protected IDataAccess DataRepository { get; set; }
    ...
}
```

<span data-ttu-id="2ec90-172">В компонентах, производный от базового класса `@inject` директива не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="2ec90-172">In components derived from the base class, the `@inject` directive isn't required.</span></span> <span data-ttu-id="2ec90-173">`InjectAttribute` Базового класса достаточно:</span><span class="sxs-lookup"><span data-stu-id="2ec90-173">The `InjectAttribute` of the base class is sufficient:</span></span>

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a><span data-ttu-id="2ec90-174">Внедрение зависимостей в службах</span><span class="sxs-lookup"><span data-stu-id="2ec90-174">Dependency injection in services</span></span>

<span data-ttu-id="2ec90-175">Сложные служб требуются дополнительные службы.</span><span class="sxs-lookup"><span data-stu-id="2ec90-175">Complex services might require additional services.</span></span> <span data-ttu-id="2ec90-176">В предыдущем примере `DataAccess` может потребоваться `HttpClient` службу по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2ec90-176">In the prior example, `DataAccess` might require the `HttpClient` default service.</span></span> <span data-ttu-id="2ec90-177">`@inject` или `InjectAttribute` не может использоваться в службах.</span><span class="sxs-lookup"><span data-stu-id="2ec90-177">`@inject` or the `InjectAttribute` can't be used in services.</span></span> <span data-ttu-id="2ec90-178">*Внедрение через конструктор* следует использовать.</span><span class="sxs-lookup"><span data-stu-id="2ec90-178">*Constructor injection* must be used instead.</span></span> <span data-ttu-id="2ec90-179">Путем добавления параметров в конструкторе службы добавляются необходимые службы.</span><span class="sxs-lookup"><span data-stu-id="2ec90-179">Required services are added by adding parameters to the service's constructor.</span></span> <span data-ttu-id="2ec90-180">Когда внедрение зависимостей создает службу, он распознает служб ему необходим в конструкторе и предоставляет их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="2ec90-180">When dependency injection creates the service, it recognizes the services it requires in the constructor and provides them accordingly.</span></span>

<span data-ttu-id="2ec90-181">В следующем образце кода показано концепции:</span><span class="sxs-lookup"><span data-stu-id="2ec90-181">The following code sample demonstrates the concept:</span></span>

```csharp
public class DataAccess : IDataAccess
{
    // The constructor receives an HttpClient via dependency
    // injection. HttpClient is a default service.
    public DataAccess(HttpClient client)
    {
        ...
    }
    ...
}
```

<span data-ttu-id="2ec90-182">Обратите внимание, указанных ниже необходимых для внедрения через конструктор:</span><span class="sxs-lookup"><span data-stu-id="2ec90-182">Note the following prerequisites for constructor injection:</span></span>

* <span data-ttu-id="2ec90-183">Должен быть хотя бы один конструктор, аргументы которых все выполнения может использоваться внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="2ec90-183">There must be one constructor whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="2ec90-184">Обратите внимание, что дополнительные параметры, не охваченных DI разрешены в том случае, если для них указаны значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2ec90-184">Note that additional parameters not covered by DI are allowed if default values are specified for them.</span></span>
* <span data-ttu-id="2ec90-185">Соответствующий конструктор должен быть *открытый*.</span><span class="sxs-lookup"><span data-stu-id="2ec90-185">The applicable constructor must be *public*.</span></span>
* <span data-ttu-id="2ec90-186">Должно существовать только один соответствующий конструктор.</span><span class="sxs-lookup"><span data-stu-id="2ec90-186">There must only be one applicable constructor.</span></span> <span data-ttu-id="2ec90-187">В случае неоднозначности DI вызывает исключение.</span><span class="sxs-lookup"><span data-stu-id="2ec90-187">In case of an ambiguity, DI throws an exception.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ec90-188">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2ec90-188">Additional resources</span></span>

* [<span data-ttu-id="2ec90-189">Внедрение зависимостей в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2ec90-189">Dependency injection in ASP.NET Core</span></span>](/aspnet/core/fundamentals/dependency-injection)
