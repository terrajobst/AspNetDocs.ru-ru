---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: Часть 1. Обзор и файл-> новый проект | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. Часть 1 охватывает общие сведения и файловый > новый проект.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451284"
---
# <a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="37783-104">Часть 1. Обзор и файл > новый проект</span><span class="sxs-lookup"><span data-stu-id="37783-104">Part 1: Overview and File->New Project</span></span>

<span data-ttu-id="37783-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="37783-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="37783-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="37783-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="37783-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="37783-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="37783-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="37783-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="37783-109">Часть 1 охватывает общие сведения и файловый&gt;новый проект.</span><span class="sxs-lookup"><span data-stu-id="37783-109">Part 1 covers Overview and File-&gt;New Project.</span></span>

## <a name="overview"></a><span data-ttu-id="37783-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="37783-110">Overview</span></span>

<span data-ttu-id="37783-111">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Web Developer для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="37783-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="37783-112">Мы будем замедленнее, так что веб-разработка на уровне "новичок" работает.</span><span class="sxs-lookup"><span data-stu-id="37783-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="37783-113">Приложение, которое мы будем создавать, — это простое музыкальное хранилище.</span><span class="sxs-lookup"><span data-stu-id="37783-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="37783-114">Приложение состоит из трех основных частей: покупки, извлечения и администрирования.</span><span class="sxs-lookup"><span data-stu-id="37783-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="37783-115">Посетители могут просматривать альбомы по жанрам:</span><span class="sxs-lookup"><span data-stu-id="37783-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="37783-116">Они могут просматривать один альбом и добавлять его в корзину:</span><span class="sxs-lookup"><span data-stu-id="37783-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="37783-117">Они могут просматривать свою корзину, удаляя все ненужные элементы:</span><span class="sxs-lookup"><span data-stu-id="37783-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="37783-118">При переходе к извлечению будут предложены вход в систему или регистрация для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="37783-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="37783-119">После создания учетной записи она может выполнить заказ, заполнив сведения о доставке и оплате.</span><span class="sxs-lookup"><span data-stu-id="37783-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="37783-120">Для простоты мы используем неудивительное продвижение: все это бесплатное, если ввести код продвижения "FREE"!</span><span class="sxs-lookup"><span data-stu-id="37783-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="37783-121">После упорядочения они видят простой экран подтверждения:</span><span class="sxs-lookup"><span data-stu-id="37783-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="37783-122">Помимо страниц, предназначенных для клиентов, мы также создадим раздел администратора со списком альбомов, из которых администраторы могут создавать, изменять и удалять альбомы.</span><span class="sxs-lookup"><span data-stu-id="37783-122">In addition to customer-facing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="37783-123">1. файл-&gt; новый проект</span><span class="sxs-lookup"><span data-stu-id="37783-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="37783-124">Установка программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="37783-124">Installing the software</span></span>

