---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: Обновление приложения ASP.NET MVC 1,0 до ASP.NET MVC 2 | Документация Майкрософт
author: rick-anderson
description: В этом документе описано, как выполнить обновление вручную и с помощью мастера ASP.NET MVC 1,0 для ASP.NET MVC 2. Этот документ также доступен для d...
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517302"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a><span data-ttu-id="6a6d2-104">Обновление приложения ASP.NET MVC 1.0 до ASP.NET MVC 2</span><span class="sxs-lookup"><span data-stu-id="6a6d2-104">Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2</span></span>

> <span data-ttu-id="6a6d2-105">В этом документе описано, как выполнить обновление вручную и с помощью мастера ASP.NET MVC 1,0 для ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-105">This document describes both how to upgrade manually and with a wizard an ASP.NET MVC 1.0 Application to ASP.NET MVC 2.</span></span> <span data-ttu-id="6a6d2-106">Этот документ также доступен для [загрузки](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span><span class="sxs-lookup"><span data-stu-id="6a6d2-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span></span>

## <a name="introduction"></a><span data-ttu-id="6a6d2-107">Введение</span><span class="sxs-lookup"><span data-stu-id="6a6d2-107">Introduction</span></span>

<span data-ttu-id="6a6d2-108">ASP.NET MVC 2 можно установить параллельно с ASP.NET MVC 1,0 на том же сервере.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-108">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server.</span></span> <span data-ttu-id="6a6d2-109">Это позволяет разработчикам приложений гибко выбирать время обновления приложения ASP.NET MVC 1,0 до ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-109">This gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span>

<span data-ttu-id="6a6d2-110">В состав Visual Studio 2010 входит мастер, который обновляет существующие проекты ASP.NET MVC 1,0, созданные с помощью Visual Studio 2008, до ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-110">Visual Studio 2010 includes a wizard that upgrades existing ASP.NET MVC 1.0 projects built with Visual Studio 2008 to ASP.NET MVC 2.</span></span> <span data-ttu-id="6a6d2-111">Мастер обновления запускается путем открытия проекта ASP.NET MVC 1,0 в Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-111">The upgrade wizard is initiated by opening an ASP.NET MVC 1.0 project in Visual Studio 2010.</span></span>

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a><span data-ttu-id="6a6d2-112">Мастер обновления для ASP.NET MVC 1,0 в Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="6a6d2-112">Upgrade Wizard for ASP.NET MVC 1.0 on Visual Studio 2008 SP1</span></span>

<span data-ttu-id="6a6d2-113">Чтобы обновить приложение ASP.NET MVC 1,0 до ASP.NET MVC 2 в Visual Studio 2008 с пакетом обновления 1 (SP1), используйте приложение (не поддерживается) Мвкаппконвертер.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-113">To upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2 in Visual Studio 2008 SP1, use the (unsupported) MvcAppConverter application.</span></span> <span data-ttu-id="6a6d2-114">Это приложение можно скачать по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="6a6d2-114">You can download this application from the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a><span data-ttu-id="6a6d2-115">Обновление проекта ASP.NET MVC 1,0 вручную</span><span class="sxs-lookup"><span data-stu-id="6a6d2-115">Manually Upgrading an ASP.NET MVC 1.0 Project</span></span>

<span data-ttu-id="6a6d2-116">Чтобы вручную обновить существующее приложение ASP.NET MVC 1,0 до версии 2, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-116">To manually upgrade an existing ASP.NET MVC 1.0 application to version 2, follow these steps:</span></span>

1. <span data-ttu-id="6a6d2-117">Создайте резервную копию существующего проекта.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-117">Make a backup of the existing project.</span></span>
2. <span data-ttu-id="6a6d2-118">В текстовом редакторе откройте файл проекта (файл с расширением CSPROJ или VBPROJ) и найдите элемент Прожекттипегуид.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-118">In a text editor, open the project file (the file with the .csproj or .vbproj file extension) and find the ProjectTypeGuid element.</span></span> <span data-ttu-id="6a6d2-119">В качестве значения этого элемента замените GUID {603c0e0b-db56-11dc-be95-000d561079b0} на {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-119">As the value of that element, replace the GUID {603c0e0b-db56-11dc-be95-000d561079b0} with {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span></span> <span data-ttu-id="6a6d2-120">По завершении значение этого элемента должно быть следующим:</span><span class="sxs-lookup"><span data-stu-id="6a6d2-120">When you are done, the value of that element should be as follows:</span></span> 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. <span data-ttu-id="6a6d2-121">В корневой папке веб-приложения измените файл Web. config.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-121">In the Web application root folder, edit the Web.config file.</span></span> <span data-ttu-id="6a6d2-122">Выполните поиск System. Web. MVC, Version = 1.0.0.0 и замените все экземпляры на System. Web. MVC, Version = 2.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-122">Search for System.Web.Mvc, Version=1.0.0.0 and replace all instances with System.Web.Mvc, Version=2.0.0.0.</span></span>
4. <span data-ttu-id="6a6d2-123">Повторите предыдущий шаг для файла Web. config, расположенного в папке Views.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-123">Repeat the previous step for the Web.config file located in the Views folder.</span></span>
5. <span data-ttu-id="6a6d2-124">Откройте проект с помощью Visual Studio, а затем в **Обозреватель решений**разверните узел **ссылки** .</span><span class="sxs-lookup"><span data-stu-id="6a6d2-124">Open the project using Visual Studio, and in **Solution Explorer**, expand the **References** node.</span></span> <span data-ttu-id="6a6d2-125">Удалите ссылку на System. Web. MVC (которая указывает на сборку версии 1,0).</span><span class="sxs-lookup"><span data-stu-id="6a6d2-125">Delete the reference to System.Web.Mvc (which points to the version 1.0 assembly).</span></span> <span data-ttu-id="6a6d2-126">Добавьте ссылку на System. Web. MVC (v 2.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="6a6d2-126">Add a reference to System.Web.Mvc (v2.0.0.0).</span></span>
6. <span data-ttu-id="6a6d2-127">Добавьте следующий элемент bindingRedirect в файл Web. config в корне приложения в разделе конфигурации:</span><span class="sxs-lookup"><span data-stu-id="6a6d2-127">Add the following bindingRedirect element to the Web.config file in the application root under the configuraton section:</span></span>   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. <span data-ttu-id="6a6d2-128">Создайте пустое приложение ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-128">Create a new empty ASP.NET MVC 2 application.</span></span> <span data-ttu-id="6a6d2-129">Скопируйте файлы из папки Scripts нового приложения в папку Scripts существующего приложения.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-129">Copy the files from the Scripts folder of the new application into the Scripts folder of the existing application.</span></span>
8. <span data-ttu-id="6a6d2-130">Обновите существующий CSS-файл приложения €™ s с определениями стиля CSS в файле Site. CSS.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-130">Update the existing applicationâ€™s CSS file with the CSS style definitions in the Site.css file.</span></span>
9. <span data-ttu-id="6a6d2-131">Скомпилируйте приложение и запустите его.</span><span class="sxs-lookup"><span data-stu-id="6a6d2-131">Compile the application and run it.</span></span> <span data-ttu-id="6a6d2-132">Если возникнут какие-либо ошибки, см. раздел критические изменения на странице [новые возможности ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) .</span><span class="sxs-lookup"><span data-stu-id="6a6d2-132">If any errors occur, refer to the Breaking Changes section of the [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) page.</span></span>
