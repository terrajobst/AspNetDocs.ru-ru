---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062721"
---
# <a name="aspnet-core-response-caching-sample"></a><span data-ttu-id="6dcdb-101">Пример кэширования ответа ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="6dcdb-101">ASP.NET Core Response Caching Sample</span></span>

<span data-ttu-id="6dcdb-102">В этом примере описывается использование ASP.NET Core [по промежуточного слоя, кэширование ответов](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span><span class="sxs-lookup"><span data-stu-id="6dcdb-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span></span>

<span data-ttu-id="6dcdb-103">Приложение отвечает его страницы индекса, включая `Cache-Control` заголовок, чтобы настроить поведение кэширования.</span><span class="sxs-lookup"><span data-stu-id="6dcdb-103">The app responds with its Index page, including a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="6dcdb-104">Приложение также задает `Vary` заголовка для настройки кэша для использования в ответе, только если `Accept-Encoding` заголовок последующих запросов соответствие исходного запроса.</span><span class="sxs-lookup"><span data-stu-id="6dcdb-104">The app also sets the `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="6dcdb-105">При выполнении этого образца, на страницу индекса обрабатывается из кэша при сохранении и кэшируются до 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="6dcdb-105">When running the sample, the Index page is served from cache when stored and cached for up to 10 seconds.</span></span>
