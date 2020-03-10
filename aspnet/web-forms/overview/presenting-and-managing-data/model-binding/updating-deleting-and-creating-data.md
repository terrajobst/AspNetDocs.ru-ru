---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: Обновление, удаление и создание данных с помощью привязки модели и веб-форм | Документация Майкрософт
author: Rick-Anderson
description: В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET. Привязка модели делает взаимодействие данных более прямым-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474138"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="34813-104">Обновление, удаление и создание данных с помощью привязки модели и веб-форм</span><span class="sxs-lookup"><span data-stu-id="34813-104">Updating, deleting, and creating data with model binding and web forms</span></span>

<span data-ttu-id="34813-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="34813-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="34813-106">В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="34813-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="34813-107">Привязка модели делает взаимодействие данных более прямым, чем работа с объектами источника данных (например, ObjectDataSource или SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="34813-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="34813-108">Эта серия начинается с вводного материала и переходит к более сложным концепциям в последующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="34813-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="34813-109">В этом руководстве показано, как создавать, обновлять и удалять данные с помощью привязки модели.</span><span class="sxs-lookup"><span data-stu-id="34813-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="34813-110">Будут заданы следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="34813-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="34813-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="34813-111">DeleteMethod</span></span>
> - <span data-ttu-id="34813-112">InsertMethod</span><span class="sxs-lookup"><span data-stu-id="34813-112">InsertMethod</span></span>
> - <span data-ttu-id="34813-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="34813-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="34813-114">Эти свойства получают имя метода, обрабатывающего соответствующую операцию.</span><span class="sxs-lookup"><span data-stu-id="34813-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="34813-115">В этом методе вы предоставляете логику для взаимодействия с данными.</span><span class="sxs-lookup"><span data-stu-id="34813-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="34813-116">Это руководство строится на проекте, созданном в первой [части](retrieving-data.md) серии.</span><span class="sxs-lookup"><span data-stu-id="34813-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="34813-117">Вы можете [скачать](https://go.microsoft.com/fwlink/?LinkId=286116) полный проект в C# или VB.</span><span class="sxs-lookup"><span data-stu-id="34813-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="34813-118">Загружаемый код работает как с Visual Studio 2012, так и с Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="34813-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="34813-119">В нем используется шаблон Visual Studio 2012, который немного отличается от шаблона Visual Studio 2013, показанного в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="34813-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="34813-120">Что будет построено</span><span class="sxs-lookup"><span data-stu-id="34813-120">What you'll build</span></span>

<span data-ttu-id="34813-121">В этом руководстве вы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="34813-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="34813-122">Добавление шаблонов динамических данных</span><span class="sxs-lookup"><span data-stu-id="34813-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="34813-123">Включение обновления и удаления данных с помощью методов привязки модели</span><span class="sxs-lookup"><span data-stu-id="34813-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="34813-124">Применение правил проверки данных — включение создания новой записи в базе данных</span><span class="sxs-lookup"><span data-stu-id="34813-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="34813-125">Добавление шаблонов динамических данных</span><span class="sxs-lookup"><span data-stu-id="34813-125">Add dynamic data templates</span></span>

<span data-ttu-id="34813-126">Чтобы обеспечить оптимальное взаимодействие с пользователем и избежать повторения кода, вы будете использовать динамические шаблоны данных.</span><span class="sxs-lookup"><span data-stu-id="34813-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="34813-127">Предварительно созданные шаблоны динамических данных можно легко интегрировать в существующий сайт, установив пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="34813-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="34813-128">В окне **Управление пакетами NuGet**установите **динамикдататемплатескс**.</span><span class="sxs-lookup"><span data-stu-id="34813-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![Шаблоны динамических данных](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="34813-130">Обратите внимание, что теперь проект включает папку с именем **DynamicData**.</span><span class="sxs-lookup"><span data-stu-id="34813-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="34813-131">В этой папке вы найдете шаблоны, которые автоматически применяются к динамическим элементам управления в веб-формах.</span><span class="sxs-lookup"><span data-stu-id="34813-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![Папка динамических данных](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="34813-133">Включить обновление и удаление</span><span class="sxs-lookup"><span data-stu-id="34813-133">Enable updating and deleting</span></span>

