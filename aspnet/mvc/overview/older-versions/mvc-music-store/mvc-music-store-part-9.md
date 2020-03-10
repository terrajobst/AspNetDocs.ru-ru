---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: Часть 9. Регистрация и извлечение | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. Часть 9 охватывает регистрацию и извлечение.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450900"
---
# <a name="part-9-registration-and-checkout"></a><span data-ttu-id="fe8f3-104">Часть 9. Регистрация и извлечение</span><span class="sxs-lookup"><span data-stu-id="fe8f3-104">Part 9: Registration and Checkout</span></span>

<span data-ttu-id="fe8f3-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="fe8f3-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="fe8f3-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="fe8f3-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="fe8f3-109">Часть 9 охватывает регистрацию и извлечение.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-109">Part 9 covers Registration and Checkout.</span></span>

<span data-ttu-id="fe8f3-110">В этом разделе мы создадим Чеккаутконтроллер, который будет получать сведения об адресе и платеже покупателя.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="fe8f3-111">Перед извлечением необходимо, чтобы пользователи регистрировались на нашем сайте, поэтому для этого контроллера потребуется авторизация.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="fe8f3-112">Пользователи будут переходить к процессу извлечения из покупательской корзины, нажав кнопку "извлечь".</span><span class="sxs-lookup"><span data-stu-id="fe8f3-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="fe8f3-113">Если пользователь не вошел в систему, ему будет предложено.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="fe8f3-114">После успешного входа пользователь отобразит представление адрес и платеж.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="fe8f3-115">После заполнения формы и отправки заказа они будут отображаться на экране подтверждения заказа.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="fe8f3-116">При попытке просмотра несуществующего заказа или заказа, который не принадлежит вам, отобразится представление ошибок.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="fe8f3-117">Перенос корзины для покупок</span><span class="sxs-lookup"><span data-stu-id="fe8f3-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="fe8f3-118">Хотя процесс покупки является анонимным, когда пользователь нажимает кнопку "извлечь", ему потребуется зарегистрироваться и войти в систему.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="fe8f3-119">Пользователи будут иметь возможность сохранять информацию о корзине для покупок между посещениями, поэтому нам нужно будет связать сведения о корзине для покупок с пользователем при завершении регистрации или входе.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="fe8f3-120">Это очень просто, так как у нашего класса ShoppingCart уже есть метод, который свяжет все элементы в текущей корзине с именем пользователя.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="fe8f3-121">При завершении регистрации или входа пользователь должен просто вызвать этот метод.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="fe8f3-122">Откройте класс **AccountController** , который мы добавили при настройке членства и авторизации.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="fe8f3-123">Добавьте инструкцию using, ссылающуюся на Мвкмусиксторе. Models, а затем добавьте следующий метод Мигратешоппингкарт:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="fe8f3-124">Затем измените действие LogOn POST, чтобы вызвать Мигратешоппингкарт после проверки пользователя, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="fe8f3-125">Внесите одно и то же изменение в действие регистрация после успешного создания учетной записи пользователя:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="fe8f3-126">Теперь она будет автоматически перенесена в учетную запись пользователя после успешной регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="fe8f3-127">Создание Чеккаутконтроллер</span><span class="sxs-lookup"><span data-stu-id="fe8f3-127">Creating the CheckoutController</span></span>

