---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: Часть 5. бизнес-логика | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. Часть 5 добавляет некоторую бизнес-логику.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511548"
---
# <a name="part-5-business-logic"></a><span data-ttu-id="e7318-104">Часть 5. бизнес-логика</span><span class="sxs-lookup"><span data-stu-id="e7318-104">Part 5: Business Logic</span></span>

<span data-ttu-id="e7318-105">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="e7318-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="e7318-106">В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET.</span><span class="sxs-lookup"><span data-stu-id="e7318-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="e7318-107">Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.</span><span class="sxs-lookup"><span data-stu-id="e7318-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="e7318-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="e7318-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="e7318-109">Часть 5 добавляет некоторую бизнес-логику.</span><span class="sxs-lookup"><span data-stu-id="e7318-109">Part 5 adds some business logic.</span></span>

## <a id="_Toc260221671"></a><span data-ttu-id="e7318-110">Добавление бизнес-логики</span><span class="sxs-lookup"><span data-stu-id="e7318-110">Adding Some Business Logic</span></span>

<span data-ttu-id="e7318-111">Мы хотим, чтобы наши товары были доступны при каждом посещении веб-узла.</span><span class="sxs-lookup"><span data-stu-id="e7318-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="e7318-112">Посетители смогут просматривать и добавлять элементы в корзину покупок, даже если они не зарегистрированы или не вошли в систему.</span><span class="sxs-lookup"><span data-stu-id="e7318-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="e7318-113">Когда они готовы к извлечению, им будет предоставлена возможность проверки подлинности и, если они еще не являются участниками, они смогут создать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="e7318-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="e7318-114">Это означает, что нам потребуется реализовать логику для преобразования корзины покупок из анонимного состояния в состояние "зарегистрированный пользователь".</span><span class="sxs-lookup"><span data-stu-id="e7318-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="e7318-115">Давайте создадим каталог с именем "classes", затем щелкните правой кнопкой мыши папку и создайте новый файл "class" с именем MyShoppingCart.cs</span><span class="sxs-lookup"><span data-stu-id="e7318-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="e7318-116">Как упоминалось ранее, мы будем расширять класс, реализующий страницу Мишоппингкарт. aspx, и будем делать это с помощью. Мощная конструкция "разделяемого класса" NET.</span><span class="sxs-lookup"><span data-stu-id="e7318-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="e7318-117">Созданный вызов для нашего файла MyShoppingCart.aspx.cf выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e7318-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="e7318-118">Обратите внимание на использование ключевого слова partial.</span><span class="sxs-lookup"><span data-stu-id="e7318-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="e7318-119">Только что созданный файл класса выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e7318-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="e7318-120">Мы будем объединять наши реализации, добавив ключевое слово partial в этот файл.</span><span class="sxs-lookup"><span data-stu-id="e7318-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="e7318-121">Теперь наш новый файл класса выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e7318-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="e7318-122">Первый метод, который будет добавлен в наш класс, — это метод AddItem.</span><span class="sxs-lookup"><span data-stu-id="e7318-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="e7318-123">Это метод, который в конечном итоге будет вызываться, когда пользователь щелкнет ссылку "добавить в рисунок" на страницах списка продуктов и сведений о продукте.</span><span class="sxs-lookup"><span data-stu-id="e7318-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="e7318-124">Добавьте следующий текст в операторы using в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e7318-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="e7318-125">И добавьте этот метод в класс Мишоппингкарт.</span><span class="sxs-lookup"><span data-stu-id="e7318-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="e7318-126">Мы используем LINQ to Entities, чтобы узнать, уже находится ли элемент в корзине.</span><span class="sxs-lookup"><span data-stu-id="e7318-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="e7318-127">Если да, то обновляется количество элементов в заказе, в противном случае мы создаем новую запись для выбранного элемента.</span><span class="sxs-lookup"><span data-stu-id="e7318-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="e7318-128">Чтобы вызвать этот метод, мы выполним страницу Аддтокарт. aspx, которая не только наследует классу этого метода, но затем выводит текущую покупку a = корзина после добавления элемента.</span><span class="sxs-lookup"><span data-stu-id="e7318-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="e7318-129">Щелкните правой кнопкой мыши имя решения в обозревателе решений и добавьте новую страницу с именем Аддтокарт. aspx, как было сделано ранее.</span><span class="sxs-lookup"><span data-stu-id="e7318-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="e7318-130">Несмотря на то, что эту страницу можно использовать для отображения промежуточных результатов, подобных проблемам с низкими расходами, и т. д. в нашей реализации страница не будет отображена, а вместо этого вызывать логику "Add" и перенаправление.</span><span class="sxs-lookup"><span data-stu-id="e7318-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="e7318-131">Для этого мы добавим следующий код на странице событие загрузки страницы\_.</span><span class="sxs-lookup"><span data-stu-id="e7318-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="e7318-132">Обратите внимание, что мы получаем продукт для добавления в корзину для покупок из параметра QueryString и вызовом метода AddItem нашего класса.</span><span class="sxs-lookup"><span data-stu-id="e7318-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="e7318-133">Если ошибки не обнаружены, управление передается странице SHoppingCart. aspx, которая будет полностью реализована далее.</span><span class="sxs-lookup"><span data-stu-id="e7318-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="e7318-134">Если возникает ошибка, возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="e7318-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="e7318-135">В настоящее время мы еще не реализовали глобальный обработчик ошибок, чтобы это исключение было бы необработанным нашим приложением, но это будет устранено чуть позже.</span><span class="sxs-lookup"><span data-stu-id="e7318-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="e7318-136">Обратите внимание также на использование инструкции Debug. Fail () (доступно через `using System.Diagnostics;)`</span><span class="sxs-lookup"><span data-stu-id="e7318-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="e7318-137">Приложение выполняется внутри отладчика. в этом методе отображается подробное диалоговое окно со сведениями о состоянии приложений, а также указанном сообщении об ошибке.</span><span class="sxs-lookup"><span data-stu-id="e7318-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="e7318-138">При запуске в рабочей среде инструкция Debug. Fail () игнорируется.</span><span class="sxs-lookup"><span data-stu-id="e7318-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="e7318-139">В коде, приведенном выше, следует вызвать метод в именах классов покупательской корзины "Жетшоппингкартид".</span><span class="sxs-lookup"><span data-stu-id="e7318-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="e7318-140">Добавьте код для реализации метода следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e7318-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="e7318-141">Обратите внимание, что мы также добавили кнопки обновления и извлечения и метку, в которой можно отобразить корзину "итог".</span><span class="sxs-lookup"><span data-stu-id="e7318-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="e7318-142">Теперь мы можем добавлять элементы в нашу корзину для покупок, но мы не реализовали логику для вывода корзины после добавления продукта.</span><span class="sxs-lookup"><span data-stu-id="e7318-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="e7318-143">Таким образом, на странице Мишоппингкарт. aspx мы добавим элемент управления EntityDataSource и элемент управления Гридвире следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e7318-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="e7318-144">Вызовите форму в конструкторе, чтобы можно было дважды щелкнуть кнопку "Обновить корзину" и создать обработчик событий щелчка, указанный в объявлении в разметке.</span><span class="sxs-lookup"><span data-stu-id="e7318-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="e7318-145">Эти сведения будут реализованы позже, но это позволит нам создавать и запускать приложение без ошибок.</span><span class="sxs-lookup"><span data-stu-id="e7318-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="e7318-146">При запуске приложения и добавлении элемента в корзину для покупок вы увидите это.</span><span class="sxs-lookup"><span data-stu-id="e7318-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="e7318-147">Обратите внимание, что мы отклоняете отображение сетки "по умолчанию", реализуя три настраиваемых столбца.</span><span class="sxs-lookup"><span data-stu-id="e7318-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="e7318-148">Первый — это редактируемое, "привязанное" поле для количества:</span><span class="sxs-lookup"><span data-stu-id="e7318-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="e7318-149">Далее следует вычисляемый столбец, в котором отображается итог по номенклатуре строки (стоимость товара для заказанного количества):</span><span class="sxs-lookup"><span data-stu-id="e7318-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="e7318-150">Наконец, у нас есть пользовательский столбец, содержащий элемент управления CheckBox, который пользователь будет использовать для указания, что элемент должен быть удален из диаграммы покупок.</span><span class="sxs-lookup"><span data-stu-id="e7318-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="e7318-151">Как видите, строка «итог заказа» пуста, поэтому мы добавим некоторую логику для вычисления итогового значения заказа.</span><span class="sxs-lookup"><span data-stu-id="e7318-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="e7318-152">Сначала мы реализуем метод "подытог" для нашего класса Мишоппингкарт.</span><span class="sxs-lookup"><span data-stu-id="e7318-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="e7318-153">Добавьте следующий код в файл MyShoppingCart.cs.</span><span class="sxs-lookup"><span data-stu-id="e7318-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="e7318-154">Затем на странице\_загрузки обработчика событий можно будет вызвать метод подытога.</span><span class="sxs-lookup"><span data-stu-id="e7318-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="e7318-155">В то же время мы добавим тест, чтобы проверить, пуста ли корзина для покупок, и соответствующим образом настроить отображение.</span><span class="sxs-lookup"><span data-stu-id="e7318-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="e7318-156">Теперь, если корзина для покупок пуста, мы получаем это:</span><span class="sxs-lookup"><span data-stu-id="e7318-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="e7318-157">В противном случае мы видим итог.</span><span class="sxs-lookup"><span data-stu-id="e7318-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="e7318-158">Однако эта страница еще не завершена.</span><span class="sxs-lookup"><span data-stu-id="e7318-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="e7318-159">Нам потребуется дополнительная логика для повторного вычисления корзины покупок путем удаления элементов, отмеченных для удаления, и определения новых значений количества, которые могут быть изменены пользователем в сетке.</span><span class="sxs-lookup"><span data-stu-id="e7318-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="e7318-160">Позволяет добавить метод "RemoveItem" в наш класс покупательской корзины в MyShoppingCart.cs для решения ситуации, когда пользователь помечает элемент для удаления.</span><span class="sxs-lookup"><span data-stu-id="e7318-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="e7318-161">Теперь давайте обходим метод для решения ситуации, когда пользователь просто изменяет качество для упорядочения в GridView.</span><span class="sxs-lookup"><span data-stu-id="e7318-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="e7318-162">Благодаря базовым функциям удаления и обновления на месте мы можем реализовать логику, которая фактически обновляет корзину покупок в базе данных.</span><span class="sxs-lookup"><span data-stu-id="e7318-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="e7318-163">(В MyShoppingCart.cs)</span><span class="sxs-lookup"><span data-stu-id="e7318-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="e7318-164">Обратите внимание, что этот метод предполагает наличие двух параметров.</span><span class="sxs-lookup"><span data-stu-id="e7318-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="e7318-165">Одна из них — идентификатор покупательской корзины, а другая — массив объектов определяемого пользователем типа.</span><span class="sxs-lookup"><span data-stu-id="e7318-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="e7318-166">Таким образом, чтобы максимально ограничить зависимость нашей логики от особенностей пользовательского интерфейса, мы определили структуру данных, которую мы можем использовать для передачи элементов корзины покупок в наш код без необходимости прямого доступа к элементу управления GridView.</span><span class="sxs-lookup"><span data-stu-id="e7318-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="e7318-167">В нашем MyShoppingCart.aspx.cs файле мы можем использовать эту структуру в обработчике событий нажатия кнопки обновления, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e7318-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="e7318-168">Обратите внимание, что в дополнение к обновлению корзины мы также будем обновлять итоговую корзину.</span><span class="sxs-lookup"><span data-stu-id="e7318-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="e7318-169">Обратите внимание на конкретную строку кода:</span><span class="sxs-lookup"><span data-stu-id="e7318-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="e7318-170">Функции "MyShoppingCart.aspx.cs" () — это специальная вспомогательная функция, которую мы будем реализовывать в качестве приведенных ниже.</span><span class="sxs-lookup"><span data-stu-id="e7318-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="e7318-171">Это обеспечивает чистый способ доступа к значениям привязанных элементов в элементе управления GridView.</span><span class="sxs-lookup"><span data-stu-id="e7318-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="e7318-172">Поскольку элемент управления CheckBox "Remove Item" не привязан, мы будем обращаться к нему через метод Финдконтрол ().</span><span class="sxs-lookup"><span data-stu-id="e7318-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="e7318-173">На этом этапе разработки проекта мы готовы к реализации процесса извлечения.</span><span class="sxs-lookup"><span data-stu-id="e7318-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="e7318-174">Перед этим мы будем использовать Visual Studio для создания базы данных членства и добавления пользователя в репозиторий членства.</span><span class="sxs-lookup"><span data-stu-id="e7318-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e7318-175">[Назад](tailspin-spyworks-part-4.md)
> [Вперед](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="e7318-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