<span data-ttu-id="34813-134">Предоставление пользователям возможности обновлять и удалять записи в базе данных очень похоже на процесс извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="34813-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="34813-135">В свойствах **UpdateMethod** и **DeleteMethod** указываются имена методов, которые выполняют эти операции.</span><span class="sxs-lookup"><span data-stu-id="34813-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="34813-136">С помощью элемента управления GridView можно также указать автоматическое создание кнопок «изменить» и «удалить».</span><span class="sxs-lookup"><span data-stu-id="34813-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="34813-137">В следующем выделенном коде показаны дополнения к коду GridView.</span><span class="sxs-lookup"><span data-stu-id="34813-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="34813-138">В файле кода программной части добавьте инструкцию using для **System. Data. Entity. Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="34813-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="34813-139">Затем добавьте следующие методы Update и DELETE.</span><span class="sxs-lookup"><span data-stu-id="34813-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="34813-140">Метод **трюпдатемодел** применяет соответствующие значения, привязанные к данным, из веб-формы к элементу данных.</span><span class="sxs-lookup"><span data-stu-id="34813-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="34813-141">Элемент данных извлекается на основе значения параметра ID.</span><span class="sxs-lookup"><span data-stu-id="34813-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="34813-142">Соблюдение требований к проверке</span><span class="sxs-lookup"><span data-stu-id="34813-142">Enforce validation requirements</span></span>

<span data-ttu-id="34813-143">Атрибуты проверки, которые были применены к свойствам FirstName, LastName и year в классе Student, автоматически применяются при обновлении данных.</span><span class="sxs-lookup"><span data-stu-id="34813-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="34813-144">Элементы управления Динамикфиелд добавляют средства проверки клиента и сервера на основе атрибутов проверки.</span><span class="sxs-lookup"><span data-stu-id="34813-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="34813-145">Свойства FirstName и LastName являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="34813-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="34813-146">Длина имени не может превышать 20 символов, а имя LastName не должно превышать 40 символов.</span><span class="sxs-lookup"><span data-stu-id="34813-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="34813-147">Год должен быть допустимым значением для перечисления Академициеар.</span><span class="sxs-lookup"><span data-stu-id="34813-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="34813-148">Если пользователь нарушает одно из требований проверки, обновление не выполняется.</span><span class="sxs-lookup"><span data-stu-id="34813-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="34813-149">Чтобы увидеть сообщение об ошибке, добавьте элемент управления ValidationSummary над элементом GridView.</span><span class="sxs-lookup"><span data-stu-id="34813-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="34813-150">Чтобы отобразить ошибки проверки из привязки модели, установите для свойства **шовмоделстатиррорс** значение **true**.</span><span class="sxs-lookup"><span data-stu-id="34813-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="34813-151">Запустите веб-приложение и обновите и удалите все записи.</span><span class="sxs-lookup"><span data-stu-id="34813-151">Run the web application, and update and delete any of the records.</span></span>

