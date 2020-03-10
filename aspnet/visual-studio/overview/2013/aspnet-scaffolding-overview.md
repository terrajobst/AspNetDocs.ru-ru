---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Формирование шаблонов ASP.NET в Visual Studio 2013 | Документация Майкрософт
author: Rick-Anderson
description: Формирование шаблонов ASP.NET — это новая функция, включенная в Visual Studio 2013.
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449568"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="c95aa-103">Формирование шаблонов ASP.NET в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c95aa-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>

<span data-ttu-id="c95aa-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c95aa-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c95aa-105">Формирование шаблонов ASP.NET — это новая функция, включенная в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c95aa-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>

## <a name="overview"></a><span data-ttu-id="c95aa-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="c95aa-106">Overview</span></span>

<span data-ttu-id="c95aa-107">Формирование шаблонов ASP.NET — это платформа создания кода для веб-приложений ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c95aa-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="c95aa-108">Visual Studio 2013 включает предварительно установленные генераторы кода для проектов MVC и веб-API.</span><span class="sxs-lookup"><span data-stu-id="c95aa-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="c95aa-109">Для быстрого добавления кода, взаимодействующего с моделями данных, необходимо добавить в проект формирование шаблонов.</span><span class="sxs-lookup"><span data-stu-id="c95aa-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="c95aa-110">Использование формирования шаблонов может сократить время, необходимое для разработки стандартных операций с данными в проекте.</span><span class="sxs-lookup"><span data-stu-id="c95aa-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="c95aa-111">По умолчанию Visual Studio 2013 не поддерживает создание кода для проекта веб-форм, но вы можете использовать формирование шаблонов с веб-формами, либо добавив зависимости MVC в проект, либо установив расширение.</span><span class="sxs-lookup"><span data-stu-id="c95aa-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="c95aa-112">Ниже показаны оба подхода.</span><span class="sxs-lookup"><span data-stu-id="c95aa-112">Both approaches are shown below.</span></span>

<span data-ttu-id="c95aa-113">Visual Studio 2013 обновление 2 (в настоящее время RC) обеспечивает возможность расширения формирования шаблонов ASP.NET в соответствии с требованиями вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="c95aa-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="c95aa-114">С помощью этой функции можно создать настраиваемый шаблон формирования шаблонов и добавить его в диалоговое окно Добавление нового шаблона.</span><span class="sxs-lookup"><span data-stu-id="c95aa-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="c95aa-115">В настраиваемом шаблоне указывается код, который создается при добавлении шаблона элемента.</span><span class="sxs-lookup"><span data-stu-id="c95aa-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="c95aa-116">Дополнительные сведения см. [в разделе Создание пользовательского шаблона для Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span><span class="sxs-lookup"><span data-stu-id="c95aa-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c95aa-117">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c95aa-117">Prerequisites</span></span>

