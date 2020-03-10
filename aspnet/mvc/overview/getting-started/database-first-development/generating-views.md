---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: Учебник. Создание представлений для EF Database First с помощью приложения ASP.NET MVC
description: В этом учебнике рассматривается использование формирования шаблонов ASP.NET для создания контроллеров и представлений.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499476"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="f11f4-103">Учебник. Создание представлений для EF Database First с помощью приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f11f4-103">Tutorial: Generate views for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="f11f4-104">С помощью MVC, Entity Framework и шаблонов ASP.NET можно создать веб-приложение, которое предоставляет интерфейс для существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="f11f4-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="f11f4-105">В этой серии руководств показано, как автоматически создавать код, позволяющий пользователям отображать, изменять, создавать и удалять данные, находящиеся в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="f11f4-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="f11f4-106">Созданный код соответствует столбцам в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="f11f4-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="f11f4-107">В этом учебнике рассматривается использование формирования шаблонов ASP.NET для создания контроллеров и представлений.</span><span class="sxs-lookup"><span data-stu-id="f11f4-107">This tutorial focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>

<span data-ttu-id="f11f4-108">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="f11f4-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f11f4-109">Добавление шаблона</span><span class="sxs-lookup"><span data-stu-id="f11f4-109">Add scaffold</span></span>
> * <span data-ttu-id="f11f4-110">Добавить ссылки на новые представления</span><span class="sxs-lookup"><span data-stu-id="f11f4-110">Add links to new views</span></span>
> * <span data-ttu-id="f11f4-111">Отображение представлений учащихся</span><span class="sxs-lookup"><span data-stu-id="f11f4-111">Display student views</span></span>
> * <span data-ttu-id="f11f4-112">Отображение представлений регистрации</span><span class="sxs-lookup"><span data-stu-id="f11f4-112">Display enrollment views</span></span>

## <a name="prerequisite"></a><span data-ttu-id="f11f4-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f11f4-113">Prerequisite</span></span>

* [<span data-ttu-id="f11f4-114">Создание веб-приложения и моделей данных</span><span class="sxs-lookup"><span data-stu-id="f11f4-114">Create the web application and data models</span></span>](creating-the-web-application.md)

## <a name="add-scaffold"></a><span data-ttu-id="f11f4-115">Добавление шаблона</span><span class="sxs-lookup"><span data-stu-id="f11f4-115">Add scaffold</span></span>

<span data-ttu-id="f11f4-116">Все готово для создания кода, который предоставит стандартные операции с данными для классов модели.</span><span class="sxs-lookup"><span data-stu-id="f11f4-116">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="f11f4-117">Код добавляется путем добавления элемента шаблона.</span><span class="sxs-lookup"><span data-stu-id="f11f4-117">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="f11f4-118">Существует множество параметров для типа шаблонов, которые можно добавить. в этом руководстве шаблон будет включать контроллер и представления, соответствующие моделям учащихся и регистраций, созданным в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="f11f4-118">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="f11f4-119">Чтобы обеспечить согласованность в проекте, необходимо добавить новый контроллер в папку существующие **контроллеры** .</span><span class="sxs-lookup"><span data-stu-id="f11f4-119">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="f11f4-120">Щелкните правой кнопкой мыши папку **Controllers** и выберите **Добавить** > **Новый**шаблонный элемент.</span><span class="sxs-lookup"><span data-stu-id="f11f4-120">Right-click the **Controllers** folder, and select **Add** > **New Scaffolded Item**.</span></span>

<span data-ttu-id="f11f4-121">Выберите **контроллер MVC 5 с представлениями с помощью параметра Entity Framework** .</span><span class="sxs-lookup"><span data-stu-id="f11f4-121">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="f11f4-122">Этот параметр позволяет создать контроллер и представления для обновления, удаления, создания и отображения данных в модели.</span><span class="sxs-lookup"><span data-stu-id="f11f4-122">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![Добавление контроллера MVC](generating-views/_static/image2.png)

<span data-ttu-id="f11f4-124">Выберите **Student (контососите. Models)** для класса Model и выберите **контосауниверситидатаентитиес (контососите. Models)** для класса контекста.</span><span class="sxs-lookup"><span data-stu-id="f11f4-124">Select **Student (ContosoSite.Models)** for the model class and select the **ContosoUniversityDataEntities (ContosoSite.Models)** for the context class.</span></span> <span data-ttu-id="f11f4-125">В качестве имени контроллера следует использовать **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="f11f4-125">Keep the controller name as **StudentsController**.</span></span>

<span data-ttu-id="f11f4-126">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f11f4-126">Click **Add**.</span></span>

