---
title: Пример файла cookie SameSite для ASP.NET C# 4.7.2 MVC
author: blowdart
description: Пример файла cookie SameSite для ASP.NET C# 4.7.2 MVC
ms.author: riande
ms.date: 2/15/2019
uid: samesite/csMVC
ms.openlocfilehash: dcbd0bee009669fb747d74e6ccef07fbae70a236
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458399"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-mvc"></a><span data-ttu-id="8ed85-103">Пример файла cookie SameSite для ASP.NET C# 4.7.2 MVC</span><span class="sxs-lookup"><span data-stu-id="8ed85-103">SameSite cookie sample for ASP.NET 4.7.2 C# MVC</span></span>

<span data-ttu-id="8ed85-104">.NET Framework 4,7 имеет встроенную поддержку атрибута [SameSite](https://www.owasp.org/index.php/SameSite) , но она соответствует исходному стандарту.</span><span class="sxs-lookup"><span data-stu-id="8ed85-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="8ed85-105">Исправленное поведение изменило значение `SameSite.None`, чтобы выдать атрибут со значением `None`, а не создавать значение вообще.</span><span class="sxs-lookup"><span data-stu-id="8ed85-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="8ed85-106">Если вы хотите не выпустить значение, можно установить свойство `SameSite` для файла cookie равным-1.</span><span class="sxs-lookup"><span data-stu-id="8ed85-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="8ed85-107">Написание атрибута SameSite</span><span class="sxs-lookup"><span data-stu-id="8ed85-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="8ed85-108">Ниже приведен пример того, как записать атрибут SameSite в файл cookie.</span><span class="sxs-lookup"><span data-stu-id="8ed85-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookieSite none.
// Note this will also require you to be running on HTTPS
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for Same
sameSiteCookie.Secure = true;

// Set the cookie to HTTP only which is good practice unless you really do need
// to access it client side in scripts.
sameSiteCookie.HttpOnly = true;

// Add the SameSite attribute, this will emit the attribute with a value of none.
// To not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None;

// Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie);
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="8ed85-109">Атрибут sameSite по умолчанию для состояния сеанса задается в параметре "Кукиесамесите" параметров сеанса в `web.config`</span><span class="sxs-lookup"><span data-stu-id="8ed85-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="8ed85-110">Проверка подлинности MVC</span><span class="sxs-lookup"><span data-stu-id="8ed85-110">MVC Authentication</span></span>

<span data-ttu-id="8ed85-111">Проверка подлинности на основе файлов cookie OWIN MVC использует диспетчер файлов cookie для включения изменения атрибутов файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="8ed85-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="8ed85-112">[SameSiteCookieManager.CS](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs) является реализацией такого класса, который можно скопировать в собственные проекты.</span><span class="sxs-lookup"><span data-stu-id="8ed85-112">The [SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="8ed85-113">Необходимо убедиться, что все компоненты Microsoft. Owin обновлены до версии 4.1.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="8ed85-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="8ed85-114">Проверьте файл `packages.config`, чтобы убедиться, что все номера версий совпадают, например.</span><span class="sxs-lookup"><span data-stu-id="8ed85-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <!-- other packages -->
  <package id="Microsoft.Owin.Host.SystemWeb" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security.Cookies" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net472" />
  <package id="Owin" version="1.0" targetFramework="net472" />
</packages>
```

<span data-ttu-id="8ed85-115">После этого компоненты проверки подлинности должны быть настроены для использования Кукиеманажер в классе Startup.</span><span class="sxs-lookup"><span data-stu-id="8ed85-115">The authentication components must then be configured to use the CookieManager in your startup class;</span></span>

```c#
public void Configuration(IAppBuilder app)
{
    app.UseCookieAuthentication(new CookieAuthenticationOptions
    {
        CookieSameSite = SameSiteMode.None,
        CookieHttpOnly = true,
        CookieSecure = CookieSecureOption.Always,
        CookieManager = new SameSiteCookieManager(new SystemWebCookieManager())
    });
}
```

<span data-ttu-id="8ed85-116">Диспетчер файлов cookie должен быть установлен для *каждого* компонента, который его поддерживает, включая Кукиеаусентикатион и опенидконнектаусентикатион.</span><span class="sxs-lookup"><span data-stu-id="8ed85-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="8ed85-117">Системвебкукиеманажер используется для предотвращения [известных проблем](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) с интеграцией файлов cookie ответа.</span><span class="sxs-lookup"><span data-stu-id="8ed85-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="8ed85-118">Запуск образца</span><span class="sxs-lookup"><span data-stu-id="8ed85-118">Running the sample</span></span>

<span data-ttu-id="8ed85-119">Если запустить пример проекта, загрузите отладчик браузера на начальной странице и используйте его для просмотра коллекции файлов cookie для сайта.</span><span class="sxs-lookup"><span data-stu-id="8ed85-119">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="8ed85-120">Чтобы сделать это на границе и Chrome, нажмите кнопку `F12` затем выберите вкладку `Application` и щелкните URL-адрес сайта в параметре `Cookies` в разделе `Storage`.</span><span class="sxs-lookup"><span data-stu-id="8ed85-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![Список файлов cookie отладчика браузера](sample/img/BrowserDebugger.png)

<span data-ttu-id="8ed85-122">На рисунке выше показано, что файл cookie, созданный при нажатии кнопки "создать файлы cookie", имеет значение `Lax`атрибута SameSite, соответствующее значению, заданному в [образце кода](#sampleCode).</span><span class="sxs-lookup"><span data-stu-id="8ed85-122">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="8ed85-123">Перехват файлов cookie, которыми вы не управляете</span><span class="sxs-lookup"><span data-stu-id="8ed85-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="8ed85-124">В .NET 4.5.2 появился новое событие для перехвата записи заголовков `Response.AddOnSendingHeaders`.</span><span class="sxs-lookup"><span data-stu-id="8ed85-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="8ed85-125">Это можно использовать для перехвата файлов cookie перед их возвратом на клиентский компьютер.</span><span class="sxs-lookup"><span data-stu-id="8ed85-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="8ed85-126">В примере мы подсоединены к статическому методу, который проверяет, поддерживает ли браузер новые изменения sameSite, и если нет, изменяет файлы cookie, чтобы они не выдавали атрибут, если было задано новое значение `None`.</span><span class="sxs-lookup"><span data-stu-id="8ed85-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="8ed85-127">Пример обработки события и [SameSiteCookieRewriter.csного](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) атрибута, который можно скопировать в собственный код, см. в разделе [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) . Пример: подключение события и изменение файла cookie `sameSite`.</span><span class="sxs-lookup"><span data-stu-id="8ed85-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```c#
public static void FilterSameSiteNoneForIncompatibleUserAgents(object sender)
{
    HttpApplication application = sender as HttpApplication;
    if (application != null)
    {
        var userAgent = application.Context.Request.UserAgent;
        if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
        {
            HttpContext.Current.Response.AddOnSendingHeaders(context =>
            {
                var cookies = context.Response.Cookies;
                for (var i = 0; i < cookies.Count; i++)
                {
                    var cookie = cookies[i];
                    if (cookie.SameSite == SameSiteMode.None)
                    {
                        cookie.SameSite = (SameSiteMode)(-1); // Unspecified
                    }
                }
            });
        }
    }
}
```

<span data-ttu-id="8ed85-128">Можно изменить конкретное поведение именованного файла cookie во многом аналогичным образом. Приведенный ниже пример изменяет файл cookie проверки подлинности по умолчанию с `Lax` на `None` в браузерах, поддерживающих значение `None`, или удаляет атрибут sameSite в браузерах, которые не поддерживают `None`.</span><span class="sxs-lookup"><span data-stu-id="8ed85-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```c#
public static void AdjustSpecificCookieSettings()
{
    HttpContext.Current.Response.AddOnSendingHeaders(context =>
    {
        var cookies = context.Response.Cookies;
        for (var i = 0; i < cookies.Count; i++)
        {
            var cookie = cookies[i]; 
            // Forms auth: ".ASPXAUTH"
            // Session: "ASP.NET_SessionId"
            if (string.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal))
            { 
                if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
                {
                    cookie.SameSite = -1;
                }
                else
                {
                    cookie.SameSite = SameSiteMode.None;
                }
                cookie.Secure = true;
            }
        }
    });
}
```

### <a name="more-information"></a><span data-ttu-id="8ed85-129">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="8ed85-129">More Information</span></span>
 
[<span data-ttu-id="8ed85-130">Обновления Chrome</span><span class="sxs-lookup"><span data-stu-id="8ed85-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="8ed85-131">Документация по OWIN SameSite</span><span class="sxs-lookup"><span data-stu-id="8ed85-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="8ed85-132">Документация по ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8ed85-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="8ed85-133">Исправления .NET SameSite</span><span class="sxs-lookup"><span data-stu-id="8ed85-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)