---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: Добавление модели (C#) | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленная версия этого учебника доступна здесь, в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще в исполнении и демонстрации...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a5f494eaa05bcfcd9d49873db728d71c1fd332c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434898"
---
# <a name="adding-a-model-c"></a><span data-ttu-id="0880e-104">Добавление модели (C#)</span><span class="sxs-lookup"><span data-stu-id="0880e-104">Adding a Model (C#)</span></span>

<span data-ttu-id="0880e-105">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0880e-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="0880e-106">В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0880e-106">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="0880e-107">Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="0880e-107">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="0880e-108">Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="0880e-108">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="0880e-109">Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:</span><span class="sxs-lookup"><span data-stu-id="0880e-109">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="0880e-110">Предварительные требования для Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="0880e-110">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="0880e-111">Обновление инструментов ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="0880e-111">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="0880e-112">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)</span><span class="sxs-lookup"><span data-stu-id="0880e-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="0880e-113">Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="0880e-113">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="0880e-114">Для этого раздела доступен проект Visual C# Web Developer с исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="0880e-114">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="0880e-115">[Скачайте C# версию](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="0880e-115">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="0880e-116">Если вы предпочитаете Visual Basic, переключитесь на [Visual Basic версию](../vb/adding-a-model.md) этого учебника.</span><span class="sxs-lookup"><span data-stu-id="0880e-116">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="0880e-117">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="0880e-117">Adding a Model</span></span>

<span data-ttu-id="0880e-118">В этом разделе вы добавите некоторые классы для управления фильмами в базе данных.</span><span class="sxs-lookup"><span data-stu-id="0880e-118">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="0880e-119">Эти классы будут частью "Model" приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0880e-119">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="0880e-120">Вы будете использовать .NET Frameworkную технологию доступа к данным, известную как Entity Framework, для определения и работы с этими классами модели.</span><span class="sxs-lookup"><span data-stu-id="0880e-120">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="0880e-121">Entity Framework (часто называемый EF) поддерживает парадигму разработки, именуемую *Code First*.</span><span class="sxs-lookup"><span data-stu-id="0880e-121">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="0880e-122">Code First позволяет создавать объекты модели, создавая простые классы.</span><span class="sxs-lookup"><span data-stu-id="0880e-122">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="0880e-123">(Они также известны как классы POCO, от "обычных объектов CLR".) Затем базу данных можно создать в режиме реального времени из классов, что позволяет выполнять очень четкий и быстрый рабочий процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="0880e-123">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="0880e-124">Добавление классов модели</span><span class="sxs-lookup"><span data-stu-id="0880e-124">Adding Model Classes</span></span>

<span data-ttu-id="0880e-125">В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="0880e-125">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="0880e-126">Присвойте *классу* имя Movie.</span><span class="sxs-lookup"><span data-stu-id="0880e-126">Name the *class* "Movie".</span></span>

<span data-ttu-id="0880e-127">[![Креатемовиекласс](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="0880e-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span></span>

<span data-ttu-id="0880e-128">Добавьте в класс `Movie` следующие пять свойств:</span><span class="sxs-lookup"><span data-stu-id="0880e-128">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="0880e-129">Мы будем использовать класс `Movie` для представления фильмов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="0880e-129">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="0880e-130">Каждый экземпляр объекта `Movie` будет соответствовать строке в таблице базы данных, а каждое свойство класса `Movie` будет сопоставляться со столбцом в таблице.</span><span class="sxs-lookup"><span data-stu-id="0880e-130">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="0880e-131">В том же файле добавьте следующий класс `MovieDBContext`:</span><span class="sxs-lookup"><span data-stu-id="0880e-131">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="0880e-132">Класс `MovieDBContext` представляет контекст базы данных Entity Framework Movie, который обрабатывает выборку, хранение и обновление экземпляров класса `Movie` в базе данных.</span><span class="sxs-lookup"><span data-stu-id="0880e-132">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="0880e-133">`MovieDBContext` является производным от базового класса `DbContext`, предоставляемого Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="0880e-133">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="0880e-134">Дополнительные сведения о `DbContext` и `DbSet`см. [в статье улучшения производительности для Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="0880e-134">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="0880e-135">Чтобы иметь возможность ссылаться на `DbContext` и `DbSet`, необходимо добавить в начало файла следующую инструкцию `using`:</span><span class="sxs-lookup"><span data-stu-id="0880e-135">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="0880e-136">Полный файл *Movie.CS* показан ниже.</span><span class="sxs-lookup"><span data-stu-id="0880e-136">The complete *Movie.cs* file is shown below.</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="0880e-137">Создание строки подключения и работа с SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="0880e-137">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="0880e-138">Созданный класс `MovieDBContext` обрабатывает задачу подключения к базе данных и сопоставление объектов `Movie` с записями базы данных.</span><span class="sxs-lookup"><span data-stu-id="0880e-138">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="0880e-139">Одним из вопросов, которые вы можете спросить, является указание того, к какой базе данных будет подключаться.</span><span class="sxs-lookup"><span data-stu-id="0880e-139">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="0880e-140">Это можно сделать, добавив сведения о подключении в файл *Web. config* приложения.</span><span class="sxs-lookup"><span data-stu-id="0880e-140">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="0880e-141">Откройте корневой файл *Web. config* приложения.</span><span class="sxs-lookup"><span data-stu-id="0880e-141">Open the application root *Web.config* file.</span></span> <span data-ttu-id="0880e-142">(Не файл *Web. config* в папке *views* .) На рисунке ниже показаны оба файла *Web. config* . Откройте файл *Web. config* , обозначенный красным цветом.</span><span class="sxs-lookup"><span data-stu-id="0880e-142">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image4.png)

<span data-ttu-id="0880e-143">Добавьте следующую строку подключения в элемент `<connectionStrings>` в файле *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="0880e-143">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="0880e-144">В следующем примере показана часть файла *Web. config* с добавленной новой строкой подключения:</span><span class="sxs-lookup"><span data-stu-id="0880e-144">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="0880e-145">Небольшой объем кода и XML — это все, что необходимо для написания, чтобы представить и сохранить данные фильмов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="0880e-145">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="0880e-146">Далее предстоит создать новый класс `MoviesController`, который можно использовать для отображения данных фильмов и предоставления пользователям возможности создавать новые списки фильмов.</span><span class="sxs-lookup"><span data-stu-id="0880e-146">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0880e-147">[Назад](adding-a-view.md)
> [Вперед](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="0880e-147">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
