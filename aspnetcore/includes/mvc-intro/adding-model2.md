---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044081"
---
## <a name="add-initial-migration-and-update-the-database"></a><span data-ttu-id="c062f-101">Добавления первоначальной миграции и обновления базы данных</span><span class="sxs-lookup"><span data-stu-id="c062f-101">Add initial migration and update the database</span></span>

* <span data-ttu-id="c062f-102">Откройте командную строку и перейдите в каталог проекта.</span><span class="sxs-lookup"><span data-stu-id="c062f-102">Open a command prompt and navigate to the project directory.</span></span> <span data-ttu-id="c062f-103">(Каталог, содержащий *Startup.cs* файла).</span><span class="sxs-lookup"><span data-stu-id="c062f-103">(The directory containing the *Startup.cs* file).</span></span>

* <span data-ttu-id="c062f-104">В командной строке выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c062f-104">Run the following commands in the command prompt:</span></span>

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  <span data-ttu-id="c062f-105">[.NET core](/dotnet/core/tools/index) — это кроссплатформенная реализация .NET.</span><span class="sxs-lookup"><span data-stu-id="c062f-105">[.NET Core](/dotnet/core/tools/index) is a cross-platform implementation of .NET.</span></span> <span data-ttu-id="c062f-106">Вот, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c062f-106">Here is what these commands do:</span></span>

  * <span data-ttu-id="c062f-107">[Команда DotNet restore](/dotnet/core/tools/dotnet-restore): Файлы для загрузки пакетов NuGet, указанных в *.csproj* файл.</span><span class="sxs-lookup"><span data-stu-id="c062f-107">[dotnet restore](/dotnet/core/tools/dotnet-restore): Downloads the NuGet packages specified in the *.csproj* file.</span></span>
  * <span data-ttu-id="c062f-108">`dotnet ef migrations add Initial` Выполняет команду миграций Entity Framework .NET Core CLI и создает первоначальной миграции.</span><span class="sxs-lookup"><span data-stu-id="c062f-108">`dotnet ef migrations add Initial` Runs the Entity Framework .NET Core CLI migrations command and creates the initial migration.</span></span> <span data-ttu-id="c062f-109">Параметр после «add» является имя, присвоенное миграции.</span><span class="sxs-lookup"><span data-stu-id="c062f-109">The parameter after "add" is a name that you assign to the migration.</span></span> <span data-ttu-id="c062f-110">Здесь присвоении миграции «Начальный» так как он является перенос исходной базы данных.</span><span class="sxs-lookup"><span data-stu-id="c062f-110">Here you're naming the migration "Initial" because it's the initial database migration.</span></span> <span data-ttu-id="c062f-111">Эта операция создает *миграций / /\<даты времени > _Initial.cs* файл, содержащий команды миграции, чтобы добавить *фильма* таблице в базе данных.</span><span class="sxs-lookup"><span data-stu-id="c062f-111">This operation creates the *Data/Migrations/\<date-time>_Initial.cs* file containing the migration commands to add the *Movie* table to the database.</span></span>
  * <span data-ttu-id="c062f-112">`dotnet ef database update`  Обновляет базу данных миграции, который мы только что создали.</span><span class="sxs-lookup"><span data-stu-id="c062f-112">`dotnet ef database update`  Updates the database with the migration we just created.</span></span>

<span data-ttu-id="c062f-113">Вы узнаете о базе данных и строку подключения в следующем учебном курсе.</span><span class="sxs-lookup"><span data-stu-id="c062f-113">You'll learn about the database and connection string in the next tutorial.</span></span> <span data-ttu-id="c062f-114">Вы узнаете об изменениях модели данных в [добавить поле](xref:tutorials/first-mvc-app/new-field) руководства.</span><span class="sxs-lookup"><span data-stu-id="c062f-114">You'll learn about data model changes in the [Add a field](xref:tutorials/first-mvc-app/new-field) tutorial.</span></span>