![Обновление данных](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="34813-153">Обратите внимание, что в режиме редактирования значение свойства Year автоматически подготавливается к просмотру в виде раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="34813-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="34813-154">Свойство year является значением перечисления, а шаблон динамических данных для значения перечисления указывает раскрывающийся список для редактирования.</span><span class="sxs-lookup"><span data-stu-id="34813-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="34813-155">Этот шаблон можно найти, открыв **Перечисление\_файл Edit. ascx** в папке **DynamicData**/**фиелдтемплатес** .</span><span class="sxs-lookup"><span data-stu-id="34813-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="34813-156">Если указать допустимые значения, обновление завершается успешно.</span><span class="sxs-lookup"><span data-stu-id="34813-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="34813-157">Если вы нарушаете одно из требований проверки, обновление не выполняется, а над сеткой отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="34813-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![сообщение об ошибке](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="34813-159">Добавить новые записи</span><span class="sxs-lookup"><span data-stu-id="34813-159">Add new records</span></span>

<span data-ttu-id="34813-160">Элемент управления GridView не включает свойство **InsertMethod** и поэтому не может использоваться для добавления новой записи с привязкой модели.</span><span class="sxs-lookup"><span data-stu-id="34813-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="34813-161">Свойство InsertMethod можно найти в элементе управления **FormView**, **DetailsView**или **ListView** .</span><span class="sxs-lookup"><span data-stu-id="34813-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="34813-162">В этом учебнике для добавления новой записи будет использоваться элемент управления FormView.</span><span class="sxs-lookup"><span data-stu-id="34813-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="34813-163">Сначала добавьте ссылку на новую страницу, которая будет создана для добавления новой записи.</span><span class="sxs-lookup"><span data-stu-id="34813-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="34813-164">Над ValidationSummary добавьте:</span><span class="sxs-lookup"><span data-stu-id="34813-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="34813-165">Новая ссылка появится в верхней части содержимого страницы учащихся.</span><span class="sxs-lookup"><span data-stu-id="34813-165">The new link will appear at the top of the content for the Students page.</span></span>

![создать ссылку](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="34813-167">Затем добавьте новую веб-форму с помощью главной страницы и назовите ее **аддстудент**.</span><span class="sxs-lookup"><span data-stu-id="34813-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="34813-168">Выберите Site. master в качестве главной страницы.</span><span class="sxs-lookup"><span data-stu-id="34813-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="34813-169">Вы будете отображать поля для добавления нового учащегося с помощью элемента управления **DynamicControl** .</span><span class="sxs-lookup"><span data-stu-id="34813-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="34813-170">Элемент управления DynamicControl визуализирует эти редактируемые свойства в классе, указанном в свойстве ItemType.</span><span class="sxs-lookup"><span data-stu-id="34813-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="34813-171">Свойство StudentID было помечено атрибутом **[скаффолдколумн (false)]** , поэтому он не подготавливается к просмотру.</span><span class="sxs-lookup"><span data-stu-id="34813-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="34813-172">В заполнитель MainContent страницы Аддстудент добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="34813-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="34813-173">В файле кода программной части (AddStudent.aspx.cs) добавьте инструкцию **using** для пространства имен **контосауниверситимоделбиндинг. Models** .</span><span class="sxs-lookup"><span data-stu-id="34813-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="34813-174">Затем добавьте следующие методы, чтобы указать, как вставить новую запись и обработчик событий для кнопки Отмена.</span><span class="sxs-lookup"><span data-stu-id="34813-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="34813-175">Сохраните все изменения.</span><span class="sxs-lookup"><span data-stu-id="34813-175">Save all of the changes.</span></span>

<span data-ttu-id="34813-176">Запустите веб-приложение и создайте учащийся.</span><span class="sxs-lookup"><span data-stu-id="34813-176">Run the web application and create a new student.</span></span>

![добавить нового учащегося](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="34813-178">Нажмите кнопку **Вставить** и обратите внимание, что создан новый учащийся.</span><span class="sxs-lookup"><span data-stu-id="34813-178">Click **Insert** and notice the new student has been created.</span></span>

![Показать нового учащегося](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="34813-180">Заключение</span><span class="sxs-lookup"><span data-stu-id="34813-180">Conclusion</span></span>

<span data-ttu-id="34813-181">В этом руководстве вы включили обновление, удаление и создание данных.</span><span class="sxs-lookup"><span data-stu-id="34813-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="34813-182">Гарантируется, что правила проверки применяются при взаимодействии с данными.</span><span class="sxs-lookup"><span data-stu-id="34813-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="34813-183">В следующем [руководстве](sorting-paging-and-filtering-data.md) этой серии вы включите сортировку, разбиение по страницам и фильтрацию данных.</span><span class="sxs-lookup"><span data-stu-id="34813-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34813-184">[Назад](retrieving-data.md)
> [Вперед](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="34813-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