<span data-ttu-id="f11f4-127">Если появляется сообщение об ошибке, это может быть вызвано тем, что проект не был построен в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="f11f4-127">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="f11f4-128">Если да, попробуйте выполнить сборку проекта, а затем снова добавьте шаблонный элемент.</span><span class="sxs-lookup"><span data-stu-id="f11f4-128">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="f11f4-129">После завершения создания кода вы увидите новый контроллер и представления в **контроллерах** и **представлениях** проекта > **учащихся** .</span><span class="sxs-lookup"><span data-stu-id="f11f4-129">After the code generation process is complete, you will see a new controller and views in your project's **Controllers** and **Views** > **Students** folders.</span></span>

<span data-ttu-id="f11f4-130">Выполните те же действия еще раз, но добавьте шаблон для класса **регистрации** .</span><span class="sxs-lookup"><span data-stu-id="f11f4-130">Perform the same steps again, but add a scaffold for the **Enrollment** class.</span></span> <span data-ttu-id="f11f4-131">По завершении вы получите файл **EnrollmentsController.CS** и папку в **представлениях** с именами **регистрации** с представлениями создание, удаление, сведения, редактирование и индекс.</span><span class="sxs-lookup"><span data-stu-id="f11f4-131">When finished, you have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

## <a name="add-links-to-new-views"></a><span data-ttu-id="f11f4-132">Добавить ссылки на новые представления</span><span class="sxs-lookup"><span data-stu-id="f11f4-132">Add links to new views</span></span>

<span data-ttu-id="f11f4-133">Чтобы упростить переход к новым представлениям, можно добавить пару гиперссылок в представления индекса для учащихся и регистраций.</span><span class="sxs-lookup"><span data-stu-id="f11f4-133">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="f11f4-134">Откройте файл в **представлении** > **Домашняя** > *index. cshtml*, который является домашней страницей для сайта.</span><span class="sxs-lookup"><span data-stu-id="f11f4-134">Open the file at **Views** > **Home** > *Index.cshtml*, which is the home page for your site.</span></span> <span data-ttu-id="f11f4-135">Добавьте следующий код под Jumbotron.</span><span class="sxs-lookup"><span data-stu-id="f11f4-135">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="f11f4-136">Для метода ActionLink первым параметром является текст, отображаемый в ссылке.</span><span class="sxs-lookup"><span data-stu-id="f11f4-136">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="f11f4-137">Вторым параметром является действие, а третий параметр — имя контроллера.</span><span class="sxs-lookup"><span data-stu-id="f11f4-137">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="f11f4-138">Например, первая ссылка указывает на действие index в StudentsController.</span><span class="sxs-lookup"><span data-stu-id="f11f4-138">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="f11f4-139">Фактическая гиперссылка создается на основе этих значений.</span><span class="sxs-lookup"><span data-stu-id="f11f4-139">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="f11f4-140">Первая ссылка в конечном итоге переводит пользователей в файл **index. cshtml** в папке **views/Students** .</span><span class="sxs-lookup"><span data-stu-id="f11f4-140">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="f11f4-141">Отображение представлений учащихся</span><span class="sxs-lookup"><span data-stu-id="f11f4-141">Display student views</span></span>

<span data-ttu-id="f11f4-142">Вы убедитесь, что код, добавленный в проект, правильно отображает список учащихся и позволяет пользователям изменять, создавать или удалять записи учащихся в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f11f4-142">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="f11f4-143">Щелкните правой кнопкой мыши файл **views** > **Home** > *index. cshtml* и выберите **Просмотреть в браузере**.</span><span class="sxs-lookup"><span data-stu-id="f11f4-143">Right-click the **Views** > **Home** > *Index.cshtml* file, and select **View in Browser**.</span></span> <span data-ttu-id="f11f4-144">На домашней странице приложения выберите **список учащихся**.</span><span class="sxs-lookup"><span data-stu-id="f11f4-144">On the application home page, select **List of students**.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="f11f4-145">На странице **индекс** Обратите внимание на список учащихся и ссылок для изменения этих данных.</span><span class="sxs-lookup"><span data-stu-id="f11f4-145">On the **Index** page, notice the list of the students and links to modify this data.</span></span> <span data-ttu-id="f11f4-146">Выберите ссылку **создать** и укажите некоторые значения для нового учащегося.</span><span class="sxs-lookup"><span data-stu-id="f11f4-146">Select the **Create New** link and provide some values for a new student.</span></span> <span data-ttu-id="f11f4-147">Нажмите кнопку **создать**и обратите внимание, что новый учащийся добавлен в список.</span><span class="sxs-lookup"><span data-stu-id="f11f4-147">Click **Create**, and notice the new student is added to your list.</span></span>

