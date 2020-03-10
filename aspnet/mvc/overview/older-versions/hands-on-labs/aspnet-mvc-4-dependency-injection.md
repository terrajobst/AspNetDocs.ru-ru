---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: Внедрение зависимостей ASP.NET MVC 4 | Документация Майкрософт
author: rick-anderson
description: Примечание. в этом практическом занятии предполагается, что у вас есть базовые знания о ASP.NET MVC и фильтрах ASP.NET MVC 4. Если вы не использовали фильтры ASP.NET MVC 4 ранее, мы предлагаем...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451824"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="71c0b-104">Внедрение зависимостей в ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="71c0b-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="71c0b-105">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="71c0b-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="71c0b-106">Скачать обучающий комплект Web Camp</span><span class="sxs-lookup"><span data-stu-id="71c0b-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="71c0b-107">В этой практической лабораторной работе предполагается, что у вас есть базовые знания о **ASP.NET MVC** и **фильтрах ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="71c0b-108">Если вы ранее не использовали **фильтры ASP.NET MVC 4** , рекомендуем вам перейти к практическим занятиям по **фильтрам настраиваемых действий ASP.NET MVC** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="71c0b-109">Все примеры кода и фрагментов включены в комплект обучающих курсов Web Camp, доступный в [выпусках Microsoft Web/вебкамптраинингкит](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="71c0b-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="71c0b-110">Проект, относящийся к этой лабораторной работе, доступен по [внедрению зависимостей ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="71c0b-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="71c0b-111">В парадигме **объектно-ориентированного программирования** объекты работают вместе в модели совместной работы, где есть участники и потребители.</span><span class="sxs-lookup"><span data-stu-id="71c0b-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="71c0b-112">Естественно, эта модель взаимодействия создает зависимости между объектами и компонентами, что затрудняет управление при увеличении сложности.</span><span class="sxs-lookup"><span data-stu-id="71c0b-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="71c0b-113">![Зависимости классов и сложность модели](aspnet-mvc-4-dependency-injection/_static/image1.png "Зависимости классов и сложность модели")</span><span class="sxs-lookup"><span data-stu-id="71c0b-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="71c0b-114">*Зависимости классов и сложность модели*</span><span class="sxs-lookup"><span data-stu-id="71c0b-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="71c0b-115">Вероятно, вы слышали о **шаблоне фабрики** и разделении между интерфейсом и реализацией с помощью служб, где клиентские объекты часто отвечают за обнаружение службы.</span><span class="sxs-lookup"><span data-stu-id="71c0b-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="71c0b-116">Шаблон внедрения зависимостей является конкретной реализацией инверсии элемента управления.</span><span class="sxs-lookup"><span data-stu-id="71c0b-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="71c0b-117">**Инверсия управления (IOC)** означает, что объекты не создают другие объекты, от которых зависит работа.</span><span class="sxs-lookup"><span data-stu-id="71c0b-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="71c0b-118">Вместо этого они получают объекты, необходимые для внешнего источника (например, XML-файл конфигурации).</span><span class="sxs-lookup"><span data-stu-id="71c0b-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="71c0b-119">**Внедрение зависимостей (DI)** означает, что это делается без вмешательства объекта, обычно с помощью компонента платформы, который передает параметры конструктора и устанавливает свойства.</span><span class="sxs-lookup"><span data-stu-id="71c0b-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="71c0b-120">Шаблон разработки внедрения зависимостей (DI)</span><span class="sxs-lookup"><span data-stu-id="71c0b-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="71c0b-121">На высоком уровне цель внедрения зависимостей заключается в том, что клиентский класс (например *, элементу гольфа*) должен удовлетворять определенному интерфейсу (например, *иклуб*).</span><span class="sxs-lookup"><span data-stu-id="71c0b-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="71c0b-122">Не имеет значения, какой конкретный тип (например *, вудклуб, иронклуб, веджеклуб* или *путтерклуб*), он хочет, чтобы кто-то другой обработал это (например, хороший *Кадди*).</span><span class="sxs-lookup"><span data-stu-id="71c0b-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="71c0b-123">Сопоставитель зависимостей в ASP.NET MVC позволяет зарегистрировать логику зависимости в другом месте (например, в контейнере или контейнере *треф*).</span><span class="sxs-lookup"><span data-stu-id="71c0b-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="71c0b-124">![Схема внедрения зависимостей](aspnet-mvc-4-dependency-injection/_static/image2.png "Иллюстрация внедрения зависимостей")</span><span class="sxs-lookup"><span data-stu-id="71c0b-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="71c0b-125">*Внедрение зависимостей — аналогия гольфа*</span><span class="sxs-lookup"><span data-stu-id="71c0b-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="71c0b-126">Ниже перечислены преимущества использования шаблона внедрения зависимостей и инверсии управления.</span><span class="sxs-lookup"><span data-stu-id="71c0b-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="71c0b-127">Сокращение взаимосвязей классов</span><span class="sxs-lookup"><span data-stu-id="71c0b-127">Reduces class coupling</span></span>
- <span data-ttu-id="71c0b-128">Увеличение повторного использования кода</span><span class="sxs-lookup"><span data-stu-id="71c0b-128">Increases code reusing</span></span>
- <span data-ttu-id="71c0b-129">Улучшение поддержки кода</span><span class="sxs-lookup"><span data-stu-id="71c0b-129">Improves code maintainability</span></span>
- <span data-ttu-id="71c0b-130">Улучшение тестирования приложений</span><span class="sxs-lookup"><span data-stu-id="71c0b-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="71c0b-131">Внедрение зависимостей иногда сравнивается с абстрактным шаблоном проектирования фабрики, но существует небольшая разница между обоими способами.</span><span class="sxs-lookup"><span data-stu-id="71c0b-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="71c0b-132">В среде внедрения инфраструктура, работающая над разрешениями зависимостей, вызывает фабрики и зарегистрированные службы.</span><span class="sxs-lookup"><span data-stu-id="71c0b-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>

<span data-ttu-id="71c0b-133">Теперь, когда вы понимаете шаблон внедрения зависимостей, вы узнаете в этой лабораторной работе, как применить ее в ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="71c0b-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="71c0b-134">Вы начнете использовать внедрение зависимостей на **контроллерах** для включения службы доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="71c0b-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="71c0b-135">Далее вы примените внедрение зависимостей к **представлениям** для использования службы и отображения информации.</span><span class="sxs-lookup"><span data-stu-id="71c0b-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="71c0b-136">Наконец, вы расширяете модель DI на ASP.NET MVC 4 Filters, добавляя настраиваемый фильтр действий в решение.</span><span class="sxs-lookup"><span data-stu-id="71c0b-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="71c0b-137">В этой практической лабораторной работе вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="71c0b-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="71c0b-138">Интеграция ASP.NET MVC 4 с Unity для внедрения зависимостей с помощью пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="71c0b-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="71c0b-139">Использование внедрения зависимостей в контроллере MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="71c0b-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="71c0b-140">Использование внедрения зависимостей в представлении MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="71c0b-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="71c0b-141">Использовать внедрение зависимостей в фильтре действий MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="71c0b-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="71c0b-142">В этом лабораторном занятии используется пакет NuGet для Unity. Mvc3 для разрешения зависимостей, но можно адаптировать любую инфраструктуру внедрения зависимостей для работы с ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="71c0b-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="71c0b-143">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="71c0b-143">Prerequisites</span></span>

<span data-ttu-id="71c0b-144">Для выполнения этой лабораторной работы необходимо иметь следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="71c0b-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="71c0b-145">[Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или старше (см. [приложение а](#AppendixA) для получения инструкций по его установке).</span><span class="sxs-lookup"><span data-stu-id="71c0b-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="71c0b-146">Настройка</span><span class="sxs-lookup"><span data-stu-id="71c0b-146">Setup</span></span>

<span data-ttu-id="71c0b-147">**Установка фрагментов кода**</span><span class="sxs-lookup"><span data-stu-id="71c0b-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="71c0b-148">Для удобства большая часть кода, который вы будете управлять в этой лаборатории, доступна в виде фрагментов кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71c0b-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="71c0b-149">Чтобы установить фрагменты кода, запустите файл **.\саурце\сетуп\кодесниппетс.ВСИ** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="71c0b-150">Если вы не знакомы с фрагментами кода Visual Studio Code и хотите узнать, как их использовать, можно обратиться к приложению из этого документа &quot;[приложении б. Использование фрагментов кода](#AppendixB)&quot;.</span><span class="sxs-lookup"><span data-stu-id="71c0b-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="71c0b-151">Полнят</span><span class="sxs-lookup"><span data-stu-id="71c0b-151">Exercises</span></span>

<span data-ttu-id="71c0b-152">Эта практическая лабораторная работа состоит из следующих упражнений:</span><span class="sxs-lookup"><span data-stu-id="71c0b-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="71c0b-153">Упражнение 1. Внедрение контроллера</span><span class="sxs-lookup"><span data-stu-id="71c0b-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="71c0b-154">Упражнение 2. Внедрение представления</span><span class="sxs-lookup"><span data-stu-id="71c0b-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="71c0b-155">Упражнение 3. Внедрение фильтров</span><span class="sxs-lookup"><span data-stu-id="71c0b-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="71c0b-156">Каждое упражнение сопровождается **конечной** папкой, содержащей итоговое решение, которое следует получить после завершения упражнений.</span><span class="sxs-lookup"><span data-stu-id="71c0b-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="71c0b-157">Это решение можно использовать в качестве инструкции, если вам нужна дополнительная помощь по работе с упражнениями.</span><span class="sxs-lookup"><span data-stu-id="71c0b-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="71c0b-158">Предполагаемое время выполнения этой лабораторной работы: **30 минут**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="71c0b-159">Упражнение 1. Внедрение контроллера</span><span class="sxs-lookup"><span data-stu-id="71c0b-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="71c0b-160">В этом упражнении вы узнаете, как использовать внедрение зависимостей в контроллерах MVC ASP.NET, интегрируя Unity с помощью пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="71c0b-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="71c0b-161">По этой причине вы включите службы в контроллеры Мвкмусиксторе, чтобы отделить логику от доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="71c0b-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="71c0b-162">Службы будут создавать новую зависимость в конструкторе контроллера, которая будет разрешаться с помощью внедрения зависимостей в справке **Unity**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="71c0b-163">Этот подход показывает, как создавать менее взаимосвязанные приложения, которые являются более гибкими и простыми в обслуживании и тестировании.</span><span class="sxs-lookup"><span data-stu-id="71c0b-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="71c0b-164">Вы также узнаете, как интегрировать ASP.NET MVC с Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="71c0b-165">Сведения о службе Стореманажер</span><span class="sxs-lookup"><span data-stu-id="71c0b-165">About StoreManager Service</span></span>

<span data-ttu-id="71c0b-166">Музыкальное хранилище MVC, предоставленное в начале решения, теперь содержит службу, которая управляет данными контроллера хранилища с именем **сторесервице**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="71c0b-167">Ниже будет обнаружена реализация службы магазина.</span><span class="sxs-lookup"><span data-stu-id="71c0b-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="71c0b-168">Обратите внимание, что все методы возвращают сущности модели.</span><span class="sxs-lookup"><span data-stu-id="71c0b-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="71c0b-169">**Стореконтроллер** из начального решения теперь использует **сторесервице**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="71c0b-170">Все ссылки на данные были удалены из **стореконтроллер**и теперь можно изменить текущий поставщик доступа к данным, не изменяя метод, использующий **сторесервице**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="71c0b-171">Ниже вы увидите, что реализация **стореконтроллер** имеет зависимость с **сторесервице** в конструкторе класса.</span><span class="sxs-lookup"><span data-stu-id="71c0b-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="71c0b-172">Зависимость, представленная в этом упражнении, связана с инверсией **управления** (IOC).</span><span class="sxs-lookup"><span data-stu-id="71c0b-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="71c0b-173">Конструктор класса **стореконтроллер** получает параметр типа **исторесервице** , который необходим для выполнения вызовов служб внутри класса.</span><span class="sxs-lookup"><span data-stu-id="71c0b-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="71c0b-174">Однако **стореконтроллер** не реализует конструктор по умолчанию (без параметров), который необходим любому контроллеру для работы с ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="71c0b-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="71c0b-175">Для разрешения зависимости контроллер должен быть создан абстрактной фабрикой (класс, возвращающий любой объект указанного типа).</span><span class="sxs-lookup"><span data-stu-id="71c0b-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="71c0b-176">При попытке класса создать Стореконтроллер без отправки объекта службы возникнет ошибка, так как конструктор без параметров не объявлен.</span><span class="sxs-lookup"><span data-stu-id="71c0b-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="71c0b-177">Задача 1. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="71c0b-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="71c0b-178">В этой задаче будет запущено приложение Begin, которое включает службу в контроллер хранилища, который отделяет доступ к данным от логики приложения.</span><span class="sxs-lookup"><span data-stu-id="71c0b-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="71c0b-179">При запуске приложения будет получено исключение, так как служба контроллера не передается как параметр по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="71c0b-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="71c0b-180">Откройте **Начальное** решение, расположенное в **Source\Ex01-Injecting контроллер\бегин**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="71c0b-181">Перед продолжением необходимо загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="71c0b-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="71c0b-182">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="71c0b-183">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="71c0b-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="71c0b-184">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="71c0b-185">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="71c0b-186">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="71c0b-187">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="71c0b-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="71c0b-188">Нажмите клавиши **CTRL + F5** , чтобы запустить приложение без отладки.</span><span class="sxs-lookup"><span data-stu-id="71c0b-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="71c0b-189">Вы получите сообщение об ошибке, &quot;**для этого объекта не определен конструктор без параметров** ,&quot;:</span><span class="sxs-lookup"><span data-stu-id="71c0b-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="71c0b-190">![Ошибка при запуске приложения ASP.NET MVC](aspnet-mvc-4-dependency-injection/_static/image3.png "Ошибка при запуске приложения ASP.NET MVC")</span><span class="sxs-lookup"><span data-stu-id="71c0b-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="71c0b-191">*Ошибка при запуске приложения ASP.NET MVC*</span><span class="sxs-lookup"><span data-stu-id="71c0b-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="71c0b-192">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="71c0b-192">Close the browser.</span></span>

<span data-ttu-id="71c0b-193">В следующих шагах вы будете работать с решением "музыкальное хранилище" для внедрения зависимости, необходимого для этого контроллера.</span><span class="sxs-lookup"><span data-stu-id="71c0b-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="71c0b-194">Задача 2. Включение Unity в решение Мвкмусиксторе</span><span class="sxs-lookup"><span data-stu-id="71c0b-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="71c0b-195">В этой задаче в решение будет включен пакет NuGet **Unity. Mvc3** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="71c0b-196">Пакет Unity. Mvc3 был разработан для ASP.NET MVC 3, но полностью совместим с ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="71c0b-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="71c0b-197">Unity — это упрощенный расширяемый контейнер внедрения зависимостей с дополнительной поддержкой перехвата экземпляра и типа.</span><span class="sxs-lookup"><span data-stu-id="71c0b-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="71c0b-198">Это контейнер общего назначения для использования в любом типе приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="71c0b-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="71c0b-199">Он предоставляет все общие функции, доступные в механизме внедрения зависимостей, включая создание объектов, абстракцию требований путем указания зависимостей во время выполнения и гибкость, откладывая конфигурацию компонента на контейнер.</span><span class="sxs-lookup"><span data-stu-id="71c0b-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>

1. <span data-ttu-id="71c0b-200">Установите пакет NuGet **Unity. Mvc3** в проект **мвкмусиксторе** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="71c0b-201">Для этого откройте **консоль диспетчера пакетов** из окна **Просмотр** | **других окон**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="71c0b-202">Выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="71c0b-202">Run the following command.</span></span>

    <span data-ttu-id="71c0b-203">PMC</span><span class="sxs-lookup"><span data-stu-id="71c0b-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="71c0b-204">![Установка пакета NuGet для Unity. Mvc3](aspnet-mvc-4-dependency-injection/_static/image4.png "Установка пакета NuGet для Unity. Mvc3")</span><span class="sxs-lookup"><span data-stu-id="71c0b-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="71c0b-205">*Установка пакета NuGet для Unity. Mvc3*</span><span class="sxs-lookup"><span data-stu-id="71c0b-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="71c0b-206">После установки пакета **Unity. Mvc3** изучите файлы и папки, которые он добавляет автоматически, чтобы упростить настройку Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="71c0b-207">![Установлен пакет Unity. Mvc3](aspnet-mvc-4-dependency-injection/_static/image5.png "Установлен пакет Unity. Mvc3")</span><span class="sxs-lookup"><span data-stu-id="71c0b-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="71c0b-208">*Установлен пакет Unity. Mvc3*</span><span class="sxs-lookup"><span data-stu-id="71c0b-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a><span data-ttu-id="71c0b-209">Задача 3. Регистрация Unity в приложении Global.asax.cs\_запуск</span><span class="sxs-lookup"><span data-stu-id="71c0b-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="71c0b-210">В этой задаче будет обновлен метод **\_запуск приложения** , расположенный в **Global.asax.CS** , чтобы вызвать инициализатор загрузчика Unity, а затем обновить файл загрузчика, регистрирующий службу и контроллер, которые будут использоваться для внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="71c0b-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="71c0b-211">Теперь необходимо подключить загрузчик, который является файлом, который инициализирует контейнер Unity и сопоставитель зависимостей.</span><span class="sxs-lookup"><span data-stu-id="71c0b-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="71c0b-212">Для этого откройте **Global.asax.CS** и добавьте следующий выделенный код в метод **\_запуска приложения** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="71c0b-213">(Фрагмент кода — *Лаборатория внедрения зависимостей ASP.NET-Ex01-Initialize Unity*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="71c0b-214">Откройте файл **bootstrapper.CS** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="71c0b-215">Включите следующие пространства имен: **мвкмусиксторе. Services** и **мусиксторе. Controllers**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="71c0b-216">(Фрагмент кода — *ASP.NET внедрения зависимостей — Ex01 — начальный загрузчик, добавляющий пространства имен*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="71c0b-217">Замените содержимое метода **буилдунитиконтаинер** следующим кодом, который регистрирует контроллер хранилища и службу хранилища.</span><span class="sxs-lookup"><span data-stu-id="71c0b-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="71c0b-218">(Фрагмент кода — *Лаборатория внедрения зависимостей ASP.NET — Ex01 — контроллер и служба регистрации магазина*).</span><span class="sxs-lookup"><span data-stu-id="71c0b-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="71c0b-219">Задача 4. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="71c0b-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="71c0b-220">В этой задаче будет запущено приложение, чтобы убедиться, что теперь его можно загрузить после включения Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="71c0b-221">Нажмите клавишу **F5** для запуска приложения. Теперь приложение должно загружаться без отображения сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="71c0b-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="71c0b-222">![Выполнение приложения с внедрением зависимостей](aspnet-mvc-4-dependency-injection/_static/image6.png "Выполнение приложения с внедрением зависимостей")</span><span class="sxs-lookup"><span data-stu-id="71c0b-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="71c0b-223">*Выполнение приложения с внедрением зависимостей*</span><span class="sxs-lookup"><span data-stu-id="71c0b-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="71c0b-224">Перейдите по **/Store**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-224">Browse to **/Store**.</span></span> <span data-ttu-id="71c0b-225">Это вызовет **стореконтроллер**, который теперь создается с помощью **Unity**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="71c0b-226">![Музыкальное хранилище MVC](aspnet-mvc-4-dependency-injection/_static/image7.png "Музыкальное хранилище MVC")</span><span class="sxs-lookup"><span data-stu-id="71c0b-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="71c0b-227">*Музыкальное хранилище MVC*</span><span class="sxs-lookup"><span data-stu-id="71c0b-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="71c0b-228">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="71c0b-228">Close the browser.</span></span>

<span data-ttu-id="71c0b-229">В следующих упражнениях вы узнаете, как расширить область внедрения зависимостей, чтобы она использовалась внутри ASP.NET представлений MVC и фильтров действий.</span><span class="sxs-lookup"><span data-stu-id="71c0b-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="71c0b-230">Упражнение 2. Внедрение представления</span><span class="sxs-lookup"><span data-stu-id="71c0b-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="71c0b-231">В этом упражнении вы узнаете, как использовать внедрение зависимостей в представлении с новыми функциями ASP.NET MVC 4 для интеграции Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="71c0b-232">Для этого необходимо вызвать пользовательскую службу в представлении обзора магазина, где будет отображаться сообщение и изображение ниже.</span><span class="sxs-lookup"><span data-stu-id="71c0b-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="71c0b-233">Затем вы интегрируете проект с Unity и создаете пользовательский сопоставитель зависимостей для внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="71c0b-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="71c0b-234">Задача 1. Создание представления, использующего службу</span><span class="sxs-lookup"><span data-stu-id="71c0b-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="71c0b-235">В этой задаче будет создано представление, которое выполняет вызов службы для создания новой зависимости.</span><span class="sxs-lookup"><span data-stu-id="71c0b-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="71c0b-236">Служба включает в себя простую службу обмена сообщениями, входящую в это решение.</span><span class="sxs-lookup"><span data-stu-id="71c0b-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="71c0b-237">Откройте **Начальное** решение, расположенное в папке **Source\Ex02-Injecting виев\бегин** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="71c0b-238">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="71c0b-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="71c0b-239">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="71c0b-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="71c0b-240">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="71c0b-241">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="71c0b-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="71c0b-242">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="71c0b-243">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="71c0b-244">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="71c0b-245">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="71c0b-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="71c0b-246">Дополнительные сведения см. в этой статье: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="71c0b-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="71c0b-247">Включите классы **MessageService.CS** и **IMessageService.CS** , расположенные в папке **Source \ассетс** в **/сервицес**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="71c0b-248">Для этого щелкните правой кнопкой мыши папку **службы** и выберите команду **Добавить существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="71c0b-249">Перейдите к расположению файлов и включите их.</span><span class="sxs-lookup"><span data-stu-id="71c0b-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="71c0b-250">![Добавление службы сообщений и интерфейса службы](aspnet-mvc-4-dependency-injection/_static/image8.png "Добавление службы сообщений и интерфейса службы")</span><span class="sxs-lookup"><span data-stu-id="71c0b-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="71c0b-251">*Добавление службы сообщений и интерфейса службы*</span><span class="sxs-lookup"><span data-stu-id="71c0b-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="71c0b-252">Интерфейс **имессажесервице** определяет два свойства, реализуемых классом **мессажесервице** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="71c0b-253">Эти свойства —**Message** и **ImageUrl**— хранят сообщение и URL-адрес отображаемого изображения.</span><span class="sxs-lookup"><span data-stu-id="71c0b-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="71c0b-254">Создайте папку **/pages** в корневой папке проекта, а затем добавьте существующий класс **MyBasePage.CS** из **саурце\ассетс**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="71c0b-255">Базовая страница, от которой будет осуществляться наследование, имеет следующую структуру.</span><span class="sxs-lookup"><span data-stu-id="71c0b-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="71c0b-256">![Папка "страницы"](aspnet-mvc-4-dependency-injection/_static/image9.png "Папка Pages")</span><span class="sxs-lookup"><span data-stu-id="71c0b-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="71c0b-257">Откройте представление **Browse. cshtml** из папки **/виевс/Сторе** и сделайте его производным от **MyBasePage.CS**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="71c0b-258">В представлении **Обзор** добавьте вызов **мессажесервице** , чтобы отобразить изображение и сообщение, полученное службой.</span><span class="sxs-lookup"><span data-stu-id="71c0b-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="71c0b-259">C#</span><span class="sxs-lookup"><span data-stu-id="71c0b-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="71c0b-260">Задача 2. Включение пользовательского сопоставителя зависимостей и активатора страниц пользовательского представления</span><span class="sxs-lookup"><span data-stu-id="71c0b-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="71c0b-261">В предыдущей задаче вы вставили новую зависимость внутри представления для выполнения вызова службы внутри нее.</span><span class="sxs-lookup"><span data-stu-id="71c0b-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="71c0b-262">Теперь вы разрешите эту зависимость, реализовав интерфейсы внедрения зависимостей ASP.NET MVC **ивиевпажеактиватор** и **IDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="71c0b-263">В решение будет включена реализация **IDependencyResolver** , которая будет работать с извлечением службы с помощью Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="71c0b-264">Затем будет включена еще одна пользовательская реализация интерфейса **ивиевпажеактиватор** , позволяющая создавать представления.</span><span class="sxs-lookup"><span data-stu-id="71c0b-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="71c0b-265">Начиная с ASP.NET MVC 3, реализация внедрения зависимостей упростила интерфейсы для регистрации служб.</span><span class="sxs-lookup"><span data-stu-id="71c0b-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="71c0b-266">**IDependencyResolver** и **ивиевпажеактиватор** являются частью функций ASP.NET MVC 3 для внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="71c0b-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="71c0b-267">**-Интерфейс IDependencyResolver** заменяет предыдущий имвксервицелокатор.</span><span class="sxs-lookup"><span data-stu-id="71c0b-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="71c0b-268">Разработчики IDependencyResolver должны возвращать экземпляр службы или коллекции служб.</span><span class="sxs-lookup"><span data-stu-id="71c0b-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="71c0b-269">Интерфейс **ивиевпажеактиватор** обеспечивает более детализированный контроль над созданием экземпляров страниц представления с помощью внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="71c0b-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="71c0b-270">Классы, реализующие интерфейс **ивиевпажеактиватор** , могут создавать экземпляры представления, используя сведения о контексте.</span><span class="sxs-lookup"><span data-stu-id="71c0b-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. <span data-ttu-id="71c0b-271">Создайте папку**фабрики** или в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="71c0b-272">Включите **CustomViewPageActivator.CS** в решение из папки **/саурцес/Ассетс/** to **фабрики** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="71c0b-273">Для этого щелкните правой кнопкой мыши папку **/факториес** и выберите **Добавить | Существующий элемент** , а затем выберите **CustomViewPageActivator.CS**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="71c0b-274">Этот класс реализует интерфейс **ивиевпажеактиватор** для хранения контейнера Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="71c0b-275">**Кустомвиевпажеактиватор** отвечает за управление созданием представления с помощью контейнера Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="71c0b-276">Включить файл **UnityDependencyResolver.CS** из папки **/саурцес/Ассетс** в **/факториес** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="71c0b-277">Для этого щелкните правой кнопкой мыши папку **/факториес** и выберите **Добавить | Существующий элемент** , а затем выберите **UnityDependencyResolver.CS** File.</span><span class="sxs-lookup"><span data-stu-id="71c0b-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="71c0b-278">Класс **унитидепенденциресолвер** является пользовательским Депенденциресолвер для Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="71c0b-279">Если службу не удается найти в контейнере Unity, базовый сопоставитель — инвокатед.</span><span class="sxs-lookup"><span data-stu-id="71c0b-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="71c0b-280">В следующей задаче будут зарегистрированы обе реализации, чтобы модель знала расположение служб и представлений.</span><span class="sxs-lookup"><span data-stu-id="71c0b-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="71c0b-281">Задача 3. Регистрация внедрения зависимостей в контейнере Unity</span><span class="sxs-lookup"><span data-stu-id="71c0b-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="71c0b-282">В этой задаче все предыдущие элементы будут размещены вместе, чтобы сделать внедрение зависимостей.</span><span class="sxs-lookup"><span data-stu-id="71c0b-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="71c0b-283">Теперь решение содержит следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="71c0b-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="71c0b-284">Представление **просмотра** , наследуемое от **мибасекласс** и использующее **мессажесервице**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="71c0b-285">Промежуточный класс-**мибасекласс**, имеющий внедрение зависимостей, объявленное для интерфейса службы.</span><span class="sxs-lookup"><span data-stu-id="71c0b-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="71c0b-286">Служба — **мессажесервице** — и ее интерфейс **имессажесервице**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="71c0b-287">Пользовательский сопоставитель зависимостей для Unity- **унитидепенденциресолвер** , который работает с извлечением служб.</span><span class="sxs-lookup"><span data-stu-id="71c0b-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="71c0b-288">Активатор страницы представления — **кустомвиевпажеактиватор** , который создает страницу.</span><span class="sxs-lookup"><span data-stu-id="71c0b-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="71c0b-289">Чтобы вставить представление " **Обзор** ", теперь можно зарегистрировать пользовательский сопоставитель зависимостей в контейнере Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="71c0b-290">Откройте файл **bootstrapper.CS** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="71c0b-291">Зарегистрируйте экземпляр **мессажесервице** в контейнере Unity для инициализации службы:</span><span class="sxs-lookup"><span data-stu-id="71c0b-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="71c0b-292">(Фрагмент кода — *Лаборатория внедрения зависимостей ASP.NET — Ex02 — регистрация сообщений Service*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="71c0b-293">Добавьте ссылку на пространство имен **мвкмусиксторе. фабрики** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="71c0b-294">(Фрагмент кода — *ASP.NET внедрения зависимостей Lab-Ex02-фабрики*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="71c0b-295">Зарегистрировать **кустомвиевпажеактиватор** в качестве активатора страницы представления в контейнере Unity:</span><span class="sxs-lookup"><span data-stu-id="71c0b-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="71c0b-296">(Фрагмент кода — *Лаборатория внедрения зависимостей ASP.NET — Ex02 — Register кустомвиевпажеактиватор*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="71c0b-297">Замените сопоставитель зависимостей по умолчанию ASP.NET MVC 4 экземпляром **унитидепенденциресолвер**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="71c0b-298">Для этого замените содержимое метода **Initialize** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="71c0b-298">To do this, replace **Initialize** method content with the following code:</span></span>

    <span data-ttu-id="71c0b-299">(Фрагмент кода — *ASP.NET внедрения зависимостей в лаборатории — Ex02 — сопоставитель зависимостей обновления*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="71c0b-300">ASP.NET MVC предоставляет класс сопоставителя зависимостей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="71c0b-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="71c0b-301">Для работы с пользовательскими арбитрами конфликтов, созданными для Unity, этот сопоставитель необходимо заменить.</span><span class="sxs-lookup"><span data-stu-id="71c0b-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="71c0b-302">Задача 4. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="71c0b-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="71c0b-303">В этой задаче будет запущено приложение для проверки того, что обозреватель магазина использует службу и показывает изображение и полученное сообщение:</span><span class="sxs-lookup"><span data-stu-id="71c0b-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="71c0b-304">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="71c0b-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="71c0b-305">Щелкните **рок** в меню жанры и посмотрите, как **мессажесервице** был вставлен в представление и загрузили приветственное сообщение и изображение.</span><span class="sxs-lookup"><span data-stu-id="71c0b-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="71c0b-306">В этом примере мы будем вводить &quot;**рок**&quot;:</span><span class="sxs-lookup"><span data-stu-id="71c0b-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="71c0b-307">![Музыкальное хранилище MVC — введение в представление](aspnet-mvc-4-dependency-injection/_static/image10.png "Музыкальное хранилище MVC — введение в представление")</span><span class="sxs-lookup"><span data-stu-id="71c0b-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="71c0b-308">*Музыкальное хранилище MVC — введение в представление*</span><span class="sxs-lookup"><span data-stu-id="71c0b-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="71c0b-309">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="71c0b-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="71c0b-310">Упражнение 3. Внедрение фильтров действий</span><span class="sxs-lookup"><span data-stu-id="71c0b-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="71c0b-311">В предыдущем практическом занятии **фильтры настраиваемых действий** работали с настройками и внедрением фильтров.</span><span class="sxs-lookup"><span data-stu-id="71c0b-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="71c0b-312">В этом упражнении вы узнаете, как внедрять фильтры с внедрением зависимостей с помощью контейнера Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="71c0b-313">Для этого вы добавите в решение "музыкальное хранилище" настраиваемый фильтр действий, который будет отслеживать активность сайта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="71c0b-314">Задача 1. Включение фильтра отслеживания в решение</span><span class="sxs-lookup"><span data-stu-id="71c0b-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="71c0b-315">В этой задаче вы включите в музыкальное хранилище пользовательский фильтр действий для трассировки событий.</span><span class="sxs-lookup"><span data-stu-id="71c0b-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="71c0b-316">Поскольку основные понятия фильтра действий уже обрабатываются в предыдущей лаборатории &quot;фильтры настраиваемых действий&quot;, вы просто включаете класс Filter из папки Assets этой лабораторной работы, а затем создаете поставщик фильтра для Unity:</span><span class="sxs-lookup"><span data-stu-id="71c0b-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="71c0b-317">Откройте **Начальное** решение, расположенное в папке **Source\Ex03 действие филтер\бегин** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="71c0b-318">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="71c0b-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="71c0b-319">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="71c0b-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="71c0b-320">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="71c0b-321">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="71c0b-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="71c0b-322">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="71c0b-323">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="71c0b-324">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="71c0b-325">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="71c0b-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="71c0b-326">Дополнительные сведения см. в этой статье: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="71c0b-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="71c0b-327">Включить файл **TraceActionFilter.CS** из папки **/саурцес/Ассетс** в **/Филтерс** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="71c0b-328">Этот настраиваемый фильтр действий выполняет трассировку ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="71c0b-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="71c0b-329">Вы можете проверить &quot;ASP.NET MVC 4 локальные и динамические фильтры действий&quot; лабораторию для получения дополнительной справки.</span><span class="sxs-lookup"><span data-stu-id="71c0b-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="71c0b-330">Добавьте пустой класс **FilterProvider.CS** в проект в папке **/Филтерс.**</span><span class="sxs-lookup"><span data-stu-id="71c0b-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="71c0b-331">Добавьте пространства имен **System. Web. MVC** и **Microsoft. Practices. Unity** в **FilterProvider.CS**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="71c0b-332">(Фрагмент кода: *Лаборатория внедрения зависимостей ASP.NET — Ex03 — поставщик фильтра, добавляющий пространства имен*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="71c0b-333">Сделайте класс производным от интерфейса **ифилтерпровидер** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="71c0b-334">Добавьте свойство **иунитиконтаинер** в класс **филтерпровидер** , а затем создайте конструктор класса, чтобы назначить контейнер.</span><span class="sxs-lookup"><span data-stu-id="71c0b-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="71c0b-335">(Фрагмент кода — *ASP.NET внедрения зависимостей — Ex03 — конструктор поставщика фильтра*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="71c0b-336">Конструктор класса фильтра поставщика не создает **Новый** объект внутри.</span><span class="sxs-lookup"><span data-stu-id="71c0b-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="71c0b-337">Контейнер передается в качестве параметра, и зависимость разрешается Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="71c0b-338">В классе **филтерпровидер** реализуйте метод, используя **фильтры** из интерфейса **ифилтерпровидер** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="71c0b-339">(Фрагмент кода: *Лаборатория внедрения зависимостей ASP.NET — Ex03 — фильтры поставщика*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="71c0b-340">Задача 2. Регистрация и включение фильтра</span><span class="sxs-lookup"><span data-stu-id="71c0b-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="71c0b-341">В этой задаче будет включено отслеживание сайта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="71c0b-342">Для этого необходимо зарегистрировать фильтр в методе **bootstrapper.CS буилдунитиконтаинер** , чтобы начать трассировку:</span><span class="sxs-lookup"><span data-stu-id="71c0b-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="71c0b-343">Откройте **файл Web. config** , расположенный в корневом каталоге проекта, и включите отслеживание трассировки в группе System. Web.</span><span class="sxs-lookup"><span data-stu-id="71c0b-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="71c0b-344">Откройте **bootstrapper.CS** в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="71c0b-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="71c0b-345">Добавьте ссылку на пространство имен **мвкмусиксторе. Filters** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="71c0b-346">(Фрагмент кода — *ASP.NET внедрения зависимостей — Ex03 — начальный загрузчик, добавляющий пространства имен*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="71c0b-347">Выберите метод **буилдунитиконтаинер** и зарегистрируйте фильтр в контейнере Unity.</span><span class="sxs-lookup"><span data-stu-id="71c0b-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="71c0b-348">Вам потребуется зарегистрировать поставщик фильтра, а также фильтр действий.</span><span class="sxs-lookup"><span data-stu-id="71c0b-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="71c0b-349">(Фрагмент кода — *Лаборатория внедрения зависимостей ASP.NET — Ex03 — Register филтерпровидер и ActionFilter*)</span><span class="sxs-lookup"><span data-stu-id="71c0b-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="71c0b-350">Задача 3. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="71c0b-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="71c0b-351">В этой задаче будет запущено приложение и выполнена проверка того, что настраиваемый фильтр действий выполняет трассировку действия:</span><span class="sxs-lookup"><span data-stu-id="71c0b-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="71c0b-352">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="71c0b-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="71c0b-353">Щелкните **рок** в меню жанры.</span><span class="sxs-lookup"><span data-stu-id="71c0b-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="71c0b-354">При необходимости можно перейти к дополнительным жанрам.</span><span class="sxs-lookup"><span data-stu-id="71c0b-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="71c0b-355">![Приложение Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Приложение Music Store")</span><span class="sxs-lookup"><span data-stu-id="71c0b-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="71c0b-356">*Приложение Music Store*</span><span class="sxs-lookup"><span data-stu-id="71c0b-356">*Music Store*</span></span>
3. <span data-ttu-id="71c0b-357">Перейдите к **/траце.аксд** , чтобы открыть страницу трассировка приложения, а затем щелкните **Просмотреть сведения**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="71c0b-358">![Журнал трассировки приложения](aspnet-mvc-4-dependency-injection/_static/image12.png "Журнал трассировки приложения")</span><span class="sxs-lookup"><span data-stu-id="71c0b-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="71c0b-359">*Журнал трассировки приложения*</span><span class="sxs-lookup"><span data-stu-id="71c0b-359">*Application Trace Log*</span></span>

    <span data-ttu-id="71c0b-360">![Трассировка приложения — сведения о запросе](aspnet-mvc-4-dependency-injection/_static/image13.png "Трассировка приложения — сведения о запросе")</span><span class="sxs-lookup"><span data-stu-id="71c0b-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="71c0b-361">*Трассировка приложения — сведения о запросе*</span><span class="sxs-lookup"><span data-stu-id="71c0b-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="71c0b-362">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="71c0b-362">Close the browser.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="71c0b-363">Сводка</span><span class="sxs-lookup"><span data-stu-id="71c0b-363">Summary</span></span>

<span data-ttu-id="71c0b-364">Выполнив эту практическое лабораторное занятие, вы узнали, как использовать внедрение зависимостей в ASP.NET MVC 4 путем интеграции Unity с помощью пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="71c0b-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="71c0b-365">Для этого вы использовали внедрение зависимостей внутри контроллеров, представлений и фильтров действий.</span><span class="sxs-lookup"><span data-stu-id="71c0b-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="71c0b-366">Были рассмотрены следующие концепции:</span><span class="sxs-lookup"><span data-stu-id="71c0b-366">The following concepts were covered:</span></span>

- <span data-ttu-id="71c0b-367">Функции внедрения зависимостей ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="71c0b-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="71c0b-368">Интеграция Unity с помощью пакета NuGet для Unity. Mvc3</span><span class="sxs-lookup"><span data-stu-id="71c0b-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="71c0b-369">Внедрение зависимостей в контроллерах</span><span class="sxs-lookup"><span data-stu-id="71c0b-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="71c0b-370">Внедрение зависимостей в представления</span><span class="sxs-lookup"><span data-stu-id="71c0b-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="71c0b-371">Внедрение зависимостей фильтров действий</span><span class="sxs-lookup"><span data-stu-id="71c0b-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="71c0b-372">Приложение а. Установка Visual Studio Express 2012 для Web</span><span class="sxs-lookup"><span data-stu-id="71c0b-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="71c0b-373">Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версии с помощью **[установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="71c0b-374">Следующие инструкции помогут вам выполнить действия, необходимые для установки *Visual Studio Express 2012 для Web* с помощью *установщик веб-платформы Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="71c0b-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="71c0b-375">Перейдите на сайт [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="71c0b-375">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="71c0b-376">Кроме того, если у вас уже установлен установщик веб-платформы, вы можете открыть его и найти продукт &quot;<em>Visual Studio Express 2012 для Web с Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="71c0b-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="71c0b-377">Щелкните **Install Now (установить сейчас**).</span><span class="sxs-lookup"><span data-stu-id="71c0b-377">Click on **Install Now**.</span></span> <span data-ttu-id="71c0b-378">Если у вас нет **установщика веб-платформы** , вы будете сначала перенаправлены на загрузку и установку.</span><span class="sxs-lookup"><span data-stu-id="71c0b-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="71c0b-379">После открытия **установщика веб-платформы** нажмите кнопку **установить** , чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="71c0b-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="71c0b-380">![Установка Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Установка Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="71c0b-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="71c0b-381">*Установка Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="71c0b-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="71c0b-382">Прочитайте все лицензии и условия продуктов и нажмите кнопку " **принять** ", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="71c0b-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Принятие условий лицензии](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="71c0b-384">*Принятие условий лицензии*</span><span class="sxs-lookup"><span data-stu-id="71c0b-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="71c0b-385">Дождитесь завершения процесса загрузки и установки.</span><span class="sxs-lookup"><span data-stu-id="71c0b-385">Wait until the downloading and installation process completes.</span></span>

    ![Ход установки](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="71c0b-387">*Ход установки*</span><span class="sxs-lookup"><span data-stu-id="71c0b-387">*Installation progress*</span></span>
6. <span data-ttu-id="71c0b-388">После завершения установки нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-388">When the installation completes, click **Finish**.</span></span>

    ![Установка завершена](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="71c0b-390">*Установка завершена*</span><span class="sxs-lookup"><span data-stu-id="71c0b-390">*Installation completed*</span></span>
7. <span data-ttu-id="71c0b-391">Нажмите кнопку **выход** , чтобы закрыть установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="71c0b-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="71c0b-392">Чтобы открыть Visual Studio Express для Интернета, перейдите на **начальный** экран и начните запись &quot;**VS Express**&quot;, а затем щелкните плитку **VS Express для Web** .</span><span class="sxs-lookup"><span data-stu-id="71c0b-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Плитка VS Express для Web](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="71c0b-394">*Плитка VS Express для Web*</span><span class="sxs-lookup"><span data-stu-id="71c0b-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="71c0b-395">Приложение б. Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="71c0b-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="71c0b-396">С помощью фрагментов кода вы можете получить все необходимые вам коды.</span><span class="sxs-lookup"><span data-stu-id="71c0b-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="71c0b-397">В лабораторном документе вы узнаете, когда можно использовать их, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="71c0b-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="71c0b-398">![Использование фрагментов кода Visual Studio для вставки кода в проект](aspnet-mvc-4-dependency-injection/_static/image19.png "Использование фрагментов кода Visual Studio для вставки кода в проект")</span><span class="sxs-lookup"><span data-stu-id="71c0b-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="71c0b-399">*Использование фрагментов кода Visual Studio для вставки кода в проект*</span><span class="sxs-lookup"><span data-stu-id="71c0b-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="71c0b-400">***Добавление фрагмента кода с помощью клавиатуры (C# только)***</span><span class="sxs-lookup"><span data-stu-id="71c0b-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="71c0b-401">Поместите курсор в то место, куда вы хотите вставить код.</span><span class="sxs-lookup"><span data-stu-id="71c0b-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="71c0b-402">Начните вводить имя фрагмента (без пробелов или дефисов).</span><span class="sxs-lookup"><span data-stu-id="71c0b-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="71c0b-403">Посмотрите, как IntelliSense отображает соответствующие имена фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="71c0b-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="71c0b-404">Выберите правильный фрагмент кода (или вводите его, пока не будет выбрано имя всего фрагмента).</span><span class="sxs-lookup"><span data-stu-id="71c0b-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="71c0b-405">Дважды нажмите клавишу TAB, чтобы вставить фрагмент в позицию курсора.</span><span class="sxs-lookup"><span data-stu-id="71c0b-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="71c0b-406">![Начните вводить имя фрагмента](aspnet-mvc-4-dependency-injection/_static/image20.png "Начните вводить имя фрагмента")</span><span class="sxs-lookup"><span data-stu-id="71c0b-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="71c0b-407">*Начните вводить имя фрагмента*</span><span class="sxs-lookup"><span data-stu-id="71c0b-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="71c0b-408">![Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.](aspnet-mvc-4-dependency-injection/_static/image21.png "Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="71c0b-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="71c0b-409">*Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="71c0b-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="71c0b-410">![Снова нажмите клавишу TAB, и фрагмент развернется](aspnet-mvc-4-dependency-injection/_static/image22.png "Снова нажмите клавишу TAB, и фрагмент развернется")</span><span class="sxs-lookup"><span data-stu-id="71c0b-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="71c0b-411">*Снова нажмите клавишу TAB, и фрагмент развернется*</span><span class="sxs-lookup"><span data-stu-id="71c0b-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="71c0b-412">***Добавление фрагмента кода с помощью мыши (C#, Visual Basic и XML)*** одного.</span><span class="sxs-lookup"><span data-stu-id="71c0b-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="71c0b-413">Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="71c0b-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="71c0b-414">Выберите **Вставить фрагмент** , за которым следуют **фрагменты кода**.</span><span class="sxs-lookup"><span data-stu-id="71c0b-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="71c0b-415">Выберите соответствующий фрагмент из списка, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="71c0b-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="71c0b-416">![Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.](aspnet-mvc-4-dependency-injection/_static/image23.png "Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="71c0b-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="71c0b-417">*Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="71c0b-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="71c0b-418">![Выберите соответствующий фрагмент из списка, щелкнув его.](aspnet-mvc-4-dependency-injection/_static/image24.png "Выберите соответствующий фрагмент из списка, щелкнув его.")</span><span class="sxs-lookup"><span data-stu-id="71c0b-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="71c0b-419">*Выберите соответствующий фрагмент из списка, щелкнув его.*</span><span class="sxs-lookup"><span data-stu-id="71c0b-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
