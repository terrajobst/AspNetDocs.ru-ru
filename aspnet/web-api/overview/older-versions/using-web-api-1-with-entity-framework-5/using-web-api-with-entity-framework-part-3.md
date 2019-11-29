---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: Часть 3. Создание административного контроллера | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600043"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="b2143-102">Часть 3. Создание административного контроллера</span><span class="sxs-lookup"><span data-stu-id="b2143-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="b2143-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b2143-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b2143-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="b2143-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="b2143-105">Добавление контроллера администратора</span><span class="sxs-lookup"><span data-stu-id="b2143-105">Add an Admin Controller</span></span>

<span data-ttu-id="b2143-106">В этом разделе мы добавим контроллер веб-API, который поддерживает операции CRUD (создание, чтение, обновление и удаление) для продуктов.</span><span class="sxs-lookup"><span data-stu-id="b2143-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="b2143-107">Контроллер будет использовать Entity Framework для взаимодействия с уровнем базы данных.</span><span class="sxs-lookup"><span data-stu-id="b2143-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="b2143-108">Только администраторы смогут использовать этот контроллер.</span><span class="sxs-lookup"><span data-stu-id="b2143-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="b2143-109">Клиенты будут получать доступ к продуктам через другой контроллер.</span><span class="sxs-lookup"><span data-stu-id="b2143-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="b2143-110">В обозреватель решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="b2143-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="b2143-111">Выберите **Добавить** , а затем — **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="b2143-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="b2143-112">В диалоговом окне **Добавление контроллера введите** имя контроллера `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="b2143-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="b2143-113">В разделе **шаблон**выберите &quot;контроллер API с действиями чтения и записи, используя Entity Framework&quot;.</span><span class="sxs-lookup"><span data-stu-id="b2143-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="b2143-114">В разделе **класс модели**выберите "продукт (Продуктсторе. Models)".</span><span class="sxs-lookup"><span data-stu-id="b2143-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="b2143-115">В разделе **контекст данных**выберите "&lt;новый контекст данных&gt;".</span><span class="sxs-lookup"><span data-stu-id="b2143-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="b2143-116">Если в раскрывающемся списке **класс модели** не отображаются классы модели, убедитесь, что проект скомпилирован.</span><span class="sxs-lookup"><span data-stu-id="b2143-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="b2143-117">Entity Framework использует отражение, поэтому ему требуется скомпилированная сборка.</span><span class="sxs-lookup"><span data-stu-id="b2143-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>

<span data-ttu-id="b2143-118">Если выбрать команду "&lt;создать контекст данных&gt;", откроется диалоговое окно " **Создание контекста данных** ".</span><span class="sxs-lookup"><span data-stu-id="b2143-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="b2143-119">Назовите `ProductStore.Models.OrdersContext`контекста данных.</span><span class="sxs-lookup"><span data-stu-id="b2143-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="b2143-120">Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **новый контекст данных** .</span><span class="sxs-lookup"><span data-stu-id="b2143-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="b2143-121">В диалоговом окне **Добавление контроллера** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b2143-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="b2143-122">Вот что было добавлено в проект:</span><span class="sxs-lookup"><span data-stu-id="b2143-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="b2143-123">Класс с именем `OrdersContext`, производный от **DbContext**.</span><span class="sxs-lookup"><span data-stu-id="b2143-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="b2143-124">Этот класс обеспечивает привязывание между моделями POCO и базой данных.</span><span class="sxs-lookup"><span data-stu-id="b2143-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="b2143-125">Контроллер веб-API с именем `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="b2143-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="b2143-126">Этот контроллер поддерживает операции CRUD на экземплярах `Product`.</span><span class="sxs-lookup"><span data-stu-id="b2143-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="b2143-127">Для взаимодействия с Entity Frameworkом используется класс `OrdersContext`.</span><span class="sxs-lookup"><span data-stu-id="b2143-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="b2143-128">Новая строка подключения к базе данных в файле Web. config.</span><span class="sxs-lookup"><span data-stu-id="b2143-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="b2143-129">Откройте файл OrdersContext.cs.</span><span class="sxs-lookup"><span data-stu-id="b2143-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="b2143-130">Обратите внимание, что конструктор задает имя строки подключения к базе данных.</span><span class="sxs-lookup"><span data-stu-id="b2143-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="b2143-131">Это имя относится к строке подключения, которая была добавлена в файл Web. config.</span><span class="sxs-lookup"><span data-stu-id="b2143-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="b2143-132">Добавьте в класс `OrdersContext` следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="b2143-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="b2143-133">**DbSet** представляет набор сущностей, которые можно запросить.</span><span class="sxs-lookup"><span data-stu-id="b2143-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="b2143-134">Ниже приведен полный список для класса `OrdersContext`.</span><span class="sxs-lookup"><span data-stu-id="b2143-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="b2143-135">Класс `AdminController` определяет пять методов, реализующих базовую функциональность CRUD.</span><span class="sxs-lookup"><span data-stu-id="b2143-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="b2143-136">Каждый метод соответствует URI, который может быть вызван клиентом:</span><span class="sxs-lookup"><span data-stu-id="b2143-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="b2143-137">Метод контроллера</span><span class="sxs-lookup"><span data-stu-id="b2143-137">Controller Method</span></span> | <span data-ttu-id="b2143-138">Описание</span><span class="sxs-lookup"><span data-stu-id="b2143-138">Description</span></span> | <span data-ttu-id="b2143-139">URI</span><span class="sxs-lookup"><span data-stu-id="b2143-139">URI</span></span> | <span data-ttu-id="b2143-140">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="b2143-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2143-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="b2143-141">GetProducts</span></span> | <span data-ttu-id="b2143-142">Возвращает все продукты.</span><span class="sxs-lookup"><span data-stu-id="b2143-142">Gets all products.</span></span> | <span data-ttu-id="b2143-143">API и продукты</span><span class="sxs-lookup"><span data-stu-id="b2143-143">api/products</span></span> | <span data-ttu-id="b2143-144">GET</span><span class="sxs-lookup"><span data-stu-id="b2143-144">GET</span></span> |
| <span data-ttu-id="b2143-145">Продукт</span><span class="sxs-lookup"><span data-stu-id="b2143-145">GetProduct</span></span> | <span data-ttu-id="b2143-146">Находит продукт по ИДЕНТИФИКАТОРу.</span><span class="sxs-lookup"><span data-stu-id="b2143-146">Finds a product by ID.</span></span> | <span data-ttu-id="b2143-147">API/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="b2143-147">api/products/*id*</span></span> | <span data-ttu-id="b2143-148">GET</span><span class="sxs-lookup"><span data-stu-id="b2143-148">GET</span></span> |
| <span data-ttu-id="b2143-149">путпродукт</span><span class="sxs-lookup"><span data-stu-id="b2143-149">PutProduct</span></span> | <span data-ttu-id="b2143-150">Обновляет продукт.</span><span class="sxs-lookup"><span data-stu-id="b2143-150">Updates a product.</span></span> | <span data-ttu-id="b2143-151">API/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="b2143-151">api/products/*id*</span></span> | <span data-ttu-id="b2143-152">PUT</span><span class="sxs-lookup"><span data-stu-id="b2143-152">PUT</span></span> |
| <span data-ttu-id="b2143-153">Продукт</span><span class="sxs-lookup"><span data-stu-id="b2143-153">PostProduct</span></span> | <span data-ttu-id="b2143-154">Создает новый продукт.</span><span class="sxs-lookup"><span data-stu-id="b2143-154">Creates a new product.</span></span> | <span data-ttu-id="b2143-155">API и продукты</span><span class="sxs-lookup"><span data-stu-id="b2143-155">api/products</span></span> | <span data-ttu-id="b2143-156">ПОМЕСТИТЬ</span><span class="sxs-lookup"><span data-stu-id="b2143-156">POST</span></span> |
| <span data-ttu-id="b2143-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="b2143-157">DeleteProduct</span></span> | <span data-ttu-id="b2143-158">Удаляет продукт.</span><span class="sxs-lookup"><span data-stu-id="b2143-158">Deletes a product.</span></span> | <span data-ttu-id="b2143-159">API/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="b2143-159">api/products/*id*</span></span> | <span data-ttu-id="b2143-160">DELETE</span><span class="sxs-lookup"><span data-stu-id="b2143-160">DELETE</span></span> |

<span data-ttu-id="b2143-161">Каждый метод вызывает `OrdersContext` для запроса к базе данных.</span><span class="sxs-lookup"><span data-stu-id="b2143-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="b2143-162">Методы, которые изменяют вызов метода Collection (размещение, публикация и удаление), `db.SaveChanges`, чтобы сохранить изменения в базе данных.</span><span class="sxs-lookup"><span data-stu-id="b2143-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="b2143-163">Контроллеры создаются для каждого HTTP-запроса, а затем удаляются, поэтому необходимо сохранить изменения перед возвратом метода.</span><span class="sxs-lookup"><span data-stu-id="b2143-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="b2143-164">Добавление инициализатора базы данных</span><span class="sxs-lookup"><span data-stu-id="b2143-164">Add a Database Initializer</span></span>

<span data-ttu-id="b2143-165">Entity Framework имеет удобную функцию, позволяющую заполнять базу данных при запуске, а также автоматически воссоздавать базу данных при каждом изменении моделей.</span><span class="sxs-lookup"><span data-stu-id="b2143-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="b2143-166">Эта функция полезна во время разработки, поскольку у вас всегда есть тестовые данные даже при изменении моделей.</span><span class="sxs-lookup"><span data-stu-id="b2143-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="b2143-167">В обозреватель решений щелкните правой кнопкой мыши папку Models и создайте новый класс с именем `OrdersContextInitializer`.</span><span class="sxs-lookup"><span data-stu-id="b2143-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="b2143-168">Вставьте следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="b2143-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="b2143-169">Наследуя класс **дропкреатедатабасеифмоделчанжес** , мы сообщаем Entity Framework удалить базу данных при изменении классов модели.</span><span class="sxs-lookup"><span data-stu-id="b2143-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="b2143-170">Когда Entity Framework создает (или повторно создает) базу данных, она вызывает метод **SEED** для заполнения таблиц.</span><span class="sxs-lookup"><span data-stu-id="b2143-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="b2143-171">Мы используем метод **SEED** для добавления примеров продуктов, а также пример порядка.</span><span class="sxs-lookup"><span data-stu-id="b2143-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="b2143-172">Эта функция отлично подходит для тестирования, но не использует класс **дропкреатедатабасеифмоделчанжес** в рабочей среде, так как вы можете потерять данные, если кто-то изменил класс модели.</span><span class="sxs-lookup"><span data-stu-id="b2143-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="b2143-173">Затем откройте Global. asax и добавьте следующий код в метод **\_запуска приложения** :</span><span class="sxs-lookup"><span data-stu-id="b2143-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="b2143-174">Отправка запроса контроллеру</span><span class="sxs-lookup"><span data-stu-id="b2143-174">Send a Request to the Controller</span></span>

<span data-ttu-id="b2143-175">На этом этапе мы не написали код клиента, но веб-API можно вызвать с помощью веб-браузера или средства отладки HTTP, такого как [Fiddler](http://www.fiddler2.com/fiddler2/).</span><span class="sxs-lookup"><span data-stu-id="b2143-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="b2143-176">В Visual Studio нажмите клавишу F5, чтобы начать отладку.</span><span class="sxs-lookup"><span data-stu-id="b2143-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="b2143-177">Веб-браузер откроется в `http://localhost:*portnum*/`, где *портнум* — это номер порта.</span><span class="sxs-lookup"><span data-stu-id="b2143-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="b2143-178">Отправка HTTP-запроса в "`http://localhost:*portnum*/api/admin`.</span><span class="sxs-lookup"><span data-stu-id="b2143-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="b2143-179">Первый запрос может быть слишком большим, так как Entity Framework необходимо создать и заполнить базу данных.</span><span class="sxs-lookup"><span data-stu-id="b2143-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="b2143-180">Ответ должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b2143-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="b2143-181">[Назад](using-web-api-with-entity-framework-part-2.md)
> [Вперед](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="b2143-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
