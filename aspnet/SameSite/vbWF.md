---
title: Пример SameSite cookie для ASP.NET 4.7.2 VB
author: blowdart
description: Пример SameSite cookie для ASP.NET 4.7.2 VB
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbWF
ms.openlocfilehash: 8979edecc5acf7dac81b9f53d31af00389f4727c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458387"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-webforms"></a>Пример SameSite cookie для ASP.NET 4.7.2 VB
.NET Framework 4,7 имеет встроенную поддержку атрибута [SameSite](https://www.owasp.org/index.php/SameSite) , но она соответствует исходному стандарту.
Исправленное поведение изменило значение `SameSite.None`, чтобы выдать атрибут со значением `None`, а не создавать значение вообще. Если вы хотите не выпустить значение, можно установить свойство `SameSite` для файла cookie равным-1.

## <a name="sampleCode"></a>Написание атрибута SameSite

Ниже приведен пример того, как записать атрибут SameSite в файл cookie.

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

Пример обработки события и настройки атрибута `sameSite` файла cookie см. в разделе [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) : пример подключения события и [SameSiteCookieRewriter.CS](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) .


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

Можно изменить конкретное поведение именованного файла cookie во многом аналогичным образом. Приведенный ниже пример изменяет файл cookie проверки подлинности по умолчанию с `Lax` на `None` в браузерах, поддерживающих значение `None`, или удаляет атрибут sameSite в браузерах, которые не поддерживают `None`.

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

## <a name="more-information"></a>Дополнительные сведения

[Обновления Chrome](https://www.chromium.org/updates/same-site)

[Документация по ASP.NET](/aspnet/samesite/system-web-samesite)

[Исправления .NET SameSite](/aspnet/samesite/kbs-samesite)