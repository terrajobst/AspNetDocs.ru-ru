---
title: Пример файла cookie SameSite для ASP.NET C# 4.7.2 MVC
author: blowdart
description: Пример файла cookie SameSite для ASP.NET C# 4.7.2 MVC
ms.author: riande
ms.date: 2/15/2019
uid: samesite/csMVC
ms.openlocfilehash: dcbd0bee009669fb747d74e6ccef07fbae70a236
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438204"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-mvc"></a>Пример файла cookie SameSite для ASP.NET C# 4.7.2 MVC

.NET Framework 4,7 имеет встроенную поддержку атрибута [SameSite](https://www.owasp.org/index.php/SameSite) , но она соответствует исходному стандарту.
Исправленное поведение изменило значение `SameSite.None`, чтобы выдать атрибут со значением `None`, а не создавать значение вообще. Если вы хотите не выпустить значение, можно установить свойство `SameSite` для файла cookie равным-1.

## <a name="sampleCode"></a>Написание атрибута SameSite

Ниже приведен пример того, как записать атрибут SameSite в файл cookie.

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

Атрибут sameSite по умолчанию для состояния сеанса задается в параметре "Кукиесамесите" параметров сеанса в `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a>Проверка подлинности MVC

Проверка подлинности на основе файлов cookie OWIN MVC использует диспетчер файлов cookie для включения изменения атрибутов файлов cookie. [SameSiteCookieManager.CS](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs) является реализацией такого класса, который можно скопировать в собственные проекты. 

Необходимо убедиться, что все компоненты Microsoft. Owin обновлены до версии 4.1.0 или более поздней. Проверьте файл `packages.config`, чтобы убедиться, что все номера версий совпадают, например.

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

После этого компоненты проверки подлинности должны быть настроены для использования Кукиеманажер в классе Startup.

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

Диспетчер файлов cookie должен быть установлен для *каждого* компонента, который его поддерживает, включая Кукиеаусентикатион и опенидконнектаусентикатион.

Системвебкукиеманажер используется для предотвращения [известных проблем](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) с интеграцией файлов cookie ответа.

### <a name="running-the-sample"></a>Выполнение примера

Если запустить пример проекта, загрузите отладчик браузера на начальной странице и используйте его для просмотра коллекции файлов cookie для сайта.
Чтобы сделать это на границе и Chrome, нажмите кнопку `F12` затем выберите вкладку `Application` и щелкните URL-адрес сайта в параметре `Cookies` в разделе `Storage`.

![Список файлов cookie отладчика браузера](sample/img/BrowserDebugger.png)

На рисунке выше показано, что файл cookie, созданный при нажатии кнопки "создать файлы cookie", имеет значение `Lax`атрибута SameSite, соответствующее значению, заданному в [образце кода](#sampleCode).

## <a name="interception"></a>Перехват файлов cookie, которыми вы не управляете

В .NET 4.5.2 появился новое событие для перехвата записи заголовков `Response.AddOnSendingHeaders`. Это можно использовать для перехвата файлов cookie перед их возвратом на клиентский компьютер. В примере мы подсоединены к статическому методу, который проверяет, поддерживает ли браузер новые изменения sameSite, и если нет, изменяет файлы cookie, чтобы они не выдавали атрибут, если было задано новое значение `None`.

Пример обработки события и [SameSiteCookieRewriter.csного](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) атрибута, который можно скопировать в собственный код, см. в разделе [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) . Пример: подключение события и изменение файла cookie `sameSite`.

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

Можно изменить конкретное поведение именованного файла cookie во многом аналогичным образом. Приведенный ниже пример изменяет файл cookie проверки подлинности по умолчанию с `Lax` на `None` в браузерах, поддерживающих значение `None`, или удаляет атрибут sameSite в браузерах, которые не поддерживают `None`.

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

### <a name="more-information"></a>Дополнительные сведения
 
[Обновления Chrome](https://www.chromium.org/updates/same-site)

[Документация по OWIN SameSite](/aspnet/samesite/owin-samesite)

[Документация по ASP.NET](/aspnet/samesite/system-web-samesite)

[Исправления .NET SameSite](/aspnet/samesite/kbs-samesite)