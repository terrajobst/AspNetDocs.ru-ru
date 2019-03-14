---
ms.openlocfilehash: 6096c5a1d5d99222cdc207ffb881406699e2ba76
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57055721"
---

Visual Studio отображает следующее диалоговое окно.

![Этот проект настроен для использования SSL. Чтобы избежать предупреждений о SSL в браузере, вы можете сделать самозаверяющий сертификат, созданный IIS Express, доверенным. Вы хотите сделать SSL-сертификат IIS Express доверенным?](~/getting-started/_static/trustCert.png)

Выберите **Да**, чтобы сделать SSL-сертификат IIS Express доверенным.

Отобразится следующее диалоговое окно.

![Диалоговое окно "Предупреждение о безопасности"](~/getting-started/_static/cert.png)

Выберите **Да**, если согласны доверять сертификату разработки.

Дополнительные сведения см. в разделе [Настройка доверия к сертификату разработки HTTPS ASP.NET Core](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos).