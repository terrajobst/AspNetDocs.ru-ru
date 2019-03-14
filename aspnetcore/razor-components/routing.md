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
# <a name="razor-components-routing"></a>Razor компонентов маршрутизации

Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)

Узнайте, как для перенаправления запросов в приложениях, а также сведения о компоненте NavLink.

[Просмотреть или скачать пример кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([описание скачивания](xref:index#how-to-download-a-sample)). Сведения о необходимых компонентах см. в разделе [Начало работы](xref:razor-components/get-started).

## <a name="route-templates"></a>Шаблоны маршрутов

`<Router>` Компонент включает маршрутизацию, а шаблон маршрута предоставляется для каждого доступного компонента. `<Router>` Компонент появится в *App.cshtml* файла:

```cshtml
<Router AppAssembly=typeof(Program).Assembly />
```

Когда  *\*.cshtml* файл с `@page` компилируется директивы, созданном классе ему присваивается [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute) Указание шаблона маршрута. Во время выполнения, маршрутизатор ищет классы компонентов с `RouteAttribute` и отображает, какой компонент имеет шаблон маршрута, соответствующий запрошенного URL-адреса.

Несколько шаблонов маршрута могут применяться к компоненту. В [пример приложения](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/), следующий компонент отвечает на запросы для `/BlazorRoute` и `/DifferentBlazorRoute`.

*Pages/BlazorRoute.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?start=1&end=4)]

`<Router>` поддерживает настройку резервной компонентом для подготовки к просмотру, если запрошенный маршрут не разрешается. Включить этот сценарий согласиться, задав `FallbackComponent` параметр к типу класса резервный компонента.

В следующем примере задается компонента, определенного в *Pages/MyFallbackRazorComponent.cshtml* как резервный компонент для `<Router>`:

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> Чтобы правильно создать маршруты, приложение должно включать `<base>` тег в его *wwwroot/index.html* файл с основной путь приложения, указанного в `href` атрибут (`<base href="/" />`). Дополнительные сведения см. в разделе [узла и развертывание: Основной путь приложения](xref:host-and-deploy/razor-components/index#app-base-path).

## <a name="route-parameters"></a>Параметры маршрута

Маршрутизатор использует параметры маршрута для заполнения соответствующих параметров компонент с тем же именем (без учета регистра).

*Pages/RouteParameter.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?start=1&end=8)]

Необязательные параметры не поддерживаются, так что два `@page` директивы применяются в приведенном выше примере. Первый позволяет навигации к компоненту без параметров. Второй `@page` принимает директивы `{text}` параметра маршрута и присваивает это значение `Text` свойства.

## <a name="route-constraints"></a>Ограничения маршрута

Ограничения маршрута обеспечивает тип соответствия сегмента маршрута в компонент.

В следующем примере маршрут к компоненту пользователей соответствует только если:

* `Id` Сегмента маршрута находится на URL-АДРЕСЕ запроса.
* `Id` Сегмента должно быть целым числом (`int`).

```cshtml
@page "/Users/{Id:int}"

<h1>The user Id is @Id!</h1>

@functions {
    [Parameter]
    private int Id { get; set; }
}
```

Ограничения маршрута, показано в следующей таблице, доступны для использования. Ограничения маршрута, соответствующие инвариантного языка и региональных параметров см. в разделе Предупреждение приведенной ниже таблице, Дополнительные сведения.

| Ограничение | Пример           | Примеры совпадений                                                                  | Инвариант<br>язык и региональные параметры<br>соответствие |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | `true`, `FALSE`                                                                  | Нет                               |
| `datetime` | `{dob:datetime}`  | `2016-12-31`, `2016-12-31 7:32pm`                                                | Да                              |
| `decimal`  | `{price:decimal}` | `49.99`, `-1,000.01`                                                             | Да                              |
| `double`   | `{weight:double}` | `1.234`, `-1,001.01e8`                                                           | Да                              |
| `float`    | `{weight:float}`  | `1.234`, `-1,001.01e8`                                                           | Да                              |
| `guid`     | `{id:guid}`       | `CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}` | Нет                               |
| `int`      | `{id:int}`        | `123456789`, `-123456789`                                                        | Да                              |
| `long`     | `{ticks:long}`    | `123456789`, `-123456789`                                                        | Да                              |

> [!WARNING]
> Ограничения маршрута, которые проверяют URL-адрес и могут быть преобразованы в тип CLR (например, `int` или `DateTime`), всегда используют инвариантные язык и региональные параметры. Эти ограничения предполагают, что URL-адрес является нелокализуемым.

## <a name="navlink-component"></a>Компонент NavLink

Использовать компонент NavLink вместо HTML  **\<>** элементы во время создания ссылок навигации. Компонент NavLink ведет себя как  **\<>** элемента, за исключением того, она переключает `active` класс CSS в зависимости от его `href` соответствует текущий URL-адрес. `active` Класс помогает пользователю понять, какая страница является страницей active среди отображаемых ссылок навигации.

Компонент NavMenu в [пример приложения](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) создает [Bootstrap](https://getbootstrap.com/docs/) панели навигации, в котором показано, как использовать компоненты NavLink. В следующей разметке показан первые два NavLinks в *Shared/NavMenu.cshtml* файла.

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?start=13&end=24&highlight=4-6,9-11)]

Существует два `NavLinkMatch` параметры:

* `NavLinkMatch.All` &ndash; Указывает, что NavLink должен быть активным, если он соответствует весь текущий URL-адрес.
* `NavLinkMatch.Prefix` &ndash; Указывает, что NavLink должен быть активным, если он соответствует любой префикс, текущий URL-адреса.

В приведенном выше примере Home NavLink (`href=""`) соответствует всем URL-адресам и всегда получает `active` класс CSS. Получает только второй NavLink `active` класса, когда пользователь посещает компонента BlazorRoute (`href="BlazorRoute"`).
