---
uid: web-pages/readme/beta3
title: Файл сведений о выпуске Web Matrix и веб-страницы ASP.NET (Razor) Beta 3 | Документация Майкрософт
author: rick-anderson
description: Файл сведений для Web Matrix и выпуска бета-версии 3 веб-страниц ASP.NET (Razor)
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510342"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="c35a1-103">Файл сведений для Web Matrix и выпуска бета-версии 3 веб-страниц ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="c35a1-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

> <span data-ttu-id="c35a1-104">Файл сведений для Web Matrix и выпуска бета-версии 3 веб-страниц ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="c35a1-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="c35a1-105">9 ноября 2010</span><span class="sxs-lookup"><span data-stu-id="c35a1-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="c35a1-106">Содержимое</span><span class="sxs-lookup"><span data-stu-id="c35a1-106">Contents</span></span>

- [<span data-ttu-id="c35a1-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="c35a1-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="c35a1-108">Установка</span><span class="sxs-lookup"><span data-stu-id="c35a1-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="c35a1-109">Новые функции, изменения и известные проблемы в выпуске бета-версии 3</span><span class="sxs-lookup"><span data-stu-id="c35a1-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="c35a1-110">Проблемы с установкой WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c35a1-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="c35a1-111">Веб-страницы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c35a1-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="c35a1-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="c35a1-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="c35a1-113">Установка приложений</span><span class="sxs-lookup"><span data-stu-id="c35a1-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="c35a1-114">Публикация приложений</span><span class="sxs-lookup"><span data-stu-id="c35a1-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="c35a1-115">Другие проблемы</span><span class="sxs-lookup"><span data-stu-id="c35a1-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="c35a1-116">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="c35a1-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="c35a1-117">Обзор</span><span class="sxs-lookup"><span data-stu-id="c35a1-117">Overview</span></span>

> <span data-ttu-id="c35a1-118">Microsoft WebMatrix Beta — это бесплатный стек веб-разработки, устанавливаемый за считанные минуты.</span><span class="sxs-lookup"><span data-stu-id="c35a1-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="c35a1-119">Он интегрирует веб-сервер с платформами баз данных и программирования для создания единого интегрированного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c35a1-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="c35a1-120">Вы можете использовать бета-версию WebMatrix для оптимизации кода, тестирования и публикации собственного веб-сайта ASP.NET или PHP или использовать бета-версию WebMatrix для запуска нового веб-сайта с помощью популярных приложений с открытым исходным кодом, таких как DotNetNuke, Umbraco, WordPress или Joomla.</span><span class="sxs-lookup"><span data-stu-id="c35a1-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="c35a1-121">В бета-версии WebMatrix используется тот же мощный веб-сервер, ядро СУБД и среда, который будет запускать ваш веб-сайт в Интернете, что делает переход от разработки к рабочей среде без проблем.</span><span class="sxs-lookup"><span data-stu-id="c35a1-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="c35a1-122">Установка</span><span class="sxs-lookup"><span data-stu-id="c35a1-122">Installation</span></span>

> <span data-ttu-id="c35a1-123">Чтобы установить бета-версию 3 WebMatrix, используйте [установщик веб-платформы Майкрософт 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="c35a1-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="c35a1-124">После установки установщика веб-платформы его можно использовать для установки бета-версии 3 WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="c35a1-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="c35a1-125">При возникновении проблем во время установки обратитесь к разделу [Устранение неполадок с установщик веб-платформы Майкрософт](https://go.microsoft.com/fwlink/?LinkId=196212).</span><span class="sxs-lookup"><span data-stu-id="c35a1-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="c35a1-126">Инструкции по публикации приложений</span><span class="sxs-lookup"><span data-stu-id="c35a1-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="c35a1-127">См. [Пошаговые инструкции по публикации приложений](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="c35a1-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="c35a1-128">Новые функции, изменения, Андкновн проблемы</span><span class="sxs-lookup"><span data-stu-id="c35a1-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="c35a1-129">Установка бета-версии 3 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c35a1-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="c35a1-130">Вопрос. бета-версия 3 WebMatrix доступна только на платформах, поддерживающих Microsoft .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="c35a1-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="c35a1-131">Для бета-версии WebMatrix требуется .NET Framework версии 4.</span><span class="sxs-lookup"><span data-stu-id="c35a1-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="c35a1-132">В некоторых случаях установщик бета-версии WebMatrix позволит установить на платформу, которая не входит в набор поддерживаемых конфигураций.</span><span class="sxs-lookup"><span data-stu-id="c35a1-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="c35a1-133">В частности, Windows Vista без обновления SP1 позволит начать установку бета-версии WebMatrix, но компонент .NET Framework 4 завершится сбоем и заблокирует установку.</span><span class="sxs-lookup"><span data-stu-id="c35a1-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="c35a1-134">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-134">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-135">Установите на поддерживаемой платформе, которая включает в себя:</span><span class="sxs-lookup"><span data-stu-id="c35a1-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="c35a1-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c35a1-136">Windows 7</span></span>
> - <span data-ttu-id="c35a1-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="c35a1-137">Windows Server 2008</span></span>
> - <span data-ttu-id="c35a1-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c35a1-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="c35a1-139">Windows Vista с пакетом обновления 1 (SP1) или выше</span><span class="sxs-lookup"><span data-stu-id="c35a1-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="c35a1-140">Windows XP с пакетом обновления 3 (SP3)</span><span class="sxs-lookup"><span data-stu-id="c35a1-140">Windows XP SP3</span></span>
> - <span data-ttu-id="c35a1-141">Windows Server 2003 с пакетом обновления 2 (SP2)</span><span class="sxs-lookup"><span data-stu-id="c35a1-141">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="c35a1-142">Вопрос. не удается установить бета-версию 3 WebMatrix, если Microsoft Visual Studio 2008 установлен без Microsoft Visual Studio 2008 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="c35a1-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="c35a1-143">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-143">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-144">Установите [Microsoft Visual Studio 2008 с пакетом обновления 1 (SP1)](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) из центра загрузки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c35a1-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="c35a1-145">Причина. Некоторые сборки для SQL Server Compact 4,0 не установлены в GAC</span><span class="sxs-lookup"><span data-stu-id="c35a1-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="c35a1-146">Управляемые сборки для SQL Server Compact 4,0 не помещаются в глобальный кэш сборок (GAC) при установке SQL Server Compact 4,0 на 64-разрядном компьютере, а на компьютере установлен только клиентский профиль .NET Framework 3,5 SP1.</span><span class="sxs-lookup"><span data-stu-id="c35a1-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="c35a1-147">В глобальный кэш сборок не установлены следующие управляемые сборки:</span><span class="sxs-lookup"><span data-stu-id="c35a1-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="c35a1-148">*System. Data. SqlServerCe. dll* (поставщик ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="c35a1-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="c35a1-149">*System. Data. SqlServerCe. Entity. dll* (ADO.NET Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="c35a1-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="c35a1-150">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-150">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-151">Удалите SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="c35a1-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="c35a1-152">Скачайте и установите полную версию .NET Framework 3,5 с пакетом обновления 1 (SP1) из следующего расположения:</span><span class="sxs-lookup"><span data-stu-id="c35a1-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="c35a1-153">Microsoft .NET Framework 3,5 с пакетом обновления 1 (SP1) (полный пакет)</span><span class="sxs-lookup"><span data-stu-id="c35a1-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="c35a1-154">Затем переустановите SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="c35a1-154">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="c35a1-155">Ошибка: не удается удалить SQL Server Compact с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="c35a1-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="c35a1-156">Удаление SQL Server Compact с помощью параметров командной строки не работает в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="c35a1-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="c35a1-157">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-157">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-158">Используйте *программы и компоненты* на панели управления Windows для удаления Microsoft SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="c35a1-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="c35a1-159">Веб-страницы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c35a1-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="c35a1-160">В этом разделе документа описаны новые функции, изменения и известные проблемы, связанные с выпуском бета-версии 3 веб-страницы ASP.NET с синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="c35a1-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="c35a1-161">Новые функции</span><span class="sxs-lookup"><span data-stu-id="c35a1-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="c35a1-162">Изменения</span><span class="sxs-lookup"><span data-stu-id="c35a1-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="c35a1-163">Проблемы</span><span class="sxs-lookup"><span data-stu-id="c35a1-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="c35a1-164">Новые возможности бета-версии 3 для веб-страницы ASP.NET с синтаксисом Razor</span><span class="sxs-lookup"><span data-stu-id="c35a1-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="c35a1-165">Новый: метод "HTML. RAW" визуализирует незакодированную разметку</span><span class="sxs-lookup"><span data-stu-id="c35a1-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="c35a1-166">Новый метод `Html.Raw` позволяет визуализировать разметку HTML в виде разметки вместо отрисовки закодированных выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c35a1-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="c35a1-167">(По умолчанию ASP.NET Razor кодирует строки перед их отрисовкой.) Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="c35a1-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="c35a1-168">В следующем примере показано использование `Html.Raw`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="c35a1-169">Изменения в бета-версии 3 для веб-страницы ASP.NET с синтаксисом Razor</span><span class="sxs-lookup"><span data-stu-id="c35a1-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="c35a1-170">Изменение: метод "Хрефаттрибуте" удален</span><span class="sxs-lookup"><span data-stu-id="c35a1-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="c35a1-171">Метод `HrefAttribute` класса `WebPage` был удален.</span><span class="sxs-lookup"><span data-stu-id="c35a1-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="c35a1-172">Этот вспомогательный метод использовался для кодирования ненадежных символов в URL-адресах.</span><span class="sxs-lookup"><span data-stu-id="c35a1-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="c35a1-173">Он больше не требуется, так как ASP.NET Razor автоматически кодирует строки.</span><span class="sxs-lookup"><span data-stu-id="c35a1-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="c35a1-174">(Используйте новый метод `Html.Raw` для отображения незакодированных строк.)</span><span class="sxs-lookup"><span data-stu-id="c35a1-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="c35a1-175">Изменение: синтаксис декларативных вспомогательных функций "@helper" изменился</span><span class="sxs-lookup"><span data-stu-id="c35a1-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="c35a1-176">В выпуске бета-версии 3 ASP.NET изменяет, как он выполняет синтаксический анализ вспомогательных функций, созданных с помощью синтаксиса `@helper`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="c35a1-177">По сути, синтаксис `@helper` теперь анализируется как блок кода, а не как блок разметки, которая может содержать код.</span><span class="sxs-lookup"><span data-stu-id="c35a1-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="c35a1-178">Поэтому код внутри вспомогательной функции не обязательно должен быть заключен в блоки `@{ }`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="c35a1-179">И наоборот, разметка внутри вспомогательной функции должна быть явно включена в элементы HTML или в теги ASP.NET Razor `<text></text>`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="c35a1-180">Например, следующий синтаксис `@helper` работает в бета-версии 3:</span><span class="sxs-lookup"><span data-stu-id="c35a1-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="c35a1-181">В выпуске Beta 3 этот вспомогательный модуль необходимо изменить, чтобы он был похож на следующий пример:</span><span class="sxs-lookup"><span data-stu-id="c35a1-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="c35a1-182">Обратите внимание, что `@{ }` символы вокруг исходного кода в вспомогательной функции больше не используются.</span><span class="sxs-lookup"><span data-stu-id="c35a1-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="c35a1-183">Это связано с тем, что содержимое вспомогательных функций по умолчанию обрабатывается как блок кода.</span><span class="sxs-lookup"><span data-stu-id="c35a1-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="c35a1-184">Вспомогательный объект визуализирует разметку, которая начинается с открывающего тега `<a>`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="c35a1-185">Если вспомогательный объект должен визуализировать обычный текст или теги, не содержащие закрывающего тега (например, `<meta>` Tags), содержимое для подготовки к просмотру должно быть в тегах `<text></text>`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>

#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="c35a1-186">Изменение: "Вебпажеконтекст. HttpContext" удалено</span><span class="sxs-lookup"><span data-stu-id="c35a1-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="c35a1-187">Свойство `WebPageContext.HttpContext` было удалено.</span><span class="sxs-lookup"><span data-stu-id="c35a1-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="c35a1-188">Используйте вместо этого `HttpContext.Current`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="c35a1-189">(Свойство `WebPageContext.HttpContext` просто обернуто в оболочку.)</span><span class="sxs-lookup"><span data-stu-id="c35a1-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>

#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="c35a1-190">Изменение: вспомогательный модуль Facebook перемещен в новый пакет</span><span class="sxs-lookup"><span data-stu-id="c35a1-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="c35a1-191">Вспомогательный модуль `Facebook` был перемещен в библиотеку *Facebook. Helper* , включающую вспомогательную функцию `Facebook` и дополнительные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="c35a1-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="c35a1-192">Эту библиотеку необходимо установить как отдельный пакет, как описано в разделе "Установка вспомогательных функций с помощью диспетчера пакетов" руководства [Начало работы со страницами ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202889).</span><span class="sxs-lookup"><span data-stu-id="c35a1-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="c35a1-193">Изменение: членство, роль и типы безопасности перемещаются в новую сборку</span><span class="sxs-lookup"><span data-stu-id="c35a1-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="c35a1-194">Следующие типы были перемещены в сборку `WebMatrix.WebData`:</span><span class="sxs-lookup"><span data-stu-id="c35a1-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="c35a1-195">Изменение: класс "TagBuilder" перемещен в сборку System. Web. веб-страниц. dll</span><span class="sxs-lookup"><span data-stu-id="c35a1-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="c35a1-196">Класс `TagBuilde` r был перемещен в сборку System. Web. веб-страниц. dll.</span><span class="sxs-lookup"><span data-stu-id="c35a1-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="c35a1-197">Ранее это было в сборке, которая была частью ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c35a1-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="c35a1-198">Это изменение означает, что нет необходимости устанавливать ASP.NET MVC для использования класса `TagBuilder`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="c35a1-199">Однако класс по-прежнему находится в пространстве имен `System.Web.Mvc`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="c35a1-200">Чтобы использовать класс `TagBuilder` (например, в пользовательском вспомогательном модуле Razor ASP.NET), необходимо сослаться на пространство имен (например, добавив `@using System.Web.Mvc` в код).</span><span class="sxs-lookup"><span data-stu-id="c35a1-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="c35a1-201">Изменение: изменился синтаксис проверки запроса; Класс "Проверка" удален</span><span class="sxs-lookup"><span data-stu-id="c35a1-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="c35a1-202">В выпуске бета-версии 3, чтобы отключить проверку для отдельного поля или набора полей, можно вызвать метод `Validation.Exclude`, передав имя или имена полей, исключаемых из проверки.</span><span class="sxs-lookup"><span data-stu-id="c35a1-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="c35a1-203">В выпуске Beta 3 доступен новый синтаксис для обхода проверки.</span><span class="sxs-lookup"><span data-stu-id="c35a1-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="c35a1-204">Метод `Validation`, используемый в бета-версии 3, был удален.</span><span class="sxs-lookup"><span data-stu-id="c35a1-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="c35a1-205">Если вы не отключаете проверку запроса, если пользователи пытаются отправить разметку HTML (например, с помощью редактора форматированного текста на странице), веб-сайт сообщит об ошибке, похожем *на потенциально опасный запрос. значение формы было обнаружено клиентом* , и введенные пользователем данные не принимаются.</span><span class="sxs-lookup"><span data-stu-id="c35a1-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="c35a1-206">Если вы отключаете проверку запроса, необходимо вручную проверить введенные пользователем данные, чтобы убедиться, что она не содержит потенциально опасной разметки или скрипта, используя нечто вроде [библиотеки сценариев защиты от межсайтовых веб-узлов Майкрософт версии 4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span><span class="sxs-lookup"><span data-stu-id="c35a1-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="c35a1-207">Чтобы отключить автоматическую проверку запросов, вызовите метод `Request.Unvalidated`, передав ему имя поля или другого объекта POST, для которого требуется обойти проверку запроса.</span><span class="sxs-lookup"><span data-stu-id="c35a1-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="c35a1-208">Этот метод можно использовать для обхода проверки любых элементов в коллекциях `Form`, `QueryString`, `Cookies`и `ServerVariables`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="c35a1-209">В следующих примерах показано, как использовать метод `Unvalidated`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="c35a1-210">Известные проблемы для веб-страницы ASP.NET с синтаксисом Razor</span><span class="sxs-lookup"><span data-stu-id="c35a1-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="c35a1-211">Причина: непредвиденное поведение при использовании пользовательской таблицы пользователя для членства</span><span class="sxs-lookup"><span data-stu-id="c35a1-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="c35a1-212">Чтобы инициализировать поставщик членства для веб-сайта ASP.NET Razor, вызовите метод `WebSecurity.InitializeDatabaseConnection`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="c35a1-213">(В WebMatrix шаблон начального сайта включает вызов этого метода в файле *\_AppStart. cshtml* .) Если для параметра `autoCreateTables` этого метода задано значение true (по умолчанию задано значение true в шаблоне начального сайта) и если в метод передается нераспознанное имя таблицы (второй параметр), метод не вызывает ошибку.</span><span class="sxs-lookup"><span data-stu-id="c35a1-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="c35a1-214">Вместо этого он автоматически создает таблицу.</span><span class="sxs-lookup"><span data-stu-id="c35a1-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="c35a1-215">Это может быть проблемой, если вы планируете использовать настраиваемую таблицу пользователей для членства, но передать неправильное имя таблицы в метод `WebSecurity.InitializeDatabaseConnection`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="c35a1-216">Так как метод не по умолчанию вызывает ошибку, если указанная таблица не существует, и, поскольку вместо этого создается новая таблица, приложение может работать нормально.</span><span class="sxs-lookup"><span data-stu-id="c35a1-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="c35a1-217">Однако код приложения, основанный на настраиваемой пользовательской таблице (и в полях), может в конечном итоге завершиться с непредвиденными ошибками.</span><span class="sxs-lookup"><span data-stu-id="c35a1-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="c35a1-218">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-218">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-219">Убедитесь, что имя, переданное в методе `InitializeDatabaseConnection`, совпадает с таблицей профиля пользователя в базе данных членства или убедитесь, что для параметра `autoCreateTables` задано значение false.</span><span class="sxs-lookup"><span data-stu-id="c35a1-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="c35a1-220">Ошибка: "не удалось создать пользовательский экземпляр SQL Server"</span><span class="sxs-lookup"><span data-stu-id="c35a1-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="c35a1-221">Если веб-приложение WebMatrix использует SQL Server Express и работает с IIS 7,5 в Windows 7 или Windows Server 2008 R2, может появиться сообщение об ошибке, свидетельствующее о том, что SQL Server не может получить путь к локальному приложению пользователя во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c35a1-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="c35a1-222">**Обходной путь** Убедитесь, что учетная запись Windows, под которой выполняется приложение (обычно СЕТЕВая служба), имеет разрешения на чтение и запись для корневых папок приложения и для вложенных папок, таких как *данные\_приложений*.</span><span class="sxs-lookup"><span data-stu-id="c35a1-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="c35a1-223">Более подробные сведения см. в статье базы знаний [проблемы с SQL Server Express проектами создания пользовательских экземпляров и ASP.NET проектов веб-приложений](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="c35a1-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="c35a1-224">Вопрос. в Visual Studio пространства имен для пользовательских сборок (DLL) не импортируются автоматически</span><span class="sxs-lookup"><span data-stu-id="c35a1-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="c35a1-225">При использовании пользовательских сборок в проекте в Visual Studio пространства имен, объявленные в этих сборках, не импортируются автоматически во время разработки.</span><span class="sxs-lookup"><span data-stu-id="c35a1-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="c35a1-226">В результате ссылки на пользовательские типы могут быть не распознаны во время разработки и помечены как нераспознаваемые в Visual Studio (с помощью «волнистой линии»).</span><span class="sxs-lookup"><span data-stu-id="c35a1-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="c35a1-227">Эта проблема возникает только во время разработки в Visual Studio; само приложение работает правильно.</span><span class="sxs-lookup"><span data-stu-id="c35a1-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="c35a1-228">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-228">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-229">Включите `using`ную инструкцию (`imports` в Visual Basic), которая ссылается на сущности, которые не распознаются во время разработки.</span><span class="sxs-lookup"><span data-stu-id="c35a1-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="c35a1-230">Вопрос. шаблоны IntelliSense и проектов Visual Studio доступны только в ASP.NET MVC версии 3</span><span class="sxs-lookup"><span data-stu-id="c35a1-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="c35a1-231">При установке веб-страницы ASP.NET также не устанавливаются средства для Visual Studio, такие как IntelliSense и шаблоны проектов для веб-страницы ASP.NET приложений.</span><span class="sxs-lookup"><span data-stu-id="c35a1-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="c35a1-232">**Обходной путь** Чтобы использовать IntelliSense и шаблоны проектов для веб-страницы ASP.NET приложений в Visual Studio, установите ASP.NET MVC 3 RC либо через установщик веб-платформы, либо в [автономный установщик](https://go.microsoft.com/fwlink/?LinkID=191797).</span><span class="sxs-lookup"><span data-stu-id="c35a1-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="c35a1-233">Ошибка: не удается найти&lt;вспомогательный класс&gt;</span><span class="sxs-lookup"><span data-stu-id="c35a1-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="c35a1-234">После обновления до бета-версии 3 может появиться сообщение об ошибке: не удается найти вспомогательный класс (например, `Facebook` класс).</span><span class="sxs-lookup"><span data-stu-id="c35a1-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="c35a1-235">Начиная с бета-версии 2 и продолжая в бета-версии 3, вспомогательные методы были перемещены в пакеты, которые необходимо явно установить.</span><span class="sxs-lookup"><span data-stu-id="c35a1-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="c35a1-236">Существующие сайты не будут обновлены для включения этих пакетов. Сюда входят сайты в папках \ \ *документс\иисекспресс* или *\ мои документы \ мои веб-узлы* .</span><span class="sxs-lookup"><span data-stu-id="c35a1-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="c35a1-237">В частности, эта ошибка возникает при использовании сайта по умолчанию на странице " *Мои сайты* " (Website1), который включает ссылку на вспомогательный метод `Twitter`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="c35a1-238">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-238">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-239">Закомментируйте вызовы для любых вспомогательных функций на сайте, запустите страницу *администрирования\_* и установите пакет или пакеты, включающие вспомогательные методы, которые вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="c35a1-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="c35a1-240">После установки пакета можно раскомментировать строки, которые ссылаются на вспомогательные методы.</span><span class="sxs-lookup"><span data-stu-id="c35a1-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="c35a1-241">Вопрос. Развертывание бета-версии 3 ASP.NET сборок Razor в папку bin может не работать на сайтах размещения</span><span class="sxs-lookup"><span data-stu-id="c35a1-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="c35a1-242">При развертывании веб-страницы ASP.NET веб-сайта на сайте размещения и при развертывании сборок ASP.NET Razor Beta 3 в папке *bin* сайта могут возникнуть ошибки, включая следующие.</span><span class="sxs-lookup"><span data-stu-id="c35a1-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="c35a1-243">Это может произойти, если поставщик услуг размещения установил веб-страницы ASP.NET сборки бета-версии 1 в глобальный кэш приложения (GAC) сервера.</span><span class="sxs-lookup"><span data-stu-id="c35a1-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="c35a1-244">Сборки в глобальном кэше сборок получают приоритет над сборками, установленными локально в папке *bin* .</span><span class="sxs-lookup"><span data-stu-id="c35a1-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="c35a1-245">**Обходной путь** Обратитесь к поставщику услуг размещения, чтобы убедиться, что наблюдаемые ошибки вызваны конфликтом между версиями сборок и Вашими поставщиками.</span><span class="sxs-lookup"><span data-stu-id="c35a1-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="c35a1-246">Если это так, запросите поставщика услуг размещения обновить сборки в глобальном кэше сборок сервера.</span><span class="sxs-lookup"><span data-stu-id="c35a1-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="c35a1-247">Ошибка: чтение веб-каналов или других внешних данных через прокси Server</span><span class="sxs-lookup"><span data-stu-id="c35a1-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="c35a1-248">Если сервер, на котором работает сайт, находится за прокси-сервером, может потребоваться настроить сведения о прокси-сервере в файле *Web. config* , чтобы иметь возможность считывать сведения, поступающие за пределы сайта.</span><span class="sxs-lookup"><span data-stu-id="c35a1-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="c35a1-249">Например, при использовании вспомогательного метода `ReCaptcha` вспомогательный объект взаимодействует со службой reCAPTCHA, но может быть заблокирован прокси-сервером.</span><span class="sxs-lookup"><span data-stu-id="c35a1-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="c35a1-250">Аналогичным образом, для веб-каналов, используемых в веб-страницы ASP.NET, например в канале, используемом диспетчером пакетов, может потребоваться настройка прокси.</span><span class="sxs-lookup"><span data-stu-id="c35a1-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="c35a1-251">Если возникают проблемы при работе с внешней службой или веб-каналом пакета, добавьте следующие элементы в корневой файл *Web. config* приложения:</span><span class="sxs-lookup"><span data-stu-id="c35a1-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="c35a1-252">Дополнительные сведения о настройке прокси-сервера см. в разделе [&lt;прокси-&gt; элемент (параметры сети)](https://msdn.microsoft.com/library/sa91de1e.aspx) на веб-сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="c35a1-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="c35a1-253">Вопрос: ошибка "Microsoft. Web. Infrastructure. dll не может быть загружена"</span><span class="sxs-lookup"><span data-stu-id="c35a1-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="c35a1-254">Если ранее вы установили бета-версию 1 веб-страницы ASP.NET с синтаксис Razor а затем установите бета-версию 3, все соответствующие сборки устанавливаются в глобальном кэше сборок, кроме *Microsoft. Web. Infrastructure. dll*.</span><span class="sxs-lookup"><span data-stu-id="c35a1-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="c35a1-255">Как следствие, при запуске ASP.NET страниц Razor отображается ошибка, указывающая, что не удалось загрузить *Microsoft. Web. Infrastructure. dll* .</span><span class="sxs-lookup"><span data-stu-id="c35a1-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="c35a1-256">Эта проблема не возникает, если вы загрузили выпуск Beta 3 на чистый компьютер.</span><span class="sxs-lookup"><span data-stu-id="c35a1-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="c35a1-257">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-257">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-258">На панели управления удалите веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c35a1-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="c35a1-259">Затем переустановите бета-версию 3.</span><span class="sxs-lookup"><span data-stu-id="c35a1-259">Then reinstall the Beta 3 release.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="c35a1-260">Ошибка: при удалении .NET Framework версии 4 отключается веб-страницы ASP.NET с синтаксисом Razor.</span><span class="sxs-lookup"><span data-stu-id="c35a1-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="c35a1-261">Если удалить .NET Framework версии 4, а затем переустановить ее, веб-страницы ASP.NET с синтаксис Razor будет отключена.</span><span class="sxs-lookup"><span data-stu-id="c35a1-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="c35a1-262">Страницы с расширением *CSHTML* выполняются неправильно.</span><span class="sxs-lookup"><span data-stu-id="c35a1-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="c35a1-263">Веб-страницы ASP.NET регистрирует сборку в корневом файле *Web. config* компьютера, а удаление .NET Framework удаляет этот файл.</span><span class="sxs-lookup"><span data-stu-id="c35a1-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="c35a1-264">При переустановке .NET Framework устанавливается новая версия файла конфигурации, но не добавляется ссылка на сборку веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c35a1-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="c35a1-265">**Обходной путь** После переустановки .NET Framework переустановите веб-страницы ASP.NET с синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="c35a1-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="c35a1-266">В файл *Web. config* в корневой папке компьютера будет добавлен следующий элемент, который обычно находится в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="c35a1-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="c35a1-267">Ошибка: приложения, ранее развернутые с помощью сборок ASP.NET в папке bin,</span><span class="sxs-lookup"><span data-stu-id="c35a1-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="c35a1-268">Во время развертывания копии веб-страницы ASP.NET сборок (например, *Microsoft. Web Pages. dll*) в папку *bin* веб-сайта на сервере.</span><span class="sxs-lookup"><span data-stu-id="c35a1-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="c35a1-269">(Это могло произойти автоматически во время развертывания или из-за того, что разработчик явно скопировал сборки.) Однако при установке выпуска бета-версии 3 возникают ошибки, например ошибки, при которых не удается найти определенные типы.</span><span class="sxs-lookup"><span data-stu-id="c35a1-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="c35a1-270">Это происходит потому, что несколько типов веб-страницы ASP.NET были перемещены в разные пространства имен для бета-версии 3.</span><span class="sxs-lookup"><span data-stu-id="c35a1-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="c35a1-271">**Обходной путь** </span><span class="sxs-lookup"><span data-stu-id="c35a1-271">**Workaround** </span></span>  
> <span data-ttu-id="c35a1-272">Очистите папку *bin* развернутого приложения, скопируйте новые сборки в папку (или повторно разверните приложение), а затем перезапустите приложение.</span><span class="sxs-lookup"><span data-stu-id="c35a1-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="c35a1-273">Ошибка: URL-адреса без расширений не могут найти файлы. cshtml/. vbhtml в IIS 7 или IIS 7,5</span><span class="sxs-lookup"><span data-stu-id="c35a1-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="c35a1-274">В IIS 7 или IIS 7,5 запросы с URL-адресом, следующим как, не могут найти страницы с расширением *CSHTML* или *VBHTML* :</span><span class="sxs-lookup"><span data-stu-id="c35a1-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="c35a1-275">Эта ошибка возникает, поскольку переписывание URL-адресов не включено по умолчанию для IIS 7 или IIS 7,5.</span><span class="sxs-lookup"><span data-stu-id="c35a1-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="c35a1-276">Сценарий ликелиест заключается в том, что вы не видите проблему при локальном тестировании с помощью IIS Express, но при развертывании веб-сайта на веб-сайте размещения эта проблема возникает.</span><span class="sxs-lookup"><span data-stu-id="c35a1-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="c35a1-277">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="c35a1-278">При наличии контроля над компьютером сервера установите обновление, описанное в разделе [обновление, которое позволяет определенным обработчикам iis 7,0 или iis 7,5 выполнять запросы, URL-адреса которых не заканчиваются точкой](https://support.microsoft.com/kb/980368).</span><span class="sxs-lookup"><span data-stu-id="c35a1-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="c35a1-279">Если у вас нет контроля над компьютером сервера (например, при развертывании на веб-сайте размещения), добавьте следующий адрес в файл *Web. config* веб-сайта:</span><span class="sxs-lookup"><span data-stu-id="c35a1-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="c35a1-280">Вопрос. Использование проекта веб-приложения или ASP.NET MVC и веб-страниц ASP.NET в одном приложении</span><span class="sxs-lookup"><span data-stu-id="c35a1-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="c35a1-281">Если вы использовали веб-страницы ASP.NET в проекте веб-приложения или в приложении MVC ASP.NET, может появиться сообщение об ошибке, которая не может быть найдена *вебпажехттпаппликатион* .</span><span class="sxs-lookup"><span data-stu-id="c35a1-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="c35a1-282">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-282">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-283">Если возникает эта ошибка, измените базовый класс, от которого наследуется приложение.</span><span class="sxs-lookup"><span data-stu-id="c35a1-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="c35a1-284">В файле *Global. asax* измените следующую строку:</span><span class="sxs-lookup"><span data-stu-id="c35a1-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="c35a1-285">На эту:</span><span class="sxs-lookup"><span data-stu-id="c35a1-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="c35a1-286">Это в действительности изменяет изменения, введенные для бета-версии 1 веб-страницы ASP.NET с синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="c35a1-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="c35a1-287">Вопрос. Развертывание приложения на компьютере, на котором не установлен SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="c35a1-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="c35a1-288">Приложения, включающие SQL Server Compact базы данных, могут выполняться на компьютере, где не установлена SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="c35a1-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="c35a1-289">Microsoft WebMatrix Beta 3 автоматически копирует эти двоичные файлы и выполняет соответствующие преобразования файла *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="c35a1-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="c35a1-290">**Обходной путь** Если необходимо скопировать эти файлы и внести изменения в файл *Web. config* вручную, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c35a1-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="c35a1-291">Скопируйте сборки ядра СУБД в папку *bin* (и вложенные папки) приложения на целевом компьютере:</span><span class="sxs-lookup"><span data-stu-id="c35a1-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="c35a1-292">Копирование *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **в** *\bin*</span><span class="sxs-lookup"><span data-stu-id="c35a1-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="c35a1-293">Копирование *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* \* **в** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="c35a1-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="c35a1-294">Копирование *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* **в** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="c35a1-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="c35a1-295">В корневой папке веб-сайта создайте или откройте файл *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="c35a1-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="c35a1-296">(В WebMatrix Beta 3 этот тип файлов доступен, если в диалоговом окне **Выбор типа файла** щелкнуть **все** .)</span><span class="sxs-lookup"><span data-stu-id="c35a1-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="c35a1-297">Добавьте следующий элемент в качестве дочернего для элемента **&gt;конфигурации&lt;** (не внутри элемента **&lt;system. Web&gt;** ):</span><span class="sxs-lookup"><span data-stu-id="c35a1-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="c35a1-298">Ошибка: вспомогательные методы баз данных и сеток не работают в Visual Basic среднего уровня доверия.</span><span class="sxs-lookup"><span data-stu-id="c35a1-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="c35a1-299">Если вы используете Visual Basic (создание файлов *. vbhtml* ), вспомогательные средства `Database` и `WebGrid` не будут работать, если приложение настроено для использования среднего уровня доверия.</span><span class="sxs-lookup"><span data-stu-id="c35a1-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="c35a1-300">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-300">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-301">Временно настройте приложение для использования полного доверия.</span><span class="sxs-lookup"><span data-stu-id="c35a1-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="c35a1-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="c35a1-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="c35a1-303">Ошибка: свойство "Encrypt" не распознано</span><span class="sxs-lookup"><span data-stu-id="c35a1-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="c35a1-304">SQL Server Compact 4,0 не распознает свойство `Encrypt` класса `SqlCeConnection`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="c35a1-305">Не следует использовать это свойство для шифрования файлов базы данных.</span><span class="sxs-lookup"><span data-stu-id="c35a1-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="c35a1-306">Свойство `Encrypt` устарело в выпуске SQL Server Compact 3,5 и было сохранено только для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="c35a1-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="c35a1-307">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-307">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-308">Для шифрования файлов базы данных SQL Server Compact 4.0 пользуйтесь свойством `Encryption Mode` класса `SqlCeConnection`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="c35a1-309">В следующем примере показано, как создать зашифрованную базу данных SQL Server Compact 4,0 с помощью свойства `Encryption Mode`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="c35a1-310">Чтобы изменить режим шифрования существующей базы данных SQL Server Compact 4,0, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c35a1-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="c35a1-311">Чтобы зашифровать незашифрованную базу данных SQL Server Compact 4,0, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c35a1-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="c35a1-312">Ошибка: требуются библиотеки C++ среды выполнения Microsoft Visual 2008</span><span class="sxs-lookup"><span data-stu-id="c35a1-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="c35a1-313">В собственных библиотеках DLL SQL Server Compact 4,0 требуются библиотеки среды C++ выполнения Microsoft Visual 2008 (x86, IA64 и x64) с пакетом обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="c35a1-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="c35a1-314">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-314">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-315">Установите .NET Framework 3,5 с пакетом обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="c35a1-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="c35a1-316">При этом также устанавливаются C++ Библиотеки среды выполнения Visual 2008 с пакетом обновления 1.</span><span class="sxs-lookup"><span data-stu-id="c35a1-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="c35a1-317">Вы можете скачать библиотеки из следующего расположения:</span><span class="sxs-lookup"><span data-stu-id="c35a1-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="c35a1-318">Обновление для C++ системы безопасности ATL распространяемого пакета Microsoft Visual 2008 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="c35a1-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="c35a1-319">Обратите внимание, что при установке .NET Framework 2,0, 3,0 или 4 *не* устанавливаются C++ библиотеки среды выполнения Visual 2008 с пакетом обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="c35a1-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="c35a1-320">Причина. Если SQL Server Compact устанавливается до установки .NET Framework на компьютере, неизменяемое имя поставщика не регистрируется в файле .NET Framework Machine. config.</span><span class="sxs-lookup"><span data-stu-id="c35a1-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="c35a1-321">SQL Server Compact можно установить на компьютере, на котором не установлен .NET Framework, поскольку для SQL Server Compact требуется платформа .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c35a1-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="c35a1-322">Если до установки SQL Server Compact не установлены ни .NET Framework версии 3,5, ни 4, SQL Server Compact программа установки не регистрирует неизменяемое имя поставщика в файле *Machine. config* .</span><span class="sxs-lookup"><span data-stu-id="c35a1-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="c35a1-323">Все приложения, использующие запись SQL Server Compact в файле *Machine. config* , завершатся ошибкой.</span><span class="sxs-lookup"><span data-stu-id="c35a1-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="c35a1-324">Запись регистрации неизменяемого имени в *Machine. config* выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c35a1-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="c35a1-325">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-325">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-326">Удалите SQL Server Compact 4,0 CTP1.</span><span class="sxs-lookup"><span data-stu-id="c35a1-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="c35a1-327">Скачайте и установите полные версии .NET Framework из следующего расположения:</span><span class="sxs-lookup"><span data-stu-id="c35a1-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="c35a1-328">Microsoft .NET Framework 3,5 с пакетом обновления 1 (SP1) (полный пакет)</span><span class="sxs-lookup"><span data-stu-id="c35a1-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="c35a1-329">Выпуск Microsoft .NET Framework 4,0 (полный пакет)</span><span class="sxs-lookup"><span data-stu-id="c35a1-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="c35a1-330">Затем переустановите [SQL Server Compact 4,0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span><span class="sxs-lookup"><span data-stu-id="c35a1-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="c35a1-331">Установка приложений</span><span class="sxs-lookup"><span data-stu-id="c35a1-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="c35a1-332">Причина. Установка приложения может занять много времени, если папка пользователя "Мои документы" перенаправлена в общую сетевую папку</span><span class="sxs-lookup"><span data-stu-id="c35a1-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="c35a1-333">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-333">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-334">Нет.</span><span class="sxs-lookup"><span data-stu-id="c35a1-334">None.</span></span> <span data-ttu-id="c35a1-335">Установка приложения может занять некоторое время, но будет установлена правильно.</span><span class="sxs-lookup"><span data-stu-id="c35a1-335">The application might take a while to install, but will install correctly.</span></span>

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="c35a1-336">Публикация приложений</span><span class="sxs-lookup"><span data-stu-id="c35a1-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="c35a1-337">Проблема. После публикации сайт может не работать, если поле "URL-адрес назначения" не имеет префикса http://или https://</span><span class="sxs-lookup"><span data-stu-id="c35a1-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="c35a1-338">Если в диалоговом окне **Параметры публикации** URL-адрес назначения не начинается с `http://` или `https://`, сайт может не работать после развертывания.</span><span class="sxs-lookup"><span data-stu-id="c35a1-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="c35a1-339">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-339">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-340">Убедитесь, что перед публикацией сайта URL-адрес назначения в диалоговом окне " **Параметры публикации** " начинается с `http://` или `https://`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="c35a1-341">Ошибка. Публикация базы данных MySQL завершается сбоем с ошибкой "не удалось опубликовать базу данных.</span><span class="sxs-lookup"><span data-stu-id="c35a1-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="c35a1-342">Это может произойти, если удаленная база данных не может выполнить скрипт ".</span><span class="sxs-lookup"><span data-stu-id="c35a1-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="c35a1-343">Эта ошибка может возникать по ряду причин.</span><span class="sxs-lookup"><span data-stu-id="c35a1-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="c35a1-344">Одной из причин возникновения этой ошибки является то, что скрипт базы данных содержит символ одинарной кавычки ('), а кодировка по умолчанию целевой базы данных MySQL — не UTF-8.</span><span class="sxs-lookup"><span data-stu-id="c35a1-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="c35a1-345">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-345">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-346">Задайте в качестве кодировки по умолчанию для удаленной базы данных MySQL кодировку UTF-8.</span><span class="sxs-lookup"><span data-stu-id="c35a1-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="c35a1-347">Другие проблемы</span><span class="sxs-lookup"><span data-stu-id="c35a1-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="c35a1-348">Ошибка: Поиск и фильтр не работают в отчетах для Group By: тип проблемы</span><span class="sxs-lookup"><span data-stu-id="c35a1-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="c35a1-349">При запуске отчета для сайта, если ввести текст в поле *Фильтровать по URL-адресу* и нажать кнопку *Поиск*, ничего не происходит.</span><span class="sxs-lookup"><span data-stu-id="c35a1-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="c35a1-350">Это связано с тем, что этот элемент управления не работает, пока состояние *Group By* отчета имеет значение *Тип выпуска*, которое является значением по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c35a1-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="c35a1-351">**Обходной путь** На вкладке " *Группировать по* " ленты щелкните *URL-адрес* , чтобы сгруппировать записи по их исходному URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="c35a1-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="c35a1-352">Текстовое поле и кнопка для фильтрации записей работают в этом состоянии.</span><span class="sxs-lookup"><span data-stu-id="c35a1-352">The text box and button to filter the entries are functional while in this state.</span></span>

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="c35a1-353">Ошибка. не удается запустить приложения WCF с IIS Express</span><span class="sxs-lookup"><span data-stu-id="c35a1-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="c35a1-354">Просмотр приложения WCF приводит к ошибке следующего вида:</span><span class="sxs-lookup"><span data-stu-id="c35a1-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="c35a1-355">*Не удалось загрузить файл или сборку "Microsoft. Web. admin, Version = 7.0.0.0, Culture = Neutral, PublicKeyToken = 31bf3856ad364e35" или одну из его зависимостей. Системе не удается найти указанный файл.*</span><span class="sxs-lookup"><span data-stu-id="c35a1-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="c35a1-356">Это происходит потому, что IIS Express бета-версии не поддерживает WCF по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c35a1-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="c35a1-357">**Обходной путь** Используйте одно из следующих обходных путей (для решения #2 требуется Microsoft Windows Vista или более поздней версии):</span><span class="sxs-lookup"><span data-stu-id="c35a1-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="c35a1-358">Скопируйте сборки *Microsoft. Web. dll* и *Microsoft. Web. Administration. dll* из расположения установки WebMatrix в каталог *bin* приложения WCF.</span><span class="sxs-lookup"><span data-stu-id="c35a1-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="c35a1-359">По умолчанию WebMatrix устанавливается во вложенную папку *Microsoft WebMatrix* в папке « *Program Files* » системы.</span><span class="sxs-lookup"><span data-stu-id="c35a1-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="c35a1-360">В Microsoft Windows Vista или более поздней версии создайте символьную ссылку для сборок в каталоге *bin* с помощью следующих команд.</span><span class="sxs-lookup"><span data-stu-id="c35a1-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="c35a1-361">(Этот подход имеет преимущество, так как он не создает копию сборок.)</span><span class="sxs-lookup"><span data-stu-id="c35a1-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="c35a1-362">Установите две сборки в глобальный кэш сборок.</span><span class="sxs-lookup"><span data-stu-id="c35a1-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="c35a1-363">В командной строке с повышенными привилегиями выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c35a1-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="c35a1-364">Вопрос. бета-версия 3 WebMatrix не может выполнять определенные задачи, требующие повышения прав</span><span class="sxs-lookup"><span data-stu-id="c35a1-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="c35a1-365">В бета-версии 3 WebMatrix не удается выполнить определенные задачи, требующие повышения прав, например установку дополнительных компонентов в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="c35a1-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="c35a1-366">В Windows Vista или Windows 7 вы выполнили вход с учетной записью, не обладающей правами администратора, и отключена функция контроля учетных записей (UAC).</span><span class="sxs-lookup"><span data-stu-id="c35a1-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="c35a1-367">Вы используете Microsoft Windows XP или Microsoft Windows Server 2003.</span><span class="sxs-lookup"><span data-stu-id="c35a1-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="c35a1-368">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-368">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-369">Большинству задач в WebMatrix Beta 3 не требуются административные разрешения.</span><span class="sxs-lookup"><span data-stu-id="c35a1-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="c35a1-370">Для тех, кто может выполнить операцию от имени администратора, или выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c35a1-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="c35a1-371">В Windows Vista или Windows 7 включите UAC.</span><span class="sxs-lookup"><span data-stu-id="c35a1-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="c35a1-372">В Windows XP добавьте пользователя в группу безопасности Администраторы.</span><span class="sxs-lookup"><span data-stu-id="c35a1-372">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="c35a1-373">Ошибка: "сайт из веб-коллекции" отключен</span><span class="sxs-lookup"><span data-stu-id="c35a1-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="c35a1-374">Параметр **сайт из веб-коллекции** отключен, если установщик веб-платформы 3,0 не установлен.</span><span class="sxs-lookup"><span data-stu-id="c35a1-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="c35a1-375">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-375">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-376">Установите [установщик веб-платформы Майкрософт 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="c35a1-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="c35a1-377">Вопрос. в Windows Server 2003 IIS Express не запускается для пользователя, не являющегося администратором</span><span class="sxs-lookup"><span data-stu-id="c35a1-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="c35a1-378">В Windows Server 2003 при запуске страницы или запуске IIS Express IIS Express не запускается.</span><span class="sxs-lookup"><span data-stu-id="c35a1-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="c35a1-379">Для веб-страниц отображается сообщение об ошибке, показывающее, что приложение запущено пользователем, не являющимся администратором.</span><span class="sxs-lookup"><span data-stu-id="c35a1-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="c35a1-380">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-380">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-381">Запустите WebMatrix Beta 3 в качестве пользователя с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="c35a1-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="c35a1-382">Дополнительные сведения см. в следующей статье базы знаний:</span><span class="sxs-lookup"><span data-stu-id="c35a1-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="c35a1-383">Приложение, запущенное неадминистративным пользователем, не может прослушивать трафик HTTP компьютера, на котором выполняется приложение, в Windows Vista, Windows Server 2003 или Windows XP.</span><span class="sxs-lookup"><span data-stu-id="c35a1-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="c35a1-384">Причина: Google Chrome недоступен в качестве варианта выполнения</span><span class="sxs-lookup"><span data-stu-id="c35a1-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="c35a1-385">Google Chrome не отображается в списке браузеров в разделе **Запуск** на вкладке **Главная** .</span><span class="sxs-lookup"><span data-stu-id="c35a1-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="c35a1-386">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-386">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-387">Некоторые версии Google Chrome неправильно регистрируются в компоненте "программы по умолчанию" в Windows.</span><span class="sxs-lookup"><span data-stu-id="c35a1-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="c35a1-388">В качестве обходного решения запустите Google Chrome, щелкните меню *Настройка и управление Google Chrome* , щелкните *Параметры*, а затем выберите команду *сделать Google Chrome браузером по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="c35a1-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="c35a1-389">Проблема. диалоговое окно "внешний ключ" не позволяет ввести первичный ключ</span><span class="sxs-lookup"><span data-stu-id="c35a1-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="c35a1-390">Диалоговое окно **внешний ключ** не позволяет ввести имя первичного ключа из таблицы первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="c35a1-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="c35a1-391">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-391">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-392">Это сделано намеренно.</span><span class="sxs-lookup"><span data-stu-id="c35a1-392">This is intentional.</span></span> <span data-ttu-id="c35a1-393">Не нужно вводить имя первичного ключа из таблицы первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="c35a1-393">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="c35a1-394">Ошибка: кнопка "связи" отключена</span><span class="sxs-lookup"><span data-stu-id="c35a1-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="c35a1-395">Кнопка **связи** на вкладке **Таблица** в рабочей области **базы данных** отключена для SQL Server Compact баз данных.</span><span class="sxs-lookup"><span data-stu-id="c35a1-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="c35a1-396">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-396">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-397">Нет.</span><span class="sxs-lookup"><span data-stu-id="c35a1-397">None.</span></span> <span data-ttu-id="c35a1-398">SQL Server Compact не поддерживает связи между таблицами.</span><span class="sxs-lookup"><span data-stu-id="c35a1-398">SQL Server Compact does not support relationships between tables.</span></span>

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="c35a1-399">Ошибка: параметризованные запросы SQL создают исключения</span><span class="sxs-lookup"><span data-stu-id="c35a1-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="c35a1-400">В SQL Server Compact 4,0, если не указать тип данных, например `SqlDbType` или `DbType` для параметров в параметризованных запросах, при выполнении запроса выдается исключение.</span><span class="sxs-lookup"><span data-stu-id="c35a1-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="c35a1-401">**Обходное решение**</span><span class="sxs-lookup"><span data-stu-id="c35a1-401">**Workaround**</span></span>  
> <span data-ttu-id="c35a1-402">Явно задайте тип данных для таких параметров, как `SqlDbType` или `DbType`.</span><span class="sxs-lookup"><span data-stu-id="c35a1-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="c35a1-403">Это важно в случае типов данных BLOB (`image` и `ntext`).</span><span class="sxs-lookup"><span data-stu-id="c35a1-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="c35a1-404">Используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="c35a1-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="c35a1-405">Дополнительные сведения см. в разделе</span><span class="sxs-lookup"><span data-stu-id="c35a1-405">For More Information</span></span>

<span data-ttu-id="c35a1-406">Дополнительные сведения о бета-версии 3 WebMatrix см. на следующих веб-сайтах:</span><span class="sxs-lookup"><span data-stu-id="c35a1-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="c35a1-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="c35a1-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="c35a1-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c35a1-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="c35a1-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="c35a1-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

---

<span data-ttu-id="c35a1-410">© 2010 Корпорация Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c35a1-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="c35a1-411">Все права защищены.</span><span class="sxs-lookup"><span data-stu-id="c35a1-411">All Rights Reserved.</span></span> <span data-ttu-id="c35a1-412">[Условия использования](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="c35a1-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
