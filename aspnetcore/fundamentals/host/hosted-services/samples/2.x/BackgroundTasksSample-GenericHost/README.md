---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056491"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a>Пример фоновых задач в ASP.NET Core (универсальный узел)

В этом примере демонстрируется использование [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice). В этом примере демонстрируются функции, описанные в разделе [Фоновые задачи с размещенными службами в ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services).

Если этот пример запускается в [Visual Studio Code](https://code.visualstudio.com/), в файле конфигурации консоли *.vscode/launch.json* задайте для параметра **console** значение `externalTerminal` или `integratedTerminal`. Значение `internalConsole` несовместимо с вводом данных в консоль через нажатие клавиш, который используется в приложении для постановки в очередь фоновых рабочих элементов.
