---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: Часть 7. Добавление компонентов | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В часть 7 добавлены дополнительные функции, такие как учетная запись ревие...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521568"
---
# <a name="part-7-adding-features"></a><span data-ttu-id="21c97-104">Часть 7. Добавление функций</span><span class="sxs-lookup"><span data-stu-id="21c97-104">Part 7: Adding Features</span></span>

<span data-ttu-id="21c97-105">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="21c97-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="21c97-106">В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET.</span><span class="sxs-lookup"><span data-stu-id="21c97-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="21c97-107">Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.</span><span class="sxs-lookup"><span data-stu-id="21c97-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="21c97-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="21c97-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="21c97-109">В часть 7 добавлены дополнительные функции, такие как проверка учетной записи, проверка продукта, а также "Популярные элементы" и "купленные" пользовательские элементы управления.</span><span class="sxs-lookup"><span data-stu-id="21c97-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>

## <a id="_Toc260221673"></a><span data-ttu-id="21c97-110">Добавление компонентов</span><span class="sxs-lookup"><span data-stu-id="21c97-110">Adding Features</span></span>

<span data-ttu-id="21c97-111">Хотя пользователи могут просматривать наш каталог, размещать товары в своей корзине для покупок и завершать процесс извлечения, существует ряд вспомогательных функций, которые мы будем улучшать для улучшения нашего сайта.</span><span class="sxs-lookup"><span data-stu-id="21c97-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="21c97-112">Проверка учетной записи (список размещенных заказов и Просмотр сведений).</span><span class="sxs-lookup"><span data-stu-id="21c97-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="21c97-113">Добавьте содержимое определенного контекста на переднюю страницу.</span><span class="sxs-lookup"><span data-stu-id="21c97-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="21c97-114">Добавьте функцию, чтобы позволить пользователям просматривать продукты в каталоге.</span><span class="sxs-lookup"><span data-stu-id="21c97-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="21c97-115">Создайте пользовательский элемент управления для показа популярных элементов и поместите этот элемент управления на переднюю страницу.</span><span class="sxs-lookup"><span data-stu-id="21c97-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="21c97-116">Создайте "также купленный" пользовательский элемент управления и добавьте его на страницу сведений о продукте.</span><span class="sxs-lookup"><span data-stu-id="21c97-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="21c97-117">Добавление страницы контактов.</span><span class="sxs-lookup"><span data-stu-id="21c97-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="21c97-118">Добавление страницы About.</span><span class="sxs-lookup"><span data-stu-id="21c97-118">Add an About Page.</span></span>
8. <span data-ttu-id="21c97-119">Глобальная ошибка</span><span class="sxs-lookup"><span data-stu-id="21c97-119">Global Error</span></span>

## <a id="_Toc260221674"></a><span data-ttu-id="21c97-120">Проверка учетной записи</span><span class="sxs-lookup"><span data-stu-id="21c97-120">Account Review</span></span>

<span data-ttu-id="21c97-121">В папке Account создайте две страницы ASPX с именем OrderList. aspx и другой с именем OrderDetails. aspx.</span><span class="sxs-lookup"><span data-stu-id="21c97-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="21c97-122">OrderList. aspx будет использовать элементы управления GridView и EntityDataSource почти так, как мы ранее.</span><span class="sxs-lookup"><span data-stu-id="21c97-122">OrderList.aspx will leverage the GridView and EntityDataSource controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="21c97-123">EntityDataSource выбирает записи из таблицы Orders, отфильтрованные по имени пользователя (см. Вхерепараметер), которые задаются в переменной сеанса при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="21c97-123">The EntityDataSource selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="21c97-124">Обратите внимание также на эти параметры в HyperlinkField элемента управления GridView:</span><span class="sxs-lookup"><span data-stu-id="21c97-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="21c97-125">Они указывают ссылку на представление "сведения о заказе" для каждого продукта, указав поле OrderID в качестве параметра QueryString на странице OrderDetails. aspx.</span><span class="sxs-lookup"><span data-stu-id="21c97-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a><span data-ttu-id="21c97-126">OrderDetails. aspx</span><span class="sxs-lookup"><span data-stu-id="21c97-126">OrderDetails.aspx</span></span>

