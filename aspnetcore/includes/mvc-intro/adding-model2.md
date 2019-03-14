---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044081"
---
## <a name="add-initial-migration-and-update-the-database"></a>Добавления первоначальной миграции и обновления базы данных

* Откройте командную строку и перейдите в каталог проекта. (Каталог, содержащий *Startup.cs* файла).

* В командной строке выполните следующие команды:

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  [.NET core](/dotnet/core/tools/index) — это кроссплатформенная реализация .NET. Вот, выполните следующие команды:

  * [Команда DotNet restore](/dotnet/core/tools/dotnet-restore): Файлы для загрузки пакетов NuGet, указанных в *.csproj* файл.
  * `dotnet ef migrations add Initial` Выполняет команду миграций Entity Framework .NET Core CLI и создает первоначальной миграции. Параметр после «add» является имя, присвоенное миграции. Здесь присвоении миграции «Начальный» так как он является перенос исходной базы данных. Эта операция создает *миграций / /\<даты времени > _Initial.cs* файл, содержащий команды миграции, чтобы добавить *фильма* таблице в базе данных.
  * `dotnet ef database update`  Обновляет базу данных миграции, который мы только что создали.

Вы узнаете о базе данных и строку подключения в следующем учебном курсе. Вы узнаете об изменениях модели данных в [добавить поле](xref:tutorials/first-mvc-app/new-field) руководства.
