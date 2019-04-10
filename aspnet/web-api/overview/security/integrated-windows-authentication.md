---
uid: web-api/overview/security/integrated-windows-authentication
title: Встроенная проверка подлинности Windows | Документация Майкрософт
author: MikeWasson
description: Описывает использование встроенной проверки подлинности Windows в ASP.NET Web API.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: ce845eb6c914321736d77e989f10344eb7596eba
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59416835"
---
# <a name="integrated-windows-authentication"></a>Встроенная проверка подлинности Windows

по [Майк Уоссон](https://github.com/MikeWasson)

Встроенная проверка подлинности Windows позволяет пользователям войти, используя свои учетные данные Windows, с помощью Kerberos или NTLM. Клиент отправляет учетные данные в заголовке авторизации. Проверка подлинности Windows лучше всего подходит для среды интрасети. Дополнительные сведения: [Проверка подлинности Windows](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).

| Преимущества | Недостатки |
| --- | --- |
| -Встроены в IIS. -Не отправляет учетные данные пользователя в запросе. — Если клиентский компьютер принадлежит к домену (например, приложение интрасети), пользователю не нужно вводить учетные данные. | -Не рекомендуется для Интернет-приложений. — Требует поддержки Kerberos или NTLM в клиенте. -Клиент должен находиться в домене Active Directory. |

> [!NOTE]
> Если приложение размещено в Azure, и у вас есть домен Active Directory на предприятии, рассмотрите возможность федерации в локальной AD с Azure Active Directory. Таким образом, пользователи могут входить с использованием учетных данных на предприятии, но выполняется проверка подлинности с помощью Azure AD. Дополнительные сведения см. в разделе [проверки подлинности Azure](../../../visual-studio/overview/2012/windows-azure-authentication.md).


Чтобы создать приложение, использующее Windows интегрированной проверки подлинности, выберите шаблон «Приложение интрасети» в мастере проектов MVC 4. Этот шаблон проекта помещает следующий параметр в файле Web.config:

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

На стороне клиента, проверки подлинности встроенная Windows работает с помощью любого браузера, поддерживающего [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) схему проверки подлинности, которая включает в себя большинства популярных браузеров. Для клиентских приложений .NET **HttpClient** класс поддерживает проверку подлинности Windows:

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Проверка подлинности Windows является уязвимым для атак с подделкой межсайтовых. См. в разделе [атак с подделкой межсайтовых запросов](preventing-cross-site-request-forgery-csrf-attacks.md).
