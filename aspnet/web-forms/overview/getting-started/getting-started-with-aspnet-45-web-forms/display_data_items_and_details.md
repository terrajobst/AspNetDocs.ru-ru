---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: Отображение элементов данных и сведений | Документация Майкрософт
author: Erikre
description: В этой серии руководств будут показаны основы создания приложения ASP.NET Web Forms с ASP.NET 4,7 и Microsoft Visual Studio 2017
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520812"
---
# <a name="display-data-items-and-details"></a><span data-ttu-id="3db6e-103">Отображение элементов данных и сведений</span><span class="sxs-lookup"><span data-stu-id="3db6e-103">Display data items and details</span></span>

<span data-ttu-id="3db6e-104">по [Эрик Реитан](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="3db6e-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="3db6e-105">В этой серии руководств вы узнаете об основах создания приложения ASP.NET Web Forms с ASP.NET 4,7 и Microsoft Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3db6e-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio 2017.</span></span>

<span data-ttu-id="3db6e-106">В этом руководстве вы узнаете, как отображать элементы данных и сведения об элементах данных с помощью веб-форм ASP.NET и Entity Framework Code First.</span><span class="sxs-lookup"><span data-stu-id="3db6e-106">In this tutorial, you'll learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="3db6e-107">Это руководство построено на предыдущем учебнике "Пользовательский интерфейс и Навигация" в рамках серии руководств по магазину Wingtip Toy.</span><span class="sxs-lookup"><span data-stu-id="3db6e-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="3db6e-108">По завершении работы с этим руководством вы увидите продукты на странице *продуктслист. aspx* и сведения о продукте на странице *продуктдетаилс. aspx* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-108">After completing this tutorial, you'll see products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page.</span></span>

## <a name="youll-learn-how-to"></a><span data-ttu-id="3db6e-109">Вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="3db6e-109">You'll learn how to:</span></span>

- <span data-ttu-id="3db6e-110">Добавление элемента управления данными для показа продуктов из базы данных</span><span class="sxs-lookup"><span data-stu-id="3db6e-110">Add a data control to display products from the database</span></span>
- <span data-ttu-id="3db6e-111">Подключение элемента управления данными к выбранным данным</span><span class="sxs-lookup"><span data-stu-id="3db6e-111">Connect a data control to the selected data</span></span>
- <span data-ttu-id="3db6e-112">Добавление элемента управления данными для вывода сведений о продукте из базы данных</span><span class="sxs-lookup"><span data-stu-id="3db6e-112">Add a data control to display product details from the database</span></span>
- <span data-ttu-id="3db6e-113">Получение значения из строки запроса и использование этого значения для ограничения данных, получаемых из базы данных</span><span class="sxs-lookup"><span data-stu-id="3db6e-113">Retrieve a value from the query string and use that value to limit the data that's retrieved from the database</span></span>

### <a name="features-introduced-in-this-tutorial"></a><span data-ttu-id="3db6e-114">Функции, представленные в этом руководстве:</span><span class="sxs-lookup"><span data-stu-id="3db6e-114">Features introduced in this tutorial:</span></span>

- <span data-ttu-id="3db6e-115">Привязка модели</span><span class="sxs-lookup"><span data-stu-id="3db6e-115">Model binding</span></span>
- <span data-ttu-id="3db6e-116">Поставщики значений</span><span class="sxs-lookup"><span data-stu-id="3db6e-116">Value providers</span></span>

## <a name="add-a-data-control"></a><span data-ttu-id="3db6e-117">Добавление элемента управления данными</span><span class="sxs-lookup"><span data-stu-id="3db6e-117">Add a data control</span></span>

<span data-ttu-id="3db6e-118">Для привязки данных к серверному элементу управления можно использовать несколько различных параметров.</span><span class="sxs-lookup"><span data-stu-id="3db6e-118">You can use a few different options to bind data to a server control.</span></span> <span data-ttu-id="3db6e-119">Наиболее распространенными являются:</span><span class="sxs-lookup"><span data-stu-id="3db6e-119">The most common include:</span></span>

* <span data-ttu-id="3db6e-120">Добавление элемента управления источником данных</span><span class="sxs-lookup"><span data-stu-id="3db6e-120">Adding a data source control</span></span>
* <span data-ttu-id="3db6e-121">Добавление кода вручную</span><span class="sxs-lookup"><span data-stu-id="3db6e-121">Adding code by hand</span></span>
* <span data-ttu-id="3db6e-122">Использование привязки модели</span><span class="sxs-lookup"><span data-stu-id="3db6e-122">Using model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="3db6e-123">Использование элемента управления источниками данных для привязки данных</span><span class="sxs-lookup"><span data-stu-id="3db6e-123">Use a data source control to bind data</span></span>

<span data-ttu-id="3db6e-124">Добавление элемента управления источниками данных позволяет связать элемент управления источником данных с элементом управления, который отображает данные.</span><span class="sxs-lookup"><span data-stu-id="3db6e-124">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="3db6e-125">При таком подходе можно декларативно, а не программно подключать серверные элементы управления к источникам данных.</span><span class="sxs-lookup"><span data-stu-id="3db6e-125">With this approach, you can declaratively,  rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="3db6e-126">Код вручную для привязки данных</span><span class="sxs-lookup"><span data-stu-id="3db6e-126">Code by hand to bind data</span></span>

<span data-ttu-id="3db6e-127">Написание кода вручную включает в себя:</span><span class="sxs-lookup"><span data-stu-id="3db6e-127">Coding by hand involves:</span></span>

1. <span data-ttu-id="3db6e-128">Считывание значения</span><span class="sxs-lookup"><span data-stu-id="3db6e-128">Reading a value</span></span>
2. <span data-ttu-id="3db6e-129">Проверка наличия значения NULL</span><span class="sxs-lookup"><span data-stu-id="3db6e-129">Checking if it's null</span></span>
3. <span data-ttu-id="3db6e-130">Преобразование в соответствующий тип</span><span class="sxs-lookup"><span data-stu-id="3db6e-130">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="3db6e-131">Проверка успешности преобразования</span><span class="sxs-lookup"><span data-stu-id="3db6e-131">Checking conversion success</span></span>
5. <span data-ttu-id="3db6e-132">Использование значения в запросе</span><span class="sxs-lookup"><span data-stu-id="3db6e-132">Using the value in the query</span></span> 

<span data-ttu-id="3db6e-133">Такой подход позволяет получить полный контроль над логикой доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="3db6e-133">This approach lets you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="3db6e-134">Использование привязки модели для привязки данных</span><span class="sxs-lookup"><span data-stu-id="3db6e-134">Use model binding to bind data</span></span>

<span data-ttu-id="3db6e-135">Привязка модели позволяет привязывать результаты с гораздо меньшим объемом кода и дает возможность повторно использовать функции во всем приложении.</span><span class="sxs-lookup"><span data-stu-id="3db6e-135">Model binding lets you bind results with far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="3db6e-136">Он упрощает работу с логикой доступа к данным, ориентированной на код, и по-прежнему предоставляет обширную платформу привязки данных.</span><span class="sxs-lookup"><span data-stu-id="3db6e-136">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="3db6e-137">Отображение продуктов</span><span class="sxs-lookup"><span data-stu-id="3db6e-137">Display products</span></span>

<span data-ttu-id="3db6e-138">В этом руководстве вы будете использовать привязку модели для привязки данных.</span><span class="sxs-lookup"><span data-stu-id="3db6e-138">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="3db6e-139">Чтобы настроить элемент управления данными для использования привязки модели для выбора данных, задайте для свойства `SelectMethod` элемента управления имя метода в коде страницы.</span><span class="sxs-lookup"><span data-stu-id="3db6e-139">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method name in the page's code.</span></span> <span data-ttu-id="3db6e-140">Элемент управления данными вызывает метод в соответствующее время в жизненном цикле страницы и автоматически привязывает возвращенные данные.</span><span class="sxs-lookup"><span data-stu-id="3db6e-140">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="3db6e-141">Нет необходимости в явном вызове метода `DataBind`.</span><span class="sxs-lookup"><span data-stu-id="3db6e-141">There's no need to explicitly call the `DataBind` method.</span></span>

1. <span data-ttu-id="3db6e-142">В **Обозреватель решений**откройте *ProductList. aspx*.</span><span class="sxs-lookup"><span data-stu-id="3db6e-142">In **Solution Explorer**, open *ProductList.aspx*.</span></span>
2. <span data-ttu-id="3db6e-143">Замените существующую разметку этой разметкой:</span><span class="sxs-lookup"><span data-stu-id="3db6e-143">Replace the existing markup with this markup:</span></span>   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="3db6e-144">Этот код использует элемент управления **ListView** с именем `productList` для вывода продуктов.</span><span class="sxs-lookup"><span data-stu-id="3db6e-144">This code uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="3db6e-145">С помощью шаблонов и стилей вы определяете, как элемент управления **ListView** отображает данные.</span><span class="sxs-lookup"><span data-stu-id="3db6e-145">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="3db6e-146">Это полезно для данных в любой повторяющейся структуре.</span><span class="sxs-lookup"><span data-stu-id="3db6e-146">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="3db6e-147">Несмотря на то, что этот пример **ListView** просто отображает данные базы данных, можно также без кода, позволяя пользователям изменять, вставлять и удалять данные, а также сортировать и отображать данные на странице.</span><span class="sxs-lookup"><span data-stu-id="3db6e-147">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="3db6e-148">Если задать свойство `ItemType` в элементе управления **ListView** , то выражение привязки данных `Item` доступно, а элемент управления становится строго типизированным.</span><span class="sxs-lookup"><span data-stu-id="3db6e-148">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="3db6e-149">Как упоминалось в предыдущем учебнике, можно выбрать сведения об объекте Item с помощью IntelliSense, например, указав `ProductName`:</span><span class="sxs-lookup"><span data-stu-id="3db6e-149">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![Отображение элементов данных и сведений — IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="3db6e-151">Вы также используете привязку модели для указания значения `SelectMethod`.</span><span class="sxs-lookup"><span data-stu-id="3db6e-151">You're also using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="3db6e-152">Это значение (`GetProducts`) соответствует методу, который добавляется в код программной части для показа продуктов на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="3db6e-152">This value (`GetProducts`) corresponds to the method you'll add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="3db6e-153">Добавление кода для показа продуктов</span><span class="sxs-lookup"><span data-stu-id="3db6e-153">Add code to display products</span></span>

<span data-ttu-id="3db6e-154">На этом шаге вы добавите код для заполнения элемента управления **ListView** данными продукта из базы данных.</span><span class="sxs-lookup"><span data-stu-id="3db6e-154">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="3db6e-155">Код поддерживает отображение всех продуктов и отдельных категорий продуктов.</span><span class="sxs-lookup"><span data-stu-id="3db6e-155">The code supports showing all products and  individual category products.</span></span>

1. <span data-ttu-id="3db6e-156">В **Обозреватель решений**щелкните правой кнопкой мыши *ProductList. aspx* и выберите **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="3db6e-156">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="3db6e-157">Замените существующий код в файле *ProductList.aspx.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3db6e-157">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="3db6e-158">В этом коде показан метод `GetProducts`, который `ItemType` свойство элемента управления **ListView** ссылается на страницу *ProductList. aspx* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-158">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in the *ProductList.aspx* page.</span></span> <span data-ttu-id="3db6e-159">Чтобы ограничить результаты определенной категорией базы данных, код задает `categoryId` значение из строки запроса, передаваемого на страницу *ProductList. aspx* при переходе на страницу *ProductList. aspx* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-159">To limit the results to a specific database category, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="3db6e-160">Класс `QueryStringAttribute` в пространстве имен `System.Web.ModelBinding` используется для получения значения переменной строки запроса `id`.</span><span class="sxs-lookup"><span data-stu-id="3db6e-160">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable `id`.</span></span> <span data-ttu-id="3db6e-161">Это инструктирует привязку модели, чтобы попытаться привязать значение из строки запроса к параметру `categoryId` во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="3db6e-161">This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="3db6e-162">Если допустимая Категория передается в виде строки запроса на страницу, результаты запроса ограничиваются теми продуктами в базе данных, которые соответствуют значению `categoryId`.</span><span class="sxs-lookup"><span data-stu-id="3db6e-162">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="3db6e-163">Например, если страница *продуктслист. aspx* имеет следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="3db6e-163">For instance, if the *ProductsList.aspx* page URL is this:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="3db6e-164">На странице отображаются только те продукты, в которых `categoryId` равно `1`.</span><span class="sxs-lookup"><span data-stu-id="3db6e-164">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="3db6e-165">Все продукты отображаются, если при вызове страницы *ProductList. aspx* не включена строка запроса.</span><span class="sxs-lookup"><span data-stu-id="3db6e-165">All products are displayed if no query string is included when the *ProductList.aspx* page is called.</span></span>

<span data-ttu-id="3db6e-166">Источники значений для этих методов называются *поставщиками значений* (например, *QueryString*), а атрибуты параметров, указывающие, какой поставщик значений следует использовать, называются *атрибутами поставщика значений* (например, `id`).</span><span class="sxs-lookup"><span data-stu-id="3db6e-166">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="3db6e-167">ASP.NET включает поставщики значений и соответствующие атрибуты для всех типовых источников вводимых пользователем данных в приложении веб-форм, таких как строка запроса, файлы cookie, значения форм, элементы управления, состояние представления, состояние сеанса и свойства профиля.</span><span class="sxs-lookup"><span data-stu-id="3db6e-167">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="3db6e-168">Кроме того, можно создавать пользовательские поставщики значений.</span><span class="sxs-lookup"><span data-stu-id="3db6e-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="3db6e-169">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="3db6e-169">Run the application</span></span>

<span data-ttu-id="3db6e-170">Запустите приложение, чтобы просмотреть все продукты или продукты категории.</span><span class="sxs-lookup"><span data-stu-id="3db6e-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="3db6e-171">Нажмите клавишу **F5** в Visual Studio, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="3db6e-171">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="3db6e-172">Откроется браузер и отобразится страница *Default. aspx* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="3db6e-173">Выберите **автомобили** в меню навигации категории продуктов.</span><span class="sxs-lookup"><span data-stu-id="3db6e-173">Select **Cars** from the product category navigation menu.</span></span>  
   <span data-ttu-id="3db6e-174">На странице *ProductList. aspx* отображаются только продукты категории **автомобилей** .</span><span class="sxs-lookup"><span data-stu-id="3db6e-174">The *ProductList.aspx* page displays showing only **Cars** category products.</span></span> <span data-ttu-id="3db6e-175">Далее в этом учебнике будут показаны сведения о продукте.</span><span class="sxs-lookup"><span data-stu-id="3db6e-175">Later in this tutorial, you'll display product details.</span></span>  

    ![Отображение элементов данных и сведений — автомобили](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="3db6e-177">В меню навигации вверху выберите **продукты** .</span><span class="sxs-lookup"><span data-stu-id="3db6e-177">Select **Products** from the navigation menu at the top.</span></span>  
   <span data-ttu-id="3db6e-178">Опять же, отобразится страница *ProductList. aspx* , но на этот раз отображается весь список продуктов.</span><span class="sxs-lookup"><span data-stu-id="3db6e-178">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![Отображение элементов данных и сведений — продукты](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="3db6e-180">Закройте браузер и вернитесь в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3db6e-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="3db6e-181">Добавление элемента управления данными для вывода сведений о продукте</span><span class="sxs-lookup"><span data-stu-id="3db6e-181">Add a data control to display product details</span></span>

<span data-ttu-id="3db6e-182">Далее предстоит изменить разметку на странице *продуктдетаилс. aspx* , добавленную в предыдущем руководстве, для просмотра конкретных сведений о продукте.</span><span class="sxs-lookup"><span data-stu-id="3db6e-182">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial to display specific product information.</span></span>

1. <span data-ttu-id="3db6e-183">В **Обозреватель решений**откройте *продуктдетаилс. aspx*.</span><span class="sxs-lookup"><span data-stu-id="3db6e-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="3db6e-184">Замените существующую разметку этой разметкой:</span><span class="sxs-lookup"><span data-stu-id="3db6e-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    <span data-ttu-id="3db6e-185">Этот код использует элемент управления **FormView** для вывода сведений о конкретном продукте.</span><span class="sxs-lookup"><span data-stu-id="3db6e-185">This code uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="3db6e-186">В этой разметке используются такие методы, как методы, используемые для вывода данных на странице *ProductList. aspx* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-186">This markup uses methods like the methods used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="3db6e-187">Элемент управления **FormView** используется для вывода одной записи за раз из источника данных.</span><span class="sxs-lookup"><span data-stu-id="3db6e-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="3db6e-188">При использовании элемента управления **FormView** создаются шаблоны для просмотра и редактирования значений, привязанных к данным.</span><span class="sxs-lookup"><span data-stu-id="3db6e-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="3db6e-189">Эти шаблоны содержат элементы управления, выражения привязки и форматирование, определяющие внешний вид и функциональность формы.</span><span class="sxs-lookup"><span data-stu-id="3db6e-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="3db6e-190">Для подключения предыдущей разметки к базе данных требуется дополнительный код.</span><span class="sxs-lookup"><span data-stu-id="3db6e-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="3db6e-191">В **Обозреватель решений**щелкните правой кнопкой мыши *продуктдетаилс. aspx* и выберите пункт **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="3db6e-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="3db6e-192">Отобразится файл *ProductDetails.aspx.CS* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="3db6e-193">Замените существующий код следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3db6e-193">Replace the existing code with this code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="3db6e-194">Этот код проверяет значение строки запроса "`productID`".</span><span class="sxs-lookup"><span data-stu-id="3db6e-194">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="3db6e-195">Если найдено допустимое значение строки запроса, отображается соответствующий продукт.</span><span class="sxs-lookup"><span data-stu-id="3db6e-195">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="3db6e-196">Если строка запроса не найдена или ее значение недопустимо, продукт не отображается.</span><span class="sxs-lookup"><span data-stu-id="3db6e-196">If the query-string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="3db6e-197">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="3db6e-197">Run the application</span></span>

<span data-ttu-id="3db6e-198">Теперь можно запустить приложение, чтобы увидеть отдельный продукт, отображаемый на основе идентификатора продукта.</span><span class="sxs-lookup"><span data-stu-id="3db6e-198">Now you can run the application to see an individual product displayed based on product ID.</span></span>

1. <span data-ttu-id="3db6e-199">Нажмите клавишу **F5** в Visual Studio, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="3db6e-199">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="3db6e-200">Откроется браузер и отобразится страница *Default. aspx* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-200">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="3db6e-201">Выберите **Боатс** в меню навигации по категории.</span><span class="sxs-lookup"><span data-stu-id="3db6e-201">Select **Boats** from the category navigation menu.</span></span>  
   <span data-ttu-id="3db6e-202">Отобразится страница *ProductList. aspx* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="3db6e-203">Выберите **бумагу** в списке продуктов.</span><span class="sxs-lookup"><span data-stu-id="3db6e-203">Select **Paper Boat** from the product list.</span></span>
   <span data-ttu-id="3db6e-204">Отобразится страница *продуктдетаилс. aspx* .</span><span class="sxs-lookup"><span data-stu-id="3db6e-204">The *ProductDetails.aspx* page is displayed.</span></span>

    ![Отображение элементов данных и сведений — продукты](display_data_items_and_details/_static/image4.png)
    
4. <span data-ttu-id="3db6e-206">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="3db6e-206">Close the browser.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3db6e-207">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3db6e-207">Additional resources</span></span>

[<span data-ttu-id="3db6e-208">Извлечение и отображение данных с помощью привязки модели и веб-форм</span><span class="sxs-lookup"><span data-stu-id="3db6e-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a><span data-ttu-id="3db6e-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3db6e-209">Next steps</span></span>

<span data-ttu-id="3db6e-210">В этом руководстве вы добавили разметку и код для просмотра продуктов и сведений о продукте.</span><span class="sxs-lookup"><span data-stu-id="3db6e-210">In this tutorial, you added markup and code to display products and product details.</span></span> <span data-ttu-id="3db6e-211">Вы узнали о строго типизированных элементах управления данными, привязке модели и поставщиках значений.</span><span class="sxs-lookup"><span data-stu-id="3db6e-211">You learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="3db6e-212">В следующем руководстве вы добавите корзину для покупок в пример приложения Wingtip Toys.</span><span class="sxs-lookup"><span data-stu-id="3db6e-212">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span> 

> [!div class="step-by-step"]
> <span data-ttu-id="3db6e-213">[Назад](ui_and_navigation.md)
> [Вперед](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="3db6e-213">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
