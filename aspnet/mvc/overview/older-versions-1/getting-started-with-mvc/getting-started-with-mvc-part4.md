---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: Создание базы данных | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Создание простого веб-приложения, считывающего и записывающего данные из базы данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469674"
---
# <a name="creating-a-database"></a><span data-ttu-id="c69c2-104">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="c69c2-104">Creating a Database</span></span>

<span data-ttu-id="c69c2-105">по [Скотт Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="c69c2-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="c69c2-106">Это руководство для начинающих, в котором представлены основы ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c69c2-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="c69c2-107">Вы создадите простое веб-приложение, считывающее и записывающее данные из базы данных.</span><span class="sxs-lookup"><span data-stu-id="c69c2-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="c69c2-108">Посетите [центр обучения ASP.NET MVC](../../../index.md) , чтобы найти другие руководства и примеры для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c69c2-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="c69c2-109">В этом разделе мы создадим новую базу данных SQL Express, которая будет использоваться для хранения и извлечения данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="c69c2-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="c69c2-110">В интегрированной среде разработки Visual Web Developer выберите вид | обозреватель сервера.</span><span class="sxs-lookup"><span data-stu-id="c69c2-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="c69c2-111">Щелкните правой кнопкой мыши подключения к данным и выберите Добавить подключение...</span><span class="sxs-lookup"><span data-stu-id="c69c2-111">Right click on Data Connections and click Add Connection...</span></span>

![аддконнектион](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="c69c2-113">В диалоговом окне Выбор источника данных выберите Microsoft SQL Server и нажмите кнопку продолжить.</span><span class="sxs-lookup"><span data-stu-id="c69c2-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="c69c2-114">В диалоговом окне Добавление соединения введите ".\SQLEXPRESS" в качестве имени сервера и введите "Movies" в качестве имени новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="c69c2-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="c69c2-115">[диалоговое окно добавления соединения ![](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="c69c2-116">Нажмите кнопку ОК, и вам будет предложено создать эту базу данных.</span><span class="sxs-lookup"><span data-stu-id="c69c2-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="c69c2-117">Выберите Да.</span><span class="sxs-lookup"><span data-stu-id="c69c2-117">Select yes.</span></span>

<span data-ttu-id="c69c2-118">[![создавать фильмы?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="c69c2-119">Теперь у вас есть пустая база данных в обозреватель сервера.</span><span class="sxs-lookup"><span data-stu-id="c69c2-119">Now you've got an empty database in Server Explorer.</span></span>

![Добавить новую таблицу](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="c69c2-121">Щелкните правой кнопкой мыши таблицы и выберите команду Добавить таблицу.</span><span class="sxs-lookup"><span data-stu-id="c69c2-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="c69c2-122">Появится конструктор таблиц.</span><span class="sxs-lookup"><span data-stu-id="c69c2-122">The Table Designer will appear.</span></span> <span data-ttu-id="c69c2-123">Добавьте столбцы для ID, Title, ReleaseDate, жанра и цены.</span><span class="sxs-lookup"><span data-stu-id="c69c2-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="c69c2-124">Щелкните правой кнопкой мыши столбец идентификатор и выберите пункт Задать первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="c69c2-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="c69c2-125">Вот как выглядят мои области разработки.</span><span class="sxs-lookup"><span data-stu-id="c69c2-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="c69c2-126">[Редактор таблиц базы данных ![](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="c69c2-127">Кроме того, выберите столбец идентификатор и в разделе Свойства столбца ниже измените "Спецификация идентификатора" на "Да".</span><span class="sxs-lookup"><span data-stu-id="c69c2-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="c69c2-128">[![свойства столбца Identity](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="c69c2-129">Когда все будет готово, щелкните значок сохранить на панели инструментов или выберите файл | В меню выберите команду Сохранить и присвойте таблице имя**Movie**(единственное значение).</span><span class="sxs-lookup"><span data-stu-id="c69c2-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="c69c2-130">У нас есть база данных и таблица!</span><span class="sxs-lookup"><span data-stu-id="c69c2-130">We've got a database and a table!</span></span>

<span data-ttu-id="c69c2-131">[![выберите имя](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="c69c2-132">Вернитесь к обозреватель сервера и щелкните правой кнопкой мыши таблицу фильмов, а затем выберите команду "отобразить данные таблицы".</span><span class="sxs-lookup"><span data-stu-id="c69c2-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="c69c2-133">Введите несколько фильмов, чтобы в базе данных были данные.</span><span class="sxs-lookup"><span data-stu-id="c69c2-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="c69c2-134">[Изменение таблицы базы данных ![](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="c69c2-135">Создание модели</span><span class="sxs-lookup"><span data-stu-id="c69c2-135">Creating a Model</span></span>

<span data-ttu-id="c69c2-136">Теперь вернитесь к обозреватель решений в правой части интегрированной среды разработки и щелкните правой кнопкой мыши папку Models и выберите Добавить | Новый элемент.</span><span class="sxs-lookup"><span data-stu-id="c69c2-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="c69c2-137">[![аддневмоделитем](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="c69c2-138">Мы создадим модель сущностей из нашей новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="c69c2-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="c69c2-139">Это приведет к добавлению в наш проект набора классов, который упрощает для нас запрос и обработку данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="c69c2-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="c69c2-140">Выберите узел данных в левой части диалогового окна, а затем выберите шаблон элемента ADO.NET EDM.</span><span class="sxs-lookup"><span data-stu-id="c69c2-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="c69c2-141">Назовите его movies. edmx.</span><span class="sxs-lookup"><span data-stu-id="c69c2-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="c69c2-142">[![Аддневдатамодел](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="c69c2-143">Нажмите кнопку "Добавить".</span><span class="sxs-lookup"><span data-stu-id="c69c2-143">Click the "Add" button.</span></span> <span data-ttu-id="c69c2-144">После этого будет запущен мастер EDM.</span><span class="sxs-lookup"><span data-stu-id="c69c2-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="c69c2-145">В появившемся диалоговом окне выберите Создать из базы данных.</span><span class="sxs-lookup"><span data-stu-id="c69c2-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="c69c2-146">Так как мы только что сделали базу данных, нам нужно только сообщить Entity Framework о нашей новой базе данных и ее таблице.</span><span class="sxs-lookup"><span data-stu-id="c69c2-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="c69c2-147">Нажмите кнопку Далее, чтобы сохранить подключение к базе данных в конфигурации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c69c2-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="c69c2-148">Теперь установите флажок таблицы и фильм и нажмите кнопку Готово.</span><span class="sxs-lookup"><span data-stu-id="c69c2-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="c69c2-149">[Мастер EDM ![](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="c69c2-150">Теперь мы можем увидеть нашу новую таблицу фильмов в Entity Framework Designer и получить к ней доступ из кода.</span><span class="sxs-lookup"><span data-stu-id="c69c2-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="c69c2-151">[![фильмов — Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="c69c2-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="c69c2-152">В области конструктора можно увидеть класс "Movie".</span><span class="sxs-lookup"><span data-stu-id="c69c2-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="c69c2-153">Этот класс сопоставляется с таблицей "Movie" в нашей базе данных, и каждое свойство в нем сопоставляется со столбцом с таблицей.</span><span class="sxs-lookup"><span data-stu-id="c69c2-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="c69c2-154">Каждый экземпляр класса "Movie" будет соответствовать строке в таблице "Movie".</span><span class="sxs-lookup"><span data-stu-id="c69c2-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="c69c2-155">Если вам не нравятся соглашения об именовании и сопоставлении по умолчанию, используемые Entity Framework, можно использовать конструктор Entity Framework для их изменения или настройки.</span><span class="sxs-lookup"><span data-stu-id="c69c2-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="c69c2-156">Для этого приложения мы будем использовать значения по умолчанию и просто сохраняем файл как есть.</span><span class="sxs-lookup"><span data-stu-id="c69c2-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="c69c2-157">Теперь давайте выполним работу с некоторыми реальными данными!</span><span class="sxs-lookup"><span data-stu-id="c69c2-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c69c2-158">[Назад](getting-started-with-mvc-part3.md)
> [Вперед](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="c69c2-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
