---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57188721"
---
> Некоторые команды не поддерживаются, если приложение использует SQLite в качестве хранилища данных удостоверений. Из-за ограничений в компоненте database engine `Alter` команды создавать следующие исключения:
>
> "System.NotSupportedException: SQLite не поддерживает эту операцию миграции.» 
>
> Решения запустите Code First migrations для изменения таблиц базы данных.
