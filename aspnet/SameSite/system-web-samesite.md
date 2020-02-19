---
title: Работа с файлами cookie SameSite в ASP.NET
author: rick-anderson
description: Узнайте, как использовать для SameSite файлов cookie в ASP.NET
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: edb368910b24be2d042afe3c19ffa1fb23245443
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455713"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>Работа с файлами cookie SameSite в ASP.NET

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT)

SameSite — это стандартный черновик [IETF](https://ietf.org/about/) , предназначенный для обеспечения защиты от атак с подделкой межсайтовых запросов (CSRF). Черновик, первоначально измененный в [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), был обновлен в [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00). Обновленный стандарт не обладает обратной совместимостью с предыдущим стандартом, и ниже приведены наиболее заметные отличия.

* Файлы cookie без заголовка SameSite по умолчанию обрабатываются как `SameSite=Lax`.
* для использования межсайтового файла cookie необходимо использовать `SameSite=None`.
* Файлы cookie, которые `SameSite=None` Assert, также должны быть помечены как `Secure`.
* Приложения, использующие [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) , могут столкнуться с проблемами `sameSite=Lax` или `sameSite=Strict` файлов cookie, так как `<iframe>` рассматривается как межсайтовые сценарии.
* Значение `SameSite=None` не разрешено [стандартом 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07) и заставляет некоторые реализации обрабатывать такие файлы cookie как `SameSite=Strict`. См. раздел [Поддержка более старых браузеров](#sob) в этом документе.

Параметр `SameSite=Lax` работает для большинства файлов cookie приложения. Некоторые формы проверки подлинности, такие как [OpenID Connect Connect](https://openid.net/connect/) (OIDC) и [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , по умолчанию перенаправления на основе POST. Перенаправления на основе POST активируют защиту обозревателя SameSite, поэтому SameSite для этих компонентов отключен. Большинство имен входа [OAuth](https://oauth.net/) не затрагивается из-за различий в способах передачи запросов.

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
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**Примечание**. "не указано" доступен только для `system.web/httpCookies@sameSite` в данный момент. Мы надеемся добавить похожий синтаксис к ранее показанным атрибутам Кукиесамесите в будущих обновлениях. Установка `(SameSiteMode)(-1)` в коде по-прежнему работает с экземплярами этих файлов cookie. *

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a>Изменение целевой платформы для приложений .NET

Для .NET 4.7.2 или более поздней версии:

* Убедитесь, что *файл Web. config* содержит следующие сведения:  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  Дополнительные сведения см. в [инструкции по миграции .NET](/dotnet/framework/migration-guide/) .

* Убедитесь, что пакеты NuGet в проекте нацелены на правильную версию платформы. Правильную версию платформы можно проверить, изучив файл *Packages. config* , например:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  В предыдущем файле *Packages. config* — пакет `Microsoft.ApplicationInsights`:
    * Предназначен для .NET 4.5.1.
    * Атрибут `targetFramework` должен быть обновлен для `net472`, если существует обновленный пакет, предназначенный для целевого объекта платформы.

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a>Версии .NET более ранние, чем 4.7.2

Корпорация Майкрософт не поддерживает версии .NET ниже, 4.7.2 для записи атрибута cookie того же сайта. Мы не нашли надежный способ:

* Убедитесь, что атрибут написан правильно, исходя из версии браузера.
* Перехватите и настройте файлы cookie проверки подлинности и сеанса в более старых версиях платформы.

### <a name="december-patch-behavior-changes"></a>Изменения режима работы с декабрьским обновлением

Изменение поведения .NET Framework заключается в том, как свойство `SameSite` интерпретирует значение `None`:

* Перед исправлением значение `None` означало:
  * Не выпустите атрибут вообще.
* После исправления:
  * Значение `None`означает «выдать атрибуту значение `None`».
  * `SameSite` значение `(SameSiteMode)(-1)` приводит к тому, что атрибут не будет выдаваться.

Значение SameSite по умолчанию для проверки подлинности форм и файлов cookie состояния сеанса изменилось с `None` на `Lax`.

### <a name="summary-of-change-impact-on-browsers"></a>Сводка влияния изменений на браузеры

Если установить исправление и отправить файл cookie с `SameSite.None`, произойдет одно из двух действий:
* Chrome V80 будет рассматривать этот файл cookie в соответствии с новой реализацией и не применяет ограничения для этого файла cookie.
* Все браузеры, которые не были обновлены для поддержки новой реализации, будут следовать за старой реализацией. Старая реализация говорит:
  * Если вы видите значение, которое вы не понимаете, проигнорируйте его и переключитесь на ограничения одного сайта.

Это значит, что приложение прерывается в Chrome или вы разбиваете на несколько других мест.

## <a name="history-and-changes"></a>Журнал и изменения

Поддержка SameSite была впервые реализована в .NET 4.7.2 с использованием [стандартного черновика 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).

19 ноября 2019 обновления для Windows обновили .NET 4.7.2 + с стандарта 2016 до стандарта 2019. Дополнительные обновления предназначены для других версий Windows. Дополнительные сведения см. в разделе <xref:samesite/kbs-samesite>.

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

Стандарт 2016 SameSite требует, чтобы неизвестные значения считались `SameSite=Strict` значениями. Приложения, доступ к которым осуществляется из старых браузеров, поддерживающих стандарт 2016 SameSite, могут прерываться при получении свойства SameSite со значением `None`. Веб-приложения должны реализовывать обнаружение браузера, если они будут поддерживать старые браузеры. ASP.NET не реализует обнаружение браузеров, так как значения агентов пользователя очень энергонезависимы и часто меняются.

Подход корпорации Майкрософт к устранению проблемы заключается в том, чтобы помочь вам реализовать компоненты обнаружения браузеров, чтобы удалить атрибут `sameSite=None` из файлов cookie, если известно, что браузер не поддерживает его. Советом Google было выдавать двойные файлы cookie, один с новым атрибутом и один без атрибута. Однако мы будем рассматривать советы Google в ограниченном объеме. Некоторые браузеры, особенно мобильные браузеры, имеют очень малые ограничения на количество файлов cookie, которые может отправить сайт или имя домена. Отправка нескольких файлов cookie, особенно больших файлов cookie, таких как файлы cookie проверки подлинности, максимально быстро достигают мобильного браузера, вызывая сбои в работе приложений, которые трудно диагностировать и исправить. Кроме того, в качестве платформы существует большая экосистема кода и компонентов сторонних производителей, которые не могут быть обновлены для использования подхода двойного файла cookie.

Код обнаружения браузера, используемый в примерах проектов в [этом репозитории GitHub]() , содержится в двух файлах

* [C#SameSiteSupport.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [VB Самеситесуппорт. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

Эти обнаружения являются наиболее распространенными агентами браузера, которые поддерживают стандарт 2016 и, для которого атрибут необходимо полностью удалить. Это не является полной реализацией:

* Приложение может просматривать браузеры, которые не поддерживаются веб-сайтами тестирования.
* При необходимости вы должны быть готовы к добавлению обнаружений для вашей среды.

Связь обнаружения зависит от используемой версии .NET и веб-платформы. Следующий код можно вызвать на веб-сайте <xref:HTTP.HttpCookie> Call:

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

См. следующие разделы ASP.NET 4.7.2 SameSite cookie:

* [C#КРУП](xref:samesite/csMVC)
* [C#WebForms](xref:samesite/CSharpWebForms)
* [Формы VB](xref:samesite/vbWF)
* [VB MVC](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a>Обеспечение перенаправления сайта по протоколу HTTPS

Для ASP.NET 4. x, WebForms и MVC можно использовать функцию [переопределения URL-адресов IIS](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) , чтобы перенаправить все запросы по протоколу HTTPS. В следующем коде XML показан пример правила:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

В локальных установках [перезаписи URL-адресов IIS](https://www.iis.net/downloads/microsoft/url-rewrite) является необязательным компонентом, который может потребоваться для установки.

## <a name="test-apps-for-samesite-problems"></a>Тестирование приложений на наличие проблем SameSite

Необходимо протестировать приложение с помощью поддерживаемых браузеров и выполнить сценарии, использующие файлы cookie. Сценарии файлов cookie обычно входят в

* Формы входа
* Внешние механизмы входа, такие как Facebook, Azure AD, OAuth и OIDC
* Страницы, принимающие запросы с других сайтов
* Страницы в приложении, предназначенные для встраивания в Iframes

Следует убедиться, что файлы cookie создаются, сохраняются и удаляются в приложении правильно.

Приложения, взаимодействующие с удаленными сайтами, например с помощью имени входа от стороннего разработчика, должны:

* Протестируйте взаимодействие в нескольких браузерах.
* Примените [Обнаружение и устранение браузеров](#sob) , описанные в этом документе.

Протестируйте веб-приложения с помощью версии клиента, которая может явно использовать новое поведение SameSite. У Chrome, Firefox и Chromium ребра есть новые флаги функций выбора, которые можно использовать для тестирования. Когда приложение применяет исправления SameSite, протестируйте его с помощью более старых версий клиента, особенно Safari. Дополнительные сведения см. в разделе [поддержка старых браузеров](#sob) в этом документе.

### <a name="test-with-chrome"></a>Тестирование с помощью Chrome

Chrome 78 + дает неверные результаты, так как это временное устранение рисков. Временная защита "Chrome 78 +" позволяет создавать файлы cookie менее чем за две минуты. Chrome 76 или 77 с включенными соответствующими флагами тестирования предоставляют более точные результаты. Чтобы проверить новое поведение SameSite, переключите `chrome://flags/#same-site-by-default-cookies` в состояние **включено**. В более ранних версиях Chrome (75 и ниже) сообщается о сбое нового параметра `None`. См. раздел [Поддержка более старых браузеров](#sob) в этом документе.

Google не делает доступными более старые версии Chrome. Следуйте инструкциям в [скачивании Chromium](https://www.chromium.org/getting-involved/download-chromium) , чтобы протестировать старые версии Chrome. **Не** скачивать Chrome из ссылок, предоставленных при поиске старых версий Chrome.

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* Если вы не используете 64-разрядную версию Windows, вы можете использовать [средство просмотра омахапрокси](https://omahaproxy.appspot.com/) для поиска ветви Chromium, соответствующей Chrome 74 (v 74.0.3729.108), с помощью [инструкций, предоставленных Chromium](https://www.chromium.org/getting-involved/download-chromium).

#### <a name="test-with-chrome-80"></a>Тестирование с помощью Chrome 80 +

[Скачайте](https://www.google.com/chrome/) версию Chrome, которая поддерживает новый атрибут. На момент написания статьи текущая версия — Chrome 80. Для Chrome 80 требуется флаг, `chrome://flags/#same-site-by-default-cookies` включенным для использования нового поведения. Также следует включить (`chrome://flags/#cookies-without-same-site-must-be-secure`), чтобы проверить предстоящее поведение для файлов cookie, для которых не включен атрибут sameSite. Chrome 80 находится на целевом объекте, чтобы переключатель рассматривал файлы cookie без атрибута как `SameSite=Lax`, хотя и с временным периодом ожидания для определенных запросов. Чтобы отключить период отсрочки с временем действия Chrome 80, можно запустить с помощью следующего аргумента командной строки:

`--enable-features=SameSiteDefaultChecksMethodRigorously`

Chrome 80 содержит предупреждающие сообщения в консоли браузера об отсутствующих атрибутах sameSite. Используйте клавишу F12, чтобы открыть консоль браузера.

### <a name="test-with-safari"></a>Тестирование с помощью Safari

Safari 12 строго реализовал ранее созданный черновик и завершается ошибкой, если новое значение `None` находится в файле cookie. `None` исключается с помощью кода обнаружения браузеров, [поддерживающего более старые браузеры](#sob) в этом документе. Протестируйте имена входа в стиле ОС Safari 12, Safari 13 и WebKit с помощью MSAL, ADAL или любой используемой библиотеки. Эта проблема зависит от базовой версии ОС. Известно, что в OSX Можаве (10,14) и iOS 12 возникают проблемы совместимости с новым поведением SameSite. Обновление операционной системы до OSX Catalina (10,15) или iOS 13 решает проблему. В настоящее время Safari не имеет флага согласия для проверки нового поведения спецификации.

### <a name="test-with-firefox"></a>Тестирование с помощью Firefox

Поддержку Firefox для нового стандарта можно протестировать в версии 68 +, проверив ее на `about:config` странице с флагом компонента `network.cookie.sameSite.laxByDefault`. В предыдущих версиях Firefox не было отчетов о проблемах совместимости.

### <a name="test-with-edge-legacy-browser"></a>Тестирование с помощью браузера "границы" (прежних версий)

Ребро поддерживает старый стандарт SameSite. Версия "44" не имеет известных проблем совместимости с новым стандартом.

### <a name="test-with-edge-chromium"></a>Тестирование с помощью ребра (Chromium)

Флаги SameSite задаются на странице `edge://flags/#same-site-by-default-cookies`. С пограничным Chromium проблем совместимости не обнаружено.

### <a name="test-with-electron"></a>Тестирование с электронными данными

Версии Electron включают в себя более старые версии Chromium. Например, используемая командами версия электронного характера — Chromium 66, которая приводит к более старому поведению. Необходимо выполнить собственное тестирование совместимости с версией электронного продукта, используемого вашим продуктом. См. раздел [поддержка старых браузеров](#sob).

## <a name="reverting-samesite-patches"></a>Возврат исправлений SameSite

Вы можете отменить обновленное поведение sameSite в .NET Frameworkных приложениях до предыдущего поведения, где атрибут sameSite не был создан для значения `None`, а затем вернуть файлы cookie проверки подлинности и сеанса, чтобы не выдать значение. Это необходимо сделать *очень временным исправлением*, так как изменения Chrome приводят к нарушению внешних запросов POST или проверке подлинности для пользователей, использующих браузеры, которые поддерживают изменения стандарта.

### <a name="reverting-net-472-behavior"></a>Отмена поведения .NET 4.7.2

Обновите *файл Web. config* , чтобы включить в него следующие параметры конфигурации:

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Предстоящие изменения cookie SameSite в ASP.NET и ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Блог по Chromium: разработчики: готовы к созданию нового SameSite = None; Параметры защиты файлов cookie](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Описание файлов cookie SameSite](https://web.dev/samesite-cookies-explained/)
* [Обновления Chrome](https://www.chromium.org/updates/same-site)
* [Исправления .NET SameSite](/aspnet/samesite/kbs-samesite)
* [Сведения о веб-приложениях Azure на одном сайте](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [Сведения об одном сайте Azure Active Directory](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
