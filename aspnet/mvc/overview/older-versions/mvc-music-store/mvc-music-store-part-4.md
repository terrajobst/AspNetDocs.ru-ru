---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: Часть 4. модели и доступ к данным | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. В части 4 приводятся модели и доступ к данным.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451020"
---
# <a name="part-4-models-and-data-access"></a><span data-ttu-id="e5270-104">Часть 4. модели и доступ к данным</span><span class="sxs-lookup"><span data-stu-id="e5270-104">Part 4: Models and Data Access</span></span>

<span data-ttu-id="e5270-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="e5270-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="e5270-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="e5270-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="e5270-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="e5270-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="e5270-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e5270-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="e5270-109">В части 4 приводятся модели и доступ к данным.</span><span class="sxs-lookup"><span data-stu-id="e5270-109">Part 4 covers Models and Data Access.</span></span>

<span data-ttu-id="e5270-110">До сих пор мы только передаем "фиктивные данные" с наших контроллеров в наши шаблоны представления.</span><span class="sxs-lookup"><span data-stu-id="e5270-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="e5270-111">Теперь все готово к подключению реальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="e5270-112">В этом учебнике мы покажем, как использовать выпуск SQL Server Compact Edition (часто именуемый SQL CE) в качестве ядра СУБД.</span><span class="sxs-lookup"><span data-stu-id="e5270-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="e5270-113">SQL CE — это бесплатная встроенная база данных на основе файлов, которая не требует установки или настройки, что делает ее действительно удобной для локальной разработки.</span><span class="sxs-lookup"><span data-stu-id="e5270-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="e5270-114">Доступ к базе данных с помощью Entity Frameworkного кода — сначала</span><span class="sxs-lookup"><span data-stu-id="e5270-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="e5270-115">Мы будем использовать поддержку Entity Framework (EF), которая включена в проекты ASP.NET MVC 3 для запроса и обновления базы данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="e5270-116">EF — это гибкая функция API данных реляционного сопоставления объектов, позволяющая разработчикам запрашивать и обновлять данные, хранящиеся в базе данных, в объектно-ориентированном виде.</span><span class="sxs-lookup"><span data-stu-id="e5270-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="e5270-117">Entity Framework версии 4 поддерживает парадигму разработки, именуемую Code-First.</span><span class="sxs-lookup"><span data-stu-id="e5270-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="e5270-118">Code-First позволяет создавать объекты модели путем написания простых классов (также известных как POCO из «обычных» объектов CLR) и даже создавать базу данных на лету из классов.</span><span class="sxs-lookup"><span data-stu-id="e5270-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="e5270-119">Изменения в наших классах модели</span><span class="sxs-lookup"><span data-stu-id="e5270-119">Changes to our Model Classes</span></span>

<span data-ttu-id="e5270-120">В Entity Framework в этом руководстве мы будем использовать функцию создания базы данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="e5270-121">Тем не менее, прежде чем делать это, давайте сделаем несколько незначительных изменений наших классов модели, чтобы добавить некоторые вещи, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="e5270-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="e5270-122">Добавление классов модели исполнителя</span><span class="sxs-lookup"><span data-stu-id="e5270-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="e5270-123">Наши альбомы будут связаны с исполнителями, поэтому мы добавим простой класс модели для описания исполнителя.</span><span class="sxs-lookup"><span data-stu-id="e5270-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="e5270-124">Добавьте новый класс в папку Models с именем Artist.cs, используя приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="e5270-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="e5270-125">Обновление наших классов модели</span><span class="sxs-lookup"><span data-stu-id="e5270-125">Updating our Model Classes</span></span>

<span data-ttu-id="e5270-126">Обновите класс альбома, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e5270-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="e5270-127">Затем внесите следующие изменения в класс жанра.</span><span class="sxs-lookup"><span data-stu-id="e5270-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a><span data-ttu-id="e5270-128">Добавление папки данных приложения\_</span><span class="sxs-lookup"><span data-stu-id="e5270-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="e5270-129">Мы добавим каталог данных приложения\_в наш проект для хранения файлов базы данных SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="e5270-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="e5270-130">Данные\_приложений — это специальный каталог в ASP.NET, который уже имеет правильные разрешения безопасности доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="e5270-131">В меню Проект выберите пункт Добавить папку ASP.NET, а затем —\_данные приложения.</span><span class="sxs-lookup"><span data-stu-id="e5270-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="e5270-132">Создание строки подключения в файле Web. config</span><span class="sxs-lookup"><span data-stu-id="e5270-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="e5270-133">Мы добавим несколько строк в файл конфигурации веб-сайта, чтобы Entity Framework знать, как подключиться к нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="e5270-134">Дважды щелкните файл Web. config, расположенный в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="e5270-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="e5270-135">Прокрутите файл до конца и добавьте &lt;connectionString&gt; раздел непосредственно над последней строкой, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e5270-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="e5270-136">Добавление класса контекста</span><span class="sxs-lookup"><span data-stu-id="e5270-136">Adding a Context Class</span></span>

