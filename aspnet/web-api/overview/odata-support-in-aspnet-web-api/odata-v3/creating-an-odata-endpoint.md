---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Создание конечной точки OData v3 с помощью веб-API 2 | Документация Майкрософт
author: MikeWasson
description: Open Data Protocol (OData) — это протокол доступа к данным для Интернета. OData обеспечивает единообразный способ структурирования данных, запроса данных и обработки данных...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448224"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="83709-104">Создание конечной точки OData v3 с веб-API 2</span><span class="sxs-lookup"><span data-stu-id="83709-104">Creating an OData v3 Endpoint with Web API 2</span></span>

<span data-ttu-id="83709-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="83709-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="83709-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="83709-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="83709-107">[Open Data Protocol](http://www.odata.org/) (OData) — это протокол доступа к данным для Интернета.</span><span class="sxs-lookup"><span data-stu-id="83709-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="83709-108">OData обеспечивает единообразный способ структурирования данных, выполнения запросов к данным и управления набором данных с помощью операций CRUD (создание, чтение, обновление и удаление).</span><span class="sxs-lookup"><span data-stu-id="83709-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="83709-109">OData поддерживает форматы AtomPub (XML) и JSON.</span><span class="sxs-lookup"><span data-stu-id="83709-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="83709-110">OData также определяет способ предоставления метаданных о данных.</span><span class="sxs-lookup"><span data-stu-id="83709-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="83709-111">Клиенты могут использовать метаданные для обнаружения сведений о типе и связей для набора данных.</span><span class="sxs-lookup"><span data-stu-id="83709-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="83709-112">Веб-API ASP.NET позволяет легко создать конечную точку OData для набора данных.</span><span class="sxs-lookup"><span data-stu-id="83709-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="83709-113">Вы можете точно контролировать, какие операции OData поддерживает конечная точка.</span><span class="sxs-lookup"><span data-stu-id="83709-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="83709-114">Можно разместить несколько конечных точек OData вместе с конечными точками, отличными от OData.</span><span class="sxs-lookup"><span data-stu-id="83709-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="83709-115">Вы имеете полный контроль над моделью данных, внутренней бизнес-логикой и уровнем данных.</span><span class="sxs-lookup"><span data-stu-id="83709-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="83709-116">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="83709-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="83709-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="83709-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="83709-118">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="83709-118">Web API 2</span></span>
> - <span data-ttu-id="83709-119">OData версии 3</span><span class="sxs-lookup"><span data-stu-id="83709-119">OData Version 3</span></span>
> - <span data-ttu-id="83709-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="83709-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="83709-121">Fiddler веб-прокси отладки (необязательно)</span><span class="sxs-lookup"><span data-stu-id="83709-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="83709-122">Поддержка веб-API OData добавлена в [ASP.NET and Web Tools обновление 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="83709-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="83709-123">Однако в этом руководстве используется формирование шаблонов, добавленное в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="83709-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>

<span data-ttu-id="83709-124">В этом руководстве вы создадите простую конечную точку OData, которую клиенты смогут запрашивать.</span><span class="sxs-lookup"><span data-stu-id="83709-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="83709-125">Вы также создадите C# клиент для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="83709-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="83709-126">После завершения работы с этим руководством в следующем наборе руководств показано, как добавить дополнительные функции, включая отношения сущностей, действия и $expand/$select.</span><span class="sxs-lookup"><span data-stu-id="83709-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="83709-127">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="83709-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="83709-128">Добавление модели сущностей</span><span class="sxs-lookup"><span data-stu-id="83709-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="83709-129">Добавление контроллера OData</span><span class="sxs-lookup"><span data-stu-id="83709-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="83709-130">Добавление модели EDM и маршрута</span><span class="sxs-lookup"><span data-stu-id="83709-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="83709-131">Заполнение базы данных (необязательно)</span><span class="sxs-lookup"><span data-stu-id="83709-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="83709-132">Изучение конечной точки OData</span><span class="sxs-lookup"><span data-stu-id="83709-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="83709-133">Форматы сериализации OData</span><span class="sxs-lookup"><span data-stu-id="83709-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="83709-134">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="83709-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="83709-135">В этом руководстве вы создадите конечную точку OData, которая поддерживает базовые операции CRUD.</span><span class="sxs-lookup"><span data-stu-id="83709-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="83709-136">Конечная точка будет предоставлять один ресурс, список продуктов.</span><span class="sxs-lookup"><span data-stu-id="83709-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="83709-137">В последующих руководствах будут добавлены дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="83709-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="83709-138">Запустите Visual Studio и выберите **создать проект** на начальной странице.</span><span class="sxs-lookup"><span data-stu-id="83709-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="83709-139">Либо в меню **файл** выберите **создать** , а затем — **проект**.</span><span class="sxs-lookup"><span data-stu-id="83709-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="83709-140">В области **шаблоны** выберите **Установленные шаблоны** и разверните узел визуального C# элемента.</span><span class="sxs-lookup"><span data-stu-id="83709-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="83709-141">В **разделе C#визуальный** элемент выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="83709-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="83709-142">Выберите шаблон **веб-приложение ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="83709-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="83709-143">В диалоговом окне **Новый проект ASP.NET** выберите **пустой** шаблон.</span><span class="sxs-lookup"><span data-stu-id="83709-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="83709-144">В разделе &quot;добавить папки и основные ссылки для...&quot;, проверьте **веб-API**.</span><span class="sxs-lookup"><span data-stu-id="83709-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="83709-145">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="83709-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="83709-146">Добавление модели сущностей</span><span class="sxs-lookup"><span data-stu-id="83709-146">Add an Entity Model</span></span>

<span data-ttu-id="83709-147">*Модель* — это объект, который представляет данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="83709-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="83709-148">Для работы с этим руководством нам нужна модель, представляющая продукт.</span><span class="sxs-lookup"><span data-stu-id="83709-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="83709-149">Модель соответствует типу сущности OData.</span><span class="sxs-lookup"><span data-stu-id="83709-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="83709-150">В обозревателе решений щелкните правой кнопкой мыши папку Models.</span><span class="sxs-lookup"><span data-stu-id="83709-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="83709-151">В контекстном меню выберите **Добавить**, а затем выберите **Класс**.</span><span class="sxs-lookup"><span data-stu-id="83709-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="83709-152">В диалоговом окне **Добавление нового** элемента назовите класс &quot;&quot;продукта.</span><span class="sxs-lookup"><span data-stu-id="83709-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="83709-153">По соглашению классы модели помещаются в папку Models.</span><span class="sxs-lookup"><span data-stu-id="83709-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="83709-154">Вам не нужно следовать этому соглашению в своих проектах, но мы будем использовать его в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="83709-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>

<span data-ttu-id="83709-155">В файле Product.cs добавьте следующее определение класса:</span><span class="sxs-lookup"><span data-stu-id="83709-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="83709-156">Свойство ID будет ключом сущности.</span><span class="sxs-lookup"><span data-stu-id="83709-156">The ID property will be the entity key.</span></span> <span data-ttu-id="83709-157">Клиенты могут запрашивать продукты по ИДЕНТИФИКАТОРу.</span><span class="sxs-lookup"><span data-stu-id="83709-157">Clients can query products by ID.</span></span> <span data-ttu-id="83709-158">Это поле также будет первичным ключом в серверной базе данных.</span><span class="sxs-lookup"><span data-stu-id="83709-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="83709-159">Постройте проект прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="83709-159">Build the project now.</span></span> <span data-ttu-id="83709-160">На следующем шаге мы будем использовать некоторые шаблоны Visual Studio, использующие отражение для поиска типа продукта.</span><span class="sxs-lookup"><span data-stu-id="83709-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="83709-161">Добавление контроллера OData</span><span class="sxs-lookup"><span data-stu-id="83709-161">Add an OData Controller</span></span>

<span data-ttu-id="83709-162">*Контроллер* — это класс, который обрабатывает HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="83709-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="83709-163">Вы определяете отдельный контроллер для каждого набора сущностей в службе OData.</span><span class="sxs-lookup"><span data-stu-id="83709-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="83709-164">В этом руководстве мы создадим один контроллер.</span><span class="sxs-lookup"><span data-stu-id="83709-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="83709-165">В обозреватель решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="83709-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="83709-166">Щелкните **Добавить**, а затем выберите **Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="83709-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="83709-167">В диалоговом окне **Добавление шаблона** выберите &quot;контроллер OData веб-API 2 с действиями с помощью Entity Framework&quot;.</span><span class="sxs-lookup"><span data-stu-id="83709-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="83709-168">В диалоговом окне **Добавление контроллера** назовите контроллер «продуктсконтроллер».</span><span class="sxs-lookup"><span data-stu-id="83709-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="83709-169">Установите флажок &quot;использовать действия асинхронного контроллера&quot;.</span><span class="sxs-lookup"><span data-stu-id="83709-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="83709-170">В раскрывающемся списке **модель** выберите класс Product.</span><span class="sxs-lookup"><span data-stu-id="83709-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="83709-171">Нажмите кнопку **создать контекст данных...** .</span><span class="sxs-lookup"><span data-stu-id="83709-171">Click the **New data context...** button.</span></span> <span data-ttu-id="83709-172">Оставьте имя по умолчанию для типа контекста данных и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83709-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="83709-173">Нажмите кнопку Добавить в диалоговом окне Добавление контроллера, чтобы добавить контроллер.</span><span class="sxs-lookup"><span data-stu-id="83709-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="83709-174">Примечание. при получении сообщения об ошибке с сообщением &quot;ошибка при получении типа...&quot;убедитесь, что проект Visual Studio создан после добавления класса Product.</span><span class="sxs-lookup"><span data-stu-id="83709-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="83709-175">Формирование шаблонов использует отражение для поиска класса.</span><span class="sxs-lookup"><span data-stu-id="83709-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="83709-176">Формирование шаблонов добавляет в проект два файла кода:</span><span class="sxs-lookup"><span data-stu-id="83709-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="83709-177">Products.cs Определяет контроллер веб-API, который реализует конечную точку OData.</span><span class="sxs-lookup"><span data-stu-id="83709-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="83709-178">ProductServiceContext.cs предоставляет методы для запроса к базовой базе данных с помощью Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="83709-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="83709-179">Добавление модели EDM и маршрута</span><span class="sxs-lookup"><span data-stu-id="83709-179">Add the EDM and Route</span></span>

<span data-ttu-id="83709-180">В обозреватель решений разверните папку приложение\_запуск и откройте файл с именем WebApiConfig.cs.</span><span class="sxs-lookup"><span data-stu-id="83709-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="83709-181">Этот класс содержит код конфигурации для веб-API.</span><span class="sxs-lookup"><span data-stu-id="83709-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="83709-182">Замените этот код следующим:</span><span class="sxs-lookup"><span data-stu-id="83709-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="83709-183">Этот код выполняет два действия:</span><span class="sxs-lookup"><span data-stu-id="83709-183">This code does two things:</span></span>

- <span data-ttu-id="83709-184">Создает EDM (модель EDM) для конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="83709-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="83709-185">Добавляет маршрут для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="83709-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="83709-186">EDM — это абстрактная модель данных.</span><span class="sxs-lookup"><span data-stu-id="83709-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="83709-187">Модель EDM используется для создания документа метаданных и определения URI для службы.</span><span class="sxs-lookup"><span data-stu-id="83709-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="83709-188">**Одатаконвентионмоделбуилдер** создает EDM с помощью набора соглашений об именовании по умолчанию EDM.</span><span class="sxs-lookup"><span data-stu-id="83709-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="83709-189">Этот подход требует наименьшего кода.</span><span class="sxs-lookup"><span data-stu-id="83709-189">This approach requires the least code.</span></span> <span data-ttu-id="83709-190">Если требуется больший контроль над EDM, можно использовать класс **одатамоделбуилдер** для создания модели EDM путем явного добавления свойств, ключей и свойств навигации.</span><span class="sxs-lookup"><span data-stu-id="83709-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="83709-191">Метод **EntitySet** добавляет набор сущностей в модель EDM:</span><span class="sxs-lookup"><span data-stu-id="83709-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="83709-192">Строка "Products" определяет имя набора сущностей.</span><span class="sxs-lookup"><span data-stu-id="83709-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="83709-193">Имя контроллера должно совпадать с именем набора сущностей.</span><span class="sxs-lookup"><span data-stu-id="83709-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="83709-194">В этом руководстве набор сущностей называется "Products", а контроллер называется `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="83709-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="83709-195">При именовании набора сущностей "набор продуктов" имя контроллера будет называться `ProductSetController`.</span><span class="sxs-lookup"><span data-stu-id="83709-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="83709-196">Обратите внимание, что конечная точка может иметь несколько наборов сущностей.</span><span class="sxs-lookup"><span data-stu-id="83709-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="83709-197">Вызовите **entityset&lt;t&gt;** для каждого набора сущностей, а затем определите соответствующий контроллер.</span><span class="sxs-lookup"><span data-stu-id="83709-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="83709-198">Метод **маподатарауте** добавляет маршрут для конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="83709-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="83709-199">Первый параметр — это понятное имя маршрута.</span><span class="sxs-lookup"><span data-stu-id="83709-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="83709-200">Клиенты службы не видят это имя.</span><span class="sxs-lookup"><span data-stu-id="83709-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="83709-201">Вторым параметром является префикс URI для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="83709-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="83709-202">Учитывая этот код, URI для набора сущностей Products — http://<em>имя узла</em>/одата/Продуктс.</span><span class="sxs-lookup"><span data-stu-id="83709-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="83709-203">Приложение может иметь более одной конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="83709-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="83709-204">Для каждой конечной точки вызовите <strong>маподатарауте</strong> и укажите уникальное имя маршрута и уникальный префикс URI.</span><span class="sxs-lookup"><span data-stu-id="83709-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="83709-205">Заполнение базы данных (необязательно)</span><span class="sxs-lookup"><span data-stu-id="83709-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="83709-206">На этом шаге вы будете использовать Entity Framework для заполнения базы данных некоторыми тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="83709-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="83709-207">Этот шаг является необязательным, но он позволяет сразу же протестировать конечную точку OData.</span><span class="sxs-lookup"><span data-stu-id="83709-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="83709-208">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="83709-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="83709-209">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="83709-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="83709-210">При этом добавляется папка с именем Migrations и файл кода с именем Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="83709-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="83709-211">Откройте этот файл и добавьте следующий код в метод `Configuration.Seed`.</span><span class="sxs-lookup"><span data-stu-id="83709-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="83709-212">В окне консоли диспетчера пакетов введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="83709-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="83709-213">Эти команды создают код, который создает базу данных, а затем выполняет этот код.</span><span class="sxs-lookup"><span data-stu-id="83709-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="83709-214">Изучение конечной точки OData</span><span class="sxs-lookup"><span data-stu-id="83709-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="83709-215">В этом разделе мы будем использовать [прокси веб-отладки Fiddler](http://www.fiddler2.com) для отправки запросов в конечную точку и проверки ответных сообщений.</span><span class="sxs-lookup"><span data-stu-id="83709-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="83709-216">Это поможет понять возможности конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="83709-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="83709-217">В Visual Studio нажмите клавишу F5, чтобы начать отладку.</span><span class="sxs-lookup"><span data-stu-id="83709-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="83709-218">По умолчанию Visual Studio открывает браузер для `http://localhost:*port*`, где *Port* — номер порта, настроенный в параметрах проекта.</span><span class="sxs-lookup"><span data-stu-id="83709-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="83709-219">Номер порта можно изменить в параметрах проекта.</span><span class="sxs-lookup"><span data-stu-id="83709-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="83709-220">В обозреватель решений щелкните правой кнопкой мыши проект и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="83709-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="83709-221">В окне Свойства выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="83709-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="83709-222">Введите номер порта в поле **URL-адрес проекта**.</span><span class="sxs-lookup"><span data-stu-id="83709-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="83709-223">Сервисный документ</span><span class="sxs-lookup"><span data-stu-id="83709-223">Service Document</span></span>

<span data-ttu-id="83709-224">*Сервисный документ* содержит список наборов сущностей для конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="83709-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="83709-225">Чтобы получить сервисный документ, отправьте запрос GET на корневой URI службы.</span><span class="sxs-lookup"><span data-stu-id="83709-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="83709-226">С помощью Fiddler введите следующий URI на вкладке **Composer** : `http://localhost:port/odata/`, где *Port* — номер порта.</span><span class="sxs-lookup"><span data-stu-id="83709-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="83709-227">Нажмите кнопку **Выполнить** .</span><span class="sxs-lookup"><span data-stu-id="83709-227">Click the **Execute** button.</span></span> <span data-ttu-id="83709-228">Fiddler отправляет в приложение запрос HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="83709-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="83709-229">Ответ должен отобразиться в списке веб-сеансов.</span><span class="sxs-lookup"><span data-stu-id="83709-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="83709-230">Если все работает, код состояния будет 200.</span><span class="sxs-lookup"><span data-stu-id="83709-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="83709-231">Дважды щелкните ответ в списке веб-сеансов, чтобы просмотреть подробные сведения о ответном сообщении на вкладке Инспекторы.</span><span class="sxs-lookup"><span data-stu-id="83709-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="83709-232">Необработанное ответное сообщение HTTP должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="83709-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="83709-233">По умолчанию веб-API возвращает сервисный документ в формате AtomPub.</span><span class="sxs-lookup"><span data-stu-id="83709-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="83709-234">Чтобы запросить JSON, добавьте следующий заголовок в HTTP-запрос:</span><span class="sxs-lookup"><span data-stu-id="83709-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="83709-235">Теперь ответ HTTP содержит полезные данные JSON:</span><span class="sxs-lookup"><span data-stu-id="83709-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="83709-236">Документ метаданных службы</span><span class="sxs-lookup"><span data-stu-id="83709-236">Service Metadata Document</span></span>

<span data-ttu-id="83709-237">В *документе метаданных службы* описывается модель данных службы с помощью языка XML, который НАЗЫВАЕТСЯ языком CSDL.</span><span class="sxs-lookup"><span data-stu-id="83709-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="83709-238">В документе метаданных представлена структура данных в службе, которую можно использовать для создания клиентского кода.</span><span class="sxs-lookup"><span data-stu-id="83709-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="83709-239">Чтобы получить документ метаданных, отправьте запрос GET в `http://localhost:port/odata/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="83709-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="83709-240">Ниже приведены метаданные для конечной точки, показанной в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="83709-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="83709-241">Набор сущностей</span><span class="sxs-lookup"><span data-stu-id="83709-241">Entity Set</span></span>

<span data-ttu-id="83709-242">Чтобы получить набор сущностей Products, отправьте запрос GET в `http://localhost:port/odata/Products`.</span><span class="sxs-lookup"><span data-stu-id="83709-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="83709-243">Сущность</span><span class="sxs-lookup"><span data-stu-id="83709-243">Entity</span></span>

<span data-ttu-id="83709-244">Чтобы получить отдельный продукт, отправьте запрос GET в `http://localhost:port/odata/Products(1)`, где "1" — это идентификатор продукта.</span><span class="sxs-lookup"><span data-stu-id="83709-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="83709-245">Форматы сериализации OData</span><span class="sxs-lookup"><span data-stu-id="83709-245">OData Serialization Formats</span></span>

<span data-ttu-id="83709-246">OData поддерживает несколько форматов сериализации:</span><span class="sxs-lookup"><span data-stu-id="83709-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="83709-247">Файл Atom (XML)</span><span class="sxs-lookup"><span data-stu-id="83709-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="83709-248">JSON "Light" (появился в OData v3)</span><span class="sxs-lookup"><span data-stu-id="83709-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="83709-249">JSON "verbose" (OData v2)</span><span class="sxs-lookup"><span data-stu-id="83709-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="83709-250">По умолчанию веб-API использует формат "Light" Атомпубжсон.</span><span class="sxs-lookup"><span data-stu-id="83709-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="83709-251">Чтобы получить формат AtomPub, задайте для заголовка Accept значение "Application/Atom + XML".</span><span class="sxs-lookup"><span data-stu-id="83709-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="83709-252">Вот пример тела запроса:</span><span class="sxs-lookup"><span data-stu-id="83709-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="83709-253">Можно увидеть один из очевидных недостатков формата Atom: он является гораздо более подробным, чем источник JSON.</span><span class="sxs-lookup"><span data-stu-id="83709-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="83709-254">Однако если у вас есть клиент, который понимает AtomPub, клиент может предпочесть этот формат через JSON.</span><span class="sxs-lookup"><span data-stu-id="83709-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="83709-255">Ниже приведена легкая версия JSON той же сущности:</span><span class="sxs-lookup"><span data-stu-id="83709-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="83709-256">Формат JSON появился в версии 3 протокола OData.</span><span class="sxs-lookup"><span data-stu-id="83709-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="83709-257">Для обеспечения обратной совместимости клиент может запросить старый формат JSON "verbose".</span><span class="sxs-lookup"><span data-stu-id="83709-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="83709-258">Чтобы запросить подробный JSON, задайте для заголовка Accept значение `application/json;odata=verbose`.</span><span class="sxs-lookup"><span data-stu-id="83709-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="83709-259">Ниже приведена подробная версия:</span><span class="sxs-lookup"><span data-stu-id="83709-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="83709-260">Этот формат передает больше метаданных в тексте ответа, что может значительно увеличить нагрузку на весь сеанс.</span><span class="sxs-lookup"><span data-stu-id="83709-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="83709-261">Кроме того, он добавляет уровень косвенного обращения, упаковывая объект в свойство с именем «d».</span><span class="sxs-lookup"><span data-stu-id="83709-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="83709-262">Next Steps</span><span class="sxs-lookup"><span data-stu-id="83709-262">Next Steps</span></span>

- [<span data-ttu-id="83709-263">Добавление связей сущностей</span><span class="sxs-lookup"><span data-stu-id="83709-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="83709-264">Добавление действий OData</span><span class="sxs-lookup"><span data-stu-id="83709-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="83709-265">Вызов службы OData из клиента .NET</span><span class="sxs-lookup"><span data-stu-id="83709-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
