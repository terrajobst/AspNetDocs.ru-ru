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
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="a4f78-103">Работа с файлами cookie SameSite в ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a4f78-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="a4f78-104">Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a4f78-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a4f78-105">SameSite — это стандартный черновик [IETF](https://ietf.org/about/) , предназначенный для обеспечения защиты от атак с подделкой межсайтовых запросов (CSRF).</span><span class="sxs-lookup"><span data-stu-id="a4f78-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="a4f78-106">Черновик, первоначально измененный в [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), был обновлен в [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span><span class="sxs-lookup"><span data-stu-id="a4f78-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="a4f78-107">Обновленный стандарт не обладает обратной совместимостью с предыдущим стандартом, и ниже приведены наиболее заметные отличия.</span><span class="sxs-lookup"><span data-stu-id="a4f78-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="a4f78-108">Файлы cookie без заголовка SameSite по умолчанию обрабатываются как `SameSite=Lax`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="a4f78-109">для использования межсайтового файла cookie необходимо использовать `SameSite=None`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="a4f78-110">Файлы cookie, которые `SameSite=None` Assert, также должны быть помечены как `Secure`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="a4f78-111">Приложения, использующие [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) , могут столкнуться с проблемами `sameSite=Lax` или `sameSite=Strict` файлов cookie, так как `<iframe>` рассматривается как межсайтовые сценарии.</span><span class="sxs-lookup"><span data-stu-id="a4f78-111">Applications that use [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) may experience issues with `sameSite=Lax` or `sameSite=Strict` cookies because `<iframe>` is treated as cross-site scenarios.</span></span>
* <span data-ttu-id="a4f78-112">Значение `SameSite=None` не разрешено [стандартом 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07) и заставляет некоторые реализации обрабатывать такие файлы cookie как `SameSite=Strict`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-112">The value `SameSite=None` is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as `SameSite=Strict`.</span></span> <span data-ttu-id="a4f78-113">См. раздел [Поддержка более старых браузеров](#sob) в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a4f78-113">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="a4f78-114">Параметр `SameSite=Lax` работает для большинства файлов cookie приложения.</span><span class="sxs-lookup"><span data-stu-id="a4f78-114">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="a4f78-115">Некоторые формы проверки подлинности, такие как [OpenID Connect Connect](https://openid.net/connect/) (OIDC) и [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , по умолчанию перенаправления на основе POST.</span><span class="sxs-lookup"><span data-stu-id="a4f78-115">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="a4f78-116">Перенаправления на основе POST активируют защиту обозревателя SameSite, поэтому SameSite для этих компонентов отключен.</span><span class="sxs-lookup"><span data-stu-id="a4f78-116">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="a4f78-117">Большинство имен входа [OAuth](https://oauth.net/) не затрагивается из-за различий в способах передачи запросов.</span><span class="sxs-lookup"><span data-stu-id="a4f78-117">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="a4f78-118">Каждый компонент ASP.NET, порождаемый файлами cookie, должен решить, подходит ли SameSite.</span><span class="sxs-lookup"><span data-stu-id="a4f78-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="a4f78-119">Сведения о проблемах с приложениями после установки обновлений 2019 .NET SameSite см. в статье [Известные проблемы](#known) .</span><span class="sxs-lookup"><span data-stu-id="a4f78-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="a4f78-120">Использование SameSite в ASP.NET 4.7.2 и 4,8</span><span class="sxs-lookup"><span data-stu-id="a4f78-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="a4f78-121">.NET 4.7.2 и 4,8 поддерживает [черновой стандарт 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) для SameSite с момента выпуска обновлений в декабре 2019.</span><span class="sxs-lookup"><span data-stu-id="a4f78-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="a4f78-122">Разработчики могут программно управлять значением заголовка SameSite с помощью [Свойства HttpCookie. SameSite](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span><span class="sxs-lookup"><span data-stu-id="a4f78-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="a4f78-123">Присвоение свойству `SameSite` значения `Strict`, `Lax`или `None` приводит к записанию этих значений в сети с помощью файла cookie.</span><span class="sxs-lookup"><span data-stu-id="a4f78-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="a4f78-124">Задание этого параметра равно `(SameSiteMode)(-1)` указывает, что в сеть с файлом cookie не должен включаться заголовок SameSite.</span><span class="sxs-lookup"><span data-stu-id="a4f78-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="a4f78-125">[Свойство HttpCookie. Secure](/dotnet/api/system.web.httpcookie.secure)или "requireSSL" в файлах конфигурации можно использовать, чтобы пометить куки-файл как `Secure` или нет.</span><span class="sxs-lookup"><span data-stu-id="a4f78-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="a4f78-126">Новые экземпляры `HttpCookie` по умолчанию будут `SameSite=(SameSiteMode)(-1)` и `Secure=false`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="a4f78-127">Эти значения по умолчанию можно переопределить в разделе конфигурации `system.web/httpCookies`, где строка `"Unspecified"` является понятным синтаксисом только конфигурации для `(SameSiteMode)(-1)`:</span><span class="sxs-lookup"><span data-stu-id="a4f78-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="a4f78-128">ASP.Net также выдает четыре отдельных файла cookie для этих функций: Анонимная проверка подлинности, проверка подлинности с помощью форм, состояние сеанса и управление ролями.</span><span class="sxs-lookup"><span data-stu-id="a4f78-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="a4f78-129">Экземпляры этих файлов cookie, полученные в среде выполнения, можно манипулировать с помощью свойств `SameSite` и `Secure`, как и для любого другого экземпляра HttpCookie.</span><span class="sxs-lookup"><span data-stu-id="a4f78-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="a4f78-130">Однако из-за одеяланого последовательного SameSite стандарта параметры конфигурации для этих четырех компонентов не согласуются.</span><span class="sxs-lookup"><span data-stu-id="a4f78-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="a4f78-131">Ниже приведены соответствующие разделы и атрибуты конфигурации со значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4f78-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="a4f78-132">Если для функции отсутствует `SameSite` или `Secure` связанный атрибут, функция будет возвращаться к значениям по умолчанию, настроенным в разделе `system.web/httpCookies`, описанном выше.</span><span class="sxs-lookup"><span data-stu-id="a4f78-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

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

<span data-ttu-id="a4f78-133">**Примечание**. "не указано" доступен только для `system.web/httpCookies@sameSite` в данный момент.</span><span class="sxs-lookup"><span data-stu-id="a4f78-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="a4f78-134">Мы надеемся добавить похожий синтаксис к ранее показанным атрибутам Кукиесамесите в будущих обновлениях.</span><span class="sxs-lookup"><span data-stu-id="a4f78-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="a4f78-135">Установка `(SameSiteMode)(-1)` в коде по-прежнему работает с экземплярами этих файлов cookie. \*</span><span class="sxs-lookup"><span data-stu-id="a4f78-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a><span data-ttu-id="a4f78-136">Изменение целевой платформы для приложений .NET</span><span class="sxs-lookup"><span data-stu-id="a4f78-136">Retarget .NET apps</span></span>

<span data-ttu-id="a4f78-137">Для .NET 4.7.2 или более поздней версии:</span><span class="sxs-lookup"><span data-stu-id="a4f78-137">To target .NET 4.7.2 or later:</span></span>

* <span data-ttu-id="a4f78-138">Убедитесь, что *файл Web. config* содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="a4f78-138">Ensure *web.config* contains the following:</span></span>  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  <span data-ttu-id="a4f78-139">Дополнительные сведения см. в [инструкции по миграции .NET](/dotnet/framework/migration-guide/) .</span><span class="sxs-lookup"><span data-stu-id="a4f78-139">The [.NET Migration Guide](/dotnet/framework/migration-guide/) has more details.</span></span>

* <span data-ttu-id="a4f78-140">Убедитесь, что пакеты NuGet в проекте нацелены на правильную версию платформы.</span><span class="sxs-lookup"><span data-stu-id="a4f78-140">Verify NuGet packages in the project are targeted at the correct framework version.</span></span> <span data-ttu-id="a4f78-141">Правильную версию платформы можно проверить, изучив файл *Packages. config* , например:</span><span class="sxs-lookup"><span data-stu-id="a4f78-141">You can verify the correct framework version by examining the *packages.config* file, for example:</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  <span data-ttu-id="a4f78-142">В предыдущем файле *Packages. config* — пакет `Microsoft.ApplicationInsights`:</span><span class="sxs-lookup"><span data-stu-id="a4f78-142">In the preceding *packages.config* file, the `Microsoft.ApplicationInsights` package:</span></span>
    * <span data-ttu-id="a4f78-143">Предназначен для .NET 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="a4f78-143">Is  targeted against .NET 4.5.1.</span></span>
    * <span data-ttu-id="a4f78-144">Атрибут `targetFramework` должен быть обновлен для `net472`, если существует обновленный пакет, предназначенный для целевого объекта платформы.</span><span class="sxs-lookup"><span data-stu-id="a4f78-144">Should have its `targetFramework` attribute updated to `net472` if an updated package targeting your framework target exists.</span></span>

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a><span data-ttu-id="a4f78-145">Версии .NET более ранние, чем 4.7.2</span><span class="sxs-lookup"><span data-stu-id="a4f78-145">.NET versions earlier than 4.7.2</span></span>

<span data-ttu-id="a4f78-146">Корпорация Майкрософт не поддерживает версии .NET ниже, 4.7.2 для записи атрибута cookie того же сайта.</span><span class="sxs-lookup"><span data-stu-id="a4f78-146">Microsoft does not support .NET versions lower that 4.7.2 for writing the same-site cookie attribute.</span></span> <span data-ttu-id="a4f78-147">Мы не нашли надежный способ:</span><span class="sxs-lookup"><span data-stu-id="a4f78-147">We have not found a reliable way to:</span></span>

* <span data-ttu-id="a4f78-148">Убедитесь, что атрибут написан правильно, исходя из версии браузера.</span><span class="sxs-lookup"><span data-stu-id="a4f78-148">Ensure the attribute is written correctly based on browser version.</span></span>
* <span data-ttu-id="a4f78-149">Перехватите и настройте файлы cookie проверки подлинности и сеанса в более старых версиях платформы.</span><span class="sxs-lookup"><span data-stu-id="a4f78-149">Intercept and adjust authentication and session cookies on older framework versions.</span></span>

### <a name="december-patch-behavior-changes"></a><span data-ttu-id="a4f78-150">Изменения режима работы с декабрьским обновлением</span><span class="sxs-lookup"><span data-stu-id="a4f78-150">December patch behavior changes</span></span>

<span data-ttu-id="a4f78-151">Изменение поведения .NET Framework заключается в том, как свойство `SameSite` интерпретирует значение `None`:</span><span class="sxs-lookup"><span data-stu-id="a4f78-151">The specific behavior change for .NET Framework is how the `SameSite` property interprets the `None` value:</span></span>

* <span data-ttu-id="a4f78-152">Перед исправлением значение `None` означало:</span><span class="sxs-lookup"><span data-stu-id="a4f78-152">Before the patch a value of `None` meant:</span></span>
  * <span data-ttu-id="a4f78-153">Не выпустите атрибут вообще.</span><span class="sxs-lookup"><span data-stu-id="a4f78-153">Do not emit the attribute at all.</span></span>
* <span data-ttu-id="a4f78-154">После исправления:</span><span class="sxs-lookup"><span data-stu-id="a4f78-154">After the patch:</span></span>
  * <span data-ttu-id="a4f78-155">Значение `None`означает «выдать атрибуту значение `None`».</span><span class="sxs-lookup"><span data-stu-id="a4f78-155">A value of `None`it means "Emit the attribute with a value of `None`".</span></span>
  * <span data-ttu-id="a4f78-156">`SameSite` значение `(SameSiteMode)(-1)` приводит к тому, что атрибут не будет выдаваться.</span><span class="sxs-lookup"><span data-stu-id="a4f78-156">A `SameSite` value of `(SameSiteMode)(-1)` causes the attribute not to be emitted.</span></span>

<span data-ttu-id="a4f78-157">Значение SameSite по умолчанию для проверки подлинности форм и файлов cookie состояния сеанса изменилось с `None` на `Lax`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-157">The default SameSite value for forms authentication and session state cookies was changed from `None` to `Lax`.</span></span>

### <a name="summary-of-change-impact-on-browsers"></a><span data-ttu-id="a4f78-158">Сводка влияния изменений на браузеры</span><span class="sxs-lookup"><span data-stu-id="a4f78-158">Summary of change impact on browsers</span></span>

<span data-ttu-id="a4f78-159">Если установить исправление и отправить файл cookie с `SameSite.None`, произойдет одно из двух действий:</span><span class="sxs-lookup"><span data-stu-id="a4f78-159">If you install the patch and issue a cookie with `SameSite.None`, one of two things will happen:</span></span>
* <span data-ttu-id="a4f78-160">Chrome V80 будет рассматривать этот файл cookie в соответствии с новой реализацией и не применяет ограничения для этого файла cookie.</span><span class="sxs-lookup"><span data-stu-id="a4f78-160">Chrome v80 will treat this cookie according to the new implementation, and not enforce same site restrictions on the cookie.</span></span>
* <span data-ttu-id="a4f78-161">Все браузеры, которые не были обновлены для поддержки новой реализации, будут следовать за старой реализацией.</span><span class="sxs-lookup"><span data-stu-id="a4f78-161">Any browser that has not been updated to support the new implementation will follow the old implementation.</span></span> <span data-ttu-id="a4f78-162">Старая реализация говорит:</span><span class="sxs-lookup"><span data-stu-id="a4f78-162">The old implementation says:</span></span>
  * <span data-ttu-id="a4f78-163">Если вы видите значение, которое вы не понимаете, проигнорируйте его и переключитесь на ограничения одного сайта.</span><span class="sxs-lookup"><span data-stu-id="a4f78-163">If you see a value you don't understand, ignore it and switch to strict same site restrictions.</span></span>

<span data-ttu-id="a4f78-164">Это значит, что приложение прерывается в Chrome или вы разбиваете на несколько других мест.</span><span class="sxs-lookup"><span data-stu-id="a4f78-164">So either the app breaks in Chrome, or you break in numerous other places.</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="a4f78-165">Журнал и изменения</span><span class="sxs-lookup"><span data-stu-id="a4f78-165">History and changes</span></span>

<span data-ttu-id="a4f78-166">Поддержка SameSite была впервые реализована в .NET 4.7.2 с использованием [стандартного черновика 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span><span class="sxs-lookup"><span data-stu-id="a4f78-166">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="a4f78-167">19 ноября 2019 обновления для Windows обновили .NET 4.7.2 + с стандарта 2016 до стандарта 2019.</span><span class="sxs-lookup"><span data-stu-id="a4f78-167">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="a4f78-168">Дополнительные обновления предназначены для других версий Windows.</span><span class="sxs-lookup"><span data-stu-id="a4f78-168">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="a4f78-169">Дополнительные сведения см. в разделе <xref:samesite/kbs-samesite>.</span><span class="sxs-lookup"><span data-stu-id="a4f78-169">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="a4f78-170">2019. черновик спецификации SameSite:</span><span class="sxs-lookup"><span data-stu-id="a4f78-170">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="a4f78-171">**Не** имеет обратной совместимости с черновиком 2016.</span><span class="sxs-lookup"><span data-stu-id="a4f78-171">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="a4f78-172">Дополнительные сведения см. в разделе [поддержка старых браузеров](#sob) в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a4f78-172">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="a4f78-173">Указывает, что файлы cookie обрабатываются как `SameSite=Lax` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4f78-173">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="a4f78-174">Указывает файлы cookie, явно подтверждающие `SameSite=None` для включения межсайтовой доставки, также должны быть помечены как `Secure`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-174">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="a4f78-175">Поддерживается выдаваемыми исправлениями, описанными в КИЛОБАЙТах, перечисленных выше.</span><span class="sxs-lookup"><span data-stu-id="a4f78-175">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="a4f78-176">По умолчанию в [фев 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)планируется включить по [Chrome](https://chromestatus.com/feature/5088147346030592) .</span><span class="sxs-lookup"><span data-stu-id="a4f78-176">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="a4f78-177">Браузеры начали переходить к этому стандарту в 2019.</span><span class="sxs-lookup"><span data-stu-id="a4f78-177">Browsers started moving to this standard in 2019.</span></span>

<a name="known"><a/>

## <a name="known-issues"></a><span data-ttu-id="a4f78-178">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="a4f78-178">Known Issues</span></span>

<span data-ttu-id="a4f78-179">Так как спецификации "2016" и "2019" не совместимы, в обновлении для .NET Framework за ноябрь 2019 появились некоторые изменения, которые могут быть нарушены.</span><span class="sxs-lookup"><span data-stu-id="a4f78-179">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="a4f78-180">Файлы cookie для проверки состояния сеанса и форм теперь записываются в сеть как `Lax`, а не как неопределенные.</span><span class="sxs-lookup"><span data-stu-id="a4f78-180">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="a4f78-181">Хотя большинство приложений работают с файлами cookie `SameSite=Lax`, приложения, которые разписываются на сайтах или в приложениях, которые используют `iframe`, могут обнаружить, что их состояние сеанса или файлы cookie авторизации форм не используются должным образом.</span><span class="sxs-lookup"><span data-stu-id="a4f78-181">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="a4f78-182">Чтобы устранить эту проблему, измените значение `cookieSameSite` в соответствующем разделе конфигурации, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="a4f78-182">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="a4f78-183">Хттпкукиес, которые явно задают `SameSite=None` в коде или конфигурации, теперь имеют это значение, записанное с помощью файла cookie, в то время как он был ранее опущен.</span><span class="sxs-lookup"><span data-stu-id="a4f78-183">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="a4f78-184">Это может вызвать проблемы с более старыми браузерами, поддерживающими только черновой стандарт 2016.</span><span class="sxs-lookup"><span data-stu-id="a4f78-184">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="a4f78-185">При разработке для браузеров, поддерживающих черновой стандарт 2019 с `SameSite=None` файлами cookie, не забудьте также пометить их `Secure` или они могут не распознаться.</span><span class="sxs-lookup"><span data-stu-id="a4f78-185">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="a4f78-186">Чтобы вернуться к поведению 2016 без записи `SameSite=None`, используйте параметр приложения `aspnet:SupressSameSiteNone=true`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-186">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="a4f78-187">Обратите внимание, что это будет применено ко всем Хттпкукиес в приложении.</span><span class="sxs-lookup"><span data-stu-id="a4f78-187">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="a4f78-188">Служба приложений Azure — обработка файлов cookie SameSite</span><span class="sxs-lookup"><span data-stu-id="a4f78-188">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="a4f78-189">Сведения о том, как служба приложений Azure настраивает поведение SameSite в приложениях .NET 4.7.2, см. в статье [Обработка SameSite файлов Azure и обновление .NET Framework 4.7.2](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .</span><span class="sxs-lookup"><span data-stu-id="a4f78-189">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="a4f78-190">Поддержка старых браузеров</span><span class="sxs-lookup"><span data-stu-id="a4f78-190">Supporting older browsers</span></span>

<span data-ttu-id="a4f78-191">Стандарт 2016 SameSite требует, чтобы неизвестные значения считались `SameSite=Strict` значениями.</span><span class="sxs-lookup"><span data-stu-id="a4f78-191">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="a4f78-192">Приложения, доступ к которым осуществляется из старых браузеров, поддерживающих стандарт 2016 SameSite, могут прерываться при получении свойства SameSite со значением `None`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-192">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="a4f78-193">Веб-приложения должны реализовывать обнаружение браузера, если они будут поддерживать старые браузеры.</span><span class="sxs-lookup"><span data-stu-id="a4f78-193">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="a4f78-194">ASP.NET не реализует обнаружение браузеров, так как значения агентов пользователя очень энергонезависимы и часто меняются.</span><span class="sxs-lookup"><span data-stu-id="a4f78-194">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span>

<span data-ttu-id="a4f78-195">Подход корпорации Майкрософт к устранению проблемы заключается в том, чтобы помочь вам реализовать компоненты обнаружения браузеров, чтобы удалить атрибут `sameSite=None` из файлов cookie, если известно, что браузер не поддерживает его.</span><span class="sxs-lookup"><span data-stu-id="a4f78-195">Microsoft's approach to fixing the problem is to help you implement browser detection components to strip the `sameSite=None` attribute from cookies if a browser is known to not support it.</span></span> <span data-ttu-id="a4f78-196">Советом Google было выдавать двойные файлы cookie, один с новым атрибутом и один без атрибута.</span><span class="sxs-lookup"><span data-stu-id="a4f78-196">Google's advice was to issue double cookies, one with the new attribute, and one without the attribute at all.</span></span> <span data-ttu-id="a4f78-197">Однако мы будем рассматривать советы Google в ограниченном объеме.</span><span class="sxs-lookup"><span data-stu-id="a4f78-197">However we consider Google's advice limited.</span></span> <span data-ttu-id="a4f78-198">Некоторые браузеры, особенно мобильные браузеры, имеют очень малые ограничения на количество файлов cookie, которые может отправить сайт или имя домена.</span><span class="sxs-lookup"><span data-stu-id="a4f78-198">Some browsers, especially mobile browsers have very small limits on the number of cookies a site, or a domain name can send.</span></span> <span data-ttu-id="a4f78-199">Отправка нескольких файлов cookie, особенно больших файлов cookie, таких как файлы cookie проверки подлинности, максимально быстро достигают мобильного браузера, вызывая сбои в работе приложений, которые трудно диагностировать и исправить.</span><span class="sxs-lookup"><span data-stu-id="a4f78-199">Sending multiple cookies, especially large cookies like authentication cookies can reach the mobile browser limit very quickly, causing app failures that are hard to diagnose and fix.</span></span> <span data-ttu-id="a4f78-200">Кроме того, в качестве платформы существует большая экосистема кода и компонентов сторонних производителей, которые не могут быть обновлены для использования подхода двойного файла cookie.</span><span class="sxs-lookup"><span data-stu-id="a4f78-200">Furthermore as a framework there is a large ecosystem of third party code and components that may not be updated to use a double cookie approach.</span></span>

<span data-ttu-id="a4f78-201">Код обнаружения браузера, используемый в примерах проектов в [этом репозитории GitHub]() , содержится в двух файлах</span><span class="sxs-lookup"><span data-stu-id="a4f78-201">The browser detection code used in the sample projects in [this GitHub repository]() is contained in two files</span></span>

* [<span data-ttu-id="a4f78-202">C#SameSiteSupport.cs</span><span class="sxs-lookup"><span data-stu-id="a4f78-202">C# SameSiteSupport.cs</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [<span data-ttu-id="a4f78-203">VB Самеситесуппорт. vb</span><span class="sxs-lookup"><span data-stu-id="a4f78-203">VB SameSiteSupport.vb</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

<span data-ttu-id="a4f78-204">Эти обнаружения являются наиболее распространенными агентами браузера, которые поддерживают стандарт 2016 и, для которого атрибут необходимо полностью удалить.</span><span class="sxs-lookup"><span data-stu-id="a4f78-204">These detections are the most common browser agents we have seen that support the 2016 standard and for which the attribute needs to be completely removed.</span></span> <span data-ttu-id="a4f78-205">Это не является полной реализацией:</span><span class="sxs-lookup"><span data-stu-id="a4f78-205">It isn't meant as a complete implementation:</span></span>

* <span data-ttu-id="a4f78-206">Приложение может просматривать браузеры, которые не поддерживаются веб-сайтами тестирования.</span><span class="sxs-lookup"><span data-stu-id="a4f78-206">Your app may see browsers that our test sites do not.</span></span>
* <span data-ttu-id="a4f78-207">При необходимости вы должны быть готовы к добавлению обнаружений для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="a4f78-207">You should be prepared to add detections as necessary for your environment.</span></span>

<span data-ttu-id="a4f78-208">Связь обнаружения зависит от используемой версии .NET и веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="a4f78-208">How you wire up the detection varies according the version of .NET and the web framework that you are using.</span></span> <span data-ttu-id="a4f78-209">Следующий код можно вызвать на веб-сайте <xref:HTTP.HttpCookie> Call:</span><span class="sxs-lookup"><span data-stu-id="a4f78-209">The following code can be called at the <xref:HTTP.HttpCookie> call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="a4f78-210">См. следующие разделы ASP.NET 4.7.2 SameSite cookie:</span><span class="sxs-lookup"><span data-stu-id="a4f78-210">See the following ASP.NET 4.7.2 SameSite cookie topics:</span></span>

* [<span data-ttu-id="a4f78-211">C#КРУП</span><span class="sxs-lookup"><span data-stu-id="a4f78-211">C# MVC</span></span>](xref:samesite/csMVC)
* [<span data-ttu-id="a4f78-212">C#WebForms</span><span class="sxs-lookup"><span data-stu-id="a4f78-212">C# WebForms</span></span>](xref:samesite/CSharpWebForms)
* [<span data-ttu-id="a4f78-213">Формы VB</span><span class="sxs-lookup"><span data-stu-id="a4f78-213">VB WebForms</span></span>](xref:samesite/vbWF)
* [<span data-ttu-id="a4f78-214">VB MVC</span><span class="sxs-lookup"><span data-stu-id="a4f78-214">VB MVC</span></span>](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a><span data-ttu-id="a4f78-215">Обеспечение перенаправления сайта по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="a4f78-215">Ensuring your site redirects to HTTPS</span></span>

<span data-ttu-id="a4f78-216">Для ASP.NET 4. x, WebForms и MVC можно использовать функцию [переопределения URL-адресов IIS](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) , чтобы перенаправить все запросы по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4f78-216">For ASP.NET 4.x, WebForms and MVC, [IIS's URL Rewrite](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) feature can be used to redirect all requests to HTTPS.</span></span> <span data-ttu-id="a4f78-217">В следующем коде XML показан пример правила:</span><span class="sxs-lookup"><span data-stu-id="a4f78-217">The following XML shows a sample rule:</span></span>

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

<span data-ttu-id="a4f78-218">В локальных установках [перезаписи URL-адресов IIS](https://www.iis.net/downloads/microsoft/url-rewrite) является необязательным компонентом, который может потребоваться для установки.</span><span class="sxs-lookup"><span data-stu-id="a4f78-218">In on-premises installations of [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) is an optional feature that may need installing.</span></span>

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="a4f78-219">Тестирование приложений на наличие проблем SameSite</span><span class="sxs-lookup"><span data-stu-id="a4f78-219">Test apps for SameSite problems</span></span>

<span data-ttu-id="a4f78-220">Необходимо протестировать приложение с помощью поддерживаемых браузеров и выполнить сценарии, использующие файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="a4f78-220">You must test your app with the browsers you support and go through your scenarios that involve cookies.</span></span> <span data-ttu-id="a4f78-221">Сценарии файлов cookie обычно входят в</span><span class="sxs-lookup"><span data-stu-id="a4f78-221">Cookie scenarios typically involve</span></span>

* <span data-ttu-id="a4f78-222">Формы входа</span><span class="sxs-lookup"><span data-stu-id="a4f78-222">Login forms</span></span>
* <span data-ttu-id="a4f78-223">Внешние механизмы входа, такие как Facebook, Azure AD, OAuth и OIDC</span><span class="sxs-lookup"><span data-stu-id="a4f78-223">External login mechanisms such as Facebook, Azure AD, OAuth and OIDC</span></span>
* <span data-ttu-id="a4f78-224">Страницы, принимающие запросы с других сайтов</span><span class="sxs-lookup"><span data-stu-id="a4f78-224">Pages that accept requests from other sites</span></span>
* <span data-ttu-id="a4f78-225">Страницы в приложении, предназначенные для встраивания в Iframes</span><span class="sxs-lookup"><span data-stu-id="a4f78-225">Pages in your app designed to be embedded in iframes</span></span>

<span data-ttu-id="a4f78-226">Следует убедиться, что файлы cookie создаются, сохраняются и удаляются в приложении правильно.</span><span class="sxs-lookup"><span data-stu-id="a4f78-226">You should check that cookies are created, persisted and deleted correctly in your app.</span></span>

<span data-ttu-id="a4f78-227">Приложения, взаимодействующие с удаленными сайтами, например с помощью имени входа от стороннего разработчика, должны:</span><span class="sxs-lookup"><span data-stu-id="a4f78-227">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="a4f78-228">Протестируйте взаимодействие в нескольких браузерах.</span><span class="sxs-lookup"><span data-stu-id="a4f78-228">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="a4f78-229">Примените [Обнаружение и устранение браузеров](#sob) , описанные в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a4f78-229">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="a4f78-230">Протестируйте веб-приложения с помощью версии клиента, которая может явно использовать новое поведение SameSite.</span><span class="sxs-lookup"><span data-stu-id="a4f78-230">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="a4f78-231">У Chrome, Firefox и Chromium ребра есть новые флаги функций выбора, которые можно использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="a4f78-231">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="a4f78-232">Когда приложение применяет исправления SameSite, протестируйте его с помощью более старых версий клиента, особенно Safari.</span><span class="sxs-lookup"><span data-stu-id="a4f78-232">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="a4f78-233">Дополнительные сведения см. в разделе [поддержка старых браузеров](#sob) в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a4f78-233">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="a4f78-234">Тестирование с помощью Chrome</span><span class="sxs-lookup"><span data-stu-id="a4f78-234">Test with Chrome</span></span>

<span data-ttu-id="a4f78-235">Chrome 78 + дает неверные результаты, так как это временное устранение рисков.</span><span class="sxs-lookup"><span data-stu-id="a4f78-235">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="a4f78-236">Временная защита "Chrome 78 +" позволяет создавать файлы cookie менее чем за две минуты.</span><span class="sxs-lookup"><span data-stu-id="a4f78-236">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="a4f78-237">Chrome 76 или 77 с включенными соответствующими флагами тестирования предоставляют более точные результаты.</span><span class="sxs-lookup"><span data-stu-id="a4f78-237">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="a4f78-238">Чтобы проверить новое поведение SameSite, переключите `chrome://flags/#same-site-by-default-cookies` в состояние **включено**.</span><span class="sxs-lookup"><span data-stu-id="a4f78-238">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="a4f78-239">В более ранних версиях Chrome (75 и ниже) сообщается о сбое нового параметра `None`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-239">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="a4f78-240">См. раздел [Поддержка более старых браузеров](#sob) в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a4f78-240">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="a4f78-241">Google не делает доступными более старые версии Chrome.</span><span class="sxs-lookup"><span data-stu-id="a4f78-241">Google does not make older chrome versions available.</span></span> <span data-ttu-id="a4f78-242">Следуйте инструкциям в [скачивании Chromium](https://www.chromium.org/getting-involved/download-chromium) , чтобы протестировать старые версии Chrome.</span><span class="sxs-lookup"><span data-stu-id="a4f78-242">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="a4f78-243">**Не** скачивать Chrome из ссылок, предоставленных при поиске старых версий Chrome.</span><span class="sxs-lookup"><span data-stu-id="a4f78-243">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="a4f78-244">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="a4f78-244">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="a4f78-245">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="a4f78-245">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* <span data-ttu-id="a4f78-246">Если вы не используете 64-разрядную версию Windows, вы можете использовать [средство просмотра омахапрокси](https://omahaproxy.appspot.com/) для поиска ветви Chromium, соответствующей Chrome 74 (v 74.0.3729.108), с помощью [инструкций, предоставленных Chromium](https://www.chromium.org/getting-involved/download-chromium).</span><span class="sxs-lookup"><span data-stu-id="a4f78-246">If you're not using a 64bit version of Windows you can use the [OmahaProxy viewer](https://omahaproxy.appspot.com/) to look up which Chromium branch corresponds to Chrome 74 (v74.0.3729.108) using the [instructions provided by Chromium](https://www.chromium.org/getting-involved/download-chromium).</span></span>

#### <a name="test-with-chrome-80"></a><span data-ttu-id="a4f78-247">Тестирование с помощью Chrome 80 +</span><span class="sxs-lookup"><span data-stu-id="a4f78-247">Test with Chrome 80+</span></span>

<span data-ttu-id="a4f78-248">[Скачайте](https://www.google.com/chrome/) версию Chrome, которая поддерживает новый атрибут.</span><span class="sxs-lookup"><span data-stu-id="a4f78-248">[Download](https://www.google.com/chrome/) a version of Chrome that supports their new attribute.</span></span> <span data-ttu-id="a4f78-249">На момент написания статьи текущая версия — Chrome 80.</span><span class="sxs-lookup"><span data-stu-id="a4f78-249">At the time of writing, the current version is Chrome 80.</span></span> <span data-ttu-id="a4f78-250">Для Chrome 80 требуется флаг, `chrome://flags/#same-site-by-default-cookies` включенным для использования нового поведения.</span><span class="sxs-lookup"><span data-stu-id="a4f78-250">Chrome 80 needs the flag `chrome://flags/#same-site-by-default-cookies` enabled to use the new behavior.</span></span> <span data-ttu-id="a4f78-251">Также следует включить (`chrome://flags/#cookies-without-same-site-must-be-secure`), чтобы проверить предстоящее поведение для файлов cookie, для которых не включен атрибут sameSite.</span><span class="sxs-lookup"><span data-stu-id="a4f78-251">You should also enable (`chrome://flags/#cookies-without-same-site-must-be-secure`) to test the upcoming behavior for cookies which have no sameSite attribute enabled.</span></span> <span data-ttu-id="a4f78-252">Chrome 80 находится на целевом объекте, чтобы переключатель рассматривал файлы cookie без атрибута как `SameSite=Lax`, хотя и с временным периодом ожидания для определенных запросов.</span><span class="sxs-lookup"><span data-stu-id="a4f78-252">Chrome 80 is on target to make the switch to treat cookies without the attribute as `SameSite=Lax`, albeit with a timed grace period for certain requests.</span></span> <span data-ttu-id="a4f78-253">Чтобы отключить период отсрочки с временем действия Chrome 80, можно запустить с помощью следующего аргумента командной строки:</span><span class="sxs-lookup"><span data-stu-id="a4f78-253">To disable the timed grace period Chrome 80 can be launched with the following command line argument:</span></span>

`--enable-features=SameSiteDefaultChecksMethodRigorously`

<span data-ttu-id="a4f78-254">Chrome 80 содержит предупреждающие сообщения в консоли браузера об отсутствующих атрибутах sameSite.</span><span class="sxs-lookup"><span data-stu-id="a4f78-254">Chrome 80 has warning messages in the browser console about missing sameSite attributes.</span></span> <span data-ttu-id="a4f78-255">Используйте клавишу F12, чтобы открыть консоль браузера.</span><span class="sxs-lookup"><span data-stu-id="a4f78-255">Use F12 to open the browser console.</span></span>

### <a name="test-with-safari"></a><span data-ttu-id="a4f78-256">Тестирование с помощью Safari</span><span class="sxs-lookup"><span data-stu-id="a4f78-256">Test with Safari</span></span>

<span data-ttu-id="a4f78-257">Safari 12 строго реализовал ранее созданный черновик и завершается ошибкой, если новое значение `None` находится в файле cookie.</span><span class="sxs-lookup"><span data-stu-id="a4f78-257">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="a4f78-258">`None` исключается с помощью кода обнаружения браузеров, [поддерживающего более старые браузеры](#sob) в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a4f78-258">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="a4f78-259">Протестируйте имена входа в стиле ОС Safari 12, Safari 13 и WebKit с помощью MSAL, ADAL или любой используемой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="a4f78-259">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="a4f78-260">Эта проблема зависит от базовой версии ОС.</span><span class="sxs-lookup"><span data-stu-id="a4f78-260">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="a4f78-261">Известно, что в OSX Можаве (10,14) и iOS 12 возникают проблемы совместимости с новым поведением SameSite.</span><span class="sxs-lookup"><span data-stu-id="a4f78-261">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="a4f78-262">Обновление операционной системы до OSX Catalina (10,15) или iOS 13 решает проблему.</span><span class="sxs-lookup"><span data-stu-id="a4f78-262">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="a4f78-263">В настоящее время Safari не имеет флага согласия для проверки нового поведения спецификации.</span><span class="sxs-lookup"><span data-stu-id="a4f78-263">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="a4f78-264">Тестирование с помощью Firefox</span><span class="sxs-lookup"><span data-stu-id="a4f78-264">Test with Firefox</span></span>

<span data-ttu-id="a4f78-265">Поддержку Firefox для нового стандарта можно протестировать в версии 68 +, проверив ее на `about:config` странице с флагом компонента `network.cookie.sameSite.laxByDefault`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-265">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="a4f78-266">В предыдущих версиях Firefox не было отчетов о проблемах совместимости.</span><span class="sxs-lookup"><span data-stu-id="a4f78-266">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-legacy-browser"></a><span data-ttu-id="a4f78-267">Тестирование с помощью браузера "границы" (прежних версий)</span><span class="sxs-lookup"><span data-stu-id="a4f78-267">Test with Edge (Legacy) browser</span></span>

<span data-ttu-id="a4f78-268">Ребро поддерживает старый стандарт SameSite.</span><span class="sxs-lookup"><span data-stu-id="a4f78-268">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="a4f78-269">Версия "44" не имеет известных проблем совместимости с новым стандартом.</span><span class="sxs-lookup"><span data-stu-id="a4f78-269">Edge version 44+ doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="a4f78-270">Тестирование с помощью ребра (Chromium)</span><span class="sxs-lookup"><span data-stu-id="a4f78-270">Test with Edge (Chromium)</span></span>

<span data-ttu-id="a4f78-271">Флаги SameSite задаются на странице `edge://flags/#same-site-by-default-cookies`.</span><span class="sxs-lookup"><span data-stu-id="a4f78-271">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="a4f78-272">С пограничным Chromium проблем совместимости не обнаружено.</span><span class="sxs-lookup"><span data-stu-id="a4f78-272">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="a4f78-273">Тестирование с электронными данными</span><span class="sxs-lookup"><span data-stu-id="a4f78-273">Test with Electron</span></span>

<span data-ttu-id="a4f78-274">Версии Electron включают в себя более старые версии Chromium.</span><span class="sxs-lookup"><span data-stu-id="a4f78-274">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="a4f78-275">Например, используемая командами версия электронного характера — Chromium 66, которая приводит к более старому поведению.</span><span class="sxs-lookup"><span data-stu-id="a4f78-275">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="a4f78-276">Необходимо выполнить собственное тестирование совместимости с версией электронного продукта, используемого вашим продуктом.</span><span class="sxs-lookup"><span data-stu-id="a4f78-276">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="a4f78-277">См. раздел [поддержка старых браузеров](#sob).</span><span class="sxs-lookup"><span data-stu-id="a4f78-277">See [Supporting older browsers](#sob).</span></span>

## <a name="reverting-samesite-patches"></a><span data-ttu-id="a4f78-278">Возврат исправлений SameSite</span><span class="sxs-lookup"><span data-stu-id="a4f78-278">Reverting SameSite patches</span></span>

<span data-ttu-id="a4f78-279">Вы можете отменить обновленное поведение sameSite в .NET Frameworkных приложениях до предыдущего поведения, где атрибут sameSite не был создан для значения `None`, а затем вернуть файлы cookie проверки подлинности и сеанса, чтобы не выдать значение.</span><span class="sxs-lookup"><span data-stu-id="a4f78-279">You can revert the updated sameSite behavior in .NET Framework apps to its previous behavior where the sameSite attribute is not emitted for a value of `None`, and revert the authentication and session cookies to not emit the value.</span></span> <span data-ttu-id="a4f78-280">Это необходимо сделать *очень временным исправлением*, так как изменения Chrome приводят к нарушению внешних запросов POST или проверке подлинности для пользователей, использующих браузеры, которые поддерживают изменения стандарта.</span><span class="sxs-lookup"><span data-stu-id="a4f78-280">This should be viewed as an *extremely temporary fix*, as the Chrome changes will break any external POST requests or authentication for users using browsers which support the changes to the standard.</span></span>

### <a name="reverting-net-472-behavior"></a><span data-ttu-id="a4f78-281">Отмена поведения .NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="a4f78-281">Reverting .NET 4.7.2 behavior</span></span>

<span data-ttu-id="a4f78-282">Обновите *файл Web. config* , чтобы включить в него следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="a4f78-282">Update *web.config* to include the following configuration settings:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="a4f78-283">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a4f78-283">Additional resources</span></span>

* [<span data-ttu-id="a4f78-284">Предстоящие изменения cookie SameSite в ASP.NET и ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a4f78-284">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="a4f78-285">Блог по Chromium: разработчики: готовы к созданию нового SameSite = None; Параметры защиты файлов cookie</span><span class="sxs-lookup"><span data-stu-id="a4f78-285">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="a4f78-286">Описание файлов cookie SameSite</span><span class="sxs-lookup"><span data-stu-id="a4f78-286">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="a4f78-287">Обновления Chrome</span><span class="sxs-lookup"><span data-stu-id="a4f78-287">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)
* [<span data-ttu-id="a4f78-288">Исправления .NET SameSite</span><span class="sxs-lookup"><span data-stu-id="a4f78-288">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
* [<span data-ttu-id="a4f78-289">Сведения о веб-приложениях Azure на одном сайте</span><span class="sxs-lookup"><span data-stu-id="a4f78-289">Azure Web Applications Same Site Information</span></span>](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [<span data-ttu-id="a4f78-290">Сведения об одном сайте Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4f78-290">Azure ActiveDirectory Same Site Information</span></span>](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
