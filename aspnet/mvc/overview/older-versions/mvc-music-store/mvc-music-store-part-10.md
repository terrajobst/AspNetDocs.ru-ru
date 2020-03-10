---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: Часть 10. окончательные обновления структуры навигации и сайта, заключение | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. Часть 10 охватывает Финальные обновления для навигации и S...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433614"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="31b7d-104">Часть 10. окончательные обновления навигации и дизайна сайта, заключение</span><span class="sxs-lookup"><span data-stu-id="31b7d-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>

<span data-ttu-id="31b7d-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="31b7d-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="31b7d-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="31b7d-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="31b7d-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="31b7d-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="31b7d-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="31b7d-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="31b7d-109">В части 10 описаны Финальные обновления навигации и дизайна узла, заключение.</span><span class="sxs-lookup"><span data-stu-id="31b7d-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>

<span data-ttu-id="31b7d-110">Мы выполнили все основные функции нашего сайта, но у нас по-прежнему есть некоторые функции для добавления в навигацию по сайту, домашнюю страницу и страницу обзора магазина.</span><span class="sxs-lookup"><span data-stu-id="31b7d-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="31b7d-111">Создание частичного представления сводки корзины для покупок</span><span class="sxs-lookup"><span data-stu-id="31b7d-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="31b7d-112">Мы хотим предоставить количество элементов в корзине для покупок пользователя на всем сайте.</span><span class="sxs-lookup"><span data-stu-id="31b7d-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="31b7d-113">Это можно легко реализовать, создав частичное представление, которое добавляется к нашему сайту site. master.</span><span class="sxs-lookup"><span data-stu-id="31b7d-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="31b7d-114">Как показано выше, контроллер ShoppingCart включает метод действия Картсуммари, который возвращает частичное представление:</span><span class="sxs-lookup"><span data-stu-id="31b7d-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="31b7d-115">Чтобы создать частичное представление Картсуммари, щелкните правой кнопкой мыши папку Views/ShoppingCart и выберите Добавить представление.</span><span class="sxs-lookup"><span data-stu-id="31b7d-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="31b7d-116">Назовите представление Картсуммари и установите флажок "создать частичное представление", как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="31b7d-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="31b7d-117">Частичное представление Картсуммари — это просто ссылка на представление индекса ShoppingCart, показывающее количество элементов в корзине.</span><span class="sxs-lookup"><span data-stu-id="31b7d-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="31b7d-118">Полный код для Картсуммари. cshtml выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31b7d-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="31b7d-119">Можно включить частичное представление на любую страницу сайта, включая главный узел, с помощью метода HTML. RenderAction.</span><span class="sxs-lookup"><span data-stu-id="31b7d-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="31b7d-120">RenderAction требует указать имя действия ("Картсуммари") и имя контроллера ("ShoppingCart"), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="31b7d-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="31b7d-121">Перед добавлением этого элемента в макет сайта мы также создадим меню жанр, чтобы мы могли сделать все наши веб-узлы. master Updates в один момент времени.</span><span class="sxs-lookup"><span data-stu-id="31b7d-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="31b7d-122">Создание частичного представления меню жанра</span><span class="sxs-lookup"><span data-stu-id="31b7d-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="31b7d-123">Мы можем сделать так, чтобы наши пользователи могли перемещаться по магазину, добавляя меню жанра, в котором перечислены все жанры, доступные в нашем магазине.</span><span class="sxs-lookup"><span data-stu-id="31b7d-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="31b7d-124">Мы выполняйте те же действия, а также создадите частичное представление Женремену, после чего мы можем добавить их в главную страницу.</span><span class="sxs-lookup"><span data-stu-id="31b7d-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="31b7d-125">Сначала добавьте следующее действие контроллера Женремену в Стореконтроллер:</span><span class="sxs-lookup"><span data-stu-id="31b7d-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="31b7d-126">Это действие возвращает список жанров, которые будут отображаться в частичном представлении, которое будет создано далее.</span><span class="sxs-lookup"><span data-stu-id="31b7d-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="31b7d-127">*Примечание. Мы добавили атрибут [Чилдактиононли] к этому действию контроллера, что означает, что мы хотим, чтобы это действие было использовано только из частичного представления. Этот атрибут предотвратит выполнение действия контроллера, перейдя к/Сторе/женремену. Это не требуется для частичных представлений, но рекомендуется, поскольку мы хотим убедиться, что наши действия контроллера используются, как мы планируем. Мы также возвращаем Партиалвиев, а не View, что позволяет обработчику представлений не использовать макет для этого представления, так как он включается в другие представления.*</span><span class="sxs-lookup"><span data-stu-id="31b7d-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="31b7d-128">Щелкните действие контроллера Женремену правой кнопкой мыши и создайте частичное представление с именем Женремену, которое строго типизировано с помощью класса данных для представления жанра, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="31b7d-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="31b7d-129">Обновите код представления для частичного представления Женремену, чтобы отобразить элементы с помощью неупорядоченного списка, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="31b7d-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="31b7d-130">Обновление макета сайта для отображения наших частичных представлений</span><span class="sxs-lookup"><span data-stu-id="31b7d-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="31b7d-131">Мы можем добавить наши частичные представления в макет узла (/Виевс/Шаред/\_Layout. cshtml), вызвав HTML. RenderAction ().</span><span class="sxs-lookup"><span data-stu-id="31b7d-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="31b7d-132">Мы добавим их как в, так и в дополнительной разметке для отображения их, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="31b7d-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="31b7d-133">Теперь, когда мы запускаем приложение, мы увидим жанр в левой области навигации и сводку по корзине вверху.</span><span class="sxs-lookup"><span data-stu-id="31b7d-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="31b7d-134">Обновление страницы обзора магазина</span><span class="sxs-lookup"><span data-stu-id="31b7d-134">Update to the Store Browse page</span></span>

