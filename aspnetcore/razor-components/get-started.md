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
# <a name="get-started-with-razor-components"></a>Начало работы с Razor компонентов

Авторы: [Дэниэл Рот (Daniel Roth)](https://github.com/danroth27) и [Люк Лэтем (Luke Latham)](https://github.com/guardrex)

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Предварительные требования

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

Создание первого проекта Razor компонентов в Visual Studio:

1. Выберите **файл** > **новый проект** > **Web** > **веб-приложение ASP.NET Core**.
1. Убедитесь, что **.NET Core** и **ASP.NET Core 3.0** выбраны вверху.
1. Выберите **компоненты Razor** шаблона и выберите **ОК**.

   ![Диалоговое окно нового приложения](https://msdnshared.blob.core.windows.net/media/2019/01/razor-components-template.png)

1. Нажмите клавишу **F5** для запуска приложения.

Поздравляем! Вы только что выполнили свое первое приложение Razor компоненты!

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

# <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli/)

Предварительные требования

* [Предварительная версия .NET core SDK 3.0](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. Создание первого проекта Razor компонентов из командной оболочки:

   ```console
   dotnet new razorcomponents -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. В браузере перейдите на адрес `https://localhost:5001`.

Поздравляем! Вы только что выполнили свое первое приложение Razor компоненты!

---

## <a name="razor-components-project"></a>Компоненты проекта Razor

Решения, созданного с помощью Razor компоненты шаблона содержит два проекта:

* *WebApplication1.Server* &ndash; серверный проект — это проект ASP.NET Core, настройка для размещения приложения компонентов Razor.
* *WebApplication1.App* &ndash; клиентские веб-проекта пользовательского интерфейса, использующего компоненты Razor.

Логика пользовательского интерфейса в *WebApplication1.App* проекта отделен от остальной части приложения из-за технических ограничений в предварительной версии 2 ASP.NET Core 3.0. Расширение файла Razor (*.cshtml*) используется для компонентов Razor также используется для представления Razor Pages и MVC. В настоящее время компоненты Razor и Razor Pages/MVC имеют моделей разных компиляции, поэтому файлы Razor компоненты Razor хранятся отдельно. В следующей предварительной версии, мы планируем запустить новое расширение файла для компонентов Razor (*.razor*). Компоненты, страниц и представлений будет размещаться *в том же проекте*.

При запуске приложения, доступны несколько страницы из вкладок на боковой панели.

* Главная страница
* Счетчик
* Выборки данных

На странице Counter нажмите кнопку **Click me** (Щелкните здесь), чтобы увеличить значение счетчика без обновления страницы. Обычно для увеличения значений счетчика на веб-странице требуется код JavaScript, но Razor Components реализует более правильный подход с использованием C#.

*WebApplication1.App/Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

Запрос `/counter` в браузере, в соответствии с `@page` директива сверху, компонент счетчика для отображения его содержимого. В выполняющейся в памяти представление дерева визуализации, можно использовать для обновления пользовательского интерфейса в гибкий и эффективный способ отображения компонентов.

Каждый раз **Click me** выбранной кнопки:

* `onclick` События.
* вызывается метод `IncrementCount` .
* `currentCount` Увеличивается.
* Компонент отображается снова.

Среда выполнения сравнивает новое содержимое для предыдущее содержимое и применяется измененное содержимое только для модели объектов документов (DOM).

Добавление компонента в другой компонент, используя синтаксис типа HTML. Параметры компонента указываются с помощью атрибутов или дочернего содержимого. Например, компонент счетчика можно добавить на домашнюю страницу приложения, добавив `<Counter />` элемент компонент индекса.

*WebApplication1.App/Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

Запустите приложение. Домашняя страница имеет свой собственный счетчика.

Чтобы добавить параметр к компоненту счетчика, обновите компонента `@functions` блок:

* Добавьте свойство для `IncrementAmount` с `[Parameter]` атрибута.
* Изменение метод `IncrementCount`, чтобы он использовал `IncrementAmount` при увеличении значения `currentCount`.

*WebApplication1.App/Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

Укажите параметр `IncrementAmount` в элементе `<Counter>` для компонента домашней страницы, используя атрибут.

*WebApplication1.App/Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

Запустите приложение. Домашняя страница имеет свой собственный счетчик, который увеличивается каждый раз, десять **Click me** выбранной кнопки.

## <a name="next-steps"></a>Следующие шаги

<xref:tutorials/first-razor-components-app>
