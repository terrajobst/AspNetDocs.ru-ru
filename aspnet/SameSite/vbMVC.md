---
title: Пример SameSite cookie для ASP.NET 4.7.2 VB MVC
author: blowdart
description: Пример SameSite cookie для ASP.NET 4.7.2 VB MVC
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440850"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a><span data-ttu-id="967e4-103">Пример SameSite cookie для ASP.NET 4.7.2 VB MVC</span><span class="sxs-lookup"><span data-stu-id="967e4-103">SameSite cookie sample for ASP.NET 4.7.2 VB MVC</span></span>

<span data-ttu-id="967e4-104">.NET Framework 4,7 имеет встроенную поддержку атрибута [SameSite](https://www.owasp.org/index.php/SameSite) , но она соответствует исходному стандарту.</span><span class="sxs-lookup"><span data-stu-id="967e4-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="967e4-105">Исправленное поведение изменило значение `SameSite.None`, чтобы выдать атрибут со значением `None`, а не создавать значение вообще.</span><span class="sxs-lookup"><span data-stu-id="967e4-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="967e4-106">Если вы хотите не выпустить значение, можно установить свойство `SameSite` для файла cookie равным-1.</span><span class="sxs-lookup"><span data-stu-id="967e4-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="967e4-107">Написание атрибута SameSite</span><span class="sxs-lookup"><span data-stu-id="967e4-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="967e4-108">Ниже приведен пример того, как записать атрибут SameSite в файл cookie.</span><span class="sxs-lookup"><span data-stu-id="967e4-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```vb
' Create the cookie
Dim sameSiteCookie As New HttpCookie("sameSiteSample")

' Set a value for the cookie
sameSiteCookie.Value = "sample"

' Set the secure flag, which Chrome's changes will require for SameSite none.
' Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = True

' Set the cookie to HTTP only which is good practice unless you really do need
' to access it client side in scripts.
sameSiteCookie.HttpOnly = True

' Expire the cookie in 1 minute
sameSiteCookie.Expires = Date.Now.AddMinutes(1)

' Add the SameSite attribute, this will emit the attribute with a value of none.
' To Not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None

' Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie)
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="967e4-109">Атрибут sameSite по умолчанию для состояния сеанса задается в параметре "Кукиесамесите" параметров сеанса в `web.config`</span><span class="sxs-lookup"><span data-stu-id="967e4-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="967e4-110">Проверка подлинности MVC</span><span class="sxs-lookup"><span data-stu-id="967e4-110">MVC Authentication</span></span>

<span data-ttu-id="967e4-111">Проверка подлинности на основе файлов cookie OWIN MVC использует диспетчер файлов cookie для включения изменения атрибутов файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="967e4-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="967e4-112">[Самеситекукиеманажер. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) — это реализация такого класса, которую можно скопировать в собственные проекты.</span><span class="sxs-lookup"><span data-stu-id="967e4-112">The [SameSiteCookieManager.vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="967e4-113">Необходимо убедиться, что все компоненты Microsoft. Owin обновлены до версии 4.1.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="967e4-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="967e4-114">Проверьте файл `packages.config`, чтобы убедиться, что все номера версий совпадают, например.</span><span class="sxs-lookup"><span data-stu-id="967e4-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

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

<span data-ttu-id="967e4-115">Компоненты проверки подлинности должны быть настроены для использования Кукиеманажер в классе Startup.</span><span class="sxs-lookup"><span data-stu-id="967e4-115">The authentication components must be configured to use the CookieManager in your startup class;</span></span>

```vb
Public Sub Configuration(app As IAppBuilder)
    app.UseCookieAuthentication(New CookieAuthenticationOptions() With {
        .CookieSameSite = SameSiteMode.None,
        .CookieHttpOnly = True,
        .CookieSecure = CookieSecureOption.Always,
        .CookieManager = New SameSiteCookieManager(New SystemWebCookieManager())
    })
End Sub
```

<span data-ttu-id="967e4-116">Диспетчер файлов cookie должен быть установлен для *каждого* компонента, который его поддерживает, включая Кукиеаусентикатион и опенидконнектаусентикатион.</span><span class="sxs-lookup"><span data-stu-id="967e4-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="967e4-117">Системвебкукиеманажер используется для предотвращения [известных проблем](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) с интеграцией файлов cookie ответа.</span><span class="sxs-lookup"><span data-stu-id="967e4-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="967e4-118">Выполнение примера</span><span class="sxs-lookup"><span data-stu-id="967e4-118">Running the sample</span></span>

<span data-ttu-id="967e4-119">Если запустить пример проекта, загрузите отладчик браузера на начальной странице и используйте его для просмотра коллекции файлов cookie для сайта.</span><span class="sxs-lookup"><span data-stu-id="967e4-119">If you run the sample project please load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="967e4-120">Чтобы сделать это на границе и Chrome, нажмите кнопку `F12` затем выберите вкладку `Application` и щелкните URL-адрес сайта в параметре `Cookies` в разделе `Storage`.</span><span class="sxs-lookup"><span data-stu-id="967e4-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![Список файлов cookie отладчика браузера](sample/img/BrowserDebugger.png)

<span data-ttu-id="967e4-122">На рисунке выше показано, что файл cookie, созданный при нажатии кнопки "создать SameSite cookie", имеет значение атрибута SameSite `Lax`, соответствующее значению, заданному в [образце кода](#sampleCode).</span><span class="sxs-lookup"><span data-stu-id="967e4-122">You can see from the image above that the cookie created by the sample when you click the "Create SameSite Cookie" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="967e4-123">Перехват файлов cookie, которыми вы не управляете</span><span class="sxs-lookup"><span data-stu-id="967e4-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="967e4-124">В .NET 4.5.2 появился новое событие для перехвата записи заголовков `Response.AddOnSendingHeaders`.</span><span class="sxs-lookup"><span data-stu-id="967e4-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="967e4-125">Это можно использовать для перехвата файлов cookie перед их возвратом на клиентский компьютер.</span><span class="sxs-lookup"><span data-stu-id="967e4-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="967e4-126">В примере мы подсоединены к статическому методу, который проверяет, поддерживает ли браузер новые изменения sameSite, и если нет, изменяет файлы cookie, чтобы они не выдавали атрибут, если было задано новое значение `None`.</span><span class="sxs-lookup"><span data-stu-id="967e4-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="967e4-127">Пример обработки [события и настройки](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) атрибута `sameSite` файла cookie, который можно скопировать в собственный код, см. в разделе [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) .</span><span class="sxs-lookup"><span data-stu-id="967e4-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) for an example of hooking up the event and [SameSiteCookieRewriter.vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```vb
Sub FilterSameSiteNoneForIncompatibleUserAgents(ByVal sender As Object)
    Dim application As HttpApplication = TryCast(sender, HttpApplication)

    If application IsNot Nothing Then
        Dim userAgent = application.Context.Request.UserAgent

        If SameSite.DisallowsSameSiteNone(userAgent) Then
            application.Response.AddOnSendingHeaders(
                Function(context)
                    Dim cookies = context.Response.Cookies

                    For i = 0 To cookies.Count - 1
                        Dim cookie = cookies(i)

                        If cookie.SameSite = SameSiteMode.None Then
                            cookie.SameSite = CType((-1), SameSiteMode)
                        End If
                    Next
                End Function)
        End If
    End If
End Sub
```

<span data-ttu-id="967e4-128">Можно изменить конкретное поведение именованного файла cookie во многом аналогичным образом. Приведенный ниже пример изменяет файл cookie проверки подлинности по умолчанию с `Lax` на `None` в браузерах, поддерживающих значение `None`, или удаляет атрибут sameSite в браузерах, которые не поддерживают `None`.</span><span class="sxs-lookup"><span data-stu-id="967e4-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```vb
Public Shared Sub AdjustSpecificCookieSettings()
    HttpContext.Current.Response.AddOnSendingHeaders(Function(context)
            Dim cookies = context.Response.Cookies

            For i = 0 To cookies.Count - 1
            Dim cookie = cookies(i)

            If String.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal) Then

                If SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent) Then
                    cookie.SameSite = -1
                Else
                    cookie.SameSite = SameSiteMode.None
                End If

                cookie.Secure = True
            End If
            Next
        End Function)
End Sub
```

## <a name="more-information"></a><span data-ttu-id="967e4-129">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="967e4-129">More Information</span></span>
 
[<span data-ttu-id="967e4-130">Обновления Chrome</span><span class="sxs-lookup"><span data-stu-id="967e4-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="967e4-131">Документация по OWIN SameSite</span><span class="sxs-lookup"><span data-stu-id="967e4-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="967e4-132">Документация по ASP.NET</span><span class="sxs-lookup"><span data-stu-id="967e4-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="967e4-133">Исправления .NET SameSite</span><span class="sxs-lookup"><span data-stu-id="967e4-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)