<span data-ttu-id="c95aa-118">Чтобы использовать формирование шаблонов ASP.NET, необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="c95aa-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="c95aa-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c95aa-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="c95aa-120">Веб-Средства для разработчиков (часть установки Visual Studio 2013 по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="c95aa-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="c95aa-121">ASP.NET Web Frameworks and Tools 2013 (часть установки Visual Studio 2013 по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="c95aa-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="c95aa-122">Добавление шаблона элемента в MVC или веб-API</span><span class="sxs-lookup"><span data-stu-id="c95aa-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="c95aa-123">Чтобы добавить шаблон, щелкните правой кнопкой мыши проект или папку в проекте и выберите **Добавить** — новый шаблонный **элемент**, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="c95aa-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![Добавить элемент шаблона](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="c95aa-125">В окне **Добавление шаблона** выберите тип шаблона для добавления.</span><span class="sxs-lookup"><span data-stu-id="c95aa-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![Выбор типа шаблона](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="c95aa-127">Окно **Добавление контроллера** дает возможность выбрать параметры для создания контроллера, в том числе использовать новые возможности асинхронного режима из Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="c95aa-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![добавить контроллер](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="c95aa-129">Для вашего сценария создаются соответствующие классы и страницы.</span><span class="sxs-lookup"><span data-stu-id="c95aa-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="c95aa-130">Например, на следующем рисунке показан контроллер MVC и представления, созданные с помощью формирования шаблонов для класса модели с именем movies.</span><span class="sxs-lookup"><span data-stu-id="c95aa-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![Созданные файлы](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="c95aa-132">Добавление шаблона элемента в веб-формы</span><span class="sxs-lookup"><span data-stu-id="c95aa-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="c95aa-133">Чтобы добавить формирование шаблонов, создающее код веб-форм, необходимо либо установить расширение в Visual Studio, либо добавить зависимости MVC.</span><span class="sxs-lookup"><span data-stu-id="c95aa-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="c95aa-134">Ниже показаны оба подхода, но необходимо выполнить только один из этих подходов.</span><span class="sxs-lookup"><span data-stu-id="c95aa-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="c95aa-135">Расширение формирования шаблонов веб-форм</span><span class="sxs-lookup"><span data-stu-id="c95aa-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="c95aa-136">Вы можете установить расширение Visual Studio, позволяющее использовать формирование шаблонов в проекте веб-форм.</span><span class="sxs-lookup"><span data-stu-id="c95aa-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="c95aa-137">В Visual Studio выберите **инструменты** , а затем — **расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="c95aa-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="c95aa-138">В этом диалоговом окне выполните поиск **шаблонов веб-форм**в коллекции Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c95aa-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![Установка шаблонов веб-форм](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="c95aa-140">Дополнительные сведения см. в разделе [формирование шаблонов веб-форм](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span><span class="sxs-lookup"><span data-stu-id="c95aa-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="c95aa-141">Зависимости MVC</span><span class="sxs-lookup"><span data-stu-id="c95aa-141">MVC Dependencies</span></span>

<span data-ttu-id="c95aa-142">Чтобы добавить зависимости MVC, выберите **добавить** - **Новый**шаблонный элемент.</span><span class="sxs-lookup"><span data-stu-id="c95aa-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="c95aa-143">В окне Добавление шаблона выберите **зависимости MVC**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c95aa-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![добавить зависимости MVC](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="c95aa-145">Существует два варианта формирования шаблонов MVC. Минимальный и полный.</span><span class="sxs-lookup"><span data-stu-id="c95aa-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="c95aa-146">Если выбрать минимум, в проект будут добавлены только пакеты NuGet и ссылки для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c95aa-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="c95aa-147">Если выбран параметр Full, добавляются минимальные зависимости, а также необходимые файлы содержимого для проекта MVC.</span><span class="sxs-lookup"><span data-stu-id="c95aa-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="c95aa-148">Чтобы легко использовать формирование шаблонов, выберите полные зависимости.</span><span class="sxs-lookup"><span data-stu-id="c95aa-148">To easily use scaffolding, select Full dependencies.</span></span>

![выбрать полные зависимости](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="c95aa-150">После добавления зависимостей вы увидите файл **readme. txt** .</span><span class="sxs-lookup"><span data-stu-id="c95aa-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="c95aa-151">Внимательно следуйте инструкциям в этом файле, чтобы убедиться, что проект работает правильно.</span><span class="sxs-lookup"><span data-stu-id="c95aa-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="c95aa-152">После выполнения действий, описанных в файле readme. txt, можно добавить новый шаблонный элемент, как показано в предыдущем разделе о MVC и веб-API.</span><span class="sxs-lookup"><span data-stu-id="c95aa-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="c95aa-153">Автоматически созданные представления и контроллер будут правильно работать в рамках проекта.</span><span class="sxs-lookup"><span data-stu-id="c95aa-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="c95aa-154">Учебники</span><span class="sxs-lookup"><span data-stu-id="c95aa-154">Tutorials</span></span>

<span data-ttu-id="c95aa-155">Сведения о создании настраиваемого шаблона формирования шаблонов см. в разделе [Создание пользовательского шаблона для Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span><span class="sxs-lookup"><span data-stu-id="c95aa-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="c95aa-156">Сведения о настройке созданных файлов см. в разделе [Настройка созданных файлов из диалогового окна Создание шаблона элемента](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span><span class="sxs-lookup"><span data-stu-id="c95aa-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="c95aa-157">Пример использования формирования шаблонов с **Database Firstной разработкой**см. в разделе [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span><span class="sxs-lookup"><span data-stu-id="c95aa-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="c95aa-158">Пример использования формирования шаблонов в проекте **MVC** см. в разделе [Начало работы with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c95aa-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="c95aa-159">Пример использования формирования шаблонов в проекте **веб-API** см. в разделе [Создание REST API с маршрутизацией атрибутов в веб-API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="c95aa-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>
