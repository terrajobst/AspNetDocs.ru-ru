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
# <a name="aspnet-webhooks-receivers"></a>Получатели веб-перехватчиков ASP.NET

Получение веб-перехватчиков зависит от отправителя. Иногда есть дополнительные шаги, регистрирующие веб-перехватчик, который проверяет, действительно ли подписчик ожидает передачи данных. Некоторые веб-перехватчики предоставляют модель Push-to-Pull, где запрос HTTP POST содержит только ссылку на сведения о событии, которые затем извлекаются независимо. Зачастую модель безопасности довольно немного различается.

Назначение Microsoft ASP.NET веб-перехватчиков заключается в том, чтобы сделать их более простыми и более единообразными для подключения API, не тратя много времени на определение того, как обдумать какой-то конкретный вариант веб-перехватчиков.

Приемник веб-перехватчика отвечает за принятие и проверка веб-перехватчиков от конкретного отправителя. Приемник веб-перехватчика может поддерживать любое количество веб-перехватчиков, каждый из которых имеет собственную конфигурацию. Например, получатель веб-перехватчика GitHub может принимать веб-перехватчики из любого числа репозиториев GitHub.

## <a name="webhook-receiver-uris"></a>URI приемника веб-перехватчика

Устанавливая Microsoft ASP.NET веб-перехватчиков, вы получаете общий контроллер веб-перехватчика, который принимает запросы к веб перехватчику из открытого количества служб. При получении запроса он выбирает соответствующего получателя, который был установлен для обработки определенного отправителя веб-перехватчика.

Универсальный код ресурса (URI) этого контроллера — это URI веб-перехватчика, регистрируемый в службе и имеющий вид:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

По соображениям безопасности для многих приемников веб-перехватчиков требуется, чтобы URI был URI *HTTPS* , а в некоторых случаях он также должен содержать дополнительный параметр запроса, который используется, чтобы только предполагаемая сторона могла отправлять веб-перехватчики на указанный выше URI.

`<receiver>` компонент — это имя получателя, например `github` или `slack`.

*{ID}* — это необязательный идентификатор, который можно использовать для идентификации конкретной конфигурации приемника веб-перехватчика. Это можно использовать для регистрации N веб-перехватчиков с определенным получателем. Например, для регистрации трех независимых веб-перехватчиков можно использовать следующие три URI:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>Установка приемника веб-перехватчика

Чтобы получить веб-перехватчики с помощью Microsoft ASP.NET веб-перехватчиков, сначала необходимо установить пакет NuGet для поставщика веб-перехватчика или поставщиков, из которых вы хотите получить веб-перехватчики. Пакеты NuGet называются [Microsoft. AspNet. WebParts. получатели. *](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) , где последняя часть указывает на поддержку службы. Например.

[Microsoft. AspNet. веб-перехватчики. приемники. GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) предоставляет поддержку для получения веб-перехватчиков из GitHub и [Microsoft. AspNet. веб-перехватчики. получатели. Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) обеспечивает поддержку получения веб-перехватчиков, созданных веб-перехватчиками ASP.NET.

Вы можете найти поддержку для Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, временного резерва, stripe, Trello и WordPress, но можно поддерживать любое количество других поставщиков.

## <a name="configuring-a-webhook-receiver"></a>Настройка приемника веб-перехватчика

Приемники веб-перехватчика настраиваются с помощью [ивебхукрецеиверконфиг](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) реализовывать, а определенные реализации этого интерфейса можно зарегистрировать с помощью любой модели внедрения зависимостей. Реализация по умолчанию использует параметры приложения, которые могут быть заданы в файле Web. config, или, при использовании веб-приложений Azure, можно настроить на [портале Azure](https://portal.azure.com/).

![Параметры приложения Azure](_static/AzureAppSettings.png)

Для ключей параметров приложения используется следующий формат:

```
MS_WebHookReceiverSecret_<receiver>
```

Значение представляет собой разделенный запятыми список значений, соответствующих значениям *{ID}* , для которых зарегистрированы веб-перехватчики, например:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>Инициализация приемника веб-перехватчика

Приемники веб-перехватчика инициализируются путем их регистрации, как правило, в статическом классе *WebApiConfig* , например:

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
