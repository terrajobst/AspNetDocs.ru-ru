---
uid: signalr/overview/advanced/dependency-injection
title: Внедрение зависимостей в SignalR | Документация Майкрософт
author: bradygaster
description: Версии программного обеспечения, используемые в этом разделе, Visual Studio 2013 .NET 4,5 SignalR версии 2 в предыдущих версиях этого раздела для получения сведений о более ранних версиях...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431868"
---
# <a name="dependency-injection-in-signalr"></a><span data-ttu-id="566a8-103">Внедрение зависимостей в SignalR</span><span class="sxs-lookup"><span data-stu-id="566a8-103">Dependency Injection in SignalR</span></span>

<span data-ttu-id="566a8-104">по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="566a8-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="566a8-105">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="566a8-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="566a8-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="566a8-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="566a8-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="566a8-107">.NET 4.5</span></span>
> - <span data-ttu-id="566a8-108">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="566a8-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="566a8-109">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="566a8-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="566a8-110">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="566a8-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="566a8-111">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="566a8-111">Questions and comments</span></span>
>
> <span data-ttu-id="566a8-112">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="566a8-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="566a8-113">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="566a8-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="566a8-114">Внедрение зависимостей — это способ удаления жестко запрограммированных зависимостей между объектами, что упрощает замену зависимостей объекта либо для тестирования (с помощью макетных объектов), либо для изменения поведения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="566a8-114">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="566a8-115">В этом руководстве показано, как выполнять внедрение зависимостей в концентраторах SignalR.</span><span class="sxs-lookup"><span data-stu-id="566a8-115">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="566a8-116">В нем также показано, как использовать контейнеры IoC с SignalR.</span><span class="sxs-lookup"><span data-stu-id="566a8-116">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="566a8-117">Контейнер IoC — это общая платформа для внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="566a8-117">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="566a8-118">Что такое внедрение зависимостей?</span><span class="sxs-lookup"><span data-stu-id="566a8-118">What is Dependency Injection?</span></span>

