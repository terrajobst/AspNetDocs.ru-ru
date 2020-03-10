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
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>Краткий справочник по API веб-страницы ASP.NET (Razor)

от [Tom фитзмаккен](https://github.com/tfitzmac)

> На этой странице содержится список с краткими примерами наиболее часто используемых объектов, свойств и методов программирования веб-страницы ASP.NET с синтаксис Razor.
> 
> Описания, помеченные как "(v2)", появились в веб-страницы ASP.NET версии 2.
> 
> Справочную документацию по API см. в [справочной документации по веб-страницы ASP.NET](https://go.microsoft.com/fwlink/?LinkId=208659) на сайте MSDN.
> 
> ## <a name="software-versions"></a>Версии программного обеспечения
> 
> 
> - Веб-страницы ASP.NET (Razor) 3
>   
> 
> Этот учебник также работает с веб-страницы ASP.NET 2 и веб-страницы ASP.NET 1,0 (за исключением функций, помеченных как v2).

На этой странице содержатся справочные сведения по следующим параметрам.

- [Классы](#Classes)
- [Data](#Data)
- [Вспомогательные функции](#Helpers)
- [Проверка](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>Классы

### `AppState[key], AppState[index],App`

Содержит данные, которые могут совместно использоваться любыми страницами в приложении. Для доступа к тем же данным можно использовать динамическое свойство `App`, как показано в следующем примере:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

Преобразует строковое значение в логическое значение (true/false). Возвращает false или указанное значение, если строка не представляет значение true/false.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

Преобразует строковое значение в дату и время. Возвращает `DateTime.MinValue` или указанное значение, если строка не представляет дату и время.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

Преобразует строковое значение в десятичное значение. Возвращает 0,0 или указанное значение, если строка не представляет десятичное значение.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

Преобразует строковое значение в число с плавающей запятой. Возвращает 0,0 или указанное значение, если строка не представляет десятичное значение.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

Преобразует строковое значение в целое число. Возвращает 0 или указанное значение, если строка не представляет целое число.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

Создает совместимый с браузером URL-адрес из локального пути к файлу с дополнительными дополнительными элементами пути.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

Отображает *значение* как HTML-разметку вместо отображения его в виде выходных данных в формате HTML.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

Возвращает значение true, если значение может быть преобразовано из строки в указанный тип.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

Возвращает значение true, если объект или переменная не имеет значения.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

Возвращает значение true, если запрос является ЗАПИСЬю. (Первоначальные запросы обычно являются GET.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

Задает путь к странице макета, применяемой к этой странице.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

Содержит данные, общие для страницы, страницы макета и частичные страницы в текущем запросе. Для доступа к тем же данным можно использовать динамическое свойство `Page`, как показано в следующем примере:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(Страницы макета) Подготавливает к просмотру содержимое страницы содержимого, не находящегося ни в одном из именованных разделов.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

Визуализирует страницу содержимого, используя указанный путь и дополнительные дополнительные данные. Можно получить значения дополнительных параметров из `PageData` по положению (например 1) или ключу (пример 2).

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(Страницы макета) Подготавливает к просмотру раздел содержимого, имеющий имя. Задайте для параметра *обязательно* значение false, чтобы сделать раздел необязательным.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

Возвращает или задает значение cookie HTTP.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

Возвращает файлы, которые были переданы в текущем запросе.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

Возвращает данные, которые были опубликованы в форме (строки). `Request[key]` проверяет коллекции `Request.Form` и `Request.QueryString`.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

Возвращает данные, указанные в строке запроса URL-адреса. `Request[key]` проверяет коллекции `Request.Form` и `Request.QueryString`.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Выборочно отключает проверку запросов для элемента Form, значения строки запроса, файла cookie или значения заголовка. Проверка запросов включена по умолчанию и запрещает пользователям публиковать разметку или другое потенциально опасное содержимое.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

Добавляет заголовок HTTP-сервера в ответ.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

Кэширует выходные данные страницы в течение заданного времени. При необходимости задайте для параметра *скользящий* значение время ожидания на каждом доступе к странице и *варибипарамс* для кэширования различных версий страницы для каждой строки запроса в запросе страницы.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

Перенаправляет запрос браузера в новое расположение.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

Задает код состояния HTTP, отправляемый браузеру.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

Записывает содержимое *данных* в ответ с необязательным типом MIME.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

Записывает содержимое файла в ответ.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(Страницы макета) Определяет раздел содержимого с именем.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

Декодирует строку, которая является HTML-кодировкой.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

Кодирует строку для отрисовки в разметке HTML.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

Возвращает физический путь к серверу для указанного виртуального пути.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

Декодирует текст из URL-адреса.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

Кодирует текст для размещения в URL-адресе.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

Возвращает или задает значение, которое существует до тех пор, пока пользователь не закроет браузер.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

Отображает строковое представление значения объекта.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

Получает дополнительные данные из URL-адреса (например, */мипаже/екстрадата*).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

Изменяет пароль заданного пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

Подтверждает учетную запись с помощью токена подтверждения учетной записи.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

Создает новую учетную запись пользователя с указанными именем пользователя и паролем. Чтобы запросить маркер подтверждения, передайте значение true для *рекуиреконфирматионтокен.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

Возвращает целочисленный идентификатор текущего вошедшего в систему пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

Возвращает имя пользователя, выполнившего вход в систему.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

Создает маркер сброса пароля, который может быть отправлен пользователю по электронной почте, чтобы пользователь мог сбросить пароль.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

Возвращает идентификатор пользователя из имени пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

Возвращает значение true, если текущий пользователь вошел в систему.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

Возвращает значение true, если пользователь подтвердил (например, с помощью сообщения электронной почты с подтверждением).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

Возвращает значение true, если имя текущего пользователя совпадает с указанным именем пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Регистрирует пользователя в, настроив маркер проверки подлинности в файле cookie.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

Записывает пользователя в журнал, удаляя файл cookie маркера проверки подлинности.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

Если пользователь не прошел проверку подлинности, задает состояние HTTP 401 (Не санкционировано).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

Если текущий пользователь не является членом одной из указанных ролей, устанавливает для состояния HTTP значение 401 (не санкционировано).

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

Если текущий пользователь не является пользователем, указанным в поле *username*, устанавливает для состояния HTTP значение 401 (не санкционировано).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

Если маркер сброса пароля действителен, изменяет пароль пользователя на новый пароль.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Данные

### `Database.Execute(SQLstatement [,parameters]`

Выполняет *SQLstatement* (с необязательными параметрами), например операции вставки, удаления или обновления, и возвращает количество затронутых записей.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

Возвращает столбец идентификаторов из последней вставленной строки.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

Открывает указанный файл базы данных или базу данных, заданную с помощью именованной строки соединения из файла *Web. config* .

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

Открывает базу данных, используя строку подключения. (Это отличается от `Database.Open`, в которой используется имя строки подключения.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

Запрашивает базу данных с помощью *SQLstatement* (при необходимости передавая параметры) и возвращает результаты в виде коллекции.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

Выполняет *SQLstatement* (с необязательными параметрами) и возвращает одну запись.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

Выполняет *SQLstatement* (с необязательными параметрами) и возвращает одно значение.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>Вспомогательные методы

### `Analytics.GetGoogleHtml(webPropertyId)`

Подготавливает к просмотру код JavaScript Google Analytics для указанного идентификатора.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

Визуализирует код JavaScript Статкаунтер Analytics для указанного проекта.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

Отображает код JavaScript для анализа Yahoo для указанной учетной записи.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Передает Поиск в Bing. Чтобы указать сайт для поиска и заголовок поля поиска, можно задать свойства `Bing.SiteUrl` и `Bing.SiteTitle`. Обычно эти свойства задаются на странице *\_AppStart* .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

Инициализирует диаграмму.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

Добавляет условные обозначения в диаграмму.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

Добавляет ряд значений в диаграмму.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

Возвращает хэш для указанных данных. Алгоритмом по умолчанию является `sha256`.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Позволяет пользователям Facebook устанавливать подключение к страницам.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

Готовит к просмотру пользовательский интерфейс для отправки файлов.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

Отображает указанный тег Xbox для игр.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

Подготавливает к просмотру образ граватаров для указанного адреса электронной почты.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

Преобразует объект данных в строку в формате нотация объектов JavaScript (JSON).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

Преобразует входную строку в кодировке JSON в объект данных, который можно перебирать или вставить в базу данных.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

Отображает ссылки социальных сетей, используя указанные заголовок и дополнительный URL-адрес.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

Связывает сообщение об ошибке с полем формы. Для доступа к этому элементу используйте вспомогательный метод `ModelState`.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

Связывает сообщение об ошибке с формой. Для доступа к этому элементу используйте вспомогательный метод `ModelState`.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

Возвращает значение true, если нет ошибок проверки. Для доступа к этому элементу используйте вспомогательный метод `ModelState`.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

Отображает свойства и значения объекта и всех его дочерних объектов.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

Отрисовывает тест проверки reCAPTCHA.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

Задает открытый и закрытый ключи для службы reCAPTCHA. Обычно эти свойства задаются на странице *\_AppStart* .

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

Возвращает результат теста reCAPTCHA.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

Отображает сведения о состоянии веб-страницы ASP.NET.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

Выполняет визуализацию потока Twitter для указанного пользователя.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

Визуализирует поток Twitter для указанного искомого текста.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

Отрисовывает видеопроигрыватель Flash для указанного файла с необязательной шириной и высотой.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

Отображает проигрыватель Windows Media для указанного файла с необязательной шириной и высотой.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

Отображает проигрыватель Silverlight для указанного *XAP* -файла с требуемой шириной и высотой.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

Возвращает объект, указанный *ключом*, или значение null, если объект не найден.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

Удаляет из кэша объект, указанный *ключом* .

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

Помещает *значение* в кэш по имени, указанному в параметре *Key*.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

Создает новый объект `WebGrid`, используя данные из запроса.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

Отображает разметку для отображения данных в HTML-таблице.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

Визуализирует пейджер для объекта `WebGrid`.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

Загружает изображение по указанному пути.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

Добавляет указанный образ в качестве водяного знака.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

Добавляет указанный текст к изображению.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

Переворачивает изображение по горизонтали или по вертикали.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

Загружает изображение при публикации изображения на странице во время передачи файла.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

Изменяет размер изображения.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

Поворачивает изображение влево или вправо.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

Сохраняет изображение по указанному пути.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

Задает пароль для SMTP-сервера. Обычно это свойство задается на странице *\_AppStart* .

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

Отправляет электронное сообщение.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

Задает имя SMTP-сервера. Обычно это свойство задается на странице *\_AppStart* .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

Задает имя пользователя для SMTP-сервера. Обычно это свойство должно быть задано на странице *\_AppStart* .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>Проверка

### `Html.ValidationMessage(field)`

шаблон Отображает сообщение об ошибке проверки для указанного поля.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

шаблон Отображает список всех ошибок проверки.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

шаблон Регистрирует элемент пользовательского ввода для указанного типа проверки.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

шаблон Динамически отображает атрибуты класса CSS для проверки на стороне клиента, чтобы можно было отформатировать сообщения об ошибках проверки. (Необходимо сослаться на соответствующие библиотеки клиентских скриптов и определить классы CSS.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

шаблон Включает проверку на стороне клиента для поля ввода пользователя. (Требуется ссылка на соответствующие библиотеки клиентских скриптов.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

шаблон Возвращает значение true, если все пользовательские элементы ввода, регистред для проверки, содержат допустимые значения.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

шаблон Указывает, что пользователи должны предоставить значение для элемента ввода пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

шаблон Указывает, что пользователи должны предоставлять значения для каждого элемента пользовательского ввода. Этот метод не позволяет указать пользовательское сообщение об ошибке.

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

шаблон Указывает проверочный тест при использовании метода `Validation.Add`.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
