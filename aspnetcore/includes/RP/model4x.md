---
ms.openlocfilehash: d875717d480fe234ac5a328493fcec6a268e37a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039521"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="1e67c-101">Модель создания фильма</span><span class="sxs-lookup"><span data-stu-id="1e67c-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="1e67c-102">Выполните следующую команду в окне командной строки (в папке проекта, содержащей файлы *Program.cs*, *Startup.cs* и *.csproj*).</span><span class="sxs-lookup"><span data-stu-id="1e67c-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

<span data-ttu-id="1e67c-103">Если возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="1e67c-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="1e67c-104">Откройте в командной оболочке папку проекта (папку, содержащую файлы *Program.cs*, *Startup.cs* и *.csproj*).</span><span class="sxs-lookup"><span data-stu-id="1e67c-104">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