<span data-ttu-id="21c97-127">Мы будем использовать элемент управления EntityDataSource для доступа к заказам и FormView для вывода данных заказа и другого элемента управления EntityDataSource с элементом управления GridView для вывода всех элементов строк заказа.</span><span class="sxs-lookup"><span data-stu-id="21c97-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="21c97-128">В файле кода программной части (OrderDetails.aspx.cs) у нас есть два маленьких бита обслуживания.</span><span class="sxs-lookup"><span data-stu-id="21c97-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="21c97-129">Сначала необходимо убедиться, что OrderDetails всегда получает значение OrderId.</span><span class="sxs-lookup"><span data-stu-id="21c97-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="21c97-130">Также необходимо вычислить и отобразить итоги заказа из элементов строки.</span><span class="sxs-lookup"><span data-stu-id="21c97-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a><span data-ttu-id="21c97-131">Домашняя страница</span><span class="sxs-lookup"><span data-stu-id="21c97-131">The Home Page</span></span>

<span data-ttu-id="21c97-132">Давайте добавим статическое содержимое на страницу Default. aspx.</span><span class="sxs-lookup"><span data-stu-id="21c97-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="21c97-133">Сначала я создам папку «Content» (содержимое), а в ней — папку Images (и в нее будет включен образ, который будет использоваться на домашней странице).</span><span class="sxs-lookup"><span data-stu-id="21c97-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="21c97-134">В нижний заполнитель страницы Default. aspx добавьте следующую разметку.</span><span class="sxs-lookup"><span data-stu-id="21c97-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a><span data-ttu-id="21c97-135">Обзоры продуктов</span><span class="sxs-lookup"><span data-stu-id="21c97-135">Product Reviews</span></span>

