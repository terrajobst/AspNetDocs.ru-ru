---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: Учебник. Улучшение проверки данных для EF Database First с помощью приложения ASP.NET MVC
description: В этом учебнике рассматривается добавление заметок к данным в модель данных для указания требований к проверке и форматирования экрана.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499536"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="80acb-103">Учебник. Улучшение проверки данных для EF Database First с помощью приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="80acb-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="80acb-104">С помощью MVC, Entity Framework и шаблонов ASP.NET можно создать веб-приложение, которое предоставляет интерфейс для существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="80acb-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="80acb-105">В этой серии руководств показано, как автоматически создавать код, позволяющий пользователям отображать, изменять, создавать и удалять данные, находящиеся в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="80acb-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="80acb-106">Созданный код соответствует столбцам в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="80acb-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="80acb-107">В этом учебнике рассматривается добавление заметок к данным в модель данных для указания требований к проверке и форматирования экрана.</span><span class="sxs-lookup"><span data-stu-id="80acb-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="80acb-108">Она была улучшена на основе отзывов пользователей в разделе комментариев.</span><span class="sxs-lookup"><span data-stu-id="80acb-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="80acb-109">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="80acb-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="80acb-110">Добавить заметки к данным</span><span class="sxs-lookup"><span data-stu-id="80acb-110">Add data annotations</span></span>
> * <span data-ttu-id="80acb-111">Добавление классов метаданных</span><span class="sxs-lookup"><span data-stu-id="80acb-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80acb-112">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="80acb-112">Prerequisites</span></span>

