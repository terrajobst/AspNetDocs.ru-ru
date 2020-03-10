---
uid: web-api/overview/security/basic-authentication
title: Обычная проверка подлинности в веб-API ASP.NET | Документация Майкрософт
author: MikeWasson
description: Описывает использование обычной проверки подлинности в веб-API ASP.NET.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447636"
---
# <a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="2bcb8-103">Обычная проверка подлинности в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2bcb8-103">Basic Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="2bcb8-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2bcb8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2bcb8-105">Обычная проверка подлинности определяется в [RFC 2617, проверка подлинности HTTP: обычная и дайджест-проверка подлинности](http://www.ietf.org/rfc/rfc2617.txt).</span><span class="sxs-lookup"><span data-stu-id="2bcb8-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="2bcb8-106">Недостатки</span><span class="sxs-lookup"><span data-stu-id="2bcb8-106">Disadvantages</span></span>

- <span data-ttu-id="2bcb8-107">Учетные данные пользователя отправляются в запросе.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="2bcb8-108">Учетные данные отправляются в виде открытого текста.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="2bcb8-109">Учетные данные отправляются при каждом запросе.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="2bcb8-110">Нет способа выйти из сеанса, за исключением случаев, когда завершается сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="2bcb8-111">Уязвимо для подделки запросов между сайтами (CSRF); требуются меры по борьбе с CSRF.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="2bcb8-112">Преимущества</span><span class="sxs-lookup"><span data-stu-id="2bcb8-112">Advantages</span></span>

- <span data-ttu-id="2bcb8-113">Стандартный Интернет.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-113">Internet standard.</span></span>
- <span data-ttu-id="2bcb8-114">Поддерживается всеми основными браузерами.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="2bcb8-115">Относительно простой протокол.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-115">Relatively simple protocol.</span></span>

<span data-ttu-id="2bcb8-116">Обычная проверка подлинности работает следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="2bcb8-117">Если для запроса требуется проверка подлинности, сервер возвращает 401 (несанкционированный).</span><span class="sxs-lookup"><span data-stu-id="2bcb8-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="2bcb8-118">Ответ включает заголовок WWW-Authenticate, указывающий, что сервер поддерживает обычную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="2bcb8-119">Клиент отправляет другой запрос с учетными данными клиента в заголовке авторизации.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="2bcb8-120">Учетные данные форматируются как строка "имя: пароль" в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="2bcb8-121">Учетные данные не шифруются.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="2bcb8-122">Обычная проверка подлинности выполняется в контексте области.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="2bcb8-123">Сервер включает имя области в заголовке WWW-Authenticate.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="2bcb8-124">Учетные данные пользователя действительны в этой области.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="2bcb8-125">Точный диапазон области определяется сервером.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="2bcb8-126">Например, можно определить несколько областей для секционирования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="2bcb8-127">Так как учетные данные отправляются незашифрованными, обычная проверка подлинности обеспечивается только по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="2bcb8-128">См. раздел [Работа с SSL в веб-API](working-with-ssl-in-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="2bcb8-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="2bcb8-129">Обычная проверка подлинности также уязвима для атак CSRF.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="2bcb8-130">После того как пользователь введет учетные данные, браузер автоматически отправляет их при последующих запросах к тому же домену в течение сеанса.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="2bcb8-131">Сюда входят запросы AJAX.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-131">This includes AJAX requests.</span></span> <span data-ttu-id="2bcb8-132">См. раздел [предотвращение атак с подделкой межсайтовых запросов (CSRF)](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="2bcb8-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="2bcb8-133">Обычная проверка подлинности в IIS</span><span class="sxs-lookup"><span data-stu-id="2bcb8-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="2bcb8-134">Службы IIS поддерживают обычную проверку подлинности, но есть ряд предостережений: проверка подлинности пользователя выполняется по учетным данным Windows.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="2bcb8-135">Это означает, что пользователь должен иметь учетную запись в домене сервера.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="2bcb8-136">Для общедоступного веб-сайта обычно требуется пройти проверку подлинности для поставщика членства ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="2bcb8-137">Чтобы включить обычную проверку подлинности с помощью служб IIS, задайте для режима проверки подлинности значение "Windows" в файле Web. config проекта ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="2bcb8-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="2bcb8-138">В этом режиме службы IIS используют учетные данные Windows для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="2bcb8-139">Кроме того, необходимо включить обычную проверку подлинности в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="2bcb8-140">В диспетчере IIS перейдите в представление "функции", выберите Проверка подлинности и включите обычную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="2bcb8-141">В проекте веб-API добавьте атрибут `[Authorize]` для всех действий контроллера, требующих проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="2bcb8-142">Клиент выполняет проверку подлинности самостоятельно, задавая заголовок авторизации в запросе.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="2bcb8-143">Клиенты браузера выполняют этот шаг автоматически.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="2bcb8-144">Клиентам, не имеющим браузер, необходимо задать заголовок.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="2bcb8-145">Обычная проверка подлинности с пользовательским членством</span><span class="sxs-lookup"><span data-stu-id="2bcb8-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="2bcb8-146">Как уже упоминалось, обычная проверка подлинности, встроенная в IIS, использует учетные данные Windows.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="2bcb8-147">Это означает, что необходимо создать учетные записи для пользователей на сервере размещения.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="2bcb8-148">Но для Интернет – учетные записи пользователей обычно хранятся во внешней базе данных.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="2bcb8-149">В следующем коде показано, как модуль HTTP выполняет обычную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="2bcb8-150">Вы можете легко подключить поставщик членства ASP.NET, заменив метод `CheckPassword`, который является фиктивным методом в этом примере.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="2bcb8-151">В веб-API 2 следует рассмотреть возможность написания [фильтра проверки подлинности](authentication-filters.md) или [OWIN по промежуточного слоя](../../../aspnet/overview/owin-and-katana/index.md), а не HTTP-модуля.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="2bcb8-152">Чтобы включить модуль HTTP, добавьте следующий фрагмент в файл Web. config в разделе **System. Web Server** :</span><span class="sxs-lookup"><span data-stu-id="2bcb8-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="2bcb8-153">Замените "Йоурассемблинаме" именем сборки (не включая расширение "DLL").</span><span class="sxs-lookup"><span data-stu-id="2bcb8-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="2bcb8-154">Следует отключить другие схемы проверки подлинности, например формы или Windows Auth.</span><span class="sxs-lookup"><span data-stu-id="2bcb8-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>
