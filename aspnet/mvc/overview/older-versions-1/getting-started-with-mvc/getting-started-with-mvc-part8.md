---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: Добавление столбца в модель | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Создание простого веб-приложения, считывающего и записывающего данные из базы данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437226"
---
# <a name="adding-a-column-to-the-model"></a><span data-ttu-id="4eb2a-104">Добавление столбца в модель</span><span class="sxs-lookup"><span data-stu-id="4eb2a-104">Adding a Column to the Model</span></span>

<span data-ttu-id="4eb2a-105">по [Скотт Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="4eb2a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="4eb2a-106">Это руководство для начинающих, в котором представлены основы ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="4eb2a-107">Вы создадите простое веб-приложение, считывающее и записывающее данные из базы данных.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="4eb2a-108">Посетите [центр обучения ASP.NET MVC](../../../index.md) , чтобы найти другие руководства и примеры для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="4eb2a-109">В этом разделе мы пошаговым инструкциями по внесению изменений в схему базы данных и обработке изменений в приложении.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="4eb2a-110">Давайте добавим столбец "Оценка" в таблицу фильмов.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-110">Let's add a "Rating" Column to the Movie table.</span></span> <span data-ttu-id="4eb2a-111">Вернитесь в интегрированную среду разработки и щелкните обозреватель базы данных.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="4eb2a-112">Щелкните правой кнопкой мыши таблицу Movie и выберите Open Table Definition (Открыть определение таблицы).</span><span class="sxs-lookup"><span data-stu-id="4eb2a-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="4eb2a-113">Добавьте столбец "Оценка", как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="4eb2a-114">Так как у нас сейчас нет оценок, столбец может допускать значения NULL.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="4eb2a-115">Нажмите кнопку «Сохранить».</span><span class="sxs-lookup"><span data-stu-id="4eb2a-115">Click Save.</span></span>

<span data-ttu-id="4eb2a-116">[![редактирования таблицы фильмов](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4eb2a-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="4eb2a-117">Затем вернитесь к обозреватель решений и откройте файл movies. EDMX (который находится в папке \Моделс).</span><span class="sxs-lookup"><span data-stu-id="4eb2a-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="4eb2a-118">Щелкните правой кнопкой мыши область конструктора (белая область) и выберите пункт Обновить модель из базы данных.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="4eb2a-119">[![фильмов — Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4eb2a-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="4eb2a-120">Запустится мастер обновления.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="4eb2a-121">Щелкните вкладку обновить внутри нее и нажмите кнопку Готово.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="4eb2a-122">Затем наш класс модели Movie будет обновлен с помощью нового столбца.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-122">Our Movie model class will then be updated with the new column.</span></span>

![Мастер обновления (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="4eb2a-124">После нажатия кнопки Готово можно увидеть, что новый столбец рейтинг добавлен в сущность Movie в нашей модели.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="4eb2a-125">[Сущность ![Movie](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="4eb2a-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="4eb2a-126">Мы добавили столбец в модель базы данных, но представления не знакомы с ними.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="4eb2a-127">Обновление представлений с изменениями модели</span><span class="sxs-lookup"><span data-stu-id="4eb2a-127">Update Views with Model Changes</span></span>

<span data-ttu-id="4eb2a-128">Существует несколько способов обновления наших шаблонов представления для отражения нового столбца рейтинга.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="4eb2a-129">Так как мы создали эти представления, создав их с помощью диалогового окна Добавление представления, мы могли бы удалить их и повторно создать заново.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="4eb2a-130">Тем не менее, обычно люди уже внесли изменения в свои шаблоны представлений из первоначального формирования шаблонов и хотят добавлять или удалять поля вручную, как и в поле идентификатора для CREATE.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="4eb2a-131">Откройте шаблон \Виевс\мовиес\индекс.аспкс и добавьте &lt;&gt;рейтинг&lt;/с&gt; в заголовок таблицы фильмов.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="4eb2a-132">После жанра я добавил мой.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-132">I added mine after Genre.</span></span> <span data-ttu-id="4eb2a-133">Затем, в том же положении столбца, но ниже, добавьте строку для вывода нашей новой оценки.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="4eb2a-134">Наш окончательный шаблон index. aspx будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4eb2a-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="4eb2a-135">Теперь откройте шаблон \Виевс\мовиес\креате.аспкс и добавьте метку и текстовое поле для нового свойства рейтинга:</span><span class="sxs-lookup"><span data-stu-id="4eb2a-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="4eb2a-136">Наш окончательный шаблон CREATE. aspx будет выглядеть следующим образом. Давайте изменим заголовок браузера и дополнительный &lt;H2&gt; заголовок на нечто вроде "создать фильм", пока мы здесь!</span><span class="sxs-lookup"><span data-stu-id="4eb2a-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="4eb2a-137">Запустите приложение, и теперь вы получили новое поле в базе данных, которое было добавлено на страницу создания.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="4eb2a-138">Добавьте новый фильм — на этот раз с рейтингом и нажмите кнопку Создать.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="4eb2a-139">[![создания фильма в Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="4eb2a-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="4eb2a-140">После нажатия кнопки создать вы отправляетесь на страницу индекса, где отображается новый фильм с новым столбцом Рейтинг в базе данных.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="4eb2a-141">[Список фильмов ![— Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="4eb2a-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="4eb2a-142">В этом учебном курсе было начато создание контроллеров, связывание их с представлениями и передача жестко запрограммированных данных.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="4eb2a-143">Затем мы создали и разработали базу данных и поместили в нее некоторые данные.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="4eb2a-144">Мы получили данные из базы данных и отображали их в таблице HTML.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="4eb2a-145">Затем мы добавили форму создания, которая позволяет пользователю добавлять данные в базу данных из веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="4eb2a-146">Мы добавили проверку, а затем выполнили проверку, используя JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="4eb2a-147">Наконец, мы изменили базу данных, включив в нее новый столбец данных, затем обновили две страницы, чтобы создать и отобразить новые данные.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="4eb2a-148">Теперь я рекомендую перейти к нашему учебнику "[музыкальное хранилище MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" на промежуточном уровне, а также ко многим видео и ресурсам на [https://asp.net/mvc](https://asp.net/mvc) , чтобы узнать больше о ASP.NET MVC!</span><span class="sxs-lookup"><span data-stu-id="4eb2a-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="4eb2a-149">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="4eb2a-149">Enjoy!</span></span>

- <span data-ttu-id="4eb2a-150">Скотт Hanselman — [http://hanselman.com](http://hanselman.com) и [@shanselman](http://twitter.com/shanselman) в Twitter.</span><span class="sxs-lookup"><span data-stu-id="4eb2a-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4eb2a-151">Назад</span><span class="sxs-lookup"><span data-stu-id="4eb2a-151">Previous</span></span>](getting-started-with-mvc-part7.md)
