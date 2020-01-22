---
title: Работа с файлами cookie SameSite в ASP.NET
author: rick-anderson
description: Узнайте, как использовать для SameSite файлов cookie в ASP.NET
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: d2160bd9aeb93398b49b3a0e5e7a8a4404a5bc63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519197"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>Работа с файлами cookie SameSite в ASP.NET

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

SameSite — это черновик [IETF](https://ietf.org/about/) , предназначенный для обеспечения защиты от атак с подделкой межсайтовых запросов (CSRF). [Черновик SameSite 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):

* По умолчанию обрабатывает файлы cookie как `SameSite=Lax`.
* Указывает, что файлы cookie, явно подтверждающие `SameSite=None` для включения межсайтовой доставки, должны быть помечены как `Secure`.

`Lax` работает для большинства файлов cookie приложения. Некоторые формы проверки подлинности, такие как [OpenID Connect Connect](https://openid.net/connect/) (OIDC) и [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , по умолчанию перенаправления на основе POST. Перенаправления на основе POST активируют защиту обозревателя SameSite, поэтому SameSite для этих компонентов отключен. Большинство имен входа [OAuth](https://oauth.net/) не затрагивается из-за различий в способах передачи запросов.

Параметр `None` вызывает проблемы совместимости с клиентами, которые реализовали ранее [2016 черновой версии Standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (например, iOS 12). См. раздел [Поддержка более старых браузеров](#sob) в этом документе.

Каждый компонент ASP.NET, порождаемый файлами cookie, должен решить, подходит ли SameSite.

## <a name="api-usage-with-samesite"></a>Использование API с SameSite

См [. раздел свойство HttpCookie. SameSite](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)

## <a name="history-and-changes"></a>Журнал и изменения

Поддержка SameSite была впервые реализована в .NET 4.7.2 с использованием [стандартного черновика 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).

19 ноября 2019 обновления для Windows обновили .NET 4.7.2 + с стандарта 2016 до стандарта 2019. Дополнительные обновления предназначены для других версий Windows. Для получения дополнительной информации см. <xref:samesite/kbs-samesite>.

 2019. черновик спецификации SameSite:

* **Не** имеет обратной совместимости с черновиком 2016. Дополнительные сведения см. в разделе [поддержка старых браузеров](#sob) в этом документе.
* Указывает, что файлы cookie обрабатываются как `SameSite=Lax` по умолчанию.
* Указывает файлы cookie, явно подтверждающие `SameSite=None` для включения межсайтовой доставки, должны быть помечены как `Secure`. `None` — это новая запись для отказаться.
* Поддерживается выдаваемыми исправлениями, описанными в КИЛОБАЙТах, перечисленных выше.
* По умолчанию в [фев 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)планируется включить по [Chrome](https://chromestatus.com/feature/5088147346030592) . Браузеры начали переходить к этому стандарту в 2019.

### <a name="azure-app-servicesamesite-cookie-handling"></a>Служба приложений Azure — обработка файлов cookie SameSite

Дополнительные сведения см. в статье [Обработка SameSite файлов cookie в службе приложений Azure и обновление .NET Framework 4.7.2](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>Поддержка старых браузеров

Стандарт 2016 SameSite требует, чтобы неизвестные значения считались `SameSite=Strict` значениями. Приложения, доступ к которым осуществляется из старых браузеров, поддерживающих стандарт 2016 SameSite, могут прерываться при получении свойства SameSite со значением `None`. Веб-приложения должны реализовывать обнаружение браузера, если они будут поддерживать старые браузеры. ASP.NET не реализует обнаружение браузеров, так как значения агентов пользователя очень энергонезависимы и часто меняются. Следующий код можно вызвать на веб-сайте <xref:HTTP.HttpCookie> Call:

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

В предыдущем примере `MyUserAgentDetectionLib.DisallowsSameSiteNone` является библиотекой, предоставляемой пользователем, которая определяет, не поддерживает ли агент пользователя SameSite `None`. В следующем коде показан пример метода `DisallowsSameSiteNone`:

> [!WARNING]
> Следующий код предназначен только для демонстрации:
> * Его не следует считать полным.
> * Он не поддерживается.

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>Тестирование приложений на наличие проблем SameSite

Приложения, взаимодействующие с удаленными сайтами, например с помощью имени входа от стороннего разработчика, должны:

* Протестируйте взаимодействие в нескольких браузерах.
* Примените [Обнаружение и устранение браузеров](#sob) , описанные в этом документе.

Протестируйте веб-приложения с помощью версии клиента, которая может явно использовать новое поведение SameSite. У Chrome, Firefox и Chromium ребра есть новые флаги функций выбора, которые можно использовать для тестирования. Когда приложение применяет исправления SameSite, протестируйте его с помощью более старых версий клиента, особенно Safari. Дополнительные сведения см. в разделе [поддержка старых браузеров](#sob) в этом документе.

### <a name="test-with-chrome"></a>Тестирование с помощью Chrome

Chrome 78 + дает неверные результаты, так как это временное устранение рисков. Временная защита "Chrome 78 +" позволяет создавать файлы cookie менее чем за две минуты. Chrome 76 или 77 с включенными соответствующими флагами тестирования предоставляют более точные результаты. Чтобы проверить новое поведение SameSite, переключите `chrome://flags/#same-site-by-default-cookies` в состояние **включено**. В более ранних версиях Chrome (75 и ниже) сообщается о сбое нового параметра `None`. См. раздел [Поддержка более старых браузеров](#sob) в этом документе.

Google не делает доступными более старые версии Chrome. Следуйте инструкциям в [скачивании Chromium](https://www.chromium.org/getting-involved/download-chromium) , чтобы протестировать старые версии Chrome. **Не** скачивать Chrome из ссылок, предоставленных при поиске старых версий Chrome.

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Тестирование с помощью Safari

Safari 12 строго реализовал ранее созданный черновик и завершается ошибкой, если новое значение `None` находится в файле cookie. `None` исключается с помощью кода обнаружения браузеров, [поддерживающего более старые браузеры](#sob) в этом документе. Протестируйте имена входа в стиле ОС Safari 12, Safari 13 и WebKit с помощью MSAL, ADAL или любой используемой библиотеки. Эта проблема зависит от базовой версии ОС. Известно, что в OSX Можаве (10,14) и iOS 12 возникают проблемы совместимости с новым поведением SameSite. Обновление операционной системы до OSX Catalina (10,15) или iOS 13 решает проблему. В настоящее время Safari не имеет флага согласия для проверки нового поведения спецификации.

### <a name="test-with-firefox"></a>Тестирование с помощью Firefox

Поддержку Firefox для нового стандарта можно протестировать в версии 68 +, проверив ее на `about:config` странице с флагом компонента `network.cookie.sameSite.laxByDefault`. В предыдущих версиях Firefox не было отчетов о проблемах совместимости.

### <a name="test-with-edge-browser"></a>Тестирование с помощью браузера пограничных устройств

Ребро поддерживает старый стандарт SameSite. Версия 44 не имеет известных проблем совместимости с новым стандартом.

### <a name="test-with-edge-chromium"></a>Тестирование с помощью ребра (Chromium)

Флаги SameSite задаются на странице `edge://flags/#same-site-by-default-cookies`. С пограничным Chromium проблем совместимости не обнаружено.

### <a name="test-with-electron"></a>Тестирование с электронными данными

Версии Electron включают в себя более старые версии Chromium. Например, используемая командами версия электронного характера — Chromium 66, которая приводит к более старому поведению. Необходимо выполнить собственное тестирование совместимости с версией электронного продукта, используемого вашим продуктом. См. раздел [Поддержка более старых браузеров](#sob) в следующем разделе.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Блог по Chromium: разработчики: готовы к созданию нового SameSite = None; Параметры защиты файлов cookie](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Описание файлов cookie SameSite](https://web.dev/samesite-cookies-explained/)
