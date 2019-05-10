---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Введение в учебнике по NerdDinner | Документация Майкрософт
author: shanselman
description: — Это наилучший способ подробнее узнать это новая платформа для создания чего-то с ним. В этом учебнике описывается создание небольшой, но законченного приложения с помощью ASP.NE...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65122323"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="e44b9-104">Общие сведения об учебнике по NerdDinner</span><span class="sxs-lookup"><span data-stu-id="e44b9-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="e44b9-105">по [(Scott hanselman)](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="e44b9-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="e44b9-106">Загрузить PDF-файл</span><span class="sxs-lookup"><span data-stu-id="e44b9-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="e44b9-107">— Это наилучший способ подробнее узнать это новая платформа для создания чего-то с ним.</span><span class="sxs-lookup"><span data-stu-id="e44b9-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="e44b9-108">Этом руководстве описано, как создать небольшой, но завершить приложение с помощью ASP.NET MVC 1 и рассматриваются некоторые основные принципы его.</span><span class="sxs-lookup"><span data-stu-id="e44b9-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="e44b9-109">Если вы используете ASP.NET MVC 3, рекомендуется следовать [Приступая к работе с MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) учебники.</span><span class="sxs-lookup"><span data-stu-id="e44b9-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="e44b9-110">Учебнике по NerdDinner</span><span class="sxs-lookup"><span data-stu-id="e44b9-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="e44b9-111">— Это наилучший способ подробнее узнать это новая платформа для создания чего-то с ним.</span><span class="sxs-lookup"><span data-stu-id="e44b9-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="e44b9-112">Этом руководстве описано, как создать небольшой, но завершить приложение с помощью ASP.NET MVC и рассматриваются некоторые основные принципы его.</span><span class="sxs-lookup"><span data-stu-id="e44b9-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="e44b9-113">Приложение, которое мы собираемся строить называется «NerdDinner».</span><span class="sxs-lookup"><span data-stu-id="e44b9-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="e44b9-114">NerdDinner предоставляет простой способ для пользователей, для поиска и упорядочения ужинов через Интернет:</span><span class="sxs-lookup"><span data-stu-id="e44b9-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="e44b9-115">Зарегистрированные пользователи могут создавать, изменять и удалять ужинов NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="e44b9-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="e44b9-116">Он содержит согласованный набор проверки и бизнес-правила для приложения:</span><span class="sxs-lookup"><span data-stu-id="e44b9-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="e44b9-117">Посетители можно использовать карты на основе AJAX, поиск предстоящих ужинов, удерживаемая рядом с ними:</span><span class="sxs-lookup"><span data-stu-id="e44b9-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="e44b9-118">Компании dinner ведет на страницу подробностей, где они могут узнать больше об этом:</span><span class="sxs-lookup"><span data-stu-id="e44b9-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="e44b9-119">Если они интересуют посещение обед, они могут войти в систему или зарегистрируйтесь на сайте:</span><span class="sxs-lookup"><span data-stu-id="e44b9-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="e44b9-120">Они затем можно щелкнуть ссылку RSVP на основе AJAX, чтобы принять участие в конференции:</span><span class="sxs-lookup"><span data-stu-id="e44b9-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="e44b9-121">Реализация NerdDinner</span><span class="sxs-lookup"><span data-stu-id="e44b9-121">Implementing NerdDinner</span></span>

<span data-ttu-id="e44b9-122">Мы хотим начать наше приложение NerdDinner с помощью файла -&gt;команду Новый проект в Visual Studio, чтобы создать новый проект ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e44b9-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="e44b9-123">Мы будем затем постепенно добавлять функциональность и возможности.</span><span class="sxs-lookup"><span data-stu-id="e44b9-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="e44b9-124">Попутно мы обсудим:</span><span class="sxs-lookup"><span data-stu-id="e44b9-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="e44b9-125">Как создать новый проект ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e44b9-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="e44b9-126">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="e44b9-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="e44b9-127">Как создать модель с проверками бизнес-правил</span><span class="sxs-lookup"><span data-stu-id="e44b9-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="e44b9-128">Практическое использование контроллеров и представлений для реализации списка и сведений пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="e44b9-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="e44b9-129">Как обеспечить CRUD (Создание, чтение, обновление и удаление) запись поддержки форм данных</span><span class="sxs-lookup"><span data-stu-id="e44b9-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="e44b9-130">Использование ViewData и реализация классов ViewModel</span><span class="sxs-lookup"><span data-stu-id="e44b9-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="e44b9-131">Как повторно использовать пользовательский Интерфейс, с помощью главных страниц и частичных представлений</span><span class="sxs-lookup"><span data-stu-id="e44b9-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="e44b9-132">Как реализовать эффективный данных разбиение по страницам</span><span class="sxs-lookup"><span data-stu-id="e44b9-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="e44b9-133">Защита приложений с помощью проверки подлинности и авторизации</span><span class="sxs-lookup"><span data-stu-id="e44b9-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="e44b9-134">Использование AJAX для доставки динамических обновлений</span><span class="sxs-lookup"><span data-stu-id="e44b9-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="e44b9-135">Использование AJAX для реализации сценариев сопоставления</span><span class="sxs-lookup"><span data-stu-id="e44b9-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="e44b9-136">Как включить автоматическое тестирование модулей</span><span class="sxs-lookup"><span data-stu-id="e44b9-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="e44b9-137">Можно создать собственную копию NerdDinner с нуля, выполнив каждый шаг мы пошагового руководства в этой главе.</span><span class="sxs-lookup"><span data-stu-id="e44b9-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="e44b9-138">Кроме того можно скачать готовую версию исходного кода, здесь: [NerdDinner на сайте GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span><span class="sxs-lookup"><span data-stu-id="e44b9-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="e44b9-139">Можно также при необходимости также [Загрузите бесплатную версию PDF данного учебника](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) Если вы хотите прочитать руководство в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="e44b9-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="e44b9-140">Visual Studio 2008 или бесплатный Visual Web Developer 2008 Express можно использовать для построения приложения.</span><span class="sxs-lookup"><span data-stu-id="e44b9-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="e44b9-141">Для базы данных можно использовать SQL Server или бесплатная SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="e44b9-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="e44b9-142">Вы можете установить ASP.NET MVC, Visual Web Developer 2008 Express и SQL Server Express (бесплатно) с помощью версии 2 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="e44b9-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="e44b9-143">Теперь приступим к работе...</span><span class="sxs-lookup"><span data-stu-id="e44b9-143">Now let's get started....</span></span>

<span data-ttu-id="e44b9-144">Теперь, когда мы рассмотрели, что такое NerdDinner, давайте наших рукава и написать код.</span><span class="sxs-lookup"><span data-stu-id="e44b9-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="e44b9-145">Начнем с помощью файла -&gt;новый проект в Visual Studio, чтобы создать приложение NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="e44b9-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e44b9-146">Вперед</span><span class="sxs-lookup"><span data-stu-id="e44b9-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
