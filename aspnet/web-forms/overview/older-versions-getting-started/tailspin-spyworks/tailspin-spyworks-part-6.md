---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: Часть 6. членство в ASP.NET | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. Часть 6 добавляет членство в ASP.NET.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454884"
---
# <a name="part-6-aspnet-membership"></a><span data-ttu-id="84367-104">Часть 6. членство в ASP.NET</span><span class="sxs-lookup"><span data-stu-id="84367-104">Part 6: ASP.NET Membership</span></span>

<span data-ttu-id="84367-105">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="84367-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="84367-106">В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET.</span><span class="sxs-lookup"><span data-stu-id="84367-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="84367-107">Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.</span><span class="sxs-lookup"><span data-stu-id="84367-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="84367-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="84367-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="84367-109">Часть 6 добавляет членство в ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="84367-109">Part 6 adds ASP.NET Membership.</span></span>

## <a id="_Toc260221672"></a><span data-ttu-id="84367-110">Работа с членством в ASP.NET</span><span class="sxs-lookup"><span data-stu-id="84367-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="84367-111">Щелкните Безопасность.</span><span class="sxs-lookup"><span data-stu-id="84367-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="84367-112">Убедитесь, что используется проверка подлинности с помощью форм.</span><span class="sxs-lookup"><span data-stu-id="84367-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="84367-113">Используйте ссылку "создать пользователя", чтобы создать несколько пользователей.</span><span class="sxs-lookup"><span data-stu-id="84367-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="84367-114">По завершении просмотрите окно обозреватель решений и обновите представление.</span><span class="sxs-lookup"><span data-stu-id="84367-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="84367-115">Обратите внимание, что ASPNETDB. Создан MDF.</span><span class="sxs-lookup"><span data-stu-id="84367-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="84367-116">Этот файл содержит таблицы для поддержки основных служб ASP.NET, таких как членство.</span><span class="sxs-lookup"><span data-stu-id="84367-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="84367-117">Теперь мы можем приступить к реализации процесса извлечения.</span><span class="sxs-lookup"><span data-stu-id="84367-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="84367-118">Начните с создания страницы CheckOut. aspx.</span><span class="sxs-lookup"><span data-stu-id="84367-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="84367-119">Страница CheckOut. aspx должна быть доступна только пользователям, вошедшим в систему, поэтому мы будем ограничивать доступ к вошедшему в систему пользователям и перенаправлять пользователей, которые не вошли на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="84367-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="84367-120">Для этого добавьте следующий элемент в раздел конфигурации нашего файла Web. config.</span><span class="sxs-lookup"><span data-stu-id="84367-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="84367-121">Шаблон для приложений веб-форм ASP.NET автоматически добавил раздел проверки подлинности в наш файл Web. config и создал страницу входа по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="84367-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="84367-122">Необходимо изменить файл кода для Login. aspx, чтобы перенести корзину анонимных покупок при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="84367-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="84367-123">Измените событие загрузки страницы\_, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="84367-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="84367-124">Затем добавьте обработчик событий с ведением журнала следующего вида, чтобы задать имя сеанса для вновь вошедшего в систему пользователя и изменить временный идентификатор сеанса в корзине для покупок на пользователя, вызвав метод Мигратекарт в нашем классе Мишоппингкарт.</span><span class="sxs-lookup"><span data-stu-id="84367-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="84367-125">(Реализовано в CS-файле)</span><span class="sxs-lookup"><span data-stu-id="84367-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="84367-126">Реализуйте метод Мигратекарт () следующим образом.</span><span class="sxs-lookup"><span data-stu-id="84367-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="84367-127">В файле Checkout. aspx мы будем использовать EntityDataSource и GridView на странице извлечения, как это делалось на странице покупательской корзины.</span><span class="sxs-lookup"><span data-stu-id="84367-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="84367-128">Обратите внимание, что наш элемент управления GridView Указывает обработчик событий "ондатабаунд" с именем Милист\_RowDataBound, так что давайте реализуем этот обработчик событий следующим образом.</span><span class="sxs-lookup"><span data-stu-id="84367-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="84367-129">Этот метод сохраняет накопленный итог корзины покупок по мере привязки каждой строки и обновляет нижнюю строку GridView.</span><span class="sxs-lookup"><span data-stu-id="84367-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="84367-130">На этом этапе мы реализовали представление заказа для просмотра.</span><span class="sxs-lookup"><span data-stu-id="84367-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="84367-131">Давайте обработаем пустого сценария корзины, добавив несколько строк кода на нашу страницу\_загрузить событие:</span><span class="sxs-lookup"><span data-stu-id="84367-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="84367-132">Когда пользователь нажимает кнопку "Отправить", в обработчике событий нажатия кнопки "Отправить" будет выполнен следующий код.</span><span class="sxs-lookup"><span data-stu-id="84367-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="84367-133">"Мясо" процесса отправки заказа должен быть реализован в методе Субмитордер () нашего класса Мишоппингкарт.</span><span class="sxs-lookup"><span data-stu-id="84367-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="84367-134">Субмитордер будет:</span><span class="sxs-lookup"><span data-stu-id="84367-134">SubmitOrder will:</span></span>

- <span data-ttu-id="84367-135">Возьмите все строки из корзины для покупок и используйте их для создания новой записи заказа и связанных записей OrderDetails.</span><span class="sxs-lookup"><span data-stu-id="84367-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="84367-136">Рассчитайте дату отгрузки.</span><span class="sxs-lookup"><span data-stu-id="84367-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="84367-137">Очистите корзину для покупок.</span><span class="sxs-lookup"><span data-stu-id="84367-137">Clear the shopping cart.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="84367-138">Для целей этого примера приложения мы вычислим дату отгрузки, просто добавив два дня к текущей дате.</span><span class="sxs-lookup"><span data-stu-id="84367-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="84367-139">Запуск приложения теперь позволит нам протестировать процесс покупки с начала до конца.</span><span class="sxs-lookup"><span data-stu-id="84367-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="84367-140">[Назад](tailspin-spyworks-part-5.md)
> [Вперед](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="84367-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
