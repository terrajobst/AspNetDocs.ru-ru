---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: Модели и доступ к данным ASP.NET MVC 4 | Документация Майкрософт
author: rick-anderson
description: Примечание. в этом практическом занятии предполагается, что у вас есть базовые знания о ASP.NET MVC. Если вы ранее не использовали ASP.NET MVC, рекомендуется перейти на ASP.NET MVC 4...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451470"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="ed424-104">Модели и доступ к данным в ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="ed424-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="ed424-105">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="ed424-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="ed424-106">Скачать обучающий комплект Web Camp</span><span class="sxs-lookup"><span data-stu-id="ed424-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="ed424-107">В этой практической лабораторной работе предполагается, что у вас есть базовые знания о **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="ed424-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="ed424-108">Если вы ранее не использовали **ASP.NET MVC** , мы рекомендуем вам перейти на практический семинар **ASP.NET MVC 4** .</span><span class="sxs-lookup"><span data-stu-id="ed424-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="ed424-109">Эта лабораторная работа посвящена усовершенствованиям и новым функциям, описанным выше, путем применения незначительных изменений в образце веб-приложения, предоставленном в исходной папке.</span><span class="sxs-lookup"><span data-stu-id="ed424-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="ed424-110">Все примеры кода и фрагментов включены в набор средств для обучения Web Camp, доступный в [выпусках Microsoft-Web/вебкамптраинингкит](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="ed424-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="ed424-111">Проект, относящийся к этой лабораторной работе, доступен по [моделям ASP.NET MVC 4 и доступу к данным](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span><span class="sxs-lookup"><span data-stu-id="ed424-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="ed424-112">В практической лабораторной работе по **ASP.NET MVC** вы передавали жестко закодированные данные из контроллеров в шаблоны представления.</span><span class="sxs-lookup"><span data-stu-id="ed424-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="ed424-113">Однако для создания реального веб-приложения может потребоваться использовать реальную базу данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="ed424-114">В этом практическом занятии будет показано, как использовать ядро СУБД для хранения и извлечения данных, необходимых для приложения музыкального магазина.</span><span class="sxs-lookup"><span data-stu-id="ed424-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="ed424-115">Для этого вы начнете с существующей базы данных и создадите EDM из нее.</span><span class="sxs-lookup"><span data-stu-id="ed424-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="ed424-116">В рамках этого лабораторного занятия вы будете соответствовать **Database First** подходу, а также **Code First** подходу.</span><span class="sxs-lookup"><span data-stu-id="ed424-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="ed424-117">Однако можно также использовать подход **Model First** , создать ту же модель с помощью инструментов, а затем создать из нее базу данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="ed424-118">![Database First и Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First и Model First")</span><span class="sxs-lookup"><span data-stu-id="ed424-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="ed424-119">*Database First и Model First*</span><span class="sxs-lookup"><span data-stu-id="ed424-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="ed424-120">После создания модели необходимо внести соответствующие изменения в Стореконтроллер, чтобы предоставить представления магазинов с данными, полученными из базы данных, а не с помощью жестко закодированных данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="ed424-121">Вносить изменения в шаблоны представления не требуется, так как Стореконтроллер будет возвращать те же ViewModel-данные в шаблоны представлений, хотя на этот раз данные поступают из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="ed424-122">**Code First подход**</span><span class="sxs-lookup"><span data-stu-id="ed424-122">**The Code First Approach**</span></span>

