---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: Включение операций CRUD в ASP.NET веб-API 1 | Документация Майкрософт
author: MikeWasson
description: Этом руководстве показано, как для поддержки операций CRUD в HTTP-службу с помощью веб-API ASP.NET. Версии программного обеспечения, используемые в учебника по Visual Studio 2012 Web AP...
ms.author: riande
ms.date: 01/28/2012
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: f3cb0004075ef7687ca1096bd407c342b4d0b7be
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423759"
---
<a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="6ff4e-104">Включение операций CRUD в ASP.NET веб-API 1</span><span class="sxs-lookup"><span data-stu-id="6ff4e-104">Enabling CRUD Operations in ASP.NET Web API 1</span></span>
====================
<span data-ttu-id="6ff4e-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6ff4e-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6ff4e-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="6ff4e-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="6ff4e-107">Этом руководстве показано, как для поддержки операций CRUD в HTTP-службу с помощью веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-107">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6ff4e-108">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="6ff4e-108">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6ff4e-109">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6ff4e-109">Visual Studio 2012</span></span>
> - <span data-ttu-id="6ff4e-110">Веб-API 1 (также работает с веб-API 2)</span><span class="sxs-lookup"><span data-stu-id="6ff4e-110">Web API 1 (also works with Web API 2)</span></span>


<span data-ttu-id="6ff4e-111">Обозначает CRUD &quot;создание, чтение, обновление и удаление,&quot; являющиеся четыре основных операций базы данных.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-111">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="6ff4e-112">Многие службы HTTP также моделировать операции CRUD с помощью REST или API-интерфейсов в стиле REST.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-112">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="6ff4e-113">В этом руководстве вы создадите простое веб-API для управления списком продуктов.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-113">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="6ff4e-114">Каждый продукт будет содержать имя, цену и категории (такие как &quot;toys&quot; или &quot;оборудования&quot;), а также идентификатора продукта.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-114">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="6ff4e-115">Продукты API предоставляет следующие методы.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-115">The products API will expose following methods.</span></span>

