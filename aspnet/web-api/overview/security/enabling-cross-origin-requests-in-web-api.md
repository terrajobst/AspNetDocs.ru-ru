---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: Включение запросов между источниками в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: Показывает, как поддерживать общий доступ к ресурсам между источниками (CORS) в веб-API ASP.NET.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447618"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="6b27d-103">Включить запросы между источниками в веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="6b27d-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>

<span data-ttu-id="6b27d-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6b27d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="6b27d-105">Параметры безопасности веб-браузера предотвращают отправку запросов AJAX с веб-страницы к другому домену.</span><span class="sxs-lookup"><span data-stu-id="6b27d-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="6b27d-106">Это ограничение называется *политикой того же происхождения*и предотвращает чтение вредоносных данных с другого сайта злоумышленником.</span><span class="sxs-lookup"><span data-stu-id="6b27d-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="6b27d-107">Однако иногда может потребоваться разрешить другим сайтам вызывать веб-API.</span><span class="sxs-lookup"><span data-stu-id="6b27d-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="6b27d-108">[Общий доступ к ресурсам в разных источниках](http://www.w3.org/TR/cors/) (CORS) — это стандарт консорциума W3C, позволяющий серверу смягчить ту же политику.</span><span class="sxs-lookup"><span data-stu-id="6b27d-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="6b27d-109">С помощью CORS сервер может явным образом разрешить некоторые запросы независимо от источника, а другие — отклонить.</span><span class="sxs-lookup"><span data-stu-id="6b27d-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="6b27d-110">CORS безопаснее и более гибкий, чем более ранние методики, такие как [JSONP](http://en.wikipedia.org/wiki/JSONP).</span><span class="sxs-lookup"><span data-stu-id="6b27d-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="6b27d-111">В этом руководстве показано, как включить CORS в приложении веб-API.</span><span class="sxs-lookup"><span data-stu-id="6b27d-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="6b27d-112">Программное обеспечение, используемое в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="6b27d-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="6b27d-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b27d-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="6b27d-114">Веб-API 2,2</span><span class="sxs-lookup"><span data-stu-id="6b27d-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="6b27d-115">Введение</span><span class="sxs-lookup"><span data-stu-id="6b27d-115">Introduction</span></span>

<span data-ttu-id="6b27d-116">В этом руководстве демонстрируется поддержка CORS в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6b27d-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="6b27d-117">Начнем с создания двух проектов ASP.NET — один под названием «WebService», который размещает контроллер веб-API, а другой — «WebClient», который вызывает WebService.</span><span class="sxs-lookup"><span data-stu-id="6b27d-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="6b27d-118">Поскольку два приложения размещаются в разных доменах, запрос AJAX от WebClient к WebService является запросом между источниками.</span><span class="sxs-lookup"><span data-stu-id="6b27d-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="6b27d-119">Что такое "тот же источник"?</span><span class="sxs-lookup"><span data-stu-id="6b27d-119">What is "same origin"?</span></span>

<span data-ttu-id="6b27d-120">Два URL-адреса имеют один и тот же источник, если они имеют идентичные схемы, узлы и порты.</span><span class="sxs-lookup"><span data-stu-id="6b27d-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="6b27d-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="6b27d-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="6b27d-122">Эти два URL-адреса имеют один и тот же источник:</span><span class="sxs-lookup"><span data-stu-id="6b27d-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="6b27d-123">Эти URL-адреса имеют разные источники, отличные от предыдущих двух:</span><span class="sxs-lookup"><span data-stu-id="6b27d-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="6b27d-124">`http://example.net`-другой домен</span><span class="sxs-lookup"><span data-stu-id="6b27d-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="6b27d-125">`http://example.com:9000/foo.html`-другой порт</span><span class="sxs-lookup"><span data-stu-id="6b27d-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="6b27d-126">Другая схема `https://example.com/foo.html`</span><span class="sxs-lookup"><span data-stu-id="6b27d-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="6b27d-127">`http://www.example.com/foo.html`-различные поддомены</span><span class="sxs-lookup"><span data-stu-id="6b27d-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="6b27d-128">При сравнении источников Internet Explorer не учитывает порт.</span><span class="sxs-lookup"><span data-stu-id="6b27d-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="6b27d-129">Создание проекта WebService</span><span class="sxs-lookup"><span data-stu-id="6b27d-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="6b27d-130">В этом разделе предполагается, что вы уже знакомы с созданием проектов веб-API.</span><span class="sxs-lookup"><span data-stu-id="6b27d-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="6b27d-131">Если нет, см. раздел [Начало работы with веб-API ASP.NET](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="6b27d-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="6b27d-132">Запустите Visual Studio и создайте проект **веб-приложения ASP.NET (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="6b27d-133">В диалоговом окне **Создание веб-приложения ASP.NET** выберите **пустой** шаблон проекта.</span><span class="sxs-lookup"><span data-stu-id="6b27d-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="6b27d-134">В разделе **Добавление папок и основных ссылок для**установите флажок **веб-API** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Диалоговое окно создания проекта ASP.NET в Visual Studio](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="6b27d-136">Добавьте контроллер веб-API с именем `TestController` со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="6b27d-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="6b27d-137">Приложение можно запустить локально или развернуть в Azure.</span><span class="sxs-lookup"><span data-stu-id="6b27d-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="6b27d-138">(Для снимков экрана в этом руководстве приложение развертывается в веб-приложениях службы приложений Azure.) Чтобы убедиться, что веб-API работает, перейдите по адресу `http://hostname/api/test/`, где *HostName* — это домен, в котором развернуто приложение.</span><span class="sxs-lookup"><span data-stu-id="6b27d-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="6b27d-139">Вы увидите текст ответа &quot;получить: тестовое сообщение&quot;.</span><span class="sxs-lookup"><span data-stu-id="6b27d-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![Веб-браузер, демонстрирующий тестовое сообщение](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="6b27d-141">Создание проекта WebClient</span><span class="sxs-lookup"><span data-stu-id="6b27d-141">Create the WebClient project</span></span>

1. <span data-ttu-id="6b27d-142">Создайте другой проект **веб-приложения ASP.NET (.NET Framework)** и выберите шаблон проекта **MVC** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="6b27d-143">При необходимости выберите **изменить проверку Подлинности** > **без проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="6b27d-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="6b27d-144">Для работы с этим руководством не требуется проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b27d-144">You don't need authentication for this tutorial.</span></span>

   ![Шаблон MVC в диалоговом окне создания проекта ASP.NET в Visual Studio](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="6b27d-146">В **Обозреватель решений**откройте файл *Views/Home/Index. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6b27d-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="6b27d-147">Замените код в этом файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="6b27d-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="6b27d-148">Для переменной *serviceUrl* используйте URI приложения WebService.</span><span class="sxs-lookup"><span data-stu-id="6b27d-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="6b27d-149">Запустите приложение WebClient локально или опубликуйте его на другом веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="6b27d-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="6b27d-150">При нажатии кнопки "попробовать" запрос AJAX отправляется в приложение WebService с помощью метода HTTP, указанного в раскрывающемся списке (GET, POST или поместить).</span><span class="sxs-lookup"><span data-stu-id="6b27d-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="6b27d-151">Это позволяет проверять различные запросы между источниками.</span><span class="sxs-lookup"><span data-stu-id="6b27d-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="6b27d-152">В настоящее время приложение WebService не поддерживает CORS, поэтому при нажатии кнопки вы получите сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="6b27d-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![Ошибка "попробовать" в браузере](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="6b27d-154">Если вы видите HTTP-трафик в таком средстве, как [Fiddler](https://www.telerik.com/fiddler), вы увидите, что браузер ОТПРАВЛЯЕТ запрос GET, и запрос завершается, но вызов AJAX возвращает ошибку.</span><span class="sxs-lookup"><span data-stu-id="6b27d-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="6b27d-155">Важно понимать, что политика того же источника не мешает обозревателю *отправлять* запрос.</span><span class="sxs-lookup"><span data-stu-id="6b27d-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="6b27d-156">Вместо этого он предотвращает просмотр *ответа*приложением.</span><span class="sxs-lookup"><span data-stu-id="6b27d-156">Instead, it prevents the application from seeing the *response*.</span></span>

![Веб-отладчик Fiddler, отображающий веб-запросы](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="6b27d-158">Включение CORS</span><span class="sxs-lookup"><span data-stu-id="6b27d-158">Enable CORS</span></span>

<span data-ttu-id="6b27d-159">Теперь включите CORS в приложении WebService.</span><span class="sxs-lookup"><span data-stu-id="6b27d-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="6b27d-160">Сначала добавьте пакет NuGet для CORS.</span><span class="sxs-lookup"><span data-stu-id="6b27d-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="6b27d-161">В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="6b27d-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="6b27d-162">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6b27d-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="6b27d-163">Эта команда устанавливает последний пакет и обновляет все зависимости, включая основные библиотеки веб-API.</span><span class="sxs-lookup"><span data-stu-id="6b27d-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="6b27d-164">Используйте флаг `-Version`, чтобы выбрать конкретную версию.</span><span class="sxs-lookup"><span data-stu-id="6b27d-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="6b27d-165">Для пакета CORS требуется веб-API 2,0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6b27d-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="6b27d-166">Откройте файл *App\_Start/WebApiConfig. CS*.</span><span class="sxs-lookup"><span data-stu-id="6b27d-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="6b27d-167">Добавьте следующий код в метод **WebApiConfig. Register** :</span><span class="sxs-lookup"><span data-stu-id="6b27d-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="6b27d-168">Затем добавьте атрибут **[EnableCors]** в класс `TestController`:</span><span class="sxs-lookup"><span data-stu-id="6b27d-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="6b27d-169">В качестве параметра *происхождения* используйте URI, в котором развернуто приложение WebClient.</span><span class="sxs-lookup"><span data-stu-id="6b27d-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="6b27d-170">Это позволяет выполнять запросы между источниками от WebClient, не разрешая все остальные междоменные запросы.</span><span class="sxs-lookup"><span data-stu-id="6b27d-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="6b27d-171">Позже я опишу параметры для **[EnableCors]** более подробно.</span><span class="sxs-lookup"><span data-stu-id="6b27d-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="6b27d-172">Не включайте косую черту в конце URL-адреса *происхождения* .</span><span class="sxs-lookup"><span data-stu-id="6b27d-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="6b27d-173">Повторно разверните обновленное приложение WebService.</span><span class="sxs-lookup"><span data-stu-id="6b27d-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="6b27d-174">Обновлять WebClient не требуется.</span><span class="sxs-lookup"><span data-stu-id="6b27d-174">You don't need to update WebClient.</span></span> <span data-ttu-id="6b27d-175">Теперь запрос AJAX от WebClient должен быть выполнен.</span><span class="sxs-lookup"><span data-stu-id="6b27d-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="6b27d-176">Методы GET, WHERE и POST разрешены.</span><span class="sxs-lookup"><span data-stu-id="6b27d-176">The GET, PUT, and POST methods are all allowed.</span></span>

![Веб-браузер, показывающий успешное тестовое сообщение](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="6b27d-178">Принцип работы CORS</span><span class="sxs-lookup"><span data-stu-id="6b27d-178">How CORS Works</span></span>

<span data-ttu-id="6b27d-179">В этом разделе описывается, что происходит в запросе CORS на уровне HTTP-сообщений.</span><span class="sxs-lookup"><span data-stu-id="6b27d-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="6b27d-180">Важно понимать, как работает CORS, чтобы можно было правильно настроить атрибут **[EnableCors]** и устранять неполадки, если они не работают должным образом.</span><span class="sxs-lookup"><span data-stu-id="6b27d-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="6b27d-181">Спецификация CORS вводит несколько новых HTTP-заголовков, которые позволяют выполнять запросы между источниками.</span><span class="sxs-lookup"><span data-stu-id="6b27d-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="6b27d-182">Если браузер поддерживает CORS, эти заголовки автоматически устанавливаются для запросов между источниками. Вам не нужно ничего делать в коде JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6b27d-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="6b27d-183">Ниже приведен пример запроса между источниками.</span><span class="sxs-lookup"><span data-stu-id="6b27d-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="6b27d-184">Заголовок "Origin" предоставляет домен сайта, выполняющего запрос.</span><span class="sxs-lookup"><span data-stu-id="6b27d-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="6b27d-185">Если сервер разрешает запрос, он устанавливает заголовок Access-Control-Allow-Origin.</span><span class="sxs-lookup"><span data-stu-id="6b27d-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="6b27d-186">Значение этого заголовка либо соответствует заголовку источника, либо является подстановочным значением «\*», что означает, что любой источник разрешен.</span><span class="sxs-lookup"><span data-stu-id="6b27d-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="6b27d-187">Если ответ не включает заголовок Access-Control-Allow-Origin, то запрос AJAX завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="6b27d-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="6b27d-188">В частности, браузер не разрешает запрос.</span><span class="sxs-lookup"><span data-stu-id="6b27d-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="6b27d-189">Даже если сервер возвращает успешный ответ, браузер не делает ответ доступным клиентскому приложению.</span><span class="sxs-lookup"><span data-stu-id="6b27d-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="6b27d-190">**Предпечатные запросы**</span><span class="sxs-lookup"><span data-stu-id="6b27d-190">**Preflight Requests**</span></span>

<span data-ttu-id="6b27d-191">Для некоторых запросов CORS браузер отправляет дополнительный запрос, называемый «предварительным запросом», перед отправкой фактического запроса ресурса.</span><span class="sxs-lookup"><span data-stu-id="6b27d-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="6b27d-192">Браузер может пропустить Предпечатный запрос, если выполняются следующие условия.</span><span class="sxs-lookup"><span data-stu-id="6b27d-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="6b27d-193">Метод запроса — GET, HEAD или POST, *а*</span><span class="sxs-lookup"><span data-stu-id="6b27d-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="6b27d-194">Приложение не устанавливает никаких заголовков запроса, кроме Accept, Accept-Language, Content-Language, Content-Type или Last-Event-ID, *и*</span><span class="sxs-lookup"><span data-stu-id="6b27d-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="6b27d-195">Заголовок Content-Type (если задан) является одним из следующих:</span><span class="sxs-lookup"><span data-stu-id="6b27d-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="6b27d-196">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="6b27d-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="6b27d-197">multipart/form-data</span><span class="sxs-lookup"><span data-stu-id="6b27d-197">multipart/form-data</span></span>
    - <span data-ttu-id="6b27d-198">text/plain</span><span class="sxs-lookup"><span data-stu-id="6b27d-198">text/plain</span></span>

<span data-ttu-id="6b27d-199">Правило о заголовках запросов применяется к заголовкам, которые устанавливаются приложением путем вызова **сетрекуессеадер** для объекта **XMLHttpRequest** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="6b27d-200">(Спецификация CORS вызывает эти "заголовки запроса автора".) Правило не применяется к заголовкам, которые может задать *браузер* , например агент пользователя, узел или длина содержимого.</span><span class="sxs-lookup"><span data-stu-id="6b27d-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="6b27d-201">Ниже приведен пример предпечатного запроса:</span><span class="sxs-lookup"><span data-stu-id="6b27d-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="6b27d-202">Запрос перед рейсом использует метод HTTP OPTIONS.</span><span class="sxs-lookup"><span data-stu-id="6b27d-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="6b27d-203">Он включает два специальных заголовка:</span><span class="sxs-lookup"><span data-stu-id="6b27d-203">It includes two special headers:</span></span>

- <span data-ttu-id="6b27d-204">Access-Control-Request-method — метод HTTP, который будет использоваться для фактического запроса.</span><span class="sxs-lookup"><span data-stu-id="6b27d-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="6b27d-205">Access-Control-request-headers. список заголовков запросов, установленных *приложением* в фактическом запросе.</span><span class="sxs-lookup"><span data-stu-id="6b27d-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="6b27d-206">(Опять же, сюда не входят заголовки, задаются браузером.)</span><span class="sxs-lookup"><span data-stu-id="6b27d-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="6b27d-207">Ниже приведен пример ответа, предполагая, что сервер разрешает запрос:</span><span class="sxs-lookup"><span data-stu-id="6b27d-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="6b27d-208">Ответ содержит заголовок Access-Control-Allow-Methods, в котором перечислены допустимые методы и при необходимости заголовок Access-Control-Allow-Headers, который перечисляет разрешенные заголовки.</span><span class="sxs-lookup"><span data-stu-id="6b27d-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="6b27d-209">Если Предпечатный запрос выполнен, браузер отправляет фактический запрос, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="6b27d-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="6b27d-210">Средства, обычно используемые для тестирования конечных точек с запросами параметров предварительной проверки (например, [Fiddler](https://www.telerik.com/fiddler) и [POST](https://www.getpostman.com/)), не отправляют обязательные заголовки параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6b27d-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="6b27d-211">Убедитесь, что заголовки `Access-Control-Request-Method` и `Access-Control-Request-Headers` отправлены с запросом, а заголовки параметров достигают приложения через IIS.</span><span class="sxs-lookup"><span data-stu-id="6b27d-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="6b27d-212">Чтобы настроить службы IIS таким образом, чтобы приложение ASP.NET получало и обрабатывал запросы параметров, добавьте следующую конфигурацию в файл *Web. config* приложения в разделе `<system.webServer><handlers>`:</span><span class="sxs-lookup"><span data-stu-id="6b27d-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="6b27d-213">Удаление `OPTIONSVerbHandler` предотвращает обработку запросов параметров службами IIS.</span><span class="sxs-lookup"><span data-stu-id="6b27d-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="6b27d-214">Замена `ExtensionlessUrlHandler-Integrated-4.0` позволяет запросам параметров обращаться к приложению, так как регистрация модуля по умолчанию разрешает только запросы GET, HEAD, POST и DEBUG с URL-адресами без расширений.</span><span class="sxs-lookup"><span data-stu-id="6b27d-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="6b27d-215">Правила области для [EnableCors]</span><span class="sxs-lookup"><span data-stu-id="6b27d-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="6b27d-216">Можно включить CORS для каждого действия, для каждого контроллера или глобально для всех контроллеров веб-API в приложении.</span><span class="sxs-lookup"><span data-stu-id="6b27d-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="6b27d-217">**За действие**</span><span class="sxs-lookup"><span data-stu-id="6b27d-217">**Per Action**</span></span>

<span data-ttu-id="6b27d-218">Чтобы включить CORS для одного действия, установите атрибут **[EnableCors]** в методе действия.</span><span class="sxs-lookup"><span data-stu-id="6b27d-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="6b27d-219">В следующем примере CORS включается только для метода `GetItem`.</span><span class="sxs-lookup"><span data-stu-id="6b27d-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="6b27d-220">**На контроллер**</span><span class="sxs-lookup"><span data-stu-id="6b27d-220">**Per Controller**</span></span>

<span data-ttu-id="6b27d-221">Если задать **[EnableCors]** в классе контроллера, он будет применяться ко всем действиям на контроллере.</span><span class="sxs-lookup"><span data-stu-id="6b27d-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="6b27d-222">Чтобы отключить CORS для действия, добавьте к действию атрибут **[дисаблекорс]** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="6b27d-223">В следующем примере показано включение CORS для каждого метода, кроме `PutItem`.</span><span class="sxs-lookup"><span data-stu-id="6b27d-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="6b27d-224">**Разместил**</span><span class="sxs-lookup"><span data-stu-id="6b27d-224">**Globally**</span></span>

<span data-ttu-id="6b27d-225">Чтобы включить CORS для всех контроллеров веб-API в приложении, передайте экземпляр **енаблекорсаттрибуте** в метод **EnableCors** :</span><span class="sxs-lookup"><span data-stu-id="6b27d-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="6b27d-226">Если задать атрибут более чем в одной области, порядок приоритета будет следующим:</span><span class="sxs-lookup"><span data-stu-id="6b27d-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="6b27d-227">Действие</span><span class="sxs-lookup"><span data-stu-id="6b27d-227">Action</span></span>
2. <span data-ttu-id="6b27d-228">Контроллер</span><span class="sxs-lookup"><span data-stu-id="6b27d-228">Controller</span></span>
3. <span data-ttu-id="6b27d-229">Global</span><span class="sxs-lookup"><span data-stu-id="6b27d-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="6b27d-230">Установка разрешенных источников</span><span class="sxs-lookup"><span data-stu-id="6b27d-230">Set the allowed origins</span></span>

<span data-ttu-id="6b27d-231">Параметр *Origins* атрибута **[EnableCors]** указывает, каким источникам разрешен доступ к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="6b27d-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="6b27d-232">Значение представляет собой разделенный запятыми список разрешенных источников.</span><span class="sxs-lookup"><span data-stu-id="6b27d-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="6b27d-233">Можно также использовать подстановочное значение "\*", чтобы разрешить запросы из любых источников.</span><span class="sxs-lookup"><span data-stu-id="6b27d-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="6b27d-234">Следует тщательно продуматьсь перед разрешением запросов из любого источника.</span><span class="sxs-lookup"><span data-stu-id="6b27d-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="6b27d-235">Это означает, что буквально любой веб-сайт может выполнять вызовы AJAX к веб-API.</span><span class="sxs-lookup"><span data-stu-id="6b27d-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="6b27d-236">Задание допустимых методов HTTP</span><span class="sxs-lookup"><span data-stu-id="6b27d-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="6b27d-237">Параметр *Methods* атрибута **[EnableCors]** указывает, какие методы HTTP могут получать доступ к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="6b27d-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="6b27d-238">Чтобы разрешить все методы, используйте подстановочное значение "\*".</span><span class="sxs-lookup"><span data-stu-id="6b27d-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="6b27d-239">В следующем примере допускаются только запросы GET и POST.</span><span class="sxs-lookup"><span data-stu-id="6b27d-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="6b27d-240">Задание разрешенных заголовков запроса</span><span class="sxs-lookup"><span data-stu-id="6b27d-240">Set the allowed request headers</span></span>

<span data-ttu-id="6b27d-241">В этой статье ранее было описано, как предварительный запрос может содержать заголовок Access-Control-request-headers, в котором перечислены заголовки HTTP, заданные приложением (так называемый «заголовки запроса автора»).</span><span class="sxs-lookup"><span data-stu-id="6b27d-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="6b27d-242">Параметр *headers* атрибута **[EnableCors]** указывает, какие заголовки запроса автора разрешены.</span><span class="sxs-lookup"><span data-stu-id="6b27d-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="6b27d-243">Чтобы разрешить любой заголовок, задайте для *заголовков* значение "\*".</span><span class="sxs-lookup"><span data-stu-id="6b27d-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="6b27d-244">Чтобы список разрешений определенные заголовки, установите для *заголовков* разделенный запятыми список разрешенных заголовков:</span><span class="sxs-lookup"><span data-stu-id="6b27d-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="6b27d-245">Однако браузеры не полностью согласуются с тем, как они устанавливают заголовки Access-Control-request-headers.</span><span class="sxs-lookup"><span data-stu-id="6b27d-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="6b27d-246">Например, Chrome в настоящее время включает "источник".</span><span class="sxs-lookup"><span data-stu-id="6b27d-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="6b27d-247">FireFox не включает стандартные заголовки, такие как "Accept", даже если приложение задает их в скрипте.</span><span class="sxs-lookup"><span data-stu-id="6b27d-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="6b27d-248">Если для *заголовков* заданы любые значения, отличные от "\*", следует включить по меньшей мере "Accept", "Content-Type" и "Origin", а также любые настраиваемые заголовки, которые требуется поддерживать.</span><span class="sxs-lookup"><span data-stu-id="6b27d-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="6b27d-249">Задание разрешенных заголовков ответа</span><span class="sxs-lookup"><span data-stu-id="6b27d-249">Set the allowed response headers</span></span>

<span data-ttu-id="6b27d-250">По умолчанию браузер не предоставляет приложению все заголовки ответа.</span><span class="sxs-lookup"><span data-stu-id="6b27d-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="6b27d-251">По умолчанию доступны заголовки ответов:</span><span class="sxs-lookup"><span data-stu-id="6b27d-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="6b27d-252">Cache-Control;</span><span class="sxs-lookup"><span data-stu-id="6b27d-252">Cache-Control</span></span>
- <span data-ttu-id="6b27d-253">Content-Language;</span><span class="sxs-lookup"><span data-stu-id="6b27d-253">Content-Language</span></span>
- <span data-ttu-id="6b27d-254">Content-Type</span><span class="sxs-lookup"><span data-stu-id="6b27d-254">Content-Type</span></span>
- <span data-ttu-id="6b27d-255">Expires</span><span class="sxs-lookup"><span data-stu-id="6b27d-255">Expires</span></span>
- <span data-ttu-id="6b27d-256">Последний измененный</span><span class="sxs-lookup"><span data-stu-id="6b27d-256">Last-Modified</span></span>
- <span data-ttu-id="6b27d-257">Включают</span><span class="sxs-lookup"><span data-stu-id="6b27d-257">Pragma</span></span>

<span data-ttu-id="6b27d-258">Спецификация CORS вызывает эти [простые заголовки ответа](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span><span class="sxs-lookup"><span data-stu-id="6b27d-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="6b27d-259">Чтобы сделать другие заголовки доступными для приложения, задайте параметр *exposedHeaders* **[EnableCors]** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="6b27d-260">В следующем примере метод `Get` контроллера задает пользовательский заголовок с именем "X-Custom-Header".</span><span class="sxs-lookup"><span data-stu-id="6b27d-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="6b27d-261">По умолчанию браузер не будет предоставлять этот заголовок в запросе между источниками.</span><span class="sxs-lookup"><span data-stu-id="6b27d-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="6b27d-262">Чтобы сделать заголовок доступным, включите "X-Custom-Header" в *exposedHeaders*.</span><span class="sxs-lookup"><span data-stu-id="6b27d-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="6b27d-263">Передача учетных данных в запросах между источниками</span><span class="sxs-lookup"><span data-stu-id="6b27d-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="6b27d-264">Учетные данные требует специальной обработки в запросе CORS.</span><span class="sxs-lookup"><span data-stu-id="6b27d-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="6b27d-265">По умолчанию браузер не отправляет учетные данные с запросом между источниками.</span><span class="sxs-lookup"><span data-stu-id="6b27d-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="6b27d-266">Учетные данные включают файлы cookie, а также схемы проверки подлинности HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b27d-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="6b27d-267">Чтобы отправить учетные данные с запросом между источниками, клиент должен установить для **XMLHttpRequest. вискредентиалс** значение true.</span><span class="sxs-lookup"><span data-stu-id="6b27d-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="6b27d-268">Непосредственное использование **XMLHttpRequest** :</span><span class="sxs-lookup"><span data-stu-id="6b27d-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="6b27d-269">В jQuery:</span><span class="sxs-lookup"><span data-stu-id="6b27d-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="6b27d-270">Кроме того, сервер должен разрешать учетные данные.</span><span class="sxs-lookup"><span data-stu-id="6b27d-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="6b27d-271">Чтобы разрешить учетные данные для разных источников в веб-API, задайте для свойства **суппортскредентиалс** атрибута **[EnableCors]** значение true:</span><span class="sxs-lookup"><span data-stu-id="6b27d-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="6b27d-272">Если это свойство имеет значение true, ответ HTTP будет включать заголовок Access-Control-Allow-Credentials.</span><span class="sxs-lookup"><span data-stu-id="6b27d-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="6b27d-273">Этот заголовок сообщает браузеру, что сервер разрешает учетные данные для запроса между источниками.</span><span class="sxs-lookup"><span data-stu-id="6b27d-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="6b27d-274">Если браузер отправляет учетные данные, но ответ не включает допустимый заголовок Access-Control-Allow-Credential, браузер не будет предоставлять ответ приложению, а запрос AJAX завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="6b27d-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="6b27d-275">Будьте внимательны при установке параметра **суппортскредентиалс** в значение true, так как это означает, что веб-сайт в другом домене может отправить учетные данные пользователя, выполнившего вход, в веб-интерфейс API от имени пользователя без уведомления пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b27d-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="6b27d-276">В спецификации CORS также указано, что установка *источников* на &quot;\*&quot; недопустима, если **суппортскредентиалс** имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="6b27d-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="6b27d-277">Пользовательские поставщики политик CORS</span><span class="sxs-lookup"><span data-stu-id="6b27d-277">Custom CORS policy providers</span></span>

<span data-ttu-id="6b27d-278">Атрибут **[EnableCors]** реализует интерфейс **икорсполиципровидер** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="6b27d-279">Вы можете предоставить собственную реализацию, создав класс, производный от **Attribute** , и реализующий **икорсполиципровидер**.</span><span class="sxs-lookup"><span data-stu-id="6b27d-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsPolicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="6b27d-280">Теперь можно применить атрибут в любом месте, которое вы бы поместили **[EnableCors]** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="6b27d-281">Например, Пользовательский поставщик политики CORS может считывать параметры из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6b27d-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="6b27d-282">В качестве альтернативы использованию атрибутов можно зарегистрировать объект **икорсполиципровидерфактори** , создающий объекты **икорсполиципровидер** .</span><span class="sxs-lookup"><span data-stu-id="6b27d-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="6b27d-283">Чтобы задать **икорсполиципровидерфактори**, вызовите метод расширения **сеткорсполиципровидерфактори** при запуске, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6b27d-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="6b27d-284">Поддержка браузеров</span><span class="sxs-lookup"><span data-stu-id="6b27d-284">Browser support</span></span>

<span data-ttu-id="6b27d-285">Пакет CORS веб-API — это технология на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="6b27d-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="6b27d-286">Браузер пользователя также должен поддерживать CORS.</span><span class="sxs-lookup"><span data-stu-id="6b27d-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="6b27d-287">К счастью, текущие версии всех основных браузеров включают [поддержку CORS](http://caniuse.com/cors).</span><span class="sxs-lookup"><span data-stu-id="6b27d-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
