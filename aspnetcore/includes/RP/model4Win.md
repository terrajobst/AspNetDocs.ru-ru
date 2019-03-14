---
ms.openlocfilehash: 85fa9f8b18dc7dfb3e9d37703549dc5c28dc7a4a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062601"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="627d9-101">Модель создания фильма</span><span class="sxs-lookup"><span data-stu-id="627d9-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="627d9-102">Выполните следующую команду в окне командной строки (в папке проекта, содержащей файлы *Program.cs*, *Startup.cs* и *.csproj*).</span><span class="sxs-lookup"><span data-stu-id="627d9-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

<span data-ttu-id="627d9-103">Если возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="627d9-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="627d9-104">Предыдущая ошибка возникает, когда вы находитесь в неверном каталоге.</span><span class="sxs-lookup"><span data-stu-id="627d9-104">The preceeding error happens when you are in the wrong directory.</span></span> <span data-ttu-id="627d9-105">Откройте в командной оболочке папку проекта (папку, содержащую файлы *Program.cs*, *Startup.cs* и *.csproj*), а затем запустите предыдущую команду.</span><span class="sxs-lookup"><span data-stu-id="627d9-105">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files), and then run the preceeding command.</span></span>

<span data-ttu-id="627d9-106">Если возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="627d9-106">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="627d9-107">Выйдите из Visual Studio и выполните команду еще раз.</span><span class="sxs-lookup"><span data-stu-id="627d9-107">Exit Visual Studio and run the command again.</span></span>
