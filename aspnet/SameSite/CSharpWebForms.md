---
title: Пример файла cookie SameSite для ASP.NET C# 4.7.2 WebForms
author: blowdart
description: Пример файла cookie SameSite для ASP.NET C# 4.7.2 WebForms
ms.author: riande
ms.date: 2/15/2019
uid: samesite/CSharpWebForms
ms.openlocfilehash: 50d4745eca5954275abaa59dab726e7cf7ea193f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458423"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a>Пример файла cookie SameSite для ASP.NET C# 4.7.2 WebForms

.NET Framework 4,7 имеет встроенную поддержку атрибута [SameSite](https://www.owasp.org/index.php/SameSite) , но она соответствует исходному стандарту.
Исправленное поведение изменило значение `SameSite.None`, чтобы выдать атрибут со значением `None`, а не создавать значение вообще. Если вы хотите не выпустить значение, можно установить свойство `SameSite` для файла cookie равным-1.

## <a name="sampleCode"></a>Написание атрибута SameSite

Ниже приведен пример того, как записать атрибут SameSite в файл cookie.

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookie
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for SameSite none.
// Note this will also require you to be running on HTTPS
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

Атрибут sameSite по умолчанию для файла cookie проверки подлинности форм задается в параметре `cookieSameSite` параметров проверки подлинности на формах в `web.config` 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

Атрибут sameSite по умолчанию для состояния сеанса также задается в параметре "Кукиесамесите" параметров сеанса в `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

В ноябре 2019 обновления .NET изменились параметры по умолчанию для проверки подлинности и сеанса форм, чтобы `lax`, так как это наиболее совместимый параметр. Однако при внедрении страниц в IFRAME может потребоваться отменить этот параметр, а затем добавить приведенный ниже код [перехвата](#interception) , чтобы настроить поведение `none` в зависимости от возможностей браузера.

### <a name="running-the-sample"></a>Запуск образца

Если запустить пример проекта, загрузите отладчик браузера на начальной странице и используйте его для просмотра коллекции файлов cookie для сайта.
Чтобы сделать это на границе и Chrome, нажмите кнопку `F12` затем выберите вкладку `Application` и щелкните URL-адрес сайта в параметре `Cookies` в разделе `Storage`.

![Список файлов cookie отладчика браузера](sample/img/BrowserDebugger.png)

На рисунке выше показано, что файл cookie, созданный при нажатии кнопки "создать файлы cookie", имеет значение `Lax`атрибута SameSite, соответствующее значению, заданному в [образце кода](#sampleCode).

## <a name="interception"></a>Перехват файлов cookie, которыми вы не управляете

В .NET 4.5.2 появился новое событие для перехвата записи заголовков `Response.AddOnSendingHeaders`. Это можно использовать для перехвата файлов cookie перед их возвратом на клиентский компьютер. В примере мы подсоединены к статическому методу, который проверяет, поддерживает ли браузер новые изменения sameSite, и если нет, изменяет файлы cookie, чтобы они не выдавали атрибут, если было задано новое значение `None`.

Пример обработки события и настройки атрибута `sameSite` файла cookie см. в разделе [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) : пример подключения события и [SameSiteCookieRewriter.CS](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) .

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

## <a name="more-information"></a>Дополнительные сведения

[Обновления Chrome](https://www.chromium.org/updates/same-site)

[Документация по ASP.NET](/aspnet/samesite/system-web-samesite)

[Исправления .NET SameSite](/aspnet/samesite/kbs-samesite)