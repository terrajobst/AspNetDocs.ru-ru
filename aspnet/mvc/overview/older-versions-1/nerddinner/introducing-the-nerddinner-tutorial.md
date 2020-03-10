---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Знакомство с руководством по NerdDinner | Документация Майкрософт
author: shanselman
description: Лучшим способом изучения новой платформы является создание чего-то с ней. В этом руководстве описано, как создать небольшое, но полное приложение, использующее ASP.NE...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468936"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="b36ac-104">Общие сведения об учебнике по NerdDinner</span><span class="sxs-lookup"><span data-stu-id="b36ac-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="b36ac-105">по [Скотт Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="b36ac-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="b36ac-106">Скачать в формате PDF</span><span class="sxs-lookup"><span data-stu-id="b36ac-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="b36ac-107">Лучшим способом изучения новой платформы является создание чего-то с ней.</span><span class="sxs-lookup"><span data-stu-id="b36ac-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="b36ac-108">В этом руководстве описано, как создать небольшое, но полное приложение, использующее ASP.NET MVC 1, и некоторые основные понятия, лежащие в основе ИТ.</span><span class="sxs-lookup"><span data-stu-id="b36ac-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="b36ac-109">Если вы используете ASP.NET MVC 3, мы рекомендуем следовать руководствам по [Начало работы в MVC 3 или в приложении для](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [музыкального магазина MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="b36ac-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="b36ac-110">Руководство по NerdDinner</span><span class="sxs-lookup"><span data-stu-id="b36ac-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="b36ac-111">Лучшим способом изучения новой платформы является создание чего-то с ней.</span><span class="sxs-lookup"><span data-stu-id="b36ac-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="b36ac-112">В этом руководстве описано, как создать небольшое, но полное приложение, использующее ASP.NET MVC, и некоторые основные понятия, лежащие в основе ИТ.</span><span class="sxs-lookup"><span data-stu-id="b36ac-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="b36ac-113">Приложение, которое мы собираемся создавать, называется "NerdDinner".</span><span class="sxs-lookup"><span data-stu-id="b36ac-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="b36ac-114">NerdDinner предоставляет пользователям простой способ поиска и организации диннерс в Интернете:</span><span class="sxs-lookup"><span data-stu-id="b36ac-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="b36ac-115">NerdDinner позволяет зарегистрированным пользователям создавать, изменять и удалять диннерс.</span><span class="sxs-lookup"><span data-stu-id="b36ac-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="b36ac-116">Он обеспечивает согласованный набор проверок и бизнес-правил для приложения:</span><span class="sxs-lookup"><span data-stu-id="b36ac-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="b36ac-117">Посетители могут использовать карту на основе AJAX для поиска предстоящих диннерс рядом:</span><span class="sxs-lookup"><span data-stu-id="b36ac-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="b36ac-118">Щелкнув обед, вы перейдете на страницу сведений, где они могут получить дополнительные сведения о них:</span><span class="sxs-lookup"><span data-stu-id="b36ac-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="b36ac-119">Если вы заинтересованы в посещении компании Dinner, то можете войти на сайт или зарегистрироваться на нем:</span><span class="sxs-lookup"><span data-stu-id="b36ac-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="b36ac-120">Затем они могут щелкнуть ссылку RSVP на основе AJAX, чтобы посетить событие:</span><span class="sxs-lookup"><span data-stu-id="b36ac-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="b36ac-121">Реализация NerdDinner</span><span class="sxs-lookup"><span data-stu-id="b36ac-121">Implementing NerdDinner</span></span>

<span data-ttu-id="b36ac-122">Мы начнем наше приложение NerdDinner, используя команду "файл-&gt;новый проект" в Visual Studio, чтобы создать новый проект ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="b36ac-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="b36ac-123">Затем мы постепенно добавим функции и функции.</span><span class="sxs-lookup"><span data-stu-id="b36ac-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="b36ac-124">Как мы будем охватывать:</span><span class="sxs-lookup"><span data-stu-id="b36ac-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="b36ac-125">Создание нового проекта MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b36ac-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="b36ac-126">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="b36ac-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="b36ac-127">Создание модели с проверками бизнес-правил</span><span class="sxs-lookup"><span data-stu-id="b36ac-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="b36ac-128">Использование контроллеров и представлений для реализации пользовательского интерфейса листинга и подробностей</span><span class="sxs-lookup"><span data-stu-id="b36ac-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="b36ac-129">Как обеспечить поддержку записи формы для CRUD (создание, чтение, обновление, удаление) данных</span><span class="sxs-lookup"><span data-stu-id="b36ac-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="b36ac-130">Использование ViewData и реализация классов ViewModel</span><span class="sxs-lookup"><span data-stu-id="b36ac-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="b36ac-131">Повторное использование пользовательского интерфейса с помощью главных страниц и частичных элементов</span><span class="sxs-lookup"><span data-stu-id="b36ac-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="b36ac-132">Реализация эффективного разбиения данных на страницы</span><span class="sxs-lookup"><span data-stu-id="b36ac-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="b36ac-133">Защита приложений с помощью проверки подлинности и авторизации</span><span class="sxs-lookup"><span data-stu-id="b36ac-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="b36ac-134">Использование AJAX для доставки динамических обновлений</span><span class="sxs-lookup"><span data-stu-id="b36ac-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="b36ac-135">Использование AJAX для реализации сценариев сопоставления</span><span class="sxs-lookup"><span data-stu-id="b36ac-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="b36ac-136">Включение автоматического модульного тестирования</span><span class="sxs-lookup"><span data-stu-id="b36ac-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="b36ac-137">Вы можете создать собственную копию NerdDinner с нуля, выполнив каждый шаг, который мы пошаговым руководством в этой главе.</span><span class="sxs-lookup"><span data-stu-id="b36ac-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="b36ac-138">Вы также можете скачать готовую версию исходного кода здесь: [NerdDinner на GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span><span class="sxs-lookup"><span data-stu-id="b36ac-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="b36ac-139">Кроме того, можно также [загрузить бесплатную версию этого учебника в формате PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) , если вы хотите прочитать учебник в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="b36ac-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="b36ac-140">Для создания приложения можно использовать Visual Studio 2008 или бесплатный выпуск Visual Web Developer 2008 Express.</span><span class="sxs-lookup"><span data-stu-id="b36ac-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="b36ac-141">Для базы данных можно использовать либо SQL Server, либо бесплатную SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="b36ac-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="b36ac-142">Вы можете установить ASP.NET MVC, Visual Web Developer 2008 Express и SQL Server Express (все бесплатное) с помощью версии 2 [установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="b36ac-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="b36ac-143">Теперь приступим к работе...</span><span class="sxs-lookup"><span data-stu-id="b36ac-143">Now let's get started....</span></span>

<span data-ttu-id="b36ac-144">Теперь, когда мы узнали, что такое NerdDinner, давайте создадим закатайте рукава и напишем некоторый код.</span><span class="sxs-lookup"><span data-stu-id="b36ac-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="b36ac-145">Начнем с использования файла-&gt;нового проекта в Visual Studio, чтобы создать приложение NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="b36ac-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b36ac-146">Дальше</span><span class="sxs-lookup"><span data-stu-id="b36ac-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
