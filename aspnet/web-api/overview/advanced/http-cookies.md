---
uid: web-api/overview/advanced/http-cookies
title: Файлы cookie HTTP в ASP.NET Web API - ASP.NET 4.x
author: MikeWasson
description: Описывается, как отправлять и получать файлы cookie HTTP в веб-API для ASP.NET 4.x.
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65126240"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="8011d-103">Файлы cookie HTTP в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8011d-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="8011d-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8011d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8011d-105">В этом разделе описывается, как отправлять и получать файлы cookie HTTP в веб-API.</span><span class="sxs-lookup"><span data-stu-id="8011d-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="8011d-106">Фон с помощью файлов cookie HTTP</span><span class="sxs-lookup"><span data-stu-id="8011d-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="8011d-107">В этом разделе дается краткий обзор реализации файлы cookie на уровне HTTP.</span><span class="sxs-lookup"><span data-stu-id="8011d-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="8011d-108">Дополнительные сведения см. в [RFC 6265](http://tools.ietf.org/html/rfc6265).</span><span class="sxs-lookup"><span data-stu-id="8011d-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="8011d-109">Файл cookie — это часть данных, которые сервер отправляет HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="8011d-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="8011d-110">(Необязательно), клиент сохраняет файл cookie и возвращает его при последующих запросах.</span><span class="sxs-lookup"><span data-stu-id="8011d-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="8011d-111">Это позволяет использовать общие состояния клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="8011d-111">This allows the client and server to share state.</span></span> <span data-ttu-id="8011d-112">Чтобы задать файл cookie, сервер включает заголовок Set-Cookie в ответе.</span><span class="sxs-lookup"><span data-stu-id="8011d-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="8011d-113">Формат файла cookie — это пара имя значение, с дополнительными атрибутами.</span><span class="sxs-lookup"><span data-stu-id="8011d-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="8011d-114">Пример:</span><span class="sxs-lookup"><span data-stu-id="8011d-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="8011d-115">Ниже приведен пример с атрибутами:</span><span class="sxs-lookup"><span data-stu-id="8011d-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="8011d-116">Чтобы вернуть файл cookie на сервер, клиент включает заголовок Cookie в последующих запросах.</span><span class="sxs-lookup"><span data-stu-id="8011d-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="8011d-117">HTTP-ответ может включать несколько заголовков Set-Cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="8011d-118">Клиент возвращает несколько файлов cookie, используя один заголовок файла Cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="8011d-119">Объема и продолжительности файла cookie управляются следующие атрибуты в заголовке Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="8011d-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="8011d-120">**Домен**: Сообщает клиенту, в какой домен должен получать куки-файл.</span><span class="sxs-lookup"><span data-stu-id="8011d-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="8011d-121">Например если домен — «example.com», клиент возвращает файл cookie в каждом поддомен example.com.</span><span class="sxs-lookup"><span data-stu-id="8011d-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="8011d-122">Если не указан, домен — на сервере-источнике.</span><span class="sxs-lookup"><span data-stu-id="8011d-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="8011d-123">**Путь**: Ограничивает куки-файл по указанному пути в пределах домена.</span><span class="sxs-lookup"><span data-stu-id="8011d-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="8011d-124">Если не указан, используется путь к URI запроса.</span><span class="sxs-lookup"><span data-stu-id="8011d-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="8011d-125">**Срок действия истекает**: Задает дату окончания срока действия файла cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="8011d-126">Клиент удаляет файл cookie, когда истечет срок его действия.</span><span class="sxs-lookup"><span data-stu-id="8011d-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="8011d-127">**Max-Age**: Задает максимальное время существования файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="8011d-128">Клиент удаляет файл cookie, когда будет достигнуто максимальное время существования.</span><span class="sxs-lookup"><span data-stu-id="8011d-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="8011d-129">Если оба `Expires` и `Max-Age` заданы, `Max-Age` имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="8011d-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="8011d-130">Если не задан, клиент удаляет файл cookie после завершения текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="8011d-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="8011d-131">(Точное значение «сеанс» определяется агентом пользователя.)</span><span class="sxs-lookup"><span data-stu-id="8011d-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="8011d-132">Однако имейте в виду, что клиенты могут игнорировать файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="8011d-133">Например пользователь может отключить файлы cookie для соблюдения конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="8011d-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="8011d-134">Клиенты могут удалять файлы cookie, до истечения срока действия или ограничить количество хранящихся файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="8011d-135">По соображениям конфиденциальности клиенты отклоняют часто файлы cookie «third party», где домен соответствует на сервере-источнике.</span><span class="sxs-lookup"><span data-stu-id="8011d-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="8011d-136">Короче говоря сервер не следует полагаться на получение, на которые он задает файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="8011d-137">Файлы cookie в веб-API</span><span class="sxs-lookup"><span data-stu-id="8011d-137">Cookies in Web API</span></span>

<span data-ttu-id="8011d-138">Чтобы добавить маркер в HTTP-ответ, создайте **CookieHeaderValue** экземпляр, представляющий файл cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="8011d-139">Затем вызовите **AddCookies** метод расширения, который определен в **System.Net.Http. HttpResponseHeadersExtensions** класс, чтобы добавить файл cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="8011d-140">Например следующий код добавляет файл cookie в действие контроллера:</span><span class="sxs-lookup"><span data-stu-id="8011d-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="8011d-141">Обратите внимание, что **AddCookies** принимает массив **CookieHeaderValue** экземпляров.</span><span class="sxs-lookup"><span data-stu-id="8011d-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="8011d-142">Чтобы извлечь файлы cookie запроса клиента, вызовите **GetCookies** метод:</span><span class="sxs-lookup"><span data-stu-id="8011d-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="8011d-143">Объект **CookieHeaderValue** содержит коллекцию **CookieState** экземпляров.</span><span class="sxs-lookup"><span data-stu-id="8011d-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="8011d-144">Каждый **CookieState** представляет один файл cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="8011d-145">Метод индексатор для получения **CookieState** по имени, как показано.</span><span class="sxs-lookup"><span data-stu-id="8011d-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="8011d-146">Файл Cookie структурированных данных</span><span class="sxs-lookup"><span data-stu-id="8011d-146">Structured Cookie Data</span></span>

<span data-ttu-id="8011d-147">Многие браузеры ограничить количество файлов cookie, они будут храниться&#8212;как общее количество, так и номер каждого домена.</span><span class="sxs-lookup"><span data-stu-id="8011d-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="8011d-148">Таким образом можно попробовать установить структурированных данных в единый файл cookie, а не задавать несколько файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="8011d-149">RFC 6265 не определяет структуру данных файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="8011d-150">С помощью **CookieHeaderValue** класса, можно передать список пар имя значение для данных файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="8011d-151">Эти пары "имя значение" кодируются в виде URL-адреса формы данных в заголовке Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="8011d-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="8011d-152">Приведенный выше код создает следующий заголовок Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="8011d-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="8011d-153">**CookieState** класс предоставляет метод индексатора для считывания вложенных значений из файла cookie в сообщении запроса:</span><span class="sxs-lookup"><span data-stu-id="8011d-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="8011d-154">Пример Задание и получение файлов cookie в обработчик сообщений</span><span class="sxs-lookup"><span data-stu-id="8011d-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="8011d-155">В предыдущих примерах показано, как использовать файлы cookie из контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="8011d-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="8011d-156">Другой вариант — использовать [обработчиков сообщений](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="8011d-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="8011d-157">Ранее в конвейере контроллеры вызываются обработчики сообщений.</span><span class="sxs-lookup"><span data-stu-id="8011d-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="8011d-158">Обработчик сообщений можно считать файлы cookie из запроса, прежде чем они достигнут контроллера или добавьте файлы cookie в ответ после контроллер создает ответ.</span><span class="sxs-lookup"><span data-stu-id="8011d-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="8011d-159">В следующем коде показано обработчик сообщений для создания идентификаторов сеансов.</span><span class="sxs-lookup"><span data-stu-id="8011d-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="8011d-160">Идентификатор сеанса хранится в файле cookie.</span><span class="sxs-lookup"><span data-stu-id="8011d-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="8011d-161">Обработчик проверяет запрос файл cookie сеанса.</span><span class="sxs-lookup"><span data-stu-id="8011d-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="8011d-162">Если запрос не содержит файл cookie, обработчик создает идентификатор нового сеанса.</span><span class="sxs-lookup"><span data-stu-id="8011d-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="8011d-163">В любом случае обработчик сохраняет идентификатор сеанса в **HttpRequestMessage.Properties** контейнер свойств.</span><span class="sxs-lookup"><span data-stu-id="8011d-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="8011d-164">Он также добавляет файл cookie сеанса для HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="8011d-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="8011d-165">Эта реализация не проверяет, что идентификатор сеанса от клиента, фактически был выдан сервером.</span><span class="sxs-lookup"><span data-stu-id="8011d-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="8011d-166">Не используйте его как форму проверки подлинности!</span><span class="sxs-lookup"><span data-stu-id="8011d-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="8011d-167">Точка примера — Показать куки-файлы HTTP.</span><span class="sxs-lookup"><span data-stu-id="8011d-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="8011d-168">Контроллер можно получить идентификатор сеанса из **HttpRequestMessage.Properties** контейнер свойств.</span><span class="sxs-lookup"><span data-stu-id="8011d-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
