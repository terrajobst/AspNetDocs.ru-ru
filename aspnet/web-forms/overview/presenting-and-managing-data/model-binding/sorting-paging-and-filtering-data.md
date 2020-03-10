---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: Сортировка, разбиение на страницы и фильтрация данных с помощью привязки модели и веб-форм | Документация Майкрософт
author: Rick-Anderson
description: В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET. Привязка модели делает взаимодействие данных более прямым-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441066"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="8e7ad-104">Сортировка, разбиение на страницы и фильтрация данных с помощью привязки модели и веб-форм</span><span class="sxs-lookup"><span data-stu-id="8e7ad-104">Sorting, paging, and filtering data with model binding and web forms</span></span>

<span data-ttu-id="8e7ad-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8e7ad-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8e7ad-106">В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="8e7ad-107">Привязка модели делает взаимодействие данных более прямым, чем работа с объектами источника данных (например, ObjectDataSource или SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="8e7ad-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="8e7ad-108">Эта серия начинается с вводного материала и переходит к более сложным концепциям в последующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="8e7ad-109">В этом руководстве показано, как добавить сортировку, разбиение по страницам и фильтрацию данных с помощью привязки модели.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="8e7ad-110">Это руководство строится на проекте, созданном в первой [части](retrieving-data.md) серии.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="8e7ad-111">Вы можете [скачать](https://go.microsoft.com/fwlink/?LinkId=286116) полный проект в C# или VB.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="8e7ad-112">Загружаемый код работает как с Visual Studio 2012, так и с Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="8e7ad-113">В нем используется шаблон Visual Studio 2012, который немного отличается от шаблона Visual Studio 2013, показанного в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="8e7ad-114">Что будет построено</span><span class="sxs-lookup"><span data-stu-id="8e7ad-114">What you'll build</span></span>

<span data-ttu-id="8e7ad-115">В этом руководстве вы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="8e7ad-116">Включение сортировки и разбиения на страницы данных</span><span class="sxs-lookup"><span data-stu-id="8e7ad-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="8e7ad-117">Включить фильтрацию данных на основе выбора пользователем</span><span class="sxs-lookup"><span data-stu-id="8e7ad-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="8e7ad-118">Добавление сортировки</span><span class="sxs-lookup"><span data-stu-id="8e7ad-118">Add sorting</span></span>

<span data-ttu-id="8e7ad-119">Включить сортировку в GridView очень просто.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="8e7ad-120">В файле Student. aspx просто задайте для **GridView** **значение true** в элементе управления GridView.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="8e7ad-121">Не нужно задавать значение **SortExpression** для каждого столбца, так как поле данных используется автоматически.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="8e7ad-122">GridView изменяет запрос, чтобы включить упорядочивание данных по выбранному значению.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="8e7ad-123">В выделенном ниже коде показано добавление, которое необходимо сделать для включения сортировки.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="8e7ad-124">Запустите веб-приложение и протестируйте сортировку записей учащихся по значениям в разных столбцах.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![Сортировка учащихся](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="8e7ad-126">Добавление разбиения по страницам</span><span class="sxs-lookup"><span data-stu-id="8e7ad-126">Add paging</span></span>

<span data-ttu-id="8e7ad-127">Включить разбиение на страницы также очень просто.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="8e7ad-128">В элементе GridView задайте для свойства **AllowPaging** **значение true** и задайте для свойства **pageSize** количество записей, которые будут отображаться на каждой странице.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="8e7ad-129">В этом руководстве вы можете задать для него значение 4.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="8e7ad-130">Запустите веб-приложение и обратите внимание, что теперь записи делятся на несколько страниц, на одной странице не более 4 записей.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![Добавить подкачку](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="8e7ad-132">Отложенное выполнение запросов повышает эффективность работы приложения.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="8e7ad-133">Вместо получения всего набора данных GridView изменяет запрос, чтобы получить только записи для текущей страницы.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="8e7ad-134">Фильтрация записей по выбору пользователя</span><span class="sxs-lookup"><span data-stu-id="8e7ad-134">Filter records by user selection</span></span>

<span data-ttu-id="8e7ad-135">Привязка модели добавляет несколько атрибутов, которые позволяют определить, как задать значение параметра в методе привязки модели.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="8e7ad-136">Эти атрибуты находятся в пространстве имен **System. Web. моделбиндинг** .</span><span class="sxs-lookup"><span data-stu-id="8e7ad-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="8e7ad-137">в том числе:</span><span class="sxs-lookup"><span data-stu-id="8e7ad-137">They include:</span></span>

- <span data-ttu-id="8e7ad-138">Control</span><span class="sxs-lookup"><span data-stu-id="8e7ad-138">Control</span></span>
- <span data-ttu-id="8e7ad-139">Куки-файл</span><span class="sxs-lookup"><span data-stu-id="8e7ad-139">Cookie</span></span>
- <span data-ttu-id="8e7ad-140">Форма</span><span class="sxs-lookup"><span data-stu-id="8e7ad-140">Form</span></span>
- <span data-ttu-id="8e7ad-141">Профиль</span><span class="sxs-lookup"><span data-stu-id="8e7ad-141">Profile</span></span>
- <span data-ttu-id="8e7ad-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="8e7ad-142">QueryString</span></span>
- <span data-ttu-id="8e7ad-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="8e7ad-143">RouteData</span></span>
- <span data-ttu-id="8e7ad-144">Сеанс</span><span class="sxs-lookup"><span data-stu-id="8e7ad-144">Session</span></span>
- <span data-ttu-id="8e7ad-145">Филе</span><span class="sxs-lookup"><span data-stu-id="8e7ad-145">UserProfile</span></span>
- <span data-ttu-id="8e7ad-146">Состояние вида</span><span class="sxs-lookup"><span data-stu-id="8e7ad-146">ViewState</span></span>

<span data-ttu-id="8e7ad-147">В этом учебнике будет использоваться значение элемента управления для фильтрации записей, отображаемых в GridView.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="8e7ad-148">Атрибут **элемента управления** будет добавлен к созданному ранее методу запроса.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="8e7ad-149">В [следующем](using-query-string-values-to-retrieve-data.md) учебнике к параметру будет применен атрибут **QueryString** , чтобы указать, что значение параметра берется из значения строки запроса.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="8e7ad-150">Во-первых, над ValidationSummary добавьте раскрывающийся список для фильтрации отображаемых учащихся.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="8e7ad-151">В файле кода программной части измените метод Select, чтобы получить значение из элемента управления, и задайте в качестве имени параметра имя элемента управления, предоставляющего значение.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="8e7ad-152">Для разрешения атрибута элемента управления необходимо добавить инструкцию **using** для пространства имен **System. Web. моделбиндинг** .</span><span class="sxs-lookup"><span data-stu-id="8e7ad-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="8e7ad-153">В следующем коде показан метод Select, который можно изменить, чтобы отфильтровать возвращенные данные на основе значения раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="8e7ad-154">Добавление атрибута элемента управления перед параметром указывает, что значение этого параметра берется из элемента управления с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="8e7ad-155">Запустите веб-приложение и выберите другие значения из раскрывающегося списка, чтобы отфильтровать список учащихся.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![Фильтрация учащихся](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="8e7ad-157">Заключение</span><span class="sxs-lookup"><span data-stu-id="8e7ad-157">Conclusion</span></span>

<span data-ttu-id="8e7ad-158">В этом руководстве вы включили сортировку и разбиение данных на страницы.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="8e7ad-159">Вы также включили фильтрацию данных по значению элемента управления.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="8e7ad-160">В следующем [руководстве](integrating-jquery-ui.md) мы улучшаем пользовательский интерфейс, интегрируя мини-приложение пользовательского интерфейса jQuery в шаблон динамических данных.</span><span class="sxs-lookup"><span data-stu-id="8e7ad-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8e7ad-161">[Назад](updating-deleting-and-creating-data.md)
> [Вперед](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="8e7ad-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