<span data-ttu-id="ed424-123">Code First подход позволяет нам определить модель из кода без создания классов, которые обычно связаны с платформой.</span><span class="sxs-lookup"><span data-stu-id="ed424-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="ed424-124">В коде сначала объекты модели определяются с помощью POCO, &quot;простые старые объекты CLR&quot;.</span><span class="sxs-lookup"><span data-stu-id="ed424-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="ed424-125">POCO — это простые обычные классы, которые не имеют наследования и не реализуют интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="ed424-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="ed424-126">Мы можем автоматически создать базу данных из них, или можно использовать существующую базу данных и создать сопоставление класса из кода.</span><span class="sxs-lookup"><span data-stu-id="ed424-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="ed424-127">Преимущества использования этого подхода в том, что модель остается независимой от платформы сохраняемости (в данном случае Entity Framework), так как классы POCO не связаны с платформой сопоставления.</span><span class="sxs-lookup"><span data-stu-id="ed424-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="ed424-128">Эта лабораторная работа основана на ASP.NET MVC 4 и версии примера приложения музыкального магазина, которая настроена и уменьшена в соответствии с функциями, представленными в этой практической лабораторной работе.</span><span class="sxs-lookup"><span data-stu-id="ed424-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="ed424-129">Если вы хотите изучить все приложение учебника по всему **музыкальному магазину** , его можно найти в [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="ed424-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="ed424-130">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ed424-130">Prerequisites</span></span>

<span data-ttu-id="ed424-131">Для выполнения этой лабораторной работы необходимо иметь следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="ed424-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="ed424-132">[Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или старше (см. [приложение а](#AppendixA) для получения инструкций по его установке).</span><span class="sxs-lookup"><span data-stu-id="ed424-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="ed424-133">Настройка</span><span class="sxs-lookup"><span data-stu-id="ed424-133">Setup</span></span>

<span data-ttu-id="ed424-134">**Установка фрагментов кода**</span><span class="sxs-lookup"><span data-stu-id="ed424-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="ed424-135">Для удобства большая часть кода, который вы будете управлять в этой лаборатории, доступна в виде фрагментов кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed424-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="ed424-136">Чтобы установить фрагменты кода, запустите файл **.\саурце\сетуп\кодесниппетс.ВСИ** .</span><span class="sxs-lookup"><span data-stu-id="ed424-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="ed424-137">Если вы не знакомы с фрагментами кода Visual Studio Code и хотите узнать, как их использовать, см. приложение в этом документе &quot;[приложении C: использование фрагментов кода](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="ed424-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="ed424-138">Полнят</span><span class="sxs-lookup"><span data-stu-id="ed424-138">Exercises</span></span>

<span data-ttu-id="ed424-139">Эта практическая лабораторная работа состоит из следующих упражнений:</span><span class="sxs-lookup"><span data-stu-id="ed424-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="ed424-140">Упражнение 1. Добавление базы данных</span><span class="sxs-lookup"><span data-stu-id="ed424-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="ed424-141">Упражнение 2. Создание базы данных с помощью Code First</span><span class="sxs-lookup"><span data-stu-id="ed424-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="ed424-142">Упражнение 3. запрос параметров к базе данных</span><span class="sxs-lookup"><span data-stu-id="ed424-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="ed424-143">Каждое упражнение сопровождается **конечной** папкой, содержащей итоговое решение, которое следует получить после завершения упражнений.</span><span class="sxs-lookup"><span data-stu-id="ed424-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="ed424-144">Это решение можно использовать в качестве инструкции, если вам нужна дополнительная помощь по работе с упражнениями.</span><span class="sxs-lookup"><span data-stu-id="ed424-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="ed424-145">Предполагаемое время выполнения этой лабораторной работы: **35 минут**.</span><span class="sxs-lookup"><span data-stu-id="ed424-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="ed424-146">Упражнение 1. Добавление базы данных</span><span class="sxs-lookup"><span data-stu-id="ed424-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="ed424-147">В этом упражнении вы узнаете, как добавить базу данных с таблицами приложения Мусиксторе в решение для использования его данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="ed424-148">После создания базы данных с моделью и добавления ее в решение будет изменен класс Стореконтроллер, чтобы предоставить шаблон представления с данными, полученными из базы данных, вместо использования жестко заданных значений.</span><span class="sxs-lookup"><span data-stu-id="ed424-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="ed424-149">Задача 1. Добавление базы данных</span><span class="sxs-lookup"><span data-stu-id="ed424-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="ed424-150">В этой задаче вы добавите уже созданную базу данных с основными таблицами приложения Мусиксторе в решение.</span><span class="sxs-lookup"><span data-stu-id="ed424-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="ed424-151">Откройте **Начальное** решение, расположенное по адресу **Source/EX1-аддингадатабаседбфирст/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="ed424-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="ed424-152">Перед продолжением необходимо загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="ed424-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="ed424-153">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ed424-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="ed424-154">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="ed424-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="ed424-155">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="ed424-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="ed424-156">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="ed424-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="ed424-157">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="ed424-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="ed424-158">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ed424-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="ed424-159">Добавьте файл базы данных **мвкмусиксторе** .</span><span class="sxs-lookup"><span data-stu-id="ed424-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="ed424-160">В этой практической лабораторной работе вы будете использовать уже созданную базу данных с именем **мвкмусиксторе. mdf**.</span><span class="sxs-lookup"><span data-stu-id="ed424-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="ed424-161">Для этого щелкните правой кнопкой мыши папку " **приложение\_данные** ", наведите указатель на пункт **Добавить** и выберите пункт **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="ed424-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="ed424-162">Перейдите к **\саурце\ассетс** и выберите файл **мвкмусиксторе. mdf** .</span><span class="sxs-lookup"><span data-stu-id="ed424-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="ed424-163">![Добавление существующего элемента](aspnet-mvc-4-models-and-data-access/_static/image2.png "Добавление существующего элемента")</span><span class="sxs-lookup"><span data-stu-id="ed424-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="ed424-164">*Добавление существующего элемента*</span><span class="sxs-lookup"><span data-stu-id="ed424-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="ed424-165">![Файл базы данных Мвкмусиксторе. mdf](aspnet-mvc-4-models-and-data-access/_static/image3.png "Файл базы данных Мвкмусиксторе. mdf")</span><span class="sxs-lookup"><span data-stu-id="ed424-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="ed424-166">*Файл базы данных Мвкмусиксторе. mdf*</span><span class="sxs-lookup"><span data-stu-id="ed424-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="ed424-167">База данных добавлена в проект.</span><span class="sxs-lookup"><span data-stu-id="ed424-167">The database has been added to the project.</span></span> <span data-ttu-id="ed424-168">Даже если база данных находится внутри решения, можно запрашивать и обновлять ее, как если бы она была размещена на другом сервере базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="ed424-169">![База данных Мвкмусиксторе в обозреватель решений](aspnet-mvc-4-models-and-data-access/_static/image4.png "База данных Мвкмусиксторе в обозреватель решений")</span><span class="sxs-lookup"><span data-stu-id="ed424-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="ed424-170">*База данных Мвкмусиксторе в обозреватель решений*</span><span class="sxs-lookup"><span data-stu-id="ed424-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="ed424-171">Проверьте соединение с базой данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-171">Verify the connection to the database.</span></span> <span data-ttu-id="ed424-172">Для этого дважды щелкните **мвкмусиксторе. mdf** , чтобы установить соединение.</span><span class="sxs-lookup"><span data-stu-id="ed424-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="ed424-173">![Подключение к Мвкмусиксторе. mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Подключение к Мвкмусиксторе. mdf")</span><span class="sxs-lookup"><span data-stu-id="ed424-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="ed424-174">*Подключение к Мвкмусиксторе. mdf*</span><span class="sxs-lookup"><span data-stu-id="ed424-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="ed424-175">Задача 2. Создание модели данных</span><span class="sxs-lookup"><span data-stu-id="ed424-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="ed424-176">В этой задаче будет создана модель данных для взаимодействия с базой данных, добавленной в предыдущей задаче.</span><span class="sxs-lookup"><span data-stu-id="ed424-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="ed424-177">Создайте модель данных, которая будет представлять базу данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="ed424-178">Для этого в обозреватель решений щелкните правой кнопкой мыши папку **модели** , наведите указатель на пункт **Добавить** и выберите пункт **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="ed424-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="ed424-179">В диалоговом окне **Добавление нового элемента** выберите шаблон **данных** , а затем элемент **EDM ADO.NET** .</span><span class="sxs-lookup"><span data-stu-id="ed424-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="ed424-180">Измените имя модели данных на **сторедб. EDMX** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ed424-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="ed424-181">![Добавление EDM ADO.NET Сторедб](aspnet-mvc-4-models-and-data-access/_static/image6.png "Добавление EDM ADO.NET Сторедб")</span><span class="sxs-lookup"><span data-stu-id="ed424-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="ed424-182">*Добавление EDM ADO.NET Сторедб*</span><span class="sxs-lookup"><span data-stu-id="ed424-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="ed424-183">Откроется **мастер EDM** .</span><span class="sxs-lookup"><span data-stu-id="ed424-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="ed424-184">Этот мастер поможет вам создать слой модели.</span><span class="sxs-lookup"><span data-stu-id="ed424-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="ed424-185">Поскольку модель должна быть создана на основе недавно добавленной существующей базы данных, выберите **создать из базы данных** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ed424-185">Since the model should be created based on the existing database recently added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="ed424-186">![Выбор содержимого модели](aspnet-mvc-4-models-and-data-access/_static/image7.png "Выбор содержимого модели")</span><span class="sxs-lookup"><span data-stu-id="ed424-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="ed424-187">*Выбор содержимого модели*</span><span class="sxs-lookup"><span data-stu-id="ed424-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="ed424-188">Поскольку модель создается на основе базы данных, необходимо указать соединение, которое будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="ed424-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="ed424-189">Нажмите кнопку **создать соединение**.</span><span class="sxs-lookup"><span data-stu-id="ed424-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="ed424-190">Выберите **Microsoft SQL Server файл базы данных** и нажмите кнопку **продолжить**.</span><span class="sxs-lookup"><span data-stu-id="ed424-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="ed424-191">![Выбор источника данных](aspnet-mvc-4-models-and-data-access/_static/image8.png "Выбор источника данных")</span><span class="sxs-lookup"><span data-stu-id="ed424-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="ed424-192">*Диалоговое окно выбора источника данных*</span><span class="sxs-lookup"><span data-stu-id="ed424-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="ed424-193">Нажмите кнопку **Обзор** и выберите базу данных **мвкмусиксторе. mdf** , расположенную в папке **приложения\_данных** , и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ed424-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="ed424-194">![Свойства соединения](aspnet-mvc-4-models-and-data-access/_static/image9.png "Свойства подключения")</span><span class="sxs-lookup"><span data-stu-id="ed424-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="ed424-195">*Свойства соединения*</span><span class="sxs-lookup"><span data-stu-id="ed424-195">*Connection properties*</span></span>
6. <span data-ttu-id="ed424-196">Созданный класс должен иметь то же имя, что и строка подключения сущности, поэтому измените его имя на **мусиксторинтитиес** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ed424-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="ed424-197">![Выбор подключения к данным](aspnet-mvc-4-models-and-data-access/_static/image10.png "Выбор подключения к данным")</span><span class="sxs-lookup"><span data-stu-id="ed424-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="ed424-198">*Выбор подключения к данным*</span><span class="sxs-lookup"><span data-stu-id="ed424-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="ed424-199">Выберите объекты базы данных для использования.</span><span class="sxs-lookup"><span data-stu-id="ed424-199">Choose the database objects to use.</span></span> <span data-ttu-id="ed424-200">Так как модель сущностей будет использовать только таблицы базы данных, выберите параметр **таблицы** и убедитесь, что выбраны также параметры **включить столбцы внешнего ключа в параметр Model** и **создания множественного или единственного числа созданные имена объектов** .</span><span class="sxs-lookup"><span data-stu-id="ed424-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="ed424-201">Измените пространство имен модели на **мвкмусиксторе. Model** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ed424-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="ed424-202">![Выбор объектов базы данных](aspnet-mvc-4-models-and-data-access/_static/image11.png "Выбор объектов базы данных")</span><span class="sxs-lookup"><span data-stu-id="ed424-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="ed424-203">*Выбор объектов базы данных*</span><span class="sxs-lookup"><span data-stu-id="ed424-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed424-204">Если отображается диалоговое окно предупреждения системы безопасности, нажмите кнопку **ОК** , чтобы запустить шаблон и создать классы для сущностей модели.</span><span class="sxs-lookup"><span data-stu-id="ed424-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="ed424-205">Появится схема сущностей для базы данных, в то время как будет создан отдельный класс, который сопоставляет каждую таблицу с базой данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="ed424-206">Например, таблица « **альбомы** » будет представлена классом **альбома** , где каждый столбец в таблице будет сопоставлен со свойством класса.</span><span class="sxs-lookup"><span data-stu-id="ed424-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="ed424-207">Это позволит вам запрашивать и работать с объектами, представляющими строки в базе данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="ed424-208">![Схема сущности](aspnet-mvc-4-models-and-data-access/_static/image12.png "Схема сущностей")</span><span class="sxs-lookup"><span data-stu-id="ed424-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="ed424-209">*Схема сущности*</span><span class="sxs-lookup"><span data-stu-id="ed424-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed424-210">Шаблон T4 (. TT) запускает код для создания классов сущностей и перезаписывает существующие классы с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="ed424-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="ed424-211">В этом примере классы &quot;&quot;альбома, &quot;жанр&quot; и &quot;исполнителя были перезаписаны созданным кодом.&quot;</span><span class="sxs-lookup"><span data-stu-id="ed424-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="ed424-212">Задача 3. Создание приложения</span><span class="sxs-lookup"><span data-stu-id="ed424-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="ed424-213">В этой задаче будет проверяться, что, несмотря на то, что создание модели удалило классы « **альбом**», « **Жанр** » и « **исполнитель** », проект успешно строится с использованием новых классов модели данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="ed424-214">Выполните сборку проекта, выбрав пункт меню **Сборка** , а затем — **сборку мвкмусиксторе**.</span><span class="sxs-lookup"><span data-stu-id="ed424-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="ed424-215">![Сборка проекта](aspnet-mvc-4-models-and-data-access/_static/image13.png "Сборка проекта")</span><span class="sxs-lookup"><span data-stu-id="ed424-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="ed424-216">*Сборка проекта*</span><span class="sxs-lookup"><span data-stu-id="ed424-216">*Building the project*</span></span>
2. <span data-ttu-id="ed424-217">Проект успешно строится.</span><span class="sxs-lookup"><span data-stu-id="ed424-217">The project builds successfully.</span></span> <span data-ttu-id="ed424-218">Почему он по-прежнему работает?</span><span class="sxs-lookup"><span data-stu-id="ed424-218">Why does it still work?</span></span> <span data-ttu-id="ed424-219">Это работает потому, что таблицы базы данных имеют поля, включающие свойства, которые использовались в **альбоме** удаленных классов и **жанре**.</span><span class="sxs-lookup"><span data-stu-id="ed424-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="ed424-220">![Сборки были выполнены](aspnet-mvc-4-models-and-data-access/_static/image14.png "Сборки были выполнены")</span><span class="sxs-lookup"><span data-stu-id="ed424-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="ed424-221">*Сборки были выполнены*</span><span class="sxs-lookup"><span data-stu-id="ed424-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="ed424-222">Хотя конструктор отображает сущности в формате схемы, они фактически C# являются классами.</span><span class="sxs-lookup"><span data-stu-id="ed424-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="ed424-223">Разверните узел **сторедб. EDMX** в Обозреватель решений а затем **StoreDB.TT**, вы увидите новые созданные сущности.</span><span class="sxs-lookup"><span data-stu-id="ed424-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="ed424-224">![Созданные файлы](aspnet-mvc-4-models-and-data-access/_static/image15.png "Созданные файлы")</span><span class="sxs-lookup"><span data-stu-id="ed424-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="ed424-225">*Созданные файлы*</span><span class="sxs-lookup"><span data-stu-id="ed424-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="ed424-226">Задача 4. запрос к базе данных</span><span class="sxs-lookup"><span data-stu-id="ed424-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="ed424-227">В этой задаче будет обновлен класс Стореконтроллер, так что вместо использования жестко зафиксированных данных будет получен запрос к базе данных для получения информации.</span><span class="sxs-lookup"><span data-stu-id="ed424-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="ed424-228">Откройте **контроллерс\стореконтроллер.КС** и добавьте в класс следующее поле для хранения экземпляра класса **Мусиксторинтитиес** с именем **сторедб**:</span><span class="sxs-lookup"><span data-stu-id="ed424-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="ed424-229">(Фрагмент кода — *модели и доступ к данным — EX1 сторедб*)</span><span class="sxs-lookup"><span data-stu-id="ed424-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="ed424-230">Класс **мусиксторинтитиес** предоставляет свойство коллекции для каждой таблицы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="ed424-231">Обновите метод действия **обзора** , чтобы получить жанр со всеми **альбомами**.</span><span class="sxs-lookup"><span data-stu-id="ed424-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="ed424-232">(Фрагмент кода — *модели и доступ к данным — обзор хранилища EX1*)</span><span class="sxs-lookup"><span data-stu-id="ed424-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="ed424-233">Для создания строго типизированных выражений запросов в этих коллекциях используется функция .NET, называемая языком **LINQ** , которая будет выполнять код для базы данных и возвращать объекты, с которыми можно программировать.</span><span class="sxs-lookup"><span data-stu-id="ed424-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="ed424-234">Дополнительные сведения о LINQ см. на [веб-сайте MSDN](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed424-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="ed424-235">Обновите метод действия **индекса** , чтобы получить все жанры.</span><span class="sxs-lookup"><span data-stu-id="ed424-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="ed424-236">(Фрагмент кода — *модели и доступ к данным — индекс хранилища EX1*)</span><span class="sxs-lookup"><span data-stu-id="ed424-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="ed424-237">Обновление метода действия **индекса** для получения всех жанров и преобразования коллекции в список.</span><span class="sxs-lookup"><span data-stu-id="ed424-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="ed424-238">(Фрагмент кода — *модели и доступ к данным — хранилище EX1 Store женремену*)</span><span class="sxs-lookup"><span data-stu-id="ed424-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="ed424-239">Задача 5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ed424-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="ed424-240">В этой задаче будет проверено, что страница "индекс магазина" теперь будет отображать жанры, хранящиеся в базе данных, а не жестко закодированные.</span><span class="sxs-lookup"><span data-stu-id="ed424-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="ed424-241">Нет необходимости изменять шаблон представления, так как **стореконтроллер** возвращает те же сущности, что и раньше, хотя на этот раз данные будут поступать из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="ed424-242">Перестройте решение и нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="ed424-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="ed424-243">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="ed424-243">The project starts in the Home page.</span></span> <span data-ttu-id="ed424-244">Убедитесь, что меню **жанров** больше не является жестко закодированным списком, и данные извлекаются из базы данных напрямую.</span><span class="sxs-lookup"><span data-stu-id="ed424-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![бровсингженресфромдатабасе](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="ed424-246">*Просмотр жанров из базы данных*</span><span class="sxs-lookup"><span data-stu-id="ed424-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="ed424-247">Теперь перейдите к любому жанру и убедитесь, что альбомы заполнены из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="ed424-248">![Просмотр альбомов из базы данных](aspnet-mvc-4-models-and-data-access/_static/image17.png "Просмотр альбомов из базы данных")</span><span class="sxs-lookup"><span data-stu-id="ed424-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="ed424-249">*Просмотр альбомов из базы данных*</span><span class="sxs-lookup"><span data-stu-id="ed424-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="ed424-250">Упражнение 2. Создание базы данных с помощью Code First</span><span class="sxs-lookup"><span data-stu-id="ed424-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="ed424-251">В этом упражнении вы узнаете, как использовать Code First подход для создания базы данных с таблицами приложения Мусиксторе и получения доступа к его данным.</span><span class="sxs-lookup"><span data-stu-id="ed424-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="ed424-252">После создания модели вы измените Стореконтроллер, чтобы предоставить шаблон представления с данными, полученными из базы данных, вместо использования жестко заданных значений.</span><span class="sxs-lookup"><span data-stu-id="ed424-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="ed424-253">Если вы выполнили упражнение 1 и уже работали с Database Firstным подходом, вы узнаете, как получить те же результаты с помощью другого процесса.</span><span class="sxs-lookup"><span data-stu-id="ed424-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="ed424-254">Для упрощения чтения были отмечены задачи, общие с помощью упражнения 1.</span><span class="sxs-lookup"><span data-stu-id="ed424-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="ed424-255">Если вы еще не выполнили упражнение 1, но хотели бы изучить Code Firstный подход, вы можете начать с этого упражнения и получить полный охват статьи.</span><span class="sxs-lookup"><span data-stu-id="ed424-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="ed424-256">Задача 1. Заполнение демонстрационных данных</span><span class="sxs-lookup"><span data-stu-id="ed424-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="ed424-257">В этой задаче вы заполните базу данных образцами данных при первоначальном создании с помощью кода — First.</span><span class="sxs-lookup"><span data-stu-id="ed424-257">In this task, you will populate the database with sample data when it is initially created using Code-First.</span></span>

1. <span data-ttu-id="ed424-258">Откройте **Начальное** решение, расположенное по адресу **Source/EX2-креатингадатабасекодефирст/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="ed424-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="ed424-259">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="ed424-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="ed424-260">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="ed424-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="ed424-261">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ed424-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="ed424-262">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="ed424-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="ed424-263">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="ed424-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="ed424-264">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="ed424-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="ed424-265">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="ed424-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="ed424-266">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ed424-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="ed424-267">Добавьте файл **SampleData.CS** в папку **Models** .</span><span class="sxs-lookup"><span data-stu-id="ed424-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="ed424-268">Для этого щелкните правой кнопкой мыши папку **модели** , наведите указатель на пункт **Добавить** и выберите пункт **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="ed424-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="ed424-269">Перейдите к **\саурце\ассетс** и выберите файл **SampleData.CS** .</span><span class="sxs-lookup"><span data-stu-id="ed424-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="ed424-270">![Пример заполнения данных в коде](aspnet-mvc-4-models-and-data-access/_static/image18.png "Пример заполнения данных в коде")</span><span class="sxs-lookup"><span data-stu-id="ed424-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="ed424-271">*Пример заполнения данных в коде*</span><span class="sxs-lookup"><span data-stu-id="ed424-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="ed424-272">Откройте файл **Global.asax.CS** и добавьте следующие операторы *using* .</span><span class="sxs-lookup"><span data-stu-id="ed424-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="ed424-273">(Фрагмент кода — *модели и доступ к данным — глобальный Ex2ный asax using*)</span><span class="sxs-lookup"><span data-stu-id="ed424-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="ed424-274">В методе **запуска\_приложения ()** добавьте следующую строку, чтобы задать инициализатор базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="ed424-275">(Фрагмент кода — *модели и доступ к данным — EX2 Global asax сетинитиализер*)</span><span class="sxs-lookup"><span data-stu-id="ed424-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="ed424-276">Задача 2. Настройка подключения к базе данных</span><span class="sxs-lookup"><span data-stu-id="ed424-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="ed424-277">Теперь, когда база данных уже добавлена в наш проект, в файле **Web. config** будет записана строка подключения.</span><span class="sxs-lookup"><span data-stu-id="ed424-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="ed424-278">Добавьте строку подключения в **файл Web. config**. Для этого откройте **файл Web. config** в корневом каталоге проекта и замените строку подключения с именем DefaultConnection следующей строкой в **&lt;ConnectionString&gt;** разделе:</span><span class="sxs-lookup"><span data-stu-id="ed424-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="ed424-279">![Расположение файла Web. config](aspnet-mvc-4-models-and-data-access/_static/image19.png "Расположение файла Web. config")</span><span class="sxs-lookup"><span data-stu-id="ed424-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="ed424-280">*Расположение файла Web. config*</span><span class="sxs-lookup"><span data-stu-id="ed424-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="ed424-281">Задача 3. Работа с моделью</span><span class="sxs-lookup"><span data-stu-id="ed424-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="ed424-282">Теперь, когда соединение с базой данных уже настроено, вы свяжете модель с таблицами базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="ed424-283">В этой задаче будет создан класс, который будет связан с базой данных с Code First.</span><span class="sxs-lookup"><span data-stu-id="ed424-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="ed424-284">Помните, что существует существующий класс модели POCO, который необходимо изменить.</span><span class="sxs-lookup"><span data-stu-id="ed424-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="ed424-285">Если вы выполнили упражнение 1, то обратите внимание, что этот шаг был выполнен мастером.</span><span class="sxs-lookup"><span data-stu-id="ed424-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="ed424-286">Выполняя Code First, вы вручную создадите классы, которые будут связаны с сущностями данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="ed424-287">Откройте класс модели POCO « **Жанр** » из папки проекта **модели** и добавьте идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ed424-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="ed424-288">Используйте свойство int с именем **GenreId**.</span><span class="sxs-lookup"><span data-stu-id="ed424-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="ed424-289">(Фрагмент кода — *модели и доступ к данным — Ex2 Code First жанр*)</span><span class="sxs-lookup"><span data-stu-id="ed424-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="ed424-290">Для работы с соглашениями Code First, жанр класса должен иметь свойство первичного ключа, которое будет автоматически обнаруживаться.</span><span class="sxs-lookup"><span data-stu-id="ed424-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="ed424-291">Дополнительные сведения о соглашениях Code First см. в этой [статье MSDN](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed424-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="ed424-292">Теперь откройте **альбом** класс модели POCO из папки проекта **модели** и включите внешние ключи, а затем создайте свойства с именами **GenreId** и **артистид**.</span><span class="sxs-lookup"><span data-stu-id="ed424-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="ed424-293">Этот класс уже имеет **GenreId** для первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="ed424-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="ed424-294">(Фрагмент кода — *модели и доступ к данным — Ex2 Code First альбом*)</span><span class="sxs-lookup"><span data-stu-id="ed424-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="ed424-295">Откройте **класс модели** POCO и включите свойство **артистид** .</span><span class="sxs-lookup"><span data-stu-id="ed424-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="ed424-296">(Фрагмент кода — *модели и доступ к данным — Ex2 Code First исполнителя*)</span><span class="sxs-lookup"><span data-stu-id="ed424-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="ed424-297">Щелкните правой кнопкой мыши папку проекта **модели** и выберите команду **Добавить | Класс**.</span><span class="sxs-lookup"><span data-stu-id="ed424-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="ed424-298">Назовите файл **MusicStoreEntities.CS**.</span><span class="sxs-lookup"><span data-stu-id="ed424-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="ed424-299">Затем нажмите кнопку **Добавить.**</span><span class="sxs-lookup"><span data-stu-id="ed424-299">Then, click **Add.**</span></span>

    <span data-ttu-id="ed424-300">![Добавление класса](aspnet-mvc-4-models-and-data-access/_static/image20.png "Добавление класса")</span><span class="sxs-lookup"><span data-stu-id="ed424-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="ed424-301">*Добавление нового элемента*</span><span class="sxs-lookup"><span data-stu-id="ed424-301">*Adding a new item*</span></span>

    <span data-ttu-id="ed424-302">![Добавление Class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Добавление Class2")</span><span class="sxs-lookup"><span data-stu-id="ed424-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="ed424-303">*Добавление класса*</span><span class="sxs-lookup"><span data-stu-id="ed424-303">*Adding a class*</span></span>
5. <span data-ttu-id="ed424-304">Откройте только что созданный класс **MusicStoreEntities.CS**и включите пространства имен **System. Data. Entity** и **System. Data. Entity. Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="ed424-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="ed424-305">Замените объявление класса для расширения класса **DbContext** : Объявите открытый **DBSet** и переопределите метод **OnModelCreating** .</span><span class="sxs-lookup"><span data-stu-id="ed424-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="ed424-306">После выполнения этого шага вы получите доменный класс, который свяжет модель с Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="ed424-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="ed424-307">Для этого замените код класса следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ed424-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="ed424-308">(Фрагмент кода — *модели и доступ к данным — Ex2 Code First мусиксторинтитиес*)</span><span class="sxs-lookup"><span data-stu-id="ed424-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="ed424-309">С помощью Entity Framework **DbContext** и **DBSet** вы сможете запросить жанр класса POCO.</span><span class="sxs-lookup"><span data-stu-id="ed424-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="ed424-310">Расширяя метод **OnModelCreating** , вы указываете в **коде** , как жанр будет сопоставляться с таблицей базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="ed424-311">Дополнительные сведения о DBContext и DBSet можно найти в этой статье MSDN: [Link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="ed424-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="ed424-312">Задача 4. запрос к базе данных</span><span class="sxs-lookup"><span data-stu-id="ed424-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="ed424-313">В этой задаче будет обновлен класс Стореконтроллер, чтобы вместо использования жестко зафиксированных данных он извлек его из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="ed424-314">Эта задача часто используется в упражнении 1.</span><span class="sxs-lookup"><span data-stu-id="ed424-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="ed424-315">Если вы выполнили упражнение 1, то эти действия будут одинаковы в обоих подходах (сначала база данных или код).</span><span class="sxs-lookup"><span data-stu-id="ed424-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="ed424-316">Они отличаются друг от друга тем, как данные связаны с моделью, но доступ к сущностям данных пока не является прозрачным для контроллера.</span><span class="sxs-lookup"><span data-stu-id="ed424-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>

1. <span data-ttu-id="ed424-317">Откройте **контроллерс\стореконтроллер.КС** и добавьте в класс следующее поле для хранения экземпляра класса **Мусиксторинтитиес** с именем **сторедб**:</span><span class="sxs-lookup"><span data-stu-id="ed424-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="ed424-318">(Фрагмент кода — *модели и доступ к данным — EX1 сторедб*)</span><span class="sxs-lookup"><span data-stu-id="ed424-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="ed424-319">Класс **мусиксторинтитиес** предоставляет свойство коллекции для каждой таблицы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="ed424-320">Обновите метод действия **обзора** , чтобы получить жанр со всеми **альбомами**.</span><span class="sxs-lookup"><span data-stu-id="ed424-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="ed424-321">(Фрагмент кода — *модели и доступ к данным — обзор хранилища EX2*)</span><span class="sxs-lookup"><span data-stu-id="ed424-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="ed424-322">Для создания строго типизированных выражений запросов в этих коллекциях используется функция .NET, называемая языком **LINQ** , которая будет выполнять код для базы данных и возвращать объекты, с которыми можно программировать.</span><span class="sxs-lookup"><span data-stu-id="ed424-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="ed424-323">Дополнительные сведения о LINQ см. на [веб-сайте MSDN](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="ed424-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="ed424-324">Обновите метод действия **индекса** , чтобы получить все жанры.</span><span class="sxs-lookup"><span data-stu-id="ed424-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="ed424-325">(Фрагмент кода — *модели и доступ к данным — индекс хранилища EX2*)</span><span class="sxs-lookup"><span data-stu-id="ed424-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="ed424-326">Обновление метода действия **индекса** для получения всех жанров и преобразования коллекции в список.</span><span class="sxs-lookup"><span data-stu-id="ed424-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="ed424-327">(Фрагмент кода — *модели и доступ к данным — хранилище EX2 Store женремену*)</span><span class="sxs-lookup"><span data-stu-id="ed424-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="ed424-328">Задача 5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ed424-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="ed424-329">В этой задаче будет проверено, что страница "индекс магазина" теперь будет отображать жанры, хранящиеся в базе данных, а не жестко закодированные.</span><span class="sxs-lookup"><span data-stu-id="ed424-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="ed424-330">Нет необходимости изменять шаблон представления, так как **стореконтроллер** возвращает тот же **стореиндексвиевмодел** , что и раньше, но на этот раз данные поступают из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="ed424-331">Перестройте решение и нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="ed424-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="ed424-332">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="ed424-332">The project starts in the Home page.</span></span> <span data-ttu-id="ed424-333">Убедитесь, что меню **жанров** больше не является жестко закодированным списком, и данные извлекаются из базы данных напрямую.</span><span class="sxs-lookup"><span data-stu-id="ed424-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![бровсингженресфромдатабасе](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="ed424-335">*Просмотр жанров из базы данных*</span><span class="sxs-lookup"><span data-stu-id="ed424-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="ed424-336">Теперь перейдите к любому жанру и убедитесь, что альбомы заполнены из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="ed424-337">![Просмотр альбомов из базы данных](aspnet-mvc-4-models-and-data-access/_static/image23.png "Просмотр альбомов из базы данных")</span><span class="sxs-lookup"><span data-stu-id="ed424-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="ed424-338">*Просмотр альбомов из базы данных*</span><span class="sxs-lookup"><span data-stu-id="ed424-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="ed424-339">Упражнение 3. запрос параметров к базе данных</span><span class="sxs-lookup"><span data-stu-id="ed424-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="ed424-340">В этом упражнении вы узнаете, как выполнять запросы к базе данных с помощью параметров, а также как использовать функцию формирования результатов запросов, которая сокращает число обращений к базе данных, получая данные более эффективным образом.</span><span class="sxs-lookup"><span data-stu-id="ed424-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="ed424-341">Дополнительные сведения о формировании результатов запроса см. в следующей [статье MSDN](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed424-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="ed424-342">Задача 1. изменение Стореконтроллер для получения альбомов из базы данных</span><span class="sxs-lookup"><span data-stu-id="ed424-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="ed424-343">В этой задаче будет изменен класс **стореконтроллер** , чтобы получить доступ к базе данных для получения альбомов от определенного жанра.</span><span class="sxs-lookup"><span data-stu-id="ed424-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="ed424-344">Откройте решение **Begin** , расположенное в папке **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** , если вы хотите использовать подход с кодом, или папку **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** , если хотите использовать подход с первой базой данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="ed424-345">В противном случае вы можете продолжать **использовать решение, полученное в результате** выполнения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="ed424-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="ed424-346">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="ed424-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="ed424-347">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ed424-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="ed424-348">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="ed424-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="ed424-349">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="ed424-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="ed424-350">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="ed424-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="ed424-351">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="ed424-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="ed424-352">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ed424-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="ed424-353">Откройте класс **стореконтроллер** , чтобы изменить метод действия **обзора** .</span><span class="sxs-lookup"><span data-stu-id="ed424-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="ed424-354">Для этого в **Обозреватель решений**разверните папку **Controllers** и дважды щелкните **StoreController.CS**.</span><span class="sxs-lookup"><span data-stu-id="ed424-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="ed424-355">Измените метод действия **обзора** , чтобы получить Альбомы для определенного жанра.</span><span class="sxs-lookup"><span data-stu-id="ed424-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="ed424-356">Для этого замените следующий код:</span><span class="sxs-lookup"><span data-stu-id="ed424-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="ed424-357">(Фрагмент кода — *модели и доступ к данным — EX3 Стореконтроллер бровсемесод*)</span><span class="sxs-lookup"><span data-stu-id="ed424-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="ed424-358">Чтобы заполнить коллекцию сущности, необходимо использовать метод **include** , чтобы указать, что нужно извлечь альбомы.</span><span class="sxs-lookup"><span data-stu-id="ed424-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="ed424-359">Можно использовать. **Одно расширение ()** в LINQ, поскольку в данном случае для альбома требуется только один жанр.</span><span class="sxs-lookup"><span data-stu-id="ed424-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="ed424-360">Метод **Single ()** принимает лямбда-выражение в качестве параметра, который в данном случае указывает один объект жанра, который соответствует определенному значению.</span><span class="sxs-lookup"><span data-stu-id="ed424-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="ed424-361">Вы будете использовать функцию, которая позволяет указать другие связанные сущности, которые нужно загрузить, а также при извлечении объекта жанра.</span><span class="sxs-lookup"><span data-stu-id="ed424-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="ed424-362">Эта функция называется **формированием результатов запроса**и позволяет сократить число попыток доступа к базе данных для получения информации.</span><span class="sxs-lookup"><span data-stu-id="ed424-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="ed424-363">В этом случае вам потребуется предварительно получить Альбомы для полученного жанра.</span><span class="sxs-lookup"><span data-stu-id="ed424-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="ed424-364">Запрос содержит **жанры. include (&quot;альбомы&quot;)** , чтобы указать, что вы хотите использовать связанные альбомы.</span><span class="sxs-lookup"><span data-stu-id="ed424-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="ed424-365">Это приведет к более эффективному приложению, так как будет извлекать данные о жанрах и альбомах в одном запросе к базе данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="ed424-366">Задача 2. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ed424-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="ed424-367">В этой задаче вы запустите приложение и получите альбомы определенного жанра из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="ed424-368">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="ed424-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="ed424-369">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="ed424-369">The project starts in the Home page.</span></span> <span data-ttu-id="ed424-370">Измените URL-адрес на **/Сторе/бровсе? жанр = POP** , чтобы убедиться, что результаты извлекаются из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="ed424-371">![Просмотр по жанру](aspnet-mvc-4-models-and-data-access/_static/image24.png "Просмотр по жанру")</span><span class="sxs-lookup"><span data-stu-id="ed424-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="ed424-372">*Просмотр/Сторе/бровсе? жанр = POP*</span><span class="sxs-lookup"><span data-stu-id="ed424-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="ed424-373">Задача 3. доступ к альбомам по идентификатору</span><span class="sxs-lookup"><span data-stu-id="ed424-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="ed424-374">В этой задаче будет повторена предыдущая процедура для получения альбомов по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="ed424-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="ed424-375">При необходимости закройте браузер, чтобы вернуться в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed424-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="ed424-376">Откройте класс **стореконтроллер** , чтобы изменить метод действия **Details** .</span><span class="sxs-lookup"><span data-stu-id="ed424-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="ed424-377">Для этого в **Обозреватель решений**разверните папку **Controllers** и дважды щелкните **StoreController.CS**.</span><span class="sxs-lookup"><span data-stu-id="ed424-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="ed424-378">Измените метод действия **Details** , чтобы получить сведения о альбомах на основе их **идентификатора**. Для этого замените следующий код:</span><span class="sxs-lookup"><span data-stu-id="ed424-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="ed424-379">(Фрагмент кода — *модели и доступ к данным — EX3 Стореконтроллер детаилсмесод*)</span><span class="sxs-lookup"><span data-stu-id="ed424-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="ed424-380">Задача 4. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ed424-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="ed424-381">В этой задаче вы запустите приложение в веб-браузере и получите сведения об альбоме по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="ed424-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="ed424-382">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="ed424-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="ed424-383">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="ed424-383">The project starts in the Home page.</span></span> <span data-ttu-id="ed424-384">Измените URL-адрес на **/Store/Details/51** или просмотрите жанры и выберите альбом, чтобы убедиться, что результаты получены из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="ed424-385">![Сведения о просмотре](aspnet-mvc-4-models-and-data-access/_static/image25.png "Сведения о просмотре")</span><span class="sxs-lookup"><span data-stu-id="ed424-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="ed424-386">*Просмотр/Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="ed424-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="ed424-387">Кроме того, это приложение можно развернуть на веб-сайтах Windows Azure в [приложении б: Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="ed424-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="ed424-388">Сводка</span><span class="sxs-lookup"><span data-stu-id="ed424-388">Summary</span></span>

<span data-ttu-id="ed424-389">Выполняя эту практическую лабораторию, вы узнали об основах моделей и доступа к данным ASP.NET MVC, используя подход **Database First** , а также **Code First** подход:</span><span class="sxs-lookup"><span data-stu-id="ed424-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="ed424-390">Добавление базы данных в решение для использования ее данных</span><span class="sxs-lookup"><span data-stu-id="ed424-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="ed424-391">Обновление контроллеров для предоставления шаблонов представлений с данными, полученными из базы данных, а не жестко запрограммированной</span><span class="sxs-lookup"><span data-stu-id="ed424-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="ed424-392">Запрос к базе данных с помощью параметров</span><span class="sxs-lookup"><span data-stu-id="ed424-392">How to query the database using parameters</span></span>
- <span data-ttu-id="ed424-393">Использование формирования результатов запроса — функции, которая сокращает количество обращений к базе данных, получение данных более эффективным способом</span><span class="sxs-lookup"><span data-stu-id="ed424-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="ed424-394">Как использовать Database First и Code First подходов в Microsoft Entity Framework для связи базы данных с моделью</span><span class="sxs-lookup"><span data-stu-id="ed424-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="ed424-395">Приложение а. Установка Visual Studio Express 2012 для Web</span><span class="sxs-lookup"><span data-stu-id="ed424-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="ed424-396">Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версии с помощью **[установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="ed424-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="ed424-397">Следующие инструкции помогут вам выполнить действия, необходимые для установки *Visual Studio Express 2012 для Web* с помощью *установщик веб-платформы Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="ed424-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="ed424-398">Перейдите в [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="ed424-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="ed424-399">Кроме того, если у вас уже установлен установщик веб-платформы, вы можете открыть его и найти продукт &quot;<em>Visual Studio Express 2012 для Web с Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="ed424-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="ed424-400">Щелкните **Install Now (установить сейчас**).</span><span class="sxs-lookup"><span data-stu-id="ed424-400">Click on **Install Now**.</span></span> <span data-ttu-id="ed424-401">Если у вас нет **установщика веб-платформы** , вы будете сначала перенаправлены на загрузку и установку.</span><span class="sxs-lookup"><span data-stu-id="ed424-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="ed424-402">После открытия **установщика веб-платформы** нажмите кнопку **установить** , чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="ed424-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="ed424-403">![Установка Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Установка Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="ed424-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="ed424-404">*Установка Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="ed424-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="ed424-405">Прочитайте все лицензии и условия продуктов и нажмите кнопку " **принять** ", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="ed424-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Принятие условий лицензии](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="ed424-407">*Принятие условий лицензии*</span><span class="sxs-lookup"><span data-stu-id="ed424-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="ed424-408">Дождитесь завершения процесса загрузки и установки.</span><span class="sxs-lookup"><span data-stu-id="ed424-408">Wait until the downloading and installation process completes.</span></span>

    ![Ход установки](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="ed424-410">*Ход установки*</span><span class="sxs-lookup"><span data-stu-id="ed424-410">*Installation progress*</span></span>
6. <span data-ttu-id="ed424-411">После завершения установки нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ed424-411">When the installation completes, click **Finish**.</span></span>

    ![Установка завершена](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="ed424-413">*Установка завершена*</span><span class="sxs-lookup"><span data-stu-id="ed424-413">*Installation completed*</span></span>
7. <span data-ttu-id="ed424-414">Нажмите кнопку **выход** , чтобы закрыть установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="ed424-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="ed424-415">Чтобы открыть Visual Studio Express для Интернета, перейдите на **начальный** экран и начните запись &quot;**VS Express**&quot;, а затем щелкните плитку **VS Express для Web** .</span><span class="sxs-lookup"><span data-stu-id="ed424-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Плитка VS Express для Web](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="ed424-417">*Плитка VS Express для Web*</span><span class="sxs-lookup"><span data-stu-id="ed424-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="ed424-418">Приложение б. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание</span><span class="sxs-lookup"><span data-stu-id="ed424-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="ed424-419">В этом приложении показано, как создать новый веб-сайт из портал управления Windows Azure и опубликовать полученное приложение, выполнив следующие лабораторные занятия, используя возможности публикации веб-развертывание, предоставляемые Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="ed424-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="ed424-420">Задача 1. Создание нового веб-сайта на портале Windows Azure</span><span class="sxs-lookup"><span data-stu-id="ed424-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="ed424-421">Перейдите в [портал управления Windows Azure](https://manage.windowsazure.com/) и выполните вход с использованием учетных данных Майкрософт, связанных с подпиской.</span><span class="sxs-lookup"><span data-stu-id="ed424-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed424-422">С помощью Windows Azure можно бесплатно разместить 10 веб-сайтов ASP.NET, а затем масштабировать их по мере роста объема трафика.</span><span class="sxs-lookup"><span data-stu-id="ed424-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="ed424-423">Вы можете зарегистрироваться [здесь](https://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="ed424-423">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="ed424-424">![Вход в Windows портал Azure](aspnet-mvc-4-models-and-data-access/_static/image31.png "Вход в Windows портал Azure")</span><span class="sxs-lookup"><span data-stu-id="ed424-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="ed424-425">*Вход в Windows Azure портал управления*</span><span class="sxs-lookup"><span data-stu-id="ed424-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="ed424-426">На панели команд щелкните **создать** .</span><span class="sxs-lookup"><span data-stu-id="ed424-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="ed424-427">![Создание нового веб-сайта](aspnet-mvc-4-models-and-data-access/_static/image32.png "Создание нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="ed424-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="ed424-428">*Создание нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="ed424-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="ed424-429">Щелкните **Compute** | **веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="ed424-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="ed424-430">Затем выберите пункт **Быстрое создание** .</span><span class="sxs-lookup"><span data-stu-id="ed424-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="ed424-431">Предоставьте доступный URL-адрес для нового веб-сайта и щелкните **создать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="ed424-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed424-432">Веб-сайт Windows Azure — это узел для веб-приложения, работающего в облаке, которыми можно управлять и которыми вы управляете.</span><span class="sxs-lookup"><span data-stu-id="ed424-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="ed424-433">Параметр Быстрое создание позволяет развернуть завершенное веб-приложение на веб-сайте Windows Azure извне портала.</span><span class="sxs-lookup"><span data-stu-id="ed424-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="ed424-434">Он не включает шаги по настройке базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="ed424-435">![Создание нового веб-сайта с помощью быстрого создания](aspnet-mvc-4-models-and-data-access/_static/image33.png "Создание нового веб-сайта с помощью быстрого создания")</span><span class="sxs-lookup"><span data-stu-id="ed424-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="ed424-436">*Создание нового веб-сайта с помощью быстрого создания*</span><span class="sxs-lookup"><span data-stu-id="ed424-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="ed424-437">Дождитесь создания нового **веб-сайта** .</span><span class="sxs-lookup"><span data-stu-id="ed424-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="ed424-438">После создания веб-сайта щелкните ссылку в столбце **URL-адрес** .</span><span class="sxs-lookup"><span data-stu-id="ed424-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="ed424-439">Убедитесь, что новый веб-сайт работает.</span><span class="sxs-lookup"><span data-stu-id="ed424-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="ed424-440">![Обзор нового веб-сайта](aspnet-mvc-4-models-and-data-access/_static/image34.png "Обзор нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="ed424-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="ed424-441">*Обзор нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="ed424-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="ed424-442">![Веб-сайт работает](aspnet-mvc-4-models-and-data-access/_static/image35.png "Веб-сайт работает")</span><span class="sxs-lookup"><span data-stu-id="ed424-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="ed424-443">*Веб-сайт работает*</span><span class="sxs-lookup"><span data-stu-id="ed424-443">*Web site running*</span></span>
6. <span data-ttu-id="ed424-444">Вернитесь на портал и щелкните имя веб-сайта в столбце **имя** , чтобы отобразить страницы управления.</span><span class="sxs-lookup"><span data-stu-id="ed424-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="ed424-445">![Открытие страниц управления веб-сайтом](aspnet-mvc-4-models-and-data-access/_static/image36.png "Открытие страниц управления веб-сайтом")</span><span class="sxs-lookup"><span data-stu-id="ed424-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="ed424-446">*Открытие страниц управления веб-сайтом*</span><span class="sxs-lookup"><span data-stu-id="ed424-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="ed424-447">На странице **панель мониторинга** в разделе **краткий обзор** щелкните ссылку **скачать профиль публикации** .</span><span class="sxs-lookup"><span data-stu-id="ed424-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed424-448">*Профиль публикации* содержит все сведения, необходимые для публикации веб-приложения на веб-сайте Windows Azure для каждого включенного метода публикации.</span><span class="sxs-lookup"><span data-stu-id="ed424-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="ed424-449">Профиль публикации содержит URL-адреса, учетные данные пользователей и строки для открытия базы данных, которые необходимы для проверки подлинности и подключения к каждой из конечных точек, соответствующей разрешенному методу публикации.</span><span class="sxs-lookup"><span data-stu-id="ed424-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="ed424-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express для Web** и **Microsoft Visual Studio 2012** поддерживают чтение профилей публикации для автоматизации настройки этих программ для публикации веб-приложений на веб-сайтах Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="ed424-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="ed424-451">![Скачивание профиля публикации веб-сайта](aspnet-mvc-4-models-and-data-access/_static/image37.png "Скачивание профиля публикации веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="ed424-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="ed424-452">*Скачивание профиля публикации веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="ed424-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="ed424-453">Скачайте файл профиля публикации в известное расположение.</span><span class="sxs-lookup"><span data-stu-id="ed424-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="ed424-454">Далее в этом упражнении вы узнаете, как использовать этот файл для публикации веб-приложения на веб-сайтах Windows Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed424-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="ed424-455">![Сохранение файла профиля публикации](aspnet-mvc-4-models-and-data-access/_static/image38.png "Сохранение профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="ed424-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="ed424-456">*Сохранение файла профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="ed424-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="ed424-457">Задача 2. Настройка сервера базы данных</span><span class="sxs-lookup"><span data-stu-id="ed424-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="ed424-458">Если приложение использует SQL Server базы данных, потребуется создать сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ed424-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="ed424-459">Если вы хотите развернуть простое приложение, которое не использует SQL Server вы можете пропустить эту задачу.</span><span class="sxs-lookup"><span data-stu-id="ed424-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="ed424-460">Для хранения базы данных приложения необходим сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ed424-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="ed424-461">Серверы базы данных SQL можно просмотреть в подписке на портале управления Windows Azure в **базах данных sql** | **серверы** | **панели мониторинга сервера**.</span><span class="sxs-lookup"><span data-stu-id="ed424-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="ed424-462">Если сервер не создан, можно создать его с помощью кнопки **Добавить** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="ed424-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="ed424-463">Запишите **имя сервера и URL-адрес, имя для входа администратора и пароль**, так как они будут использоваться в следующих задачах.</span><span class="sxs-lookup"><span data-stu-id="ed424-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="ed424-464">Пока не создавайте базу данных, так как она будет создана на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="ed424-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="ed424-465">![Панель мониторинга сервера базы данных SQL](aspnet-mvc-4-models-and-data-access/_static/image39.png "Панель мониторинга сервера базы данных SQL")</span><span class="sxs-lookup"><span data-stu-id="ed424-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="ed424-466">*Панель мониторинга сервера базы данных SQL*</span><span class="sxs-lookup"><span data-stu-id="ed424-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="ed424-467">В следующей задаче вы проверите подключение к базе данных из Visual Studio. по этой причине необходимо включить локальный IP-адрес в список **разрешенных IP-адресов**сервера.</span><span class="sxs-lookup"><span data-stu-id="ed424-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="ed424-468">Для этого нажмите кнопку **настроить**, выберите IP-адрес из **текущего IP-адреса клиента** и вставьте его в текстовые поля **начальный IP-адрес** и **конечный IP** -адрес и нажмите кнопку ![добавить-клиент-IP – адрес-OK-кнопка](aspnet-mvc-4-models-and-data-access/_static/image40.png).</span><span class="sxs-lookup"><span data-stu-id="ed424-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![Добавление IP-адреса клиента](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="ed424-470">*Добавление IP-адреса клиента*</span><span class="sxs-lookup"><span data-stu-id="ed424-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="ed424-471">После добавления **IP-адреса клиента** в список Разрешенные IP-адреса нажмите кнопку **сохранить** , чтобы подтвердить изменения.</span><span class="sxs-lookup"><span data-stu-id="ed424-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Подтверждение изменений](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="ed424-473">*Подтверждение изменений*</span><span class="sxs-lookup"><span data-stu-id="ed424-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="ed424-474">Задача 3. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание</span><span class="sxs-lookup"><span data-stu-id="ed424-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="ed424-475">Вернитесь к решению ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="ed424-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="ed424-476">В **Обозреватель решений**щелкните правой кнопкой мыши проект веб-сайта и выберите **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="ed424-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="ed424-477">![Публикация приложения](aspnet-mvc-4-models-and-data-access/_static/image43.png "Публикация приложения")</span><span class="sxs-lookup"><span data-stu-id="ed424-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="ed424-478">*Публикация веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="ed424-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="ed424-479">Импортируйте профиль публикации, сохраненный в первой задаче.</span><span class="sxs-lookup"><span data-stu-id="ed424-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="ed424-480">![Импорт профиля публикации](aspnet-mvc-4-models-and-data-access/_static/image44.png "Импорт профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="ed424-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="ed424-481">*Импорт профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="ed424-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="ed424-482">Щелкните **проверить подключение**.</span><span class="sxs-lookup"><span data-stu-id="ed424-482">Click **Validate Connection**.</span></span> <span data-ttu-id="ed424-483">После завершения проверки нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ed424-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed424-484">Проверка завершится, когда появится зеленая галочка рядом с кнопкой проверить подключение.</span><span class="sxs-lookup"><span data-stu-id="ed424-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="ed424-485">![Проверка подключения](aspnet-mvc-4-models-and-data-access/_static/image45.png "Проверка подключения")</span><span class="sxs-lookup"><span data-stu-id="ed424-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="ed424-486">*Проверка подключения*</span><span class="sxs-lookup"><span data-stu-id="ed424-486">*Validating connection*</span></span>
4. <span data-ttu-id="ed424-487">На странице **Параметры** в разделе **базы данных** нажмите кнопку рядом с текстовым полем подключения к базе данных (т. е. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="ed424-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="ed424-488">![Конфигурация веб-развертывания](aspnet-mvc-4-models-and-data-access/_static/image46.png "Конфигурация веб-развертывания")</span><span class="sxs-lookup"><span data-stu-id="ed424-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="ed424-489">*Конфигурация веб-развертывания*</span><span class="sxs-lookup"><span data-stu-id="ed424-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="ed424-490">Настройте подключение к базе данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ed424-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="ed424-491">В поле **имя сервера** введите URL-адрес сервера базы данных SQL с помощью префикса *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="ed424-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="ed424-492">В окне **имя пользователя** введите имя для входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="ed424-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="ed424-493">В окне **пароль** введите пароль для входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="ed424-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="ed424-494">Введите новое имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed424-494">Type a new database name.</span></span>

     <span data-ttu-id="ed424-495">![Настройка строки подключения к целевому объекту](aspnet-mvc-4-models-and-data-access/_static/image47.png "Настройка строки подключения к целевому объекту")</span><span class="sxs-lookup"><span data-stu-id="ed424-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="ed424-496">*Настройка строки подключения к целевому объекту*</span><span class="sxs-lookup"><span data-stu-id="ed424-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="ed424-497">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ed424-497">Then click **OK**.</span></span> <span data-ttu-id="ed424-498">При появлении запроса на создание базы данных нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="ed424-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="ed424-499">![Создание базы данных](aspnet-mvc-4-models-and-data-access/_static/image48.png "Создание строки базы данных")</span><span class="sxs-lookup"><span data-stu-id="ed424-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="ed424-500">*Создание базы данных*</span><span class="sxs-lookup"><span data-stu-id="ed424-500">*Creating the database*</span></span>
7. <span data-ttu-id="ed424-501">Строка подключения, которая будет использоваться для подключения к базе данных SQL в Windows Azure, отображается в текстовом поле подключения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ed424-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="ed424-502">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ed424-502">Then click **Next**.</span></span>

    <span data-ttu-id="ed424-503">![Строка подключения, указывающая на базу данных SQL](aspnet-mvc-4-models-and-data-access/_static/image49.png "Строка подключения, указывающая на базу данных SQL")</span><span class="sxs-lookup"><span data-stu-id="ed424-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="ed424-504">*Строка подключения, указывающая на базу данных SQL*</span><span class="sxs-lookup"><span data-stu-id="ed424-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="ed424-505">На странице **Предварительный просмотр** нажмите кнопку **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="ed424-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="ed424-506">![Публикация веб-приложения](aspnet-mvc-4-models-and-data-access/_static/image50.png "Публикация веб-приложения")</span><span class="sxs-lookup"><span data-stu-id="ed424-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="ed424-507">*Публикация веб-приложения*</span><span class="sxs-lookup"><span data-stu-id="ed424-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="ed424-508">По завершении процесса публикации браузер по умолчанию будет открывать опубликованный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="ed424-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="ed424-509">Приложение в. Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="ed424-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="ed424-510">С помощью фрагментов кода вы можете получить все необходимые вам коды.</span><span class="sxs-lookup"><span data-stu-id="ed424-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="ed424-511">В лабораторном документе вы узнаете, когда можно использовать их, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="ed424-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="ed424-512">![Использование фрагментов кода Visual Studio для вставки кода в проект](aspnet-mvc-4-models-and-data-access/_static/image51.png "Использование фрагментов кода Visual Studio для вставки кода в проект")</span><span class="sxs-lookup"><span data-stu-id="ed424-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="ed424-513">*Использование фрагментов кода Visual Studio для вставки кода в проект*</span><span class="sxs-lookup"><span data-stu-id="ed424-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="ed424-514">***Добавление фрагмента кода с помощью клавиатуры (C# только)***</span><span class="sxs-lookup"><span data-stu-id="ed424-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="ed424-515">Поместите курсор в то место, куда вы хотите вставить код.</span><span class="sxs-lookup"><span data-stu-id="ed424-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="ed424-516">Начните вводить имя фрагмента (без пробелов или дефисов).</span><span class="sxs-lookup"><span data-stu-id="ed424-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="ed424-517">Посмотрите, как IntelliSense отображает соответствующие имена фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="ed424-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="ed424-518">Выберите правильный фрагмент кода (или вводите его, пока не будет выбрано имя всего фрагмента).</span><span class="sxs-lookup"><span data-stu-id="ed424-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="ed424-519">Дважды нажмите клавишу TAB, чтобы вставить фрагмент в позицию курсора.</span><span class="sxs-lookup"><span data-stu-id="ed424-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="ed424-520">![Начните вводить имя фрагмента](aspnet-mvc-4-models-and-data-access/_static/image52.png "Начните вводить имя фрагмента")</span><span class="sxs-lookup"><span data-stu-id="ed424-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="ed424-521">*Начните вводить имя фрагмента*</span><span class="sxs-lookup"><span data-stu-id="ed424-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="ed424-522">![Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.](aspnet-mvc-4-models-and-data-access/_static/image53.png "Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="ed424-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="ed424-523">*Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="ed424-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="ed424-524">![Снова нажмите клавишу TAB, и фрагмент развернется](aspnet-mvc-4-models-and-data-access/_static/image54.png "Снова нажмите клавишу TAB, и фрагмент развернется")</span><span class="sxs-lookup"><span data-stu-id="ed424-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="ed424-525">*Снова нажмите клавишу TAB, и фрагмент развернется*</span><span class="sxs-lookup"><span data-stu-id="ed424-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="ed424-526">***Добавление фрагмента кода с помощью мыши (C#, Visual Basic и XML)*** одного.</span><span class="sxs-lookup"><span data-stu-id="ed424-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="ed424-527">Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="ed424-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="ed424-528">Выберите **Вставить фрагмент** , за которым следуют **фрагменты кода**.</span><span class="sxs-lookup"><span data-stu-id="ed424-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="ed424-529">Выберите соответствующий фрагмент из списка, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="ed424-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="ed424-530">![Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.](aspnet-mvc-4-models-and-data-access/_static/image55.png "Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="ed424-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="ed424-531">*Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="ed424-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="ed424-532">![Выберите соответствующий фрагмент из списка, щелкнув его.](aspnet-mvc-4-models-and-data-access/_static/image56.png "Выберите соответствующий фрагмент из списка, щелкнув его.")</span><span class="sxs-lookup"><span data-stu-id="ed424-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="ed424-533">*Выберите соответствующий фрагмент из списка, щелкнув его.*</span><span class="sxs-lookup"><span data-stu-id="ed424-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
