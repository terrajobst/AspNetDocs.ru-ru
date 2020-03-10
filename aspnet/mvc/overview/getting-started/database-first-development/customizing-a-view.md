---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: Учебник. Настройка представления для EF Database First с помощью приложения ASP.NET MVC
description: В этом учебнике основное внимание уделяется изменению автоматически создаваемых представлений для улучшения презентации.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471522"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="e2d28-103">Учебник. Настройка представления для EF Database First с помощью приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e2d28-103">Tutorial: Customize view for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="e2d28-104">С помощью MVC, Entity Framework и шаблонов ASP.NET можно создать веб-приложение, которое предоставляет интерфейс для существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="e2d28-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="e2d28-105">В этой серии руководств показано, как автоматически создавать код, позволяющий пользователям отображать, изменять, создавать и удалять данные, находящиеся в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="e2d28-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="e2d28-106">Созданный код соответствует столбцам в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="e2d28-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="e2d28-107">В этом учебнике основное внимание уделяется изменению автоматически создаваемых представлений для улучшения презентации.</span><span class="sxs-lookup"><span data-stu-id="e2d28-107">This tutorial focuses on changing the automatically-generated views to enhance the presentation.</span></span>

<span data-ttu-id="e2d28-108">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="e2d28-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2d28-109">Добавление курсов на страницу сведений об учащихся</span><span class="sxs-lookup"><span data-stu-id="e2d28-109">Add courses to the student detail page</span></span>
> * <span data-ttu-id="e2d28-110">Убедитесь, что курсы добавлены на страницу</span><span class="sxs-lookup"><span data-stu-id="e2d28-110">Confirm that the courses are added to the page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2d28-111">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e2d28-111">Prerequisites</span></span>

* [<span data-ttu-id="e2d28-112">Изменение базы данных</span><span class="sxs-lookup"><span data-stu-id="e2d28-112">Change the database</span></span>](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a><span data-ttu-id="e2d28-113">Добавление курсов в сведения об учащихся</span><span class="sxs-lookup"><span data-stu-id="e2d28-113">Add courses to student detail</span></span>

<span data-ttu-id="e2d28-114">Созданный код обеспечивает хорошую отправную точку для приложения, но не обязательно предоставляет все функциональные возможности, необходимые в приложении.</span><span class="sxs-lookup"><span data-stu-id="e2d28-114">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="e2d28-115">Вы можете настроить код в соответствии с определенными требованиями приложения.</span><span class="sxs-lookup"><span data-stu-id="e2d28-115">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="e2d28-116">В настоящее время в приложении не отображаются зарегистрированные курсы для выбранного учащегося.</span><span class="sxs-lookup"><span data-stu-id="e2d28-116">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="e2d28-117">В этом разделе вы добавите зарегистрированные курсы для каждого учащегося в представление **сведений** для учащегося.</span><span class="sxs-lookup"><span data-stu-id="e2d28-117">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="e2d28-118">Откройте **views** > **students** > *Details. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e2d28-118">Open **Views** > **Students** > *Details.cshtml*.</span></span> <span data-ttu-id="e2d28-119">После последнего тега &lt;/дл&gt;, но перед закрывающим тегом &lt;/див&gt; добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="e2d28-119">Below the last &lt;/dl&gt; tag, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="e2d28-120">Этот код создает таблицу, которая отображает строку для каждой записи в таблице регистрации для выбранного учащегося.</span><span class="sxs-lookup"><span data-stu-id="e2d28-120">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="e2d28-121">Метод **отображения** отображает HTML для объекта (ModelItem), представляющего выражение.</span><span class="sxs-lookup"><span data-stu-id="e2d28-121">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="e2d28-122">Используйте метод дисплея (вместо простого встраивания значения свойства в код), чтобы убедиться, что значение имеет правильный формат в зависимости от типа и шаблона для этого типа.</span><span class="sxs-lookup"><span data-stu-id="e2d28-122">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="e2d28-123">В этом примере каждое выражение возвращает одно свойство из текущей записи в цикле, а значения — простые типы, которые подготавливаются к просмотру как текст.</span><span class="sxs-lookup"><span data-stu-id="e2d28-123">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

## <a name="confirm-courses-are-added"></a><span data-ttu-id="e2d28-124">Подтверждение добавления курсов</span><span class="sxs-lookup"><span data-stu-id="e2d28-124">Confirm courses are added</span></span>

<span data-ttu-id="e2d28-125">Запустите решение.</span><span class="sxs-lookup"><span data-stu-id="e2d28-125">Run the solution.</span></span> <span data-ttu-id="e2d28-126">Щелкните **список учащихся** и выберите **сведения** для одного из учащихся.</span><span class="sxs-lookup"><span data-stu-id="e2d28-126">Click **List of students** and select **Details** for one of the students.</span></span> <span data-ttu-id="e2d28-127">Вы увидите, что зарегистрированные курсы были добавлены в представление.</span><span class="sxs-lookup"><span data-stu-id="e2d28-127">You will see the enrolled courses have been included in the view.</span></span>

![учащийся с регистрацией](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a><span data-ttu-id="e2d28-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2d28-129">Next steps</span></span>
<span data-ttu-id="e2d28-130">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="e2d28-130">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2d28-131">Добавление курсов на страницу сведений об учащихся</span><span class="sxs-lookup"><span data-stu-id="e2d28-131">Added courses to the student detail page</span></span>
> * <span data-ttu-id="e2d28-132">Подтвердила, что курсы будут добавлены на страницу</span><span class="sxs-lookup"><span data-stu-id="e2d28-132">Confirmed that the courses are added to the page</span></span>

<span data-ttu-id="e2d28-133">Перейдите к следующему руководству, чтобы научиться добавлять заметки к данным для указания требований к проверке и форматирования отображения.</span><span class="sxs-lookup"><span data-stu-id="e2d28-133">Advance to the next tutorial to learn how to add data annotations to specify validation requirements and display formatting.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e2d28-134">Улучшение проверки данных</span><span class="sxs-lookup"><span data-stu-id="e2d28-134">Enhance data validation</span></span>](enhancing-data-validation.md)
