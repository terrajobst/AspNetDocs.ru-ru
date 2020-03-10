---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: Часть 1. Файл-> новый проект | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. Часть 1 охватывает общие сведения и файл/новый проект.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516540"
---
# <a name="part-1-file--new-project"></a><span data-ttu-id="c1c10-104">Часть 1. Файл-> новый проект</span><span class="sxs-lookup"><span data-stu-id="c1c10-104">Part 1: File-> New Project</span></span>

<span data-ttu-id="c1c10-105">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="c1c10-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="c1c10-106">В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET.</span><span class="sxs-lookup"><span data-stu-id="c1c10-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="c1c10-107">Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.</span><span class="sxs-lookup"><span data-stu-id="c1c10-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="c1c10-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="c1c10-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="c1c10-109">Часть 1 охватывает общие сведения и файл/новый проект.</span><span class="sxs-lookup"><span data-stu-id="c1c10-109">Part 1 covers Overview and File/New Project.</span></span>

## <a id="_Toc260221666"></a><span data-ttu-id="c1c10-110">Средств</span><span class="sxs-lookup"><span data-stu-id="c1c10-110">Overview</span></span>

<span data-ttu-id="c1c10-111">Это руководство представляет собой введение в ASP.NET WebForms.</span><span class="sxs-lookup"><span data-stu-id="c1c10-111">This tutorial is an introduction to ASP.NET WebForms.</span></span> <span data-ttu-id="c1c10-112">Мы будем замедленнее, так что веб-разработка на уровне "новичок" работает.</span><span class="sxs-lookup"><span data-stu-id="c1c10-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="c1c10-113">Приложение, которое мы будем создавать, — это простое интерактивное хранилище.</span><span class="sxs-lookup"><span data-stu-id="c1c10-113">The application we'll be building is a simple on-line store.</span></span>

![](tailspin-spyworks-part-1/_static/image1.jpg)

<span data-ttu-id="c1c10-114">Посетители могут просматривать продукты по категориям:</span><span class="sxs-lookup"><span data-stu-id="c1c10-114">Visitors can browse Products by Category:</span></span>

![](tailspin-spyworks-part-1/_static/image2.jpg)

<span data-ttu-id="c1c10-115">Они могут просматривать один продукт и добавлять его в корзину:</span><span class="sxs-lookup"><span data-stu-id="c1c10-115">They can view a single product and add it to their cart:</span></span>

![](tailspin-spyworks-part-1/_static/image3.jpg)

<span data-ttu-id="c1c10-116">Они могут просматривать свою корзину, удаляя все ненужные элементы:</span><span class="sxs-lookup"><span data-stu-id="c1c10-116">They can review their cart, removing any items they no longer want:</span></span>

![](tailspin-spyworks-part-1/_static/image4.jpg)

<span data-ttu-id="c1c10-117">При переходе к извлечению будут предложены</span><span class="sxs-lookup"><span data-stu-id="c1c10-117">Proceeding to Checkout will prompt them to</span></span>

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

<span data-ttu-id="c1c10-118">После упорядочения они видят простой экран подтверждения:</span><span class="sxs-lookup"><span data-stu-id="c1c10-118">After ordering, they see a simple confirmation screen:</span></span>

![](tailspin-spyworks-part-1/_static/image7.jpg)

<span data-ttu-id="c1c10-119">Начнем с создания нового проекта ASP.NET WebForms в Visual Studio 2010, и мы постепенно добавим компоненты для создания полноценного приложения.</span><span class="sxs-lookup"><span data-stu-id="c1c10-119">We'll begin by creating a new ASP.NET WebForms project in Visual Studio 2010, and we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="c1c10-120">Кроме того, мы будем охватывать доступ к базам данных, представления списков и таблиц, страницы обновления данных, проверку данных, использование главных страниц для согласованного макета страницы, AJAX, проверки, членства пользователей и т. д.</span><span class="sxs-lookup"><span data-stu-id="c1c10-120">Along the way, we'll cover database access, list and grid views, data update pages, data validation, using master pages for consistent page layout, AJAX, validation, user membership, and more.</span></span>

