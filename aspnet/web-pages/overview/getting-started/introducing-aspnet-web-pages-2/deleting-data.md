---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: Введение веб-страницы ASP.NET-удаление данных базы данных | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике показано, как удалить отдельную запись базы данных. Предполагается, что вы выполнили цикл по обновлению данных базы данных в ASP.NET Web PA...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510462"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="a240d-104">Введение веб-страницы ASP.NET-удаление данных базы данных</span><span class="sxs-lookup"><span data-stu-id="a240d-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>

<span data-ttu-id="a240d-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a240d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a240d-106">В этом учебнике показано, как удалить отдельную запись базы данных.</span><span class="sxs-lookup"><span data-stu-id="a240d-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="a240d-107">Предполагается, что вы выполнили цикл по [обновлению данных базы данных в веб-страницы ASP.NET](updating-data.md).</span><span class="sxs-lookup"><span data-stu-id="a240d-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="a240d-108">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="a240d-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="a240d-109">Выбор отдельной записи из списка записей.</span><span class="sxs-lookup"><span data-stu-id="a240d-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="a240d-110">Удаление одной записи из базы данных.</span><span class="sxs-lookup"><span data-stu-id="a240d-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="a240d-111">Как проверить, была ли нажата определенная кнопка в форме.</span><span class="sxs-lookup"><span data-stu-id="a240d-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="a240d-112">Обсуждаемые функции и технологии:</span><span class="sxs-lookup"><span data-stu-id="a240d-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="a240d-113">Вспомогательный метод `WebGrid`.</span><span class="sxs-lookup"><span data-stu-id="a240d-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="a240d-114">Команда SQL `Delete`.</span><span class="sxs-lookup"><span data-stu-id="a240d-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="a240d-115">Метод `Database.Execute` для выполнения команды SQL `Delete`.</span><span class="sxs-lookup"><span data-stu-id="a240d-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="a240d-116">Что вы создадите</span><span class="sxs-lookup"><span data-stu-id="a240d-116">What You'll Build</span></span>

<span data-ttu-id="a240d-117">В предыдущем руководстве вы узнали, как обновить существующую запись базы данных.</span><span class="sxs-lookup"><span data-stu-id="a240d-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="a240d-118">Этот учебник аналогичен, но вместо обновления записи вы удалите его.</span><span class="sxs-lookup"><span data-stu-id="a240d-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="a240d-119">Процессы во многом одинаковы, за исключением того, что удаление упрощается, поэтому этот учебник будет небольшим.</span><span class="sxs-lookup"><span data-stu-id="a240d-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="a240d-120">На странице *фильмов* вы обновите вспомогательную функцию `WebGrid`, чтобы она отображала ссылку **Delete (удалить** ) рядом с каждым фильмом, сопровождающую ссылку на **изменение** , добавленную ранее.</span><span class="sxs-lookup"><span data-stu-id="a240d-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![Страница фильмов, на которой показана ссылка для удаления каждого фильма](deleting-data/_static/image1.png)

<span data-ttu-id="a240d-122">Как и при редактировании, при щелчке ссылки **Удалить** выполняется переход на другую страницу, где сведения о фильме уже находятся в форме:</span><span class="sxs-lookup"><span data-stu-id="a240d-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![Удаление страницы фильма с отображаемым фильмом](deleting-data/_static/image2.png)

<span data-ttu-id="a240d-124">Затем можно нажать кнопку, чтобы удалить запись без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="a240d-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="a240d-125">Добавление ссылки на удаление в список фильмов</span><span class="sxs-lookup"><span data-stu-id="a240d-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="a240d-126">Начнем с добавления ссылки **Delete** в вспомогательную функцию `WebGrid`.</span><span class="sxs-lookup"><span data-stu-id="a240d-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="a240d-127">Эта ссылка похожа на ссылку **редактирования** , добавленную в предыдущем руководстве.</span><span class="sxs-lookup"><span data-stu-id="a240d-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="a240d-128">Откройте файл *movies. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a240d-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="a240d-129">Измените `WebGrid` разметку в тексте страницы, добавив столбец.</span><span class="sxs-lookup"><span data-stu-id="a240d-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="a240d-130">Измененная разметка:</span><span class="sxs-lookup"><span data-stu-id="a240d-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="a240d-131">Новый столбец является следующим:</span><span class="sxs-lookup"><span data-stu-id="a240d-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="a240d-132">Способ настройки сетки, столбец « **Правка** » является крайним левым в сетке, а столбец « **Удаление** » — крайний правый.</span><span class="sxs-lookup"><span data-stu-id="a240d-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="a240d-133">(В случае, если вы не заметите, есть запятая после `Year` столбца.) Нет ничего особенного, о том, где находятся эти ссылочные столбцы, и можно легко разместить их рядом друг с другом.</span><span class="sxs-lookup"><span data-stu-id="a240d-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="a240d-134">В этом случае они разделяются, чтобы их было сложнее приступить к изприятию.</span><span class="sxs-lookup"><span data-stu-id="a240d-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![Страница "фильмы" с ссылками "Изменить" и "подробности", помеченными, чтобы показывать, что они не находятся рядом](deleting-data/_static/image3.png)

