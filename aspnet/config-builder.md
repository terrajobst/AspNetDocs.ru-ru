---
uid: config-builder
title: Построители конфигураций для ASP.NET
author: rick-anderson
description: Узнайте, как получить данные конфигурации из источников, отличных от значений Web. config из внешних источников.
ms.author: riande
ms.date: 10/29/2018
msc.type: content
ms.openlocfilehash: 5299d9ab057c3096773955a7461e77a80673ebfe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586762"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="168b1-103">Построители конфигураций для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="168b1-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="168b1-104">В [Стивен Моллой](https://github.com/StephenMolloy) и [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="168b1-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="168b1-105">Построители конфигураций предоставляют современный и гибкий механизм для ASP.NET приложений с целью получения значений конфигурации из внешних источников.</span><span class="sxs-lookup"><span data-stu-id="168b1-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="168b1-106">Построители конфигураций:</span><span class="sxs-lookup"><span data-stu-id="168b1-106">Configuration builders:</span></span>

* <span data-ttu-id="168b1-107">Доступны в .NET Framework 4.7.1 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="168b1-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="168b1-108">Предоставьте гибкий механизм чтения значений конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="168b1-109">Устраните некоторые из основных потребностей приложений по мере их перемещения в контейнер и в облачную среду.</span><span class="sxs-lookup"><span data-stu-id="168b1-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="168b1-110">Можно использовать для улучшения защиты данных конфигурации путем рисования из ранее недоступных источников (например, Azure Key Vault и переменных среды) в системе конфигурации .NET.</span><span class="sxs-lookup"><span data-stu-id="168b1-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="168b1-111">Построители конфигурации "ключ — значение"</span><span class="sxs-lookup"><span data-stu-id="168b1-111">Key/value configuration builders</span></span>

<span data-ttu-id="168b1-112">Распространенным сценарием, который может обработать построители конфигураций, является предоставление базового механизма замены ключа и значения для разделов конфигурации, которые следуют шаблону "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="168b1-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="168b1-113">.NET Framework концепция ConfigurationBuilders не ограничена конкретными разделами конфигурации или шаблонами.</span><span class="sxs-lookup"><span data-stu-id="168b1-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="168b1-114">Однако многие построители конфигураций в `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) работают в шаблоне "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="168b1-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="168b1-115">Параметры построителя конфигурации "ключ — значение"</span><span class="sxs-lookup"><span data-stu-id="168b1-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="168b1-116">Следующие параметры применяются ко всем сборщикам конфигурации "ключ — значение" в `Microsoft.Configuration.ConfigurationBuilders`.</span><span class="sxs-lookup"><span data-stu-id="168b1-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="168b1-117">Режим</span><span class="sxs-lookup"><span data-stu-id="168b1-117">Mode</span></span>

<span data-ttu-id="168b1-118">Построители конфигурации используют внешний источник сведений о ключе и значении для заполнения выбранных элементов "ключ-значение" системы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="168b1-119">В частности, разделы `<appSettings/>` и `<connectionStrings/>` получают особую обработку от построителей конфигураций.</span><span class="sxs-lookup"><span data-stu-id="168b1-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="168b1-120">Построители работают в трех режимах:</span><span class="sxs-lookup"><span data-stu-id="168b1-120">The builders work in three modes:</span></span>

* <span data-ttu-id="168b1-121">`Strict` — режим по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="168b1-121">`Strict` - The default mode.</span></span> <span data-ttu-id="168b1-122">В этом режиме построитель конфигурации работает только с хорошо известными разделами конфигурации, основанными на ключах и значениях.</span><span class="sxs-lookup"><span data-stu-id="168b1-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="168b1-123">`Strict` режим перечисляет каждый ключ в разделе.</span><span class="sxs-lookup"><span data-stu-id="168b1-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="168b1-124">Если в внешнем источнике найден соответствующий ключ:</span><span class="sxs-lookup"><span data-stu-id="168b1-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="168b1-125">Построители конфигурации заменяют значение в результирующем разделе конфигурации значением из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="168b1-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="168b1-126">`Greedy` — этот режим тесно связан с режимом `Strict`.</span><span class="sxs-lookup"><span data-stu-id="168b1-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="168b1-127">Вместо того чтобы ограничиваться ключами, которые уже существуют в исходной конфигурации:</span><span class="sxs-lookup"><span data-stu-id="168b1-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="168b1-128">Построители конфигурации добавляют все пары "ключ-значение" из внешнего источника в результирующий раздел конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="168b1-129">`Expand` — работает с необработанным XML до того, как он будет разобран в объект раздела конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="168b1-130">Его можно рассматривать как расширение токенов в строке.</span><span class="sxs-lookup"><span data-stu-id="168b1-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="168b1-131">Любая часть необработанной XML-строки, соответствующей шаблону `${token}`, является кандидатом для расширения маркера.</span><span class="sxs-lookup"><span data-stu-id="168b1-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="168b1-132">Если в внешнем источнике не найдено соответствующее значение, токен не изменяется.</span><span class="sxs-lookup"><span data-stu-id="168b1-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="168b1-133">Построители в этом режиме не ограничиваются разделами `<appSettings/>` и `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="168b1-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="168b1-134">Следующая разметка из *файла Web. config* включает [енвиронментконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) в режиме `Strict`:</span><span class="sxs-lookup"><span data-stu-id="168b1-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="168b1-135">Следующий код считывает `<appSettings/>` и `<connectionStrings/>`, показанные в предыдущем файле *Web. config* :</span><span class="sxs-lookup"><span data-stu-id="168b1-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="168b1-136">В приведенном выше коде значения свойств будут заданы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="168b1-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="168b1-137">Значения в файле *Web. config* , если ключи не заданы в переменных среды.</span><span class="sxs-lookup"><span data-stu-id="168b1-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="168b1-138">Значения переменной среды, если задано значение.</span><span class="sxs-lookup"><span data-stu-id="168b1-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="168b1-139">Например, `ServiceID` будет содержать:</span><span class="sxs-lookup"><span data-stu-id="168b1-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="168b1-140">Значение ServiceID из Web. config, если не задана переменная среды `ServiceID`.</span><span class="sxs-lookup"><span data-stu-id="168b1-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="168b1-141">Значение переменной среды `ServiceID`, если оно задано.</span><span class="sxs-lookup"><span data-stu-id="168b1-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="168b1-142">На следующем рисунке показаны ключи и значения `<appSettings/>` из предыдущего набора файлов *Web. config* в редакторе среды:</span><span class="sxs-lookup"><span data-stu-id="168b1-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![редактор среды](config-builder/static/env.png)

<span data-ttu-id="168b1-144">Примечание. для просмотра изменений в переменных среды может потребоваться выйти и перезапустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="168b1-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="168b1-145">Обработка префиксов</span><span class="sxs-lookup"><span data-stu-id="168b1-145">Prefix handling</span></span>

<span data-ttu-id="168b1-146">Префиксы ключей позволяют упростить параметры ключей, так как:</span><span class="sxs-lookup"><span data-stu-id="168b1-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="168b1-147">Конфигурация .NET Framework является сложной и вложенной.</span><span class="sxs-lookup"><span data-stu-id="168b1-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="168b1-148">Внешние источники "ключ — значение" обычно являются базовыми и плоскими по природе.</span><span class="sxs-lookup"><span data-stu-id="168b1-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="168b1-149">Например, переменные среды не являются вложенными.</span><span class="sxs-lookup"><span data-stu-id="168b1-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="168b1-150">Используйте любой из следующих подходов, чтобы внедрить `<appSettings/>` и `<connectionStrings/>` в конфигурацию с помощью переменных среды:</span><span class="sxs-lookup"><span data-stu-id="168b1-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="168b1-151">С `EnvironmentConfigBuilder` в режиме `Strict` по умолчанию и соответствующими именами ключей в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="168b1-152">Этот подход используется в приведенном выше коде и разметке.</span><span class="sxs-lookup"><span data-stu-id="168b1-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="168b1-153">При таком подходе нельзя **использовать одинаковые** именованные ключи как в `<appSettings/>`, так и в `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="168b1-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="168b1-154">Используйте два `EnvironmentConfigBuilder`s в режиме `Greedy` с разными префиксами и `stripPrefix`.</span><span class="sxs-lookup"><span data-stu-id="168b1-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="168b1-155">При таком подходе приложение может считывать `<appSettings/>` и `<connectionStrings/>` без необходимости обновлять файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="168b1-156">В следующем разделе [стриппрефикс](#stripprefix)показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="168b1-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="168b1-157">Используйте два `EnvironmentConfigBuilder`s в режиме `Greedy` с разными префиксами.</span><span class="sxs-lookup"><span data-stu-id="168b1-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="168b1-158">При таком подходе не допускается наличие повторяющихся имен ключей, так как имена ключей должны отличаться по префиксу.</span><span class="sxs-lookup"><span data-stu-id="168b1-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="168b1-159">Например:</span><span class="sxs-lookup"><span data-stu-id="168b1-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="168b1-160">В предыдущей разметке для заполнения конфигурации двух разных разделов можно использовать один и тот же источник «Плоский ключ/значение».</span><span class="sxs-lookup"><span data-stu-id="168b1-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="168b1-161">На следующем рисунке показаны `<appSettings/>` и `<connectionStrings/>` ключи и значения из предыдущего файла *Web. config* , заданного в редакторе среды:</span><span class="sxs-lookup"><span data-stu-id="168b1-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![редактор среды](config-builder/static/prefix.png)

<span data-ttu-id="168b1-163">Следующий код считывает `<appSettings/>` и `<connectionStrings/>` ключи/значения, содержащиеся в предыдущем файле *Web. config* :</span><span class="sxs-lookup"><span data-stu-id="168b1-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="168b1-164">В приведенном выше коде значения свойств будут заданы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="168b1-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="168b1-165">Значения в файле *Web. config* , если ключи не заданы в переменных среды.</span><span class="sxs-lookup"><span data-stu-id="168b1-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="168b1-166">Значения переменной среды, если задано значение.</span><span class="sxs-lookup"><span data-stu-id="168b1-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="168b1-167">Например, используя предыдущий файл *Web. config* , ключи/значения в предыдущем изображении редактора среды и предыдущий код, задаются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="168b1-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="168b1-168">Key</span><span class="sxs-lookup"><span data-stu-id="168b1-168">Key</span></span>              | <span data-ttu-id="168b1-169">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="168b1-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="168b1-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="168b1-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="168b1-171">AppSetting_ServiceID из переменных env</span><span class="sxs-lookup"><span data-stu-id="168b1-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="168b1-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="168b1-172">AppSetting_default</span></span>            | <span data-ttu-id="168b1-173">AppSetting_default значение из env</span><span class="sxs-lookup"><span data-stu-id="168b1-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="168b1-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="168b1-174">ConnStr_default</span></span>         | <span data-ttu-id="168b1-175">ConnStr_default Val из env</span><span class="sxs-lookup"><span data-stu-id="168b1-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="168b1-176">стриппрефикс</span><span class="sxs-lookup"><span data-stu-id="168b1-176">stripPrefix</span></span>

<span data-ttu-id="168b1-177">`stripPrefix`: логическое значение, по умолчанию — `false`.</span><span class="sxs-lookup"><span data-stu-id="168b1-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="168b1-178">Предыдущая разметка XML разделяет параметры приложения из строк соединения, но требует, чтобы все ключи в файле *Web. config* использовали указанный префикс.</span><span class="sxs-lookup"><span data-stu-id="168b1-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="168b1-179">Например, префикс `AppSetting` должен быть добавлен в `ServiceID`ный ключ ("AppSetting_ServiceID").</span><span class="sxs-lookup"><span data-stu-id="168b1-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="168b1-180">При использовании `stripPrefix`префикс не используется в файле *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="168b1-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="168b1-181">Префикс является обязательным в источнике построителя конфигураций (например, в среде). Мы ожидаем, что большинство разработчиков будут использовать `stripPrefix`.</span><span class="sxs-lookup"><span data-stu-id="168b1-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="168b1-182">Приложения обычно удаляются с префикса.</span><span class="sxs-lookup"><span data-stu-id="168b1-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="168b1-183">Следующий *файл Web. config* отделяет префикс:</span><span class="sxs-lookup"><span data-stu-id="168b1-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="168b1-184">В предыдущем файле *Web. config* `default` ключ находится как в `<appSettings/>`, так и в `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="168b1-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="168b1-185">На следующем рисунке показаны `<appSettings/>` и `<connectionStrings/>` ключи и значения из предыдущего файла *Web. config* , заданного в редакторе среды:</span><span class="sxs-lookup"><span data-stu-id="168b1-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![редактор среды](config-builder/static/prefix.png)

<span data-ttu-id="168b1-187">Следующий код считывает `<appSettings/>` и `<connectionStrings/>` ключи/значения, содержащиеся в предыдущем файле *Web. config* :</span><span class="sxs-lookup"><span data-stu-id="168b1-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="168b1-188">В приведенном выше коде значения свойств будут заданы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="168b1-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="168b1-189">Значения в файле *Web. config* , если ключи не заданы в переменных среды.</span><span class="sxs-lookup"><span data-stu-id="168b1-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="168b1-190">Значения переменной среды, если задано значение.</span><span class="sxs-lookup"><span data-stu-id="168b1-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="168b1-191">Например, используя предыдущий файл *Web. config* , ключи/значения в предыдущем изображении редактора среды и предыдущий код, задаются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="168b1-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="168b1-192">Key</span><span class="sxs-lookup"><span data-stu-id="168b1-192">Key</span></span>              | <span data-ttu-id="168b1-193">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="168b1-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="168b1-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="168b1-194">ServiceID</span></span>           | <span data-ttu-id="168b1-195">AppSetting_ServiceID из переменных env</span><span class="sxs-lookup"><span data-stu-id="168b1-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="168b1-196">default</span><span class="sxs-lookup"><span data-stu-id="168b1-196">default</span></span>            | <span data-ttu-id="168b1-197">AppSetting_default значение из env</span><span class="sxs-lookup"><span data-stu-id="168b1-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="168b1-198">default</span><span class="sxs-lookup"><span data-stu-id="168b1-198">default</span></span>         | <span data-ttu-id="168b1-199">ConnStr_default Val из env</span><span class="sxs-lookup"><span data-stu-id="168b1-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="168b1-200">токенпаттерн</span><span class="sxs-lookup"><span data-stu-id="168b1-200">tokenPattern</span></span>

<span data-ttu-id="168b1-201">`tokenPattern`: String, по умолчанию — `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="168b1-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="168b1-202">`Expand`ное поведение сборщиков ищет маркеры, которые выглядят как `${token}`, в необработанном XML-коде.</span><span class="sxs-lookup"><span data-stu-id="168b1-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="168b1-203">Поиск выполняется с помощью регулярного выражения по умолчанию `@"\$\{(\w+)\}"`.</span><span class="sxs-lookup"><span data-stu-id="168b1-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="168b1-204">Набор символов, соответствующих `\w`, более точно, чем XML, и позволяет использовать множество источников конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="168b1-205">Используйте `tokenPattern`, если в имени токена требуется больше символов, чем `@"\$\{(\w+)\}"`.</span><span class="sxs-lookup"><span data-stu-id="168b1-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="168b1-206">`tokenPattern`: строка:</span><span class="sxs-lookup"><span data-stu-id="168b1-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="168b1-207">Позволяет разработчикам изменять регулярное выражение, используемое для сопоставления маркеров.</span><span class="sxs-lookup"><span data-stu-id="168b1-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="168b1-208">Проверка не выполняется, чтобы убедиться, что это правильно сформированное, неопасное регулярное выражение.</span><span class="sxs-lookup"><span data-stu-id="168b1-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="168b1-209">Он должен содержать группу захвата.</span><span class="sxs-lookup"><span data-stu-id="168b1-209">It must contain a capture group.</span></span> <span data-ttu-id="168b1-210">Целое регулярное выражение должно соответствовать всему токену.</span><span class="sxs-lookup"><span data-stu-id="168b1-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="168b1-211">Первая запись должна быть именем токена для поиска в источнике конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="168b1-212">Построители конфигураций в Microsoft. Configuration. ConfigurationBuilders</span><span class="sxs-lookup"><span data-stu-id="168b1-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="168b1-213">енвиронментконфигбуилдер</span><span class="sxs-lookup"><span data-stu-id="168b1-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="168b1-214">[Енвиронментконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="168b1-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="168b1-215">— Это самая простая из построителей конфигураций.</span><span class="sxs-lookup"><span data-stu-id="168b1-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="168b1-216">Считывает значения из среды.</span><span class="sxs-lookup"><span data-stu-id="168b1-216">Reads values from the environment.</span></span>
* <span data-ttu-id="168b1-217">Не имеет дополнительных параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="168b1-218">Значение атрибута `name` является произвольным.</span><span class="sxs-lookup"><span data-stu-id="168b1-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="168b1-219">**Примечание.** В среде контейнера Windows переменные, заданные во время выполнения, вставляются только в среду процесса EntryPoint.</span><span class="sxs-lookup"><span data-stu-id="168b1-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="168b1-220">Приложения, работающие как службы или процессы, не являющиеся точкой входа, не получают эти переменные, если они не вставляются через механизм в контейнере.</span><span class="sxs-lookup"><span data-stu-id="168b1-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="168b1-221">Для [служб IIS](https://github.com/Microsoft/iis-docker/pull/41)/контейнеры на основе [ASP.NET](https://github.com/Microsoft/aspnet-docker)Текущая версия [сервицемонитор. exe](https://github.com/Microsoft/iis-docker/pull/41) обрабатывает это только в *DefaultAppPool* .</span><span class="sxs-lookup"><span data-stu-id="168b1-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="168b1-222">Другим вариантам контейнеров на основе Windows может потребоваться разработать собственный механизм внедрения для процессов, не относящихся к EntryPoint.</span><span class="sxs-lookup"><span data-stu-id="168b1-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="168b1-223">усерсекретсконфигбуилдер</span><span class="sxs-lookup"><span data-stu-id="168b1-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="168b1-224">Никогда не храните пароли, конфиденциальные строки подключения или другие конфиденциальные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="168b1-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="168b1-225">Рабочие секреты не следует использовать для разработки или тестирования.</span><span class="sxs-lookup"><span data-stu-id="168b1-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="168b1-226">Этот построитель конфигураций предоставляет функцию, аналогичную [ASP.NET Core диспетчере секретов](/aspnet/core/security/app-secrets).</span><span class="sxs-lookup"><span data-stu-id="168b1-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="168b1-227">[Усерсекретсконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) можно использовать в проектах .NET Framework, но должен быть указан секретный файл.</span><span class="sxs-lookup"><span data-stu-id="168b1-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="168b1-228">Кроме того, можно определить свойство `UserSecretsId` в файле проекта и создать необработанный файл секретов в правильном расположении для чтения.</span><span class="sxs-lookup"><span data-stu-id="168b1-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="168b1-229">Для сохранения внешних зависимостей в проекте секретный файл имеет формат XML.</span><span class="sxs-lookup"><span data-stu-id="168b1-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="168b1-230">Форматирование XML является подробным описанием реализации, и формат не должен рассчитываться на этот момент.</span><span class="sxs-lookup"><span data-stu-id="168b1-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="168b1-231">Если необходимо совместно использовать файл *секреты. JSON* с проектами .NET Core, рассмотрите возможность использования [симплежсонконфигбуилдер](#simplejsonconfigbuilder).</span><span class="sxs-lookup"><span data-stu-id="168b1-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="168b1-232">Формат `SimpleJsonConfigBuilder` для .NET Core также следует рассматривать как сведения о реализации, которые могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="168b1-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="168b1-233">Атрибуты конфигурации для `UserSecretsConfigBuilder`:</span><span class="sxs-lookup"><span data-stu-id="168b1-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="168b1-234">`userSecretsId` — это предпочтительный метод для определения XML-файла секретов.</span><span class="sxs-lookup"><span data-stu-id="168b1-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="168b1-235">Он работает аналогично .NET Core, который использует свойство проекта `UserSecretsId` для хранения этого идентификатора.</span><span class="sxs-lookup"><span data-stu-id="168b1-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="168b1-236">Строка должна быть уникальной, она не должна быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="168b1-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="168b1-237">С помощью этого атрибута `UserSecretsConfigBuilder` искать секретный файл, принадлежащий этому идентификатору, в известном локальном расположении (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`).</span><span class="sxs-lookup"><span data-stu-id="168b1-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="168b1-238">`userSecretsFile` — необязательный атрибут, указывающий файл, содержащий секреты.</span><span class="sxs-lookup"><span data-stu-id="168b1-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="168b1-239">Символ `~` можно использовать в начале для ссылки на корень приложения.</span><span class="sxs-lookup"><span data-stu-id="168b1-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="168b1-240">Требуется этот атрибут или атрибут `userSecretsId`.</span><span class="sxs-lookup"><span data-stu-id="168b1-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="168b1-241">Если указаны оба значения, `userSecretsFile` имеет приоритет.</span><span class="sxs-lookup"><span data-stu-id="168b1-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="168b1-242">`optional`: Boolean, значение по умолчанию `true` — предотвращает исключение, если не удается найти секретный файл.</span><span class="sxs-lookup"><span data-stu-id="168b1-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="168b1-243">Значение атрибута `name` является произвольным.</span><span class="sxs-lookup"><span data-stu-id="168b1-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="168b1-244">Секретный файл имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="168b1-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="168b1-245">азурекэйваултконфигбуилдер</span><span class="sxs-lookup"><span data-stu-id="168b1-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="168b1-246">[Азурекэйваултконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) считывает значения, хранящиеся в [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="168b1-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="168b1-247">требуется `vaultName` (имя хранилища или URI-адрес хранилища).</span><span class="sxs-lookup"><span data-stu-id="168b1-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="168b1-248">Другие атрибуты позволяют управлять тем, к какому хранилищу подключаться, но это необходимо только в том случае, если приложение работает не в среде, работающей с `Microsoft.Azure.Services.AppAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="168b1-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="168b1-249">Библиотека проверки подлинности служб Azure используется для автоматического выбора сведений о подключении из среды выполнения, если это возможно.</span><span class="sxs-lookup"><span data-stu-id="168b1-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="168b1-250">Вы можете переопределить автоматическое получение сведений о соединении, предоставив строку подключения.</span><span class="sxs-lookup"><span data-stu-id="168b1-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="168b1-251">`vaultName` — требуется, если `uri` не предоставлены.</span><span class="sxs-lookup"><span data-stu-id="168b1-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="168b1-252">Указывает имя хранилища в подписке Azure, из которого считываются пары "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="168b1-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="168b1-253">`connectionString` — строка подключения, используемая [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span><span class="sxs-lookup"><span data-stu-id="168b1-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="168b1-254">`uri` — подключается к другим поставщикам Key Vault с указанным значением `uri`.</span><span class="sxs-lookup"><span data-stu-id="168b1-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="168b1-255">Если этот параметр не указан, Azure (`vaultName`) является поставщиком хранилища.</span><span class="sxs-lookup"><span data-stu-id="168b1-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="168b1-256">`version`-Azure Key Vault предоставляет функцию управления версиями для секретов.</span><span class="sxs-lookup"><span data-stu-id="168b1-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="168b1-257">Если указан `version`, построитель получит только секреты, соответствующие этой версии.</span><span class="sxs-lookup"><span data-stu-id="168b1-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="168b1-258">`preloadSecretNames`. по умолчанию этот конструктор запрашивает **все** имена ключей в хранилище ключей при инициализации.</span><span class="sxs-lookup"><span data-stu-id="168b1-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="168b1-259">Чтобы предотвратить чтение всех значений ключей, присвойте этому атрибуту значение `false`.</span><span class="sxs-lookup"><span data-stu-id="168b1-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="168b1-260">Если задать для этого параметра значение `false` считывает секреты по одному за раз.</span><span class="sxs-lookup"><span data-stu-id="168b1-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="168b1-261">Чтение секретов по одному может оказаться полезным, если хранилище разрешает доступ "Get", но не "List".</span><span class="sxs-lookup"><span data-stu-id="168b1-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="168b1-262">**Примечание.** При использовании режима `Greedy` `preloadSecretNames` должен быть `true` (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="168b1-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="168b1-263">кэйперфилеконфигбуилдер</span><span class="sxs-lookup"><span data-stu-id="168b1-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="168b1-264">[Кэйперфилеконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) — это базовый построитель конфигураций, в котором файлы каталога используются в качестве источника значений.</span><span class="sxs-lookup"><span data-stu-id="168b1-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="168b1-265">Имя файла является ключом, а содержимое — значением.</span><span class="sxs-lookup"><span data-stu-id="168b1-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="168b1-266">Этот построитель конфигурации может быть полезен при работе в управляемой среде контейнера.</span><span class="sxs-lookup"><span data-stu-id="168b1-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="168b1-267">Такие системы, как DOCKER Swarm и Kubernetes, предоставляют `secrets` своим управляемым контейнерам Windows в соответствии с этим ключом для каждого файла.</span><span class="sxs-lookup"><span data-stu-id="168b1-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="168b1-268">Сведения об атрибуте:</span><span class="sxs-lookup"><span data-stu-id="168b1-268">Attribute details:</span></span>

* <span data-ttu-id="168b1-269">`directoryPath` — обязательный.</span><span class="sxs-lookup"><span data-stu-id="168b1-269">`directoryPath` - Required.</span></span> <span data-ttu-id="168b1-270">Указывает путь для поиска значений.</span><span class="sxs-lookup"><span data-stu-id="168b1-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="168b1-271">Docker для Windows секреты по умолчанию хранятся в каталоге *к:\програмдата\доккер\секретс* .</span><span class="sxs-lookup"><span data-stu-id="168b1-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="168b1-272">`ignorePrefix`-файлы, начинающиеся с этого префикса, исключаются.</span><span class="sxs-lookup"><span data-stu-id="168b1-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="168b1-273">Значение по умолчанию — "ignore.".</span><span class="sxs-lookup"><span data-stu-id="168b1-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="168b1-274">`keyDelimiter` — значение по умолчанию — `null`.</span><span class="sxs-lookup"><span data-stu-id="168b1-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="168b1-275">Если этот параметр указан, построитель конфигурации проходит по нескольким уровням каталога, создавая имена ключей с помощью этого разделителя.</span><span class="sxs-lookup"><span data-stu-id="168b1-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="168b1-276">Если это значение равно `null`, построитель конфигурации рассматривает только верхний уровень каталога.</span><span class="sxs-lookup"><span data-stu-id="168b1-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="168b1-277">`optional` — значение по умолчанию — `false`.</span><span class="sxs-lookup"><span data-stu-id="168b1-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="168b1-278">Указывает, должны ли построитель конфигурации вызывать ошибки, если исходный каталог не существует.</span><span class="sxs-lookup"><span data-stu-id="168b1-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="168b1-279">симплежсонконфигбуилдер</span><span class="sxs-lookup"><span data-stu-id="168b1-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="168b1-280">Никогда не храните пароли, конфиденциальные строки подключения или другие конфиденциальные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="168b1-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="168b1-281">Рабочие секреты не следует использовать для разработки или тестирования.</span><span class="sxs-lookup"><span data-stu-id="168b1-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="168b1-282">Проекты .NET Core часто используют JSON файлы для настройки.</span><span class="sxs-lookup"><span data-stu-id="168b1-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="168b1-283">Построитель [симплежсонконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) позволяет использовать файлы JSON .NET Core в .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="168b1-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="168b1-284">Этот построитель конфигураций обеспечивает базовое сопоставление из источника «ключ-значение» с конкретными областями «ключ-значение» .NET Framework конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="168b1-285">Этот построитель конфигураций **не** предоставляет иерархические конфигурации.</span><span class="sxs-lookup"><span data-stu-id="168b1-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="168b1-286">Резервный файл JSON подобен словарю, а не сложному иерархическому объекту.</span><span class="sxs-lookup"><span data-stu-id="168b1-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="168b1-287">Можно использовать многоуровневый иерархический файл.</span><span class="sxs-lookup"><span data-stu-id="168b1-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="168b1-288">Этот поставщик `flatten`глубиной, добавляя имя свойства на каждом уровне, используя `:` в качестве разделителя.</span><span class="sxs-lookup"><span data-stu-id="168b1-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="168b1-289">Сведения об атрибуте:</span><span class="sxs-lookup"><span data-stu-id="168b1-289">Attribute details:</span></span>

* <span data-ttu-id="168b1-290">`jsonFile` — обязательный.</span><span class="sxs-lookup"><span data-stu-id="168b1-290">`jsonFile` - Required.</span></span> <span data-ttu-id="168b1-291">Указывает JSON файл, из которого производится чтение.</span><span class="sxs-lookup"><span data-stu-id="168b1-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="168b1-292">Символ `~` можно использовать в начале для ссылки на корень приложения.</span><span class="sxs-lookup"><span data-stu-id="168b1-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="168b1-293">`optional`-Boolean, значение по умолчанию — `true`.</span><span class="sxs-lookup"><span data-stu-id="168b1-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="168b1-294">Предотвращает создание исключений, если не удается найти JSON файл.</span><span class="sxs-lookup"><span data-stu-id="168b1-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="168b1-295">`jsonMode` - `[Flat|Sectional]`.</span><span class="sxs-lookup"><span data-stu-id="168b1-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="168b1-296">Значение по умолчанию — `Flat`.</span><span class="sxs-lookup"><span data-stu-id="168b1-296">`Flat` is the default.</span></span> <span data-ttu-id="168b1-297">Если `jsonMode` `Flat`, JSON-файл является одним плоским источником «ключ-значение».</span><span class="sxs-lookup"><span data-stu-id="168b1-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="168b1-298">`EnvironmentConfigBuilder` и `AzureKeyVaultConfigBuilder` также являются единичными источниками «ключ-значение».</span><span class="sxs-lookup"><span data-stu-id="168b1-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="168b1-299">Когда `SimpleJsonConfigBuilder` настраивается в режиме `Sectional`:</span><span class="sxs-lookup"><span data-stu-id="168b1-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="168b1-300">Файл JSON концептуально делится на несколько словарей только на верхнем уровне.</span><span class="sxs-lookup"><span data-stu-id="168b1-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="168b1-301">Каждый из словарей применяется только к разделу конфигурации, который соответствует имени свойства верхнего уровня, присоединенному к ним.</span><span class="sxs-lookup"><span data-stu-id="168b1-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="168b1-302">Например:</span><span class="sxs-lookup"><span data-stu-id="168b1-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="168b1-303">Реализация пользовательского построителя конфигурации "ключ — значение"</span><span class="sxs-lookup"><span data-stu-id="168b1-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="168b1-304">Если построители конфигураций не соответствуют вашим потребностям, вы можете написать собственный.</span><span class="sxs-lookup"><span data-stu-id="168b1-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="168b1-305">Базовый класс `KeyValueConfigBuilder` обрабатывает режимы подстановки и большинство проблем префикса.</span><span class="sxs-lookup"><span data-stu-id="168b1-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="168b1-306">Для реализации проекта требуется только:</span><span class="sxs-lookup"><span data-stu-id="168b1-306">An implementing project need only:</span></span>

* <span data-ttu-id="168b1-307">Наследование от базового класса и реализация базового источника пар "ключ-значение" с помощью `GetValue` и `GetAllValues`:</span><span class="sxs-lookup"><span data-stu-id="168b1-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="168b1-308">Добавьте в проект [Microsoft. Configuration. ConfigurationBuilders. base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) .</span><span class="sxs-lookup"><span data-stu-id="168b1-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="168b1-309">Базовый класс `KeyValueConfigBuilder` предоставляет большую часть работы и согласованное поведение для построителей конфигурации "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="168b1-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="168b1-310">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="168b1-310">Additional resources</span></span>

* [<span data-ttu-id="168b1-311">Репозиторий GitHub для сборщиков конфигураций</span><span class="sxs-lookup"><span data-stu-id="168b1-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="168b1-312">Проверка подлинности между службами для Azure Key Vault с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="168b1-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
