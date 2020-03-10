---
uid: webhooks/receiving/handlers
title: Обработчики веб-перехватчиков ASP.NET | Документация Майкрософт
author: rick-anderson
description: Обработка запросов в веб-перехватчиках ASP.NET.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518034"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="184c4-103">Обработчики веб-перехватчиков ASP.NET</span><span class="sxs-lookup"><span data-stu-id="184c4-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="184c4-104">После проверки запросов веб-перехватчиков приемником веб-перехватчика он готов к обработке с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="184c4-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="184c4-105">Именно здесь поступают *обработчики* .</span><span class="sxs-lookup"><span data-stu-id="184c4-105">This is where *handlers* come in.</span></span> <span data-ttu-id="184c4-106">Обработчики являются производными от интерфейса [ивебхукхандлер](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) , но обычно используют класс [вебхукхандлер](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) вместо наследования непосредственно от интерфейса.</span><span class="sxs-lookup"><span data-stu-id="184c4-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="184c4-107">Запрос веб-перехватчика может обрабатываться одним или несколькими обработчиками.</span><span class="sxs-lookup"><span data-stu-id="184c4-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="184c4-108">Обработчики вызываются в порядке, основанном на их свойствах *Order* , которые передаются от нижнего к большему, где порядок является простым целым числом (от 1 до 100):</span><span class="sxs-lookup"><span data-stu-id="184c4-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![Диаграмма свойств "порядок обработчика веб-перехватчика"](_static/Handlers.png)

<span data-ttu-id="184c4-110">Обработчик может дополнительно задать свойство *Response* для вебхукхандлерконтекст, которое приведет к прерыванию обработки, а ответ будет отправлен обратно как HTTP-ответ на веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="184c4-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="184c4-111">В приведенном выше случае обработчик C не будет вызываться, так как он имеет более высокий порядок, чем B, а B задает ответ.</span><span class="sxs-lookup"><span data-stu-id="184c4-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="184c4-112">Установка ответа обычно относится только к веб-перехватчикам, в которых ответ может передавать информацию обратно в исходный API.</span><span class="sxs-lookup"><span data-stu-id="184c4-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="184c4-113">Например, в случае с веб-перехватчиками временного резерва, где ответ отправляется обратно в канал, из которого поступил веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="184c4-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="184c4-114">Обработчики могут задать свойство получателя, если им требуется только получить веб-перехватчики от этого конкретного получателя.</span><span class="sxs-lookup"><span data-stu-id="184c4-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="184c4-115">Если они не задают получателя, они вызываются для всех из них.</span><span class="sxs-lookup"><span data-stu-id="184c4-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="184c4-116">Еще одним распространенным применением ответа является использование ответа *410* , чтобы указать, что веб-перехватчик больше не активен и дальнейшие запросы не должны отправляться.</span><span class="sxs-lookup"><span data-stu-id="184c4-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="184c4-117">По умолчанию обработчик будет вызываться всеми приемниками веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="184c4-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="184c4-118">Однако если свойству *получателя* присвоено имя обработчика, этот обработчик будет принимать только запросы веб-перехватчика от этого получателя.</span><span class="sxs-lookup"><span data-stu-id="184c4-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="184c4-119">Обработка веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="184c4-119">Processing a WebHook</span></span>

<span data-ttu-id="184c4-120">При вызове обработчика он получает [вебхукхандлерконтекст](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) , содержащий сведения о запросе веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="184c4-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="184c4-121">Данные (обычно текст HTTP-запроса) доступны в свойстве *Data* .</span><span class="sxs-lookup"><span data-stu-id="184c4-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="184c4-122">Тип данных обычно представляет собой данные в формате JSON или HTML, но при необходимости можно привести к более конкретному типу.</span><span class="sxs-lookup"><span data-stu-id="184c4-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="184c4-123">Например, пользовательские веб-перехватчики, создаваемые веб-перехватчиками ASP.NET, можно привести к типу [кустомнотификатионс](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="184c4-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="184c4-124">Обработка в очереди</span><span class="sxs-lookup"><span data-stu-id="184c4-124">Queued Processing</span></span>

<span data-ttu-id="184c4-125">Большинство Отправители веб-перехватчиков повторно отправляют веб-перехватчик, если ответ не будет создан в течение нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="184c4-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="184c4-126">Это означает, что обработчик должен завершить обработку в течение этого промежутка времени, чтобы не вызывать его снова.</span><span class="sxs-lookup"><span data-stu-id="184c4-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="184c4-127">Если обработка занимает больше времени или лучше обрабатывается отдельно, [вебхуккуеуехандлер](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) можно использовать для отправки запроса веб-перехватчика в очередь, например [очередь службы хранилища Azure](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span><span class="sxs-lookup"><span data-stu-id="184c4-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="184c4-128">Структура реализации [вебхуккуеуехандлер](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) представлена здесь:</span><span class="sxs-lookup"><span data-stu-id="184c4-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
