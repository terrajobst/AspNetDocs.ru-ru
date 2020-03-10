---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: Часть 7. Создание главной страницы | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484452"
---
# <a name="part-7-creating-the-main-page"></a><span data-ttu-id="fd26a-102">Часть 7. Создание главной страницы</span><span class="sxs-lookup"><span data-stu-id="fd26a-102">Part 7: Creating the Main Page</span></span>

<span data-ttu-id="fd26a-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fd26a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="fd26a-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="fd26a-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="fd26a-105">Создание главной страницы</span><span class="sxs-lookup"><span data-stu-id="fd26a-105">Creating the Main Page</span></span>

<span data-ttu-id="fd26a-106">В этом разделе вы создадите страницу основного приложения.</span><span class="sxs-lookup"><span data-stu-id="fd26a-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="fd26a-107">Эта страница будет более сложной, чем страница администрирования, поэтому мы будем использовать ее в нескольких шагах.</span><span class="sxs-lookup"><span data-stu-id="fd26a-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="fd26a-108">Кстати, вы увидите некоторые более сложные методы маскирования. js.</span><span class="sxs-lookup"><span data-stu-id="fd26a-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="fd26a-109">Вот базовый макет страницы:</span><span class="sxs-lookup"><span data-stu-id="fd26a-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="fd26a-110">"Products" содержит массив продуктов.</span><span class="sxs-lookup"><span data-stu-id="fd26a-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="fd26a-111">"Корзина" содержит массив продуктов с количествами.</span><span class="sxs-lookup"><span data-stu-id="fd26a-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="fd26a-112">При выборе пункта "добавить в корзину" обновляется корзина.</span><span class="sxs-lookup"><span data-stu-id="fd26a-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="fd26a-113">"Orders" содержит массив идентификаторов заказов.</span><span class="sxs-lookup"><span data-stu-id="fd26a-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="fd26a-114">"Details" содержит сведения о заказе — массив элементов (продукты с количествами).</span><span class="sxs-lookup"><span data-stu-id="fd26a-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="fd26a-115">Начнем с определения базовой структуры в формате HTML без привязки данных или скрипта.</span><span class="sxs-lookup"><span data-stu-id="fd26a-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="fd26a-116">Откройте файл Views/Home/Index. cshtml и замените все содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="fd26a-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="fd26a-117">Затем добавьте раздел Scripts и создайте пустую модель представления:</span><span class="sxs-lookup"><span data-stu-id="fd26a-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="fd26a-118">В зависимости от проекта, разработанного ранее, нашей модели представления требуется observable для продуктов, корзин, заказов и сведений.</span><span class="sxs-lookup"><span data-stu-id="fd26a-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="fd26a-119">Добавьте следующие переменные в объект `AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="fd26a-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="fd26a-120">Пользователи могут добавлять элементы из списка продуктов в корзину и удалять элементы из корзины.</span><span class="sxs-lookup"><span data-stu-id="fd26a-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="fd26a-121">Чтобы инкапсулировать эти функции, мы создадим еще один класс представления — модель, представляющий продукт.</span><span class="sxs-lookup"><span data-stu-id="fd26a-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="fd26a-122">Добавьте следующий код в `AppViewModel`.</span><span class="sxs-lookup"><span data-stu-id="fd26a-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="fd26a-123">Класс `ProductViewModel` содержит две функции, которые используются для перемещения продукта в корзину и из нее: `addItemToCart` добавляет одну единицу продукта в корзину и `removeAllFromCart` удаляет все количества продуктов.</span><span class="sxs-lookup"><span data-stu-id="fd26a-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="fd26a-124">Пользователи могут выбрать существующий заказ и получить сведения о заказе.</span><span class="sxs-lookup"><span data-stu-id="fd26a-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="fd26a-125">Мы будем инкапсулировать эту функцию в другую модель представления:</span><span class="sxs-lookup"><span data-stu-id="fd26a-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="fd26a-126">`OrderDetailsViewModel` инициализируется заказом и извлекает сведения о заказе путем отправки запроса AJAX на сервер.</span><span class="sxs-lookup"><span data-stu-id="fd26a-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="fd26a-127">Кроме того, обратите внимание на свойство `total` в `OrderDetailsViewModel`.</span><span class="sxs-lookup"><span data-stu-id="fd26a-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="fd26a-128">Это свойство является особым видом наблюдаемого, называемого [вычисленным наблюдаемым](http://knockoutjs.com/documentation/computedObservables.html).</span><span class="sxs-lookup"><span data-stu-id="fd26a-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="fd26a-129">Как следует из названия, вычисленный наблюдаемый объект позволяет выполнить привязку данных к вычисленному значению&#8212;в данном случае, а также к общей стоимости заказа.</span><span class="sxs-lookup"><span data-stu-id="fd26a-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="fd26a-130">Затем добавьте эти функции в `AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="fd26a-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="fd26a-131">`resetCart` удаляет все элементы из корзины.</span><span class="sxs-lookup"><span data-stu-id="fd26a-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="fd26a-132">`getDetails` получает сведения о заказе (путем помещения нового `OrderDetailsViewModel` в список `details`).</span><span class="sxs-lookup"><span data-stu-id="fd26a-132">`getDetails` gets the details for an order (by pushing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="fd26a-133">`createOrder` создает новый заказ и очищает корзину.</span><span class="sxs-lookup"><span data-stu-id="fd26a-133">`createOrder` creates a new order and empties the cart.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="fd26a-134">Наконец, инициализируйте модель представления, делая запросы AJAX для продуктов и заказов:</span><span class="sxs-lookup"><span data-stu-id="fd26a-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="fd26a-135">Ладно, это большой объем кода, но мы создали его пошаговым образом, поэтому будем надеяться, что проектирование ясно.</span><span class="sxs-lookup"><span data-stu-id="fd26a-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="fd26a-136">Теперь к HTML можно добавить несколько привязок маскирования. js.</span><span class="sxs-lookup"><span data-stu-id="fd26a-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="fd26a-137">**Продукты**</span><span class="sxs-lookup"><span data-stu-id="fd26a-137">**Products**</span></span>

<span data-ttu-id="fd26a-138">Ниже приведены привязки для списка продуктов.</span><span class="sxs-lookup"><span data-stu-id="fd26a-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="fd26a-139">Это перебирает массив Products и отображает имя и цену.</span><span class="sxs-lookup"><span data-stu-id="fd26a-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="fd26a-140">Кнопка "добавить в порядок" отображается только в том случае, если пользователь вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="fd26a-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="fd26a-141">Кнопка "добавить в заказ" вызывает `addItemToCart` в экземпляре `ProductViewModel` для продукта.</span><span class="sxs-lookup"><span data-stu-id="fd26a-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="fd26a-142">Это демонстрирует удобную функцию файла выколачивание. js: когда модель представления содержит другие модели представления, можно применить привязки к внутренней модели.</span><span class="sxs-lookup"><span data-stu-id="fd26a-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="fd26a-143">В этом примере привязки в `foreach` применяются к каждому из экземпляров `ProductViewModel`.</span><span class="sxs-lookup"><span data-stu-id="fd26a-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="fd26a-144">Этот подход намного более понятен, чем помещение всех функциональных возможностей в одну модель представления.</span><span class="sxs-lookup"><span data-stu-id="fd26a-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="fd26a-145">**Покупатель**</span><span class="sxs-lookup"><span data-stu-id="fd26a-145">**Cart**</span></span>

<span data-ttu-id="fd26a-146">Ниже приведены привязки для корзины.</span><span class="sxs-lookup"><span data-stu-id="fd26a-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="fd26a-147">Это перебирает массив корзины и отображает имя, цену и количество.</span><span class="sxs-lookup"><span data-stu-id="fd26a-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="fd26a-148">Обратите внимание, что ссылка "Удалить" и кнопка "создать заказ" привязаны к функциям модели представления.</span><span class="sxs-lookup"><span data-stu-id="fd26a-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="fd26a-149">**Перемещен**</span><span class="sxs-lookup"><span data-stu-id="fd26a-149">**Orders**</span></span>

<span data-ttu-id="fd26a-150">Ниже приведены привязки для списка Orders:</span><span class="sxs-lookup"><span data-stu-id="fd26a-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="fd26a-151">Будет выполнена итерация по заказам и показан идентификатор заказа.</span><span class="sxs-lookup"><span data-stu-id="fd26a-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="fd26a-152">Событие щелчка по ссылке привязано к функции `getDetails`.</span><span class="sxs-lookup"><span data-stu-id="fd26a-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="fd26a-153">**Сведения о заказе**</span><span class="sxs-lookup"><span data-stu-id="fd26a-153">**Order Details**</span></span>

<span data-ttu-id="fd26a-154">Ниже приведены привязки для сведений о заказе.</span><span class="sxs-lookup"><span data-stu-id="fd26a-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="fd26a-155">Это перебирает элементы в порядке и отображает продукт, цену и количество.</span><span class="sxs-lookup"><span data-stu-id="fd26a-155">This iterates over the items in the order and displays the product, price, and quantity.</span></span> <span data-ttu-id="fd26a-156">Окружающий элемент DIV отображается только в том случае, если массив Details содержит один или несколько элементов.</span><span class="sxs-lookup"><span data-stu-id="fd26a-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="fd26a-157">Заключение</span><span class="sxs-lookup"><span data-stu-id="fd26a-157">Conclusion</span></span>

<span data-ttu-id="fd26a-158">В этом руководстве вы создали приложение, которое использует Entity Framework для взаимодействия с базой данных и веб-API ASP.NET для предоставления общедоступного интерфейса поверх уровня данных.</span><span class="sxs-lookup"><span data-stu-id="fd26a-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="fd26a-159">Мы используем ASP.NET MVC 4 для подготовки к просмотру страниц HTML, а также маскирования. js Plus jQuery, чтобы обеспечить динамическое взаимодействие без перегрузок страниц.</span><span class="sxs-lookup"><span data-stu-id="fd26a-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="fd26a-160">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="fd26a-160">Additional resources:</span></span>

- [<span data-ttu-id="fd26a-161">Схема содержимого ASP.NET доступа к данным</span><span class="sxs-lookup"><span data-stu-id="fd26a-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="fd26a-162">Центр разработчиков Entity Framework</span><span class="sxs-lookup"><span data-stu-id="fd26a-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="fd26a-163">Назад</span><span class="sxs-lookup"><span data-stu-id="fd26a-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
