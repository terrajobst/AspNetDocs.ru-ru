---
title: Макеты компонентов Razor
author: guardrex
description: Узнайте, как создать компоненты повторно используемый шаблон для Blazor и Razor компонентов приложений.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/layouts
ms.openlocfilehash: 23d8f441c0b3bbde7a73717f6257013831617ec0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039041"
---
# <a name="razor-components-layouts"></a><span data-ttu-id="e9a18-103">Макеты компонентов Razor</span><span class="sxs-lookup"><span data-stu-id="e9a18-103">Razor Components layouts</span></span>

<span data-ttu-id="e9a18-104">По [Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="e9a18-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="e9a18-105">Приложения обычно содержат больше одной страницы.</span><span class="sxs-lookup"><span data-stu-id="e9a18-105">Apps typically contain more than one page.</span></span> <span data-ttu-id="e9a18-106">Элементы макета, такие как меню, сообщения об авторских правах и логотипы, должен присутствовать на всех страницах.</span><span class="sxs-lookup"><span data-stu-id="e9a18-106">Layout elements, such as menus, copyright messages, and logos, must be present on all pages.</span></span> <span data-ttu-id="e9a18-107">Скопировав код из этих элементов макета в все страницы приложения не является эффективным решением.</span><span class="sxs-lookup"><span data-stu-id="e9a18-107">Copying the code of these layout elements into all of the pages of an app isn't an efficient solution.</span></span> <span data-ttu-id="e9a18-108">Такое дублирование сложен в сопровождении и, возможно, приводит к несогласованности содержимое со временем.</span><span class="sxs-lookup"><span data-stu-id="e9a18-108">Such duplication is hard to maintain and probably leads to inconsistent content over time.</span></span> <span data-ttu-id="e9a18-109">*Макеты* решить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="e9a18-109">*Layouts* solve this problem.</span></span>

<span data-ttu-id="e9a18-110">С технической точки зрения макета — просто еще один компонент.</span><span class="sxs-lookup"><span data-stu-id="e9a18-110">Technically, a layout is just another component.</span></span> <span data-ttu-id="e9a18-111">Макет определяется в шаблоне Razor или в C# кода и может содержать привязки данных, внедрение зависимостей и других возможностей обычные компоненты.</span><span class="sxs-lookup"><span data-stu-id="e9a18-111">A layout is defined in a Razor template or in C# code and can contain data binding, dependency injection, and other ordinary features of components.</span></span> <span data-ttu-id="e9a18-112">Включить два дополнительных аспектов *компонент* в *макета*:</span><span class="sxs-lookup"><span data-stu-id="e9a18-112">Two additional aspects turn a *component* into a *layout*:</span></span>

* <span data-ttu-id="e9a18-113">Макет компонента должен наследовать от `BlazorLayoutComponent`.</span><span class="sxs-lookup"><span data-stu-id="e9a18-113">The layout component must inherit from `BlazorLayoutComponent`.</span></span> <span data-ttu-id="e9a18-114">`BlazorLayoutComponent` Определяет `Body` свойство, которое содержит содержимое для отображения внутри макета.</span><span class="sxs-lookup"><span data-stu-id="e9a18-114">`BlazorLayoutComponent` defines a `Body` property that contains the content to be rendered inside the layout.</span></span>
* <span data-ttu-id="e9a18-115">Использует компонент макета `Body` свойство, чтобы указать, где должен быть содержимому текста к просмотру с использованием синтаксиса Razor `@Body`.</span><span class="sxs-lookup"><span data-stu-id="e9a18-115">The layout component uses the `Body` property to specify where the body content should be rendered using the Razor syntax `@Body`.</span></span> <span data-ttu-id="e9a18-116">Во время отрисовки, `@Body` заменяется содержимое макета.</span><span class="sxs-lookup"><span data-stu-id="e9a18-116">During rendering, `@Body` is replaced by the content of the layout.</span></span>

<span data-ttu-id="e9a18-117">В следующем образце кода показан шаблон Razor компонента макета.</span><span class="sxs-lookup"><span data-stu-id="e9a18-117">The following code sample shows the Razor template of a layout component.</span></span> <span data-ttu-id="e9a18-118">Обратите внимание на использование `BlazorLayoutComponent` и `@Body`:</span><span class="sxs-lookup"><span data-stu-id="e9a18-118">Note the use of `BlazorLayoutComponent` and `@Body`:</span></span>

```csharp
@inherits BlazorLayoutComponent

<header>
    <h1>ERP Master 3000</h1>
</header>

<nav>
    <a href="master-data">Master Data Management</a>
    <a href="invoicing">Invoicing</a>
    <a href="accounting">Accounting</a>
</nav>

@Body

<footer>
    &copy; by @CopyrightMessage
</footer>

@functions {
    public string CopyrightMessage { get; set; }
    ...
}
```

## <a name="use-a-layout-in-a-component"></a><span data-ttu-id="e9a18-119">Использование макета в компоненте</span><span class="sxs-lookup"><span data-stu-id="e9a18-119">Use a layout in a component</span></span>

<span data-ttu-id="e9a18-120">Использовать директивы Razor `@layout` для применения макета в компонент.</span><span class="sxs-lookup"><span data-stu-id="e9a18-120">Use the Razor directive `@layout` to apply a layout to a component.</span></span> <span data-ttu-id="e9a18-121">Компилятор преобразует эту директиву в `LayoutAttribute`, который применяется к классу component.</span><span class="sxs-lookup"><span data-stu-id="e9a18-121">The compiler converts this directive into a `LayoutAttribute`, which is applied to the component class.</span></span>

<span data-ttu-id="e9a18-122">В следующем образце кода показано концепции.</span><span class="sxs-lookup"><span data-stu-id="e9a18-122">The following code sample demonstrates the concept.</span></span> <span data-ttu-id="e9a18-123">Содержимое этого компонента будет вставлен *MasterLayout* с позиции `@Body`:</span><span class="sxs-lookup"><span data-stu-id="e9a18-123">The content of this component is inserted into the *MasterLayout* at the position of `@Body`:</span></span>

```csharp
@layout MasterLayout

@page "/master-data"

<h2>Master Data Management</h2>
...
```

## <a name="centralized-layout-selection"></a><span data-ttu-id="e9a18-124">Выбор централизованного макета</span><span class="sxs-lookup"><span data-stu-id="e9a18-124">Centralized layout selection</span></span>

<span data-ttu-id="e9a18-125">Каждой папки из приложения может содержать файл шаблона с именем *_ViewImports.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e9a18-125">Every folder of a an app can optionally contain a template file named *_ViewImports.cshtml*.</span></span> <span data-ttu-id="e9a18-126">Компилятор включает директивы, указанный в файле imports представление всех шаблонов Razor в той же папке и рекурсивно во всех вложенных в нее папках.</span><span class="sxs-lookup"><span data-stu-id="e9a18-126">The compiler includes the directives specified in the view imports file in all of the Razor templates in the same folder and recursively in all of its subfolders.</span></span> <span data-ttu-id="e9a18-127">Таким образом *_ViewImports.cshtml* файл, содержащий `@layout MainLayout` гарантирует, что все компоненты в папку, используйте *MainLayout* макета.</span><span class="sxs-lookup"><span data-stu-id="e9a18-127">Therefore, a *_ViewImports.cshtml* file containing `@layout MainLayout` ensures that all of the components in a folder use the *MainLayout* layout.</span></span> <span data-ttu-id="e9a18-128">Нет необходимости повторно добавить `@layout` ко всем  *\*.cshtml* файлов.</span><span class="sxs-lookup"><span data-stu-id="e9a18-128">There's no need to repeatedly add `@layout` to all of the *\*.cshtml* files.</span></span>

<span data-ttu-id="e9a18-129">Обратите внимание, что в шаблоне по умолчанию используется *_ViewImports.cshtml* механизм для выбора макета.</span><span class="sxs-lookup"><span data-stu-id="e9a18-129">Note that the default template uses the *_ViewImports.cshtml* mechanism for layout selection.</span></span> <span data-ttu-id="e9a18-130">Содержит только что созданному приложению *_ViewImports.cshtml* файл *страниц* папки.</span><span class="sxs-lookup"><span data-stu-id="e9a18-130">A newly created app contains the *_ViewImports.cshtml* file in the *Pages* folder.</span></span>

## <a name="nested-layouts"></a><span data-ttu-id="e9a18-131">Вложенным макетам</span><span class="sxs-lookup"><span data-stu-id="e9a18-131">Nested layouts</span></span>

<span data-ttu-id="e9a18-132">Приложения могут состоять из вложенным макетам.</span><span class="sxs-lookup"><span data-stu-id="e9a18-132">Apps can consist of nested layouts.</span></span> <span data-ttu-id="e9a18-133">Компонент может ссылаться на макет, который в свою очередь ссылается на другую структуру.</span><span class="sxs-lookup"><span data-stu-id="e9a18-133">A component can reference a layout which in turn references another layout.</span></span> <span data-ttu-id="e9a18-134">Например можно использовать вложенности макетов в соответствии с многоуровневой структурой.</span><span class="sxs-lookup"><span data-stu-id="e9a18-134">For example, nesting layouts can be used to reflect a multi-level menu structure.</span></span>

<span data-ttu-id="e9a18-135">В следующем образце кода демонстрируется использование вложенным макетам.</span><span class="sxs-lookup"><span data-stu-id="e9a18-135">The following code samples show how to use nested layouts.</span></span> <span data-ttu-id="e9a18-136">*CustomersComponent.cshtml* файл — это компонент для отображения.</span><span class="sxs-lookup"><span data-stu-id="e9a18-136">The *CustomersComponent.cshtml* file is the component to display.</span></span> <span data-ttu-id="e9a18-137">Обратите внимание, что компонент ссылается на макет `MasterDataLayout`.</span><span class="sxs-lookup"><span data-stu-id="e9a18-137">Note that the component references the layout `MasterDataLayout`.</span></span>

<span data-ttu-id="e9a18-138">*CustomersComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e9a18-138">*CustomersComponent.cshtml*:</span></span>

```csharp
@layout MasterDataLayout

@page "/master-data/customers"

<h1>Customer Maintenance</h1>
...
```

<span data-ttu-id="e9a18-139">*MasterDataLayout.cshtml* файл предоставляет `MasterDataLayout`.</span><span class="sxs-lookup"><span data-stu-id="e9a18-139">The *MasterDataLayout.cshtml* file provides the `MasterDataLayout`.</span></span> <span data-ttu-id="e9a18-140">Макет ссылается на другую структуру `MainLayout`, куда они передаются для внедрения.</span><span class="sxs-lookup"><span data-stu-id="e9a18-140">The layout references another layout, `MainLayout`, where it's going to be embedded.</span></span>

<span data-ttu-id="e9a18-141">*MasterDataLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e9a18-141">*MasterDataLayout.cshtml*:</span></span>

```csharp
@layout MainLayout
@inherits BlazorLayoutComponent

<nav>
    <!-- Menu structure of master data module -->
    ...
</nav>

@Body
```

<span data-ttu-id="e9a18-142">Наконец `MainLayout` содержит элементы макета верхнего уровня, например заголовка, нижнего колонтитула и главного меню.</span><span class="sxs-lookup"><span data-stu-id="e9a18-142">Finally, `MainLayout` contains the top-level layout elements, such as the header, footer, and main menu.</span></span>

<span data-ttu-id="e9a18-143">*MainLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e9a18-143">*MainLayout.cshtml*:</span></span>

```csharp
@inherits BlazorLayoutComponent

<header>...</header>
<nav>...</nav>

@Body
```
