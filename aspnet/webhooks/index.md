---
uid: webhooks/index
title: Общие сведения о веб-перехватчиках ASP.NET | Документация Майкрософт
author: rick-anderson
description: Введение в веб-перехватчики ASP.NET.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 1e21c92e950893c0ff87c63f03f4710a158441fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517536"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="1473d-103">Общие сведения о веб-перехватчиках ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1473d-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="1473d-104">Веб-перехватчик — это упрощенный HTTP-шаблон, обеспечивающий простую модель подписки для связи друг с другом веб-API и SaaS-служб.</span><span class="sxs-lookup"><span data-stu-id="1473d-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="1473d-105">Когда в службе происходит событие, зарегистрированным подписчикам отправляется уведомление в форме POST HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="1473d-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="1473d-106">Запрос POST содержит сведения о событии, благодаря чему получатель может выполнить соответствующие действия.</span><span class="sxs-lookup"><span data-stu-id="1473d-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="1473d-107">Благодаря простоте веб-перехватчики уже предоставляются большим количеством служб, включая [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [BitBucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [резервный](http://www.slack.com)период, [stripe](http://www.stripe.com), [Trello](http://www.trello.com/)и многие другие.</span><span class="sxs-lookup"><span data-stu-id="1473d-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="1473d-108">Например, веб-перехватчик может указывать на то, что файл был изменен в [Dropbox](http://dropbox.com/), или если изменение кода было зафиксировано в GitHub или если платеж был инициирован в [PayPal](http://www.paypal.com/)или если в [Trello](http://www.trello.com/)создана карточка.</span><span class="sxs-lookup"><span data-stu-id="1473d-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="1473d-109">Возможности бесконечно!</span><span class="sxs-lookup"><span data-stu-id="1473d-109">The possibilities are endless!</span></span>

<span data-ttu-id="1473d-110">Microsoft ASP.NET веб-перехватчики упрощают отправку и получение веб-перехватчиков в рамках приложения ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="1473d-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="1473d-111">На принимающей стороне она предоставляет общую модель для получения и обработки веб-перехватчиков из любого числа поставщиков веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="1473d-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="1473d-112">Она поставляется в комплекте с поддержкой [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [BitBucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [временного резерва](http://www.slack.com), [stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) и [Zendesk](https://www.zendesk.com/) , но вы легко добавляете поддержку.</span><span class="sxs-lookup"><span data-stu-id="1473d-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="1473d-113">На отправляющей стороне он обеспечивает поддержку для управления и хранения подписок, а также для отправки уведомлений о событиях в правильный набор подписчиков.</span><span class="sxs-lookup"><span data-stu-id="1473d-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="1473d-114">Это позволяет определить собственный набор событий, на которые подписчики могут подписываться, и уведомлять их о происходящих событиях.</span><span class="sxs-lookup"><span data-stu-id="1473d-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="1473d-115">В зависимости от вашего сценария эти две части можно использовать вместе или отдельно.</span><span class="sxs-lookup"><span data-stu-id="1473d-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="1473d-116">Если требуется только получение веб-перехватчиков из других служб, можно использовать только часть получателя. Если вы хотите предоставлять только веб-перехватчики для использования другими пользователями, то можете сделать именно это.</span><span class="sxs-lookup"><span data-stu-id="1473d-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="1473d-117">Код предназначен для веб-API ASP.NET 2 и ASP.NET MVC 5 и доступен в виде [OSS на GitHub](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="1473d-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="1473d-118">Обзор веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="1473d-118">WebHooks Overview</span></span>

<span data-ttu-id="1473d-119">Веб-перехватчики — это шаблон, который означает, что он используется в разных службах, но основная идея одинакова.</span><span class="sxs-lookup"><span data-stu-id="1473d-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="1473d-120">Веб-перехватчики можно рассматривать как простую модель публикации и подсоединения, где пользователь может подписываться на события, происходящие в других местах.</span><span class="sxs-lookup"><span data-stu-id="1473d-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="1473d-121">Уведомления о событиях распространяются как HTTP-запросы POST, содержащие сведения о самом событии.</span><span class="sxs-lookup"><span data-stu-id="1473d-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="1473d-122">Обычно запрос HTTP POST содержит объект JSON или данные формы HTML, определенные отправителем веб-перехватчика, включая сведения о событии, вызвавшем срабатывание веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="1473d-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="1473d-123">Например, текст запроса POST веб-перехватчика из [GitHub](https://www.github.com/) выглядит следующим образом в результате открытия новой проблемы в определенном репозитории:</span><span class="sxs-lookup"><span data-stu-id="1473d-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="1473d-124">Чтобы обеспечить действительность веб-перехватчика от предполагаемого отправителя, запрос POST защищается каким-либо образом и затем проверяется получателем.</span><span class="sxs-lookup"><span data-stu-id="1473d-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="1473d-125">Например, [веб-перехватчики GitHub](https://developer.github.com/webhooks/) содержат заголовок HTTP с *подписью X концентратора* с хэшем текста запроса, который проверяется реализацией получателя, поэтому вам не нужно беспокоиться о нем.</span><span class="sxs-lookup"><span data-stu-id="1473d-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="1473d-126">Поток веб-перехватчика обычно выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="1473d-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="1473d-127">Отправитель веб-перехватчика предоставляет события, на которые клиент может подписываться.</span><span class="sxs-lookup"><span data-stu-id="1473d-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="1473d-128">События описывают наблюдаемые изменения в системе, например, когда был вставлен новый элемент данных, процесс завершен или что-то еще.</span><span class="sxs-lookup"><span data-stu-id="1473d-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="1473d-129">Приемник веб-перехватчика подписывается путем регистрации веб-перехватчика, состоящего из четырех вещей:</span><span class="sxs-lookup"><span data-stu-id="1473d-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="1473d-130">Универсальный код ресурса (URI), по которому должно быть опубликовано уведомление о событии в виде HTTP-запроса POST;</span><span class="sxs-lookup"><span data-stu-id="1473d-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="1473d-131">Набор фильтров, описывающих конкретные события, для которых должен быть запущен веб-перехватчик;</span><span class="sxs-lookup"><span data-stu-id="1473d-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="1473d-132">Секретный ключ, который используется для подписания запроса HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="1473d-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="1473d-133">Дополнительные данные, которые должны быть добавлены в запрос HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="1473d-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="1473d-134">Это может быть, например, дополнительные поля заголовка HTTP или свойства, включенные в текст запроса HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="1473d-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="1473d-135">После наступления события обнаруживаются соответствующие регистрации веб-перехватчика и отправляются запросы HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="1473d-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="1473d-136">Как правило, повторное создание запросов HTTP POST выполняется несколько раз, если по какой-либо причине получатель не отвечает или запрос HTTP POST приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="1473d-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="1473d-137">Конвейер обработки веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="1473d-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="1473d-138">Конвейер обработки Microsoft ASP.NET веб-перехватчиков для входящих веб-перехватчиков выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1473d-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![Конвейер обработки веб-перехватчиков ASP.NET](_static/WebHookReceivers.png)

<span data-ttu-id="1473d-140">Ниже приведены два ключевых понятия: *приемники* и *обработчики*.</span><span class="sxs-lookup"><span data-stu-id="1473d-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="1473d-141">*Получатели* отвечают за обработку конкретной разновидности веб-перехватчика от данного отправителя и применение проверок безопасности, чтобы убедиться, что запрос веб-перехватчик действительно относится к предполагаемому отправителю.</span><span class="sxs-lookup"><span data-stu-id="1473d-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="1473d-142">*Обработчики* обычно используются, когда пользовательский код выполняет обработку конкретного веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="1473d-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="1473d-143">В следующих узлах эти понятия описаны более подробно.</span><span class="sxs-lookup"><span data-stu-id="1473d-143">In the following nodes these concepts are described in more details.</span></span>
