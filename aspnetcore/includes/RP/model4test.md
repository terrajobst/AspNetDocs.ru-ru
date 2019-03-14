---
ms.openlocfilehash: 22c540058e0b3b9ae612f1b2612cecc08627ea2b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063991"
---
<a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="e700b-101">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="e700b-101">Test the app</span></span>

* <span data-ttu-id="e700b-102">Запустите приложение и добавьте `/Movies` к URL-адресу в браузере (`http://localhost:port/movies`).</span><span class="sxs-lookup"><span data-stu-id="e700b-102">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="e700b-103">Протестируйте ссылку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e700b-103">Test the **Create** link.</span></span>

  ![Страница "Создать"](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="e700b-105">Протестируйте ссылки **Изменить**, **Сведения** и **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="e700b-105">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="e700b-106">Если появляется следующая ошибка, выполните миграции и обновите базу данных.</span><span class="sxs-lookup"><span data-stu-id="e700b-106">If you get the following error, verify you have run migrations and updated the database:</span></span>

```
An unhandled exception occurred while processing the request.
SqliteException: SQLite Error 1: 'no such table: Movie'.
Microsoft.Data.Sqlite.SqliteException.ThrowExceptionForRC(int rc, sqlite3 db)
```
