---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 'Практическое занятие: Visual Studio 2013 веб-средств | Документация Майкрософт'
author: rick-anderson
description: Visual Studio — отличная среда разработки для. NET-Windows и веб-проекты. Он содержит мощный текстовый редактор, который можно легко использовать в...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505008"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="b6cc9-104">Практические занятия: Visual Studio 2013 веб-инструменты</span><span class="sxs-lookup"><span data-stu-id="b6cc9-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>

<span data-ttu-id="b6cc9-105">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="b6cc9-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="b6cc9-106">Скачать обучающий комплект Web Camp</span><span class="sxs-lookup"><span data-stu-id="b6cc9-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="b6cc9-107">Visual Studio — отличная среда разработки для. NET-Windows и веб-проекты.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="b6cc9-108">Он содержит мощный текстовый редактор, который можно легко использовать для редактирования отдельных файлов без проекта.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="b6cc9-109">Visual Studio поддерживает полнофункциональное дерево синтаксического анализа при редактировании каждого файла.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="b6cc9-110">Это позволяет Visual Studio обеспечивать непараллельное автоматическое завершение и действия на основе документов, одновременно делая процесс разработки более быстрым и более приятный.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="b6cc9-111">Эти функции особенно эффективны в документах HTML и CSS.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="b6cc9-112">Все эти возможности также доступны для расширений, что упрощает расширение редакторов с помощью мощных новых функций в соответствии с вашими потребностями.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="b6cc9-113">Web Essentials — это набор (в основном) веб-усовершенствований Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="b6cc9-114">Он включает множество новых функций завершения IntelliSense (особенно для CSS), новые функции связи с браузером, автоматическое Жшинт для файлов JavaScript, новые предупреждения для HTML и CSS и многие другие функции, которые необходимы для современной разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="b6cc9-115">Все примеры кода и фрагментов включены в комплект обучающих курсов Web Camp, доступный по адресу [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="b6cc9-115">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="b6cc9-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="b6cc9-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b6cc9-117">Цели</span><span class="sxs-lookup"><span data-stu-id="b6cc9-117">Objectives</span></span>

<span data-ttu-id="b6cc9-118">В этой практической лабораторной работе вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="b6cc9-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="b6cc9-119">Используйте новые функции редактора HTML, содержащиеся в веб-Essentials, такие как Расширенные фрагменты кода HTML5 и Zen код.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="b6cc9-120">Использование новых функций редактора CSS, входящих в веб-Essentials, таких как всплывающая подсказка цвета и матрица браузера</span><span class="sxs-lookup"><span data-stu-id="b6cc9-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="b6cc9-121">Использование новых функций редактора JavaScript, входящих в веб-Essentials, например извлечение в файл и IntelliSense для всех элементов HTML</span><span class="sxs-lookup"><span data-stu-id="b6cc9-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="b6cc9-122">Обмен данными между браузером и Visual Studio с помощью связи с браузером</span><span class="sxs-lookup"><span data-stu-id="b6cc9-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b6cc9-123">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b6cc9-123">Prerequisites</span></span>

<span data-ttu-id="b6cc9-124">Для выполнения этой практической лабораторной работы требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="b6cc9-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="b6cc9-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) или выше</span><span class="sxs-lookup"><span data-stu-id="b6cc9-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="b6cc9-126">Web Essentials 2013</span><span class="sxs-lookup"><span data-stu-id="b6cc9-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="b6cc9-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="b6cc9-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b6cc9-128">Настройка</span><span class="sxs-lookup"><span data-stu-id="b6cc9-128">Setup</span></span>

<span data-ttu-id="b6cc9-129">Чтобы выполнить упражнения в этой практической лабораторной работе, сначала необходимо настроить среду.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="b6cc9-130">Откройте окно проводника Windows и перейдите к **исходной** папке лаборатории.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="b6cc9-131">Щелкните правой кнопкой мыши **Setup. cmd** и выберите **Запуск от имени администратора** , чтобы запустить процесс установки, который будет настраивать среду и установить фрагменты кода Visual Studio для этой лабораторной работы.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="b6cc9-132">Если отображается диалоговое окно Контроль учетных записей пользователей, подтвердите действие для продолжения.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="b6cc9-133">Убедитесь, что проверены все зависимости для этой лабораторной работы перед запуском программы установки.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="b6cc9-134">Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="b6cc9-134">Using the Code Snippets</span></span>

<span data-ttu-id="b6cc9-135">На протяжении всего лабораторного документа вы получите инструкции по вставке блоков кода.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="b6cc9-136">Для удобства большая часть этого кода предоставляется как Visual Studio Code фрагменты, к которым можно получить доступ из Visual Studio 2013, чтобы не добавлять их вручную.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="b6cc9-137">Каждое упражнение сопровождается начальным решением, расположенным в **начальной** папке упражнения, которое позволяет выполнять каждое упражнение независимо от других.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="b6cc9-138">Имейте в виду, что фрагменты кода, добавленные во время упражнения, отсутствуют в этих начальных решениях и могут не работать, пока вы не завершите упражнение.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="b6cc9-139">В исходном коде для упражнения также будет найдена **Конечная** папка, содержащая решение Visual Studio с кодом, полученным в результате выполнения шагов в соответствующем упражнении.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="b6cc9-140">Эти решения можно использовать в качестве руководства, если вам нужна дополнительная помощь во время работы с этой практической лабораторной работой.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b6cc9-141">Полнят</span><span class="sxs-lookup"><span data-stu-id="b6cc9-141">Exercises</span></span>

