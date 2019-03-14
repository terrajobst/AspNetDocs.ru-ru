---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059641"
---
# <a name="custom-model-binding-demo"></a>Демонстрация пользовательской привязки модели

Протестируйте `ByteArrayModelBinder`, запустив приложение и выполнив запрос POST для размещения строки в кодировке base64 в конечной точке `ImageController` (`/api/image/`). В тексте запроса необходимо задать свойства файла и имени файла в виде данных формы (с помощью [Postman](https://www.getpostman.com/) или аналогичного средства). Можно использовать [этот пример строки](Base64String.txt). Результат будет сохранен в папке *wwwroot/images/upload* под указанным именем файла.

Чтобы проверить пример пользовательской привязки, попробуйте следующие конечные точки:

* /api/authors/1
* /api/authors/2 (NOT FOUND)
* /api/boundauthors/1
* /api/boundauthors/2 (NOT FOUND)
* /api/boundauthors/get/1
* /api/boundauthors/get/2 (NO CONTENT) &ndash; Это действие не проверяет значения NULL и возвращает *404 Не найдено*.