<span data-ttu-id="c1c10-121">Вы можете выполнить пошаговую процедуру или скачать готовое приложение из [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="c1c10-121">You can follow along step by step, or you can download the completed application from [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span></span>

<span data-ttu-id="c1c10-122">Вы можете использовать Visual Studio 2010 или бесплатный Visual Web Developer 2010 от [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span><span class="sxs-lookup"><span data-stu-id="c1c10-122">You can use either Visual Studio 2010 or the free Visual Web Developer 2010 from [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="c1c10-123">Для сборки приложения можно использовать либо SQL Server, либо бесплатную SQL Server Express для размещения базы данных.</span><span class="sxs-lookup"><span data-stu-id="c1c10-123">To build the application, you can use either SQL Server or the free SQL Server Express to host the database.</span></span>

## <a id="_Toc260221667"></a><span data-ttu-id="c1c10-124">Файл или новый проект</span><span class="sxs-lookup"><span data-stu-id="c1c10-124">File / New Project</span></span>

<span data-ttu-id="c1c10-125">Начнем с выбора нового проекта в меню файл в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1c10-125">We'll start by selecting the New Project from the File menu in Visual Studio.</span></span> <span data-ttu-id="c1c10-126">Откроется диалоговое окно Новый проект.</span><span class="sxs-lookup"><span data-stu-id="c1c10-126">This brings up the New Project dialog.</span></span>

![](tailspin-spyworks-part-1/_static/image8.jpg)

<span data-ttu-id="c1c10-127">В левой части экрана будет C# выбрана группа визуальных и веб-шаблонов, а затем в центральном столбце выбрать шаблон "веб-приложение ASP.NET".</span><span class="sxs-lookup"><span data-stu-id="c1c10-127">We'll select the Visual C# / Web Templates group on the left, and then choose the "ASP.NET Web Application" template in the center column.</span></span> <span data-ttu-id="c1c10-128">Присвойте проекту имя Таилспинспиворкс и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="c1c10-128">Name your project TailspinSpyworks and press the OK button.</span></span>

![](tailspin-spyworks-part-1/_static/image9.jpg)

<span data-ttu-id="c1c10-129">Будет создан наш проект.</span><span class="sxs-lookup"><span data-stu-id="c1c10-129">This will create our project.</span></span> <span data-ttu-id="c1c10-130">Давайте взглянем на папки, включенные в наше приложение в обозреватель решений с правой стороны.</span><span class="sxs-lookup"><span data-stu-id="c1c10-130">Let's take a look at the folders that are included in our application in the Solution Explorer on the right side.</span></span>

![](tailspin-spyworks-part-1/_static/image10.jpg)

<span data-ttu-id="c1c10-131">Пустое решение не полностью пусто — оно добавляет простую структуру папок:</span><span class="sxs-lookup"><span data-stu-id="c1c10-131">The Empty Solution isn't completely empty – it adds a basic folder structure:</span></span>

![](tailspin-spyworks-part-1/_static/image1.png)

<span data-ttu-id="c1c10-132">Обратите внимание на соглашения, реализуемые шаблоном проекта ASP.NET 4 по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c1c10-132">Note the conventions implemented by the ASP.NET 4 default project template.</span></span>

- <span data-ttu-id="c1c10-133">В папке Account реализуется базовый пользовательский интерфейс для ASP. Подсистема членства NET.</span><span class="sxs-lookup"><span data-stu-id="c1c10-133">The "Account" folder implements a basic user interface for ASP.NET's membership subsystem.</span></span>
- <span data-ttu-id="c1c10-134">Папка Scripts выступает в качестве репозитория для файлов JavaScript на стороне клиента, а основные файлы jQuery. js становятся доступными по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c1c10-134">The "Scripts" folder serves as the repository for client side JavaScript files and the core jQuery .js files are made available by default.</span></span>
- <span data-ttu-id="c1c10-135">Папка "стили" используется для Организации визуальных элементов веб-сайта (таблиц стилей CSS).</span><span class="sxs-lookup"><span data-stu-id="c1c10-135">The "Styles" folder is used to organize our web site visuals (CSS Style Sheets)</span></span>

<span data-ttu-id="c1c10-136">При нажатии клавиши F5 для запуска нашего приложения и визуализации страницы Default. aspx отображаются следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="c1c10-136">When we press F5 to run our application and render the default.aspx page we see the following.</span></span>

![](tailspin-spyworks-part-1/_static/image11.jpg)

<span data-ttu-id="c1c10-137">Первое улучшение приложения — заменить файл style. CSS из шаблона по умолчанию с помощью классов CSS и связанных файлов изображений, которые будут визуализировать визуальный ассетикс, который нам нужен для нашего приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="c1c10-137">Our first application enhancement will be to replace the Style.css file from the default WebForms template with the CSS classes and associated image files that will render the visual asthetics that we want for our Tailspin Spyworks application.</span></span>

<span data-ttu-id="c1c10-138">После этого страница Default. aspx визуализируется подобным образом.</span><span class="sxs-lookup"><span data-stu-id="c1c10-138">After doing so our default.aspx page renders like this.</span></span>

![](tailspin-spyworks-part-1/_static/image12.jpg)

<span data-ttu-id="c1c10-139">Обратите внимание на ссылки на изображение в правом верхнем углу страницы и на пункты меню, добавленные на главную страницу.</span><span class="sxs-lookup"><span data-stu-id="c1c10-139">Notice the image links at the top right of the page and the menu items that have been added to the master page.</span></span> <span data-ttu-id="c1c10-140">Только ссылки "вход" и "учетная запись" указывают на страницы, которые существуют (сформированы шаблоном по умолчанию), и остальные страницы, которые мы будем реализовывать по мере создания нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="c1c10-140">Only the "Sign In" and "Account" links point to pages that exist (generated by the default template) and the rest of the pages we will implement as we build our application.</span></span>

<span data-ttu-id="c1c10-141">Также мы перейдем главную страницу к каталогу Styles.</span><span class="sxs-lookup"><span data-stu-id="c1c10-141">We're also going to relocate the Master Page to the Styles directory.</span></span> <span data-ttu-id="c1c10-142">Хотя это и предпочтительно, это может быть немного проще, если мы решили сделать наше приложение «обложкой» в будущем.</span><span class="sxs-lookup"><span data-stu-id="c1c10-142">Though this is only a preference it may make things a little easier if we decide to make our application "skinable" in the future.</span></span>

<span data-ttu-id="c1c10-143">После этого необходимо будет изменить ссылки на главную страницу во всех ASPX-файлах, созданных страницами ASP.NET по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c1c10-143">After doing this we'll need to change the master page references in all the .aspx files generated by the default ASP.NET WebForms pages.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c1c10-144">Дальше</span><span class="sxs-lookup"><span data-stu-id="c1c10-144">Next</span></span>](tailspin-spyworks-part-2.md)
