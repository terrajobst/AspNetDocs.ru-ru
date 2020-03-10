---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: Руководство. изменение базы данных для EF Database First с помощью приложения ASP.NET MVC
description: В этом учебнике рассматривается обновление структуры базы данных и распространение изменений по всему веб-приложению.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499524"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="ddf8d-103">Руководство. изменение базы данных для EF Database First с помощью приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="ddf8d-103">Tutorial: Change the database for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="ddf8d-104">С помощью MVC, Entity Framework и шаблонов ASP.NET можно создать веб-приложение, которое предоставляет интерфейс для существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="ddf8d-105">В этой серии руководств показано, как автоматически создавать код, позволяющий пользователям отображать, изменять, создавать и удалять данные, находящиеся в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="ddf8d-106">Созданный код соответствует столбцам в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="ddf8d-107">В этом учебнике рассматривается обновление структуры базы данных и распространение изменений по всему веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-107">This tutorial focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>

<span data-ttu-id="ddf8d-108">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="ddf8d-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ddf8d-109">Добавление столбца</span><span class="sxs-lookup"><span data-stu-id="ddf8d-109">Add a column</span></span>
> * <span data-ttu-id="ddf8d-110">Добавление свойства в представления</span><span class="sxs-lookup"><span data-stu-id="ddf8d-110">Add the property to the views</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddf8d-111">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ddf8d-111">Prerequisites</span></span>

* [<span data-ttu-id="ddf8d-112">Создание представлений</span><span class="sxs-lookup"><span data-stu-id="ddf8d-112">Generating views</span></span>](generating-views.md)

## <a name="add-a-column"></a><span data-ttu-id="ddf8d-113">Добавление столбца</span><span class="sxs-lookup"><span data-stu-id="ddf8d-113">Add a column</span></span>

<span data-ttu-id="ddf8d-114">При обновлении структуры таблицы в базе данных необходимо убедиться, что изменение распространяется на модель данных, представления и контроллер.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-114">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="ddf8d-115">В этом руководстве вы добавите новый столбец в таблицу Student, чтобы записать отчество учащегося.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-115">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="ddf8d-116">Чтобы добавить этот столбец, откройте проект базы данных и откройте файл Student. SQL.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-116">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="ddf8d-117">С помощью конструктора или кода T-SQL добавьте столбец с именем **MiddleName** , который имеет тип nvarchar (50) и допускает значения NULL.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-117">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

<span data-ttu-id="ddf8d-118">Разверните это изменение в локальной базе данных, запустив проект базы данных (или нажав клавишу F5).</span><span class="sxs-lookup"><span data-stu-id="ddf8d-118">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="ddf8d-119">Новое поле будет добавлено в таблицу.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-119">The new field is added to the table.</span></span> <span data-ttu-id="ddf8d-120">Если вы не видите его в обозреватель объектов SQL Server, нажмите кнопку Обновить на панели.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-120">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![отобразить новый столбец](changing-the-database/_static/image2.png)

<span data-ttu-id="ddf8d-122">Новый столбец существует в таблице базы данных, но в настоящее время он не существует в классе модели данных.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-122">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="ddf8d-123">Необходимо обновить модель, включив в нее новый столбец.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-123">You must update the model to include your new column.</span></span> <span data-ttu-id="ddf8d-124">В папке **Models** откройте файл **контосомодел. EDMX** , чтобы отобразить диаграмму модели.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-124">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="ddf8d-125">Обратите внимание, что модель Student не содержит свойство MiddleName.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-125">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="ddf8d-126">Щелкните правой кнопкой мыши в любом месте области конструктора и выберите пункт **Обновить модель из базы данных**.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-126">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

<span data-ttu-id="ddf8d-127">В мастере обновления перейдите на вкладку **Обновление** , а затем выберите **таблицы** > **dbo** > **Student**.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-127">In the Update Wizard, select the **Refresh** tab and then select **Tables** > **dbo** > **Student**.</span></span> <span data-ttu-id="ddf8d-128">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-128">Click **Finish**.</span></span>

<span data-ttu-id="ddf8d-129">После завершения процесса обновления диаграмма базы данных включает новое свойство **MiddleName** .</span><span class="sxs-lookup"><span data-stu-id="ddf8d-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="ddf8d-130">Сохраните файл **контосомодел. EDMX** .</span><span class="sxs-lookup"><span data-stu-id="ddf8d-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="ddf8d-131">Необходимо сохранить этот файл, чтобы новое свойство распространялось на класс **Student.CS** .</span><span class="sxs-lookup"><span data-stu-id="ddf8d-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="ddf8d-132">Теперь база данных и модель обновлены.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="ddf8d-133">Создайте решение.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-133">Build the solution.</span></span>

## <a name="add-the-property-to-the-views"></a><span data-ttu-id="ddf8d-134">Добавление свойства в представления</span><span class="sxs-lookup"><span data-stu-id="ddf8d-134">Add the property to the views</span></span>

<span data-ttu-id="ddf8d-135">К сожалению, представления по-прежнему не содержат нового свойства.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-135">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="ddf8d-136">Чтобы обновить представления с двумя параметрами, можно либо повторно создать представления, снова добавив формирование шаблонов для класса Student, либо добавить новое свойство в существующие представления вручную.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-136">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="ddf8d-137">В этом учебнике вы добавите формирование шаблонов еще раз, так как вы не внесли какие-либо изменения в автоматически создаваемые представления.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-137">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="ddf8d-138">Вы можете добавить свойство вручную, когда вы внесли изменения в представления и не хотите потерять эти изменения.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-138">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="ddf8d-139">Чтобы убедиться, что представления созданы повторно, удалите папку **students** в области **представления**и удалите **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-139">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="ddf8d-140">Затем щелкните правой кнопкой мыши папку **Controllers** и добавьте формирование шаблонов для модели **учащихся** .</span><span class="sxs-lookup"><span data-stu-id="ddf8d-140">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="ddf8d-141">Снова назовите контроллер **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-141">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="ddf8d-142">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-142">Select **Add**.</span></span>

<span data-ttu-id="ddf8d-143">Выполните повторную сборку решения.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-143">Build the solution again.</span></span> <span data-ttu-id="ddf8d-144">Представления теперь содержат свойство MiddleName.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-144">The views now contain the MiddleName property.</span></span>

![показывать отчество](changing-the-database/_static/image5.png)

## <a name="next-steps"></a><span data-ttu-id="ddf8d-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ddf8d-146">Next steps</span></span>

<span data-ttu-id="ddf8d-147">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="ddf8d-147">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ddf8d-148">Добавлен столбец</span><span class="sxs-lookup"><span data-stu-id="ddf8d-148">Added a column</span></span>
> * <span data-ttu-id="ddf8d-149">Добавлено свойство в представления</span><span class="sxs-lookup"><span data-stu-id="ddf8d-149">Added the property to the views</span></span>

<span data-ttu-id="ddf8d-150">Перейдите к следующему руководству, чтобы узнать, как настроить представление для отображения сведений о записи учащегося.</span><span class="sxs-lookup"><span data-stu-id="ddf8d-150">Advance to the next tutorial to learn how to customize the view for showing details about a student record.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ddf8d-151">Настройка представления</span><span class="sxs-lookup"><span data-stu-id="ddf8d-151">Customize a view</span></span>](customizing-a-view.md)