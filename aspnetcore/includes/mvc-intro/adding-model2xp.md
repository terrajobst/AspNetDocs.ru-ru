---
ms.openlocfilehash: 0084d8c6bc5d16eaa1c3fa36d8aabb2aa31e1283
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029471"
---
<a name="cli"></a>
## <a name="perform-initial-migration"></a><span data-ttu-id="eab67-101">Выполнение первоначальной миграции</span><span class="sxs-lookup"><span data-stu-id="eab67-101">Perform initial migration</span></span>

<span data-ttu-id="eab67-102">Из командной строки выполните следующие команды интерфейса командной строки .NET Core.</span><span class="sxs-lookup"><span data-stu-id="eab67-102">From the command line, run the following .NET Core CLI commands:</span></span>

```console
dotnet ef migrations add InitialCreate
dotnet ef database update
```

<span data-ttu-id="eab67-103">Команда `dotnet ef migrations add InitialCreate` формирует код для создания схемы исходной базы данных.</span><span class="sxs-lookup"><span data-stu-id="eab67-103">The `dotnet ef migrations add InitialCreate` command generates code to create the initial database schema.</span></span> <span data-ttu-id="eab67-104">Схема создается на основе модели, указанной в `DbContext` (в файле *Models/MvcMovieContext.cs*).</span><span class="sxs-lookup"><span data-stu-id="eab67-104">The schema is based on the model specified in the `DbContext` (In the *Models/MvcMovieContext.cs* file).</span></span> <span data-ttu-id="eab67-105">Аргумент `Initial` используется для присвоения имен миграциям.</span><span class="sxs-lookup"><span data-stu-id="eab67-105">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="eab67-106">Можно использовать любое имя, но обычно выбирается имя, описывающее миграцию.</span><span class="sxs-lookup"><span data-stu-id="eab67-106">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="eab67-107">Дополнительные сведения см. в статье [Введение в миграции](xref:data/ef-mvc/migrations#introduction-to-migrations).</span><span class="sxs-lookup"><span data-stu-id="eab67-107">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="eab67-108">Команда `dotnet ef database update` выполняет `Up` метод в файле *Migrations/\<отметка-времени>_InitialCreate.cs*, который создает базу данных.</span><span class="sxs-lookup"><span data-stu-id="eab67-108">The `dotnet ef database update` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file, which creates the database.</span></span>
