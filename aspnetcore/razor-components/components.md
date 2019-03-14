---
title: Создание и использование компонентов Razor
author: guardrex
description: Узнайте, как создать и использовать компоненты Razor, включая как привязка к данным, обработка событий и управление компонент жизненные циклы.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: razor-components/components
ms.openlocfilehash: 1533587f9f11e99f24d860c02f0efb6713119308
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031101"
---
# <a name="create-and-use-razor-components"></a><span data-ttu-id="b2919-103">Создание и использование компонентов Razor</span><span class="sxs-lookup"><span data-stu-id="b2919-103">Create and use Razor Components</span></span>

<span data-ttu-id="b2919-104">По [Люк Лэтем](https://github.com/guardrex), [Дэниэл рот](https://github.com/danroth27), и [Morné Zaayman](https://github.com/MorneZaayman)</span><span class="sxs-lookup"><span data-stu-id="b2919-104">By [Luke Latham](https://github.com/guardrex), [Daniel Roth](https://github.com/danroth27), and [Morné Zaayman](https://github.com/MorneZaayman)</span></span>

<span data-ttu-id="b2919-105">[Просмотреть или скачать пример кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([описание скачивания](xref:index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="b2919-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="b2919-106">Сведения о необходимых компонентах см. в разделе [Начало работы](xref:razor-components/get-started).</span><span class="sxs-lookup"><span data-stu-id="b2919-106">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

<span data-ttu-id="b2919-107">Razor компоненты приложения создаются с помощью *компоненты*.</span><span class="sxs-lookup"><span data-stu-id="b2919-107">Razor Components apps are built using *components*.</span></span> <span data-ttu-id="b2919-108">Компонент — это автономное фрагмент пользовательский интерфейс (UI), например страницы, диалоговое окно или форму.</span><span class="sxs-lookup"><span data-stu-id="b2919-108">A component is a self-contained chunk of user interface (UI), such as a page, dialog, or form.</span></span> <span data-ttu-id="b2919-109">Компонент включает разметки HTML и логика обработки, необходимые для вставки данных и реагировать на события пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b2919-109">A component includes HTML markup and the processing logic required to inject data or respond to UI events.</span></span> <span data-ttu-id="b2919-110">Компоненты, гибкий и простой.</span><span class="sxs-lookup"><span data-stu-id="b2919-110">Components are flexible and lightweight.</span></span> <span data-ttu-id="b2919-111">Они могут быть вложенными повторно и совместно использоваться проектами.</span><span class="sxs-lookup"><span data-stu-id="b2919-111">They can be nested, reused, and shared among projects.</span></span>

## <a name="component-classes"></a><span data-ttu-id="b2919-112">Классы компонентов</span><span class="sxs-lookup"><span data-stu-id="b2919-112">Component classes</span></span>

<span data-ttu-id="b2919-113">Компоненты обычно выполнены в *.cshtml* файлы, используя сочетание C# и HTML-разметка.</span><span class="sxs-lookup"><span data-stu-id="b2919-113">Components are typically implemented in *.cshtml* files using a combination of C# and HTML markup.</span></span> <span data-ttu-id="b2919-114">Пользовательский Интерфейс для компонента определяется с помощью HTML.</span><span class="sxs-lookup"><span data-stu-id="b2919-114">The UI for a component is defined using HTML.</span></span> <span data-ttu-id="b2919-115">Логика динамического отображения (например выражения, циклы и условные выражения) добавляется с помощью встроенного синтаксиса C# под названием [Razor](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="b2919-115">Dynamic rendering logic (for example, loops, conditionals, expressions) is added using an embedded C# syntax called [Razor](xref:mvc/views/razor).</span></span> <span data-ttu-id="b2919-116">При компиляции приложения компонентов Razor, HTML-разметка и C# логикой отрисовки, преобразуются в класс компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-116">When a Razor Components app is compiled, the HTML markup and C# rendering logic are converted into a component class.</span></span> <span data-ttu-id="b2919-117">Имя создаваемого класса соответствует имени файла.</span><span class="sxs-lookup"><span data-stu-id="b2919-117">The name of the generated class matches the name of the file.</span></span>

<span data-ttu-id="b2919-118">Члены класса компонента определены `@functions` блока (более одного `@functions` блок является допустимым).</span><span class="sxs-lookup"><span data-stu-id="b2919-118">Members of the component class are defined in a `@functions` block (more than one `@functions` block is permissible).</span></span> <span data-ttu-id="b2919-119">В `@functions` блока, состояние компонентов (свойства, поля) указан вместе с методы для обработки событий или для определения других логикой компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-119">In the `@functions` block, component state (properties, fields) is specified along with methods for event handling or for defining other component logic.</span></span>

<span data-ttu-id="b2919-120">Затем можно использовать члены компонента, как отрисовки части компонента приложения логики с помощью C# выражения, которые начинаются с `@`.</span><span class="sxs-lookup"><span data-stu-id="b2919-120">Component members can then be used as part of the component's rendering logic using C# expressions that start with `@`.</span></span> <span data-ttu-id="b2919-121">Например C# поле визуализируется с помощью префикса `@` на имя поля.</span><span class="sxs-lookup"><span data-stu-id="b2919-121">For example, a C# field is rendered by prefixing `@` to the field name.</span></span> <span data-ttu-id="b2919-122">Следующий пример вычисляет и отображает:</span><span class="sxs-lookup"><span data-stu-id="b2919-122">The following example evaluates and renders:</span></span>

* <span data-ttu-id="b2919-123">`_headingFontStyle` значение свойства CSS для `font-style`.</span><span class="sxs-lookup"><span data-stu-id="b2919-123">`_headingFontStyle` to the CSS property value for `font-style`.</span></span>
* <span data-ttu-id="b2919-124">`_headingText` к содержимому `<h1>` элемент.</span><span class="sxs-lookup"><span data-stu-id="b2919-124">`_headingText` to the content of the `<h1>` element.</span></span>

```cshtml
<h1 style="font-style:@_headingFontStyle">@_headingText</h1>

@functions {
    private string _headingFontStyle = "italic";
    private string _headingText = "Put on your new Blazor!";
}
```

<span data-ttu-id="b2919-125">После изначально визуализируется компонента, компонент повторно создает его дерева визуализации в ответ на события.</span><span class="sxs-lookup"><span data-stu-id="b2919-125">After the component is initially rendered, the component regenerates its render tree in response to events.</span></span> <span data-ttu-id="b2919-126">Компоненты Razor затем сравнивает новое дерево визуализации от предыдущей и применяет все изменения для модели объектов обозревателя документов (DOM).</span><span class="sxs-lookup"><span data-stu-id="b2919-126">Razor Components then compares the new render tree against the previous one and applies any modifications to the browser's Document Object Model (DOM).</span></span>

## <a name="using-components"></a><span data-ttu-id="b2919-127">Использование компонентов</span><span class="sxs-lookup"><span data-stu-id="b2919-127">Using components</span></span>

<span data-ttu-id="b2919-128">Компоненты можно добавить и другие компоненты, объявляя их с использованием синтаксиса элемента HTML.</span><span class="sxs-lookup"><span data-stu-id="b2919-128">Components can include other components by declaring them using HTML element syntax.</span></span> <span data-ttu-id="b2919-129">Разметка для использования компонента выглядит как тег HTML с именем, соответствующем типу компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-129">The markup for using a component looks like an HTML tag where the name of the tag is the component type.</span></span>

<span data-ttu-id="b2919-130">Следующая разметка отображает `HeadingComponent` (*HeadingComponent.cshtml*) экземпляр:</span><span class="sxs-lookup"><span data-stu-id="b2919-130">The following markup renders a `HeadingComponent` (*HeadingComponent.cshtml*) instance:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/Index.cshtml?name=snippet_HeadingComponent)]

## <a name="component-parameters"></a><span data-ttu-id="b2919-131">Параметры компонентов</span><span class="sxs-lookup"><span data-stu-id="b2919-131">Component parameters</span></span>

<span data-ttu-id="b2919-132">Компоненты могут иметь *параметры компонента*, которые определены с помощью *закрытые* оформлен свойства класса компонента `[Parameter]`.</span><span class="sxs-lookup"><span data-stu-id="b2919-132">Components can have *component parameters*, which are defined using *non-public* properties on the component class decorated with `[Parameter]`.</span></span> <span data-ttu-id="b2919-133">Используйте атрибуты, чтобы указать аргументы для компонента в разметке.</span><span class="sxs-lookup"><span data-stu-id="b2919-133">Use attributes to specify arguments for a component in markup.</span></span>

<span data-ttu-id="b2919-134">В следующем примере `ParentComponent` задает значение `Title` свойство `ChildComponent`:</span><span class="sxs-lookup"><span data-stu-id="b2919-134">In the following example, the `ParentComponent` sets the value of the `Title` property of the `ChildComponent`:</span></span>

<span data-ttu-id="b2919-135">*ParentComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-135">*ParentComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=5)]

<span data-ttu-id="b2919-136">*ChildComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-136">*ChildComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=7-8)]

## <a name="child-content"></a><span data-ttu-id="b2919-137">Дочерний тип содержимого</span><span class="sxs-lookup"><span data-stu-id="b2919-137">Child content</span></span>

<span data-ttu-id="b2919-138">Компоненты можно установить содержимое из другого компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-138">Components can set the content of another component.</span></span> <span data-ttu-id="b2919-139">Назначение компонента предоставляет содержимое между тегами, указывающие получатель.</span><span class="sxs-lookup"><span data-stu-id="b2919-139">The assigning component provides the content between the tags that specify the receiving component.</span></span> <span data-ttu-id="b2919-140">Например `ParentComponent` можно предоставить содержимое для подготовки к просмотру, дочернего компонента, поместив содержимое внутри `<ChildComponent>` теги.</span><span class="sxs-lookup"><span data-stu-id="b2919-140">For example, a `ParentComponent` can provide content for rendering by a Child component by placing the content inside `<ChildComponent>` tags.</span></span>

<span data-ttu-id="b2919-141">*ParentComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-141">*ParentComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=6-7)]

<span data-ttu-id="b2919-142">У компонента дочерних `ChildContent` свойство, которое представляет `RenderFragment`.</span><span class="sxs-lookup"><span data-stu-id="b2919-142">The Child component has a `ChildContent` property that represents a `RenderFragment`.</span></span> <span data-ttu-id="b2919-143">Значение `ChildContent` располагается в разметку дочерних компонентов, где должны отображаться содержимое.</span><span class="sxs-lookup"><span data-stu-id="b2919-143">The value of `ChildContent` is positioned in the child component's markup where the content should be rendered.</span></span> <span data-ttu-id="b2919-144">В следующем примере значение `ChildContent` получен из родительского компонента и отображено внутри панели начальной загрузки `panel-body`.</span><span class="sxs-lookup"><span data-stu-id="b2919-144">In the following example, the value of `ChildContent` is received from the parent component and rendered inside the Bootstrap panel's `panel-body`.</span></span>

<span data-ttu-id="b2919-145">*ChildComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-145">*ChildComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=3,10-11)]

> [!NOTE]
> <span data-ttu-id="b2919-146">Получение свойств `RenderFragment` содержимого должен иметь имя `ChildContent` по соглашению.</span><span class="sxs-lookup"><span data-stu-id="b2919-146">The property receiving the `RenderFragment` content must be named `ChildContent` by convention.</span></span>

## <a name="data-binding"></a><span data-ttu-id="b2919-147">привязка данных,</span><span class="sxs-lookup"><span data-stu-id="b2919-147">Data binding</span></span>

<span data-ttu-id="b2919-148">Привязка данных для компонентов и элементов DOM осуществляется с помощью `bind` атрибута.</span><span class="sxs-lookup"><span data-stu-id="b2919-148">Data binding to both components and DOM elements is accomplished with the `bind` attribute.</span></span> <span data-ttu-id="b2919-149">Следующий пример связывает `ItalicsCheck` свойство флажок проверки состояния:</span><span class="sxs-lookup"><span data-stu-id="b2919-149">The following example binds the `ItalicsCheck` property to the check box's checked state:</span></span>

```cshtml
<input type="checkbox" class="form-check-input" id="italicsCheck" 
    bind="@_italicsCheck" />
```

<span data-ttu-id="b2919-150">Если флажок выбран и очищен, значение свойства присваивается `true` и `false`, соответственно.</span><span class="sxs-lookup"><span data-stu-id="b2919-150">When the check box is selected and cleared, the property's value is updated to `true` and `false`, respectively.</span></span>

<span data-ttu-id="b2919-151">Флажок в пользовательском Интерфейсе обновляется, только в том случае, когда компонент отображается, не в ответ на изменение значения свойства.</span><span class="sxs-lookup"><span data-stu-id="b2919-151">The check box is updated in the UI only when the component is rendered, not in response to changing the property's value.</span></span> <span data-ttu-id="b2919-152">Так как компоненты отображаются после выполнения код обработчика событий, обновления свойств обычно отражаются в пользовательском Интерфейсе сразу же.</span><span class="sxs-lookup"><span data-stu-id="b2919-152">Since components render themselves after event handler code executes, property updates are usually reflected in the UI immediately.</span></span>

<span data-ttu-id="b2919-153">С помощью `bind` с `CurrentValue` свойство (`<input bind="@CurrentValue" />`) является по существу эквивалентно следующему:</span><span class="sxs-lookup"><span data-stu-id="b2919-153">Using `bind` with a `CurrentValue` property (`<input bind="@CurrentValue" />`) is essentially equivalent to the following:</span></span>

```cshtml
<input value="@CurrentValue" 
    onchange="@((UIChangeEventArgs __e) => CurrentValue = __e.Value)" />
```

<span data-ttu-id="b2919-154">При отображении компонента `value` элемента ввода поступают из `CurrentValue` свойство.</span><span class="sxs-lookup"><span data-stu-id="b2919-154">When the component is rendered, the `value` of the input element comes from the `CurrentValue` property.</span></span> <span data-ttu-id="b2919-155">Когда пользователь вводит в текстовом поле `onchange` события и `CurrentValue` свойству присваивается измененное значение.</span><span class="sxs-lookup"><span data-stu-id="b2919-155">When the user types in the text box, the `onchange` event is fired and the `CurrentValue` property is set to the changed value.</span></span> <span data-ttu-id="b2919-156">На самом деле, формирования кода является чуть более сложный, так как `bind` обрабатывает несколько случаев, когда выполняются преобразования типов.</span><span class="sxs-lookup"><span data-stu-id="b2919-156">In reality, the code generation is a little more complex because `bind` handles a few cases where type conversions are performed.</span></span> <span data-ttu-id="b2919-157">В принципе `bind` связывает текущее значение выражения с `value` атрибут и обрабатывает изменения, с помощью зарегистрированного обработчика.</span><span class="sxs-lookup"><span data-stu-id="b2919-157">In principle, `bind` associates the current value of an expression with a `value` attribute and handles changes using the registered handler.</span></span>

<span data-ttu-id="b2919-158">**Строки формата**</span><span class="sxs-lookup"><span data-stu-id="b2919-158">**Format strings**</span></span>

<span data-ttu-id="b2919-159">Привязка данных работает с <xref:System.DateTime> форматирования строк.</span><span class="sxs-lookup"><span data-stu-id="b2919-159">Data binding works with <xref:System.DateTime> format strings.</span></span> <span data-ttu-id="b2919-160">В настоящее время недоступны другие выражения формат, например валюта или числовые форматы.</span><span class="sxs-lookup"><span data-stu-id="b2919-160">Other format expressions, such as currency or number formats, aren't available at this time.</span></span>

```cshtml
<input bind="@StartDate" format-value="yyyy-MM-dd" />

@functions {
    [Parameter]
    private DateTime StartDate { get; set; } = new DateTime(2020, 1, 1);
}
```

<span data-ttu-id="b2919-161">`format-value` Атрибут указывает формат даты для применения к `value` из `input` элемент.</span><span class="sxs-lookup"><span data-stu-id="b2919-161">The `format-value` attribute specifies the date format to apply to the `value` of the `input` element.</span></span> <span data-ttu-id="b2919-162">Выполнить синтаксический анализ значение также используется формат при `onchange` событием.</span><span class="sxs-lookup"><span data-stu-id="b2919-162">The format is also used to parse the value when an `onchange` event occurs.</span></span>

<span data-ttu-id="b2919-163">**Параметры компонента**</span><span class="sxs-lookup"><span data-stu-id="b2919-163">**Component parameters**</span></span>

<span data-ttu-id="b2919-164">Привязки также распознает параметры компонента, где `bind-{property}` можно привязать значение свойства по компонентам.</span><span class="sxs-lookup"><span data-stu-id="b2919-164">Binding also recognizes component parameters, where `bind-{property}` can bind a property value across components.</span></span>

<span data-ttu-id="b2919-165">В следующем компоненте используются `ChildComponent` и привязывает `ParentYear` параметр из родительского `Year` параметр в компоненте дочерних:</span><span class="sxs-lookup"><span data-stu-id="b2919-165">The following component uses `ChildComponent` and binds the `ParentYear` parameter from the parent to the `Year` parameter on the child component:</span></span>

<span data-ttu-id="b2919-166">Родительский компонент:</span><span class="sxs-lookup"><span data-stu-id="b2919-166">Parent component:</span></span>

```cshtml
@page "/ParentComponent"

<h1>Parent Component</h1>

<p>ParentYear: @ParentYear</p>

<ChildComponent bind-Year="@ParentYear" />

<button class="btn btn-primary" onclick="@ChangeTheYear">
    Change Year to 1986
</button>

@functions {
    [Parameter]
    private int ParentYear { get; set; } = 1978;

    void ChangeTheYear()
    {
        ParentYear = 1986;
    }
}
```

<span data-ttu-id="b2919-167">Дочерний компонент:</span><span class="sxs-lookup"><span data-stu-id="b2919-167">Child component:</span></span>

```cshtml
<h2>Child Component</h2>

<p>Year: @Year</p>

@functions {
    [Parameter]
    private int Year { get; set; }

    [Parameter]
    private Action<int> YearChanged { get; set; }
}
```

<span data-ttu-id="b2919-168">`Year` Параметра возможности привязки, поскольку в нем вспомогательное `YearChanged` событие, которое совпадает с типом `Year` параметра.</span><span class="sxs-lookup"><span data-stu-id="b2919-168">The `Year` parameter is bindable because it has a companion `YearChanged` event that matches the type of the `Year` parameter.</span></span>

<span data-ttu-id="b2919-169">Загрузка `ParentComponent` создает следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="b2919-169">Loading the `ParentComponent` produces the following markup:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1978</p>

<h2>Child Component</h2>

<p>Year: 1978</p>
```

<span data-ttu-id="b2919-170">Если значение `ParentYear` изменении свойства, нажав кнопку в `ParentComponent`, `Year` свойство `ChildComponent` обновляется.</span><span class="sxs-lookup"><span data-stu-id="b2919-170">If the value of the `ParentYear` property is changed by selecting the button in the `ParentComponent`, the `Year` property of the `ChildComponent` is updated.</span></span> <span data-ttu-id="b2919-171">Новое значение `Year` отображается в пользовательском Интерфейсе при `ParentComponent` когда:</span><span class="sxs-lookup"><span data-stu-id="b2919-171">The new value of `Year` is rendered in the UI when the `ParentComponent` is rerendered:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1986</p>

<h2>Child Component</h2>

<p>Year: 1986</p>
```

## <a name="event-handling"></a><span data-ttu-id="b2919-172">Обработка событий</span><span class="sxs-lookup"><span data-stu-id="b2919-172">Event handling</span></span>

<span data-ttu-id="b2919-173">Компоненты Razor обеспечивают функции обработки событий.</span><span class="sxs-lookup"><span data-stu-id="b2919-173">Razor Components provide event handling features.</span></span> <span data-ttu-id="b2919-174">Для атрибута элемент HTML с именем `on<event>` (например, `onclick`, `onsubmit`) со значением, типом делегата, компоненты Razor обрабатывает значение атрибута как обработчик событий.</span><span class="sxs-lookup"><span data-stu-id="b2919-174">For an HTML element attribute named `on<event>` (for example, `onclick`, `onsubmit`) with a delegate-typed value, Razor Components treats the attribute's value as an event handler.</span></span> <span data-ttu-id="b2919-175">Имя атрибута всегда начинается с `on`.</span><span class="sxs-lookup"><span data-stu-id="b2919-175">The attribute's name always starts with `on`.</span></span>

<span data-ttu-id="b2919-176">Следующий код вызывает `UpdateHeading` метод при нажатии кнопки в пользовательском Интерфейсе:</span><span class="sxs-lookup"><span data-stu-id="b2919-176">The following code calls the `UpdateHeading` method when the button is selected in the UI:</span></span>

```cshtml
<button class="btn btn-primary" onclick="@UpdateHeading">
    Update heading
</button>

@functions {
    void UpdateHeading(UIMouseEventArgs e)
    {
        ...
    }
}
```

<span data-ttu-id="b2919-177">Следующий код вызывает `CheckboxChanged` метода при его изменении в пользовательском Интерфейсе:</span><span class="sxs-lookup"><span data-stu-id="b2919-177">The following code calls the `CheckboxChanged` method when the check box is changed in the UI:</span></span>

```cshtml
<input type="checkbox" class="form-check-input" onchange="@CheckboxChanged" />

@functions {
    void CheckboxChanged()
    {
        ...
    }
}
```

<span data-ttu-id="b2919-178">Обработчики событий также может быть асинхронной и возврата <xref:System.Threading.Tasks.Task>.</span><span class="sxs-lookup"><span data-stu-id="b2919-178">Event handlers can also be asynchronous and return a <xref:System.Threading.Tasks.Task>.</span></span> <span data-ttu-id="b2919-179">Нет необходимости вручную вызывать функции `StateHasChanged()`.</span><span class="sxs-lookup"><span data-stu-id="b2919-179">There's no need to manually call `StateHasChanged()`.</span></span> <span data-ttu-id="b2919-180">Исключения записываются при их возникновении.</span><span class="sxs-lookup"><span data-stu-id="b2919-180">Exceptions are logged when they occur.</span></span>

```cshtml
<button class="btn btn-primary" onclick="@UpdateHeading">
    Update heading
</button>

@functions {
    async Task UpdateHeading(UIMouseEventArgs e)
    {
        ...
    }
}
```

<span data-ttu-id="b2919-181">Для некоторых событий допускаются типы аргументов событий, связанных с событием.</span><span class="sxs-lookup"><span data-stu-id="b2919-181">For some events, event-specific event argument types are permitted.</span></span> <span data-ttu-id="b2919-182">Если доступ к одному из таких типов событий, не является обязательным, это не обязательно в вызове метода.</span><span class="sxs-lookup"><span data-stu-id="b2919-182">If access to one of these event types isn't necessary, it isn't required in the method call.</span></span>

<span data-ttu-id="b2919-183">Приведен список событий, поддерживаемые аргументы.</span><span class="sxs-lookup"><span data-stu-id="b2919-183">The list of supported event arguments is:</span></span>

* <span data-ttu-id="b2919-184">UIEventArgs</span><span class="sxs-lookup"><span data-stu-id="b2919-184">UIEventArgs</span></span>
* <span data-ttu-id="b2919-185">UIChangeEventArgs</span><span class="sxs-lookup"><span data-stu-id="b2919-185">UIChangeEventArgs</span></span>
* <span data-ttu-id="b2919-186">UIKeyboardEventArgs</span><span class="sxs-lookup"><span data-stu-id="b2919-186">UIKeyboardEventArgs</span></span>
* <span data-ttu-id="b2919-187">UIMouseEventArgs</span><span class="sxs-lookup"><span data-stu-id="b2919-187">UIMouseEventArgs</span></span>

<span data-ttu-id="b2919-188">Можно также использовать лямбда-выражения:</span><span class="sxs-lookup"><span data-stu-id="b2919-188">Lambda expressions can also be used:</span></span>

```cshtml
<button onclick="@(e => Console.WriteLine("Hello, world!"))">Say hello</button>
```

<span data-ttu-id="b2919-189">Часто бывает удобно закрыть через дополнительные значения, такие как при итерации по набору элементов.</span><span class="sxs-lookup"><span data-stu-id="b2919-189">It's often convenient to close over additional values, such as when iterating over a set of elements.</span></span> <span data-ttu-id="b2919-190">В следующем примере создается три кнопки, каждый из которых вызывает `UpdateHeading` передача аргумента события (`UIMouseEventArgs`) и ее номер кнопки (`buttonNumber`) при выборе в пользовательском Интерфейсе:</span><span class="sxs-lookup"><span data-stu-id="b2919-190">The following example creates three buttons, each of which calls `UpdateHeading` passing an event argument (`UIMouseEventArgs`) and its button number (`buttonNumber`) when selected in the UI:</span></span>

```cshtml
<h2>@message</h2>

@for (var i = 1; i < 4; i++)
{
    var buttonNumber = i;

    <button class="btn btn-primary" 
            onclick="@(e => UpdateHeading(e, buttonNumber))">
        Button #@i
    </button>
}

@functions {
    string message = "Select a button to learn its position.";

    void UpdateHeading(UIMouseEventArgs e, int buttonNumber)
    {
        message = $"You selected Button #{buttonNumber} at " +
            "mouse position: {e.ClientX} X {e.ClientY}.";
    }
}
```

## <a name="capture-references-to-components"></a><span data-ttu-id="b2919-191">Захват ссылки на компоненты</span><span class="sxs-lookup"><span data-stu-id="b2919-191">Capture references to components</span></span>

<span data-ttu-id="b2919-192">Ссылки на компонент предоставить образом получить ссылку на экземпляр компонента таким образом, вы сможете выполнять команды для этого экземпляра, такие как `Show` или `Reset`.</span><span class="sxs-lookup"><span data-stu-id="b2919-192">Component references provide a way get a reference to a component instance so that you can issue commands to that instance, such as `Show` or `Reset`.</span></span> <span data-ttu-id="b2919-193">Чтобы записать ссылку на компонент, добавьте `ref` атрибут дочерний компонент, а затем определите поле с тем же именем и типом как дочерний компонент.</span><span class="sxs-lookup"><span data-stu-id="b2919-193">To capture a component reference, add a `ref` attribute to the child component and then define a field with the same name and the same type as the child component.</span></span>

```cshtml
<MyLoginDialog ref="loginDialog" ... />

@functions {
    MyLoginDialog loginDialog;

    void OnSomething()
    {
        loginDialog.Show();
    }
}
```

<span data-ttu-id="b2919-194">При отображении компонента `loginDialog` поле заполняется `MyLoginDialog` дочерний экземпляр компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-194">When the component is rendered, the `loginDialog` field is populated with the `MyLoginDialog` child component instance.</span></span> <span data-ttu-id="b2919-195">Затем можно вызывать методы .NET экземпляра компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-195">You can then invoke .NET methods on the component instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b2919-196">`loginDialog` Переменной заполняется только после того как компонент отображается, и его выходные данные содержат `MyLoginDialog` элемент.</span><span class="sxs-lookup"><span data-stu-id="b2919-196">The `loginDialog` variable is only populated after the component is rendered and its output includes the `MyLoginDialog` element.</span></span> <span data-ttu-id="b2919-197">До этого момента нет ничего для ссылки.</span><span class="sxs-lookup"><span data-stu-id="b2919-197">Until that point, there's nothing to reference.</span></span> <span data-ttu-id="b2919-198">Используются для операций ссылки на компонентов после завершения подготовки к просмотру компонента `OnAfterRenderAsync` или `OnAfterRender` методы.</span><span class="sxs-lookup"><span data-stu-id="b2919-198">To manipulate components references after the component has finished rendering, use the `OnAfterRenderAsync` or `OnAfterRender` methods.</span></span>

<span data-ttu-id="b2919-199">Тогда как захват ссылки на компонент использует аналогичный синтаксис для [захват ссылок на элементы](xref:razor-components/javascript-interop#capture-references-to-elements), это не так [взаимодействия JavaScript](xref:razor-components/javascript-interop) функции.</span><span class="sxs-lookup"><span data-stu-id="b2919-199">While capturing component references uses a similar syntax to [capturing element references](xref:razor-components/javascript-interop#capture-references-to-elements), it isn't a [JavaScript interop](xref:razor-components/javascript-interop) feature.</span></span> <span data-ttu-id="b2919-200">Ссылки на компонент не передаются в код JavaScript; они используются только в коде .NET.</span><span class="sxs-lookup"><span data-stu-id="b2919-200">Component references aren't passed to JavaScript code; they're only used in .NET code.</span></span>

> [!NOTE]
> <span data-ttu-id="b2919-201">Сделать **не** использовать ссылки на компонент изменяемая состояние дочерних компонентов.</span><span class="sxs-lookup"><span data-stu-id="b2919-201">Do **not** use component references to mutate the state of child components.</span></span> <span data-ttu-id="b2919-202">Вместо этого используйте обычный декларативные параметры для передачи данных дочерними компонентами.</span><span class="sxs-lookup"><span data-stu-id="b2919-202">Instead, use normal declarative parameters to pass data to child components.</span></span> <span data-ttu-id="b2919-203">В результате дочерними компонентами для rerender правильность времени автоматически.</span><span class="sxs-lookup"><span data-stu-id="b2919-203">This causes child components to rerender at the correct times automatically.</span></span>

## <a name="lifecycle-methods"></a><span data-ttu-id="b2919-204">Методы жизненного цикла</span><span class="sxs-lookup"><span data-stu-id="b2919-204">Lifecycle methods</span></span>

<span data-ttu-id="b2919-205">`OnInitAsync` и `OnInit` выполнять код для инициализации компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-205">`OnInitAsync` and `OnInit` execute code to initialize the component.</span></span> <span data-ttu-id="b2919-206">Чтобы выполнить асинхронную операцию, используйте `OnInitAsync` и `await` ключевое слово на операцию:</span><span class="sxs-lookup"><span data-stu-id="b2919-206">To perform an asynchronous operation, use `OnInitAsync` and the `await` keyword on the operation:</span></span>

```csharp
protected override async Task OnInitAsync()
{
    await ...
}
```

<span data-ttu-id="b2919-207">Синхронную операцию, используйте `OnInit`:</span><span class="sxs-lookup"><span data-stu-id="b2919-207">For a synchronous operation, use `OnInit`:</span></span>

```csharp
protected override void OnInit()
{
    ...
}
```

<span data-ttu-id="b2919-208">`OnParametersSetAsync` и `OnParametersSet` вызываются, когда компонент получил параметров из его родительского элемента и значения присваиваются свойствам.</span><span class="sxs-lookup"><span data-stu-id="b2919-208">`OnParametersSetAsync` and `OnParametersSet` are called when a component has received parameters from its parent and the values are assigned to properties.</span></span> <span data-ttu-id="b2919-209">Эти методы применяются после инициализации компонента и затем каждый раз компонент отображается:</span><span class="sxs-lookup"><span data-stu-id="b2919-209">These methods are executed after component initialization and then each time the component is rendered:</span></span>

```csharp
protected override async Task OnParametersSetAsync()
{
    await ...
}
```

```csharp
protected override void OnParametersSet()
{
    ...
}
```

<span data-ttu-id="b2919-210">`OnAfterRenderAsync` и `OnAfterRender` вызываются после компонент завершил отрисовку.</span><span class="sxs-lookup"><span data-stu-id="b2919-210">`OnAfterRenderAsync` and `OnAfterRender` are called after a component has finished rendering.</span></span> <span data-ttu-id="b2919-211">На этом этапе заполняются ссылки на элемент и компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-211">Element and component references are populated at this point.</span></span> <span data-ttu-id="b2919-212">Позволяет выполнять дополнительные действия по инициализации с использованием готового для просмотра содержимого, например активация сторонних библиотек JavaScript, которые оперируют визуализированных элементов DOM этого этапа.</span><span class="sxs-lookup"><span data-stu-id="b2919-212">Use this stage to perform additional initialization steps using the rendered content, such as activating third-party JavaScript libraries that operate on the rendered DOM elements.</span></span>

```csharp
protected override async Task OnAfterRenderAsync()
{
    await ...
}
```

```csharp
protected override void OnAfterRender()
{
    ...
}
```

<span data-ttu-id="b2919-213">`SetParameters` можно переопределить, чтобы выполнять код до параметры заданы:</span><span class="sxs-lookup"><span data-stu-id="b2919-213">`SetParameters` can be overridden to execute code before parameters are set:</span></span>

```csharp
public override void SetParameters(ParameterCollection parameters)
{
    ...

    base.SetParameters(parameters);
}
```

<span data-ttu-id="b2919-214">Если `base.SetParameters` не вызван, пользовательский код может интерпретировать входящее значение параметров в любом способом требуется.</span><span class="sxs-lookup"><span data-stu-id="b2919-214">If `base.SetParameters` isn't invoked, the custom code can interpret the incoming parameters value in any way required.</span></span> <span data-ttu-id="b2919-215">Например параметры входящего не обязательно должны назначаться свойства класса.</span><span class="sxs-lookup"><span data-stu-id="b2919-215">For example, the incoming parameters aren't required to be assigned to the properties on the class.</span></span>

<span data-ttu-id="b2919-216">`ShouldRender` можно переопределить для подавления обновление пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b2919-216">`ShouldRender` can be overridden to suppress refreshing of the UI.</span></span> <span data-ttu-id="b2919-217">Если реализация возвращает `true`, обновляется пользовательский Интерфейс.</span><span class="sxs-lookup"><span data-stu-id="b2919-217">If the implementation returns `true`, the UI is refreshed.</span></span> <span data-ttu-id="b2919-218">Даже если `ShouldRender` будет переопределено, компонент всегда изначально визуализируется.</span><span class="sxs-lookup"><span data-stu-id="b2919-218">Even if `ShouldRender` is overridden, the component is always initially rendered.</span></span>

```csharp
protected override bool ShouldRender()
{
    var renderUI = true;

    return renderUI;
}
```

## <a name="component-disposal-with-idisposable"></a><span data-ttu-id="b2919-219">Реализация компонента с IDisposable</span><span class="sxs-lookup"><span data-stu-id="b2919-219">Component disposal with IDisposable</span></span>

<span data-ttu-id="b2919-220">Если компонент реализует <xref:System.IDisposable>, [метод Dispose](/dotnet/standard/garbage-collection/implementing-dispose) вызывается, когда компонент будет удален из пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b2919-220">If a component implements <xref:System.IDisposable>, the [Dispose method](/dotnet/standard/garbage-collection/implementing-dispose) is called when the component is removed from the UI.</span></span> <span data-ttu-id="b2919-221">В следующем компоненте используются `@implements IDisposable` и `Dispose` метод:</span><span class="sxs-lookup"><span data-stu-id="b2919-221">The following component uses `@implements IDisposable` and the `Dispose` method:</span></span>

```csharp
@using System
@implements IDisposable

...

@functions {
    public void Dispose()
    {
        ...
    }
}
```

## <a name="routing"></a><span data-ttu-id="b2919-222">Маршрутизация</span><span class="sxs-lookup"><span data-stu-id="b2919-222">Routing</span></span>

<span data-ttu-id="b2919-223">Маршрутизация в компонентах Razor достигается с помощью шаблона маршрута для каждого компонента, доступного в приложении.</span><span class="sxs-lookup"><span data-stu-id="b2919-223">Routing in Razor Components is achieved by providing a route template to each accessible component in the app.</span></span>

<span data-ttu-id="b2919-224">Когда *.cshtml* файл с `@page` компилируется директивы, созданном классе ему присваивается <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> указания шаблона маршрута.</span><span class="sxs-lookup"><span data-stu-id="b2919-224">When a *.cshtml* file with an `@page` directive is compiled, the generated class is given a <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> specifying the route template.</span></span> <span data-ttu-id="b2919-225">Во время выполнения, маршрутизатор ищет классы компонентов с `RouteAttribute` и отображает, какой компонент имеет шаблон маршрута, соответствующий запрошенного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="b2919-225">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="b2919-226">Несколько шаблонов маршрута могут применяться к компоненту.</span><span class="sxs-lookup"><span data-stu-id="b2919-226">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="b2919-227">Следующий компонент отвечает на запросы для `/BlazorRoute` и `/DifferentBlazorRoute`:</span><span class="sxs-lookup"><span data-stu-id="b2919-227">The following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?name=snippet_BlazorRoute)]

## <a name="route-parameters"></a><span data-ttu-id="b2919-228">Параметры маршрута</span><span class="sxs-lookup"><span data-stu-id="b2919-228">Route parameters</span></span>

<span data-ttu-id="b2919-229">Компоненты могут получать параметры маршрута с шаблоном маршрута в `@page` директива.</span><span class="sxs-lookup"><span data-stu-id="b2919-229">Components can receive route parameters from the route template provided in the `@page` directive.</span></span> <span data-ttu-id="b2919-230">Маршрутизатор использует параметры маршрута для заполнения соответствующих параметров компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-230">The router uses route parameters to populate the corresponding component parameters.</span></span>

<span data-ttu-id="b2919-231">*RouteParameter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-231">*RouteParameter.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?name=snippet_RouteParameter)]

<span data-ttu-id="b2919-232">Необязательные параметры не поддерживаются, так что два `@page` директивы применяются в приведенном выше примере.</span><span class="sxs-lookup"><span data-stu-id="b2919-232">Optional parameters aren't supported, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="b2919-233">Первый позволяет навигации к компоненту без параметров.</span><span class="sxs-lookup"><span data-stu-id="b2919-233">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="b2919-234">Второй `@page` принимает директивы `{text}` параметра маршрута и присваивает это значение `Text` свойства.</span><span class="sxs-lookup"><span data-stu-id="b2919-234">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="base-class-inheritance-for-a-code-behind-experience"></a><span data-ttu-id="b2919-235">Наследование базовый класс для взаимодействия кода «программной»</span><span class="sxs-lookup"><span data-stu-id="b2919-235">Base class inheritance for a "code-behind" experience</span></span>

<span data-ttu-id="b2919-236">Файлы компонентов (*.cshtml*) смешивать разметки HTML и C# обработке кода в одном файле.</span><span class="sxs-lookup"><span data-stu-id="b2919-236">Component files (*.cshtml*) mix HTML markup and C# processing code in the same file.</span></span> <span data-ttu-id="b2919-237">`@inherits` Директива может использоваться для предоставления Razor компонентов приложений с интерфейсом «кода», разделяющий разметки компонента из кода обработки.</span><span class="sxs-lookup"><span data-stu-id="b2919-237">The `@inherits` directive can be used to provide Razor Components apps with a "code-behind" experience that separates component markup from processing code.</span></span>

<span data-ttu-id="b2919-238">[Пример приложения](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) показано, как компонент может наследовать базовому классу, `BlazorRocksBase`, чтобы предоставлять методы и свойства компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-238">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) shows how a component can inherit a base class, `BlazorRocksBase`, to provide the component's properties and methods.</span></span>

<span data-ttu-id="b2919-239">*BlazorRocks.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-239">*BlazorRocks.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRocks.cshtml?name=snippet_BlazorRocks)]

<span data-ttu-id="b2919-240">*BlazorRocksBase.cs*:</span><span class="sxs-lookup"><span data-stu-id="b2919-240">*BlazorRocksBase.cs*:</span></span>

[!code-csharp[](common/samples/3.x/BlazorSample/Pages/BlazorRocksBase.cs)]

<span data-ttu-id="b2919-241">Базовый класс должен быть производным от `BlazorComponent`.</span><span class="sxs-lookup"><span data-stu-id="b2919-241">The base class should derive from `BlazorComponent`.</span></span>

## <a name="razor-support"></a><span data-ttu-id="b2919-242">Поддержка Razor</span><span class="sxs-lookup"><span data-stu-id="b2919-242">Razor support</span></span>

<span data-ttu-id="b2919-243">**Директивы Razor**</span><span class="sxs-lookup"><span data-stu-id="b2919-243">**Razor directives**</span></span>

<span data-ttu-id="b2919-244">В следующей таблице показаны директивы Razor.</span><span class="sxs-lookup"><span data-stu-id="b2919-244">Razor directives are shown in the following table.</span></span>

| <span data-ttu-id="b2919-245">Директива</span><span class="sxs-lookup"><span data-stu-id="b2919-245">Directive</span></span> | <span data-ttu-id="b2919-246">Описание:</span><span class="sxs-lookup"><span data-stu-id="b2919-246">Description</span></span> |
| --------- | ----------- |
| [<span data-ttu-id="b2919-247">\@Функции</span><span class="sxs-lookup"><span data-stu-id="b2919-247">\@functions</span></span>](xref:mvc/views/razor#section-5) | <span data-ttu-id="b2919-248">Добавляет C# блок кода в компонент.</span><span class="sxs-lookup"><span data-stu-id="b2919-248">Adds a C# code block to a component.</span></span> |
| `@implements` | <span data-ttu-id="b2919-249">Реализует интерфейс для класса созданный компонент.</span><span class="sxs-lookup"><span data-stu-id="b2919-249">Implements an interface for the generated component class.</span></span> |
| [<span data-ttu-id="b2919-250">\@Наследует</span><span class="sxs-lookup"><span data-stu-id="b2919-250">\@inherits</span></span>](xref:mvc/views/razor#section-3) | <span data-ttu-id="b2919-251">Предоставляет полный контроль над класс, который наследует компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-251">Provides full control of the class that the component inherits.</span></span> |
| [<span data-ttu-id="b2919-252">\@внедрить</span><span class="sxs-lookup"><span data-stu-id="b2919-252">\@inject</span></span>](xref:mvc/views/razor#section-4) | <span data-ttu-id="b2919-253">Позволяет услуг внедрения из [контейнер службы](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="b2919-253">Enables service injection from the [service container](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="b2919-254">Дополнительные сведения: [Внедрение зависимостей в представления](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="b2919-254">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span> |
| `@layout` | <span data-ttu-id="b2919-255">Указывает компонента макета.</span><span class="sxs-lookup"><span data-stu-id="b2919-255">Specifies a layout component.</span></span> <span data-ttu-id="b2919-256">Компоненты макета используются во избежание дублирования и несогласованности.</span><span class="sxs-lookup"><span data-stu-id="b2919-256">Layout components are used to avoid code duplication and inconsistency.</span></span> |
| [<span data-ttu-id="b2919-257">\@Страница</span><span class="sxs-lookup"><span data-stu-id="b2919-257">\@page</span></span>](xref:razor-pages/index#razor-pages) | <span data-ttu-id="b2919-258">Указывает, что компонент должен обрабатывать запросы напрямую.</span><span class="sxs-lookup"><span data-stu-id="b2919-258">Specifies that the component should handle requests directly.</span></span> <span data-ttu-id="b2919-259">`@page` Директивы можно указать параметром маршрута и необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="b2919-259">The `@page` directive can be specified with a route and optional parameters.</span></span> <span data-ttu-id="b2919-260">В отличие от Razor Pages `@page` директива не обязательно должен быть первой директивой в верхней части файла.</span><span class="sxs-lookup"><span data-stu-id="b2919-260">Unlike Razor Pages, the `@page` directive doesn't need to be the first directive at the top of the file.</span></span> <span data-ttu-id="b2919-261">Дополнительные сведения см. в разделе [Маршрутизация](xref:razor-components/routing).</span><span class="sxs-lookup"><span data-stu-id="b2919-261">For more information, see [Routing](xref:razor-components/routing).</span></span> |
| [<span data-ttu-id="b2919-262">\@С помощью</span><span class="sxs-lookup"><span data-stu-id="b2919-262">\@using</span></span>](xref:mvc/views/razor#using) | <span data-ttu-id="b2919-263">Добавляет C# `using` директивы в класс созданный компонент.</span><span class="sxs-lookup"><span data-stu-id="b2919-263">Adds the C# `using` directive to the generated component class.</span></span> |
| [<span data-ttu-id="b2919-264">\@addTagHelper</span><span class="sxs-lookup"><span data-stu-id="b2919-264">\@addTagHelper</span></span>](xref:mvc/views/razor#tag-helpers) | <span data-ttu-id="b2919-265">Использовать `@addTagHelper` для использования компонента в другой сборке, чем сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="b2919-265">Use `@addTagHelper` to use a component in a different assembly than the app's assembly.</span></span> |

<span data-ttu-id="b2919-266">**Условные атрибуты**</span><span class="sxs-lookup"><span data-stu-id="b2919-266">**Conditional attributes**</span></span>

<span data-ttu-id="b2919-267">Атрибуты отображаются по условию на основе значения .NET.</span><span class="sxs-lookup"><span data-stu-id="b2919-267">Attributes are conditionally rendered based on the .NET value.</span></span> <span data-ttu-id="b2919-268">Если значение равно `false` или `null`, атрибут не отображается.</span><span class="sxs-lookup"><span data-stu-id="b2919-268">If the value is `false` or `null`,  the attribute isn't rendered.</span></span> <span data-ttu-id="b2919-269">Если значение равно `true`, атрибут визуализируется в свернутом состоянии.</span><span class="sxs-lookup"><span data-stu-id="b2919-269">If the value is `true`, the attribute is rendered minimized.</span></span>

<span data-ttu-id="b2919-270">В следующем примере `IsCompleted` определяет `checked` визуализируется в разметке элемента управления:</span><span class="sxs-lookup"><span data-stu-id="b2919-270">In the following example, `IsCompleted` determines if `checked` is rendered in the control's markup:</span></span>

```cshtml
<input type="checkbox" checked="@IsCompleted" />

@functions {
    [Parameter]
    private bool IsCompleted { get; set; }
}
```

<span data-ttu-id="b2919-271">Если `IsCompleted` является `true`, флажок отображается как:</span><span class="sxs-lookup"><span data-stu-id="b2919-271">If `IsCompleted` is `true`, the check box is rendered as:</span></span>

```html
<input type="checkbox" checked />
```

<span data-ttu-id="b2919-272">Если `IsCompleted` является `false`, флажок отображается как:</span><span class="sxs-lookup"><span data-stu-id="b2919-272">If `IsCompleted` is `false`, the check box is rendered as:</span></span>

```html
<input type="checkbox" />
```

<span data-ttu-id="b2919-273">**Дополнительные сведения о Razor**</span><span class="sxs-lookup"><span data-stu-id="b2919-273">**Additional information on Razor**</span></span>

<span data-ttu-id="b2919-274">Дополнительные сведения о Razor, см. в разделе [Справочник по синтаксису Razor](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="b2919-274">For more information on Razor, see the [Razor syntax reference](xref:mvc/views/razor).</span></span>

## <a name="raw-html"></a><span data-ttu-id="b2919-275">Необработанный HTML</span><span class="sxs-lookup"><span data-stu-id="b2919-275">Raw HTML</span></span>

<span data-ttu-id="b2919-276">Строки обычно отображаются с использованием DOM текстовые узлы, что означает, что любой разметку, с которой они могут содержать игнорируется и обрабатывается как обычный текст.</span><span class="sxs-lookup"><span data-stu-id="b2919-276">Strings are normally rendered using DOM text nodes, which means that any markup they may contain is ignored and treated as literal text.</span></span> <span data-ttu-id="b2919-277">Чтобы отобразить необработанный HTML, поместить содержимое HTML в `MarkupString` значение.</span><span class="sxs-lookup"><span data-stu-id="b2919-277">To render raw HTML, wrap the HTML content in a `MarkupString` value.</span></span> <span data-ttu-id="b2919-278">Значение анализируется как HTML или SVG и вставить в модель DOM.</span><span class="sxs-lookup"><span data-stu-id="b2919-278">The value is parsed as HTML or SVG and inserted into the DOM.</span></span>

> [!WARNING]
> <span data-ttu-id="b2919-279">Визуализации необработанный HTML, созданный из любой ненадежных источником является **угрозу безопасности** следует избегать использования!</span><span class="sxs-lookup"><span data-stu-id="b2919-279">Rendering raw HTML constructed from any untrusted source is a **security risk** and should be avoided!</span></span>

<span data-ttu-id="b2919-280">В следующем примере показано использование `MarkupString` тип добавляемого блока статического содержимого HTML выводимые данные компонента:</span><span class="sxs-lookup"><span data-stu-id="b2919-280">The following example shows using the `MarkupString` type to add a block of static HTML content to the rendered output of a component:</span></span>

```html
@((MarkupString)myMarkup)

@functions {
    string myMarkup = "<p class='markup'>This is a <em>markup string</em>.</p>";
}
```

## <a name="templated-components"></a><span data-ttu-id="b2919-281">Компоненты на основе шаблона</span><span class="sxs-lookup"><span data-stu-id="b2919-281">Templated components</span></span>

<span data-ttu-id="b2919-282">Шаблонный компонентами являются компоненты, которые принимают один или несколько шаблонов пользовательского интерфейса в качестве параметров, которые затем могут использоваться как часть логики отображения компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-282">Templated components are components that accept one or more UI templates as parameters, which can then be used as part of the component's rendering logic.</span></span> <span data-ttu-id="b2919-283">Шаблонный компоненты позволяют создавать компоненты более высокого уровня, более многократно используемых, чем обычных компонентов.</span><span class="sxs-lookup"><span data-stu-id="b2919-283">Templated components allow you to author higher-level components that are more reusable than regular components.</span></span> <span data-ttu-id="b2919-284">Включают несколько примеров:</span><span class="sxs-lookup"><span data-stu-id="b2919-284">A couple of examples include:</span></span>

* <span data-ttu-id="b2919-285">Таблица компонент, который позволяет пользователю указать шаблоны для заголовка, строки и нижнего колонтитула таблицы.</span><span class="sxs-lookup"><span data-stu-id="b2919-285">A table component that allows a user to specify templates for the table's header, rows, and footer.</span></span>
* <span data-ttu-id="b2919-286">Компонент списка, который позволяет пользователю указать шаблон для подготовки к просмотру элементов в списке.</span><span class="sxs-lookup"><span data-stu-id="b2919-286">A list component that allows a user to specify a template for rendering items in a list.</span></span>

### <a name="template-parameters"></a><span data-ttu-id="b2919-287">Параметры шаблона</span><span class="sxs-lookup"><span data-stu-id="b2919-287">Template parameters</span></span>

<span data-ttu-id="b2919-288">Компонент шаблона определяется путем указания одного или нескольких параметров компонента типа `RenderFragment` или `RenderFragment<T>`.</span><span class="sxs-lookup"><span data-stu-id="b2919-288">A templated component is defined by specifying one or more component parameters of type `RenderFragment` or `RenderFragment<T>`.</span></span> <span data-ttu-id="b2919-289">Отрисовки фрагмент представляет часть пользовательского интерфейса, который отображается в компоненте.</span><span class="sxs-lookup"><span data-stu-id="b2919-289">A render fragment represents a segment of UI that is rendered by the component.</span></span> <span data-ttu-id="b2919-290">Фрагмент визуализации при необходимости принимает параметр, который можно указать при вызове фрагмента отрисовки.</span><span class="sxs-lookup"><span data-stu-id="b2919-290">A render fragment optionally takes a parameter that can be specified when the render fragment is invoked.</span></span>

<span data-ttu-id="b2919-291">*Components/TableTemplate.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-291">*Components/TableTemplate.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TableTemplate.cshtml)]

<span data-ttu-id="b2919-292">При использовании компонента, шаблон, параметры шаблона можно задать с помощью дочерних элементов, совпадающих с именами параметров (`TableHeader` и `RowTemplate` в следующем примере):</span><span class="sxs-lookup"><span data-stu-id="b2919-292">When using a templated component, the template parameters can be specified using child elements that match the names of the parameters (`TableHeader` and `RowTemplate` in the following example):</span></span>

```cshtml
<TableTemplate Items="@pets">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate>
        <td>@context.PetId</td>
        <td>@context.Name</td>
    </RowTemplate>
</TableTemplate>
```

### <a name="template-context-parameters"></a><span data-ttu-id="b2919-293">Контекстные параметры шаблона</span><span class="sxs-lookup"><span data-stu-id="b2919-293">Template context parameters</span></span>

<span data-ttu-id="b2919-294">Компонент аргументы типа `RenderFragment<T>` передаваемое в качестве элементов имеют неявный параметр с именем `context` (например из в предыдущем образце кода `@context.PetId`), но можно изменить имя параметра с помощью `Context` атрибут дочерних элементов элемент.</span><span class="sxs-lookup"><span data-stu-id="b2919-294">Component arguments of type `RenderFragment<T>` passed as elements have an implicit parameter named `context` (for example from the preceding code sample, `@context.PetId`), but you can change the parameter name using the `Context` attribute on the child element.</span></span> <span data-ttu-id="b2919-295">В следующем примере `RowTemplate` элемента `Context` атрибут задает `pet` параметр:</span><span class="sxs-lookup"><span data-stu-id="b2919-295">In the following example, the `RowTemplate` element's `Context` attribute specifies the `pet` parameter:</span></span>

```cshtml
<TableTemplate Items="@pets">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate Context="pet">
        <td>@pet.PetId</td>
        <td>@pet.Name</td>
    </RowTemplate>
</TableTemplate>
```

<span data-ttu-id="b2919-296">Кроме того, можно указать `Context` атрибута элемента компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-296">Alternatively, you can specify the `Context` attribute on the component element.</span></span> <span data-ttu-id="b2919-297">Указанный `Context` атрибут применяется для всех остальных параметров указанного шаблона.</span><span class="sxs-lookup"><span data-stu-id="b2919-297">The specified `Context` attribute applies to all specified template parameters.</span></span> <span data-ttu-id="b2919-298">Это может быть полезно, когда требуется указать имя параметра содержимого для неявного дочерний тип содержимого (без переносов любой дочерний элемент).</span><span class="sxs-lookup"><span data-stu-id="b2919-298">This can be useful when you want to specify the content parameter name for implicit child content (without any wrapping child element).</span></span> <span data-ttu-id="b2919-299">В следующем примере `Context` атрибут находится в `TableTemplate` элемент и применяется для всех параметров шаблона:</span><span class="sxs-lookup"><span data-stu-id="b2919-299">In the following example, the `Context` attribute appears on the `TableTemplate` element and applies to all template parameters:</span></span>

```cshtml
<TableTemplate Items="@pets" Context="pet">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate>
        <td>@pet.PetId</td>
        <td>@pet.Name</td>
    </RowTemplate>
</TableTemplate>
```

### <a name="generic-typed-components"></a><span data-ttu-id="b2919-300">Компоненты типизированными универсальными</span><span class="sxs-lookup"><span data-stu-id="b2919-300">Generic-typed components</span></span>

<span data-ttu-id="b2919-301">Шаблонный компоненты часто универсально типизированы.</span><span class="sxs-lookup"><span data-stu-id="b2919-301">Templated components are often generically typed.</span></span> <span data-ttu-id="b2919-302">Например, можно использовать общий компонент шаблон представления списка для подготовки к просмотру `IEnumerable<T>` значения.</span><span class="sxs-lookup"><span data-stu-id="b2919-302">For example, a generic List View Template component can be used to render `IEnumerable<T>` values.</span></span> <span data-ttu-id="b2919-303">Чтобы определить общий компонент, используйте `@typeparam` директиву, чтобы задать параметры типа.</span><span class="sxs-lookup"><span data-stu-id="b2919-303">To define a generic component, use the `@typeparam` directive to specify type parameters.</span></span>

<span data-ttu-id="b2919-304">*Components/ListViewTemplate.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-304">*Components/ListViewTemplate.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/ListViewTemplate.cshtml?highlight=1)]

<span data-ttu-id="b2919-305">При использовании компонентов типизированными универсальными, параметр типа выводится, если это возможно:</span><span class="sxs-lookup"><span data-stu-id="b2919-305">When using generic-typed components, the type parameter is inferred if possible:</span></span>

```cshtml
<ListViewTemplate Items="@pets">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

<span data-ttu-id="b2919-306">В противном случае параметр типа необходимо явно указать с помощью атрибута, который совпадает с именем параметра типа.</span><span class="sxs-lookup"><span data-stu-id="b2919-306">Otherwise, the type parameter must be explicitly specified using an attribute that matches the name of the type parameter.</span></span> <span data-ttu-id="b2919-307">В следующем примере `TItem="Pet"` указывает тип:</span><span class="sxs-lookup"><span data-stu-id="b2919-307">In the following example, `TItem="Pet"` specifies the type:</span></span>

```cshtml
<ListViewTemplate Items="@pets" TItem="Pet">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

## <a name="cascading-values-and-parameters"></a><span data-ttu-id="b2919-308">Каскадные значения и параметры</span><span class="sxs-lookup"><span data-stu-id="b2919-308">Cascading values and parameters</span></span>

<span data-ttu-id="b2919-309">В некоторых сценариях, нет смысла для вывода данных из компонента предка в дочерних компонентов с помощью [параметры компонента](#component-parameters), особенно в том случае, если существуют несколько уровней компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-309">In some scenarios, it's inconvenient to flow data from an ancestor component to a descendent component using [component parameters](#component-parameters), especially when there are several component layers.</span></span> <span data-ttu-id="b2919-310">Каскадные значения и параметры решить эту проблему, предоставляя удобный способ для предка компонента для предоставления значения для всех его дочерних компонентов.</span><span class="sxs-lookup"><span data-stu-id="b2919-310">Cascading values and parameters solve this problem by providing a convenient way for an ancestor component to provide a value to all of its descendent components.</span></span> <span data-ttu-id="b2919-311">Каскадные значения и параметры также предоставляют способ компоненты для координации.</span><span class="sxs-lookup"><span data-stu-id="b2919-311">Cascading values and parameters also provide an approach for components to coordinate.</span></span>

### <a name="theme-example"></a><span data-ttu-id="b2919-312">Пример темы</span><span class="sxs-lookup"><span data-stu-id="b2919-312">Theme example</span></span>

<span data-ttu-id="b2919-313">В следующем *темы* пример из примера приложения, `ThemeInfo` класс задает информацию темы к нижележащим сайтам иерархии компонент таким образом, все кнопки в определенной части приложения тот же стиль.</span><span class="sxs-lookup"><span data-stu-id="b2919-313">In the following *Theme* example from the sample app, the `ThemeInfo` class specifies the theme information to flow down the component hierarchy so that all of the buttons within a given part of the app share the same style.</span></span>

<span data-ttu-id="b2919-314">*UIThemeClasses/ThemeInfo.cs*:</span><span class="sxs-lookup"><span data-stu-id="b2919-314">*UIThemeClasses/ThemeInfo.cs*:</span></span>

```csharp
public class ThemeInfo
{
    public string ButtonClass { get; set; }
}
```

<span data-ttu-id="b2919-315">Компонент предка можно указать каскадные значение с помощью каскадных значение компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-315">An ancestor component can provide a cascading value using the Cascading Value component.</span></span> <span data-ttu-id="b2919-316">Компонент каскадных значения ветви иерархии компонент заключает в оболочку и предоставляет одно значение для всех компонентов в этом поддереве.</span><span class="sxs-lookup"><span data-stu-id="b2919-316">The Cascading Value component wraps a subtree of the component hierarchy and supplies a single value to all components within that subtree.</span></span>

<span data-ttu-id="b2919-317">Например, в примере приложения задает сведения о теме (`ThemeInfo`) в одном из макетов приложений как каскадного параметра для всех компонентов, составляющих тело макета `@Body` свойство.</span><span class="sxs-lookup"><span data-stu-id="b2919-317">For example, the sample app specifies theme information (`ThemeInfo`) in one of the app's layouts as a cascading parameter for all components that make up the layout body of the `@Body` property.</span></span> <span data-ttu-id="b2919-318">`ButtonClass` присваивается значение `btn-success` в компоненте макета.</span><span class="sxs-lookup"><span data-stu-id="b2919-318">`ButtonClass` is assigned a value of `btn-success` in the layout component.</span></span> <span data-ttu-id="b2919-319">Любой потомок компонент может использовать это свойство через `ThemeInfo` каскадных объекта.</span><span class="sxs-lookup"><span data-stu-id="b2919-319">Any descendent component can consume this property through the `ThemeInfo` cascading object.</span></span>

<span data-ttu-id="b2919-320">*Shared/CascadingValuesParametersLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-320">*Shared/CascadingValuesParametersLayout.cshtml*:</span></span>

```cshtml
@inherits BlazorLayoutComponent
@using BlazorSample.UIThemeClasses

<div class="container-fluid">
    <div class="row">
        <div class="col-sm-3">
            <NavMenu />
        </div>
        <div class="col-sm-9">
            <CascadingValue Value="@theme">
                <div class="content px-4">
                    @Body
                </div>
            </CascadingValue>
        </div>
    </div>
</div>

@functions {
    ThemeInfo theme = new ThemeInfo { ButtonClass = "btn-success" };
}
```

<span data-ttu-id="b2919-321">Чтобы использовать каскадных значений, компоненты объявить каскадных параметров с помощью `[CascadingParameter]` атрибута или в зависимости от строковое значение имени:</span><span class="sxs-lookup"><span data-stu-id="b2919-321">To make use of cascading values, components declare cascading parameters using the `[CascadingParameter]` attribute or based on a string name value:</span></span>

```cshtml
<CascadingValue Value=@PermInfo Name="UserPermissions">...</CascadingValue>

[CascadingParameter(Name = "UserPermissions")] PermInfo Permissions { get; set; }
```

<span data-ttu-id="b2919-322">Привязки со строковым значением имя относится, если у вас несколько каскадных значений одного типа и необходимо разделить их в данном поддереве.</span><span class="sxs-lookup"><span data-stu-id="b2919-322">Binding with a string name value is relevant if you have multiple cascading values of the same type and need to differentiate them within the same subtree.</span></span>

<span data-ttu-id="b2919-323">Каскадные значения привязаны к каскадные параметры по типу.</span><span class="sxs-lookup"><span data-stu-id="b2919-323">Cascading values are bound to cascading parameters by type.</span></span>

<span data-ttu-id="b2919-324">В примере приложения каскадные параметры темы значения компонента привязывается к `ThemeInfo` каскадных значение для каскадного параметра.</span><span class="sxs-lookup"><span data-stu-id="b2919-324">In the sample app, the Cascading Values Parameters Theme component binds to the `ThemeInfo` cascading value to a cascading parameter.</span></span> <span data-ttu-id="b2919-325">Параметр используется для задания класс CSS для одной из кнопок, отображаемому в компоненте.</span><span class="sxs-lookup"><span data-stu-id="b2919-325">The parameter is used to set the CSS class for one of the buttons displayed by the component.</span></span>

<span data-ttu-id="b2919-326">*Pages/CascadingValuesParametersTheme.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-326">*Pages/CascadingValuesParametersTheme.cshtml*:</span></span>

```cshtml
@page "/cascadingvaluesparameterstheme"
@layout CascadingValuesParametersLayout
@using BlazorSample.UIThemeClasses

<h1>Cascading Values & Parameters</h1>

<p>Current count: @currentCount</p>

<p>
    <button class="btn" onclick="@IncrementCount">
        Increment Counter (Unthemed)
    </button>
</p>

<p>
    <button class="btn @ThemeInfo.ButtonClass" onclick="@IncrementCount">
        Increment Counter (Themed)
    </button>
</p>

@functions {
    int currentCount = 0;

    [CascadingParameter] protected ThemeInfo ThemeInfo { get; set; }

    void IncrementCount()
    {
        currentCount++;
    }
}
```

### <a name="tabset-example"></a><span data-ttu-id="b2919-327">Пример TabSet</span><span class="sxs-lookup"><span data-stu-id="b2919-327">TabSet example</span></span>

<span data-ttu-id="b2919-328">Каскадные параметры также включить компоненты для совместной работы по всей иерархии компонента.</span><span class="sxs-lookup"><span data-stu-id="b2919-328">Cascading parameters also enable components to collaborate across the component hierarchy.</span></span> <span data-ttu-id="b2919-329">Например, рассмотрим следующие *TabSet* пример, в примере приложения.</span><span class="sxs-lookup"><span data-stu-id="b2919-329">For example, consider the following *TabSet* example in the sample app.</span></span>

<span data-ttu-id="b2919-330">В примере приложения есть `ITab` интерфейса, реализуйте вкладки:</span><span class="sxs-lookup"><span data-stu-id="b2919-330">The sample app has an `ITab` interface that tabs implement:</span></span>

[!code-cs[](common/samples/3.x/BlazorSample/UIInterfaces/ITab.cs)]

<span data-ttu-id="b2919-331">Каскадные параметры TabSet значения компонент использует компонент набор вкладок, который содержит несколько компонентов вкладки:</span><span class="sxs-lookup"><span data-stu-id="b2919-331">The Cascading Values Parameters TabSet component uses the Tab Set component, which contains several Tab components:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/CascadingValuesParametersTabSet.cshtml?name=snippet_TabSet)]

<span data-ttu-id="b2919-332">Вкладка дочерние компоненты не явно передаются как параметры в набор вкладок.</span><span class="sxs-lookup"><span data-stu-id="b2919-332">The child Tab components aren't explicitly passed as parameters to the Tab Set.</span></span> <span data-ttu-id="b2919-333">Вместо этого дочерние вкладку компоненты являются частью дочернего содержимого набор вкладок.</span><span class="sxs-lookup"><span data-stu-id="b2919-333">Instead, the child Tab components are part of the child content of the Tab Set.</span></span> <span data-ttu-id="b2919-334">Тем не менее набор вкладок по-прежнему необходимо знать о каждом компоненте вкладку, чтобы он мог преобразовать заголовки и активной вкладки. Чтобы включить эту координацию без необходимости написания дополнительного кода, компонент набор вкладок *можно указать сам как значение каскадных* , затем выбирается дочерних компонентов вкладки.</span><span class="sxs-lookup"><span data-stu-id="b2919-334">However, the Tab Set still needs to know about each Tab component so that it can render the headers and the active tab. To enable this coordination without requiring additional code, the Tab Set component *can provide itself as a cascading value* that is then picked up by the descendent Tab components.</span></span>

<span data-ttu-id="b2919-335">*Components/TabSet.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-335">*Components/TabSet.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TabSet.cshtml)]

<span data-ttu-id="b2919-336">Дочерние записи компонентов вкладку содержащего набор вкладок как каскадного параметра, поэтому компоненты вкладку добавлять себя в набор вкладок и координат на вкладках активна.</span><span class="sxs-lookup"><span data-stu-id="b2919-336">The descendent Tab components capture the containing Tab Set as a cascading parameter, so the Tab components add themselves to the Tab Set and coordinate on which tab is active.</span></span>

<span data-ttu-id="b2919-337">*Components/Tab.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-337">*Components/Tab.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/Tab.cshtml)]

## <a name="razor-templates"></a><span data-ttu-id="b2919-338">Шаблоны Razor</span><span class="sxs-lookup"><span data-stu-id="b2919-338">Razor templates</span></span>

<span data-ttu-id="b2919-339">Визуализации фрагментов можно определить с помощью синтаксиса Razor шаблона.</span><span class="sxs-lookup"><span data-stu-id="b2919-339">Render fragments can be defined using Razor template syntax.</span></span> <span data-ttu-id="b2919-340">Шаблоны Razor — это способ определения пользовательского интерфейса фрагмента и предполагают следующий формат:</span><span class="sxs-lookup"><span data-stu-id="b2919-340">Razor templates are a way to define a UI snippet and assume the following format:</span></span>

```cshtml
@<tag>...</tag>
```

<span data-ttu-id="b2919-341">В следующем примере показан способ указания `RenderFragment` и `RenderFragment<T>` значения.</span><span class="sxs-lookup"><span data-stu-id="b2919-341">The following example illustrates how to specify `RenderFragment` and `RenderFragment<T>` values.</span></span>

<span data-ttu-id="b2919-342">*RazorTemplates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b2919-342">*RazorTemplates.cshtml*:</span></span>

```cshtml
@{
    RenderFragment template = @<p>The time is @DateTime.Now.</p>;
    RenderFragment<Pet> petTemplate = (pet) => @<p>Your pet's name is @pet.Name.</p>;
}
```

<span data-ttu-id="b2919-343">Отображать фрагментов, определенных с помощью Razor, шаблоны можно передаются как аргументы шаблона компонентов или отображена непосредственно.</span><span class="sxs-lookup"><span data-stu-id="b2919-343">Render fragments defined using Razor templates can be passed as arguments to templated components or rendered directly.</span></span> <span data-ttu-id="b2919-344">Например предыдущий шаблоны непосредственно выводятся в виде следующая разметка Razor:</span><span class="sxs-lookup"><span data-stu-id="b2919-344">For example, the previous templates are directly rendered with the following Razor markup:</span></span>

```cshtml
@template

@petTemplate(new Pet { Name = "Rex" })
```

<span data-ttu-id="b2919-345">Отображенные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b2919-345">Rendered output:</span></span>

```
The time is 10/04/2018 01:26:52.

Your pet's name is Rex.
```
