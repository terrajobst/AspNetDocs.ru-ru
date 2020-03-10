---
uid: web-pages/readme/overview
title: Файл readme для WebMatrix | Документация Майкрософт
author: rick-anderson
description: Файл сведений о выпуске WebMatrix и веб-страницы ASP.NET (Razor) 1,0
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454272"
---
# <a name="webmatrix-readme"></a><span data-ttu-id="77c4d-103">Файл сведений для WebMatrix</span><span class="sxs-lookup"><span data-stu-id="77c4d-103">WebMatrix Readme</span></span>

<span data-ttu-id="77c4d-104">13 января 2011</span><span class="sxs-lookup"><span data-stu-id="77c4d-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="77c4d-105">Содержимое</span><span class="sxs-lookup"><span data-stu-id="77c4d-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="77c4d-106">Этот файл readme относится к выпуску 1,0 WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="77c4d-106">This readme applies to the 1.0 release of WebMatrix.</span></span>

- [<span data-ttu-id="77c4d-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="77c4d-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="77c4d-108">Установка</span><span class="sxs-lookup"><span data-stu-id="77c4d-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="77c4d-109">Публикация приложений</span><span class="sxs-lookup"><span data-stu-id="77c4d-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="77c4d-110">Изменения и проблемы</span><span class="sxs-lookup"><span data-stu-id="77c4d-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="77c4d-111">Установка WebMatrix 1,0</span><span class="sxs-lookup"><span data-stu-id="77c4d-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="77c4d-112">Веб-страницы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="77c4d-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="77c4d-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="77c4d-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="77c4d-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="77c4d-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="77c4d-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="77c4d-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="77c4d-116">Установка приложений</span><span class="sxs-lookup"><span data-stu-id="77c4d-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="77c4d-117">Публикация приложений</span><span class="sxs-lookup"><span data-stu-id="77c4d-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="77c4d-118">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="77c4d-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="77c4d-119">Обзор</span><span class="sxs-lookup"><span data-stu-id="77c4d-119">Overview</span></span>

> <span data-ttu-id="77c4d-120">Microsoft WebMatrix 1,0 — это бесплатный стек веб-разработки, устанавливаемый за считанные минуты.</span><span class="sxs-lookup"><span data-stu-id="77c4d-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="77c4d-121">Он интегрирует веб-сервер с платформами баз данных и программирования для создания единого интегрированного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="77c4d-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="77c4d-122">WebMatrix можно использовать для оптимизации кода, тестирования и публикации собственного веб-сайта ASP.NET или PHP. также можно использовать WebMatrix для запуска нового веб-сайта с помощью популярных приложений с открытым исходным кодом, таких как DotNetNuke, Umbraco, WordPress или Joomla.</span><span class="sxs-lookup"><span data-stu-id="77c4d-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="77c4d-123">WebMatrix использует тот же мощный веб-сервер, ядро СУБД и среду, которая будет запускать ваш веб-сайт в Интернете, что делает переход от разработки к рабочей среде беспрепятственно и плавно.</span><span class="sxs-lookup"><span data-stu-id="77c4d-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="77c4d-124">Установка</span><span class="sxs-lookup"><span data-stu-id="77c4d-124">Installation</span></span>

> <span data-ttu-id="77c4d-125">Чтобы установить WebMatrix 1,0, необходимо сначала установить [установщик веб-платформы Майкрософт 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="77c4d-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="77c4d-126">После установки установщика веб-платформы его можно использовать для установки WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="77c4d-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="77c4d-127">При возникновении проблем во время установки обратитесь к разделу [Устранение неполадок с установщик веб-платформы Майкрософт](https://go.microsoft.com/fwlink/?LinkId=196212).</span><span class="sxs-lookup"><span data-stu-id="77c4d-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="77c4d-128">Публикация приложений</span><span class="sxs-lookup"><span data-stu-id="77c4d-128">How to Publish Applications</span></span>

> <span data-ttu-id="77c4d-129">См. [Пошаговые инструкции по публикации приложений](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="77c4d-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="77c4d-130">Изменения и проблемы</span><span class="sxs-lookup"><span data-stu-id="77c4d-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="77c4d-131">Проблемы с установкой WebMatrix 1,0</span><span class="sxs-lookup"><span data-stu-id="77c4d-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="77c4d-132">Вопрос. WebMatrix 1,0 доступен только на платформах, поддерживающих Microsoft .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="77c4d-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="77c4d-133">Для WebMatrix требуется .NET Framework версии 4.</span><span class="sxs-lookup"><span data-stu-id="77c4d-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="77c4d-134">В некоторых случаях установщик WebMatrix 1,0 попытается установить на платформу, которая не входит в набор поддерживаемых конфигураций.</span><span class="sxs-lookup"><span data-stu-id="77c4d-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="77c4d-135">В частности, Windows Vista без обновления с пакетом обновления 1 (SP1) позволит начать установку WebMatrix, но компонент .NET Framework 4 завершится сбоем и заблокирует установку.</span><span class="sxs-lookup"><span data-stu-id="77c4d-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="77c4d-136">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-136">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-137">Установите на поддерживаемой платформе, которая включает в себя:</span><span class="sxs-lookup"><span data-stu-id="77c4d-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="77c4d-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="77c4d-138">Windows 7</span></span>
> - <span data-ttu-id="77c4d-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="77c4d-139">Windows Server 2008</span></span>
> - <span data-ttu-id="77c4d-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="77c4d-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="77c4d-141">Windows Vista с пакетом обновления 1 (SP1) или выше</span><span class="sxs-lookup"><span data-stu-id="77c4d-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="77c4d-142">Windows XP с пакетом обновления 3 (SP3)</span><span class="sxs-lookup"><span data-stu-id="77c4d-142">Windows XP SP3</span></span>
> - <span data-ttu-id="77c4d-143">Windows Server 2003 с пакетом обновления 2 (SP2)</span><span class="sxs-lookup"><span data-stu-id="77c4d-143">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="77c4d-144">Ошибка: не удается установить WebMatrix 1,0, если Microsoft Visual Studio 2008 установлен без Microsoft Visual Studio 2008 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="77c4d-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="77c4d-145">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-145">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-146">Установите [Microsoft Visual Studio 2008 с пакетом обновления 1 (SP1)](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) из центра загрузки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="77c4d-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="77c4d-147">Причина. Некоторые сборки для SQL Server Compact 4,0 не установлены в GAC</span><span class="sxs-lookup"><span data-stu-id="77c4d-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="77c4d-148">Управляемые сборки для SQL Server Compact 4,0 не помещаются в глобальный кэш сборок (GAC) при установке SQL Server Compact 4,0 на 64-разрядном компьютере, а на компьютере установлен только клиентский профиль .NET Framework 3,5 SP1.</span><span class="sxs-lookup"><span data-stu-id="77c4d-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="77c4d-149">В глобальный кэш сборок не установлены следующие управляемые сборки:</span><span class="sxs-lookup"><span data-stu-id="77c4d-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="77c4d-150">*System. Data. SqlServerCe. dll* (поставщик ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="77c4d-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="77c4d-151">*System. Data. SqlServerCe. Entity. dll* (ADO.NET Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="77c4d-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="77c4d-152">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-152">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-153">Удалите SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="77c4d-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="77c4d-154">Скачайте и установите полную версию .NET Framework 3,5 с пакетом обновления 1 (SP1) из следующего расположения:</span><span class="sxs-lookup"><span data-stu-id="77c4d-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="77c4d-155">Microsoft .NET Framework 3,5 с пакетом обновления 1 (SP1) (полный пакет)</span><span class="sxs-lookup"><span data-stu-id="77c4d-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="77c4d-156">Затем переустановите SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="77c4d-156">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="77c4d-157">Ошибка: не удается удалить SQL Server Compact с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="77c4d-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="77c4d-158">Удаление SQL Server Compact с помощью параметров командной строки не работает в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="77c4d-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="77c4d-159">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-159">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-160">Используйте *программы и компоненты* на панели управления Windows для удаления Microsoft SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="77c4d-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="77c4d-161">Веб-страницы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="77c4d-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="77c4d-162">В этом разделе документа описаны новые функции, изменения и известные проблемы с выпуском 1,0 веб-страницы ASP.NET с синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="77c4d-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="77c4d-163">Новые функции</span><span class="sxs-lookup"><span data-stu-id="77c4d-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="77c4d-164">Изменения</span><span class="sxs-lookup"><span data-stu-id="77c4d-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="77c4d-165">Проблемы</span><span class="sxs-lookup"><span data-stu-id="77c4d-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a><span data-ttu-id="77c4d-166">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="77c4d-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="77c4d-167">Новый: добавлен параметр конфигурации для отключения диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="77c4d-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="77c4d-168">Новый ключ `asp:AdminManagerEnabled` доступен для элемента `<appSettings>` в файле *Web. config* , который позволяет полностью отключить диспетчер пакетов.</span><span class="sxs-lookup"><span data-stu-id="77c4d-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="77c4d-169">Значение по умолчанию для этого элемента равно true, то есть если оно не включено в файл *Web. config* , диспетчер пакетов включен.</span><span class="sxs-lookup"><span data-stu-id="77c4d-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="77c4d-170">Чтобы отключить диспетчер пакетов, добавьте следующий элемент в файл *Web. config* в корневой папке веб-сайта:</span><span class="sxs-lookup"><span data-stu-id="77c4d-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a><span data-ttu-id="77c4d-171">Изменениями</span><span class="sxs-lookup"><span data-stu-id="77c4d-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="77c4d-172">Изменение: раздел "веб-страницы: Админфолдервиртуалпас" переименован в "ASP: Админфолдервиртуалпас"</span><span class="sxs-lookup"><span data-stu-id="77c4d-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="77c4d-173">Ключ `webPages:AdminFolderVirtualPath`, который можно добавить в файл *Web. config* для указания расположения диспетчера пакетов, был переименован для использования пространства имен `asp:` вместо пространства имен `webPages`.</span><span class="sxs-lookup"><span data-stu-id="77c4d-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="77c4d-174">Если вы использовали этот элемент, необходимо переименовать его в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="77c4d-174">If you have used this element, you must rename it in the configuration file.</span></span>

#### <a id="Issues"></a> <span data-ttu-id="77c4d-175">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="77c4d-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="77c4d-176">Ошибка: пароли для пользователей членства больше не распознаются</span><span class="sxs-lookup"><span data-stu-id="77c4d-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="77c4d-177">Алгоритм создания и сохранения паролей членства (имени входа) был изменен для обеспечения большей безопасности.</span><span class="sxs-lookup"><span data-stu-id="77c4d-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="77c4d-178">В результате пароли, сохраненные для участников (пользователей), созданных в бета-версиях ASP.NET Razor, не будут распознаны.</span><span class="sxs-lookup"><span data-stu-id="77c4d-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="77c4d-179">**Обходной путь** Если сайт еще не помещен в рабочую среду, удалите записи пользователей из базы данных членства.</span><span class="sxs-lookup"><span data-stu-id="77c4d-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="77c4d-180">Если база данных находится в режиме реального времени, программным способом повторное создание существующих паролей в базе данных членства.</span><span class="sxs-lookup"><span data-stu-id="77c4d-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="77c4d-181">Причина: непредвиденное поведение при использовании пользовательской таблицы пользователя для членства</span><span class="sxs-lookup"><span data-stu-id="77c4d-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="77c4d-182">Чтобы инициализировать поставщик членства для веб-сайта ASP.NET Razor, вызовите метод `WebSecurity.InitializeDatabaseConnection`.</span><span class="sxs-lookup"><span data-stu-id="77c4d-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="77c4d-183">(В WebMatrix шаблон начального сайта включает вызов этого метода в файле *\_AppStart. cshtml* .) Если для параметра `autoCreateTables` этого метода задано значение true (по умолчанию задано значение true в шаблоне начального сайта) и если в метод передается нераспознанное имя таблицы (второй параметр), метод не вызывает ошибку.</span><span class="sxs-lookup"><span data-stu-id="77c4d-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="77c4d-184">Вместо этого он автоматически создает таблицу.</span><span class="sxs-lookup"><span data-stu-id="77c4d-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="77c4d-185">Это может быть проблемой, если вы планируете использовать настраиваемую таблицу пользователей для членства, но передать неправильное имя таблицы в метод `WebSecurity.InitializeDatabaseConnection`.</span><span class="sxs-lookup"><span data-stu-id="77c4d-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="77c4d-186">Так как метод не по умолчанию вызывает ошибку, если указанная таблица не существует, и, поскольку вместо этого создается новая таблица, приложение может работать нормально.</span><span class="sxs-lookup"><span data-stu-id="77c4d-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="77c4d-187">Однако код приложения, основанный на настраиваемой пользовательской таблице (и в полях), может в конечном итоге завершиться с непредвиденными ошибками.</span><span class="sxs-lookup"><span data-stu-id="77c4d-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="77c4d-188">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-188">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-189">Убедитесь, что имя, переданное в методе `InitializeDatabaseConnection`, совпадает с таблицей профиля пользователя в базе данных членства или убедитесь, что для параметра `autoCreateTables` задано значение false.</span><span class="sxs-lookup"><span data-stu-id="77c4d-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a><span data-ttu-id="77c4d-190">Ошибка: сообщение об ошибке "модулю администрирования требуется доступ к ~/АПП\_Data"</span><span class="sxs-lookup"><span data-stu-id="77c4d-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="77c4d-191">В некоторых обстоятельствах попытка создать пользователей или иным образом работать с системой членства в ASP.NET может привести к тому, что на странице будет отображаться сообщение об ошибке " *для модуля администрирования требуется доступ к ~/апп\_Data*.</span><span class="sxs-lookup"><span data-stu-id="77c4d-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="77c4d-192">Это происходит, если учетная запись, от которой выполняется IIS или IIS Express, не имеет разрешений на создание и запись в папку *данных приложения\_* в корневом каталоге веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="77c4d-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="77c4d-193">**Обходной путь** Вручную создайте папку *данных\_приложений* для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="77c4d-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="77c4d-194">Затем убедитесь, что учетная запись Windows, под которой выполняется приложение (обычно СЕТЕВая служба), имеет разрешения на чтение и запись для корневых папок приложения и для вложенных папок, таких как данные приложения\_.</span><span class="sxs-lookup"><span data-stu-id="77c4d-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="77c4d-195">Более подробные сведения см. в статье базы знаний [проблемы с SQL Server Express проектами создания пользовательских экземпляров и ASP.NET проектов веб-приложений](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="77c4d-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="77c4d-196">Ошибка: "не удалось создать пользовательский экземпляр SQL Server"</span><span class="sxs-lookup"><span data-stu-id="77c4d-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="77c4d-197">Если веб-приложение WebMatrix использует SQL Server Express и работает с IIS 7,5 в Windows 7 или Windows Server 2008 R2, может появиться сообщение об ошибке, свидетельствующее о том, что SQL Server не может получить путь к локальному приложению пользователя во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="77c4d-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="77c4d-198">**Обходной путь** Убедитесь, что учетная запись Windows, под которой выполняется приложение (обычно СЕТЕВая служба), имеет разрешения на чтение и запись для корневых папок приложения и для вложенных папок, таких как *данные\_приложений*.</span><span class="sxs-lookup"><span data-stu-id="77c4d-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="77c4d-199">Более подробные сведения см. в статье базы знаний [проблемы с SQL Server Express проектами создания пользовательских экземпляров и ASP.NET проектов веб-приложений](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="77c4d-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="77c4d-200">Вопрос. файлы, содержащие ресурсы диспетчера пакетов или пароли диспетчера пакетов, обслуживаемые в IIS 6,0 и более ранних версиях</span><span class="sxs-lookup"><span data-stu-id="77c4d-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="77c4d-201">Если вы развертываете приложение веб-страницы ASP.NET (Razor), которое было создано с помощью выпуска RC2, и если приложение содержит файл *Password. txt* или *паккажесаурцес. txt* в */АПП\_Data/Admin*, IIS 6,0 будет обслуживать файл по запросу, потенциально предоставляя пароли для экземпляра диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="77c4d-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="77c4d-202">**Обходной путь** Переименование файла *Password. txt* или *паккажесаурцес. txt* в файл *Password. config* или *паккажесаурцес. config*. По умолчанию службы IIS 6,0 не обслуживает файлы с расширением *config* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="77c4d-203">(В IIS 7 файлы в папке *приложения\_данных* не обслуживаются, поэтому переименовывать файлы не нужно).</span><span class="sxs-lookup"><span data-stu-id="77c4d-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="77c4d-204">Причина. при удалении пакетов, установленных с помощью бета-версии 3, компоненты пакета не полностью удаляются.</span><span class="sxs-lookup"><span data-stu-id="77c4d-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="77c4d-205">Если пакет был установлен с помощью диспетчера пакетов в выпуске Beta 3, а затем попытаться удалить его с помощью текущего выпуска, пакет не будет полностью удален.</span><span class="sxs-lookup"><span data-stu-id="77c4d-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="77c4d-206">С помощью кнопки **удаления** диспетчера пакетов можно удалить некоторые компоненты, но оставить код библиотеки пакета и не обновить файл *Package. config* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="77c4d-207">**Обходной путь** </span><span class="sxs-lookup"><span data-stu-id="77c4d-207">**Workaround** </span></span>  
> <span data-ttu-id="77c4d-208">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="77c4d-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="77c4d-209">Удалите папку *приложения\_дата\паккажес* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="77c4d-210">При этом удаляются все пакеты.</span><span class="sxs-lookup"><span data-stu-id="77c4d-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="77c4d-211">Удалите файл *Packages. config* в корневой папке веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="77c4d-211">Delete the *packages.config* file in the root of the website.</span></span>

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="77c4d-212">Вопрос. в Visual Studio при вызове диспетчера пакетов на основе веб-приложений приложение переводится в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="77c4d-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="77c4d-213">Если вы работаете в Visual Studio (не в WebMatrix) и используете *\_функцию администрирования* для запуска диспетчера пакетов, Visual Studio переводит приложение в автономный режим и отправляет приложение *\_offline. htm* в корневую папку веб-сайта, что нарушает возможность использования диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="77c4d-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="77c4d-214">Хотя это поведение обычно встречается при использовании веб-интерфейса диспетчера пакетов, такое же поведение возникает при добавлении, удалении или изменении любых файлов в папке *приложения\_данных* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="77c4d-215">**Обходной путь** </span><span class="sxs-lookup"><span data-stu-id="77c4d-215">**Workaround** </span></span>  
> <span data-ttu-id="77c4d-216">Для работы с пакетами в Visual Studio используйте расширение NuGet вместо диспетчера пакетов на основе веб-служб.</span><span class="sxs-lookup"><span data-stu-id="77c4d-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="77c4d-217">Дополнительные сведения см. в [документации по NuGet](https://docs.microsoft.com/nuget/).</span><span class="sxs-lookup"><span data-stu-id="77c4d-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="77c4d-218">Если вы работаете с другими файлами в папке *приложения\_данных* , рекомендуется хранить их в другом расположении, чтобы избежать этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="77c4d-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="77c4d-219">Если это непрактично, удалите *приложение\_автономный htm* -файл вручную или дождитесь, пока сайт снова не вернется в оперативный режим (по умолчанию через 30 секунд).</span><span class="sxs-lookup"><span data-stu-id="77c4d-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="77c4d-220">Вопрос. шаблоны IntelliSense и проектов Visual Studio доступны только в ASP.NET MVC версии 3</span><span class="sxs-lookup"><span data-stu-id="77c4d-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="77c4d-221">При установке веб-страницы ASP.NET также не устанавливаются средства для Visual Studio, такие как IntelliSense и шаблоны проектов для веб-страницы ASP.NET приложений.</span><span class="sxs-lookup"><span data-stu-id="77c4d-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="77c4d-222">**Обходной путь** Чтобы использовать IntelliSense и шаблоны проектов для веб-страницы ASP.NET приложений в Visual Studio, установите ASP.NET MVC 3 RC либо через установщик веб-платформы, либо в [автономный установщик](https://go.microsoft.com/fwlink/?LinkID=191797).</span><span class="sxs-lookup"><span data-stu-id="77c4d-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="77c4d-223">Ошибка: чтение веб-каналов или других внешних данных через прокси Server</span><span class="sxs-lookup"><span data-stu-id="77c4d-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="77c4d-224">Если сервер, на котором работает сайт, находится за прокси-сервером, может потребоваться настроить сведения о прокси-сервере в файле *Web. config* , чтобы иметь возможность считывать сведения, поступающие за пределы сайта.</span><span class="sxs-lookup"><span data-stu-id="77c4d-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="77c4d-225">Например, при использовании вспомогательного метода `ReCaptcha` вспомогательный объект взаимодействует со службой reCAPTCHA, но может быть заблокирован прокси-сервером.</span><span class="sxs-lookup"><span data-stu-id="77c4d-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="77c4d-226">Аналогичным образом, для веб-каналов, используемых в веб-страницы ASP.NET, например в канале, используемом диспетчером пакетов, может потребоваться настройка прокси.</span><span class="sxs-lookup"><span data-stu-id="77c4d-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="77c4d-227">Если возникают проблемы при работе с внешней службой или веб-каналом пакета, добавьте следующие элементы в корневой файл *Web. config* приложения:</span><span class="sxs-lookup"><span data-stu-id="77c4d-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="77c4d-228">Дополнительные сведения о настройке прокси-сервера см. в разделе [&lt;прокси-&gt; элемент (параметры сети)](https://msdn.microsoft.com/library/sa91de1e.aspx) на веб-сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="77c4d-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="77c4d-229">Ошибка: при удалении .NET Framework версии 4 отключается веб-страницы ASP.NET с синтаксисом Razor.</span><span class="sxs-lookup"><span data-stu-id="77c4d-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="77c4d-230">Если удалить .NET Framework версии 4, а затем переустановить ее, веб-страницы ASP.NET с синтаксис Razor будет отключена.</span><span class="sxs-lookup"><span data-stu-id="77c4d-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="77c4d-231">Страницы с расширением *CSHTML* выполняются неправильно.</span><span class="sxs-lookup"><span data-stu-id="77c4d-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="77c4d-232">Веб-страницы ASP.NET регистрирует сборку в корневом файле *Web. config* компьютера, а удаление .NET Framework удаляет этот файл.</span><span class="sxs-lookup"><span data-stu-id="77c4d-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="77c4d-233">При переустановке .NET Framework устанавливается новая версия файла конфигурации, но не добавляется ссылка на сборку веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="77c4d-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="77c4d-234">**Обходной путь** После переустановки .NET Framework переустановите веб-страницы ASP.NET с синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="77c4d-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="77c4d-235">В файл *Web. config* в корневой папке компьютера будет добавлен следующий элемент, который обычно находится в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="77c4d-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="77c4d-236">Ошибка: URL-адреса без расширений не могут найти файлы. cshtml/. vbhtml в IIS 7 или IIS 7,5</span><span class="sxs-lookup"><span data-stu-id="77c4d-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="77c4d-237">В IIS 7 или IIS 7,5 запросы с URL-адресом, следующим как, не могут найти страницы с расширением *CSHTML* или *VBHTML* :</span><span class="sxs-lookup"><span data-stu-id="77c4d-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="77c4d-238">Эта ошибка возникает, поскольку переписывание URL-адресов не включено по умолчанию для IIS 7 или IIS 7,5.</span><span class="sxs-lookup"><span data-stu-id="77c4d-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="77c4d-239">Сценарий ликелиест заключается в том, что вы не видите проблему при локальном тестировании с помощью IIS Express, но при развертывании веб-сайта на веб-сайте размещения эта проблема возникает.</span><span class="sxs-lookup"><span data-stu-id="77c4d-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="77c4d-240">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="77c4d-241">При наличии контроля над компьютером сервера установите обновление, описанное в разделе [обновление, которое позволяет определенным обработчикам iis 7,0 или iis 7,5 выполнять запросы, URL-адреса которых не заканчиваются точкой](https://support.microsoft.com/kb/980368).</span><span class="sxs-lookup"><span data-stu-id="77c4d-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="77c4d-242">Если у вас нет контроля над компьютером сервера (например, при развертывании на веб-сайте размещения), добавьте следующий адрес в файл *Web. config* веб-сайта:</span><span class="sxs-lookup"><span data-stu-id="77c4d-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="77c4d-243">Вопрос. Развертывание приложения на компьютере, на котором не установлен SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="77c4d-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="77c4d-244">Приложения, включающие SQL Server Compact базы данных, могут выполняться на компьютере, где не установлена SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="77c4d-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="77c4d-245">Microsoft WebMatrix 1,0 автоматически копирует эти двоичные файлы и выполняет соответствующие преобразования файла *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="77c4d-246">**Обходной путь** Если необходимо скопировать эти файлы и внести изменения в файл *Web. config* вручную, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="77c4d-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="77c4d-247">Скопируйте сборки ядра СУБД в папку *bin* (и вложенные папки) приложения на целевом компьютере:</span><span class="sxs-lookup"><span data-stu-id="77c4d-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="77c4d-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span><span class="sxs-lookup"><span data-stu-id="77c4d-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>      <span data-ttu-id="77c4d-249">**в** *\bin*</span><span class="sxs-lookup"><span data-stu-id="77c4d-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="77c4d-250">Копирование *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **в** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="77c4d-250">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **to** *\Bin\x86*</span></span>
>    - <span data-ttu-id="77c4d-251">Копирование *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* **в** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="77c4d-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 
> 2. <span data-ttu-id="77c4d-252">В корневой папке веб-сайта создайте или откройте файл *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="77c4d-253">(В WebMatrix 1,0 этот тип файлов доступен, если в диалоговом окне **Выбор типа файла** щелкнуть **все** .)</span><span class="sxs-lookup"><span data-stu-id="77c4d-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="77c4d-254">Добавьте следующий элемент в качестве дочернего для элемента `<configuration>` (не внутри элемента `<system.web>`):</span><span class="sxs-lookup"><span data-stu-id="77c4d-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="77c4d-255">Ошибка: вспомогательные функции "база данных" и "Сетка" не работают со средним уровнем доверия в Visual Basic</span><span class="sxs-lookup"><span data-stu-id="77c4d-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="77c4d-256">Если вы используете Visual Basic (создание файлов *. vbhtml* ), вспомогательные средства `Database` и `WebGrid` не будут работать, если приложение настроено для использования среднего уровня доверия.</span><span class="sxs-lookup"><span data-stu-id="77c4d-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="77c4d-257">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-257">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-258">Если вы используете Visual Studio 2010, эту проблему можно устранить, установив выпуск с пакетом обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="77c4d-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="77c4d-259">Пока не будет доступна окончательная версия пакета обновления 1 (SP1), вы можете загрузить бета-версию пакета обновления 1 (SP1) с веб-страницы [Microsoft Visual Studio 2010 с пакетом обновления](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) SP1 в центре загрузки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="77c4d-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="77c4d-260">Если это непрактично или если вы не используете Visual Studio 2010, можно временно настроить приложение для использования полного доверия.</span><span class="sxs-lookup"><span data-stu-id="77c4d-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="77c4d-261">Причина: ресурсы "Аппликатионпарт" доступны извне.</span><span class="sxs-lookup"><span data-stu-id="77c4d-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="77c4d-262">Если сборка содержит объекты, производные от класса `ApplicationPart`, то ресурсы этой сборки предоставляются классом `ResourceRouteHandler`.</span><span class="sxs-lookup"><span data-stu-id="77c4d-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="77c4d-263">Например, рассмотрим следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="77c4d-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="77c4d-264">Этот запрос скачивает все строки ресурсов в сборке *System. Web. веб-страниц. Administration. dll* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="77c4d-265">Скачаны все внедренные ресурсы (даже те, которые не предназначены для обслуживания в виде статического содержимого).</span><span class="sxs-lookup"><span data-stu-id="77c4d-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="77c4d-266">Если внедренные ресурсы содержат конфиденциальные сведения, это может представлять угрозу безопасности.</span><span class="sxs-lookup"><span data-stu-id="77c4d-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="77c4d-267">**Обходной путь** </span><span class="sxs-lookup"><span data-stu-id="77c4d-267">**Workaround** </span></span>  
> <span data-ttu-id="77c4d-268">При создании объекта **аппликатионпарт** убедитесь, что внедренные ресурсы, связанные с этой сборкой объекта **аппликатионпарт** , не содержат конфиденциальную информацию.</span><span class="sxs-lookup"><span data-stu-id="77c4d-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="77c4d-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="77c4d-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="77c4d-270">Сведения о проблемах установки для WebMatrix см. в разделе [проблемы установки WebMatrix](#Known_Issues_Installation) ранее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="77c4d-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

<span data-ttu-id="77c4d-271">В этом разделе документа описаны известные проблемы среды разработки WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="77c4d-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="77c4d-272">Ошибка. изменения имени пользователя или пароля строки подключения к базе данных в файле Web. config не отражаются в рабочей области базы данных.</span><span class="sxs-lookup"><span data-stu-id="77c4d-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="77c4d-273">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="77c4d-274">В файле *Web. config* измените имя базы данных в строке подключения (например, добавьте в нее "1").</span><span class="sxs-lookup"><span data-stu-id="77c4d-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="77c4d-275">Сохраните файл *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="77c4d-276">Щелкните **базы данных** и обновить.</span><span class="sxs-lookup"><span data-stu-id="77c4d-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="77c4d-277">Измените имя базы данных в строке подключения в файле *Web. config* на исходное имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="77c4d-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="77c4d-278">Сохраните файл *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="77c4d-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="77c4d-279">Щелкните **базы данных** и обновить.</span><span class="sxs-lookup"><span data-stu-id="77c4d-279">Click **Databases** and refresh.</span></span>

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="77c4d-280">Ошибка: невозможно удалить папки, созданные WebMatrix</span><span class="sxs-lookup"><span data-stu-id="77c4d-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="77c4d-281">Если WebMatrix работает с повышенными разрешениями (то есть запущен WebMatrix с помощью команды **Запуск от имени администратора** в Windows), папки, созданные WebMatrix, нельзя удалить с помощью проводника Windows.</span><span class="sxs-lookup"><span data-stu-id="77c4d-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="77c4d-282">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-282">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-283">Запустите проводник Windows с повышенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="77c4d-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="77c4d-284">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="77c4d-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="77c4d-285">В Windows нажмите кнопку **Пуск**.</span><span class="sxs-lookup"><span data-stu-id="77c4d-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="77c4d-286">Введите "Проводник Windows" и щелкните правой кнопкой мыши запись **проводника Windows**.</span><span class="sxs-lookup"><span data-stu-id="77c4d-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="77c4d-287">Щелкните **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="77c4d-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="77c4d-288">Затем можно удалить папки.</span><span class="sxs-lookup"><span data-stu-id="77c4d-288">You can then delete the folders.</span></span>

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="77c4d-289">Ошибка: WebMatrix 1,0 не может выполнить определенные задачи, требующие повышения прав</span><span class="sxs-lookup"><span data-stu-id="77c4d-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="77c4d-290">WebMatrix 1,0 не может выполнять определенные задачи, требующие повышения прав, например установку дополнительных компонентов в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="77c4d-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="77c4d-291">В Windows Vista или Windows 7 вы выполнили вход с учетной записью, не обладающей правами администратора, и отключена функция контроля учетных записей (UAC).</span><span class="sxs-lookup"><span data-stu-id="77c4d-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="77c4d-292">Вы используете Microsoft Windows XP или Microsoft Windows Server 2003.</span><span class="sxs-lookup"><span data-stu-id="77c4d-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="77c4d-293">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-293">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-294">Для большинства задач в WebMatrix 1,0 не требуются административные разрешения.</span><span class="sxs-lookup"><span data-stu-id="77c4d-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="77c4d-295">Для тех, кто может выполнить операцию от имени администратора, или выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="77c4d-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="77c4d-296">В Windows Vista или Windows 7 включите UAC.</span><span class="sxs-lookup"><span data-stu-id="77c4d-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="77c4d-297">В Windows XP добавьте пользователя в группу безопасности Администраторы.</span><span class="sxs-lookup"><span data-stu-id="77c4d-297">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="77c4d-298">Ошибка: "сайт из веб-коллекции" отключен</span><span class="sxs-lookup"><span data-stu-id="77c4d-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="77c4d-299">Параметр **сайт из веб-коллекции** отключен, если установщик веб-платформы 3,0 не установлен.</span><span class="sxs-lookup"><span data-stu-id="77c4d-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="77c4d-300">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-300">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-301">Установите [установщик веб-платформы Майкрософт 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="77c4d-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="77c4d-302">Причина: Google Chrome недоступен в качестве варианта выполнения</span><span class="sxs-lookup"><span data-stu-id="77c4d-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="77c4d-303">Google Chrome не отображается в списке браузеров в разделе **Запуск** на вкладке **Главная** .</span><span class="sxs-lookup"><span data-stu-id="77c4d-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="77c4d-304">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-304">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-305">Некоторые версии Google Chrome неправильно регистрируются в компоненте "программы по умолчанию" в Windows.</span><span class="sxs-lookup"><span data-stu-id="77c4d-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="77c4d-306">В качестве обходного решения запустите Google Chrome, щелкните меню *Настройка и управление Google Chrome* , щелкните *Параметры*, а затем выберите команду *сделать Google Chrome браузером по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="77c4d-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="77c4d-307">Проблема. диалоговое окно "внешний ключ" не позволяет ввести первичный ключ</span><span class="sxs-lookup"><span data-stu-id="77c4d-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="77c4d-308">Диалоговое окно **внешний ключ** не позволяет ввести имя первичного ключа из таблицы первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="77c4d-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="77c4d-309">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-309">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-310">Это сделано намеренно.</span><span class="sxs-lookup"><span data-stu-id="77c4d-310">This is intentional.</span></span> <span data-ttu-id="77c4d-311">Не нужно вводить имя первичного ключа из таблицы первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="77c4d-311">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="77c4d-312">Ошибка. Технология IntelliSense недоступна в WebMatrix для синтаксис Razor C#, или Visual Basic</span><span class="sxs-lookup"><span data-stu-id="77c4d-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="77c4d-313">Технология IntelliSense поддерживается в WebMatrix для HTML и CSS.</span><span class="sxs-lookup"><span data-stu-id="77c4d-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="77c4d-314">Однако он недоступен для других языков.</span><span class="sxs-lookup"><span data-stu-id="77c4d-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="77c4d-315">**Обходной путь** </span><span class="sxs-lookup"><span data-stu-id="77c4d-315">**Workaround** </span></span>  
> <span data-ttu-id="77c4d-316">Нет.</span><span class="sxs-lookup"><span data-stu-id="77c4d-316">None.</span></span>

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="77c4d-317">Вопрос. IntelliSense для HTML и CSS предлагает элементы, которые не соответствуют контексту.</span><span class="sxs-lookup"><span data-stu-id="77c4d-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="77c4d-318">Технология IntelliSense для разметки в WebMatrix поддерживает HTML, используя [переходную схему XHTML 1,0](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) и CSS с помощью [схемы CSS 2,1](http://www.w3.org/TR/CSS2/).</span><span class="sxs-lookup"><span data-stu-id="77c4d-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="77c4d-319">Поскольку технология IntelliSense основана на этих конкретных схемах, могут быть предложены некоторые теги, атрибуты или свойства, которые не подходят для текущей страницы или определения стиля.</span><span class="sxs-lookup"><span data-stu-id="77c4d-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="77c4d-320">Для HTML это также может привести к непредвиденным рекомендациям в содержимом, которое может интерпретироваться как неправильно сформированное XHTML (например, если теги не закрыты).</span><span class="sxs-lookup"><span data-stu-id="77c4d-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="77c4d-321">Эта проблема может быть более заметной, если точка вставки находится внутри неполного тега. в этом случае IntelliSense может предложить новые открывающие теги или предложить другие неправильные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="77c4d-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="77c4d-322">**Обходной путь** </span><span class="sxs-lookup"><span data-stu-id="77c4d-322">**Workaround** </span></span>  
> <span data-ttu-id="77c4d-323">Для HTML убедитесь, что вы работаете на правильно сформированной, полной странице XHTML.</span><span class="sxs-lookup"><span data-stu-id="77c4d-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="77c4d-324">Для CSS нет решения.</span><span class="sxs-lookup"><span data-stu-id="77c4d-324">For CSS, there is no workaround.</span></span>

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="77c4d-325">Причина: технология IntelliSense не вызывается при вводе</span><span class="sxs-lookup"><span data-stu-id="77c4d-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="77c4d-326">В некоторых случаях IntelliSense может не вызываться, так как в редакторе не введен HTML или CSS.</span><span class="sxs-lookup"><span data-stu-id="77c4d-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="77c4d-327">В частности, это может произойти, когда точка вставки расположена непосредственно рядом с другим элементом или в конце файла.</span><span class="sxs-lookup"><span data-stu-id="77c4d-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="77c4d-328">**Обходной путь** </span><span class="sxs-lookup"><span data-stu-id="77c4d-328">**Workaround** </span></span>  
> <span data-ttu-id="77c4d-329">Убедитесь, что вокруг точки вставки имеется пробел, а точка вставки не находится в конце файла.</span><span class="sxs-lookup"><span data-stu-id="77c4d-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="77c4d-330">Можно также вызвать IntelliSense вручную, нажав клавиши Ctrl + пробел.</span><span class="sxs-lookup"><span data-stu-id="77c4d-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="77c4d-331">Ошибка: Пользовательский интерфейс для отключения IntelliSense недоступен</span><span class="sxs-lookup"><span data-stu-id="77c4d-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="77c4d-332">WebMatrix 1,0 не предоставляет пользовательского интерфейса или жеста для отключения IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="77c4d-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="77c4d-333">**Обходной путь** </span><span class="sxs-lookup"><span data-stu-id="77c4d-333">**Workaround** </span></span>  
> <span data-ttu-id="77c4d-334">Запустите WebMatrix с помощью следующей команды, которая включает параметр, который отключает IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="77c4d-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="77c4d-335">IIS Express.</span><span class="sxs-lookup"><span data-stu-id="77c4d-335">IIS Express</span></span>

<span data-ttu-id="77c4d-336">IIS Express имеет собственный файл сведений, доступный по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="77c4d-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="77c4d-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x409</span><span class="sxs-lookup"><span data-stu-id="77c4d-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="77c4d-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="77c4d-338">SQL Server Compact</span></span>

<span data-ttu-id="77c4d-339">SQL Server Compact имеет собственный файл сведений, доступный по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="77c4d-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="77c4d-340">Сведения о проблемах, связанных с установкой SQL Server Compact в составе WebMatrix, см. в разделе [проблемы установки WebMatrix](#Known_Issues_Installation) ранее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="77c4d-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a><span data-ttu-id="77c4d-341">Установка приложений</span><span class="sxs-lookup"><span data-stu-id="77c4d-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="77c4d-342">Причина. Установка приложения может занять много времени, если папка пользователя "Мои документы" перенаправлена в общую сетевую папку</span><span class="sxs-lookup"><span data-stu-id="77c4d-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="77c4d-343">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-343">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-344">Нет.</span><span class="sxs-lookup"><span data-stu-id="77c4d-344">None.</span></span> <span data-ttu-id="77c4d-345">Установка приложения может занять некоторое время, но будет установлена правильно.</span><span class="sxs-lookup"><span data-stu-id="77c4d-345">The application might take a while to install, but will install correctly.</span></span>

### <a id="Known_Issues_Publishing_Applications"></a><span data-ttu-id="77c4d-346">Публикация приложений</span><span class="sxs-lookup"><span data-stu-id="77c4d-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="77c4d-347">Ошибка: при публикации базы данных SQL Compact появляется сообщение об ошибке "не удается получить необходимые разрешения"</span><span class="sxs-lookup"><span data-stu-id="77c4d-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="77c4d-348">WebMatrix не полностью поддерживает развертывание вспомогательных двоичных файлов для SQL Server Compact на сервере под управлением .NET Framework версии 3,5 с конфигурацией среднего уровня доверия.</span><span class="sxs-lookup"><span data-stu-id="77c4d-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="77c4d-349">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-349">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-350">Наиболее предпочтительным решением является установка .NET Framework 4 на сервере.</span><span class="sxs-lookup"><span data-stu-id="77c4d-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="77c4d-351">Кроме того, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="77c4d-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="77c4d-352">Добавьте следующие элементы в раздел `SecurityClasses` в файле *Web\_медиумтруст. config* :</span><span class="sxs-lookup"><span data-stu-id="77c4d-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="77c4d-353">Создайте новый набор разрешений в файле *Web\_медиумтруст. config* со следующими необходимыми разрешениями:</span><span class="sxs-lookup"><span data-stu-id="77c4d-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="77c4d-354">Примените набор разрешений к SQL Server Compact, поместив следующие элементы в файл *Web\_медиумтруст. config* :</span><span class="sxs-lookup"><span data-stu-id="77c4d-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="77c4d-355">Причина: в коллекции и веб-приложениях PhpBB отображается ошибка "Служба недоступна" после публикации</span><span class="sxs-lookup"><span data-stu-id="77c4d-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="77c4d-356">В некоторых случаях публикация приложения приводит к ошибке "Служба недоступна".</span><span class="sxs-lookup"><span data-stu-id="77c4d-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="77c4d-357">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-357">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-358">В WebMatrix добавьте обратную косую черту (\) в конец имени сервера в окне **Параметры публикации** , а затем опубликуйте приложение еще раз.</span><span class="sxs-lookup"><span data-stu-id="77c4d-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="77c4d-359">Причина: макет веб-сайта Moodle и ссылки не нарушаются после публикации</span><span class="sxs-lookup"><span data-stu-id="77c4d-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="77c4d-360">После публикации приложения Moodle приложение работает неправильно.</span><span class="sxs-lookup"><span data-stu-id="77c4d-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="77c4d-361">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-361">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-362">В WebMatrix добавьте косую черту (/) в конец поля **имя сайта** в окне **Параметры публикации** , а затем опубликуйте приложение еще раз.</span><span class="sxs-lookup"><span data-stu-id="77c4d-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="77c4d-363">Ошибка: сбой публикации nopCommerce с ошибкой базы данных</span><span class="sxs-lookup"><span data-stu-id="77c4d-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="77c4d-364">Публикация nopCommerce завершается сбоем и сообщает об ошибке базы данных, например "Ошибка вставки в таблицу журнала\_NOP".</span><span class="sxs-lookup"><span data-stu-id="77c4d-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="77c4d-365">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="77c4d-366">В WebMatrix щелкните **запустить** , чтобы запустить nopCommerce локально.</span><span class="sxs-lookup"><span data-stu-id="77c4d-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="77c4d-367">Войдите на страницу администрирования.</span><span class="sxs-lookup"><span data-stu-id="77c4d-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="77c4d-368">Щелкните **системное** меню.</span><span class="sxs-lookup"><span data-stu-id="77c4d-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="77c4d-369">Выберите параметр **Журнал** .</span><span class="sxs-lookup"><span data-stu-id="77c4d-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="77c4d-370">Нажмите кнопку **Очистить журнал**.</span><span class="sxs-lookup"><span data-stu-id="77c4d-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="77c4d-371">Опубликуйте nopCommerce еще раз.</span><span class="sxs-lookup"><span data-stu-id="77c4d-371">Publish nopCommerce again.</span></span>

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="77c4d-372">Ошибка. при скачивании опубликованного сайта в Силверстрипе CMS отображается сообщение об ошибке HTTP 500 PHP FCGI.</span><span class="sxs-lookup"><span data-stu-id="77c4d-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="77c4d-373">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-373">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-374">После нажатия кнопки **скачать опубликованный сайт**пропустите `silverstripe-cache/manifest_main` в **предварительной версии публикации**.</span><span class="sxs-lookup"><span data-stu-id="77c4d-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="77c4d-375">Этот файл используется в целях кэширования и зависит от конкретного компьютера.</span><span class="sxs-lookup"><span data-stu-id="77c4d-375">This file is used for caching purposes and is specific to each computer.</span></span>

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="77c4d-376">Ошибка: при скачивании опубликованного сайта в подтексте отображается сообщение об ошибке сервера в "/" приложении ".</span><span class="sxs-lookup"><span data-stu-id="77c4d-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="77c4d-377">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-377">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-378">Откройте файл *Web. config* сайта и замените идентификатор пользователя и пароль в строке подключения к базе данных учетными данными администратора SQL Server (учетные данные SA).</span><span class="sxs-lookup"><span data-stu-id="77c4d-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="77c4d-379">Кроме того, чтобы предоставить учетной записи пользователя, к которой вы выполнили вход, разрешения `db_owner`, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="77c4d-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="77c4d-380">Установите SQL Server Management Studio с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="77c4d-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="77c4d-381">Подключитесь к локальному экземпляру SQL Server Express (по умолчанию `.\SQLEXPRESS`).</span><span class="sxs-lookup"><span data-stu-id="77c4d-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="77c4d-382">Щелкните **базы данных** &gt; *[Локалсубтекстдатабасе]* &gt; **Безопасность** &gt; **Пользователи** &gt; *[локалсубтекстусер*] (по умолчанию — `subtextuser`], щелкните правой кнопкой мыши и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="77c4d-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="77c4d-383">Выберите **база данных\_владелец** в разделе членство в роли.</span><span class="sxs-lookup"><span data-stu-id="77c4d-383">Select **db\_owner** in the role membership section.</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="77c4d-384">Проблема. После публикации сайт может не работать, если поле "URL-адрес назначения" не имеет префикса http://или https://</span><span class="sxs-lookup"><span data-stu-id="77c4d-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="77c4d-385">Если в диалоговом окне **Параметры публикации** URL-адрес назначения не начинается с `http://` или `https://`, сайт может не работать после развертывания.</span><span class="sxs-lookup"><span data-stu-id="77c4d-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="77c4d-386">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-386">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-387">Убедитесь, что перед публикацией сайта URL-адрес назначения в диалоговом окне " **Параметры публикации** " начинается с `http://` или `https://`.</span><span class="sxs-lookup"><span data-stu-id="77c4d-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="77c4d-388">Ошибка. Публикация базы данных MySQL завершается сбоем с ошибкой "не удалось опубликовать базу данных.</span><span class="sxs-lookup"><span data-stu-id="77c4d-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="77c4d-389">Это может произойти, если удаленная база данных не может выполнить скрипт ".</span><span class="sxs-lookup"><span data-stu-id="77c4d-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="77c4d-390">Эта ошибка может возникать по ряду причин.</span><span class="sxs-lookup"><span data-stu-id="77c4d-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="77c4d-391">Одной из причин возникновения этой ошибки является то, что скрипт базы данных содержит символ одинарной кавычки ('), а кодировка по умолчанию целевой базы данных MySQL — не UTF-8.</span><span class="sxs-lookup"><span data-stu-id="77c4d-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="77c4d-392">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-392">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-393">Задайте в качестве кодировки по умолчанию для удаленной базы данных MySQL кодировку UTF-8.</span><span class="sxs-lookup"><span data-stu-id="77c4d-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="77c4d-394">Причина. Некоторые ссылки не отображаются в DotNetNuke после публикации или скачивания сайта</span><span class="sxs-lookup"><span data-stu-id="77c4d-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="77c4d-395">Если вы публикуете или скачиваете сайт DotNetNuke, может потребоваться очистить кэш, чтобы отобразить новые ссылки на сайте.</span><span class="sxs-lookup"><span data-stu-id="77c4d-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="77c4d-396">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="77c4d-397">Войдите в систему как "узел".</span><span class="sxs-lookup"><span data-stu-id="77c4d-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="77c4d-398">Перейдите в меню узел и выберите **Параметры узла**.</span><span class="sxs-lookup"><span data-stu-id="77c4d-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="77c4d-399">Прокрутите вниз и в разделе **Дополнительные параметры**разверните узел **Параметры производительности**.</span><span class="sxs-lookup"><span data-stu-id="77c4d-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="77c4d-400">Щелкните ссылку **очистить кэш** для страниц.</span><span class="sxs-lookup"><span data-stu-id="77c4d-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="77c4d-401">Перейдите в нижнюю часть страницы и перезапустите приложение.</span><span class="sxs-lookup"><span data-stu-id="77c4d-401">Go to the bottom of the page and restart the application.</span></span>

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="77c4d-402">Причина. при скачивании опубликованного сайта некоторые ссылки в Атомсите нарушаются</span><span class="sxs-lookup"><span data-stu-id="77c4d-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="77c4d-403">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-403">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-404">В файле *Service. config* , файле *Users. config* и всех *XML-* файлах замените строку URL-адреса (например, `http://myhost.com/atomsite`) на локальную (например, `http://localhost:1239`).</span><span class="sxs-lookup"><span data-stu-id="77c4d-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="77c4d-405">Ошибка: приложениям на основе MySQL, например WordPress, не удалось опубликовать и сообщить об ошибке базы данных</span><span class="sxs-lookup"><span data-stu-id="77c4d-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="77c4d-406">По умолчанию WebMatrix устанавливает MySQL с кодировкой UTF-8.</span><span class="sxs-lookup"><span data-stu-id="77c4d-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="77c4d-407">Если вы устанавливаете MySQL самостоятельно, а кодировка не UTF-8 (например, это Latin1), процесс публикации баз данных может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="77c4d-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="77c4d-408">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="77c4d-409">Измените кодировку MySQL на UTF-8.</span><span class="sxs-lookup"><span data-stu-id="77c4d-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="77c4d-410">(Дополнительные сведения см. в разделе [Серверный набор символов и параметры сортировки](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) на веб-сайте MySQL.)</span><span class="sxs-lookup"><span data-stu-id="77c4d-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="77c4d-411">Переустановите приложение.</span><span class="sxs-lookup"><span data-stu-id="77c4d-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="77c4d-412">Повторно опубликуйте приложение.</span><span class="sxs-lookup"><span data-stu-id="77c4d-412">Republish the application.</span></span>

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="77c4d-413">Ошибка: "скачивание опубликованного сайта" завершается неудачей для приложений, имеющих браузерную установку</span><span class="sxs-lookup"><span data-stu-id="77c4d-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="77c4d-414">Для некоторых приложений (например, Kentico CMS) требуется запустить их в браузере, чтобы выполнить установку после установки, например создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="77c4d-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="77c4d-415">Если вы публикуете приложение подобным образом, не выполняя настройку на основе браузера, попытка скачать тот же сайт с удаленного сервера завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="77c4d-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="77c4d-416">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-416">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-417">Завершите настройку на основе браузера перед публикацией сайта.</span><span class="sxs-lookup"><span data-stu-id="77c4d-417">Finish browser-based setup before publishing the site.</span></span>

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="77c4d-418">Ошибка: "скачивание опубликованного сайта" завершается сбоем с ошибкой базы данных для DotNetNuke и Kooboo CMS.</span><span class="sxs-lookup"><span data-stu-id="77c4d-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="77c4d-419">При попытке загрузить приложение с сервера и наличии учетных данных администратора в строке подключения к базе данных в диалоговом окне " **Параметры публикации** " в журнале публикации может появиться следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="77c4d-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="77c4d-420">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="77c4d-420">**Workaround**</span></span>  
> <span data-ttu-id="77c4d-421">Если это целесообразно, повторно опубликуйте сайт (или разработайте его), используя учетные данные без прав администратора для базы данных.</span><span class="sxs-lookup"><span data-stu-id="77c4d-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="77c4d-422">Дополнительные сведения см. в разделе</span><span class="sxs-lookup"><span data-stu-id="77c4d-422">For More Information</span></span>

<span data-ttu-id="77c4d-423">Дополнительные сведения о WebMatrix 1,0 см. на следующих веб-сайтах:</span><span class="sxs-lookup"><span data-stu-id="77c4d-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="77c4d-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="77c4d-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="77c4d-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="77c4d-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="77c4d-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="77c4d-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="77c4d-427">© Корпорация Майкрософт (Microsoft Corporation), 2011.</span><span class="sxs-lookup"><span data-stu-id="77c4d-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="77c4d-428">Все права защищены.</span><span class="sxs-lookup"><span data-stu-id="77c4d-428">All Rights Reserved.</span></span> <span data-ttu-id="77c4d-429">[Условия использования](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="77c4d-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
