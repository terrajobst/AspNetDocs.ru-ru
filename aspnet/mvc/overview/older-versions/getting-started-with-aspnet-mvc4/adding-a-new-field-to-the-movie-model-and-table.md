---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: Добавление нового поля в модель и таблицу фильмов | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленная версия этого учебника доступна здесь, в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще в исполнении и демонстрации...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498516"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a><span data-ttu-id="4c4d8-104">Добавление нового поля в модель и таблицу Movie</span><span class="sxs-lookup"><span data-stu-id="4c4d8-104">Adding a New Field to the Movie Model and Table</span></span>

<span data-ttu-id="4c4d8-105">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4c4d8-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="4c4d8-106">Обновленная версия этого учебника доступна [здесь](../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="4c4d8-107">Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="4c4d8-108">В этом разделе вы будете использовать Entity Framework Code First Migrations для переноса некоторых изменений в классы модели, чтобы изменения применялись к базе данных.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-108">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="4c4d8-109">По умолчанию при использовании Entity Framework Code First для автоматического создания базы данных, как это было сделано ранее в этом руководстве, Code First добавляет таблицу в базу данных, чтобы определить, синхронизирована ли схема базы данных с классами модели, из которых она была создана.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-109">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="4c4d8-110">Если они не синхронизированы, Entity Framework выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-110">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="4c4d8-111">Это упрощает отслеживание проблем во время разработки, которые в противном случае могут быть найдены (путем маскировки ошибок) во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-111">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="4c4d8-112">Настройка Code First Migrations для изменений модели</span><span class="sxs-lookup"><span data-stu-id="4c4d8-112">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="4c4d8-113">Если вы используете Visual Studio 2012, дважды щелкните файл *movies. mdf* в Обозреватель решений, чтобы открыть средство базы данных.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-113">If you are using Visual Studio 2012, double click the *Movies.mdf* file from Solution Explorer to open the database tool.</span></span> <span data-ttu-id="4c4d8-114">Visual Studio Express для веб-узла покажет обозреватель базы данных, Visual Studio 2012 отобразит обозреватель сервера.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-114">Visual Studio Express for Web will show Database Explorer, Visual Studio 2012 will show Server Explorer.</span></span> <span data-ttu-id="4c4d8-115">Если вы используете Visual Studio 2010, используйте обозреватель объектов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-115">If you are using Visual Studio 2010, use SQL Server Object Explorer.</span></span>

<span data-ttu-id="4c4d8-116">В средстве "база данных" (обозреватель базы данных, обозреватель сервера или обозреватель объектов SQL Server) щелкните правой кнопкой мыши `MovieDBContext` и выберите **Удалить** , чтобы удалить базу данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-116">In the database tool (Database Explorer, Server Explorer or SQL Server Object Explorer), right click on `MovieDBContext` and select **Delete** to drop the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

<span data-ttu-id="4c4d8-117">Вернитесь к обозреватель решений.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-117">Navigate back to Solution Explorer.</span></span> <span data-ttu-id="4c4d8-118">Щелкните правой кнопкой мыши файл *movies. mdf* и выберите **Удалить** , чтобы удалить базу данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-118">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

<span data-ttu-id="4c4d8-119">Постройте приложение, чтобы убедиться в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-119">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="4c4d8-120">В меню **Сервис** щелкните **Диспетчер пакетов NuGet**, а затем щелкните **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-120">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![Добавить пакет man](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

<span data-ttu-id="4c4d8-122">В окне **консоли диспетчера пакетов** в строке `PM>` введите "Enable-migrations-ContextTypeName MvcMovie. Models. мовиедбконтекст".</span><span class="sxs-lookup"><span data-stu-id="4c4d8-122">In the **Package Manager Console** window at the `PM>` prompt enter "Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext".</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

<span data-ttu-id="4c4d8-123">Команда **включить-миграции** (показанная выше) создает файл *Configuration.CS* в новой папке *migrations* .</span><span class="sxs-lookup"><span data-stu-id="4c4d8-123">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

<span data-ttu-id="4c4d8-124">Visual Studio откроет файл *Configuration.CS* .</span><span class="sxs-lookup"><span data-stu-id="4c4d8-124">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="4c4d8-125">Замените метод `Seed` в файле *Configuration.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="4c4d8-125">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

<span data-ttu-id="4c4d8-126">Щелкните правой кнопкой мыши красную волнистую линию в разделе `Movie` и выберите **Разрешить** , **а затем —** **MvcMovie. Models;**</span><span class="sxs-lookup"><span data-stu-id="4c4d8-126">Right click on the red squiggly line under `Movie` and select **Resolve** then **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

<span data-ttu-id="4c4d8-127">При этом добавляется следующая инструкция using:</span><span class="sxs-lookup"><span data-stu-id="4c4d8-127">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="4c4d8-128">Code First Migrations вызывает метод `Seed` после каждой миграции (то есть вызывает **Обновление базы данных** в консоли диспетчера пакетов), и этот метод обновляет уже вставленные строки или вставляет их, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-128">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>

<span data-ttu-id="4c4d8-129">**Нажмите клавиши CTRL + SHIFT + B, чтобы выполнить сборку проекта.** (Если на этом этапе не выполняется сборка, следующие действия завершаются ошибкой.)</span><span class="sxs-lookup"><span data-stu-id="4c4d8-129">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if your don't build at this point.)</span></span>

<span data-ttu-id="4c4d8-130">Следующим шагом является создание класса `DbMigration` для первоначальной миграции.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-130">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="4c4d8-131">Эта миграция создает новую базу данных, поэтому вы удалили файл *Movie. mdf* на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-131">This migration to creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="4c4d8-132">В окне **консоли диспетчера пакетов** введите команду "добавить начальную миграцию", чтобы создать первоначальную миграцию.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-132">In the **Package Manager Console** window, enter the command "add-migration Initial" to create the initial migration.</span></span> <span data-ttu-id="4c4d8-133">Имя «Initial» является произвольным и используется для имени создаваемого файла миграции.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-133">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

<span data-ttu-id="4c4d8-134">Code First Migrations создает другой файл класса в папке *migrations* (с именем *{датестамп}\_Initial.CS* ), а этот класс содержит код, создающий схему базы данных.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-134">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="4c4d8-135">Имя файла миграции предварительно исправлено с меткой времени, помогающей в упорядочении.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-135">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="4c4d8-136">Проверьте файл *{датестамп}\_Initial.CS* , он содержит инструкции по созданию таблицы фильмов для базы данных Movie.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-136">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the Movies table for the Movie DB.</span></span> <span data-ttu-id="4c4d8-137">При обновлении базы данных в приведенных ниже инструкциях файл *{датестамп}\_Initial.CS* будет запущен и создана схема базы данных.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-137">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="4c4d8-138">Затем будет выполнен метод **SEED** для заполнения базы данных тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-138">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="4c4d8-139">В **консоли диспетчера пакетов**введите команду Update-Database, чтобы создать базу данных и запустить метод **SEED** .</span><span class="sxs-lookup"><span data-stu-id="4c4d8-139">In the **Package Manager Console**, enter the command "update-database" to create the database and run the **Seed** method.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

<span data-ttu-id="4c4d8-140">Если появляется сообщение об ошибке, показывающее, что таблица уже существует и не может быть создана, возможно, приложение было запущено после удаления базы данных и перед выполнением `update-database`.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-140">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="4c4d8-141">В этом случае удалите файл *movies. mdf* еще раз и повторите команду `update-database`.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-141">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="4c4d8-142">Если вы по-прежнему получаете сообщение об ошибке, удалите папку и содержимое миграции, а затем начните с указания в верхней части этой страницы (которая удаляет файл *movies. mdf* , а затем переходит к включению-миграции).</span><span class="sxs-lookup"><span data-stu-id="4c4d8-142">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span>

<span data-ttu-id="4c4d8-143">Запустите приложение и перейдите по URL-адресу */Movies* .</span><span class="sxs-lookup"><span data-stu-id="4c4d8-143">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="4c4d8-144">Отобразятся начальные данные.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-144">The seed data is displayed.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="4c4d8-145">Добавление свойства Rating в модель Movie</span><span class="sxs-lookup"><span data-stu-id="4c4d8-145">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="4c4d8-146">Для начала добавьте новое свойство `Rating` в существующий класс `Movie`.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-146">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="4c4d8-147">Откройте файл *моделс\мовие.КС* и добавьте свойство `Rating` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4c4d8-147">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

<span data-ttu-id="4c4d8-148">Теперь полный `Movie` класс выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4c4d8-148">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

<span data-ttu-id="4c4d8-149">Создайте приложение с помощью команды меню **построить** &gt;**создать фильм** или нажав клавиши CTRL + SHIFT + B.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-149">Build the application using the **Build** &gt;**Build Movie** menu command or by pressing CTRL-SHIFT-B.</span></span>

<span data-ttu-id="4c4d8-150">Теперь, когда вы обновили класс `Model`, вам также потребуется обновить шаблоны представления *\виевс\мовиес\индекс.кштмл* и *\виевс\мовиес\креате.кштмл* , чтобы отобразить новое свойство `Rating` в представлении браузера.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-150">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to display the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="4c4d8-151">Откройте файл<em>\виевс\мовиес\индекс.кштмл</em> и добавьте заголовок столбца `<th>Rating</th>` сразу после столбца <strong>Price</strong> .</span><span class="sxs-lookup"><span data-stu-id="4c4d8-151">Open the<em>\Views\Movies\Index.cshtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="4c4d8-152">Затем добавьте `<td>` столбец рядом с концом шаблона, чтобы отобразить значение `@item.Rating`.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-152">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="4c4d8-153">Ниже показано, как выглядит обновленный шаблон представления <em>index. cshtml</em> :</span><span class="sxs-lookup"><span data-stu-id="4c4d8-153">Below is what the updated <em>Index.cshtml</em> view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

<span data-ttu-id="4c4d8-154">Затем откройте файл *\виевс\мовиес\креате.кштмл* и добавьте следующую разметку в конец формы.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-154">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="4c4d8-155">При этом текстовое поле подготавливается к просмотру, что позволяет указать рейтинг при создании нового фильма.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-155">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

<span data-ttu-id="4c4d8-156">Теперь вы обновили код приложения для поддержки нового свойства `Rating`.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-156">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="4c4d8-157">Теперь запустите приложение и перейдите по URL-адресу */Movies* .</span><span class="sxs-lookup"><span data-stu-id="4c4d8-157">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="4c4d8-158">Однако при этом вы увидите одну из следующих ошибок:</span><span class="sxs-lookup"><span data-stu-id="4c4d8-158">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

<span data-ttu-id="4c4d8-159">Эта ошибка возникает, поскольку обновленный класс модели `Movie` в приложении теперь отличается от схемы `Movie` таблицы существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-159">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="4c4d8-160">(В таблице базы данных отсутствует столбец `Rating`.)</span><span class="sxs-lookup"><span data-stu-id="4c4d8-160">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="4c4d8-161">Устранить эту ошибку можно несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="4c4d8-161">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="4c4d8-162">Можно с помощью Entity Framework автоматически удалить и повторно создать базу данных на основе новой схемы класса модели.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-162">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="4c4d8-163">Этот подход очень удобен при выполнении активной разработки в тестовой базе данных. Это позволяет быстро развивать модель и схему базы данных вместе.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-163">This approach is very convenient when doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="4c4d8-164">Недостаток этого подхода заключается в том, что в базе данных теряются существующие данные — поэтому вы *не* хотите использовать этот подход в рабочей базе данных!</span><span class="sxs-lookup"><span data-stu-id="4c4d8-164">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="4c4d8-165">Использование инициализатора для автоматического заполнения базы данных с тестовыми данными часто является эффективным способом разработки приложения.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-165">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="4c4d8-166">Дополнительные сведения об Entity Framework инициализаторах баз данных см. в руководстве по [ASP.NET MVC и Entity Framework](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)для Tom Dykstra).</span><span class="sxs-lookup"><span data-stu-id="4c4d8-166">For more information on Entity Framework database initializers, see Tom Dykstra's [ASP.NET MVC/Entity Framework tutorial](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="4c4d8-167">Можно явно изменить схему существующей базы данных в соответствии с новыми классами модели.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-167">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="4c4d8-168">Преимущество такого подхода состоит в том, что сохраняются все данные.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-168">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="4c4d8-169">Это изменение можно выполнить как вручную, так и с помощью соответствующего скрипта базы данных.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-169">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="4c4d8-170">Можно обновить схему базы данных с помощью Code First Migrations.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-170">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="4c4d8-171">В этом руководстве используется Code First Migrations.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-171">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="4c4d8-172">Обновите метод SEED, чтобы он выдает значение для нового столбца.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-172">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="4c4d8-173">Откройте файл Migrations\Configuration.cs и добавьте поле рейтинга в каждый объект Movie.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-173">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

<span data-ttu-id="4c4d8-174">Выполните сборку решения, а затем откройте окно **консоли диспетчера пакетов** и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4c4d8-174">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration AddRatingMig`

<span data-ttu-id="4c4d8-175">Команда `add-migration` сообщает платформе миграции, что необходимо проверить текущую модель фильма с текущей схемой базы данных Movie и создать необходимый код для переноса базы данных в новую модель.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-175">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="4c4d8-176">Аддратингмиг является произвольным и используется для имени файла миграции.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-176">The AddRatingMig is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="4c4d8-177">Полезно использовать понятное имя для шага миграции.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-177">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="4c4d8-178">По завершении этой команды Visual Studio открывает файл класса, который определяет новый производный класс `DbMigration`, а в методе `Up` можно увидеть код, создающий новый столбец.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-178">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

<span data-ttu-id="4c4d8-179">Выполните сборку решения, а затем введите команду "обновить базу данных" в окне **консоли диспетчера пакетов** .</span><span class="sxs-lookup"><span data-stu-id="4c4d8-179">Build the solution, and then enter the "update-database" command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="4c4d8-180">На следующем рисунке показаны выходные данные в окне **консоли диспетчера пакетов** (отметка даты ожидаемая аддратингмиг будет отличаться).</span><span class="sxs-lookup"><span data-stu-id="4c4d8-180">The following image shows the output in the **Package Manager Console** window (The date stamp prepending AddRatingMig will be different.)</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

<span data-ttu-id="4c4d8-181">Повторно запустите приложение и перейдите по URL-адресу/movies.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-181">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="4c4d8-182">Можно увидеть новое поле рейтинг.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-182">You can see the new Rating field.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

<span data-ttu-id="4c4d8-183">Щелкните ссылку **создать** , чтобы добавить новый фильм.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-183">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="4c4d8-184">Обратите внимание, что можно добавить оценку.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-184">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

<span data-ttu-id="4c4d8-186">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-186">Click **Create**.</span></span> <span data-ttu-id="4c4d8-187">Теперь новый фильм, включая рейтинг, отображается в списке фильмов:</span><span class="sxs-lookup"><span data-stu-id="4c4d8-187">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

<span data-ttu-id="4c4d8-189">Также следует добавить поле `Rating` в шаблоны представлений Edit, Details и Сеарчиндекс.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-189">You should also add the `Rating` field to the Edit, Details and SearchIndex view templates.</span></span>

<span data-ttu-id="4c4d8-190">Можно снова ввести команду "обновить базу данных" в окне **консоли диспетчера пакетов** и не вносить изменения, так как схема соответствует модели.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-190">You could enter the "update-database" command in the **Package Manager Console** window again and no changes would be made, because the schema matches the model.</span></span>

<span data-ttu-id="4c4d8-191">В этом разделе вы узнали, как можно изменить объекты модели и синхронизировать базу данных с изменениями.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-191">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="4c4d8-192">Вы также узнали, как заполнить созданную базу данных образцами данных, чтобы вы могли испытать сценарии.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-192">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="4c4d8-193">Теперь рассмотрим, как можно добавить расширенную логику проверки к классам модели и обеспечить применение некоторых бизнес-правил.</span><span class="sxs-lookup"><span data-stu-id="4c4d8-193">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4c4d8-194">[Назад](examining-the-edit-methods-and-edit-view.md)
> [Вперед](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="4c4d8-194">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
