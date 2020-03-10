---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'Отправка данных HTML-формы в веб-API ASP.NET: Form-UrlEncoded Data-ASP.NET 4. x'
author: MikeWasson
description: В этой статье показано, как отправить данные Form-UrlEncoded в контроллер веб-API с помощью ASP.NET 4. x.
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449244"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="0728d-103">Отправка данных HTML-формы в веб-API ASP.NET: данные Form-UrlEncoded</span><span class="sxs-lookup"><span data-stu-id="0728d-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="0728d-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0728d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="0728d-105">Часть 1. форма-UrlEncoded данных</span><span class="sxs-lookup"><span data-stu-id="0728d-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="0728d-106">В этой статье показано, как опубликовать данные формы-UrlEncoded в контроллере веб-API.</span><span class="sxs-lookup"><span data-stu-id="0728d-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="0728d-107">Общие сведения о HTML-формах</span><span class="sxs-lookup"><span data-stu-id="0728d-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="0728d-108">Отправка сложных типов</span><span class="sxs-lookup"><span data-stu-id="0728d-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="0728d-109">Отправка данных формы через AJAX</span><span class="sxs-lookup"><span data-stu-id="0728d-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="0728d-110">Отправка простых типов</span><span class="sxs-lookup"><span data-stu-id="0728d-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="0728d-111">[Скачайте завершенный проект](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span><span class="sxs-lookup"><span data-stu-id="0728d-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="0728d-112">Общие сведения о HTML-формах</span><span class="sxs-lookup"><span data-stu-id="0728d-112">Overview of HTML Forms</span></span>

<span data-ttu-id="0728d-113">Для отправки данных на сервер в HTML-формах используется либо GET, либо POST.</span><span class="sxs-lookup"><span data-stu-id="0728d-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="0728d-114">Атрибут **method** элемента **Form** предоставляет метод HTTP:</span><span class="sxs-lookup"><span data-stu-id="0728d-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="0728d-115">Метод по умолчанию — GET.</span><span class="sxs-lookup"><span data-stu-id="0728d-115">The default method is GET.</span></span> <span data-ttu-id="0728d-116">Если форма использует GET, данные формы кодируются в универсальном коде ресурса (URI) в виде строки запроса.</span><span class="sxs-lookup"><span data-stu-id="0728d-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="0728d-117">Если форма использует POST, данные формы помещаются в текст запроса.</span><span class="sxs-lookup"><span data-stu-id="0728d-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="0728d-118">Для отправленных данных атрибут **енктипе** задает формат текста запроса:</span><span class="sxs-lookup"><span data-stu-id="0728d-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="0728d-119">енктипе</span><span class="sxs-lookup"><span data-stu-id="0728d-119">enctype</span></span> | <span data-ttu-id="0728d-120">Description</span><span class="sxs-lookup"><span data-stu-id="0728d-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0728d-121">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="0728d-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="0728d-122">Данные формы кодируются как пары "имя-значение", аналогично строке запроса URI.</span><span class="sxs-lookup"><span data-stu-id="0728d-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="0728d-123">Это формат по умолчанию для POST.</span><span class="sxs-lookup"><span data-stu-id="0728d-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="0728d-124">multipart/form-data</span><span class="sxs-lookup"><span data-stu-id="0728d-124">multipart/form-data</span></span> | <span data-ttu-id="0728d-125">Данные формы кодируются как составное сообщение MIME.</span><span class="sxs-lookup"><span data-stu-id="0728d-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="0728d-126">Используйте этот формат при отправке файла на сервер.</span><span class="sxs-lookup"><span data-stu-id="0728d-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="0728d-127">В первой части этой статьи рассматривается формат x-www-Form-UrlEncoded.</span><span class="sxs-lookup"><span data-stu-id="0728d-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="0728d-128">[Часть 2](sending-html-form-data-part-2.md) описывает составной MIME.</span><span class="sxs-lookup"><span data-stu-id="0728d-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="0728d-129">Отправка сложных типов</span><span class="sxs-lookup"><span data-stu-id="0728d-129">Sending Complex Types</span></span>

<span data-ttu-id="0728d-130">Как правило, будет отправлен сложный тип, состоящий из значений, взятых из нескольких элементов управления формы.</span><span class="sxs-lookup"><span data-stu-id="0728d-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="0728d-131">Рассмотрим следующую модель, представляющую обновление состояния:</span><span class="sxs-lookup"><span data-stu-id="0728d-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="0728d-132">Ниже приведен контроллер веб-API, принимающий объект `Update` через POST.</span><span class="sxs-lookup"><span data-stu-id="0728d-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="0728d-133">Этот контроллер использует [маршрутизацию на основе действий](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), поэтому шаблон маршрута &quot;API/{Controller}/{Action}/{id}&quot;.</span><span class="sxs-lookup"><span data-stu-id="0728d-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="0728d-134">Клиент будет отправлять данные в &quot;/АПИ/упдатес/комплекс&quot;.</span><span class="sxs-lookup"><span data-stu-id="0728d-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>

