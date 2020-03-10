---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: Использование Entity Framework 4,0 и элемента управления ObjectDataSource, часть 3. Сортировка и фильтрация | Документация Майкрософт
author: tdykstra
description: Эта серия руководств основана на веб-приложении университета Contoso, которое создается начало работы с руководством по Entity Framework 4,0. Он...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512718"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="e82b8-104">Использование Entity Framework 4,0 и элемента управления ObjectDataSource, часть 3. Сортировка и фильтрация</span><span class="sxs-lookup"><span data-stu-id="e82b8-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>

<span data-ttu-id="e82b8-105">от [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e82b8-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="e82b8-106">Эта серия руководств основана на веб-приложении университета Contoso, которое создается [Начало работы с руководством по Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) .</span><span class="sxs-lookup"><span data-stu-id="e82b8-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="e82b8-107">Если вы не выполнили предыдущие учебники, в качестве отправной точки для этого учебника вы можете скачать созданное [приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) .</span><span class="sxs-lookup"><span data-stu-id="e82b8-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="e82b8-108">Вы также можете [скачать приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , созданное с помощью полной серии руководств.</span><span class="sxs-lookup"><span data-stu-id="e82b8-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="e82b8-109">Если у вас есть вопросы о учебниках, их можно опубликовать на [форуме ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).</span><span class="sxs-lookup"><span data-stu-id="e82b8-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>

<span data-ttu-id="e82b8-110">В предыдущем руководстве вы реализовали шаблон репозитория в многоуровневом веб-приложении, которое использует Entity Framework и элемент управления `ObjectDataSource`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="e82b8-111">В этом учебнике показано, как выполнять сортировку и фильтрацию и обработку сценариев "основной/подробности".</span><span class="sxs-lookup"><span data-stu-id="e82b8-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="e82b8-112">Вы добавите следующие усовершенствования на страницу *Departments. aspx* :</span><span class="sxs-lookup"><span data-stu-id="e82b8-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="e82b8-113">Текстовое поле, позволяющее пользователям выбирать отделы по имени.</span><span class="sxs-lookup"><span data-stu-id="e82b8-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="e82b8-114">Список курсов для каждого отдела, показанного в сетке.</span><span class="sxs-lookup"><span data-stu-id="e82b8-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="e82b8-115">Возможность сортировки путем щелчка заголовков столбцов.</span><span class="sxs-lookup"><span data-stu-id="e82b8-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="e82b8-116">[![image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e82b8-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="e82b8-117">Добавление возможности сортировки столбцов GridView</span><span class="sxs-lookup"><span data-stu-id="e82b8-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="e82b8-118">Откройте страницу *departmentss. aspx* и добавьте атрибут `SortParameterName="sortExpression"` в элемент управления `ObjectDataSource` с именем `DepartmentsObjectDataSource`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="e82b8-119">(Позже вы создадите метод `GetDepartments`, который принимает параметр с именем `sortExpression`.) Разметка для открывающего тега элемента управления теперь напоминает следующий пример.</span><span class="sxs-lookup"><span data-stu-id="e82b8-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="e82b8-120">Добавьте атрибут `AllowSorting="true"` в открывающий тег элемента управления `GridView`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="e82b8-121">Разметка для открывающего тега элемента управления теперь напоминает следующий пример.</span><span class="sxs-lookup"><span data-stu-id="e82b8-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="e82b8-122">В *Departments.aspx.CS*задайте порядок сортировки по умолчанию, вызвав метод `Sort` `GridView` элемента управления из метода `Page_Load`:</span><span class="sxs-lookup"><span data-stu-id="e82b8-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="e82b8-123">Можно добавить код, который сортирует или фильтрует либо в классе бизнес-логики, либо в классе репозитория.</span><span class="sxs-lookup"><span data-stu-id="e82b8-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="e82b8-124">Если сделать это в классе бизнес-логики, работа по сортировке или фильтрации будет выполнена после извлечения данных из базы данных, так как класс бизнес-логики работает с объектом `IEnumerable`, возвращенным репозиторием.</span><span class="sxs-lookup"><span data-stu-id="e82b8-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="e82b8-125">Если добавить в класс репозитория код сортировки и фильтрации и сделать это до того, как выражение LINQ или запрос к объекту были преобразованы в `IEnumerable` объект, команды будут переданы в базу данных для обработки, что, как правило, более эффективно.</span><span class="sxs-lookup"><span data-stu-id="e82b8-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="e82b8-126">В этом учебнике вы реализуете сортировку и фильтрацию таким образом, чтобы обработка была выполнена базой данных, т. е. в репозитории.</span><span class="sxs-lookup"><span data-stu-id="e82b8-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="e82b8-127">Чтобы добавить возможность сортировки, необходимо добавить новый метод в интерфейс репозитория и классы репозитория, а также в класс бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="e82b8-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="e82b8-128">В файле *ISchoolRepository.CS* добавьте новый метод `GetDepartments`, который принимает `sortExpression` параметр, который будет использоваться для сортировки списка возвращаемых отделов:</span><span class="sxs-lookup"><span data-stu-id="e82b8-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="e82b8-129">В параметре `sortExpression` будет указан столбец для сортировки и направление сортировки.</span><span class="sxs-lookup"><span data-stu-id="e82b8-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="e82b8-130">Добавьте код для нового метода в файл *SchoolRepository.CS* :</span><span class="sxs-lookup"><span data-stu-id="e82b8-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="e82b8-131">Измените существующий метод `GetDepartments` без параметров, чтобы вызвать новый метод:</span><span class="sxs-lookup"><span data-stu-id="e82b8-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="e82b8-132">В тестовом проекте добавьте следующий новый метод в *MockSchoolRepository.CS*:</span><span class="sxs-lookup"><span data-stu-id="e82b8-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="e82b8-133">Если вы собираетесь создавать модульные тесты, зависящие от этого метода, возвращающего отсортированный список, необходимо отсортировать список перед его возвратом.</span><span class="sxs-lookup"><span data-stu-id="e82b8-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="e82b8-134">Вы не создадите такие тесты, как в этом руководстве, поэтому метод может просто возвратить Несортированный список отделов.</span><span class="sxs-lookup"><span data-stu-id="e82b8-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="e82b8-135">В файле *SchoolBL.CS* добавьте следующий новый метод в класс бизнес-логики:</span><span class="sxs-lookup"><span data-stu-id="e82b8-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="e82b8-136">Этот код передает параметр Sort методу репозитория.</span><span class="sxs-lookup"><span data-stu-id="e82b8-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="e82b8-137">Запустите страницу *departmentss. aspx* .</span><span class="sxs-lookup"><span data-stu-id="e82b8-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="e82b8-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e82b8-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="e82b8-139">Теперь можно щелкнуть заголовок любого столбца, чтобы выполнить сортировку по этому столбцу.</span><span class="sxs-lookup"><span data-stu-id="e82b8-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="e82b8-140">Если столбец уже отсортирован, щелчок заголовка меняет направление сортировки на противоположное.</span><span class="sxs-lookup"><span data-stu-id="e82b8-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="e82b8-141">Добавление поля поиска</span><span class="sxs-lookup"><span data-stu-id="e82b8-141">Adding a Search Box</span></span>

<span data-ttu-id="e82b8-142">В этом разделе вы добавите текстовое поле поиска, свяжете его с элементом управления `ObjectDataSource`, используя параметр элемента управления, и добавите метод в класс бизнес-логики для поддержки фильтрации.</span><span class="sxs-lookup"><span data-stu-id="e82b8-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="e82b8-143">Откройте страницу *departmentss. aspx* и добавьте следующую разметку между заголовком и первым элементом управления `ObjectDataSource`:</span><span class="sxs-lookup"><span data-stu-id="e82b8-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="e82b8-144">В элементе управления `ObjectDataSource` с именем `DepartmentsObjectDataSource`выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e82b8-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="e82b8-145">Добавьте элемент `SelectParameters` для параметра с именем `nameSearchString`, который получает значение, указанное в элементе управления `SearchTextBox`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="e82b8-146">Измените значение атрибута `SelectMethod` на `GetDepartmentsByName`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="e82b8-147">(Этот метод будет создан позже.)</span><span class="sxs-lookup"><span data-stu-id="e82b8-147">(You'll create this method later.)</span></span>

<span data-ttu-id="e82b8-148">Разметка для элемента управления `ObjectDataSource` теперь напоминает следующий пример:</span><span class="sxs-lookup"><span data-stu-id="e82b8-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="e82b8-149">В *ISchoolRepository.CS*добавьте метод `GetDepartmentsByName`, который принимает `sortExpression` и `nameSearchString` параметры:</span><span class="sxs-lookup"><span data-stu-id="e82b8-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="e82b8-150">В *SchoolRepository.CS*добавьте следующий новый метод:</span><span class="sxs-lookup"><span data-stu-id="e82b8-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="e82b8-151">Этот код использует метод `Where` для выбора элементов, содержащих строку поиска.</span><span class="sxs-lookup"><span data-stu-id="e82b8-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="e82b8-152">Если строка поиска пуста, будут выбраны все записи.</span><span class="sxs-lookup"><span data-stu-id="e82b8-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="e82b8-153">Обратите внимание, что при указании вызовов методов вместе в одном операторе (`Include`, затем `OrderBy`, а затем `Where`) метод `Where` должен всегда быть последним.</span><span class="sxs-lookup"><span data-stu-id="e82b8-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="e82b8-154">Измените существующий метод `GetDepartments`, который принимает параметр `sortExpression` для вызова нового метода:</span><span class="sxs-lookup"><span data-stu-id="e82b8-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="e82b8-155">В *MockSchoolRepository.CS* в тестовом проекте добавьте следующий новый метод:</span><span class="sxs-lookup"><span data-stu-id="e82b8-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="e82b8-156">В *SchoolBL.CS*добавьте следующий новый метод:</span><span class="sxs-lookup"><span data-stu-id="e82b8-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="e82b8-157">Запустите страницу *departmentss. aspx* и введите строку поиска, чтобы убедиться, что логика выбора работает.</span><span class="sxs-lookup"><span data-stu-id="e82b8-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="e82b8-158">Оставьте текстовое поле пустым и попробуйте выполнить поиск, чтобы убедиться, что все записи возвращены.</span><span class="sxs-lookup"><span data-stu-id="e82b8-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="e82b8-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e82b8-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="e82b8-160">Добавление столбца сведений для каждой строки сетки</span><span class="sxs-lookup"><span data-stu-id="e82b8-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="e82b8-161">Далее нужно просмотреть все курсы по каждому отделу, отображаемому в правой ячейке сетки.</span><span class="sxs-lookup"><span data-stu-id="e82b8-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="e82b8-162">Для этого используется вложенный элемент управления `GridView` и привязка его к данным из свойства навигации `Courses` сущности `Department`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="e82b8-163">Откройте *отделы. aspx* и в разметке для элемента управления `GridView` укажите обработчик для события `RowDataBound`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="e82b8-164">Разметка для открывающего тега элемента управления теперь напоминает следующий пример.</span><span class="sxs-lookup"><span data-stu-id="e82b8-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="e82b8-165">Добавьте новый элемент `TemplateField` после поля шаблона `Administrator`:</span><span class="sxs-lookup"><span data-stu-id="e82b8-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="e82b8-166">Эта разметка создает вложенный элемент управления `GridView`, который показывает номер курса и заголовок списка курсов.</span><span class="sxs-lookup"><span data-stu-id="e82b8-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="e82b8-167">Он не указывает источник данных, так как он будет привязку к нему в коде обработчика `RowDataBound`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="e82b8-168">Откройте *Departments.aspx.CS* и добавьте следующий обработчик для события `RowDataBound`:</span><span class="sxs-lookup"><span data-stu-id="e82b8-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="e82b8-169">Этот код получает `Department` сущность из аргументов события, преобразует `Courses` свойство навигации в коллекцию `List` и привязывает вложенные `GridView` к коллекции.</span><span class="sxs-lookup"><span data-stu-id="e82b8-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="e82b8-170">Откройте файл *SchoolRepository.CS* и укажите безотлагательную загрузку для свойства навигации `Courses`, вызвав метод `Include` в запросе объекта, созданном в методе `GetDepartmentsByName`.</span><span class="sxs-lookup"><span data-stu-id="e82b8-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="e82b8-171">Оператор `return` в методе `GetDepartmentsByName` теперь напоминает следующий пример.</span><span class="sxs-lookup"><span data-stu-id="e82b8-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="e82b8-172">Запустите страницу.</span><span class="sxs-lookup"><span data-stu-id="e82b8-172">Run the page.</span></span> <span data-ttu-id="e82b8-173">Помимо возможностей сортировки и фильтрации, добавленных ранее, в элементе управления GridView теперь отображаются вложенные сведения о курсе для каждого отдела.</span><span class="sxs-lookup"><span data-stu-id="e82b8-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="e82b8-174">[![image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="e82b8-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="e82b8-175">В результате вы закончите вводные сведения о сценариях сортировки, фильтрации и "основной/подробности".</span><span class="sxs-lookup"><span data-stu-id="e82b8-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="e82b8-176">В следующем руководстве вы узнаете, как работать с параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="e82b8-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e82b8-177">[Назад](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [Вперед](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="e82b8-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
