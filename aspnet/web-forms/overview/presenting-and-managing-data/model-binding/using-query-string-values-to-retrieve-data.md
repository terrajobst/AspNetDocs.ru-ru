---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: Использование строковых значений запроса для фильтрации данных с помощью привязки модели и веб-форм | Документация Майкрософт
author: Rick-Anderson
description: В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET. Привязка модели делает взаимодействие данных более прямым-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519084"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a><span data-ttu-id="b1605-104">Использование строковых значений запроса для фильтрации данных с помощью привязки модели и веб-форм</span><span class="sxs-lookup"><span data-stu-id="b1605-104">Using query string values to filter data with model binding and web forms</span></span>

<span data-ttu-id="b1605-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b1605-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b1605-106">В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b1605-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="b1605-107">Привязка модели делает взаимодействие данных более прямым, чем работа с объектами источника данных (например, ObjectDataSource или SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="b1605-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="b1605-108">Эта серия начинается с вводного материала и переходит к более сложным концепциям в последующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="b1605-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="b1605-109">В этом руководстве показано, как передать значение в строке запроса и использовать это значение для получения данных с помощью привязки модели.</span><span class="sxs-lookup"><span data-stu-id="b1605-109">This tutorial shows how to pass a value in the query string and use that value to retrieve data through model binding.</span></span>
> 
> <span data-ttu-id="b1605-110">Это руководство строится на проекте, созданном в [предыдущих](retrieving-data.md) частях серии.</span><span class="sxs-lookup"><span data-stu-id="b1605-110">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="b1605-111">Вы можете [скачать](https://go.microsoft.com/fwlink/?LinkId=286116) полный проект в C# или VB.</span><span class="sxs-lookup"><span data-stu-id="b1605-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="b1605-112">Загружаемый код работает как с Visual Studio 2012, так и с Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="b1605-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="b1605-113">В нем используется шаблон Visual Studio 2012, который немного отличается от шаблона Visual Studio 2013, показанного в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b1605-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="b1605-114">Что будет построено</span><span class="sxs-lookup"><span data-stu-id="b1605-114">What you'll build</span></span>

<span data-ttu-id="b1605-115">В этом руководстве вы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b1605-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="b1605-116">Добавление новой страницы для отображения зарегистрированных курсов для учащихся</span><span class="sxs-lookup"><span data-stu-id="b1605-116">Add a new page to show the enrolled courses for a student</span></span>
2. <span data-ttu-id="b1605-117">Получение зарегистрированных курсов для выбранного учащегося на основе значения в строке запроса</span><span class="sxs-lookup"><span data-stu-id="b1605-117">Retrieve the enrolled courses for the selected student based on a value in the query string</span></span>
3. <span data-ttu-id="b1605-118">Добавление гиперссылки со значением строки запроса из представления сетки на новую страницу</span><span class="sxs-lookup"><span data-stu-id="b1605-118">Add a hyperlink with a query string value from the grid view to the new page</span></span>

<span data-ttu-id="b1605-119">Действия, описанные в этом руководстве, практически похожи на те, что были в предыдущем [учебнике](sorting-paging-and-filtering-data.md) для фильтрации отображаемых учащихся на основе выбора пользователя в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="b1605-119">The steps in this tutorial are fairly similar to what you did in the earlier [tutorial](sorting-paging-and-filtering-data.md) to filter the displayed students based on the user selection in a drop down list.</span></span> <span data-ttu-id="b1605-120">В этом руководстве вы использовали атрибут **Control** в методе Select, чтобы указать, что значение параметра берется из элемента управления.</span><span class="sxs-lookup"><span data-stu-id="b1605-120">In that tutorial, you used the **Control** attribute in the select method to specify that the parameter value comes from a control.</span></span> <span data-ttu-id="b1605-121">В этом руководстве вы будете использовать атрибут **QueryString** в методе Select, чтобы указать, что значение параметра берется из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="b1605-121">In this tutorial, you'll use the **QueryString** attribute in the select method to specify that the parameter value comes from the query string.</span></span>

## <a name="add-new-page-for-displaying-a-students-courses"></a><span data-ttu-id="b1605-122">Добавление новой страницы для отображения курсов учащихся</span><span class="sxs-lookup"><span data-stu-id="b1605-122">Add new page for displaying a student's courses</span></span>

<span data-ttu-id="b1605-123">Добавьте новую веб-форму, использующую главную страницу site. master, и назовите страницы **Courses**.</span><span class="sxs-lookup"><span data-stu-id="b1605-123">Add a new web form that uses the Site.master master page, and name the page **Courses**.</span></span>

<span data-ttu-id="b1605-124">В файле **Courses. aspx** добавьте представление сетки для отображения курсов выбранного учащегося.</span><span class="sxs-lookup"><span data-stu-id="b1605-124">In the **Courses.aspx** file, add a grid view to display the courses for the selected student.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a><span data-ttu-id="b1605-125">Определение метода Select</span><span class="sxs-lookup"><span data-stu-id="b1605-125">Define the select method</span></span>

<span data-ttu-id="b1605-126">В **Courses.aspx.CS**вы добавите метод Select с именем, указанным в свойстве **SelectMethod** в представлении сетки.</span><span class="sxs-lookup"><span data-stu-id="b1605-126">In **Courses.aspx.cs**, you will add the select method with the name you specified in the grid view's **SelectMethod** property.</span></span> <span data-ttu-id="b1605-127">В этом методе вы определите запрос для получения курсов учащегося и укажите, что параметр поступает из значения строки запроса с тем же именем, что и у параметра.</span><span class="sxs-lookup"><span data-stu-id="b1605-127">In that method, you'll define the query for retrieving a student's courses, and specify that the parameter comes from a query string value with the same name as the parameter.</span></span>

<span data-ttu-id="b1605-128">Сначала необходимо добавить следующие операторы **using** .</span><span class="sxs-lookup"><span data-stu-id="b1605-128">First, you must add the following **using** statements.</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

<span data-ttu-id="b1605-129">Затем добавьте следующий код в Courses.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="b1605-129">Then, add the following code to Courses.aspx.cs:</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

<span data-ttu-id="b1605-130">Атрибут QueryString означает, что значение строки запроса с именем StudentID автоматически назначается параметру в этом методе.</span><span class="sxs-lookup"><span data-stu-id="b1605-130">The QueryString attribute means that a query string value named StudentID is automatically assigned to the parameter in this method.</span></span>

## <a name="add-hyperlink-with-query-string-value"></a><span data-ttu-id="b1605-131">Добавить гиперссылку со значением строки запроса</span><span class="sxs-lookup"><span data-stu-id="b1605-131">Add hyperlink with query string value</span></span>

<span data-ttu-id="b1605-132">В представлении сетки на учащихся. aspx Вы добавите поле гиперссылки, которое ссылается на новую страницу курсов.</span><span class="sxs-lookup"><span data-stu-id="b1605-132">In the grid view on Students.aspx, you will add a hyperlink field that links to your new Courses page.</span></span> <span data-ttu-id="b1605-133">Гиперссылка будет содержать значение строки запроса с идентификатором учащегося.</span><span class="sxs-lookup"><span data-stu-id="b1605-133">The hyperlink will include a query string value with the student's id.</span></span>

<span data-ttu-id="b1605-134">В файле students. aspx добавьте следующее поле в столбцы представления сетки непосредственно под полем для общего количества кредитов.</span><span class="sxs-lookup"><span data-stu-id="b1605-134">In Students.aspx, add the following field to the grid view columns just below the field for Total Credits.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

<span data-ttu-id="b1605-135">Запустите приложение и обратите внимание, что в представлении "Сетка" теперь есть ссылка "курсы".</span><span class="sxs-lookup"><span data-stu-id="b1605-135">Run the application and notice that the grid view now includes the Courses link.</span></span>

![Добавить гиперссылку](using-query-string-values-to-retrieve-data/_static/image1.png)

<span data-ttu-id="b1605-137">Щелкнув одну из ссылок, вы увидите зарегистрированные курсы учащегося.</span><span class="sxs-lookup"><span data-stu-id="b1605-137">When you click one of the links, you'll see that student's enrolled courses.</span></span>

![Отображение курсов](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="b1605-139">Заключение</span><span class="sxs-lookup"><span data-stu-id="b1605-139">Conclusion</span></span>

<span data-ttu-id="b1605-140">В этом руководстве вы добавили ссылку со значением строки запроса.</span><span class="sxs-lookup"><span data-stu-id="b1605-140">In this tutorial, you added a link with a query string value.</span></span> <span data-ttu-id="b1605-141">Вы использовали это значение строки запроса для значения параметра в методе Select.</span><span class="sxs-lookup"><span data-stu-id="b1605-141">You used that query string value for the parameter value in the select method.</span></span>

<span data-ttu-id="b1605-142">В следующем [руководстве](adding-business-logic-layer.md)мы перейдем код из файлов кода программной части в слой бизнес-логики и уровень доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="b1605-142">In the next [tutorial](adding-business-logic-layer.md), you will move the code from the code-behind files into a business logic layer and a data access layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b1605-143">[Назад](integrating-jquery-ui.md)
> [Вперед](adding-business-logic-layer.md)</span><span class="sxs-lookup"><span data-stu-id="b1605-143">[Previous](integrating-jquery-ui.md)
[Next](adding-business-logic-layer.md)</span></span>
