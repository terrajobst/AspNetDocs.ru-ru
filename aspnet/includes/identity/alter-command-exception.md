---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57188721"
---
> <span data-ttu-id="eeea8-101">Некоторые команды не поддерживаются, если приложение использует SQLite в качестве хранилища данных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="eeea8-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="eeea8-102">Из-за ограничений в компоненте database engine `Alter` команды создавать следующие исключения:</span><span class="sxs-lookup"><span data-stu-id="eeea8-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="eeea8-103">"System.NotSupportedException: SQLite не поддерживает эту операцию миграции.»</span><span class="sxs-lookup"><span data-stu-id="eeea8-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="eeea8-104">Решения запустите Code First migrations для изменения таблиц базы данных.</span><span class="sxs-lookup"><span data-stu-id="eeea8-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