<span data-ttu-id="566a8-119">Пропустите этот раздел, если вы уже знакомы с внедрением зависимостей.</span><span class="sxs-lookup"><span data-stu-id="566a8-119">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="566a8-120">*Внедрение зависимостей* (DI) — это шаблон, в котором объекты не отвечают за создание собственных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="566a8-120">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="566a8-121">Ниже приведен простой пример мотивации.</span><span class="sxs-lookup"><span data-stu-id="566a8-121">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="566a8-122">Предположим, что у вас есть объект, который должен записывать сообщения в журнал.</span><span class="sxs-lookup"><span data-stu-id="566a8-122">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="566a8-123">Вы можете определить интерфейс ведения журнала:</span><span class="sxs-lookup"><span data-stu-id="566a8-123">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="566a8-124">В объекте можно создать `ILogger` для записи сообщений в журнал:</span><span class="sxs-lookup"><span data-stu-id="566a8-124">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="566a8-125">Это работает, но это не лучшая структура.</span><span class="sxs-lookup"><span data-stu-id="566a8-125">This works, but it's not the best design.</span></span> <span data-ttu-id="566a8-126">Если вы хотите заменить `FileLogger` другой реализацией `ILogger`, необходимо будет изменить `SomeComponent`.</span><span class="sxs-lookup"><span data-stu-id="566a8-126">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="566a8-127">Допустим, что многие другие объекты используют `FileLogger`, необходимо изменить их все.</span><span class="sxs-lookup"><span data-stu-id="566a8-127">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="566a8-128">Или, если вы решили сделать `FileLogger` Singleton, вам также потребуется внести изменения во всем приложении.</span><span class="sxs-lookup"><span data-stu-id="566a8-128">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="566a8-129">Лучшим подходом является «внедрение» `ILogger` в объект, например с помощью аргумента конструктора:</span><span class="sxs-lookup"><span data-stu-id="566a8-129">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="566a8-130">Теперь объект не отвечает за выбор `ILogger` для использования.</span><span class="sxs-lookup"><span data-stu-id="566a8-130">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="566a8-131">Можно переключать реализации `ILogger`, не изменяя зависимые от нее объекты.</span><span class="sxs-lookup"><span data-stu-id="566a8-131">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="566a8-132">Этот шаблон называется [внедрением конструктора](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="566a8-132">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="566a8-133">Другой шаблон — это внедрение метода присваивания, где зависимость задается через метод задания или свойство.</span><span class="sxs-lookup"><span data-stu-id="566a8-133">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="566a8-134">Простое внедрение зависимостей в SignalR</span><span class="sxs-lookup"><span data-stu-id="566a8-134">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="566a8-135">Рассмотрим приложение разговора из учебника [Начало работы с SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="566a8-135">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="566a8-136">Ниже приведен класс Hub из этого приложения.</span><span class="sxs-lookup"><span data-stu-id="566a8-136">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="566a8-137">Предположим, что необходимо сохранить сообщения разговора на сервере перед их отправкой.</span><span class="sxs-lookup"><span data-stu-id="566a8-137">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="566a8-138">Вы можете определить интерфейс, который абстрагирует эту функциональность, и использовать DI для внедрения интерфейса в класс `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="566a8-138">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="566a8-139">Единственная проблема заключается в том, что приложение SignalR не создает концентраторы напрямую. SignalR создает их для вас.</span><span class="sxs-lookup"><span data-stu-id="566a8-139">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="566a8-140">По умолчанию SignalR ждет, что класс концентратора имеет конструктор без параметров.</span><span class="sxs-lookup"><span data-stu-id="566a8-140">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="566a8-141">Однако можно легко зарегистрировать функцию для создания экземпляров концентратора и использовать эту функцию для выполнения внедрения.</span><span class="sxs-lookup"><span data-stu-id="566a8-141">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="566a8-142">Зарегистрируйте функцию, вызвав **GlobalHost. депенденциресолвер. Register**.</span><span class="sxs-lookup"><span data-stu-id="566a8-142">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="566a8-143">Теперь SignalR будет вызывать эту анонимную функцию при необходимости создания экземпляра `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="566a8-143">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="566a8-144">Контейнеры IoC</span><span class="sxs-lookup"><span data-stu-id="566a8-144">IoC Containers</span></span>

<span data-ttu-id="566a8-145">Предыдущий код подходит для простых случаев.</span><span class="sxs-lookup"><span data-stu-id="566a8-145">The previous code is fine for simple cases.</span></span> <span data-ttu-id="566a8-146">Но все еще пришлось написать следующее:</span><span class="sxs-lookup"><span data-stu-id="566a8-146">But you still had to write this:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

<span data-ttu-id="566a8-147">В сложном приложении с множеством зависимостей может потребоваться написать большой код "проводной связи".</span><span class="sxs-lookup"><span data-stu-id="566a8-147">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="566a8-148">Этот код может быть трудно поддерживать, особенно если зависимости являются вложенными.</span><span class="sxs-lookup"><span data-stu-id="566a8-148">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="566a8-149">Это также затрудняет тестирование модулей.</span><span class="sxs-lookup"><span data-stu-id="566a8-149">It is also hard to unit test.</span></span>

