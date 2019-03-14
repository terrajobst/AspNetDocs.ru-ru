---
title: Взаимодействие компонентов JavaScript в Razor
author: guardrex
description: Узнайте, как вызывать функции JavaScript, .NET, .NET методы из JavaScript в приложениях Blazor и компоненты Razor.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/javascript-interop
ms.openlocfilehash: 9f822fee8990b03ff15ffa9857a2ddd95328a6ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050371"
---
# <a name="razor-components-javascript-interop"></a><span data-ttu-id="d75b2-103">Взаимодействие компонентов JavaScript в Razor</span><span class="sxs-lookup"><span data-stu-id="d75b2-103">Razor Components JavaScript interop</span></span>

<span data-ttu-id="d75b2-104">По [Нельсон Calvarro Хавьер](https://github.com/javiercn), [Дэниэл рот](https://github.com/danroth27), и [Люк Лэтем](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="d75b2-104">By [Javier Calvarro Nelson](https://github.com/javiercn), [Daniel Roth](https://github.com/danroth27), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="d75b2-105">В приложение Razor компоненты могут вызывать функции JavaScript, .NET, .NET методы из кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-105">A Razor Components app can invoke JavaScript functions from .NET and .NET methods from JavaScript code.</span></span>

## <a name="invoke-javascript-functions-from-net-methods"></a><span data-ttu-id="d75b2-106">Вызова функций JavaScript из методов .NET</span><span class="sxs-lookup"><span data-stu-id="d75b2-106">Invoke JavaScript functions from .NET methods</span></span>

<span data-ttu-id="d75b2-107">Бывают случаи, когда код .NET не требуется для вызова функции JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-107">There are times when .NET code is required to call a JavaScript function.</span></span> <span data-ttu-id="d75b2-108">Например вызов JavaScript может предоставлять возможности браузера или функции из библиотеки JavaScript в приложение.</span><span class="sxs-lookup"><span data-stu-id="d75b2-108">For example, a JavaScript call can expose browser capabilities or functionality from a JavaScript library to the app.</span></span>

<span data-ttu-id="d75b2-109">Чтобы вызывать JavaScript с помощью .NET, используйте `IJSRuntime` абстракции.</span><span class="sxs-lookup"><span data-stu-id="d75b2-109">To call into JavaScript from .NET, use the `IJSRuntime` abstraction.</span></span> <span data-ttu-id="d75b2-110">`InvokeAsync<T>` Метод `IJSRuntime` принимает идентификатор для функции JavaScript, который вы хотите вызвать, наряду с любое количество аргументов, сериализуемые в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="d75b2-110">The `InvokeAsync<T>` method on `IJSRuntime` takes an identifier for the JavaScript function you wish to invoke along with any number of JSON-serializable arguments.</span></span> <span data-ttu-id="d75b2-111">Идентификатор функции задается относительно глобальной области (`window`).</span><span class="sxs-lookup"><span data-stu-id="d75b2-111">The function identifier is relative to the global scope (`window`).</span></span> <span data-ttu-id="d75b2-112">Если вы хотите вызвать `window.someScope.someFunction`, идентификатор является `someScope.someFunction`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-112">If you wish to call `window.someScope.someFunction`, the identifier is `someScope.someFunction`.</span></span> <span data-ttu-id="d75b2-113">Нет необходимости зарегистрировать функцию перед его вызовом.</span><span class="sxs-lookup"><span data-stu-id="d75b2-113">There's no need to register the function before it's called.</span></span> <span data-ttu-id="d75b2-114">Тип возвращаемого значения `T` также должны быть JSON сериализуемыми.</span><span class="sxs-lookup"><span data-stu-id="d75b2-114">The return type `T` must also be JSON serializable.</span></span>

<span data-ttu-id="d75b2-115">Для приложений ASP.NET Core Razor компоненты на стороне сервера:</span><span class="sxs-lookup"><span data-stu-id="d75b2-115">For server-side ASP.NET Core Razor Components apps:</span></span>

* <span data-ttu-id="d75b2-116">Нескольких пользовательских запросов обрабатываются приложением на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d75b2-116">Multiple user requests are processed by the server-side app.</span></span> <span data-ttu-id="d75b2-117">Не вызывайте `JSRuntime.Current` в компоненте для вызова функций JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-117">Don't call `JSRuntime.Current` in a component to invoke JavaScript functions.</span></span>
* <span data-ttu-id="d75b2-118">Внедрить `IJSRuntime` абстракции и использование внедренного объекта взаимодействия вызовов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-118">Inject the `IJSRuntime` abstraction and use the injected object to issue JavaScript interop calls.</span></span>

<span data-ttu-id="d75b2-119">Следующий пример построен на основе [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), экспериментальный декодера, на основе JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-119">The following example is based on [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), an experimental JavaScript-based decoder.</span></span> <span data-ttu-id="d75b2-120">В примере для вызова функции JavaScript из C# метод.</span><span class="sxs-lookup"><span data-stu-id="d75b2-120">The example demonstrates how to invoke a JavaScript function from a C# method.</span></span> <span data-ttu-id="d75b2-121">Функция JavaScript, которая принимает массив байтов из C# метод, декодирует массива и возвращает текст в компонент для отображения.</span><span class="sxs-lookup"><span data-stu-id="d75b2-121">The JavaScript function accepts a byte array from a C# method, decodes the array, and returns the text to the component for display.</span></span>

<span data-ttu-id="d75b2-122">Внутри `<head>` элемент *wwwroot/index.html*, предоставляют функции, которая использует `TextDecoder` для декодирования переданный массив:</span><span class="sxs-lookup"><span data-stu-id="d75b2-122">Inside the `<head>` element of *wwwroot/index.html*, provide a function that uses `TextDecoder` to decode a passed array:</span></span>

```html
<script>
  window.ConvertArray = (win1251Array) => {
    var win1251decoder = new TextDecoder('windows-1251');
    var bytes = new Uint8Array(win1251Array);
    var decodedArray = win1251decoder.decode(bytes);
    console.log(decodedArray);
    return decodedArray;
  };
</script>
```

<span data-ttu-id="d75b2-123">Код JavaScript, например код, показанный в предыдущем примере, также может быть загружено с помощью файла JavaScript со ссылкой на файл скрипта в *wwwroot/index.html* файла.</span><span class="sxs-lookup"><span data-stu-id="d75b2-123">JavaScript code, such as the code shown in the preceding example, can also be loaded by a JavaScript file with a reference to the script file in the *wwwroot/index.html* file.</span></span>

<span data-ttu-id="d75b2-124">Следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="d75b2-124">The following component:</span></span>

* <span data-ttu-id="d75b2-125">Вызывает `ConvertArray` функцию JavaScript с помощью `JsRuntime` при кнопки компонент (**преобразовать массив**) выбран.</span><span class="sxs-lookup"><span data-stu-id="d75b2-125">Invokes the `ConvertArray` JavaScript function using `JsRuntime` when a component button (**Convert Array**) is selected.</span></span>
* <span data-ttu-id="d75b2-126">После вызова функции JavaScript, переданный массив преобразуется в строку.</span><span class="sxs-lookup"><span data-stu-id="d75b2-126">After the JavaScript function is called, the passed array is converted into a string.</span></span> <span data-ttu-id="d75b2-127">Строка возвращается к компоненту для отображения.</span><span class="sxs-lookup"><span data-stu-id="d75b2-127">The string is returned to the component for display.</span></span>

```cshtml
@page "/"
@using Microsoft.JSInterop;
@inject IJSRuntime JsRuntime;

<h1>Call JavaScript Function Example</h1>

<button type="button" class="btn btn-primary" onclick="@ConvertArray">
    Convert Array
</button>

<p class="mt-2" style="font-size:1.6em">
    <span class="badge badge-success">
        @ConvertedText
    </span>
</p>

@functions {
    // Quote (c)2005 Universal Pictures: Serenity
    // https://www.uphe.com/movies/serenity
    // David Krumholtz on IMDB: https://www.imdb.com/name/nm0472710/

    private MarkupString ConvertedText =
        new MarkupString("Select the <b>Convert Array</b> button.");

    private uint[] QuoteArray = new uint[]
        {
            60, 101, 109, 62, 67, 97, 110, 39, 116, 32, 115, 116, 111, 112, 32,
            116, 104, 101, 32, 115, 105, 103, 110, 97, 108, 44, 32, 77, 97,
            108, 46, 60, 47, 101, 109, 62, 32, 45, 32, 77, 114, 46, 32, 85, 110,
            105, 118, 101, 114, 115, 101, 10, 10,
        };

    async void ConvertArray()
    {
        var text =
            await JsRuntime.InvokeAsync<string>("ConvertArray", QuoteArray);

        ConvertedText = new MarkupString(text);

        StateHasChanged();
    }
}
```

<span data-ttu-id="d75b2-128">Для клиентских приложений Blazor `IJSRuntime` абстракции, доступен из `JSRuntime.Current`, которая относится к запросу текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d75b2-128">For client-side Blazor apps, the `IJSRuntime` abstraction is accessible from `JSRuntime.Current`, which refers to the current user's request.</span></span> <span data-ttu-id="d75b2-129">Поскольку имеется только один пользователь Blazor приложения на стороне клиента, с помощью `JSRuntime.Current` для вызова JavaScript функция работает как обычно.</span><span class="sxs-lookup"><span data-stu-id="d75b2-129">Because there's only a single user of a client-side Blazor app, using `JSRuntime.Current` to invoke a JavaScript function works normally.</span></span> <span data-ttu-id="d75b2-130">Использовать только `JSRuntime.Current` в приложениях Blazor на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="d75b2-130">Only use `JSRuntime.Current` in client-side Blazor apps.</span></span>

<span data-ttu-id="d75b2-131">В примере клиентского приложения, используемый в этом разделе доступны две функции JavaScript для клиентского приложения, взаимодействия с DOM для ввода данных пользователем и отображения приветственное сообщение:</span><span class="sxs-lookup"><span data-stu-id="d75b2-131">In the client-side sample app that accompanies this topic, two JavaScript functions are available to the client-side app that interact with the DOM to receive user input and display a welcome message:</span></span>

* <span data-ttu-id="d75b2-132">`showPrompt` &ndash; Выводит приглашение на ввод пользователя (имя пользователя) и возвращает имя вызывающей стороне.</span><span class="sxs-lookup"><span data-stu-id="d75b2-132">`showPrompt` &ndash; Produces a prompt to accept user input (the user's name) and returns the name to the caller.</span></span>
* <span data-ttu-id="d75b2-133">`displayWelcome` &ndash; Назначает приветственное сообщение от вызывающего объекта DOM с `id` из `welcome`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-133">`displayWelcome` &ndash; Assigns a welcome message from the caller to a DOM object with an `id` of `welcome`.</span></span>

<span data-ttu-id="d75b2-134">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-134">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

<span data-ttu-id="d75b2-135">Место `<script>` тег, который ссылается на файл JavaScript в *wwwroot/index.html* файла:</span><span class="sxs-lookup"><span data-stu-id="d75b2-135">Place the `<script>` tag that references the JavaScript file in the *wwwroot/index.html* file:</span></span>

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

<span data-ttu-id="d75b2-136">Не разместить тег скрипта в файле компонента, поскольку тег script не может обновляться динамически.</span><span class="sxs-lookup"><span data-stu-id="d75b2-136">Don't place a script tag in a component file because the script tag can't be updated dynamically.</span></span>

<span data-ttu-id="d75b2-137">Методы взаимодействие .NET с помощью функций JavaScript путем вызова `InvokeAsync<T>` метод `IJSRuntime`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-137">.NET methods interop with the JavaScript functions by calling `InvokeAsync<T>` method on `IJSRuntime`.</span></span>

<span data-ttu-id="d75b2-138">Пример приложения использует пару C# методы, `Prompt` и `Display`, чтобы вызвать `showPrompt` и `displayWelcome` функции JavaScript:</span><span class="sxs-lookup"><span data-stu-id="d75b2-138">The sample app uses a pair of C# methods, `Prompt` and `Display`, to invoke the `showPrompt` and `displayWelcome` JavaScript functions:</span></span>

<span data-ttu-id="d75b2-139">*JsInteropClasses/ExampleJsInterop.cs*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-139">*JsInteropClasses/ExampleJsInterop.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

<span data-ttu-id="d75b2-140">`IJSRuntime` Абстракции является асинхронным, разрешающие сценарии на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d75b2-140">The `IJSRuntime` abstraction is asynchronous to allow for server-side scenarios.</span></span> <span data-ttu-id="d75b2-141">Если приложение выполняется на стороне клиента и нужно вызвать функцию JavaScript синхронно, получено нисходящим `IJSInProcessRuntime` и вызвать `Invoke<T>` вместо этого.</span><span class="sxs-lookup"><span data-stu-id="d75b2-141">If the app runs client-side and you want to invoke a JavaScript function synchronously, downcast to `IJSInProcessRuntime` and call `Invoke<T>` instead.</span></span> <span data-ttu-id="d75b2-142">Мы рекомендуем, что большинство используют взаимодействия библиотек JavaScript асинхронные интерфейсы API, чтобы обеспечить библиотеки доступны в все сценарии, на стороне клиента или на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d75b2-142">We recommend that most JavaScript interop libraries use the async APIs to ensure the libraries are available in all scenarios, client-side or server-side.</span></span>

<span data-ttu-id="d75b2-143">Пример приложения включает компонент для демонстрации взаимодействия JS.</span><span class="sxs-lookup"><span data-stu-id="d75b2-143">The sample app includes a component to demonstrate JS interop.</span></span> <span data-ttu-id="d75b2-144">Компонент:</span><span class="sxs-lookup"><span data-stu-id="d75b2-144">The component:</span></span>

* <span data-ttu-id="d75b2-145">Получает входные данные пользователя с помощью строки JS.</span><span class="sxs-lookup"><span data-stu-id="d75b2-145">Receives user input via a JS prompt.</span></span>
* <span data-ttu-id="d75b2-146">Возвращает текст к компоненту для обработки.</span><span class="sxs-lookup"><span data-stu-id="d75b2-146">Returns the text to the component for processing.</span></span>
* <span data-ttu-id="d75b2-147">Вызывает функцию второй JS, взаимодействующий с DOM для отображения приветственного сообщения.</span><span class="sxs-lookup"><span data-stu-id="d75b2-147">Calls a second JS function that interacts with the DOM to display a welcome message.</span></span>

<span data-ttu-id="d75b2-148">*Pages/JSInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-148">*Pages/JSInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. <span data-ttu-id="d75b2-149">При `TriggerJsPrompt` выполняется путем выбора компонента **триггера JavaScript Prompt** кнопки `ExampleJsInterop.Prompt` метод в C# вызова кода.</span><span class="sxs-lookup"><span data-stu-id="d75b2-149">When `TriggerJsPrompt` is executed by selecting the component's **Trigger JavaScript Prompt** button, the `ExampleJsInterop.Prompt` method in C# code is called.</span></span>
1. <span data-ttu-id="d75b2-150">`Prompt` JavaScript выполняется метод `showPrompt` функция, предоставленная в *wwwroot/exampleJsInterop.js* файла.</span><span class="sxs-lookup"><span data-stu-id="d75b2-150">The `Prompt` method executes the JavaScript `showPrompt` function provided in the *wwwroot/exampleJsInterop.js* file.</span></span>
1. <span data-ttu-id="d75b2-151">`showPrompt` Функция принимает вводимые пользователем данные (имя пользователя), являющееся HTML-кодирование и осуществляется возврат в `Prompt` метод и в конечном итоге обратно в компонент.</span><span class="sxs-lookup"><span data-stu-id="d75b2-151">The `showPrompt` function accepts user input (the user's name), which is HTML-encoded and returned to the `Prompt` method and ultimately back to the component.</span></span> <span data-ttu-id="d75b2-152">Компонент сохраняет имя пользователя в локальной переменной, `name`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-152">The component stores the user's name in a local variable, `name`.</span></span>
1. <span data-ttu-id="d75b2-153">Строки хранятся в `name` является частью приветственное сообщение, передаваемое секунды C# метод, `ExampleJsInterop.Display`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-153">The string stored in `name` is incorporated into a welcome message, which is passed to a second C# method, `ExampleJsInterop.Display`.</span></span>
1. <span data-ttu-id="d75b2-154">`Display` вызывает функцию JavaScript, `displayWelcome`, который отображает приветственное сообщение в тег заголовка.</span><span class="sxs-lookup"><span data-stu-id="d75b2-154">`Display` calls a JavaScript function, `displayWelcome`, which renders the welcome message into a heading tag.</span></span>

## <a name="capture-references-to-elements"></a><span data-ttu-id="d75b2-155">Захват ссылок на элементы</span><span class="sxs-lookup"><span data-stu-id="d75b2-155">Capture references to elements</span></span>

<span data-ttu-id="d75b2-156">Некоторые [взаимодействия JavaScript](xref:razor-components/javascript-interop) сценарии требуют ссылки на элементы HTML.</span><span class="sxs-lookup"><span data-stu-id="d75b2-156">Some [JavaScript interop](xref:razor-components/javascript-interop) scenarios require references to HTML elements.</span></span> <span data-ttu-id="d75b2-157">Например, библиотека пользовательского интерфейса может потребоваться ссылки на элемент для инициализации, или может потребоваться вызвать подобные API-интерфейсы на элементе, например `focus` или `play`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-157">For example, a UI library may require an element reference for initialization, or you might need to call command-like APIs on an element, such as `focus` or `play`.</span></span>

<span data-ttu-id="d75b2-158">Ссылки на элементы HTML в компоненте можно записать, добавив `ref` атрибут к элементу HTML, а затем определив поле типа `ElementRef` , имя которого совпадает со значением `ref` атрибута.</span><span class="sxs-lookup"><span data-stu-id="d75b2-158">You can capture references to HTML elements in a component by adding a `ref` attribute to the HTML element and then defining a field of type `ElementRef` whose name matches the value of the `ref` attribute.</span></span>

<span data-ttu-id="d75b2-159">В следующем примере показано, захват ссылку на элемент ввода имени пользователя:</span><span class="sxs-lookup"><span data-stu-id="d75b2-159">The following example shows capturing a reference to the username input element:</span></span>

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> <span data-ttu-id="d75b2-160">Сделать **не** использовать ссылки на элементы, записанный как способ заполнения модели DOM.</span><span class="sxs-lookup"><span data-stu-id="d75b2-160">Do **not** use captured element references as a way of populating the DOM.</span></span> <span data-ttu-id="d75b2-161">Это может помешать модели для декларативной подготовки отчетов.</span><span class="sxs-lookup"><span data-stu-id="d75b2-161">Doing so may interfere with the declarative rendering model.</span></span>

<span data-ttu-id="d75b2-162">Что касается кода .NET является, `ElementRef` – это прозрачный дескриптор.</span><span class="sxs-lookup"><span data-stu-id="d75b2-162">As far as .NET code is concerned, an `ElementRef` is an opaque handle.</span></span> <span data-ttu-id="d75b2-163">*Только* , что можно сделать с ней будет передавать его с помощью кода JavaScript через взаимодействие JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-163">The *only* thing you can do with it is pass it through to JavaScript code via JavaScript interop.</span></span> <span data-ttu-id="d75b2-164">При этом код JavaScript на стороне получает `HTMLElement` экземпляр, который его можно использовать с обычной интерфейсы API модели DOM.</span><span class="sxs-lookup"><span data-stu-id="d75b2-164">When you do so, the JavaScript-side code receives an `HTMLElement` instance, which it can use with normal DOM APIs.</span></span>

<span data-ttu-id="d75b2-165">Например следующий код определяет метод расширения .NET, который позволяет установить фокус на элементе:</span><span class="sxs-lookup"><span data-stu-id="d75b2-165">For example, the following code defines a .NET extension method that enables setting the focus on an element:</span></span>

<span data-ttu-id="d75b2-166">*MyLib.js*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-166">*mylib.js*:</span></span>

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

<span data-ttu-id="d75b2-167">*ElementRefExtensions.cs*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-167">*ElementRefExtensions.cs*:</span></span>

```csharp
using Microsoft.AspNetCore.Blazor;
using Microsoft.JSInterop;
using System.Threading.Tasks;

namespace MyLib
{
    public static class MyLibElementRefExtensions
    {
        public static Task Focus(this ElementRef elementRef)
        {
            return JSRuntime.Current.InvokeAsync<object>("myLib.focusElement", elementRef);
        }
    }
}
```

<span data-ttu-id="d75b2-168">Теперь вы сможете сосредоточиться входные данные в любом из компонентов:</span><span class="sxs-lookup"><span data-stu-id="d75b2-168">Now you can focus inputs in any of your components:</span></span>

```cshtml
@using MyLib

<input ref="username" />
<button onclick="@SetFocus">Set focus</button>

@functions {
    ElementRef username;

    void SetFocus()
    {
        username.Focus();
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="d75b2-169">`username` Переменной заполняется только после того как компонент осуществляет визуализацию и его выходные данные содержат `<input>` элемент.</span><span class="sxs-lookup"><span data-stu-id="d75b2-169">The `username` variable is only populated after the component renders and its output includes the `<input>` element.</span></span> <span data-ttu-id="d75b2-170">Если при попытке передать другой незаполненной `ElementRef` в код JavaScript код JavaScript получает `null`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-170">If you try to pass an unpopulated `ElementRef` to JavaScript code, the JavaScript code receives `null`.</span></span> <span data-ttu-id="d75b2-171">Для управления ссылки на элементы, после завершения отрисовки (чтобы устанавливать исходный фокус в элементе) используйте компонент `OnAfterRenderAsync` или `OnAfterRender` [методы жизненного цикла компонент](xref:razor-components/components#lifecycle-methods).</span><span class="sxs-lookup"><span data-stu-id="d75b2-171">To manipulate element references after the component has finished rendering (to set the initial focus on an element) use the `OnAfterRenderAsync` or `OnAfterRender` [component lifecycle methods](xref:razor-components/components#lifecycle-methods).</span></span>

## <a name="invoke-net-methods-from-javascript-functions"></a><span data-ttu-id="d75b2-172">Вызов методов .NET из функции JavaScript</span><span class="sxs-lookup"><span data-stu-id="d75b2-172">Invoke .NET methods from JavaScript functions</span></span>

### <a name="static-net-method-call"></a><span data-ttu-id="d75b2-173">Статический вызов метода .NET</span><span class="sxs-lookup"><span data-stu-id="d75b2-173">Static .NET method call</span></span>

<span data-ttu-id="d75b2-174">Чтобы вызвать статический метод .NET из JavaScript, используйте `DotNet.invokeMethod` или `DotNet.invokeMethodAsync` функции.</span><span class="sxs-lookup"><span data-stu-id="d75b2-174">To invoke a static .NET method from JavaScript, use the `DotNet.invokeMethod` or `DotNet.invokeMethodAsync` functions.</span></span> <span data-ttu-id="d75b2-175">Необходимо передать идентификатор статического метода, который вы хотите вызвать, имя сборки, содержащей функцию и все аргументы.</span><span class="sxs-lookup"><span data-stu-id="d75b2-175">Pass in the identifier of the static method you wish to call, the name of the assembly containing the function, and any arguments.</span></span> <span data-ttu-id="d75b2-176">Опять же асинхронный вариант является предпочтительным для поддержки сценариев на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d75b2-176">Again, the async version is preferred to support server-side scenarios.</span></span> <span data-ttu-id="d75b2-177">Чтобы иметь могут вызываться из JavaScript, метод .NET должен быть общедоступный статический и декорированные с `[JSInvokable]`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-177">To be invokable from JavaScript, the .NET method must be public, static, and decorated with `[JSInvokable]`.</span></span> <span data-ttu-id="d75b2-178">По умолчанию идентификатор метода — это имя метода, но можно указать другой идентификатор с помощью `JSInvokableAttribute` конструктор.</span><span class="sxs-lookup"><span data-stu-id="d75b2-178">By default, the method identifier is the method name, but you can specify a different identifier using the `JSInvokableAttribute` constructor.</span></span> <span data-ttu-id="d75b2-179">Вызов открытые универсальные методы сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d75b2-179">Calling open generic methods isn't currently supported.</span></span>

<span data-ttu-id="d75b2-180">Образец приложения включает C# метод, чтобы вернуть массив `int`s.</span><span class="sxs-lookup"><span data-stu-id="d75b2-180">The sample app includes a C# method to return an array of `int`s.</span></span> <span data-ttu-id="d75b2-181">Метод дополняется `JSInvokable` атрибута.</span><span class="sxs-lookup"><span data-stu-id="d75b2-181">The method is decorated with the `JSInvokable` attribute.</span></span>

<span data-ttu-id="d75b2-182">*Pages/JsInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-182">*Pages/JsInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

<span data-ttu-id="d75b2-183">Клиенту JavaScript вызывает C# метода .NET.</span><span class="sxs-lookup"><span data-stu-id="d75b2-183">JavaScript served to the client invokes the C# .NET method.</span></span>

<span data-ttu-id="d75b2-184">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-184">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

<span data-ttu-id="d75b2-185">Когда **статический метод .NET триггера ReturnArrayAsync** выбрана кнопка, изучите выходные данные консоли в браузере веб-инструменты разработчиков:</span><span class="sxs-lookup"><span data-stu-id="d75b2-185">When the **Trigger .NET static method ReturnArrayAsync** button is selected, examine the console output in the browser's web developer tools:</span></span>

```console
Array(4) [ 1, 2, 3, 4 ]
```

<span data-ttu-id="d75b2-186">Четвертое значение массива передается в массив (`data.push(4);`) возвращаемый `ReturnArrayAsync`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-186">The fourth array value is pushed to the array (`data.push(4);`) returned by `ReturnArrayAsync`.</span></span>

### <a name="instance-method-call"></a><span data-ttu-id="d75b2-187">Вызов метода экземпляра</span><span class="sxs-lookup"><span data-stu-id="d75b2-187">Instance method call</span></span>

<span data-ttu-id="d75b2-188">Также можно вызывать методы экземпляра .NET из JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-188">You can also call .NET instance methods from JavaScript.</span></span> <span data-ttu-id="d75b2-189">Для вызова экземпляра метода .NET из JavaScript, сначала пройти экземпляр .NET в JavaScript, если поместить его в `DotNetObjectRef` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="d75b2-189">To invoke a .NET instance method from JavaScript, first pass the .NET instance to JavaScript by wrapping it in a `DotNetObjectRef` instance.</span></span> <span data-ttu-id="d75b2-190">Экземпляр .NET передается по ссылке на JavaScript, и можно вызывать методами экземпляра .NET для экземпляра с помощью `invokeMethod` или `invokeMethodAsync` функции.</span><span class="sxs-lookup"><span data-stu-id="d75b2-190">The .NET instance is passed by reference to JavaScript, and you can invoke .NET instance methods on the instance using the `invokeMethod` or `invokeMethodAsync` functions.</span></span> <span data-ttu-id="d75b2-191">Экземпляр .NET также можно передать в качестве аргумента, при вызове других методов .NET из JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-191">The .NET instance can also be passed as an argument when invoking other .NET methods from JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="d75b2-192">Пример приложения регистрирует сообщения в консоль на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="d75b2-192">The sample app logs messages to the client-side console.</span></span> <span data-ttu-id="d75b2-193">Для приведенных ниже примерах демонстрируется в примере приложения проверьте выходные данные консоли браузера в средствах разработчика браузера.</span><span class="sxs-lookup"><span data-stu-id="d75b2-193">For the following examples demonstrated by the sample app, examine the browser's console output in the browser's developer tools.</span></span>

<span data-ttu-id="d75b2-194">При **метод экземпляра триггера .NET HelloHelper.SayHello** выбран переключатель, `ExampleJsInterop.CallHelloHelperSayHello` вызывается и передает имя, `Blazor`, в метод.</span><span class="sxs-lookup"><span data-stu-id="d75b2-194">When the **Trigger .NET instance method HelloHelper.SayHello** button is selected, `ExampleJsInterop.CallHelloHelperSayHello` is called and passes a name, `Blazor`, to the method.</span></span>

<span data-ttu-id="d75b2-195">*Pages/JsInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-195">*Pages/JsInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

<span data-ttu-id="d75b2-196">`CallHelloHelperSayHello` вызывает функцию JavaScript `sayHello` для нового экземпляра `HelloHelper`.</span><span class="sxs-lookup"><span data-stu-id="d75b2-196">`CallHelloHelperSayHello` invokes the JavaScript function `sayHello` with a new instance of `HelloHelper`.</span></span>

<span data-ttu-id="d75b2-197">*JsInteropClasses/ExampleJsInterop.cs*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-197">*JsInteropClasses/ExampleJsInterop.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

<span data-ttu-id="d75b2-198">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-198">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

<span data-ttu-id="d75b2-199">Передается имя `HelloHelper`в конструктор, который задает `HelloHelper.Name` свойства.</span><span class="sxs-lookup"><span data-stu-id="d75b2-199">The name is passed to `HelloHelper`'s constructor, which sets the `HelloHelper.Name` property.</span></span> <span data-ttu-id="d75b2-200">Когда функция JavaScript, которая `sayHello` выполняется, `HelloHelper.SayHello` возвращает `Hello, {Name}!` сообщения, которое записывается в консоль с помощью функции JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d75b2-200">When the JavaScript function `sayHello` is executed, `HelloHelper.SayHello` returns the `Hello, {Name}!` message, which is written to the console by the JavaScript function.</span></span>

<span data-ttu-id="d75b2-201">*JsInteropClasses/HelloHelper.cs*:</span><span class="sxs-lookup"><span data-stu-id="d75b2-201">*JsInteropClasses/HelloHelper.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

<span data-ttu-id="d75b2-202">Выходные данные в браузере веб-инструменты разработчиков консоли:</span><span class="sxs-lookup"><span data-stu-id="d75b2-202">Console output in the browser's web developer tools:</span></span>

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a><span data-ttu-id="d75b2-203">Совместное использование взаимодействия кода в библиотеку классов для компонента Razor</span><span class="sxs-lookup"><span data-stu-id="d75b2-203">Share interop code in a Razor Component class library</span></span>

<span data-ttu-id="d75b2-204">Взаимодействия кода JavaScript, которые могут быть включены в библиотеку классов для компонента Razor (`dotnet new blazorlib`), который позволяет совместно использовать код в виде пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="d75b2-204">JavaScript interop code can be included in a Razor Component class library (`dotnet new blazorlib`), which allows you to share the code in a NuGet package.</span></span>

<span data-ttu-id="d75b2-205">Библиотеки классов Razor компонент обрабатывает внедрения ресурсов JavaScript в построенной сборке.</span><span class="sxs-lookup"><span data-stu-id="d75b2-205">The Razor Component class library handles embedding JavaScript resources in the built assembly.</span></span> <span data-ttu-id="d75b2-206">Файлы JavaScript, помещаются в *wwwroot* папки и инструментарий отвечает за внедрение ресурсов при построении библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d75b2-206">The JavaScript files are placed in the *wwwroot* folder, and the tooling takes care of embedding the resources when the library is built.</span></span>

<span data-ttu-id="d75b2-207">Встроенный пакет NuGet есть ссылки в файле проекта приложения, так же, как используется ссылка на любой обычный пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="d75b2-207">The built NuGet package is referenced in the project file of the app just as any normal NuGet package is referenced.</span></span> <span data-ttu-id="d75b2-208">После восстановления приложения, код приложения может вызывать в JavaScript, как если бы он был C#.</span><span class="sxs-lookup"><span data-stu-id="d75b2-208">After the app has been restored, app code can call into JavaScript as if it were C#.</span></span>
