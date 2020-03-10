---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: Проверка модели в веб-API ASP.NET ASP.NET 4. x
author: MikeWasson
description: Общие сведения о проверке модели в веб-API ASP.NET ASP.NET 4. x.
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448932"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="9bfe7-103">Проверка модели в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9bfe7-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="9bfe7-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9bfe7-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9bfe7-105">В этой статье показано, как добавлять заметки к моделям, использовать заметки для проверки данных и обрабатывайте ошибки проверки в веб-API.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="9bfe7-106">Когда клиент отправляет данные в веб-API, часто требуется проверить данные перед обработкой.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="9bfe7-107">Заметки к данным</span><span class="sxs-lookup"><span data-stu-id="9bfe7-107">Data Annotations</span></span>

<span data-ttu-id="9bfe7-108">В веб-API ASP.NET можно использовать атрибуты из пространства имен [System. ComponentModel. аннотации](/dotnet/api/system.componentmodel.dataannotations) , чтобы задать правила проверки для свойств модели.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="9bfe7-109">Рассмотрим следующую модель:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="9bfe7-110">Если вы использовали проверку модели в ASP.NET MVC, это должно показаться знакомым.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="9bfe7-111">**Обязательный** атрибут говорит, что свойство `Name` не должно иметь значение null.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="9bfe7-112">Атрибут **Range** говорит, что `Weight` должны быть в диапазоне от 0 до 999.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="9bfe7-113">Предположим, что клиент отправляет запрос POST со следующим представлением JSON:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="9bfe7-114">Вы видите, что клиент не включал свойство `Name`, которое отмечено как обязательное.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="9bfe7-115">Когда веб-API преобразует JSON в экземпляр `Product`, он проверяет `Product` по атрибутам проверки.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="9bfe7-116">В действии контроллера можно проверить, является ли модель допустимой:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="9bfe7-117">Проверка модели не гарантирует, что данные клиента являются безнадежными.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="9bfe7-118">На других уровнях приложения может потребоваться дополнительная проверка.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="9bfe7-119">(Например, на уровне данных могут применяться ограничения внешнего ключа.) В руководстве [Использование веб-API с Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) рассматриваются некоторые из этих проблем.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="9bfe7-120">**"Под учетной записью"** : Разноска происходит, когда клиент оставляет некоторые свойства.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="9bfe7-121">Например, предположим, что клиент отправляет следующее:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="9bfe7-122">Здесь клиент не указал значения для `Price` или `Weight`.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="9bfe7-123">Модуль форматирования JSON присваивает отсутствующим свойствам значение по умолчанию, равное нулю.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="9bfe7-124">Состояние модели является допустимым, поскольку ноль является допустимым значением для этих свойств.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="9bfe7-125">Зависит ли проблема от вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="9bfe7-126">Например, в операции обновления может потребоваться отличать "ноль" и "Not Set".</span><span class="sxs-lookup"><span data-stu-id="9bfe7-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="9bfe7-127">Чтобы заставить клиентов задать значение, сделайте свойство обнуляемым и задайте **требуемый** атрибут:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="9bfe7-128">**"Over-Post"** : Клиент также может отправлять *больше* данных, чем ожидалось.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="9bfe7-129">Пример:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="9bfe7-130">В этом случае JSON включает свойство ("Color"), которое не существует в модели `Product`.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="9bfe7-131">В этом случае модуль форматирования JSON просто игнорирует это значение.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="9bfe7-132">(Модуль форматирования XML делает то же самое.) Избыточная передача вызывает проблемы, если у модели есть свойства, предназначенные только для чтения.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="9bfe7-133">Пример:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="9bfe7-134">Пользователям не нужно обновлять свойство `IsAdmin` и повышать уровень прав для администраторов!</span><span class="sxs-lookup"><span data-stu-id="9bfe7-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="9bfe7-135">Наиболее надежной стратегией является использование класса модели, точно соответствующего тому, что клиенту разрешено передавать:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="9bfe7-136">В записи блога Михаил Уилсон ("[Проверка входных данных и проверка модели в ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" есть хорошее обсуждение вложений в публикацию и последующей публикации.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="9bfe7-137">Несмотря на то, что запись относится к ASP.NET MVC 2, проблемы по-прежнему связаны с Web API.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>

## <a name="handling-validation-errors"></a><span data-ttu-id="9bfe7-138">Обработка ошибок проверки</span><span class="sxs-lookup"><span data-stu-id="9bfe7-138">Handling Validation Errors</span></span>

<span data-ttu-id="9bfe7-139">Веб-API не возвращает клиенту ошибку автоматически при сбое проверки.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="9bfe7-140">Действие контроллера проверяет состояние модели и отвечает соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="9bfe7-141">Можно также создать фильтр действий для проверки состояния модели перед вызовом действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="9bfe7-142">Пример кода приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="9bfe7-143">Если проверка модели завершается неудачно, этот фильтр возвращает ответ HTTP, содержащий ошибки проверки.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="9bfe7-144">В этом случае действие контроллера не вызывается.</span><span class="sxs-lookup"><span data-stu-id="9bfe7-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="9bfe7-145">Чтобы применить этот фильтр ко всем контроллерам веб-API, добавьте экземпляр фильтра в коллекцию **HttpConfiguration. Filters** во время настройки:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="9bfe7-146">Другой вариант — задать фильтр в качестве атрибута для отдельных контроллеров или действий контроллера:</span><span class="sxs-lookup"><span data-stu-id="9bfe7-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
