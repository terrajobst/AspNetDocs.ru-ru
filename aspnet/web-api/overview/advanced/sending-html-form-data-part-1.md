---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'Отправка данных формы HTML в веб-API ASP.NET: Данные формы urlencoded — ASP.NET 4.x'
author: MikeWasson
description: В этой статье показано, как для отправки данных формы urlencoded контроллер Web API с помощью ASP.NET 4.x
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: fb0309af11910125943737ebb721b356b7bd08bc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59418304"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="81a98-103">Отправка данных формы HTML в веб-API ASP.NET: Данные формы в URL-кодировке</span><span class="sxs-lookup"><span data-stu-id="81a98-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="81a98-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="81a98-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="81a98-105">Часть 1. Данные формы в URL-кодировке</span><span class="sxs-lookup"><span data-stu-id="81a98-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="81a98-106">В этой статье показано, как для отправки данных формы urlencoded контроллер Web API.</span><span class="sxs-lookup"><span data-stu-id="81a98-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="81a98-107">Общие сведения о HTML-формы</span><span class="sxs-lookup"><span data-stu-id="81a98-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="81a98-108">Отправка сложных типов</span><span class="sxs-lookup"><span data-stu-id="81a98-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="81a98-109">Отправка данных формы с помощью AJAX</span><span class="sxs-lookup"><span data-stu-id="81a98-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="81a98-110">Отправка простых типов</span><span class="sxs-lookup"><span data-stu-id="81a98-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="81a98-111">[Скачивание готового проекта](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span><span class="sxs-lookup"><span data-stu-id="81a98-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="81a98-112">Общие сведения о HTML-формы</span><span class="sxs-lookup"><span data-stu-id="81a98-112">Overview of HTML Forms</span></span>

<span data-ttu-id="81a98-113">Использование форм HTML GET или POST для отправки данных на сервер.</span><span class="sxs-lookup"><span data-stu-id="81a98-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="81a98-114">**Метод** атрибут **формы** элемента предоставляет метод HTTP:</span><span class="sxs-lookup"><span data-stu-id="81a98-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="81a98-115">Метод по умолчанию — GET.</span><span class="sxs-lookup"><span data-stu-id="81a98-115">The default method is GET.</span></span> <span data-ttu-id="81a98-116">Если форма использует GET, формы, в которой данные кодируются в виде строки запроса URI.</span><span class="sxs-lookup"><span data-stu-id="81a98-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="81a98-117">Если в форме используется POST, данные формы помещается в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="81a98-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="81a98-118">Для отправки данных **enctype** атрибут задает формат текста запроса:</span><span class="sxs-lookup"><span data-stu-id="81a98-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="81a98-119">Enctype</span><span class="sxs-lookup"><span data-stu-id="81a98-119">enctype</span></span> | <span data-ttu-id="81a98-120">Описание</span><span class="sxs-lookup"><span data-stu-id="81a98-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="81a98-121">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="81a98-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="81a98-122">Данные формы кодируются как пары имя/значение, аналогичную строку запроса URI.</span><span class="sxs-lookup"><span data-stu-id="81a98-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="81a98-123">Это формат по умолчанию для POST.</span><span class="sxs-lookup"><span data-stu-id="81a98-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="81a98-124">данные multipart/формы</span><span class="sxs-lookup"><span data-stu-id="81a98-124">multipart/form-data</span></span> | <span data-ttu-id="81a98-125">Данные формы кодируются как составное сообщение MIME.</span><span class="sxs-lookup"><span data-stu-id="81a98-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="81a98-126">Этот формат следует используйте, если при передаче файла на сервер.</span><span class="sxs-lookup"><span data-stu-id="81a98-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="81a98-127">Часть 1 из этой статье рассматривается x-www-формы-urlencoded формат.</span><span class="sxs-lookup"><span data-stu-id="81a98-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="81a98-128">[Часть 2](sending-html-form-data-part-2.md) описывает составное сообщение MIME.</span><span class="sxs-lookup"><span data-stu-id="81a98-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="81a98-129">Отправка сложных типов</span><span class="sxs-lookup"><span data-stu-id="81a98-129">Sending Complex Types</span></span>

<span data-ttu-id="81a98-130">Как правило будет отправлять сложный тип, состоящий из значения, взятые из нескольких элементов управления формы.</span><span class="sxs-lookup"><span data-stu-id="81a98-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="81a98-131">Рассмотрим следующую модель, представляющий состояние.</span><span class="sxs-lookup"><span data-stu-id="81a98-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="81a98-132">Вот контроллер веб-API, который принимает `Update` объекта с помощью запроса POST.</span><span class="sxs-lookup"><span data-stu-id="81a98-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="81a98-133">Этот контроллер с помощью [маршрутизации на основе действия](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), поэтому в шаблоне маршрута будет &quot;api / {controller} / {action} / {id}&quot;.</span><span class="sxs-lookup"><span data-stu-id="81a98-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="81a98-134">Клиент будет размещать данные для &quot;/api/updates/complex&quot;.</span><span class="sxs-lookup"><span data-stu-id="81a98-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>


<span data-ttu-id="81a98-135">Теперь давайте напишем HTML-формы для пользователей отправить обновление состояния.</span><span class="sxs-lookup"><span data-stu-id="81a98-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="81a98-136">Обратите внимание, что **действие** атрибут на форме представляет собой URI наши действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="81a98-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="81a98-137">Вот какие-либо значения, введенные в форму.</span><span class="sxs-lookup"><span data-stu-id="81a98-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="81a98-138">Когда пользователь нажимает кнопку Submit, браузер отправляет запрос HTTP следующего вида:</span><span class="sxs-lookup"><span data-stu-id="81a98-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="81a98-139">Обратите внимание на то, что текст запроса содержит данные формы, в формате пар "имя значение".</span><span class="sxs-lookup"><span data-stu-id="81a98-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="81a98-140">Веб-API автоматически преобразует пары "имя значение" в экземпляре `Update` класса.</span><span class="sxs-lookup"><span data-stu-id="81a98-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="81a98-141">Отправка данных формы с помощью AJAX</span><span class="sxs-lookup"><span data-stu-id="81a98-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="81a98-142">Когда пользователь отправляет форму, браузер выходит за пределы текущей страницы и отображает текст ответного сообщения.</span><span class="sxs-lookup"><span data-stu-id="81a98-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="81a98-143">Это нормально, когда ответ является HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="81a98-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="81a98-144">С помощью веб-API, тем не менее, текст ответа — обычно либо пуст или содержит структурированных данных, таких как JSON.</span><span class="sxs-lookup"><span data-stu-id="81a98-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="81a98-145">В этом случае более разумно для отправки запросов данных формы, с помощью AJAX, чтобы страницы может обработать ответ.</span><span class="sxs-lookup"><span data-stu-id="81a98-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="81a98-146">Ниже показано, как при отправке данных формы, с помощью jQuery.</span><span class="sxs-lookup"><span data-stu-id="81a98-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="81a98-147">JQuery **отправить** функция заменяет действий формы с помощью новой функции.</span><span class="sxs-lookup"><span data-stu-id="81a98-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="81a98-148">Это значение переопределяет поведение по умолчанию для кнопки «Отправить».</span><span class="sxs-lookup"><span data-stu-id="81a98-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="81a98-149">**Сериализации** функция сериализует данные формы в пары "имя значение".</span><span class="sxs-lookup"><span data-stu-id="81a98-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="81a98-150">Чтобы отправить данные формы на сервер, вызовите `$.post()`.</span><span class="sxs-lookup"><span data-stu-id="81a98-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="81a98-151">По завершении запроса `.success()` или `.error()` обработчика отображается соответствующее сообщение для пользователя.</span><span class="sxs-lookup"><span data-stu-id="81a98-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="81a98-152">Отправка простых типов</span><span class="sxs-lookup"><span data-stu-id="81a98-152">Sending Simple Types</span></span>

<span data-ttu-id="81a98-153">В предыдущих разделах мы отправили сложный тип, который веб-API десериализовать в экземпляр класса модели.</span><span class="sxs-lookup"><span data-stu-id="81a98-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="81a98-154">Вы также можете отправлять простые типы, такие как строка.</span><span class="sxs-lookup"><span data-stu-id="81a98-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="81a98-155">Перед отправкой простой тип, рекомендуется вместо этого поместив значение сложного типа.</span><span class="sxs-lookup"><span data-stu-id="81a98-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="81a98-156">Это дает преимущества модели проверки на стороне сервера и позволяет добавлять в модель при необходимости.</span><span class="sxs-lookup"><span data-stu-id="81a98-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>


<span data-ttu-id="81a98-157">Основные шаги для отправки простого типа одинаковы, но есть две небольшие отличия.</span><span class="sxs-lookup"><span data-stu-id="81a98-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="81a98-158">Во-первых, в контроллере, необходимо снабдить имени параметра **FromBody** атрибута.</span><span class="sxs-lookup"><span data-stu-id="81a98-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="81a98-159">По умолчанию веб-API будет предпринята попытка простых типов из идентификатора URI запроса.</span><span class="sxs-lookup"><span data-stu-id="81a98-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="81a98-160">**FromBody** атрибут сообщает веб-API для чтения значения из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="81a98-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="81a98-161">Веб-API считывает текст ответа и не более одного раза, только один параметр действия могут поступать из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="81a98-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="81a98-162">Если вам нужно получить несколько значений из текста запроса, определения сложного типа.</span><span class="sxs-lookup"><span data-stu-id="81a98-162">If you need to get multiple values from the request body, define a complex type.</span></span>


<span data-ttu-id="81a98-163">Во-вторых клиенту необходимо отправить значение в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="81a98-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="81a98-164">В частности часть пары "имя/значение" должен быть пустым для простого типа.</span><span class="sxs-lookup"><span data-stu-id="81a98-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="81a98-165">Не все браузеры поддерживают это для HTML-формы, но создавать этот формат в скрипте следующим образом:</span><span class="sxs-lookup"><span data-stu-id="81a98-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="81a98-166">Вот примеры формы:</span><span class="sxs-lookup"><span data-stu-id="81a98-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="81a98-167">И Вот сценарий для отправки значения формы.</span><span class="sxs-lookup"><span data-stu-id="81a98-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="81a98-168">Единственное отличие от предыдущего сценария — это аргумент, переданный в **блога** функции.</span><span class="sxs-lookup"><span data-stu-id="81a98-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="81a98-169">Тот же подход можно использовать для отправки массив простых типов:</span><span class="sxs-lookup"><span data-stu-id="81a98-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="81a98-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="81a98-170">Additional Resources</span></span>

[<span data-ttu-id="81a98-171">Часть 2. Отправка файлов и составное сообщение MIME</span><span class="sxs-lookup"><span data-stu-id="81a98-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