<span data-ttu-id="e5270-137">Щелкните правой кнопкой мыши папку Models и добавьте новый класс с именем MusicStoreEntities.cs.</span><span class="sxs-lookup"><span data-stu-id="e5270-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="e5270-138">Этот класс будет представлять контекст базы данных Entity Framework и будет выполнять операции создания, чтения, обновления и удаления для нас.</span><span class="sxs-lookup"><span data-stu-id="e5270-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="e5270-139">Код для этого класса показан ниже.</span><span class="sxs-lookup"><span data-stu-id="e5270-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="e5270-140">Вот и другие настройки, специальные интерфейсы и т. д. Благодаря расширению базового класса DbContext наш класс Мусиксторинтитиес способен справиться с нашими операциями с базой данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="e5270-141">Теперь, когда у нас есть подключение, давайте добавим еще несколько свойств в наши классы модели, чтобы воспользоваться преимуществами некоторых дополнительных сведений в нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="e5270-142">Добавление данных каталога магазинов</span><span class="sxs-lookup"><span data-stu-id="e5270-142">Adding our store catalog data</span></span>

<span data-ttu-id="e5270-143">Мы будем использовать функцию в Entity Framework, которая добавляет "начальные" данные во вновь созданную базу данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="e5270-144">В нашем каталоге магазина будет заполняться список жанров, исполнителей и альбомов.</span><span class="sxs-lookup"><span data-stu-id="e5270-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="e5270-145">Загрузка Мвкмусиксторе-Ассетс. zip, которая включала в себя файлы разработки сайта, использовавшиеся ранее в этом руководстве, содержит файл класса с этими начальными данными, расположенный в папке с именем Code.</span><span class="sxs-lookup"><span data-stu-id="e5270-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="e5270-146">В папке Code/Models выберите файл SampleData.cs и поместите его в папку Models в нашем проекте, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e5270-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="e5270-147">Теперь нужно добавить одну строку кода, чтобы сообщить Entity Framework об этом классе SampleData.</span><span class="sxs-lookup"><span data-stu-id="e5270-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="e5270-148">Дважды щелкните файл Global. asax в корневом каталоге проекта, чтобы открыть его, и добавьте следующую строку в начало приложения\_запуск.</span><span class="sxs-lookup"><span data-stu-id="e5270-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="e5270-149">На этом этапе мы завершили работу, необходимую для настройки Entity Framework для нашего проекта.</span><span class="sxs-lookup"><span data-stu-id="e5270-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="e5270-150">Запрос к базе данных</span><span class="sxs-lookup"><span data-stu-id="e5270-150">Querying the Database</span></span>

