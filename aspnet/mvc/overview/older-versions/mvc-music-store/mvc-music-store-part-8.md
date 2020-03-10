---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: Часть 8. Корзина для покупок с обновлениями AJAX | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. В части 8 описывается покупательская корзина с обновлениями AJAX.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433518"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="ffb76-104">Часть 8. Корзина для покупок с обновлениями AJAX</span><span class="sxs-lookup"><span data-stu-id="ffb76-104">Part 8: Shopping Cart with Ajax Updates</span></span>

<span data-ttu-id="ffb76-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="ffb76-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="ffb76-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="ffb76-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="ffb76-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="ffb76-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="ffb76-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="ffb76-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="ffb76-109">В части 8 описывается покупательская корзина с обновлениями AJAX.</span><span class="sxs-lookup"><span data-stu-id="ffb76-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>

<span data-ttu-id="ffb76-110">Мы разоставим пользователям возможность размещения альбомов в корзине без регистрации, но для завершения их извлечения потребуется зарегистрироваться как гости.</span><span class="sxs-lookup"><span data-stu-id="ffb76-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="ffb76-111">Процесс покупки и извлечения будет разделен на два контроллера: контроллер ShoppingCart, который разрешает анонимное Добавление элементов в корзину и контроллер извлечения, который обрабатывает процесс извлечения.</span><span class="sxs-lookup"><span data-stu-id="ffb76-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="ffb76-112">Мы начнем с корзины для покупок в этом разделе, а затем создадим процесс извлечения в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="ffb76-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="ffb76-113">Добавление классов моделей корзины, заказов и OrderDetail</span><span class="sxs-lookup"><span data-stu-id="ffb76-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="ffb76-114">В нашей корзине и процессах извлечения будут использоваться некоторые новые классы.</span><span class="sxs-lookup"><span data-stu-id="ffb76-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="ffb76-115">Щелкните правой кнопкой мыши папку Models и добавьте класс корзины (Cart.cs) со следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="ffb76-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="ffb76-116">Этот класс очень похож на другие, которые мы использовали до сих пор, за исключением атрибута [key] для свойства RecordId.</span><span class="sxs-lookup"><span data-stu-id="ffb76-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="ffb76-117">Наши элементы корзины будут иметь строковый идентификатор с именем Картид, чтобы разрешить анонимные покупки, но таблица включает целочисленный первичный ключ с именем RecordId.</span><span class="sxs-lookup"><span data-stu-id="ffb76-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="ffb76-118">По соглашению Entity Framework Code-First ожидает, что первичный ключ для таблицы с именем корзины будет либо Картид, либо ИДЕНТИФИКАТОРом, но мы можем легко переопределить это с помощью заметок или кода, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="ffb76-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="ffb76-119">Вот пример того, как мы можем использовать простые соглашения в Entity Framework коде — сначала, если они соответствуют нам, но мы не ограничены по ним, если это не так.</span><span class="sxs-lookup"><span data-stu-id="ffb76-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="ffb76-120">Затем добавьте класс Order (Order.cs) со следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="ffb76-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="ffb76-121">Этот класс отслеживает сводку и сведения о доставке для заказа.</span><span class="sxs-lookup"><span data-stu-id="ffb76-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="ffb76-122">**Он еще не компилируется**, так как имеет свойство навигации OrderDetails, которое зависит от класса, который еще не создан.</span><span class="sxs-lookup"><span data-stu-id="ffb76-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="ffb76-123">Теперь добавим класс с именем OrderDetail.cs, добавив в него следующий код.</span><span class="sxs-lookup"><span data-stu-id="ffb76-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="ffb76-124">Мы сделаем Последнее обновление нашего класса Мусиксторинтитиес, чтобы включить Дбсетс, которые предоставляют эти новые классы модели, также включая DbSet&lt;исполнителя&gt;.</span><span class="sxs-lookup"><span data-stu-id="ffb76-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="ffb76-125">Обновленный класс Мусиксторинтитиес выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ffb76-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="ffb76-126">Управление бизнес-логикой покупательской корзины</span><span class="sxs-lookup"><span data-stu-id="ffb76-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="ffb76-127">Далее мы создадим класс ShoppingCart в папке Models.</span><span class="sxs-lookup"><span data-stu-id="ffb76-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="ffb76-128">Модель ShoppingCart обрабатывает доступ к данным в таблице корзины.</span><span class="sxs-lookup"><span data-stu-id="ffb76-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="ffb76-129">Кроме того, он будет выполнять бизнес-логику для добавления и удаления элементов из корзины для покупок.</span><span class="sxs-lookup"><span data-stu-id="ffb76-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="ffb76-130">Так как мы не хотим требовать от пользователей регистрации учетной записи только для добавления элементов в покупательскую корзину, мы назначаем пользователям временный уникальный идентификатор (с помощью GUID или глобальный уникальный идентификатор) при обращении к корзине для покупок.</span><span class="sxs-lookup"><span data-stu-id="ffb76-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="ffb76-131">Этот идентификатор будет храниться с помощью класса сеанса ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ffb76-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="ffb76-132">*Примечание. сеанс ASP.NET — это удобное место для хранения сведений о пользователе, срок действия которого истекает после выхода сайта. В то время как неправильное использование состояния сеанса может негативно сказаться на производительности на больших сайтах, наша легкая работа будет хорошо работать в демонстрационных целях.*</span><span class="sxs-lookup"><span data-stu-id="ffb76-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="ffb76-133">Класс ShoppingCart предоставляет следующие методы:</span><span class="sxs-lookup"><span data-stu-id="ffb76-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="ffb76-134">**Аддтокарт** принимает в качестве параметра альбом и добавляет его в корзину пользователя.</span><span class="sxs-lookup"><span data-stu-id="ffb76-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="ffb76-135">Так как таблица корзины отслеживает количество для каждого альбома, она включает в себя логику для создания новой строки при необходимости или просто увеличивает количество, если пользователь уже выполнил сортировку по одной копии альбома.</span><span class="sxs-lookup"><span data-stu-id="ffb76-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="ffb76-136">**Ремовефромкарт** принимает идентификатор альбома и удаляет его из корзины пользователя.</span><span class="sxs-lookup"><span data-stu-id="ffb76-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="ffb76-137">Если у пользователя есть только одна копия альбома в корзине, строка удаляется.</span><span class="sxs-lookup"><span data-stu-id="ffb76-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="ffb76-138">**Емптикарт** удаляет все элементы из покупательской корзины пользователя.</span><span class="sxs-lookup"><span data-stu-id="ffb76-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="ffb76-139">**Жеткартитемс** извлекает список картитемс для вывода или обработки.</span><span class="sxs-lookup"><span data-stu-id="ffb76-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="ffb76-140">Функция **NOCOUNT** извлекает общее число альбомов, имеющихся у пользователя в корзине для покупок.</span><span class="sxs-lookup"><span data-stu-id="ffb76-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="ffb76-141">**Подытог** вычисляет общую стоимость всех элементов в корзине.</span><span class="sxs-lookup"><span data-stu-id="ffb76-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="ffb76-142">**CreateOrder** преобразует корзину для покупок в заказ на этапе извлечения.</span><span class="sxs-lookup"><span data-stu-id="ffb76-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="ffb76-143">GetObject **— это статический метод,** позволяющий контроллерам получить объект корзины.</span><span class="sxs-lookup"><span data-stu-id="ffb76-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="ffb76-144">Он использует метод **жеткартид** для управления чтением картид из сеанса пользователя.</span><span class="sxs-lookup"><span data-stu-id="ffb76-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="ffb76-145">Метод Жеткартид требует HttpContextBase, чтобы он мог считывать Картид пользователя из сеанса пользователя.</span><span class="sxs-lookup"><span data-stu-id="ffb76-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="ffb76-146">Вот полный **класс ShoppingCart**:</span><span class="sxs-lookup"><span data-stu-id="ffb76-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="ffb76-147">Модели представлений</span><span class="sxs-lookup"><span data-stu-id="ffb76-147">ViewModels</span></span>

