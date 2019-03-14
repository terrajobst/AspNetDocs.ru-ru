---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049111"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="caa43-101">Как построение и запуск образца данных безопасности пользователей</span><span class="sxs-lookup"><span data-stu-id="caa43-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="caa43-102">Задайте пароль с помощью диспетчера секретов:</span><span class="sxs-lookup"><span data-stu-id="caa43-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="caa43-103">Обновление базы данных:</span><span class="sxs-lookup"><span data-stu-id="caa43-103">Update the database:</span></span>

    `dotnet ef database update`

* <span data-ttu-id="caa43-104">Включение протокола HTTPS в проекте</span><span class="sxs-lookup"><span data-stu-id="caa43-104">Enable HTTPS in the project</span></span>
