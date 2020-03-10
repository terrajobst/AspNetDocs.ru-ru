---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: Часть 6. Создание контроллеров продуктов и заказов | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421290"
---
# <a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="98735-102">Часть 6. Создание контроллеров продуктов и заказов</span><span class="sxs-lookup"><span data-stu-id="98735-102">Part 6: Creating Product and Order Controllers</span></span>

<span data-ttu-id="98735-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="98735-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="98735-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="98735-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="98735-105">Добавление контроллера продуктов</span><span class="sxs-lookup"><span data-stu-id="98735-105">Add a Products Controller</span></span>

<span data-ttu-id="98735-106">Административный контроллер предназначен для пользователей с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="98735-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="98735-107">Клиенты, с другой стороны, могут просматривать продукты, но не могут создавать, обновлять или удалять их.</span><span class="sxs-lookup"><span data-stu-id="98735-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="98735-108">Можно легко ограничить доступ к методам POST, WHERE и DELETE, не открывая методы Get.</span><span class="sxs-lookup"><span data-stu-id="98735-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="98735-109">Но взгляните на данные, возвращаемые для продукта:</span><span class="sxs-lookup"><span data-stu-id="98735-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="98735-110">Свойство `ActualCost` не должно быть видимым для клиентов!</span><span class="sxs-lookup"><span data-stu-id="98735-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="98735-111">Решение заключается в определении *объекта передачи данных* (DTO), который включает подмножество свойств, которые должны быть видимыми для клиентов.</span><span class="sxs-lookup"><span data-stu-id="98735-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="98735-112">Для `ProductDTO` экземпляров мы будем использовать LINQ to Project `Product` Instances.</span><span class="sxs-lookup"><span data-stu-id="98735-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="98735-113">Добавьте класс с именем `ProductDTO` в папку Models.</span><span class="sxs-lookup"><span data-stu-id="98735-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="98735-114">Теперь добавьте контроллер.</span><span class="sxs-lookup"><span data-stu-id="98735-114">Now add the controller.</span></span> <span data-ttu-id="98735-115">В обозреватель решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="98735-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="98735-116">Нажмите кнопку **Добавить**, а затем выберите **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="98735-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="98735-117">В диалоговом окне **Добавление контроллера введите** имя контроллера &quot;продуктсконтроллер&quot;.</span><span class="sxs-lookup"><span data-stu-id="98735-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="98735-118">В разделе **шаблон**выберите **пустой контроллер API**.</span><span class="sxs-lookup"><span data-stu-id="98735-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="98735-119">Замените все в исходном файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="98735-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="98735-120">Контроллер по-прежнему использует `OrdersContext` для запроса к базе данных.</span><span class="sxs-lookup"><span data-stu-id="98735-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="98735-121">Но вместо того, чтобы возвращать экземпляры `Product` напрямую, мы вызываем `MapProducts` для проецирования их на экземпляры `ProductDTO`:</span><span class="sxs-lookup"><span data-stu-id="98735-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="98735-122">Метод `MapProducts` возвращает **IQueryable**, поэтому мы можем составить результат с другими параметрами запроса.</span><span class="sxs-lookup"><span data-stu-id="98735-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="98735-123">Это можно увидеть в методе `GetProduct`, который добавляет к запросу предложение **WHERE** :</span><span class="sxs-lookup"><span data-stu-id="98735-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="98735-124">Добавление контроллера заказов</span><span class="sxs-lookup"><span data-stu-id="98735-124">Add an Orders Controller</span></span>

