---
ms.openlocfilehash: 4d6b6309e6e15c364542b5d3ae296d53c6ea4358
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037401"
---
<span data-ttu-id="72b02-101">Созданный код базы данных удостоверений требует [Entity Framework Core Migrations](/ef/core/managing-schemas/migrations/).</span><span class="sxs-lookup"><span data-stu-id="72b02-101">The generated Identity database code requires [Entity Framework Core Migrations](/ef/core/managing-schemas/migrations/).</span></span> <span data-ttu-id="72b02-102">Создание миграции и обновления базы данных.</span><span class="sxs-lookup"><span data-stu-id="72b02-102">Create a migration and update the database.</span></span> <span data-ttu-id="72b02-103">Например выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="72b02-103">For example, run the following commands:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="72b02-104">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72b02-104">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="72b02-105">В Visual Studio **консоль диспетчера пакетов**:</span><span class="sxs-lookup"><span data-stu-id="72b02-105">In the Visual Studio **Package Manager Console**:</span></span>

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="72b02-106">Интерфейс командной строки .NET Core</span><span class="sxs-lookup"><span data-stu-id="72b02-106">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

<span data-ttu-id="72b02-107">Параметр name «CreateIdentitySchema» для `Add-Migration` команда может быть произвольным.</span><span class="sxs-lookup"><span data-stu-id="72b02-107">The "CreateIdentitySchema" name parameter for the `Add-Migration` command is arbitrary.</span></span> <span data-ttu-id="72b02-108">`"CreateIdentitySchema"` содержит описание миграции.</span><span class="sxs-lookup"><span data-stu-id="72b02-108">`"CreateIdentitySchema"` describes the migration.</span></span>
