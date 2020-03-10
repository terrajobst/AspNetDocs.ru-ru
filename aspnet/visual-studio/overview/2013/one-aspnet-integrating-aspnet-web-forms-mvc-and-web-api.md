---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 'Практическое занятие. одна ASP.NET: Интеграция ASP.NET Web Forms, MVC и веб-API | Документация Майкрософт'
author: rick-anderson
description: ASP.NET — это платформа для создания веб-сайтов, приложений и служб с помощью специализированных технологий, таких как MVC, веб-API и др. С расширением ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505458"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a><span data-ttu-id="3a67c-104">Практическое занятие. одна ASP.NET: Интеграция ASP.NET Web Forms, MVC и веб-API</span><span class="sxs-lookup"><span data-stu-id="3a67c-104">Hands On Lab: One ASP.NET: Integrating ASP.NET Web Forms, MVC and Web API</span></span>

<span data-ttu-id="3a67c-105">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="3a67c-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="3a67c-106">Скачать обучающий комплект Web Camp</span><span class="sxs-lookup"><span data-stu-id="3a67c-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="3a67c-107">ASP.NET — это платформа для создания веб-сайтов, приложений и служб с помощью специализированных технологий, таких как MVC, веб-API и др.</span><span class="sxs-lookup"><span data-stu-id="3a67c-107">ASP.NET is a framework for building Web sites, apps and services using specialized technologies such as MVC, Web API and others.</span></span> <span data-ttu-id="3a67c-108">С момента создания ASP.NET расширения и выражения, которые должны интегрировать эти технологии, существуют последние усилия по работе с **одним ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-108">With the expansion ASP.NET has seen since its creation and the expressed need to have these technologies integrated, there have been recent efforts in working towards **One ASP.NET**.</span></span>
> 
> <span data-ttu-id="3a67c-109">В Visual Studio 2013 введена новая унифицированная система проектов, позволяющая создавать приложения и использовать все технологии ASP.NET в одном проекте.</span><span class="sxs-lookup"><span data-stu-id="3a67c-109">Visual Studio 2013 introduces a new unified project system which lets you build an application and use all the ASP.NET technologies in one project.</span></span> <span data-ttu-id="3a67c-110">Эта функция избавляет от необходимости выбирать одну технологию в начале проекта и заменять ее, а вместо этого способствует использованию нескольких ASP.NET платформ в рамках одного проекта.</span><span class="sxs-lookup"><span data-stu-id="3a67c-110">This feature eliminates the need to pick one technology at the start of a project and stick with it, and instead encourages the use of multiple ASP.NET frameworks within one project.</span></span>
> 
> <span data-ttu-id="3a67c-111">Все примеры кода и фрагментов включены в комплект обучающих курсов Web Camp, доступный по адресу [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="3a67c-111">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="3a67c-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="3a67c-112">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="3a67c-113">Цели</span><span class="sxs-lookup"><span data-stu-id="3a67c-113">Objectives</span></span>

<span data-ttu-id="3a67c-114">В этой практической лабораторной работе вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="3a67c-114">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="3a67c-115">Создание веб-сайта на основе одного типа проекта **ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="3a67c-115">Create a Web site based on the **One ASP.NET** project type</span></span>
- <span data-ttu-id="3a67c-116">Использование различных платформ **ASP.NET** , таких как **MVC** и **веб-API** , в одном проекте</span><span class="sxs-lookup"><span data-stu-id="3a67c-116">Use different **ASP.NET** frameworks like **MVC** and **Web API** in the same project</span></span>
- <span data-ttu-id="3a67c-117">Поиск основных компонентов приложения **ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="3a67c-117">Identify the main components of an **ASP.NET** application</span></span>
- <span data-ttu-id="3a67c-118">Воспользуйтесь преимуществами платформы **формирования шаблонов ASP.NET** , чтобы автоматически создавать контроллеры и представления для выполнения операций CRUD на основе классов модели.</span><span class="sxs-lookup"><span data-stu-id="3a67c-118">Take advantage of the **ASP.NET Scaffolding** framework to automatically create Controllers and Views to perform CRUD operations based on your model classes</span></span>
- <span data-ttu-id="3a67c-119">Предоставление одинакового набора сведений в форматах машинного и удобного для чтения данных с помощью правильного инструмента для каждого задания</span><span class="sxs-lookup"><span data-stu-id="3a67c-119">Expose the same set of information in machine- and human-readable formats using the right tool for each job</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="3a67c-120">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3a67c-120">Prerequisites</span></span>

<span data-ttu-id="3a67c-121">Для выполнения этой практической лабораторной работы требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="3a67c-121">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="3a67c-122">[Visual Studio Express 2013 для Web](https://www.microsoft.com/visualstudio/) или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="3a67c-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="3a67c-123">Visual Studio 2013 с обновлением 1</span><span class="sxs-lookup"><span data-stu-id="3a67c-123">Visual Studio 2013 Update 1</span></span>](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="3a67c-124">Настройка</span><span class="sxs-lookup"><span data-stu-id="3a67c-124">Setup</span></span>

<span data-ttu-id="3a67c-125">Чтобы выполнить упражнения в этой практической лабораторной работе, сначала необходимо настроить среду.</span><span class="sxs-lookup"><span data-stu-id="3a67c-125">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="3a67c-126">Откройте проводник Windows и перейдите к **исходной** папке лаборатории.</span><span class="sxs-lookup"><span data-stu-id="3a67c-126">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="3a67c-127">Щелкните **Setup. cmd** правой кнопкой мыши и выберите **Запуск от имени администратора** , чтобы запустить процесс установки, который будет настраивать среду и установить фрагменты кода Visual Studio для этой лабораторной работы.</span><span class="sxs-lookup"><span data-stu-id="3a67c-127">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="3a67c-128">Если отображается диалоговое окно Контроль учетных записей пользователей, подтвердите действие для продолжения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-128">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="3a67c-129">Убедитесь, что проверены все зависимости для этой лабораторной работы перед запуском программы установки.</span><span class="sxs-lookup"><span data-stu-id="3a67c-129">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="3a67c-130">Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="3a67c-130">Using the Code Snippets</span></span>

<span data-ttu-id="3a67c-131">На протяжении всего лабораторного документа вы получите инструкции по вставке блоков кода.</span><span class="sxs-lookup"><span data-stu-id="3a67c-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="3a67c-132">Для удобства большая часть этого кода предоставляется как Visual Studio Code фрагменты, к которым можно получить доступ из Visual Studio 2013, чтобы не добавлять их вручную.</span><span class="sxs-lookup"><span data-stu-id="3a67c-132">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="3a67c-133">Каждое упражнение сопровождается начальным решением, расположенным в **начальной** папке упражнения, которое позволяет выполнять каждое упражнение независимо от других.</span><span class="sxs-lookup"><span data-stu-id="3a67c-133">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="3a67c-134">Имейте в виду, что фрагменты кода, добавленные во время упражнения, отсутствуют в этих начальных решениях и могут не работать, пока вы не завершите упражнение.</span><span class="sxs-lookup"><span data-stu-id="3a67c-134">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="3a67c-135">В исходном коде для упражнения также будет найдена **Конечная** папка, содержащая решение Visual Studio с кодом, полученным в результате выполнения шагов в соответствующем упражнении.</span><span class="sxs-lookup"><span data-stu-id="3a67c-135">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="3a67c-136">Эти решения можно использовать в качестве руководства, если вам нужна дополнительная помощь во время работы с этой практической лабораторной работой.</span><span class="sxs-lookup"><span data-stu-id="3a67c-136">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="3a67c-137">Полнят</span><span class="sxs-lookup"><span data-stu-id="3a67c-137">Exercises</span></span>

<span data-ttu-id="3a67c-138">Эта практическая лабораторная работа включает в себя следующие упражнения:</span><span class="sxs-lookup"><span data-stu-id="3a67c-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="3a67c-139">Создание нового проекта веб-форм</span><span class="sxs-lookup"><span data-stu-id="3a67c-139">Creating a New Web Forms Project</span></span>](#Exercise1)
2. [<span data-ttu-id="3a67c-140">Создание контроллера MVC с помощью формирования шаблонов</span><span class="sxs-lookup"><span data-stu-id="3a67c-140">Creating an MVC Controller Using Scaffolding</span></span>](#Exercise2)
3. [<span data-ttu-id="3a67c-141">Создание контроллера веб-API с помощью формирования шаблонов</span><span class="sxs-lookup"><span data-stu-id="3a67c-141">Creating a Web API Controller Using Scaffolding</span></span>](#Exercise3)

<span data-ttu-id="3a67c-142">Предполагаемое время выполнения этой лабораторной работы: **60 минут**</span><span class="sxs-lookup"><span data-stu-id="3a67c-142">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="3a67c-143">При первом запуске Visual Studio необходимо выбрать одну из предварительно определенных коллекций параметров.</span><span class="sxs-lookup"><span data-stu-id="3a67c-143">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="3a67c-144">Каждая предопределенная коллекция разработана для соответствия определенному стилю разработки и определяет макеты окон, поведение редактора, фрагменты кода IntelliSense и параметры диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="3a67c-144">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="3a67c-145">Процедуры в этом лабораторном занятии описывают действия, необходимые для выполнения данной задачи в Visual Studio при использовании коллекции **общих параметров разработки** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-145">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="3a67c-146">При выборе другой коллекции параметров для среды разработки могут возникнуть различия в действиях, которые необходимо учитывать.</span><span class="sxs-lookup"><span data-stu-id="3a67c-146">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a><span data-ttu-id="3a67c-147">Упражнение 1. Создание нового проекта веб-форм</span><span class="sxs-lookup"><span data-stu-id="3a67c-147">Exercise 1: Creating a New Web Forms Project</span></span>

<span data-ttu-id="3a67c-148">В этом упражнении вы создадите новый сайт Web Forms в Visual Studio 2013 с помощью единого унифицированного проекта **ASP.NET** , который позволит легко интегрировать веб-формы, MVC и компоненты веб-API в одно приложение.</span><span class="sxs-lookup"><span data-stu-id="3a67c-148">In this exercise you will create a new Web Forms site in Visual Studio 2013 using the **One ASP.NET** unified project experience, which will allow you to easily integrate Web Forms, MVC and Web API components in the same application.</span></span> <span data-ttu-id="3a67c-149">Затем будет рассмотрено созданное решение и его части, и, наконец, вы увидите, что веб-сайт в действии.</span><span class="sxs-lookup"><span data-stu-id="3a67c-149">You will then explore the generated solution and identify its parts, and finally you will see the Web site in action.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a><span data-ttu-id="3a67c-150">Задача 1. Создание нового сайта с помощью одного интерфейса ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3a67c-150">Task 1 – Creating a New Site Using the One ASP.NET Experience</span></span>

<span data-ttu-id="3a67c-151">В этой задаче вы приступите к созданию нового веб-сайта в Visual Studio на основе одного типа проекта **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-151">In this task you will start creating a new Web site in Visual Studio based on the **One ASP.NET** project type.</span></span> <span data-ttu-id="3a67c-152">**Один ASP.NET** объединяет все технологии ASP.NET и дает возможность смешивать и сопоставлять их по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="3a67c-152">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="3a67c-153">Затем вы узнаете о различных компонентах веб-форм, MVC и веб-API, которые параллельно находятся в приложении.</span><span class="sxs-lookup"><span data-stu-id="3a67c-153">You will then recognize the different components of Web Forms, MVC and Web API that live side by side within your application.</span></span>

1. <span data-ttu-id="3a67c-154">Откройте **Visual Studio Express 2013 для Web** и выберите **файл | Создать проект...** для запуска нового решения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-154">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    ![Создание нового проекта](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    <span data-ttu-id="3a67c-156">*Создание нового проекта*</span><span class="sxs-lookup"><span data-stu-id="3a67c-156">*Creating a New Project*</span></span>
2. <span data-ttu-id="3a67c-157">В диалоговом окне **Новый проект** выберите **ASP.NET веб-приложение** в **визуальном C# элементе | Веб-** вкладку и убедитесь, что выбран **.NET Framework 4,5** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-157">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab, and make sure **.NET Framework 4.5** is selected.</span></span> <span data-ttu-id="3a67c-158">Назовите проект *михибридсите*, выберите **Расположение** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-158">Name the project *MyHybridSite*, choose a **Location** and click **OK**.</span></span>

    ![Новый проект веб-приложения ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    <span data-ttu-id="3a67c-160">*Создание нового проекта веб-приложения ASP.NET*</span><span class="sxs-lookup"><span data-stu-id="3a67c-160">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="3a67c-161">В диалоговом окне **Новый проект ASP.NET** выберите шаблон **веб-формы** и выберите параметры **MVC** и **веб-API** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-161">In the **New ASP.NET Project** dialog box, select the **Web Forms** template and select the **MVC** and **Web API** options.</span></span> <span data-ttu-id="3a67c-162">Кроме того, убедитесь, что для параметра **Проверка подлинности** задано значение **индивидуальные учетные записи пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-162">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="3a67c-163">Чтобы продолжить, нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-163">Click **OK** to continue.</span></span>

    ![Создание нового проекта с помощью шаблона веб-форм, включая веб-API и компоненты MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    <span data-ttu-id="3a67c-165">*Создание нового проекта с помощью шаблона веб-форм, включая веб-API и компоненты MVC*</span><span class="sxs-lookup"><span data-stu-id="3a67c-165">*Creating a new project with the Web Forms template, including Web API and MVC components*</span></span>
4. <span data-ttu-id="3a67c-166">Теперь вы можете исследовать структуру созданного решения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-166">You can now explore the structure of the generated solution.</span></span>

    ![Изучение созданного решения](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    <span data-ttu-id="3a67c-168">*Изучение созданного решения*</span><span class="sxs-lookup"><span data-stu-id="3a67c-168">*Exploring the generated solution*</span></span>

    1. <span data-ttu-id="3a67c-169">**Учетная запись:** Эта папка содержит страницы веб-форм для регистрации, входа в систему и управления учетными записями пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-169">**Account:** This folder contains the Web Form pages to register, log in to and manage the application's user accounts.</span></span> <span data-ttu-id="3a67c-170">Эта папка добавляется при выборе параметра Проверка подлинности **отдельных учетных записей пользователей** во время настройки шаблона проекта веб-форм.</span><span class="sxs-lookup"><span data-stu-id="3a67c-170">This folder is added when the **Individual User Accounts** authentication option is selected during the configuration of the Web Forms project template.</span></span>
    2. <span data-ttu-id="3a67c-171">**Модели:** В этой папке будут содержаться классы, представляющие данные приложения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-171">**Models:** This folder will contain the classes that represent your application data.</span></span>
    3. <span data-ttu-id="3a67c-172">**Контроллеры** и **представления**. Эти папки необходимы для компонентов **ASP.NET MVC** и **веб-API ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-172">**Controllers** and **Views**: These folders are required for the **ASP.NET MVC** and **ASP.NET Web API** components.</span></span> <span data-ttu-id="3a67c-173">В следующих упражнениях рассматривается технология MVC и веб-API.</span><span class="sxs-lookup"><span data-stu-id="3a67c-173">You will explore the MVC and Web API technologies in the next exercises.</span></span>
    4. <span data-ttu-id="3a67c-174">Файлы **Default. aspx**, **Contact. aspx** и **About. aspx** являются предварительно определенными страницами веб-форм, которые можно использовать в качестве начальных точек для создания страниц, относящихся к конкретному приложению.</span><span class="sxs-lookup"><span data-stu-id="3a67c-174">The **Default.aspx**, **Contact.aspx** and **About.aspx** files are pre-defined Web Form pages that you can use as starting points to build the pages specific to your application.</span></span> <span data-ttu-id="3a67c-175">Логика программирования этих файлов размещается в отдельном файле, который называется &quot;ным файлом кода&quot; программной части, который имеет расширение &quot;. aspx. vb&quot; или &quot;. aspx.cs&quot; (в зависимости от используемого языка).</span><span class="sxs-lookup"><span data-stu-id="3a67c-175">The programming logic of those files resides in a separate file referred to as the &quot;code-behind&quot; file, which has an &quot;.aspx.vb&quot; or &quot;.aspx.cs&quot; extension (depending on the language used).</span></span> <span data-ttu-id="3a67c-176">Логика кода программной части выполняется на сервере и динамически создает выходные данные HTML для страницы.</span><span class="sxs-lookup"><span data-stu-id="3a67c-176">The code-behind logic runs on the server and dynamically produces the HTML output for your page.</span></span>
    5. <span data-ttu-id="3a67c-177">Страницы **site. master** и **site. Mobile. master** определяют внешний вид и стандартное поведение всех страниц в приложении.</span><span class="sxs-lookup"><span data-stu-id="3a67c-177">The **Site.Master** and **Site.Mobile.Master** pages define the look and feel and the standard behavior of all the pages in the application.</span></span>
5. <span data-ttu-id="3a67c-178">Дважды щелкните файл **Default. aspx** , чтобы просмотреть содержимое страницы.</span><span class="sxs-lookup"><span data-stu-id="3a67c-178">Double-click the **Default.aspx** file to explore the content of the page.</span></span>

    ![Изучение страницы Default. aspx](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    <span data-ttu-id="3a67c-180">*Изучение страницы Default. aspx*</span><span class="sxs-lookup"><span data-stu-id="3a67c-180">*Exploring the Default.aspx page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a67c-181">Директива **Page** в верхней части файла определяет атрибуты страницы Web Forms.</span><span class="sxs-lookup"><span data-stu-id="3a67c-181">The **Page** directive at the top of the file defines the attributes of the Web Forms page.</span></span> <span data-ttu-id="3a67c-182">Например, атрибут **MasterPageFile** задает путь к главной странице, в данном случае — на странице *site. master* — и атрибут **Inherits** определяет класс кода программной части для наследуемой страницы.</span><span class="sxs-lookup"><span data-stu-id="3a67c-182">For example, the **MasterPageFile** attribute specifies the path to the master page -in this case, the *Site.Master* page- and the **Inherits** attribute defines the code-behind class for the page to inherit.</span></span> <span data-ttu-id="3a67c-183">Этот класс находится в файле, определяемом атрибутом **CodeBehind** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-183">This class is located in the file determined by the **CodeBehind** attribute.</span></span>
    > 
    > <span data-ttu-id="3a67c-184">Элемент управления **ASP: Content** содержит фактическое содержимое страницы (текст, разметку и элементы управления) и сопоставляется с элементом управления **ASP: ContentPlaceHolder** на главной странице.</span><span class="sxs-lookup"><span data-stu-id="3a67c-184">The **asp:Content** control holds the actual content of the page (text, markup and controls) and is mapped to a **asp:ContentPlaceHolder** control on the master page.</span></span> <span data-ttu-id="3a67c-185">В этом случае содержимое страницы будет отображаться внутри элемента управления *MainContent* , определенного на странице *site. master* .</span><span class="sxs-lookup"><span data-stu-id="3a67c-185">In this case, the page content will be rendered inside the *MainContent* control defined in the *Site.Master* page.</span></span>
6. <span data-ttu-id="3a67c-186">Разверните папку **App\_Start** и обратите внимание на файл **WebApiConfig.CS** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-186">Expand the **App\_Start** folder and notice the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="3a67c-187">Visual Studio включил этот файл в созданное решение, так как вы включили веб-API при настройке проекта с помощью шаблона "один ASP.NET".</span><span class="sxs-lookup"><span data-stu-id="3a67c-187">Visual Studio included that file in the generated solution because you included Web API when configuring your project with the One ASP.NET template.</span></span>
7. <span data-ttu-id="3a67c-188">Откройте файл **WebApiConfig.CS** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-188">Open the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="3a67c-189">В классе *WebApiConfig* вы найдете конфигурацию, связанную с веб-API, которая СОПОСТАВЛЯЕТ маршруты HTTP с **контроллерами веб-API**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-189">In the *WebApiConfig* class you will find the configuration associated with Web API, which maps HTTP routes to **Web API controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. <span data-ttu-id="3a67c-190">Откройте файл **RouteConfig.CS** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-190">Open the **RouteConfig.cs** file.</span></span> <span data-ttu-id="3a67c-191">В методе *регистерраутес* вы найдете конфигурацию, связанную с MVC, которая СОПОСТАВЛЯЕТ маршруты HTTP с **контроллерами MVC**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-191">Inside the *RegisterRoutes* method you will find the configuration associated with MVC, which maps HTTP routes to **MVC controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="3a67c-192">Задача 2. Запуск решения</span><span class="sxs-lookup"><span data-stu-id="3a67c-192">Task 2 – Running the Solution</span></span>

<span data-ttu-id="3a67c-193">В этой задаче будет запущено созданное решение, рассмотрено приложение и некоторые его функции, такие как переписывание URL-адресов и встроенная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="3a67c-193">In this task you will run the generated solution, explore the app and some of its features, like URL rewriting and built-in authentication.</span></span>

1. <span data-ttu-id="3a67c-194">Чтобы запустить решение, нажмите клавишу **F5** или кнопку **запустить** , расположенную на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="3a67c-194">To run the solution, press **F5** or click the **Start** button located on the toolbar.</span></span> <span data-ttu-id="3a67c-195">Домашняя страница приложения должна открываться в браузере.</span><span class="sxs-lookup"><span data-stu-id="3a67c-195">The application home page should open in the browser.</span></span>

    ![Запуск решения](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. <span data-ttu-id="3a67c-197">Убедитесь, что страницы веб-форм вызываются.</span><span class="sxs-lookup"><span data-stu-id="3a67c-197">Verify that the Web Forms pages are being invoked.</span></span> <span data-ttu-id="3a67c-198">Для этого добавьте **/контакт.аспкс** в URL-адрес в адресной строке и нажмите клавишу **Ввод**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-198">To do this, append **/contact.aspx** to the URL in the address bar and press **Enter**.</span></span>

    ![Понятные URL-адреса](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    <span data-ttu-id="3a67c-200">*Понятные URL-адреса*</span><span class="sxs-lookup"><span data-stu-id="3a67c-200">*Friendly URLs*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a67c-201">Как видите, URL-адрес меняется на **/контакт**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-201">As you can see, the URL changes to **/contact**.</span></span> <span data-ttu-id="3a67c-202">Начиная с **ASP.NET 4**, возможности маршрутизации URL-адресов были добавлены в веб-формы, поэтому вместо *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* можно создавать URL-адреса, такие как *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* .</span><span class="sxs-lookup"><span data-stu-id="3a67c-202">Starting from **ASP.NET 4**, URL routing capabilities were added to Web Forms, so you can write URLs like *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* instead of *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span></span> <span data-ttu-id="3a67c-203">Дополнительные сведения см. в разделе [Маршрутизация URL-адресов](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span><span class="sxs-lookup"><span data-stu-id="3a67c-203">For more information refer to [URL Routing](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span></span>
3. <span data-ttu-id="3a67c-204">Теперь мы рассмотрим поток проверки подлинности, интегрированный в приложение.</span><span class="sxs-lookup"><span data-stu-id="3a67c-204">You will now explore the authentication flow integrated into the application.</span></span> <span data-ttu-id="3a67c-205">Для этого щелкните **зарегистрировать** в правом верхнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="3a67c-205">To do this, click **Register** in the upper-right corner of the page.</span></span>

    ![Регистрация нового пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    <span data-ttu-id="3a67c-207">*Регистрация нового пользователя*</span><span class="sxs-lookup"><span data-stu-id="3a67c-207">*Registering a new user*</span></span>
4. <span data-ttu-id="3a67c-208">На странице **Регистрация** введите **имя пользователя** и **пароль**, а затем нажмите кнопку **зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-208">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    ![Страница "регистрация"](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    <span data-ttu-id="3a67c-210">*Страница "регистрация"*</span><span class="sxs-lookup"><span data-stu-id="3a67c-210">*Register page*</span></span>
5. <span data-ttu-id="3a67c-211">Приложение регистрирует новую учетную запись, и пользователь проходит проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="3a67c-211">The application registers the new account, and the user is authenticated.</span></span>

    ![Пользователь прошел проверку подлинности](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    <span data-ttu-id="3a67c-213">*Пользователь прошел проверку подлинности*</span><span class="sxs-lookup"><span data-stu-id="3a67c-213">*User authenticated*</span></span>
6. <span data-ttu-id="3a67c-214">Вернитесь в Visual Studio и нажмите клавиши **SHIFT + F5** , чтобы прерывать отладку.</span><span class="sxs-lookup"><span data-stu-id="3a67c-214">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a><span data-ttu-id="3a67c-215">Упражнение 2. Создание контроллера MVC с помощью формирования шаблонов</span><span class="sxs-lookup"><span data-stu-id="3a67c-215">Exercise 2: Creating an MVC Controller Using Scaffolding</span></span>

<span data-ttu-id="3a67c-216">В этом упражнении вы будете использовать преимущества платформы формирования шаблонов ASP.NET, предоставляемой Visual Studio для создания контроллера ASP.NET MVC 5 с действиями и представлениями Razor для выполнения операций CRUD, не написав ни одной строки кода.</span><span class="sxs-lookup"><span data-stu-id="3a67c-216">In this exercise you will take advantage of the ASP.NET Scaffolding framework provided by Visual Studio to create an ASP.NET MVC 5 controller with actions and Razor views to perform CRUD operations, without writing a single line of code.</span></span> <span data-ttu-id="3a67c-217">Процесс формирования шаблонов будет использовать Entity Framework Code First для создания контекста данных и схемы базы данных в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3a67c-217">The scaffolding process will use Entity Framework Code First to generate the data context and the database schema in the SQL database.</span></span>

<span data-ttu-id="3a67c-218">**Сведения о Entity Framework Code First**</span><span class="sxs-lookup"><span data-stu-id="3a67c-218">**About Entity Framework Code First**</span></span>

<span data-ttu-id="3a67c-219">Entity Framework (EF) — это объектно-реляционная система сопоставления (ORM), позволяющая создавать приложения для доступа к данным с помощью программирования с концептуальной моделью приложения, а не непосредственно с помощью реляционной схемы хранилища.</span><span class="sxs-lookup"><span data-stu-id="3a67c-219">Entity Framework (EF) is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span>

<span data-ttu-id="3a67c-220">Рабочий процесс моделирования Entity Framework Code First позволяет использовать собственные доменные классы для представления модели, используемой EF при выполнении запросов, функций отслеживания изменений и обновления.</span><span class="sxs-lookup"><span data-stu-id="3a67c-220">The Entity Framework Code First modeling workflow allows you to use your own domain classes to represent the model that EF relies on when performing querying, change-tracking and updating functions.</span></span> <span data-ttu-id="3a67c-221">С помощью рабочего процесса разработки Code First не нужно начинать приложение путем создания базы данных или указания схемы.</span><span class="sxs-lookup"><span data-stu-id="3a67c-221">Using the Code First development workflow, you do not need to begin your application by creating a database or specifying a schema.</span></span> <span data-ttu-id="3a67c-222">Вместо этого можно написать стандартные классы .NET, определяющие наиболее подходящие объекты модели предметной области для приложения, а Entity Framework создаст базу данных.</span><span class="sxs-lookup"><span data-stu-id="3a67c-222">Instead, you can write standard .NET classes that define the most appropriate domain model objects for your application, and Entity Framework will create the database for you.</span></span>

> [!NOTE]
> <span data-ttu-id="3a67c-223">Дополнительные сведения о Entity Framework см. [здесь](../../../entity-framework.md).</span><span class="sxs-lookup"><span data-stu-id="3a67c-223">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a><span data-ttu-id="3a67c-224">Задача 1. Создание новой модели</span><span class="sxs-lookup"><span data-stu-id="3a67c-224">Task 1 – Creating a New Model</span></span>

<span data-ttu-id="3a67c-225">Теперь вы определите класс **Person** , который будет моделью, используемой процессом формирования шаблонов для создания контроллера MVC и представлений.</span><span class="sxs-lookup"><span data-stu-id="3a67c-225">You will now define a **Person** class, which will be the model used by the scaffolding process to create the MVC controller and the views.</span></span> <span data-ttu-id="3a67c-226">Начнем с создания класса модели **Person** , и операции CRUD в контроллере будут автоматически созданы с помощью функций формирования шаблонов.</span><span class="sxs-lookup"><span data-stu-id="3a67c-226">You will start by creating a **Person** model class, and the CRUD operations in the controller will be automatically created using scaffolding features.</span></span>

1. <span data-ttu-id="3a67c-227">Откройте **Visual Studio Express 2013 для Web** и решение **михибридсите. sln** , расположенное в папке **Source/EX2-MvcScaffolding/Begin** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-227">Open **Visual Studio Express 2013 for Web** and the **MyHybridSite.sln** solution located in the **Source/Ex2-MvcScaffolding/Begin** folder.</span></span> <span data-ttu-id="3a67c-228">Кроме того, можно продолжить работу с решением, полученным в предыдущем упражнении.</span><span class="sxs-lookup"><span data-stu-id="3a67c-228">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="3a67c-229">В **Обозреватель решений**щелкните правой кнопкой мыши папку **Models** проекта **михибридсите** и выберите **Добавить | Класс...** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-229">In **Solution Explorer**, right-click the **Models** folder of the **MyHybridSite** project and select **Add | Class...**.</span></span>

    ![Добавление класса модели Person](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    <span data-ttu-id="3a67c-231">*Добавление класса модели Person*</span><span class="sxs-lookup"><span data-stu-id="3a67c-231">*Adding the Person model class*</span></span>
3. <span data-ttu-id="3a67c-232">В диалоговом окне **Добавление нового элемента** укажите имя файла *Person.CS* и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-232">In the **Add New Item** dialog box, name the file *Person.cs* and click **Add**.</span></span>

    ![Создание класса модели Person](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    <span data-ttu-id="3a67c-234">*Создание класса модели Person*</span><span class="sxs-lookup"><span data-stu-id="3a67c-234">*Creating the Person model class*</span></span>
4. <span data-ttu-id="3a67c-235">Замените содержимое файла **Person.CS** следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="3a67c-235">Replace the content of the **Person.cs** file with the following code.</span></span> <span data-ttu-id="3a67c-236">Нажмите клавиши **CTRL + S** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-236">Press **CTRL + S** to save the changes.</span></span>

    <span data-ttu-id="3a67c-237">(Фрагмент кода — *брингингтожесеронеаспнет-EX2-персонкласс*)</span><span class="sxs-lookup"><span data-stu-id="3a67c-237">(Code Snippet - *BringingTogetherOneAspNet - Ex2 - PersonClass*)</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. <span data-ttu-id="3a67c-238">В **Обозреватель решений**щелкните правой кнопкой мыши проект **михибридсите** и выберите пункт **Сборка**или нажмите клавиши **CTRL + SHIFT + B** , чтобы выполнить сборку проекта.</span><span class="sxs-lookup"><span data-stu-id="3a67c-238">In **Solution Explorer**, right-click the **MyHybridSite** project and select **Build**, or press **CTRL + SHIFT + B** to build the project.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a><span data-ttu-id="3a67c-239">Задача 2. Создание контроллера MVC</span><span class="sxs-lookup"><span data-stu-id="3a67c-239">Task 2 – Creating an MVC Controller</span></span>

<span data-ttu-id="3a67c-240">Теперь, когда модель **Person** создана, вы будете использовать формирование шаблонов ASP.NET MVC с Entity Framework, чтобы создать действия и представления контроллера CRUD для **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-240">Now that the **Person** model is created, you will use ASP.NET MVC scaffolding with Entity Framework to create the CRUD controller actions and views for **Person**.</span></span>

1. <span data-ttu-id="3a67c-241">В **Обозреватель решений**щелкните правой кнопкой мыши папку **Controllers** проекта **михибридсите** и выберите **Добавить | Создать шаблонный элемент...**</span><span class="sxs-lookup"><span data-stu-id="3a67c-241">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![Создание нового шаблона контроллера](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    <span data-ttu-id="3a67c-243">*Создание нового шаблона контроллера*</span><span class="sxs-lookup"><span data-stu-id="3a67c-243">*Creating a new Scaffolded Controller*</span></span>
2. <span data-ttu-id="3a67c-244">В диалоговом окне **Добавление шаблона** выберите **контроллер MVC 5 с представлениями, используя Entity Framework** и нажмите кнопку **Добавить.**</span><span class="sxs-lookup"><span data-stu-id="3a67c-244">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework** and then click **Add.**</span></span>

    ![Выбор контроллера MVC 5 с представлениями и Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    <span data-ttu-id="3a67c-246">*Выбор контроллера MVC 5 с представлениями и Entity Framework*</span><span class="sxs-lookup"><span data-stu-id="3a67c-246">*Selecting MVC 5 Controller with views and Entity Framework*</span></span>
3. <span data-ttu-id="3a67c-247">Задайте *мвкперсонконтроллер* в качестве **имени контроллера**, выберите параметр **использовать действия асинхронного контроллера** и выберите **Person (михибридсите. Models)** в качестве **класса модели**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-247">Set *MvcPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** as the **Model class**.</span></span>

    ![Добавление контроллера MVC с формированием шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    <span data-ttu-id="3a67c-249">*Добавление контроллера MVC с формированием шаблонов*</span><span class="sxs-lookup"><span data-stu-id="3a67c-249">*Adding an MVC controller with scaffolding*</span></span>
4. <span data-ttu-id="3a67c-250">В разделе **класс контекста данных**щелкните **создать контекст данных.** ...</span><span class="sxs-lookup"><span data-stu-id="3a67c-250">Under **Data context class**, click **New data context...**.</span></span>

    ![Создание нового контекста данных](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    <span data-ttu-id="3a67c-252">*Создание нового контекста данных*</span><span class="sxs-lookup"><span data-stu-id="3a67c-252">*Creating a new data context*</span></span>
5. <span data-ttu-id="3a67c-253">В диалоговом окне **новый контекст данных** введите имя нового контекста данных *персонконтекст* и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-253">In the **New Data Context** dialog box, name the new data context *PersonContext* and click **Add**.</span></span>

    ![Создание нового Персонконтекст](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    <span data-ttu-id="3a67c-255">*Создание нового типа Персонконтекст*</span><span class="sxs-lookup"><span data-stu-id="3a67c-255">*Creating the new PersonContext type*</span></span>
6. <span data-ttu-id="3a67c-256">Нажмите кнопку **Добавить** , чтобы создать новый контроллер для **пользователя** с формированием шаблонов.</span><span class="sxs-lookup"><span data-stu-id="3a67c-256">Click **Add** to create the new controller for **Person** with scaffolding.</span></span> <span data-ttu-id="3a67c-257">Visual Studio создаст действия контроллера, контекст данных Person и представления Razor.</span><span class="sxs-lookup"><span data-stu-id="3a67c-257">Visual Studio will then generate the controller actions, the Person data context and the Razor views.</span></span>

    ![После создания контроллера MVC с формированием шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    <span data-ttu-id="3a67c-259">*После создания контроллера MVC с формированием шаблонов*</span><span class="sxs-lookup"><span data-stu-id="3a67c-259">*After creating the MVC controller with scaffolding*</span></span>
7. <span data-ttu-id="3a67c-260">Откройте файл **MvcPersonController.CS** в папке **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-260">Open the **MvcPersonController.cs** file in the **Controllers** folder.</span></span> <span data-ttu-id="3a67c-261">Обратите внимание, что методы действия CRUD были созданы автоматически.</span><span class="sxs-lookup"><span data-stu-id="3a67c-261">Notice that the CRUD action methods have been generated automatically.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > <span data-ttu-id="3a67c-262">Установив флажок **использовать действия асинхронного контроллера** из параметров формирования шаблонов на предыдущих шагах, Visual Studio создает асинхронные методы действия для всех действий, которые задействуют доступ к контексту данных Person.</span><span class="sxs-lookup"><span data-stu-id="3a67c-262">By selecting the **Use async controller actions** check box from the scaffolding options in the previous steps, Visual Studio generates asynchronous action methods for all actions that involve access to the Person data context.</span></span> <span data-ttu-id="3a67c-263">Рекомендуется использовать асинхронные методы действий для длительно выполняющихся запросов, не связанных с ЦП, чтобы предотвратить выполнение работы веб-сервером во время обработки запроса.</span><span class="sxs-lookup"><span data-stu-id="3a67c-263">It is recommended that you use asynchronous action methods for long-running, non-CPU bound requests to avoid blocking the Web server from performing work while the request is being processed.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="3a67c-264">Задача 3. Запуск решения</span><span class="sxs-lookup"><span data-stu-id="3a67c-264">Task 3 – Running the Solution</span></span>

<span data-ttu-id="3a67c-265">В этой задаче будет снова запущено решение, чтобы убедиться, что представления для **пользователя** работают должным образом.</span><span class="sxs-lookup"><span data-stu-id="3a67c-265">In this task, you will run the solution again to verify that the views for **Person** are working as expected.</span></span> <span data-ttu-id="3a67c-266">Вы добавите нового пользователя, чтобы убедиться, что оно успешно сохранено в базе данных.</span><span class="sxs-lookup"><span data-stu-id="3a67c-266">You will add a new person to verify that it is successfully saved to the database.</span></span>

1. <span data-ttu-id="3a67c-267">Чтобы запустить решение, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-267">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="3a67c-268">Перейдите по адресу **/мвкперсон**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-268">Navigate to **/MvcPerson**.</span></span> <span data-ttu-id="3a67c-269">Представление с формированием шаблонов, в котором отображается список людей.</span><span class="sxs-lookup"><span data-stu-id="3a67c-269">The scaffolded view that shows the list of people should appear.</span></span>
3. <span data-ttu-id="3a67c-270">Щелкните **создать** , чтобы добавить нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="3a67c-270">Click **Create New** to add a new person.</span></span>

    ![Переход к формированию сформированных представлений MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    <span data-ttu-id="3a67c-272">*Переход к формированию сформированных представлений MVC*</span><span class="sxs-lookup"><span data-stu-id="3a67c-272">*Navigating to the scaffolded MVC views*</span></span>
4. <span data-ttu-id="3a67c-273">В представлении **создать** укажите **имя** и **возраст** пользователя, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-273">In the **Create** view, provide a **Name** and an **Age** for the person, and click **Create**.</span></span>

    ![Добавление нового пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    <span data-ttu-id="3a67c-275">*Добавление нового пользователя*</span><span class="sxs-lookup"><span data-stu-id="3a67c-275">*Adding a new person*</span></span>
5. <span data-ttu-id="3a67c-276">Новый пользователь будет добавлен в список.</span><span class="sxs-lookup"><span data-stu-id="3a67c-276">The new person is added to the list.</span></span> <span data-ttu-id="3a67c-277">В списке элемент щелкните **сведения** , чтобы отобразить представление сведений о лице.</span><span class="sxs-lookup"><span data-stu-id="3a67c-277">In the element list, click **Details** to display the person's details view.</span></span> <span data-ttu-id="3a67c-278">Затем в представлении " **сведения** " нажмите кнопку **назад к списку** , чтобы вернуться к представлению списка.</span><span class="sxs-lookup"><span data-stu-id="3a67c-278">Then, in the **Details** view, click **Back to List** to go back to the list view.</span></span>

    ![Представление сведений о лице](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    <span data-ttu-id="3a67c-280">*Представление сведений о лице*</span><span class="sxs-lookup"><span data-stu-id="3a67c-280">*Person's details view*</span></span>
6. <span data-ttu-id="3a67c-281">Щелкните ссылку **Удалить** , чтобы удалить пользователя.</span><span class="sxs-lookup"><span data-stu-id="3a67c-281">Click the **Delete** link to delete the person.</span></span> <span data-ttu-id="3a67c-282">В представлении **Удаление** нажмите кнопку **Удалить** , чтобы подтвердить операцию.</span><span class="sxs-lookup"><span data-stu-id="3a67c-282">In the **Delete** view, click **Delete** to confirm the operation.</span></span>

    ![Удаление пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    <span data-ttu-id="3a67c-284">*Удаление пользователя*</span><span class="sxs-lookup"><span data-stu-id="3a67c-284">*Deleting a person*</span></span>
7. <span data-ttu-id="3a67c-285">Вернитесь в Visual Studio и нажмите клавиши **SHIFT + F5** , чтобы прерывать отладку.</span><span class="sxs-lookup"><span data-stu-id="3a67c-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a><span data-ttu-id="3a67c-286">Упражнение 3. Создание контроллера веб-API с помощью формирования шаблонов</span><span class="sxs-lookup"><span data-stu-id="3a67c-286">Exercise 3: Creating a Web API Controller Using Scaffolding</span></span>

<span data-ttu-id="3a67c-287">Платформа веб-API является частью стека ASP.NET и предназначена для упрощения реализации служб HTTP, которая обычно отправляет и получает данные в формате JSON или XML через API RESTFUL.</span><span class="sxs-lookup"><span data-stu-id="3a67c-287">The Web API framework is part of the ASP.NET Stack and designed to make implementing HTTP services easier, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span>

<span data-ttu-id="3a67c-288">В этом упражнении для создания контроллера веб-API будет использоваться формирование шаблонов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3a67c-288">In this exercise, you will use ASP.NET Scaffolding again to generate a Web API controller.</span></span> <span data-ttu-id="3a67c-289">Вы будете использовать те же классы **Person** и **персонконтекст** из предыдущего упражнения, чтобы предоставить одни и те же данные пользователя в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="3a67c-289">You will use the same **Person** and **PersonContext** classes from the previous exercise to provide the same person data in JSON format.</span></span> <span data-ttu-id="3a67c-290">Вы увидите, как можно предоставить одни и те же ресурсы различными способами в рамках одного приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3a67c-290">You will see how you can expose the same resources in different ways within the same ASP.NET application.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a><span data-ttu-id="3a67c-291">Задача 1. Создание контроллера веб-API</span><span class="sxs-lookup"><span data-stu-id="3a67c-291">Task 1 – Creating a Web API Controller</span></span>

<span data-ttu-id="3a67c-292">В этой задаче вы создадите новый **контроллер веб-API** , который будет предоставлять данные о пользователях в используемом для компьютера формате, например JSON.</span><span class="sxs-lookup"><span data-stu-id="3a67c-292">In this task you will create a new **Web API Controller** that will expose the person data in a machine-consumable format like JSON.</span></span>

1. <span data-ttu-id="3a67c-293">Если он еще не открыт, откройте **Visual Studio Express 2013 для Web** и откройте решение **михибридсите. sln** , расположенное в папке **Source/EX3-WebAPI/Begin** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-293">If not already opened, open **Visual Studio Express 2013 for Web** and open the **MyHybridSite.sln** solution located in the **Source/Ex3-WebAPI/Begin** folder.</span></span> <span data-ttu-id="3a67c-294">Кроме того, можно продолжить работу с решением, полученным в предыдущем упражнении.</span><span class="sxs-lookup"><span data-stu-id="3a67c-294">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a67c-295">Если вы начинаете с упражнения 3, нажмите клавиши **CTRL + SHIFT + B** , чтобы создать решение.</span><span class="sxs-lookup"><span data-stu-id="3a67c-295">If you start with the Begin solution from Exercise 3, press **CTRL + SHIFT + B** to build the solution.</span></span>
2. <span data-ttu-id="3a67c-296">В **Обозреватель решений**щелкните правой кнопкой мыши папку **Controllers** проекта **михибридсите** и выберите **Добавить | Создать шаблонный элемент...**</span><span class="sxs-lookup"><span data-stu-id="3a67c-296">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![Создание нового шаблона контроллера](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    <span data-ttu-id="3a67c-298">*Создание нового шаблона контроллера*</span><span class="sxs-lookup"><span data-stu-id="3a67c-298">*Creating a new scaffolded Controller*</span></span>
3. <span data-ttu-id="3a67c-299">В диалоговом окне **Добавление шаблона** в области слева выберите **веб-API** , затем **контроллер Web API 2 с действиями, с помощью Entity Framework** в средней области и нажмите кнопку **Добавить.**</span><span class="sxs-lookup"><span data-stu-id="3a67c-299">In the **Add Scaffold** dialog box, select **Web API** in the left pane, then **Web API 2 Controller with actions, using Entity Framework** in the middle pane and then click **Add.**</span></span>

    <span data-ttu-id="3a67c-300">![Выбор контроллера веб-API 2 с действиями и Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Выбор контроллера веб-API 2 с действиями и Entity Framework")</span><span class="sxs-lookup"><span data-stu-id="3a67c-300">![Selecting Web API 2 Controller with actions and Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Selecting Web API 2 Controller with actions and Entity Framework")</span></span>

    <span data-ttu-id="3a67c-301">*Выбор контроллера веб-API 2 с действиями и Entity Framework*</span><span class="sxs-lookup"><span data-stu-id="3a67c-301">*Selecting Web API 2 Controller with actions and Entity Framework*</span></span>
4. <span data-ttu-id="3a67c-302">Задайте *апиперсонконтроллер* в качестве **имени контроллера**, выберите параметр **использовать действия асинхронного контроллера** **и в качестве** классов **контекста данных** выберите **Person (михибридсите. Models)** и **персонконтекст (михибридсите. Models)** соответственно.</span><span class="sxs-lookup"><span data-stu-id="3a67c-302">Set *ApiPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** and **PersonContext (MyHybridSite.Models)** as the **Model** and **Data context** classes respectively.</span></span> <span data-ttu-id="3a67c-303">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-303">Then click **Add**.</span></span>

    <span data-ttu-id="3a67c-304">![Добавление контроллера веб-API с формированием шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Добавление контроллера веб-API с формированием шаблонов")</span><span class="sxs-lookup"><span data-stu-id="3a67c-304">![Adding a Web API Controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Adding a Web API controller with scaffolding")</span></span>

    <span data-ttu-id="3a67c-305">*Добавление контроллера веб-API с формированием шаблонов*</span><span class="sxs-lookup"><span data-stu-id="3a67c-305">*Adding a Web API controller with scaffolding*</span></span>
5. <span data-ttu-id="3a67c-306">Visual Studio создаст класс **апиперсонконтроллер** с четырьмя действиями CRUD для работы с данными.</span><span class="sxs-lookup"><span data-stu-id="3a67c-306">Visual Studio will then generate the **ApiPersonController** class with the four CRUD actions to work with your data.</span></span>

    <span data-ttu-id="3a67c-307">![После создания контроллера веб-API с формированием шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "После создания контроллера веб-API с формированием шаблонов")</span><span class="sxs-lookup"><span data-stu-id="3a67c-307">![After creating the Web API controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "After creating the Web API controller with scaffolding")</span></span>

    <span data-ttu-id="3a67c-308">*После создания контроллера веб-API с формированием шаблонов*</span><span class="sxs-lookup"><span data-stu-id="3a67c-308">*After creating the Web API controller with scaffolding*</span></span>
6. <span data-ttu-id="3a67c-309">Откройте файл **ApiPersonController.CS** и проверьте метод действия для *пользователей* .</span><span class="sxs-lookup"><span data-stu-id="3a67c-309">Open the **ApiPersonController.cs** file and inspect the *GetPeople* action method.</span></span> <span data-ttu-id="3a67c-310">Этот метод запрашивает поле базы данных типа **персонконтекст** , чтобы получить данные о людях.</span><span class="sxs-lookup"><span data-stu-id="3a67c-310">This method queries the db field of **PersonContext** type in order to get the people data.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. <span data-ttu-id="3a67c-311">Теперь обратите внимание на комментарий над определением метода.</span><span class="sxs-lookup"><span data-stu-id="3a67c-311">Now notice the comment above the method definition.</span></span> <span data-ttu-id="3a67c-312">Он предоставляет универсальный код ресурса (URI), который предоставляет это действие, которое будет использоваться в следующей задаче.</span><span class="sxs-lookup"><span data-stu-id="3a67c-312">It provides the URI that exposes this action which you will use in the next task.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="3a67c-313">По умолчанию веб-API настроен для перехвата запросов к */API* пути во избежание конфликтов с контроллерами MVC.</span><span class="sxs-lookup"><span data-stu-id="3a67c-313">By default, Web API is configured to catch the queries to the */api* path to avoid collisions with MVC controllers.</span></span> <span data-ttu-id="3a67c-314">Если необходимо изменить этот параметр, см. сведения в разделе [Маршрутизация в веб-API ASP.NET](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="3a67c-314">If you need to change this setting, refer to [Routing in ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="3a67c-315">Задача 2. Запуск решения</span><span class="sxs-lookup"><span data-stu-id="3a67c-315">Task 2 – Running the Solution</span></span>

<span data-ttu-id="3a67c-316">В этой задаче вы будете использовать **средства разработчика F12** для Internet Explorer, чтобы проверить полный ответ от контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="3a67c-316">In this task you will use the Internet Explorer **F12 developer tools** to inspect the full response from the Web API controller.</span></span> <span data-ttu-id="3a67c-317">Вы увидите, как можно захватить сетевой трафик, чтобы получить более подробные сведения о данных приложения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-317">You will see how you can capture network traffic to get more insight into your application data.</span></span>

> [!NOTE]
> <span data-ttu-id="3a67c-318">Убедитесь, что в кнопке **Пуск** на панели инструментов Visual Studio выбран параметр **Internet Explorer** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-318">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Параметр Internet Explorer](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> <span data-ttu-id="3a67c-320">**Средства разработчика F12** имеют широкий набор функциональных возможностей, которые не рассматриваются в этом практическом занятии.</span><span class="sxs-lookup"><span data-stu-id="3a67c-320">The **F12 developer tools** have a wide set of functionality that is not covered in this hands-on-lab.</span></span> <span data-ttu-id="3a67c-321">Дополнительные сведения об этом см. в статье [использование средств разработчика F12](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="3a67c-321">If you want to learn more about it, refer to [Using the F12 developer tools](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span></span>

1. <span data-ttu-id="3a67c-322">Чтобы запустить решение, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-322">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a67c-323">Чтобы правильно выполнить эту задачу, приложение должно иметь данные.</span><span class="sxs-lookup"><span data-stu-id="3a67c-323">In order to follow this task correctly, your application needs to have data.</span></span> <span data-ttu-id="3a67c-324">Если база данных пуста, можно вернуться к задаче 3 в упражнении 2 и выполнить инструкции по созданию нового пользователя с помощью представлений MVC.</span><span class="sxs-lookup"><span data-stu-id="3a67c-324">If your database is empty, you can go back to Task 3 in Exercise 2 and follow the steps on how to create a new person using the MVC views.</span></span>
2. <span data-ttu-id="3a67c-325">В браузере нажмите клавишу **F12** , чтобы открыть панель **средства для разработчиков** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-325">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="3a67c-326">Нажмите **сочетание клавиш CTRL** + **4** или щелкните значок **сети** , а затем нажмите кнопку с зеленой стрелкой, чтобы начать запись сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="3a67c-326">Press **CTRL** + **4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="3a67c-327">![Инициация записи сети веб-API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Инициация записи сети веб-API")</span><span class="sxs-lookup"><span data-stu-id="3a67c-327">![Initiating Web API network capture](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="3a67c-328">*Инициация записи сети веб-API*</span><span class="sxs-lookup"><span data-stu-id="3a67c-328">*Initiating Web API network capture*</span></span>
3. <span data-ttu-id="3a67c-329">Добавьте **API/апиперсон** в URL-адрес в адресной строке браузера.</span><span class="sxs-lookup"><span data-stu-id="3a67c-329">Append **api/ApiPerson** to the URL in the browser's address bar.</span></span> <span data-ttu-id="3a67c-330">Теперь вы проверите сведения о ответе в **апиперсонконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-330">You will now inspect the details of the response from the **ApiPersonController**.</span></span>

    <span data-ttu-id="3a67c-331">![Получение данных Person через веб-API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Получение данных Person через веб-API")</span><span class="sxs-lookup"><span data-stu-id="3a67c-331">![Retrieving person data through Web API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Retrieving person data through Web API")</span></span>

    <span data-ttu-id="3a67c-332">*Получение данных Person через веб-API*</span><span class="sxs-lookup"><span data-stu-id="3a67c-332">*Retrieving person data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a67c-333">После завершения загрузки вам будет предложено выполнить действие с скачанным файлом.</span><span class="sxs-lookup"><span data-stu-id="3a67c-333">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="3a67c-334">Оставьте диалоговое окно открытым, чтобы иметь возможность просматривать содержимое ответа через окно инструментов разработчиков.</span><span class="sxs-lookup"><span data-stu-id="3a67c-334">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
4. <span data-ttu-id="3a67c-335">Теперь вы проверите текст ответа.</span><span class="sxs-lookup"><span data-stu-id="3a67c-335">Now you will inspect the body of the response.</span></span> <span data-ttu-id="3a67c-336">Для этого перейдите на вкладку **сведения** и щелкните **текст ответа**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-336">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="3a67c-337">Можно проверить, что загруженные данные представляют собой список объектов со свойствами **ID**, **Name** и **Age** , которые соответствуют классу **Person** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-337">You can check that the downloaded data is a list of objects with the properties **Id**, **Name** and **Age** that correspond to the **Person** class.</span></span>

    <span data-ttu-id="3a67c-338">![Просмотр текста ответа веб-API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Просмотр текста ответа веб-API")</span><span class="sxs-lookup"><span data-stu-id="3a67c-338">![Viewing Web API Response Body](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Viewing Web API Response Body")</span></span>

    <span data-ttu-id="3a67c-339">*Просмотр текста ответа веб-API*</span><span class="sxs-lookup"><span data-stu-id="3a67c-339">*Viewing Web API Response Body*</span></span>

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a><span data-ttu-id="3a67c-340">Задача 3. Добавление страниц справки по веб-API</span><span class="sxs-lookup"><span data-stu-id="3a67c-340">Task 3 – Adding Web API Help Pages</span></span>

<span data-ttu-id="3a67c-341">При создании веб-API полезно создать страницу справки, чтобы другие разработчики узнают, как вызывать API.</span><span class="sxs-lookup"><span data-stu-id="3a67c-341">When you create a Web API, it is useful to create a help page so that other developers will know how to call your API.</span></span> <span data-ttu-id="3a67c-342">Можно создавать и обновлять страницы документации вручную, но лучше создавать их автоматически, чтобы не выполнять обслуживание.</span><span class="sxs-lookup"><span data-stu-id="3a67c-342">You could create and update the documentation pages manually, but it is better to auto-generate them to avoid having to do maintenance work.</span></span> <span data-ttu-id="3a67c-343">В этой задаче будет использоваться пакет NuGet для автоматического создания страниц справки веб-API для решения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-343">In this task you will use a Nuget package to automatically generate Web API help pages to the solution.</span></span>

1. <span data-ttu-id="3a67c-344">В меню **Сервис** в Visual Studio выберите **Диспетчер пакетов NuGet**, а затем щелкните **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-344">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="3a67c-345">В окне **консоли диспетчера пакетов** выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3a67c-345">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > <span data-ttu-id="3a67c-346">Пакет **Microsoft. AspNet. WebApi. хелппаже** устанавливает необходимые сборки и добавляет представления MVC для страниц справки в папке **Areas/хелппаже** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-346">The **Microsoft.AspNet.WebApi.HelpPage** package installs the necessary assemblies and adds MVC Views for the help pages under the **Areas/HelpPage** folder.</span></span>

    <span data-ttu-id="3a67c-347">![Область Хелппаже](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "Область Хелппаже")</span><span class="sxs-lookup"><span data-stu-id="3a67c-347">![HelpPage Area](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage Area")</span></span>

    <span data-ttu-id="3a67c-348">*Область Хелппаже*</span><span class="sxs-lookup"><span data-stu-id="3a67c-348">*HelpPage Area*</span></span>
3. <span data-ttu-id="3a67c-349">По умолчанию страницы справки содержат строки заполнителей для документации.</span><span class="sxs-lookup"><span data-stu-id="3a67c-349">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="3a67c-350">Для создания документации можно использовать комментарии XML-документации.</span><span class="sxs-lookup"><span data-stu-id="3a67c-350">You can use XML documentation comments to create the documentation.</span></span> <span data-ttu-id="3a67c-351">Чтобы включить эту функцию, откройте файл **HelpPageConfig.CS** , расположенный в папке **Areas/хелппаже/App\_Start** , и раскомментируйте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="3a67c-351">To enable this feature, open the **HelpPageConfig.cs** file located in the **Areas/HelpPage/App\_Start** folder and uncomment the following line:</span></span>

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. <span data-ttu-id="3a67c-352">В **Обозреватель решений**щелкните правой кнопкой мыши проект **михибридсите**, выберите пункт **Свойства** и перейдите на вкладку **Сборка** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-352">In **Solution Explorer**, right-click the project **MyHybridSite**, select **Properties** and click the **Build** tab.</span></span>

    <span data-ttu-id="3a67c-353">![Вкладка "сборка"](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Раздел "сборка"")</span><span class="sxs-lookup"><span data-stu-id="3a67c-353">![Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Build section")</span></span>

    <span data-ttu-id="3a67c-354">*Вкладка "сборка"*</span><span class="sxs-lookup"><span data-stu-id="3a67c-354">*Build tab*</span></span>
5. <span data-ttu-id="3a67c-355">В разделе **выходные данные**выберите **XML-файл документации**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-355">Under **Output**, select **XML documentation file**.</span></span> <span data-ttu-id="3a67c-356">В поле ввода введите **App\_Data/XmlDocument. XML**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-356">In the edit box, type **App\_Data/XmlDocument.xml**.</span></span>

    <span data-ttu-id="3a67c-357">![Раздел выходных данных на вкладке "сборка"](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Раздел выходных данных на вкладке "сборка"")</span><span class="sxs-lookup"><span data-stu-id="3a67c-357">![Output section in Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Output section in build tab")</span></span>

    <span data-ttu-id="3a67c-358">*Раздел выходных данных на вкладке "сборка"*</span><span class="sxs-lookup"><span data-stu-id="3a67c-358">*Output section in Build tab*</span></span>
6. <span data-ttu-id="3a67c-359">Нажмите клавиши **CTRL** + **S** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-359">Press **CTRL** + **S** to save the changes.</span></span>
7. <span data-ttu-id="3a67c-360">Откройте файл **ApiPersonController.CS** в папке **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-360">Open the **ApiPersonController.cs** file from the **Controllers** folder.</span></span>
8. <span data-ttu-id="3a67c-361">Введите новую строку между сигнатурой *метода апиперсон* и комментарием *//Get API/* , а затем введите три косые черты.</span><span class="sxs-lookup"><span data-stu-id="3a67c-361">Enter a new line between the *GetPeople* method signature and the *// GET api/ApiPerson* comment, and then type three forward slashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a67c-362">Visual Studio автоматически вставляет XML-элементы, определяющие документацию по методам.</span><span class="sxs-lookup"><span data-stu-id="3a67c-362">Visual Studio automatically inserts the XML elements which define the method documentation.</span></span>
9. <span data-ttu-id="3a67c-363">Добавьте текст сводки и возвращаемое значение для метода *People* .</span><span class="sxs-lookup"><span data-stu-id="3a67c-363">Add a summary text and the return value for the *GetPeople* method.</span></span> <span data-ttu-id="3a67c-364">Он должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="3a67c-364">It should look like the following.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. <span data-ttu-id="3a67c-365">Чтобы запустить решение, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="3a67c-365">Press **F5** to run the solution.</span></span>
11. <span data-ttu-id="3a67c-366">Добавьте **/Help** в URL-адрес в адресной строке, чтобы перейти на страницу справки.</span><span class="sxs-lookup"><span data-stu-id="3a67c-366">Append **/help** to the URL in the address bar to browse to the help page.</span></span>

    <span data-ttu-id="3a67c-367">![Страница справки веб-API ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "Страница справки веб-API ASP.NET")</span><span class="sxs-lookup"><span data-stu-id="3a67c-367">![ASP.NET Web API Help Page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Help Page")</span></span>

    <span data-ttu-id="3a67c-368">*Страница справки веб-API ASP.NET*</span><span class="sxs-lookup"><span data-stu-id="3a67c-368">*ASP.NET Web API Help Page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a67c-369">Основное содержимое страницы — это таблица API-интерфейсов, сгруппированных по контроллеру.</span><span class="sxs-lookup"><span data-stu-id="3a67c-369">The main content of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="3a67c-370">Записи таблицы создаются динамически с помощью интерфейса **иапиексплорер** .</span><span class="sxs-lookup"><span data-stu-id="3a67c-370">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="3a67c-371">При добавлении или обновлении контроллера API таблица будет автоматически обновляться при следующей сборке приложения.</span><span class="sxs-lookup"><span data-stu-id="3a67c-371">If you add or update an API controller, the table will be automatically updated the next time you build the application.</span></span>
    > 
    > <span data-ttu-id="3a67c-372">В столбце **API** перечисляются метод HTTP и относительный URI.</span><span class="sxs-lookup"><span data-stu-id="3a67c-372">The **API** column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="3a67c-373">В столбце **Описание** содержатся сведения, извлеченные из документации по методу.</span><span class="sxs-lookup"><span data-stu-id="3a67c-373">The **Description** column contains information that has been extracted from the method's documentation.</span></span>
12. <span data-ttu-id="3a67c-374">Обратите внимание, что описание, добавленное над определением метода, отображается в столбце Описание.</span><span class="sxs-lookup"><span data-stu-id="3a67c-374">Note that the description you added above the method definition is displayed in the description column.</span></span>

    <span data-ttu-id="3a67c-375">![Описание метода API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "Описание метода API")</span><span class="sxs-lookup"><span data-stu-id="3a67c-375">![API method description](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API method description")</span></span>

    <span data-ttu-id="3a67c-376">*Описание метода API*</span><span class="sxs-lookup"><span data-stu-id="3a67c-376">*API method description*</span></span>
13. <span data-ttu-id="3a67c-377">Щелкните один из методов API, чтобы переходить к странице с более подробными сведениями, включая образцы текстов ответов.</span><span class="sxs-lookup"><span data-stu-id="3a67c-377">Click one of the API methods to navigate to a page with more detailed information, including sample response bodies.</span></span>

    <span data-ttu-id="3a67c-378">![Страница сведений](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Страница сведений")</span><span class="sxs-lookup"><span data-stu-id="3a67c-378">![Detail Information page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Detail Information page")</span></span>

    <span data-ttu-id="3a67c-379">*Страница подробных сведений*</span><span class="sxs-lookup"><span data-stu-id="3a67c-379">*Detailed information page*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="3a67c-380">Сводка</span><span class="sxs-lookup"><span data-stu-id="3a67c-380">Summary</span></span>

<span data-ttu-id="3a67c-381">С помощью этой практической лабораторной работы вы узнали, как:</span><span class="sxs-lookup"><span data-stu-id="3a67c-381">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="3a67c-382">Создание нового веб-приложения с помощью одного интерфейса ASP.NET в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3a67c-382">Create a new Web application using the One ASP.NET Experience in Visual Studio 2013</span></span>
- <span data-ttu-id="3a67c-383">Интеграция нескольких ASP.NET технологий в один проект</span><span class="sxs-lookup"><span data-stu-id="3a67c-383">Integrate multiple ASP.NET technologies into one single project</span></span>
- <span data-ttu-id="3a67c-384">Создание контроллеров и представлений MVC из классов модели с помощью формирования шаблонов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3a67c-384">Generate MVC controllers and views from your model classes using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="3a67c-385">Создание контроллеров веб-API, использующих такие функции, как асинхронное программирование и доступ к данным с помощью Entity Framework</span><span class="sxs-lookup"><span data-stu-id="3a67c-385">Generate Web API controllers, which use features such as Async Programming and data access through Entity Framework</span></span>
- <span data-ttu-id="3a67c-386">Автоматическое создание страниц справки по веб-API для контроллеров</span><span class="sxs-lookup"><span data-stu-id="3a67c-386">Automatically generate Web API Help Pages for your controllers</span></span>
