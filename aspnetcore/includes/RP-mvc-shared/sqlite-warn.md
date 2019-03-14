---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048221"
---

> [!NOTE]
> <span data-ttu-id="b18f1-101">Многие операции изменения схемы не поддерживаются поставщиком EF Core SQLite.</span><span class="sxs-lookup"><span data-stu-id="b18f1-101">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="b18f1-102">Например, добавление столбца поддерживается, но удаление столбца не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b18f1-102">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="b18f1-103">Если создается миграции, чтобы удалить столбец, `ef migrations add` команда выполняется успешно, но `ef database update` из команд завершается неуспешно.</span><span class="sxs-lookup"><span data-stu-id="b18f1-103">If a migration is created to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="b18f1-104">Некоторые из этих ограничений можно устранить, написании кода миграций для перестроения таблицы вручную.</span><span class="sxs-lookup"><span data-stu-id="b18f1-104">Some of these limitations can be overcome by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="b18f1-105">Перестройка таблицы включает в себя:</span><span class="sxs-lookup"><span data-stu-id="b18f1-105">A table rebuild involves:</span></span>

>* <span data-ttu-id="b18f1-106">Переименование существующей таблицы.</span><span class="sxs-lookup"><span data-stu-id="b18f1-106">Renaming the existing table.</span></span>
>* <span data-ttu-id="b18f1-107">Создание новой таблицы.</span><span class="sxs-lookup"><span data-stu-id="b18f1-107">Creating a new table.</span></span>
>* <span data-ttu-id="b18f1-108">Копирование данных из старой таблицы в новую таблицу.</span><span class="sxs-lookup"><span data-stu-id="b18f1-108">Copying data from the old table to the new table.</span></span>
>* <span data-ttu-id="b18f1-109">Удаление старого таблицы.</span><span class="sxs-lookup"><span data-stu-id="b18f1-109">Dropping the old table.</span></span>

<span data-ttu-id="b18f1-110">Дополнительные сведения см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="b18f1-110">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="b18f1-111">Ограничения поставщика базы данных SQLite EF Core</span><span class="sxs-lookup"><span data-stu-id="b18f1-111">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="b18f1-112">Настройка кода миграции</span><span class="sxs-lookup"><span data-stu-id="b18f1-112">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="b18f1-113">Присвоение начальных значений данных</span><span class="sxs-lookup"><span data-stu-id="b18f1-113">Data seeding</span></span>](/ef/core/modeling/data-seeding)