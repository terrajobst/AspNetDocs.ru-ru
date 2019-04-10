---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Вызов веб-API из клиента .NET (C#)-ASP.NET 4.x
author: MikeWasson
description: Этом руководстве показано, как вызывать веб-API из приложения .NET 4.x.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 113600ca1e77ae9667465464da505478fc948c9b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421112"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="b3340-103">Вызов веб-API из клиента .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="b3340-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="b3340-104">по [Майк Уоссон](https://github.com/MikeWasson) и [Рик Андерсон](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b3340-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b3340-105">[Скачать завершенный проект](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="b3340-105">[Download Completed Project](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="b3340-106">[Указания по скачиванию](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="b3340-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="b3340-107">Этом руководстве показано, как вызывать веб-API из приложения .NET с помощью [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="b3340-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="b3340-108">В этом руководстве клиентского приложения записываются, которые используют следующие веб-API:</span><span class="sxs-lookup"><span data-stu-id="b3340-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="b3340-109">Действие</span><span class="sxs-lookup"><span data-stu-id="b3340-109">Action</span></span> | <span data-ttu-id="b3340-110">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="b3340-110">HTTP method</span></span> | <span data-ttu-id="b3340-111">Относительный URI</span><span class="sxs-lookup"><span data-stu-id="b3340-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3340-112">Получить продукт по Идентификатору</span><span class="sxs-lookup"><span data-stu-id="b3340-112">Get a product by ID</span></span> | <span data-ttu-id="b3340-113">GET</span><span class="sxs-lookup"><span data-stu-id="b3340-113">GET</span></span> | <span data-ttu-id="b3340-114">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="b3340-114">/api/products/*id*</span></span> |
| <span data-ttu-id="b3340-115">Создать продукт</span><span class="sxs-lookup"><span data-stu-id="b3340-115">Create a new product</span></span> | <span data-ttu-id="b3340-116">ПОМЕСТИТЬ</span><span class="sxs-lookup"><span data-stu-id="b3340-116">POST</span></span> | <span data-ttu-id="b3340-117">/ api/продуктов</span><span class="sxs-lookup"><span data-stu-id="b3340-117">/api/products</span></span> |
| <span data-ttu-id="b3340-118">Обновления продукта</span><span class="sxs-lookup"><span data-stu-id="b3340-118">Update a product</span></span> | <span data-ttu-id="b3340-119">PUT</span><span class="sxs-lookup"><span data-stu-id="b3340-119">PUT</span></span> | <span data-ttu-id="b3340-120">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="b3340-120">/api/products/*id*</span></span> |
| <span data-ttu-id="b3340-121">Удалить продукт</span><span class="sxs-lookup"><span data-stu-id="b3340-121">Delete a product</span></span> | <span data-ttu-id="b3340-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="b3340-122">DELETE</span></span> | <span data-ttu-id="b3340-123">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="b3340-123">/api/products/*id*</span></span> |

<span data-ttu-id="b3340-124">Чтобы узнать, как реализовать этот интерфейс API с веб-API ASP.NET, см. в разделе [Создание веб-API, поддерживает операции CRUD](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="b3340-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="b3340-125">Для простоты клиентское приложение в этом руководстве используется консольное приложение Windows.</span><span class="sxs-lookup"><span data-stu-id="b3340-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="b3340-126">**HttpClient** также поддерживается для приложений Windows Phone и Windows Store.</span><span class="sxs-lookup"><span data-stu-id="b3340-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="b3340-127">Дополнительные сведения см. в разделе [код записи веб-API клиента для нескольких платформ с помощью переносимых библиотек](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="b3340-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="b3340-128">Создание консольного приложения</span><span class="sxs-lookup"><span data-stu-id="b3340-128">Create the Console Application</span></span>

<span data-ttu-id="b3340-129">В Visual Studio создайте новое консольное приложение Windows с именем **HttpClientSample** и вставьте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="b3340-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="b3340-130">Приведенный выше код является полный клиентским приложением.</span><span class="sxs-lookup"><span data-stu-id="b3340-130">The preceding code is the complete client app.</span></span>

`RunAsync` <span data-ttu-id="b3340-131">запуски и блокируется до его завершения.</span><span class="sxs-lookup"><span data-stu-id="b3340-131">runs and blocks until it completes.</span></span> <span data-ttu-id="b3340-132">Большинство **HttpClient** методы являются async, поскольку они выполняют подсистемы ввода/вывода.</span><span class="sxs-lookup"><span data-stu-id="b3340-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="b3340-133">Все асинхронные задачи выполняемые в `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="b3340-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="b3340-134">Обычно приложения не блокирует основной поток, но это приложение не допускает каких-либо взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="b3340-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="b3340-135">Установка библиотеки Web API клиента</span><span class="sxs-lookup"><span data-stu-id="b3340-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="b3340-136">С помощью диспетчера пакетов NuGet для установки пакета Web API клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="b3340-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="b3340-137">В меню **Сервис** последовательно выберите пункты **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="b3340-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="b3340-138">В консоли диспетчера пакетов (PMC), введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b3340-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="b3340-139">Предыдущая команда добавляет в проект следующие пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="b3340-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="b3340-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="b3340-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="b3340-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="b3340-141">Newtonsoft.Json</span></span>

<span data-ttu-id="b3340-142">Json.NET — это популярная платформа JSON высокой производительности для .NET.</span><span class="sxs-lookup"><span data-stu-id="b3340-142">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="b3340-143">Добавление класса модели</span><span class="sxs-lookup"><span data-stu-id="b3340-143">Add a Model Class</span></span>

<span data-ttu-id="b3340-144">Проверьте класс `Product`:</span><span class="sxs-lookup"><span data-stu-id="b3340-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="b3340-145">Этот класс соответствует модели данных, используемых веб-API.</span><span class="sxs-lookup"><span data-stu-id="b3340-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="b3340-146">Приложение может использовать **HttpClient** для чтения `Product` экземпляр HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="b3340-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="b3340-147">Приложение не нужно писать код десериализации.</span><span class="sxs-lookup"><span data-stu-id="b3340-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="b3340-148">Создание и инициализация HttpClient</span><span class="sxs-lookup"><span data-stu-id="b3340-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="b3340-149">Изучите статический **HttpClient** свойство:</span><span class="sxs-lookup"><span data-stu-id="b3340-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="b3340-150">**HttpClient** будет должен создаваться один раз и повторно использоваться на протяжении всего жизненного цикла приложения.</span><span class="sxs-lookup"><span data-stu-id="b3340-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="b3340-151">Можно привести следующие условия **SocketException** ошибок:</span><span class="sxs-lookup"><span data-stu-id="b3340-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="b3340-152">Создание нового **HttpClient** экземпляра на запрос.</span><span class="sxs-lookup"><span data-stu-id="b3340-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="b3340-153">Сервер в условиях большой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b3340-153">Server under heavy load.</span></span>

<span data-ttu-id="b3340-154">Создание нового **HttpClient** экземпляра на запрос может исчерпать все доступные сокеты.</span><span class="sxs-lookup"><span data-stu-id="b3340-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="b3340-155">В следующем примере кода инициализирует **HttpClient** экземпляр:</span><span class="sxs-lookup"><span data-stu-id="b3340-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="b3340-156">Предыдущий код:</span><span class="sxs-lookup"><span data-stu-id="b3340-156">The preceding code:</span></span>

* <span data-ttu-id="b3340-157">Задает базовый URI для HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="b3340-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="b3340-158">Измените номер порта к порту, используемому в серверное приложение.</span><span class="sxs-lookup"><span data-stu-id="b3340-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="b3340-159">Если не используется порт для серверного приложения для работы приложения.</span><span class="sxs-lookup"><span data-stu-id="b3340-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="b3340-160">Задает заголовок Accept «application/json».</span><span class="sxs-lookup"><span data-stu-id="b3340-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="b3340-161">Параметр этот заголовок указывает, что сервер для отправки данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b3340-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="b3340-162">Отправка запроса GET для извлечения ресурса</span><span class="sxs-lookup"><span data-stu-id="b3340-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="b3340-163">Следующий код отправляет запрос GET для продукта:</span><span class="sxs-lookup"><span data-stu-id="b3340-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="b3340-164">**GetAsync** метод отправляет запрос HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="b3340-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="b3340-165">Если метод завершается, она возвращает **HttpResponseMessage** , содержащий HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="b3340-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="b3340-166">Если код состояния в ответе код успешного выполнения, текст ответа содержит представление JSON продукта.</span><span class="sxs-lookup"><span data-stu-id="b3340-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="b3340-167">Вызовите **ReadAsAsync** для полезных данных JSON для десериализации `Product` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b3340-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="b3340-168">**ReadAsAsync** метод является асинхронным, поскольку текст ответа может быть произвольно большим.</span><span class="sxs-lookup"><span data-stu-id="b3340-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="b3340-169">**HttpClient** не выдает исключение при HTTP-ответа содержит код ошибки.</span><span class="sxs-lookup"><span data-stu-id="b3340-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="b3340-170">Вместо этого **IsSuccessStatusCode** свойство **false** Если состояние — код ошибки.</span><span class="sxs-lookup"><span data-stu-id="b3340-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="b3340-171">Если вы предпочитаете обрабатывать коды ошибок HTTP как исключения, вызвать [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) объекта response.</span><span class="sxs-lookup"><span data-stu-id="b3340-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> `EnsureSuccessStatusCode` <span data-ttu-id="b3340-172">создает исключение, если код состояния находится вне диапазона 200&ndash;299.</span><span class="sxs-lookup"><span data-stu-id="b3340-172">throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="b3340-173">Обратите внимание, что **HttpClient** может создавать исключения по другим причинам &mdash; к примеру, если тайм-аута запроса.</span><span class="sxs-lookup"><span data-stu-id="b3340-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="b3340-174">Модули форматирования типа мультимедиа для десериализации</span><span class="sxs-lookup"><span data-stu-id="b3340-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="b3340-175">Когда **ReadAsAsync** вызывается без параметров, он использует набор по умолчанию *модули форматирования мультимедиа* прочитать текст ответа.</span><span class="sxs-lookup"><span data-stu-id="b3340-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="b3340-176">Модули форматирования по умолчанию поддерживает JSON, XML и данные в форме кодировке к URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b3340-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="b3340-177">Вместо того чтобы использовать модули форматирования по умолчанию, можно предоставить список модулей форматирования для **ReadAsAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="b3340-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="b3340-178">Использование список модулей форматирования полезно в том случае, если у вас есть модуль форматирования типа мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b3340-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="b3340-179">Дополнительные сведения см. в разделе [модули форматирования мультимедиа в ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="b3340-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="b3340-180">Отправить запрос POST для создания ресурса</span><span class="sxs-lookup"><span data-stu-id="b3340-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="b3340-181">Следующий код отправляет запрос POST, содержащий `Product` экземпляра в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="b3340-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="b3340-182">**PostAsJsonAsync** метод:</span><span class="sxs-lookup"><span data-stu-id="b3340-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="b3340-183">Сериализует объект в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="b3340-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="b3340-184">Отправляет полезные данные JSON в запросе POST.</span><span class="sxs-lookup"><span data-stu-id="b3340-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="b3340-185">Если запрос выполнен успешно:</span><span class="sxs-lookup"><span data-stu-id="b3340-185">If the request succeeds:</span></span>

* <span data-ttu-id="b3340-186">Он должен вернуть ответ 201 (создано).</span><span class="sxs-lookup"><span data-stu-id="b3340-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="b3340-187">Ответ должен содержать URL-адрес созданные ресурсы в заголовке Location.</span><span class="sxs-lookup"><span data-stu-id="b3340-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="b3340-188">Отправка запроса PUT для обновления ресурса</span><span class="sxs-lookup"><span data-stu-id="b3340-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="b3340-189">Следующий код отправляет запрос PUT для обновления продукта:</span><span class="sxs-lookup"><span data-stu-id="b3340-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="b3340-190">**PutAsJsonAsync** метод работает подобно **PostAsJsonAsync**, за исключением того, что он отправляет запрос PUT вместо POST.</span><span class="sxs-lookup"><span data-stu-id="b3340-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="b3340-191">Отправляя запрос DELETE для удаления ресурса</span><span class="sxs-lookup"><span data-stu-id="b3340-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="b3340-192">Следующий код отправляет запрос DELETE для удаления продукта:</span><span class="sxs-lookup"><span data-stu-id="b3340-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="b3340-193">Например GET запрос DELETE не имеет текста запроса.</span><span class="sxs-lookup"><span data-stu-id="b3340-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="b3340-194">Не нужно указать формат JSON или XML с помощью удаления.</span><span class="sxs-lookup"><span data-stu-id="b3340-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="b3340-195">Тестирование образца</span><span class="sxs-lookup"><span data-stu-id="b3340-195">Test the sample</span></span>

<span data-ttu-id="b3340-196">Чтобы проверить его:</span><span class="sxs-lookup"><span data-stu-id="b3340-196">To test the client app:</span></span>

1. <span data-ttu-id="b3340-197">[Скачайте](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) и запуск приложения сервера.</span><span class="sxs-lookup"><span data-stu-id="b3340-197">[Download](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="b3340-198">[Указания по скачиванию](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="b3340-198">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> <span data-ttu-id="b3340-199">Убедитесь, что работает серверное приложение.</span><span class="sxs-lookup"><span data-stu-id="b3340-199">Verify the server app is working.</span></span> <span data-ttu-id="b3340-200">Например `http://localhost:64195/api/products` должен возвращать список продуктов.</span><span class="sxs-lookup"><span data-stu-id="b3340-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="b3340-201">Задайте базовый URI для HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="b3340-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="b3340-202">Измените номер порта к порту, используемому в серверное приложение.</span><span class="sxs-lookup"><span data-stu-id="b3340-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="b3340-203">Запустите клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="b3340-203">Run the client app.</span></span> <span data-ttu-id="b3340-204">Выводятся следующие результаты.</span><span class="sxs-lookup"><span data-stu-id="b3340-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
