---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: Включение операций CRUD в веб-API ASP.NET 1-ASP.NET 4. x
author: MikeWasson
description: В этом руководстве показано, как поддерживать операции CRUD в службе HTTP с помощью веб-API ASP.NET для ASP.NET 4. x.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600340"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="42c49-103">Включение операций CRUD в веб-API ASP.NET 1</span><span class="sxs-lookup"><span data-stu-id="42c49-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="42c49-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="42c49-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="42c49-105">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="42c49-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="42c49-106">В этом руководстве показано, как поддерживать операции CRUD в службе HTTP с помощью веб-API ASP.NET для ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="42c49-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="42c49-107">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="42c49-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="42c49-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="42c49-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="42c49-109">Веб-API 1 (также работает с веб-API 2)</span><span class="sxs-lookup"><span data-stu-id="42c49-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="42c49-110">CRUD означает &quot;создания, чтения, обновления и удаления&quot; которые являются четырьмя основными операциями с базой данных.</span><span class="sxs-lookup"><span data-stu-id="42c49-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="42c49-111">Многие службы HTTP также моделируют операции CRUD с помощью API-интерфейсов RESTFUL или RESTFUL.</span><span class="sxs-lookup"><span data-stu-id="42c49-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="42c49-112">В этом руководстве вы создадите очень простой веб-API для управления списком продуктов.</span><span class="sxs-lookup"><span data-stu-id="42c49-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="42c49-113">Каждый продукт будет содержать имя, цену и категорию (например, &quot;Toys&quot; или &quot;оборудования&quot;), а также идентификатор продукта.</span><span class="sxs-lookup"><span data-stu-id="42c49-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="42c49-114">API продуктов предоставит следующие методы.</span><span class="sxs-lookup"><span data-stu-id="42c49-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="42c49-115">Действие</span><span class="sxs-lookup"><span data-stu-id="42c49-115">Action</span></span> | <span data-ttu-id="42c49-116">HTTP-метод</span><span class="sxs-lookup"><span data-stu-id="42c49-116">HTTP method</span></span> | <span data-ttu-id="42c49-117">Относительный URI</span><span class="sxs-lookup"><span data-stu-id="42c49-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42c49-118">Получить список всех продуктов</span><span class="sxs-lookup"><span data-stu-id="42c49-118">Get a list of all products</span></span> | <span data-ttu-id="42c49-119">GET</span><span class="sxs-lookup"><span data-stu-id="42c49-119">GET</span></span> | <span data-ttu-id="42c49-120">/апи/продуктс</span><span class="sxs-lookup"><span data-stu-id="42c49-120">/api/products</span></span> |
| <span data-ttu-id="42c49-121">Получение продукта по ИДЕНТИФИКАТОРу</span><span class="sxs-lookup"><span data-stu-id="42c49-121">Get a product by ID</span></span> | <span data-ttu-id="42c49-122">GET</span><span class="sxs-lookup"><span data-stu-id="42c49-122">GET</span></span> | <span data-ttu-id="42c49-123">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="42c49-123">/api/products/*id*</span></span> |
| <span data-ttu-id="42c49-124">Получение продукта по категории</span><span class="sxs-lookup"><span data-stu-id="42c49-124">Get a product by category</span></span> | <span data-ttu-id="42c49-125">GET</span><span class="sxs-lookup"><span data-stu-id="42c49-125">GET</span></span> | <span data-ttu-id="42c49-126">/АПИ/Продуктс? Category =*Категория*</span><span class="sxs-lookup"><span data-stu-id="42c49-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="42c49-127">Создать продукт</span><span class="sxs-lookup"><span data-stu-id="42c49-127">Create a new product</span></span> | <span data-ttu-id="42c49-128">ПОМЕСТИТЬ</span><span class="sxs-lookup"><span data-stu-id="42c49-128">POST</span></span> | <span data-ttu-id="42c49-129">/апи/продуктс</span><span class="sxs-lookup"><span data-stu-id="42c49-129">/api/products</span></span> |
| <span data-ttu-id="42c49-130">Обновить продукт</span><span class="sxs-lookup"><span data-stu-id="42c49-130">Update a product</span></span> | <span data-ttu-id="42c49-131">PUT</span><span class="sxs-lookup"><span data-stu-id="42c49-131">PUT</span></span> | <span data-ttu-id="42c49-132">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="42c49-132">/api/products/*id*</span></span> |
| <span data-ttu-id="42c49-133">Удалить продукт</span><span class="sxs-lookup"><span data-stu-id="42c49-133">Delete a product</span></span> | <span data-ttu-id="42c49-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="42c49-134">DELETE</span></span> | <span data-ttu-id="42c49-135">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="42c49-135">/api/products/*id*</span></span> |

<span data-ttu-id="42c49-136">Обратите внимание, что некоторые URI содержат идентификатор продукта в пути.</span><span class="sxs-lookup"><span data-stu-id="42c49-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="42c49-137">Например, чтобы получить продукт, идентификатор которого равен 28, клиент отправляет запрос GET для `http://hostname/api/products/28`.</span><span class="sxs-lookup"><span data-stu-id="42c49-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="42c49-138">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="42c49-138">Resources</span></span>

<span data-ttu-id="42c49-139">API продуктов определяет URI для двух типов ресурсов:</span><span class="sxs-lookup"><span data-stu-id="42c49-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="42c49-140">Resource</span><span class="sxs-lookup"><span data-stu-id="42c49-140">Resource</span></span> | <span data-ttu-id="42c49-141">URI</span><span class="sxs-lookup"><span data-stu-id="42c49-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="42c49-142">Список всех продуктов.</span><span class="sxs-lookup"><span data-stu-id="42c49-142">The list of all the products.</span></span> | <span data-ttu-id="42c49-143">/апи/продуктс</span><span class="sxs-lookup"><span data-stu-id="42c49-143">/api/products</span></span> |
| <span data-ttu-id="42c49-144">Отдельный продукт.</span><span class="sxs-lookup"><span data-stu-id="42c49-144">An individual product.</span></span> | <span data-ttu-id="42c49-145">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="42c49-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="42c49-146">Методы</span><span class="sxs-lookup"><span data-stu-id="42c49-146">Methods</span></span>

<span data-ttu-id="42c49-147">Четыре основных метода HTTP (GET, WHERE, POST и DELETE) можно сопоставить с операциями CRUD следующим образом:</span><span class="sxs-lookup"><span data-stu-id="42c49-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="42c49-148">GET получает представление ресурса по указанному универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="42c49-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="42c49-149">GET не должен иметь побочных эффектов на сервере.</span><span class="sxs-lookup"><span data-stu-id="42c49-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="42c49-150">Помещает обновление ресурса по указанному универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="42c49-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="42c49-151">Также можно использовать для создания нового ресурса по указанному универсальному коду ресурса (URI), если сервер позволяет клиентам указывать новые URI.</span><span class="sxs-lookup"><span data-stu-id="42c49-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="42c49-152">В этом руководстве API не поддерживает создание с помощью инструкции For.</span><span class="sxs-lookup"><span data-stu-id="42c49-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="42c49-153">POST создает новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="42c49-153">POST creates a new resource.</span></span> <span data-ttu-id="42c49-154">Сервер назначает универсальный код ресурса (URI) для нового объекта и возвращает этот URI как часть ответного сообщения.</span><span class="sxs-lookup"><span data-stu-id="42c49-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="42c49-155">DELETE удаляет ресурс по указанному универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="42c49-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="42c49-156">Примечание. метод размещения заменяет всю сущность Product.</span><span class="sxs-lookup"><span data-stu-id="42c49-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="42c49-157">То есть клиент должен отправить полное представление обновленного продукта.</span><span class="sxs-lookup"><span data-stu-id="42c49-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="42c49-158">Если требуется поддержка частичных обновлений, рекомендуется использовать метод PATCH.</span><span class="sxs-lookup"><span data-stu-id="42c49-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="42c49-159">В этом руководстве не реализовано исправление.</span><span class="sxs-lookup"><span data-stu-id="42c49-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="42c49-160">Создание нового проекта веб-API</span><span class="sxs-lookup"><span data-stu-id="42c49-160">Create a New Web API Project</span></span>

<span data-ttu-id="42c49-161">Начните с запуска Visual Studio и выберите **создать проект** на **начальной** странице.</span><span class="sxs-lookup"><span data-stu-id="42c49-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="42c49-162">Либо в меню **файл** выберите **создать** , а затем — **проект**.</span><span class="sxs-lookup"><span data-stu-id="42c49-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="42c49-163">В области **шаблоны** выберите **Установленные шаблоны** и разверните узел  **C# визуального** элемента.</span><span class="sxs-lookup"><span data-stu-id="42c49-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="42c49-164">В **разделе C#визуальный** элемент выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="42c49-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="42c49-165">В списке шаблонов проектов выберите **ASP.NET MVC 4 веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="42c49-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="42c49-166">Присвойте проекту имя &quot;Продуктсторе&quot; и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="42c49-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="42c49-167">В диалоговом окне **Новый проект ASP.NET MVC 4** выберите **веб-API** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="42c49-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="42c49-168">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="42c49-168">Adding a Model</span></span>

<span data-ttu-id="42c49-169">*Модель* — это объект, представляющий данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="42c49-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="42c49-170">В веб-API ASP.NET можно использовать строго типизированные объекты CLR в качестве моделей, и они будут автоматически сериализованы в XML или JSON для клиента.</span><span class="sxs-lookup"><span data-stu-id="42c49-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="42c49-171">Для API Продуктсторе наши данные состоят из продуктов, поэтому мы создадим новый класс с именем `Product`.</span><span class="sxs-lookup"><span data-stu-id="42c49-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="42c49-172">Если обозреватель решений еще не отображается, откройте меню **вид** и выберите **Обозреватель решений**.</span><span class="sxs-lookup"><span data-stu-id="42c49-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="42c49-173">В обозреватель решений щелкните правой кнопкой мыши папку **модели** .</span><span class="sxs-lookup"><span data-stu-id="42c49-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="42c49-174">В контекстном меню выберите **Добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="42c49-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="42c49-175">Присвойте классу имя &quot;&quot;продукта.</span><span class="sxs-lookup"><span data-stu-id="42c49-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="42c49-176">Добавьте следующие свойства в класс `Product`.</span><span class="sxs-lookup"><span data-stu-id="42c49-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="42c49-177">Добавление репозитория</span><span class="sxs-lookup"><span data-stu-id="42c49-177">Adding a Repository</span></span>

<span data-ttu-id="42c49-178">Необходимо сохранить коллекцию продуктов.</span><span class="sxs-lookup"><span data-stu-id="42c49-178">We need to store a collection of products.</span></span> <span data-ttu-id="42c49-179">Рекомендуется отделить коллекцию от нашей реализации службы.</span><span class="sxs-lookup"><span data-stu-id="42c49-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="42c49-180">Таким образом, можно изменить резервное хранилище, не переписывая класс службы.</span><span class="sxs-lookup"><span data-stu-id="42c49-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="42c49-181">Этот тип проекта называется шаблоном *репозитория* .</span><span class="sxs-lookup"><span data-stu-id="42c49-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="42c49-182">Начните с определения универсального интерфейса для репозитория.</span><span class="sxs-lookup"><span data-stu-id="42c49-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="42c49-183">В обозреватель решений щелкните правой кнопкой мыши папку **модели** .</span><span class="sxs-lookup"><span data-stu-id="42c49-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="42c49-184">Нажмите кнопку **Добавить**, а затем выберите **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="42c49-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="42c49-185">В области **шаблоны** выберите **Установленные шаблоны** и разверните C# узел.</span><span class="sxs-lookup"><span data-stu-id="42c49-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="42c49-186">В C#разделе Выберите **код**.</span><span class="sxs-lookup"><span data-stu-id="42c49-186">Under C#, select **Code**.</span></span> <span data-ttu-id="42c49-187">В списке шаблонов кода выберите **интерфейс**.</span><span class="sxs-lookup"><span data-stu-id="42c49-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="42c49-188">Присвойте интерфейсу имя &quot;&quot;Ипродуктрепоситори.</span><span class="sxs-lookup"><span data-stu-id="42c49-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="42c49-189">Добавьте следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="42c49-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="42c49-190">Теперь добавьте еще один класс в папку Models с именем &quot;Продуктрепоситори.&quot; этот класс будет реализовывать интерфейс `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="42c49-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="42c49-191">Добавьте следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="42c49-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="42c49-192">Репозиторий хранит список в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="42c49-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="42c49-193">Это нормально для учебника, но в реальном приложении вы храните данные извне, либо в базе данных, либо в облачном хранилище.</span><span class="sxs-lookup"><span data-stu-id="42c49-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="42c49-194">Шаблон репозитория упростит изменение реализации.</span><span class="sxs-lookup"><span data-stu-id="42c49-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="42c49-195">Добавление контроллера веб-API</span><span class="sxs-lookup"><span data-stu-id="42c49-195">Adding a Web API Controller</span></span>

<span data-ttu-id="42c49-196">Если вы работали с ASP.NET MVC, вы уже знакомы с контроллерами.</span><span class="sxs-lookup"><span data-stu-id="42c49-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="42c49-197">В веб-API ASP.NET *контроллер* — это класс, который обрабатывает HTTP-запросы от клиента.</span><span class="sxs-lookup"><span data-stu-id="42c49-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="42c49-198">При создании проекта мастер создания проекта создал два контроллера.</span><span class="sxs-lookup"><span data-stu-id="42c49-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="42c49-199">Чтобы увидеть их, разверните папку Controllers в обозреватель решений.</span><span class="sxs-lookup"><span data-stu-id="42c49-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="42c49-200">HomeController — это традиционный контроллер MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="42c49-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="42c49-201">Он отвечает за обслуживание HTML-страниц для сайта и не связан напрямую с нашим веб-API.</span><span class="sxs-lookup"><span data-stu-id="42c49-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="42c49-202">Объекта valuescontroller — это пример контроллера WebAPI.</span><span class="sxs-lookup"><span data-stu-id="42c49-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="42c49-203">Удалите объекта valuescontroller, щелкнув правой кнопкой мыши файл в обозреватель решений и выбрав пункт **Удалить.**</span><span class="sxs-lookup"><span data-stu-id="42c49-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="42c49-204">Теперь добавьте новый контроллер, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="42c49-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="42c49-205">В **Обозреватель решений**щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="42c49-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="42c49-206">Нажмите кнопку **Добавить** , а затем выберите **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="42c49-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="42c49-207">В мастере **добавления контроллера** назовите контроллер &quot;продуктсконтроллер&quot;.</span><span class="sxs-lookup"><span data-stu-id="42c49-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="42c49-208">В раскрывающемся списке **шаблон** выберите **пустой контроллер API**.</span><span class="sxs-lookup"><span data-stu-id="42c49-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="42c49-209">Затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="42c49-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="42c49-210">Нет необходимости размещать контроллеры в папке с именем Controllers.</span><span class="sxs-lookup"><span data-stu-id="42c49-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="42c49-211">Имя папки не имеет значения; Это просто удобный способ организации исходных файлов.</span><span class="sxs-lookup"><span data-stu-id="42c49-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="42c49-212">Мастер **добавления контроллера** создаст файл с именем ProductsController.cs в папке Controllers.</span><span class="sxs-lookup"><span data-stu-id="42c49-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="42c49-213">Если этот файл еще не открыт, дважды щелкните файл, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="42c49-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="42c49-214">Добавьте следующую инструкцию **using** :</span><span class="sxs-lookup"><span data-stu-id="42c49-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="42c49-215">Добавьте поле, содержащее экземпляр **ипродуктрепоситори** .</span><span class="sxs-lookup"><span data-stu-id="42c49-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="42c49-216">Вызов `new ProductRepository()` в контроллере не является оптимальным решением, так как он связывает контроллер с определенной реализацией `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="42c49-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="42c49-217">Более эффективный подход см. в разделе [Использование сопоставителя зависимостей веб-API](../advanced/dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="42c49-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="42c49-218">Получение ресурса</span><span class="sxs-lookup"><span data-stu-id="42c49-218">Getting a Resource</span></span>

<span data-ttu-id="42c49-219">API Продуктсторе предоставит несколько &quot;чтения&quot; действий в виде методов HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="42c49-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="42c49-220">Каждое действие будет соответствовать методу в классе `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="42c49-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="42c49-221">Действие</span><span class="sxs-lookup"><span data-stu-id="42c49-221">Action</span></span> | <span data-ttu-id="42c49-222">HTTP-метод</span><span class="sxs-lookup"><span data-stu-id="42c49-222">HTTP method</span></span> | <span data-ttu-id="42c49-223">Относительный URI</span><span class="sxs-lookup"><span data-stu-id="42c49-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42c49-224">Получить список всех продуктов</span><span class="sxs-lookup"><span data-stu-id="42c49-224">Get a list of all products</span></span> | <span data-ttu-id="42c49-225">GET</span><span class="sxs-lookup"><span data-stu-id="42c49-225">GET</span></span> | <span data-ttu-id="42c49-226">/апи/продуктс</span><span class="sxs-lookup"><span data-stu-id="42c49-226">/api/products</span></span> |
| <span data-ttu-id="42c49-227">Получение продукта по ИДЕНТИФИКАТОРу</span><span class="sxs-lookup"><span data-stu-id="42c49-227">Get a product by ID</span></span> | <span data-ttu-id="42c49-228">GET</span><span class="sxs-lookup"><span data-stu-id="42c49-228">GET</span></span> | <span data-ttu-id="42c49-229">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="42c49-229">/api/products/*id*</span></span> |
| <span data-ttu-id="42c49-230">Получение продукта по категории</span><span class="sxs-lookup"><span data-stu-id="42c49-230">Get a product by category</span></span> | <span data-ttu-id="42c49-231">GET</span><span class="sxs-lookup"><span data-stu-id="42c49-231">GET</span></span> | <span data-ttu-id="42c49-232">/АПИ/Продуктс? Category =*Категория*</span><span class="sxs-lookup"><span data-stu-id="42c49-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="42c49-233">Чтобы получить список всех продуктов, добавьте этот метод в класс `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="42c49-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="42c49-234">Имя метода начинается с &quot;Get&quot;, поэтому по сопоставлению с запросами GET.</span><span class="sxs-lookup"><span data-stu-id="42c49-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="42c49-235">Кроме того, поскольку метод не имеет параметров, он сопоставляется с URI, который не содержит *&quot;идентификатор&quot;* сегмент в пути.</span><span class="sxs-lookup"><span data-stu-id="42c49-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="42c49-236">Чтобы получить продукт по ИДЕНТИФИКАТОРу, добавьте этот метод в класс `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="42c49-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="42c49-237">Это имя метода также начинается с &quot;Get&quot;, но у метода есть параметр с именем *ID*. Этот параметр сопоставляется с идентификатором &quot;&quot; сегменте пути URI.</span><span class="sxs-lookup"><span data-stu-id="42c49-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="42c49-238">Платформа веб-API ASP.NET автоматически преобразует идентификатор в правильный тип данных (**int**) для параметра.</span><span class="sxs-lookup"><span data-stu-id="42c49-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="42c49-239">Если *идентификатор* является недопустимым, метод **хттпреспонсиксцептион** создает исключение типа.</span><span class="sxs-lookup"><span data-stu-id="42c49-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="42c49-240">Это исключение будет переведено платформой в ошибку 404 (не найдено).</span><span class="sxs-lookup"><span data-stu-id="42c49-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="42c49-241">Наконец, добавьте метод для поиска продуктов по категории:</span><span class="sxs-lookup"><span data-stu-id="42c49-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="42c49-242">Если URI запроса содержит строку запроса, веб-API пытается сопоставить параметры запроса с параметрами метода контроллера.</span><span class="sxs-lookup"><span data-stu-id="42c49-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="42c49-243">Таким образом, URI в форме "API/Products? Category =*Category*" будет сопоставляться с этим методом.</span><span class="sxs-lookup"><span data-stu-id="42c49-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="42c49-244">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="42c49-244">Creating a Resource</span></span>

<span data-ttu-id="42c49-245">Далее мы добавим метод в класс `ProductsController`, чтобы создать новый продукт.</span><span class="sxs-lookup"><span data-stu-id="42c49-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="42c49-246">Ниже приведена простая реализация метода.</span><span class="sxs-lookup"><span data-stu-id="42c49-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="42c49-247">Обратите внимание на два вещи, касающиеся этого метода:</span><span class="sxs-lookup"><span data-stu-id="42c49-247">Note two things about this method:</span></span>

- <span data-ttu-id="42c49-248">Имя метода начинается с &quot;POST...&quot;.</span><span class="sxs-lookup"><span data-stu-id="42c49-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="42c49-249">Чтобы создать новый продукт, клиент отправляет запрос HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="42c49-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="42c49-250">Метод принимает параметр типа Product.</span><span class="sxs-lookup"><span data-stu-id="42c49-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="42c49-251">В веб-API параметры со сложными типами десериализованы из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="42c49-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="42c49-252">Поэтому мы ожидаем, что клиент отправляет сериализованное представление объекта Product в формате XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="42c49-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="42c49-253">Эта реализация будет работать, но это не совсем полная.</span><span class="sxs-lookup"><span data-stu-id="42c49-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="42c49-254">В идеале мы хотим, чтобы HTTP-ответ включал следующее:</span><span class="sxs-lookup"><span data-stu-id="42c49-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="42c49-255">**Код ответа:** По умолчанию платформа веб-API устанавливает для кода состояния ответа значение 200 (ОК).</span><span class="sxs-lookup"><span data-stu-id="42c49-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="42c49-256">Но в соответствии с протоколом HTTP/1.1, когда запрос POST приводит к созданию ресурса, сервер должен ответить с состоянием 201 (создано).</span><span class="sxs-lookup"><span data-stu-id="42c49-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="42c49-257">**Расположение:** Когда сервер создает ресурс, он должен содержать URI нового ресурса в заголовке Location ответа.</span><span class="sxs-lookup"><span data-stu-id="42c49-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="42c49-258">Веб-API ASP.NET позволяет легко управлять ответным сообщением HTTP.</span><span class="sxs-lookup"><span data-stu-id="42c49-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="42c49-259">Ниже приведена Улучшенная реализация.</span><span class="sxs-lookup"><span data-stu-id="42c49-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="42c49-260">Обратите внимание, что возвращаемый тип метода теперь **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="42c49-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="42c49-261">При возврате **HttpResponseMessage** вместо продукта можно управлять сведениями об ответном сообщении HTTP, включая код состояния и заголовок Location.</span><span class="sxs-lookup"><span data-stu-id="42c49-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="42c49-262">Метод **креатереспонсе** создает **HttpResponseMessage** и автоматически записывает сериализованное представление объекта Product в текст ответного сообщения.</span><span class="sxs-lookup"><span data-stu-id="42c49-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="42c49-263">В этом примере не выполняется проверка `Product`.</span><span class="sxs-lookup"><span data-stu-id="42c49-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="42c49-264">Дополнительные сведения о проверке модели см. [в разделе Проверка модели в веб-API ASP.NET](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="42c49-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="42c49-265">Обновление ресурса</span><span class="sxs-lookup"><span data-stu-id="42c49-265">Updating a Resource</span></span>

<span data-ttu-id="42c49-266">Обновление продукта с помощью постановки выполняется просто:</span><span class="sxs-lookup"><span data-stu-id="42c49-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="42c49-267">Имя метода начинается с &quot;помещения...&quot;, поэтому веб-API сопоставляет его для размещения запросов.</span><span class="sxs-lookup"><span data-stu-id="42c49-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="42c49-268">Этот метод принимает два параметра: идентификатор продукта и обновленный продукт.</span><span class="sxs-lookup"><span data-stu-id="42c49-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="42c49-269">Параметр *ID* берется из пути URI, а параметр *Product* десериализуется из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="42c49-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="42c49-270">По умолчанию веб-API ASP.NET Framework принимает простые типы параметров из маршрута и сложных типов из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="42c49-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="42c49-271">Удаление ресурса</span><span class="sxs-lookup"><span data-stu-id="42c49-271">Deleting a Resource</span></span>

<span data-ttu-id="42c49-272">Чтобы удалить ресурс, определите "Delete..." Method.</span><span class="sxs-lookup"><span data-stu-id="42c49-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="42c49-273">Если запрос на удаление завершился успешно, он может вернуть состояние 200 (ОК) с текстом сущности, описывающим состояние. состояние 202 (принято), если удаление все еще ожидается; или состояние 204 (без содержимого) без тела сущности.</span><span class="sxs-lookup"><span data-stu-id="42c49-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="42c49-274">В этом случае метод `DeleteProduct` имеет тип возвращаемого значения `void`, поэтому веб-API ASP.NET автоматически преобразует его в код состояния 204 (нет содержимого).</span><span class="sxs-lookup"><span data-stu-id="42c49-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
