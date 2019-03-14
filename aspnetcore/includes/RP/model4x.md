---
ms.openlocfilehash: d875717d480fe234ac5a328493fcec6a268e37a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039521"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>Модель создания фильма

* Выполните следующую команду в окне командной строки (в папке проекта, содержащей файлы *Program.cs*, *Startup.cs* и *.csproj*).

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

Если возникает ошибка.
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

Откройте в командной оболочке папку проекта (папку, содержащую файлы *Program.cs*, *Startup.cs* и *.csproj*).
