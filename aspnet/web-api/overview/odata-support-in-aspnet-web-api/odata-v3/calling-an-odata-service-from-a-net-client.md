---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: Вызов службы OData из клиента .NET (C#) | Документация Майкрософт
author: MikeWasson
description: В этом руководстве показано, как вызвать службу OData из C# клиентского приложения. Версии программного обеспечения, используемые в руководстве Visual Studio 2013 (работает с Visual S...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600396"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="106c5-104">Вызов службы OData из клиента .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="106c5-104">Calling an OData Service From a .NET Client (C#)</span></span>

<span data-ttu-id="106c5-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="106c5-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="106c5-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="106c5-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="106c5-107">В этом руководстве показано, как вызвать службу OData из C# клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="106c5-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="106c5-108">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="106c5-108">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="106c5-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (работает с Visual Studio 2012)</span><span class="sxs-lookup"><span data-stu-id="106c5-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="106c5-110">Библиотека клиентов служб данных WCF</span><span class="sxs-lookup"><span data-stu-id="106c5-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/library/cc668772.aspx)
> - <span data-ttu-id="106c5-111">Веб-API 2.</span><span class="sxs-lookup"><span data-stu-id="106c5-111">Web API 2.</span></span> <span data-ttu-id="106c5-112">(Пример службы OData создается с помощью веб-API 2, но клиентское приложение не зависит от веб-API.)</span><span class="sxs-lookup"><span data-stu-id="106c5-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>

<span data-ttu-id="106c5-113">В этом руководстве я расскажу о создании клиентского приложения, которое вызывает службу OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="106c5-114">Служба OData предоставляет следующие сущности:</span><span class="sxs-lookup"><span data-stu-id="106c5-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="106c5-115">В следующих статьях описывается реализация службы OData в веб-API.</span><span class="sxs-lookup"><span data-stu-id="106c5-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="106c5-116">(Однако вам не нужно читать их для понимания этого руководства.)</span><span class="sxs-lookup"><span data-stu-id="106c5-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="106c5-117">Создание конечной точки OData в веб-API 2</span><span class="sxs-lookup"><span data-stu-id="106c5-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="106c5-118">Связи сущностей OData в веб-API 2</span><span class="sxs-lookup"><span data-stu-id="106c5-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="106c5-119">Действия OData в веб-API 2</span><span class="sxs-lookup"><span data-stu-id="106c5-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="106c5-120">Создание прокси-сервера службы</span><span class="sxs-lookup"><span data-stu-id="106c5-120">Generate the Service Proxy</span></span>

<span data-ttu-id="106c5-121">Первым шагом является создание прокси-сервера службы.</span><span class="sxs-lookup"><span data-stu-id="106c5-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="106c5-122">Прокси-сервер службы — это класс .NET, который определяет методы для доступа к службе OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="106c5-123">Прокси-сервер преобразует вызовы метода в HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="106c5-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="106c5-124">Для начала откройте проект службы OData в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="106c5-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="106c5-125">Нажмите клавиши CTRL + F5, чтобы запустить службу локально в IIS Express.</span><span class="sxs-lookup"><span data-stu-id="106c5-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="106c5-126">Запишите локальный адрес, включая номер порта, который назначается Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="106c5-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="106c5-127">Этот адрес потребуется при создании учетной записи-посредника.</span><span class="sxs-lookup"><span data-stu-id="106c5-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="106c5-128">Затем откройте другой экземпляр Visual Studio и создайте проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="106c5-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="106c5-129">Консольное приложение будет клиентским приложением OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-129">The console application will be our OData client application.</span></span> <span data-ttu-id="106c5-130">(Можно также добавить проект в то же решение, что и служба.)</span><span class="sxs-lookup"><span data-stu-id="106c5-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="106c5-131">Остальные шаги относятся к проекту консоли.</span><span class="sxs-lookup"><span data-stu-id="106c5-131">The remaining steps refer the console project.</span></span>

<span data-ttu-id="106c5-132">В обозреватель решений щелкните правой кнопкой мыши **ссылки** и выберите **Добавление ссылки на службу**.</span><span class="sxs-lookup"><span data-stu-id="106c5-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="106c5-133">В диалоговом окне **Добавление ссылки на службу** введите адрес службы OData:</span><span class="sxs-lookup"><span data-stu-id="106c5-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="106c5-134">где *Port* — номер порта.</span><span class="sxs-lookup"><span data-stu-id="106c5-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="106c5-135">В качестве **пространства имен**введите "продуктсервице".</span><span class="sxs-lookup"><span data-stu-id="106c5-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="106c5-136">Этот параметр определяет пространство имен прокси-класса.</span><span class="sxs-lookup"><span data-stu-id="106c5-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="106c5-137">Нажмите **Перейти**.</span><span class="sxs-lookup"><span data-stu-id="106c5-137">Click **Go**.</span></span> <span data-ttu-id="106c5-138">Visual Studio считывает документ метаданных OData для обнаружения сущностей в службе.</span><span class="sxs-lookup"><span data-stu-id="106c5-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="106c5-139">Нажмите кнопку **ОК** , чтобы добавить класс прокси в проект.</span><span class="sxs-lookup"><span data-stu-id="106c5-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="106c5-140">Создание экземпляра класса прокси службы</span><span class="sxs-lookup"><span data-stu-id="106c5-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="106c5-141">В методе `Main` создайте новый экземпляр класса-посредника следующим образом:</span><span class="sxs-lookup"><span data-stu-id="106c5-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="106c5-142">Опять же, используйте фактический номер порта, на котором запущена служба.</span><span class="sxs-lookup"><span data-stu-id="106c5-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="106c5-143">При развертывании службы будет использоваться универсальный код ресурса (URI) динамической службы.</span><span class="sxs-lookup"><span data-stu-id="106c5-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="106c5-144">Вам не нужно обновлять прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="106c5-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="106c5-145">Следующий код добавляет обработчик событий, который выводит URI запроса в окно консоли.</span><span class="sxs-lookup"><span data-stu-id="106c5-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="106c5-146">Этот шаг не является обязательным, но интересно увидеть коды URI для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="106c5-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="106c5-147">Запрос к службе</span><span class="sxs-lookup"><span data-stu-id="106c5-147">Query the Service</span></span>

<span data-ttu-id="106c5-148">Следующий код возвращает список продуктов из службы OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="106c5-149">Обратите внимание, что вам не нужно писать код для отправки HTTP-запроса или синтаксического анализа ответа.</span><span class="sxs-lookup"><span data-stu-id="106c5-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="106c5-150">Прокси-класс выполняет это автоматически при перечислении коллекции `Container.Products` в цикле **foreach** .</span><span class="sxs-lookup"><span data-stu-id="106c5-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="106c5-151">При запуске приложения выходные данные должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="106c5-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="106c5-152">Чтобы получить сущность по ИДЕНТИФИКАТОРу, используйте предложение `where`.</span><span class="sxs-lookup"><span data-stu-id="106c5-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="106c5-153">В оставшейся части этого раздела я не буду показывать всю функцию `Main`, просто код, необходимый для вызова службы.</span><span class="sxs-lookup"><span data-stu-id="106c5-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="106c5-154">Применить параметры запроса</span><span class="sxs-lookup"><span data-stu-id="106c5-154">Apply Query Options</span></span>

<span data-ttu-id="106c5-155">OData определяет [Параметры запроса](../supporting-odata-query-options.md) , которые можно использовать для фильтрации, сортировки, данных страницы и т. д.</span><span class="sxs-lookup"><span data-stu-id="106c5-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="106c5-156">В прокси-сервере службы эти параметры можно применять с помощью различных выражений LINQ.</span><span class="sxs-lookup"><span data-stu-id="106c5-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="106c5-157">В этом разделе я продемонстрирую краткие примеры.</span><span class="sxs-lookup"><span data-stu-id="106c5-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="106c5-158">Дополнительные сведения см. в разделе [рекомендации по LINQ (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="106c5-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="106c5-159">Фильтрация ($filter)</span><span class="sxs-lookup"><span data-stu-id="106c5-159">Filtering ($filter)</span></span>

<span data-ttu-id="106c5-160">Чтобы отфильтровать, используйте предложение `where`.</span><span class="sxs-lookup"><span data-stu-id="106c5-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="106c5-161">В следующем примере производится фильтрация по категории продуктов.</span><span class="sxs-lookup"><span data-stu-id="106c5-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="106c5-162">Этот код соответствует следующему запросу OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="106c5-163">Обратите внимание, что прокси-сервер преобразует предложение `where` в выражение `$filter` OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="106c5-164">Сортировка ($orderby)</span><span class="sxs-lookup"><span data-stu-id="106c5-164">Sorting ($orderby)</span></span>

<span data-ttu-id="106c5-165">Для сортировки используйте предложение `orderby`.</span><span class="sxs-lookup"><span data-stu-id="106c5-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="106c5-166">В следующем примере выполняется сортировка по цене, от самого высокого до самого низкого.</span><span class="sxs-lookup"><span data-stu-id="106c5-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="106c5-167">Ниже приведен соответствующий запрос OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="106c5-168">Разбиение на страницы на стороне клиента ($skip и $top)</span><span class="sxs-lookup"><span data-stu-id="106c5-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="106c5-169">Для больших наборов сущностей клиенту может потребоваться ограничить количество результатов.</span><span class="sxs-lookup"><span data-stu-id="106c5-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="106c5-170">Например, клиент может отображать 10 записей за раз.</span><span class="sxs-lookup"><span data-stu-id="106c5-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="106c5-171">Это называется *страничным обменом на стороне клиента*.</span><span class="sxs-lookup"><span data-stu-id="106c5-171">This is called *client-side paging*.</span></span> <span data-ttu-id="106c5-172">(Имеется также [страничный обмен на стороне сервера](../supporting-odata-query-options.md#server-paging), где сервер ограничивает количество результатов.) Для выполнения разбиения на страницы на стороне клиента используйте методы LINQ **Skip** и **Take** .</span><span class="sxs-lookup"><span data-stu-id="106c5-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="106c5-173">Следующий пример пропускает первые 40 результатов и принимает следующий 10.</span><span class="sxs-lookup"><span data-stu-id="106c5-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="106c5-174">Ниже приведен соответствующий запрос OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="106c5-175">Выберите ($select) и разверните ($expand)</span><span class="sxs-lookup"><span data-stu-id="106c5-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="106c5-176">Чтобы включить связанные сущности, используйте метод `DataServiceQuery<t>.Expand`.</span><span class="sxs-lookup"><span data-stu-id="106c5-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="106c5-177">Например, чтобы включить `Supplier` для каждой `Product`:</span><span class="sxs-lookup"><span data-stu-id="106c5-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="106c5-178">Ниже приведен соответствующий запрос OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="106c5-179">Чтобы изменить форму ответа, используйте предложение **SELECT** LINQ.</span><span class="sxs-lookup"><span data-stu-id="106c5-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="106c5-180">В следующем примере возвращается только имя каждого продукта без других свойств.</span><span class="sxs-lookup"><span data-stu-id="106c5-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="106c5-181">Ниже приведен соответствующий запрос OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="106c5-182">Предложение SELECT может включать связанные сущности.</span><span class="sxs-lookup"><span data-stu-id="106c5-182">A select clause can include related entities.</span></span> <span data-ttu-id="106c5-183">В этом случае не вызывайте **expand**; в этом случае прокси-сервер автоматически включает расширение.</span><span class="sxs-lookup"><span data-stu-id="106c5-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="106c5-184">В следующем примере показано получение имени и поставщика каждого продукта.</span><span class="sxs-lookup"><span data-stu-id="106c5-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="106c5-185">Ниже приведен соответствующий запрос OData.</span><span class="sxs-lookup"><span data-stu-id="106c5-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="106c5-186">Обратите внимание, что он включает параметр **$expand** .</span><span class="sxs-lookup"><span data-stu-id="106c5-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="106c5-187">Дополнительные сведения о $select и $expand см. [в разделе использование $SELECT, $Expand и $value в веб-API 2](../using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="106c5-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="106c5-188">Добавить новую сущность</span><span class="sxs-lookup"><span data-stu-id="106c5-188">Add a New Entity</span></span>

<span data-ttu-id="106c5-189">Чтобы добавить новую сущность в набор сущностей, вызовите `AddToEntitySet`, где *EntitySet* — это имя набора сущностей.</span><span class="sxs-lookup"><span data-stu-id="106c5-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="106c5-190">Например, `AddToProducts` добавляет новую `Product` в набор сущностей `Products`.</span><span class="sxs-lookup"><span data-stu-id="106c5-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="106c5-191">При создании прокси-сервера WCF Data Services автоматически создает эти методы строго типизированных **AddTo** .</span><span class="sxs-lookup"><span data-stu-id="106c5-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="106c5-192">Чтобы добавить ссылку между двумя сущностями, используйте методы **AddLink** и **сетлинк** .</span><span class="sxs-lookup"><span data-stu-id="106c5-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="106c5-193">Следующий код добавляет нового поставщика и новый продукт, а затем создает связи между ними.</span><span class="sxs-lookup"><span data-stu-id="106c5-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="106c5-194">Используйте **AddLink** , если свойство навигации является коллекцией.</span><span class="sxs-lookup"><span data-stu-id="106c5-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="106c5-195">В этом примере мы добавляем продукт в коллекцию `Products` поставщика.</span><span class="sxs-lookup"><span data-stu-id="106c5-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="106c5-196">Используйте **сетлинк** , если свойство навигации является одной сущностью.</span><span class="sxs-lookup"><span data-stu-id="106c5-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="106c5-197">В этом примере мы задаете свойство `Supplier` для продукта.</span><span class="sxs-lookup"><span data-stu-id="106c5-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="106c5-198">Обновление или исправление</span><span class="sxs-lookup"><span data-stu-id="106c5-198">Update / Patch</span></span>

<span data-ttu-id="106c5-199">Чтобы обновить сущность, вызовите метод **UpdateObject** .</span><span class="sxs-lookup"><span data-stu-id="106c5-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="106c5-200">Обновление выполняется при вызове метода **SaveChanges**.</span><span class="sxs-lookup"><span data-stu-id="106c5-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="106c5-201">По умолчанию WCF отправляет HTTP-запрос на СЛИЯНИе.</span><span class="sxs-lookup"><span data-stu-id="106c5-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="106c5-202">Параметр **патчонупдате** сообщает WCF, что вместо этого ОТПРАВЛЯЕТСЯ исправление HTTP.</span><span class="sxs-lookup"><span data-stu-id="106c5-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="106c5-203">Почему исправления и СЛИЯНИе?</span><span class="sxs-lookup"><span data-stu-id="106c5-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="106c5-204">В исходной спецификации HTTP 1,1 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) не определен ни один метод HTTP с семантикой "частичного обновления".</span><span class="sxs-lookup"><span data-stu-id="106c5-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="106c5-205">Для поддержки частичных обновлений спецификация OData определила метод MERGE.</span><span class="sxs-lookup"><span data-stu-id="106c5-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="106c5-206">В 2010 [RFC 5789](http://tools.ietf.org/html/rfc5789) ОПРЕДЕЛИЛ метод исправления для частичных обновлений.</span><span class="sxs-lookup"><span data-stu-id="106c5-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="106c5-207">Некоторые журналы из этой [записи блога](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) можно прочитать в блоге WCF Data Services.</span><span class="sxs-lookup"><span data-stu-id="106c5-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="106c5-208">Сейчас исправление является предпочтительным по сравнению с СЛИЯНИем.</span><span class="sxs-lookup"><span data-stu-id="106c5-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="106c5-209">Контроллер OData, созданный с помощью формирования шаблонов веб-API, поддерживает оба метода.</span><span class="sxs-lookup"><span data-stu-id="106c5-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>

<span data-ttu-id="106c5-210">Если требуется заменить всю сущность (семантика вставки), укажите параметр **реплацеонупдате** .</span><span class="sxs-lookup"><span data-stu-id="106c5-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="106c5-211">Это приводит к тому, что WCF отправляет запрос HTTP-размещения.</span><span class="sxs-lookup"><span data-stu-id="106c5-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="106c5-212">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="106c5-212">Delete an Entity</span></span>

<span data-ttu-id="106c5-213">Чтобы удалить сущность, вызовите **DeleteObject**.</span><span class="sxs-lookup"><span data-stu-id="106c5-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="106c5-214">Вызов действия OData</span><span class="sxs-lookup"><span data-stu-id="106c5-214">Invoke an OData Action</span></span>

<span data-ttu-id="106c5-215">В OData [действия](odata-actions.md) — это способ добавления поведений на стороне сервера, которые не просто определяются как операции CRUD с сущностями.</span><span class="sxs-lookup"><span data-stu-id="106c5-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="106c5-216">Хотя в документе метаданных OData описываются действия, прокси-класс не создает для них строго типизированные методы.</span><span class="sxs-lookup"><span data-stu-id="106c5-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="106c5-217">Действие OData по-прежнему можно вызывать с помощью универсального метода **EXECUTE** .</span><span class="sxs-lookup"><span data-stu-id="106c5-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="106c5-218">Тем не менее необходимо знать типы данных параметров и возвращаемое значение.</span><span class="sxs-lookup"><span data-stu-id="106c5-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="106c5-219">Например, `RateProduct` действие принимает параметр с именем "Оценка" типа `Int32` и возвращает `double`.</span><span class="sxs-lookup"><span data-stu-id="106c5-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="106c5-220">В следующем коде показано, как вызвать это действие.</span><span class="sxs-lookup"><span data-stu-id="106c5-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="106c5-221">Дополнительные сведения см. в разделе[вызов операций и действий службы](https://msdn.microsoft.com/library/hh230677.aspx).</span><span class="sxs-lookup"><span data-stu-id="106c5-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/library/hh230677.aspx).</span></span>

<span data-ttu-id="106c5-222">Один из вариантов — расширить класс **контейнера** , чтобы предоставить строго типизированный метод, который вызывает действие:</span><span class="sxs-lookup"><span data-stu-id="106c5-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
