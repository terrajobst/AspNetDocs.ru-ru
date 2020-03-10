---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework формирование шаблонов и миграция | Документация Майкрософт
author: rick-anderson
description: Если вы знакомы с методами контроллера ASP.NET MVC 4 или выполнили &quot;вспомогательные функции, формы и проверки&quot; практической лабораторной работе, следует иметь в виду...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484644"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="79c33-103">Перенос и формирование шаблонов ASP.NET MVC 4 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="79c33-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="79c33-104">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="79c33-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="79c33-105">Скачать обучающий комплект Web Camp</span><span class="sxs-lookup"><span data-stu-id="79c33-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="79c33-106">Если вы знакомы с методами контроллера ASP.NET MVC 4 или выполнили &quot;вспомогательные функции, формы и проверки&quot; практической лабораторной работе, необходимо знать, что многие из логики для создания, обновления, перечисления и удаления любой сущности данных, которая повторяется в приложении.</span><span class="sxs-lookup"><span data-stu-id="79c33-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that many of the logic to create, update, list and remove any data entity it is repeated among the application.</span></span> <span data-ttu-id="79c33-107">Не говоря уже о том, что если модель имеет несколько классов для управления, то, скорее всего, придется потратить значительное время на написание методов POST и GET для каждой операции сущности, а также каждого представления.</span><span class="sxs-lookup"><span data-stu-id="79c33-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="79c33-108">В этой лабораторной работе вы узнаете, как использовать формирование шаблонов ASP.NET MVC 4 для автоматического создания базовых показателей CRUD приложения (создание, чтение, обновление и удаление).</span><span class="sxs-lookup"><span data-stu-id="79c33-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="79c33-109">Начиная с простого класса модели и без написания отдельной строки кода, вы создадите контроллер, который будет содержать все операции CRUD, а также все необходимые представления.</span><span class="sxs-lookup"><span data-stu-id="79c33-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="79c33-110">После создания и выполнения простого решения будет создана база данных приложения, а также логика и представления MVC для обработки данных.</span><span class="sxs-lookup"><span data-stu-id="79c33-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="79c33-111">Кроме того, вы узнаете, как просто использовать Entity Framework миграции для выполнения обновлений модели всего приложения.</span><span class="sxs-lookup"><span data-stu-id="79c33-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="79c33-112">Entity Framework миграции позволяют изменить базу данных после того, как модель будет изменена простыми действиями.</span><span class="sxs-lookup"><span data-stu-id="79c33-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="79c33-113">Учитывая все это, вы сможете более эффективно создавать и обслуживать веб-приложения, используя преимущества новейших функций ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="79c33-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="79c33-114">Все примеры кода и фрагментов включены в комплект обучающих курсов Web Camp, доступный в [выпусках Microsoft Web/вебкамптраинингкит](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="79c33-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="79c33-115">Проект, относящийся к этой лабораторной работе, доступен по адресу [ASP.NET MVC 4 Entity Framework формирования шаблонов и миграций](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span><span class="sxs-lookup"><span data-stu-id="79c33-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="79c33-116">Цели</span><span class="sxs-lookup"><span data-stu-id="79c33-116">Objectives</span></span>

<span data-ttu-id="79c33-117">В этой практической лабораторной работе вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="79c33-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="79c33-118">Для операций CRUD на контроллерах используйте формирование шаблонов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="79c33-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="79c33-119">Измените модель базы данных с помощью Entity Framework миграции.</span><span class="sxs-lookup"><span data-stu-id="79c33-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="79c33-120">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="79c33-120">Prerequisites</span></span>

<span data-ttu-id="79c33-121">Для выполнения этой лабораторной работы необходимо иметь следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="79c33-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="79c33-122">[Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или старше (см. [приложение а](#AppendixA) для получения инструкций по его установке).</span><span class="sxs-lookup"><span data-stu-id="79c33-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="79c33-123">Настройка</span><span class="sxs-lookup"><span data-stu-id="79c33-123">Setup</span></span>

<span data-ttu-id="79c33-124">**Установка фрагментов кода**</span><span class="sxs-lookup"><span data-stu-id="79c33-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="79c33-125">Для удобства большая часть кода, который вы будете управлять в этой лаборатории, доступна в виде фрагментов кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79c33-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="79c33-126">Чтобы установить фрагменты кода, запустите файл **.\саурце\сетуп\кодесниппетс.ВСИ** .</span><span class="sxs-lookup"><span data-stu-id="79c33-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="79c33-127">Если вы не знакомы с фрагментами кода Visual Studio Code и хотите узнать, как их использовать, можно обратиться к приложению из этого документа &quot;[приложении б. Использование фрагментов кода](#AppendixB)&quot;.</span><span class="sxs-lookup"><span data-stu-id="79c33-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="79c33-128">Полнят</span><span class="sxs-lookup"><span data-stu-id="79c33-128">Exercises</span></span>

<span data-ttu-id="79c33-129">Это практическое лабораторное занятие состоит из следующих упражнений:</span><span class="sxs-lookup"><span data-stu-id="79c33-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="79c33-130">Использование формирования шаблонов ASP.NET MVC 4 с миграцией Entity Framework</span><span class="sxs-lookup"><span data-stu-id="79c33-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="79c33-131">Это упражнение сопровождается **конечной** папкой, содержащей итоговое решение, которое необходимо получить после завершения этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="79c33-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="79c33-132">Это решение можно использовать в качестве руководства, если требуется дополнительная помощь по работе с этим упражнением.</span><span class="sxs-lookup"><span data-stu-id="79c33-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>

<span data-ttu-id="79c33-133">Предполагаемое время выполнения этой лабораторной работы: **30 минут**</span><span class="sxs-lookup"><span data-stu-id="79c33-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="79c33-134">Упражнение 1. Использование шаблонов ASP.NET MVC 4 с миграцией Entity Framework</span><span class="sxs-lookup"><span data-stu-id="79c33-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="79c33-135">Формирование шаблонов MVC ASP.NET позволяет быстро создавать операции CRUD в стандартизированном виде, создавая необходимую логику, которая позволяет приложению взаимодействовать с уровнем базы данных.</span><span class="sxs-lookup"><span data-stu-id="79c33-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="79c33-136">В этом упражнении вы узнаете, как использовать формирование шаблонов ASP.NET MVC 4 с кодом First для создания методов CRUD.</span><span class="sxs-lookup"><span data-stu-id="79c33-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="79c33-137">Затем вы узнаете, как обновить модель, применяя изменения в базе данных, с помощью Entity Framework миграции.</span><span class="sxs-lookup"><span data-stu-id="79c33-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="79c33-138">Задача 1. Создание нового проекта ASP.NET MVC 4 с помощью формирования шаблонов</span><span class="sxs-lookup"><span data-stu-id="79c33-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="79c33-139">Если он еще не открыт, запустите **Visual Studio 2012**.</span><span class="sxs-lookup"><span data-stu-id="79c33-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="79c33-140">Выберите **файл | Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="79c33-140">Select **File | New Project**.</span></span> <span data-ttu-id="79c33-141">В диалоговом окне Новый проект в **визуальном C# элементе |** В разделе "веб-приложение" выберите **ASP.NET MVC 4 Web Application**.</span><span class="sxs-lookup"><span data-stu-id="79c33-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="79c33-142">Присвойте проекту имя **MVC4andEFMigrations** и задайте в качестве расположения папку **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** этой лабораторной работы.</span><span class="sxs-lookup"><span data-stu-id="79c33-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="79c33-143">Задайте для параметра **имя решения** значение **Начало** и убедитесь, что установлен флажок **создать каталог для решения** .</span><span class="sxs-lookup"><span data-stu-id="79c33-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="79c33-144">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="79c33-144">Click **OK**.</span></span>

    <span data-ttu-id="79c33-145">![Диалоговое окно "Создание проекта ASP.NET MVC 4"](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "Диалоговое окно "Создание проекта ASP.NET MVC 4"")</span><span class="sxs-lookup"><span data-stu-id="79c33-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="79c33-146">*Диалоговое окно "Создание проекта ASP.NET MVC 4"*</span><span class="sxs-lookup"><span data-stu-id="79c33-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="79c33-147">В диалоговом окне **Новый проект ASP.NET MVC 4** выберите шаблон **Интернет-приложение** и убедитесь, что **Razor** является выбранным **обработчиком представлений**.</span><span class="sxs-lookup"><span data-stu-id="79c33-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="79c33-148">Чтобы создать проект, нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="79c33-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="79c33-149">![Новое Интернет – приложение ASP.NET MVC 4](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "Новое Интернет – приложение ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="79c33-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="79c33-150">*Новое Интернет – приложение ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="79c33-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="79c33-151">В обозреватель решений щелкните правой кнопкой мыши элемент **модели** и выберите команду **Добавить | Класс** для создания простого класса Person (POCO).</span><span class="sxs-lookup"><span data-stu-id="79c33-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="79c33-152">Присвойте ему имя **Person** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="79c33-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="79c33-153">Откройте класс Person и вставьте следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="79c33-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="79c33-154">(Фрагмент кода — *ASP.NET MVC 4 и Entity Framework, EX1 свойства Person*)</span><span class="sxs-lookup"><span data-stu-id="79c33-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. <span data-ttu-id="79c33-155">Щелкните " **Сборка" | Создайте решение** для сохранения изменений и сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="79c33-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="79c33-156">![Сборка приложения](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Построение приложения")</span><span class="sxs-lookup"><span data-stu-id="79c33-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="79c33-157">*Сборка приложения*</span><span class="sxs-lookup"><span data-stu-id="79c33-157">*Building the Application*</span></span>
7. <span data-ttu-id="79c33-158">В обозреватель решений щелкните правой кнопкой мыши папку Controllers и выберите **Добавить | Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="79c33-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="79c33-159">Присвойте контроллеру имя *персонконтроллер* и выполните **Параметры формирования шаблонов** со следующими значениями.</span><span class="sxs-lookup"><span data-stu-id="79c33-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

   1. <span data-ttu-id="79c33-160">В раскрывающемся списке **шаблон** выберите **контроллер MVC с действиями чтения и записи и представлениями с помощью параметра Entity Framework** .</span><span class="sxs-lookup"><span data-stu-id="79c33-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
   2. <span data-ttu-id="79c33-161">В раскрывающемся списке **класс модели** выберите класс **Person** .</span><span class="sxs-lookup"><span data-stu-id="79c33-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
   3. <span data-ttu-id="79c33-162">В списке **класс контекста данных** выберите **&lt;новый контекст данных...&gt;** .</span><span class="sxs-lookup"><span data-stu-id="79c33-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="79c33-163">Выберите любое имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="79c33-163">Choose any name and click **OK**.</span></span>
   4. <span data-ttu-id="79c33-164">Убедитесь, что в раскрывающемся списке **представления** выбран параметр **Razor** .</span><span class="sxs-lookup"><span data-stu-id="79c33-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

      <span data-ttu-id="79c33-165">![Добавление контроллера Person с формированием шаблонов](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Добавление контроллера Person с формированием шаблонов")</span><span class="sxs-lookup"><span data-stu-id="79c33-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

      <span data-ttu-id="79c33-166">*Добавление контроллера Person с формированием шаблонов*</span><span class="sxs-lookup"><span data-stu-id="79c33-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="79c33-167">Нажмите кнопку **Добавить** , чтобы создать новый контроллер для пользователя с формированием шаблонов.</span><span class="sxs-lookup"><span data-stu-id="79c33-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="79c33-168">Вы создали действия контроллера, а также представления.</span><span class="sxs-lookup"><span data-stu-id="79c33-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="79c33-169">![После создания контроллера Person с формированием шаблонов](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "После создания контроллера Person с формированием шаблонов")</span><span class="sxs-lookup"><span data-stu-id="79c33-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="79c33-170">*После создания контроллера Person с формированием шаблонов*</span><span class="sxs-lookup"><span data-stu-id="79c33-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="79c33-171">Откройте класс **персонконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="79c33-171">Open **PersonController** class.</span></span> <span data-ttu-id="79c33-172">Обратите внимание, что все методы действия CRUD были созданы автоматически.</span><span class="sxs-lookup"><span data-stu-id="79c33-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

   <span data-ttu-id="79c33-173">![Внутри контроллера Person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Внутри контроллера Person")</span><span class="sxs-lookup"><span data-stu-id="79c33-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

   <span data-ttu-id="79c33-174">*Внутри контроллера Person*</span><span class="sxs-lookup"><span data-stu-id="79c33-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="79c33-175">Задача 2. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="79c33-175">Task 2- Running the application</span></span>

<span data-ttu-id="79c33-176">На этом этапе база данных еще не создана.</span><span class="sxs-lookup"><span data-stu-id="79c33-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="79c33-177">В этой задаче вы запустите приложение в первый раз и проверите операции CRUD.</span><span class="sxs-lookup"><span data-stu-id="79c33-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="79c33-178">База данных будет создана на лету с Code First.</span><span class="sxs-lookup"><span data-stu-id="79c33-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="79c33-179">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="79c33-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="79c33-180">В браузере добавьте **/персон** в URL-адрес, чтобы открыть страницу Person.</span><span class="sxs-lookup"><span data-stu-id="79c33-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="79c33-181">![Первый запуск приложения](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Первый запуск приложения")</span><span class="sxs-lookup"><span data-stu-id="79c33-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="79c33-182">*Приложение: первый запуск*</span><span class="sxs-lookup"><span data-stu-id="79c33-182">*Application: first run*</span></span>
3. <span data-ttu-id="79c33-183">Теперь вы просматриваете страницы Person и протестируете операции CRUD.</span><span class="sxs-lookup"><span data-stu-id="79c33-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="79c33-184">Щелкните **создать** , чтобы добавить нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="79c33-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="79c33-185">Введите имя и фамилию и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="79c33-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="79c33-186">![Добавление нового пользователя](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Добавление нового пользователя")</span><span class="sxs-lookup"><span data-stu-id="79c33-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="79c33-187">*Добавление нового пользователя*</span><span class="sxs-lookup"><span data-stu-id="79c33-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="79c33-188">В списке людей можно удалять, изменять и добавлять элементы.</span><span class="sxs-lookup"><span data-stu-id="79c33-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="79c33-189">![список лиц](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "список лиц")</span><span class="sxs-lookup"><span data-stu-id="79c33-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="79c33-190">*Список лиц*</span><span class="sxs-lookup"><span data-stu-id="79c33-190">*Person list*</span></span>
    3. <span data-ttu-id="79c33-191">Щелкните **сведения** , чтобы открыть сведения о лице.</span><span class="sxs-lookup"><span data-stu-id="79c33-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="79c33-192">![Сведения о лице](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Сведения о лице")</span><span class="sxs-lookup"><span data-stu-id="79c33-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="79c33-193">*Сведения о лице*</span><span class="sxs-lookup"><span data-stu-id="79c33-193">*Person's details*</span></span>
4. <span data-ttu-id="79c33-194">Закройте браузер и вернитесь в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79c33-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="79c33-195">Обратите внимание, что вы создали всю CRUD для сущности Person в приложении — от модели до представлений — без необходимости писать одну строку кода!</span><span class="sxs-lookup"><span data-stu-id="79c33-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="79c33-196">Задача 3. обновление базы данных с помощью Entity Framework миграции</span><span class="sxs-lookup"><span data-stu-id="79c33-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="79c33-197">В этой задаче будет обновлена база данных с помощью Entity Framework миграций.</span><span class="sxs-lookup"><span data-stu-id="79c33-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="79c33-198">Вы узнаете, как просто изменить модель и отразить изменения в базах данных с помощью функции миграции Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="79c33-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="79c33-199">Откройте консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="79c33-199">Open the Package Manager Console.</span></span> <span data-ttu-id="79c33-200">Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="79c33-200">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="79c33-201">В консоли диспетчера пакетов введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="79c33-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="79c33-202">PMC</span><span class="sxs-lookup"><span data-stu-id="79c33-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="79c33-203">![Включение миграции](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Включение миграций")</span><span class="sxs-lookup"><span data-stu-id="79c33-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="79c33-204">*Включение миграции*</span><span class="sxs-lookup"><span data-stu-id="79c33-204">*Enabling migrations*</span></span>

    <span data-ttu-id="79c33-205">Команда Enable-Migration создает папку **migrations** , которая содержит скрипт для инициализации базы данных.</span><span class="sxs-lookup"><span data-stu-id="79c33-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="79c33-206">![Папка "миграции"](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Папка "миграции"")</span><span class="sxs-lookup"><span data-stu-id="79c33-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="79c33-207">*Папка "миграции"*</span><span class="sxs-lookup"><span data-stu-id="79c33-207">*Migrations folder*</span></span>
3. <span data-ttu-id="79c33-208">Откройте файл **Configuration.CS** в папке migrations.</span><span class="sxs-lookup"><span data-stu-id="79c33-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="79c33-209">Перейдите к конструктору класса и измените значение **аутоматикмигратионсенаблед** на *true*.</span><span class="sxs-lookup"><span data-stu-id="79c33-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. <span data-ttu-id="79c33-210">Откройте класс Person и добавьте атрибут для отчества человека.</span><span class="sxs-lookup"><span data-stu-id="79c33-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="79c33-211">С помощью этого нового атрибута вы изменяете модель.</span><span class="sxs-lookup"><span data-stu-id="79c33-211">With this new attribute, you are changing the model.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. <span data-ttu-id="79c33-212">Выбор **сборки | Создайте решение** в меню, чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="79c33-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="79c33-213">![Сборка приложения](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Построение приложения")</span><span class="sxs-lookup"><span data-stu-id="79c33-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="79c33-214">*Сборка приложения*</span><span class="sxs-lookup"><span data-stu-id="79c33-214">*Building the application*</span></span>
6. <span data-ttu-id="79c33-215">В консоли диспетчера пакетов введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="79c33-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="79c33-216">PMC</span><span class="sxs-lookup"><span data-stu-id="79c33-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="79c33-217">Эта команда выполнит поиск изменений в объектах данных, а затем добавит необходимые команды, чтобы соответствующим образом изменить базу данных.</span><span class="sxs-lookup"><span data-stu-id="79c33-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="79c33-218">![Добавление отчества](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Добавление отчества")</span><span class="sxs-lookup"><span data-stu-id="79c33-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="79c33-219">*Добавление отчества*</span><span class="sxs-lookup"><span data-stu-id="79c33-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="79c33-220">Используемых Можно выполнить следующую команду, чтобы создать скрипт SQL с разностным обновлением.</span><span class="sxs-lookup"><span data-stu-id="79c33-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="79c33-221">Это позволит обновить базу данных вручную (в данном случае это необязательно) или применить изменения в других базах данных:</span><span class="sxs-lookup"><span data-stu-id="79c33-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="79c33-222">PMC</span><span class="sxs-lookup"><span data-stu-id="79c33-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="79c33-223">![Создание скрипта SQL](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Формирование скрипта SQL")</span><span class="sxs-lookup"><span data-stu-id="79c33-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="79c33-224">*Создание скрипта SQL*</span><span class="sxs-lookup"><span data-stu-id="79c33-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="79c33-225">![Обновление скрипта SQL](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "Обновление скрипта SQL")</span><span class="sxs-lookup"><span data-stu-id="79c33-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="79c33-226">*Обновление скрипта SQL*</span><span class="sxs-lookup"><span data-stu-id="79c33-226">*SQL Script update*</span></span>
8. <span data-ttu-id="79c33-227">В консоли диспетчера пакетов введите следующую команду, чтобы обновить базу данных:</span><span class="sxs-lookup"><span data-stu-id="79c33-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="79c33-228">PMC</span><span class="sxs-lookup"><span data-stu-id="79c33-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="79c33-229">![Обновление базы данных](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Обновление базы данных")</span><span class="sxs-lookup"><span data-stu-id="79c33-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="79c33-230">*Обновление базы данных*</span><span class="sxs-lookup"><span data-stu-id="79c33-230">*Updating the Database*</span></span>

    <span data-ttu-id="79c33-231">Это приведет к добавлению столбца **MiddleName** в таблицу **People** в соответствии с текущим определением класса **Person** .</span><span class="sxs-lookup"><span data-stu-id="79c33-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="79c33-232">После обновления базы данных щелкните правой кнопкой мыши папку контроллера и выберите **Добавить | Контроллер** для повторного добавления контроллера Person (с теми же значениями).</span><span class="sxs-lookup"><span data-stu-id="79c33-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="79c33-233">При этом будут обновлены существующие методы и представления, добавляющие новый атрибут.</span><span class="sxs-lookup"><span data-stu-id="79c33-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="79c33-234">![Добавление обновления контроллера](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Добавление обновления контроллера")</span><span class="sxs-lookup"><span data-stu-id="79c33-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="79c33-235">*Обновление контроллера*</span><span class="sxs-lookup"><span data-stu-id="79c33-235">*Updating the controller*</span></span>
10. <span data-ttu-id="79c33-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="79c33-236">Click **Add**.</span></span> <span data-ttu-id="79c33-237">Затем выберите значения **Перезаписать PersonController.CS** и **Перезапись связанных представлений** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="79c33-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

   ![Добавление перезаписи контроллера](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   <span data-ttu-id="79c33-239">*Обновление контроллера*</span><span class="sxs-lookup"><span data-stu-id="79c33-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="79c33-240">Task4 — запуск приложения</span><span class="sxs-lookup"><span data-stu-id="79c33-240">Task4- Running the application</span></span>

1. <span data-ttu-id="79c33-241">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="79c33-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="79c33-242">Откройте **/персон**.</span><span class="sxs-lookup"><span data-stu-id="79c33-242">Open **/Person**.</span></span> <span data-ttu-id="79c33-243">Обратите внимание, что данные были сохранены, а столбец отчества был добавлен.</span><span class="sxs-lookup"><span data-stu-id="79c33-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="79c33-244">![Отчество Добавлено](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Отчество Добавлено")</span><span class="sxs-lookup"><span data-stu-id="79c33-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="79c33-245">*Отчество Добавлено*</span><span class="sxs-lookup"><span data-stu-id="79c33-245">*Middle Name added*</span></span>
3. <span data-ttu-id="79c33-246">Если нажать кнопку **изменить**, вы сможете добавить отчество к текущему человеку.</span><span class="sxs-lookup"><span data-stu-id="79c33-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="79c33-247">![Выпуск отчества](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Выпуск отчества")</span><span class="sxs-lookup"><span data-stu-id="79c33-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="79c33-248">Сводка</span><span class="sxs-lookup"><span data-stu-id="79c33-248">Summary</span></span>

<span data-ttu-id="79c33-249">В этой практической лабораторной работе вы узнали простые действия по созданию операций CRUD с помощью формирования шаблонов ASP.NET MVC 4 с использованием любого класса модели.</span><span class="sxs-lookup"><span data-stu-id="79c33-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="79c33-250">Затем вы узнали, как выполнить комплексное обновление в приложении — из базы данных в представления, используя Entity Framework миграции.</span><span class="sxs-lookup"><span data-stu-id="79c33-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="79c33-251">Приложение а. Установка Visual Studio Express 2012 для Web</span><span class="sxs-lookup"><span data-stu-id="79c33-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="79c33-252">Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версии с помощью **[установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="79c33-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="79c33-253">Следующие инструкции помогут вам выполнить действия, необходимые для установки *Visual Studio Express 2012 для Web* с помощью *установщик веб-платформы Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="79c33-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="79c33-254">Перейдите на сайт [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="79c33-254">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="79c33-255">Кроме того, если у вас уже установлен установщик веб-платформы, вы можете открыть его и найти продукт &quot;<em>Visual Studio Express 2012 для Web с Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="79c33-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="79c33-256">Щелкните **Install Now (установить сейчас**).</span><span class="sxs-lookup"><span data-stu-id="79c33-256">Click on **Install Now**.</span></span> <span data-ttu-id="79c33-257">Если у вас нет **установщика веб-платформы** , вы будете сначала перенаправлены на загрузку и установку.</span><span class="sxs-lookup"><span data-stu-id="79c33-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="79c33-258">После открытия **установщика веб-платформы** нажмите кнопку **установить** , чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="79c33-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="79c33-259">![Установка Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Установка Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="79c33-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="79c33-260">*Установка Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="79c33-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="79c33-261">Прочитайте все лицензии и условия продуктов и нажмите кнопку " **принять** ", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="79c33-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Принятие условий лицензии](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="79c33-263">*Принятие условий лицензии*</span><span class="sxs-lookup"><span data-stu-id="79c33-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="79c33-264">Дождитесь завершения процесса загрузки и установки.</span><span class="sxs-lookup"><span data-stu-id="79c33-264">Wait until the downloading and installation process completes.</span></span>

    ![Ход установки](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="79c33-266">*Ход установки*</span><span class="sxs-lookup"><span data-stu-id="79c33-266">*Installation progress*</span></span>
6. <span data-ttu-id="79c33-267">После завершения установки нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="79c33-267">When the installation completes, click **Finish**.</span></span>

    ![Установка завершена](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="79c33-269">*Установка завершена*</span><span class="sxs-lookup"><span data-stu-id="79c33-269">*Installation completed*</span></span>
7. <span data-ttu-id="79c33-270">Нажмите кнопку **выход** , чтобы закрыть установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="79c33-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="79c33-271">Чтобы открыть Visual Studio Express для Интернета, перейдите на **начальный** экран и начните запись &quot;**VS Express**&quot;, а затем щелкните плитку **VS Express для Web** .</span><span class="sxs-lookup"><span data-stu-id="79c33-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Плитка VS Express для Web](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="79c33-273">*Плитка VS Express для Web*</span><span class="sxs-lookup"><span data-stu-id="79c33-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="79c33-274">Приложение б. Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="79c33-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="79c33-275">С помощью фрагментов кода вы можете получить все необходимые вам коды.</span><span class="sxs-lookup"><span data-stu-id="79c33-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="79c33-276">В лабораторном документе вы узнаете, когда можно использовать их, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="79c33-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="79c33-277">![Использование фрагментов кода Visual Studio для вставки кода в проект](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Использование фрагментов кода Visual Studio для вставки кода в проект")</span><span class="sxs-lookup"><span data-stu-id="79c33-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="79c33-278">*Использование фрагментов кода Visual Studio для вставки кода в проект*</span><span class="sxs-lookup"><span data-stu-id="79c33-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="79c33-279">***Добавление фрагмента кода с помощью клавиатуры (C# только)***</span><span class="sxs-lookup"><span data-stu-id="79c33-279">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="79c33-280">Поместите курсор в то место, куда вы хотите вставить код.</span><span class="sxs-lookup"><span data-stu-id="79c33-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="79c33-281">Начните вводить имя фрагмента (без пробелов или дефисов).</span><span class="sxs-lookup"><span data-stu-id="79c33-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="79c33-282">Посмотрите, как IntelliSense отображает соответствующие имена фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="79c33-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="79c33-283">Выберите правильный фрагмент кода (или вводите его, пока не будет выбрано имя всего фрагмента).</span><span class="sxs-lookup"><span data-stu-id="79c33-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="79c33-284">Дважды нажмите клавишу TAB, чтобы вставить фрагмент в позицию курсора.</span><span class="sxs-lookup"><span data-stu-id="79c33-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="79c33-285">![Начните вводить имя фрагмента](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Начните вводить имя фрагмента")</span><span class="sxs-lookup"><span data-stu-id="79c33-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="79c33-286">*Начните вводить имя фрагмента*</span><span class="sxs-lookup"><span data-stu-id="79c33-286">*Start typing the snippet name*</span></span>

<span data-ttu-id="79c33-287">![Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="79c33-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="79c33-288">*Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="79c33-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="79c33-289">![Снова нажмите клавишу TAB, и фрагмент развернется](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Снова нажмите клавишу TAB, и фрагмент развернется")</span><span class="sxs-lookup"><span data-stu-id="79c33-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="79c33-290">*Снова нажмите клавишу TAB, и фрагмент развернется*</span><span class="sxs-lookup"><span data-stu-id="79c33-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="79c33-291">***Добавление фрагмента кода с помощью мыши (C#, Visual Basic и XML)*** одного.</span><span class="sxs-lookup"><span data-stu-id="79c33-291">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="79c33-292">Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="79c33-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="79c33-293">Выберите **Вставить фрагмент** , за которым следуют **фрагменты кода**.</span><span class="sxs-lookup"><span data-stu-id="79c33-293">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="79c33-294">Выберите соответствующий фрагмент из списка, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="79c33-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="79c33-295">![Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="79c33-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="79c33-296">*Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="79c33-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="79c33-297">![Выберите соответствующий фрагмент из списка, щелкнув его.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Выберите соответствующий фрагмент из списка, щелкнув его.")</span><span class="sxs-lookup"><span data-stu-id="79c33-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="79c33-298">*Выберите соответствующий фрагмент из списка, щелкнув его.*</span><span class="sxs-lookup"><span data-stu-id="79c33-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>
