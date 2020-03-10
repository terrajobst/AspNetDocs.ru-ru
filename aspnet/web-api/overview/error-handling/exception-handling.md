---
uid: web-api/overview/error-handling/exception-handling
title: Обработка исключений в веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504702"
---
# <a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="aee02-102">Обработка исключений в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="aee02-102">Exception Handling in ASP.NET Web API</span></span>

<span data-ttu-id="aee02-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="aee02-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="aee02-104">В этой статье описывается обработка ошибок и исключений в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aee02-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="aee02-105">хттпреспонсиксцептион</span><span class="sxs-lookup"><span data-stu-id="aee02-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="aee02-106">Фильтры исключений</span><span class="sxs-lookup"><span data-stu-id="aee02-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="aee02-107">Регистрация фильтров исключений</span><span class="sxs-lookup"><span data-stu-id="aee02-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="aee02-108">HttpError</span><span class="sxs-lookup"><span data-stu-id="aee02-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="aee02-109">хттпреспонсиксцептион</span><span class="sxs-lookup"><span data-stu-id="aee02-109">HttpResponseException</span></span>

<span data-ttu-id="aee02-110">Что происходит, если контроллер веб-API вызывает неперехваченное исключение?</span><span class="sxs-lookup"><span data-stu-id="aee02-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="aee02-111">По умолчанию большинство исключений преобразуются в HTTP-ответ с кодом состояния 500, внутренняя ошибка сервера.</span><span class="sxs-lookup"><span data-stu-id="aee02-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="aee02-112">Тип **хттпреспонсиксцептион** является особым случаем.</span><span class="sxs-lookup"><span data-stu-id="aee02-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="aee02-113">Это исключение возвращает любой код состояния HTTP, указанный в конструкторе исключений.</span><span class="sxs-lookup"><span data-stu-id="aee02-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="aee02-114">Например, следующий метод возвращает 404, но не найден, если параметр *ID* является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="aee02-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="aee02-115">Чтобы получить более полный контроль над ответом, можно также создать все ответное сообщение и включить его в **хттпреспонсиксцептион:**</span><span class="sxs-lookup"><span data-stu-id="aee02-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="aee02-116">Фильтры исключений</span><span class="sxs-lookup"><span data-stu-id="aee02-116">Exception Filters</span></span>

<span data-ttu-id="aee02-117">Вы можете настроить обработку исключений веб-API, написав *фильтр исключений*.</span><span class="sxs-lookup"><span data-stu-id="aee02-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="aee02-118">Фильтр исключений выполняется, когда метод контроллера создает любое необработанное исключение, которое *не* является исключением **хттпреспонсиксцептион** .</span><span class="sxs-lookup"><span data-stu-id="aee02-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="aee02-119">Тип **хттпреспонсиксцептион** является особым случаем, так как он предназначен специально для возврата HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="aee02-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="aee02-120">Фильтры исключений реализуют интерфейс **System. Web. http. Filters. иексцептионфилтер** .</span><span class="sxs-lookup"><span data-stu-id="aee02-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="aee02-121">Самым простым способом написания фильтра исключений является наследование от класса **System. Web. http. Filters. ексцептионфилтераттрибуте** и переопределение метода, **Кроме** .</span><span class="sxs-lookup"><span data-stu-id="aee02-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="aee02-122">Фильтры исключений в веб-API ASP.NET похожи на те, которые относятся к ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="aee02-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="aee02-123">Однако они объявляются в отдельном пространстве имен и работают отдельно.</span><span class="sxs-lookup"><span data-stu-id="aee02-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="aee02-124">В частности, класс **хандлиррораттрибуте** , используемый в MVC, не обрабатывает исключения, созданные контроллерами веб-API.</span><span class="sxs-lookup"><span data-stu-id="aee02-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>

<span data-ttu-id="aee02-125">Ниже приведен фильтр, преобразующий исключения **NotImplementedException** в код состояния HTTP 501, который не реализован:</span><span class="sxs-lookup"><span data-stu-id="aee02-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="aee02-126">Свойство **Response** объекта **хттпактионексекутедконтекст** содержит ответное сообщение HTTP, которое будет отправлено клиенту.</span><span class="sxs-lookup"><span data-stu-id="aee02-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="aee02-127">Регистрация фильтров исключений</span><span class="sxs-lookup"><span data-stu-id="aee02-127">Registering Exception Filters</span></span>

