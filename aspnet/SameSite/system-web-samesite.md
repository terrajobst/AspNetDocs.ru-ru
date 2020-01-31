---
title: Работа с файлами cookie SameSite в ASP.NET
author: rick-anderson
description: Узнайте, как использовать для SameSite файлов cookie в ASP.NET
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: c81ca38648609aa5347d2a8cc11889fc85d81711
ms.sourcegitcommit: 4d439e01c82c7c95b19216fedaf5b1a11a1deb06
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2020
ms.locfileid: "76826618"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>Работа с файлами cookie SameSite в ASP.NET

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

SameSite — это стандартный черновик [IETF](https://ietf.org/about/) , предназначенный для обеспечения защиты от атак с подделкой межсайтовых запросов (CSRF). Черновик, первоначально измененный в [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), был обновлен в [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00). Обновленный стандарт не обладает обратной совместимостью с предыдущим стандартом, и ниже приведены наиболее заметные отличия.

* Файлы cookie без заголовка SameSite по умолчанию обрабатываются как `SameSite=Lax`.
* для использования межсайтового файла cookie необходимо использовать `SameSite=None`.
* Файлы cookie, которые `SameSite=None` Assert, также должны быть помечены как `Secure`.
* Значение SameSite = None не разрешено [стандартом 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07) и приводит к тому, что некоторые реализации обрабатывают такие файлы cookie как SameSite =. См. раздел [Поддержка более старых браузеров](#sob) в этом документе.

Параметр `SameSite=Lax` работает для большинства файлов cookie приложения. Некоторые формы проверки подлинности, такие как [OpenID Connect Connect](https://openid.net/connect/) (OIDC) и [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , по умолчанию перенаправления на основе POST. Перенаправления на основе POST активируют защиту обозревателя SameSite, поэтому SameSite для этих компонентов отключен. Большинство имен входа [OAuth](https://oauth.net/) не затрагивается из-за различий в способах передачи запросов.

Приложения, использующие `iframe`, могут столкнуться с проблемами с `SameSite=Lax` или `SameSite=Strict` файлами cookie, так как Iframes рассматривается как межсайтовые сценарии.

Каждый компонент ASP.NET, порождаемый файлами cookie, должен решить, подходит ли SameSite.

Сведения о проблемах с приложениями после установки обновлений 2019 .NET SameSite см. в статье [Известные проблемы](#known) .

## <a name="using-samesite-in-aspnet-472-and-48"></a>Использование SameSite в ASP.NET 4.7.2 и 4,8

.NET 4.7.2 и 4,8 поддерживает [черновой стандарт 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) для SameSite с момента выпуска обновлений в декабре 2019. Разработчики могут программно управлять значением заголовка SameSite с помощью [Свойства HttpCookie. SameSite](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite). Присвоение свойству `SameSite` значения `Strict`, `Lax`или `None` приводит к записанию этих значений в сети с помощью файла cookie. Задание этого параметра равно `(SameSiteMode)(-1)` указывает, что в сеть с файлом cookie не должен включаться заголовок SameSite. [Свойство HttpCookie. Secure](/dotnet/api/system.web.httpcookie.secure)или "requireSSL" в файлах конфигурации можно использовать, чтобы пометить куки-файл как `Secure` или нет.

Новые экземпляры `HttpCookie` по умолчанию будут `SameSite=(SameSiteMode)(-1)` и `Secure=false`. Эти значения по умолчанию можно переопределить в разделе конфигурации `system.web/httpCookies`, где строка `"Unspecified"` является понятным синтаксисом только конфигурации для `(SameSiteMode)(-1)`:

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

ASP.Net также выдает четыре отдельных файла cookie для этих функций: Анонимная проверка подлинности, проверка подлинности с помощью форм, состояние сеанса и управление ролями. Экземпляры этих файлов cookie, полученные в среде выполнения, можно манипулировать с помощью свойств `SameSite` и `Secure`, как и для любого другого экземпляра HttpCookie. Однако из-за одеяланого последовательного SameSite стандарта параметры конфигурации для этих четырех компонентов не согласуются. Ниже приведены соответствующие разделы и атрибуты конфигурации со значениями по умолчанию. Если для функции отсутствует `SameSite` или `Secure` связанный атрибут, функция будет возвращаться к значениям по умолчанию, настроенным в разделе `system.web/httpCookies`, описанном выше.

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequiresSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**Примечание**. "не указано" доступен только для `system.web/httpCookies@sameSite` в данный момент. Мы надеемся добавить похожий синтаксис к ранее показанным атрибутам Кукиесамесите в будущих обновлениях. Установка `(SameSiteMode)(-1)` в коде по-прежнему работает с экземплярами этих файлов cookie. *

## <a name="history-and-changes"></a>Журнал и изменения

Поддержка SameSite была впервые реализована в .NET 4.7.2 с использованием [стандартного черновика 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).

19 ноября 2019 обновления для Windows обновили .NET 4.7.2 + с стандарта 2016 до стандарта 2019. Дополнительные обновления предназначены для других версий Windows. Для получения дополнительной информации см. <xref:samesite/kbs-samesite>.

 2019. черновик спецификации SameSite:

* **Не** имеет обратной совместимости с черновиком 2016. Дополнительные сведения см. в разделе [поддержка старых браузеров](#sob) в этом документе.
* Указывает, что файлы cookie обрабатываются как `SameSite=Lax` по умолчанию.
* Указывает файлы cookie, явно подтверждающие `SameSite=None` для включения межсайтовой доставки, также должны быть помечены как `Secure`.
* Поддерживается выдаваемыми исправлениями, описанными в КИЛОБАЙТах, перечисленных выше.
* По умолчанию в [фев 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)планируется включить по [Chrome](https://chromestatus.com/feature/5088147346030592) . Браузеры начали переходить к этому стандарту в 2019.

<a name="known"><a/>

## <a name="known-issues"></a>Известные проблемы

Так как спецификации "2016" и "2019" не совместимы, в обновлении для .NET Framework за ноябрь 2019 появились некоторые изменения, которые могут быть нарушены.

* Файлы cookie для проверки состояния сеанса и форм теперь записываются в сеть как `Lax`, а не как неопределенные.
  * Хотя большинство приложений работают с файлами cookie `SameSite=Lax`, приложения, которые разписываются на сайтах или в приложениях, которые используют `iframe`, могут обнаружить, что их состояние сеанса или файлы cookie авторизации форм не используются должным образом. Чтобы устранить эту проблему, измените значение `cookieSameSite` в соответствующем разделе конфигурации, как описано выше.
* Хттпкукиес, которые явно задают `SameSite=None` в коде или конфигурации, теперь имеют это значение, записанное с помощью файла cookie, в то время как он был ранее опущен. Это может вызвать проблемы с более старыми браузерами, поддерживающими только черновой стандарт 2016.
  * При разработке для браузеров, поддерживающих черновой стандарт 2019 с `SameSite=None` файлами cookie, не забудьте также пометить их `Secure` или они могут не распознаться.
  * Чтобы вернуться к поведению 2016 без записи `SameSite=None`, используйте параметр приложения `aspnet:SupressSameSiteNone=true`. Обратите внимание, что это будет применено ко всем Хттпкукиес в приложении.

### <a name="azure-app-servicesamesite-cookie-handling"></a>Служба приложений Azure — обработка файлов cookie SameSite

Сведения о том, как служба приложений Azure настраивает поведение SameSite в приложениях .NET 4.7.2, см. в статье [Обработка SameSite файлов Azure и обновление .NET Framework 4.7.2](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .

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

* [Предстоящие изменения cookie SameSite в ASP.NET и ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Блог по Chromium: разработчики: готовы к созданию нового SameSite = None; Параметры защиты файлов cookie](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Описание файлов cookie SameSite](https://web.dev/samesite-cookies-explained/)
