---
ms.openlocfilehash: 122088c1227df81114de77fd578769770c3f6fd1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045591"
---
# <a name="key-vault-configuration-provider-sample-app"></a>Хранилище ключей конфигурации поставщика примера приложения

В этом примере описывается использование поставщика конфигурации хранилища ключей Azure.

Пример выполняется в одном из двух режимов определяется `#define` инструкция в верхней части *Program.cs* файл. Инструкции см. в разделе [директивы препроцессора в образце кода](https://docs.microsoft.com/aspnet/core#preprocessor-directives-in-sample-code):

* `Basic` &ndash; Демонстрирует использование секрет и идентификатор клиента хранилища ключей Azure для доступа к секреты, хранящиеся в хранилище ключей Azure. Эта версия образца может выполняться из любого места, развернутых в службе приложений Azure или любом узле, может обслуживать приложения ASP.NET Core.
* `Managed` &ndash; Демонстрирует использование Azure [управляемое удостоверение службы](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) для проверки подлинности приложения в хранилище ключей Azure с аутентификацией Azure AD без учетных данных в коде или конфигурации приложения. Идентификатор клиента Azure AD и секрет не являются обязательными для приложения для проверки подлинности с хранилищем ключей Azure. В этом примере должны быть развернуты в службе приложений Azure для изучения scearnio управляемое удостоверение.

Дополнительные сведения см. в разделе [поставщик конфигурации Azure Key Vault](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration).
