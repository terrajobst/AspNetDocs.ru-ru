---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: Создание конечной точки OData v4 с помощью веб-API ASP.NET 2,2 | Документация Майкрософт
author: MikeWasson
description: Open Data Protocol (OData) — это протокол доступа к данным для Интернета. OData обеспечивает единообразный способ запроса и обработки наборов данных с помощью операций CRUD...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484500"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="9f01a-104">Создание конечной точки OData v4 с помощью веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9f01a-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="9f01a-105">Open Data Protocol (OData) — это протокол доступа к данным для Интернета.</span><span class="sxs-lookup"><span data-stu-id="9f01a-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="9f01a-106">OData обеспечивает единообразный способ запроса и обработки наборов данных с помощью операций CRUD (создание, чтение, обновление и удаление).</span><span class="sxs-lookup"><span data-stu-id="9f01a-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="9f01a-107">Веб-API ASP.NET поддерживает протокол версии v3 и v4.</span><span class="sxs-lookup"><span data-stu-id="9f01a-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="9f01a-108">Можно даже иметь конечную точку V4, которая работает параллельно с конечной точкой v3.</span><span class="sxs-lookup"><span data-stu-id="9f01a-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="9f01a-109">В этом руководстве показано, как создать конечную точку OData V4, которая поддерживает операции CRUD.</span><span class="sxs-lookup"><span data-stu-id="9f01a-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9f01a-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="9f01a-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="9f01a-111">Веб-API 5,2</span><span class="sxs-lookup"><span data-stu-id="9f01a-111">Web API 5.2</span></span>
> - <span data-ttu-id="9f01a-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="9f01a-112">OData v4</span></span>
> - <span data-ttu-id="9f01a-113">Visual Studio 2017 (загрузить Visual Studio 2017 [здесь](https://visualstudio.microsoft.com/downloads/))</span><span class="sxs-lookup"><span data-stu-id="9f01a-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="9f01a-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="9f01a-114">Entity Framework 6</span></span>
> - <span data-ttu-id="9f01a-115">4\.7.2 .NET</span><span class="sxs-lookup"><span data-stu-id="9f01a-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="9f01a-116">Учебные версии</span><span class="sxs-lookup"><span data-stu-id="9f01a-116">Tutorial versions</span></span>
>
> <span data-ttu-id="9f01a-117">Сведения о OData версии 3 см. в разделе [Создание конечной точки OData v3](../odata-v3/creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="9f01a-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="9f01a-118">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9f01a-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="9f01a-119">В Visual Studio в меню **файл** выберите пункт **создать** &gt; **проект**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="9f01a-120">Разверните узел **установленные** &gt; **Visual C#**  &gt; **Web**и выберите шаблон **веб-приложение ASP.NET (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="9f01a-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="9f01a-121">Присвойте проекту имя &quot;Продуктсервице&quot;.</span><span class="sxs-lookup"><span data-stu-id="9f01a-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="9f01a-122">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-122">Select **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="9f01a-123">Выберите шаблон **Пустой**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-123">Select the **Empty** template.</span></span> <span data-ttu-id="9f01a-124">В разделе **Добавление папок и основных ссылок для:** выберите **веб-API**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="9f01a-125">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="9f01a-126">Установка пакетов OData</span><span class="sxs-lookup"><span data-stu-id="9f01a-126">Install the OData packages</span></span>

<span data-ttu-id="9f01a-127">В меню **Сервис**  последовательно выберите пункты **Диспетчер пакетов NuGet** &gt; **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="9f01a-128">В окне консоли диспетчера пакетов введите:</span><span class="sxs-lookup"><span data-stu-id="9f01a-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="9f01a-129">Эта команда устанавливает последние пакеты NuGet OData.</span><span class="sxs-lookup"><span data-stu-id="9f01a-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="9f01a-130">Добавление класса модели</span><span class="sxs-lookup"><span data-stu-id="9f01a-130">Add a model class</span></span>

<span data-ttu-id="9f01a-131">*Модель* — это объект, представляющий сущность данных в приложении.</span><span class="sxs-lookup"><span data-stu-id="9f01a-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="9f01a-132">В обозревателе решений щелкните правой кнопкой мыши папку Models.</span><span class="sxs-lookup"><span data-stu-id="9f01a-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="9f01a-133">В контекстном меню выберите **добавить** &gt; **класс**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="9f01a-134">По соглашению классы модели помещаются в папку Models, но вам не нужно следовать этому соглашению в своих проектах.</span><span class="sxs-lookup"><span data-stu-id="9f01a-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>

<span data-ttu-id="9f01a-135">Назовите класс `Product`.</span><span class="sxs-lookup"><span data-stu-id="9f01a-135">Name the class `Product`.</span></span> <span data-ttu-id="9f01a-136">В файле Product.cs замените стандартный код следующим:</span><span class="sxs-lookup"><span data-stu-id="9f01a-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="9f01a-137">Свойство `Id` — это ключ сущности.</span><span class="sxs-lookup"><span data-stu-id="9f01a-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="9f01a-138">Клиенты могут запрашивать сущности по ключу.</span><span class="sxs-lookup"><span data-stu-id="9f01a-138">Clients can query entities by key.</span></span> <span data-ttu-id="9f01a-139">Например, чтобы получить продукт с ИДЕНТИФИКАТОРом 5, URI `/Products(5)`.</span><span class="sxs-lookup"><span data-stu-id="9f01a-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="9f01a-140">Свойство `Id` также будет первичным ключом в серверной базе данных.</span><span class="sxs-lookup"><span data-stu-id="9f01a-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="9f01a-141">Включить Entity Framework</span><span class="sxs-lookup"><span data-stu-id="9f01a-141">Enable Entity Framework</span></span>

<span data-ttu-id="9f01a-142">В этом руководстве мы будем использовать Entity Framework (EF) Code First для создания серверной базы данных.</span><span class="sxs-lookup"><span data-stu-id="9f01a-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="9f01a-143">Для веб-API OData не требуется EF.</span><span class="sxs-lookup"><span data-stu-id="9f01a-143">Web API OData does not require EF.</span></span> <span data-ttu-id="9f01a-144">Используйте любой уровень доступа к данным, который может переводить сущности базы данных в модели.</span><span class="sxs-lookup"><span data-stu-id="9f01a-144">Use any data-access layer that can translate database entities into models.</span></span>

<span data-ttu-id="9f01a-145">Сначала установите пакет NuGet для EF.</span><span class="sxs-lookup"><span data-stu-id="9f01a-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="9f01a-146">В меню **Сервис**  последовательно выберите пункты **Диспетчер пакетов NuGet** &gt; **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="9f01a-147">В окне консоли диспетчера пакетов введите:</span><span class="sxs-lookup"><span data-stu-id="9f01a-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="9f01a-148">Откройте файл Web. config и добавьте следующий раздел в элемент **Configuration** после элемента **configSections** .</span><span class="sxs-lookup"><span data-stu-id="9f01a-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="9f01a-149">Этот параметр добавляет строку подключения для базы данных LocalDB.</span><span class="sxs-lookup"><span data-stu-id="9f01a-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="9f01a-150">Эта база данных будет использоваться при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="9f01a-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="9f01a-151">Затем добавьте класс с именем `ProductsContext` в папку Models:</span><span class="sxs-lookup"><span data-stu-id="9f01a-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="9f01a-152">В конструкторе `"name=ProductsContext"` выдает имя строки подключения.</span><span class="sxs-lookup"><span data-stu-id="9f01a-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="9f01a-153">Настройка конечной точки OData</span><span class="sxs-lookup"><span data-stu-id="9f01a-153">Configure the OData endpoint</span></span>

<span data-ttu-id="9f01a-154">Откройте файл App\_Start/WebApiConfig. cs.</span><span class="sxs-lookup"><span data-stu-id="9f01a-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="9f01a-155">Добавьте следующие операторы **using** :</span><span class="sxs-lookup"><span data-stu-id="9f01a-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="9f01a-156">Затем добавьте следующий код в метод **Register** :</span><span class="sxs-lookup"><span data-stu-id="9f01a-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="9f01a-157">Этот код выполняет два действия:</span><span class="sxs-lookup"><span data-stu-id="9f01a-157">This code does two things:</span></span>

- <span data-ttu-id="9f01a-158">Создает EDM (модель EDM).</span><span class="sxs-lookup"><span data-stu-id="9f01a-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="9f01a-159">Добавляет маршрут.</span><span class="sxs-lookup"><span data-stu-id="9f01a-159">Adds a route.</span></span>

<span data-ttu-id="9f01a-160">EDM — это абстрактная модель данных.</span><span class="sxs-lookup"><span data-stu-id="9f01a-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="9f01a-161">Модель EDM используется для создания документа метаданных службы.</span><span class="sxs-lookup"><span data-stu-id="9f01a-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="9f01a-162">Класс **одатаконвентионмоделбуилдер** создает модель EDM с использованием соглашений об именовании по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9f01a-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="9f01a-163">Этот подход требует наименьшего кода.</span><span class="sxs-lookup"><span data-stu-id="9f01a-163">This approach requires the least code.</span></span> <span data-ttu-id="9f01a-164">Если требуется больший контроль над EDM, можно использовать класс **одатамоделбуилдер** для создания модели EDM путем явного добавления свойств, ключей и свойств навигации.</span><span class="sxs-lookup"><span data-stu-id="9f01a-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="9f01a-165">*Маршрут* сообщает веб-API о МАРШРУТИЗАЦИИ запросов HTTP к конечной точке.</span><span class="sxs-lookup"><span data-stu-id="9f01a-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="9f01a-166">Чтобы создать маршрут OData V4, вызовите метод расширения **маподатасервицерауте** .</span><span class="sxs-lookup"><span data-stu-id="9f01a-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="9f01a-167">Если в приложении есть несколько конечных точек OData, создайте отдельный маршрут для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="9f01a-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="9f01a-168">Присвойте каждому маршруту уникальное имя маршрута и префикс.</span><span class="sxs-lookup"><span data-stu-id="9f01a-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="9f01a-169">Добавление контроллера OData</span><span class="sxs-lookup"><span data-stu-id="9f01a-169">Add the OData controller</span></span>

<span data-ttu-id="9f01a-170">*Контроллер* — это класс, который обрабатывает HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="9f01a-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="9f01a-171">Для каждого набора сущностей в службе OData создается отдельный контроллер.</span><span class="sxs-lookup"><span data-stu-id="9f01a-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="9f01a-172">В этом руководстве вы создадите один контроллер для сущности `Product`.</span><span class="sxs-lookup"><span data-stu-id="9f01a-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="9f01a-173">В обозреватель решений щелкните правой кнопкой мыши папку Controllers и выберите пункт **добавить** &gt; **класс**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="9f01a-174">Назовите класс `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="9f01a-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="9f01a-175">В версии этого руководства для OData v3 используется формирование шаблонов для **добавления контроллеров** .</span><span class="sxs-lookup"><span data-stu-id="9f01a-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="9f01a-176">В настоящее время формирование шаблонов для OData v4 не предусмотрено.</span><span class="sxs-lookup"><span data-stu-id="9f01a-176">Currently, there is no scaffolding for OData v4.</span></span>

<span data-ttu-id="9f01a-177">Замените стандартный код в ProductsController.cs следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="9f01a-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="9f01a-178">Контроллер использует класс `ProductsContext` для доступа к базе данных с помощью EF.</span><span class="sxs-lookup"><span data-stu-id="9f01a-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="9f01a-179">Обратите внимание, что контроллер переопределяет метод **Dispose** для удаления **продуктсконтекст**.</span><span class="sxs-lookup"><span data-stu-id="9f01a-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="9f01a-180">Это начальная точка контроллера.</span><span class="sxs-lookup"><span data-stu-id="9f01a-180">This is the starting point for the controller.</span></span> <span data-ttu-id="9f01a-181">Далее мы добавим методы для всех операций CRUD.</span><span class="sxs-lookup"><span data-stu-id="9f01a-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="9f01a-182">Запрос набора сущностей</span><span class="sxs-lookup"><span data-stu-id="9f01a-182">Query the entity set</span></span>

<span data-ttu-id="9f01a-183">Добавьте следующие методы для `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="9f01a-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="9f01a-184">Версия метода `Get` без параметров возвращает коллекцию всех продуктов.</span><span class="sxs-lookup"><span data-stu-id="9f01a-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="9f01a-185">Метод `Get` с параметром *ключа* ищет продукт по ключу (в данном случае свойство `Id`).</span><span class="sxs-lookup"><span data-stu-id="9f01a-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="9f01a-186">Атрибут **[енаблекуери]** позволяет клиентам изменять запрос с помощью параметров запроса, таких как $filter, $sort и $Page.</span><span class="sxs-lookup"><span data-stu-id="9f01a-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="9f01a-187">Дополнительные сведения см. в разделе [Поддержка параметров запросов OData](../supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="9f01a-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="9f01a-188">Добавление сущности в набор сущностей</span><span class="sxs-lookup"><span data-stu-id="9f01a-188">Add an entity to the entity set</span></span>

<span data-ttu-id="9f01a-189">Чтобы позволить клиентам добавлять новый продукт в базу данных, добавьте следующий метод для `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="9f01a-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="9f01a-190">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="9f01a-190">Update an entity</span></span>

<span data-ttu-id="9f01a-191">OData поддерживает две различные семантики для обновления сущности, исправления и размещения.</span><span class="sxs-lookup"><span data-stu-id="9f01a-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="9f01a-192">ИСПРАВЛЕНИЕ выполняет частичное обновление.</span><span class="sxs-lookup"><span data-stu-id="9f01a-192">PATCH performs a partial update.</span></span> <span data-ttu-id="9f01a-193">Клиент указывает только обновляемые свойства.</span><span class="sxs-lookup"><span data-stu-id="9f01a-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="9f01a-194">Постановка заменяет всю сущность.</span><span class="sxs-lookup"><span data-stu-id="9f01a-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="9f01a-195">Недостаток метода размещения заключается в том, что клиент должен отправлять значения для всех свойств сущности, включая неизменяемые значения.</span><span class="sxs-lookup"><span data-stu-id="9f01a-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="9f01a-196">В [спецификации OData](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) указывается, что это исправление является предпочтительным.</span><span class="sxs-lookup"><span data-stu-id="9f01a-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="9f01a-197">В любом случае ниже приведен код для методов PATCH и РАЗМЕСТИЛ:</span><span class="sxs-lookup"><span data-stu-id="9f01a-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="9f01a-198">В случае исправления контроллер использует тип **разностного&lt;t&gt;** для отслеживания изменений.</span><span class="sxs-lookup"><span data-stu-id="9f01a-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="9f01a-199">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="9f01a-199">Delete an entity</span></span>

<span data-ttu-id="9f01a-200">Чтобы разрешить клиентам удалять продукт из базы данных, добавьте следующий метод для `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="9f01a-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