<span data-ttu-id="98735-125">Затем добавьте контроллер, позволяющий пользователям создавать и просматривать заказы.</span><span class="sxs-lookup"><span data-stu-id="98735-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="98735-126">Мы начнем с другого DTO.</span><span class="sxs-lookup"><span data-stu-id="98735-126">We'll start with another DTO.</span></span> <span data-ttu-id="98735-127">В обозреватель решений щелкните правой кнопкой мыши папку Models и добавьте класс с именем `OrderDTO` использовать следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="98735-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="98735-128">Теперь добавьте контроллер.</span><span class="sxs-lookup"><span data-stu-id="98735-128">Now add the controller.</span></span> <span data-ttu-id="98735-129">В обозреватель решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="98735-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="98735-130">Нажмите кнопку **Добавить**, а затем выберите **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="98735-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="98735-131">В диалоговом окне **Добавление контроллера** задайте следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="98735-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="98735-132">В разделе **имя контроллера**введите "ордерсконтроллер".</span><span class="sxs-lookup"><span data-stu-id="98735-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="98735-133">В разделе **шаблон**выберите "контроллер API с действиями чтения и записи, используя Entity Framework".</span><span class="sxs-lookup"><span data-stu-id="98735-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="98735-134">В разделе **класс модели**выберите&quot;порядок &quot;(Продуктсторе. Models).</span><span class="sxs-lookup"><span data-stu-id="98735-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="98735-135">В разделе **класс контекста данных**выберите &quot;Ордерсконтекст (Продуктсторе. Models)&quot;.</span><span class="sxs-lookup"><span data-stu-id="98735-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="98735-136">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="98735-136">Click **Add**.</span></span> <span data-ttu-id="98735-137">При этом добавляется файл с именем OrdersController.cs.</span><span class="sxs-lookup"><span data-stu-id="98735-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="98735-138">Далее необходимо изменить реализацию контроллера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="98735-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="98735-139">Сначала удалите методы `PutOrder` и `DeleteOrder`.</span><span class="sxs-lookup"><span data-stu-id="98735-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="98735-140">В этом примере клиенты не могут изменять или удалять существующие заказы.</span><span class="sxs-lookup"><span data-stu-id="98735-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="98735-141">В реальных приложениях для обработки таких случаев потребуется много серверной логики.</span><span class="sxs-lookup"><span data-stu-id="98735-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="98735-142">(Например, был ли уже отгружен заказ?)</span><span class="sxs-lookup"><span data-stu-id="98735-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="98735-143">Измените метод `GetOrders`, чтобы возвращались только заказы, принадлежащие пользователю.</span><span class="sxs-lookup"><span data-stu-id="98735-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="98735-144">Измените метод `GetOrder` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="98735-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="98735-145">Ниже приведены изменения, внесенные в метод.</span><span class="sxs-lookup"><span data-stu-id="98735-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="98735-146">Возвращаемое значение — это `OrderDTO` экземпляр, а не `Order`.</span><span class="sxs-lookup"><span data-stu-id="98735-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="98735-147">При запросе базы данных для заказа мы используем метод [дбкуери. include](https://msdn.microsoft.com/library/gg696395) для получения связанных `OrderDetail` и `Product` сущностей.</span><span class="sxs-lookup"><span data-stu-id="98735-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="98735-148">Мы будем сводить результаты с помощью проекции.</span><span class="sxs-lookup"><span data-stu-id="98735-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="98735-149">HTTP-ответ будет содержать массив продуктов с количествами:</span><span class="sxs-lookup"><span data-stu-id="98735-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="98735-150">Этот формат легче использовать для клиентов, чем исходный граф объектов, который содержит вложенные сущности (Order, Details и Products).</span><span class="sxs-lookup"><span data-stu-id="98735-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="98735-151">Последний метод, который следует рассмотреть `PostOrder`.</span><span class="sxs-lookup"><span data-stu-id="98735-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="98735-152">Сейчас этот метод принимает `Order` экземпляр.</span><span class="sxs-lookup"><span data-stu-id="98735-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="98735-153">Но рассмотрим, что произойдет, если клиент отправляет текст запроса следующим образом:</span><span class="sxs-lookup"><span data-stu-id="98735-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="98735-154">Это хорошо структурированный порядок, который Entity Framework, в своюмся случае, будет куда-то вставить в базу данных.</span><span class="sxs-lookup"><span data-stu-id="98735-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="98735-155">Но она содержит сущность Product, которая ранее не существовала.</span><span class="sxs-lookup"><span data-stu-id="98735-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="98735-156">Клиент только что создал новый продукт в нашей базе данных!</span><span class="sxs-lookup"><span data-stu-id="98735-156">The client just created a new product in our database!</span></span> <span data-ttu-id="98735-157">Это будет неожиданным для отдела выполнения заказов, когда он увидит заказ на Koala.</span><span class="sxs-lookup"><span data-stu-id="98735-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="98735-158">Мораль — это, по сути, тщательный анализ данных, принимаемых в запросе POST или Request.</span><span class="sxs-lookup"><span data-stu-id="98735-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="98735-159">Чтобы избежать этой проблемы, измените метод `PostOrder` для получения экземпляра `OrderDTO`.</span><span class="sxs-lookup"><span data-stu-id="98735-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="98735-160">Для создания `Order`используйте `OrderDTO`.</span><span class="sxs-lookup"><span data-stu-id="98735-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="98735-161">Обратите внимание, что мы используем свойства `ProductID` и `Quantity` и будем пропускать все значения, отправленные клиентом по названию или цене продукта.</span><span class="sxs-lookup"><span data-stu-id="98735-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="98735-162">Если идентификатор продукта недействителен, он нарушает ограничение внешнего ключа в базе данных, и вставка завершится ошибкой, как это должно произойти.</span><span class="sxs-lookup"><span data-stu-id="98735-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="98735-163">Ниже приведен полный метод `PostOrder`.</span><span class="sxs-lookup"><span data-stu-id="98735-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="98735-164">Наконец, добавьте к контроллеру атрибут **авторизации** :</span><span class="sxs-lookup"><span data-stu-id="98735-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="98735-165">Теперь только зарегистрированные пользователи могут создавать или просматривать заказы.</span><span class="sxs-lookup"><span data-stu-id="98735-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="98735-166">[Назад](using-web-api-with-entity-framework-part-5.md)
> [Вперед](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="98735-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
