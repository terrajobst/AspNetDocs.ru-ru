---
title: Начало работы с Razor компонентов
author: guardrex
description: Узнайте, как приступить к работе с компонентами Razor путем создания и изменения проекта Razor компонентов.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/03/2019
uid: razor-components/get-started
ms.openlocfilehash: a9ada603e5ed4e0e75c4aebc5105c331118666e6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036391"
---
# <a name="get-started-with-razor-components"></a><span data-ttu-id="99cde-103">Начало работы с Razor компонентов</span><span class="sxs-lookup"><span data-stu-id="99cde-103">Get started with Razor Components</span></span>

<span data-ttu-id="99cde-104">Авторы: [Дэниэл Рот (Daniel Roth)](https://github.com/danroth27) и [Люк Лэтем (Luke Latham)](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="99cde-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="99cde-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99cde-105">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="99cde-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="99cde-106">Prerequisites:</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

<span data-ttu-id="99cde-107">Создание первого проекта Razor компонентов в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="99cde-107">To create your first Razor Components project in Visual Studio:</span></span>

1. <span data-ttu-id="99cde-108">Выберите **файл** > **новый проект** > **Web** > **веб-приложение ASP.NET Core**.</span><span class="sxs-lookup"><span data-stu-id="99cde-108">Select **File** > **New Project** > **Web** > **ASP.NET Core Web Application**.</span></span>
1. <span data-ttu-id="99cde-109">Убедитесь, что **.NET Core** и **ASP.NET Core 3.0** выбраны вверху.</span><span class="sxs-lookup"><span data-stu-id="99cde-109">Make sure **.NET Core** and **ASP.NET Core 3.0** are selected at the top.</span></span>
1. <span data-ttu-id="99cde-110">Выберите **компоненты Razor** шаблона и выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="99cde-110">Choose the **Razor Components** template and select **OK**.</span></span>

   ![Диалоговое окно нового приложения](https://msdnshared.blob.core.windows.net/media/2019/01/razor-components-template.png)

1. <span data-ttu-id="99cde-112">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="99cde-112">Press **F5** to run the app.</span></span>

<span data-ttu-id="99cde-113">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="99cde-113">Congratulations!</span></span> <span data-ttu-id="99cde-114">Вы только что выполнили свое первое приложение Razor компоненты!</span><span class="sxs-lookup"><span data-stu-id="99cde-114">You just ran your first Razor Components app!</span></span>

<!--

# [Visual Studio Code](#tab/visual-studio-code)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vsc-3.0.md)]

To create your first Razor Components project in Visual Studio Code:

1. Execute the following command from a command shell:

   ```console
   dotnet new razorcomponents -o WebApplication1
   ```

1. Open the *WebApplication1* folder in Visual Studio Code.

1. Add a *.vscode* folder.

1. Add a *tasks.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/tasks.json)]

1. Add a *launch.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/launch.json)]

1. Execute the app using the Visual Studio Code debugger.

1. In a browser, navigate to `https://localhost:5001`.

Congratulations! You just ran your first Razor Components app!

# [Visual Studio for Mac](#tab/visual-studio-mac)

.NET Core 3.0 will be supported with Visual Studio for Mac version 8.0 or later. Visual Studio for Mac version 8.0 Preview isn't available at this time.

Use the [.NET Core CLI version of this topic](xref:razor-components/get-started?tabs=netcore-cli) on macOS.


[!INCLUDE[](~/includes/net-core-prereqs-mac-3.0.md)]

To create your first project Razor Components project in Visual Studio for Mac:

1. Select **File** > **New Solution** or **New Project**.
1. In the sidebar, select **.NET Core** > **App**.
1. Select **ASP.NET Core Razor Components** and select **Next**.
1. The **Target Framework** defaults to **.NET Core 3.0**. Select **Next**.
1. In the **Project Name** field, enter `WebApplication1`. Select **Create**.
1. Select **Run** > **Run Without Debugging** to run the app *without the debugger*. Running with the debugger isn't supported at this time.