<span data-ttu-id="a240d-136">В новом столбце отображается ссылка (`<a>` элемент), текст которой говорит «DELETE».</span><span class="sxs-lookup"><span data-stu-id="a240d-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="a240d-137">Целевой объект ссылки (его атрибут `href`) — это код, который, в конечном итоге, разрешается в нечто вроде этого URL-адреса, и `id` значение для каждого фильма отличается.</span><span class="sxs-lookup"><span data-stu-id="a240d-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="a240d-138">Эта ссылка приведет к вызову страницы с именем *делетемовие* и передаче ей идентификатора выбранного фильма.</span><span class="sxs-lookup"><span data-stu-id="a240d-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="a240d-139">В этом учебнике не будет подробно рассмотрено, как создается эта ссылка, так как она почти идентична ссылке **Edit** из предыдущего руководства ([Обновление данных базы данных в веб-страницы ASP.NET](updating-data.md)).</span><span class="sxs-lookup"><span data-stu-id="a240d-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="a240d-140">Создание страницы удаления</span><span class="sxs-lookup"><span data-stu-id="a240d-140">Creating the Delete Page</span></span>

<span data-ttu-id="a240d-141">Теперь можно создать страницу, которая будет целевым объектом для ссылки **Delete** в сетке.</span><span class="sxs-lookup"><span data-stu-id="a240d-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a240d-142">**Важно!** Метод сначала выбирает удаляемую запись, а затем использует отдельную страницу и кнопку для подтверждения того, что процесс чрезвычайно важен для обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="a240d-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="a240d-143">Как вы прочитали в предыдущих учебных курсах, внесение изменений на веб-сайт *всегда* должно выполняться с помощью формы &mdash; *то есть с* помощью операции HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a240d-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="a240d-144">Если вы сделали возможным изменение сайта просто щелкнув ссылку (то есть с помощью операции GET), пользователи смогут выполнять простые запросы к сайту и удалять данные.</span><span class="sxs-lookup"><span data-stu-id="a240d-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="a240d-145">Даже модуль поиска, который индексирует ваш сайт, может случайно удалить данные только по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="a240d-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="a240d-146">Когда приложение позволяет пользователям изменять запись, в любом случае необходимо предоставить пользователю запись для редактирования.</span><span class="sxs-lookup"><span data-stu-id="a240d-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="a240d-147">Но вы, возможно, пропустите этот шаг, чтобы удалить запись.</span><span class="sxs-lookup"><span data-stu-id="a240d-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="a240d-148">Но не пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="a240d-148">Don't skip that step, though.</span></span> <span data-ttu-id="a240d-149">(Кроме того, пользователям рекомендуется просматривать записи и подтверждать, что они удаляют записи, которые они предполагали.)</span><span class="sxs-lookup"><span data-stu-id="a240d-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="a240d-150">В последующем наборе руководств вы узнаете, как добавить функции входа в систему, чтобы пользователь мог выполнить вход перед удалением записи.</span><span class="sxs-lookup"><span data-stu-id="a240d-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>

