---
title: Функции запросов в ASP.NET Core
author: ardalis
description: Сведения о реализации веб-сервера, связанные с HTTP-запросами и откликами, определяемые в интерфейсах для ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: fundamentals/request-features
ms.openlocfilehash: d0f3ae521d1f314dd04cb581d9a921da4719273d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031261"
---
# <a name="request-features-in-aspnet-core"></a>Функции запросов в ASP.NET Core

Автор: [Стив Смит](https://ardalis.com/) (Steve Smith)

Сведения о реализации веб-сервера, связанные с HTTP-запросами и ответами, определяются в интерфейсах. Эти интерфейсы используются реализациями сервера и ПО промежуточного слоя для создания и изменения конвейера размещения приложения.

## <a name="feature-interfaces"></a>Интерфейсы функций

ASP.NET Core определяет несколько интерфейсов функций HTTP в `Microsoft.AspNetCore.Http.Features`, которые используются серверами для определения поддерживаемых ими функций. Следующие интерфейсы функций обрабатывают запросы и возвращают отклики:

`IHttpRequestFeature` определяет структуру HTTP-запроса, включая протокол, путь, строку запроса, заголовки и основной текст.

`IHttpResponseFeature` определяет структуру HTTP-отклика, включая код состояния, заголовки и основной текст отклика.

`IHttpAuthenticationFeature` определяет поддержку для идентификации пользователей на основе `ClaimsPrincipal` и указания обработчика проверки подлинности.

`IHttpUpgradeFeature` определяет поддержку для [обновлений HTTP](https://tools.ietf.org/html/rfc2616.html#section-14.42), позволяющих клиенту указать дополнительные протоколы, которые требуется использовать, когда серверу нужно сменить протоколы.

`IHttpBufferingFeature` определяет методы для отключения буферизации запросов и (или) откликов.

`IHttpConnectionFeature` определяет свойства для локальных и удаленных адресов и портов.

`IHttpRequestLifetimeFeature` определяет поддержку для прерывания подключений или обнаружения преждевременного завершения запроса, например при отключении клиента.

`IHttpSendFileFeature` определяет метод для асинхронной передачи файлов.

`IHttpWebSocketFeature` определяет API для поддержки веб-сокетов.

`IHttpRequestIdentifierFeature` добавляет свойство, которое можно реализовать для уникальной идентификации запросов.

`ISessionFeature` определяет абстрактные классы `ISessionFactory` и `ISession` для поддержки пользовательских сеансов.

`ITlsConnectionFeature` определяет API для получения сертификатов клиента.

`ITlsTokenBindingFeature` определяет методы для работы с параметрами привязки токена TLS.

> [!NOTE]
> `ISessionFeature` не является функцией сервера, но реализуется `SessionMiddleware` (см. раздел [Управление состоянием приложения](app-state.md)).

## <a name="feature-collections"></a>Коллекции функций

Свойство `Features` объекта `HttpContext` предоставляет интерфейс для получения и задания доступных функций HTTP для текущего запроса. Так как коллекция функций является изменяемой даже внутри контекста запроса, ПО промежуточного слоя можно использовать для изменения этой коллекции и добавления поддержки дополнительных функций.

## <a name="middleware-and-request-features"></a>ПО промежуточного слоя и функции запросов

Хотя серверы отвечают за создание коллекции функций, ПО промежуточного слоя может как добавлять элементы в эту коллекцию, так и использовать функции из нее. Например, `StaticFileMiddleware` обращается к функции `IHttpSendFileFeature`. Если функция существует, она используется для отправки запрашиваемого статического файла из его физического пути. В противном случае для отправки файла применяется более медленный альтернативный метод. Когда функция `IHttpSendFileFeature` доступна, она позволяет операционной системе открыть файл и выполнить прямое копирование в режиме ядра на сетевую карту.

Кроме того, ПО промежуточного слоя может добавлять элементы в коллекцию функций, заданную сервером. ПО промежуточного слоя даже может заменять существующие функции, что позволяет ему расширять функциональность сервера. Добавляемые в коллекцию функции сразу же становятся доступными другому ПО промежуточного слоя или самому базовому приложению на более позднем этапе конвейера.

Объединив пользовательские реализации сервера и улучшения ПО промежуточного слоя, можно создать именно тот набор функций, который необходим приложению. Это позволяет добавлять отсутствующие функции без внесения изменений на сервере, а также предоставлять лишь минимальный набор функций, что ограничивает направления атак и повышает производительность.

## <a name="summary"></a>Сводка

Интерфейсы функций определяют конкретные функции HTTP, которые может поддерживать указанный запрос. Серверы определяют коллекции функций и первоначальный набор функций, поддерживаемый этим сервером, но эти функции можно расширить с помощью ПО промежуточного слоя.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Серверы](xref:fundamentals/servers/index)
* [ПО промежуточного слоя](xref:fundamentals/middleware/index)
* [Открытый веб-интерфейс для .NET (OWIN)](xref:fundamentals/owin)