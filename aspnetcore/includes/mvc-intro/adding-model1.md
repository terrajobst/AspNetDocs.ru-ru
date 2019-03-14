---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038871"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="f504d-101">Добавление модели в приложение MVC ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f504d-101">Add a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="f504d-102">Авторы: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson) и [Том Дайкстра](https://github.com/tdykstra) (Tom Dykstra)</span><span class="sxs-lookup"><span data-stu-id="f504d-102">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="f504d-103">В этом разделе мы добавим некоторые классы для управления фильмами в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f504d-103">In this section, you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="f504d-104">Эти классы будут представлять уровень **м**одели в приложении **M**VC.</span><span class="sxs-lookup"><span data-stu-id="f504d-104">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="f504d-105">Эти классы используются в [Entity Framework Core](/ef/core) (EF Core) для работы с базой данных.</span><span class="sxs-lookup"><span data-stu-id="f504d-105">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="f504d-106">EF Core —это платформа объектно реляционного сопоставления (ORM), которая позволяет упростить необходимый код доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="f504d-106">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span> <span data-ttu-id="f504d-107">[EF Core поддерживает множество систем баз данных](/ef/core/providers/).</span><span class="sxs-lookup"><span data-stu-id="f504d-107">[EF Core supports many database engines](/ef/core/providers/).</span></span>

<span data-ttu-id="f504d-108">Создаваемые вами классы моделей называются классами POCO (от "plain old CLR objects" — старые добрые объекты CLR), так как они не зависят от EF Core.</span><span class="sxs-lookup"><span data-stu-id="f504d-108">The model classes you'll create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="f504d-109">Эти классы просто определяют свойства данных, которые будут храниться в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f504d-109">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="f504d-110">Работая с этим учебником, вы напишете классы моделей, а затем EF Core создаст базу данных.</span><span class="sxs-lookup"><span data-stu-id="f504d-110">In this tutorial you'll write the model classes first, and EF Core will create the database.</span></span> <span data-ttu-id="f504d-111">Другой вариант, который здесь не рассматривается, состоит в создании классов моделей из уже существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="f504d-111">An alternate approach not covered here is to generate model classes from an already-existing database.</span></span> <span data-ttu-id="f504d-112">Дополнительные сведения об этом подходе см. в разделе [ASP.NET Core — существующая база данных](/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="f504d-112">For information about that approach, see [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="f504d-113">Добавление класса модели данных</span><span class="sxs-lookup"><span data-stu-id="f504d-113">Add a data model class</span></span>