<span data-ttu-id="ffb76-148">Нашему контроллеру покупательской корзины необходимо передать некоторую сложную информацию в свои представления, которые не будут четко сопоставляться с нашими объектами модели.</span><span class="sxs-lookup"><span data-stu-id="ffb76-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="ffb76-149">Мы не хотим изменять наши модели в соответствии с нашими представлениями; Классы моделей должны представлять наш домен, а не пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="ffb76-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="ffb76-150">Одним из решений было бы передача информации в наши представления с помощью класса ViewBag, как это было сделано с раскрывающимся списком менеджеров магазина, но передача большого объема информации через ViewBag становится трудной для управления.</span><span class="sxs-lookup"><span data-stu-id="ffb76-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="ffb76-151">Решением этой проблемы является использование шаблона *ViewModel* .</span><span class="sxs-lookup"><span data-stu-id="ffb76-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="ffb76-152">При использовании этого шаблона создаются строго типизированные классы, оптимизированные для наших сценариев представления, которые предоставляют свойства для динамических значений и содержимого, необходимых для наших шаблонов представления.</span><span class="sxs-lookup"><span data-stu-id="ffb76-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="ffb76-153">Наши классы контроллеров могут затем заполнять и передавать эти оптимизированные для просмотра классы в наш шаблон представления для использования.</span><span class="sxs-lookup"><span data-stu-id="ffb76-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="ffb76-154">Это обеспечивает безопасность типов, проверку во время компиляции и IntelliSense в редакторе в шаблонах представления.</span><span class="sxs-lookup"><span data-stu-id="ffb76-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="ffb76-155">Мы создадим две модели представления для использования в нашем контроллере покупательской корзины: Шоппингкартвиевмодел будет содержать содержимое покупательской корзины, а Шоппингкартремовевиевмодел будет использоваться для отображения сведений о подтверждении, когда пользователь удаляет что-либо. из своей корзины.</span><span class="sxs-lookup"><span data-stu-id="ffb76-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="ffb76-156">Давайте создадим новую папку ViewModels в корне нашего проекта, чтобы не усложнять их.</span><span class="sxs-lookup"><span data-stu-id="ffb76-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="ffb76-157">Щелкните правой кнопкой мыши проект и выберите Добавить или создать папку.</span><span class="sxs-lookup"><span data-stu-id="ffb76-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="ffb76-158">Присвойте папке имя ViewModel.</span><span class="sxs-lookup"><span data-stu-id="ffb76-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="ffb76-159">Затем добавьте класс Шоппингкартвиевмодел в папку ViewModels.</span><span class="sxs-lookup"><span data-stu-id="ffb76-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="ffb76-160">Он имеет два свойства: список элементов корзины и десятичное значение для хранения общей цены для всех элементов в корзине.</span><span class="sxs-lookup"><span data-stu-id="ffb76-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="ffb76-161">Теперь добавьте Шоппингкартремовевиевмодел в папку ViewModels со следующими четырьмя свойствами.</span><span class="sxs-lookup"><span data-stu-id="ffb76-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="ffb76-162">Контроллер корзины для покупок</span><span class="sxs-lookup"><span data-stu-id="ffb76-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="ffb76-163">Контроллер корзины для покупок имеет три основных цели: Добавление элементов в корзину, удаление элементов из корзины и просмотр элементов в корзине.</span><span class="sxs-lookup"><span data-stu-id="ffb76-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="ffb76-164">В нем будут использоваться только что созданные три класса: Шоппингкартвиевмодел, Шоппингкартремовевиевмодел и ShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="ffb76-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="ffb76-165">Как и в Стореконтроллер и Стореманажерконтроллер, мы добавим поле для хранения экземпляра Мусиксторинтитиес.</span><span class="sxs-lookup"><span data-stu-id="ffb76-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="ffb76-166">Добавьте новый контроллер корзины для покупок в проект, используя пустой шаблон контроллера.</span><span class="sxs-lookup"><span data-stu-id="ffb76-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="ffb76-167">Вот полный контроллер ShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="ffb76-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="ffb76-168">Действия индекса и добавления контроллера должны выглядеть очень хорошо.</span><span class="sxs-lookup"><span data-stu-id="ffb76-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="ffb76-169">Действия контроллера Remove и Картсуммари обрабатывались в двух особых случаях, которые обсуждаются в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="ffb76-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="ffb76-170">Обновления AJAX с jQuery</span><span class="sxs-lookup"><span data-stu-id="ffb76-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="ffb76-171">Далее мы создадим страницу индекса покупательской корзины, которая является строго типизированной для Шоппингкартвиевмодел и использует шаблон представления списка, используя тот же метод, что и раньше.</span><span class="sxs-lookup"><span data-stu-id="ffb76-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="ffb76-172">Однако вместо использования HTML. ActionLink для удаления элементов из корзины мы будем использовать jQuery для "подключения" события Click для всех ссылок в этом представлении, имеющих HTML-класс Ремовелинк.</span><span class="sxs-lookup"><span data-stu-id="ffb76-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="ffb76-173">Вместо отправки формы этот обработчик событий щелчка мыши просто сделает обратный вызов AJAX для нашего действия контроллера Ремовефромкарт.</span><span class="sxs-lookup"><span data-stu-id="ffb76-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="ffb76-174">Ремовефромкарт Возвращает сериализованный результат JSON, который затем осуществляет обратный вызов jQuery и выполняет четыре быстрых обновления страницы с помощью jQuery:</span><span class="sxs-lookup"><span data-stu-id="ffb76-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="ffb76-175">Удаляет удаленный альбом из списка</span><span class="sxs-lookup"><span data-stu-id="ffb76-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="ffb76-176">Обновляет число корзин в заголовке</span><span class="sxs-lookup"><span data-stu-id="ffb76-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="ffb76-177">Отображает сообщение об обновлении для пользователя</span><span class="sxs-lookup"><span data-stu-id="ffb76-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="ffb76-178">Обновляет общую цену корзины</span><span class="sxs-lookup"><span data-stu-id="ffb76-178">Updates the cart total price</span></span>