* [<span data-ttu-id="80acb-113">Настройка представления</span><span class="sxs-lookup"><span data-stu-id="80acb-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="80acb-114">Добавить заметки к данным</span><span class="sxs-lookup"><span data-stu-id="80acb-114">Add data annotations</span></span>

<span data-ttu-id="80acb-115">Как было показано в предыдущем разделе, некоторые правила проверки данных автоматически применяются к введенным пользователем данным.</span><span class="sxs-lookup"><span data-stu-id="80acb-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="80acb-116">Например, можно указать только число для свойства Grade.</span><span class="sxs-lookup"><span data-stu-id="80acb-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="80acb-117">Чтобы указать дополнительные правила проверки данных, можно добавить заметки к данным в класс модели.</span><span class="sxs-lookup"><span data-stu-id="80acb-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="80acb-118">Эти заметки применяются ко всему веб-приложению для указанного свойства.</span><span class="sxs-lookup"><span data-stu-id="80acb-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="80acb-119">Можно также применить атрибуты форматирования, которые изменяют способ отображения свойств. Например, изменение значения, используемого для текстовых меток.</span><span class="sxs-lookup"><span data-stu-id="80acb-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="80acb-120">В этом руководстве вы добавите заметки к данным, чтобы ограничить длину значений, указанных для свойств FirstName, LastName и MiddleName.</span><span class="sxs-lookup"><span data-stu-id="80acb-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="80acb-121">В базе данных эти значения ограничены 50 символами. Однако в веб-приложении ограничения по символам в настоящее время не применяются.</span><span class="sxs-lookup"><span data-stu-id="80acb-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="80acb-122">Если пользователь предоставляет более 50 символов для одного из этих значений, при попытке сохранить значение в базе данных произойдет сбой страницы.</span><span class="sxs-lookup"><span data-stu-id="80acb-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="80acb-123">Кроме того, можно ограничить производительность до значений от 0 до 4.</span><span class="sxs-lookup"><span data-stu-id="80acb-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="80acb-124">Выберите **модели** > **контосомодел. EDMX** > **ContosoModel.TT** и откройте файл *Student.CS* .</span><span class="sxs-lookup"><span data-stu-id="80acb-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="80acb-125">Добавьте выделенный ниже код в класс.</span><span class="sxs-lookup"><span data-stu-id="80acb-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="80acb-126">Откройте *Enrollment.CS* и добавьте следующий выделенный код.</span><span class="sxs-lookup"><span data-stu-id="80acb-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="80acb-127">Создайте решение.</span><span class="sxs-lookup"><span data-stu-id="80acb-127">Build the solution.</span></span>

<span data-ttu-id="80acb-128">Щелкните **список учащихся** и выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="80acb-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="80acb-129">При попытке ввести более 50 символов выводится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="80acb-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![Отображение сообщения об ошибке](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="80acb-131">Вернитесь на домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="80acb-131">Go back to the home page.</span></span> <span data-ttu-id="80acb-132">Щелкните **список регистраций** и выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="80acb-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="80acb-133">Попытка указать уровень выше 4.</span><span class="sxs-lookup"><span data-stu-id="80acb-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="80acb-134">Появится следующее сообщение об ошибке: *поле Grade должно находиться в диапазоне от 0 до 4.*</span><span class="sxs-lookup"><span data-stu-id="80acb-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="80acb-135">Добавление классов метаданных</span><span class="sxs-lookup"><span data-stu-id="80acb-135">Add metadata classes</span></span>

<span data-ttu-id="80acb-136">Добавление атрибутов проверки непосредственно в класс модели работает, если изменение базы данных не предполагается. Однако если база данных изменяется и необходимо повторно создать класс модели, все атрибуты, примененные к классу Model, будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="80acb-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="80acb-137">Этот подход может быть очень неэффективным и подвержен потере важных правил проверки.</span><span class="sxs-lookup"><span data-stu-id="80acb-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="80acb-138">Чтобы избежать этой проблемы, можно добавить класс метаданных, содержащий атрибуты.</span><span class="sxs-lookup"><span data-stu-id="80acb-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="80acb-139">При связывании класса Model с классом метаданных эти атрибуты применяются к модели.</span><span class="sxs-lookup"><span data-stu-id="80acb-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="80acb-140">При таком подходе класс модели может быть создан повторно без потери всех атрибутов, примененных к классу метаданных.</span><span class="sxs-lookup"><span data-stu-id="80acb-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="80acb-141">В папке **Models** добавьте класс с именем *Metadata.CS*.</span><span class="sxs-lookup"><span data-stu-id="80acb-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="80acb-142">Замените код в *Metadata.CS* на следующий код.</span><span class="sxs-lookup"><span data-stu-id="80acb-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="80acb-143">Эти классы метаданных содержат все атрибуты проверки, которые ранее были применены к классам модели.</span><span class="sxs-lookup"><span data-stu-id="80acb-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="80acb-144">Атрибут « **экран** » используется для изменения значения, используемого для текстовых меток.</span><span class="sxs-lookup"><span data-stu-id="80acb-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="80acb-145">Теперь классы модели необходимо связать с классами метаданных.</span><span class="sxs-lookup"><span data-stu-id="80acb-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="80acb-146">В папке **Models** добавьте класс с именем *PartialClasses.CS*.</span><span class="sxs-lookup"><span data-stu-id="80acb-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="80acb-147">Замените содержимое файла на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="80acb-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="80acb-148">Обратите внимание, что каждый класс помечен как класс `partial`, каждый из которых соответствует имени и пространству имен в качестве класса, который создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="80acb-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="80acb-149">Применяя атрибут метаданных к разделяемому классу, вы гарантируете, что атрибуты проверки данных будут применены к автоматически созданному классу.</span><span class="sxs-lookup"><span data-stu-id="80acb-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="80acb-150">Эти атрибуты не будут потеряны при повторном создании классов модели, так как атрибут метаданных применяется в разделяемых классах, которые не создаются повторно.</span><span class="sxs-lookup"><span data-stu-id="80acb-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="80acb-151">Чтобы повторно создать автоматически создаваемые классы, откройте файл *контосомодел. EDMX* .</span><span class="sxs-lookup"><span data-stu-id="80acb-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="80acb-152">Опять же, щелкните правой кнопкой мыши область конструктора и выберите пункт **Обновить модель из базы данных**.</span><span class="sxs-lookup"><span data-stu-id="80acb-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="80acb-153">Несмотря на то, что база данных не была изменена, этот процесс приведет к повторному формированию классов.</span><span class="sxs-lookup"><span data-stu-id="80acb-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="80acb-154">На вкладке **Обновление** выберите **таблицы** и **Готово**.</span><span class="sxs-lookup"><span data-stu-id="80acb-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="80acb-155">Сохраните файл *контосомодел. EDMX* , чтобы применить изменения.</span><span class="sxs-lookup"><span data-stu-id="80acb-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="80acb-156">Откройте файл *Student.CS* или *Enrollment.CS* и обратите внимание, что ранее примененные атрибуты проверки данных больше не находятся в файле.</span><span class="sxs-lookup"><span data-stu-id="80acb-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="80acb-157">Однако запустите приложение и обратите внимание, что правила проверки по-прежнему применяются при вводе данных.</span><span class="sxs-lookup"><span data-stu-id="80acb-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="80acb-158">Заключение</span><span class="sxs-lookup"><span data-stu-id="80acb-158">Conclusion</span></span>

<span data-ttu-id="80acb-159">В этой серии представлен простой пример создания кода из существующей базы данных, которая позволяет пользователям изменять, обновлять, создавать и удалять данные.</span><span class="sxs-lookup"><span data-stu-id="80acb-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="80acb-160">Он использовал ASP.NET MVC 5, Entity Framework и ASP.NET для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="80acb-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="80acb-161">Вводный пример разработки Code First см. в разделе [Начало работы с ASP.NET MVC 5](../introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="80acb-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="80acb-162">Более сложные примеры см. в разделе [создание Entity Framework модели данных для приложения ASP.NET MVC 4](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="80acb-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="80acb-163">Обратите внимание, что API DbContext, используемый для работы с данными в Database First, аналогичен API-интерфейсу, используемому для работы с данными в Code First.</span><span class="sxs-lookup"><span data-stu-id="80acb-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="80acb-164">Даже если вы планируете использовать Database First, вы можете узнать, как обрабатывать более сложные сценарии, такие как чтение и обновление связанных данных, обработка конфликтов параллелизма и т. д. из учебника по Code First.</span><span class="sxs-lookup"><span data-stu-id="80acb-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="80acb-165">Единственное различие заключается в том, как создаются база данных, класс контекста и классы сущностей.</span><span class="sxs-lookup"><span data-stu-id="80acb-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="80acb-166">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="80acb-166">Additional resources</span></span>

<span data-ttu-id="80acb-167">Полный список аннотаций проверки данных, которые можно применять к свойствам и классам, см. в разделе [Примечания к System. ComponentModel](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span><span class="sxs-lookup"><span data-stu-id="80acb-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80acb-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80acb-168">Next steps</span></span>

<span data-ttu-id="80acb-169">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="80acb-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="80acb-170">Добавлены заметки к данным</span><span class="sxs-lookup"><span data-stu-id="80acb-170">Added data annotations</span></span>
> * <span data-ttu-id="80acb-171">Добавленные классы метаданных</span><span class="sxs-lookup"><span data-stu-id="80acb-171">Added metadata classes</span></span>

<span data-ttu-id="80acb-172">Сведения о развертывании веб-приложения и базы данных SQL в службе приложений Azure см. в этом руководстве:</span><span class="sxs-lookup"><span data-stu-id="80acb-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="80acb-173">Развертывание приложения .NET в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="80acb-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