<span data-ttu-id="21c97-136">Сначала мы добавим кнопку со ссылкой на форму, которую можно использовать для ввода проверки продукта.</span><span class="sxs-lookup"><span data-stu-id="21c97-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="21c97-137">Обратите внимание, что код ProductID передается в строку запроса.</span><span class="sxs-lookup"><span data-stu-id="21c97-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="21c97-138">Далее давайте добавим страницу с именем Ревиевадд. aspx.</span><span class="sxs-lookup"><span data-stu-id="21c97-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="21c97-139">На этой странице будет использоваться набор средств управления AJAX ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="21c97-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="21c97-140">Если вы еще не сделали этого, скачайте его из [Подписка DevExpress](http://devexpress.com/act) и получите рекомендации по настройке набора средств для использования с Visual Studio здесь [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span><span class="sxs-lookup"><span data-stu-id="21c97-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="21c97-141">В режиме конструктора перетащите элементы управления и средства проверки из панели элементов и создайте форму, подобную приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="21c97-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="21c97-142">Разметка будет выглядеть примерно так.</span><span class="sxs-lookup"><span data-stu-id="21c97-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="21c97-143">Теперь, когда мы можем ввести рецензии, можно отобразить эти проверки на странице продукта.</span><span class="sxs-lookup"><span data-stu-id="21c97-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="21c97-144">Добавьте эту разметку на страницу Продуктдетаилс. aspx.</span><span class="sxs-lookup"><span data-stu-id="21c97-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="21c97-145">Запустив наше приложение сейчас и перейдя к продукту, вы увидите сведения о продукте, включая отзывы клиентов.</span><span class="sxs-lookup"><span data-stu-id="21c97-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a><span data-ttu-id="21c97-146">Элемент управления популярными элементами (создание пользовательских элементов управления)</span><span class="sxs-lookup"><span data-stu-id="21c97-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="21c97-147">Чтобы увеличить объем продаж на веб-сайте, мы добавим несколько функций для «предполагающее определенную продать» популярных или связанных продуктов.</span><span class="sxs-lookup"><span data-stu-id="21c97-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="21c97-148">Первая из этих функций будет представлять собой список наиболее популярных продуктов в нашем каталоге продуктов.</span><span class="sxs-lookup"><span data-stu-id="21c97-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="21c97-149">Мы создадим «пользовательский элемент управления» для показа лучших элементов, которые будут продаваться на домашней странице нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="21c97-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="21c97-150">Так как это будет элемент управления, мы можем использовать его на любой странице, просто перетащив элемент управления в конструкторе Visual Studio на любую страницу, которая нам нравится.</span><span class="sxs-lookup"><span data-stu-id="21c97-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="21c97-151">В обозревателе решений Visual Studio щелкните правой кнопкой мыши имя решения и создайте новый каталог с именем Controls.</span><span class="sxs-lookup"><span data-stu-id="21c97-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="21c97-152">Хотя это необязательно, мы сможем обеспечить упорядочение нашего проекта, создавая все пользовательские элементы управления в каталоге "Controls".</span><span class="sxs-lookup"><span data-stu-id="21c97-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="21c97-153">Щелкните правой кнопкой мыши папку Controls и выберите пункт "создать элемент":</span><span class="sxs-lookup"><span data-stu-id="21c97-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="21c97-154">Укажите имя для элемента управления "Популаритемс".</span><span class="sxs-lookup"><span data-stu-id="21c97-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="21c97-155">Обратите внимание, что расширение файла для пользовательских элементов управления — ASCX, а не aspx.</span><span class="sxs-lookup"><span data-stu-id="21c97-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="21c97-156">Пользовательский элемент управления популярными элементами будет определен следующим образом.</span><span class="sxs-lookup"><span data-stu-id="21c97-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="21c97-157">Здесь мы используем метод, который мы еще не использовали в этом приложении.</span><span class="sxs-lookup"><span data-stu-id="21c97-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="21c97-158">Мы используем элемент управления Repeater и вместо использования элемента управления источниками данных привязка элемента управления Repeater к результатам запроса LINQ to Entities.</span><span class="sxs-lookup"><span data-stu-id="21c97-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="21c97-159">В коде программной части нашего элемента управления мы делаем это следующим образом.</span><span class="sxs-lookup"><span data-stu-id="21c97-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="21c97-160">Обратите внимание также на эту важную строку в верхней части разметки элемента управления.</span><span class="sxs-lookup"><span data-stu-id="21c97-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="21c97-161">Так как самые популярные элементы не изменяются в течение минуты, мы можем добавить директиву Ачинг для повышения производительности нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="21c97-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="21c97-162">Эта директива приведет к тому, что код элементов управления будет выполняться только при истечении срока действия кэшированного вывода элемента управления.</span><span class="sxs-lookup"><span data-stu-id="21c97-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="21c97-163">В противном случае будет использоваться кэшированная версия выходных данных элемента управления.</span><span class="sxs-lookup"><span data-stu-id="21c97-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="21c97-164">Теперь все, что нам нужно сделать, — это добавить наш новый элемент управления на странице Default. aspx.</span><span class="sxs-lookup"><span data-stu-id="21c97-164">Now all we have to do is include our new control in our Default.aspx page.</span></span>

<span data-ttu-id="21c97-165">Используйте перетаскивание, чтобы поместить экземпляр элемента управления в столбец Open формы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="21c97-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="21c97-166">Теперь при запуске нашего приложения на домашней странице отображаются наиболее популярные элементы.</span><span class="sxs-lookup"><span data-stu-id="21c97-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a><span data-ttu-id="21c97-167">"Также купленный" элемент управления (пользовательские элементы управления с параметрами)</span><span class="sxs-lookup"><span data-stu-id="21c97-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="21c97-168">Второй пользовательский элемент управления, который мы создадим, будет принимать предполагающее определенную на следующий уровень, добавляя для него особенности контекста.</span><span class="sxs-lookup"><span data-stu-id="21c97-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="21c97-169">Логика вычисления верхних и купленных элементов не является тривиальной.</span><span class="sxs-lookup"><span data-stu-id="21c97-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="21c97-170">Наш «купленный» элемент управления выберет записи OrderDetails (ранее приобретенные) для текущего выбранного ProductID и захватите элементы OrderID для каждого найденного уникального заказа.</span><span class="sxs-lookup"><span data-stu-id="21c97-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="21c97-171">Затем мы выберем пункт Al продуктов из всех заказов и вычислите количество приобретенных.</span><span class="sxs-lookup"><span data-stu-id="21c97-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="21c97-172">Мы будем Сортировать продукты по этой сумме и отображать пять верхних элементов.</span><span class="sxs-lookup"><span data-stu-id="21c97-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="21c97-173">Учитывая сложность этой логики, мы будем реализовывать этот алгоритм как хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="21c97-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="21c97-174">Процедура T-SQL для хранимой процедуры выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="21c97-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="21c97-175">Обратите внимание, что эта хранимая процедура (Селектпурчаседвиспродуктс) существовала в базе данных, когда мы включили ее в наше приложение, и когда мы создали EDM мы указали, что в дополнение к нужным таблицам и представлениям EDM должна содержать эту хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="21c97-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="21c97-176">Чтобы получить доступ к хранимой процедуре из EDM необходимо импортировать функцию.</span><span class="sxs-lookup"><span data-stu-id="21c97-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="21c97-177">Дважды щелкните EDM в обозревателе решений, чтобы открыть его в конструкторе и открыть Обозреватель моделей, щелкните правой кнопкой мыши в конструкторе и выберите "добавить функцию импорта функции".</span><span class="sxs-lookup"><span data-stu-id="21c97-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="21c97-178">Это приведет к открытию этого диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="21c97-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="21c97-179">Заполните поля, как показано выше, выбрав "Селектпурчаседвиспродуктс" и используя имя процедуры для имени импортированной функции.</span><span class="sxs-lookup"><span data-stu-id="21c97-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="21c97-180">Нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="21c97-180">Click "Ok".</span></span>

<span data-ttu-id="21c97-181">После этого мы можем просто программировать хранимую процедуру так же, как и любой другой элемент в модели.</span><span class="sxs-lookup"><span data-stu-id="21c97-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="21c97-182">Поэтому в папке Controls создайте новый пользовательский элемент управления с именем Алсопурчасед. ascx.</span><span class="sxs-lookup"><span data-stu-id="21c97-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="21c97-183">Разметка для этого элемента управления будет очень знакома с элементом управления Популаритемс.</span><span class="sxs-lookup"><span data-stu-id="21c97-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="21c97-184">Заметным различием является то, что не кэширование выходных данных, так как отображаемый элемент будет отличаться по сравнению с продуктом.</span><span class="sxs-lookup"><span data-stu-id="21c97-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="21c97-185">ProductId будет "свойством" для элемента управления.</span><span class="sxs-lookup"><span data-stu-id="21c97-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="21c97-186">В обработчике событий PreRender элемента управления мы ИД три вещи.</span><span class="sxs-lookup"><span data-stu-id="21c97-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="21c97-187">Убедитесь, что установлен параметр ProductID.</span><span class="sxs-lookup"><span data-stu-id="21c97-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="21c97-188">Проверьте, есть ли продукты, приобретенные с текущим.</span><span class="sxs-lookup"><span data-stu-id="21c97-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="21c97-189">Выводить некоторые элементы, как определено в #2.</span><span class="sxs-lookup"><span data-stu-id="21c97-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="21c97-190">Обратите внимание, насколько просто вызывать хранимую процедуру через модель.</span><span class="sxs-lookup"><span data-stu-id="21c97-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="21c97-191">После определения наличия "также приобретенных" можно просто привязать Repeater к результатам, возвращаемым запросом.</span><span class="sxs-lookup"><span data-stu-id="21c97-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="21c97-192">Если не было ни одного купленного элемента, мы просто отображаем другие популярные товары из нашего каталога.</span><span class="sxs-lookup"><span data-stu-id="21c97-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="21c97-193">Чтобы просмотреть "также купленные" элементы, откройте страницу Продуктдетаилс. aspx и перетащите элемент управления Алсопурчасед из обозревателя решений, чтобы он появился в этой позиции в разметке.</span><span class="sxs-lookup"><span data-stu-id="21c97-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="21c97-194">Это приведет к созданию ссылки на элемент управления в верхней части страницы Продуктдетаилс.</span><span class="sxs-lookup"><span data-stu-id="21c97-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="21c97-195">Так как пользовательский элемент управления Алсопурчасед требует номер ProductId, мы зададим свойство ProductID элемента управления, используя инструкцию eval для текущего элемента модели данных страницы.</span><span class="sxs-lookup"><span data-stu-id="21c97-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="21c97-196">Когда мы выполним сборку и запуск, а также перейдя к продукту, вы увидите «купленные» элементы.</span><span class="sxs-lookup"><span data-stu-id="21c97-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="21c97-197">[Назад](tailspin-spyworks-part-6.md)
> [Вперед](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="21c97-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
