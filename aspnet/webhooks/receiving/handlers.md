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
# <a name="aspnet-webhooks-handlers"></a>Обработчики веб-перехватчиков ASP.NET

После проверки запросов веб-перехватчиков приемником веб-перехватчика он готов к обработке с помощью пользовательского кода. Именно здесь поступают *обработчики* . Обработчики являются производными от интерфейса [ивебхукхандлер](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) , но обычно используют класс [вебхукхандлер](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) вместо наследования непосредственно от интерфейса.

Запрос веб-перехватчика может обрабатываться одним или несколькими обработчиками. Обработчики вызываются в порядке, основанном на их свойствах *Order* , которые передаются от нижнего к большему, где порядок является простым целым числом (от 1 до 100):

![Диаграмма свойств "порядок обработчика веб-перехватчика"](_static/Handlers.png)

Обработчик может дополнительно задать свойство *Response* для вебхукхандлерконтекст, которое приведет к прерыванию обработки, а ответ будет отправлен обратно как HTTP-ответ на веб-перехватчик. В приведенном выше случае обработчик C не будет вызываться, так как он имеет более высокий порядок, чем B, а B задает ответ.

Установка ответа обычно относится только к веб-перехватчикам, в которых ответ может передавать информацию обратно в исходный API. Например, в случае с веб-перехватчиками временного резерва, где ответ отправляется обратно в канал, из которого поступил веб-перехватчик. Обработчики могут задать свойство получателя, если им требуется только получить веб-перехватчики от этого конкретного получателя. Если они не задают получателя, они вызываются для всех из них.

Еще одним распространенным применением ответа является использование ответа *410* , чтобы указать, что веб-перехватчик больше не активен и дальнейшие запросы не должны отправляться.

По умолчанию обработчик будет вызываться всеми приемниками веб-перехватчика. Однако если свойству *получателя* присвоено имя обработчика, этот обработчик будет принимать только запросы веб-перехватчика от этого получателя.

## <a name="processing-a-webhook"></a>Обработка веб-перехватчика

При вызове обработчика он получает [вебхукхандлерконтекст](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) , содержащий сведения о запросе веб-перехватчика. Данные (обычно текст HTTP-запроса) доступны в свойстве *Data* .

Тип данных обычно представляет собой данные в формате JSON или HTML, но при необходимости можно привести к более конкретному типу. Например, пользовательские веб-перехватчики, создаваемые веб-перехватчиками ASP.NET, можно привести к типу [кустомнотификатионс](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) следующим образом:

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

  ## <a name="queued-processing"></a>Обработка в очереди

Большинство Отправители веб-перехватчиков повторно отправляют веб-перехватчик, если ответ не будет создан в течение нескольких секунд. Это означает, что обработчик должен завершить обработку в течение этого промежутка времени, чтобы не вызывать его снова.

Если обработка занимает больше времени или лучше обрабатывается отдельно, [вебхуккуеуехандлер](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) можно использовать для отправки запроса веб-перехватчика в очередь, например [очередь службы хранилища Azure](https://msdn.microsoft.com/library/azure/dd179353.aspx).

Структура реализации [вебхуккуеуехандлер](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) представлена здесь:

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
