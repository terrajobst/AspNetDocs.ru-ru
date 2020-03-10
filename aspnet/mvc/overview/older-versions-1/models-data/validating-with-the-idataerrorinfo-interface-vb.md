---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: Проверка с помощью интерфейса IDataErrorInfo (VB) | Документация Майкрософт
author: StephenWalther
description: Стивен Вальтер показывает, как отобразить пользовательские сообщения об ошибках проверки, реализовав интерфейс IDataErrorInfo в классе модели.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ff3adc5db8114dcca2c66d937e1706f0bac0d30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436302"
---
# <a name="validating-with-the-idataerrorinfo-interface-vb"></a><span data-ttu-id="2dbe7-103">Проверка с помощью интерфейса IDataErrorInfo (VB)</span><span class="sxs-lookup"><span data-stu-id="2dbe7-103">Validating with the IDataErrorInfo Interface (VB)</span></span>

<span data-ttu-id="2dbe7-104">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="2dbe7-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="2dbe7-105">Стивен Вальтер показывает, как отобразить пользовательские сообщения об ошибках проверки, реализовав интерфейс IDataErrorInfo в классе модели.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>

<span data-ttu-id="2dbe7-106">Цель этого учебника — объяснить один подход к выполнению проверки в приложении ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="2dbe7-107">Вы узнаете, как предотвратить отправку HTML-формы, не предоставляя значения для обязательных полей формы.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="2dbe7-108">В этом руководстве вы узнаете, как выполнить проверку с помощью интерфейса Иеррордатаинфо.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="2dbe7-109">Предположения</span><span class="sxs-lookup"><span data-stu-id="2dbe7-109">Assumptions</span></span>

<span data-ttu-id="2dbe7-110">В этом руководстве я буду использовать базу данных Мовиесдб и таблицу фильмов.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="2dbe7-111">Эта таблица имеет следующие столбцы.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-111">This table has the following columns:</span></span>

<a id="0.6_table01"></a>

| <span data-ttu-id="2dbe7-112">**Имя столбца**</span><span class="sxs-lookup"><span data-stu-id="2dbe7-112">**Column Name**</span></span> | <span data-ttu-id="2dbe7-113">**Тип данных**</span><span class="sxs-lookup"><span data-stu-id="2dbe7-113">**Data Type**</span></span> | <span data-ttu-id="2dbe7-114">**Разрешить значения NULL**</span><span class="sxs-lookup"><span data-stu-id="2dbe7-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2dbe7-115">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="2dbe7-115">Id</span></span> | <span data-ttu-id="2dbe7-116">Int</span><span class="sxs-lookup"><span data-stu-id="2dbe7-116">Int</span></span> | <span data-ttu-id="2dbe7-117">False</span><span class="sxs-lookup"><span data-stu-id="2dbe7-117">False</span></span> |
| <span data-ttu-id="2dbe7-118">Title</span><span class="sxs-lookup"><span data-stu-id="2dbe7-118">Title</span></span> | <span data-ttu-id="2dbe7-119">Nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="2dbe7-119">Nvarchar(100)</span></span> | <span data-ttu-id="2dbe7-120">False</span><span class="sxs-lookup"><span data-stu-id="2dbe7-120">False</span></span> |
| <span data-ttu-id="2dbe7-121">Директор</span><span class="sxs-lookup"><span data-stu-id="2dbe7-121">Director</span></span> | <span data-ttu-id="2dbe7-122">Nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="2dbe7-122">Nvarchar(100)</span></span> | <span data-ttu-id="2dbe7-123">False</span><span class="sxs-lookup"><span data-stu-id="2dbe7-123">False</span></span> |
| <span data-ttu-id="2dbe7-124">датерелеасед</span><span class="sxs-lookup"><span data-stu-id="2dbe7-124">DateReleased</span></span> | <span data-ttu-id="2dbe7-125">Дата и время</span><span class="sxs-lookup"><span data-stu-id="2dbe7-125">DateTime</span></span> | <span data-ttu-id="2dbe7-126">False</span><span class="sxs-lookup"><span data-stu-id="2dbe7-126">False</span></span> |