<span data-ttu-id="e5270-151">Теперь давайте изменим наш Стореконтроллер, чтобы вместо использования "фиктивных данных" вместо этого он обращается к нашей базе данных для запроса всей информации.</span><span class="sxs-lookup"><span data-stu-id="e5270-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="e5270-152">Начнем с объявления поля в **стореконтроллер** для хранения экземпляра класса мусиксторинтитиес с именем сторедб:</span><span class="sxs-lookup"><span data-stu-id="e5270-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="e5270-153">Обновление индекса хранилища для запроса базы данных</span><span class="sxs-lookup"><span data-stu-id="e5270-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="e5270-154">Класс Мусиксторинтитиес поддерживается Entity Framework и предоставляет свойство коллекции для каждой таблицы в нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="e5270-155">Давайте изменим действие индекса Стореконтроллер, чтобы получить все жанры в нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="e5270-156">Ранее мы сделали это с помощью жестко запрограммированных строковых данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="e5270-157">Теперь можно просто использовать Entity Frameworkную коллекцию Женерес Context:</span><span class="sxs-lookup"><span data-stu-id="e5270-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="e5270-158">В наш шаблон представления не нужно вносить никаких изменений, так как мы по-прежнему возвращаем те же Стореиндексвиевмодел, которые мы возвращали до-мы просто возвращаем данные из нашей базы данных прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="e5270-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="e5270-159">После повторного запуска проекта и перехода по URL-адресу «/Store» будет выведен список всех жанров в нашей базе данных:</span><span class="sxs-lookup"><span data-stu-id="e5270-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="e5270-160">Обновление обзора и сведений о магазине для использования динамических данных</span><span class="sxs-lookup"><span data-stu-id="e5270-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="e5270-161">При использовании метода действия/Сторе/бровсе? жанр = *[some-жанр]* выполняется поиск жанра по имени.</span><span class="sxs-lookup"><span data-stu-id="e5270-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="e5270-162">Мы предполагаем только один результат, так как у нас никогда не будет двух записей с одинаковым названием жанра, и поэтому мы можем использовать. Single () в LINQ для запроса соответствующего объекта жанра (это еще не вводите):</span><span class="sxs-lookup"><span data-stu-id="e5270-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="e5270-163">Один метод принимает лямбда-выражение в качестве параметра, которое указывает, что нам нужен один объект жанра, который соответствует заданному значению.</span><span class="sxs-lookup"><span data-stu-id="e5270-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="e5270-164">В приведенном выше примере мы загружаем один объект жанра со значением Name, соответствующим Disco.</span><span class="sxs-lookup"><span data-stu-id="e5270-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="e5270-165">Мы будем использовать функцию Entity Framework, которая позволяет указать другие связанные сущности, которые нужно загрузить, а также при извлечении объекта жанра.</span><span class="sxs-lookup"><span data-stu-id="e5270-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="e5270-166">Эта функция называется формированием результатов запроса и позволяет сократить количество обращений к базе данных, чтобы получить всю необходимую информацию.</span><span class="sxs-lookup"><span data-stu-id="e5270-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="e5270-167">Мы хотим предварительно получить Альбомы для жанра, который мы получаем, поэтому мы будем обновлять наш запрос для включения в жанры. Включите ("альбомы"), чтобы указать, что нам нужны связанные альбомы.</span><span class="sxs-lookup"><span data-stu-id="e5270-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="e5270-168">Это более эффективно, так как в одном запросе к базе данных будут извлекаться данные о жанре и альбоме.</span><span class="sxs-lookup"><span data-stu-id="e5270-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="e5270-169">Выполнив объяснения, мы рассмотрим, как выглядит обновленное действие контроллера Browse:</span><span class="sxs-lookup"><span data-stu-id="e5270-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="e5270-170">Теперь можно обновить представление обзора хранилища, чтобы отобразить альбомы, доступные в каждом жанре.</span><span class="sxs-lookup"><span data-stu-id="e5270-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="e5270-171">Откройте шаблон представления (находится в/Виевс/Сторе/бровсе.кштмл) и добавьте маркированный список альбомов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e5270-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="e5270-172">Запустив наше приложение и перейдя к/Сторе/бровсе? Жанр = Джаз, вы увидите, что наши результаты теперь извлекаются из базы данных, отображая все альбомы в нашем выбранном жанре.</span><span class="sxs-lookup"><span data-stu-id="e5270-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="e5270-173">Мы изменим те же изменения в нашем URL-адресе/Сторе/детаилс/[ID] и заменяем фиктивные данные запросом к базе данных, который загружает альбом, идентификатор которого соответствует значению параметра.</span><span class="sxs-lookup"><span data-stu-id="e5270-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="e5270-174">Запуск нашего приложения и просмотр в/Store/Details/1 показывает, что наши результаты теперь извлекаются из базы данных.</span><span class="sxs-lookup"><span data-stu-id="e5270-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="e5270-175">Теперь, когда страница сведений о магазине настроена на отображение альбома по ИДЕНТИФИКАТОРу альбома, обновите представление " **Обзор** ", чтобы связать с представлением сведений.</span><span class="sxs-lookup"><span data-stu-id="e5270-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="e5270-176">Мы будем использовать HTML. ActionLink, точно так же, как мы содержали ссылку из индекса магазина, чтобы сохранить обзор в конце предыдущего раздела.</span><span class="sxs-lookup"><span data-stu-id="e5270-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="e5270-177">Полный исходный код для представления "Обзор" показан ниже.</span><span class="sxs-lookup"><span data-stu-id="e5270-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="e5270-178">Теперь можно перейти со страницы Store на страницу жанра, в которой перечислены доступные альбомы, а также щелкнуть альбом, чтобы просмотреть сведения об этом альбоме.</span><span class="sxs-lookup"><span data-stu-id="e5270-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="e5270-179">[Назад](mvc-music-store-part-3.md)
> [Вперед](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="e5270-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
