---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049111"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a>Как построение и запуск образца данных безопасности пользователей

* Задайте пароль с помощью диспетчера секретов:

  `dotnet user-secrets set SeedUserPW <pw>`

* Обновление базы данных:

    `dotnet ef database update`

* Включение протокола HTTPS в проекте
