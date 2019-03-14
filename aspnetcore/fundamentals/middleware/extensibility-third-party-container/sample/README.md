---
ms.openlocfilehash: 282871e5db197dfb4226cc02918f2d6ba1135c04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045601"
---
# <a name="aspnet-core-middleware-extensibility-sample"></a><span data-ttu-id="cd306-101">Пример расширяемости ПО промежуточного слоя ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cd306-101">ASP.NET Core Middleware Extensibility Sample</span></span>

<span data-ttu-id="cd306-102">В этом примере описывается использование [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) и [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) со сторонним контейнером внедрения зависимостей, [Simple Injector](https://simpleinjector.org).</span><span class="sxs-lookup"><span data-stu-id="cd306-102">This sample illustrates the use of [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) and [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) with a 3rd party dependency injection container, [Simple Injector](https://simpleinjector.org).</span></span> <span data-ttu-id="cd306-103">Пример демонстрирует использование функций, описанных в статье [Активация ПО промежуточного слоя с помощью контейнера сторонних разработчиков в ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container).</span><span class="sxs-lookup"><span data-stu-id="cd306-103">This sample demonstrates the features described in [Middleware activation with a third-party container in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container).</span></span>
