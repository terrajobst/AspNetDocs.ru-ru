---
uid: web-api/overview/security/integrated-windows-authentication
title: Встроенная проверка подлинности Windows | Документация Майкрософт
author: MikeWasson
description: Описывает использование встроенной проверки подлинности Windows в веб-API ASP.NET.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: e4f31f191f3c0fabff308ea5dadb0f1d9ce7d448
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504210"
---
# <a name="integrated-windows-authentication"></a>Встроенная проверка подлинности Windows

по [Майк Уоссон](https://github.com/MikeWasson)

Встроенная проверка подлинности Windows позволяет пользователям выполнять вход с использованием учетных данных Windows, используя Kerberos или NTLM. Клиент отправляет учетные данные в заголовке авторизации. Проверка подлинности Windows лучше всего подходит для среды интрасети. Дополнительные сведения: [Проверка подлинности Windows](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).

| Преимущества | Недостатки |
| --- | --- |
| Встроенные в IIS. — Не отправляет учетные данные пользователя в запросе. — Если клиентский компьютер принадлежит домену (например, приложению интрасети), пользователю не нужно вводить учетные данные. | — Не рекомендуется для Интернет-приложений. — Требует поддержки Kerberos или NTLM в клиенте. -Клиент должен быть в домене Active Directory. |

> [!NOTE]
> Если ваше приложение размещено в Azure и имеется локальный домен Active Directory, рассмотрите возможность Федерации локального AD с Azure Active Directory. Таким образом пользователи смогут входить с использованием локальных учетных данных, но проверка подлинности выполняется Azure AD. Дополнительные сведения см. в статье [Проверка подлинности Azure](../../../visual-studio/overview/2012/windows-azure-authentication.md).

Чтобы создать приложение, использующее встроенную проверку подлинности Windows, выберите шаблон "приложение интрасети" в мастере проектов MVC 4. Этот шаблон проекта помещает в файл Web. config следующий параметр:

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

На стороне клиента встроенная проверка подлинности Windows работает с любым браузером, поддерживающим схему проверки подлинности [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) , которая включает большинство основных браузеров. Для клиентских приложений .NET класс **HttpClient** поддерживает проверку подлинности Windows:

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Проверка подлинности Windows уязвима для атак с подделкой межсайтовых запросов (CSRF). См. раздел [предотвращение атак с подделкой межсайтовых запросов (CSRF)](preventing-cross-site-request-forgery-csrf-attacks.md).
