---
uid: web-api/overview/advanced/dependency-injection
title: Внедрение зависимостей в ASP.NET Web API 2 — ASP.NET 4.x
author: MikeWasson
description: Этом руководстве показано, как внедрить зависимости в контроллере веб-API ASP.NET для ASP.NET 4.x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 138ccb5800e801d382c11e3989ec3e3c074a79fe
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115705"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="b2f51-103">Внедрение зависимостей в ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="b2f51-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="b2f51-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b2f51-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b2f51-105">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="b2f51-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="b2f51-106">Этом руководстве показано, как внедрить зависимости в контроллере веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b2f51-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b2f51-107">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="b2f51-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b2f51-108">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="b2f51-108">Web API 2</span></span>
> - [<span data-ttu-id="b2f51-109">Unity Application Block</span><span class="sxs-lookup"><span data-stu-id="b2f51-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="b2f51-110">Entity Framework 6 (версии 5 также работает)</span><span class="sxs-lookup"><span data-stu-id="b2f51-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="b2f51-111">Что такое внедрение зависимостей?</span><span class="sxs-lookup"><span data-stu-id="b2f51-111">What is Dependency Injection?</span></span>

<span data-ttu-id="b2f51-112">*Зависимость* — это любой объект, который требуется другому объекту.</span><span class="sxs-lookup"><span data-stu-id="b2f51-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="b2f51-113">Например, довольно часто для определения [репозитория](http://martinfowler.com/eaaCatalog/repository.html) , служащий для обработки доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="b2f51-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="b2f51-114">Давайте рассмотрим пример.</span><span class="sxs-lookup"><span data-stu-id="b2f51-114">Let's illustrate with an example.</span></span> <span data-ttu-id="b2f51-115">Во-первых мы определим модель предметной области:</span><span class="sxs-lookup"><span data-stu-id="b2f51-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="b2f51-116">Ниже приведен простой репозиторий класс, который хранит элементы в базе данных, использующий Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="b2f51-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="b2f51-117">Теперь давайте определим контроллер веб-API, который поддерживает запросы GET для `Product` сущностей.</span><span class="sxs-lookup"><span data-stu-id="b2f51-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="b2f51-118">(Я пропускают POST и другие методы для простоты.) Ниже приведен первой попытки.</span><span class="sxs-lookup"><span data-stu-id="b2f51-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="b2f51-119">Обратите внимание, что зависит от класса контроллера `ProductRepository`, и мы сообщаем создать контроллер `ProductRepository` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b2f51-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="b2f51-120">Тем не менее рекомендуется явно указывать зависимость таким образом, это по следующим причинам.</span><span class="sxs-lookup"><span data-stu-id="b2f51-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="b2f51-121">Если вы хотите заменить `ProductRepository` другой реализацией, необходимо также изменить класс контроллера.</span><span class="sxs-lookup"><span data-stu-id="b2f51-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="b2f51-122">Если `ProductRepository` имеет зависимости, их необходимо настроить в контроллере.</span><span class="sxs-lookup"><span data-stu-id="b2f51-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="b2f51-123">Для большого проекта с несколькими контроллерами код конфигурации становится разбиты на проект.</span><span class="sxs-lookup"><span data-stu-id="b2f51-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="b2f51-124">Трудно модульного теста, так как контроллер, жестко заданные для запроса базы данных.</span><span class="sxs-lookup"><span data-stu-id="b2f51-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="b2f51-125">Для модульного теста следует использовать репозитории макет или заглушки, что не поддерживается в текущей архитектуре.</span><span class="sxs-lookup"><span data-stu-id="b2f51-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="b2f51-126">Можно устранить эти проблемы путем *внедрение* репозитория в контроллер.</span><span class="sxs-lookup"><span data-stu-id="b2f51-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="b2f51-127">Во-первых, рефакторинг `ProductRepository` класс в интерфейсе:</span><span class="sxs-lookup"><span data-stu-id="b2f51-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="b2f51-128">Затем укажите `IProductRepository` качестве параметра конструктора:</span><span class="sxs-lookup"><span data-stu-id="b2f51-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="b2f51-129">В этом примере используется [внедрение через конструктор](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="b2f51-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="b2f51-130">Можно также использовать *внедрения setter*, где можно устанавливать для зависимости через метод или свойство.</span><span class="sxs-lookup"><span data-stu-id="b2f51-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="b2f51-131">Но теперь имеется проблема, поскольку приложение не создает контроллер напрямую.</span><span class="sxs-lookup"><span data-stu-id="b2f51-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="b2f51-132">Веб-API создает контроллер, когда он направляет запрос и веб-API не знает ничего о `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="b2f51-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="b2f51-133">Это, когда вступает в дело в сопоставителе зависимостей веб-API.</span><span class="sxs-lookup"><span data-stu-id="b2f51-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="b2f51-134">Сопоставитель зависимостей веб-API</span><span class="sxs-lookup"><span data-stu-id="b2f51-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="b2f51-135">Веб-API определяет **IDependencyResolver** интерфейс для разрешения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b2f51-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="b2f51-136">Вот определение интерфейса:</span><span class="sxs-lookup"><span data-stu-id="b2f51-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="b2f51-137">**IDependencyScope** интерфейс содержит два метода:</span><span class="sxs-lookup"><span data-stu-id="b2f51-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="b2f51-138">**GetService** создает один экземпляр типа.</span><span class="sxs-lookup"><span data-stu-id="b2f51-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="b2f51-139">**GetServices** создает коллекцию объектов указанного типа.</span><span class="sxs-lookup"><span data-stu-id="b2f51-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="b2f51-140">**IDependencyResolver** наследует метод **IDependencyScope** и добавляет **BeginScope** метод.</span><span class="sxs-lookup"><span data-stu-id="b2f51-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="b2f51-141">Я расскажу об областях далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b2f51-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="b2f51-142">Когда веб-API создает экземпляр контроллера, в первую очередь вызывает **IDependencyResolver.GetService**, передав тип контроллера.</span><span class="sxs-lookup"><span data-stu-id="b2f51-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="b2f51-143">Этот обработчик расширяемости можно использовать для создания контроллера, разрешение всех зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b2f51-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="b2f51-144">Если **GetService** возвращает значение null, ищет конструктор класса контроллера в веб-API.</span><span class="sxs-lookup"><span data-stu-id="b2f51-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="b2f51-145">Разрешение зависимостей для контейнера Unity</span><span class="sxs-lookup"><span data-stu-id="b2f51-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="b2f51-146">Несмотря на то, что можно написать полное **IDependencyResolver** реализация с нуля, интерфейс действительно предназначена для работы в качестве моста между веб-API и существующие контейнеры IoC.</span><span class="sxs-lookup"><span data-stu-id="b2f51-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="b2f51-147">IoC-контейнер — это программный компонент, который отвечает за управление зависимостями.</span><span class="sxs-lookup"><span data-stu-id="b2f51-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="b2f51-148">Зарегистрируйте типов в контейнере и затем использовать для создания объектов контейнера.</span><span class="sxs-lookup"><span data-stu-id="b2f51-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="b2f51-149">Контейнер автоматически определяет отношение зависимость.</span><span class="sxs-lookup"><span data-stu-id="b2f51-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="b2f51-150">Кроме того, множество контейнеров инверсии управления позволяют управлять времени существования объектов и области.</span><span class="sxs-lookup"><span data-stu-id="b2f51-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="b2f51-151">«IoC» означает «инверсии элемента управления», который является общий шаблон, когда платформа вызывает в код приложения.</span><span class="sxs-lookup"><span data-stu-id="b2f51-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="b2f51-152">Контейнер IoC создает объектов, который «инвертирует» обычного потока управления.</span><span class="sxs-lookup"><span data-stu-id="b2f51-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="b2f51-153">В этом учебнике мы будем использовать [Unity](https://msdn.microsoft.com/library/ff647202.aspx) из Microsoft Patterns &amp; рекомендации.</span><span class="sxs-lookup"><span data-stu-id="b2f51-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="b2f51-154">(Включить других популярных библиотек [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), и [StructureMap ](http://structuremap.github.io/documentation/).) Можно использовать диспетчер пакетов NuGet для установки Unity.</span><span class="sxs-lookup"><span data-stu-id="b2f51-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="b2f51-155">Из **средства** меню в Visual Studio, выберите пункт **диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="b2f51-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b2f51-156">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b2f51-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="b2f51-157">Вот реализация **IDependencyResolver** , который служит оболочкой контейнера Unity.</span><span class="sxs-lookup"><span data-stu-id="b2f51-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="b2f51-158">Если **GetService** метод не может разрешить тип, он должен вернуть **null**.</span><span class="sxs-lookup"><span data-stu-id="b2f51-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="b2f51-159">Если **GetServices** метод не может разрешить тип, она должна возвращать пустой объект коллекции.</span><span class="sxs-lookup"><span data-stu-id="b2f51-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="b2f51-160">Не создают исключения для неизвестных типов.</span><span class="sxs-lookup"><span data-stu-id="b2f51-160">Don't throw exceptions for unknown types.</span></span>

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="b2f51-161">Настройка сопоставителя зависимостей</span><span class="sxs-lookup"><span data-stu-id="b2f51-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="b2f51-162">Установите средство разрешения зависимостей на **DependencyResolver** свойства глобального **HttpConfiguration** объекта.</span><span class="sxs-lookup"><span data-stu-id="b2f51-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="b2f51-163">В следующем коде регистрах `IProductRepository` интерфейса с помощью Unity, а затем создает `UnityResolver`.</span><span class="sxs-lookup"><span data-stu-id="b2f51-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="b2f51-164">Область зависимостей и временем существования контроллера</span><span class="sxs-lookup"><span data-stu-id="b2f51-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="b2f51-165">Контроллеры создаются отдельно для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="b2f51-165">Controllers are created per request.</span></span> <span data-ttu-id="b2f51-166">Для управления временем существования объектов, **IDependencyResolver** использует концепцию *область*.</span><span class="sxs-lookup"><span data-stu-id="b2f51-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="b2f51-167">Сопоставитель зависимостей подключен к **HttpConfiguration** объект имеет глобальную область.</span><span class="sxs-lookup"><span data-stu-id="b2f51-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="b2f51-168">Когда веб-API создает контроллер, он вызывает **BeginScope**.</span><span class="sxs-lookup"><span data-stu-id="b2f51-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="b2f51-169">Этот метод возвращает **IDependencyScope** , представляющий дочерней области.</span><span class="sxs-lookup"><span data-stu-id="b2f51-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="b2f51-170">Веб-API, затем вызывает **GetService** в дочерней области для создания контроллера.</span><span class="sxs-lookup"><span data-stu-id="b2f51-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="b2f51-171">По завершении запроса вызывает веб-API **Dispose** в дочерней области.</span><span class="sxs-lookup"><span data-stu-id="b2f51-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="b2f51-172">Используйте **Dispose** метод для удаления зависимостей контроллера.</span><span class="sxs-lookup"><span data-stu-id="b2f51-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="b2f51-173">Как реализовать **BeginScope** зависит от контейнера IoC.</span><span class="sxs-lookup"><span data-stu-id="b2f51-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="b2f51-174">Для Unity область соответствует в дочернем контейнере:</span><span class="sxs-lookup"><span data-stu-id="b2f51-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="b2f51-175">Большинство IoC-контейнеры имеют аналогичные эквиваленты.</span><span class="sxs-lookup"><span data-stu-id="b2f51-175">Most IoC containers have similar equivalents.</span></span>