<span data-ttu-id="31b7d-135">Страница обзора хранилища является функциональной, но она не выглядит очень хорошо.</span><span class="sxs-lookup"><span data-stu-id="31b7d-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="31b7d-136">Мы можем обновить страницу, чтобы отобразить альбомы в более качественном макете, обновив код представления (в/Виевс/Сторе/бровсе.кштмл) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31b7d-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="31b7d-137">Здесь мы используем URL-адрес. Action, а не HTML. ActionLink, чтобы мы могли применить к ссылке специальное форматирование, включающее иллюстрацию альбома.</span><span class="sxs-lookup"><span data-stu-id="31b7d-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="31b7d-138">*Примечание. для этих альбомов выводится универсальная Обложка альбома. Эти сведения хранятся в базе данных и редактируются с помощью диспетчера магазинов. Вы можете добавить собственную иллюстрацию.*</span><span class="sxs-lookup"><span data-stu-id="31b7d-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="31b7d-139">Теперь, когда мы перейдем по жанру, мы увидим альбомы, показанные в сетке с иллюстрациями альбома.</span><span class="sxs-lookup"><span data-stu-id="31b7d-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="31b7d-140">Обновление домашней страницы для отображения лучших продаваемых альбомов</span><span class="sxs-lookup"><span data-stu-id="31b7d-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="31b7d-141">Мы хотим приподняться к нашим лучшим альбомам на домашней странице, чтобы увеличить объем продаж.</span><span class="sxs-lookup"><span data-stu-id="31b7d-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="31b7d-142">Мы сделаем некоторые обновления для нашего HomeController, чтобы справиться с этим, а также добавили дополнительные графические изображения.</span><span class="sxs-lookup"><span data-stu-id="31b7d-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="31b7d-143">Во-первых, мы добавим свойство навигации в наш класс «альбом», чтобы EntityFramework знать, что они связаны.</span><span class="sxs-lookup"><span data-stu-id="31b7d-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="31b7d-144">Последние несколько строк нашего класса **альбома** теперь должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31b7d-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="31b7d-145">*Примечание. для этого потребуется добавить оператор using для переноса в пространство имен System. Collections. Generic.*</span><span class="sxs-lookup"><span data-stu-id="31b7d-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="31b7d-146">Сначала мы добавим поля Сторедб и Мвкмусиксторе. Models с помощью инструкций, как в других контроллерах.</span><span class="sxs-lookup"><span data-stu-id="31b7d-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="31b7d-147">Далее мы добавим следующий метод в HomeController, который запрашивает нашу базу данных для поиска лучших в продаже альбомов в соответствии с OrderDetails.</span><span class="sxs-lookup"><span data-stu-id="31b7d-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="31b7d-148">Это частный метод, так как мы не хотим сделать его доступным в качестве действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="31b7d-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="31b7d-149">Мы используем его в HomeController для простоты, но при необходимости рекомендуется переместить бизнес-логику в отдельные классы служб.</span><span class="sxs-lookup"><span data-stu-id="31b7d-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="31b7d-150">Теперь мы можем обновить действие контроллера индекса, чтобы запросить пять лучших альбомов и вернуть их в представление.</span><span class="sxs-lookup"><span data-stu-id="31b7d-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="31b7d-151">Полный код для обновленного HomeController показан ниже.</span><span class="sxs-lookup"><span data-stu-id="31b7d-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="31b7d-152">Наконец, необходимо обновить представление домашнего индекса таким образом, чтобы он мог отобразить список альбомов, обновив тип модели и добавив список альбомов в нижнюю часть.</span><span class="sxs-lookup"><span data-stu-id="31b7d-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="31b7d-153">Эта возможность также будет использоваться для добавления заголовка и раздела продвижения на страницу.</span><span class="sxs-lookup"><span data-stu-id="31b7d-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="31b7d-154">Теперь, когда мы запустим приложение, мы увидим обновленную домашнюю страницу с помощью самых популярных альбомов и нашего рекламного сообщения.</span><span class="sxs-lookup"><span data-stu-id="31b7d-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="31b7d-155">Заключение</span><span class="sxs-lookup"><span data-stu-id="31b7d-155">Conclusion</span></span>

<span data-ttu-id="31b7d-156">Мы увидели, что ASP.NET MVC упрощает создание сложного веб-сайта с доступом к базе данных, членством, AJAX и т. д.</span><span class="sxs-lookup"><span data-stu-id="31b7d-156">We've seen that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="31b7d-157">очень быстро.</span><span class="sxs-lookup"><span data-stu-id="31b7d-157">pretty quickly.</span></span> <span data-ttu-id="31b7d-158">Надеюсь, в этом учебнике были предоставлены средства, необходимые для начала создания собственных приложений ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="31b7d-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="31b7d-159">Назад</span><span class="sxs-lookup"><span data-stu-id="31b7d-159">Previous</span></span>](mvc-music-store-part-9.md)
