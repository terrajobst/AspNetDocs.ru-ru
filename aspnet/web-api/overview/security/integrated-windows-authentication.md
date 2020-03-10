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
# <a name="integrated-windows-authentication"></a><span data-ttu-id="8bfe8-103">Встроенная проверка подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="8bfe8-103">Integrated Windows Authentication</span></span>

<span data-ttu-id="8bfe8-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8bfe8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8bfe8-105">Встроенная проверка подлинности Windows позволяет пользователям выполнять вход с использованием учетных данных Windows, используя Kerberos или NTLM.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="8bfe8-106">Клиент отправляет учетные данные в заголовке авторизации.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="8bfe8-107">Проверка подлинности Windows лучше всего подходит для среды интрасети.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="8bfe8-108">Дополнительные сведения: [Проверка подлинности Windows](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span><span class="sxs-lookup"><span data-stu-id="8bfe8-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="8bfe8-109">Преимущества</span><span class="sxs-lookup"><span data-stu-id="8bfe8-109">Advantages</span></span> | <span data-ttu-id="8bfe8-110">Недостатки</span><span class="sxs-lookup"><span data-stu-id="8bfe8-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="8bfe8-111">Встроенные в IIS.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-111">- Built into IIS.</span></span> <span data-ttu-id="8bfe8-112">— Не отправляет учетные данные пользователя в запросе.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-112">- Does not send the user credentials in the request.</span></span> <span data-ttu-id="8bfe8-113">— Если клиентский компьютер принадлежит домену (например, приложению интрасети), пользователю не нужно вводить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-113">- If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="8bfe8-114">— Не рекомендуется для Интернет-приложений.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-114">- Not recommended for Internet applications.</span></span> <span data-ttu-id="8bfe8-115">— Требует поддержки Kerberos или NTLM в клиенте.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-115">- Requires Kerberos or NTLM support in the client.</span></span> <span data-ttu-id="8bfe8-116">-Клиент должен быть в домене Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-116">- Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="8bfe8-117">Если ваше приложение размещено в Azure и имеется локальный домен Active Directory, рассмотрите возможность Федерации локального AD с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="8bfe8-118">Таким образом пользователи смогут входить с использованием локальных учетных данных, но проверка подлинности выполняется Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="8bfe8-119">Дополнительные сведения см. в статье [Проверка подлинности Azure](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8bfe8-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>

<span data-ttu-id="8bfe8-120">Чтобы создать приложение, использующее встроенную проверку подлинности Windows, выберите шаблон "приложение интрасети" в мастере проектов MVC 4.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="8bfe8-121">Этот шаблон проекта помещает в файл Web. config следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="8bfe8-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="8bfe8-122">На стороне клиента встроенная проверка подлинности Windows работает с любым браузером, поддерживающим схему проверки подлинности [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) , которая включает большинство основных браузеров.</span><span class="sxs-lookup"><span data-stu-id="8bfe8-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="8bfe8-123">Для клиентских приложений .NET класс **HttpClient** поддерживает проверку подлинности Windows:</span><span class="sxs-lookup"><span data-stu-id="8bfe8-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="8bfe8-124">Проверка подлинности Windows уязвима для атак с подделкой межсайтовых запросов (CSRF).</span><span class="sxs-lookup"><span data-stu-id="8bfe8-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="8bfe8-125">См. раздел [предотвращение атак с подделкой межсайтовых запросов (CSRF)](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="8bfe8-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
