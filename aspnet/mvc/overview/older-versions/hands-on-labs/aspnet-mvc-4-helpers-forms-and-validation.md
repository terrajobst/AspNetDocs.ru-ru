---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: Вспомогательные методы, формы и проверка ASP.NET MVC 4 | Документация Майкрософт
author: rick-anderson
description: В модели ASP.NET MVC 4 и практическом занятии доступа к данным вы загрузили и выводите данные из базы данных. В этой практической лабораторной работе вы добавите в...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433794"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="f1837-104">Вспомогательные приложения, формы и проверка в ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f1837-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="f1837-105">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="f1837-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="f1837-106">Скачать обучающий комплект Web Camp</span><span class="sxs-lookup"><span data-stu-id="f1837-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="f1837-107">В **модели ASP.NET MVC 4 и** практическом занятии доступа к данным вы загрузили и выводите данные из базы данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="f1837-108">В этой практической лабораторной работе вы добавите в приложение **музыкального магазина** возможность редактирования этих данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="f1837-109">С учетом этой цели вы сначала создадите контроллер, который будет поддерживать действия создания, чтения, обновления и удаления (CRUD) альбомов.</span><span class="sxs-lookup"><span data-stu-id="f1837-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="f1837-110">Вы создадите шаблон представления индекса, используя преимущества функции формирования шаблонов ASP.NET MVC для отображения свойств альбомов в таблице HTML.</span><span class="sxs-lookup"><span data-stu-id="f1837-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="f1837-111">Чтобы улучшить это представление, необходимо добавить пользовательский вспомогательный метод HTML, который будет усекать длинные описания.</span><span class="sxs-lookup"><span data-stu-id="f1837-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="f1837-112">После этого будут добавлены представления Edit и CREATE, позволяющие изменять альбомы в базе данных с помощью элементов формы, таких как раскрывающиеся списки.</span><span class="sxs-lookup"><span data-stu-id="f1837-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="f1837-113">Наконец, пользователи смогут удалить альбом, а также запретить им вводить неверные данные, проверив их ввод.</span><span class="sxs-lookup"><span data-stu-id="f1837-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="f1837-114">В этой практической лабораторной работе предполагается, что у вас есть базовые знания о **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="f1837-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="f1837-115">Если вы ранее не использовали **ASP.NET MVC** , мы рекомендуем вам перейти на практический семинар **ASP.NET MVC** .</span><span class="sxs-lookup"><span data-stu-id="f1837-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="f1837-116">Эта лабораторная работа посвящена усовершенствованиям и новым функциям, описанным выше, путем применения незначительных изменений в образце веб-приложения, предоставленном в исходной папке.</span><span class="sxs-lookup"><span data-stu-id="f1837-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="f1837-117">Все примеры кода и фрагментов включены в набор средств для обучения Web Camp, доступный в [выпусках Microsoft-Web/вебкамптраинингкит](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="f1837-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="f1837-118">Проект, относящийся к этой лабораторной работе [, доступен по ASP.NETам, формам и проверке в MVC 4](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span><span class="sxs-lookup"><span data-stu-id="f1837-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="f1837-119">Цели</span><span class="sxs-lookup"><span data-stu-id="f1837-119">Objectives</span></span>

<span data-ttu-id="f1837-120">В этой практической лабораторной работе вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="f1837-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="f1837-121">Создание контроллера для поддержки операций CRUD</span><span class="sxs-lookup"><span data-stu-id="f1837-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="f1837-122">Создание представления индекса для отображения свойств сущности в таблице HTML</span><span class="sxs-lookup"><span data-stu-id="f1837-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="f1837-123">Добавление пользовательского вспомогательного метода HTML</span><span class="sxs-lookup"><span data-stu-id="f1837-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="f1837-124">Создание и Настройка представления редактирования</span><span class="sxs-lookup"><span data-stu-id="f1837-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="f1837-125">Отличить методы действий, реагирующие на вызовы HTTP-GET или HTTP-POST</span><span class="sxs-lookup"><span data-stu-id="f1837-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="f1837-126">Добавление и Настройка представления создания</span><span class="sxs-lookup"><span data-stu-id="f1837-126">Add and customize a Create View</span></span>
- <span data-ttu-id="f1837-127">Обработку удаления сущности</span><span class="sxs-lookup"><span data-stu-id="f1837-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="f1837-128">Проверка вводимых пользователем данных</span><span class="sxs-lookup"><span data-stu-id="f1837-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f1837-129">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f1837-129">Prerequisites</span></span>

<span data-ttu-id="f1837-130">Для выполнения этой лабораторной работы необходимо иметь следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="f1837-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="f1837-131">[Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или старше (см. [приложение а](#AppendixA) для получения инструкций по его установке).</span><span class="sxs-lookup"><span data-stu-id="f1837-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f1837-132">Настройка</span><span class="sxs-lookup"><span data-stu-id="f1837-132">Setup</span></span>

<span data-ttu-id="f1837-133">**Установка фрагментов кода**</span><span class="sxs-lookup"><span data-stu-id="f1837-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="f1837-134">Для удобства большая часть кода, который вы будете управлять в этой лаборатории, доступна в виде фрагментов кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1837-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="f1837-135">Чтобы установить фрагменты кода, запустите файл **.\саурце\сетуп\кодесниппетс.ВСИ** .</span><span class="sxs-lookup"><span data-stu-id="f1837-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="f1837-136">Если вы не знакомы с фрагментами кода Visual Studio Code и хотите узнать, как их использовать, можно обратиться к приложению из этого документа &quot;[приложении б. Использование фрагментов кода](#AppendixB)&quot;.</span><span class="sxs-lookup"><span data-stu-id="f1837-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f1837-137">Полнят</span><span class="sxs-lookup"><span data-stu-id="f1837-137">Exercises</span></span>

<span data-ttu-id="f1837-138">Эта практическая лабораторная работа состоит из следующих упражнений:</span><span class="sxs-lookup"><span data-stu-id="f1837-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="f1837-139">Создание контроллера диспетчера хранилища и его представления индекса</span><span class="sxs-lookup"><span data-stu-id="f1837-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="f1837-140">Добавление вспомогательного метода HTML</span><span class="sxs-lookup"><span data-stu-id="f1837-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="f1837-141">Создание представления редактирования</span><span class="sxs-lookup"><span data-stu-id="f1837-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="f1837-142">Добавление представления создания</span><span class="sxs-lookup"><span data-stu-id="f1837-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="f1837-143">Обработка удаления</span><span class="sxs-lookup"><span data-stu-id="f1837-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="f1837-144">Добавление проверки</span><span class="sxs-lookup"><span data-stu-id="f1837-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="f1837-145">Использование ненавязчивой jQuery на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="f1837-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="f1837-146">Каждое упражнение сопровождается **конечной** папкой, содержащей итоговое решение, которое следует получить после завершения упражнений.</span><span class="sxs-lookup"><span data-stu-id="f1837-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="f1837-147">Это решение можно использовать в качестве инструкции, если вам нужна дополнительная помощь по работе с упражнениями.</span><span class="sxs-lookup"><span data-stu-id="f1837-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="f1837-148">Предполагаемое время выполнения этой лабораторной работы: **60 минут**</span><span class="sxs-lookup"><span data-stu-id="f1837-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="f1837-149">Упражнение 1. Создание контроллера диспетчера хранилища и его представления индекса</span><span class="sxs-lookup"><span data-stu-id="f1837-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="f1837-150">В этом упражнении вы узнаете, как создать новый контроллер для поддержки операций CRUD, настроить метод действия с индексами для возврата списка альбомов из базы данных и, наконец, создать шаблон представления индекса, используя преимущества формирования шаблонов MVC ASP.NET. Функция для вывода свойств альбомов в таблице HTML.</span><span class="sxs-lookup"><span data-stu-id="f1837-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="f1837-151">Задача 1. Создание Стореманажерконтроллер</span><span class="sxs-lookup"><span data-stu-id="f1837-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="f1837-152">В этой задаче вы создадите новый контроллер с именем **стореманажерконтроллер** для поддержки операций CRUD.</span><span class="sxs-lookup"><span data-stu-id="f1837-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="f1837-153">Откройте **Начальное** решение, расположенное по адресу **Source/EX1-креатингсестореманажерконтроллер/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f1837-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="f1837-154">Перед продолжением необходимо загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1837-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f1837-155">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f1837-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f1837-156">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f1837-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f1837-157">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="f1837-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f1837-158">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f1837-159">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f1837-160">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1837-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f1837-161">Добавьте новый контроллер.</span><span class="sxs-lookup"><span data-stu-id="f1837-161">Add a new controller.</span></span> <span data-ttu-id="f1837-162">Для этого щелкните правой кнопкой мыши папку **Controllers** в Обозреватель решений, выберите **Добавить** , а затем — команду **контроллер** .</span><span class="sxs-lookup"><span data-stu-id="f1837-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="f1837-163">Измените имя **контроллера** на **стореманажерконтроллер** и убедитесь, что выбран параметр **контроллер MVC с пустыми действиями чтения и записи** .</span><span class="sxs-lookup"><span data-stu-id="f1837-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="f1837-164">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1837-164">Click **Add**.</span></span>

    <span data-ttu-id="f1837-165">![Диалоговое окно добавления контроллера](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Диалоговое окно добавления контроллера")</span><span class="sxs-lookup"><span data-stu-id="f1837-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="f1837-166">*Диалоговое окно добавления контроллера*</span><span class="sxs-lookup"><span data-stu-id="f1837-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="f1837-167">Создается новый класс контроллера.</span><span class="sxs-lookup"><span data-stu-id="f1837-167">A new Controller class is generated.</span></span> <span data-ttu-id="f1837-168">Так как вы указали, как добавлять действия для чтения и записи, методы-заглушки для таких, общие действия CRUD создаются с заполненными комментариями TODO, предлагающими включить логику конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="f1837-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="f1837-169">Задача 2. Настройка индекса Стореманажер</span><span class="sxs-lookup"><span data-stu-id="f1837-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="f1837-170">В этой задаче вы настроите метод действия индекса Стореманажер, чтобы возвращалось представление со списком альбомов из базы данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="f1837-171">В классе Стореманажерконтроллер добавьте следующие директивы *using* .</span><span class="sxs-lookup"><span data-stu-id="f1837-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="f1837-172">(Фрагмент кода — *вспомогательные средства и формы ASP.NET MVC 4 и проверка — EX1 с использованием мвкмусиксторе*)</span><span class="sxs-lookup"><span data-stu-id="f1837-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="f1837-173">Добавьте поле в **стореманажерконтроллер** для хранения экземпляра **мусиксторинтитиес.**</span><span class="sxs-lookup"><span data-stu-id="f1837-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="f1837-174">(Фрагмент кода — *вспомогательные функции и формы ASP.NET MVC 4 и проверка — EX1 мусиксторинтитиес*)</span><span class="sxs-lookup"><span data-stu-id="f1837-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="f1837-175">Реализуйте действие индекса Стореманажерконтроллер, чтобы вернуть представление со списком альбомов.</span><span class="sxs-lookup"><span data-stu-id="f1837-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="f1837-176">Логика действия контроллера будет очень похожа на действие индекса Стореконтроллер, написанное ранее.</span><span class="sxs-lookup"><span data-stu-id="f1837-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="f1837-177">Используйте LINQ для получения всех альбомов, включая сведения о жанрах и исполнителях для показа.</span><span class="sxs-lookup"><span data-stu-id="f1837-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="f1837-178">(Фрагмент кода — *вспомогательные функции и формы ASP.NET MVC 4 и проверка — EX1 Стореманажерконтроллер index*)</span><span class="sxs-lookup"><span data-stu-id="f1837-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="f1837-179">Задача 3. Создание представления индекса</span><span class="sxs-lookup"><span data-stu-id="f1837-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="f1837-180">В этой задаче будет создан шаблон представления индекса для отображения списка альбомов, возвращаемых контроллером **стореманажер** .</span><span class="sxs-lookup"><span data-stu-id="f1837-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="f1837-181">Перед созданием нового шаблона представления необходимо выполнить сборку проекта, чтобы **диалоговое окно добавления представления** знало о том, какой класс **альбома** будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="f1837-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="f1837-182">Выбор **сборки | Создайте Мвкмусиксторе** для сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="f1837-183">Щелкните правой кнопкой мыши внутри метода действия **индекса** и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="f1837-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="f1837-184">Откроется диалоговое окно **Добавление представления** .</span><span class="sxs-lookup"><span data-stu-id="f1837-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="f1837-185">![Добавить представление](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Добавить представление")</span><span class="sxs-lookup"><span data-stu-id="f1837-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="f1837-186">*Добавление представления из метода index*</span><span class="sxs-lookup"><span data-stu-id="f1837-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="f1837-187">В диалоговом окне Добавление представления убедитесь, что имя представления — **index**.</span><span class="sxs-lookup"><span data-stu-id="f1837-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="f1837-188">Выберите параметр **создать строго типизированное представление** и в раскрывающемся списке **класс модели** выберите **альбом (мвкмусиксторе. Models)** .</span><span class="sxs-lookup"><span data-stu-id="f1837-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="f1837-189">Выберите **список** из раскрывающегося списка **шаблон шаблонов** .</span><span class="sxs-lookup"><span data-stu-id="f1837-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="f1837-190">Оставьте для **обработчика представлений** **Razor** , а для других полей — значение по умолчанию, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1837-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="f1837-191">![Добавление представления индекса](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Добавление представления индекса")</span><span class="sxs-lookup"><span data-stu-id="f1837-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="f1837-192">*Добавление представления индекса*</span><span class="sxs-lookup"><span data-stu-id="f1837-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="f1837-193">Задача 4. Настройка формирования шаблонов представления индекса</span><span class="sxs-lookup"><span data-stu-id="f1837-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="f1837-194">В этой задаче вы настроите шаблон простого представления, созданный с помощью функции формирования шаблонов ASP.NET MVC, чтобы отображать нужные вам поля.</span><span class="sxs-lookup"><span data-stu-id="f1837-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="f1837-195">Поддержка **формирования шаблонов** в ASP.NET MVC создает простой шаблон представления, в котором перечислены все поля в модели альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="f1837-196">**Формирование шаблонов** позволяет быстро приступить к работе со строго типизированным представлением: вместо того, чтобы создавать шаблон представления вручную, формирование шаблонов быстро создает шаблон по умолчанию, а затем можно изменить созданный код.</span><span class="sxs-lookup"><span data-stu-id="f1837-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>

1. <span data-ttu-id="f1837-197">Проверьте созданный код.</span><span class="sxs-lookup"><span data-stu-id="f1837-197">Review the code created.</span></span> <span data-ttu-id="f1837-198">Созданный список полей будет входить в следующую таблицу HTML, которую использует **формирование шаблонов** для отображения табличных данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="f1837-199">Замените **таблицу&lt;&gt;** кодом следующим кодом, чтобы отображались только поля **жанра**, **исполнитель**, **Название альбома**и **Цена** .</span><span class="sxs-lookup"><span data-stu-id="f1837-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="f1837-200">Это приведет к удалению столбцов **URL-адресов** **албумид** и альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="f1837-201">Кроме того, он изменяет столбцы GenreId и Артистид, чтобы отображались связанные свойства класса **artist.Name** и **genre.Name**, и удаляет ссылку **Details** .</span><span class="sxs-lookup"><span data-stu-id="f1837-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="f1837-202">Измените следующие описания.</span><span class="sxs-lookup"><span data-stu-id="f1837-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="f1837-203">Задача 5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="f1837-204">В этой задаче будет протестировать, что шаблон представления **индекса** **стореманажер** отображает список альбомов в соответствии со структурой предыдущих шагов.</span><span class="sxs-lookup"><span data-stu-id="f1837-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="f1837-205">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-206">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-206">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-207">Измените URL-адрес на **/стореманажер** , чтобы убедиться, что список альбомов отображается, указывая **название**, **исполнителя** и **Жанр**.</span><span class="sxs-lookup"><span data-stu-id="f1837-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="f1837-208">![Просмотр списка альбомов](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Просмотр списка альбомов")</span><span class="sxs-lookup"><span data-stu-id="f1837-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="f1837-209">*Просмотр списка альбомов*</span><span class="sxs-lookup"><span data-stu-id="f1837-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="f1837-210">Упражнение 2. Добавление вспомогательного метода HTML</span><span class="sxs-lookup"><span data-stu-id="f1837-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="f1837-211">Страница индекса Стореманажер имеет одну потенциальную ошибку: свойства Title и имя исполнителя могут быть достаточно длинными, чтобы выпустить форматирование таблицы.</span><span class="sxs-lookup"><span data-stu-id="f1837-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="f1837-212">В этом упражнении вы узнаете, как добавить пользовательский вспомогательный метод HTML для усечения этого текста.</span><span class="sxs-lookup"><span data-stu-id="f1837-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="f1837-213">На следующем рисунке показано, как изменяется формат, так как длина текста при использовании небольшого размера браузера.</span><span class="sxs-lookup"><span data-stu-id="f1837-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="f1837-214">![Просмотр списка альбомов без усечения текста](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Просмотр списка альбомов без усечения текста")</span><span class="sxs-lookup"><span data-stu-id="f1837-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="f1837-215">*Просмотр списка альбомов без усечения текста*</span><span class="sxs-lookup"><span data-stu-id="f1837-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="f1837-216">Задача 1. расширение вспомогательного метода HTML</span><span class="sxs-lookup"><span data-stu-id="f1837-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="f1837-217">В этой задаче будет добавлен новый метод **Truncate** в **HTML-** объект, представленный в представлениях MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f1837-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="f1837-218">Для этого необходимо реализовать **метод расширения** для встроенного класса **System. Web. MVC. HtmlHelper** , предоставляемого ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f1837-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="f1837-219">Дополнительные сведения о **методах расширения**см. в этой статье MSDN.</span><span class="sxs-lookup"><span data-stu-id="f1837-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="f1837-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1837-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>

1. <span data-ttu-id="f1837-221">Откройте **Начальное** решение, расположенное по адресу **Source/EX2-аддинганхтмлхелпер/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f1837-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="f1837-222">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="f1837-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f1837-223">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1837-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f1837-224">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f1837-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f1837-225">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f1837-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f1837-226">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="f1837-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f1837-227">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f1837-228">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f1837-229">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1837-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f1837-230">Откройте представление индекса Стореманажер.</span><span class="sxs-lookup"><span data-stu-id="f1837-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="f1837-231">Для этого в обозреватель решений разверните папку **views** , а затем **стореманажер** и откройте файл **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="f1837-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="f1837-232">Добавьте следующий код под директивой <strong>@model</strong> , чтобы определить вспомогательный метод <strong>Truncate</strong> .</span><span class="sxs-lookup"><span data-stu-id="f1837-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="f1837-233">Задача 2. усечение текста на странице</span><span class="sxs-lookup"><span data-stu-id="f1837-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="f1837-234">В этой задаче будет использоваться метод **Truncate** для усечения текста в шаблоне представления.</span><span class="sxs-lookup"><span data-stu-id="f1837-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="f1837-235">Откройте представление индекса Стореманажер.</span><span class="sxs-lookup"><span data-stu-id="f1837-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="f1837-236">Для этого в обозреватель решений разверните папку **views** , а затем **стореманажер** и откройте файл **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="f1837-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="f1837-237">Замените строки, отображающие **имя исполнителя** и **название**альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="f1837-238">Для этого замените следующие строки.</span><span class="sxs-lookup"><span data-stu-id="f1837-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="f1837-239">Задача 3. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="f1837-240">В этой задаче будет протестировать, что шаблон представления **индекса** **Стореманажер** усекает название альбома и имя исполнителя.</span><span class="sxs-lookup"><span data-stu-id="f1837-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="f1837-241">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-242">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-242">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-243">Измените URL-адрес на **/стореманажер** , чтобы убедиться в усечении длинных текстов в столбце **Title** и **исполнитель** .</span><span class="sxs-lookup"><span data-stu-id="f1837-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="f1837-244">![Усеченные названия и имена исполнителей](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Усеченные названия и имена исполнителей")</span><span class="sxs-lookup"><span data-stu-id="f1837-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="f1837-245">*Усеченные заголовки и имена исполнителей*</span><span class="sxs-lookup"><span data-stu-id="f1837-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="f1837-246">Упражнение 3. Создание представления редактирования</span><span class="sxs-lookup"><span data-stu-id="f1837-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="f1837-247">В этом упражнении вы узнаете, как создать форму, позволяющую менеджерам магазина изменять альбом.</span><span class="sxs-lookup"><span data-stu-id="f1837-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="f1837-248">Они будут просматривать URL-адрес **/стореманажер/едит/ИД** (**идентификатор** является уникальным идентификатором изменяемого альбома), тем самым ДЕЛАЯ вызов HTTP-Get серверу.</span><span class="sxs-lookup"><span data-stu-id="f1837-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="f1837-249">Метод действия "изменить контроллер" извлекает соответствующий альбом из базы данных, создает объект **стореманажервиевмодел** для его инкапсуляции (вместе со списком исполнителей и жанров), а затем передает его в шаблон представления, чтобы отобразить HTML-страницу обратно пользователю.</span><span class="sxs-lookup"><span data-stu-id="f1837-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="f1837-250">На этой странице будет содержаться **&lt;форма&gt;** элемента с полями и раскрывающимися списками для редактирования свойств альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="f1837-251">Когда пользователь обновляет значения формы альбома и нажимает кнопку **сохранить** , изменения отправляются через обратный вызов HTTP-POST обратно в **/стореманажер/едит/ИД**. Хотя URL-адрес остается таким же, как и в последнем вызове, ASP.NET MVC определяет, что на этот раз это HTTP-POST, и, следовательно, выполняет другой метод действия Edit (один с именем **[HttpPost]** ).</span><span class="sxs-lookup"><span data-stu-id="f1837-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="f1837-252">Задача 1. Реализация метода действия HTTP-GET Edit</span><span class="sxs-lookup"><span data-stu-id="f1837-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="f1837-253">В этой задаче будет реализована версия HTTP-GET метода редактирования действия для получения соответствующего альбома из базы данных, а также список всех жанров и исполнителей.</span><span class="sxs-lookup"><span data-stu-id="f1837-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="f1837-254">Эти данные упаковываются в объект **стореманажервиевмодел** , определенный на последнем шаге, который затем передается в шаблон представления для отрисовки ответа с помощью.</span><span class="sxs-lookup"><span data-stu-id="f1837-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="f1837-255">Откройте **Начальное** решение, расположенное по адресу **Source/EX3-креатингсидитвиев/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f1837-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="f1837-256">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="f1837-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f1837-257">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1837-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f1837-258">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f1837-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f1837-259">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f1837-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f1837-260">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="f1837-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f1837-261">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f1837-262">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f1837-263">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1837-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f1837-264">Откройте класс **стореманажерконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="f1837-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="f1837-265">Для этого разверните папку **Controllers** и дважды щелкните **StoreManagerController.CS**.</span><span class="sxs-lookup"><span data-stu-id="f1837-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="f1837-266">Чтобы получить соответствующий **альбом** , а также списки **жанров** и **исполнителей** , замените метод действия **HTTP-Get Edit** следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="f1837-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="f1837-267">(Фрагмент кода — *вспомогательные функции и формы ASP.NET MVC 4 и проверка — EX3 СТОРЕМАНАЖЕРКОНТРОЛЛЕР HTTP — получение действия изменения*)</span><span class="sxs-lookup"><span data-stu-id="f1837-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="f1837-268">Вы используете **System. Web. MVC** **SelectList** для исполнителей и жанров вместо списка **System. Collections. Generic** .</span><span class="sxs-lookup"><span data-stu-id="f1837-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="f1837-269">**SelectList** — это более понятный способ заполнения раскрывающихся списков HTML и управления такими элементами, как текущее выделение.</span><span class="sxs-lookup"><span data-stu-id="f1837-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="f1837-270">При создании экземпляра и последующей настройке этих объектов ViewModel в действии контроллера будет предприниматься очистка сценария формы редактирования.</span><span class="sxs-lookup"><span data-stu-id="f1837-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="f1837-271">Задача 2. Создание представления редактирования</span><span class="sxs-lookup"><span data-stu-id="f1837-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="f1837-272">В этой задаче вы создадите шаблон представления редактирования, который позже будет отображать свойства альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="f1837-273">Создайте представление редактирования.</span><span class="sxs-lookup"><span data-stu-id="f1837-273">Create the Edit View.</span></span> <span data-ttu-id="f1837-274">Для этого щелкните правой кнопкой мыши внутри метода действия **изменить** и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="f1837-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="f1837-275">В диалоговом окне Добавление представления убедитесь, что имя представления имеет значение **изменить**.</span><span class="sxs-lookup"><span data-stu-id="f1837-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="f1837-276">Установите флажок **создать строго типизированное представление** и выберите **альбом (мвкмусиксторе. Models)** из раскрывающегося списка **класс представления данных** .</span><span class="sxs-lookup"><span data-stu-id="f1837-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="f1837-277">В раскрывающемся списке **шаблон шаблона** выберите **изменить** .</span><span class="sxs-lookup"><span data-stu-id="f1837-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="f1837-278">Оставьте в других полях значения по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1837-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="f1837-279">![Добавление представления редактирования](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Добавление представления редактирования")</span><span class="sxs-lookup"><span data-stu-id="f1837-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="f1837-280">*Добавление представления редактирования*</span><span class="sxs-lookup"><span data-stu-id="f1837-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="f1837-281">Задача 3. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="f1837-282">В этой задаче вы проверите, что на странице " **изменение** представления **стореманажер** " отображаются значения свойств для альбома, переданного в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="f1837-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="f1837-283">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-284">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-284">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-285">Измените URL-адрес на **/StoreManager/Edit/1** , чтобы убедиться, что отображаются значения свойств для переданного альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="f1837-286">![Просмотр представления редактирования альбома](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Просмотр представления редактирования альбома")</span><span class="sxs-lookup"><span data-stu-id="f1837-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="f1837-287">*Просмотр представления редактирования альбома*</span><span class="sxs-lookup"><span data-stu-id="f1837-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="f1837-288">Задача 4. Реализация раскрывающихся списка в шаблоне редактора альбомов</span><span class="sxs-lookup"><span data-stu-id="f1837-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="f1837-289">В этой задаче вы добавите раскрывающиеся списки в шаблон представления, созданный в последней задаче, чтобы пользователь мог выбрать из списка исполнителей и жанров.</span><span class="sxs-lookup"><span data-stu-id="f1837-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="f1837-290">Замените все коды полей **альбома** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="f1837-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="f1837-291">В раскрывающиеся раскрывающиеся элементы для выбора исполнителей и жанров добавлен вспомогательный элемент **HTML. DropDownList** .</span><span class="sxs-lookup"><span data-stu-id="f1837-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="f1837-292">Параметры, передаваемые в **HTML. DropDownList** :</span><span class="sxs-lookup"><span data-stu-id="f1837-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="f1837-293">Имя поля формы ( **&quot;артистид&quot;** ).</span><span class="sxs-lookup"><span data-stu-id="f1837-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="f1837-294">**SelectList** значений для раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="f1837-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="f1837-295">Задача 5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="f1837-296">В этой задаче вы проверите, что на странице " **изменение** представления **стореманажер** " отображаются раскрывающиеся окна, а не текстовые поля идентификаторы исполнителя и жанра.</span><span class="sxs-lookup"><span data-stu-id="f1837-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="f1837-297">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-298">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-298">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-299">Измените URL-адрес на **/StoreManager/Edit/1** , чтобы убедиться в том, что в нем отображаются раскрывающиеся поля вместо текстовых полей идентификаторы исполнителя и жанра.</span><span class="sxs-lookup"><span data-stu-id="f1837-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="f1837-300">![Просмотр представления редактирования альбома с раскрывающимися списками](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Просмотр представления редактирования альбома с раскрывающимися списками")</span><span class="sxs-lookup"><span data-stu-id="f1837-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="f1837-301">*Просмотр представления редактирования альбома, на этот раз с раскрывающимися списками*</span><span class="sxs-lookup"><span data-stu-id="f1837-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="f1837-302">Задача 6. Реализация метода действия HTTP-POST Edit</span><span class="sxs-lookup"><span data-stu-id="f1837-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="f1837-303">Теперь, когда представление редактирования отображается так, как ожидалось, необходимо реализовать метод действия HTTP-POST, чтобы сохранить изменения, внесенные в альбом.</span><span class="sxs-lookup"><span data-stu-id="f1837-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="f1837-304">При необходимости закройте браузер, чтобы вернуться в окно Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1837-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="f1837-305">Откройте **стореманажерконтроллер** из папки **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="f1837-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="f1837-306">Замените код метода действия **HTTP-POST** следующим кодом (Обратите внимание, что метод, который необходимо заменить, является перегруженной версией, принимающей два параметра):</span><span class="sxs-lookup"><span data-stu-id="f1837-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="f1837-307">(Фрагмент кода — *вспомогательные функции и формы ASP.NET MVC 4 и проверка — EX3 СТОРЕМАНАЖЕРКОНТРОЛЛЕР HTTP — действие после изменения*)</span><span class="sxs-lookup"><span data-stu-id="f1837-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="f1837-308">Этот метод будет выполняться, когда пользователь нажимает кнопку **сохранить** в представлении и выполняет HTTP-POST значений формы обратно на сервер, чтобы сохранить их в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="f1837-309">Декоратор **[HttpPost]** указывает, что метод следует использовать для сценариев HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="f1837-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="f1837-310">Метод принимает объект **альбома** .</span><span class="sxs-lookup"><span data-stu-id="f1837-310">The method takes an **Album** object.</span></span> <span data-ttu-id="f1837-311">ASP.NET MVC автоматически создаст объект альбома из опубликованной &lt;формы&gt; значений.</span><span class="sxs-lookup"><span data-stu-id="f1837-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="f1837-312">Метод выполнит следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f1837-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="f1837-313">Если модель допустима:</span><span class="sxs-lookup"><span data-stu-id="f1837-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="f1837-314">Обновите запись альбома в контексте, чтобы пометить ее как измененный объект.</span><span class="sxs-lookup"><span data-stu-id="f1837-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="f1837-315">Сохраните изменения и перенаправление в представление индекса.</span><span class="sxs-lookup"><span data-stu-id="f1837-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="f1837-316">Если модель является недопустимой, она заполнит ViewBag на **GenreId** и **артистид**, а затем вернет представление с объектом Received, чтобы разрешить пользователю выполнять любое необходимое обновление.</span><span class="sxs-lookup"><span data-stu-id="f1837-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="f1837-317">Задача 7. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="f1837-318">В этой задаче будет протестировать, что страница «представление **редактирования стореманажер** » фактически сохраняет обновленные данные из этого альбома в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="f1837-319">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-320">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-320">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-321">Измените URL-адрес на **/StoreManager/Edit/1**.</span><span class="sxs-lookup"><span data-stu-id="f1837-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="f1837-322">Измените заголовок альбома для **загрузки** и щелкните Save ( **сохранить**).</span><span class="sxs-lookup"><span data-stu-id="f1837-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="f1837-323">Убедитесь, что название альбома в списке альбомов действительно изменилось.</span><span class="sxs-lookup"><span data-stu-id="f1837-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="f1837-324">![Обновление альбома](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Обновление альбома")</span><span class="sxs-lookup"><span data-stu-id="f1837-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="f1837-325">*Обновление альбома*</span><span class="sxs-lookup"><span data-stu-id="f1837-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="f1837-326">Упражнение 4. Добавление представления создания</span><span class="sxs-lookup"><span data-stu-id="f1837-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="f1837-327">Теперь, когда **стореманажерконтроллер** поддерживает возможности **редактирования** , в этом упражнении вы узнаете, как добавить шаблон создания представления, чтобы позволить диспетчерам магазинов добавить в приложение новые альбомы.</span><span class="sxs-lookup"><span data-stu-id="f1837-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="f1837-328">Как и в случае с функцией редактирования, вы реализуете сценарий создания с помощью двух отдельных методов в классе **стореманажерконтроллер** :</span><span class="sxs-lookup"><span data-stu-id="f1837-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="f1837-329">Один метод действия отображает пустую форму, когда диспетчеры магазинов сначала посещают URL-адрес **/стореманажер/креате** .</span><span class="sxs-lookup"><span data-stu-id="f1837-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="f1837-330">Второй метод действия обрабатывает сценарий, в котором диспетчер магазина нажимает кнопку **сохранить** в форме и отправляет значения обратно в URL-адрес **/СТОРЕМАНАЖЕР/КРЕАТЕ** в виде HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="f1837-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="f1837-331">Задача 1. Реализация метода создания действия HTTP-GET</span><span class="sxs-lookup"><span data-stu-id="f1837-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="f1837-332">В этой задаче будет реализована версия HTTP-GET метода создания действия, чтобы получить список всех жанров и исполнителей, упаковать эти данные в объект **стореманажервиевмодел** , который затем будет передан в шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="f1837-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="f1837-333">Откройте **Начальное** решение, расположенное по адресу **Source/EX4-аддингакреатевиев/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f1837-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="f1837-334">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="f1837-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f1837-335">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1837-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f1837-336">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f1837-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f1837-337">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f1837-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f1837-338">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="f1837-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f1837-339">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f1837-340">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f1837-341">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1837-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f1837-342">Откройте класс **стореманажерконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="f1837-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="f1837-343">Для этого разверните папку **Controllers** и дважды щелкните **StoreManagerController.CS**.</span><span class="sxs-lookup"><span data-stu-id="f1837-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="f1837-344">Замените код метода действия **CREATE** Action следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="f1837-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="f1837-345">(Фрагмент кода — *вспомогательные функции и формы ASP.NET MVC 4 и проверка-EX4 СТОРЕМАНАЖЕРКОНТРОЛЛЕР HTTP-GET Create*)</span><span class="sxs-lookup"><span data-stu-id="f1837-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="f1837-346">Задача 2. Добавление представления создания</span><span class="sxs-lookup"><span data-stu-id="f1837-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="f1837-347">В этой задаче вы добавите шаблон создания представления, в котором будет отображаться новая (пустая) форма альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="f1837-348">Щелкните правой кнопкой мыши внутри метода **создания** действия и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="f1837-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="f1837-349">Откроется диалоговое окно Добавление представления.</span><span class="sxs-lookup"><span data-stu-id="f1837-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="f1837-350">В диалоговом окне Добавление представления убедитесь, что имя представления — **CREATE**.</span><span class="sxs-lookup"><span data-stu-id="f1837-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="f1837-351">Выберите параметр **создать строго типизированное представление** и в раскрывающемся списке **класс модели** выберите **альбом (мвкмусиксторе. Models)** и **Создайте** из раскрывающегося списка **шаблон шаблонов** .</span><span class="sxs-lookup"><span data-stu-id="f1837-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="f1837-352">Оставьте в других полях значения по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1837-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="f1837-353">![Добавление представления создания](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "аддинг-а-креате-виев. png")</span><span class="sxs-lookup"><span data-stu-id="f1837-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="f1837-354">*Добавление представления создания*</span><span class="sxs-lookup"><span data-stu-id="f1837-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="f1837-355">Обновите поля **GenreId** и **артистид** , чтобы использовать раскрывающийся список, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f1837-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="f1837-356">Задача 3. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="f1837-357">В этой задаче вы проверите, что на странице **Создание** представления **стореманажер** отображается пустая форма альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="f1837-358">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-359">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-359">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-360">Измените URL-адрес на **/стореманажер/креате**.</span><span class="sxs-lookup"><span data-stu-id="f1837-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="f1837-361">Убедитесь, что для заполнения новых свойств альбома отображается пустая форма.</span><span class="sxs-lookup"><span data-stu-id="f1837-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="f1837-362">![Создать представление с пустой формой](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Создать представление с пустой формой")</span><span class="sxs-lookup"><span data-stu-id="f1837-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="f1837-363">*Создать представление с пустой формой*</span><span class="sxs-lookup"><span data-stu-id="f1837-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="f1837-364">Задача 4. Реализация метода действия HTTP-POST CREATE</span><span class="sxs-lookup"><span data-stu-id="f1837-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="f1837-365">В этой задаче будет реализована версия HTTP-POST метода создания действия, который будет вызываться при нажатии пользователем кнопки **сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f1837-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="f1837-366">Метод должен сохранить новый альбом в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="f1837-367">При необходимости закройте браузер, чтобы вернуться в окно Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1837-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="f1837-368">Откройте класс **стореманажерконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="f1837-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="f1837-369">Для этого разверните папку **Controllers** и дважды щелкните **StoreManagerController.CS**.</span><span class="sxs-lookup"><span data-stu-id="f1837-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="f1837-370">Замените код метода действия **HTTP-POST** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="f1837-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="f1837-371">(Фрагмент кода — *вспомогательные функции и формы ASP.NET MVC 4 и проверка-EX4 СТОРЕМАНАЖЕРКОНТРОЛЛЕР HTTP-после создания*)</span><span class="sxs-lookup"><span data-stu-id="f1837-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="f1837-372">Действие Create практически аналогично предыдущему методу действия Edit, но вместо настройки объекта как измененного он добавляется в контекст.</span><span class="sxs-lookup"><span data-stu-id="f1837-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="f1837-373">Задача 5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="f1837-374">В этой задаче вы проверите, что страница **Создание представления стореманажер** позволяет создать новый альбом, а затем перенаправит его в представление индекса стореманажер.</span><span class="sxs-lookup"><span data-stu-id="f1837-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="f1837-375">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-376">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-376">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-377">Измените URL-адрес на **/стореманажер/креате**.</span><span class="sxs-lookup"><span data-stu-id="f1837-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="f1837-378">Заполните все поля формы данными для нового альбома, как показано на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="f1837-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="f1837-379">![Создание альбома](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Создание альбома")</span><span class="sxs-lookup"><span data-stu-id="f1837-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="f1837-380">*Создание альбома*</span><span class="sxs-lookup"><span data-stu-id="f1837-380">*Creating an Album*</span></span>
3. <span data-ttu-id="f1837-381">Убедитесь, что вы перенаправлены в представление индекса Стореманажер, которое содержит только что созданный новый альбом.</span><span class="sxs-lookup"><span data-stu-id="f1837-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="f1837-382">![Создан новый альбом](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "Создан новый альбом")</span><span class="sxs-lookup"><span data-stu-id="f1837-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="f1837-383">*Создан новый альбом*</span><span class="sxs-lookup"><span data-stu-id="f1837-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="f1837-384">Упражнение 5. Обработка удаления</span><span class="sxs-lookup"><span data-stu-id="f1837-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="f1837-385">Возможность удаления альбомов еще не реализована.</span><span class="sxs-lookup"><span data-stu-id="f1837-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="f1837-386">Это упражнение будет соблюдаться.</span><span class="sxs-lookup"><span data-stu-id="f1837-386">This is what this exercise will be about.</span></span> <span data-ttu-id="f1837-387">Как и раньше, вы реализуете сценарий удаления, используя два отдельных метода в классе **стореманажерконтроллер** :</span><span class="sxs-lookup"><span data-stu-id="f1837-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="f1837-388">В одном методе действия отображается форма подтверждения</span><span class="sxs-lookup"><span data-stu-id="f1837-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="f1837-389">Второй метод действия будет выполнять отправку формы</span><span class="sxs-lookup"><span data-stu-id="f1837-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="f1837-390">Задача 1. Реализация метода действия HTTP-GET Delete</span><span class="sxs-lookup"><span data-stu-id="f1837-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="f1837-391">В этой задаче будет реализована версия HTTP-GET метода действия Delete для получения сведений о альбоме.</span><span class="sxs-lookup"><span data-stu-id="f1837-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="f1837-392">Откройте **Начальное** решение, расположенное по адресу **Source/Ex5-хандлингделетион/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f1837-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="f1837-393">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="f1837-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f1837-394">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1837-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f1837-395">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f1837-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f1837-396">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f1837-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f1837-397">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="f1837-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f1837-398">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f1837-399">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f1837-400">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1837-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f1837-401">Откройте класс **стореманажерконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="f1837-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="f1837-402">Для этого разверните папку **Controllers** и дважды щелкните **StoreManagerController.CS**.</span><span class="sxs-lookup"><span data-stu-id="f1837-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="f1837-403">Действие "Удаление контроллера" точно совпадает с предыдущим действием контроллера сведений о хранилище: запрашивает объект **альбома** из базы данных, используя **идентификатор** , указанный в URL-адресе, и возвращает соответствующее **представление**.</span><span class="sxs-lookup"><span data-stu-id="f1837-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="f1837-404">Для этого замените код метода действия HTTP-GET **Delete** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="f1837-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="f1837-405">(Фрагмент кода — *вспомогательные функции и формы ASP.NET MVC 4 и проверка — удаление операции HTTP — получение удаления*)</span><span class="sxs-lookup"><span data-stu-id="f1837-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="f1837-406">Щелкните правой кнопкой мыши внутри метода действия **Delete** и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="f1837-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="f1837-407">Откроется диалоговое окно Добавление представления.</span><span class="sxs-lookup"><span data-stu-id="f1837-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="f1837-408">В диалоговом окне Добавление представления убедитесь, что имя представления — **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f1837-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="f1837-409">Выберите параметр **создать строго типизированное представление** и в раскрывающемся списке **класс модели** выберите **альбом (мвкмусиксторе. Models)** .</span><span class="sxs-lookup"><span data-stu-id="f1837-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="f1837-410">Выберите **Удалить** из раскрывающегося списка **шаблон шаблонов** .</span><span class="sxs-lookup"><span data-stu-id="f1837-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="f1837-411">Оставьте в других полях значения по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1837-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="f1837-412">![Добавление представления удаления](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Добавление представления удаления")</span><span class="sxs-lookup"><span data-stu-id="f1837-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="f1837-413">*Добавление представления удаления*</span><span class="sxs-lookup"><span data-stu-id="f1837-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="f1837-414">В шаблоне удаления отображаются все поля модели.</span><span class="sxs-lookup"><span data-stu-id="f1837-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="f1837-415">Отобразится только название альбома.</span><span class="sxs-lookup"><span data-stu-id="f1837-415">You will show only the album's title.</span></span> <span data-ttu-id="f1837-416">Для этого замените содержимое представления следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="f1837-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="f1837-417">Задача 2. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="f1837-418">В этой задаче вы проверите, что на странице **стореманажер** **Delete** View (удаление представления) отображается форма удаления подтверждения.</span><span class="sxs-lookup"><span data-stu-id="f1837-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="f1837-419">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-420">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-420">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-421">Измените URL-адрес на **/стореманажер**.</span><span class="sxs-lookup"><span data-stu-id="f1837-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="f1837-422">Выберите один из альбомов для удаления, нажав кнопку **Удалить** и убедившись, что новое представление отправлено.</span><span class="sxs-lookup"><span data-stu-id="f1837-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="f1837-423">![Удаление альбома](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Удаление альбома")</span><span class="sxs-lookup"><span data-stu-id="f1837-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="f1837-424">*Удаление альбома*</span><span class="sxs-lookup"><span data-stu-id="f1837-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="f1837-425">Задача 3. Реализация метода действия HTTP-POST Delete</span><span class="sxs-lookup"><span data-stu-id="f1837-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="f1837-426">В этой задаче будет реализована версия HTTP-POST метода действия Delete, которая будет вызываться при нажатии пользователем кнопки **Удалить** .</span><span class="sxs-lookup"><span data-stu-id="f1837-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="f1837-427">Метод должен удалить альбом в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="f1837-428">При необходимости закройте браузер, чтобы вернуться в окно Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1837-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="f1837-429">Откройте класс **стореманажерконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="f1837-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="f1837-430">Для этого разверните папку **Controllers** и дважды щелкните **StoreManagerController.CS**.</span><span class="sxs-lookup"><span data-stu-id="f1837-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="f1837-431">Замените код метода действия **http, выполняемого после удаления** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="f1837-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="f1837-432">(Фрагмент кода — *вспомогательные функции и формы ASP.NET MVC 4 и проверка-Ex5 удаление HTTP-POST Action*)</span><span class="sxs-lookup"><span data-stu-id="f1837-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="f1837-433">Задача 4. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="f1837-434">В этой задаче вы проверите, что страница **Стореманажер удаление** представления позволяет удалить альбом, а затем перенаправит его в представление индекса стореманажер.</span><span class="sxs-lookup"><span data-stu-id="f1837-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="f1837-435">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-436">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-436">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-437">Измените URL-адрес на **/стореманажер**.</span><span class="sxs-lookup"><span data-stu-id="f1837-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="f1837-438">Выберите один из альбомов для удаления, нажав кнопку **Удалить.**</span><span class="sxs-lookup"><span data-stu-id="f1837-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="f1837-439">Подтвердите удаление, нажав кнопку " **Удалить** ":</span><span class="sxs-lookup"><span data-stu-id="f1837-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="f1837-440">![Удаление альбома](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Удаление альбома")</span><span class="sxs-lookup"><span data-stu-id="f1837-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="f1837-441">*Удаление альбома*</span><span class="sxs-lookup"><span data-stu-id="f1837-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="f1837-442">Убедитесь, что альбом удален, так как он не отображается на странице **индекса** .</span><span class="sxs-lookup"><span data-stu-id="f1837-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="f1837-443">Упражнение 6. Добавление проверки</span><span class="sxs-lookup"><span data-stu-id="f1837-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="f1837-444">В настоящее время формы создания и редактирования на месте не выполняют каких либо проверок.</span><span class="sxs-lookup"><span data-stu-id="f1837-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="f1837-445">Если пользователь оставляет обязательное поле пустым или вводите буквы в поле Price (цена), первая ошибка, которую вы будете получать, будет находиться в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="f1837-446">Можно добавить проверку в приложение, добавив заметки к данным в класс модели.</span><span class="sxs-lookup"><span data-stu-id="f1837-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="f1837-447">Заметки к данным позволяют описать правила, которые необходимо применить к свойствам модели, а ASP.NET MVC будет обеспечивать применение и отображение соответствующих сообщений пользователям.</span><span class="sxs-lookup"><span data-stu-id="f1837-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="f1837-448">Задача 1. Добавление заметок к данным</span><span class="sxs-lookup"><span data-stu-id="f1837-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="f1837-449">В этой задаче в модель альбома добавляются заметки к данным, которые при необходимости будут отображать сообщения проверки на странице создания и редактирования.</span><span class="sxs-lookup"><span data-stu-id="f1837-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="f1837-450">Для простого класса модели Добавление заметки к данным выполняется только путем добавления оператора **using** для **System. ComponentModel. Аннотация**и последующего размещения атрибута **[Required]** в соответствующих свойствах.</span><span class="sxs-lookup"><span data-stu-id="f1837-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="f1837-451">В следующем примере свойство **Name** станет обязательным полем в представлении.</span><span class="sxs-lookup"><span data-stu-id="f1837-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="f1837-452">Это немного сложнее в таких случаях, как это приложение, в котором создается EDM.</span><span class="sxs-lookup"><span data-stu-id="f1837-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="f1837-453">Если вы добавили заметки к данным непосредственно в классы модели, они будут перезаписаны при обновлении модели из базы данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="f1837-454">Вместо этого можно использовать разделяемые классы метаданных, которые будут существовать для хранения заметок и связаны с классами модели с помощью атрибута **[метадататипе]** .</span><span class="sxs-lookup"><span data-stu-id="f1837-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="f1837-455">Откройте **Начальное** решение, расположенное по адресу **Source/Ex6-аддингвалидатион/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f1837-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="f1837-456">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="f1837-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f1837-457">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1837-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f1837-458">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f1837-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f1837-459">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f1837-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f1837-460">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="f1837-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f1837-461">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f1837-462">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f1837-463">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1837-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f1837-464">Откройте **Album.CS** из папки **Models** .</span><span class="sxs-lookup"><span data-stu-id="f1837-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="f1837-465">Замените содержимое **Album.CS** выделенным кодом, чтобы он выглядел следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f1837-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="f1837-466">Строка **[DisplayFormat (конвертемптистрингтонулл = false)]** указывает, что пустые строки из модели не будут преобразованы в значение null при обновлении поля данных в источнике данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="f1837-467">Этот параметр позволяет избежать исключения, когда Entity Framework присваивает модели значения NULL, прежде чем заметка данных проверит поля.</span><span class="sxs-lookup"><span data-stu-id="f1837-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="f1837-468">(Фрагмент кода — *вспомогательные методы и формы ASP.NET MVC 4 и проверка-Ex6 разделяемого класса метаданных альбома*)</span><span class="sxs-lookup"><span data-stu-id="f1837-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="f1837-469">Этот разделяемый класс **альбома** имеет атрибут **метадататипе** , указывающий на класс **Албумметадата** для заметок к данным.</span><span class="sxs-lookup"><span data-stu-id="f1837-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="f1837-470">Вот некоторые атрибуты аннотации данных, которые вы используете для создания заметок к модели альбома:</span><span class="sxs-lookup"><span data-stu-id="f1837-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="f1837-471">Обязательное — указывает, что свойство является обязательным полем.</span><span class="sxs-lookup"><span data-stu-id="f1837-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="f1837-472">DisplayName — определяет текст, используемый в полях формы и сообщениях проверки.</span><span class="sxs-lookup"><span data-stu-id="f1837-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="f1837-473">DisplayFormat — задает способ отображения и форматирования полей данных.</span><span class="sxs-lookup"><span data-stu-id="f1837-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="f1837-474">StringLength — определяет максимальную длину для строкового поля</span><span class="sxs-lookup"><span data-stu-id="f1837-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="f1837-475">Range — максимальное и минимальное значение для числового поля.</span><span class="sxs-lookup"><span data-stu-id="f1837-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="f1837-476">Скаффолдколумн — позволяет скрывать поля из форм редактора</span><span class="sxs-lookup"><span data-stu-id="f1837-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="f1837-477">Задача 2. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f1837-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="f1837-478">В этой задаче будет проверено, что поля "создать" и "Изменить страницу" проверяются с использованием отображаемых имен, выбранных в последней задаче.</span><span class="sxs-lookup"><span data-stu-id="f1837-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="f1837-479">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1837-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f1837-480">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-480">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-481">Измените URL-адрес на **/стореманажер/креате**.</span><span class="sxs-lookup"><span data-stu-id="f1837-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="f1837-482">Убедитесь, что отображаемые имена совпадают с именами в разделяемом классе (например, в **URL-адресе обложки альбома** вместо **албумартурл**).</span><span class="sxs-lookup"><span data-stu-id="f1837-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="f1837-483">Нажмите кнопку **создать**, не заполняя форму.</span><span class="sxs-lookup"><span data-stu-id="f1837-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="f1837-484">Убедитесь, что вы получаете соответствующие сообщения проверки.</span><span class="sxs-lookup"><span data-stu-id="f1837-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="f1837-485">![Проверенные поля на странице создания](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Проверенные поля на странице создания")</span><span class="sxs-lookup"><span data-stu-id="f1837-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="f1837-486">*Проверенные поля на странице создания*</span><span class="sxs-lookup"><span data-stu-id="f1837-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="f1837-487">Это можно проверить с помощью страницы **изменить** .</span><span class="sxs-lookup"><span data-stu-id="f1837-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="f1837-488">Измените URL-адрес на **/StoreManager/Edit/1** и убедитесь, что отображаемые имена совпадают с именами в разделяемом классе (например, **URL-адрес обложки альбома** вместо **албумартурл**).</span><span class="sxs-lookup"><span data-stu-id="f1837-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="f1837-489">Очистите поля **Title** и **Price** и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f1837-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="f1837-490">Убедитесь, что вы получаете соответствующие сообщения проверки.</span><span class="sxs-lookup"><span data-stu-id="f1837-490">Verify that you get the corresponding validation messages.</span></span>

    ![Проверенные поля на странице "Правка"](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="f1837-492">*Проверенные поля на странице "Правка"*</span><span class="sxs-lookup"><span data-stu-id="f1837-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="f1837-493">Упражнение 7. Использование ненавязчивой jQuery на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="f1837-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="f1837-494">В этом упражнении вы узнаете, как включить ненавязчивую проверку jQuery 4 на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="f1837-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="f1837-495">Ненавязчивая jQuery использует префикс AJAX для данных для вызова методов действий на сервере, а не для принудительного создания встроенных клиентских скриптов.</span><span class="sxs-lookup"><span data-stu-id="f1837-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="f1837-496">Задача 1. Запуск приложения перед включением ненавязчивой jQuery</span><span class="sxs-lookup"><span data-stu-id="f1837-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="f1837-497">В этой задаче будет запущено приложение перед включением jQuery для сравнения обеих моделей проверки.</span><span class="sxs-lookup"><span data-stu-id="f1837-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="f1837-498">Откройте **Начальное** решение, расположенное по адресу **Source/Ex7-унобтрусивежкуеривалидатион/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f1837-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="f1837-499">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="f1837-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f1837-500">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1837-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f1837-501">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f1837-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f1837-502">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="f1837-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f1837-503">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="f1837-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f1837-504">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f1837-505">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f1837-506">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1837-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f1837-507">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="f1837-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="f1837-508">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-508">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-509">Просмотрите **/стореманажер/креате** и нажмите кнопку **создать** , не заполнив форму, чтобы убедиться, что вы получаете сообщения проверки:</span><span class="sxs-lookup"><span data-stu-id="f1837-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="f1837-510">![Проверка клиента отключена](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Проверка клиента отключена")</span><span class="sxs-lookup"><span data-stu-id="f1837-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="f1837-511">*Проверка клиента отключена*</span><span class="sxs-lookup"><span data-stu-id="f1837-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="f1837-512">В браузере откройте исходный код HTML:</span><span class="sxs-lookup"><span data-stu-id="f1837-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="f1837-513">Задача 2. Включение ненавязчивой проверки клиента</span><span class="sxs-lookup"><span data-stu-id="f1837-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="f1837-514">В этой задаче будет включена **ненавязчивая клиентская проверка** jQuery из файла **Web. config** . по умолчанию для всех новых проектов ASP.NET MVC 4 устанавливается значение false.</span><span class="sxs-lookup"><span data-stu-id="f1837-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="f1837-515">Кроме того, вы добавите необходимые ссылки на скрипты, чтобы сделать ненавязчивую проверку клиента jQuery некорректной.</span><span class="sxs-lookup"><span data-stu-id="f1837-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="f1837-516">Откройте файл **Web. config** в корневом каталоге проекта и убедитесь, что для значений ключей **клиентвалидатионенаблед** и **унобтрусивежаваскриптенаблед** задано значение **true**.</span><span class="sxs-lookup"><span data-stu-id="f1837-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="f1837-517">Вы также можете включить проверку клиента по коду в Global.asax.cs, чтобы получить те же результаты:</span><span class="sxs-lookup"><span data-stu-id="f1837-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="f1837-518">**HtmlHelper. Клиентвалидатионенаблед = true;**</span><span class="sxs-lookup"><span data-stu-id="f1837-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="f1837-519">Кроме того, атрибут Клиентвалидатионенаблед можно назначить любому контроллеру, чтобы иметь настраиваемое поведение.</span><span class="sxs-lookup"><span data-stu-id="f1837-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="f1837-520">Откройте **Create. cshtml** по адресу **виевс\стореманажер**.</span><span class="sxs-lookup"><span data-stu-id="f1837-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="f1837-521">Убедитесь в том, что в представлении имеются ссылки на следующие файлы скриптов, **jQuery. Validate** и **jQuery. Validate. unobtrusiveые**, а в списке — &quot; **~/бундлес/жкуеривал**&quot;.</span><span class="sxs-lookup"><span data-stu-id="f1837-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view through the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="f1837-522">Все эти библиотеки jQuery включены в новые проекты MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f1837-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="f1837-523">Дополнительные библиотеки можно найти в папке **/Scripts** проекта.</span><span class="sxs-lookup"><span data-stu-id="f1837-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="f1837-524">Чтобы обеспечить работу библиотек проверки, необходимо добавить ссылку на библиотеку платформы jQuery.</span><span class="sxs-lookup"><span data-stu-id="f1837-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="f1837-525">Так как эта ссылка уже добавлена в файл **\_Layout. cshtml** , вам не нужно добавлять его в этом конкретном представлении.</span><span class="sxs-lookup"><span data-stu-id="f1837-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="f1837-526">Задача 3. Запуск приложения с использованием ненавязчивой проверки jQuery</span><span class="sxs-lookup"><span data-stu-id="f1837-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="f1837-527">В этой задаче вы проверите, что шаблон представления создания **стореманажер** выполняет проверку на стороне клиента с помощью библиотек jQuery, когда пользователь создает новый альбом.</span><span class="sxs-lookup"><span data-stu-id="f1837-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="f1837-528">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="f1837-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="f1837-529">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="f1837-529">The project starts in the Home page.</span></span> <span data-ttu-id="f1837-530">Просмотрите **/стореманажер/креате** и нажмите кнопку **создать** , не заполнив форму, чтобы убедиться, что вы получаете сообщения проверки:</span><span class="sxs-lookup"><span data-stu-id="f1837-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="f1837-531">![Проверка клиентов с включенной поддержкой jQuery](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Проверка клиентов с включенной поддержкой jQuery")</span><span class="sxs-lookup"><span data-stu-id="f1837-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="f1837-532">*Проверка клиентов с включенной поддержкой jQuery*</span><span class="sxs-lookup"><span data-stu-id="f1837-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="f1837-533">В браузере откройте исходный код для создания представления.</span><span class="sxs-lookup"><span data-stu-id="f1837-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="f1837-534">Для каждого правила проверки клиента ненавязчивая jQuery добавляет атрибут с данными-Val-*rulename*=&quot;*сообщения*&quot;.</span><span class="sxs-lookup"><span data-stu-id="f1837-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="f1837-535">Ниже приведен список тегов, которые ненавязчивые вставки jQuery в поле ввода HTML для выполнения проверки клиента.</span><span class="sxs-lookup"><span data-stu-id="f1837-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="f1837-536">Данные-Val</span><span class="sxs-lookup"><span data-stu-id="f1837-536">Data-val</span></span>
   > - <span data-ttu-id="f1837-537">Данные-Val-Number</span><span class="sxs-lookup"><span data-stu-id="f1837-537">Data-val-number</span></span>
   > - <span data-ttu-id="f1837-538">Данные-Val-Range</span><span class="sxs-lookup"><span data-stu-id="f1837-538">Data-val-range</span></span>
   > - <span data-ttu-id="f1837-539">Data-Val-Range-min/Data-Val-Range-Max</span><span class="sxs-lookup"><span data-stu-id="f1837-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="f1837-540">Data-Val — обязательное</span><span class="sxs-lookup"><span data-stu-id="f1837-540">Data-val-required</span></span>
   > - <span data-ttu-id="f1837-541">Данные-Val-length</span><span class="sxs-lookup"><span data-stu-id="f1837-541">Data-val-length</span></span>
   > - <span data-ttu-id="f1837-542">Data-Val-length-Max/Data-Val-length-min</span><span class="sxs-lookup"><span data-stu-id="f1837-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="f1837-543">Все значения данных заполняются **заметками данных**модели.</span><span class="sxs-lookup"><span data-stu-id="f1837-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="f1837-544">Затем вся логика, которая работает на стороне сервера, может выполняться на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="f1837-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="f1837-545">Например, атрибут Price содержит следующие данные в модели:</span><span class="sxs-lookup"><span data-stu-id="f1837-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="f1837-546">После использования ненавязчивой jQuery созданный код будет следующим:</span><span class="sxs-lookup"><span data-stu-id="f1837-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f1837-547">Сводка</span><span class="sxs-lookup"><span data-stu-id="f1837-547">Summary</span></span>

<span data-ttu-id="f1837-548">С помощью этой практической лабораторной работы вы узнали, как разрешить пользователям изменять данные, хранящиеся в базе данных, с помощью следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="f1837-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="f1837-549">Действия контроллера, такие как индекс, создание, изменение, удаление</span><span class="sxs-lookup"><span data-stu-id="f1837-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="f1837-550">Функция формирования шаблонов MVC ASP.NET для отображения свойств в таблице HTML</span><span class="sxs-lookup"><span data-stu-id="f1837-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="f1837-551">Пользовательские вспомогательные методы HTML для улучшения взаимодействия с пользователем</span><span class="sxs-lookup"><span data-stu-id="f1837-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="f1837-552">Методы действия, реагирующие на вызовы HTTP-GET или HTTP-POST</span><span class="sxs-lookup"><span data-stu-id="f1837-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="f1837-553">Шаблон общего редактора для похожих шаблонов представлений, таких как создание и редактирование</span><span class="sxs-lookup"><span data-stu-id="f1837-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="f1837-554">Элементы формы, такие как раскрывающиеся</span><span class="sxs-lookup"><span data-stu-id="f1837-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="f1837-555">Заметки к данным для проверки модели</span><span class="sxs-lookup"><span data-stu-id="f1837-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="f1837-556">Проверка на стороне клиента с помощью ненавязчивой библиотеки jQuery</span><span class="sxs-lookup"><span data-stu-id="f1837-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f1837-557">Приложение а. Установка Visual Studio Express 2012 для Web</span><span class="sxs-lookup"><span data-stu-id="f1837-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f1837-558">Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версии с помощью **[установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="f1837-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f1837-559">Следующие инструкции помогут вам выполнить действия, необходимые для установки *Visual Studio Express 2012 для Web* с помощью *установщик веб-платформы Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="f1837-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f1837-560">Перейдите в [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="f1837-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f1837-561">Кроме того, если у вас уже установлен установщик веб-платформы, вы можете открыть его и найти продукт &quot;<em>Visual Studio Express 2012 для Web с Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="f1837-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f1837-562">Щелкните **Install Now (установить сейчас**).</span><span class="sxs-lookup"><span data-stu-id="f1837-562">Click on **Install Now**.</span></span> <span data-ttu-id="f1837-563">Если у вас нет **установщика веб-платформы** , вы будете сначала перенаправлены на загрузку и установку.</span><span class="sxs-lookup"><span data-stu-id="f1837-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f1837-564">После открытия **установщика веб-платформы** нажмите кнопку **установить** , чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="f1837-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f1837-565">![Установка Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Установка Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="f1837-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="f1837-566">*Установка Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="f1837-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="f1837-567">Прочитайте все лицензии и условия продуктов и нажмите кнопку " **принять** ", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="f1837-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Принятие условий лицензии](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="f1837-569">*Принятие условий лицензии*</span><span class="sxs-lookup"><span data-stu-id="f1837-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="f1837-570">Дождитесь завершения процесса загрузки и установки.</span><span class="sxs-lookup"><span data-stu-id="f1837-570">Wait until the downloading and installation process completes.</span></span>

    ![Ход установки](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="f1837-572">*Ход установки*</span><span class="sxs-lookup"><span data-stu-id="f1837-572">*Installation progress*</span></span>
6. <span data-ttu-id="f1837-573">После завершения установки нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f1837-573">When the installation completes, click **Finish**.</span></span>

    ![Установка завершена](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="f1837-575">*Установка завершена*</span><span class="sxs-lookup"><span data-stu-id="f1837-575">*Installation completed*</span></span>
7. <span data-ttu-id="f1837-576">Нажмите кнопку **выход** , чтобы закрыть установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="f1837-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f1837-577">Чтобы открыть Visual Studio Express для Интернета, перейдите на **начальный** экран и начните запись &quot;**VS Express**&quot;, а затем щелкните плитку **VS Express для Web** .</span><span class="sxs-lookup"><span data-stu-id="f1837-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Плитка VS Express для Web](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="f1837-579">*Плитка VS Express для Web*</span><span class="sxs-lookup"><span data-stu-id="f1837-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="f1837-580">Приложение б. Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="f1837-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="f1837-581">С помощью фрагментов кода вы можете получить все необходимые вам коды.</span><span class="sxs-lookup"><span data-stu-id="f1837-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="f1837-582">В лабораторном документе вы узнаете, когда можно использовать их, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="f1837-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="f1837-583">![Использование фрагментов кода Visual Studio для вставки кода в проект](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Использование фрагментов кода Visual Studio для вставки кода в проект")</span><span class="sxs-lookup"><span data-stu-id="f1837-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="f1837-584">*Использование фрагментов кода Visual Studio для вставки кода в проект*</span><span class="sxs-lookup"><span data-stu-id="f1837-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="f1837-585">***Добавление фрагмента кода с помощью клавиатуры (C# только)***</span><span class="sxs-lookup"><span data-stu-id="f1837-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="f1837-586">Поместите курсор в то место, куда вы хотите вставить код.</span><span class="sxs-lookup"><span data-stu-id="f1837-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="f1837-587">Начните вводить имя фрагмента (без пробелов или дефисов).</span><span class="sxs-lookup"><span data-stu-id="f1837-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="f1837-588">Посмотрите, как IntelliSense отображает соответствующие имена фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="f1837-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="f1837-589">Выберите правильный фрагмент кода (или вводите его, пока не будет выбрано имя всего фрагмента).</span><span class="sxs-lookup"><span data-stu-id="f1837-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="f1837-590">Дважды нажмите клавишу TAB, чтобы вставить фрагмент в позицию курсора.</span><span class="sxs-lookup"><span data-stu-id="f1837-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="f1837-591">![Начните вводить имя фрагмента](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Начните вводить имя фрагмента")</span><span class="sxs-lookup"><span data-stu-id="f1837-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="f1837-592">*Начните вводить имя фрагмента*</span><span class="sxs-lookup"><span data-stu-id="f1837-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="f1837-593">![Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="f1837-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="f1837-594">*Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="f1837-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="f1837-595">![Снова нажмите клавишу TAB, и фрагмент развернется](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Снова нажмите клавишу TAB, и фрагмент развернется")</span><span class="sxs-lookup"><span data-stu-id="f1837-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="f1837-596">*Снова нажмите клавишу TAB, и фрагмент развернется*</span><span class="sxs-lookup"><span data-stu-id="f1837-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="f1837-597">***Добавление фрагмента кода с помощью мыши (C#, Visual Basic и XML)*** одного.</span><span class="sxs-lookup"><span data-stu-id="f1837-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="f1837-598">Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="f1837-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="f1837-599">Выберите **Вставить фрагмент** , за которым следуют **фрагменты кода**.</span><span class="sxs-lookup"><span data-stu-id="f1837-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="f1837-600">Выберите соответствующий фрагмент из списка, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="f1837-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="f1837-601">![Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="f1837-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="f1837-602">*Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="f1837-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="f1837-603">![Выберите соответствующий фрагмент из списка, щелкнув его.](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Выберите соответствующий фрагмент из списка, щелкнув его.")</span><span class="sxs-lookup"><span data-stu-id="f1837-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="f1837-604">*Выберите соответствующий фрагмент из списка, щелкнув его.*</span><span class="sxs-lookup"><span data-stu-id="f1837-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
