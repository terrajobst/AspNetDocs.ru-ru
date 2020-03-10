---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: Добавление модели (VB) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1)...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e69d59aed4d74f08f1c653c4965b128c4dbe20ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434604"
---
# <a name="adding-a-model-vb"></a><span data-ttu-id="a1638-103">Добавление модели (VB)</span><span class="sxs-lookup"><span data-stu-id="a1638-103">Adding a Model (VB)</span></span>

<span data-ttu-id="a1638-104">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a1638-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="a1638-105">В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a1638-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="a1638-106">Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="a1638-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="a1638-107">Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="a1638-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="a1638-108">Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:</span><span class="sxs-lookup"><span data-stu-id="a1638-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="a1638-109">Предварительные требования для Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="a1638-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="a1638-110">Обновление инструментов ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="a1638-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="a1638-111">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)</span><span class="sxs-lookup"><span data-stu-id="a1638-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="a1638-112">Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="a1638-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="a1638-113">Для этого раздела доступен проект Visual Web Developer с исходным кодом VB.NET.</span><span class="sxs-lookup"><span data-stu-id="a1638-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="a1638-114">[Скачайте версию VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="a1638-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="a1638-115">При желании C#переключитесь на [ C# версию](../cs/adding-a-model.md) этого учебника.</span><span class="sxs-lookup"><span data-stu-id="a1638-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="a1638-116">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="a1638-116">Adding a Model</span></span>

<span data-ttu-id="a1638-117">В этом разделе вы добавите некоторые классы для управления фильмами в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a1638-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="a1638-118">Эти классы будут частью "Model" приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a1638-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="a1638-119">Вы будете использовать .NET Frameworkную технологию доступа к данным, известную как Entity Framework, для определения и работы с этими классами модели.</span><span class="sxs-lookup"><span data-stu-id="a1638-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="a1638-120">Entity Framework (часто называемый EF) поддерживает парадигму разработки, именуемую *Code First*.</span><span class="sxs-lookup"><span data-stu-id="a1638-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="a1638-121">Code First позволяет создавать объекты модели, создавая простые классы.</span><span class="sxs-lookup"><span data-stu-id="a1638-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="a1638-122">(Они также известны как классы POCO, от "обычных объектов CLR".) Затем базу данных можно создать в режиме реального времени из классов, что позволяет выполнять очень четкий и быстрый рабочий процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="a1638-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="a1638-123">Добавление классов модели</span><span class="sxs-lookup"><span data-stu-id="a1638-123">Adding Model Classes</span></span>

<span data-ttu-id="a1638-124">В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="a1638-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="a1638-125">Присвойте классу имя Movie.</span><span class="sxs-lookup"><span data-stu-id="a1638-125">Name the class "Movie".</span></span>

<span data-ttu-id="a1638-126">Добавьте в класс `Movie` следующие пять свойств:</span><span class="sxs-lookup"><span data-stu-id="a1638-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="a1638-127">Мы будем использовать класс `Movie` для представления фильмов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a1638-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="a1638-128">Каждый экземпляр объекта `Movie` будет соответствовать строке в таблице базы данных, а каждое свойство класса `Movie` будет сопоставляться со столбцом в таблице.</span><span class="sxs-lookup"><span data-stu-id="a1638-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="a1638-129">В том же файле добавьте следующий класс `MovieDBContext`:</span><span class="sxs-lookup"><span data-stu-id="a1638-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="a1638-130">Класс `MovieDBContext` представляет контекст базы данных Entity Framework Movie, который обрабатывает выборку, хранение и обновление экземпляров класса `Movie` в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a1638-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="a1638-131">`MovieDBContext` является производным от базового класса `DbContext`, предоставляемого Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="a1638-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="a1638-132">Дополнительные сведения о `DbContext` и `DbSet`см. [в статье улучшения производительности для Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="a1638-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="a1638-133">Чтобы иметь возможность ссылаться на `DbContext` и `DbSet`, необходимо добавить в начало файла следующую инструкцию `imports`:</span><span class="sxs-lookup"><span data-stu-id="a1638-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="a1638-134">Полный файл *Movie. vb* показан ниже.</span><span class="sxs-lookup"><span data-stu-id="a1638-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="a1638-135">Создание строки подключения и работа с SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="a1638-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="a1638-136">Созданный класс `MovieDBContext` обрабатывает задачу подключения к базе данных и сопоставление объектов `Movie` с записями базы данных.</span><span class="sxs-lookup"><span data-stu-id="a1638-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="a1638-137">Одним из вопросов, которые вы можете спросить, является указание того, к какой базе данных будет подключаться.</span><span class="sxs-lookup"><span data-stu-id="a1638-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="a1638-138">Это можно сделать, добавив сведения о подключении в файл *Web. config* приложения.</span><span class="sxs-lookup"><span data-stu-id="a1638-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="a1638-139">Откройте корневой файл *Web. config* приложения.</span><span class="sxs-lookup"><span data-stu-id="a1638-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="a1638-140">(Не файл *Web. config* в папке *views* .) На рисунке ниже показаны оба файла *Web. config* . Откройте файл *Web. config* , обозначенный красным цветом.</span><span class="sxs-lookup"><span data-stu-id="a1638-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="a1638-141">Добавьте следующую строку подключения в элемент `<connectionStrings>` в файле *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="a1638-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="a1638-142">В следующем примере показана часть файла *Web. config* с добавленной новой строкой подключения:</span><span class="sxs-lookup"><span data-stu-id="a1638-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="a1638-143">Небольшой объем кода и XML — это все, что необходимо для написания, чтобы представить и сохранить данные фильмов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a1638-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="a1638-144">Далее предстоит создать новый класс `MoviesController`, который можно использовать для отображения данных фильмов и предоставления пользователям возможности создавать новые списки фильмов.</span><span class="sxs-lookup"><span data-stu-id="a1638-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1638-145">[Назад](adding-a-view.md)
> [Вперед](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="a1638-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
