---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062721"
---
# <a name="aspnet-core-response-caching-sample"></a>Пример кэширования ответа ASP.NET Core

В этом примере описывается использование ASP.NET Core [по промежуточного слоя, кэширование ответов](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).

Приложение отвечает его страницы индекса, включая `Cache-Control` заголовок, чтобы настроить поведение кэширования. Приложение также задает `Vary` заголовка для настройки кэша для использования в ответе, только если `Accept-Encoding` заголовок последующих запросов соответствие исходного запроса.

При выполнении этого образца, на страницу индекса обрабатывается из кэша при сохранении и кэшируются до 10 секунд.
