---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Вызов веб-API из клиента .NET (C#) — ASP.NET 4. x
author: MikeWasson
description: В этом руководстве показано, как вызвать веб-API из приложения .NET 4. x.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: ab3ba71839123e848dffaa59871f9dac8c1a88d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504960"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="a9473-103">Вызов веб-API из клиента .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="a9473-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="a9473-104">[Майк Уоссон](https://github.com/MikeWasson) и [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a9473-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a9473-105">[Скачивание завершенного проекта](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="a9473-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="a9473-106">[Указания по скачиванию](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="a9473-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="a9473-107">В этом руководстве показано, как вызвать веб-API из приложения .NET с помощью [System .NET. http. HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="a9473-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="a9473-108">В этом руководстве написано клиентское приложение, использующее следующий веб-API:</span><span class="sxs-lookup"><span data-stu-id="a9473-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="a9473-109">Действие</span><span class="sxs-lookup"><span data-stu-id="a9473-109">Action</span></span> | <span data-ttu-id="a9473-110">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="a9473-110">HTTP method</span></span> | <span data-ttu-id="a9473-111">Относительный URI</span><span class="sxs-lookup"><span data-stu-id="a9473-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9473-112">Получение продукта по ИДЕНТИФИКАТОРу</span><span class="sxs-lookup"><span data-stu-id="a9473-112">Get a product by ID</span></span> | <span data-ttu-id="a9473-113">GET</span><span class="sxs-lookup"><span data-stu-id="a9473-113">GET</span></span> | <span data-ttu-id="a9473-114">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="a9473-114">/api/products/*id*</span></span> |
| <span data-ttu-id="a9473-115">Создать продукт</span><span class="sxs-lookup"><span data-stu-id="a9473-115">Create a new product</span></span> | <span data-ttu-id="a9473-116">POST</span><span class="sxs-lookup"><span data-stu-id="a9473-116">POST</span></span> | <span data-ttu-id="a9473-117">/апи/продуктс</span><span class="sxs-lookup"><span data-stu-id="a9473-117">/api/products</span></span> |
| <span data-ttu-id="a9473-118">Обновить продукт</span><span class="sxs-lookup"><span data-stu-id="a9473-118">Update a product</span></span> | <span data-ttu-id="a9473-119">ОТПРАВКА</span><span class="sxs-lookup"><span data-stu-id="a9473-119">PUT</span></span> | <span data-ttu-id="a9473-120">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="a9473-120">/api/products/*id*</span></span> |
| <span data-ttu-id="a9473-121">Удалить продукт</span><span class="sxs-lookup"><span data-stu-id="a9473-121">Delete a product</span></span> | <span data-ttu-id="a9473-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="a9473-122">DELETE</span></span> | <span data-ttu-id="a9473-123">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="a9473-123">/api/products/*id*</span></span> |

<span data-ttu-id="a9473-124">Сведения о том, как реализовать этот API с веб-API ASP.NET, см. в разделе [Создание веб-API, поддерживающего операции CRUD](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="a9473-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="a9473-125">Для простоты клиентское приложение в этом учебнике является консольным приложением Windows.</span><span class="sxs-lookup"><span data-stu-id="a9473-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="a9473-126">**HttpClient** также поддерживается для приложений Windows Phone и магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="a9473-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="a9473-127">Дополнительные сведения см. в статье [написание кода клиента веб-API для нескольких платформ с помощью переносимых библиотек](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a9473-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="a9473-128">Создание консольного приложения</span><span class="sxs-lookup"><span data-stu-id="a9473-128">Create the Console Application</span></span>

<span data-ttu-id="a9473-129">В Visual Studio создайте новое консольное приложение Windows с именем **хттпклиентсампле** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="a9473-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="a9473-130">Приведенный выше код является полноценным клиентским приложением.</span><span class="sxs-lookup"><span data-stu-id="a9473-130">The preceding code is the complete client app.</span></span>

<span data-ttu-id="a9473-131">`RunAsync` выполняется и блокируется до завершения.</span><span class="sxs-lookup"><span data-stu-id="a9473-131">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="a9473-132">Большинство методов **HttpClient** являются асинхронными, так как они выполняют сетевые операции ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="a9473-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="a9473-133">Все асинхронные задачи выполняются в `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="a9473-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="a9473-134">Обычно приложение не блокирует основной поток, но это приложение не позволяет никакого взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="a9473-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="a9473-135">Установка клиентских библиотек веб-API</span><span class="sxs-lookup"><span data-stu-id="a9473-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="a9473-136">Используйте диспетчер пакетов NuGet для установки пакета клиентских библиотек веб-API.</span><span class="sxs-lookup"><span data-stu-id="a9473-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="a9473-137">В меню **Инструменты** выберите **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="a9473-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="a9473-138">В консоли диспетчера пакетов (PMC) введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a9473-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="a9473-139">Предыдущая команда добавляет в проект следующие пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="a9473-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="a9473-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="a9473-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="a9473-141">Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="a9473-141">Newtonsoft.Json</span></span>

<span data-ttu-id="a9473-142">Нетвонсофт. JSON (также называется Json.NET) — это популярная высокопроизводительная платформа JSON для .NET.</span><span class="sxs-lookup"><span data-stu-id="a9473-142">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="a9473-143">Добавление класса модели</span><span class="sxs-lookup"><span data-stu-id="a9473-143">Add a Model Class</span></span>

<span data-ttu-id="a9473-144">Проверьте класс `Product`:</span><span class="sxs-lookup"><span data-stu-id="a9473-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="a9473-145">Этот класс соответствует модели данных, используемой веб-API.</span><span class="sxs-lookup"><span data-stu-id="a9473-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="a9473-146">Приложение может использовать **HttpClient** для чтения экземпляра `Product` из HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="a9473-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="a9473-147">Приложению не нужно писать код десериализации.</span><span class="sxs-lookup"><span data-stu-id="a9473-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="a9473-148">Создание и инициализация HttpClient</span><span class="sxs-lookup"><span data-stu-id="a9473-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="a9473-149">Изучите статическое свойство **HttpClient** :</span><span class="sxs-lookup"><span data-stu-id="a9473-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="a9473-150">**HttpClient** предназначен для однократного создания и повторного использования в течение всего жизненного цикла приложения.</span><span class="sxs-lookup"><span data-stu-id="a9473-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="a9473-151">Следующие условия могут привести к ошибкам **SocketException** :</span><span class="sxs-lookup"><span data-stu-id="a9473-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="a9473-152">Создание нового экземпляра **HttpClient** для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="a9473-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="a9473-153">Сервер при интенсивной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="a9473-153">Server under heavy load.</span></span>

<span data-ttu-id="a9473-154">Создание нового экземпляра **HttpClient** для каждого запроса может исчерпать доступные сокеты.</span><span class="sxs-lookup"><span data-stu-id="a9473-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="a9473-155">Следующий код инициализирует экземпляр **HttpClient** :</span><span class="sxs-lookup"><span data-stu-id="a9473-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="a9473-156">Предыдущий код:</span><span class="sxs-lookup"><span data-stu-id="a9473-156">The preceding code:</span></span>

* <span data-ttu-id="a9473-157">Задает базовый URI для HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="a9473-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="a9473-158">Измените номер порта на порт, используемый в серверном приложении.</span><span class="sxs-lookup"><span data-stu-id="a9473-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="a9473-159">Приложение не будет работать, если не используется порт для серверного приложения.</span><span class="sxs-lookup"><span data-stu-id="a9473-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="a9473-160">Устанавливает заголовок Accept в значение Application/JSON.</span><span class="sxs-lookup"><span data-stu-id="a9473-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="a9473-161">Установка этого заголовка сообщает серверу о необходимости отправки данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="a9473-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="a9473-162">Отправка запроса GET для получения ресурса</span><span class="sxs-lookup"><span data-stu-id="a9473-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="a9473-163">Следующий код отправляет запрос GET для продукта:</span><span class="sxs-lookup"><span data-stu-id="a9473-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="a9473-164">Метод **Async** ОТПРАВЛЯЕТ запрос HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="a9473-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="a9473-165">Когда метод завершает работу, он возвращает **HttpResponseMessage** , СОДЕРЖАЩИЙ ответ HTTP.</span><span class="sxs-lookup"><span data-stu-id="a9473-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="a9473-166">Если код состояния в ответе является кодом успешного выполнения, текст ответа содержит представление JSON продукта.</span><span class="sxs-lookup"><span data-stu-id="a9473-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="a9473-167">Вызовите **реадасасинк** , чтобы десериализовать полезные данные JSON в экземпляр `Product`.</span><span class="sxs-lookup"><span data-stu-id="a9473-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="a9473-168">Метод **реадасасинк** является асинхронным, так как текст ответа может быть произвольным большим.</span><span class="sxs-lookup"><span data-stu-id="a9473-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="a9473-169">**HttpClient** не создает исключение, если HTTP-ответ содержит код ошибки.</span><span class="sxs-lookup"><span data-stu-id="a9473-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="a9473-170">Вместо этого свойство **IsSuccessStatusCode** имеет **значение false** , если состояние — код ошибки.</span><span class="sxs-lookup"><span data-stu-id="a9473-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="a9473-171">Если вы предпочитаете обрабатывать коды ошибок HTTP как исключения, вызовите метод [HttpResponseMessage. енсуресукцессстатускоде](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) для объекта Response.</span><span class="sxs-lookup"><span data-stu-id="a9473-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="a9473-172">`EnsureSuccessStatusCode` создает исключение, если код состояния находится за пределами диапазона 200&ndash;299.</span><span class="sxs-lookup"><span data-stu-id="a9473-172">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="a9473-173">Обратите внимание, что **HttpClient** может создавать исключения по другим причинам &mdash; например, если время ожидания запроса истекло.</span><span class="sxs-lookup"><span data-stu-id="a9473-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="a9473-174">Модули форматирования типов мультимедиа для десериализации</span><span class="sxs-lookup"><span data-stu-id="a9473-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="a9473-175">Когда **реадасасинк** вызывается без параметров, он использует набор *модулей форматирования мультимедиа* по умолчанию для чтения текста ответа.</span><span class="sxs-lookup"><span data-stu-id="a9473-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="a9473-176">Модули форматирования по умолчанию поддерживают данные JSON, XML и кодируются в формате URL.</span><span class="sxs-lookup"><span data-stu-id="a9473-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="a9473-177">Вместо использования модулей форматирования по умолчанию можно предоставить список модулей форматирования для метода **реадасасинк** .</span><span class="sxs-lookup"><span data-stu-id="a9473-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="a9473-178">Использование списка модулей форматирования полезно при наличии пользовательского модуля форматирования типа мультимедиа:</span><span class="sxs-lookup"><span data-stu-id="a9473-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="a9473-179">Дополнительные сведения см. [в разделе модули форматирования мультимедиа в веб-API ASP.NET 2](../formats-and-model-binding/media-formatters.md) .</span><span class="sxs-lookup"><span data-stu-id="a9473-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="a9473-180">Отправка запроса POST для создания ресурса</span><span class="sxs-lookup"><span data-stu-id="a9473-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="a9473-181">Следующий код отправляет запрос POST, содержащий экземпляр `Product` в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="a9473-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="a9473-182">Метод **постасжсонасинк** :</span><span class="sxs-lookup"><span data-stu-id="a9473-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="a9473-183">Сериализует объект в JSON.</span><span class="sxs-lookup"><span data-stu-id="a9473-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="a9473-184">Отправляет полезные данные JSON в запрос POST.</span><span class="sxs-lookup"><span data-stu-id="a9473-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="a9473-185">Если запрос будет выполнен, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a9473-185">If the request succeeds:</span></span>

* <span data-ttu-id="a9473-186">Он должен возвращать ответ 201 (создан).</span><span class="sxs-lookup"><span data-stu-id="a9473-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="a9473-187">Ответ должен содержать URL-адрес созданных ресурсов в заголовке Location.</span><span class="sxs-lookup"><span data-stu-id="a9473-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="a9473-188">Отправка запроса на размещение для обновления ресурса</span><span class="sxs-lookup"><span data-stu-id="a9473-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="a9473-189">Следующий код отправляет запрос на размещение для обновления продукта:</span><span class="sxs-lookup"><span data-stu-id="a9473-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="a9473-190">Метод **путасжсонасинк** работает так же, как **постасжсонасинк**, за исключением того, что он отправляет запрос на размещение вместо POST.</span><span class="sxs-lookup"><span data-stu-id="a9473-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="a9473-191">Отправка запроса на удаление для удаления ресурса</span><span class="sxs-lookup"><span data-stu-id="a9473-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="a9473-192">Следующий код отправляет запрос на удаление для удаления продукта:</span><span class="sxs-lookup"><span data-stu-id="a9473-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="a9473-193">Как и в случае GET, запрос на удаление не содержит текст запроса.</span><span class="sxs-lookup"><span data-stu-id="a9473-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="a9473-194">Не нужно указывать формат JSON или XML с помощью DELETE.</span><span class="sxs-lookup"><span data-stu-id="a9473-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="a9473-195">Тестирование примера</span><span class="sxs-lookup"><span data-stu-id="a9473-195">Test the sample</span></span>

<span data-ttu-id="a9473-196">Чтобы протестировать клиентское приложение, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a9473-196">To test the client app:</span></span>

1. <span data-ttu-id="a9473-197">[Скачайте](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) и запустите серверное приложение.</span><span class="sxs-lookup"><span data-stu-id="a9473-197">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="a9473-198">[Указания по скачиванию](/aspnet/core/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="a9473-198">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="a9473-199">Убедитесь, что серверное приложение работает.</span><span class="sxs-lookup"><span data-stu-id="a9473-199">Verify the server app is working.</span></span> <span data-ttu-id="a9473-200">Например, `http://localhost:64195/api/products` должен возвращать список продуктов.</span><span class="sxs-lookup"><span data-stu-id="a9473-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="a9473-201">Задайте базовый URI для HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="a9473-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="a9473-202">Измените номер порта на порт, используемый в серверном приложении.</span><span class="sxs-lookup"><span data-stu-id="a9473-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="a9473-203">Запустите клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="a9473-203">Run the client app.</span></span> <span data-ttu-id="a9473-204">Выводятся следующие результаты.</span><span class="sxs-lookup"><span data-stu-id="a9473-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
