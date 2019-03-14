---
ms.openlocfilehash: 85fa9f8b18dc7dfb3e9d37703549dc5c28dc7a4a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062601"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>Модель создания фильма

* Выполните следующую команду в окне командной строки (в папке проекта, содержащей файлы *Program.cs*, *Startup.cs* и *.csproj*).

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

Если возникает ошибка.
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

Предыдущая ошибка возникает, когда вы находитесь в неверном каталоге. Откройте в командной оболочке папку проекта (папку, содержащую файлы *Program.cs*, *Startup.cs* и *.csproj*), а затем запустите предыдущую команду.

Если возникает ошибка.
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

Выйдите из Visual Studio и выполните команду еще раз.
