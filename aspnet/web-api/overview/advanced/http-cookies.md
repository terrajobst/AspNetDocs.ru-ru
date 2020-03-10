---
uid: web-api/overview/advanced/http-cookies
title: Файлы cookie HTTP в веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: Описывает, как отправлять и получать файлы cookie HTTP в веб-API для ASP.NET 4. x.
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449316"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="91115-103">Файлы cookie HTTP в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="91115-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="91115-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="91115-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="91115-105">В этом разделе описано, как отправлять и получать файлы cookie HTTP в веб-API.</span><span class="sxs-lookup"><span data-stu-id="91115-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="91115-106">Общие сведения об cookie-файлах HTTP</span><span class="sxs-lookup"><span data-stu-id="91115-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="91115-107">В этом разделе приводится краткий обзор реализации файлов cookie на уровне HTTP.</span><span class="sxs-lookup"><span data-stu-id="91115-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="91115-108">Дополнительные сведения см. в [RFC 6265](http://tools.ietf.org/html/rfc6265).</span><span class="sxs-lookup"><span data-stu-id="91115-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="91115-109">Файл cookie — это часть данных, которую сервер отправляет в ответе HTTP.</span><span class="sxs-lookup"><span data-stu-id="91115-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="91115-110">Клиент (необязательно) сохраняет файл cookie и возвращает его в последующие запросы.</span><span class="sxs-lookup"><span data-stu-id="91115-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="91115-111">Это позволяет клиенту и серверу совместно использовать состояние.</span><span class="sxs-lookup"><span data-stu-id="91115-111">This allows the client and server to share state.</span></span> <span data-ttu-id="91115-112">Чтобы задать файл cookie, сервер включает в ответ заголовок Set-cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="91115-113">Формат файла cookie — это пара "имя-значение" с необязательными атрибутами.</span><span class="sxs-lookup"><span data-stu-id="91115-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="91115-114">Пример:</span><span class="sxs-lookup"><span data-stu-id="91115-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="91115-115">Ниже приведен пример с атрибутами.</span><span class="sxs-lookup"><span data-stu-id="91115-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="91115-116">Чтобы вернуть файл cookie на сервер, клиент включает заголовок cookie в последующих запросах.</span><span class="sxs-lookup"><span data-stu-id="91115-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="91115-117">HTTP-ответ может включать несколько заголовков Set-cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="91115-118">Клиент возвращает несколько файлов cookie, используя один заголовок файла cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="91115-119">Область и длительность файла cookie контролируются следующими атрибутами в заголовке Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="91115-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="91115-120">**Домен**: сообщает клиенту, какой домен должен получить файл cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="91115-121">Например, если домен имеет значение "example.com", клиент возвращает файл cookie в каждый поддомен example.com.</span><span class="sxs-lookup"><span data-stu-id="91115-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="91115-122">Если этот параметр не указан, то домен является сервером-источником.</span><span class="sxs-lookup"><span data-stu-id="91115-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="91115-123">**Путь**: файл cookie ограничен указанным путем в домене.</span><span class="sxs-lookup"><span data-stu-id="91115-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="91115-124">Если этот параметр не указан, используется путь URI запроса.</span><span class="sxs-lookup"><span data-stu-id="91115-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="91115-125">**Срок действия**: задает дату окончания срока действия для файла cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="91115-126">Клиент удаляет файл cookie по истечении срока его действия.</span><span class="sxs-lookup"><span data-stu-id="91115-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="91115-127">**Max-age**: задает максимальный возраст для cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="91115-128">Клиент удаляет файл cookie при достижении максимального срока.</span><span class="sxs-lookup"><span data-stu-id="91115-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="91115-129">Если заданы и `Expires`, и `Max-Age`, `Max-Age` имеет приоритет.</span><span class="sxs-lookup"><span data-stu-id="91115-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="91115-130">Если ни один из этих параметров не задан, клиент удаляет файл cookie при завершении текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="91115-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="91115-131">(Точное значение параметра Session определяется агентом пользователя.)</span><span class="sxs-lookup"><span data-stu-id="91115-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="91115-132">Однако имейте в виду, что клиенты могут игнорировать файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="91115-133">Например, пользователь может отключить файлы cookie в целях обеспечения конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="91115-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="91115-134">Клиенты могут удалять файлы cookie до истечения срока их действия или ограничивать число хранимых файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="91115-135">В целях обеспечения конфиденциальности клиенты часто ототклоняют "сторонние" файлы cookie, в которых домен не соответствует серверу источника.</span><span class="sxs-lookup"><span data-stu-id="91115-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="91115-136">Вкратце, сервер не должен полагаться на возвращение файлов cookie, которые он задает.</span><span class="sxs-lookup"><span data-stu-id="91115-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="91115-137">Файлы cookie в веб-API</span><span class="sxs-lookup"><span data-stu-id="91115-137">Cookies in Web API</span></span>

