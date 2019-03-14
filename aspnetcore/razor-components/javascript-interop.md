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
# <a name="razor-components-javascript-interop"></a>Взаимодействие компонентов JavaScript в Razor

По [Нельсон Calvarro Хавьер](https://github.com/javiercn), [Дэниэл рот](https://github.com/danroth27), и [Люк Лэтем](https://github.com/guardrex)

В приложение Razor компоненты могут вызывать функции JavaScript, .NET, .NET методы из кода JavaScript.

## <a name="invoke-javascript-functions-from-net-methods"></a>Вызова функций JavaScript из методов .NET

Бывают случаи, когда код .NET не требуется для вызова функции JavaScript. Например вызов JavaScript может предоставлять возможности браузера или функции из библиотеки JavaScript в приложение.

Чтобы вызывать JavaScript с помощью .NET, используйте `IJSRuntime` абстракции. `InvokeAsync<T>` Метод `IJSRuntime` принимает идентификатор для функции JavaScript, который вы хотите вызвать, наряду с любое количество аргументов, сериализуемые в формат JSON. Идентификатор функции задается относительно глобальной области (`window`). Если вы хотите вызвать `window.someScope.someFunction`, идентификатор является `someScope.someFunction`. Нет необходимости зарегистрировать функцию перед его вызовом. Тип возвращаемого значения `T` также должны быть JSON сериализуемыми.

Для приложений ASP.NET Core Razor компоненты на стороне сервера:

* Нескольких пользовательских запросов обрабатываются приложением на стороне сервера. Не вызывайте `JSRuntime.Current` в компоненте для вызова функций JavaScript.
* Внедрить `IJSRuntime` абстракции и использование внедренного объекта взаимодействия вызовов JavaScript.

Следующий пример построен на основе [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), экспериментальный декодера, на основе JavaScript. В примере для вызова функции JavaScript из C# метод. Функция JavaScript, которая принимает массив байтов из C# метод, декодирует массива и возвращает текст в компонент для отображения.

Внутри `<head>` элемент *wwwroot/index.html*, предоставляют функции, которая использует `TextDecoder` для декодирования переданный массив:

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

Код JavaScript, например код, показанный в предыдущем примере, также может быть загружено с помощью файла JavaScript со ссылкой на файл скрипта в *wwwroot/index.html* файла.

Следующие компоненты:

* Вызывает `ConvertArray` функцию JavaScript с помощью `JsRuntime` при кнопки компонент (**преобразовать массив**) выбран.
* После вызова функции JavaScript, переданный массив преобразуется в строку. Строка возвращается к компоненту для отображения.

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

Для клиентских приложений Blazor `IJSRuntime` абстракции, доступен из `JSRuntime.Current`, которая относится к запросу текущего пользователя. Поскольку имеется только один пользователь Blazor приложения на стороне клиента, с помощью `JSRuntime.Current` для вызова JavaScript функция работает как обычно. Использовать только `JSRuntime.Current` в приложениях Blazor на стороне клиента.

В примере клиентского приложения, используемый в этом разделе доступны две функции JavaScript для клиентского приложения, взаимодействия с DOM для ввода данных пользователем и отображения приветственное сообщение:

* `showPrompt` &ndash; Выводит приглашение на ввод пользователя (имя пользователя) и возвращает имя вызывающей стороне.
* `displayWelcome` &ndash; Назначает приветственное сообщение от вызывающего объекта DOM с `id` из `welcome`.

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

Место `<script>` тег, который ссылается на файл JavaScript в *wwwroot/index.html* файла:

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

Не разместить тег скрипта в файле компонента, поскольку тег script не может обновляться динамически.

Методы взаимодействие .NET с помощью функций JavaScript путем вызова `InvokeAsync<T>` метод `IJSRuntime`.

Пример приложения использует пару C# методы, `Prompt` и `Display`, чтобы вызвать `showPrompt` и `displayWelcome` функции JavaScript:

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

`IJSRuntime` Абстракции является асинхронным, разрешающие сценарии на стороне сервера. Если приложение выполняется на стороне клиента и нужно вызвать функцию JavaScript синхронно, получено нисходящим `IJSInProcessRuntime` и вызвать `Invoke<T>` вместо этого. Мы рекомендуем, что большинство используют взаимодействия библиотек JavaScript асинхронные интерфейсы API, чтобы обеспечить библиотеки доступны в все сценарии, на стороне клиента или на стороне сервера.

Пример приложения включает компонент для демонстрации взаимодействия JS. Компонент:

* Получает входные данные пользователя с помощью строки JS.
* Возвращает текст к компоненту для обработки.
* Вызывает функцию второй JS, взаимодействующий с DOM для отображения приветственного сообщения.

*Pages/JSInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. При `TriggerJsPrompt` выполняется путем выбора компонента **триггера JavaScript Prompt** кнопки `ExampleJsInterop.Prompt` метод в C# вызова кода.
1. `Prompt` JavaScript выполняется метод `showPrompt` функция, предоставленная в *wwwroot/exampleJsInterop.js* файла.
1. `showPrompt` Функция принимает вводимые пользователем данные (имя пользователя), являющееся HTML-кодирование и осуществляется возврат в `Prompt` метод и в конечном итоге обратно в компонент. Компонент сохраняет имя пользователя в локальной переменной, `name`.
1. Строки хранятся в `name` является частью приветственное сообщение, передаваемое секунды C# метод, `ExampleJsInterop.Display`.
1. `Display` вызывает функцию JavaScript, `displayWelcome`, который отображает приветственное сообщение в тег заголовка.

## <a name="capture-references-to-elements"></a>Захват ссылок на элементы

Некоторые [взаимодействия JavaScript](xref:razor-components/javascript-interop) сценарии требуют ссылки на элементы HTML. Например, библиотека пользовательского интерфейса может потребоваться ссылки на элемент для инициализации, или может потребоваться вызвать подобные API-интерфейсы на элементе, например `focus` или `play`.

Ссылки на элементы HTML в компоненте можно записать, добавив `ref` атрибут к элементу HTML, а затем определив поле типа `ElementRef` , имя которого совпадает со значением `ref` атрибута.

В следующем примере показано, захват ссылку на элемент ввода имени пользователя:

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> Сделать **не** использовать ссылки на элементы, записанный как способ заполнения модели DOM. Это может помешать модели для декларативной подготовки отчетов.

Что касается кода .NET является, `ElementRef` – это прозрачный дескриптор. *Только* , что можно сделать с ней будет передавать его с помощью кода JavaScript через взаимодействие JavaScript. При этом код JavaScript на стороне получает `HTMLElement` экземпляр, который его можно использовать с обычной интерфейсы API модели DOM.

Например следующий код определяет метод расширения .NET, который позволяет установить фокус на элементе:

*MyLib.js*:

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

*ElementRefExtensions.cs*:

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

Теперь вы сможете сосредоточиться входные данные в любом из компонентов:

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
> `username` Переменной заполняется только после того как компонент осуществляет визуализацию и его выходные данные содержат `<input>` элемент. Если при попытке передать другой незаполненной `ElementRef` в код JavaScript код JavaScript получает `null`. Для управления ссылки на элементы, после завершения отрисовки (чтобы устанавливать исходный фокус в элементе) используйте компонент `OnAfterRenderAsync` или `OnAfterRender` [методы жизненного цикла компонент](xref:razor-components/components#lifecycle-methods).

## <a name="invoke-net-methods-from-javascript-functions"></a>Вызов методов .NET из функции JavaScript

### <a name="static-net-method-call"></a>Статический вызов метода .NET

Чтобы вызвать статический метод .NET из JavaScript, используйте `DotNet.invokeMethod` или `DotNet.invokeMethodAsync` функции. Необходимо передать идентификатор статического метода, который вы хотите вызвать, имя сборки, содержащей функцию и все аргументы. Опять же асинхронный вариант является предпочтительным для поддержки сценариев на стороне сервера. Чтобы иметь могут вызываться из JavaScript, метод .NET должен быть общедоступный статический и декорированные с `[JSInvokable]`. По умолчанию идентификатор метода — это имя метода, но можно указать другой идентификатор с помощью `JSInvokableAttribute` конструктор. Вызов открытые универсальные методы сейчас не поддерживается.

Образец приложения включает C# метод, чтобы вернуть массив `int`s. Метод дополняется `JSInvokable` атрибута.

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

Клиенту JavaScript вызывает C# метода .NET.

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

Когда **статический метод .NET триггера ReturnArrayAsync** выбрана кнопка, изучите выходные данные консоли в браузере веб-инструменты разработчиков:

```console
Array(4) [ 1, 2, 3, 4 ]
```

Четвертое значение массива передается в массив (`data.push(4);`) возвращаемый `ReturnArrayAsync`.

### <a name="instance-method-call"></a>Вызов метода экземпляра

Также можно вызывать методы экземпляра .NET из JavaScript. Для вызова экземпляра метода .NET из JavaScript, сначала пройти экземпляр .NET в JavaScript, если поместить его в `DotNetObjectRef` экземпляра. Экземпляр .NET передается по ссылке на JavaScript, и можно вызывать методами экземпляра .NET для экземпляра с помощью `invokeMethod` или `invokeMethodAsync` функции. Экземпляр .NET также можно передать в качестве аргумента, при вызове других методов .NET из JavaScript.

> [!NOTE]
> Пример приложения регистрирует сообщения в консоль на стороне клиента. Для приведенных ниже примерах демонстрируется в примере приложения проверьте выходные данные консоли браузера в средствах разработчика браузера.

При **метод экземпляра триггера .NET HelloHelper.SayHello** выбран переключатель, `ExampleJsInterop.CallHelloHelperSayHello` вызывается и передает имя, `Blazor`, в метод.

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

`CallHelloHelperSayHello` вызывает функцию JavaScript `sayHello` для нового экземпляра `HelloHelper`.

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

Передается имя `HelloHelper`в конструктор, который задает `HelloHelper.Name` свойства. Когда функция JavaScript, которая `sayHello` выполняется, `HelloHelper.SayHello` возвращает `Hello, {Name}!` сообщения, которое записывается в консоль с помощью функции JavaScript.

*JsInteropClasses/HelloHelper.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

Выходные данные в браузере веб-инструменты разработчиков консоли:

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a>Совместное использование взаимодействия кода в библиотеку классов для компонента Razor

Взаимодействия кода JavaScript, которые могут быть включены в библиотеку классов для компонента Razor (`dotnet new blazorlib`), который позволяет совместно использовать код в виде пакета NuGet.

Библиотеки классов Razor компонент обрабатывает внедрения ресурсов JavaScript в построенной сборке. Файлы JavaScript, помещаются в *wwwroot* папки и инструментарий отвечает за внедрение ресурсов при построении библиотеки.

Встроенный пакет NuGet есть ссылки в файле проекта приложения, так же, как используется ссылка на любой обычный пакет NuGet. После восстановления приложения, код приложения может вызывать в JavaScript, как если бы он был C#.