<span data-ttu-id="ffb76-179">Так как сценарий удаления обрабатывается обратным вызовом AJAX в представлении индекса, для действия Ремовефромкарт не требуется дополнительное представление.</span><span class="sxs-lookup"><span data-stu-id="ffb76-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="ffb76-180">Ниже приведен полный код для представления/Шоппингкарт/индекс:</span><span class="sxs-lookup"><span data-stu-id="ffb76-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="ffb76-181">Чтобы протестировать это, нам нужно иметь возможность добавлять элементы в нашу корзину для покупок.</span><span class="sxs-lookup"><span data-stu-id="ffb76-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="ffb76-182">Мы будем обновлять наше представление **сведений о магазине** , включив кнопку "добавить в корзину".</span><span class="sxs-lookup"><span data-stu-id="ffb76-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="ffb76-183">Мы можем включить в него некоторые дополнительные сведения, которые мы добавили с момента последнего обновления этого представления: Жанр, исполнитель, Цена и обложка альбома.</span><span class="sxs-lookup"><span data-stu-id="ffb76-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="ffb76-184">Обновленный код представления сведений о магазине отображается, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ffb76-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="ffb76-185">Теперь мы можем щелкнуть магазин и протестировать Добавление и удаление альбомов в нашей корзине для покупок.</span><span class="sxs-lookup"><span data-stu-id="ffb76-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="ffb76-186">Запустите приложение и перейдите к индексу магазина.</span><span class="sxs-lookup"><span data-stu-id="ffb76-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="ffb76-187">Затем щелкните Жанр, чтобы просмотреть список альбомов.</span><span class="sxs-lookup"><span data-stu-id="ffb76-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="ffb76-188">Щелкнув название альбома, вы увидите обновленное представление сведений о альбоме, включая кнопку "добавить в корзину".</span><span class="sxs-lookup"><span data-stu-id="ffb76-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="ffb76-189">При нажатии кнопки "добавить в корзину" отображается представление индекса корзины для покупок с перечнем сводки корзины.</span><span class="sxs-lookup"><span data-stu-id="ffb76-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="ffb76-190">После загрузки корзины для покупок можно щелкнуть ссылку удалить из корзины, чтобы просмотреть обновление AJAX в корзину для покупок.</span><span class="sxs-lookup"><span data-stu-id="ffb76-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="ffb76-191">Мы создали рабочую корзину для покупок, которая позволяет незарегистрированным пользователям добавлять элементы в корзину.</span><span class="sxs-lookup"><span data-stu-id="ffb76-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="ffb76-192">В следующем разделе мы развернемся к регистрации и завершению процесса извлечения.</span><span class="sxs-lookup"><span data-stu-id="ffb76-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ffb76-193">[Назад](mvc-music-store-part-7.md)
> [Вперед](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="ffb76-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