<span data-ttu-id="a240d-151">Создайте страницу с именем *делетемовие. cshtml* и замените содержимое файла следующей разметкой:</span><span class="sxs-lookup"><span data-stu-id="a240d-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="a240d-152">Эта разметка похожа на страницы *едитмовие* , за исключением того, что вместо использования текстовых полей (`<input type="text">`) разметка включает `<span>` элементы.</span><span class="sxs-lookup"><span data-stu-id="a240d-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="a240d-153">Здесь нет ничего редактировать.</span><span class="sxs-lookup"><span data-stu-id="a240d-153">There's nothing here to edit.</span></span> <span data-ttu-id="a240d-154">Все, что нужно сделать, — отобразить сведения о фильме, чтобы пользователи могли убедиться, что они удаляют нужный фильм.</span><span class="sxs-lookup"><span data-stu-id="a240d-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="a240d-155">Разметка уже содержит ссылку, которая позволяет пользователю вернуться на страницу со списком фильмов.</span><span class="sxs-lookup"><span data-stu-id="a240d-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="a240d-156">Как и на странице *едитмовие* , идентификатор выбранного фильма хранится в скрытом поле.</span><span class="sxs-lookup"><span data-stu-id="a240d-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="a240d-157">(Он передается на страницу в первом месте как значение строки запроса). Есть `Html.ValidationSummary` вызов, который будет отображать ошибки проверки.</span><span class="sxs-lookup"><span data-stu-id="a240d-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="a240d-158">В этом случае ошибка может быть вызвана тем, что на страницу не был передан идентификатор фильма или что идентификатор фильма недопустим.</span><span class="sxs-lookup"><span data-stu-id="a240d-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="a240d-159">Такая ситуация может возникнуть, если кто-то запустил эту страницу без предварительного выбора фильма на странице *фильмов* .</span><span class="sxs-lookup"><span data-stu-id="a240d-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="a240d-160">Заголовок кнопки — **удалить фильм**, а его атрибут name имеет значение `buttonDelete`.</span><span class="sxs-lookup"><span data-stu-id="a240d-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="a240d-161">Атрибут `name` будет использоваться в коде для распознавания кнопки, которая отправила форму.</span><span class="sxs-lookup"><span data-stu-id="a240d-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="a240d-162">Вам потребуется написать код в 1) прочитать сведения о фильме при первом отображении страницы и 2) удалить фильм, когда пользователь нажмет кнопку.</span><span class="sxs-lookup"><span data-stu-id="a240d-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="a240d-163">Добавление кода для чтения одного фильма</span><span class="sxs-lookup"><span data-stu-id="a240d-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="a240d-164">В верхней части страницы *делетемовие. cshtml* добавьте следующий блок кода:</span><span class="sxs-lookup"><span data-stu-id="a240d-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="a240d-165">Эта разметка аналогична соответствующему коду на странице *едитмовие* .</span><span class="sxs-lookup"><span data-stu-id="a240d-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="a240d-166">Он получает идентификатор фильма из строки запроса и использует идентификатор для чтения записи из базы данных.</span><span class="sxs-lookup"><span data-stu-id="a240d-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="a240d-167">Код включает проверочный тест (`IsInt()` и `row != null`), чтобы убедиться, что идентификатор фильма, передаваемый на страницу, является допустимым.</span><span class="sxs-lookup"><span data-stu-id="a240d-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="a240d-168">Помните, что этот код должен выполняться только при первом запуске страницы.</span><span class="sxs-lookup"><span data-stu-id="a240d-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="a240d-169">Вы не хотите повторно считывать запись фильма из базы данных, когда пользователь нажимает кнопку **удалить фильм** .</span><span class="sxs-lookup"><span data-stu-id="a240d-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="a240d-170">Таким образом, код для чтения фильма находится внутри теста, который говорит `if(!IsPost)` &mdash; то есть, *Если запрос не является операцией POST (отправка формы)* .</span><span class="sxs-lookup"><span data-stu-id="a240d-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="a240d-171">Добавление кода для удаления выбранного фильма</span><span class="sxs-lookup"><span data-stu-id="a240d-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="a240d-172">Чтобы удалить фильм при нажатии кнопки, добавьте следующий код непосредственно в закрывающую фигурную скобку блока `@`:</span><span class="sxs-lookup"><span data-stu-id="a240d-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="a240d-173">Этот код похож на код для обновления существующей записи, но проще.</span><span class="sxs-lookup"><span data-stu-id="a240d-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="a240d-174">Код, по сути, выполняет инструкцию SQL `Delete`.</span><span class="sxs-lookup"><span data-stu-id="a240d-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="a240d-175">Как и на странице *едитмовие* , код находится в блоке `if(IsPost)`.</span><span class="sxs-lookup"><span data-stu-id="a240d-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="a240d-176">На этот раз `if()` условие немного сложнее:</span><span class="sxs-lookup"><span data-stu-id="a240d-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="a240d-177">Здесь есть два условия.</span><span class="sxs-lookup"><span data-stu-id="a240d-177">There are two conditions here.</span></span> <span data-ttu-id="a240d-178">Первый заключается в том, что страница отправляется, как показано выше &mdash; `if(IsPost)`.</span><span class="sxs-lookup"><span data-stu-id="a240d-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="a240d-179">Второе условие — `!Request["buttonDelete"].IsEmpty()`, то есть запрос содержит объект с именем `buttonDelete`.</span><span class="sxs-lookup"><span data-stu-id="a240d-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="a240d-180">Разумеется, это косвенный способ проверки того, какая кнопка отправила форму.</span><span class="sxs-lookup"><span data-stu-id="a240d-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="a240d-181">Если форма содержит несколько кнопок отправки, в запросе отображается только имя кнопки, которая была нажата.</span><span class="sxs-lookup"><span data-stu-id="a240d-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="a240d-182">Таким образом, логически, если имя определенной кнопки появляется в запросе &mdash; или как указано в коде, если эта кнопка не пуста &mdash; это кнопка, которая отправляла форму.</span><span class="sxs-lookup"><span data-stu-id="a240d-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="a240d-183">Оператор `&&` означает "and" (логическое и).</span><span class="sxs-lookup"><span data-stu-id="a240d-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="a240d-184">Таким образом, все `if` условие имеет значение...</span><span class="sxs-lookup"><span data-stu-id="a240d-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="a240d-185">*Этот запрос является сообщением POST (не запросом в первый раз)*</span><span class="sxs-lookup"><span data-stu-id="a240d-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="a240d-186">AND</span><span class="sxs-lookup"><span data-stu-id="a240d-186">AND</span></span>  
  
