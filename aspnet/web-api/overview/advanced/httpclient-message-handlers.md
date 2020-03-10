---
uid: web-api/overview/advanced/httpclient-message-handlers
title: Обработчики сообщений HttpClient в веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: Создание пользовательских обработчиков сообщений для веб-API ASP.NET в ASP.NET 4. x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449280"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a>Обработчики сообщений HttpClient в веб-API ASP.NET

по [Майк Уоссон](https://github.com/MikeWasson)

*Обработчик сообщений* — это класс, который получает HTTP-запрос и ВОЗВРАЩАЕТ ответ HTTP.

Как правило, ряд обработчиков сообщений объединяется в цепочку. Первый обработчик получает HTTP-запрос, выполняет некоторую обработку и передает запрос следующему обработчику. В какой-то момент ответ создается и помещается в резервную копию цепочки. Этот шаблон называется *делегированным* обработчиком.

![](httpclient-message-handlers/_static/image1.png)

На стороне клиента класс **HttpClient** использует обработчик сообщений для обработки запросов. Обработчик по умолчанию — **HttpClientHandler**, который отправляет запрос по сети и получает ответ от сервера. В клиентский конвейер можно вставлять пользовательские обработчики сообщений:

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> Веб-API ASP.NET также использует обработчики сообщений на стороне сервера. Дополнительные сведения см. в разделе [обработчики сообщений HTTP](http-message-handlers.md).

## <a name="custom-message-handlers"></a>Пользовательские обработчики сообщений

Для написания пользовательского обработчика сообщений следует использовать класс **System .NET. http. DelegatingHandler** и переопределить метод **SendAsync** . Вот так выглядит подпись метода.

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

Метод принимает **HttpRequestMessage** в качестве входных данных и асинхронно возвращает **HttpResponseMessage**. Типичная реализация выполняет следующие действия:

1. Обработать сообщение запроса.
2. Вызовите `base.SendAsync`, чтобы отправить запрос внутреннему обработчику.
3. Внутренний обработчик возвращает ответное сообщение. (Этот шаг является асинхронным.)
4. Обработайте ответ и верните его вызывающему объекту.

В следующем примере показан обработчик сообщений, который добавляет пользовательский заголовок к исходящему запросу:

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

Вызов к `base.SendAsync` выполняется асинхронно. Если после этого вызова обработчик выполняет какие – либо действия, используйте ключевое слово **await** , чтобы возобновить выполнение после завершения метода. В следующем примере показан обработчик, который записывает коды ошибок. Сам журнал не очень интересен, но в примере показано, как получить ответ внутри обработчика.

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>Добавление обработчиков сообщений в клиентский конвейер

Чтобы добавить пользовательские обработчики в **HttpClient**, используйте метод **хттпклиентфактори. Create** :

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

Обработчики сообщений вызываются в том порядке, в котором они передаются в метод **CREATE** . Так как обработчики являются вложенными, ответное сообщение перемещается в другое направление. То есть последний обработчик является первым, чтобы получить ответное сообщение.