<span data-ttu-id="37783-125">В этом руководстве мы начнем с создания нового проекта ASP.NET MVC 3 с помощью бесплатного выпуска Visual Web Developer 2010 Express (бесплатное), а затем постепенно добавим компоненты для создания полноценного приложения.</span><span class="sxs-lookup"><span data-stu-id="37783-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="37783-126">Кроме того, мы будем охватывать доступ к базам данных, сценарии разнесения форм, проверку данных, использование главных страниц для согласованного макета страниц, использование AJAX для обновления страниц и проверки, входа пользователей и т. д.</span><span class="sxs-lookup"><span data-stu-id="37783-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="37783-127">Вы можете следовать пошаговым инструкциям или скачать готовое приложение из [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="37783-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="37783-128">Для создания приложения можно использовать Visual Studio 2010 с пакетом обновления 1 (SP1) или Visual Web Developer 2010 Express с пакетом обновления 1 (SP1) (бесплатная версия Visual Studio 2010).</span><span class="sxs-lookup"><span data-stu-id="37783-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="37783-129">Мы будем использовать SQL Server Compact (также бесплатный) для размещения базы данных.</span><span class="sxs-lookup"><span data-stu-id="37783-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="37783-130">Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="37783-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="37783-131">[Предварительные требования для Visual Studio Web Developer Express SP1]</span><span class="sxs-lookup"><span data-stu-id="37783-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="37783-132">[ASP.NET MVC 3 Tools Update]</span><span class="sxs-lookup"><span data-stu-id="37783-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="37783-133">[SQL Server Compact 4,0] — включая поддержку среды выполнения и средств</span><span class="sxs-lookup"><span data-stu-id="37783-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>

### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="37783-134">Создание нового проекта ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="37783-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="37783-135">Начнем с выбора пункта "создать проект" в меню "файл" в Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="37783-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="37783-136">Откроется диалоговое окно Новый проект.</span><span class="sxs-lookup"><span data-stu-id="37783-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="37783-137">Мы выберем группу веб C# -шаблонов Visual&gt; слева, а затем выбираете шаблон "веб-приложение ASP.NET MVC 3" в центральном столбце.</span><span class="sxs-lookup"><span data-stu-id="37783-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="37783-138">Присвойте проекту имя Мвкмусиксторе и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="37783-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="37783-139">При этом отобразится вторичное диалоговое окно, которое позволит нам внести в проект определенные параметры MVC.</span><span class="sxs-lookup"><span data-stu-id="37783-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="37783-140">Выберите следующее:</span><span class="sxs-lookup"><span data-stu-id="37783-140">Select the following:</span></span>

<span data-ttu-id="37783-141">Шаблон проекта — выберите пустой</span><span class="sxs-lookup"><span data-stu-id="37783-141">Project Template - select Empty</span></span>

<span data-ttu-id="37783-142">Просмотр подсистемы — выбор Razor</span><span class="sxs-lookup"><span data-stu-id="37783-142">View Engine - select Razor</span></span>

<span data-ttu-id="37783-143">Использовать семантическую разметку HTML5 — проверяется</span><span class="sxs-lookup"><span data-stu-id="37783-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="37783-144">Проверьте параметры, как показано ниже, а затем нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="37783-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="37783-145">Будет создан наш проект.</span><span class="sxs-lookup"><span data-stu-id="37783-145">This will create our project.</span></span> <span data-ttu-id="37783-146">Давайте взглянем на папки, добавленные в наше приложение в обозреватель решений с правой стороны.</span><span class="sxs-lookup"><span data-stu-id="37783-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="37783-147">Пустой шаблон MVC 3 не полностью пуст — он добавляет простую структуру папок:</span><span class="sxs-lookup"><span data-stu-id="37783-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="37783-148">ASP.NET MVC использует некоторые основные соглашения об именовании имен папок:</span><span class="sxs-lookup"><span data-stu-id="37783-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="37783-149">**Папка**</span><span class="sxs-lookup"><span data-stu-id="37783-149">**Folder**</span></span> | <span data-ttu-id="37783-150">**Назначение**</span><span class="sxs-lookup"><span data-stu-id="37783-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="37783-151">**/контроллерс**</span><span class="sxs-lookup"><span data-stu-id="37783-151">**/Controllers**</span></span> | <span data-ttu-id="37783-152">Контроллеры реагируют на входные данные из браузера, решают, что делать с ним и возвращают ответ пользователю.</span><span class="sxs-lookup"><span data-stu-id="37783-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="37783-153">**/Views**</span><span class="sxs-lookup"><span data-stu-id="37783-153">**/Views**</span></span> | <span data-ttu-id="37783-154">Представления содержат шаблоны пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="37783-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="37783-155">**/моделс**</span><span class="sxs-lookup"><span data-stu-id="37783-155">**/Models**</span></span> | <span data-ttu-id="37783-156">Модели хранят данные и манипулируют ими</span><span class="sxs-lookup"><span data-stu-id="37783-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="37783-157">**/контент**</span><span class="sxs-lookup"><span data-stu-id="37783-157">**/Content**</span></span> | <span data-ttu-id="37783-158">Эта папка содержит наши образы, CSS и любые другие статические материалы</span><span class="sxs-lookup"><span data-stu-id="37783-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="37783-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="37783-159">**/Scripts**</span></span> | <span data-ttu-id="37783-160">В этой папке содержатся файлы JavaScript</span><span class="sxs-lookup"><span data-stu-id="37783-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="37783-161">Эти папки включаются даже в пустое приложение MVC ASP.NET, поскольку платформа ASP.NET MVC по умолчанию использует подход "соглашение по конфигурации" и делает некоторые предположения по умолчанию на основе соглашений об именовании папок.</span><span class="sxs-lookup"><span data-stu-id="37783-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="37783-162">Например, контроллеры ищут представления в папке Views по умолчанию без явного указания этого значения в коде.</span><span class="sxs-lookup"><span data-stu-id="37783-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="37783-163">При использовании соглашений по умолчанию уменьшается объем кода, который необходимо написать, а также может облегчить другим разработчикам понимание проекта.</span><span class="sxs-lookup"><span data-stu-id="37783-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="37783-164">Мы объясним эти соглашения более подробно, как мы создаем наше приложение.</span><span class="sxs-lookup"><span data-stu-id="37783-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="37783-165">Дальше</span><span class="sxs-lookup"><span data-stu-id="37783-165">Next</span></span>](mvc-music-store-part-2.md)