<span data-ttu-id="91115-138">Чтобы добавить файл cookie в HTTP-ответ, создайте экземпляр **кукиехеадервалуе** , представляющий файл cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="91115-139">Затем вызовите метод расширения **аддкукиес** , который определен в **системе .NET. http. Класс Хттпреспонсехеадерсекстенсионс** для добавления файла cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="91115-140">Например, следующий код добавляет файл cookie в действие контроллера:</span><span class="sxs-lookup"><span data-stu-id="91115-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="91115-141">Обратите внимание, что **аддкукиес** принимает массив экземпляров **кукиехеадервалуе** .</span><span class="sxs-lookup"><span data-stu-id="91115-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="91115-142">Чтобы извлечь файлы cookie из клиентского запроса, вызовите метод **Кука** :</span><span class="sxs-lookup"><span data-stu-id="91115-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="91115-143">**Кукиехеадервалуе** содержит коллекцию экземпляров **кукиестате** .</span><span class="sxs-lookup"><span data-stu-id="91115-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="91115-144">Каждый **кукиестате** представляет один файл cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="91115-145">Используйте метод индексатора для получения **кукиестате** по имени, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="91115-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="91115-146">Структурированные данные файлов cookie</span><span class="sxs-lookup"><span data-stu-id="91115-146">Structured Cookie Data</span></span>

<span data-ttu-id="91115-147">Многие браузеры ограничивают количество файлов cookie,&#8212;в которых они будут хранить как общее число, так и число на каждый домен.</span><span class="sxs-lookup"><span data-stu-id="91115-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="91115-148">Таким образом, можно разместить структурированные данные в одном файле cookie, а не задавать несколько файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="91115-149">В RFC 6265 не определена структура данных файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="91115-150">С помощью класса **кукиехеадервалуе** можно передать список пар "имя-значение" для данных файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="91115-151">Эти пары "имя-значение" кодируются как данные формы в формате URL-адреса в заголовке Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="91115-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="91115-152">Предыдущий код создает следующий заголовок Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="91115-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="91115-153">Класс **кукиестате** предоставляет метод индексатора для чтения подзначений из файла cookie в сообщении запроса:</span><span class="sxs-lookup"><span data-stu-id="91115-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="91115-154">Пример. задание и извлечение файлов cookie в обработчике сообщений</span><span class="sxs-lookup"><span data-stu-id="91115-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="91115-155">В предыдущих примерах было показано, как использовать файлы cookie в контроллере веб-API.</span><span class="sxs-lookup"><span data-stu-id="91115-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="91115-156">Другой вариант — использовать [обработчики сообщений](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="91115-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="91115-157">Обработчики сообщений вызываются в конвейере раньше, чем на контроллерах.</span><span class="sxs-lookup"><span data-stu-id="91115-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="91115-158">Обработчик сообщений может считывать файлы cookie из запроса до того, как запрос достигнет контроллера, или добавить файлы cookie в ответ после того, как контроллер создаст ответ.</span><span class="sxs-lookup"><span data-stu-id="91115-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="91115-159">В следующем коде показан обработчик сообщений для создания идентификаторов сеансов.</span><span class="sxs-lookup"><span data-stu-id="91115-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="91115-160">Идентификатор сеанса хранится в файле cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="91115-161">Обработчик проверяет запрос для файла cookie сеанса.</span><span class="sxs-lookup"><span data-stu-id="91115-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="91115-162">Если запрос не содержит файл cookie, обработчик создает новый идентификатор сеанса.</span><span class="sxs-lookup"><span data-stu-id="91115-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="91115-163">В любом случае обработчик сохраняет идентификатор сеанса в контейнере свойств **HttpRequestMessage. Properties** .</span><span class="sxs-lookup"><span data-stu-id="91115-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="91115-164">Он также добавляет файл cookie сеанса в HTTP-ответ.</span><span class="sxs-lookup"><span data-stu-id="91115-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="91115-165">Эта реализация не проверяет, что идентификатор сеанса клиента фактически выдан сервером.</span><span class="sxs-lookup"><span data-stu-id="91115-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="91115-166">Не используйте его в качестве формы проверки подлинности!</span><span class="sxs-lookup"><span data-stu-id="91115-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="91115-167">Точкой примера является отображение управления HTTP-файлами cookie.</span><span class="sxs-lookup"><span data-stu-id="91115-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="91115-168">Контроллер может получить идентификатор сеанса из контейнера свойств **HttpRequestMessage. Properties** .</span><span class="sxs-lookup"><span data-stu-id="91115-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
