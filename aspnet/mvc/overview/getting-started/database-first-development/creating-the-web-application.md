---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: Руководство. Создание веб-приложения и моделей данных для EF Database First с помощью ASP.NET MVC
description: В этом учебнике рассматривается создание веб-приложения и создание моделей данных на основе таблиц базы данных.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499530"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="f0c89-103">Руководство. Создание веб-приложения и моделей данных для EF Database First с помощью ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f0c89-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="f0c89-104">С помощью MVC, Entity Framework и шаблонов ASP.NET можно создать веб-приложение, которое предоставляет интерфейс для существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="f0c89-105">В этой серии руководств показано, как автоматически создавать код, позволяющий пользователям отображать, изменять, создавать и удалять данные, находящиеся в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="f0c89-106">Созданный код соответствует столбцам в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="f0c89-107">В этом учебнике рассматривается создание веб-приложения и создание моделей данных на основе таблиц базы данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="f0c89-108">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="f0c89-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f0c89-109">Создание веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0c89-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="f0c89-110">Создание моделей</span><span class="sxs-lookup"><span data-stu-id="f0c89-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0c89-111">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f0c89-111">Prerequisites</span></span>

* [<span data-ttu-id="f0c89-112">Приступая к работе с Entity Framework 6 Database First с помощью MVC 5</span><span class="sxs-lookup"><span data-stu-id="f0c89-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="f0c89-113">Создание веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0c89-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="f0c89-114">В новом решении или в том же решении, что и проект базы данных, создайте новый проект в Visual Studio и выберите шаблон **веб-приложение ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="f0c89-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="f0c89-115">Назовите проект **контососите**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-115">Name the project **ContosoSite**.</span></span>

![создание проекта](creating-the-web-application/_static/image1.png)

<span data-ttu-id="f0c89-117">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-117">Click **OK**.</span></span>

<span data-ttu-id="f0c89-118">В окне Новый проект ASP.NET выберите шаблон **MVC** .</span><span class="sxs-lookup"><span data-stu-id="f0c89-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="f0c89-119">Вы можете очистить **узел в облаке** сейчас, так как приложение будет развернуто в облаке позже.</span><span class="sxs-lookup"><span data-stu-id="f0c89-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="f0c89-120">Нажмите кнопку **ОК** , чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="f0c89-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="f0c89-121">Проект создается с файлами и папками по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f0c89-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="f0c89-122">В этом учебнике будет использоваться Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="f0c89-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="f0c89-123">Вы можете дважды проверить версию Entity Framework в проекте, используя окно Управление пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0c89-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="f0c89-124">При необходимости обновите версию Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="f0c89-124">If necessary, update your version of Entity Framework.</span></span>

![показывать версию](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="f0c89-126">Создание моделей</span><span class="sxs-lookup"><span data-stu-id="f0c89-126">Generate the models</span></span>

<span data-ttu-id="f0c89-127">Теперь в таблицах базы данных будут созданы Entity Framework модели.</span><span class="sxs-lookup"><span data-stu-id="f0c89-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="f0c89-128">Эти модели представляют собой классы, которые будут использоваться для работы с данными.</span><span class="sxs-lookup"><span data-stu-id="f0c89-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="f0c89-129">Каждая модель отражает таблицу в базе данных и содержит свойства, соответствующие столбцам в таблице.</span><span class="sxs-lookup"><span data-stu-id="f0c89-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="f0c89-130">Щелкните правой кнопкой мыши папку **модели** и выберите **Добавить** и **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="f0c89-131">В окне Добавление нового элемента выберите **данные** в левой области и **ADO.NET EDM** из параметров в центральной области.</span><span class="sxs-lookup"><span data-stu-id="f0c89-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="f0c89-132">Назовите новый файл модели **контосомодел**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="f0c89-133">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-133">Click **Add**.</span></span>

<span data-ttu-id="f0c89-134">В мастере EDM выберите элемент **конструктор EF из базы данных**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="f0c89-135">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-135">Click **Next**.</span></span>

<span data-ttu-id="f0c89-136">Если в среде разработки определены подключения к базе данных, вы можете увидеть одно из этих подключений, которые были выбраны заранее.</span><span class="sxs-lookup"><span data-stu-id="f0c89-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="f0c89-137">Однако необходимо создать новое подключение к базе данных, созданной в первой части этого руководства.</span><span class="sxs-lookup"><span data-stu-id="f0c89-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="f0c89-138">Нажмите кнопку **создать подключение** .</span><span class="sxs-lookup"><span data-stu-id="f0c89-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="f0c89-139">В окно свойств подключения укажите имя локального сервера, на котором создана база данных (в данном случае — **LocalDB) \ProjectsV13**).</span><span class="sxs-lookup"><span data-stu-id="f0c89-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="f0c89-140">После указания имени сервера выберите Контосауниверситидата из доступных баз данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![Задание свойств соединения](creating-the-web-application/_static/image8.png)

<span data-ttu-id="f0c89-142">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-142">Click **OK**.</span></span>

<span data-ttu-id="f0c89-143">Теперь отображаются правильные свойства соединения.</span><span class="sxs-lookup"><span data-stu-id="f0c89-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="f0c89-144">Для соединения в файле Web. config можно использовать имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f0c89-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="f0c89-145">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-145">Click **Next**.</span></span>

<span data-ttu-id="f0c89-146">Выберите последнюю версию Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="f0c89-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="f0c89-147">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-147">Click **Next**.</span></span>

<span data-ttu-id="f0c89-148">Выберите **таблицы** , чтобы создать модели для всех трех таблиц.</span><span class="sxs-lookup"><span data-stu-id="f0c89-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="f0c89-149">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f0c89-149">Click **Finish**.</span></span>

<span data-ttu-id="f0c89-150">Если вы получаете предупреждение системы безопасности, нажмите кнопку **ОК** , чтобы продолжить выполнение шаблона.</span><span class="sxs-lookup"><span data-stu-id="f0c89-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="f0c89-151">Модели формируются из таблиц базы данных, и отображается диаграмма, на которой показаны свойства и связи между таблицами.</span><span class="sxs-lookup"><span data-stu-id="f0c89-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![Схема модели](creating-the-web-application/_static/image11.png)

<span data-ttu-id="f0c89-153">Папка Models теперь содержит много новых файлов, связанных с моделями, созданными из базы данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="f0c89-154">Файл **ContosoModel.Context.CS** содержит класс, производный от класса **DbContext** , и предоставляет свойство для каждого класса модели, соответствующего таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="f0c89-155">Файлы **Course.CS**, **Enrollment.CS**и **Student.CS** содержат классы модели, представляющие таблицы баз данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="f0c89-156">При работе с формированием шаблонов вы будете использовать как класс контекста, так и классы модели.</span><span class="sxs-lookup"><span data-stu-id="f0c89-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="f0c89-157">Прежде чем продолжить работу с этим руководством, выполните сборку проекта.</span><span class="sxs-lookup"><span data-stu-id="f0c89-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="f0c89-158">В следующем разделе будет создан код на основе моделей данных, но этот раздел не будет работать, если проект не был построен.</span><span class="sxs-lookup"><span data-stu-id="f0c89-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0c89-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0c89-159">Next steps</span></span>

<span data-ttu-id="f0c89-160">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="f0c89-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f0c89-161">Создано веб-приложение ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0c89-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="f0c89-162">Созданные модели</span><span class="sxs-lookup"><span data-stu-id="f0c89-162">Generated the models</span></span>

<span data-ttu-id="f0c89-163">Перейдите к следующему руководству, чтобы научиться создавать код на основе моделей данных.</span><span class="sxs-lookup"><span data-stu-id="f0c89-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f0c89-164">Создание представлений</span><span class="sxs-lookup"><span data-stu-id="f0c89-164">Generating views</span></span>](generating-views.md)
