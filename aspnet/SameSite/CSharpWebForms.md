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
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a><span data-ttu-id="14c63-103">Пример файла cookie SameSite для ASP.NET C# 4.7.2 WebForms</span><span class="sxs-lookup"><span data-stu-id="14c63-103">SameSite cookie sample for ASP.NET 4.7.2 C# WebForms</span></span>

<span data-ttu-id="14c63-104">.NET Framework 4,7 имеет встроенную поддержку атрибута [SameSite](https://www.owasp.org/index.php/SameSite) , но она соответствует исходному стандарту.</span><span class="sxs-lookup"><span data-stu-id="14c63-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="14c63-105">Исправленное поведение изменило значение `SameSite.None`, чтобы выдать атрибут со значением `None`, а не создавать значение вообще.</span><span class="sxs-lookup"><span data-stu-id="14c63-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="14c63-106">Если вы хотите не выпустить значение, можно установить свойство `SameSite` для файла cookie равным-1.</span><span class="sxs-lookup"><span data-stu-id="14c63-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="14c63-107">Написание атрибута SameSite</span><span class="sxs-lookup"><span data-stu-id="14c63-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="14c63-108">Ниже приведен пример того, как записать атрибут SameSite в файл cookie.</span><span class="sxs-lookup"><span data-stu-id="14c63-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

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

<span data-ttu-id="14c63-109">Атрибут sameSite по умолчанию для файла cookie проверки подлинности форм задается в параметре `cookieSameSite` параметров проверки подлинности на формах в `web.config`</span><span class="sxs-lookup"><span data-stu-id="14c63-109">The default sameSite attribute for a forms authentication cookie is set in the `cookieSameSite` parameter of the forms authentication settings in `web.config`</span></span> 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

<span data-ttu-id="14c63-110">Атрибут sameSite по умолчанию для состояния сеанса также задается в параметре "Кукиесамесите" параметров сеанса в `web.config`</span><span class="sxs-lookup"><span data-stu-id="14c63-110">The default sameSite attribute for session state is also set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

<span data-ttu-id="14c63-111">В ноябре 2019 обновления .NET изменились параметры по умолчанию для проверки подлинности и сеанса форм, чтобы `lax`, так как это наиболее совместимый параметр. Однако при внедрении страниц в IFRAME может потребоваться отменить этот параметр, а затем добавить приведенный ниже код [перехвата](#interception) , чтобы настроить поведение `none` в зависимости от возможностей браузера.</span><span class="sxs-lookup"><span data-stu-id="14c63-111">The November 2019 update to .NET changed the default settings for Forms Authentication and Session to `lax` as is the most compatible setting, however if you embed pages into iframes you may need to revert this setting to None, and then add the [interception](#interception) code shown below to adjust the `none` behavior depending on browser capability.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="14c63-112">Запуск образца</span><span class="sxs-lookup"><span data-stu-id="14c63-112">Running the sample</span></span>

<span data-ttu-id="14c63-113">Если запустить пример проекта, загрузите отладчик браузера на начальной странице и используйте его для просмотра коллекции файлов cookie для сайта.</span><span class="sxs-lookup"><span data-stu-id="14c63-113">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="14c63-114">Чтобы сделать это на границе и Chrome, нажмите кнопку `F12` затем выберите вкладку `Application` и щелкните URL-адрес сайта в параметре `Cookies` в разделе `Storage`.</span><span class="sxs-lookup"><span data-stu-id="14c63-114">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![Список файлов cookie отладчика браузера](sample/img/BrowserDebugger.png)

<span data-ttu-id="14c63-116">На рисунке выше показано, что файл cookie, созданный при нажатии кнопки "создать файлы cookie", имеет значение `Lax`атрибута SameSite, соответствующее значению, заданному в [образце кода](#sampleCode).</span><span class="sxs-lookup"><span data-stu-id="14c63-116">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="14c63-117">Перехват файлов cookie, которыми вы не управляете</span><span class="sxs-lookup"><span data-stu-id="14c63-117">Intercepting cookies you do not control</span></span>

<span data-ttu-id="14c63-118">В .NET 4.5.2 появился новое событие для перехвата записи заголовков `Response.AddOnSendingHeaders`.</span><span class="sxs-lookup"><span data-stu-id="14c63-118">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="14c63-119">Это можно использовать для перехвата файлов cookie перед их возвратом на клиентский компьютер.</span><span class="sxs-lookup"><span data-stu-id="14c63-119">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="14c63-120">В примере мы подсоединены к статическому методу, который проверяет, поддерживает ли браузер новые изменения sameSite, и если нет, изменяет файлы cookie, чтобы они не выдавали атрибут, если было задано новое значение `None`.</span><span class="sxs-lookup"><span data-stu-id="14c63-120">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="14c63-121">Пример обработки события и настройки атрибута `sameSite` файла cookie см. в разделе [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) : пример подключения события и [SameSiteCookieRewriter.CS](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) .</span><span class="sxs-lookup"><span data-stu-id="14c63-121">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) for an example of handling the event and adjusting the cookie `sameSite` attribute.</span></span>

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

<span data-ttu-id="14c63-122">Можно изменить конкретное поведение именованного файла cookie во многом аналогичным образом. Приведенный ниже пример изменяет файл cookie проверки подлинности по умолчанию с `Lax` на `None` в браузерах, поддерживающих значение `None`, или удаляет атрибут sameSite в браузерах, которые не поддерживают `None`.</span><span class="sxs-lookup"><span data-stu-id="14c63-122">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

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

## <a name="more-information"></a><span data-ttu-id="14c63-123">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="14c63-123">More Information</span></span>

[<span data-ttu-id="14c63-124">Обновления Chrome</span><span class="sxs-lookup"><span data-stu-id="14c63-124">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="14c63-125">Документация по ASP.NET</span><span class="sxs-lookup"><span data-stu-id="14c63-125">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="14c63-126">Исправления .NET SameSite</span><span class="sxs-lookup"><span data-stu-id="14c63-126">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)