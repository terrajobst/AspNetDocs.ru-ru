---
uid: whitepapers/side-by-side-with-10
title: ASP.NET параллельное выполнение .NET Framework 1,0 и 1,1 | Документация Майкрософт
author: rick-anderson
description: В этом техническом документе описывается установка .NET 1,0 и .NET 1,1 на компьютере, что позволяет веб-приложению ASP.NET работать в любой версии Фрам...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513834"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="2ef08-103">Параллельное выполнение нескольких версий .NET Framework 1.0 и 1.1 в ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2ef08-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="2ef08-104">В этом техническом документе описывается установка .NET 1,0 и .NET 1,1 на компьютере, что позволяет веб-приложению ASP.NET работать в любой версии платформы.</span><span class="sxs-lookup"><span data-stu-id="2ef08-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="2ef08-105">Применяется к ASP.NET 1,0 и ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="2ef08-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="2ef08-106">В ASP.NET приложения говорят, что они работают параллельно, если они установлены на одном компьютере, но используют разные версии .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ef08-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="2ef08-107">В следующем разделе описывается настройка приложений ASP.NET для параллельного выполнения и даются подробные инструкции по выполнению следующих действий.</span><span class="sxs-lookup"><span data-stu-id="2ef08-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="2ef08-108">Поддержание сопоставления веб-приложения с .NET Framework версии 1,0 во время установки</span><span class="sxs-lookup"><span data-stu-id="2ef08-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="2ef08-109">Сопоставьте веб-приложение с определенной версией .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2ef08-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="2ef08-110">Поиск версии .NET Framework, используемой веб-сайтом</span><span class="sxs-lookup"><span data-stu-id="2ef08-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="2ef08-111">Обычно при обновлении компонента или приложения на компьютере старая версия удаляется и заменяется новой версией.</span><span class="sxs-lookup"><span data-stu-id="2ef08-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="2ef08-112">Если новая версия несовместима с предыдущей, это обычно приводит к разрыву работы других приложений, использующих этот компонент или приложение.</span><span class="sxs-lookup"><span data-stu-id="2ef08-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="2ef08-113">.NET Framework обеспечивает поддержку параллельного выполнения, что позволяет одновременно установить на одном компьютере несколько версий сборки или приложения одновременно.</span><span class="sxs-lookup"><span data-stu-id="2ef08-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="2ef08-114">Поскольку несколько версий можно установить одновременно, управляемые приложения могут выбрать версию, которая будет использоваться, не влияя на приложения, использующие другую версию.</span><span class="sxs-lookup"><span data-stu-id="2ef08-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="2ef08-115">По умолчанию во время установки .NET Framework версии 1,1 все существующие приложения ASP.NET автоматически перестраиваются для использования последней версии .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ef08-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="2ef08-116">Если вы не хотите, чтобы приложения ASP.NET по умолчанию .NET Framework 1,1, щелкните [здесь](#1) , чтобы узнать, как предотвратить это во время установки.</span><span class="sxs-lookup"><span data-stu-id="2ef08-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="2ef08-117">Если вы обновите веб-сервер до .NET Framework 1,1 и хотите, чтобы одно или несколько веб-приложений выполняли .NET Framework 1,0, необходимо обновить карту сценариев службы IIS (IIS).</span><span class="sxs-lookup"><span data-stu-id="2ef08-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="2ef08-118">Сопоставление сценариев — это механизм сопоставления расширения ASPX-файла для конкретного веб приложения с версией .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ef08-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="2ef08-119">Щелкните [здесь](#2) , чтобы узнать, как сопоставлять веб-приложения с определенной версией .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ef08-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="2ef08-120">Вы можете использовать диспетчер Internet Information Manager или средство регистрации ASP.NET IIS (ASPNET\_regiis. exe), чтобы найти .NET Framework версию, на которой выполняется определенное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="2ef08-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="2ef08-121">Щелкните [здесь](#3) , чтобы узнать, как найти версию .NET Framework, используемую веб-сайтом.</span><span class="sxs-lookup"><span data-stu-id="2ef08-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="2ef08-122">При переходе на .NET Framework 1,1 в каждой версии .NET Framework используется собственный файл Machine. config.</span><span class="sxs-lookup"><span data-stu-id="2ef08-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="2ef08-123">В результате, если веб-администратор внес изменения в файл Machine. config, эти изменения необходимо перенести в файл Machine. config .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="2ef08-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="2ef08-124">Поддержание сопоставления веб-приложения с .NET Framework 1,0 во время установки</span><span class="sxs-lookup"><span data-stu-id="2ef08-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="2ef08-125">По умолчанию все существующие приложения ASP.NET автоматически перестраиваются во время установки, чтобы использовать более новую версию .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ef08-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="2ef08-126">Используя более новую версию .NET Framework, приложения могут воспользоваться всеми преимуществами усовершенствований и новых функций, реализованных в новом выпуске.</span><span class="sxs-lookup"><span data-stu-id="2ef08-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="2ef08-127">В то же время веб-администратор, которому может потребоваться детальный контроль над тем, какие приложения обновляются, может предотвратить автоматическое повторное сопоставление всех существующих ASP.NET приложений во время установки .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ef08-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="2ef08-128">Чтобы предотвратить автоматическое повторное сопоставление всего приложения ASP.NET с новой версией .NET Framework, веб-администратор может использовать параметр командной строки/ноаспупграде с программой установки Dotnetfx. exe.</span><span class="sxs-lookup"><span data-stu-id="2ef08-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="2ef08-129">**Предотвращение общего пересопоставления приложения ASP.NET с новой версией**</span><span class="sxs-lookup"><span data-stu-id="2ef08-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="2ef08-130">Выберите **Пуск**.</span><span class="sxs-lookup"><span data-stu-id="2ef08-130">Go to **Start**.</span></span>
2. <span data-ttu-id="2ef08-131">Щелкните **выполнить**.</span><span class="sxs-lookup"><span data-stu-id="2ef08-131">Click on **run**.</span></span>
3. <span data-ttu-id="2ef08-132">Наберите команду **cmd**.</span><span class="sxs-lookup"><span data-stu-id="2ef08-132">Type **cmd**.</span></span>
4. <span data-ttu-id="2ef08-133">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2ef08-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="2ef08-134">В командной строке введите следующую строку, чтобы начать установку .NET Framework: **Dotnetfx. exe/c: "Install/ноаспупграде?** .</span><span class="sxs-lookup"><span data-stu-id="2ef08-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="2ef08-135">Нажмите кнопку **Да** в программе установки Microsoft .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="2ef08-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="2ef08-136">Это приведет к запуску процесса установки .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="2ef08-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="2ef08-137">Сопоставьте веб-приложение с определенной версией .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2ef08-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="2ef08-138">Каждая версия .NET Framework включает версию средства регистрации служб IIS ASP.NET (ASPNET\_regiis. exe).</span><span class="sxs-lookup"><span data-stu-id="2ef08-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="2ef08-139">Это средство позволяет администраторам указать, что веб-приложение должно выполняться в определенной версии .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ef08-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="2ef08-140">Это называется сопоставлением веб-приложения с версией .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ef08-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="2ef08-141">Администраторы должны выбрать ASPNET\_regiis. exe, соответствующий версии .NET Framework, которая будет связана с веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="2ef08-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="2ef08-142">Например, администратор, желающий указать, что веб-сайт использует .NET Framework 1,1, должен использовать ASPNET\_regiis. exe, поставляемый с .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="2ef08-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="2ef08-143">Файл ASPNET\_regiis. exe для версии 1,0 находится по адресу:</span><span class="sxs-lookup"><span data-stu-id="2ef08-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="2ef08-144">К:\виндовс\микрософт.нет\фрамеворк\\**v 1.0.3705**\ASPNET\_regiis</span><span class="sxs-lookup"><span data-stu-id="2ef08-144">C:\WINDOWS\Microsoft.NET\Framework\\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="2ef08-145">Файл ASPNET\_regiis. exe для версии 1, 1 находится по адресу:</span><span class="sxs-lookup"><span data-stu-id="2ef08-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="2ef08-146">К:\виндовс\микрософт.нет\фрамеворк\\**v 1.1.4322**\ASPNET\_regiis</span><span class="sxs-lookup"><span data-stu-id="2ef08-146">C:\WINDOWS\Microsoft.NET\Framework\\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="2ef08-147">ASPNET\_regiis. exe предоставляет два варианта создания сценариев для сопоставления веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="2ef08-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="2ef08-148">**-s** задает схему скрипта в пути и в ее дочерних каталогах.</span><span class="sxs-lookup"><span data-stu-id="2ef08-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="2ef08-149">**-SN** задает схему сценария только в пути.</span><span class="sxs-lookup"><span data-stu-id="2ef08-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="2ef08-150">Путь определяет путь метаданных IIS веб-приложения, который определен в формате W3SVC/ROOT/{Вебситенумбер}/{имя приложения\_}.</span><span class="sxs-lookup"><span data-stu-id="2ef08-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="2ef08-151">Например, для веб-приложения с именем Portal, расположенным на веб-сайте по умолчанию, путь к метабазе — W3SVC/1/ROOT/портал.</span><span class="sxs-lookup"><span data-stu-id="2ef08-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="2ef08-152">Примечание. для получения пути к метабазе можно также использовать средство, называемое редактором метабазы.</span><span class="sxs-lookup"><span data-stu-id="2ef08-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="2ef08-153">Это средство можно загрузить на служба поддержки Майкрософт сайте по адресу [https://support.microsoft.com/default.aspx?scid=kb; en-US; 232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span><span class="sxs-lookup"><span data-stu-id="2ef08-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="2ef08-154">Выполните команду ASPNET\_regiis. exe-s W3SVC/1/ROOT/портал, чтобы обновить карту скриптов IIS портала и ее подприложение.</span><span class="sxs-lookup"><span data-stu-id="2ef08-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="2ef08-155">Выполните команду ASPNET\_regiis. exe-SN W3SVC/1/ROOT/портал, чтобы обновить карту сценариев портала IIS, не затрагивая приложения в подкаталогах портала.</span><span class="sxs-lookup"><span data-stu-id="2ef08-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="2ef08-156">Поиск версии .NET Framework, используемой веб-приложением</span><span class="sxs-lookup"><span data-stu-id="2ef08-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="2ef08-157">Администратор может использовать Service Manager Интернета, чтобы узнать, какая версия .NET Framework запускает веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="2ef08-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="2ef08-158">Разные версии операционных систем запускают Интернет-Service Manager по-другому.</span><span class="sxs-lookup"><span data-stu-id="2ef08-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="2ef08-159">Чтобы запустить Service Manager, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="2ef08-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="2ef08-160">**Запуск Service Manager Интернета**</span><span class="sxs-lookup"><span data-stu-id="2ef08-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="2ef08-161">Выберите **Пуск**.</span><span class="sxs-lookup"><span data-stu-id="2ef08-161">Go to **Start**.</span></span>
2. <span data-ttu-id="2ef08-162">Щелкните **выполнить**.</span><span class="sxs-lookup"><span data-stu-id="2ef08-162">Click on **run**.</span></span>
3. <span data-ttu-id="2ef08-163">Введите **inetmgr**.</span><span class="sxs-lookup"><span data-stu-id="2ef08-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="2ef08-164">В Service Manager Интернета выберите веб-приложение, версию .NET Framework которого необходимо получить.</span><span class="sxs-lookup"><span data-stu-id="2ef08-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="2ef08-165">Щелкните правой кнопкой мыши веб-приложение и выберите пункт **Свойства.**</span><span class="sxs-lookup"><span data-stu-id="2ef08-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="2ef08-166">В окне свойств выберите **Конфигурация.**</span><span class="sxs-lookup"><span data-stu-id="2ef08-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="2ef08-167">В таблице сопоставление приложений выберите **ASPX**и нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="2ef08-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="2ef08-168">В текстовом поле **исполняемый объект** просмотрите каталог версий, прокрутите его.</span><span class="sxs-lookup"><span data-stu-id="2ef08-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="2ef08-169">Если каталог версий — v. 1.1.4322, приложение сопоставляется с .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="2ef08-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="2ef08-170">И наоборот, если каталог версии — версия 1.0.3705, приложение сопоставляется с .NET Framework 1,0.</span><span class="sxs-lookup"><span data-stu-id="2ef08-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