<span data-ttu-id="a240d-187">Кнопка `buttonDelete`*была отправлена в форму.*</span><span class="sxs-lookup"><span data-stu-id="a240d-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="a240d-188">Эта форма (на самом деле, эта страница) содержит только одну кнопку, поэтому дополнительный тест `buttonDelete` технически не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="a240d-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="a240d-189">Тем не менее вы собираетесь выполнить операцию, которая будет окончательно удалять данные.</span><span class="sxs-lookup"><span data-stu-id="a240d-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="a240d-190">Так что вы должны быть уверены, что операция выполняется только в том случае, если пользователь явно запросил ее.</span><span class="sxs-lookup"><span data-stu-id="a240d-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="a240d-191">Например, предположим, что вы развернули эту страницу позже и добавили в нее другие кнопки.</span><span class="sxs-lookup"><span data-stu-id="a240d-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="a240d-192">Даже после этого код, который удаляет фильм, будет выполняться только в том случае, если была нажата кнопка `buttonDelete`.</span><span class="sxs-lookup"><span data-stu-id="a240d-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="a240d-193">Как и на странице *едитмовие* , вы получаете идентификатор из скрытого поля, а затем выполняете команду SQL.</span><span class="sxs-lookup"><span data-stu-id="a240d-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="a240d-194">Синтаксис инструкции `Delete`:</span><span class="sxs-lookup"><span data-stu-id="a240d-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="a240d-195">Крайне важно включать предложение `WHERE` и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="a240d-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="a240d-196">Если оставить предложение WHERE, *все записи в таблице будут удалены*.</span><span class="sxs-lookup"><span data-stu-id="a240d-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="a240d-197">Как вы видите, значение идентификатора передается команде SQL с помощью заполнителя.</span><span class="sxs-lookup"><span data-stu-id="a240d-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="a240d-198">Тестирование процесса удаления фильма</span><span class="sxs-lookup"><span data-stu-id="a240d-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="a240d-199">Теперь можно протестировать.</span><span class="sxs-lookup"><span data-stu-id="a240d-199">Now you can test.</span></span> <span data-ttu-id="a240d-200">Запустите страницу *фильмов* и щелкните **Удалить** рядом с фильмом.</span><span class="sxs-lookup"><span data-stu-id="a240d-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="a240d-201">Когда появится страница *делетемовие* , щелкните **удалить фильм**.</span><span class="sxs-lookup"><span data-stu-id="a240d-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![Удаление страницы фильма с выделенной кнопкой "удалить фильм"](deleting-data/_static/image4.png)

<span data-ttu-id="a240d-203">При нажатии кнопки код удаляет фильмы и возвращает их в список фильмов.</span><span class="sxs-lookup"><span data-stu-id="a240d-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="a240d-204">Там можно найти удаленный фильм и убедиться, что он был удален.</span><span class="sxs-lookup"><span data-stu-id="a240d-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="a240d-205">Далее</span><span class="sxs-lookup"><span data-stu-id="a240d-205">Coming Up Next</span></span>

<span data-ttu-id="a240d-206">В следующем учебнике показано, как дать всем страницам на сайте общий вид и макет.</span><span class="sxs-lookup"><span data-stu-id="a240d-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="a240d-207">Полный список для страницы фильмов (обновляется ссылками для удаления)</span><span class="sxs-lookup"><span data-stu-id="a240d-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="a240d-208">Полный список для страницы Делетемовие</span><span class="sxs-lookup"><span data-stu-id="a240d-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="a240d-209">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a240d-209">Additional Resources</span></span>

- [<span data-ttu-id="a240d-210">Введение в веб-программирование ASP.NET с помощью синтаксиса Razor</span><span class="sxs-lookup"><span data-stu-id="a240d-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="a240d-211">[Инструкция SQL DELETE](http://www.w3schools.com/sql/sql_delete.asp) на сайте W3Schools</span><span class="sxs-lookup"><span data-stu-id="a240d-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a240d-212">[Назад](updating-data.md)
> [Вперед](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="a240d-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
