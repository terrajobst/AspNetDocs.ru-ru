---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Заметки о выпуске для ASP.NET and Web Tools 2013,1 для Visual Studio 2012 | Документация Майкрософт
author: microsoft
description: В этом документе описывается выпуск ASP.NET and Web Tools 2013,1 для Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467106"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="dfe2c-103">Заметки о выпуске ASP.NET and Web Tools 2013.1 для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="dfe2c-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="dfe2c-104">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="dfe2c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="dfe2c-105">В этом документе описывается выпуск ASP.NET and Web Tools 2013,1 для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="dfe2c-106">Содержимое</span><span class="sxs-lookup"><span data-stu-id="dfe2c-106">Contents</span></span>

- [<span data-ttu-id="dfe2c-107">Заметки об установке</span><span class="sxs-lookup"><span data-stu-id="dfe2c-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="dfe2c-108">Требования к программному обеспечению</span><span class="sxs-lookup"><span data-stu-id="dfe2c-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="dfe2c-109">Новые функции в ASP.NET and Web Tools 2013,1 для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="dfe2c-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="dfe2c-110">Начальная загрузка</span><span class="sxs-lookup"><span data-stu-id="dfe2c-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="dfe2c-111">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="dfe2c-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="dfe2c-112">Шаблон ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="dfe2c-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="dfe2c-113">Шаблон веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="dfe2c-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="dfe2c-114">Шаблоны элементов</span><span class="sxs-lookup"><span data-stu-id="dfe2c-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="dfe2c-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="dfe2c-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="dfe2c-116">Формирование шаблонов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dfe2c-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="dfe2c-117">Редактор Razor</span><span class="sxs-lookup"><span data-stu-id="dfe2c-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="dfe2c-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="dfe2c-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="dfe2c-119">Известные проблемы и критические изменения</span><span class="sxs-lookup"><span data-stu-id="dfe2c-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="dfe2c-120">Формирование шаблонов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dfe2c-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="dfe2c-121">Формирование шаблонов MVC и веб-API — HTTP 404, ошибка "не найдено"</span><span class="sxs-lookup"><span data-stu-id="dfe2c-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="dfe2c-122">Visual Studio Express 2012 для веб-сайта прекращает работу после добавления шаблона элемента</span><span class="sxs-lookup"><span data-stu-id="dfe2c-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="dfe2c-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="dfe2c-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="dfe2c-124">Просмотр файла CSHTML с помощью кнопки "Обзор" или нажатия клавиши F5 приводит к ошибке сервера</span><span class="sxs-lookup"><span data-stu-id="dfe2c-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="dfe2c-125">Перезапись URL-адреса и тильда (~)</span><span class="sxs-lookup"><span data-stu-id="dfe2c-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="dfe2c-126">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="dfe2c-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="dfe2c-127">Замечания по установке</span><span class="sxs-lookup"><span data-stu-id="dfe2c-127">Installation Notes</span></span>

<span data-ttu-id="dfe2c-128">[Установка](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013,1 для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="dfe2c-129">Требования к программному обеспечению</span><span class="sxs-lookup"><span data-stu-id="dfe2c-129">Software Requirements</span></span>

<span data-ttu-id="dfe2c-130">Необходимо иметь Visual Studio 2012 или Visual Studio Express 2012 для Web.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="dfe2c-131">Новые функции в ASP.NET and Web Tools 2013,1 для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="dfe2c-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="dfe2c-132">Загрузке</span><span class="sxs-lookup"><span data-stu-id="dfe2c-132">Bootstrap</span></span>

<span data-ttu-id="dfe2c-133">При формировании шаблонов MVC 5 и представлений в разметке для представлений используется [Начальная](http://getbootstrap.com/)загрузка.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="dfe2c-134">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="dfe2c-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="dfe2c-135">Шаблон ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="dfe2c-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="dfe2c-136">Мы добавили новый шаблон MVC 5.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="dfe2c-137">Он ссылается на последние версии пакетов NuGet для MVC 5, и для добавления контроллеров и представлений можно использовать формирование шаблонов.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="dfe2c-138">Шаблон веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="dfe2c-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="dfe2c-139">Мы добавили новый шаблон веб-API 2.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="dfe2c-140">Он ссылается на последние версии пакетов NuGet для Web API 2, и вы можете использовать формирование шаблонов для добавления контроллеров и представлений.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="dfe2c-141">Шаблоны элементов</span><span class="sxs-lookup"><span data-stu-id="dfe2c-141">Item Templates</span></span>

<span data-ttu-id="dfe2c-142">Мы добавили новые шаблоны элементов для представлений MVC 5, Web Pages (Razor 3) и Web API 2 Controllers.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="dfe2c-143">Они устанавливают связанные пакеты NuGet в проект при добавлении новых элементов.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="dfe2c-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="dfe2c-144">Entity Framework 6</span></span>

<span data-ttu-id="dfe2c-145">При формировании шаблона контроллера MVC или веб-API с помощью Entity Framework используется платформа 6.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="dfe2c-146">Дополнительные сведения о Entity Framework см. в [журнале версий Entity Framework](https://msdn.com/data/jj574253).</span><span class="sxs-lookup"><span data-stu-id="dfe2c-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="dfe2c-147">Вы также можете скачать и установить инструменты Entity Framework 6 для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="dfe2c-148">См. раздел [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span><span class="sxs-lookup"><span data-stu-id="dfe2c-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="dfe2c-149">Формирование шаблонов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dfe2c-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="dfe2c-150">Формирование шаблонов ASP.NET — это платформа создания кода для веб-приложений ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="dfe2c-151">Это упрощает добавление в проект стандартного кода, взаимодействующего с моделью данных.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="dfe2c-152">В предыдущих версиях Visual Studio формирование шаблонов было ограничено ASP.NET проектами MVC.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="dfe2c-153">В этом обновлении теперь можно использовать формирование шаблонов для любого проекта ASP.NET, включая веб-формы.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="dfe2c-154">Это обновление не поддерживает создание страниц для проекта веб-форм, но вы по-прежнему можете использовать формирование шаблонов с веб-формами, добавив зависимости MVC в проект.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="dfe2c-155">Поддержка создания страниц для веб-форм будет добавлена в будущем обновлении.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="dfe2c-156">При использовании формирования шаблонов убедитесь, что в проекте установлены все необходимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="dfe2c-157">Например, если начать с проекта веб-форм ASP.NET, а затем использовать формирование шаблонов для добавления контроллера веб-API, необходимые пакеты NuGet и ссылки добавляются в проект автоматически.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="dfe2c-158">Чтобы добавить формирование шаблонов MVC в проект веб-форм, добавьте новый шаблонный **элемент** и выберите **зависимости MVC 5** в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="dfe2c-159">Существует два варианта формирования шаблонов MVC. Минимальный и полный.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="dfe2c-160">Если выбрать минимум, в проект будут добавлены только пакеты NuGet и ссылки для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="dfe2c-161">Если выбран параметр Full, добавляются минимальные зависимости, а также необходимые файлы содержимого для проекта MVC.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="dfe2c-162">Поддержка формирования шаблонов асинхронных контроллеров использует новые асинхронные функции из Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="dfe2c-163">Дополнительные сведения и учебники см. в разделе [Общие сведения о формировании шаблонов ASP.NET](../2013/aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfe2c-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="dfe2c-164">В этих руководствах показано формирование шаблонов с помощью Visual Studio 2013, но они также применимы к ASP.NET and Web Tools 2013,1 для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="dfe2c-165">Редактор Razor</span><span class="sxs-lookup"><span data-stu-id="dfe2c-165">Razor Editor</span></span>

<span data-ttu-id="dfe2c-166">В этом обновлении Visual Studio 2012 теперь поддерживает инструментарий и редактирование Razor 3.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="dfe2c-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="dfe2c-167">NuGet 2.7</span></span>

<span data-ttu-id="dfe2c-168">NuGet 2,7 включает широкий набор новых функций, которые подробно описаны в [заметках о выпуске NuGet 2,7](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="dfe2c-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="dfe2c-169">Эта версия NuGet устраняет необходимость явно разрешить NuGet восстанавливать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="dfe2c-170">При установке NuGet 2,7 пользователям неявно предоставляется согласие на автоматическое восстановление отсутствующих пакетов.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="dfe2c-171">Пользователи могут явно отказаться от восстановления пакетов с помощью параметров NuGet в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="dfe2c-172">Это изменение упрощает восстановление пакетов.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="dfe2c-173">Известные проблемы и критические изменения</span><span class="sxs-lookup"><span data-stu-id="dfe2c-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="dfe2c-174">Формирование шаблонов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dfe2c-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="dfe2c-175">Формирование шаблонов MVC и веб-API — HTTP 404, ошибка "не найдено"</span><span class="sxs-lookup"><span data-stu-id="dfe2c-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="dfe2c-176">Если при добавлении шаблона элемента в проект возникла ошибка, возможно, проект будет оставаться в нестабильном состоянии.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="dfe2c-177">Откат некоторых изменений, внесенных в формирование шаблонов, будет выполнен, однако откат других изменений, таких как установленные пакеты NuGet, не будет отменен.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="dfe2c-178">При откате изменений конфигурации маршрутизации пользователи получат ошибку HTTP 404 при переходе к шаблонным элементам.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="dfe2c-179">Чтобы устранить эту ошибку для MVC, добавьте новый шаблонный элемент и выберите зависимости MVC 5 (минимальное или полное).</span><span class="sxs-lookup"><span data-stu-id="dfe2c-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="dfe2c-180">Этот процесс добавит все необходимые изменения в проект.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="dfe2c-181">Чтобы устранить эту ошибку для веб-API, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="dfe2c-182">Добавьте в проект следующий класс WebApiConfig.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="dfe2c-183">Настройте WebApiConfig. Register в методе запуска приложения\_в Global. asax следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dfe2c-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="dfe2c-184">Visual Studio Express 2012 для веб-сайта прекращает работу после добавления шаблона элемента</span><span class="sxs-lookup"><span data-stu-id="dfe2c-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="dfe2c-185">Если Visual Studio Express 2012 для веб-сайта прекращает работу после добавления шаблона элемента с Entity Framework (например, контроллер веб-API 2 с действиями с помощью Entity Framework), возможно, Visual Studio Express не удалось загрузить машинный образ сборки. зависит от System. Web. Extensions.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="dfe2c-186">Чтобы устранить эту проблему, настройте Visual Studio Express для работы с изображением MSIL для System. Web. Extensions:</span><span class="sxs-lookup"><span data-stu-id="dfe2c-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="dfe2c-187">Откройте командную строку в режиме администратора.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="dfe2c-188">Перейдите в%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE или% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\IDE (для 64 разрядов Windows).</span><span class="sxs-lookup"><span data-stu-id="dfe2c-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="dfe2c-189">Откройте файл Ввдекспресс. exe. config в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="dfe2c-190">Добавьте следующую строку в элемент конфигурации &lt;&gt;/&lt;среды выполнения&gt;:</span><span class="sxs-lookup"><span data-stu-id="dfe2c-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="dfe2c-191">Перезапустите Visual Studio Express 2012 для Web.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="dfe2c-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="dfe2c-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="dfe2c-193">Просмотр файла CSHTML с помощью кнопки "Обзор" или нажатия клавиши F5 приводит к ошибке сервера</span><span class="sxs-lookup"><span data-stu-id="dfe2c-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="dfe2c-194">При создании проекта MVC 5 в Visual Studio 2012 (или открытом в Visual Studio 2012 проект MVC 5, созданный в Visual Studio 2013) и попытке просмотра файла CSHTML с помощью команды "Обзор" или "F5" вы получите сообщение об ошибке **"ошибка сервера" в приложении "/"** .</span><span class="sxs-lookup"><span data-stu-id="dfe2c-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="dfe2c-195">Сервер пытается переходить к `http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="dfe2c-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="dfe2c-196">Чтобы устранить эту проблему, измените значение параметра **действие при запуске** в проекте на **определенную страницу**.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="dfe2c-197">Вам не нужно указывать значение для страницы.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="dfe2c-198">После внесения этого изменения при нажатии клавиши F5 выполняется переход к корню приложения (`http://localhost:XXXX`).</span><span class="sxs-lookup"><span data-stu-id="dfe2c-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="dfe2c-199">Это поведение отличается от поведения проектов MVC 5 в Visual Studio 2013, где **Текущая страница** запускает открытую страницу.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="dfe2c-200">Перезапись URL-адреса и тильда (~)</span><span class="sxs-lookup"><span data-stu-id="dfe2c-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="dfe2c-201">После обновления до ASP.NET Razor 3 или ASP.NET MVC 5, тильда (~) может перестать работать правильно, если используется переписывание URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="dfe2c-202">Переписывание URL-адресов влияет на нотацию тильды (~) в HTML-элементах, таких как &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, и в результате тильда больше не сопоставляется с корневым каталогом.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="dfe2c-203">Например, при перезаписи запросов для **ASP.NET/Content** в **ASP.NET**атрибут href в &lt;A href = "~/контент/"/&gt; разрешается в **/контент/контент/** вместо **/** .</span><span class="sxs-lookup"><span data-stu-id="dfe2c-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="dfe2c-204">Чтобы отключить это изменение, можно задать для контекста **IIS\_васурлревриттен** значение false на каждой веб-странице или в **приложении\_BeginRequest** в Global. asax.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="dfe2c-205">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="dfe2c-205">Templates</span></span>

<span data-ttu-id="dfe2c-206">При создании проектов ASP.NET MVC с помощью Visual Studio 2012 на Windows 8.1 или Windows Server 2012 R2 в Visual Studio отображается сообщение об ошибке "Настройка веб-узла [URL] для ASP.NET 4,5".</span><span class="sxs-lookup"><span data-stu-id="dfe2c-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![Ошибка конфигурации](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="dfe2c-208">Вы видите эту ошибку, так как Visual Studio 2012 не включает компонент ASP.NET 4,5 при установке в этих выпусках Windows.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="dfe2c-209">Чтобы включить ASP.NET 4,5, выполните действия, описанные в разделе [Включение или отключение компонентов Windows](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span><span class="sxs-lookup"><span data-stu-id="dfe2c-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Включение или отключение функций Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="dfe2c-211">Кроме того, можно включить ASP.NET 4,5 с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="dfe2c-212">Откройте командную строку в режиме администратора.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="dfe2c-213">Выполните следующую команду, чтобы включить ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="dfe2c-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
