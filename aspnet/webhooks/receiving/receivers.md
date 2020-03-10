---
uid: webhooks/receiving/receivers
title: Получатели веб-перехватчиков ASP.NET | Документация Майкрософт
author: rick-anderson
description: Получатели веб-перехватчиков ASP.NET
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463464"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="4de8c-103">Получатели веб-перехватчиков ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4de8c-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="4de8c-104">Получение веб-перехватчиков зависит от отправителя.</span><span class="sxs-lookup"><span data-stu-id="4de8c-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="4de8c-105">Иногда есть дополнительные шаги, регистрирующие веб-перехватчик, который проверяет, действительно ли подписчик ожидает передачи данных.</span><span class="sxs-lookup"><span data-stu-id="4de8c-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="4de8c-106">Некоторые веб-перехватчики предоставляют модель Push-to-Pull, где запрос HTTP POST содержит только ссылку на сведения о событии, которые затем извлекаются независимо.</span><span class="sxs-lookup"><span data-stu-id="4de8c-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="4de8c-107">Зачастую модель безопасности довольно немного различается.</span><span class="sxs-lookup"><span data-stu-id="4de8c-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="4de8c-108">Назначение Microsoft ASP.NET веб-перехватчиков заключается в том, чтобы сделать их более простыми и более единообразными для подключения API, не тратя много времени на определение того, как обдумать какой-то конкретный вариант веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="4de8c-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="4de8c-109">Приемник веб-перехватчика отвечает за принятие и проверка веб-перехватчиков от конкретного отправителя.</span><span class="sxs-lookup"><span data-stu-id="4de8c-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="4de8c-110">Приемник веб-перехватчика может поддерживать любое количество веб-перехватчиков, каждый из которых имеет собственную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="4de8c-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="4de8c-111">Например, получатель веб-перехватчика GitHub может принимать веб-перехватчики из любого числа репозиториев GitHub.</span><span class="sxs-lookup"><span data-stu-id="4de8c-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="4de8c-112">URI приемника веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="4de8c-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="4de8c-113">Устанавливая Microsoft ASP.NET веб-перехватчиков, вы получаете общий контроллер веб-перехватчика, который принимает запросы к веб перехватчику из открытого количества служб.</span><span class="sxs-lookup"><span data-stu-id="4de8c-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="4de8c-114">При получении запроса он выбирает соответствующего получателя, который был установлен для обработки определенного отправителя веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="4de8c-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="4de8c-115">Универсальный код ресурса (URI) этого контроллера — это URI веб-перехватчика, регистрируемый в службе и имеющий вид:</span><span class="sxs-lookup"><span data-stu-id="4de8c-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="4de8c-116">По соображениям безопасности для многих приемников веб-перехватчиков требуется, чтобы URI был URI *HTTPS* , а в некоторых случаях он также должен содержать дополнительный параметр запроса, который используется, чтобы только предполагаемая сторона могла отправлять веб-перехватчики на указанный выше URI.</span><span class="sxs-lookup"><span data-stu-id="4de8c-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="4de8c-117">`<receiver>` компонент — это имя получателя, например `github` или `slack`.</span><span class="sxs-lookup"><span data-stu-id="4de8c-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="4de8c-118">*{ID}* — это необязательный идентификатор, который можно использовать для идентификации конкретной конфигурации приемника веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="4de8c-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="4de8c-119">Это можно использовать для регистрации N веб-перехватчиков с определенным получателем.</span><span class="sxs-lookup"><span data-stu-id="4de8c-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="4de8c-120">Например, для регистрации трех независимых веб-перехватчиков можно использовать следующие три URI:</span><span class="sxs-lookup"><span data-stu-id="4de8c-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="4de8c-121">Установка приемника веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="4de8c-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="4de8c-122">Чтобы получить веб-перехватчики с помощью Microsoft ASP.NET веб-перехватчиков, сначала необходимо установить пакет NuGet для поставщика веб-перехватчика или поставщиков, из которых вы хотите получить веб-перехватчики.</span><span class="sxs-lookup"><span data-stu-id="4de8c-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="4de8c-123">Пакеты NuGet называются [Microsoft. AspNet. WebParts. получатели. \*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) , где последняя часть указывает на поддержку службы.</span><span class="sxs-lookup"><span data-stu-id="4de8c-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="4de8c-124">Например.</span><span class="sxs-lookup"><span data-stu-id="4de8c-124">For example</span></span>

<span data-ttu-id="4de8c-125">[Microsoft. AspNet. веб-перехватчики. приемники. GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) предоставляет поддержку для получения веб-перехватчиков из GitHub и [Microsoft. AspNet. веб-перехватчики. получатели. Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) обеспечивает поддержку получения веб-перехватчиков, созданных веб-перехватчиками ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4de8c-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="4de8c-126">Вы можете найти поддержку для Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, временного резерва, stripe, Trello и WordPress, но можно поддерживать любое количество других поставщиков.</span><span class="sxs-lookup"><span data-stu-id="4de8c-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="4de8c-127">Настройка приемника веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="4de8c-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="4de8c-128">Приемники веб-перехватчика настраиваются с помощью [ивебхукрецеиверконфиг](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) реализовывать, а определенные реализации этого интерфейса можно зарегистрировать с помощью любой модели внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="4de8c-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="4de8c-129">Реализация по умолчанию использует параметры приложения, которые могут быть заданы в файле Web. config, или, при использовании веб-приложений Azure, можно настроить на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4de8c-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Параметры приложения Azure](_static/AzureAppSettings.png)

<span data-ttu-id="4de8c-131">Для ключей параметров приложения используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="4de8c-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="4de8c-132">Значение представляет собой разделенный запятыми список значений, соответствующих значениям *{ID}* , для которых зарегистрированы веб-перехватчики, например:</span><span class="sxs-lookup"><span data-stu-id="4de8c-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="4de8c-133">Инициализация приемника веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="4de8c-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="4de8c-134">Приемники веб-перехватчика инициализируются путем их регистрации, как правило, в статическом классе *WebApiConfig* , например:</span><span class="sxs-lookup"><span data-stu-id="4de8c-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
