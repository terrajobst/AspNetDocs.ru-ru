---
title: Razor компонентов маршрутизации
author: guardrex
description: Узнайте, как для перенаправления запросов в приложениях, а также сведения о компоненте NavLink.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/01/2019
uid: razor-components/routing
ms.openlocfilehash: 5c648ba1bb3846f5baa515e808a98a3b33f81438
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031611"
---
# <a name="razor-components-routing"></a><span data-ttu-id="7cdfd-103">Razor компонентов маршрутизации</span><span class="sxs-lookup"><span data-stu-id="7cdfd-103">Razor Components routing</span></span>

<span data-ttu-id="7cdfd-104">Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)</span><span class="sxs-lookup"><span data-stu-id="7cdfd-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="7cdfd-105">Узнайте, как для перенаправления запросов в приложениях, а также сведения о компоненте NavLink.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-105">Learn how to route requests in apps and about the NavLink component.</span></span>

<span data-ttu-id="7cdfd-106">[Просмотреть или скачать пример кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([описание скачивания](xref:index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="7cdfd-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="7cdfd-107">Сведения о необходимых компонентах см. в разделе [Начало работы](xref:razor-components/get-started).</span><span class="sxs-lookup"><span data-stu-id="7cdfd-107">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

## <a name="route-templates"></a><span data-ttu-id="7cdfd-108">Шаблоны маршрутов</span><span class="sxs-lookup"><span data-stu-id="7cdfd-108">Route templates</span></span>

<span data-ttu-id="7cdfd-109">`<Router>` Компонент включает маршрутизацию, а шаблон маршрута предоставляется для каждого доступного компонента.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-109">The `<Router>` component enables routing, and a route template is provided to each accessible component.</span></span> <span data-ttu-id="7cdfd-110">`<Router>` Компонент появится в *App.cshtml* файла:</span><span class="sxs-lookup"><span data-stu-id="7cdfd-110">The `<Router>` component appears in the *App.cshtml* file:</span></span>

```cshtml
<Router AppAssembly=typeof(Program).Assembly />
```

<span data-ttu-id="7cdfd-111">Когда  *\*.cshtml* файл с `@page` компилируется директивы, созданном классе ему присваивается [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute) Указание шаблона маршрута.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-111">When a *\*.cshtml* file with an `@page` directive is compiled, the generated class is given a [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute) specifying the route template.</span></span> <span data-ttu-id="7cdfd-112">Во время выполнения, маршрутизатор ищет классы компонентов с `RouteAttribute` и отображает, какой компонент имеет шаблон маршрута, соответствующий запрошенного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-112">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="7cdfd-113">Несколько шаблонов маршрута могут применяться к компоненту.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-113">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="7cdfd-114">В [пример приложения](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/), следующий компонент отвечает на запросы для `/BlazorRoute` и `/DifferentBlazorRoute`.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-114">In the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/), the following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`.</span></span>

<span data-ttu-id="7cdfd-115">*Pages/BlazorRoute.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="7cdfd-115">*Pages/BlazorRoute.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?start=1&end=4)]

<span data-ttu-id="7cdfd-116">`<Router>` поддерживает настройку резервной компонентом для подготовки к просмотру, если запрошенный маршрут не разрешается.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-116">`<Router>` supports setting a fallback component for rendering when a requested route isn't resolved.</span></span> <span data-ttu-id="7cdfd-117">Включить этот сценарий согласиться, задав `FallbackComponent` параметр к типу класса резервный компонента.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-117">Enable this opt-in scenario by setting the `FallbackComponent` parameter to the type of the fallback component class.</span></span>

<span data-ttu-id="7cdfd-118">В следующем примере задается компонента, определенного в *Pages/MyFallbackRazorComponent.cshtml* как резервный компонент для `<Router>`:</span><span class="sxs-lookup"><span data-stu-id="7cdfd-118">The following example sets a component defined in *Pages/MyFallbackRazorComponent.cshtml* as the fallback component for a `<Router>`:</span></span>

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> <span data-ttu-id="7cdfd-119">Чтобы правильно создать маршруты, приложение должно включать `<base>` тег в его *wwwroot/index.html* файл с основной путь приложения, указанного в `href` атрибут (`<base href="/" />`).</span><span class="sxs-lookup"><span data-stu-id="7cdfd-119">To generate routes properly, the app must include a `<base>` tag in its *wwwroot/index.html* file with the app base path specified in the `href` attribute (`<base href="/" />`).</span></span> <span data-ttu-id="7cdfd-120">Дополнительные сведения см. в разделе [узла и развертывание: Основной путь приложения](xref:host-and-deploy/razor-components/index#app-base-path).</span><span class="sxs-lookup"><span data-stu-id="7cdfd-120">For more information, see [Host and deploy: App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="route-parameters"></a><span data-ttu-id="7cdfd-121">Параметры маршрута</span><span class="sxs-lookup"><span data-stu-id="7cdfd-121">Route parameters</span></span>

<span data-ttu-id="7cdfd-122">Маршрутизатор использует параметры маршрута для заполнения соответствующих параметров компонент с тем же именем (без учета регистра).</span><span class="sxs-lookup"><span data-stu-id="7cdfd-122">The router uses route parameters to populate the corresponding component parameters with the same name (case insensitive).</span></span>

<span data-ttu-id="7cdfd-123">*Pages/RouteParameter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="7cdfd-123">*Pages/RouteParameter.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?start=1&end=8)]

<span data-ttu-id="7cdfd-124">Необязательные параметры не поддерживаются, так что два `@page` директивы применяются в приведенном выше примере.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-124">Optional parameters aren't supported yet, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="7cdfd-125">Первый позволяет навигации к компоненту без параметров.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-125">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="7cdfd-126">Второй `@page` принимает директивы `{text}` параметра маршрута и присваивает это значение `Text` свойства.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-126">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="route-constraints"></a><span data-ttu-id="7cdfd-127">Ограничения маршрута</span><span class="sxs-lookup"><span data-stu-id="7cdfd-127">Route constraints</span></span>

<span data-ttu-id="7cdfd-128">Ограничения маршрута обеспечивает тип соответствия сегмента маршрута в компонент.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-128">A route constraint enforces type matching on a route segment to a component.</span></span>

<span data-ttu-id="7cdfd-129">В следующем примере маршрут к компоненту пользователей соответствует только если:</span><span class="sxs-lookup"><span data-stu-id="7cdfd-129">In the following example, the route to the Users component only matches if:</span></span>

* <span data-ttu-id="7cdfd-130">`Id` Сегмента маршрута находится на URL-АДРЕСЕ запроса.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-130">An `Id` route segment is present on the request URL.</span></span>
* <span data-ttu-id="7cdfd-131">`Id` Сегмента должно быть целым числом (`int`).</span><span class="sxs-lookup"><span data-stu-id="7cdfd-131">The `Id` segment is an integer (`int`).</span></span>

```cshtml
@page "/Users/{Id:int}"

<h1>The user Id is @Id!</h1>

@functions {
    [Parameter]
    private int Id { get; set; }
}
```

<span data-ttu-id="7cdfd-132">Ограничения маршрута, показано в следующей таблице, доступны для использования.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-132">The route constraints shown in the following table are available for use.</span></span> <span data-ttu-id="7cdfd-133">Ограничения маршрута, соответствующие инвариантного языка и региональных параметров см. в разделе Предупреждение приведенной ниже таблице, Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-133">For the route constraints that match with the invariant culture, see the warning below the table for more information.</span></span>

| <span data-ttu-id="7cdfd-134">Ограничение</span><span class="sxs-lookup"><span data-stu-id="7cdfd-134">Constraint</span></span> | <span data-ttu-id="7cdfd-135">Пример</span><span class="sxs-lookup"><span data-stu-id="7cdfd-135">Example</span></span>           | <span data-ttu-id="7cdfd-136">Примеры совпадений</span><span class="sxs-lookup"><span data-stu-id="7cdfd-136">Example Matches</span></span>                                                                  | <span data-ttu-id="7cdfd-137">Инвариант</span><span class="sxs-lookup"><span data-stu-id="7cdfd-137">Invariant</span></span><br><span data-ttu-id="7cdfd-138">язык и региональные параметры</span><span class="sxs-lookup"><span data-stu-id="7cdfd-138">culture</span></span><br><span data-ttu-id="7cdfd-139">соответствие</span><span class="sxs-lookup"><span data-stu-id="7cdfd-139">matching</span></span> |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | <span data-ttu-id="7cdfd-140">`true`, `FALSE`</span><span class="sxs-lookup"><span data-stu-id="7cdfd-140">`true`, `FALSE`</span></span>                                                                  | <span data-ttu-id="7cdfd-141">Нет</span><span class="sxs-lookup"><span data-stu-id="7cdfd-141">No</span></span>                               |
| `datetime` | `{dob:datetime}`  | <span data-ttu-id="7cdfd-142">`2016-12-31`, `2016-12-31 7:32pm`</span><span class="sxs-lookup"><span data-stu-id="7cdfd-142">`2016-12-31`, `2016-12-31 7:32pm`</span></span>                                                | <span data-ttu-id="7cdfd-143">Да</span><span class="sxs-lookup"><span data-stu-id="7cdfd-143">Yes</span></span>                              |
| `decimal`  | `{price:decimal}` | <span data-ttu-id="7cdfd-144">`49.99`, `-1,000.01`</span><span class="sxs-lookup"><span data-stu-id="7cdfd-144">`49.99`, `-1,000.01`</span></span>                                                             | <span data-ttu-id="7cdfd-145">Да</span><span class="sxs-lookup"><span data-stu-id="7cdfd-145">Yes</span></span>                              |
| `double`   | `{weight:double}` | <span data-ttu-id="7cdfd-146">`1.234`, `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="7cdfd-146">`1.234`, `-1,001.01e8`</span></span>                                                           | <span data-ttu-id="7cdfd-147">Да</span><span class="sxs-lookup"><span data-stu-id="7cdfd-147">Yes</span></span>                              |
| `float`    | `{weight:float}`  | <span data-ttu-id="7cdfd-148">`1.234`, `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="7cdfd-148">`1.234`, `-1,001.01e8`</span></span>                                                           | <span data-ttu-id="7cdfd-149">Да</span><span class="sxs-lookup"><span data-stu-id="7cdfd-149">Yes</span></span>                              |
| `guid`     | `{id:guid}`       | <span data-ttu-id="7cdfd-150">`CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span><span class="sxs-lookup"><span data-stu-id="7cdfd-150">`CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span></span> | <span data-ttu-id="7cdfd-151">Нет</span><span class="sxs-lookup"><span data-stu-id="7cdfd-151">No</span></span>                               |
| `int`      | `{id:int}`        | <span data-ttu-id="7cdfd-152">`123456789`, `-123456789`</span><span class="sxs-lookup"><span data-stu-id="7cdfd-152">`123456789`, `-123456789`</span></span>                                                        | <span data-ttu-id="7cdfd-153">Да</span><span class="sxs-lookup"><span data-stu-id="7cdfd-153">Yes</span></span>                              |
| `long`     | `{ticks:long}`    | <span data-ttu-id="7cdfd-154">`123456789`, `-123456789`</span><span class="sxs-lookup"><span data-stu-id="7cdfd-154">`123456789`, `-123456789`</span></span>                                                        | <span data-ttu-id="7cdfd-155">Да</span><span class="sxs-lookup"><span data-stu-id="7cdfd-155">Yes</span></span>                              |

> [!WARNING]
> <span data-ttu-id="7cdfd-156">Ограничения маршрута, которые проверяют URL-адрес и могут быть преобразованы в тип CLR (например, `int` или `DateTime`), всегда используют инвариантные язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-156">Route constraints that verify the URL and are converted to a CLR type (such as `int` or `DateTime`) always use the invariant culture.</span></span> <span data-ttu-id="7cdfd-157">Эти ограничения предполагают, что URL-адрес является нелокализуемым.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-157">These constraints assume that the URL is non-localizable.</span></span>

## <a name="navlink-component"></a><span data-ttu-id="7cdfd-158">Компонент NavLink</span><span class="sxs-lookup"><span data-stu-id="7cdfd-158">NavLink component</span></span>

<span data-ttu-id="7cdfd-159">Использовать компонент NavLink вместо HTML  **\<>** элементы во время создания ссылок навигации.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-159">Use a NavLink component in place of HTML **\<a>** elements when creating navigation links.</span></span> <span data-ttu-id="7cdfd-160">Компонент NavLink ведет себя как  **\<>** элемента, за исключением того, она переключает `active` класс CSS в зависимости от его `href` соответствует текущий URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-160">A NavLink component behaves like an **\<a>** element, except it toggles an `active` CSS class based on whether its `href` matches the current URL.</span></span> <span data-ttu-id="7cdfd-161">`active` Класс помогает пользователю понять, какая страница является страницей active среди отображаемых ссылок навигации.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-161">The `active` class helps a user understand which page is the active page among the navigation links displayed.</span></span>

<span data-ttu-id="7cdfd-162">Компонент NavMenu в [пример приложения](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) создает [Bootstrap](https://getbootstrap.com/docs/) панели навигации, в котором показано, как использовать компоненты NavLink.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-162">The NavMenu component in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) creates a [Bootstrap](https://getbootstrap.com/docs/) nav bar that demonstrates how to use NavLink components.</span></span> <span data-ttu-id="7cdfd-163">В следующей разметке показан первые два NavLinks в *Shared/NavMenu.cshtml* файла.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-163">The following markup shows the first two NavLinks in the *Shared/NavMenu.cshtml* file.</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?start=13&end=24&highlight=4-6,9-11)]

<span data-ttu-id="7cdfd-164">Существует два `NavLinkMatch` параметры:</span><span class="sxs-lookup"><span data-stu-id="7cdfd-164">There are two `NavLinkMatch` options:</span></span>

* <span data-ttu-id="7cdfd-165">`NavLinkMatch.All` &ndash; Указывает, что NavLink должен быть активным, если он соответствует весь текущий URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-165">`NavLinkMatch.All` &ndash; Specifies that the NavLink should be active when it matches the entire current URL.</span></span>
* <span data-ttu-id="7cdfd-166">`NavLinkMatch.Prefix` &ndash; Указывает, что NavLink должен быть активным, если он соответствует любой префикс, текущий URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-166">`NavLinkMatch.Prefix` &ndash; Specifies that the NavLink should be active when it matches any prefix of the current URL.</span></span>

<span data-ttu-id="7cdfd-167">В приведенном выше примере Home NavLink (`href=""`) соответствует всем URL-адресам и всегда получает `active` класс CSS.</span><span class="sxs-lookup"><span data-stu-id="7cdfd-167">In the preceding example, the Home NavLink (`href=""`) matches all URLs and always receives the `active` CSS class.</span></span> <span data-ttu-id="7cdfd-168">Получает только второй NavLink `active` класса, когда пользователь посещает компонента BlazorRoute (`href="BlazorRoute"`).</span><span class="sxs-lookup"><span data-stu-id="7cdfd-168">The second NavLink only receives the `active` class when the user visits the BlazorRoute component (`href="BlazorRoute"`).</span></span>
