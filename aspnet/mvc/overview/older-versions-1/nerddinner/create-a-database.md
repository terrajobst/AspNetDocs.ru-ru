---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Создание базы данных | Документация Майкрософт
author: microsoft
description: На шаге 2 показаны шаги по созданию базы данных, содержащей все данные о ужинах и RSVP для нашего приложения NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469302"
---
# <a name="create-a-database"></a><span data-ttu-id="d940c-103">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="d940c-103">Create a Database</span></span>

<span data-ttu-id="d940c-104">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d940c-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d940c-105">Скачать в формате PDF</span><span class="sxs-lookup"><span data-stu-id="d940c-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="d940c-106">Это шаг 2 бесплатного [учебника по NerdDinner приложению](introducing-the-nerddinner-tutorial.md) , в котором рассматривается создание небольшого, но полного веб-приложения с использованием ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="d940c-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="d940c-107">На шаге 2 показаны шаги по созданию базы данных, содержащей все данные о ужинах и RSVP для нашего приложения NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="d940c-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="d940c-108">Если вы используете ASP.NET MVC 3, мы рекомендуем следовать руководствам по [Начало работы в MVC 3 или в приложении для](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [музыкального магазина MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="d940c-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="d940c-109">NerdDinner. шаг 2. Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="d940c-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="d940c-110">Мы будем использовать базу данных для хранения всех данных о обедах и RSVP для нашего приложения NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="d940c-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="d940c-111">Приведенные ниже действия показывают создание базы данных с помощью бесплатного SQL Server Express выпуска (который можно легко установить с помощью версии 2 [установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d940c-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="d940c-112">Весь код, который мы будем писать, работает как с SQL Server Express, так и с полной SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d940c-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="d940c-113">Создание новой базы данных SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="d940c-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="d940c-114">Для начала щелкните правой кнопкой мыши наш веб-проект и выберите команду **Добавить-&gt;новый элемент** :</span><span class="sxs-lookup"><span data-stu-id="d940c-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="d940c-115">Откроется диалоговое окно "Добавление нового элемента" в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d940c-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="d940c-116">Мы отфильтрим по категории "данные" и выбираем шаблон элемента "база данных" SQL Server:</span><span class="sxs-lookup"><span data-stu-id="d940c-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="d940c-117">Мы назовем базу данных SQL Server Express, которую нужно создать "NerdDinner. mdf", и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="d940c-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="d940c-118">Visual Studio запросит нас, если нам нужно добавить этот файл в наш каталог данных \Апп\_(каталог уже настроен для чтения и записи списков ACL безопасности):</span><span class="sxs-lookup"><span data-stu-id="d940c-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="d940c-119">Нажмите кнопку "Да", и наша новая база данных будет создана и добавлена в наш обозреватель решений:</span><span class="sxs-lookup"><span data-stu-id="d940c-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="d940c-120">Создание таблиц в базе данных</span><span class="sxs-lookup"><span data-stu-id="d940c-120">Creating Tables within our Database</span></span>

<span data-ttu-id="d940c-121">Теперь у нас есть новая пустая база данных.</span><span class="sxs-lookup"><span data-stu-id="d940c-121">We now have a new empty database.</span></span> <span data-ttu-id="d940c-122">Давайте добавим к ней несколько таблиц.</span><span class="sxs-lookup"><span data-stu-id="d940c-122">Let's add some tables to it.</span></span>

<span data-ttu-id="d940c-123">Для этого перейдите в окно вкладки "обозреватель сервера" в Visual Studio, что позволит нам управлять базами данных и серверами.</span><span class="sxs-lookup"><span data-stu-id="d940c-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="d940c-124">SQL Server Express базы данных, хранящиеся в папке \Апп\_данных приложения, будут автоматически отображаться в обозреватель сервера.</span><span class="sxs-lookup"><span data-stu-id="d940c-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="d940c-125">Можно также использовать значок "подключиться к базе данных" в верхней части окна "обозреватель сервера" для добавления дополнительных SQL Server баз данных (как локальных, так и удаленных) в список:</span><span class="sxs-lookup"><span data-stu-id="d940c-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="d940c-126">Мы добавим две таблицы в нашу базу данных NerdDinner — одну для хранения нашей диннерс, а другую — для контроля принятия RSVP.</span><span class="sxs-lookup"><span data-stu-id="d940c-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="d940c-127">Чтобы создать новые таблицы, щелкните правой кнопкой мыши папку "Tables" в нашей базе данных и выберите команду "добавить новую таблицу":</span><span class="sxs-lookup"><span data-stu-id="d940c-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="d940c-128">Откроется конструктор таблиц, позволяющий настроить схему таблицы.</span><span class="sxs-lookup"><span data-stu-id="d940c-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="d940c-129">Для нашей таблицы "диннерс" мы добавим 10 столбцов данных:</span><span class="sxs-lookup"><span data-stu-id="d940c-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="d940c-130">Мы хотим, чтобы столбец "Диннерид" был уникальным первичным ключом для таблицы.</span><span class="sxs-lookup"><span data-stu-id="d940c-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="d940c-131">Это можно настроить, щелкнув правой кнопкой мыши столбец "Диннерид" и выбрав пункт меню "Задать первичный ключ":</span><span class="sxs-lookup"><span data-stu-id="d940c-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="d940c-132">Кроме того, чтобы сделать Диннерид первичным ключом, мы также хотим настроить его как столбец Identity, значение которого автоматически увеличивается по мере добавления новых строк данных в таблицу (то есть первая вставленная строка обеда будет иметь значение Диннерид, равное 1, вторая вставленная строка будет иметь значение Диннерид, равное 2 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="d940c-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="d940c-133">Для этого можно выбрать столбец "Диннерид", а затем использовать редактор "Свойства столбца", чтобы задать для свойства "(является идентификатором)" значение "Да".</span><span class="sxs-lookup"><span data-stu-id="d940c-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="d940c-134">Мы будем использовать стандартные идентификаторы по умолчанию (начинаются с 1 и увеличивая 1 для каждой новой строки обеда):</span><span class="sxs-lookup"><span data-stu-id="d940c-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="d940c-135">Затем мы сохраним нашу таблицу, введя CTRL-S или выполнив команду меню **File-&gt;Save** .</span><span class="sxs-lookup"><span data-stu-id="d940c-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="d940c-136">При этом будет предложено ввести имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="d940c-136">This will prompt us to name the table.</span></span> <span data-ttu-id="d940c-137">Мы назовем его «диннерс»:</span><span class="sxs-lookup"><span data-stu-id="d940c-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="d940c-138">Новая таблица диннерс будет отображаться в базе данных в обозревателе сервера.</span><span class="sxs-lookup"><span data-stu-id="d940c-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="d940c-139">Затем мы повторим описанные выше действия и создадим таблицу "RSVP".</span><span class="sxs-lookup"><span data-stu-id="d940c-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="d940c-140">Эта таблица содержит 3 столбца.</span><span class="sxs-lookup"><span data-stu-id="d940c-140">This table with have 3 columns.</span></span> <span data-ttu-id="d940c-141">Столбец Рсвпид будет настроен в качестве первичного ключа, а также станет столбцом идентификаторов:</span><span class="sxs-lookup"><span data-stu-id="d940c-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="d940c-142">Мы сохраним его и присвоим ему имя "RSVP".</span><span class="sxs-lookup"><span data-stu-id="d940c-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="d940c-143">Настройка связи по внешнему ключу между таблицами</span><span class="sxs-lookup"><span data-stu-id="d940c-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="d940c-144">Теперь у нас есть две таблицы в нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="d940c-144">We now have two tables within our database.</span></span> <span data-ttu-id="d940c-145">Последний этап проектирования схемы заключается в настройке связи «один ко многим» между этими двумя таблицами. Таким образом, можно связать каждую строку из компании с нулевым или несколькими строками RSVP, которые применяются к нему.</span><span class="sxs-lookup"><span data-stu-id="d940c-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="d940c-146">Для этого нужно настроить в столбце "Диннерид" таблицы RSVP связь с внешним ключом к столбцу "Диннерид" в таблице "диннерс".</span><span class="sxs-lookup"><span data-stu-id="d940c-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="d940c-147">Для этого нужно открыть таблицу RSVP в конструкторе таблиц, дважды щелкнув ее в обозревателе сервера.</span><span class="sxs-lookup"><span data-stu-id="d940c-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="d940c-148">Затем выберите в нем столбец "Диннерид", щелкните правой кнопкой мыши и выберите "связи...". Команда контекстного меню:</span><span class="sxs-lookup"><span data-stu-id="d940c-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="d940c-149">Откроется диалоговое окно, которое можно использовать для установки связей между таблицами:</span><span class="sxs-lookup"><span data-stu-id="d940c-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="d940c-150">Нажмите кнопку "Добавить", чтобы добавить новую связь в диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d940c-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="d940c-151">После добавления связи мы развернем узел древовидного представления "таблицы и столбцы" в сетке свойств справа от диалогового окна и нажимайте кнопку "...". справа от нее:</span><span class="sxs-lookup"><span data-stu-id="d940c-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="d940c-152">Нажатие кнопки "..." появится еще одно диалоговое окно, позволяющее указать, какие таблицы и столбцы участвуют в связи, а также дать нам возможность присвоить имя связи.</span><span class="sxs-lookup"><span data-stu-id="d940c-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="d940c-153">Мы изменим таблицу первичного ключа на "диннерс" и выбираем столбец "Диннерид" в таблице диннерс в качестве первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="d940c-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="d940c-154">Наша таблица RSVP будет таблицей с внешним ключом и RSVP. Столбец Диннерид будет связан как внешний ключ:</span><span class="sxs-lookup"><span data-stu-id="d940c-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="d940c-155">Теперь каждая строка в таблице RSVP будет связана со строкой в таблице Dinner.</span><span class="sxs-lookup"><span data-stu-id="d940c-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="d940c-156">SQL Server будет поддерживать целостность данных в США и не допустить добавления новой строки RSVP, если она не указывает на допустимую строку в обеде.</span><span class="sxs-lookup"><span data-stu-id="d940c-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="d940c-157">Кроме того, она не позволит нам удалить строку в обеде, если на нее ссылаются все строки RSVP.</span><span class="sxs-lookup"><span data-stu-id="d940c-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="d940c-158">Добавление данных в таблицы</span><span class="sxs-lookup"><span data-stu-id="d940c-158">Adding Data to our Tables</span></span>

<span data-ttu-id="d940c-159">Добавим примеры данных в нашу таблицу диннерс.</span><span class="sxs-lookup"><span data-stu-id="d940c-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="d940c-160">Можно добавить данные в таблицу, щелкнув ее правой кнопкой мыши в обозреватель сервера и выбрав команду "отобразить данные таблицы":</span><span class="sxs-lookup"><span data-stu-id="d940c-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="d940c-161">Мы добавим несколько строк данных о обедах, которые можно будет использовать позже, как мы начнем с реализации приложения:</span><span class="sxs-lookup"><span data-stu-id="d940c-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="d940c-162">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="d940c-162">Next Step</span></span>

<span data-ttu-id="d940c-163">Создание базы данных завершено.</span><span class="sxs-lookup"><span data-stu-id="d940c-163">We've finished creating our database.</span></span> <span data-ttu-id="d940c-164">Теперь создадим классы модели, которые можно использовать для запроса и обновления.</span><span class="sxs-lookup"><span data-stu-id="d940c-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d940c-165">[Назад](create-a-new-aspnet-mvc-project.md)
> [Вперед](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="d940c-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