<span data-ttu-id="0728d-135">Теперь напишем HTML-форму, чтобы пользователи могли отправить обновление состояния.</span><span class="sxs-lookup"><span data-stu-id="0728d-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="0728d-136">Обратите внимание, что атрибут **Action** в форме является универсальным кодом ресурса (URI) действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="0728d-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="0728d-137">Ниже приведена форма с некоторыми значениями, введенными в:</span><span class="sxs-lookup"><span data-stu-id="0728d-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="0728d-138">Когда пользователь нажимает кнопку Отправить, браузер отправляет HTTP-запрос, аналогичный следующему:</span><span class="sxs-lookup"><span data-stu-id="0728d-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="0728d-139">Обратите внимание, что текст запроса содержит данные формы, отформатированные как пары "имя-значение".</span><span class="sxs-lookup"><span data-stu-id="0728d-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="0728d-140">Веб-API автоматически преобразует пары "имя-значение" в экземпляр класса `Update`.</span><span class="sxs-lookup"><span data-stu-id="0728d-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="0728d-141">Отправка данных формы через AJAX</span><span class="sxs-lookup"><span data-stu-id="0728d-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="0728d-142">Когда пользователь отправляет форму, браузер переходит от текущей страницы и отображает текст ответного сообщения.</span><span class="sxs-lookup"><span data-stu-id="0728d-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="0728d-143">Это нормально, когда ответ является HTML-страницей.</span><span class="sxs-lookup"><span data-stu-id="0728d-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="0728d-144">Однако в веб-API текст ответа обычно либо пуст, либо содержит структурированные данные, такие как JSON.</span><span class="sxs-lookup"><span data-stu-id="0728d-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="0728d-145">В этом случае имеет смысл отправить данные формы с помощью запроса AJAX, чтобы страница могла обработать ответ.</span><span class="sxs-lookup"><span data-stu-id="0728d-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="0728d-146">В следующем коде показано, как отправлять данные формы с помощью jQuery.</span><span class="sxs-lookup"><span data-stu-id="0728d-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="0728d-147">Функция **отправки** jQuery заменяет действие формы новой функцией.</span><span class="sxs-lookup"><span data-stu-id="0728d-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="0728d-148">Это переопределяет поведение по умолчанию кнопки Отправить.</span><span class="sxs-lookup"><span data-stu-id="0728d-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="0728d-149">Функция **Serialize** сериализует данные формы в пары "имя-значение".</span><span class="sxs-lookup"><span data-stu-id="0728d-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="0728d-150">Чтобы отправить данные формы на сервер, вызовите `$.post()`.</span><span class="sxs-lookup"><span data-stu-id="0728d-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="0728d-151">По завершении запроса обработчик `.success()` или `.error()` отображает соответствующее сообщение пользователю.</span><span class="sxs-lookup"><span data-stu-id="0728d-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="0728d-152">Отправка простых типов</span><span class="sxs-lookup"><span data-stu-id="0728d-152">Sending Simple Types</span></span>

<span data-ttu-id="0728d-153">В предыдущих разделах мы отправили сложный тип, который веб-API десериализует в экземпляр класса Model.</span><span class="sxs-lookup"><span data-stu-id="0728d-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="0728d-154">Можно также отправить простые типы, например строку.</span><span class="sxs-lookup"><span data-stu-id="0728d-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="0728d-155">Перед отправкой простого типа рекомендуется обернуть значение в сложный тип.</span><span class="sxs-lookup"><span data-stu-id="0728d-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="0728d-156">Это дает преимущества проверки модели на стороне сервера и упрощает расширение модели при необходимости.</span><span class="sxs-lookup"><span data-stu-id="0728d-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>

<span data-ttu-id="0728d-157">Основные шаги для отправки простого типа одинаковы, но есть два незначительных различия.</span><span class="sxs-lookup"><span data-stu-id="0728d-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="0728d-158">Сначала в контроллере необходимо снабдить имя параметра атрибутом **FromBody** .</span><span class="sxs-lookup"><span data-stu-id="0728d-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="0728d-159">По умолчанию веб-API пытается получить простые типы из универсального кода ресурса (URI) запроса.</span><span class="sxs-lookup"><span data-stu-id="0728d-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="0728d-160">Атрибут **FromBody** сообщает веб-API о необходимости считывания значения из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="0728d-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="0728d-161">Веб-API считывает текст ответа не более одного раза, поэтому в тексте запроса может быть только один параметр действия.</span><span class="sxs-lookup"><span data-stu-id="0728d-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="0728d-162">Если необходимо получить несколько значений из текста запроса, определите сложный тип.</span><span class="sxs-lookup"><span data-stu-id="0728d-162">If you need to get multiple values from the request body, define a complex type.</span></span>

<span data-ttu-id="0728d-163">Во вторых, клиенту необходимо отправить значение в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="0728d-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="0728d-164">В частности, часть имени пары «имя-значение» для простого типа должна быть пустой.</span><span class="sxs-lookup"><span data-stu-id="0728d-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="0728d-165">Не все браузеры поддерживают это для HTML-форм, но этот формат создается в скрипте следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0728d-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="0728d-166">Ниже приведен пример формы.</span><span class="sxs-lookup"><span data-stu-id="0728d-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="0728d-167">И вот сценарий для отправки значения формы.</span><span class="sxs-lookup"><span data-stu-id="0728d-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="0728d-168">Единственное отличие от предыдущего скрипта — это аргумент, передаваемый в функцию **POST** .</span><span class="sxs-lookup"><span data-stu-id="0728d-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="0728d-169">Один и тот же подход можно использовать для отправки массива простых типов:</span><span class="sxs-lookup"><span data-stu-id="0728d-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="0728d-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0728d-170">Additional Resources</span></span>

[<span data-ttu-id="0728d-171">Часть 2. Передача файлов и составной MIME</span><span class="sxs-lookup"><span data-stu-id="0728d-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
