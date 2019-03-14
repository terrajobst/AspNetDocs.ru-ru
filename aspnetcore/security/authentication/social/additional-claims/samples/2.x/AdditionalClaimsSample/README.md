---
ms.openlocfilehash: 09cd8e639238b998212b813cba5bc1aa85f36a75
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045581"
---
# <a name="aspnet-core-external-authentication-provider-additional-claims-sample-aspnet-core-2x"></a><span data-ttu-id="aed7c-101">ASP.NET Core внешнего поставщика проверки подлинности дополнительных утверждений образец (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="aed7c-101">ASP.NET Core External Authentication Provider Additional Claims Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="aed7c-102">В этом примере описывается установка дополнительные утверждения на основе данных пользователя Google, с помощью поставщика проверки подлинности Google.</span><span class="sxs-lookup"><span data-stu-id="aed7c-102">This sample illustrates establishing additional claims from Google user data using the Google authentication provider.</span></span> <span data-ttu-id="aed7c-103">Этот пример, прилагаемый к [сохранения дополнительные утверждения и маркеры от внешних поставщиков](https://docs.microsoft.com/aspnet/core/security/authentication/social/additional-claims).</span><span class="sxs-lookup"><span data-stu-id="aed7c-103">This sample accompanies [Persist additional claims and tokens from external providers](https://docs.microsoft.com/aspnet/core/security/authentication/social/additional-claims).</span></span>

<span data-ttu-id="aed7c-104">Для работы с образцом, укажите допустимый идентификатор клиента Google и секрет в `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="aed7c-104">To use the sample, provide a valid Google Client ID and Secret in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="aed7c-105">Дополнительные сведения см. в разделе [установки внешней учетной записи Google](https://docs.microsoft.com/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="aed7c-105">For more information, see [Google external login setup](https://docs.microsoft.com/aspnet/core/security/authentication/social/google-logins).</span></span>
