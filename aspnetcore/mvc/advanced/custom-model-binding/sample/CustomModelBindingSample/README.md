---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059641"
---
# <a name="custom-model-binding-demo"></a><span data-ttu-id="37c8b-101">Демонстрация пользовательской привязки модели</span><span class="sxs-lookup"><span data-stu-id="37c8b-101">Custom Model Binding Demo</span></span>

<span data-ttu-id="37c8b-102">Протестируйте `ByteArrayModelBinder`, запустив приложение и выполнив запрос POST для размещения строки в кодировке base64 в конечной точке `ImageController` (`/api/image/`).</span><span class="sxs-lookup"><span data-stu-id="37c8b-102">Test `ByteArrayModelBinder` by running the app and POSTing a base64-encoded string to the `ImageController` endpoint (`/api/image/`).</span></span> <span data-ttu-id="37c8b-103">В тексте запроса необходимо задать свойства файла и имени файла в виде данных формы (с помощью [Postman](https://www.getpostman.com/) или аналогичного средства).</span><span class="sxs-lookup"><span data-stu-id="37c8b-103">Specify the file and filename properties in the request body as form-data (using [Postman](https://www.getpostman.com/) or a similar tool).</span></span> <span data-ttu-id="37c8b-104">Можно использовать [этот пример строки](Base64String.txt).</span><span class="sxs-lookup"><span data-stu-id="37c8b-104">You can use [this sample string](Base64String.txt).</span></span> <span data-ttu-id="37c8b-105">Результат будет сохранен в папке *wwwroot/images/upload* под указанным именем файла.</span><span class="sxs-lookup"><span data-stu-id="37c8b-105">The result is saved in the *wwwroot/images/upload* folder with the filename specified.</span></span>

<span data-ttu-id="37c8b-106">Чтобы проверить пример пользовательской привязки, попробуйте следующие конечные точки:</span><span class="sxs-lookup"><span data-stu-id="37c8b-106">To test the custom binding example, try the following endpoints:</span></span>

* <span data-ttu-id="37c8b-107">/api/authors/1</span><span class="sxs-lookup"><span data-stu-id="37c8b-107">/api/authors/1</span></span>
* <span data-ttu-id="37c8b-108">/api/authors/2 (NOT FOUND)</span><span class="sxs-lookup"><span data-stu-id="37c8b-108">/api/authors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="37c8b-109">/api/boundauthors/1</span><span class="sxs-lookup"><span data-stu-id="37c8b-109">/api/boundauthors/1</span></span>
* <span data-ttu-id="37c8b-110">/api/boundauthors/2 (NOT FOUND)</span><span class="sxs-lookup"><span data-stu-id="37c8b-110">/api/boundauthors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="37c8b-111">/api/boundauthors/get/1</span><span class="sxs-lookup"><span data-stu-id="37c8b-111">/api/boundauthors/get/1</span></span>
* <span data-ttu-id="37c8b-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; Это действие не проверяет значения NULL и возвращает *404 Не найдено*.</span><span class="sxs-lookup"><span data-stu-id="37c8b-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; This action doesn't check for null and returns a *404 Not Found*.</span></span>
