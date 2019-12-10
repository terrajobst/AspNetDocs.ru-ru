---
title: Работа с файлами cookie SameSite и открытым веб-интерфейсом для .NET (OWIN)
author: rick-anderson
description: Работа с файлами cookie SameSite и открытым веб-интерфейсом для .NET (OWIN)
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: ac5ae24eeb9e8e1cc6296667a4bebef72c3eb62c
ms.sourcegitcommit: 7b1e1784213dd4c301635f9e181764f3e2f94162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2019
ms.locfileid: "74993074"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a>SameSite файлы cookie и открытый веб-интерфейс для .NET (OWIN)

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT)

`SameSite` — это черновик [IETF](https://ietf.org/about/) , предназначенный для обеспечения защиты от атак с подделкой межсайтовых запросов (CSRF). [Черновик SameSite 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):

* По умолчанию обрабатывает файлы cookie как `SameSite=Lax`.
* Указывает, что файлы cookie, явно подтверждающие `SameSite=None` для включения межсайтовой доставки, должны быть помечены как `Secure`.

`Lax` работает для большинства файлов cookie приложения. Некоторые формы проверки подлинности, такие как [OpenID Connect Connect](https://openid.net/connect/) (OIDC) и [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , по умолчанию перенаправления на основе POST. Перенаправления на основе POST активируют `SameSite` защиту обозревателя, поэтому `SameSite` для этих компонентов отключена. Большинство имен входа [OAuth](https://oauth.net/) не затрагивается из-за различий в последовательностях запросов. Все остальные компоненты **не** устанавливают `SameSite` по умолчанию и используют поведение клиентов по умолчанию (старый или новый).

Параметр `None` вызывает проблемы совместимости с клиентами, которые реализовали ранее [2016 черновой версии Standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (например, iOS 12). См. раздел [Поддержка более старых браузеров](#sob) в этом документе.

Каждый компонент OWIN, порождаемый файлами cookie, должен решить, подходит ли `SameSite`.

Сведения о версии ASP.NET 4. x этой статьи см. в разделе <xref:samesite/system-web-samesite>.

## <a name="api-usage-with-samesite"></a>Использование API с SameSite

`Microsoft.Owin` имеет собственную реализацию `SameSite`:

* Это не зависит от того, в каком `System.Web`.
* `SameSite` работает на всех версиях, предназначенных для пакетов `Microsoft.Owin`, .NET 4,5 и более поздних версий.
* Только компонент [системвебкукиеманажер](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) напрямую взаимодействует с классом `System.Web` `HttpCookie`.

`SystemWebCookieManager` зависит от интерфейсов API `System.Web` .NET 4.7.2, чтобы обеспечить поддержку `SameSite`, а также исправления для изменения поведения.

Причины, по которым следует использовать `SystemWebCookieManager`, описаны в [вопросах интеграции файлов cookie OWIN и System. Web Response](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues). `SystemWebCookieManager` рекомендуется использовать при запуске на `System.Web`.

Следующий код задает `SameSite` для `Lax`:

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

Следующие API используют `SameSite`:

* [Microsoft. Owin. Самеситемоде](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [CookieOptions. SameSite](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* [Класс CookieAuthenticationOptions](/previous-versions/aspnet/dn385599(v%3Dvs.113)) <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [CookieAuthenticationOptions. Кукиесамесите](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* [икукиеманажер](/previous-versions/aspnet/dn800238(v%3Dvs.113))
* [системвебкукиеманажер](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [системвебчункингкукиеманажер](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [CookieAuthenticationOptions. Кукиеманажер](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [OpenIdConnectAuthenticationOptions. Кукиеманажер](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a>Журнал и изменения

[Microsoft. Owin](https://www.nuget.org/packages/Microsoft.Owin/) никогда не поддерживал [стандартный черновой стандарт`SameSite` 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).

Поддержка [черновика SameSite 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) доступна только в `Microsoft.Owin` 4.1.0 и более поздних версиях. Исправления для предыдущих версий отсутствуют.

2019. черновик спецификации `SameSite`:

* **Не** имеет обратной совместимости с черновиком 2016. Дополнительные сведения см. в разделе [поддержка старых браузеров](#sob) в этом документе.
* Указывает, что файлы cookie обрабатываются как `SameSite=Lax` по умолчанию.
* Указывает файлы cookie, явно подтверждающие `SameSite=None` для включения межсайтовой доставки, должны быть помечены как `Secure`. `None` — это новая запись для отказаться.
* По умолчанию в [фев 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)планируется включить по [Chrome](https://chromestatus.com/feature/5088147346030592) . Браузеры начали переходить к этому стандарту в 2019.
* Поддерживается исправлениями, которые были выпущены, как описано в статьях базы знаний. Для получения дополнительной информации см. <xref:samesite/kbs-samesite>.

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>Поддержка старых браузеров

Стандарт 2016 `SameSite` предписание, что неизвестные значения должны обрабатываться как `SameSite=Strict` значения. Приложения, доступ к которым осуществляется из старых браузеров, поддерживающих 2016 `SameSite` Standard, могут прерываться при получении свойства `SameSite` со значением `None`. Веб-приложения должны реализовывать обнаружение браузера, если они будут поддерживать старые браузеры. ASP.NET не реализует обнаружение браузеров, так как значения агентов пользователя очень энергонезависимы и часто меняются. Точка расширения в [икукиеманажер](/previous-versions/aspnet/dn800238(v%3Dvs.113)) позволяет подключать определенные логики агента пользователя.
<!-- https://docs.microsoft.com/en-us/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

В `Startup.Configuration`добавьте код, аналогичный приведенному ниже:

[!code-csharp[](sample/Startup1.cs?name=snippet)]

Для приведенного выше кода требуется исправление .NET 4.7.2 или более поздней версии `SameSite`.

В следующем коде показан пример реализации `SameSiteCookieManager`.

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

В предыдущем примере `DisallowsSameSiteNone` вызывается в методе `CheckSameSite`. `DisallowsSameSiteNone` — это пользовательский метод, который определяет, поддерживает ли агент пользователя `SameSite` `None`:

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

В следующем коде показан пример метода `DisallowsSameSiteNone`:

> [!WARNING]
> Следующий код предназначен только для демонстрации:
> * Его не следует считать полным.
> * Он не поддерживается.

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>Тестирование приложений на наличие проблем SameSite

Приложения, взаимодействующие с удаленными сайтами, например с помощью имени входа от стороннего разработчика, должны:

* Протестируйте взаимодействие в нескольких браузерах.
* Примените [Обнаружение и устранение браузеров](#sob) , описанные в этом документе.

Протестируйте веб-приложения с помощью версии клиента, которая может явно использовать новое поведение `SameSite`. У Chrome, Firefox и Chromium ребра есть новые флаги функций выбора, которые можно использовать для тестирования. Когда приложение применяет исправления `SameSite`, протестируйте его с помощью более старых версий клиента, особенно Safari. Дополнительные сведения см. в разделе [поддержка старых браузеров](#sob) в этом документе.

### <a name="test-with-chrome"></a>Тестирование с помощью Chrome

Chrome 78 + дает неверные результаты, так как это временное устранение рисков. Временная защита "Chrome 78 +" позволяет создавать файлы cookie менее чем за две минуты. Chrome 76 или 77 с включенными соответствующими флагами тестирования предоставляют более точные результаты. Чтобы проверить новое поведение `SameSite`, переключите `chrome://flags/#same-site-by-default-cookies` в состояние **включено**. В более ранних версиях Chrome (75 и ниже) сообщается о сбое нового параметра `None`. См. раздел [Поддержка более старых браузеров](#sob) в этом документе.

Google не делает доступными более старые версии Chrome. Следуйте инструкциям в [скачивании Chromium](https://www.chromium.org/getting-involved/download-chromium) , чтобы протестировать старые версии Chrome. **Не** скачивать Chrome из ссылок, предоставленных при поиске старых версий Chrome.

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Тестирование с помощью Safari

Safari 12 строго реализовал ранее созданный черновик и завершается ошибкой, если новое значение `None` находится в файле cookie. `None` исключается с помощью кода обнаружения браузеров, [поддерживающего более старые браузеры](#sob) в этом документе. Протестируйте имена входа в стиле ОС Safari 12, Safari 13 и WebKit с помощью MSAL, ADAL или любой используемой библиотеки. Эта проблема зависит от базовой версии ОС. OSX Можаве (10,14) и iOS 12 имеют проблемы совместимости с новым поведением `SameSite`. Обновление операционной системы до OSX Catalina (10,15) или iOS 13 решает проблему. В настоящее время Safari не имеет флага согласия для проверки нового поведения спецификации.

### <a name="test-with-firefox"></a>Тестирование с помощью Firefox

Поддержку Firefox для нового стандарта можно протестировать в версии 68 +, проверив ее на `about:config` странице с флагом компонента `network.cookie.sameSite.laxByDefault`. В предыдущих версиях Firefox не было отчетов о проблемах совместимости.

### <a name="test-with-edge-browser"></a>Тестирование с помощью браузера пограничных устройств

Ребро поддерживает старый стандарт `SameSite`. Версия 44 не имеет известных проблем совместимости с новым стандартом.

### <a name="test-with-edge-chromium"></a>Тестирование с помощью ребра (Chromium)

Флаги `SameSite` задаются на странице `edge://flags/#same-site-by-default-cookies`. С пограничным Chromium проблем совместимости не обнаружено.

### <a name="test-with-electron"></a>Тестирование с электронными данными

Версии Electron включают в себя более старые версии Chromium. Например, используемая командами версия электронного характера — Chromium 66, которая приводит к более старому поведению. Необходимо выполнить собственное тестирование совместимости с версией электронного продукта, используемого вашим продуктом. См. раздел [Поддержка более старых браузеров](#sob) в следующем разделе.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Блог по Chromium: разработчики: готовы к созданию нового SameSite = None; Параметры защиты файлов cookie](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Описание файлов cookie SameSite](https://web.dev/samesite-cookies-explained/)
* [Проблемы интеграции файлов cookie OWIN и System. Web Response](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)