Congratulations! You just ran your first Razor Components app!
-->

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="99cde-115">Интерфейс командной строки .NET Core</span><span class="sxs-lookup"><span data-stu-id="99cde-115">.NET Core CLI</span></span>](#tab/netcore-cli/)

<span data-ttu-id="99cde-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="99cde-116">Prerequisites:</span></span>

* [<span data-ttu-id="99cde-117">Предварительная версия .NET core SDK 3.0</span><span class="sxs-lookup"><span data-stu-id="99cde-117">.NET Core SDK 3.0 Preview</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. <span data-ttu-id="99cde-118">Создание первого проекта Razor компонентов из командной оболочки:</span><span class="sxs-lookup"><span data-stu-id="99cde-118">To create your first Razor Components project from a command shell:</span></span>

   ```console
   dotnet new razorcomponents -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. <span data-ttu-id="99cde-119">В браузере перейдите на адрес `https://localhost:5001`.</span><span class="sxs-lookup"><span data-stu-id="99cde-119">In a browser, navigate to `https://localhost:5001`.</span></span>

<span data-ttu-id="99cde-120">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="99cde-120">Congratulations!</span></span> <span data-ttu-id="99cde-121">Вы только что выполнили свое первое приложение Razor компоненты!</span><span class="sxs-lookup"><span data-stu-id="99cde-121">You just ran your first Razor Components app!</span></span>

---

## <a name="razor-components-project"></a><span data-ttu-id="99cde-122">Компоненты проекта Razor</span><span class="sxs-lookup"><span data-stu-id="99cde-122">Razor Components project</span></span>

<span data-ttu-id="99cde-123">Решения, созданного с помощью Razor компоненты шаблона содержит два проекта:</span><span class="sxs-lookup"><span data-stu-id="99cde-123">The solution created by the Razor Components template contains two projects:</span></span>

* <span data-ttu-id="99cde-124">*WebApplication1.Server* &ndash; серверный проект — это проект ASP.NET Core, настройка для размещения приложения компонентов Razor.</span><span class="sxs-lookup"><span data-stu-id="99cde-124">*WebApplication1.Server* &ndash; The server project is an ASP.NET Core project set up to host the Razor Components app.</span></span>
* <span data-ttu-id="99cde-125">*WebApplication1.App* &ndash; клиентские веб-проекта пользовательского интерфейса, использующего компоненты Razor.</span><span class="sxs-lookup"><span data-stu-id="99cde-125">*WebApplication1.App* &ndash; The client-side web UI project that uses Razor Components.</span></span>

<span data-ttu-id="99cde-126">Логика пользовательского интерфейса в *WebApplication1.App* проекта отделен от остальной части приложения из-за технических ограничений в предварительной версии 2 ASP.NET Core 3.0.</span><span class="sxs-lookup"><span data-stu-id="99cde-126">The UI logic in the *WebApplication1.App* project is separated from the rest of the app due to a technical limitation in ASP.NET Core 3.0 Preview 2.</span></span> <span data-ttu-id="99cde-127">Расширение файла Razor (*.cshtml*) используется для компонентов Razor также используется для представления Razor Pages и MVC.</span><span class="sxs-lookup"><span data-stu-id="99cde-127">The Razor file extension (*.cshtml*) used for Razor Components is also used for Razor Pages and MVC views.</span></span> <span data-ttu-id="99cde-128">В настоящее время компоненты Razor и Razor Pages/MVC имеют моделей разных компиляции, поэтому файлы Razor компоненты Razor хранятся отдельно.</span><span class="sxs-lookup"><span data-stu-id="99cde-128">Currently, Razor Components and Razor Pages/MVC have different compilation models, so the Razor Components Razor files are kept separate.</span></span> <span data-ttu-id="99cde-129">В следующей предварительной версии, мы планируем запустить новое расширение файла для компонентов Razor (*.razor*).</span><span class="sxs-lookup"><span data-stu-id="99cde-129">In a future preview, we plan to introduce a new file extension for Razor Components (*.razor*).</span></span> <span data-ttu-id="99cde-130">Компоненты, страниц и представлений будет размещаться *в том же проекте*.</span><span class="sxs-lookup"><span data-stu-id="99cde-130">Components, pages, and views will be hosted *in the same project*.</span></span>

<span data-ttu-id="99cde-131">При запуске приложения, доступны несколько страницы из вкладок на боковой панели.</span><span class="sxs-lookup"><span data-stu-id="99cde-131">When the app is run, multiple pages are available from tabs in the sidebar:</span></span>

* <span data-ttu-id="99cde-132">Главная страница</span><span class="sxs-lookup"><span data-stu-id="99cde-132">Home</span></span>
* <span data-ttu-id="99cde-133">Счетчик</span><span class="sxs-lookup"><span data-stu-id="99cde-133">Counter</span></span>
* <span data-ttu-id="99cde-134">Выборки данных</span><span class="sxs-lookup"><span data-stu-id="99cde-134">Fetch data</span></span>

<span data-ttu-id="99cde-135">На странице Counter нажмите кнопку **Click me** (Щелкните здесь), чтобы увеличить значение счетчика без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="99cde-135">On the Counter page, select the **Click me** button to increment the counter without a page refresh.</span></span> <span data-ttu-id="99cde-136">Обычно для увеличения значений счетчика на веб-странице требуется код JavaScript, но Razor Components реализует более правильный подход с использованием C#.</span><span class="sxs-lookup"><span data-stu-id="99cde-136">Incrementing a counter in a webpage normally requires writing JavaScript, but Razor Components provides a better approach using C#.</span></span>

<span data-ttu-id="99cde-137">*WebApplication1.App/Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="99cde-137">*WebApplication1.App/Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

<span data-ttu-id="99cde-138">Запрос `/counter` в браузере, в соответствии с `@page` директива сверху, компонент счетчика для отображения его содержимого.</span><span class="sxs-lookup"><span data-stu-id="99cde-138">A request for `/counter` in the browser, as specified by the `@page` directive at the top, causes the Counter component to render its content.</span></span> <span data-ttu-id="99cde-139">В выполняющейся в памяти представление дерева визуализации, можно использовать для обновления пользовательского интерфейса в гибкий и эффективный способ отображения компонентов.</span><span class="sxs-lookup"><span data-stu-id="99cde-139">Components render into an in-memory representation of the render tree that can then be used to update the UI in a flexible and efficient way.</span></span>

<span data-ttu-id="99cde-140">Каждый раз **Click me** выбранной кнопки:</span><span class="sxs-lookup"><span data-stu-id="99cde-140">Each time the **Click me** button is selected:</span></span>

* <span data-ttu-id="99cde-141">`onclick` События.</span><span class="sxs-lookup"><span data-stu-id="99cde-141">The `onclick` event is fired.</span></span>
* <span data-ttu-id="99cde-142">вызывается метод `IncrementCount` .</span><span class="sxs-lookup"><span data-stu-id="99cde-142">The `IncrementCount` method is called.</span></span>
* <span data-ttu-id="99cde-143">`currentCount` Увеличивается.</span><span class="sxs-lookup"><span data-stu-id="99cde-143">The `currentCount` is incremented.</span></span>
* <span data-ttu-id="99cde-144">Компонент отображается снова.</span><span class="sxs-lookup"><span data-stu-id="99cde-144">The component is rendered again.</span></span>

<span data-ttu-id="99cde-145">Среда выполнения сравнивает новое содержимое для предыдущее содержимое и применяется измененное содержимое только для модели объектов документов (DOM).</span><span class="sxs-lookup"><span data-stu-id="99cde-145">The runtime compares the new content to the previous content and only applies the changed content to the Document Object Model (DOM).</span></span>

<span data-ttu-id="99cde-146">Добавление компонента в другой компонент, используя синтаксис типа HTML.</span><span class="sxs-lookup"><span data-stu-id="99cde-146">Add a component to another component using an HTML-like syntax.</span></span> <span data-ttu-id="99cde-147">Параметры компонента указываются с помощью атрибутов или дочернего содержимого.</span><span class="sxs-lookup"><span data-stu-id="99cde-147">Component parameters are specified using attributes or child content.</span></span> <span data-ttu-id="99cde-148">Например, компонент счетчика можно добавить на домашнюю страницу приложения, добавив `<Counter />` элемент компонент индекса.</span><span class="sxs-lookup"><span data-stu-id="99cde-148">For example, a Counter component can be added to the app's homepage by adding a `<Counter />` element to the Index component.</span></span>

<span data-ttu-id="99cde-149">*WebApplication1.App/Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="99cde-149">*WebApplication1.App/Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

<span data-ttu-id="99cde-150">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="99cde-150">Run the app.</span></span> <span data-ttu-id="99cde-151">Домашняя страница имеет свой собственный счетчика.</span><span class="sxs-lookup"><span data-stu-id="99cde-151">The homepage has its own counter.</span></span>

<span data-ttu-id="99cde-152">Чтобы добавить параметр к компоненту счетчика, обновите компонента `@functions` блок:</span><span class="sxs-lookup"><span data-stu-id="99cde-152">To add a parameter to the Counter component, update the component's `@functions` block:</span></span>

* <span data-ttu-id="99cde-153">Добавьте свойство для `IncrementAmount` с `[Parameter]` атрибута.</span><span class="sxs-lookup"><span data-stu-id="99cde-153">Add a property for `IncrementAmount` decorated with the `[Parameter]` attribute.</span></span>
* <span data-ttu-id="99cde-154">Изменение метод `IncrementCount`, чтобы он использовал `IncrementAmount` при увеличении значения `currentCount`.</span><span class="sxs-lookup"><span data-stu-id="99cde-154">Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.</span></span>

<span data-ttu-id="99cde-155">*WebApplication1.App/Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="99cde-155">*WebApplication1.App/Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

<span data-ttu-id="99cde-156">Укажите параметр `IncrementAmount` в элементе `<Counter>` для компонента домашней страницы, используя атрибут.</span><span class="sxs-lookup"><span data-stu-id="99cde-156">Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.</span></span>

<span data-ttu-id="99cde-157">*WebApplication1.App/Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="99cde-157">*WebApplication1.App/Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

<span data-ttu-id="99cde-158">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="99cde-158">Run the app.</span></span> <span data-ttu-id="99cde-159">Домашняя страница имеет свой собственный счетчик, который увеличивается каждый раз, десять **Click me** выбранной кнопки.</span><span class="sxs-lookup"><span data-stu-id="99cde-159">The homepage has its own counter that increments by ten each time the **Click me** button is selected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99cde-160">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="99cde-160">Next steps</span></span>

<xref:tutorials/first-razor-components-app>
