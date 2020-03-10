---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: Интеграция пользовательского интерфейса JQuery с привязкой модели и веб-формами | Документация Майкрософт
author: Rick-Anderson
description: В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET. Привязка модели делает взаимодействие данных более прямым-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521982"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="6b39f-104">Интеграция пользовательского интерфейса JQuery с привязкой модели и веб-формами</span><span class="sxs-lookup"><span data-stu-id="6b39f-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>

<span data-ttu-id="6b39f-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6b39f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6b39f-106">В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6b39f-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="6b39f-107">Привязка модели делает взаимодействие данных более прямым, чем работа с объектами источника данных (например, ObjectDataSource или SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="6b39f-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="6b39f-108">Эта серия начинается с вводного материала и переходит к более сложным концепциям в последующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="6b39f-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="6b39f-109">В этом руководстве показано, как добавить мини-приложение [DatePicker](http://jqueryui.com/datepicker/) пользовательского интерфейса jQuery в форму Web Forms и использовать привязку модели для обновления базы данных с выбранным значением.</span><span class="sxs-lookup"><span data-stu-id="6b39f-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="6b39f-110">Это руководство строится на проекте, созданном в [первой](retrieving-data.md) и [второй](updating-deleting-and-creating-data.md) частях серии.</span><span class="sxs-lookup"><span data-stu-id="6b39f-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="6b39f-111">Вы можете [скачать](https://go.microsoft.com/fwlink/?LinkId=286116) полный проект в C# или VB.</span><span class="sxs-lookup"><span data-stu-id="6b39f-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="6b39f-112">Загружаемый код работает как с Visual Studio 2012, так и с Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6b39f-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="6b39f-113">В нем используется шаблон Visual Studio 2012, который немного отличается от шаблона Visual Studio 2013, показанного в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="6b39f-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="6b39f-114">Что будет построено</span><span class="sxs-lookup"><span data-stu-id="6b39f-114">What you'll build</span></span>

<span data-ttu-id="6b39f-115">В этом руководстве вы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6b39f-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="6b39f-116">Добавление свойства в модель для записи даты регистрации учащегося</span><span class="sxs-lookup"><span data-stu-id="6b39f-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="6b39f-117">Предоставление пользователю возможности выбора даты регистрации с помощью мини-приложения DatePicker пользовательского интерфейса JQuery</span><span class="sxs-lookup"><span data-stu-id="6b39f-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="6b39f-118">Применение правил проверки для даты регистрации</span><span class="sxs-lookup"><span data-stu-id="6b39f-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="6b39f-119">Мини-приложение DatePicker пользовательского интерфейса JQuery позволяет пользователям легко выбирать дату из календаря, который появляется, когда пользователь взаимодействует с полем.</span><span class="sxs-lookup"><span data-stu-id="6b39f-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="6b39f-120">Использование этого мини-приложения может оказаться более удобным для пользователей, чем ввод даты вручную.</span><span class="sxs-lookup"><span data-stu-id="6b39f-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="6b39f-121">Интеграция мини-приложения DatePicker в страницу, использующую привязку модели для операций с данными, требует лишь небольшого объема дополнительной работы.</span><span class="sxs-lookup"><span data-stu-id="6b39f-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="6b39f-122">Добавление нового свойства в модель</span><span class="sxs-lookup"><span data-stu-id="6b39f-122">Add a new property to the model</span></span>

<span data-ttu-id="6b39f-123">Во-первых, вы добавите свойство **DateTime** в модель учащихся и перенесите это изменение в базу данных.</span><span class="sxs-lookup"><span data-stu-id="6b39f-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="6b39f-124">Откройте **UniversityModels.CS**и добавьте выделенный код в модель учащихся.</span><span class="sxs-lookup"><span data-stu-id="6b39f-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="6b39f-125">**Ранжеаттрибуте** включается для применения правил проверки для свойства.</span><span class="sxs-lookup"><span data-stu-id="6b39f-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="6b39f-126">В этом руководстве предполагается, что университет Contoso основан на 1 января 2013, а значит, что предыдущие даты регистрации недействительны.</span><span class="sxs-lookup"><span data-stu-id="6b39f-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="6b39f-127">В окне Управление пакетами добавьте миграцию, выполнив команду **Add-Migration адденроллментдате**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="6b39f-128">Обратите внимание, что код миграции добавляет новый столбец datetime в таблицу Student.</span><span class="sxs-lookup"><span data-stu-id="6b39f-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="6b39f-129">Чтобы сопоставить значение, указанное в Ранжеаттрибуте, добавьте значение по умолчанию для нового столбца, как показано в выделенном ниже коде.</span><span class="sxs-lookup"><span data-stu-id="6b39f-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="6b39f-130">Сохраните изменения в файле миграции.</span><span class="sxs-lookup"><span data-stu-id="6b39f-130">Save your change to the migration file.</span></span>

<span data-ttu-id="6b39f-131">Повторное заполнение данных не требуется.</span><span class="sxs-lookup"><span data-stu-id="6b39f-131">You do not need to seed the data again.</span></span> <span data-ttu-id="6b39f-132">Поэтому откройте **Configuration.CS** в папке Migrations и удалите или закомментируйте код в методе **SEED** .</span><span class="sxs-lookup"><span data-stu-id="6b39f-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="6b39f-133">Сохраните файл и закройте его.</span><span class="sxs-lookup"><span data-stu-id="6b39f-133">Save and close the file.</span></span>

<span data-ttu-id="6b39f-134">Теперь выполните команду **Update-Database**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="6b39f-135">Обратите внимание, что столбец теперь существует в базе данных, а все существующие записи имеют значение по умолчанию для Енроллментдате.</span><span class="sxs-lookup"><span data-stu-id="6b39f-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="6b39f-136">Добавление динамических элементов управления для даты регистрации</span><span class="sxs-lookup"><span data-stu-id="6b39f-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="6b39f-137">Теперь вы добавите элементы управления для отображения и изменения даты регистрации.</span><span class="sxs-lookup"><span data-stu-id="6b39f-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="6b39f-138">На этом этапе значение изменяется через текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="6b39f-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="6b39f-139">Далее в этом руководстве вы измените текстовое поле на мини-приложение DatePicker JQuery.</span><span class="sxs-lookup"><span data-stu-id="6b39f-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="6b39f-140">Во-первых, важно отметить, что вносить изменения в файл **аддстудент. aspx** не требуется.</span><span class="sxs-lookup"><span data-stu-id="6b39f-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="6b39f-141">Элемент управления DynamicControl автоматически выполнит визуализацию нового свойства.</span><span class="sxs-lookup"><span data-stu-id="6b39f-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="6b39f-142">Откройте **students. aspx**и добавьте следующий выделенный код.</span><span class="sxs-lookup"><span data-stu-id="6b39f-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="6b39f-143">Запустите приложение и обратите внимание, что значение даты регистрации можно задать, введя дату.</span><span class="sxs-lookup"><span data-stu-id="6b39f-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="6b39f-144">При добавлении нового учащегося:</span><span class="sxs-lookup"><span data-stu-id="6b39f-144">When adding a new student:</span></span>

![задать дату](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="6b39f-146">Или измените существующее значение:</span><span class="sxs-lookup"><span data-stu-id="6b39f-146">Or, editing an existing value:</span></span>

![изменить дату](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="6b39f-148">Ввод даты работает, но может не быть клиентом, который вы хотите предоставлять.</span><span class="sxs-lookup"><span data-stu-id="6b39f-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="6b39f-149">В следующем разделе вы включите выбор даты в календаре.</span><span class="sxs-lookup"><span data-stu-id="6b39f-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="6b39f-150">Установка пакета NuGet для работы с пользовательским интерфейсом JQuery</span><span class="sxs-lookup"><span data-stu-id="6b39f-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="6b39f-151">Пакет NuGet **пользовательского интерфейса сок** обеспечивает простую интеграцию мини-приложений пользовательского интерфейса jQuery в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="6b39f-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="6b39f-152">Чтобы использовать этот пакет, установите его через NuGet.</span><span class="sxs-lookup"><span data-stu-id="6b39f-152">To use this package, install it through NuGet.</span></span>

![Добавление пользовательского интерфейса сок](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="6b39f-154">Устанавливаемая версия пользовательского интерфейса сок может конфликтовать с версией JQuery в приложении.</span><span class="sxs-lookup"><span data-stu-id="6b39f-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="6b39f-155">Прежде чем продолжить работу с этим руководством, попробуйте запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="6b39f-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="6b39f-156">При возникновении ошибки JavaScript необходимо согласовать версию JQuery.</span><span class="sxs-lookup"><span data-stu-id="6b39f-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="6b39f-157">Вы можете добавить ожидаемую версию JQuery в папку Scripts (версия 1.8.2 во время написания этого руководства) или в site. master укажите путь к файлу JQuery.</span><span class="sxs-lookup"><span data-stu-id="6b39f-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="6b39f-158">Настройка шаблона даты и времени для включения мини-приложения DatePicker</span><span class="sxs-lookup"><span data-stu-id="6b39f-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="6b39f-159">Вы добавите мини-приложение DatePicker в шаблон динамических данных для редактирования значения DateTime.</span><span class="sxs-lookup"><span data-stu-id="6b39f-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="6b39f-160">Добавив мини-приложение в шаблон, оно автоматически отображается как в форме для добавления нового учащегося, так и в представлении сетки для редактирования учащихся.</span><span class="sxs-lookup"><span data-stu-id="6b39f-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="6b39f-161">Откройте **DateTime\_Edit. ascx**и добавьте следующий выделенный код.</span><span class="sxs-lookup"><span data-stu-id="6b39f-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="6b39f-162">В файле кода программной части будут заданы минимальные и максимальные даты для DatePicker.</span><span class="sxs-lookup"><span data-stu-id="6b39f-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="6b39f-163">Устанавливая эти значения, пользователи не смогут переходить к недопустимым датам.</span><span class="sxs-lookup"><span data-stu-id="6b39f-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="6b39f-164">Вы получите минимальное и максимальное значения из **ранжеаттрибуте** для свойства DateTime, если оно предоставлено.</span><span class="sxs-lookup"><span data-stu-id="6b39f-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="6b39f-165">Откройте **DateTime\_Edit.ascx.CS**и добавьте следующий выделенный код на страницу\_метод Load.</span><span class="sxs-lookup"><span data-stu-id="6b39f-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="6b39f-166">Запустите веб-приложение и перейдите на страницу Аддстудент.</span><span class="sxs-lookup"><span data-stu-id="6b39f-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="6b39f-167">Укажите значения для полей и обратите внимание, что при щелчке текстового поля для даты регистрации отображается календарь.</span><span class="sxs-lookup"><span data-stu-id="6b39f-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![Выбор даты](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="6b39f-169">Выберите дату и нажмите кнопку **Вставить**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="6b39f-170">Ранжеаттрибуте принудительно применяет проверку на сервере.</span><span class="sxs-lookup"><span data-stu-id="6b39f-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="6b39f-171">Установив свойство minDate для DatePicker, вы также примените проверку на клиенте.</span><span class="sxs-lookup"><span data-stu-id="6b39f-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="6b39f-172">Календарь не позволяет пользователю переходить к дате до значения minDate.</span><span class="sxs-lookup"><span data-stu-id="6b39f-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="6b39f-173">При редактировании записи в представлении сетки также отображается календарь.</span><span class="sxs-lookup"><span data-stu-id="6b39f-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![DatePicker в GridView](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="6b39f-175">Заключение</span><span class="sxs-lookup"><span data-stu-id="6b39f-175">Conclusion</span></span>

<span data-ttu-id="6b39f-176">В этом учебнике вы узнали, как внедрить мини-приложение JQuery в форму Web Forms, использующую привязку модели.</span><span class="sxs-lookup"><span data-stu-id="6b39f-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="6b39f-177">В следующем [руководстве](using-query-string-values-to-retrieve-data.md)для выбора данных будет использоваться значение строки запроса.</span><span class="sxs-lookup"><span data-stu-id="6b39f-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6b39f-178">[Назад](sorting-paging-and-filtering-data.md)
> [Вперед](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="6b39f-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
