---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: Фильтры настраиваемых действий ASP.NET MVC 4 | Документация Майкрософт
author: rick-anderson
description: ASP.NET MVC предоставляет фильтры действий для выполнения логики фильтрации либо до, либо после вызова метода действия. Фильтры действий являются пользовательскими атрибутами Tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468180"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="e1cca-104">Фильтры настраиваемых действий в ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="e1cca-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="e1cca-105">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="e1cca-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="e1cca-106">Скачать обучающий комплект Web Camp</span><span class="sxs-lookup"><span data-stu-id="e1cca-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="e1cca-107">ASP.NET MVC предоставляет фильтры действий для выполнения логики фильтрации либо до, либо после вызова метода действия.</span><span class="sxs-lookup"><span data-stu-id="e1cca-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="e1cca-108">Фильтры действий — это настраиваемые атрибуты, которые предоставляют декларативные средства для добавления поведения действий, выполняемых перед действием и после действия, в методы действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="e1cca-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="e1cca-109">В этой практической лабораторной работе вы создадите настраиваемый атрибут фильтра действий в решении Мвкмусиксторе для перехвата запросов контроллера и регистрации активности сайта в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="e1cca-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="e1cca-110">Вы сможете добавить фильтр ведения журнала путем внедрения в любой контроллер или действие.</span><span class="sxs-lookup"><span data-stu-id="e1cca-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="e1cca-111">Наконец, вы увидите представление журнала, в котором отображается список посетителей.</span><span class="sxs-lookup"><span data-stu-id="e1cca-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="e1cca-112">В этой практической лабораторной работе предполагается, что у вас есть базовые знания о **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="e1cca-113">Если вы ранее не использовали **ASP.NET MVC** , мы рекомендуем вам перейти на практический семинар **ASP.NET MVC 4** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="e1cca-114">Все примеры кода и фрагментов включены в комплект обучающих курсов Web Camp, доступный в [выпусках Microsoft Web/вебкамптраинингкит](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="e1cca-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="e1cca-115">Проект, относящийся к этой лабораторной работе, доступен по [настраиваемым фильтрам действий ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span><span class="sxs-lookup"><span data-stu-id="e1cca-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="e1cca-116">Цели</span><span class="sxs-lookup"><span data-stu-id="e1cca-116">Objectives</span></span>

<span data-ttu-id="e1cca-117">В этой практической лабораторной работе вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e1cca-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="e1cca-118">Создание атрибута настраиваемого фильтра действий для расширения возможностей фильтрации</span><span class="sxs-lookup"><span data-stu-id="e1cca-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="e1cca-119">Применение настраиваемого атрибута фильтра путем внедрения к определенному уровню</span><span class="sxs-lookup"><span data-stu-id="e1cca-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="e1cca-120">Глобально зарегистрировать фильтры настраиваемых действий</span><span class="sxs-lookup"><span data-stu-id="e1cca-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="e1cca-121">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e1cca-121">Prerequisites</span></span>

<span data-ttu-id="e1cca-122">Для выполнения этой лабораторной работы необходимо иметь следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="e1cca-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="e1cca-123">[Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или старше (см. [приложение а](#AppendixA) для получения инструкций по его установке).</span><span class="sxs-lookup"><span data-stu-id="e1cca-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="e1cca-124">Настройка</span><span class="sxs-lookup"><span data-stu-id="e1cca-124">Setup</span></span>

<span data-ttu-id="e1cca-125">**Установка фрагментов кода**</span><span class="sxs-lookup"><span data-stu-id="e1cca-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="e1cca-126">Для удобства большая часть кода, который вы будете управлять в этой лаборатории, доступна в виде фрагментов кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1cca-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="e1cca-127">Чтобы установить фрагменты кода, запустите файл **.\саурце\сетуп\кодесниппетс.ВСИ** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="e1cca-128">Если вы не знакомы с фрагментами кода Visual Studio Code и хотите узнать, как их использовать, см. приложение в этом документе &quot;[приложении C: использование фрагментов кода](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="e1cca-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="e1cca-129">Полнят</span><span class="sxs-lookup"><span data-stu-id="e1cca-129">Exercises</span></span>

<span data-ttu-id="e1cca-130">Эта практическая лабораторная работа состоит из следующих упражнений:</span><span class="sxs-lookup"><span data-stu-id="e1cca-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="e1cca-131">Упражнение 1. действия ведения журнала</span><span class="sxs-lookup"><span data-stu-id="e1cca-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="e1cca-132">Упражнение 2. Управление несколькими фильтрами действий</span><span class="sxs-lookup"><span data-stu-id="e1cca-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="e1cca-133">Предполагаемое время выполнения этой лабораторной работы: **30 минут**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="e1cca-134">Каждое упражнение сопровождается **конечной** папкой, содержащей итоговое решение, которое следует получить после завершения упражнений.</span><span class="sxs-lookup"><span data-stu-id="e1cca-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="e1cca-135">Это решение можно использовать в качестве инструкции, если вам нужна дополнительная помощь по работе с упражнениями.</span><span class="sxs-lookup"><span data-stu-id="e1cca-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="e1cca-136">Упражнение 1. действия ведения журнала</span><span class="sxs-lookup"><span data-stu-id="e1cca-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="e1cca-137">В этом упражнении вы узнаете, как создать настраиваемый фильтр журнала действий с помощью поставщиков фильтров ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="e1cca-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="e1cca-138">Для этой цели вы примените фильтр ведения журнала к сайту Мусиксторе, который будет записывать все действия в выбранных контроллерах.</span><span class="sxs-lookup"><span data-stu-id="e1cca-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="e1cca-139">Фильтр расширяет **актионфилтераттрибутекласс** и переопределяет метод **OnActionExecuting** для перехвата каждого запроса, а затем выполняет действия по ведению журнала.</span><span class="sxs-lookup"><span data-stu-id="e1cca-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="e1cca-140">Контекстные сведения о HTTP-запросах, методах, результатах и параметрах будут предоставлены классом ASP.NET MVC **ActionExecutingContext** **.**</span><span class="sxs-lookup"><span data-stu-id="e1cca-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="e1cca-141">В ASP.NET MVC 4 также есть поставщики фильтров по умолчанию, которые можно использовать без создания настраиваемого фильтра.</span><span class="sxs-lookup"><span data-stu-id="e1cca-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="e1cca-142">ASP.NET MVC 4 предоставляет следующие типы фильтров:</span><span class="sxs-lookup"><span data-stu-id="e1cca-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="e1cca-143">Фильтр **авторизации** , позволяющий принимать решения по безопасности о том, следует ли выполнять метод действия, например выполнять проверку подлинности или проверять свойства запроса.</span><span class="sxs-lookup"><span data-stu-id="e1cca-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="e1cca-144">Фильтр **действий** , который служит оболочкой для выполнения метода действия.</span><span class="sxs-lookup"><span data-stu-id="e1cca-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="e1cca-145">Этот фильтр может выполнять дополнительную обработку, например предоставление дополнительных данных для метода действия, проверку возвращаемого значения или Отмена выполнения метода действия.</span><span class="sxs-lookup"><span data-stu-id="e1cca-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="e1cca-146">Фильтр **результатов** , который служит оболочкой для выполнения объекта ActionResult.</span><span class="sxs-lookup"><span data-stu-id="e1cca-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="e1cca-147">Этот фильтр может выполнять дополнительную обработку результата, например изменение HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="e1cca-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="e1cca-148">Фильтр **исключений** , который выполняется при возникновении необработанного исключения в методе действия, начиная с фильтров авторизации и заканчивая выполнением результата.</span><span class="sxs-lookup"><span data-stu-id="e1cca-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="e1cca-149">Фильтры исключений можно использовать для ведения журнала или для отображения страниц об ошибках.</span><span class="sxs-lookup"><span data-stu-id="e1cca-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="e1cca-150">Дополнительные сведения о поставщиках фильтров см. по этой ссылке MSDN: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)).</span><span class="sxs-lookup"><span data-stu-id="e1cca-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="e1cca-151">О функции ведения журнала приложения музыкального магазина MVC</span><span class="sxs-lookup"><span data-stu-id="e1cca-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="e1cca-152">В этом решении музыкального магазина имеется новая таблица модели данных для ведения журнала сайта **актионлог**со следующими полями: имя контроллера, получившего запрос, называемый действием, IP-адрес клиента и отметка времени.</span><span class="sxs-lookup"><span data-stu-id="e1cca-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="e1cca-153">![Модель данных. Таблица Актионлог.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Модель данных. Таблица Актионлог.")</span><span class="sxs-lookup"><span data-stu-id="e1cca-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="e1cca-154">*Модель данных — таблица Актионлог*</span><span class="sxs-lookup"><span data-stu-id="e1cca-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="e1cca-155">Решение предоставляет представление MVC ASP.NET для журнала действий, которое можно найти по адресу **мвкмусиксторес/views/актионлог**:</span><span class="sxs-lookup"><span data-stu-id="e1cca-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="e1cca-156">![Представление журнала действий](aspnet-mvc-4-custom-action-filters/_static/image2.png "Представление журнала действий")</span><span class="sxs-lookup"><span data-stu-id="e1cca-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="e1cca-157">*Представление журнала действий*</span><span class="sxs-lookup"><span data-stu-id="e1cca-157">*Action Log view*</span></span>

<span data-ttu-id="e1cca-158">Учитывая эту структуру, вся работа будет сосредоточена на запросе контроллера прерывания и выполнении ведения журнала с помощью пользовательской фильтрации.</span><span class="sxs-lookup"><span data-stu-id="e1cca-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="e1cca-159">Задача 1. Создание настраиваемого фильтра для перехвата запроса контроллера</span><span class="sxs-lookup"><span data-stu-id="e1cca-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="e1cca-160">В этой задаче будет создан класс настраиваемого атрибута фильтра, который будет содержать логику ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="e1cca-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="e1cca-161">Для этой цели будет расширен класс ASP.NET MVC **ActionFilterAttribute** и реализован интерфейс **иактионфилтер**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="e1cca-162">**ActionFilterAttribute** является базовым классом для всех фильтров атрибутов.</span><span class="sxs-lookup"><span data-stu-id="e1cca-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="e1cca-163">Он предоставляет следующие методы для выполнения определенной логики после и до выполнения действия контроллера:</span><span class="sxs-lookup"><span data-stu-id="e1cca-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="e1cca-164">**OnActionExecuting**(ActionExecutingContext филтерконтекст): непосредственно перед вызовом метода действия.</span><span class="sxs-lookup"><span data-stu-id="e1cca-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="e1cca-165">**OnActionExecuted**(актионексекутедконтекст филтерконтекст): после вызова метода действия и перед выполнением результата (перед отрисовкой представления).</span><span class="sxs-lookup"><span data-stu-id="e1cca-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="e1cca-166">**OnResultExecuting**(ресултексекутингконтекст филтерконтекст): непосредственно перед выполнением результата (перед отрисовкой представления).</span><span class="sxs-lookup"><span data-stu-id="e1cca-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="e1cca-167">**Онресултексекутед**(ресултексекутедконтекст филтерконтекст): после выполнения результата (после подготовки представления).</span><span class="sxs-lookup"><span data-stu-id="e1cca-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="e1cca-168">Переопределяя любой из этих методов в производный класс, можно выполнить собственный код фильтрации.</span><span class="sxs-lookup"><span data-stu-id="e1cca-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>

1. <span data-ttu-id="e1cca-169">Откройте решение **Начало** решения, расположенное в папке **\Source\Ex01-LoggingActions\Begin** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="e1cca-170">Перед продолжением необходимо загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="e1cca-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="e1cca-171">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e1cca-172">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="e1cca-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e1cca-173">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e1cca-174">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="e1cca-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e1cca-175">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="e1cca-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e1cca-176">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e1cca-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="e1cca-177">Дополнительные сведения см. в этой статье: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="e1cca-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="e1cca-178">Добавьте новый C# класс в папку **Filters** и назовите его *CustomActionFilter.CS*.</span><span class="sxs-lookup"><span data-stu-id="e1cca-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="e1cca-179">В этой папке будут храниться все настраиваемые фильтры.</span><span class="sxs-lookup"><span data-stu-id="e1cca-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="e1cca-180">Откройте **CustomActionFilter.CS** и добавьте ссылку на пространства имен **System. Web. MVC** и **мвкмусиксторе. Models** :</span><span class="sxs-lookup"><span data-stu-id="e1cca-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="e1cca-181">(Фрагмент кода — *ASP.NET MVC 4 Custom Action Filters-EX1-кустомактионфилтернамеспацес*)</span><span class="sxs-lookup"><span data-stu-id="e1cca-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="e1cca-182">Наследуйте класс **кустомактионфилтер** из **ActionFilterAttribute** , а затем создайте класс **Кустомактионфилтер** , реализующий интерфейс **иактионфилтер** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="e1cca-183">Сделайте класс **кустомактионфилтер** переопределять метод **OnActionExecuting** и добавить необходимую логику для записи в журнал выполнения фильтра.</span><span class="sxs-lookup"><span data-stu-id="e1cca-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="e1cca-184">Для этого добавьте следующий выделенный код в класс **кустомактионфилтер** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="e1cca-185">(Фрагмент кода — *ASP.NET MVC 4 Custom Action Filters-EX1-логгингактионс*)</span><span class="sxs-lookup"><span data-stu-id="e1cca-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="e1cca-186">Метод **OnActionExecuting** использует **Entity Framework** для добавления нового регистра актионлог.</span><span class="sxs-lookup"><span data-stu-id="e1cca-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="e1cca-187">Он создает и заполняет новый экземпляр сущности сведениями о контексте из **филтерконтекст**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="e1cca-188">Дополнительные сведения о классе **контроллерконтекст** можно узнать на [сайте MSDN](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1cca-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="e1cca-189">Задача 2. Внедрение перехватчика кода в класс контроллера Store</span><span class="sxs-lookup"><span data-stu-id="e1cca-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="e1cca-190">В этой задаче будет добавлен настраиваемый фильтр, который будет внедрен во все классы контроллеров и действия контроллера, которые будут регистрироваться в журнале.</span><span class="sxs-lookup"><span data-stu-id="e1cca-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="e1cca-191">В этом упражнении класс контроллера хранилища будет иметь журнал.</span><span class="sxs-lookup"><span data-stu-id="e1cca-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="e1cca-192">Метод **OnActionExecuting** из настраиваемого фильтра **актионлогфилтераттрибуте** запускается при вызове внедренного элемента.</span><span class="sxs-lookup"><span data-stu-id="e1cca-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="e1cca-193">Кроме того, можно перехватить конкретный метод контроллера.</span><span class="sxs-lookup"><span data-stu-id="e1cca-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="e1cca-194">Откройте **стореконтроллер** по адресу **мвкмусиксторе\контроллерс** и добавьте ссылку на пространство имен **Filters** :</span><span class="sxs-lookup"><span data-stu-id="e1cca-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="e1cca-195">Вставьте пользовательский фильтр **кустомактионфилтер** в класс **стореконтроллер** , добавив атрибут **[кустомактионфилтер]** перед объявлением класса.</span><span class="sxs-lookup"><span data-stu-id="e1cca-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="e1cca-196">При внедрении фильтра в класс контроллера также вставляются все его действия.</span><span class="sxs-lookup"><span data-stu-id="e1cca-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="e1cca-197">Если вы хотите применить фильтр только к набору действий, необходимо внедрить **[кустомактионфилтер]** в один из них:</span><span class="sxs-lookup"><span data-stu-id="e1cca-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="e1cca-198">Задача 3. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="e1cca-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="e1cca-199">В этой задаче будет протестировать работу фильтра ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="e1cca-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="e1cca-200">Вы запустите приложение и зайдете в магазин, а затем проверите зарегистрированные действия.</span><span class="sxs-lookup"><span data-stu-id="e1cca-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="e1cca-201">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="e1cca-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="e1cca-202">Перейдите по **/актионлог** , чтобы просмотреть начальное состояние представления журнала:</span><span class="sxs-lookup"><span data-stu-id="e1cca-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="e1cca-203">![Состояние средства записи журнала перед действием страницы](aspnet-mvc-4-custom-action-filters/_static/image3.png "Состояние средства записи журнала перед действием страницы")</span><span class="sxs-lookup"><span data-stu-id="e1cca-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="e1cca-204">*Состояние средства записи журнала перед действием страницы*</span><span class="sxs-lookup"><span data-stu-id="e1cca-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="e1cca-205">По умолчанию он всегда будет отображать один элемент, созданный при извлечении существующих жанров для меню.</span><span class="sxs-lookup"><span data-stu-id="e1cca-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="e1cca-206">В целях простоты мы очищаете таблицу **актионлог** при каждом запуске приложения, чтобы они показывали только журналы проверки каждой конкретной задачи.</span><span class="sxs-lookup"><span data-stu-id="e1cca-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="e1cca-207">Может потребоваться удалить следующий код из метода **сеанса\_Start** (в классе **Global. asax** ), чтобы сохранить журнал журнала для всех действий, выполняемых в контроллере хранилища.</span><span class="sxs-lookup"><span data-stu-id="e1cca-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="e1cca-208">Щелкните один из **жанров** в меню и выполните некоторые действия, например просмотр доступного альбома.</span><span class="sxs-lookup"><span data-stu-id="e1cca-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="e1cca-209">Перейдите в **/актионлог** и, если журнал пуст, нажмите клавишу **F5** , чтобы обновить страницу.</span><span class="sxs-lookup"><span data-stu-id="e1cca-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="e1cca-210">Убедитесь, что посещения были отслеживанием:</span><span class="sxs-lookup"><span data-stu-id="e1cca-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="e1cca-211">![Журнал действий с регистрируемым действием](aspnet-mvc-4-custom-action-filters/_static/image4.png "Журнал действий с регистрируемым действием")</span><span class="sxs-lookup"><span data-stu-id="e1cca-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="e1cca-212">*Журнал действий с регистрируемым действием*</span><span class="sxs-lookup"><span data-stu-id="e1cca-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="e1cca-213">Упражнение 2. Управление несколькими фильтрами действий</span><span class="sxs-lookup"><span data-stu-id="e1cca-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="e1cca-214">В этом упражнении вы добавите второй настраиваемый фильтр действий в класс Стореконтроллер и определите конкретный порядок, в котором будут выполняться оба фильтра.</span><span class="sxs-lookup"><span data-stu-id="e1cca-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="e1cca-215">Затем вы обновите код, чтобы зарегистрировать фильтр глобально.</span><span class="sxs-lookup"><span data-stu-id="e1cca-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="e1cca-216">При определении порядка выполнения фильтров можно учитывать различные параметры.</span><span class="sxs-lookup"><span data-stu-id="e1cca-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="e1cca-217">Например, свойство Order и область фильтров:</span><span class="sxs-lookup"><span data-stu-id="e1cca-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="e1cca-218">Можно определить **область** для каждого из фильтров, например, можно задать область действия всех фильтров действий, которые будут выполняться в пределах **области контроллера**, и все фильтры авторизации для выполнения в **глобальной области**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="e1cca-219">Области имеют определенный порядок выполнения.</span><span class="sxs-lookup"><span data-stu-id="e1cca-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="e1cca-220">Кроме того, у каждого фильтра действий есть свойство Order, которое используется для определения порядка выполнения в области фильтра.</span><span class="sxs-lookup"><span data-stu-id="e1cca-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="e1cca-221">Дополнительные сведения о порядке выполнения фильтров настраиваемых действий см. в этой статье MSDN: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span><span class="sxs-lookup"><span data-stu-id="e1cca-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="e1cca-222">Задача 1. Создание нового настраиваемого фильтра действий</span><span class="sxs-lookup"><span data-stu-id="e1cca-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="e1cca-223">В этой задаче вы создадите новый настраиваемый фильтр действий для внедрения в класс Стореконтроллер, чтобы узнать, как управлять порядком выполнения фильтров.</span><span class="sxs-lookup"><span data-stu-id="e1cca-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="e1cca-224">Откройте решение **Начало** решения, расположенное в папке **\Source\Ex02-ManagingMultipleActionFilters\Begin** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="e1cca-225">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="e1cca-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="e1cca-226">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="e1cca-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e1cca-227">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="e1cca-228">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="e1cca-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="e1cca-229">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="e1cca-230">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="e1cca-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e1cca-231">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="e1cca-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e1cca-232">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e1cca-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="e1cca-233">Дополнительные сведения см. в этой статье: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="e1cca-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="e1cca-234">Добавьте новый C# класс в папку **Filters** и назовите его *MyNewCustomActionFilter.CS* .</span><span class="sxs-lookup"><span data-stu-id="e1cca-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="e1cca-235">Откройте **MyNewCustomActionFilter.CS** и добавьте ссылку на **System. Web. MVC** и пространство имен **мвкмусиксторе. Models** :</span><span class="sxs-lookup"><span data-stu-id="e1cca-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="e1cca-236">(Фрагмент кода — *ASP.NET MVC 4 Custom Action Filters-EX2-миневкустомактионфилтернамеспацес*)</span><span class="sxs-lookup"><span data-stu-id="e1cca-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="e1cca-237">Замените объявление класса по умолчанию следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="e1cca-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="e1cca-238">(Фрагмент кода — *ASP.NET MVC 4 Custom Action Filters-EX2-миневкустомактионфилтеркласс*)</span><span class="sxs-lookup"><span data-stu-id="e1cca-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="e1cca-239">Этот настраиваемый фильтр действий почти не тот, который был создан в предыдущем упражнении.</span><span class="sxs-lookup"><span data-stu-id="e1cca-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="e1cca-240">Основное отличие заключается в том, что в нем есть *&quot;, регистрируемые&quot;ным* атрибутом, обновленным с помощью этого нового класса "имя", чтобы узнать, какой фильтр зарегистрировал журнал.</span><span class="sxs-lookup"><span data-stu-id="e1cca-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify which filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="e1cca-241">Задача 2. внедрение нового перехватчика кода в класс Стореконтроллер</span><span class="sxs-lookup"><span data-stu-id="e1cca-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="e1cca-242">В этой задаче вы добавите новый настраиваемый фильтр в класс Стореконтроллер и запустите решение, чтобы проверить, как оба фильтра работают вместе.</span><span class="sxs-lookup"><span data-stu-id="e1cca-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="e1cca-243">Откройте класс **стореконтроллер** , расположенный по адресу **мвкмусиксторе\контроллерс** , и вставьте новый настраиваемый фильтр **миневкустомактионфилтер** в класс **стореконтроллер** , как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="e1cca-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="e1cca-244">Теперь запустите приложение, чтобы увидеть, как работают эти два настраиваемых фильтра действий.</span><span class="sxs-lookup"><span data-stu-id="e1cca-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="e1cca-245">Для этого нажмите клавишу **F5** и дождитесь запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="e1cca-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="e1cca-246">Перейдите по **/актионлог** , чтобы просмотреть начальное состояние представления журнала.</span><span class="sxs-lookup"><span data-stu-id="e1cca-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="e1cca-247">![Состояние средства записи журнала перед действием страницы](aspnet-mvc-4-custom-action-filters/_static/image5.png "Состояние средства записи журнала перед действием страницы")</span><span class="sxs-lookup"><span data-stu-id="e1cca-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="e1cca-248">*Состояние средства записи журнала перед действием страницы*</span><span class="sxs-lookup"><span data-stu-id="e1cca-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="e1cca-249">Щелкните один из **жанров** в меню и выполните некоторые действия, например просмотр доступного альбома.</span><span class="sxs-lookup"><span data-stu-id="e1cca-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="e1cca-250">Проверьте это время. посещения были записаны дважды: один раз для каждого из фильтров настраиваемых действий, добавленных в класс **сторажеконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="e1cca-251">![Журнал действий с регистрируемым действием](aspnet-mvc-4-custom-action-filters/_static/image6.png "Журнал действий с регистрируемым действием")</span><span class="sxs-lookup"><span data-stu-id="e1cca-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="e1cca-252">*Журнал действий с регистрируемым действием*</span><span class="sxs-lookup"><span data-stu-id="e1cca-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="e1cca-253">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="e1cca-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="e1cca-254">Задача 3. Управление порядком фильтрации</span><span class="sxs-lookup"><span data-stu-id="e1cca-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="e1cca-255">В этой задаче вы узнаете, как управлять порядком выполнения фильтров с помощью свойства Order.</span><span class="sxs-lookup"><span data-stu-id="e1cca-255">In this task, you will learn how to manage the filters' execution order by using the Order property.</span></span>

1. <span data-ttu-id="e1cca-256">Откройте класс **стореконтроллер** , расположенный по адресу **мвкмусиксторе\контроллерс** , и укажите свойство **Order** в обоих фильтрах, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e1cca-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="e1cca-257">Теперь проверьте, как выполняются фильтры в зависимости от значения свойства Order.</span><span class="sxs-lookup"><span data-stu-id="e1cca-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="e1cca-258">Вы обнаружите, что фильтр с наименьшим порядковым значением (**кустомактионфилтер**) является первым из выполняемых.</span><span class="sxs-lookup"><span data-stu-id="e1cca-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="e1cca-259">Нажмите клавишу **F5** и дождитесь запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="e1cca-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="e1cca-260">Перейдите по **/актионлог** , чтобы просмотреть начальное состояние представления журнала.</span><span class="sxs-lookup"><span data-stu-id="e1cca-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="e1cca-261">![Состояние средства записи журнала перед действием страницы](aspnet-mvc-4-custom-action-filters/_static/image7.png "Состояние средства записи журнала перед действием страницы")</span><span class="sxs-lookup"><span data-stu-id="e1cca-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="e1cca-262">*Состояние средства записи журнала перед действием страницы*</span><span class="sxs-lookup"><span data-stu-id="e1cca-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="e1cca-263">Щелкните один из **жанров** в меню и выполните некоторые действия, например просмотр доступного альбома.</span><span class="sxs-lookup"><span data-stu-id="e1cca-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="e1cca-264">Убедитесь, что на этот раз посещения были отсортированы по порядковому номеру: сначала **кустомактионфилтер** журналы.</span><span class="sxs-lookup"><span data-stu-id="e1cca-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="e1cca-265">![Журнал действий с регистрируемым действием](aspnet-mvc-4-custom-action-filters/_static/image8.png "Журнал действий с регистрируемым действием")</span><span class="sxs-lookup"><span data-stu-id="e1cca-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="e1cca-266">*Журнал действий с регистрируемым действием*</span><span class="sxs-lookup"><span data-stu-id="e1cca-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="e1cca-267">Теперь вы обновите значение порядка фильтров и убедитесь, как изменяется порядок ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="e1cca-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="e1cca-268">В классе **стореконтроллер** обновите значение порядка фильтров, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e1cca-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="e1cca-269">Запустите приложение еще раз, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="e1cca-270">Щелкните один из **жанров** в меню и выполните некоторые действия, например просмотр доступного альбома.</span><span class="sxs-lookup"><span data-stu-id="e1cca-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="e1cca-271">Убедитесь, что в этот раз журналы, созданные с помощью фильтра **миневкустомактионфилтер** , отображаются первыми.</span><span class="sxs-lookup"><span data-stu-id="e1cca-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="e1cca-272">![Журнал действий с регистрируемым действием](aspnet-mvc-4-custom-action-filters/_static/image9.png "Журнал действий с регистрируемым действием")</span><span class="sxs-lookup"><span data-stu-id="e1cca-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="e1cca-273">*Журнал действий с регистрируемым действием*</span><span class="sxs-lookup"><span data-stu-id="e1cca-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="e1cca-274">Задача 4. Глобальная регистрация фильтров</span><span class="sxs-lookup"><span data-stu-id="e1cca-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="e1cca-275">В этой задаче будет обновлено решение для регистрации нового фильтра (**миневкустомактионфилтер**) в качестве глобального фильтра.</span><span class="sxs-lookup"><span data-stu-id="e1cca-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="e1cca-276">Таким образом, все действия, выполняемые в приложении, будут запускаться не только в Стореконтроллер, но и в предыдущей задаче.</span><span class="sxs-lookup"><span data-stu-id="e1cca-276">By doing this, it will be triggered by all the actions performed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="e1cca-277">В классе **стореконтроллер** удалите атрибут **[миневкустомактионфилтер]** и свойство Order из **[кустомактионфилтер]** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="e1cca-278">Он должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="e1cca-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="e1cca-279">Откройте файл **Global. asax** и перейдите к методу **\_запуск приложения** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="e1cca-280">Обратите внимание, что каждый раз, когда приложение запускается, регистрирует глобальные фильтры путем вызова метода **регистерглобалфилтерс** в классе **филтерконфиг** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="e1cca-281">![Регистрация глобальных фильтров в Global. asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Регистрация глобальных фильтров в Global. asax")</span><span class="sxs-lookup"><span data-stu-id="e1cca-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="e1cca-282">*Регистрация глобальных фильтров в Global. asax*</span><span class="sxs-lookup"><span data-stu-id="e1cca-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="e1cca-283">Откройте файл **FilterConfig.CS** в папке **app\_Start** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="e1cca-284">Добавить ссылку на использование System. Web. MVC; Использование Мвкмусиксторе. Filters; имен.</span><span class="sxs-lookup"><span data-stu-id="e1cca-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="e1cca-285">Обновите метод **регистерглобалфилтерс** , добавив настраиваемый фильтр.</span><span class="sxs-lookup"><span data-stu-id="e1cca-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="e1cca-286">Для этого добавьте выделенный код:</span><span class="sxs-lookup"><span data-stu-id="e1cca-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="e1cca-287">Запустите приложение, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="e1cca-288">Щелкните один из **жанров** в меню и выполните некоторые действия, например просмотр доступного альбома.</span><span class="sxs-lookup"><span data-stu-id="e1cca-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="e1cca-289">Убедитесь, что сейчас **[миневкустомактионфилтер]** будет внедрен в HomeController и актионлогконтроллер.</span><span class="sxs-lookup"><span data-stu-id="e1cca-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="e1cca-290">![Журнал действий с регистрируемым действием](aspnet-mvc-4-custom-action-filters/_static/image11.png "Журнал действий с регистрируемым действием")</span><span class="sxs-lookup"><span data-stu-id="e1cca-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="e1cca-291">*Журнал действий с зарегистрированным глобальным действием*</span><span class="sxs-lookup"><span data-stu-id="e1cca-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="e1cca-292">Кроме того, это приложение можно развернуть на веб-сайтах Windows Azure в [приложении б: Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="e1cca-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="e1cca-293">Сводка</span><span class="sxs-lookup"><span data-stu-id="e1cca-293">Summary</span></span>

<span data-ttu-id="e1cca-294">С помощью этой практической лабораторной работы вы узнали, как расширить фильтр действий для выполнения настраиваемых действий.</span><span class="sxs-lookup"><span data-stu-id="e1cca-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="e1cca-295">Вы также узнали, как внедрить любой фильтр на контроллеры страниц.</span><span class="sxs-lookup"><span data-stu-id="e1cca-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="e1cca-296">Используются следующие основные понятия:</span><span class="sxs-lookup"><span data-stu-id="e1cca-296">The following concepts were used:</span></span>

- <span data-ttu-id="e1cca-297">Создание настраиваемых фильтров действий с помощью класса ASP.NET MVC ActionFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="e1cca-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="e1cca-298">Как внедрять фильтры в ASP.NET MVC Controllers</span><span class="sxs-lookup"><span data-stu-id="e1cca-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="e1cca-299">Управление порядком фильтрации с помощью свойства Order</span><span class="sxs-lookup"><span data-stu-id="e1cca-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="e1cca-300">Глобальная регистрация фильтров</span><span class="sxs-lookup"><span data-stu-id="e1cca-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="e1cca-301">Приложение а. Установка Visual Studio Express 2012 для Web</span><span class="sxs-lookup"><span data-stu-id="e1cca-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="e1cca-302">Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версии с помощью **[установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="e1cca-303">Следующие инструкции помогут вам выполнить действия, необходимые для установки *Visual Studio Express 2012 для Web* с помощью *установщик веб-платформы Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="e1cca-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="e1cca-304">Перейдите на сайт [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="e1cca-304">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="e1cca-305">Кроме того, если у вас уже установлен установщик веб-платформы, вы можете открыть его и найти продукт &quot;<em>Visual Studio Express 2012 для Web с Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="e1cca-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="e1cca-306">Щелкните **Install Now (установить сейчас**).</span><span class="sxs-lookup"><span data-stu-id="e1cca-306">Click on **Install Now**.</span></span> <span data-ttu-id="e1cca-307">Если у вас нет **установщика веб-платформы** , вы будете сначала перенаправлены на загрузку и установку.</span><span class="sxs-lookup"><span data-stu-id="e1cca-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="e1cca-308">После открытия **установщика веб-платформы** нажмите кнопку **установить** , чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="e1cca-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="e1cca-309">![Установка Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Установка Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="e1cca-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="e1cca-310">*Установка Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="e1cca-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="e1cca-311">Прочитайте все лицензии и условия продуктов и нажмите кнопку " **принять** ", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="e1cca-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Принятие условий лицензии](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="e1cca-313">*Принятие условий лицензии*</span><span class="sxs-lookup"><span data-stu-id="e1cca-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="e1cca-314">Дождитесь завершения процесса загрузки и установки.</span><span class="sxs-lookup"><span data-stu-id="e1cca-314">Wait until the downloading and installation process completes.</span></span>

    ![Ход установки](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="e1cca-316">*Ход установки*</span><span class="sxs-lookup"><span data-stu-id="e1cca-316">*Installation progress*</span></span>
6. <span data-ttu-id="e1cca-317">После завершения установки нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-317">When the installation completes, click **Finish**.</span></span>

    ![Установка завершена](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="e1cca-319">*Установка завершена*</span><span class="sxs-lookup"><span data-stu-id="e1cca-319">*Installation completed*</span></span>
7. <span data-ttu-id="e1cca-320">Нажмите кнопку **выход** , чтобы закрыть установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="e1cca-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="e1cca-321">Чтобы открыть Visual Studio Express для Интернета, перейдите на **начальный** экран и начните запись &quot;**VS Express**&quot;, а затем щелкните плитку **VS Express для Web** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Плитка VS Express для Web](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="e1cca-323">*Плитка VS Express для Web*</span><span class="sxs-lookup"><span data-stu-id="e1cca-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="e1cca-324">Приложение б. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание</span><span class="sxs-lookup"><span data-stu-id="e1cca-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="e1cca-325">В этом приложении показано, как создать новый веб-сайт из портал управления Windows Azure и опубликовать полученное приложение, выполнив следующие лабораторные занятия, используя возможности публикации веб-развертывание, предоставляемые Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cca-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="e1cca-326">Задача 1. Создание нового веб-сайта на портале Windows Azure</span><span class="sxs-lookup"><span data-stu-id="e1cca-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="e1cca-327">Перейдите в [портал управления Windows Azure](https://manage.windowsazure.com/) и выполните вход с использованием учетных данных Майкрософт, связанных с подпиской.</span><span class="sxs-lookup"><span data-stu-id="e1cca-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e1cca-328">С помощью Windows Azure можно бесплатно разместить 10 веб-сайтов ASP.NET, а затем масштабировать их по мере роста объема трафика.</span><span class="sxs-lookup"><span data-stu-id="e1cca-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="e1cca-329">Вы можете зарегистрироваться [здесь](https://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="e1cca-329">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="e1cca-330">![Вход в Windows портал Azure](aspnet-mvc-4-custom-action-filters/_static/image17.png "Вход в Windows портал Azure")</span><span class="sxs-lookup"><span data-stu-id="e1cca-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="e1cca-331">*Вход в Windows Azure портал управления*</span><span class="sxs-lookup"><span data-stu-id="e1cca-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="e1cca-332">На панели команд щелкните **создать** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="e1cca-333">![Создание нового веб-сайта](aspnet-mvc-4-custom-action-filters/_static/image18.png "Создание нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="e1cca-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="e1cca-334">*Создание нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="e1cca-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="e1cca-335">Щелкните **Compute** | **веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="e1cca-336">Затем выберите пункт **Быстрое создание** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="e1cca-337">Предоставьте доступный URL-адрес для нового веб-сайта и щелкните **создать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e1cca-338">Веб-сайт Windows Azure — это узел для веб-приложения, работающего в облаке, которыми можно управлять и которыми вы управляете.</span><span class="sxs-lookup"><span data-stu-id="e1cca-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="e1cca-339">Параметр Быстрое создание позволяет развернуть завершенное веб-приложение на веб-сайте Windows Azure извне портала.</span><span class="sxs-lookup"><span data-stu-id="e1cca-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="e1cca-340">Он не включает шаги по настройке базы данных.</span><span class="sxs-lookup"><span data-stu-id="e1cca-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="e1cca-341">![Создание нового веб-сайта с помощью быстрого создания](aspnet-mvc-4-custom-action-filters/_static/image19.png "Создание нового веб-сайта с помощью быстрого создания")</span><span class="sxs-lookup"><span data-stu-id="e1cca-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="e1cca-342">*Создание нового веб-сайта с помощью быстрого создания*</span><span class="sxs-lookup"><span data-stu-id="e1cca-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="e1cca-343">Дождитесь создания нового **веб-сайта** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="e1cca-344">После создания веб-сайта щелкните ссылку в столбце **URL-адрес** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="e1cca-345">Убедитесь, что новый веб-сайт работает.</span><span class="sxs-lookup"><span data-stu-id="e1cca-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="e1cca-346">![Обзор нового веб-сайта](aspnet-mvc-4-custom-action-filters/_static/image20.png "Обзор нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="e1cca-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="e1cca-347">*Обзор нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="e1cca-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="e1cca-348">![Веб-сайт работает](aspnet-mvc-4-custom-action-filters/_static/image21.png "Веб-сайт работает")</span><span class="sxs-lookup"><span data-stu-id="e1cca-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="e1cca-349">*Веб-сайт работает*</span><span class="sxs-lookup"><span data-stu-id="e1cca-349">*Web site running*</span></span>
6. <span data-ttu-id="e1cca-350">Вернитесь на портал и щелкните имя веб-сайта в столбце **имя** , чтобы отобразить страницы управления.</span><span class="sxs-lookup"><span data-stu-id="e1cca-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="e1cca-351">![Открытие страниц управления веб-сайтом](aspnet-mvc-4-custom-action-filters/_static/image22.png "Открытие страниц управления веб-сайтом")</span><span class="sxs-lookup"><span data-stu-id="e1cca-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="e1cca-352">*Открытие страниц управления веб-сайтом*</span><span class="sxs-lookup"><span data-stu-id="e1cca-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="e1cca-353">На странице **панель мониторинга** в разделе **краткий обзор** щелкните ссылку **скачать профиль публикации** .</span><span class="sxs-lookup"><span data-stu-id="e1cca-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e1cca-354">*Профиль публикации* содержит все сведения, необходимые для публикации веб-приложения на веб-сайте Windows Azure для каждого включенного метода публикации.</span><span class="sxs-lookup"><span data-stu-id="e1cca-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="e1cca-355">Профиль публикации содержит URL-адреса, учетные данные пользователей и строки для открытия базы данных, которые необходимы для проверки подлинности и подключения к каждой из конечных точек, соответствующей разрешенному методу публикации.</span><span class="sxs-lookup"><span data-stu-id="e1cca-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="e1cca-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express для Web** и **Microsoft Visual Studio 2012** поддерживают чтение профилей публикации для автоматизации настройки этих программ для публикации веб-приложений на веб-сайтах Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cca-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="e1cca-357">![Скачивание профиля публикации веб-сайта](aspnet-mvc-4-custom-action-filters/_static/image23.png "Скачивание профиля публикации веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="e1cca-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="e1cca-358">*Скачивание профиля публикации веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="e1cca-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="e1cca-359">Скачайте файл профиля публикации в известное расположение.</span><span class="sxs-lookup"><span data-stu-id="e1cca-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="e1cca-360">Далее в этом упражнении вы узнаете, как использовать этот файл для публикации веб-приложения на веб-сайтах Windows Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1cca-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="e1cca-361">![Сохранение файла профиля публикации](aspnet-mvc-4-custom-action-filters/_static/image24.png "Сохранение профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="e1cca-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="e1cca-362">*Сохранение файла профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="e1cca-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="e1cca-363">Задача 2. Настройка сервера базы данных</span><span class="sxs-lookup"><span data-stu-id="e1cca-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="e1cca-364">Если приложение использует SQL Server базы данных, потребуется создать сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e1cca-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="e1cca-365">Если вы хотите развернуть простое приложение, которое не использует SQL Server вы можете пропустить эту задачу.</span><span class="sxs-lookup"><span data-stu-id="e1cca-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="e1cca-366">Для хранения базы данных приложения необходим сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e1cca-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="e1cca-367">Серверы базы данных SQL можно просмотреть в подписке на портале управления Windows Azure в **базах данных sql** | **серверы** | **панели мониторинга сервера**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="e1cca-368">Если сервер не создан, можно создать его с помощью кнопки **Добавить** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="e1cca-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="e1cca-369">Запишите **имя сервера и URL-адрес, имя для входа администратора и пароль**, так как они будут использоваться в следующих задачах.</span><span class="sxs-lookup"><span data-stu-id="e1cca-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="e1cca-370">Пока не создавайте базу данных, так как она будет создана на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="e1cca-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="e1cca-371">![Панель мониторинга сервера базы данных SQL](aspnet-mvc-4-custom-action-filters/_static/image25.png "Панель мониторинга сервера базы данных SQL")</span><span class="sxs-lookup"><span data-stu-id="e1cca-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="e1cca-372">*Панель мониторинга сервера базы данных SQL*</span><span class="sxs-lookup"><span data-stu-id="e1cca-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="e1cca-373">В следующей задаче вы проверите подключение к базе данных из Visual Studio. по этой причине необходимо включить локальный IP-адрес в список **разрешенных IP-адресов**сервера.</span><span class="sxs-lookup"><span data-stu-id="e1cca-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="e1cca-374">Для этого нажмите кнопку **настроить**, выберите IP-адрес из **текущего IP-адреса клиента** и вставьте его в текстовые поля **начальный IP-адрес** и **конечный IP** -адрес и нажмите кнопку ![добавить-клиент-IP – адрес-OK-кнопка](aspnet-mvc-4-custom-action-filters/_static/image26.png).</span><span class="sxs-lookup"><span data-stu-id="e1cca-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![Добавление IP-адреса клиента](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="e1cca-376">*Добавление IP-адреса клиента*</span><span class="sxs-lookup"><span data-stu-id="e1cca-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="e1cca-377">После добавления **IP-адреса клиента** в список Разрешенные IP-адреса нажмите кнопку **сохранить** , чтобы подтвердить изменения.</span><span class="sxs-lookup"><span data-stu-id="e1cca-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Подтверждение изменений](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="e1cca-379">*Подтверждение изменений*</span><span class="sxs-lookup"><span data-stu-id="e1cca-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="e1cca-380">Задача 3. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание</span><span class="sxs-lookup"><span data-stu-id="e1cca-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="e1cca-381">Вернитесь к решению ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="e1cca-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="e1cca-382">В **Обозреватель решений**щелкните правой кнопкой мыши проект веб-сайта и выберите **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="e1cca-383">![Публикация приложения](aspnet-mvc-4-custom-action-filters/_static/image29.png "Публикация приложения")</span><span class="sxs-lookup"><span data-stu-id="e1cca-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="e1cca-384">*Публикация веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="e1cca-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="e1cca-385">Импортируйте профиль публикации, сохраненный в первой задаче.</span><span class="sxs-lookup"><span data-stu-id="e1cca-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="e1cca-386">![Импорт профиля публикации](aspnet-mvc-4-custom-action-filters/_static/image30.png "Импорт профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="e1cca-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="e1cca-387">*Импорт профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="e1cca-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="e1cca-388">Щелкните **проверить подключение**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-388">Click **Validate Connection**.</span></span> <span data-ttu-id="e1cca-389">После завершения проверки нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e1cca-390">Проверка завершится, когда появится зеленая галочка рядом с кнопкой проверить подключение.</span><span class="sxs-lookup"><span data-stu-id="e1cca-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="e1cca-391">![Проверка подключения](aspnet-mvc-4-custom-action-filters/_static/image31.png "Проверка подключения")</span><span class="sxs-lookup"><span data-stu-id="e1cca-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="e1cca-392">*Проверка подключения*</span><span class="sxs-lookup"><span data-stu-id="e1cca-392">*Validating connection*</span></span>
4. <span data-ttu-id="e1cca-393">На странице **Параметры** в разделе **базы данных** нажмите кнопку рядом с текстовым полем подключения к базе данных (т. е. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="e1cca-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="e1cca-394">![Конфигурация веб-развертывания](aspnet-mvc-4-custom-action-filters/_static/image32.png "Конфигурация веб-развертывания")</span><span class="sxs-lookup"><span data-stu-id="e1cca-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="e1cca-395">*Конфигурация веб-развертывания*</span><span class="sxs-lookup"><span data-stu-id="e1cca-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="e1cca-396">Настройте подключение к базе данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e1cca-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="e1cca-397">В поле **имя сервера** введите URL-адрес сервера базы данных SQL с помощью префикса *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="e1cca-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="e1cca-398">В окне **имя пользователя** введите имя для входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="e1cca-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="e1cca-399">В окне **пароль** введите пароль для входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="e1cca-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="e1cca-400">Введите новое имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="e1cca-400">Type a new database name.</span></span>

     <span data-ttu-id="e1cca-401">![Настройка строки подключения к целевому объекту](aspnet-mvc-4-custom-action-filters/_static/image33.png "Настройка строки подключения к целевому объекту")</span><span class="sxs-lookup"><span data-stu-id="e1cca-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="e1cca-402">*Настройка строки подключения к целевому объекту*</span><span class="sxs-lookup"><span data-stu-id="e1cca-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="e1cca-403">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-403">Then click **OK**.</span></span> <span data-ttu-id="e1cca-404">При появлении запроса на создание базы данных нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="e1cca-405">![Создание базы данных](aspnet-mvc-4-custom-action-filters/_static/image34.png "Создание строки базы данных")</span><span class="sxs-lookup"><span data-stu-id="e1cca-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="e1cca-406">*Создание базы данных*</span><span class="sxs-lookup"><span data-stu-id="e1cca-406">*Creating the database*</span></span>
7. <span data-ttu-id="e1cca-407">Строка подключения, которая будет использоваться для подключения к базе данных SQL в Windows Azure, отображается в текстовом поле подключения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e1cca-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="e1cca-408">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-408">Then click **Next**.</span></span>

    <span data-ttu-id="e1cca-409">![Строка подключения, указывающая на базу данных SQL](aspnet-mvc-4-custom-action-filters/_static/image35.png "Строка подключения, указывающая на базу данных SQL")</span><span class="sxs-lookup"><span data-stu-id="e1cca-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="e1cca-410">*Строка подключения, указывающая на базу данных SQL*</span><span class="sxs-lookup"><span data-stu-id="e1cca-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="e1cca-411">На странице **Предварительный просмотр** нажмите кнопку **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="e1cca-412">![Публикация веб-приложения](aspnet-mvc-4-custom-action-filters/_static/image36.png "Публикация веб-приложения")</span><span class="sxs-lookup"><span data-stu-id="e1cca-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="e1cca-413">*Публикация веб-приложения*</span><span class="sxs-lookup"><span data-stu-id="e1cca-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="e1cca-414">По завершении процесса публикации браузер по умолчанию будет открывать опубликованный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="e1cca-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="e1cca-415">Приложение в. Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="e1cca-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="e1cca-416">С помощью фрагментов кода вы можете получить все необходимые вам коды.</span><span class="sxs-lookup"><span data-stu-id="e1cca-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="e1cca-417">В лабораторном документе вы узнаете, когда можно использовать их, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="e1cca-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="e1cca-418">![Использование фрагментов кода Visual Studio для вставки кода в проект](aspnet-mvc-4-custom-action-filters/_static/image37.png "Использование фрагментов кода Visual Studio для вставки кода в проект")</span><span class="sxs-lookup"><span data-stu-id="e1cca-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="e1cca-419">*Использование фрагментов кода Visual Studio для вставки кода в проект*</span><span class="sxs-lookup"><span data-stu-id="e1cca-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="e1cca-420">***Добавление фрагмента кода с помощью клавиатуры (C# только)***</span><span class="sxs-lookup"><span data-stu-id="e1cca-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="e1cca-421">Поместите курсор в то место, куда вы хотите вставить код.</span><span class="sxs-lookup"><span data-stu-id="e1cca-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="e1cca-422">Начните вводить имя фрагмента (без пробелов или дефисов).</span><span class="sxs-lookup"><span data-stu-id="e1cca-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="e1cca-423">Посмотрите, как IntelliSense отображает соответствующие имена фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="e1cca-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="e1cca-424">Выберите правильный фрагмент кода (или вводите его, пока не будет выбрано имя всего фрагмента).</span><span class="sxs-lookup"><span data-stu-id="e1cca-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="e1cca-425">Дважды нажмите клавишу TAB, чтобы вставить фрагмент в позицию курсора.</span><span class="sxs-lookup"><span data-stu-id="e1cca-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="e1cca-426">![Начните вводить имя фрагмента](aspnet-mvc-4-custom-action-filters/_static/image38.png "Начните вводить имя фрагмента")</span><span class="sxs-lookup"><span data-stu-id="e1cca-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="e1cca-427">*Начните вводить имя фрагмента*</span><span class="sxs-lookup"><span data-stu-id="e1cca-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="e1cca-428">![Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.](aspnet-mvc-4-custom-action-filters/_static/image39.png "Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="e1cca-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="e1cca-429">*Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="e1cca-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="e1cca-430">![Снова нажмите клавишу TAB, и фрагмент развернется](aspnet-mvc-4-custom-action-filters/_static/image40.png "Снова нажмите клавишу TAB, и фрагмент развернется")</span><span class="sxs-lookup"><span data-stu-id="e1cca-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="e1cca-431">*Снова нажмите клавишу TAB, и фрагмент развернется*</span><span class="sxs-lookup"><span data-stu-id="e1cca-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="e1cca-432">***Добавление фрагмента кода с помощью мыши (C#, Visual Basic и XML)*** одного.</span><span class="sxs-lookup"><span data-stu-id="e1cca-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="e1cca-433">Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="e1cca-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="e1cca-434">Выберите **Вставить фрагмент** , за которым следуют **фрагменты кода**.</span><span class="sxs-lookup"><span data-stu-id="e1cca-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="e1cca-435">Выберите соответствующий фрагмент из списка, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="e1cca-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="e1cca-436">![Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.](aspnet-mvc-4-custom-action-filters/_static/image41.png "Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="e1cca-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="e1cca-437">*Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="e1cca-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="e1cca-438">![Выберите соответствующий фрагмент из списка, щелкнув его.](aspnet-mvc-4-custom-action-filters/_static/image42.png "Выберите соответствующий фрагмент из списка, щелкнув его.")</span><span class="sxs-lookup"><span data-stu-id="e1cca-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="e1cca-439">*Выберите соответствующий фрагмент из списка, щелкнув его.*</span><span class="sxs-lookup"><span data-stu-id="e1cca-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
