---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: Добавление уровня бизнес-логики в проект, использующий привязку модели и веб-формы | Документация Майкрософт
author: Rick-Anderson
description: В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET. Привязка модели делает взаимодействие данных более прямым-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515430"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="9febd-104">Добавление уровня бизнес-логики в проект, использующий привязку модели и веб-формы</span><span class="sxs-lookup"><span data-stu-id="9febd-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="9febd-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9febd-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9febd-106">В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9febd-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="9febd-107">Привязка модели делает взаимодействие данных более прямым, чем работа с объектами источника данных (например, ObjectDataSource или SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="9febd-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="9febd-108">Эта серия начинается с вводного материала и переходит к более сложным концепциям в последующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="9febd-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="9febd-109">В этом руководстве показано, как использовать привязку модели с уровнем бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="9febd-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="9febd-110">Вы настроите элемент Онкаллингдатамесодс, чтобы указать, что для вызова методов данных используется объект, отличный от текущей страницы.</span><span class="sxs-lookup"><span data-stu-id="9febd-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="9febd-111">Это руководство строится на проекте, созданном в [предыдущих](retrieving-data.md) частях серии.</span><span class="sxs-lookup"><span data-stu-id="9febd-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="9febd-112">Вы можете [скачать](https://go.microsoft.com/fwlink/?LinkId=286116) полный проект в C# или VB.</span><span class="sxs-lookup"><span data-stu-id="9febd-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="9febd-113">Загружаемый код работает как с Visual Studio 2012, так и с Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="9febd-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="9febd-114">В нем используется шаблон Visual Studio 2012, который немного отличается от шаблона Visual Studio 2013, показанного в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="9febd-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="9febd-115">Что будет построено</span><span class="sxs-lookup"><span data-stu-id="9febd-115">What you'll build</span></span>

<span data-ttu-id="9febd-116">Привязка модели позволяет разместить код взаимодействия данных в файле кода программной части для веб-страницы или в отдельном классе бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="9febd-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="9febd-117">В предыдущих руководствах было показано, как использовать файлы кода программной части для кода взаимодействия с данными.</span><span class="sxs-lookup"><span data-stu-id="9febd-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="9febd-118">Этот подход работает для небольших сайтов, но он может привести к повторению кода и большей сложности при обслуживании большого сайта.</span><span class="sxs-lookup"><span data-stu-id="9febd-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="9febd-119">Программный тест кода, который находится в файлах кода программной части, может быть очень трудным, поскольку уровень абстракции отсутствует.</span><span class="sxs-lookup"><span data-stu-id="9febd-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="9febd-120">Для централизации кода взаимодействия данных можно создать уровень бизнес-логики, который содержит всю логику взаимодействия с данными.</span><span class="sxs-lookup"><span data-stu-id="9febd-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="9febd-121">Затем вы вызываете уровень бизнес-логики с веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="9febd-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="9febd-122">В этом руководстве показано, как переместить весь код, записанный в предыдущих руководствах, в уровень бизнес-логики, а затем использовать этот код на страницах.</span><span class="sxs-lookup"><span data-stu-id="9febd-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="9febd-123">В этом руководстве вы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9febd-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="9febd-124">Перемещение кода из файлов кода программной части в слой бизнес-логики</span><span class="sxs-lookup"><span data-stu-id="9febd-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="9febd-125">Изменение элементов управления, привязанных к данным, для вызова методов на уровне бизнес-логики</span><span class="sxs-lookup"><span data-stu-id="9febd-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="9febd-126">Создание уровня бизнес-логики</span><span class="sxs-lookup"><span data-stu-id="9febd-126">Create business logic layer</span></span>

<span data-ttu-id="9febd-127">Теперь создадим класс, который вызывается из веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="9febd-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="9febd-128">Методы в этом классе похожи на методы, использованные в предыдущих руководствах, и включают атрибуты поставщика значений.</span><span class="sxs-lookup"><span data-stu-id="9febd-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="9febd-129">Сначала добавьте новую папку с именем **BLL**.</span><span class="sxs-lookup"><span data-stu-id="9febd-129">First, add a new folder called **BLL**.</span></span>

![Добавить папку](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="9febd-131">В папке BLL создайте новый класс с именем **SchoolBL.CS**.</span><span class="sxs-lookup"><span data-stu-id="9febd-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="9febd-132">Он будет содержать все операции с данными, которые изначально находились в файлах кода программной части.</span><span class="sxs-lookup"><span data-stu-id="9febd-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="9febd-133">Методы практически совпадают с методами в файле кода программной части, но содержат некоторые изменения.</span><span class="sxs-lookup"><span data-stu-id="9febd-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="9febd-134">Наиболее важное изменение, которое следует учесть, заключается в том, что вы больше не используете код из экземпляра класса **Page** .</span><span class="sxs-lookup"><span data-stu-id="9febd-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="9febd-135">Класс Page содержит метод **трюпдатемодел** и свойство **ModelState** .</span><span class="sxs-lookup"><span data-stu-id="9febd-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="9febd-136">При перемещении этого кода на уровень бизнес-логики у вас больше не будет экземпляра класса Page для вызова этих элементов.</span><span class="sxs-lookup"><span data-stu-id="9febd-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="9febd-137">Чтобы обойти эту ошибку, необходимо добавить параметр **моделмесодконтекст** в любой метод, обращающийся к Трюпдатемодел или ModelState.</span><span class="sxs-lookup"><span data-stu-id="9febd-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="9febd-138">Этот параметр Моделмесодконтекст используется для вызова Трюпдатемодел или получения ModelState.</span><span class="sxs-lookup"><span data-stu-id="9febd-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="9febd-139">Для этого нового параметра не нужно изменять содержимое веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="9febd-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="9febd-140">Замените код в SchoolBL.cs на следующий код.</span><span class="sxs-lookup"><span data-stu-id="9febd-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="9febd-141">Пересмотр существующих страниц для получения данных из уровня бизнес-логики</span><span class="sxs-lookup"><span data-stu-id="9febd-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="9febd-142">Наконец, будут преобразованы страницы students. aspx, Аддстудент. aspx и Courses. aspx из использования запросов в файле кода программной части для использования уровня бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="9febd-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="9febd-143">В файлах кода программной части для учащихся, Аддстудент и курсов удалите или закомментируйте следующие методы запроса:</span><span class="sxs-lookup"><span data-stu-id="9febd-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="9febd-144">Студентсгрид\_GetData</span><span class="sxs-lookup"><span data-stu-id="9febd-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="9febd-145">Студентсгрид\_Упдатеитем</span><span class="sxs-lookup"><span data-stu-id="9febd-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="9febd-146">Студентсгрид\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="9febd-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="9febd-147">Аддстудентформ\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="9febd-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="9febd-148">Каурсесгрид\_GetData</span><span class="sxs-lookup"><span data-stu-id="9febd-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="9febd-149">Теперь у вас не должно быть кода в файле кода программной части, который относится к операциям с данными.</span><span class="sxs-lookup"><span data-stu-id="9febd-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="9febd-150">Обработчик событий **онкаллингдатамесодс** позволяет указать объект, который будет использоваться для методов данных.</span><span class="sxs-lookup"><span data-stu-id="9febd-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="9febd-151">В файле students. aspx добавьте значение для этого обработчика событий и измените имена методов данных на имена методов в классе бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="9febd-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="9febd-152">В файле кода программной части для students. aspx определите обработчик событий для события Каллингдатамесодс.</span><span class="sxs-lookup"><span data-stu-id="9febd-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="9febd-153">В этом обработчике событий указывается класс бизнес-логики для операций с данными.</span><span class="sxs-lookup"><span data-stu-id="9febd-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="9febd-154">Внесите аналогичные изменения в Аддстудент. aspx.</span><span class="sxs-lookup"><span data-stu-id="9febd-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="9febd-155">В файле Courses. aspx Внесите аналогичные изменения.</span><span class="sxs-lookup"><span data-stu-id="9febd-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="9febd-156">Запустите приложение и обратите внимание, что все страницы работают так, как будто они были ранее.</span><span class="sxs-lookup"><span data-stu-id="9febd-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="9febd-157">Логика проверки также работает правильно.</span><span class="sxs-lookup"><span data-stu-id="9febd-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9febd-158">Заключение</span><span class="sxs-lookup"><span data-stu-id="9febd-158">Conclusion</span></span>

<span data-ttu-id="9febd-159">В этом руководстве вы переструктурированы приложение для использования уровня доступа к данным и уровня бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="9febd-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="9febd-160">Вы указали, что элементы управления данными используют объект, который не является текущей страницей для операций с данными.</span><span class="sxs-lookup"><span data-stu-id="9febd-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9febd-161">Назад</span><span class="sxs-lookup"><span data-stu-id="9febd-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