<span data-ttu-id="566a8-150">Одним из решений является использование контейнера IoC.</span><span class="sxs-lookup"><span data-stu-id="566a8-150">One solution is to use an IoC container.</span></span> <span data-ttu-id="566a8-151">Контейнер IoC — это программный компонент, отвечающий за управление зависимостями. Вы регистрируете типы в контейнере, а затем используете контейнер для создания объектов.</span><span class="sxs-lookup"><span data-stu-id="566a8-151">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="566a8-152">Контейнер автоматически определяет отношения зависимости.</span><span class="sxs-lookup"><span data-stu-id="566a8-152">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="566a8-153">Многие контейнеры IoC также позволяют контролировать время существования и области действия объекта.</span><span class="sxs-lookup"><span data-stu-id="566a8-153">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="566a8-154">"IoC" означает "инверсия управления", которая представляет собой общий шаблон, в котором инфраструктура вызывает код приложения.</span><span class="sxs-lookup"><span data-stu-id="566a8-154">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="566a8-155">Контейнер IoC конструирует ваши объекты, что «инвертирует» обычный поток управления.</span><span class="sxs-lookup"><span data-stu-id="566a8-155">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="566a8-156">Использование контейнеров IoC в SignalR</span><span class="sxs-lookup"><span data-stu-id="566a8-156">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="566a8-157">Возможно, приложение для разговора слишком просто, чтобы получить преимущество от IoC-контейнера.</span><span class="sxs-lookup"><span data-stu-id="566a8-157">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="566a8-158">Вместо этого давайте взглянем на пример [стокктиккер](http://nuget.org/packages/microsoft.aspnet.signalr.sample) .</span><span class="sxs-lookup"><span data-stu-id="566a8-158">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="566a8-159">Образец Стокктиккер определяет два основных класса:</span><span class="sxs-lookup"><span data-stu-id="566a8-159">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="566a8-160">`StockTickerHub`: класс Hub, который управляет подключениями клиентов.</span><span class="sxs-lookup"><span data-stu-id="566a8-160">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="566a8-161">`StockTicker`: одноэлементный экземпляр, содержащий цены акций, и периодически обновляет их.</span><span class="sxs-lookup"><span data-stu-id="566a8-161">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="566a8-162">`StockTickerHub` содержит ссылку на `StockTicker` Singleton, а `StockTicker` содержит ссылку на **ихубконнектионконтекст** для `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="566a8-162">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="566a8-163">Он использует этот интерфейс для взаимодействия с экземплярами `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="566a8-163">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="566a8-164">(Дополнительные сведения см. [в статье серверное вещание с помощью ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span><span class="sxs-lookup"><span data-stu-id="566a8-164">(For more information, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span></span>

<span data-ttu-id="566a8-165">Мы можем использовать контейнер IoC для унтангле этих зависимостей чуть ниже.</span><span class="sxs-lookup"><span data-stu-id="566a8-165">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="566a8-166">Во первых, давайте Упростите классы `StockTickerHub` и `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="566a8-166">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="566a8-167">В следующем коде я добавил в комментарий те части, которые нам не нужны.</span><span class="sxs-lookup"><span data-stu-id="566a8-167">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="566a8-168">Удалите конструктор без параметров из `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="566a8-168">Remove the parameterless constructor from `StockTickerHub`.</span></span> <span data-ttu-id="566a8-169">Вместо этого мы всегда будем использовать DI для создания концентратора.</span><span class="sxs-lookup"><span data-stu-id="566a8-169">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="566a8-170">Для Стокктиккер удалите одноэлементный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="566a8-170">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="566a8-171">Позже мы будем использовать контейнер IoC для управления временем жизни Стокктиккер.</span><span class="sxs-lookup"><span data-stu-id="566a8-171">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="566a8-172">Кроме того, сделайте конструктор открытым.</span><span class="sxs-lookup"><span data-stu-id="566a8-172">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="566a8-173">Теперь можно выполнить рефакторинг кода, создав интерфейс для `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="566a8-173">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="566a8-174">Мы будем использовать этот интерфейс для отделения `StockTickerHub` от класса `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="566a8-174">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="566a8-175">Visual Studio упрощает этот тип рефакторинга.</span><span class="sxs-lookup"><span data-stu-id="566a8-175">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="566a8-176">Откройте файл StockTicker.cs, щелкните правой кнопкой мыши объявление класса `StockTicker` и выберите **Рефакторинг** ... **Извлечение интерфейса**.</span><span class="sxs-lookup"><span data-stu-id="566a8-176">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="566a8-177">В диалоговом окне **Извлечение интерфейса** нажмите кнопку **выбрать все**.</span><span class="sxs-lookup"><span data-stu-id="566a8-177">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="566a8-178">Оставьте другие значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="566a8-178">Leave the other defaults.</span></span> <span data-ttu-id="566a8-179">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="566a8-179">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="566a8-180">Visual Studio создает новый интерфейс с именем `IStockTicker`, а также изменяет `StockTicker` на производный от `IStockTicker`.</span><span class="sxs-lookup"><span data-stu-id="566a8-180">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="566a8-181">Откройте файл IStockTicker.cs и измените интерфейс на **Public**.</span><span class="sxs-lookup"><span data-stu-id="566a8-181">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="566a8-182">В классе `StockTickerHub` измените два экземпляра `StockTicker` на `IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="566a8-182">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="566a8-183">Создание `IStockTicker` интерфейса не является обязательным, но я хотел продемонстрировать, как DI может помочь уменьшить взаимозависимость между компонентами в приложении.</span><span class="sxs-lookup"><span data-stu-id="566a8-183">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="566a8-184">Добавление библиотеки Нинжект</span><span class="sxs-lookup"><span data-stu-id="566a8-184">Add the Ninject Library</span></span>

<span data-ttu-id="566a8-185">Существует множество контейнеров IoC с открытым кодом для .NET.</span><span class="sxs-lookup"><span data-stu-id="566a8-185">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="566a8-186">В этом руководстве я буду использовать [нинжект](http://www.ninject.org/).</span><span class="sxs-lookup"><span data-stu-id="566a8-186">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="566a8-187">(Другие популярные библиотеки включают [Castle Windsor](http://www.castleproject.org/), [Spring.NET](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)и [StructureMap](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="566a8-187">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="566a8-188">Используйте диспетчер пакетов NuGet для установки [библиотеки нинжект](https://nuget.org/packages/Ninject/3.0.1.10).</span><span class="sxs-lookup"><span data-stu-id="566a8-188">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="566a8-189">В Visual Studio в меню **Сервис** выберите **диспетчер пакетов NuGet** > **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="566a8-189">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="566a8-190">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="566a8-190">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="566a8-191">Замена сопоставителя зависимостей SignalR</span><span class="sxs-lookup"><span data-stu-id="566a8-191">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="566a8-192">Чтобы использовать Нинжект в SignalR, создайте класс, производный от **дефаултдепенденциресолвер**.</span><span class="sxs-lookup"><span data-stu-id="566a8-192">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="566a8-193">Этот класс переопределяет **методы** **дефаултдепенденциресолвер** **и методом WebService.**</span><span class="sxs-lookup"><span data-stu-id="566a8-193">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="566a8-194">SignalR вызывает эти методы для создания различных объектов во время выполнения, включая экземпляры концентратора, а также различные службы, которые внутренне используют SignalR.</span><span class="sxs-lookup"><span data-stu-id="566a8-194">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="566a8-195">Метод **WebService** создает один экземпляр типа.</span><span class="sxs-lookup"><span data-stu-id="566a8-195">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="566a8-196">Переопределите этот метод, чтобы вызвать метод **TryGet** ядра нинжект.</span><span class="sxs-lookup"><span data-stu-id="566a8-196">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="566a8-197">Если этот метод возвращает значение null, возвращается сопоставитель по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="566a8-197">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="566a8-198">Метод **WebService** создает коллекцию объектов указанного типа.</span><span class="sxs-lookup"><span data-stu-id="566a8-198">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="566a8-199">Переопределите этот метод, чтобы объединить результаты из Нинжект с результатами распознавателя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="566a8-199">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="566a8-200">Настройка привязок Нинжект</span><span class="sxs-lookup"><span data-stu-id="566a8-200">Configure Ninject Bindings</span></span>

<span data-ttu-id="566a8-201">Теперь мы будем использовать Нинжект для объявления привязок типов.</span><span class="sxs-lookup"><span data-stu-id="566a8-201">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="566a8-202">Откройте класс Startup.cs приложения (созданный вручную в соответствии с инструкциями по пакету в `readme.txt`или созданный путем добавления проверки подлинности в проект).</span><span class="sxs-lookup"><span data-stu-id="566a8-202">Open your application's Startup.cs class (that you either created manually as per the package instructions in `readme.txt`, or that was created by adding authentication to your project).</span></span> <span data-ttu-id="566a8-203">В методе `Startup.Configuration` создайте контейнер Нинжект, который Нинжект вызывает *ядро*.</span><span class="sxs-lookup"><span data-stu-id="566a8-203">In the `Startup.Configuration` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="566a8-204">Создайте экземпляр пользовательского сопоставителя зависимостей:</span><span class="sxs-lookup"><span data-stu-id="566a8-204">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="566a8-205">Создайте привязку для `IStockTicker` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="566a8-205">Create a binding for `IStockTicker` as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

<span data-ttu-id="566a8-206">Этот код говорит две вещи.</span><span class="sxs-lookup"><span data-stu-id="566a8-206">This code is saying two things.</span></span> <span data-ttu-id="566a8-207">Во всяком случае, когда приложению требуется `IStockTicker`, ядро должно создать экземпляр `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="566a8-207">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="566a8-208">Во-вторых, класс `StockTicker` должен быть создан как одноэлементный объект.</span><span class="sxs-lookup"><span data-stu-id="566a8-208">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="566a8-209">Нинжект создаст один экземпляр объекта и возвратит тот же экземпляр для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="566a8-209">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="566a8-210">Создайте привязку для **ихубконнектионконтекст** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="566a8-210">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="566a8-211">Этот код создает анонимную функцию, которая возвращает **ихубконнектион**.</span><span class="sxs-lookup"><span data-stu-id="566a8-211">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="566a8-212">Метод **вхенинжектединто** указывает нинжект использовать эту функцию только при создании экземпляров `IStockTicker`.</span><span class="sxs-lookup"><span data-stu-id="566a8-212">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="566a8-213">Причина заключается в том, что SignalR создает экземпляры **ихубконнектионконтекст** внутренне, и мы не хотим переопределять способ их создания.</span><span class="sxs-lookup"><span data-stu-id="566a8-213">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="566a8-214">Эта функция применяется только к нашему `StockTicker` классу.</span><span class="sxs-lookup"><span data-stu-id="566a8-214">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="566a8-215">Передайте сопоставитель зависимостей в метод **мапсигналр** , добавив конфигурацию концентратора:</span><span class="sxs-lookup"><span data-stu-id="566a8-215">Pass the dependency resolver into the **MapSignalR** method by adding a hub configuration:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="566a8-216">Обновите метод Startup. Конфигуресигналр в классе Startup примера с помощью нового параметра:</span><span class="sxs-lookup"><span data-stu-id="566a8-216">Update the Startup.ConfigureSignalR method in the sample's Startup class with the new parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="566a8-217">Теперь SignalR будет использовать сопоставитель, указанный в **мапсигналр**, вместо распознавателя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="566a8-217">Now SignalR will use the resolver specified in **MapSignalR**, instead of the default resolver.</span></span>

<span data-ttu-id="566a8-218">Ниже приведен полный листинг кода для `Startup.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="566a8-218">Here is the complete code listing for `Startup.Configuration`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

<span data-ttu-id="566a8-219">Чтобы запустить приложение Стокктиккер в Visual Studio, нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="566a8-219">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="566a8-220">В окне браузера перейдите к `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span><span class="sxs-lookup"><span data-stu-id="566a8-220">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="566a8-221">Приложение имеет точно те же функциональные возможности, что и ранее.</span><span class="sxs-lookup"><span data-stu-id="566a8-221">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="566a8-222">(Описание см. в разделе [серверное вещание с помощью ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) Поведение не изменилось. просто сделать код проще в тестировании, обслуживании и развитии.</span><span class="sxs-lookup"><span data-stu-id="566a8-222">(For a description, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
