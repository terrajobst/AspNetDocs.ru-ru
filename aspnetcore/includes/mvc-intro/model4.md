---
ms.openlocfilehash: 568fa161b27e554fd8b474670b8f9a7ec2f39f45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047131"
---
В следующей таблице представлены параметры генератора кода ASP.NET Core.

| Параметр               | Описание:|
| ----------------- | ------------ |
| -m  | Имя модели |
| -dc  | Контекст данных |
| -udl | Использование макета по умолчанию |
| --relativeFolderPath | Относительный путь к папке выходных данных для создания представлений |
| --useDefaultLayout | Макет по умолчанию следует использовать для представлений. |
| --referenceScriptLibraries | Добавляет `_ValidationScriptsPartial` для страниц редактирования и создания |

Чтобы получить справку по команде `aspnet-codegenerator controller`, используйте коммутатор `h`.

```console
dotnet aspnet-codegenerator controller -h
```