<span data-ttu-id="f11f4-148">Вернитесь на страницу **индекса** , щелкните ссылку **изменить** и измените некоторые значения учащегося.</span><span class="sxs-lookup"><span data-stu-id="f11f4-148">Back on the **Index** page, select the **Edit** link, and change some of the values for a student.</span></span> <span data-ttu-id="f11f4-149">Нажмите кнопку **сохранить**и обратите внимание, что запись учащегося изменена.</span><span class="sxs-lookup"><span data-stu-id="f11f4-149">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="f11f4-150">Наконец, выберите ссылку **Удалить** и подтвердите, что вы хотите удалить запись, нажав кнопку **Удалить** .</span><span class="sxs-lookup"><span data-stu-id="f11f4-150">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

<span data-ttu-id="f11f4-151">Без написания кода вы добавили представления, которые выполняют общие операции с данными в таблице Student.</span><span class="sxs-lookup"><span data-stu-id="f11f4-151">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="f11f4-152">Возможно, вы заметили, что текстовая метка для поля основана на свойстве базы данных (например, **LastName**), которое не обязательно должно отображаться на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="f11f4-152">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="f11f4-153">Например, имя метки может быть **фамилией**.</span><span class="sxs-lookup"><span data-stu-id="f11f4-153">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="f11f4-154">Вы сможете устранить эту проблему с отображением позже в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f11f4-154">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="f11f4-155">Отображение представлений регистрации</span><span class="sxs-lookup"><span data-stu-id="f11f4-155">Display enrollment views</span></span>

<span data-ttu-id="f11f4-156">База данных включает связь «один ко многим» между таблицами учащихся и регистраций, а также связь «один ко многим» между таблицами «курс» и «регистрация».</span><span class="sxs-lookup"><span data-stu-id="f11f4-156">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="f11f4-157">Представления для регистрации правильно обрабатывали эти связи.</span><span class="sxs-lookup"><span data-stu-id="f11f4-157">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="f11f4-158">Перейдите на домашнюю страницу сайта и выберите ссылку на **список регистраций** , а затем щелкните **создать** ссылку.</span><span class="sxs-lookup"><span data-stu-id="f11f4-158">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span>

<span data-ttu-id="f11f4-159">Представление отображает форму для создания новой записи регистрации.</span><span class="sxs-lookup"><span data-stu-id="f11f4-159">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="f11f4-160">В частности, обратите внимание, что форма содержит раскрывающийся список **CourseID** и раскрывающийся список **StudentId** .</span><span class="sxs-lookup"><span data-stu-id="f11f4-160">In particular, notice that the form contains a **CourseID** drop-down list and a **StudentID** drop-down list.</span></span> <span data-ttu-id="f11f4-161">Оба значения заполняются значениями из связанных таблиц.</span><span class="sxs-lookup"><span data-stu-id="f11f4-161">Both are populated with values from the related tables.</span></span>

<span data-ttu-id="f11f4-162">Кроме того, проверка указанных значений автоматически применяется в зависимости от типа данных поля.</span><span class="sxs-lookup"><span data-stu-id="f11f4-162">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="f11f4-163">**Оценка** требует числового значения, поэтому при попытке предоставить несовместимое значение выводится сообщение об ошибке: *поле Grade должно быть числом.*</span><span class="sxs-lookup"><span data-stu-id="f11f4-163">**Grade** requires a number, so an error message is displayed if you try to provide an incompatible value: *The field Grade must be a number.*</span></span>

<span data-ttu-id="f11f4-164">Вы проверили, что автоматически создаваемые представления позволяют пользователям работать с данными в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f11f4-164">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="f11f4-165">В следующем учебнике этой серии будет обновлена база данных и внесены соответствующие изменения в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="f11f4-165">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f11f4-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f11f4-166">Next steps</span></span>

<span data-ttu-id="f11f4-167">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="f11f4-167">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f11f4-168">Добавлен шаблон</span><span class="sxs-lookup"><span data-stu-id="f11f4-168">Added scaffold</span></span>
> * <span data-ttu-id="f11f4-169">Добавлены ссылки на новые представления</span><span class="sxs-lookup"><span data-stu-id="f11f4-169">Added links to new views</span></span>
> * <span data-ttu-id="f11f4-170">Отображаемые представления учащихся</span><span class="sxs-lookup"><span data-stu-id="f11f4-170">Displayed student views</span></span>
> * <span data-ttu-id="f11f4-171">Отображаемые представления регистрации</span><span class="sxs-lookup"><span data-stu-id="f11f4-171">Displayed enrollment views</span></span>

<span data-ttu-id="f11f4-172">Перейдите к следующему руководству, чтобы узнать, как изменить базу данных.</span><span class="sxs-lookup"><span data-stu-id="f11f4-172">Advance to the next tutorial to learn how to change the database.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f11f4-173">Изменение базы данных</span><span class="sxs-lookup"><span data-stu-id="f11f4-173">Change the database</span></span>](changing-the-database.md)