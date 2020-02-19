---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: Добавление модели | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленная версия этого учебника доступна здесь, в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще в исполнении и демонстрации...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457808"
---
# <a name="adding-a-model"></a><span data-ttu-id="8349a-104">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="8349a-104">Adding a Model</span></span>

<span data-ttu-id="8349a-105">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8349a-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="8349a-106">Обновленная версия этого учебника доступна [здесь](../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8349a-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="8349a-107">Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="8349a-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="8349a-108">В этом разделе вы добавите некоторые классы для управления фильмами в базе данных.</span><span class="sxs-lookup"><span data-stu-id="8349a-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="8349a-109">Эти классы будут &quot;моделью,&quot; частью приложения MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8349a-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="8349a-110">Вы будете использовать .NET Frameworkную технологию доступа к данным, известную как [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) , для определения и работы с этими классами модели.</span><span class="sxs-lookup"><span data-stu-id="8349a-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="8349a-111">Entity Framework (часто называемый EF) поддерживает парадигму разработки, именуемую *Code First*.</span><span class="sxs-lookup"><span data-stu-id="8349a-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="8349a-112">Code First позволяет создавать объекты модели, создавая простые классы.</span><span class="sxs-lookup"><span data-stu-id="8349a-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="8349a-113">(Они также называются классами POCO, от &quot;обычных объектов CLR.&quot;) Затем базу данных можно создать в режиме реального времени из классов, что позволяет выполнять очень четкий и быстрый рабочий процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="8349a-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="8349a-114">Добавление классов модели</span><span class="sxs-lookup"><span data-stu-id="8349a-114">Adding Model Classes</span></span>

<span data-ttu-id="8349a-115">В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="8349a-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="8349a-116">Введите имя *класса* &quot;&quot;фильмов.</span><span class="sxs-lookup"><span data-stu-id="8349a-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="8349a-117">Добавьте в класс `Movie` следующие пять свойств:</span><span class="sxs-lookup"><span data-stu-id="8349a-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="8349a-118">Мы будем использовать класс `Movie` для представления фильмов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="8349a-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="8349a-119">Каждый экземпляр объекта `Movie` будет соответствовать строке в таблице базы данных, а каждое свойство класса `Movie` будет сопоставляться со столбцом в таблице.</span><span class="sxs-lookup"><span data-stu-id="8349a-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="8349a-120">В том же файле добавьте следующий класс `MovieDBContext`:</span><span class="sxs-lookup"><span data-stu-id="8349a-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="8349a-121">Класс `MovieDBContext` представляет контекст базы данных Entity Framework Movie, который обрабатывает выборку, хранение и обновление экземпляров класса `Movie` в базе данных.</span><span class="sxs-lookup"><span data-stu-id="8349a-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="8349a-122">`MovieDBContext` является производным от базового класса `DbContext`, предоставляемого Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="8349a-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="8349a-123">Чтобы иметь возможность ссылаться на `DbContext` и `DbSet`, необходимо добавить в начало файла следующую инструкцию `using`:</span><span class="sxs-lookup"><span data-stu-id="8349a-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="8349a-124">Полный файл *Movie.CS* показан ниже.</span><span class="sxs-lookup"><span data-stu-id="8349a-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="8349a-125">(Несколько ненужных инструкций using были удалены.)</span><span class="sxs-lookup"><span data-stu-id="8349a-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="8349a-126">Создание строки подключения и работа с SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="8349a-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="8349a-127">Созданный класс `MovieDBContext` обрабатывает задачу подключения к базе данных и сопоставление объектов `Movie` с записями базы данных.</span><span class="sxs-lookup"><span data-stu-id="8349a-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="8349a-128">Одним из вопросов, которые вы можете спросить, является указание того, к какой базе данных будет подключаться.</span><span class="sxs-lookup"><span data-stu-id="8349a-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="8349a-129">Это можно сделать, добавив сведения о подключении в файл *Web. config* приложения.</span><span class="sxs-lookup"><span data-stu-id="8349a-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="8349a-130">Откройте корневой файл *Web. config* приложения.</span><span class="sxs-lookup"><span data-stu-id="8349a-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="8349a-131">(Не файл *Web. config* в папке *views* .) Откройте файл *Web. config* , выделенный красным цветом.</span><span class="sxs-lookup"><span data-stu-id="8349a-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="8349a-132">Добавьте следующую строку подключения в элемент `<connectionStrings>` в файле *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="8349a-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="8349a-133">В следующем примере показана часть файла *Web. config* с добавленной новой строкой подключения:</span><span class="sxs-lookup"><span data-stu-id="8349a-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="8349a-134">Небольшой объем кода и XML — это все, что необходимо для написания, чтобы представить и сохранить данные фильмов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="8349a-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="8349a-135">Далее предстоит создать новый класс `MoviesController`, который можно использовать для отображения данных фильмов и предоставления пользователям возможности создавать новые списки фильмов.</span><span class="sxs-lookup"><span data-stu-id="8349a-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8349a-136">[Назад](adding-a-view.md)
> [Вперед](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="8349a-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