| <span data-ttu-id="6ff4e-116">Действие</span><span class="sxs-lookup"><span data-stu-id="6ff4e-116">Action</span></span> | <span data-ttu-id="6ff4e-117">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="6ff4e-117">HTTP method</span></span> | <span data-ttu-id="6ff4e-118">Относительный URI</span><span class="sxs-lookup"><span data-stu-id="6ff4e-118">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ff4e-119">Получение списка всех продуктов</span><span class="sxs-lookup"><span data-stu-id="6ff4e-119">Get a list of all products</span></span> | <span data-ttu-id="6ff4e-120">GET</span><span class="sxs-lookup"><span data-stu-id="6ff4e-120">GET</span></span> | <span data-ttu-id="6ff4e-121">/ api/продуктов</span><span class="sxs-lookup"><span data-stu-id="6ff4e-121">/api/products</span></span> |
| <span data-ttu-id="6ff4e-122">Получить продукт по Идентификатору</span><span class="sxs-lookup"><span data-stu-id="6ff4e-122">Get a product by ID</span></span> | <span data-ttu-id="6ff4e-123">GET</span><span class="sxs-lookup"><span data-stu-id="6ff4e-123">GET</span></span> | <span data-ttu-id="6ff4e-124">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="6ff4e-124">/api/products/*id*</span></span> |
| <span data-ttu-id="6ff4e-125">Получить продукт по категории</span><span class="sxs-lookup"><span data-stu-id="6ff4e-125">Get a product by category</span></span> | <span data-ttu-id="6ff4e-126">GET</span><span class="sxs-lookup"><span data-stu-id="6ff4e-126">GET</span></span> | <span data-ttu-id="6ff4e-127">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="6ff4e-127">/api/products?category=*category*</span></span> |
| <span data-ttu-id="6ff4e-128">Создать продукт</span><span class="sxs-lookup"><span data-stu-id="6ff4e-128">Create a new product</span></span> | <span data-ttu-id="6ff4e-129">ПОМЕСТИТЬ</span><span class="sxs-lookup"><span data-stu-id="6ff4e-129">POST</span></span> | <span data-ttu-id="6ff4e-130">/ api/продуктов</span><span class="sxs-lookup"><span data-stu-id="6ff4e-130">/api/products</span></span> |
| <span data-ttu-id="6ff4e-131">Обновления продукта</span><span class="sxs-lookup"><span data-stu-id="6ff4e-131">Update a product</span></span> | <span data-ttu-id="6ff4e-132">PUT</span><span class="sxs-lookup"><span data-stu-id="6ff4e-132">PUT</span></span> | <span data-ttu-id="6ff4e-133">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="6ff4e-133">/api/products/*id*</span></span> |
| <span data-ttu-id="6ff4e-134">Удалить продукт</span><span class="sxs-lookup"><span data-stu-id="6ff4e-134">Delete a product</span></span> | <span data-ttu-id="6ff4e-135">DELETE</span><span class="sxs-lookup"><span data-stu-id="6ff4e-135">DELETE</span></span> | <span data-ttu-id="6ff4e-136">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="6ff4e-136">/api/products/*id*</span></span> |

<span data-ttu-id="6ff4e-137">Обратите внимание на то, что некоторые из URI включают идентификатор продукта в пути.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-137">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="6ff4e-138">Например, чтобы получить продукт, идентификатор которого — 28, клиент отправляет запрос GET для `http://hostname/api/products/28`.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-138">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="6ff4e-139">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="6ff4e-139">Resources</span></span>

<span data-ttu-id="6ff4e-140">Продукты API определяет идентификаторы URI для двух типов ресурсов:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-140">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="6ff4e-141">Ресурс</span><span class="sxs-lookup"><span data-stu-id="6ff4e-141">Resource</span></span> | <span data-ttu-id="6ff4e-142">URI</span><span class="sxs-lookup"><span data-stu-id="6ff4e-142">URI</span></span> |
| --- | --- |
| <span data-ttu-id="6ff4e-143">Список всех продуктов.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-143">The list of all the products.</span></span> | <span data-ttu-id="6ff4e-144">/ api/продуктов</span><span class="sxs-lookup"><span data-stu-id="6ff4e-144">/api/products</span></span> |
| <span data-ttu-id="6ff4e-145">Отдельному продукту.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-145">An individual product.</span></span> | <span data-ttu-id="6ff4e-146">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="6ff4e-146">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="6ff4e-147">Методы</span><span class="sxs-lookup"><span data-stu-id="6ff4e-147">Methods</span></span>

<span data-ttu-id="6ff4e-148">Четыре основных метода HTTP (GET, PUT, POST и DELETE) может быть сопоставлен операции CRUD следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-148">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="6ff4e-149">GET возвращает представление ресурса по указанному URI.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-149">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="6ff4e-150">GET не оказывает влияния на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-150">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="6ff4e-151">PUT обновляет ресурс с указанным URI.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-151">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="6ff4e-152">PUT можно также использовать для создания нового ресурса с указанным URI, если сервер разрешает клиентам указывать новые URI.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-152">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="6ff4e-153">В этом учебнике API не будет поддерживать создание через PUT.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-153">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="6ff4e-154">POST создает новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-154">POST creates a new resource.</span></span> <span data-ttu-id="6ff4e-155">Сервер назначает URI для нового объекта и возвращает этот URI как часть ответного сообщения.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-155">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="6ff4e-156">DELETE удаляет ресурс по указанному URI.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-156">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="6ff4e-157">Примечание. Метод PUT заменяет сущность всего продукта.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-157">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="6ff4e-158">То есть клиент ожидается для отправки обновленных продукта полное представление.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-158">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="6ff4e-159">Если вы хотите обеспечить поддержку частичных обновлений, метод PATCH является предпочтительным.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-159">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="6ff4e-160">В этом руководстве реализуются PATCH.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-160">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="6ff4e-161">Создать проект нового веб-API</span><span class="sxs-lookup"><span data-stu-id="6ff4e-161">Create a New Web API Project</span></span>

<span data-ttu-id="6ff4e-162">Начните с запуска Visual Studio и выберите **новый проект** из **запустить** страницы.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-162">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="6ff4e-163">Или с **файл** меню, выберите **New** и затем **проекта**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-163">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="6ff4e-164">В **шаблоны** области выберите **установленные шаблоны** и разверните **Visual C#** узла.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-164">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="6ff4e-165">В разделе **Visual C#** выберите **Web**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-165">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="6ff4e-166">В списке шаблонов проектов выберите **веб-приложение ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-166">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="6ff4e-167">Назовите проект &quot;ProductStore&quot; и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-167">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="6ff4e-168">В **создания проекта ASP.NET MVC 4** диалоговом окне выберите **веб-API** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-168">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="6ff4e-169">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="6ff4e-169">Adding a Model</span></span>

<span data-ttu-id="6ff4e-170">*Модель* — это объект, представляющий данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-170">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="6ff4e-171">В веб-API ASP.NET строго типизированные объекты CLR можно использовать в качестве модели, и они будет автоматически сериализован в XML или JSON для клиента.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-171">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="6ff4e-172">Для ProductStore API, наших данных состоит из продуктов, поэтому мы создадим новый класс с именем `Product`.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-172">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="6ff4e-173">Если обозреватель решений не отображается, нажмите кнопку **представление** меню и выберите **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-173">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="6ff4e-174">В обозревателе решений щелкните правой кнопкой мыши **моделей** папки.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-174">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="6ff4e-175">Постановка контекста, выберите **добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-175">From the context meny, select **Add**, then select **Class**.</span></span> <span data-ttu-id="6ff4e-176">Назовите класс &quot;продукта&quot;.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-176">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="6ff4e-177">Добавьте следующие свойства `Product` класса.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-177">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="6ff4e-178">Добавление репозитория</span><span class="sxs-lookup"><span data-stu-id="6ff4e-178">Adding a Repository</span></span>

<span data-ttu-id="6ff4e-179">Нам нужно хранить коллекции продуктов.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-179">We need to store a collection of products.</span></span> <span data-ttu-id="6ff4e-180">Это хороший способ разделения коллекции из нашей реализации службы.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-180">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="6ff4e-181">Таким образом, мы можем изменить хранилище без перезаписи классу службы.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-181">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="6ff4e-182">Этот тип проектирования называется *репозитория* шаблон.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-182">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="6ff4e-183">Начинается с определения универсальный интерфейс для репозитория.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-183">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="6ff4e-184">В обозревателе решений щелкните правой кнопкой мыши **моделей** папки.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-184">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="6ff4e-185">Выберите **добавить**, а затем выберите **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-185">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="6ff4e-186">В **шаблоны** области выберите **установленные шаблоны** и разверните узел C#.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-186">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="6ff4e-187">В области C#, выберите **кода**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-187">Under C#, select **Code**.</span></span> <span data-ttu-id="6ff4e-188">В списке шаблонов кода, выберите **интерфейс**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-188">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="6ff4e-189">Назовите этот интерфейс &quot;IProductRepository&quot;.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-189">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="6ff4e-190">Добавьте следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-190">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="6ff4e-191">Теперь добавьте еще один класс в папке «модели», с именем &quot;ProductRepository.&quot; Этот класс реализует интерфейс `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-191">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="6ff4e-192">Добавьте следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-192">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="6ff4e-193">Хранилище сохраняет список в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-193">The repository keeps the list in local memory.</span></span> <span data-ttu-id="6ff4e-194">Это нормально для учебника, но в реальном приложении, будут храниться данные во внешней системе, либо базы данных или в облачном хранилище.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-194">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="6ff4e-195">Шаблон репозитория упростит состоит в изменении реализации более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-195">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="6ff4e-196">Добавление контроллер веб-API</span><span class="sxs-lookup"><span data-stu-id="6ff4e-196">Adding a Web API Controller</span></span>

<span data-ttu-id="6ff4e-197">Если вы работали с ASP.NET MVC, то вы уже знакомы с контроллерами.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-197">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="6ff4e-198">В веб-API ASP.NET *контроллера* является классом, который обрабатывает HTTP-запросы от клиента.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-198">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="6ff4e-199">При создании проекта мастером создания проекта автоматически создается два контроллера.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-199">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="6ff4e-200">Чтобы увидеть их, разверните папку Controllers в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-200">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="6ff4e-201">HomeController — это традиционный контроллер ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-201">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="6ff4e-202">Он отвечает за обслуживание HTML-страниц для сайта и не имеет прямого отношения к нашей веб-API.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-202">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="6ff4e-203">ValuesController — это пример контроллера WebAPI.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-203">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="6ff4e-204">Продолжить и удалить ValuesController, дважды щелкнув файл в обозревателе решений и выбрав **удалить.**</span><span class="sxs-lookup"><span data-stu-id="6ff4e-204">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="6ff4e-205">Теперь добавьте новый контроллер, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-205">Now add a new controller, as follows:</span></span>

<span data-ttu-id="6ff4e-206">В **обозревателе решений**, щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-206">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="6ff4e-207">Выберите **добавить** , а затем выберите **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-207">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="6ff4e-208">В **Добавление контроллера** мастера, назовите контроллер &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-208">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="6ff4e-209">В **шаблона** стрелку раскрывающегося списка выберите **пустой контроллер API**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-209">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="6ff4e-210">Затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-210">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="6ff4e-211">Не бывает необходимо поместить в папку с именем контроллеры контроллеров.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-211">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="6ff4e-212">Имя папки не имеет значения; Это просто удобный способ организации исходные файлы.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-212">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>


<span data-ttu-id="6ff4e-213">**Добавление контроллера** мастер создаст файл с именем ProductsController.cs в папку "контроллеры".</span><span class="sxs-lookup"><span data-stu-id="6ff4e-213">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="6ff4e-214">Если этот файл еще не открыт, дважды щелкните файл, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-214">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="6ff4e-215">Добавьте следующий **с помощью** инструкции:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-215">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="6ff4e-216">Добавьте поле, которое хранит **IProductRepository** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-216">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="6ff4e-217">Вызов `new ProductRepository()` в контроллере не является лучшим Дизайн, привязывает контроллера для конкретной реализации `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-217">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="6ff4e-218">Лучший подход, см. в разделе [с помощью сопоставителя зависимостей Web API](../advanced/dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="6ff4e-218">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>


## <a name="getting-a-resource"></a><span data-ttu-id="6ff4e-219">Получение сведений о ресурсе</span><span class="sxs-lookup"><span data-stu-id="6ff4e-219">Getting a Resource</span></span>

<span data-ttu-id="6ff4e-220">Предоставляет несколько ProductStore API &quot;чтение&quot; действия, как методы HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-220">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="6ff4e-221">Каждое действие будет соответствовать методу в `ProductsController` класса.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-221">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="6ff4e-222">Действие</span><span class="sxs-lookup"><span data-stu-id="6ff4e-222">Action</span></span> | <span data-ttu-id="6ff4e-223">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="6ff4e-223">HTTP method</span></span> | <span data-ttu-id="6ff4e-224">Относительный URI</span><span class="sxs-lookup"><span data-stu-id="6ff4e-224">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ff4e-225">Получение списка всех продуктов</span><span class="sxs-lookup"><span data-stu-id="6ff4e-225">Get a list of all products</span></span> | <span data-ttu-id="6ff4e-226">GET</span><span class="sxs-lookup"><span data-stu-id="6ff4e-226">GET</span></span> | <span data-ttu-id="6ff4e-227">/ api/продуктов</span><span class="sxs-lookup"><span data-stu-id="6ff4e-227">/api/products</span></span> |
| <span data-ttu-id="6ff4e-228">Получить продукт по Идентификатору</span><span class="sxs-lookup"><span data-stu-id="6ff4e-228">Get a product by ID</span></span> | <span data-ttu-id="6ff4e-229">GET</span><span class="sxs-lookup"><span data-stu-id="6ff4e-229">GET</span></span> | <span data-ttu-id="6ff4e-230">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="6ff4e-230">/api/products/*id*</span></span> |
| <span data-ttu-id="6ff4e-231">Получить продукт по категории</span><span class="sxs-lookup"><span data-stu-id="6ff4e-231">Get a product by category</span></span> | <span data-ttu-id="6ff4e-232">GET</span><span class="sxs-lookup"><span data-stu-id="6ff4e-232">GET</span></span> | <span data-ttu-id="6ff4e-233">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="6ff4e-233">/api/products?category=*category*</span></span> |

<span data-ttu-id="6ff4e-234">Чтобы получить список всех продуктов, добавьте этот метод, чтобы `ProductsController` класса:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-234">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="6ff4e-235">Имя метода начинается с &quot;получить&quot;, поэтому по соглашению он сопоставляет на запросы GET.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-235">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="6ff4e-236">Кроме того, поскольку метод не имеет параметров, он сопоставляется с URI, который не содержит *&quot;идентификатор&quot;* сегментом пути.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-236">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="6ff4e-237">Чтобы получить продукт по Идентификатору, добавьте этот метод, чтобы `ProductsController` класса:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-237">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="6ff4e-238">Это имя метода также начинается с &quot;получить&quot;, но метод будет иметь параметр с именем *идентификатор*. Этот параметр сопоставляется &quot;идентификатор&quot; сегмент пути URI.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-238">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="6ff4e-239">Платформа веб-API ASP.NET автоматически преобразует идентификатор в правильный тип данных (**int**) для параметра.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-239">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="6ff4e-240">Метод GetProduct вызывает исключение типа **HttpResponseException** Если *идентификатор* является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-240">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="6ff4e-241">Это исключение будет преобразован средой в ошибку 404 (не найдено).</span><span class="sxs-lookup"><span data-stu-id="6ff4e-241">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="6ff4e-242">Наконец добавьте метод для поиска продуктов по категориям:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-242">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="6ff4e-243">Если URI запроса содержит строку запроса, веб-API пытается сопоставить параметры запроса для параметров метода контроллера.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-243">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="6ff4e-244">Таким образом, URI в формате «api/products? категории =*категории*"будет сопоставлен этот метод.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-244">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="6ff4e-245">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="6ff4e-245">Creating a Resource</span></span>

<span data-ttu-id="6ff4e-246">Далее мы добавим метод `ProductsController` класса для создания нового продукта.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-246">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="6ff4e-247">Вот простая реализация метода:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-247">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="6ff4e-248">Обратите внимание два аспекта этот метод:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-248">Note two things about this method:</span></span>

- <span data-ttu-id="6ff4e-249">Имя метода начинается с &quot;Post... &quot;.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-249">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="6ff4e-250">Чтобы создать новый продукт, клиент отправляет запрос HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-250">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="6ff4e-251">Этот метод принимает параметр типа продукта.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-251">The method takes a parameter of type Product.</span></span> <span data-ttu-id="6ff4e-252">В веб-API параметры со сложными типами десериализуются из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-252">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="6ff4e-253">Следовательно мы ожидаем, чтобы клиент отправлял сериализованное представление объекта продукта, в формате XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-253">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="6ff4e-254">Эта реализация будет работать, но он не дописан.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-254">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="6ff4e-255">В идеале хотелось бы, ответ HTTP, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-255">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="6ff4e-256">**Код ответа:** По умолчанию платформа веб-API задает код состояния отклика 200 (ОК).</span><span class="sxs-lookup"><span data-stu-id="6ff4e-256">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="6ff4e-257">Но в соответствии с протоколом HTTP/1.1, когда запрос POST приводит к созданию ресурса, сервер должен возвращаться состояния 201 (создано).</span><span class="sxs-lookup"><span data-stu-id="6ff4e-257">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="6ff4e-258">**Расположение:** Когда сервер создает ресурс, оно должно содержать URI нового ресурса в заголовке Location ответа.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-258">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="6ff4e-259">Веб-API ASP.NET позволяет легко управлять сообщение HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-259">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="6ff4e-260">Вот улучшенную реализацию:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-260">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="6ff4e-261">Обратите внимание, что тип возвращаемого значения метода теперь **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-261">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="6ff4e-262">Путем возвращения **HttpResponseMessage** вместо продукта, можно управлять параметрами сообщение HTTP-ответа, включая код состояния и заголовок Location.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-262">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="6ff4e-263">**CreateResponse** метод создает **HttpResponseMessage** и автоматически записывает сериализованное представление объекта продукта в тексте fo ответного сообщения.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-263">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="6ff4e-264">В этом примере не проверяет `Product`.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-264">This example does not validate the `Product`.</span></span> <span data-ttu-id="6ff4e-265">Сведения о проверке модели, см. в разделе [проверка модели в веб-API ASP.NET](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="6ff4e-265">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>


## <a name="updating-a-resource"></a><span data-ttu-id="6ff4e-266">Обновление ресурса</span><span class="sxs-lookup"><span data-stu-id="6ff4e-266">Updating a Resource</span></span>

<span data-ttu-id="6ff4e-267">При обновлении продукта с PUT прост:</span><span class="sxs-lookup"><span data-stu-id="6ff4e-267">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="6ff4e-268">Имя метода начинается с &quot;поместить... &quot;, поэтому веб-API соответствующих запросов PUT.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-268">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="6ff4e-269">Этот метод принимает два параметра: идентификатор продукта и обновленные продукта.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-269">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="6ff4e-270">*Идентификатор* параметр взят из пути URI и *продукта* параметр десериализации из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-270">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="6ff4e-271">По умолчанию платформа ASP.NET веб-API принимает простые типы параметров из маршрута и сложные типы из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-271">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="6ff4e-272">Удаление ресурса</span><span class="sxs-lookup"><span data-stu-id="6ff4e-272">Deleting a Resource</span></span>

<span data-ttu-id="6ff4e-273">Чтобы удалить ресурс, определите «удалить...» метод.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-273">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="6ff4e-274">Успешное завершение запроса на удаление, он может возвращать состояние 200 (ОК) с тело сущности, описывающая состояние; состояние 202 (принято), если удаление по-прежнему ожидающие; или состояния 204 (нет содержимого) без тела сущности.</span><span class="sxs-lookup"><span data-stu-id="6ff4e-274">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="6ff4e-275">В этом случае `DeleteProduct` имеет метод `void` тип возвращаемого значения, поэтому веб-API ASP.NET автоматически преобразует это в состояние код 204 (нет содержимого).</span><span class="sxs-lookup"><span data-stu-id="6ff4e-275">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
