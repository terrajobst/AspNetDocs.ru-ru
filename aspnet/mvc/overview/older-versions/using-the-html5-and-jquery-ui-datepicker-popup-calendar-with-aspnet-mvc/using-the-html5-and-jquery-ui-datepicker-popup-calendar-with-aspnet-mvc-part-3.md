---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 3 | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в ASP.NET МВ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457899"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="3b2de-103">Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 3</span><span class="sxs-lookup"><span data-stu-id="3b2de-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>

<span data-ttu-id="3b2de-104">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3b2de-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="3b2de-105">В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в веб-приложении ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="3b2de-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="working-with-complex-types"></a><span data-ttu-id="3b2de-106">Работа со сложными типами</span><span class="sxs-lookup"><span data-stu-id="3b2de-106">Working with Complex Types</span></span>

<span data-ttu-id="3b2de-107">В этом разделе вы создадите класс Address и узнаете, как создать шаблон для его отображения.</span><span class="sxs-lookup"><span data-stu-id="3b2de-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="3b2de-108">В папке *Models* создайте новый файл класса с именем *Person.CS* , в котором будут размещены два типа: класс `Person` и класс `Address`.</span><span class="sxs-lookup"><span data-stu-id="3b2de-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="3b2de-109">Класс `Person` будет содержать свойство, которое имеет тип `Address`.</span><span class="sxs-lookup"><span data-stu-id="3b2de-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="3b2de-110">Тип `Address` является сложным типом, то есть не является одним из встроенных типов, таких как `int`, `string`или `double`.</span><span class="sxs-lookup"><span data-stu-id="3b2de-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="3b2de-111">Вместо этого у него есть несколько свойств.</span><span class="sxs-lookup"><span data-stu-id="3b2de-111">Instead, it has several properties.</span></span> <span data-ttu-id="3b2de-112">Код для новых классов выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3b2de-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="3b2de-113">В контроллере `Movie` добавьте следующее действие `PersonDetail`, чтобы отобразить экземпляр Person:</span><span class="sxs-lookup"><span data-stu-id="3b2de-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="3b2de-114">Затем добавьте следующий код в контроллер `Movie`, чтобы заполнить модель `Person` несколькими демонстрационными данными:</span><span class="sxs-lookup"><span data-stu-id="3b2de-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="3b2de-115">Откройте файл *виевс\мовиес\персондетаил.кштмл* и добавьте следующую разметку для представления `PersonDetail`.</span><span class="sxs-lookup"><span data-stu-id="3b2de-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="3b2de-116">Нажмите клавиши CTRL + F5, чтобы запустить приложение и выбрать *фильмы/персондетаил*.</span><span class="sxs-lookup"><span data-stu-id="3b2de-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="3b2de-117">Представление `PersonDetail` не содержит `Address` сложного типа, как видно на этом снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="3b2de-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="3b2de-118">(Адрес не отображается.)</span><span class="sxs-lookup"><span data-stu-id="3b2de-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="3b2de-119">Данные модели `Address` не отображаются, так как это сложный тип.</span><span class="sxs-lookup"><span data-stu-id="3b2de-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="3b2de-120">Чтобы отобразить сведения об адресе, снова откройте файл *виевс\мовиес\персондетаил.кштмл* и добавьте следующую разметку.</span><span class="sxs-lookup"><span data-stu-id="3b2de-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="3b2de-121">Полная разметка для представления `PersonDetail` Now выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3b2de-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="3b2de-122">Запустите приложение еще раз и отобразите представление `PersonDetail`.</span><span class="sxs-lookup"><span data-stu-id="3b2de-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="3b2de-123">Теперь отображаются сведения об адресе:</span><span class="sxs-lookup"><span data-stu-id="3b2de-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="3b2de-124">Создание шаблона для сложного типа</span><span class="sxs-lookup"><span data-stu-id="3b2de-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="3b2de-125">В этом разделе вы создадите шаблон, который будет использоваться для визуализации `Address` сложного типа.</span><span class="sxs-lookup"><span data-stu-id="3b2de-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="3b2de-126">При создании шаблона для типа `Address` ASP.NET MVC может автоматически использовать его для форматирования модели адресов в любом месте приложения.</span><span class="sxs-lookup"><span data-stu-id="3b2de-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="3b2de-127">Это позволяет управлять визуализацией типа `Address` только из одного места в приложении.</span><span class="sxs-lookup"><span data-stu-id="3b2de-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="3b2de-128">В папке *views\shared\displaytemplates.* создайте строго типизированное частичное представление с именем **Address**:</span><span class="sxs-lookup"><span data-stu-id="3b2de-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="3b2de-129">Нажмите кнопку **Добавить**, а затем откройте новый файл *виевс\шаред\дисплайтемплатес\аддресс.кштмл* .</span><span class="sxs-lookup"><span data-stu-id="3b2de-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="3b2de-130">Новое представление содержит следующую созданную разметку:</span><span class="sxs-lookup"><span data-stu-id="3b2de-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="3b2de-131">Запустите приложение и отобразите представление `PersonDetail`.</span><span class="sxs-lookup"><span data-stu-id="3b2de-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="3b2de-132">На этот раз только что созданный шаблон `Address` используется для вывода `Address` сложного типа, поэтому отображение выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3b2de-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="3b2de-133">Сводка. способы указания формата и шаблона представления модели</span><span class="sxs-lookup"><span data-stu-id="3b2de-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="3b2de-134">Вы видели, что можно указать формат или шаблон для свойства модели с помощью следующих подходов:</span><span class="sxs-lookup"><span data-stu-id="3b2de-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="3b2de-135">Применение атрибута `DisplayFormat` к свойству в модели.</span><span class="sxs-lookup"><span data-stu-id="3b2de-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="3b2de-136">Например, следующий код приводит к отображению даты без времени:</span><span class="sxs-lookup"><span data-stu-id="3b2de-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="3b2de-137">Применение атрибута [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) к свойству в модели и указание типа данных.</span><span class="sxs-lookup"><span data-stu-id="3b2de-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="3b2de-138">Например, следующий код приводит к отображению даты без времени.</span><span class="sxs-lookup"><span data-stu-id="3b2de-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="3b2de-139">Если приложение содержит шаблон *Date. cshtml* в папке *Views\shared\displaytemplates.* или папке *виевс\мовиес\дисплайтемплатес* , то этот шаблон будет использоваться для визуализации свойства `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="3b2de-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="3b2de-140">В противном случае встроенная система создания шаблонов ASP.NET отображает свойство как дату.</span><span class="sxs-lookup"><span data-stu-id="3b2de-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="3b2de-141">Создание шаблона вывода в папке *views\shared\displaytemplates.* или папке *виевс\мовиес\дисплайтемплатес* , имя которой соответствует типу данных, который необходимо отформатировать.</span><span class="sxs-lookup"><span data-stu-id="3b2de-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="3b2de-142">Например, вы видели, что *виевс\шаред\дисплайтемплатес\датетиме.кштмл* использовался для отображения `DateTime` свойств в модели без добавления атрибута в модель и без добавления разметки в представления.</span><span class="sxs-lookup"><span data-stu-id="3b2de-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="3b2de-143">Использование атрибута [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) в модели для указания шаблона для вывода свойства модели.</span><span class="sxs-lookup"><span data-stu-id="3b2de-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="3b2de-144">Явное добавление имени шаблона отображения в вызов [HTML. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) в представлении.</span><span class="sxs-lookup"><span data-stu-id="3b2de-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="3b2de-145">Используемый подход зависит от того, что необходимо сделать в приложении.</span><span class="sxs-lookup"><span data-stu-id="3b2de-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="3b2de-146">Нередко приходится смешивать эти подходы, чтобы получить именно тот тип форматирования, который вам нужен.</span><span class="sxs-lookup"><span data-stu-id="3b2de-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="3b2de-147">В следующем разделе вы будете переключать шестеренки на несколько компонентов и переходить от настройки отображения данных для настройки способа их введения.</span><span class="sxs-lookup"><span data-stu-id="3b2de-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="3b2de-148">Вы присоедините jQuery DatePicker к представлениям редактирования в приложении, чтобы предоставить изящен способ указания дат.</span><span class="sxs-lookup"><span data-stu-id="3b2de-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3b2de-149">[Назад](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [Вперед](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="3b2de-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