<span data-ttu-id="fe8f3-128">Щелкните правой кнопкой мыши папку Controllers и добавьте новый контроллер в проект с именем Чеккаутконтроллер, используя пустой шаблон контроллера.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="fe8f3-129">Сначала добавьте атрибут авторизовать над объявлением класса контроллера, чтобы требовать, чтобы пользователи регистрировались перед извлечением:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="fe8f3-130">*Примечание. Это похоже на изменение, которое мы ранее внесли в Стореманажерконтроллер, но в этом случае атрибуту авторизации требуется, чтобы пользователь был в роли администратора. В контроллере извлечения требуется, чтобы пользователь вошел в систему, но не требовал, чтобы он был администратором.*</span><span class="sxs-lookup"><span data-stu-id="fe8f3-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="fe8f3-131">Для простоты мы не будем работать со сведениями о платежах в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="fe8f3-132">Вместо этого мы предоставляем пользователям возможность извлекаться с помощью рекламного кода.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="fe8f3-133">Мы будем хранить этот код рекламной акции с помощью константы с именем промокод.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="fe8f3-134">Как и в Стореконтроллер, мы объявляем поле для хранения экземпляра класса Мусиксторинтитиес с именем Сторедб.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="fe8f3-135">Чтобы использовать класс Мусиксторинтитиес, необходимо добавить инструкцию using для пространства имен Мвкмусиксторе. Models.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="fe8f3-136">Верхняя часть нашего контроллера извлечения показана ниже.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="fe8f3-137">Чеккаутконтроллер будет иметь следующие действия контроллера:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="fe8f3-138">**Аддрессандпаймент (метод Get)** будет отображать форму, позволяющую пользователю вводить данные.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="fe8f3-139">**Аддрессандпаймент (метод POST)** проверит ввод и обработает заказ.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="fe8f3-140">**Полная** будет показана после успешного завершения процесса извлечения пользователем.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="fe8f3-141">Это представление будет включать номер заказа пользователя в качестве подтверждения.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="fe8f3-142">Во-первых, переименование действия контроллера индекса (созданного при создании контроллера) в Аддрессандпаймент.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="fe8f3-143">Это действие контроллера просто отображает форму извлечения, поэтому для нее не требуются сведения о модели.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="fe8f3-144">Наш метод Аддрессандпаймент POST будет следовать тому же шаблону, который мы использовали в Стореманажерконтроллер: он попытается принять отправку формы и выполнить заказ, после чего снова отобразит форму в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="fe8f3-145">После проверки того, что входные данные соответствуют требованиям к проверке заказа, мы будем проверять значение формы промокод напрямую.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="fe8f3-146">Предполагая, что все правильно, мы сохраняем обновленные сведения в заказе, наскажуи объекту ShoppingCart завершить процесс заказа и перейдете к выполнению действия.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="fe8f3-147">После успешного завершения процесса извлечения пользователи будут перенаправлены к полному действию контроллера.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="fe8f3-148">Это действие выполняет простую проверку того, что заказ действительно принадлежит пользователю, вошедшему в систему, перед отображением номера заказа в качестве подтверждения.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="fe8f3-149">*Примечание. представление ошибок было автоматически создано для нас в папке/Виевс/Шаред, когда мы начали проект.*</span><span class="sxs-lookup"><span data-stu-id="fe8f3-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="fe8f3-150">Полный код Чеккаутконтроллер выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="fe8f3-151">Добавление представления Аддрессандпаймент</span><span class="sxs-lookup"><span data-stu-id="fe8f3-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="fe8f3-152">Теперь создадим представление Аддрессандпаймент.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="fe8f3-153">Щелкните правой кнопкой мыши одно из действий контроллера Аддрессандпаймент и добавьте представление с именем Аддрессандпаймент, которое строго типизировано как заказ и использует шаблон редактирования, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="fe8f3-154">В этом представлении будут использоваться два метода, которые мы рассматривали при создании представления Стореманажередит:</span><span class="sxs-lookup"><span data-stu-id="fe8f3-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="fe8f3-155">Мы будем использовать HTML. Едиторформодел () для вывода полей формы для модели заказа.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="fe8f3-156">Мы будем использовать правила проверки, используя класс Order с атрибутами проверки.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="fe8f3-157">Мы начнем с обновления кода формы для использования HTML. Едиторформодел (), за которым следует дополнительное текстовое поле для кода Акционная.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="fe8f3-158">Полный код для представления Аддрессандпаймент приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="fe8f3-159">Определение правил проверки для заказа</span><span class="sxs-lookup"><span data-stu-id="fe8f3-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="fe8f3-160">Теперь, когда наше представление настроено, мы настроили правила проверки для нашей модели заказов, как это было сделано ранее для модели альбома.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="fe8f3-161">Щелкните правой кнопкой мыши папку Models и добавьте класс с именем Order.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="fe8f3-162">Помимо атрибутов проверки, использовавшихся ранее для альбома, мы также будем использовать регулярное выражение для проверки адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="fe8f3-163">При попытке отправить форму с отсутствующими или недопустимыми сведениями будет отображаться сообщение об ошибке с помощью проверки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="fe8f3-164">Итак, мы сделали большую часть сложной работы для процесса извлечения. у нас есть несколько вероятность и завершение.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="fe8f3-165">Нам нужно добавить два простых представления, и во время входа в систему необходимо принять во внимание сведения о корзине.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="fe8f3-166">Добавление представления "Извлечение завершено"</span><span class="sxs-lookup"><span data-stu-id="fe8f3-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="fe8f3-167">Представление "Извлечение завершено" довольно простое, так как ему просто нужно отобразить идентификатор заказа.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="fe8f3-168">Щелкните правой кнопкой мыши действие завершение контроллера и добавьте представление с именем Complete, которое строго типизировано как целое число.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="fe8f3-169">Теперь мы будем обновлять код представления для отображения идентификатора заказа, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="fe8f3-170">Обновление представления ошибок</span><span class="sxs-lookup"><span data-stu-id="fe8f3-170">Updating The Error view</span></span>

<span data-ttu-id="fe8f3-171">Шаблон по умолчанию включает представление ошибок в папку Общие представления, чтобы его можно было повторно использовать в любом месте сайта.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="fe8f3-172">Это представление ошибок содержит очень простую ошибку и не использует макет сайта, поэтому мы будем обновлять его.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="fe8f3-173">Так как это общая страница ошибки, содержимое очень простое.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="fe8f3-174">Мы будем включать сообщение и ссылку для перехода на предыдущую страницу в журнале, если пользователь хочет повторно выполнить действие.</span><span class="sxs-lookup"><span data-stu-id="fe8f3-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> <span data-ttu-id="fe8f3-175">[Назад](mvc-music-store-part-8.md)
> [Вперед](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="fe8f3-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
