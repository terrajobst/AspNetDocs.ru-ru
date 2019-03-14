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
# <a name="razor-components-dependency-injection"></a>Внедрение зависимостей компонентов Razor

По [Rainer Stropek](https://www.timecockpit.com)

[Внедрение зависимостей (DI)](/aspnet/core/fundamentals/dependency-injection) является встроенной функцией. Приложения могут использовать встроенные службы, внедряя их в компоненты. Приложения также можно определять пользовательские службы и сделать их доступными через внедрение Зависимостей.

## <a name="dependency-injection"></a>Внедрение зависимостей

Внедрение Зависимостей — это способ для доступа к службам, настроенным в центральном расположении. Это может быть полезно для:

* Использовать один экземпляр класса службы многих компонентов (известный как *одноэлементный* службы).
* Отделять компоненты от конкретной службы конкретных классов и ссылаться только на абстракции. Например, интерфейс `IDataAccess` реализуется конкретный класс `DataAccess`. Когда компонент использует внедрения Зависимостей для получения `IDataAccess` реализации, компонент не связан с конкретным типом. Реализацию можно переключать, возможно для реализации макетов в модульных тестах.

В системе внедрения Зависимостей отвечает за предоставление экземпляров служб компонентов. Внедрение Зависимостей также позволяет устранить зависимости рекурсивно сами службы может зависеть от дополнительной службы. DI настраивается во время запуска приложения. Пример показан далее в этом разделе.

## <a name="add-services-to-di"></a>Добавление служб для внедрения Зависимостей

После создания нового приложения, изучите `Startup.ConfigureServices` метод:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

`ConfigureServices` Методу передается [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), являющимся списком объектов дескриптора службы ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)). Службы добавляются, предоставляя дескрипторов службы для службы коллекции. В следующем образце кода показано концепции:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

Службы можно настроить следующие параметры времени существования:

| Метод      | Описание |
| ----------- | ----------- |
| [Одноэлементные](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | Создает DI *единственных* службы. Все компоненты, требующие эта служба получена ссылка на этот экземпляр. |
| [Временный](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | Каждый раз, когда эта служба необходима для компонента, он получает *новый экземпляр* службы. |
| [Ограниченный областью](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | В настоящее время понятие областей внедрения Зависимостей не имеет Blazor на стороне клиента. `Scoped` ведет себя как `Singleton`. Тем не менее, ASP.NET Core Razor компоненты поддерживают `Scoped` времени существования. В компоненте Razor регистрация службы с заданной областью, ограничиваются соединения. По этой причине использование ограниченных служб является предпочтительным для служб, которые должны быть привязаны к текущему пользователю (даже если текущий предполагается выполняемых на стороне клиента в браузере). |

DI система основана на системе внедрения Зависимостей в ASP.NET Core. Дополнительные сведения см. в разделе [внедрение зависимостей в ASP.NET Core](/aspnet/core/fundamentals/dependency-injection).

## <a name="default-services"></a>Службы по умолчанию

Службы по умолчанию автоматически добавляются в коллекцию службы приложения. Ниже приведены некоторые полезные значения по умолчанию служб, предоставляемых.

| Метод       | Описание: |
| ------------ | ----------- |
| [HttpClient](/dotnet/api/system.net.http.httpclient) | Предоставляет методы для отправки HTTP-запросов и получения HTTP-ответов от ресурса с заданным URI (единственного экземпляра). Обратите внимание, что этот экземпляр `HttpClient` использует браузер для обработки трафика HTTP в фоновом режиме. [HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) автоматически присваивается базовый префикс URI приложения. `HttpClient` предоставляется только для приложений Blazor на стороне клиента. |
| `IJSRuntime` | Представляет экземпляр среды выполнения JavaScript, на который может быть отправлен вызовов. Дополнительные сведения см. в разделе <xref:razor-components/javascript-interop>. |
| `IUriHelper` | Вспомогательные функции для работы с состоянием URI и навигации (единственного экземпляра). `IUriHelper` предоставляется клиентских Blazor и ASP.NET Core Razor компонентов приложений. |

Обратите внимание, что можно использовать поставщик пользовательских служб вместо поставщика службы по умолчанию, который добавляется с помощью шаблона по умолчанию. Поставщик пользовательская служба не предоставляет автоматически службы по умолчанию, перечисленных в таблице. Эти службы необходимо явно добавить нового поставщика служб.

## <a name="request-a-service-in-a-component"></a>Запрос службы в компоненте

Когда службы добавляются в коллекцию служб, они могут внедряться в шаблоны Razor компонентов с помощью `@inject` директивы Razor. `@inject` имеет два параметра:

* Имя типа: Тип службы для вставки.
* Имя свойства: Имя свойства, получение внедренного приложения службы. Обратите внимание на то, что свойство не требует создания вручную. Компилятор создает свойства.

Несколько `@inject` операторы могут использоваться для добавления различных служб.

В следующем примере показано, как использовать `@inject`. Реализация службы `Services.IDataAccess` вставляется в свойство компонента `DataRepository`. Обратите внимание на то, как код использует только `IDataAccess` абстракции:

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

На внутреннем уровне созданное свойство (`DataRepository`) снабжен `InjectAttribute` атрибута. Как правило этот атрибут не используется напрямую. Если базовый класс является обязательным для компонентов и внедренного свойства также требуются для базового класса, `InjectAttribute` можно добавлять вручную:

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

В компонентах, производный от базового класса `@inject` директива не является обязательным. `InjectAttribute` Базового класса достаточно:

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a>Внедрение зависимостей в службах

Сложные служб требуются дополнительные службы. В предыдущем примере `DataAccess` может потребоваться `HttpClient` службу по умолчанию. `@inject` или `InjectAttribute` не может использоваться в службах. *Внедрение через конструктор* следует использовать. Путем добавления параметров в конструкторе службы добавляются необходимые службы. Когда внедрение зависимостей создает службу, он распознает служб ему необходим в конструкторе и предоставляет их соответствующим образом.

В следующем образце кода показано концепции:

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

Обратите внимание, указанных ниже необходимых для внедрения через конструктор:

* Должен быть хотя бы один конструктор, аргументы которых все выполнения может использоваться внедрения зависимостей. Обратите внимание, что дополнительные параметры, не охваченных DI разрешены в том случае, если для них указаны значения по умолчанию.
* Соответствующий конструктор должен быть *открытый*.
* Должно существовать только один соответствующий конструктор. В случае неоднозначности DI вызывает исключение.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Внедрение зависимостей в ASP.NET Core](/aspnet/core/fundamentals/dependency-injection)
