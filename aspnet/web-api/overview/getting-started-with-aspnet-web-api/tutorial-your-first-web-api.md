---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: Начало работы с веб-API ASP.NET 2 (C#)-ASP.NET 4. x
author: MikeWasson
description: Учебник с кодом. Используйте веб-API ASP.NET, чтобы создать веб-API, который возвращает список продуктов.
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 2717d93f47be9d4a6548731d8deeca312b25f39f
ms.sourcegitcommit: 9e3ca74997a67c18589729d4b7303799905473eb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/11/2020
ms.locfileid: "79084056"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="cf501-104">Начало работы с веб-API ASP.NET 2 (C#)</span><span class="sxs-lookup"><span data-stu-id="cf501-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="cf501-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cf501-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="cf501-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="cf501-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="cf501-107">В этом учебнике для создания веб-API, возвращающего список продуктов, будет использоваться веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cf501-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="cf501-108">HTTP не только обслуживает веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="cf501-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="cf501-109">Протокол HTTP также является мощной платформой для создания API-интерфейсов, предоставляющих службы и данные.</span><span class="sxs-lookup"><span data-stu-id="cf501-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="cf501-110">HTTP является простой, гибкой и повсеместной.</span><span class="sxs-lookup"><span data-stu-id="cf501-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="cf501-111">Практически любая платформа, которой можно считать, имеет библиотеку HTTP, поэтому службы HTTP могут обращаться к широкому спектру клиентов, включая браузеры, мобильные устройства и традиционные классические приложения.</span><span class="sxs-lookup"><span data-stu-id="cf501-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="cf501-112">Веб-API ASP.NET — это платформа для создания веб-API поверх .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cf501-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cf501-113">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="cf501-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="cf501-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="cf501-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="cf501-115">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="cf501-115">Web API 2</span></span>

<span data-ttu-id="cf501-116">Более новую версию этого руководства см. в статье [Создание веб-API с помощью ASP.NET Core и Visual Studio для Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) .</span><span class="sxs-lookup"><span data-stu-id="cf501-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="cf501-117">Создание проекта веб-API</span><span class="sxs-lookup"><span data-stu-id="cf501-117">Create a Web API Project</span></span>

<span data-ttu-id="cf501-118">В этом учебнике для создания веб-API, возвращающего список продуктов, будет использоваться веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cf501-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="cf501-119">Интерфейсная веб-страница использует jQuery для вывода результатов.</span><span class="sxs-lookup"><span data-stu-id="cf501-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="cf501-120">Запустите Visual Studio и выберите **создать проект** на **начальной** странице.</span><span class="sxs-lookup"><span data-stu-id="cf501-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="cf501-121">Либо в меню **файл** выберите **создать** , а затем — **проект**.</span><span class="sxs-lookup"><span data-stu-id="cf501-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="cf501-122">В области **шаблоны** выберите **Установленные шаблоны** и разверните узел  **C# визуального** элемента.</span><span class="sxs-lookup"><span data-stu-id="cf501-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="cf501-123">В **разделе C#визуальный** элемент выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="cf501-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="cf501-124">В списке шаблонов проектов выберите **ASP.NET веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="cf501-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="cf501-125">Присвойте проекту имя "Продуктсапп" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cf501-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="cf501-126">В диалоговом окне **Новый проект ASP.NET** выберите **пустой** шаблон.</span><span class="sxs-lookup"><span data-stu-id="cf501-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="cf501-127">В разделе &quot;добавить папки и основные ссылки для&quot;, проверьте **веб-API**.</span><span class="sxs-lookup"><span data-stu-id="cf501-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="cf501-128">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cf501-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="cf501-129">Вы также можете создать проект веб-API, используя шаблон &quot;веб-API&quot;.</span><span class="sxs-lookup"><span data-stu-id="cf501-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="cf501-130">Шаблон веб-API использует ASP.NET MVC для предоставления страниц справки API.</span><span class="sxs-lookup"><span data-stu-id="cf501-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="cf501-131">Я использую пустой шаблон для этого руководства, так как я хочу отобразить веб-API без MVC.</span><span class="sxs-lookup"><span data-stu-id="cf501-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="cf501-132">В общем случае нет необходимости знать ASP.NET MVC для использования веб-API.</span><span class="sxs-lookup"><span data-stu-id="cf501-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="cf501-133">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="cf501-133">Adding a Model</span></span>

<span data-ttu-id="cf501-134">*Модель* — это объект, который представляет данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="cf501-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="cf501-135">Веб-API ASP.NET может автоматически сериализовать вашу модель в формат JSON, XML или в какой-либо другие форматы, а затем записать сериализованные данные в текст сообщения HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="cf501-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="cf501-136">Пока клиент может считывать формат сериализации, он может десериализовать объект.</span><span class="sxs-lookup"><span data-stu-id="cf501-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="cf501-137">Большинство клиентов могут выполнять синтаксический анализ XML-кода или JSON.</span><span class="sxs-lookup"><span data-stu-id="cf501-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="cf501-138">Более того, клиент может указать, какой формат требуется, установив заголовок Accept в сообщении HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="cf501-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="cf501-139">Начнем с создания простой модели, представляющей продукт.</span><span class="sxs-lookup"><span data-stu-id="cf501-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="cf501-140">Если обозреватель решений не отображается, щелкните меню **Просмотр** и выберите **Обозреватель решений**.</span><span class="sxs-lookup"><span data-stu-id="cf501-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="cf501-141">В обозревателе решений щелкните правой кнопкой мыши папку Models.</span><span class="sxs-lookup"><span data-stu-id="cf501-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="cf501-142">В контекстном меню выберите **Добавить**, а затем выберите **Класс**.</span><span class="sxs-lookup"><span data-stu-id="cf501-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="cf501-143">Присвойте классу имя &quot;&quot;продукта.</span><span class="sxs-lookup"><span data-stu-id="cf501-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="cf501-144">Добавьте следующие свойства в класс `Product`.</span><span class="sxs-lookup"><span data-stu-id="cf501-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="cf501-145">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="cf501-145">Adding a Controller</span></span>

<span data-ttu-id="cf501-146">В веб-API *контроллер* — это объект, который обрабатывает HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="cf501-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="cf501-147">Мы добавим контроллер, который может возвращать либо список продуктов, либо отдельный продукт, заданный по ИДЕНТИФИКАТОРу.</span><span class="sxs-lookup"><span data-stu-id="cf501-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="cf501-148">Если вы использовали ASP.NET MVC, вы уже знакомы с контроллерами.</span><span class="sxs-lookup"><span data-stu-id="cf501-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="cf501-149">Контроллеры веб-API похожи на контроллеры MVC, но наследуют класс **ApiController** , а не класс **Controller** .</span><span class="sxs-lookup"><span data-stu-id="cf501-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="cf501-150">В **обозревателе решений** щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="cf501-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="cf501-151">Щелкните **Добавить**, а затем выберите **Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="cf501-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="cf501-152">В диалоговом окне **Добавление шаблона** выберите **Контроллер веб-API — пустой**.</span><span class="sxs-lookup"><span data-stu-id="cf501-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="cf501-153">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cf501-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="cf501-154">В диалоговом окне **Добавление контроллера введите** имя контроллера &quot;продуктсконтроллер&quot;.</span><span class="sxs-lookup"><span data-stu-id="cf501-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="cf501-155">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cf501-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="cf501-156">Формирование шаблонов создает файл с именем ProductsController.cs в папке Controllers.</span><span class="sxs-lookup"><span data-stu-id="cf501-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="cf501-157">Вам не нужно размещать контроллеры в папке с именем Controllers.</span><span class="sxs-lookup"><span data-stu-id="cf501-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="cf501-158">Имя папки — это просто удобный способ организации исходных файлов.</span><span class="sxs-lookup"><span data-stu-id="cf501-158">The folder name is just a convenient way to organize your source files.</span></span>

<span data-ttu-id="cf501-159">Если этот файл еще не открыт, дважды щелкните его.</span><span class="sxs-lookup"><span data-stu-id="cf501-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="cf501-160">Замените код в этом файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="cf501-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="cf501-161">Чтобы упростить этот пример, продукты хранятся в фиксированном массиве внутри класса Controller.</span><span class="sxs-lookup"><span data-stu-id="cf501-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="cf501-162">Разумеется, в реальных приложениях можно запрашивать базу данных или использовать какой-либо другой внешний источник данных.</span><span class="sxs-lookup"><span data-stu-id="cf501-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="cf501-163">Контроллер определяет два метода, которые возвращают продукты:</span><span class="sxs-lookup"><span data-stu-id="cf501-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="cf501-164">Метод `GetAllProducts` возвращает весь список продуктов как тип **&gt;продукта IEnumerable&lt;** .</span><span class="sxs-lookup"><span data-stu-id="cf501-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="cf501-165">Метод `GetProduct` ищет один продукт по его ИДЕНТИФИКАТОРу.</span><span class="sxs-lookup"><span data-stu-id="cf501-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="cf501-166">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="cf501-166">That's it!</span></span> <span data-ttu-id="cf501-167">У вас есть рабочий веб-API.</span><span class="sxs-lookup"><span data-stu-id="cf501-167">You have a working web API.</span></span> <span data-ttu-id="cf501-168">Каждый метод на контроллере соответствует одному или нескольким URI:</span><span class="sxs-lookup"><span data-stu-id="cf501-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="cf501-169">Метод контроллера</span><span class="sxs-lookup"><span data-stu-id="cf501-169">Controller Method</span></span> | <span data-ttu-id="cf501-170">URI</span><span class="sxs-lookup"><span data-stu-id="cf501-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="cf501-171">жеталлпродуктс</span><span class="sxs-lookup"><span data-stu-id="cf501-171">GetAllProducts</span></span> | <span data-ttu-id="cf501-172">/апи/продуктс</span><span class="sxs-lookup"><span data-stu-id="cf501-172">/api/products</span></span> |
| <span data-ttu-id="cf501-173">Продукт</span><span class="sxs-lookup"><span data-stu-id="cf501-173">GetProduct</span></span> | <span data-ttu-id="cf501-174">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="cf501-174">/api/products/*id*</span></span> |

<span data-ttu-id="cf501-175">Для метода `GetProduct` *идентификатором* в URI является заполнитель.</span><span class="sxs-lookup"><span data-stu-id="cf501-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="cf501-176">Например, чтобы получить продукт с ИДЕНТИФИКАТОРом 5, URI `api/products/5`.</span><span class="sxs-lookup"><span data-stu-id="cf501-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="cf501-177">Дополнительные сведения о том, как веб-API направляет запросы HTTP к методам контроллера, см. [в разделе Маршрутизация в веб-API ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="cf501-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="cf501-178">Вызов веб-API с помощью JavaScript и jQuery</span><span class="sxs-lookup"><span data-stu-id="cf501-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="cf501-179">В этом разделе мы добавим страницу HTML, которая использует AJAX для вызова веб-API.</span><span class="sxs-lookup"><span data-stu-id="cf501-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="cf501-180">Мы будем использовать jQuery для выполнения вызовов AJAX, а также для обновления страницы с результатами.</span><span class="sxs-lookup"><span data-stu-id="cf501-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="cf501-181">В обозреватель решений щелкните правой кнопкой мыши проект и выберите **Добавить**, а затем выберите **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="cf501-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="cf501-182">В диалоговом окне **Добавление нового элемента** выберите **веб-** узел в **разделе C#визуальный** элемент, а затем выберите **HTML Page** .</span><span class="sxs-lookup"><span data-stu-id="cf501-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="cf501-183">Присвойте странице имя &quot;index. HTML&quot;.</span><span class="sxs-lookup"><span data-stu-id="cf501-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="cf501-184">Замените все в этом файле следующим:</span><span class="sxs-lookup"><span data-stu-id="cf501-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="cf501-185">Для получения jQuery можно использовать следующие способы.</span><span class="sxs-lookup"><span data-stu-id="cf501-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="cf501-186">В этом примере я использовал [CDN Microsoft AJAX](../../../ajax/cdn/overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf501-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="cf501-187">Его также можно скачать из [http://jquery.com/](http://jquery.com/), а шаблон проекта веб-API ASP.NET включает также jQuery.</span><span class="sxs-lookup"><span data-stu-id="cf501-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="cf501-188">Получение списка продуктов</span><span class="sxs-lookup"><span data-stu-id="cf501-188">Getting a List of Products</span></span>

<span data-ttu-id="cf501-189">Чтобы получить список продуктов, отправьте запрос HTTP GET в &quot;&quot;/АПИ/Продуктс.</span><span class="sxs-lookup"><span data-stu-id="cf501-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="cf501-190">Функция jQuery [JSON](http://api.jquery.com/jQuery.getJSON/) ОТПРАВЛЯЕТ запрос Ajax.</span><span class="sxs-lookup"><span data-stu-id="cf501-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="cf501-191">Ответ содержит массив объектов JSON.</span><span class="sxs-lookup"><span data-stu-id="cf501-191">The response contains array of JSON objects.</span></span> <span data-ttu-id="cf501-192">Функция `done` указывает обратный вызов, который вызывается при удачном выполнении запроса.</span><span class="sxs-lookup"><span data-stu-id="cf501-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="cf501-193">В ответном вызове мы обновляем модель DOM с помощью сведений о продукте.</span><span class="sxs-lookup"><span data-stu-id="cf501-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="cf501-194">Получение продукта по ИДЕНТИФИКАТОРу</span><span class="sxs-lookup"><span data-stu-id="cf501-194">Getting a Product By ID</span></span>

<span data-ttu-id="cf501-195">Чтобы получить продукт по ИДЕНТИФИКАТОРу, отправьте запрос HTTP GET в &quot;*идентификатор* /АПИ/Продуктс/&quot;, где *ID* — это идентификатор продукта.</span><span class="sxs-lookup"><span data-stu-id="cf501-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="cf501-196">Мы по-прежнему вызываем `getJSON` для отправки запроса AJAX, но на этот раз идентификатор помещается в URI запроса.</span><span class="sxs-lookup"><span data-stu-id="cf501-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="cf501-197">Ответ этого запроса представляет собой представление JSON одного продукта.</span><span class="sxs-lookup"><span data-stu-id="cf501-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="cf501-198">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="cf501-198">Running the Application</span></span>

<span data-ttu-id="cf501-199">Нажмите клавишу F5 для запуска отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="cf501-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="cf501-200">Веб-страница должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cf501-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="cf501-201">Чтобы получить продукт по ИДЕНТИФИКАТОРу, введите идентификатор и нажмите кнопку Поиск:</span><span class="sxs-lookup"><span data-stu-id="cf501-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="cf501-202">При вводе недопустимого идентификатора сервер возвращает ошибку HTTP:</span><span class="sxs-lookup"><span data-stu-id="cf501-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="cf501-203">Использование F12 для просмотра HTTP-запроса и ответа</span><span class="sxs-lookup"><span data-stu-id="cf501-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="cf501-204">При работе со службой HTTP может быть полезно просмотреть сообщения HTTP-запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="cf501-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and response messages.</span></span> <span data-ttu-id="cf501-205">Это можно сделать с помощью средств разработчика F12 в Internet Explorer 9.</span><span class="sxs-lookup"><span data-stu-id="cf501-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="cf501-206">В Internet Explorer 9 нажмите клавишу **F12** , чтобы открыть средства.</span><span class="sxs-lookup"><span data-stu-id="cf501-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="cf501-207">Перейдите на вкладку **сеть** и нажмите кнопку **начать запись**.</span><span class="sxs-lookup"><span data-stu-id="cf501-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="cf501-208">Теперь вернитесь на веб-страницу и нажмите клавишу **F5** , чтобы перезагрузить веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="cf501-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="cf501-209">Internet Explorer захватывает трафик HTTP между браузером и веб-сервером.</span><span class="sxs-lookup"><span data-stu-id="cf501-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="cf501-210">В представлении "Сводка" отображается весь сетевой трафик для страницы:</span><span class="sxs-lookup"><span data-stu-id="cf501-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="cf501-211">Нахождение записи относительно URI "API/Products/".</span><span class="sxs-lookup"><span data-stu-id="cf501-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="cf501-212">Выберите эту запись и щелкните **Перейти к подробному просмотру**.</span><span class="sxs-lookup"><span data-stu-id="cf501-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="cf501-213">В подробном представлении имеются вкладки для просмотра заголовков запроса и ответа и текста.</span><span class="sxs-lookup"><span data-stu-id="cf501-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="cf501-214">Например, если щелкнуть вкладку **заголовки запросов** , можно увидеть, что клиент запросил &quot;Application/JSON&quot; в заголовке Accept.</span><span class="sxs-lookup"><span data-stu-id="cf501-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="cf501-215">Если щелкнуть вкладку текст ответа, можно увидеть, как список продуктов был сериализован в JSON.</span><span class="sxs-lookup"><span data-stu-id="cf501-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="cf501-216">Другие браузеры имеют аналогичные функции.</span><span class="sxs-lookup"><span data-stu-id="cf501-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="cf501-217">Другой полезный инструмент — [Fiddler](http://www.fiddler2.com/fiddler2/), прокси-сервер отладки.</span><span class="sxs-lookup"><span data-stu-id="cf501-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="cf501-218">Fiddler можно использовать для просмотра HTTP-трафика, а также для составления HTTP-запросов, что дает полный контроль над заголовками HTTP в запросе.</span><span class="sxs-lookup"><span data-stu-id="cf501-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="cf501-219">См. приложение, работающее в Azure</span><span class="sxs-lookup"><span data-stu-id="cf501-219">See this App Running on Azure</span></span>

<span data-ttu-id="cf501-220">Вы хотите увидеть готовый сайт, работающий как активное веб-приложение?</span><span class="sxs-lookup"><span data-stu-id="cf501-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="cf501-221">Вы можете развернуть полную версию приложения в учетной записи Azure, просто нажав кнопку ниже.</span><span class="sxs-lookup"><span data-stu-id="cf501-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="cf501-222">Для развертывания этого решения в Azure необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="cf501-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="cf501-223">Если у вас еще нет учетной записи, возможны следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="cf501-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="cf501-224">[Откройте учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) — вы получаете кредиты, которые можно использовать для пробного использования платных служб Azure, и даже после их использования вы можете удержать учетную запись и использовать бесплатные службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cf501-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="cf501-225">[Активация преимуществ для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) . Ваша подписка MSDN предоставляет Вам кредиты каждый месяц, который можно использовать для платных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="cf501-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf501-226">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cf501-226">Next Steps</span></span>

- <span data-ttu-id="cf501-227">Более полный пример службы HTTP, поддерживающей действия POST, WHERE и DELETE и записывающих данные в базу данных, см. в разделе [Использование веб-API 2 с Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span><span class="sxs-lookup"><span data-stu-id="cf501-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="cf501-228">Дополнительные сведения о создании гибких и реагирующих веб-приложений поверх службы HTTP см. в разделе [одностраничное приложение ASP.NET](../../../single-page-application/index.md).</span><span class="sxs-lookup"><span data-stu-id="cf501-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="cf501-229">Сведения о том, как развернуть веб-проект Visual Studio в службе приложений Azure, см. [в статье Создание веб-приложения ASP.NET в службе приложений Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span><span class="sxs-lookup"><span data-stu-id="cf501-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
