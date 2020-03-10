---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: Краткий справочник по API веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: На этой странице содержится список с краткими примерами наиболее часто используемых объектов, свойств и методов программирования веб-страницы ASP.NET с синтаксис Razor.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463584"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="22094-103">Краткий справочник по API веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="22094-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="22094-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="22094-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="22094-105">На этой странице содержится список с краткими примерами наиболее часто используемых объектов, свойств и методов программирования веб-страницы ASP.NET с синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="22094-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="22094-106">Описания, помеченные как "(v2)", появились в веб-страницы ASP.NET версии 2.</span><span class="sxs-lookup"><span data-stu-id="22094-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="22094-107">Справочную документацию по API см. в [справочной документации по веб-страницы ASP.NET](https://go.microsoft.com/fwlink/?LinkId=208659) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="22094-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="22094-108">Версии программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="22094-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="22094-109">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="22094-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="22094-110">Этот учебник также работает с веб-страницы ASP.NET 2 и веб-страницы ASP.NET 1,0 (за исключением функций, помеченных как v2).</span><span class="sxs-lookup"><span data-stu-id="22094-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>

<span data-ttu-id="22094-111">На этой странице содержатся справочные сведения по следующим параметрам.</span><span class="sxs-lookup"><span data-stu-id="22094-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="22094-112">Классы</span><span class="sxs-lookup"><span data-stu-id="22094-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="22094-113">Data</span><span class="sxs-lookup"><span data-stu-id="22094-113">Data</span></span>](#Data)
- [<span data-ttu-id="22094-114">Вспомогательные функции</span><span class="sxs-lookup"><span data-stu-id="22094-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="22094-115">Проверка</span><span class="sxs-lookup"><span data-stu-id="22094-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="22094-116">Классы</span><span class="sxs-lookup"><span data-stu-id="22094-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="22094-117">Содержит данные, которые могут совместно использоваться любыми страницами в приложении.</span><span class="sxs-lookup"><span data-stu-id="22094-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="22094-118">Для доступа к тем же данным можно использовать динамическое свойство `App`, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="22094-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="22094-119">Преобразует строковое значение в логическое значение (true/false).</span><span class="sxs-lookup"><span data-stu-id="22094-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="22094-120">Возвращает false или указанное значение, если строка не представляет значение true/false.</span><span class="sxs-lookup"><span data-stu-id="22094-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="22094-121">Преобразует строковое значение в дату и время.</span><span class="sxs-lookup"><span data-stu-id="22094-121">Converts a string value to date/time.</span></span> <span data-ttu-id="22094-122">Возвращает `DateTime.MinValue` или указанное значение, если строка не представляет дату и время.</span><span class="sxs-lookup"><span data-stu-id="22094-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="22094-123">Преобразует строковое значение в десятичное значение.</span><span class="sxs-lookup"><span data-stu-id="22094-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="22094-124">Возвращает 0,0 или указанное значение, если строка не представляет десятичное значение.</span><span class="sxs-lookup"><span data-stu-id="22094-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="22094-125">Преобразует строковое значение в число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="22094-125">Converts a string value to a float.</span></span> <span data-ttu-id="22094-126">Возвращает 0,0 или указанное значение, если строка не представляет десятичное значение.</span><span class="sxs-lookup"><span data-stu-id="22094-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="22094-127">Преобразует строковое значение в целое число.</span><span class="sxs-lookup"><span data-stu-id="22094-127">Converts a string value to an integer.</span></span> <span data-ttu-id="22094-128">Возвращает 0 или указанное значение, если строка не представляет целое число.</span><span class="sxs-lookup"><span data-stu-id="22094-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="22094-129">Создает совместимый с браузером URL-адрес из локального пути к файлу с дополнительными дополнительными элементами пути.</span><span class="sxs-lookup"><span data-stu-id="22094-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="22094-130">Отображает *значение* как HTML-разметку вместо отображения его в виде выходных данных в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="22094-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="22094-131">Возвращает значение true, если значение может быть преобразовано из строки в указанный тип.</span><span class="sxs-lookup"><span data-stu-id="22094-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="22094-132">Возвращает значение true, если объект или переменная не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="22094-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="22094-133">Возвращает значение true, если запрос является ЗАПИСЬю.</span><span class="sxs-lookup"><span data-stu-id="22094-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="22094-134">(Первоначальные запросы обычно являются GET.)</span><span class="sxs-lookup"><span data-stu-id="22094-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="22094-135">Задает путь к странице макета, применяемой к этой странице.</span><span class="sxs-lookup"><span data-stu-id="22094-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="22094-136">Содержит данные, общие для страницы, страницы макета и частичные страницы в текущем запросе.</span><span class="sxs-lookup"><span data-stu-id="22094-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="22094-137">Для доступа к тем же данным можно использовать динамическое свойство `Page`, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="22094-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="22094-138">(Страницы макета) Подготавливает к просмотру содержимое страницы содержимого, не находящегося ни в одном из именованных разделов.</span><span class="sxs-lookup"><span data-stu-id="22094-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="22094-139">Визуализирует страницу содержимого, используя указанный путь и дополнительные дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="22094-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="22094-140">Можно получить значения дополнительных параметров из `PageData` по положению (например 1) или ключу (пример 2).</span><span class="sxs-lookup"><span data-stu-id="22094-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="22094-141">(Страницы макета) Подготавливает к просмотру раздел содержимого, имеющий имя.</span><span class="sxs-lookup"><span data-stu-id="22094-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="22094-142">Задайте для параметра *обязательно* значение false, чтобы сделать раздел необязательным.</span><span class="sxs-lookup"><span data-stu-id="22094-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="22094-143">Возвращает или задает значение cookie HTTP.</span><span class="sxs-lookup"><span data-stu-id="22094-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="22094-144">Возвращает файлы, которые были переданы в текущем запросе.</span><span class="sxs-lookup"><span data-stu-id="22094-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="22094-145">Возвращает данные, которые были опубликованы в форме (строки).</span><span class="sxs-lookup"><span data-stu-id="22094-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="22094-146">`Request[key]` проверяет коллекции `Request.Form` и `Request.QueryString`.</span><span class="sxs-lookup"><span data-stu-id="22094-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="22094-147">Возвращает данные, указанные в строке запроса URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="22094-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="22094-148">`Request[key]` проверяет коллекции `Request.Form` и `Request.QueryString`.</span><span class="sxs-lookup"><span data-stu-id="22094-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="22094-149">Выборочно отключает проверку запросов для элемента Form, значения строки запроса, файла cookie или значения заголовка.</span><span class="sxs-lookup"><span data-stu-id="22094-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="22094-150">Проверка запросов включена по умолчанию и запрещает пользователям публиковать разметку или другое потенциально опасное содержимое.</span><span class="sxs-lookup"><span data-stu-id="22094-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="22094-151">Добавляет заголовок HTTP-сервера в ответ.</span><span class="sxs-lookup"><span data-stu-id="22094-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="22094-152">Кэширует выходные данные страницы в течение заданного времени.</span><span class="sxs-lookup"><span data-stu-id="22094-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="22094-153">При необходимости задайте для параметра *скользящий* значение время ожидания на каждом доступе к странице и *варибипарамс* для кэширования различных версий страницы для каждой строки запроса в запросе страницы.</span><span class="sxs-lookup"><span data-stu-id="22094-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="22094-154">Перенаправляет запрос браузера в новое расположение.</span><span class="sxs-lookup"><span data-stu-id="22094-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="22094-155">Задает код состояния HTTP, отправляемый браузеру.</span><span class="sxs-lookup"><span data-stu-id="22094-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="22094-156">Записывает содержимое *данных* в ответ с необязательным типом MIME.</span><span class="sxs-lookup"><span data-stu-id="22094-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="22094-157">Записывает содержимое файла в ответ.</span><span class="sxs-lookup"><span data-stu-id="22094-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="22094-158">(Страницы макета) Определяет раздел содержимого с именем.</span><span class="sxs-lookup"><span data-stu-id="22094-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="22094-159">Декодирует строку, которая является HTML-кодировкой.</span><span class="sxs-lookup"><span data-stu-id="22094-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="22094-160">Кодирует строку для отрисовки в разметке HTML.</span><span class="sxs-lookup"><span data-stu-id="22094-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="22094-161">Возвращает физический путь к серверу для указанного виртуального пути.</span><span class="sxs-lookup"><span data-stu-id="22094-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="22094-162">Декодирует текст из URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="22094-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="22094-163">Кодирует текст для размещения в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="22094-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="22094-164">Возвращает или задает значение, которое существует до тех пор, пока пользователь не закроет браузер.</span><span class="sxs-lookup"><span data-stu-id="22094-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="22094-165">Отображает строковое представление значения объекта.</span><span class="sxs-lookup"><span data-stu-id="22094-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="22094-166">Получает дополнительные данные из URL-адреса (например, */мипаже/екстрадата*).</span><span class="sxs-lookup"><span data-stu-id="22094-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="22094-167">Изменяет пароль заданного пользователя.</span><span class="sxs-lookup"><span data-stu-id="22094-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="22094-168">Подтверждает учетную запись с помощью токена подтверждения учетной записи.</span><span class="sxs-lookup"><span data-stu-id="22094-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="22094-169">Создает новую учетную запись пользователя с указанными именем пользователя и паролем.</span><span class="sxs-lookup"><span data-stu-id="22094-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="22094-170">Чтобы запросить маркер подтверждения, передайте значение true для *рекуиреконфирматионтокен.*</span><span class="sxs-lookup"><span data-stu-id="22094-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="22094-171">Возвращает целочисленный идентификатор текущего вошедшего в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="22094-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="22094-172">Возвращает имя пользователя, выполнившего вход в систему.</span><span class="sxs-lookup"><span data-stu-id="22094-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="22094-173">Создает маркер сброса пароля, который может быть отправлен пользователю по электронной почте, чтобы пользователь мог сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="22094-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="22094-174">Возвращает идентификатор пользователя из имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="22094-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="22094-175">Возвращает значение true, если текущий пользователь вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="22094-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="22094-176">Возвращает значение true, если пользователь подтвердил (например, с помощью сообщения электронной почты с подтверждением).</span><span class="sxs-lookup"><span data-stu-id="22094-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="22094-177">Возвращает значение true, если имя текущего пользователя совпадает с указанным именем пользователя.</span><span class="sxs-lookup"><span data-stu-id="22094-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="22094-178">Регистрирует пользователя в, настроив маркер проверки подлинности в файле cookie.</span><span class="sxs-lookup"><span data-stu-id="22094-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="22094-179">Записывает пользователя в журнал, удаляя файл cookie маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="22094-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="22094-180">Если пользователь не прошел проверку подлинности, задает состояние HTTP 401 (Не санкционировано).</span><span class="sxs-lookup"><span data-stu-id="22094-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="22094-181">Если текущий пользователь не является членом одной из указанных ролей, устанавливает для состояния HTTP значение 401 (не санкционировано).</span><span class="sxs-lookup"><span data-stu-id="22094-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="22094-182">Если текущий пользователь не является пользователем, указанным в поле *username*, устанавливает для состояния HTTP значение 401 (не санкционировано).</span><span class="sxs-lookup"><span data-stu-id="22094-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="22094-183">Если маркер сброса пароля действителен, изменяет пароль пользователя на новый пароль.</span><span class="sxs-lookup"><span data-stu-id="22094-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="22094-184">Данные</span><span class="sxs-lookup"><span data-stu-id="22094-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="22094-185">Выполняет *SQLstatement* (с необязательными параметрами), например операции вставки, удаления или обновления, и возвращает количество затронутых записей.</span><span class="sxs-lookup"><span data-stu-id="22094-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="22094-186">Возвращает столбец идентификаторов из последней вставленной строки.</span><span class="sxs-lookup"><span data-stu-id="22094-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="22094-187">Открывает указанный файл базы данных или базу данных, заданную с помощью именованной строки соединения из файла *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="22094-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="22094-188">Открывает базу данных, используя строку подключения.</span><span class="sxs-lookup"><span data-stu-id="22094-188">Opens a database using the connection string.</span></span> <span data-ttu-id="22094-189">(Это отличается от `Database.Open`, в которой используется имя строки подключения.)</span><span class="sxs-lookup"><span data-stu-id="22094-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="22094-190">Запрашивает базу данных с помощью *SQLstatement* (при необходимости передавая параметры) и возвращает результаты в виде коллекции.</span><span class="sxs-lookup"><span data-stu-id="22094-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="22094-191">Выполняет *SQLstatement* (с необязательными параметрами) и возвращает одну запись.</span><span class="sxs-lookup"><span data-stu-id="22094-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="22094-192">Выполняет *SQLstatement* (с необязательными параметрами) и возвращает одно значение.</span><span class="sxs-lookup"><span data-stu-id="22094-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="22094-193">Вспомогательные методы</span><span class="sxs-lookup"><span data-stu-id="22094-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="22094-194">Подготавливает к просмотру код JavaScript Google Analytics для указанного идентификатора.</span><span class="sxs-lookup"><span data-stu-id="22094-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="22094-195">Визуализирует код JavaScript Статкаунтер Analytics для указанного проекта.</span><span class="sxs-lookup"><span data-stu-id="22094-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="22094-196">Отображает код JavaScript для анализа Yahoo для указанной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="22094-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="22094-197">Передает Поиск в Bing.</span><span class="sxs-lookup"><span data-stu-id="22094-197">Passes a search to Bing.</span></span> <span data-ttu-id="22094-198">Чтобы указать сайт для поиска и заголовок поля поиска, можно задать свойства `Bing.SiteUrl` и `Bing.SiteTitle`.</span><span class="sxs-lookup"><span data-stu-id="22094-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="22094-199">Обычно эти свойства задаются на странице *\_AppStart* .</span><span class="sxs-lookup"><span data-stu-id="22094-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="22094-200">Инициализирует диаграмму.</span><span class="sxs-lookup"><span data-stu-id="22094-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="22094-201">Добавляет условные обозначения в диаграмму.</span><span class="sxs-lookup"><span data-stu-id="22094-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="22094-202">Добавляет ряд значений в диаграмму.</span><span class="sxs-lookup"><span data-stu-id="22094-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="22094-203">Возвращает хэш для указанных данных.</span><span class="sxs-lookup"><span data-stu-id="22094-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="22094-204">Алгоритмом по умолчанию является `sha256`.</span><span class="sxs-lookup"><span data-stu-id="22094-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="22094-205">Позволяет пользователям Facebook устанавливать подключение к страницам.</span><span class="sxs-lookup"><span data-stu-id="22094-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="22094-206">Готовит к просмотру пользовательский интерфейс для отправки файлов.</span><span class="sxs-lookup"><span data-stu-id="22094-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="22094-207">Отображает указанный тег Xbox для игр.</span><span class="sxs-lookup"><span data-stu-id="22094-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="22094-208">Подготавливает к просмотру образ граватаров для указанного адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="22094-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="22094-209">Преобразует объект данных в строку в формате нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="22094-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="22094-210">Преобразует входную строку в кодировке JSON в объект данных, который можно перебирать или вставить в базу данных.</span><span class="sxs-lookup"><span data-stu-id="22094-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="22094-211">Отображает ссылки социальных сетей, используя указанные заголовок и дополнительный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="22094-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="22094-212">Связывает сообщение об ошибке с полем формы.</span><span class="sxs-lookup"><span data-stu-id="22094-212">Associates an error message with a form field.</span></span> <span data-ttu-id="22094-213">Для доступа к этому элементу используйте вспомогательный метод `ModelState`.</span><span class="sxs-lookup"><span data-stu-id="22094-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="22094-214">Связывает сообщение об ошибке с формой.</span><span class="sxs-lookup"><span data-stu-id="22094-214">Associates an error message with a form.</span></span> <span data-ttu-id="22094-215">Для доступа к этому элементу используйте вспомогательный метод `ModelState`.</span><span class="sxs-lookup"><span data-stu-id="22094-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="22094-216">Возвращает значение true, если нет ошибок проверки.</span><span class="sxs-lookup"><span data-stu-id="22094-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="22094-217">Для доступа к этому элементу используйте вспомогательный метод `ModelState`.</span><span class="sxs-lookup"><span data-stu-id="22094-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="22094-218">Отображает свойства и значения объекта и всех его дочерних объектов.</span><span class="sxs-lookup"><span data-stu-id="22094-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="22094-219">Отрисовывает тест проверки reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="22094-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="22094-220">Задает открытый и закрытый ключи для службы reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="22094-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="22094-221">Обычно эти свойства задаются на странице *\_AppStart* .</span><span class="sxs-lookup"><span data-stu-id="22094-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="22094-222">Возвращает результат теста reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="22094-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="22094-223">Отображает сведения о состоянии веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="22094-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="22094-224">Выполняет визуализацию потока Twitter для указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="22094-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="22094-225">Визуализирует поток Twitter для указанного искомого текста.</span><span class="sxs-lookup"><span data-stu-id="22094-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="22094-226">Отрисовывает видеопроигрыватель Flash для указанного файла с необязательной шириной и высотой.</span><span class="sxs-lookup"><span data-stu-id="22094-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="22094-227">Отображает проигрыватель Windows Media для указанного файла с необязательной шириной и высотой.</span><span class="sxs-lookup"><span data-stu-id="22094-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="22094-228">Отображает проигрыватель Silverlight для указанного *XAP* -файла с требуемой шириной и высотой.</span><span class="sxs-lookup"><span data-stu-id="22094-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="22094-229">Возвращает объект, указанный *ключом*, или значение null, если объект не найден.</span><span class="sxs-lookup"><span data-stu-id="22094-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="22094-230">Удаляет из кэша объект, указанный *ключом* .</span><span class="sxs-lookup"><span data-stu-id="22094-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="22094-231">Помещает *значение* в кэш по имени, указанному в параметре *Key*.</span><span class="sxs-lookup"><span data-stu-id="22094-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="22094-232">Создает новый объект `WebGrid`, используя данные из запроса.</span><span class="sxs-lookup"><span data-stu-id="22094-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="22094-233">Отображает разметку для отображения данных в HTML-таблице.</span><span class="sxs-lookup"><span data-stu-id="22094-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="22094-234">Визуализирует пейджер для объекта `WebGrid`.</span><span class="sxs-lookup"><span data-stu-id="22094-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="22094-235">Загружает изображение по указанному пути.</span><span class="sxs-lookup"><span data-stu-id="22094-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="22094-236">Добавляет указанный образ в качестве водяного знака.</span><span class="sxs-lookup"><span data-stu-id="22094-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="22094-237">Добавляет указанный текст к изображению.</span><span class="sxs-lookup"><span data-stu-id="22094-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="22094-238">Переворачивает изображение по горизонтали или по вертикали.</span><span class="sxs-lookup"><span data-stu-id="22094-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="22094-239">Загружает изображение при публикации изображения на странице во время передачи файла.</span><span class="sxs-lookup"><span data-stu-id="22094-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="22094-240">Изменяет размер изображения.</span><span class="sxs-lookup"><span data-stu-id="22094-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="22094-241">Поворачивает изображение влево или вправо.</span><span class="sxs-lookup"><span data-stu-id="22094-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="22094-242">Сохраняет изображение по указанному пути.</span><span class="sxs-lookup"><span data-stu-id="22094-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="22094-243">Задает пароль для SMTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="22094-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="22094-244">Обычно это свойство задается на странице *\_AppStart* .</span><span class="sxs-lookup"><span data-stu-id="22094-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="22094-245">Отправляет электронное сообщение.</span><span class="sxs-lookup"><span data-stu-id="22094-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="22094-246">Задает имя SMTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="22094-246">Sets the SMTP server name.</span></span> <span data-ttu-id="22094-247">Обычно это свойство задается на странице *\_AppStart* .</span><span class="sxs-lookup"><span data-stu-id="22094-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="22094-248">Задает имя пользователя для SMTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="22094-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="22094-249">Обычно это свойство должно быть задано на странице *\_AppStart* .</span><span class="sxs-lookup"><span data-stu-id="22094-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="22094-250">Проверка</span><span class="sxs-lookup"><span data-stu-id="22094-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="22094-251">шаблон Отображает сообщение об ошибке проверки для указанного поля.</span><span class="sxs-lookup"><span data-stu-id="22094-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="22094-252">шаблон Отображает список всех ошибок проверки.</span><span class="sxs-lookup"><span data-stu-id="22094-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="22094-253">шаблон Регистрирует элемент пользовательского ввода для указанного типа проверки.</span><span class="sxs-lookup"><span data-stu-id="22094-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="22094-254">шаблон Динамически отображает атрибуты класса CSS для проверки на стороне клиента, чтобы можно было отформатировать сообщения об ошибках проверки.</span><span class="sxs-lookup"><span data-stu-id="22094-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="22094-255">(Необходимо сослаться на соответствующие библиотеки клиентских скриптов и определить классы CSS.)</span><span class="sxs-lookup"><span data-stu-id="22094-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="22094-256">шаблон Включает проверку на стороне клиента для поля ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="22094-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="22094-257">(Требуется ссылка на соответствующие библиотеки клиентских скриптов.)</span><span class="sxs-lookup"><span data-stu-id="22094-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="22094-258">шаблон Возвращает значение true, если все пользовательские элементы ввода, регистред для проверки, содержат допустимые значения.</span><span class="sxs-lookup"><span data-stu-id="22094-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="22094-259">шаблон Указывает, что пользователи должны предоставить значение для элемента ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="22094-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="22094-260">шаблон Указывает, что пользователи должны предоставлять значения для каждого элемента пользовательского ввода.</span><span class="sxs-lookup"><span data-stu-id="22094-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="22094-261">Этот метод не позволяет указать пользовательское сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="22094-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="22094-262">шаблон Указывает проверочный тест при использовании метода `Validation.Add`.</span><span class="sxs-lookup"><span data-stu-id="22094-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
