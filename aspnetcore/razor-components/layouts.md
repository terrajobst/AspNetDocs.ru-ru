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
# <a name="razor-components-layouts"></a>Макеты компонентов Razor

По [Rainer Stropek](https://www.timecockpit.com)

Приложения обычно содержат больше одной страницы. Элементы макета, такие как меню, сообщения об авторских правах и логотипы, должен присутствовать на всех страницах. Скопировав код из этих элементов макета в все страницы приложения не является эффективным решением. Такое дублирование сложен в сопровождении и, возможно, приводит к несогласованности содержимое со временем. *Макеты* решить эту проблему.

С технической точки зрения макета — просто еще один компонент. Макет определяется в шаблоне Razor или в C# кода и может содержать привязки данных, внедрение зависимостей и других возможностей обычные компоненты. Включить два дополнительных аспектов *компонент* в *макета*:

* Макет компонента должен наследовать от `BlazorLayoutComponent`. `BlazorLayoutComponent` Определяет `Body` свойство, которое содержит содержимое для отображения внутри макета.
* Использует компонент макета `Body` свойство, чтобы указать, где должен быть содержимому текста к просмотру с использованием синтаксиса Razor `@Body`. Во время отрисовки, `@Body` заменяется содержимое макета.

В следующем образце кода показан шаблон Razor компонента макета. Обратите внимание на использование `BlazorLayoutComponent` и `@Body`:

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

## <a name="use-a-layout-in-a-component"></a>Использование макета в компоненте

Использовать директивы Razor `@layout` для применения макета в компонент. Компилятор преобразует эту директиву в `LayoutAttribute`, который применяется к классу component.

В следующем образце кода показано концепции. Содержимое этого компонента будет вставлен *MasterLayout* с позиции `@Body`:

```csharp
@layout MasterLayout

@page "/master-data"

<h2>Master Data Management</h2>
...
```

## <a name="centralized-layout-selection"></a>Выбор централизованного макета

Каждой папки из приложения может содержать файл шаблона с именем *_ViewImports.cshtml*. Компилятор включает директивы, указанный в файле imports представление всех шаблонов Razor в той же папке и рекурсивно во всех вложенных в нее папках. Таким образом *_ViewImports.cshtml* файл, содержащий `@layout MainLayout` гарантирует, что все компоненты в папку, используйте *MainLayout* макета. Нет необходимости повторно добавить `@layout` ко всем  *\*.cshtml* файлов.

Обратите внимание, что в шаблоне по умолчанию используется *_ViewImports.cshtml* механизм для выбора макета. Содержит только что созданному приложению *_ViewImports.cshtml* файл *страниц* папки.

## <a name="nested-layouts"></a>Вложенным макетам

Приложения могут состоять из вложенным макетам. Компонент может ссылаться на макет, который в свою очередь ссылается на другую структуру. Например можно использовать вложенности макетов в соответствии с многоуровневой структурой.

В следующем образце кода демонстрируется использование вложенным макетам. *CustomersComponent.cshtml* файл — это компонент для отображения. Обратите внимание, что компонент ссылается на макет `MasterDataLayout`.

*CustomersComponent.cshtml*:

```csharp
@layout MasterDataLayout

@page "/master-data/customers"

<h1>Customer Maintenance</h1>
...
```

*MasterDataLayout.cshtml* файл предоставляет `MasterDataLayout`. Макет ссылается на другую структуру `MainLayout`, куда они передаются для внедрения.

*MasterDataLayout.cshtml*:

```csharp
@layout MainLayout
@inherits BlazorLayoutComponent

<nav>
    <!-- Menu structure of master data module -->
    ...
</nav>

@Body
```

Наконец `MainLayout` содержит элементы макета верхнего уровня, например заголовка, нижнего колонтитула и главного меню.

*MainLayout.cshtml*:

```csharp
@inherits BlazorLayoutComponent

<header>...</header>
<nav>...</nav>

@Body
```