<span data-ttu-id="2dbe7-127">В этом руководстве я использую Microsoft Entity Framework для создания классов модели базы данных.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="2dbe7-128">Класс Movie, созданный Entity Framework, отображается на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>

<span data-ttu-id="2dbe7-129">[![сущности «Movie»](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2dbe7-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span></span>

<span data-ttu-id="2dbe7-130">**Рис. 01**. сущность "фильм" ([щелкните, чтобы просмотреть изображение с полным размером](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="2dbe7-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2dbe7-131">Дополнительные сведения об использовании Entity Framework для создания классов модели базы данных см. в разделе мой учебник, посвященный созданию классов моделей с Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>

## <a name="the-controller-class"></a><span data-ttu-id="2dbe7-132">Класс контроллера</span><span class="sxs-lookup"><span data-stu-id="2dbe7-132">The Controller Class</span></span>

<span data-ttu-id="2dbe7-133">Мы используем контроллер Home для вывода списка фильмов и создания новых фильмов.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="2dbe7-134">Код для этого класса содержится в листинге 1.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="2dbe7-135">**Листинг 1. Контроллерс\хомеконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="2dbe7-135">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

<span data-ttu-id="2dbe7-136">Класс контроллера Home в листинге 1 содержит два действия Create ().</span><span class="sxs-lookup"><span data-stu-id="2dbe7-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="2dbe7-137">Первое действие отображает HTML-форму для создания нового фильма.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="2dbe7-138">Второе действие Create () выполняет фактическую вставку нового фильма в базу данных.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="2dbe7-139">Второе действие Create () вызывается при отправке на сервер формы, отображаемой первым действием Create ().</span><span class="sxs-lookup"><span data-stu-id="2dbe7-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="2dbe7-140">Обратите внимание, что второе действие Create () содержит следующие строки кода:</span><span class="sxs-lookup"><span data-stu-id="2dbe7-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

<span data-ttu-id="2dbe7-141">Свойство IsValid возвращает значение false в случае ошибки проверки.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="2dbe7-142">В этом случае повторно отображается представление создания, содержащее HTML-форму для создания фильма.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="2dbe7-143">Создание разделяемого класса</span><span class="sxs-lookup"><span data-stu-id="2dbe7-143">Creating a Partial Class</span></span>

<span data-ttu-id="2dbe7-144">Класс Movie создается Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="2dbe7-145">Код для класса Movie можно увидеть, если развернуть файл Мовиесдбмодел. EDMX в окне обозреватель решений и открыть файл Мовиесдбмодел. Designer. vb в редакторе кода (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="2dbe7-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.vb file in the Code Editor (see Figure 2).</span></span>

<span data-ttu-id="2dbe7-146">[![кода для сущности «Movie»](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2dbe7-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span></span>

<span data-ttu-id="2dbe7-147">**Рис. 02**. код для сущности Movie ([щелкните, чтобы просмотреть изображение с полным размером](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="2dbe7-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span></span>

<span data-ttu-id="2dbe7-148">Класс Movie является разделяемым классом.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-148">The Movie class is a partial class.</span></span> <span data-ttu-id="2dbe7-149">Это означает, что мы можем добавить еще один разделяемый класс с тем же именем, чтобы расширить функциональные возможности класса Movie.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="2dbe7-150">Мы добавим логику проверки к новому разделяемому классу.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="2dbe7-151">Добавьте класс в листинге 2 в папку Models.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="2dbe7-152">**Листинг 2. Моделс\мовие.ВБ**</span><span class="sxs-lookup"><span data-stu-id="2dbe7-152">**Listing 2 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

<span data-ttu-id="2dbe7-153">Обратите внимание, что класс в листинге 2 содержит модификатор *partial* .</span><span class="sxs-lookup"><span data-stu-id="2dbe7-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="2dbe7-154">Все методы или свойства, добавляемые в этот класс, становятся частью класса Movie, созданного Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="2dbe7-155">Добавление меняющихся и неизменных разделяемых методов</span><span class="sxs-lookup"><span data-stu-id="2dbe7-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="2dbe7-156">Когда Entity Framework создает класс сущностей, Entity Framework автоматически добавляет разделяемые методы в класс.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="2dbe7-157">Entity Framework создает частичные и меняющиеся разделяемые методы, соответствующие каждому свойству класса.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="2dbe7-158">В случае класса Movie Entity Framework создает следующие методы:</span><span class="sxs-lookup"><span data-stu-id="2dbe7-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="2dbe7-159">онидчангинг</span><span class="sxs-lookup"><span data-stu-id="2dbe7-159">OnIdChanging</span></span>
- <span data-ttu-id="2dbe7-160">онидчанжед</span><span class="sxs-lookup"><span data-stu-id="2dbe7-160">OnIdChanged</span></span>
- <span data-ttu-id="2dbe7-161">онтитлечангинг</span><span class="sxs-lookup"><span data-stu-id="2dbe7-161">OnTitleChanging</span></span>
- <span data-ttu-id="2dbe7-162">онтитлечанжед</span><span class="sxs-lookup"><span data-stu-id="2dbe7-162">OnTitleChanged</span></span>
- <span data-ttu-id="2dbe7-163">ондиректорчангинг</span><span class="sxs-lookup"><span data-stu-id="2dbe7-163">OnDirectorChanging</span></span>
- <span data-ttu-id="2dbe7-164">ондиректорчанжед</span><span class="sxs-lookup"><span data-stu-id="2dbe7-164">OnDirectorChanged</span></span>
- <span data-ttu-id="2dbe7-165">ондатерелеаседчангинг</span><span class="sxs-lookup"><span data-stu-id="2dbe7-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="2dbe7-166">ондатерелеаседчанжед</span><span class="sxs-lookup"><span data-stu-id="2dbe7-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="2dbe7-167">Метод onchangingd вызывается прямо перед изменением соответствующего свойства.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="2dbe7-168">Переданный метод вызывается сразу после изменения свойства.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="2dbe7-169">Можно воспользоваться преимуществами этих разделяемых методов, чтобы добавить логику проверки к классу Movie.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="2dbe7-170">Класс фильмов Update в листинге 3 проверяет, назначены ли свойства Title и Director непустыми значениями.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2dbe7-171">Разделяемый метод — это метод, определенный в классе, который не требуется реализовывать.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="2dbe7-172">Если не реализовать разделяемый метод, компилятор удаляет сигнатуру метода и все вызовы метода, чтобы не было никаких затрат времени выполнения, связанных с разделяемым методом.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="2dbe7-173">В редакторе Visual Studio Code можно добавить разделяемый метод, введя ключевое слово *partial* , за которым следует пробел, чтобы просмотреть список разделяемых элементов для реализации.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>

<span data-ttu-id="2dbe7-174">**Листинг 3. Моделс\мовие.ВБ**</span><span class="sxs-lookup"><span data-stu-id="2dbe7-174">**Listing 3 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

<span data-ttu-id="2dbe7-175">Например, при попытке присвоить свойству Title пустую строку сообщение об ошибке будет назначено словарю с именем \_Errors.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="2dbe7-176">На этом этапе ничто не происходит при присвоении пустой строки свойству Title, и в поле Private \_Errors добавляется ошибка.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="2dbe7-177">Нам нужно реализовать интерфейс IDataErrorInfo, чтобы предоставить эти ошибки проверки платформе ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="2dbe7-178">Реализация интерфейса IDataErrorInfo</span><span class="sxs-lookup"><span data-stu-id="2dbe7-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="2dbe7-179">С момента первой версии интерфейс IDataErrorInfo был частью платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="2dbe7-180">Этот интерфейс является очень простым интерфейсом:</span><span class="sxs-lookup"><span data-stu-id="2dbe7-180">This interface is a very simple interface:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

<span data-ttu-id="2dbe7-181">Если класс реализует интерфейс IDataErrorInfo, платформа ASP.NET MVC будет использовать этот интерфейс при создании экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="2dbe7-182">Например, действие "создать" контроллера Home () принимает экземпляр класса Movie:</span><span class="sxs-lookup"><span data-stu-id="2dbe7-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

<span data-ttu-id="2dbe7-183">Платформа ASP.NET MVC создает экземпляр фильма, переданный в действие Create () с помощью связывателя модели (DefaultModelBinder).</span><span class="sxs-lookup"><span data-stu-id="2dbe7-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="2dbe7-184">Связыватель модели отвечает за создание экземпляра объекта Movie путем привязки полей HTML-формы к экземпляру объекта Movie.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="2dbe7-185">DefaultModelBinder определяет, реализует ли класс интерфейс IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="2dbe7-186">Если класс реализует этот интерфейс, связыватель модели вызывает IDataErrorInfo. Этот индексатор для каждого свойства класса.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="2dbe7-187">Если индексатор возвращает сообщение об ошибке, связыватель модели добавляет это сообщение об ошибке в состояние модели автоматически.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="2dbe7-188">DefaultModelBinder также проверяет свойство IDataErrorInfo. Error.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="2dbe7-189">Это свойство предназначено для представления ошибок проверки, относящихся к конкретному свойству, связанных с классом.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="2dbe7-190">Например, может потребоваться применить правило проверки, которое зависит от значений нескольких свойств класса Movie.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="2dbe7-191">В этом случае вы вернете ошибку проверки из свойства Error.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="2dbe7-192">Обновленный класс Movie в листинге 4 реализует интерфейс IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="2dbe7-193">**Листинг 4 — Моделс\мовие.ВБ (реализация IDataErrorInfo)**</span><span class="sxs-lookup"><span data-stu-id="2dbe7-193">**Listing 4 - Models\Movie.vb (implements IDataErrorInfo)**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

<span data-ttu-id="2dbe7-194">В листинге 4 свойство индексатора проверяет коллекцию ошибок \_, чтобы проверить, содержит ли он ключ, соответствующий имени свойства, переданного индексатору.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="2dbe7-195">Если нет ошибки проверки, связанной со свойством, возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="2dbe7-196">Вам не нужно изменять контроллер Home любым способом использования измененного класса Movie.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="2dbe7-197">Страница, показанная на рис. 3, показывает, что происходит, если не введено значение для полей формы Title или Director.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>

<span data-ttu-id="2dbe7-198">[![автоматическое создание методов действий](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2dbe7-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span></span>

<span data-ttu-id="2dbe7-199">**Рис. 03**. форма с отсутствующими значениями ([щелкните, чтобы просмотреть изображение с полным размером](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2dbe7-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span></span>

<span data-ttu-id="2dbe7-200">Обратите внимание, что значение Датерелеасед проверяется автоматически.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="2dbe7-201">Поскольку свойство Датерелеасед не принимает значения NULL, DefaultModelBinder автоматически создает ошибку проверки для этого свойства, если у него нет значения.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="2dbe7-202">Если необходимо изменить сообщение об ошибке для свойства Датерелеасед, необходимо создать пользовательский связыватель модели.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="2dbe7-203">Сводка</span><span class="sxs-lookup"><span data-stu-id="2dbe7-203">Summary</span></span>

<span data-ttu-id="2dbe7-204">В этом руководстве вы узнали, как использовать интерфейс IDataErrorInfo для создания сообщений об ошибках проверки.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="2dbe7-205">Во-первых, мы создали частичный класс Movie, расширяющий функциональные возможности частичного класса Movie, созданного Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="2dbe7-206">Далее мы добавили логику проверки к разделяемым методам класса Movie Онтитлечангинг () и Ондиректорчангинг ().</span><span class="sxs-lookup"><span data-stu-id="2dbe7-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="2dbe7-207">Наконец, мы реализовали интерфейс IDataErrorInfo, чтобы предоставить эти сообщения проверки платформе ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2dbe7-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2dbe7-208">[Назад](performing-simple-validation-vb.md)
> [Вперед](validating-with-a-service-layer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2dbe7-208">[Previous](performing-simple-validation-vb.md)
[Next](validating-with-a-service-layer-vb.md)</span></span>
