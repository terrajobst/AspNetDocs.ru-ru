---
title: Библиотеки классов Razor компонентов
author: guardrex
description: Узнайте, как компоненты могут быть включены в приложениях Razor компоненты из библиотеки внешнего компонента.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/09/2019
uid: razor-components/class-libraries
ms.openlocfilehash: 0e644627178bae2b8880760335860b3e0ebef156
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037411"
---
# <a name="razor-components-class-libraries"></a><span data-ttu-id="521a2-103">Библиотеки классов Razor компонентов</span><span class="sxs-lookup"><span data-stu-id="521a2-103">Razor Components Class Libraries</span></span>

<span data-ttu-id="521a2-104">По [Тиммса Simon](https://github.com/stimms)</span><span class="sxs-lookup"><span data-stu-id="521a2-104">By [Simon Timms](https://github.com/stimms)</span></span>

> [!NOTE]
> <span data-ttu-id="521a2-105">SDK для .NET Core 3.0 Предварительная версия 2 не содержит шаблон проекта для библиотеки классов Razor компонента, но мы планируем добавить шаблон в следующей предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="521a2-105">The .NET Core 3.0 Preview 2 SDK doesn't include a project template for Razor Component Class Libraries, but we expect to add a template in a future preview.</span></span> <span data-ttu-id="521a2-106">В пока можно использовать шаблон библиотеки классов компонентов Blazor, описанных в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="521a2-106">In meantime, you can use the Blazor Component Class Library template explained in this topic.</span></span>

<span data-ttu-id="521a2-107">Компоненты в библиотек компонентов могут совместно использоваться проектами.</span><span class="sxs-lookup"><span data-stu-id="521a2-107">Components can be shared in component libraries across projects.</span></span> <span data-ttu-id="521a2-108">Компоненты можно включить из:</span><span class="sxs-lookup"><span data-stu-id="521a2-108">Components can be included from:</span></span>

* <span data-ttu-id="521a2-109">Другой проект в решении.</span><span class="sxs-lookup"><span data-stu-id="521a2-109">Another project in the solution.</span></span>
* <span data-ttu-id="521a2-110">Пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="521a2-110">A NuGet package.</span></span>
* <span data-ttu-id="521a2-111">Библиотека .NET, на которую указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="521a2-111">A referenced .NET library.</span></span>

<span data-ttu-id="521a2-112">Так же, как компоненты регулярные типы .NET, компонент библиотеки — обычный сборок .NET.</span><span class="sxs-lookup"><span data-stu-id="521a2-112">Just as components are regular .NET types, component libraries are normal .NET assemblies.</span></span>

<span data-ttu-id="521a2-113">Чтобы создать новую библиотеку компонента, используйте `blazorlib` шаблон с [команды dotnet new](/dotnet/core/tools/dotnet-new) команды.</span><span class="sxs-lookup"><span data-stu-id="521a2-113">To create a new component library, use the `blazorlib` template with the [dotnet new](/dotnet/core/tools/dotnet-new) command.</span></span> <span data-ttu-id="521a2-114">Шаблон является частью шаблоны, установленные при [Настройка компонентов Razor](xref:razor-components/get-started).</span><span class="sxs-lookup"><span data-stu-id="521a2-114">The template is part of the templates installed when [setting up Razor Components](xref:razor-components/get-started).</span></span>

```console
dotnet new blazorlib -o MyComponentLib1
```

<span data-ttu-id="521a2-115">Чтобы добавить в библиотеку в существующий проект, используйте [dotnet sln](/dotnet/core/tools/dotnet-sln) команды:</span><span class="sxs-lookup"><span data-stu-id="521a2-115">To add the library to an existing project, use the [dotnet sln](/dotnet/core/tools/dotnet-sln) command:</span></span>

```console
dotnet sln add .\MyComponentLib1
```

<span data-ttu-id="521a2-116">Библиотеки компонентов может содержать статические файлы, такие как изображения, JavaScript и таблицы стилей.</span><span class="sxs-lookup"><span data-stu-id="521a2-116">Component libraries may contain static files, such as images, JavaScript, and stylesheets.</span></span> <span data-ttu-id="521a2-117">Во время сборки, статические файлы внедряются в сборку файл (*.dll*), позволяющий потребления компонентов не нужно беспокоиться о том, как включить их ресурсы.</span><span class="sxs-lookup"><span data-stu-id="521a2-117">At build time, static files are embedded into the built assembly file (*.dll*), which allows consumption of the components without having to worry about how to include their resources.</span></span> <span data-ttu-id="521a2-118">Все файлы, включенные в `content` directory помечаются как внедренный ресурс.</span><span class="sxs-lookup"><span data-stu-id="521a2-118">Any files included in the `content` directory are marked as an embedded resource.</span></span> 

## <a name="consume-a-library-component"></a><span data-ttu-id="521a2-119">Использует компонент библиотеки</span><span class="sxs-lookup"><span data-stu-id="521a2-119">Consume a library component</span></span>

<span data-ttu-id="521a2-120">Чтобы использовать компоненты, определенные в библиотеке в другом проекте [ @addTagHelper ](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label) необходимо использовать директиву.</span><span class="sxs-lookup"><span data-stu-id="521a2-120">In order to consume components defined in a library in another project, the [@addTagHelper](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label) directive must be used.</span></span> <span data-ttu-id="521a2-121">Отдельные компоненты могут быть добавлены по имени.</span><span class="sxs-lookup"><span data-stu-id="521a2-121">Individual components may be added by name.</span></span> <span data-ttu-id="521a2-122">Например, следующая директива добавляет `Component1` из `MyComponentLib1`:</span><span class="sxs-lookup"><span data-stu-id="521a2-122">For example, the following directive adds `Component1` of `MyComponentLib1`:</span></span>

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

<span data-ttu-id="521a2-123">Директивы общие выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="521a2-123">The general format of the directive is:</span></span>

```cshtml
@addTagHelper <namespaced component name>, <assembly name>
```

<span data-ttu-id="521a2-124">Тем не менее он являются общими для включения всех компонентов из сборки с помощью подстановочного знака.</span><span class="sxs-lookup"><span data-stu-id="521a2-124">However, it's common to include all of the components from an assembly using a wildcard:</span></span>

```cshtml
@addTagHelper *, MyComponentLib1
```

<span data-ttu-id="521a2-125">`@addTagHelper` Директивы может быть включено в *_ViewImport.cshtml* для этих компонентов доступны для всего проекта или примененные к одной странице или набору страниц в папке.</span><span class="sxs-lookup"><span data-stu-id="521a2-125">The `@addTagHelper` directive can be included in *_ViewImport.cshtml* to make the components available for an entire project or applied to a single page or set of pages within a folder.</span></span> <span data-ttu-id="521a2-126">С помощью `@addTagHelper` директив на месте, компоненты библиотеки компонентов могут быть использованы как если бы они были в той же сборке, что и приложение.</span><span class="sxs-lookup"><span data-stu-id="521a2-126">With the `@addTagHelper` directive in place, the components of the component library can be consumed as if they were in the same assembly as the app.</span></span> 

## <a name="build-pack-and-ship-to-nuget"></a><span data-ttu-id="521a2-127">Сборки, пакет и поставки для NuGet</span><span class="sxs-lookup"><span data-stu-id="521a2-127">Build, pack, and ship to NuGet</span></span>

<span data-ttu-id="521a2-128">Так как компонент библиотеки — стандартные библиотеки .NET, упаковки и их отправки в NuGet в качестве примеров, ничем не отличается от упаковки и доставки любую библиотеку в NuGet.</span><span class="sxs-lookup"><span data-stu-id="521a2-128">Because component libraries are standard .NET libraries, packaging and shipping them to NuGet is no different from packaging and shipping any library to NuGet.</span></span> <span data-ttu-id="521a2-129">Упаковка выполняется с помощью [dotnet pack](/dotnet/core/tools/dotnet-pack) команды:</span><span class="sxs-lookup"><span data-stu-id="521a2-129">Packaging is performed using the [dotnet pack](/dotnet/core/tools/dotnet-pack) command:</span></span>

```console
dotnet pack
```

<span data-ttu-id="521a2-130">Отправка пакета NuGet с помощью [публикации dotnet nuget](/dotnet/core/tools/dotnet-nuget-push) команды:</span><span class="sxs-lookup"><span data-stu-id="521a2-130">Upload the package to NuGet using the [dotnet nuget publish](/dotnet/core/tools/dotnet-nuget-push) command:</span></span>

```console
dotnet nuget publish
```

<span data-ttu-id="521a2-131">Все включенные статические ресурсы включаются в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="521a2-131">Any included static resources are included in the NuGet package.</span></span> <span data-ttu-id="521a2-132">Потребители библиотеки автоматически получать скриптов и таблиц стилей, чтобы потребители не требуется вручную установить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="521a2-132">Library consumers automatically receive scripts and stylesheets, so consumers aren't required to manually install the resources.</span></span>
