---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047421"
---
<span data-ttu-id="1e93d-101"><!-- THIS INCLUDE USED BY MVC AND RP -->Добавьте в класс `Movie` следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="1e93d-101"><!-- THIS INCLUDE USED BY MVC AND RP --> Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

<span data-ttu-id="1e93d-102">Класс `Movie` содержит:</span><span class="sxs-lookup"><span data-stu-id="1e93d-102">The `Movie` class contains:</span></span>

* <span data-ttu-id="1e93d-103">Поле `ID` является обязательным для первичного ключа базы данных.</span><span class="sxs-lookup"><span data-stu-id="1e93d-103">The `ID` field is required by the database for the primary key.</span></span>
* <span data-ttu-id="1e93d-104">`[DataType(DataType.Date)]`:  Атрибут [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) указывает тип данных (Date).</span><span class="sxs-lookup"><span data-stu-id="1e93d-104">`[DataType(DataType.Date)]`:  The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (Date).</span></span> <span data-ttu-id="1e93d-105">С этим атрибутом:</span><span class="sxs-lookup"><span data-stu-id="1e93d-105">With this attribute:</span></span>

  * <span data-ttu-id="1e93d-106">пользователю не требуется вводить сведения о времени в поле даты.</span><span class="sxs-lookup"><span data-stu-id="1e93d-106">The user is not required to enter time information in the date field.</span></span>
  * <span data-ttu-id="1e93d-107">Отображается только дата, а не время.</span><span class="sxs-lookup"><span data-stu-id="1e93d-107">Only the date is displayed, not time information.</span></span>

<span data-ttu-id="1e93d-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) рассматриваются в следующем руководстве.</span><span class="sxs-lookup"><span data-stu-id="1e93d-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) are covered in a later tutorial.</span></span>