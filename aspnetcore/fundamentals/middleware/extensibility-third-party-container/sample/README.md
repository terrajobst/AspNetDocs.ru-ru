---
ms.openlocfilehash: 282871e5db197dfb4226cc02918f2d6ba1135c04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045601"
---
# <a name="aspnet-core-middleware-extensibility-sample"></a>Пример расширяемости ПО промежуточного слоя ASP.NET Core

В этом примере описывается использование [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) и [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) со сторонним контейнером внедрения зависимостей, [Simple Injector](https://simpleinjector.org). Пример демонстрирует использование функций, описанных в статье [Активация ПО промежуточного слоя с помощью контейнера сторонних разработчиков в ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container).