<span data-ttu-id="b6cc9-142">Эта практическая лабораторная работа включает в себя следующие упражнения:</span><span class="sxs-lookup"><span data-stu-id="b6cc9-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="b6cc9-143">Работа со связью с браузером и веб-Essentials</span><span class="sxs-lookup"><span data-stu-id="b6cc9-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="b6cc9-144">Использование фрагментов кода и IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b6cc9-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="b6cc9-145">При первом запуске Visual Studio необходимо выбрать одну из предварительно определенных коллекций параметров.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="b6cc9-146">Каждая предопределенная коллекция разработана для соответствия определенному стилю разработки и определяет макеты окон, поведение редактора, фрагменты кода IntelliSense и параметры диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="b6cc9-147">Процедуры в этом лабораторном занятии описывают действия, необходимые для выполнения данной задачи в Visual Studio при использовании коллекции **общих параметров разработки** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="b6cc9-148">При выборе другой коллекции параметров для среды разработки могут возникнуть различия в действиях, которые необходимо учитывать.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="b6cc9-149">Упражнение 1. Работа с ссылками на браузер и веб-Essentials</span><span class="sxs-lookup"><span data-stu-id="b6cc9-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="b6cc9-150">**Web Essentials** — это расширение Visual Studio, которое добавляет различные полезные функции для современной веб-разработки, в основном нацеленное на повышение скорости работы веб-разработки и более приятный.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="b6cc9-151">Вы можете установить веб-Essentials из коллекции расширений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="b6cc9-152">**Ссылка на браузер** — это новая функция, включенная в Visual Studio 2013, которая предоставляет канал между интегрированной средой разработки Visual Studio и любым открытым браузером для обмена данными между веб-приложением и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="b6cc9-153">Web Essentials расширяет связь браузера с инструментами для управления объектной моделью DOM и стилями CSS веб-страниц непосредственно из браузера.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="b6cc9-154">В этом упражнении вы узнаете о некоторых функциях, поддерживаемых **веб-компонентами** и **ссылками на браузер** , чтобы улучшить простую страницу головоломки.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="b6cc9-155">Задача 1. Запуск проекта в нескольких браузерах</span><span class="sxs-lookup"><span data-stu-id="b6cc9-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="b6cc9-156">В этой задаче вы настроите веб-приложение для запуска в нескольких браузерах одновременно, что полезно для тестирования в разных браузерах.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="b6cc9-157">Откройте **Microsoft Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="b6cc9-158">В меню **файл** выберите **Открыть | Проект или решение...** и перейдите к **EX1-WorkingwithBrowserLinkandWebEssentials\Begin** в **исходной** папке лаборатории (к:\вебкампстк\хол\всвебтулинг\саурце).</span><span class="sxs-lookup"><span data-stu-id="b6cc9-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="b6cc9-159">Выберите **Begin. sln** и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="b6cc9-160">На панели инструментов Visual Studio разверните меню браузера и выберите **Обзор с помощью...** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="b6cc9-161">![Просмотр с помощью пункта меню](visual-studio-2013-web-tools/_static/image1.png "Просмотреть с помощью... в меню браузера")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="b6cc9-162">*Просмотр с помощью пункта меню*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="b6cc9-163">В диалоговом окне **Просмотр с помощью** выберите **Google Chrome** и **Internet Explorer** , удерживая нажатой клавишу **CTRL** и выбрав **установить по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="b6cc9-164">![Диалоговое окно «Просмотр с помощью»](visual-studio-2013-web-tools/_static/image2.png "Диалоговое окно «Просмотр с помощью»")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="b6cc9-165">*Выбор нескольких браузеров по умолчанию*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="b6cc9-166">И Google Chrome, и Internet Explorer теперь должны отображаться в качестве браузеров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="b6cc9-167">Нажмите кнопку **Отмена**, чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="b6cc9-168">![Google Chrome и Internet Explorer в качестве браузеров по умолчанию](visual-studio-2013-web-tools/_static/image3.png "Браузеры Google Chrome и Internet Explorer по умолчанию")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="b6cc9-169">*Google Chrome и Internet Explorer в качестве браузеров по умолчанию*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6cc9-170">После настройки браузеров по умолчанию в меню браузера выбирается параметр **несколько браузеров** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="b6cc9-171">![Несколько браузеров](visual-studio-2013-web-tools/_static/image4.png "Несколько браузеров")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="b6cc9-172">Нажмите клавиши **CTRL** + **F5** , чтобы запустить приложение без отладки.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="b6cc9-173">При открытии обоих окон браузера поместите одно из них выше, чтобы они могли видеть обновления в обоих браузерах одновременно.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="b6cc9-174">Браузер должен отображать веб-страницу с светло-голубым прямоугольником.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="b6cc9-175">![Размещение одного браузера над другим](visual-studio-2013-web-tools/_static/image5.png "Размещение одного браузера над другим")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="b6cc9-176">*Размещение одного браузера над другим*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="b6cc9-177">Не закрывайте браузеры.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-177">Do not close the browsers.</span></span> <span data-ttu-id="b6cc9-178">Они будут использоваться в следующей задаче.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="b6cc9-179">Задача 2. Использование кода Zen для создания HTML-элементов</span><span class="sxs-lookup"><span data-stu-id="b6cc9-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="b6cc9-180">**Написание кода Zen** — это подключаемый модуль редактора для высокоскоростного кода HTML, XML, XSL (или любого другого формата структурированного кода) и редактирования.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="b6cc9-181">Ядро этого подключаемого модуля — это мощный механизм сокращения, позволяющий расширять выражения, аналогично селекторам CSS — в HTML-коде.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="b6cc9-182">Написание кода Zen — это быстрый способ написания кода HTML с помощью синтаксиса селектора стиля CSS.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="b6cc9-183">В этом упражнении вы будете использовать функцию кодирования Zen, предоставляемую Web Essentials, для создания HTML-кнопок, представляющих параметры вопроса.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="b6cc9-184">Вернитесь в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="b6cc9-185">Откройте файл **index. cshtml** , расположенный в папке **views** | **Home** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="b6cc9-186">Замените **&lt;!--TODO: Добавьте здесь параметры--&gt;** комментарий со следующим кодом и нажмите клавишу **Tab**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="b6cc9-187">Код должен быть расширен до HTML.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="b6cc9-188">![Развернутый HTML](visual-studio-2013-web-tools/_static/image6.png "Развернутый HTML")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="b6cc9-189">*Развернутый HTML*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6cc9-190">Дополнительные сведения о синтаксисе кодирования Zen см. в следующей [статье](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span><span class="sxs-lookup"><span data-stu-id="b6cc9-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="b6cc9-191">Нажмите кнопку **обновить связанные браузеры** , чтобы обновить оба браузера.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="b6cc9-192">![Обновить связанные браузеры](visual-studio-2013-web-tools/_static/image7.png "Обновить связанные браузеры")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="b6cc9-193">*Обновить связанные браузеры*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="b6cc9-194">![Internet Explorer — страница обновлена с четырьмя кнопками](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer — страница обновлена с четырьмя кнопками")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="b6cc9-195">*Internet Explorer — страница обновлена с четырьмя кнопками*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="b6cc9-196">![Google Chrome — страница обновлена четырьмя кнопками](visual-studio-2013-web-tools/_static/image9.png "Google Chrome — страница обновлена четырьмя кнопками")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="b6cc9-197">*Google Chrome — страница обновлена четырьмя кнопками*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="b6cc9-198">Вернитесь в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="b6cc9-199">Вы добавили кнопки на страницу, но по-прежнему нужно добавить шаблон вопроса.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="b6cc9-200">Для этого вы будете использовать новую функцию в Web Essentials под названием **Lorem Ipsum Generator**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="b6cc9-201">Нахождение элемента **div** с атрибутом **класса** **Front**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="b6cc9-202">Добавьте следующий код в качестве первого дочернего элемента **div**и нажмите клавишу **Tab**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="b6cc9-203">Код должен быть расширен до HTML.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="b6cc9-204">![Lorem Ipsum автоматически создан](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum автоматически создан")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="b6cc9-205">*Lorem Ipsum автоматически создан*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6cc9-206">В рамках Zen кодирования теперь можно создавать код Lorem Ipsum непосредственно в редакторе HTML.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="b6cc9-207">Просто введите **Lorem** и **Tab** , после чего будет вставлено 30-Lorem текст Ipsum.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="b6cc9-208">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6cc9-208">E.g.</span></span> <span data-ttu-id="b6cc9-209">*lorem10* вставляет 10 Lorem Ipsum слов.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="b6cc9-210">Вы добавите логотип в верхней части вопроса, используя другую новую функцию в Web Essentials, именуемую **генератором Lorem пикселей**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="b6cc9-211">Добавьте следующий код в качестве первого дочернего элемента элемента **div** с **контейнером** в качестве значения **класса** и нажмите клавишу **Tab**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="b6cc9-212">Код должен расширяться до HTML.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="b6cc9-213">![Автоматически сформированный пиксель Lorem](visual-studio-2013-web-tools/_static/image11.png "Автоматически сформированный пиксель Lorem")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="b6cc9-214">*Автоматически сформированный пиксель Lorem*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6cc9-215">В рамках Zen кодирования можно также создать код Lorem пикселей непосредственно в редакторе HTML.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="b6cc9-216">Просто введите **PIX-200x200-животные** и **Tab** и тег **img** с изображением 200x200а животного.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="b6cc9-217">Дополнительные сведения см. в разделе [Lorem Pixel](http://www.lorempixel.com).</span><span class="sxs-lookup"><span data-stu-id="b6cc9-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="b6cc9-218">Нажмите кнопку **обновить связанные браузеры** , чтобы обновить оба браузера.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="b6cc9-219">![Internet Explorer — автоматически созданное изображение и текст](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer — автоматически созданное изображение и текст")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="b6cc9-220">*Internet Explorer — автоматически созданное изображение и текст*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="b6cc9-221">![Google Chrome — автоматически созданное изображение и текст](visual-studio-2013-web-tools/_static/image13.png "Google Chrome — автоматически созданное изображение и текст")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="b6cc9-222">*Google Chrome — автоматически созданное изображение и текст*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6cc9-223">Поскольку изображение выбирается случайным образом при добавлении фрагмента кода, изображение, отображаемое в браузерах, может отличаться.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="b6cc9-224">Не закрывайте браузеры.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-224">Do not close the browsers.</span></span> <span data-ttu-id="b6cc9-225">Они будут использоваться в следующей задаче.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="b6cc9-226">Задача 3. обновление свойства стиля</span><span class="sxs-lookup"><span data-stu-id="b6cc9-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="b6cc9-227">В этой задаче будет использоваться функция **режима проверки** связи с браузером для определения точного расположения, в котором создается КОНКРЕТНЫЙ элемент DOM, и последующего обновления свойства Color этого элемента с помощью палитры цветов, предоставляемой веб-Essentials.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="b6cc9-228">В браузере Internet Explorer нажмите клавиши **CTRL** + **ALT** + **I** , чтобы включить режим проверки.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="b6cc9-229">Наведите указатель на светло-синюю границу и щелкните.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="b6cc9-230">![Перемещение указателя над светлой синей границей](visual-studio-2013-web-tools/_static/image14.png "Перемещение указателя над светлой синей границей")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="b6cc9-231">*Перемещение указателя над светлой синей границей*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="b6cc9-232">Вернитесь в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="b6cc9-233">Обратите внимание, как элемент HTML, выбранный в браузере, также выбирается в HTML-редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="b6cc9-234">![Элемент HTML, выбранный в редакторе HTML Visual Studio](visual-studio-2013-web-tools/_static/image15.png "Элемент HTML, выбранный в редакторе HTML Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="b6cc9-235">*Элемент HTML, выбранный в редакторе HTML Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="b6cc9-236">Теперь необходимо обновить **внешний** класс CSS, чтобы изменить стиль выбранного элемента.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="b6cc9-237">Для этого нажмите сочетание клавиш **CTRL** +  **,** чтобы открыть поле **Перейти к** поиску.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="b6cc9-238">Введите **site. CSS** и нажмите клавишу **Ввод** , чтобы открыть файл.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="b6cc9-239">![Открытие файла site. CSS](visual-studio-2013-web-tools/_static/image16.png "Открытие файла site. CSS")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="b6cc9-240">*Открытие файла site. CSS*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="b6cc9-241">Нажмите клавиши **CTRL** + **F** и введите **. переворот-Container. Front** , чтобы найти селектор CSS.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-241">Press **CTRL** + **F** and type **.flip-container .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="b6cc9-242">Щелкните светло-синий квадрат в свойстве Border класса, чтобы открыть палитру цветов.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="b6cc9-243">![Открытие палитры цветов](visual-studio-2013-web-tools/_static/image17.png "Открытие палитры цветов")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="b6cc9-244">*Открытие палитры цветов*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="b6cc9-245">Разверните палитру цветов, нажав кнопку с многоточием, и выберите новый цвет.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="b6cc9-246">![Развертывание палитры цветов](visual-studio-2013-web-tools/_static/image18.png "Развертывание палитры цветов")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="b6cc9-247">*Развертывание палитры цветов*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="b6cc9-248">Нажмите клавиши **CTRL** + **ALT** + **Enter** , чтобы обновить связанные браузеры.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="b6cc9-249">Переключитесь в Internet Explorer и обратите внимание на изменение цвета границы.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="b6cc9-250">![Internet Explorer-цвет границы изменен](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-цвет границы изменен")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="b6cc9-251">*Internet Explorer-цвет границы изменен*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="b6cc9-252">Переключитесь в Google Chrome и обратите внимание на изменение цвета границы.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="b6cc9-253">![Google Chrome — изменен цвет границы](visual-studio-2013-web-tools/_static/image20.png "Google Chrome — изменен цвет границы")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="b6cc9-254">*Google Chrome — изменен цвет границы*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="b6cc9-255">Вернитесь в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="b6cc9-256">Перейдите в конец файла **site. CSS** и нажмите клавиши **CTRL** + **F** , чтобы найти селектор **. БТН** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="b6cc9-257">Обратите внимание, что свойство **-WebKit-Border-радиус** подчеркнуто зеленым цветом.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="b6cc9-258">![Свойство-WebKit-Border-радиус селектора БТН](visual-studio-2013-web-tools/_static/image21.png "Свойство-WebKit-Border-радиус селектора БТН")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="b6cc9-259">*Свойство-WebKit-Border-радиус селектора БТН*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="b6cc9-260">Поместите курсор в свойство **-WebKit-Border-радиус** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="b6cc9-261">Под первой буквой первого слова свойства должна появиться синяя линия.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="b6cc9-262">Это **смарт-тег**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="b6cc9-263">Нажмите клавиши **CTRL** +  **.**</span><span class="sxs-lookup"><span data-stu-id="b6cc9-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="b6cc9-264">чтобы открыть меню вариантов и выбрать пункт **Добавить отсутствующее стандартное свойство (Border-RADIUS)** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="b6cc9-265">![Добавить отсутствующее предложение стандартного свойства](visual-studio-2013-web-tools/_static/image22.png "Добавить отсутствующее предложение стандартного свойства")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="b6cc9-266">*Добавить отсутствующее предложение стандартного свойства*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="b6cc9-267">Свойство **border-radius** автоматически добавляется в правило CSS.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="b6cc9-268">![Добавление стандартного свойства отсутствует](visual-studio-2013-web-tools/_static/image23.png "Добавление стандартного свойства отсутствует")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="b6cc9-269">*Добавление стандартного свойства отсутствует*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="b6cc9-270">Наведите указатель мыши на свойство **border-радиус** , чтобы отобразить **всплывающую подсказку матрицы браузера**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="b6cc9-271">**Всплывающая подсказка матрица браузера** показывает доступность свойства в каждом браузере.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="b6cc9-272">![Всплывающая подсказка матрицы браузера](visual-studio-2013-web-tools/_static/image24.png "Всплывающая подсказка матрицы браузера")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="b6cc9-273">*Всплывающая подсказка матрицы браузера*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="b6cc9-274">Обратите внимание, что значение свойства **border-radius** по-прежнему подчеркнуто.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="b6cc9-275">Наведите указатель мыши на значение, чтобы увидеть предупреждающее сообщение.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="b6cc9-276">![Граница — предупреждение значения свойства RADIUS](visual-studio-2013-web-tools/_static/image25.png "Граница — предупреждение значения свойства RADIUS")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="b6cc9-277">*Граница — предупреждение значения свойства RADIUS*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="b6cc9-278">Удалите единицу измерения **border — значение свойства радиуса** , как это было предложено подсказкой.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="b6cc9-279">Поскольку **border-radius** является стандартным свойством для определения того, как скругленные углы границы, можно удалить свойство **-WebKit-Border-радиус** и значение из правила CSS.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="b6cc9-280">Поместите курсор в свойство **переноса слов** и обратите внимание, что смарт-тег также отображается ниже.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="b6cc9-281">Откройте меню и выберите пункт **добавить недостающие особенности поставщика**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="b6cc9-282">![Добавить предложение "недостающие особенности поставщика"](visual-studio-2013-web-tools/_static/image26.png "Добавить предложение "недостающие особенности поставщика"")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="b6cc9-283">*Добавить предложение "недостающие особенности поставщика"*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="b6cc9-284">Свойство **-MS-Word-Wrap** автоматически добавляется в правило CSS.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="b6cc9-285">![Добавлено свойство, относящееся к поставщику](visual-studio-2013-web-tools/_static/image27.png "Добавлено свойство, относящееся к поставщику")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="b6cc9-286">*Добавлено свойство, относящееся к поставщику*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="b6cc9-287">Задача 4. Обновление кода HTML из браузера</span><span class="sxs-lookup"><span data-stu-id="b6cc9-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="b6cc9-288">В этой задаче для редактирования объекта DOM в браузере и передачи изменений в исходный файл HTML в Visual Studio будет использоваться функция **режима конструктора** связи с браузером.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="b6cc9-289">В Google Chrome нажмите клавиши **CTRL** + **ALT** + **D** , чтобы включить режим конструктора.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="b6cc9-290">Наведите указатель мыши на метку **Lorem Ipsum Dolor Sit Amet** и нажмите кнопку.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="b6cc9-291">![Изменение вопроса](visual-studio-2013-web-tools/_static/image28.png "Изменение вопроса")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="b6cc9-292">*Изменение вопроса*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-292">*Editing the question*</span></span>
3. <span data-ttu-id="b6cc9-293">Должен появиться курсор.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-293">A cursor should appear.</span></span> <span data-ttu-id="b6cc9-294">Замените исходный текст на то, *как он выглядит при написании более длинного вопроса?* , а затем нажмите клавишу **ESC** , чтобы выйти из режима конструктора.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="b6cc9-295">![Вопрос изменен](visual-studio-2013-web-tools/_static/image29.png "Вопрос изменен")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="b6cc9-296">*Вопрос изменен*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-296">*Question edited*</span></span>
4. <span data-ttu-id="b6cc9-297">Вернитесь в Visual Studio и откройте **индекс. cshtml**, если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="b6cc9-298">Обратите внимание, что внутренний текст элемента **&lt;p&gt;** был обновлен.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="b6cc9-299">![Обновленный вопрос на странице HTML](visual-studio-2013-web-tools/_static/image30.png "Обновленный вопрос на странице HTML")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="b6cc9-300">*Обновленный вопрос на странице HTML*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="b6cc9-301">Задача 5. Просмотр предупреждений, связанных с SEO</span><span class="sxs-lookup"><span data-stu-id="b6cc9-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="b6cc9-302">**Оптимизация поисковой системы** (SEO) — это процесс повышения ранга веб-сайта в списке результатов поисковой системы.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="b6cc9-303">Чем выше ранги сайта, тем более согласованно они перечислены, тем больше посетителей веб-узла получит эта поисковая система.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="b6cc9-304">Web Essentials включает в себя аналитический инструмент, который проверяет HTML, сообщает о найденных проблемах и предоставляет помощь по их устранению.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="b6cc9-305">Перейдите в меню **вид** и выберите пункт **Список ошибок** , чтобы открыть окно **Список ошибок** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="b6cc9-306">![Список ошибок в меню "вид"](visual-studio-2013-web-tools/_static/image31.png "Список ошибок в меню "вид"")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="b6cc9-307">*Список ошибок в меню "вид"*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="b6cc9-308">Обратите внимание, что существует предупреждение SEO, уведомляющее о том, что отсутствует тег **&lt;meta&gt;** для описания страницы.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="b6cc9-309">Дважды щелкните запись предупреждения SEO, чтобы исправить ее.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="b6cc9-310">![Окно "Список ошибок"](visual-studio-2013-web-tools/_static/image32.png "Окно "Список ошибок"")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="b6cc9-311">*Окно "Список ошибок"*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-311">*Error List window*</span></span>
3. <span data-ttu-id="b6cc9-312">В диалоговом окне " **веб-компоненты** " нажмите кнопку **Да** , чтобы вставить описание &lt;тега meta&gt;.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="b6cc9-313">![Диалоговое окно "веб-компоненты"](visual-studio-2013-web-tools/_static/image33.png "Диалоговое окно "веб-компоненты"")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="b6cc9-314">*Диалоговое окно "веб-компоненты"*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="b6cc9-315">Откроется редактор для **\_Layout. cshtml** , и тег **&lt;meta&gt;** автоматически добавляется в раздел **head** файла HTML.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="b6cc9-316">![Тег META автоматически добавлен в _Layout страницу](visual-studio-2013-web-tools/_static/image34.png "Тег META автоматически добавлен в _Layout страницу")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="b6cc9-317">*Тег META автоматически добавлен на страницу макета \_*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="b6cc9-318">Измените значение атрибута **Content** на *жееккуиз* и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="b6cc9-319">Упражнение 2. Использование фрагментов кода и IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b6cc9-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="b6cc9-320">С помощью веб-Essentials редактор HTML дополнен дополнительными функциональными возможностями.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="b6cc9-321">В этом упражнении вы увидите некоторые новые функции, которые полезны при разработке веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="b6cc9-322">Задача 1. Использование IntelliSense в HTML-документах</span><span class="sxs-lookup"><span data-stu-id="b6cc9-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="b6cc9-323">Первая новая функция, которая будет отображаться в этой задаче, называется **динамической технологией IntelliSense**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="b6cc9-324">Динамическая IntelliSense считывает другие теги и атрибуты, чтобы определить возможные идентификаторы, которые будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="b6cc9-325">В этой задаче будет создан новый элемент формы HTML, содержащий метку и поле ввода.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="b6cc9-326">Затем вы добавите атрибут **for** к метке, чтобы привязать его к входным данным, и вы увидите предложения IntelliSense на основе идентификаторов входных данных в области.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="b6cc9-327">Откройте **Visual Studio Express 2013 для Web** и решение **Begin. sln** , расположенное в папке **Source/EX2-такингадвантажеофкодесниппетсандинтеллисенсе/Begin** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="b6cc9-328">Кроме того, можно продолжить работу с решением, полученным в предыдущем упражнении.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="b6cc9-329">В **Обозреватель решений**откройте файл **index. cshtml** , расположенный в папке **views** | **Home** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="b6cc9-330">Добавьте следующую форму в элемент **&lt;раздела&gt;** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="b6cc9-331">(Фрагмент кода — *VisualStudio2013WebTooling* - *EX2* - *Form*)</span><span class="sxs-lookup"><span data-stu-id="b6cc9-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="b6cc9-332">Тегу input должен предшествовать элемент Label с описанием поля.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="b6cc9-333">Добавьте следующую метку перед тегом входных данных.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="b6cc9-334">Атрибут **&lt;метки&gt;** **указывает, к** какому элементу формы привязана метка.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="b6cc9-335">Значение атрибута должно быть равно идентификатору связанного элемента.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="b6cc9-336">Добавьте атрибут **for** в элемент **&lt;Label&gt;** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="b6cc9-337">Как показано на следующем рисунке, в поле IntelliSense появляется значение &quot;имя&quot;, основанное на идентификаторах элементов в одной области (включающая **&lt;форма&gt;** ).</span><span class="sxs-lookup"><span data-stu-id="b6cc9-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="b6cc9-338">![Отображение идентификатора в IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Отображение идентификатора в IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="b6cc9-339">*Отображение идентификатора в IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="b6cc9-340">Удаление недавно добавленного **&lt;формы&gt;** элемента и его содержимого.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="b6cc9-341">Задача 2. Использование фрагментов кода HTML</span><span class="sxs-lookup"><span data-stu-id="b6cc9-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="b6cc9-342">В HTML5 появился более 25 новых семантических тегов.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="b6cc9-343">Visual Studio уже поддерживала поддержку IntelliSense для этих тегов, но Visual Studio 2013 ускоряет и упрощает написание разметки путем добавления новых фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="b6cc9-344">Хотя эти теги не сложны, они поставляются с небольшим числом тонкостей, такими как добавление правильных резервных фрагментов кодека для *звукового* тега.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="b6cc9-345">В этой задаче вы увидите фрагменты кода HTML для тега audio.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="b6cc9-346">В файле **index. cshtml** введите **&lt;AUD** внутри **&lt;раздела&gt;** , как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="b6cc9-347">![Вставка элемента audio](visual-studio-2013-web-tools/_static/image36.png "Вставка элемента audio")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="b6cc9-348">*Вставка элемента audio*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="b6cc9-349">Дважды нажмите клавишу **Tab** и обратите внимание на то, как на странице добавляется следующий код, и курсор помещается на атрибут **src** первого источника.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="b6cc9-350">Нажимая клавишу **Tab** дважды, фрагмент кода вставляется.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="b6cc9-351">В звуковом фрагменте показано стандартное использование тега *Audio* с двумя исходными файлами для улучшения поддержки.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="b6cc9-352">Удалите вторую строку и обновите источник первой строки следующей ссылкой на Вебкампств Katana: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span><span class="sxs-lookup"><span data-stu-id="b6cc9-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="b6cc9-353">Полученный код показан ниже.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="b6cc9-354">В качестве примера используется исходный файл *катанапрожект. mp3* .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="b6cc9-355">При желании можно использовать другой источник.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="b6cc9-356">Нажмите клавиши **CTRL** + **S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="b6cc9-357">Нажмите клавиши **CTRL** + **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="b6cc9-358">Обратите внимание, что в приложение добавлен звуковой проигрыватель.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="b6cc9-359">![Аудио Player в Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Аудио Player в Internet Explorer")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="b6cc9-360">*Аудио Player в Internet Explorer*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="b6cc9-361">![Аудио проигрыватель в Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Аудио проигрыватель в Google Chrome")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="b6cc9-362">*Аудио проигрыватель в Google Chrome*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="b6cc9-363">Не закрывайте браузеры.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-363">Do not close the browsers.</span></span> <span data-ttu-id="b6cc9-364">Они будут использоваться в следующей задаче.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="b6cc9-365">Задача 3. Использование IntelliSense в документах JavaScript</span><span class="sxs-lookup"><span data-stu-id="b6cc9-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="b6cc9-366">С помощью Web Essentials 2013 таблицы стилей и HTML-страницы создают список идентификаторов и имен классов.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="b6cc9-367">В этой задаче вы узнаете, как эти списки улучшают поддержку JavaScript IntelliSense в Web Essentials 2013.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="b6cc9-368">В файле **index. cshtml** добавьте следующий код, чтобы определить тег **скрипта** для кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="b6cc9-369">Добавьте следующий код внутри тега **скрипта** , чтобы определить функцию обратного вызова Ready.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="b6cc9-370">(Фрагмент кода — *VisualStudio2013WebTooling* - *EX2* - *реадифунктион*)</span><span class="sxs-lookup"><span data-stu-id="b6cc9-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="b6cc9-371">Поместите курсор в тег **script** и нажмите клавиши **CTRL** +  **.**</span><span class="sxs-lookup"><span data-stu-id="b6cc9-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="b6cc9-372">, чтобы открыть меню предложений.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="b6cc9-373">Щелкните **извлечь в файл**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="b6cc9-374">![Предложение "извлечь в файл" JavaScript](visual-studio-2013-web-tools/_static/image39.png "Предложение "извлечь в файл" JavaScript")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="b6cc9-375">*Предложение "извлечь в файл" JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="b6cc9-376">В окне **Сохранить как** выберите папку **скрипты** , назовите файл **init. js** и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="b6cc9-377">![Сохранить как окно](visual-studio-2013-web-tools/_static/image40.png "Сохранить как окно")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="b6cc9-378">*Сохранить как окно*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6cc9-379">Создается файл **init. js** , и содержимое скрипта перемещается в файл.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="b6cc9-380">![Файл init. js, созданный с помощью входящего содержимого](visual-studio-2013-web-tools/_static/image41.png "Файл init. js, созданный с помощью входящего содержимого")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="b6cc9-381">*Файл init. js, созданный с помощью входящего содержимого*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="b6cc9-382">Откройте файл **index. cshtml** и убедитесь, что тег скрипта был заменен ссылкой на файл **init. js** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="b6cc9-383">![Справочник HTML по init. js](visual-studio-2013-web-tools/_static/image42.png "Справочник HTML по init. js")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="b6cc9-384">*Справочник HTML по init. js*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="b6cc9-385">Перейдите к **Обозреватель решений** и обратите внимание, что файл **init. js** был автоматически добавлен в решение.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="b6cc9-386">![Файл init. js, входящий в решение](visual-studio-2013-web-tools/_static/image43.png "Файл init. js, входящий в решение")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="b6cc9-387">*Файл init. js, входящий в решение*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="b6cc9-388">Вернитесь в файл **init. js** , чтобы обновить функцию обратного вызова функции **Ready** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="b6cc9-389">Внутри определения обратного вызова функции, которое передается в *состояние Ready*, добавьте следующий код, чтобы получить все элементы по определенному атрибуту класса.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="b6cc9-390">Нажмите клавиши **CTRL** + **пробел** между кавычками в вызове функции **жетелементсбикласснаме** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="b6cc9-391">![Отображение IntelliSense для функции Жетелементсбикласснаме](visual-studio-2013-web-tools/_static/image44.png "Отображение IntelliSense для функции Жетелементсбикласснаме")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="b6cc9-392">*Отображение IntelliSense для функции Жетелементсбикласснаме*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6cc9-393">Обратите внимание, что IntelliSense показывает классы, определенные в таблицах стилей проекта.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="b6cc9-394">Замените созданную строку следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="b6cc9-395">Установите курсор после **Au** внутри кавычек функции **getElementsByTagName** и нажмите клавиши **CTRL** + **Space**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="b6cc9-396">![Отображение IntelliSense для метода Жетелементбитагнаме](visual-studio-2013-web-tools/_static/image45.png "Отображение IntelliSense для метода Жетелементбитагнаме")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="b6cc9-397">*Отображение IntelliSense для метода getElementsByTagName*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="b6cc9-398">Выберите **&quot;audio&quot;** из списка и нажмите клавишу **Ввод**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="b6cc9-399">Результат показан на примере ниже.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="b6cc9-400">![Получение звуковых элементов](visual-studio-2013-web-tools/_static/image46.png "Получение звуковых элементов")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="b6cc9-401">*Получение звуковых элементов*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="b6cc9-402">В **Обозреватель решений**щелкните правой кнопкой мыши файл **init. js** в папке **Scripts** и выберите в меню **веб-компоненты** пункт **уменьшение (файлы JavaScript)** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="b6cc9-403">![Файлы JavaScript уменьшение](visual-studio-2013-web-tools/_static/image47.png "Файлы JavaScript уменьшение")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="b6cc9-404">*Файлы JavaScript уменьшение*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="b6cc9-405">При появлении запроса на включение автоматического минификации при изменении исходного файла нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="b6cc9-406">![Включение автоматического предупреждения минификации](visual-studio-2013-web-tools/_static/image48.png "Включение автоматического предупреждения минификации")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="b6cc9-407">*Включение автоматического предупреждения минификации*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6cc9-408">Создается файл **init. min. js** , который добавляется как зависимость от файла **init. js** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="b6cc9-409">![Файл init. min. js создан](visual-studio-2013-web-tools/_static/image49.png "Файл init. min. js создан")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="b6cc9-410">*Файл init. min. js создан*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="b6cc9-411">Откройте файл **init. min. js** и обратите внимание, что это файл минифицированные.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="b6cc9-412">![Содержимое файла init. min. js](visual-studio-2013-web-tools/_static/image50.png "Содержимое файла init. min. js")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="b6cc9-413">*Содержимое файла init. min. js*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="b6cc9-414">В файле **init. js** добавьте следующий код под вызовом функции **getElementsByTagName** для воспроизведения всех звуковых элементов.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="b6cc9-415">(Фрагмент кода — *VisualStudio2013WebTooling* - *EX2* - *плайаудиоелементс*)</span><span class="sxs-lookup"><span data-stu-id="b6cc9-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="b6cc9-416">Нажмите **клавиши CTRL** + **S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="b6cc9-417">Так как файл минифицированные уже открыт, вы увидите диалоговое окно с сообщением о том, что файл был изменен вне редактора исходного кода.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="b6cc9-418">Щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-418">Click **Yes**.</span></span>

    <span data-ttu-id="b6cc9-419">![Предупреждение Microsoft Visual Studio](visual-studio-2013-web-tools/_static/image51.png "Предупреждение Microsoft Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="b6cc9-420">*Предупреждение Microsoft Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="b6cc9-421">Вернитесь к файлу **init. min. js** , чтобы убедиться, что файл был обновлен с помощью нового кода.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="b6cc9-422">![Файл init. min. js обновлен](visual-studio-2013-web-tools/_static/image52.png "Файл init. min. js обновлен")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="b6cc9-423">*Файл init. min. js обновлен*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="b6cc9-424">Нажмите кнопку **Обновить связь с браузером** .</span><span class="sxs-lookup"><span data-stu-id="b6cc9-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="b6cc9-425">После обновления обоих браузеров звуковые проигрыватели, которые вы видели в предыдущей задаче, начинают играть автоматически.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="b6cc9-426">![Аудио проигрыватель, добавленный в представление](visual-studio-2013-web-tools/_static/image53.png "Аудио проигрыватель, добавленный в представление")</span><span class="sxs-lookup"><span data-stu-id="b6cc9-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="b6cc9-427">*Аудио проигрыватель, добавленный в представление*</span><span class="sxs-lookup"><span data-stu-id="b6cc9-427">*Audio player included in view*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b6cc9-428">Сводка</span><span class="sxs-lookup"><span data-stu-id="b6cc9-428">Summary</span></span>

<span data-ttu-id="b6cc9-429">С помощью этой практической лабораторной работы вы узнали, как:</span><span class="sxs-lookup"><span data-stu-id="b6cc9-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="b6cc9-430">Используйте новые функции редактора HTML, содержащиеся в веб-Essentials, такие как Расширенные фрагменты кода HTML5 и Zen код.</span><span class="sxs-lookup"><span data-stu-id="b6cc9-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="b6cc9-431">Использование новых функций редактора CSS, входящих в веб-Essentials, таких как всплывающая подсказка цвета и матрица браузера</span><span class="sxs-lookup"><span data-stu-id="b6cc9-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="b6cc9-432">Использование новых функций редактора JavaScript, входящих в веб-Essentials, например извлечение в файл и IntelliSense для всех элементов HTML</span><span class="sxs-lookup"><span data-stu-id="b6cc9-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="b6cc9-433">Обмен данными между браузером и Visual Studio с помощью связи с браузером</span><span class="sxs-lookup"><span data-stu-id="b6cc9-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>
