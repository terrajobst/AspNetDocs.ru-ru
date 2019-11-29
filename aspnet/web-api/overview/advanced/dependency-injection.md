---
uid: web-api/overview/advanced/dependency-injection
title: Внедрение зависимостей в веб-API ASP.NET 2 — ASP.NET 4. x
author: MikeWasson
description: В этом руководстве показано, как внедрить зависимости в контроллер веб-API ASP.NET для ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600410"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="0692f-103">Внедрение зависимостей в веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="0692f-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="0692f-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0692f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="0692f-105">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="0692f-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="0692f-106">В этом руководстве показано, как внедрить зависимости в контроллер веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0692f-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0692f-107">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="0692f-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0692f-108">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="0692f-108">Web API 2</span></span>
> - [<span data-ttu-id="0692f-109">Блок приложения Unity</span><span class="sxs-lookup"><span data-stu-id="0692f-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="0692f-110">Entity Framework 6 (версия 5 также работает)</span><span class="sxs-lookup"><span data-stu-id="0692f-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="0692f-111">Что такое внедрение зависимостей?</span><span class="sxs-lookup"><span data-stu-id="0692f-111">What is Dependency Injection?</span></span>

<span data-ttu-id="0692f-112">*Зависимость* — это любой объект, который требуется другому объекту.</span><span class="sxs-lookup"><span data-stu-id="0692f-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="0692f-113">Например, вы обычно определяете [репозиторий](http://martinfowler.com/eaaCatalog/repository.html) , который обрабатывает доступ к данным.</span><span class="sxs-lookup"><span data-stu-id="0692f-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="0692f-114">Давайте продемонстрируем пример.</span><span class="sxs-lookup"><span data-stu-id="0692f-114">Let's illustrate with an example.</span></span> <span data-ttu-id="0692f-115">Сначала мы определим модель предметной области:</span><span class="sxs-lookup"><span data-stu-id="0692f-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="0692f-116">Ниже приведен простой класс репозитория, в котором хранятся элементы в базе данных с помощью Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="0692f-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="0692f-117">Теперь определим контроллер веб-API, который поддерживает запросы GET для сущностей `Product`.</span><span class="sxs-lookup"><span data-stu-id="0692f-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="0692f-118">(Я не использую POST и другие методы для простоты.) Вот первая предпринятая ошибка:</span><span class="sxs-lookup"><span data-stu-id="0692f-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="0692f-119">Обратите внимание, что класс Controller зависит от `ProductRepository`, и мы разрешив контроллеру создавать экземпляр `ProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="0692f-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="0692f-120">Тем не менее, неплохой смысл жестко запрограммировать зависимость таким образом, по нескольким причинам.</span><span class="sxs-lookup"><span data-stu-id="0692f-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="0692f-121">Если требуется заменить `ProductRepository` другой реализацией, необходимо также изменить класс контроллера.</span><span class="sxs-lookup"><span data-stu-id="0692f-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="0692f-122">Если `ProductRepository` имеет зависимости, их необходимо настроить внутри контроллера.</span><span class="sxs-lookup"><span data-stu-id="0692f-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="0692f-123">Для большого проекта с несколькими контроллерами код конфигурации преобразуется в несколько проектов.</span><span class="sxs-lookup"><span data-stu-id="0692f-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="0692f-124">Трудно тестировать модульный тест, так как контроллер жестко закодирован для запроса базы данных.</span><span class="sxs-lookup"><span data-stu-id="0692f-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="0692f-125">Для модульного теста следует использовать репозиторий или заглушку, что невозможно с текущим дизайном.</span><span class="sxs-lookup"><span data-stu-id="0692f-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="0692f-126">Эти проблемы можно решить, *внедряя* репозиторий в контроллер.</span><span class="sxs-lookup"><span data-stu-id="0692f-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="0692f-127">Сначала выполните рефакторинг класса `ProductRepository` в интерфейсе:</span><span class="sxs-lookup"><span data-stu-id="0692f-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="0692f-128">Затем укажите `IProductRepository` в качестве параметра конструктора:</span><span class="sxs-lookup"><span data-stu-id="0692f-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="0692f-129">В этом примере используется [внедрение конструктора](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="0692f-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="0692f-130">Можно также использовать *внедрение метода задания*, где зависимость задается через метод задания или свойство.</span><span class="sxs-lookup"><span data-stu-id="0692f-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="0692f-131">Но теперь возникла проблема, так как приложение не создает контроллер напрямую.</span><span class="sxs-lookup"><span data-stu-id="0692f-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="0692f-132">Веб-API создает контроллер при маршрутизации запроса, и веб-API не знает о `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="0692f-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="0692f-133">Именно здесь поступает сопоставитель зависимостей веб-API.</span><span class="sxs-lookup"><span data-stu-id="0692f-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="0692f-134">Сопоставитель зависимостей веб-API</span><span class="sxs-lookup"><span data-stu-id="0692f-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="0692f-135">Веб-API определяет интерфейс **IDependencyResolver** для разрешения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="0692f-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="0692f-136">Ниже приведено определение интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0692f-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="0692f-137">Интерфейс **идепенденцископе** имеет два метода:</span><span class="sxs-lookup"><span data-stu-id="0692f-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="0692f-138">**Служба "услуга** " создает один экземпляр типа.</span><span class="sxs-lookup"><span data-stu-id="0692f-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="0692f-139">**Службы** создают коллекцию объектов указанного типа.</span><span class="sxs-lookup"><span data-stu-id="0692f-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="0692f-140">Метод **IDependencyResolver** наследует **идепенденцископе** и добавляет метод **бегинскопе** .</span><span class="sxs-lookup"><span data-stu-id="0692f-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="0692f-141">Далее в этом руководстве я расскажу об областях.</span><span class="sxs-lookup"><span data-stu-id="0692f-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="0692f-142">Когда веб-API создает экземпляр контроллера, он сначала вызывает **IDependencyResolver.-Service**, передавая ему тип контроллера.</span><span class="sxs-lookup"><span data-stu-id="0692f-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="0692f-143">С помощью этого обработчика расширяемости можно создать контроллер, разрешающий все зависимости.</span><span class="sxs-lookup"><span data-stu-id="0692f-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="0692f-144">Если функция " **услуга** " возвращает значение null, веб-API ищет конструктор без параметров в классе Controller.</span><span class="sxs-lookup"><span data-stu-id="0692f-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="0692f-145">Разрешение зависимостей с помощью контейнера Unity</span><span class="sxs-lookup"><span data-stu-id="0692f-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="0692f-146">Несмотря на то, что можно написать полную реализацию **IDependencyResolver** с нуля, интерфейс на самом деле спроектирован так, что он выступает в роли моста между веб-API и существующими контейнерами IOC.</span><span class="sxs-lookup"><span data-stu-id="0692f-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="0692f-147">Контейнер IoC — это программный компонент, отвечающий за управление зависимостями.</span><span class="sxs-lookup"><span data-stu-id="0692f-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="0692f-148">Вы регистрируете типы в контейнере, а затем используете контейнер для создания объектов.</span><span class="sxs-lookup"><span data-stu-id="0692f-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="0692f-149">Контейнер автоматически определяет отношения зависимости.</span><span class="sxs-lookup"><span data-stu-id="0692f-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="0692f-150">Многие контейнеры IoC также позволяют контролировать время существования и области действия объекта.</span><span class="sxs-lookup"><span data-stu-id="0692f-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="0692f-151">"IoC" означает "инверсия управления", которая представляет собой общий шаблон, в котором инфраструктура вызывает код приложения.</span><span class="sxs-lookup"><span data-stu-id="0692f-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="0692f-152">Контейнер IoC конструирует ваши объекты, что «инвертирует» обычный поток управления.</span><span class="sxs-lookup"><span data-stu-id="0692f-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="0692f-153">В рамках этого руководства мы будем использовать [Unity](https://msdn.microsoft.com/library/ff647202.aspx) из шаблонов Майкрософт &amp; методик.</span><span class="sxs-lookup"><span data-stu-id="0692f-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="0692f-154">(Другие популярные библиотеки включают [Castle Windsor](http://www.castleproject.org/), [Spring.NET](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [нинжект](http://www.ninject.org/)и [StructureMap](http://structuremap.github.io/documentation/).) Для установки Unity можно использовать диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="0692f-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="0692f-155">В меню **Сервис** в Visual Studio выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="0692f-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="0692f-156">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0692f-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="0692f-157">Ниже приведена реализация **IDependencyResolver** , которая заключает в оболочку контейнер Unity.</span><span class="sxs-lookup"><span data-stu-id="0692f-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="0692f-158">Если методу метода **WebService** не удается разрешить тип, он должен вернуть **значение NULL**.</span><span class="sxs-lookup"><span data-stu-id="0692f-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="0692f-159">Если **методу** GetObject не удается разрешить тип, он должен возвращать пустой объект коллекции.</span><span class="sxs-lookup"><span data-stu-id="0692f-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="0692f-160">Не вызывайте исключения для неизвестных типов.</span><span class="sxs-lookup"><span data-stu-id="0692f-160">Don't throw exceptions for unknown types.</span></span>

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="0692f-161">Настройка сопоставителя зависимостей</span><span class="sxs-lookup"><span data-stu-id="0692f-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="0692f-162">Установите сопоставитель зависимостей в свойстве **депенденциресолвер** глобального объекта **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="0692f-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="0692f-163">Следующий код регистрирует интерфейс `IProductRepository` с помощью Unity, а затем создает `UnityResolver`.</span><span class="sxs-lookup"><span data-stu-id="0692f-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="0692f-164">Область зависимости и время существования контроллера</span><span class="sxs-lookup"><span data-stu-id="0692f-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="0692f-165">Контроллеры создаются для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="0692f-165">Controllers are created per request.</span></span> <span data-ttu-id="0692f-166">Для управления жизненным циклом объекта **IDependencyResolver** использует концепцию *области*.</span><span class="sxs-lookup"><span data-stu-id="0692f-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="0692f-167">Сопоставитель зависимостей, присоединенный к объекту **HttpConfiguration** , имеет глобальную область видимости.</span><span class="sxs-lookup"><span data-stu-id="0692f-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="0692f-168">Когда веб-API создает контроллер, он вызывает **бегинскопе**.</span><span class="sxs-lookup"><span data-stu-id="0692f-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="0692f-169">Этот метод возвращает объект **идепенденцископе** , представляющий дочернюю область.</span><span class="sxs-lookup"><span data-stu-id="0692f-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="0692f-170">Затем веб-API вызывает метод **WebService** для дочерней области, чтобы создать контроллер.</span><span class="sxs-lookup"><span data-stu-id="0692f-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="0692f-171">По завершении запроса веб-API вызывает **Dispose** для дочерней области.</span><span class="sxs-lookup"><span data-stu-id="0692f-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="0692f-172">Используйте метод **Dispose** для удаления зависимостей контроллера.</span><span class="sxs-lookup"><span data-stu-id="0692f-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="0692f-173">Реализация **бегинскопе** зависит от контейнера IoC.</span><span class="sxs-lookup"><span data-stu-id="0692f-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="0692f-174">Для Unity область соответствует дочернему контейнеру:</span><span class="sxs-lookup"><span data-stu-id="0692f-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="0692f-175">Большинство контейнеров IoC имеют аналогичные эквиваленты.</span><span class="sxs-lookup"><span data-stu-id="0692f-175">Most IoC containers have similar equivalents.</span></span>
