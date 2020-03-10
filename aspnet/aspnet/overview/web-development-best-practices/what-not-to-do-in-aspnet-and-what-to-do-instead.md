---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: Что не нужно делать в ASP.NET и что делать вместо этого | Документация Майкрософт
author: Rick-Anderson
description: В этом разделе описаны некоторые распространенные ошибки, вносимые пользователями в веб-проекты ASP.NET. В нем приводятся рекомендации по предотвращению этих Коммо...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500136"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="581c8-104">Запрещенные и разрешенные действия в ASP.NET</span><span class="sxs-lookup"><span data-stu-id="581c8-104">What not to do in ASP.NET, and what to do instead</span></span>

> <span data-ttu-id="581c8-105">В этом разделе описаны некоторые распространенные ошибки, вносимые пользователями в веб-проекты ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="581c8-105">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="581c8-106">Он предоставляет рекомендации по предотвращению этих распространенных ошибок.</span><span class="sxs-lookup"><span data-stu-id="581c8-106">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="581c8-107">Он основан на [презентации](http://vimeo.com/68390507) , **Дэмиен Edwards** на веб-сайте, посвященном норвежским разработчикам.</span><span class="sxs-lookup"><span data-stu-id="581c8-107">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="581c8-108">Отказ от ответственности</span><span class="sxs-lookup"><span data-stu-id="581c8-108">Disclaimer</span></span>

<span data-ttu-id="581c8-109">Этот раздел не является полным руководством по обеспечению безопасности и эффективности приложения.</span><span class="sxs-lookup"><span data-stu-id="581c8-109">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="581c8-110">Вам по-прежнему необходимо следовать рекомендациям по безопасности и производительности, которые не описаны в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="581c8-110">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="581c8-111">Он только предлагает, как избежать распространенных ошибок, связанных с классами и процессами .NET.</span><span class="sxs-lookup"><span data-stu-id="581c8-111">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="581c8-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="581c8-112">Overview</span></span>

<span data-ttu-id="581c8-113">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="581c8-113">This topic contains the following sections:</span></span>

- [<span data-ttu-id="581c8-114">Соответствие стандартам</span><span class="sxs-lookup"><span data-stu-id="581c8-114">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="581c8-115">Адаптеры элементов управления</span><span class="sxs-lookup"><span data-stu-id="581c8-115">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="581c8-116">Свойства стиля в элементах управления</span><span class="sxs-lookup"><span data-stu-id="581c8-116">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="581c8-117">Обратные вызовы страниц и элементов управления</span><span class="sxs-lookup"><span data-stu-id="581c8-117">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="581c8-118">Обнаружение возможностей браузера</span><span class="sxs-lookup"><span data-stu-id="581c8-118">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="581c8-119">Безопасность</span><span class="sxs-lookup"><span data-stu-id="581c8-119">Security</span></span>](#security)

    - [<span data-ttu-id="581c8-120">Проверка запроса</span><span class="sxs-lookup"><span data-stu-id="581c8-120">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="581c8-121">Проверка подлинности и сеанс с помощью форм без файлов cookie</span><span class="sxs-lookup"><span data-stu-id="581c8-121">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="581c8-122">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="581c8-122">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="581c8-123">Средний уровень доверия</span><span class="sxs-lookup"><span data-stu-id="581c8-123">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="581c8-124">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="581c8-124">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="581c8-125">урлпасенкоде</span><span class="sxs-lookup"><span data-stu-id="581c8-125">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="581c8-126">Надежность и производительность</span><span class="sxs-lookup"><span data-stu-id="581c8-126">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="581c8-127">Пресендрекуессеадерс и PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="581c8-127">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="581c8-128">Асинхронные события страниц с веб-формами</span><span class="sxs-lookup"><span data-stu-id="581c8-128">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="581c8-129">Пожарные и забытые работы</span><span class="sxs-lookup"><span data-stu-id="581c8-129">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="581c8-130">Тело запроса объекта</span><span class="sxs-lookup"><span data-stu-id="581c8-130">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="581c8-131">Response. Redirect и Response. end</span><span class="sxs-lookup"><span data-stu-id="581c8-131">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="581c8-132">EnableViewState и Виевстатемоде</span><span class="sxs-lookup"><span data-stu-id="581c8-132">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="581c8-133">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="581c8-133">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="581c8-134">Долго выполняющиеся запросы (> 110 секунд)</span><span class="sxs-lookup"><span data-stu-id="581c8-134">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="581c8-135">Соответствие стандартам</span><span class="sxs-lookup"><span data-stu-id="581c8-135">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="581c8-136">Адаптеры элементов управления</span><span class="sxs-lookup"><span data-stu-id="581c8-136">Control adapters</span></span>

<span data-ttu-id="581c8-137">Рекомендация: отключите использование адаптеров элементов управления для адаптивной отрисовки, а вместо этого используйте запросы к мультимедиа CSS и соответствующий стандартам HTML.</span><span class="sxs-lookup"><span data-stu-id="581c8-137">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="581c8-138">Адаптеры элементов управления появились в .NET 2,0 для отрисовки кода представления, настроенного для различных устройств и сред.</span><span class="sxs-lookup"><span data-stu-id="581c8-138">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="581c8-139">Теперь эту адаптивную визуализацию можно выполнить с помощью CSS и HTML.</span><span class="sxs-lookup"><span data-stu-id="581c8-139">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="581c8-140">Следует прерывать использование адаптеров элементов управления и преобразовывать существующие адаптеры в CSS и HTML.</span><span class="sxs-lookup"><span data-stu-id="581c8-140">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="581c8-141">Дополнительные сведения см. в статьях [запросы носителей](http://www.w3.org/TR/css3-mediaqueries/) и [инструкции: Добавление мобильных страниц в приложение ASP.NET Web Forms/MVC](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="581c8-141">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="581c8-142">Свойства стиля в элементах управления</span><span class="sxs-lookup"><span data-stu-id="581c8-142">Style properties on controls</span></span>

<span data-ttu-id="581c8-143">Рекомендация: прерывать настройку значений стиля в разметке элемента управления, а также задавать значения форматирования в таблицах стилей CSS.</span><span class="sxs-lookup"><span data-stu-id="581c8-143">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="581c8-144">Серверные веб-элементы управления содержат десятки свойств, которые можно использовать для задания свойств встроенного стиля.</span><span class="sxs-lookup"><span data-stu-id="581c8-144">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="581c8-145">Например, свойство ForeColor задает цвет текста для элемента управления.</span><span class="sxs-lookup"><span data-stu-id="581c8-145">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="581c8-146">Этот же результат можно более эффективно реализовать с помощью таблиц стилей CSS.</span><span class="sxs-lookup"><span data-stu-id="581c8-146">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="581c8-147">Таблицы стилей позволяют централизовать значения стилей и не задавать эти значения во всем приложении.</span><span class="sxs-lookup"><span data-stu-id="581c8-147">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="581c8-148">В следующем примере показан класс CSS, который устанавливает для текста красный цвет.</span><span class="sxs-lookup"><span data-stu-id="581c8-148">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="581c8-149">В следующем примере показано, как динамически применить класс CSS.</span><span class="sxs-lookup"><span data-stu-id="581c8-149">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="581c8-150">Обратные вызовы страниц и элементов управления</span><span class="sxs-lookup"><span data-stu-id="581c8-150">Page and control callbacks</span></span>

<span data-ttu-id="581c8-151">Рекомендация: прерывать использование обратных вызовов страниц и элементов управления, а вместо этого использовать следующие элементы: AJAX, UpdatePanel, методы действий MVC, веб-API или SignalR.</span><span class="sxs-lookup"><span data-stu-id="581c8-151">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="581c8-152">В предыдущих версиях ASP.NET методы обратного вызова страницы и управления позволили вам обновить часть веб-страницы без обновления всей страницы.</span><span class="sxs-lookup"><span data-stu-id="581c8-152">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="581c8-153">Теперь можно выполнять частичные обновления страниц с помощью [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [веб-API](../../../web-api/index.md) или [SignalR](../../../signalr/index.md).</span><span class="sxs-lookup"><span data-stu-id="581c8-153">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="581c8-154">Следует перестать использовать методы обратного вызова, так как они могут вызвать проблемы с понятными URL-адресами и маршрутизацией.</span><span class="sxs-lookup"><span data-stu-id="581c8-154">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="581c8-155">По умолчанию элементы управления не поддерживают методы обратного вызова, но если эта функция включена в элементе управления, ее следует отключить.</span><span class="sxs-lookup"><span data-stu-id="581c8-155">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="581c8-156">Обнаружение возможностей браузера</span><span class="sxs-lookup"><span data-stu-id="581c8-156">Browser capability detection</span></span>

<span data-ttu-id="581c8-157">Рекомендация: завершите использование статического обнаружения возможностей браузера, а вместо этого используйте обнаружение динамических компонентов.</span><span class="sxs-lookup"><span data-stu-id="581c8-157">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="581c8-158">В более ранних версиях ASP.NET поддерживаемые функции для каждого браузера хранились в XML-файле.</span><span class="sxs-lookup"><span data-stu-id="581c8-158">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="581c8-159">Поиск поддержки функций посредством статического поиска не является лучшим подходом.</span><span class="sxs-lookup"><span data-stu-id="581c8-159">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="581c8-160">Теперь можно динамически обнаруживать поддерживаемые в браузере функции с помощью платформы обнаружения компонентов, например [Modernizr](http://modernizr.com/).</span><span class="sxs-lookup"><span data-stu-id="581c8-160">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="581c8-161">Обнаружение компонентов определяет поддержку, пытаясь использовать метод или свойство, а затем проверить, был ли браузер выдал желаемый результат.</span><span class="sxs-lookup"><span data-stu-id="581c8-161">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="581c8-162">По умолчанию Modernizr включается в шаблоны веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="581c8-162">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="581c8-163">безопасность</span><span class="sxs-lookup"><span data-stu-id="581c8-163">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="581c8-164">Проверка запросов</span><span class="sxs-lookup"><span data-stu-id="581c8-164">Request validation</span></span>

<span data-ttu-id="581c8-165">Рекомендация: проверка вводимых пользователем данных и кодирование выходных данных от пользователей.</span><span class="sxs-lookup"><span data-stu-id="581c8-165">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="581c8-166">Проверка запросов — это функция ASP.NET, которая проверяет каждый запрос и останавливает запрос, если обнаружена воспринимаемая угроза.</span><span class="sxs-lookup"><span data-stu-id="581c8-166">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="581c8-167">Не зависят от проверки запроса для защиты приложения от атак с использованием межсайтовых сценариев.</span><span class="sxs-lookup"><span data-stu-id="581c8-167">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="581c8-168">Вместо этого следует проверить все входные данные пользователей и закодировать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="581c8-168">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="581c8-169">В некоторых ограниченных случаях можно использовать регулярные выражения для проверки входных данных, но в более сложных случаях следует проверять вводимые пользователем данные с помощью классов .NET, которые определяют, соответствуют ли значения допустимым значениям.</span><span class="sxs-lookup"><span data-stu-id="581c8-169">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="581c8-170">В следующем примере показано, как использовать статический метод в классе URI, чтобы определить, является ли допустимым URI, предоставленный пользователем.</span><span class="sxs-lookup"><span data-stu-id="581c8-170">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="581c8-171">Тем не менее, чтобы достаточно проверить универсальный код ресурса (URI), необходимо также убедиться, что он указывает `http` или `https`.</span><span class="sxs-lookup"><span data-stu-id="581c8-171">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="581c8-172">В следующем примере методы экземпляра используются для проверки допустимости URI.</span><span class="sxs-lookup"><span data-stu-id="581c8-172">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="581c8-173">Перед отображением вводимых пользователем данных в формате HTML или ввода данных пользователем в SQL-запросе необходимо закодировать значения, чтобы убедиться в том, что вредоносный код не включен.</span><span class="sxs-lookup"><span data-stu-id="581c8-173">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="581c8-174">Можно кодировать значение HTML в разметке с помощью синтаксиса &lt;%:%&gt;, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="581c8-174">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="581c8-175">Или в синтаксис Razor можно выполнить кодирование в формате HTML с помощью @, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="581c8-175">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="581c8-176">В следующем примере показано, как кодировать значение HTML в коде программной части.</span><span class="sxs-lookup"><span data-stu-id="581c8-176">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="581c8-177">Чтобы безопасно закодировать значение для команд SQL, используйте параметры командной строки, такие как [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span><span class="sxs-lookup"><span data-stu-id="581c8-177">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="581c8-178">Проверка подлинности и сеанс с помощью форм без файлов cookie</span><span class="sxs-lookup"><span data-stu-id="581c8-178">Cookieless forms authentication and session</span></span>

<span data-ttu-id="581c8-179">Рекомендация: требуются файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="581c8-179">Recommendation: Require cookies.</span></span>

<span data-ttu-id="581c8-180">Передача сведений о проверке подлинности в строку запроса не является безопасной.</span><span class="sxs-lookup"><span data-stu-id="581c8-180">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="581c8-181">Таким образом, если приложение включает проверку подлинности, требуются файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="581c8-181">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="581c8-182">Если файл cookie хранит конфиденциальные данные, рассмотрите возможность обязательного использования SSL для файла cookie.</span><span class="sxs-lookup"><span data-stu-id="581c8-182">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="581c8-183">В следующем примере показано, как указать в файле Web. config, что для проверки подлинности форм требуется файл cookie, передаваемый по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="581c8-183">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="581c8-184">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="581c8-184">EnableViewStateMac</span></span>

<span data-ttu-id="581c8-185">Рекомендация: не устанавливайте значение false.</span><span class="sxs-lookup"><span data-stu-id="581c8-185">Recommendation: Never set to false.</span></span>

<span data-ttu-id="581c8-186">По умолчанию EnableViewStateMac имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="581c8-186">By default, EnableViewStateMac is set to true.</span></span> <span data-ttu-id="581c8-187">Даже если приложение не использует состояние просмотра, не устанавливайте для EnableViewStateMac значение false.</span><span class="sxs-lookup"><span data-stu-id="581c8-187">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="581c8-188">Установка этого параметра в значение false сделает приложение уязвимым для межсайтовых сценариев.</span><span class="sxs-lookup"><span data-stu-id="581c8-188">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="581c8-189">Начиная с ASP.NET 4.5.2 среда выполнения применяет **EnableViewStateMac = true**.</span><span class="sxs-lookup"><span data-stu-id="581c8-189">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="581c8-190">Даже если задано значение false, среда выполнения игнорирует это значение и переходит к значению true.</span><span class="sxs-lookup"><span data-stu-id="581c8-190">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="581c8-191">Дополнительные сведения см. в разделе [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span><span class="sxs-lookup"><span data-stu-id="581c8-191">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="581c8-192">В следующем примере показано, как установить для EnableViewStateMac значение true.</span><span class="sxs-lookup"><span data-stu-id="581c8-192">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="581c8-193">Нет необходимости присвоить этому параметру значение true, так как по умолчанию имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="581c8-193">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="581c8-194">Тем не менее, если на любой странице приложения задано значение false, необходимо немедленно исправить это значение.</span><span class="sxs-lookup"><span data-stu-id="581c8-194">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="581c8-195">Средний уровень доверия</span><span class="sxs-lookup"><span data-stu-id="581c8-195">Medium trust</span></span>

<span data-ttu-id="581c8-196">Рекомендация: не зависят от среднего уровня доверия (или любого другого) в качестве границы безопасности.</span><span class="sxs-lookup"><span data-stu-id="581c8-196">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="581c8-197">Частичное доверие не защищает приложение надлежащим образом и не должно использоваться.</span><span class="sxs-lookup"><span data-stu-id="581c8-197">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="581c8-198">Вместо этого используйте полное доверие и изолируйте недоверенные приложения в отдельных пулах приложений.</span><span class="sxs-lookup"><span data-stu-id="581c8-198">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="581c8-199">Кроме того, запустите каждый пул приложений с уникальным удостоверением.</span><span class="sxs-lookup"><span data-stu-id="581c8-199">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="581c8-200">Дополнительные сведения см. в разделе [ASP.NET частичное доверие не гарантирует изоляцию приложений](https://support.microsoft.com/kb/2698981).</span><span class="sxs-lookup"><span data-stu-id="581c8-200">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="581c8-201">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="581c8-201">&lt;appSettings&gt;</span></span>

<span data-ttu-id="581c8-202">Рекомендация: не отключайте параметры безопасности в элементе &lt;appSettings&gt;.</span><span class="sxs-lookup"><span data-stu-id="581c8-202">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="581c8-203">Элемент appSettings содержит множество значений, необходимых для обновлений безопасности.</span><span class="sxs-lookup"><span data-stu-id="581c8-203">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="581c8-204">Не следует изменять или отключать эти значения.</span><span class="sxs-lookup"><span data-stu-id="581c8-204">You should not change or disable these values.</span></span> <span data-ttu-id="581c8-205">Если необходимо отключить эти значения при развертывании обновления, сразу снова включите его после завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="581c8-205">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="581c8-206">Дополнительные сведения см. в разделе [ASP.NET appSettings element](https://msdn.microsoft.com/library/hh975440.aspx).</span><span class="sxs-lookup"><span data-stu-id="581c8-206">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="581c8-207">урлпасенкоде</span><span class="sxs-lookup"><span data-stu-id="581c8-207">UrlPathEncode</span></span>

<span data-ttu-id="581c8-208">Рекомендация: вместо этого используйте [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) .</span><span class="sxs-lookup"><span data-stu-id="581c8-208">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="581c8-209">Метод Урлпасенкоде был добавлен в .NET Framework для разрешения очень специфической проблемы совместимости с браузером.</span><span class="sxs-lookup"><span data-stu-id="581c8-209">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="581c8-210">Он не кодирует URL-адрес надлежащим образом и не защищает приложение от межузловых сценариев.</span><span class="sxs-lookup"><span data-stu-id="581c8-210">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="581c8-211">Его никогда не следует использовать в приложении.</span><span class="sxs-lookup"><span data-stu-id="581c8-211">You should never use it in your application.</span></span> <span data-ttu-id="581c8-212">Вместо этого используйте [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span><span class="sxs-lookup"><span data-stu-id="581c8-212">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="581c8-213">В следующем примере показано, как передать закодированный URL-адрес как параметр строки запроса для элемента управления HyperLink.</span><span class="sxs-lookup"><span data-stu-id="581c8-213">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="581c8-214">Надежность и производительность</span><span class="sxs-lookup"><span data-stu-id="581c8-214">Reliability and performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="581c8-215">Пресендрекуессеадерс и PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="581c8-215">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="581c8-216">Рекомендация: не используйте эти события с управляемыми модулями.</span><span class="sxs-lookup"><span data-stu-id="581c8-216">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="581c8-217">Вместо этого напишите собственный модуль IIS для выполнения требуемой задачи.</span><span class="sxs-lookup"><span data-stu-id="581c8-217">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="581c8-218">См. раздел [Создание модулей HTTP с машинным кодом](https://msdn.microsoft.com/library/ms693629.aspx).</span><span class="sxs-lookup"><span data-stu-id="581c8-218">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="581c8-219">Вы можете использовать события [пресендрекуессеадерс](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) и [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) с собственными модулями IIS.</span><span class="sxs-lookup"><span data-stu-id="581c8-219">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="581c8-220">Не используйте `PreSendRequestHeaders` и `PreSendRequestContent` с управляемыми модулями, которые реализуют `IHttpModule`.</span><span class="sxs-lookup"><span data-stu-id="581c8-220">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="581c8-221">Установка этих свойств может вызвать проблемы с асинхронными запросами.</span><span class="sxs-lookup"><span data-stu-id="581c8-221">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="581c8-222">Сочетание запрошенного приложением маршрутизации (ARR) и WebSockets может привести к исключениям нарушения доступа, которые могут привести к сбою w3wp.</span><span class="sxs-lookup"><span data-stu-id="581c8-222">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="581c8-223">Например, иискоре! W3_CONTEXT_BASE:: Жетисластнотификатион + 68 в иискоре. dll вызвало исключение нарушения прав доступа (0xC0000005).</span><span class="sxs-lookup"><span data-stu-id="581c8-223">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="581c8-224">Асинхронные события страниц с веб-формами</span><span class="sxs-lookup"><span data-stu-id="581c8-224">Asynchronous page events with web forms</span></span>

<span data-ttu-id="581c8-225">Рекомендация: в веб-формах Избегайте написания асинхронных методов void для событий жизненного цикла страницы, а вместо этого используйте [Page. метод RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) для асинхронного кода.</span><span class="sxs-lookup"><span data-stu-id="581c8-225">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="581c8-226">При пометке события страницы с **модификатором Async** и **void**невозможно определить время завершения асинхронного кода.</span><span class="sxs-lookup"><span data-stu-id="581c8-226">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="581c8-227">Вместо этого используйте Page. метод RegisterAsyncTask для выполнения асинхронного кода способом, позволяющим отследить его завершение.</span><span class="sxs-lookup"><span data-stu-id="581c8-227">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="581c8-228">В следующем примере показан обработчик нажатия кнопки, который содержит асинхронный код.</span><span class="sxs-lookup"><span data-stu-id="581c8-228">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="581c8-229">Этот пример включает асинхронное чтение строкового значения, которое предоставляется только в качестве упрощенного примера асинхронной задачи, а не рекомендуемой практикой.</span><span class="sxs-lookup"><span data-stu-id="581c8-229">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="581c8-230">При использовании асинхронных задач задайте в качестве целевой платформы среды выполнения HTTP значение 4,5 (или более позднюю) в файле Web. config.</span><span class="sxs-lookup"><span data-stu-id="581c8-230">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 (or later) in the Web.config file.</span></span> <span data-ttu-id="581c8-231">При установке целевой платформы в значение 4,5 включается новый контекст синхронизации, добавленный в .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="581c8-231">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="581c8-232">Это значение по умолчанию задается в новых проектах Visual Studio, но не устанавливается при работе с существующим проектом.</span><span class="sxs-lookup"><span data-stu-id="581c8-232">This value is set by default in new projects in Visual Studio, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="581c8-233">Пожарные и забытые работы</span><span class="sxs-lookup"><span data-stu-id="581c8-233">Fire-and-forget work</span></span>

<span data-ttu-id="581c8-234">Рекомендация. при обработке запроса в ASP.NET старайтесь не запускать запуск пожарной и забытой работы (например, вызов метода ThreadPool. QueueUserWorkItem или создание таймера, который многократно вызывает делегат).</span><span class="sxs-lookup"><span data-stu-id="581c8-234">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="581c8-235">Если в приложении есть работа, которая работает в ASP.NET, приложение может не синхронизироваться. В любое время домен приложения можно уничтожить, что означает, что текущий процесс может больше не соответствовать текущему состоянию приложения.</span><span class="sxs-lookup"><span data-stu-id="581c8-235">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="581c8-236">Этот тип работы следует перемещать за пределы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="581c8-236">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="581c8-237">Вы можете использовать веб-задания, службу Windows или рабочую роль в Azure для выполнения текущей работы и запуска этого кода из другого процесса.</span><span class="sxs-lookup"><span data-stu-id="581c8-237">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="581c8-238">Если вам необходимо выполнить эту работу в ASP.NET, можно добавить пакет NuGet с именем " [фон](http://www.nuget.org/packages/webbackgrounder) " для запуска кода.</span><span class="sxs-lookup"><span data-stu-id="581c8-238">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="581c8-239">Тело запроса объекта</span><span class="sxs-lookup"><span data-stu-id="581c8-239">Request entity body</span></span>

<span data-ttu-id="581c8-240">Рекомендация: Избегайте чтения запроса. Form или Request. InputStream перед событием выполнения обработчика.</span><span class="sxs-lookup"><span data-stu-id="581c8-240">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="581c8-241">Самая ранняя из них должна быть считана из запроса. Form или Request. InputStream во время события Execute обработчика.</span><span class="sxs-lookup"><span data-stu-id="581c8-241">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="581c8-242">В MVC контроллер является обработчиком, а событие выполнения — при выполнении метода действия.</span><span class="sxs-lookup"><span data-stu-id="581c8-242">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="581c8-243">В веб-формах страница является обработчиком, а событие выполнения — при срабатывании события Page. init.</span><span class="sxs-lookup"><span data-stu-id="581c8-243">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="581c8-244">При чтении тела запроса, предшествующего событию Execute, вы повлияете на обработку запроса.</span><span class="sxs-lookup"><span data-stu-id="581c8-244">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="581c8-245">Если необходимо прочитать текст сущности запроса перед событием Execute, используйте [request. жетбуфферлессинпутстреам](https://msdn.microsoft.com/library/ff406798.aspx) или [request. GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span><span class="sxs-lookup"><span data-stu-id="581c8-245">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="581c8-246">При использовании Жетбуфферлессинпутстреам вы получаете необработанный поток из запроса и несете ответственность за обработку всего запроса.</span><span class="sxs-lookup"><span data-stu-id="581c8-246">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="581c8-247">После вызова Жетбуфферлессинпутстреам запросы. Form и Request. InputStream недоступны, так как они не заполнены ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="581c8-247">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="581c8-248">При использовании GetBufferedInputStream вы получаете копию потока из запроса.</span><span class="sxs-lookup"><span data-stu-id="581c8-248">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="581c8-249">Запрос. Form и Request. InputStream по-прежнему доступны позже в запросе, так как ASP.NET заполняет другую копию.</span><span class="sxs-lookup"><span data-stu-id="581c8-249">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="581c8-250">Response. Redirect и Response. end</span><span class="sxs-lookup"><span data-stu-id="581c8-250">Response.Redirect and Response.End</span></span>

<span data-ttu-id="581c8-251">Рекомендация: Обратите внимание на различия в обработке потока после вызова [Response. Redirect (строка)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span><span class="sxs-lookup"><span data-stu-id="581c8-251">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="581c8-252">Метод Response [. Redirect (строка)](https://msdn.microsoft.com/library/t9dwyts4.aspx) вызывает метод Response. end.</span><span class="sxs-lookup"><span data-stu-id="581c8-252">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="581c8-253">В синхронном процессе вызов запроса. Redirect приводит к немедленному прерыванию текущего потока.</span><span class="sxs-lookup"><span data-stu-id="581c8-253">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="581c8-254">Однако в асинхронном процессе вызов Response. Redirect не прерывает текущий поток, поэтому выполнение кода продолжится для запроса.</span><span class="sxs-lookup"><span data-stu-id="581c8-254">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="581c8-255">В асинхронном процессе необходимо вернуть задачу из метода, чтобы прерывать выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="581c8-255">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="581c8-256">В проекте MVC не следует вызывать ответ. Redirect.</span><span class="sxs-lookup"><span data-stu-id="581c8-256">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="581c8-257">Вместо этого следует возвращать Редиректресулт.</span><span class="sxs-lookup"><span data-stu-id="581c8-257">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="581c8-258">EnableViewState и Виевстатемоде</span><span class="sxs-lookup"><span data-stu-id="581c8-258">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="581c8-259">Рекомендация: используйте Виевстатемоде вместо EnableViewState, чтобы обеспечить детальный контроль над тем, какие элементы управления используют состояние представления.</span><span class="sxs-lookup"><span data-stu-id="581c8-259">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="581c8-260">При установке для EnableViewState значения false в директиве Page состояние представления отключается для всех элементов управления на странице и не может быть включено.</span><span class="sxs-lookup"><span data-stu-id="581c8-260">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="581c8-261">Если вы хотите включить состояние просмотра только для определенных элементов управления на странице, установите для параметра Виевстатемоде значение Disabled (отключено) для страницы.</span><span class="sxs-lookup"><span data-stu-id="581c8-261">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="581c8-262">Затем установите Виевстатемоде в значение Enabled только для элементов управления, которые действительно требуют состояния представления.</span><span class="sxs-lookup"><span data-stu-id="581c8-262">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="581c8-263">Включив состояние просмотра только для тех элементов управления, которые им нужны, можно уменьшить размер состояния представления для веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="581c8-263">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="581c8-264">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="581c8-264">SqlMembershipProvider</span></span>

<span data-ttu-id="581c8-265">Рекомендация: используйте универсальные поставщики.</span><span class="sxs-lookup"><span data-stu-id="581c8-265">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="581c8-266">В текущих шаблонах проектов SqlMembershipProvider был заменен [универсальные поставщики ASP.NET](http://www.nuget.org/packages/Microsoft.AspNet.Providers), который доступен в виде пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="581c8-266">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="581c8-267">При использовании SqlMembershipProvider в проекте, построенном с использованием более ранней версии шаблонов, следует переключиться на универсальные поставщики.</span><span class="sxs-lookup"><span data-stu-id="581c8-267">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="581c8-268">Универсальные поставщики работать со всеми базами данных, которые поддерживаются Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="581c8-268">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="581c8-269">Дополнительные сведения см. в разделе [Введение в универсальные поставщики ASP.NET](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span><span class="sxs-lookup"><span data-stu-id="581c8-269">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="581c8-270">Долго выполняющиеся запросы (> 110 секунд)</span><span class="sxs-lookup"><span data-stu-id="581c8-270">Long-running requests (>110 seconds)</span></span>

<span data-ttu-id="581c8-271">Рекомендация: используйте [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) или [SignalR](../../../signalr/index.md) для подключенных клиентов и используйте асинхронные операции ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="581c8-271">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="581c8-272">Длительные запросы могут привести к непредсказуемым результатам и снижению производительности веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="581c8-272">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="581c8-273">Значение времени ожидания по умолчанию для запроса составляет 110 секунд.</span><span class="sxs-lookup"><span data-stu-id="581c8-273">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="581c8-274">Если вы используете состояние сеанса с длительным запросом, ASP.NET снимает блокировку объекта сеанса через 110 секунд.</span><span class="sxs-lookup"><span data-stu-id="581c8-274">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="581c8-275">Однако приложение может находиться в процессе операции над объектом Session, когда блокировка снимается, и операция может завершиться неудачно.</span><span class="sxs-lookup"><span data-stu-id="581c8-275">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="581c8-276">Если второй запрос пользователя блокируется во время выполнения первого запроса, второй запрос может получить доступ к объекту сеанса в непротиворечивом состоянии.</span><span class="sxs-lookup"><span data-stu-id="581c8-276">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="581c8-277">Если приложение включает в себя блокирующие (или синхронные) операции ввода-вывода, приложение не будет отвечать.</span><span class="sxs-lookup"><span data-stu-id="581c8-277">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="581c8-278">Для повышения производительности используйте асинхронные операции ввода-вывода в .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="581c8-278">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="581c8-279">Кроме того, используйте WebSockets или SignalR для подключения клиентов к серверу.</span><span class="sxs-lookup"><span data-stu-id="581c8-279">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="581c8-280">Эти функции предназначены для эффективной обработки долго выполняющихся запросов.</span><span class="sxs-lookup"><span data-stu-id="581c8-280">These features are designed to efficiently handle long-running requests.</span></span>