<span data-ttu-id="aee02-128">Существует несколько способов регистрации фильтра исключений веб-API:</span><span class="sxs-lookup"><span data-stu-id="aee02-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="aee02-129">Для действия</span><span class="sxs-lookup"><span data-stu-id="aee02-129">By action</span></span>
- <span data-ttu-id="aee02-130">Для контроллера</span><span class="sxs-lookup"><span data-stu-id="aee02-130">By controller</span></span>
- <span data-ttu-id="aee02-131">Глобально</span><span class="sxs-lookup"><span data-stu-id="aee02-131">Globally</span></span>

<span data-ttu-id="aee02-132">Чтобы применить фильтр к определенному действию, добавьте его в качестве атрибута в действие:</span><span class="sxs-lookup"><span data-stu-id="aee02-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="aee02-133">Чтобы применить фильтр ко всем действиям на контроллере, добавьте фильтр в качестве атрибута в класс Controller:</span><span class="sxs-lookup"><span data-stu-id="aee02-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="aee02-134">Чтобы применить фильтр глобально ко всем контроллерам веб-API, добавьте экземпляр фильтра в коллекцию **глобалконфигуратион. Configuration. Filters** .</span><span class="sxs-lookup"><span data-stu-id="aee02-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="aee02-135">В этой коллекции фильтры исключений применяются к любому действию контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="aee02-135">Exception filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="aee02-136">Если вы используете шаблон проекта "веб-приложение ASP.NET MVC 4" для создания проекта, добавьте код конфигурации веб-API в класс `WebApiConfig`, который находится в папке приложения\_Start.</span><span class="sxs-lookup"><span data-stu-id="aee02-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="aee02-137">HttpError</span><span class="sxs-lookup"><span data-stu-id="aee02-137">HttpError</span></span>

<span data-ttu-id="aee02-138">Объект **HttpError** обеспечивает единообразный способ возврата сведений об ошибке в тексте ответа.</span><span class="sxs-lookup"><span data-stu-id="aee02-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="aee02-139">В следующем примере показано, как вернуть код состояния HTTP 404 (не найдено) с **HttpError** в тексте ответа.</span><span class="sxs-lookup"><span data-stu-id="aee02-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="aee02-140">**Креатиррорреспонсе** — это метод расширения, определенный в классе **System .NET. http. хттпрекуестмессажеекстенсионс** .</span><span class="sxs-lookup"><span data-stu-id="aee02-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="aee02-141">На внутреннем уровне **креатиррорреспонсе** создает экземпляр **HttpError** , а затем создает **HttpResponseMessage** , содержащий **HttpError**.</span><span class="sxs-lookup"><span data-stu-id="aee02-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="aee02-142">В этом примере, если метод выполнен успешно, он возвращает продукт в HTTP-ответе.</span><span class="sxs-lookup"><span data-stu-id="aee02-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="aee02-143">Но если запрошенный продукт не найден, HTTP-ответ содержит **HttpError** в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="aee02-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="aee02-144">Ответ может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="aee02-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="aee02-145">Обратите внимание, что в этом примере **HttpError** был СЕРИАЛИЗОВАН в JSON.</span><span class="sxs-lookup"><span data-stu-id="aee02-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="aee02-146">Одним из преимуществ использования **HttpError** является то, что он проходит через тот же процесс [согласования содержимого](../formats-and-model-binding/content-negotiation.md) и сериализации, что и любая другая строго типизированная модель.</span><span class="sxs-lookup"><span data-stu-id="aee02-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="aee02-147">HttpError и проверка модели</span><span class="sxs-lookup"><span data-stu-id="aee02-147">HttpError and Model Validation</span></span>

<span data-ttu-id="aee02-148">Для проверки модели можно передать состояние модели в **креатиррорреспонсе**, чтобы включить в ответ ошибки проверки:</span><span class="sxs-lookup"><span data-stu-id="aee02-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="aee02-149">Этот пример может вернуть следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="aee02-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="aee02-150">Дополнительные сведения о проверке модели см. [в разделе Проверка модели в веб-API ASP.NET](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="aee02-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="aee02-151">Использование HttpError с Хттпреспонсиксцептион</span><span class="sxs-lookup"><span data-stu-id="aee02-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="aee02-152">В предыдущих примерах возвращается сообщение **HttpResponseMessage** из действия контроллера, но можно также использовать **Хттпреспонсиксцептион** для возврата **HttpError**.</span><span class="sxs-lookup"><span data-stu-id="aee02-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="aee02-153">Это позволяет возвращать строго типизированную модель в нормальном случае успеха, при этом возвращая **HttpError** в случае ошибки:</span><span class="sxs-lookup"><span data-stu-id="aee02-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
