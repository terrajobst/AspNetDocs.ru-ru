---
ms.openlocfilehash: 568fa161b27e554fd8b474670b8f9a7ec2f39f45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047131"
---
<span data-ttu-id="30e94-101">В следующей таблице представлены параметры генератора кода ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="30e94-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="30e94-102">Параметр</span><span class="sxs-lookup"><span data-stu-id="30e94-102">Parameter</span></span>               | <span data-ttu-id="30e94-103">Описание:</span><span class="sxs-lookup"><span data-stu-id="30e94-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="30e94-104">-m</span><span class="sxs-lookup"><span data-stu-id="30e94-104">-m</span></span>  | <span data-ttu-id="30e94-105">Имя модели</span><span class="sxs-lookup"><span data-stu-id="30e94-105">The name of the model.</span></span> |
| <span data-ttu-id="30e94-106">-dc</span><span class="sxs-lookup"><span data-stu-id="30e94-106">-dc</span></span>  | <span data-ttu-id="30e94-107">Контекст данных</span><span class="sxs-lookup"><span data-stu-id="30e94-107">The data context.</span></span> |
| <span data-ttu-id="30e94-108">-udl</span><span class="sxs-lookup"><span data-stu-id="30e94-108">-udl</span></span> | <span data-ttu-id="30e94-109">Использование макета по умолчанию</span><span class="sxs-lookup"><span data-stu-id="30e94-109">Use the default layout.</span></span> |
| <span data-ttu-id="30e94-110">--relativeFolderPath</span><span class="sxs-lookup"><span data-stu-id="30e94-110">--relativeFolderPath</span></span> | <span data-ttu-id="30e94-111">Относительный путь к папке выходных данных для создания представлений</span><span class="sxs-lookup"><span data-stu-id="30e94-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="30e94-112">--useDefaultLayout</span><span class="sxs-lookup"><span data-stu-id="30e94-112">--useDefaultLayout</span></span> | <span data-ttu-id="30e94-113">Макет по умолчанию следует использовать для представлений.</span><span class="sxs-lookup"><span data-stu-id="30e94-113">The default layout should be used for the views.</span></span> |
| <span data-ttu-id="30e94-114">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="30e94-114">--referenceScriptLibraries</span></span> | <span data-ttu-id="30e94-115">Добавляет `_ValidationScriptsPartial` для страниц редактирования и создания</span><span class="sxs-lookup"><span data-stu-id="30e94-115">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="30e94-116">Чтобы получить справку по команде `aspnet-codegenerator controller`, используйте коммутатор `h`.</span><span class="sxs-lookup"><span data-stu-id="30e94-116">Use the `h` switch to get help on the `aspnet-codegenerator controller` command:</span></span>

```console
dotnet aspnet-codegenerator controller -h
```