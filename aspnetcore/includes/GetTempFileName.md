---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165864"
---
**Предупреждение**: В следующем коде используется `GetTempFileName`, какие вызывает `IOException` Если превышает 65535 файлы создаются без удаления предыдущей временные файлы. Реальное приложение должно удалить временные файлы или использовать `GetTempPath` и `GetRandomFileName` для создания имен временных файлов. Существует ограничение в 65 535 файлов на сервер, поэтому другое приложение на сервере может использовать максимум 65 535 файлов. 