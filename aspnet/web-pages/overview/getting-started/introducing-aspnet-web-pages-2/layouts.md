---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: Введение в веб-страницы ASP.NET создания единообразного макета | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике показано, как использовать макеты для создания единообразного вида страниц на сайте, который использует веб-страницы ASP.NET. Предполагается, что вы завершили...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422748"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="c1ab9-104">Введение в веб-страницы ASP.NET — создание единообразного макета</span><span class="sxs-lookup"><span data-stu-id="c1ab9-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>

<span data-ttu-id="c1ab9-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c1ab9-106">В этом учебнике показано, как использовать *макеты* для создания единообразного вида страниц на сайте, который использует веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="c1ab9-107">Предполагается, что вы выполнили серию, [удалив данные базы данных в веб-страницы ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251584).</span><span class="sxs-lookup"><span data-stu-id="c1ab9-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="c1ab9-108">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c1ab9-109">Что такое страница макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-109">What a layout page is.</span></span>
> - <span data-ttu-id="c1ab9-110">Объединение страниц макета с динамическим содержимым.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="c1ab9-111">Передача значений на страницу макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-111">How to pass values to a layout page.</span></span>

## <a name="about-layouts"></a><span data-ttu-id="c1ab9-112">О макетах</span><span class="sxs-lookup"><span data-stu-id="c1ab9-112">About Layouts</span></span>

<span data-ttu-id="c1ab9-113">Страницы, созданные до сих пор, полностью готовы, являются автономными страницами.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="c1ab9-114">Все они принадлежат одному сайту, но у них нет общих элементов или стандартного вида.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="c1ab9-115">У большинства веб-сайтов есть единообразный внешний вид и макет.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="c1ab9-116">Например, если вы перейдете на сайт [Microsoft.com/Web](https://www.microsoft.com/web/) и пройдете, вы увидите, что все страницы соответствуют общему макету и визуальной теме:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![Страница сайта Microsoft.com/web, отображающая макет заголовка, области навигации, области содержимого и нижнего колонтитула](layouts/_static/image1.png)

<span data-ttu-id="c1ab9-118">*Неэффективным* способом создания такого макета является определение заголовка, панели навигации и нижнего колонтитула отдельно для каждой страницы.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="c1ab9-119">Вы бы могли дублировать одну и ту же разметку каждый раз.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="c1ab9-120">Если вы хотите изменить что-нибудь (например, обновить нижний колонтитул), придется отдельно изменить каждую страницу.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="c1ab9-121">Именно здесь поступают *страницы макета* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="c1ab9-122">В веб-страницы ASP.NET можно определить страницу макета, которая предоставляет общий контейнер для страниц сайта.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="c1ab9-123">Например, страница макета может содержать заголовок, область навигации и нижний колонтитул.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="c1ab9-124">Страница макета содержит заполнитель, в котором происходит основное содержимое.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="c1ab9-125">Затем можно определить отдельные страницы содержимого, содержащие разметку и код только для этой страницы.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="c1ab9-126">Страницы содержимого не обязательно должны быть полными HTML-страницами; они даже не обязательно должны иметь элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="c1ab9-127">Они также содержат строку кода, сообщающую ASP.NET, в какой странице макета нужно отображать содержимое.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="c1ab9-128">Вот рисунок, на котором показано, как работает эта связь:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-128">Here's a picture that shows roughly how this relationship works:</span></span>

![Концептуальная схема, на которой показаны две страницы содержимого и страница макета, в которой они размещены](layouts/_static/image2.png)

<span data-ttu-id="c1ab9-130">Это взаимодействие легко понять, когда вы видите его в действии.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="c1ab9-131">В этом руководстве вы измените страницы фильмов, чтобы они использовали макет.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="c1ab9-132">Добавление страницы макета</span><span class="sxs-lookup"><span data-stu-id="c1ab9-132">Adding a Layout Page</span></span>

<span data-ttu-id="c1ab9-133">Начнем с создания страницы макета, которая определяет типичный макет страницы с заголовком, нижним колонтитулом и областью для основного содержимого.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="c1ab9-134">На сайте Вебпажесмовиес добавьте страницу CSHTML с именем *\_Layout. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="c1ab9-135">Знак подчеркивания в начале (`_`) важен.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="c1ab9-136">Если имя страницы начинается с символа подчеркивания, ASP.NET не будет напрямую передавать эту страницу в браузер.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="c1ab9-137">Это соглашение позволяет определить страницы, необходимые для сайта, но пользователи не должны иметь возможность запрашивать их напрямую.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="c1ab9-138">Замените содержимое на странице следующим:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="c1ab9-139">Как видите, эта разметка — это просто HTML, который использует элементы `<div>` для определения трех разделов на странице плюс еще один элемент `<div>` для хранения трех разделов.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="c1ab9-140">Нижний колонтитул содержит несколько фрагментов кода Razor: `@DateTime.Now.Year`, который выводит текущий год в этом месте страницы.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="c1ab9-141">Обратите внимание, что имеется ссылка на таблицу стилей с именем *movies. CSS*.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="c1ab9-142">Таблица стилей — это место, где будут определены подробные сведения о физическом макете элементов.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="c1ab9-143">Вы создадите это чуть позже.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-143">You'll create that in a moment.</span></span>

<span data-ttu-id="c1ab9-144">Единственная необычная функция на этой странице *\_Layout. cshtml* — это `@Render.Body()`ая строка.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="c1ab9-145">Это заполнитель, в котором содержимое будет передвигаться при слиянии макета с другой страницей.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="c1ab9-146">Добавление CSS-файла</span><span class="sxs-lookup"><span data-stu-id="c1ab9-146">Adding a .css File</span></span>

<span data-ttu-id="c1ab9-147">Предпочтительным способом определения фактического расположения (внешнего вида) элементов на странице является использование правил каскадной таблицы стилей (CSS).</span><span class="sxs-lookup"><span data-stu-id="c1ab9-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="c1ab9-148">Поэтому вы создадите *CSS* -файл с правилами для нового макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="c1ab9-149">В WebMatrix выберите корень сайта.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="c1ab9-150">Затем на вкладке " **файлы** " ленты щелкните стрелку под кнопкой **создать** и выберите пункт **создать папку**.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![Параметр "создать папку" в разделе "создать" на ленте.](layouts/_static/image3.png)

<span data-ttu-id="c1ab9-152">Назовите новые *стили*папок.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-152">Name the new folder *Styles*.</span></span>

![Присвоение имени новой папке Styles](layouts/_static/image4.png)

<span data-ttu-id="c1ab9-154">В папке New *styles* (новые стили) создайте файл с именем *movies. CSS*.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![Создание файла movies. CSS](layouts/_static/image5.png)

<span data-ttu-id="c1ab9-156">Замените содержимое нового *CSS* файл следующим:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="c1ab9-157">Мы не будем говорить о таких правилах CSS, за исключением того, что обратите внимание на две вещи.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="c1ab9-158">Один из них заключается в том, что в дополнение к установке шрифтов и размеров правила используют абсолютное позиционирование для определения расположения верхнего, нижнего колонтитула и области основного содержимого.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="c1ab9-159">Если вы не знакомы с размещением в CSS, то можете ознакомиться с руководством по [размещению CSS](http://www.w3schools.com/css/css_positioning.asp) на сайте W3Schools.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="c1ab9-160">Обратите внимание, что в нижней части мы скопировали правила стилей, которые изначально были определены по отдельности, в файле *movies. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="c1ab9-161">Эти правила использовались во [введении для отображения данных с помощью веб-страницы ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251580) учебнике, чтобы сделать `WebGrid` вспомогательным модулем визуализации разметки, которая добавила в таблицу полосы.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="c1ab9-162">(Если вы собираетесь использовать *CSS* -файл для определения стиля, можно также разместить правила стилей для всего сайта в нем.)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="c1ab9-163">Обновление файла фильмов для использования макета</span><span class="sxs-lookup"><span data-stu-id="c1ab9-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="c1ab9-164">Теперь можно обновить существующие файлы на сайте, чтобы использовать новый макет.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="c1ab9-165">Откройте файл *movies. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="c1ab9-166">В верхней части, как первая строка кода, добавьте следующее:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="c1ab9-167">Теперь страница запускается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="c1ab9-168">Эта одна строка кода сообщает ASP.NET, что при запуске страницы *фильмов* ее следует объединить с файлом *\_Layout. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="c1ab9-169">Так как файл *movies. cshtml* теперь использует страницу макета, вы можете удалить разметку из страницы *movies. cshtml* , которую позаботится файл *\_Layout. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="c1ab9-170">Выйдите `<!DOCTYPE>`, `<html>`и `<body>` открывающие и закрывающие теги.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="c1ab9-171">Извлекайте весь элемент `<head>` и его содержимое, в том числе правила стилей для сетки, так как теперь эти правила имеются в *CSS* -файле.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="c1ab9-172">Когда Вы находитесь на нем, измените существующий элемент `<h1>` на элемент `<h2>`. на странице макета уже имеется элемент `<h1>`.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="c1ab9-173">Измените `<h2>` текст на "список фильмов".</span><span class="sxs-lookup"><span data-stu-id="c1ab9-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="c1ab9-174">Обычно вам не придется вносить такие изменения на странице содержимого.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="c1ab9-175">При запуске сайта с помощью страницы макета создаются страницы содержимого без всех этих элементов.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="c1ab9-176">Однако в данном случае вы преобразуете автономную страницу в ту, которая использует макет, поэтому существует немного очистки.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="c1ab9-177">По завершении страница *movies. cshtml* будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="c1ab9-178">Тестирование макета</span><span class="sxs-lookup"><span data-stu-id="c1ab9-178">Testing the Layout</span></span>

<span data-ttu-id="c1ab9-179">Теперь можно увидеть, как выглядит макет.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="c1ab9-180">В WebMatrix щелкните правой кнопкой мыши страницу *movies. cshtml* и выберите **запустить в браузере**.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="c1ab9-181">При отображении страницы браузер выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-181">When the browser displays the page, it looks like this page:</span></span>

![Страница фильмов, подготовленная к просмотру с помощью макета](layouts/_static/image6.png)

<span data-ttu-id="c1ab9-183">ASP.NET объединила содержимое страницы movies. cshtml на странице *\_Layout. cshtml* справа, где метод `RenderBody` имеет значение.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="c1ab9-184">И, конечно, страница *\_Layout. cshtml* ссылается на *CSS* -файл, определяющий внешний вид страницы.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="c1ab9-185">Обновление страницы Аддмовие для использования макета</span><span class="sxs-lookup"><span data-stu-id="c1ab9-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="c1ab9-186">Реальное преимущество макетов заключается в том, что их можно использовать для всех страниц сайта.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="c1ab9-187">Откройте страницу *аддмовие. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="c1ab9-188">Возможно, вы помните, что на странице *аддмовие. cshtml* изначально существовали некоторые правила CSS для определения вида сообщений об ошибках проверки.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="c1ab9-189">Так как у вас уже есть *CSS* -файл для сайта, можно переместить эти правила в файл *CSS* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="c1ab9-190">Удалите их из файла *аддмовие. cshtml* и добавьте их в конец файла *movies. CSS* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="c1ab9-191">Вы перемещаете следующие правила:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="c1ab9-192">Теперь внесите те же изменения в *аддмовие. cshtml* , что и для *фильмов. cshtml* — добавьте `Layout="~/_Layout.cshtml;` и удалите разметку HTML, которая теперь является лишней.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="c1ab9-193">Измените элемент `<h1>` на `<h2>`.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="c1ab9-194">По завершении страница будет выглядеть, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="c1ab9-195">Запустите страницу.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-195">Run the page.</span></span> <span data-ttu-id="c1ab9-196">Теперь он выглядит так:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-196">Now it looks like this illustration:</span></span>

![Страница "Добавление фильмов", отображаемая с помощью макета](layouts/_static/image7.png)

<span data-ttu-id="c1ab9-198">Необходимо внести аналогичные изменения в страницы сайта — *едитмовие. cshtml* и *делетемовие. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="c1ab9-199">Однако перед этим можно внести еще одно изменение в макет, что сделает его более гибким.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="c1ab9-200">Передача сведений о названии на страницу макета</span><span class="sxs-lookup"><span data-stu-id="c1ab9-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="c1ab9-201">Созданная страница *\_Layout. cshtml* содержит элемент `<title>`, для которого задано значение "мой сайт фильма".</span><span class="sxs-lookup"><span data-stu-id="c1ab9-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="c1ab9-202">В большинстве браузеров содержимое этого элемента отображается в виде текста на вкладке:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-202">Most browsers display the content of this element as the text on a tab:</span></span>

![Элемент&gt; заголовка &lt;страницы, отображаемый на вкладке браузера](layouts/_static/image8.png)

<span data-ttu-id="c1ab9-204">Эти сведения о заголовке являются универсальными.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-204">This title information is generic.</span></span> <span data-ttu-id="c1ab9-205">Предположим, что текст заголовка должен быть более специфичным для текущей страницы.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="c1ab9-206">(Текст заголовка также используется поисковыми механизмами для определения того, что собирается ваша страница.) Вы можете передать сведения со страницы содержимого, например *movies. cshtml* или *аддмовие. cshtml* , на страницу макета, а затем использовать эту информацию для настройки отрисовки страницы макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="c1ab9-207">Снова откройте страницу *movies. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="c1ab9-208">В верхней части кода добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="c1ab9-209">Объект `Page` доступен на всех страницах *. cshtml* и предназначен для этой цели, а именно для обмена информацией между страницей и ее макетом.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="c1ab9-210">Откройте страницу *\_Layout. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-210">Open the *\_Layout.cshtml* page.</span></span> <span data-ttu-id="c1ab9-211">Измените элемент `<title>` так, чтобы он выглядел как в этой разметке:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="c1ab9-212">Этот код визуализирует все, что находится в свойстве `Page.Title`, прямо в этом месте страницы.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="c1ab9-213">Запустите страницу *movies. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="c1ab9-214">На этот раз вкладка Браузер показывает, что передано в качестве значения `Page.Title`:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![Вкладка браузера, в которой отображается заголовок, созданный динамически](layouts/_static/image9.png)

<span data-ttu-id="c1ab9-216">При необходимости просмотрите исходный код страницы в браузере.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="c1ab9-217">Видно, что элемент `<title>` подготавливается к просмотру как `<title>List Movies</title>`.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="c1ab9-218">**Объект Page**</span><span class="sxs-lookup"><span data-stu-id="c1ab9-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="c1ab9-219">Полезной функцией `Page` является то, что это динамический объект, а свойство `Title` не является фиксированным или зарезервированным именем.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="c1ab9-220">Для значения объекта `Page` можно использовать *любое* имя.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="c1ab9-221">Например, можно легко передать заголовок, используя свойство с именем `Page.CurrentName` или `Page.MyPage`.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="c1ab9-222">Единственное ограничение заключается в том, что имя должно соответствовать обычным правилам, для которых можно назвать свойства.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="c1ab9-223">(Например, имя не может содержать пробелы.)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="c1ab9-224">Можно передать любое количество значений с помощью объекта `Page`.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="c1ab9-225">Если вы хотите передать сведения о фильме на страницу макета, можно передать значения, используя `Page.MovieTitle` и `Page.Genre` и `Page.MovieYear`.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="c1ab9-226">(Или любые другие имена, которые вы вымышлены для хранения информации.) Единственное требование, которое, вероятно, очевидно, заключается в том, что необходимо использовать те же имена на странице содержимого и на странице макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="c1ab9-227">Данные, передаваемые с помощью объекта `Page`, не ограничиваются только текстом, отображаемым на странице макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="c1ab9-228">Можно передать значение на страницу макета, а затем код на странице макета может использовать значение для принятия решения о том, следует ли отображать раздел страницы, какой *CSS* -файл использовать и т. д.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="c1ab9-229">Значения, передаваемые в объект `Page`, аналогичны любым другим значениям, используемым в коде.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="c1ab9-230">Это просто то, что значения происходят на странице содержимого и передаются на страницу макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>

<span data-ttu-id="c1ab9-231">Откройте страницу *аддмовие. cshtml* и добавьте в начало кода строку, которая содержит название страницы *аддмовие. cshtml* :</span><span class="sxs-lookup"><span data-stu-id="c1ab9-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="c1ab9-232">Запустите страницу *аддмовие. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c1ab9-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="c1ab9-233">Вы увидите новый заголовок:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-233">You see the new title there:</span></span>

![Вкладка браузера с динамическим созданием заголовка "Добавление фильмов"](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="c1ab9-235">Обновление оставшихся страниц для использования макета</span><span class="sxs-lookup"><span data-stu-id="c1ab9-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="c1ab9-236">Теперь можно завершить оставшиеся страницы сайта, чтобы они использовали новый макет.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="c1ab9-237">В свою очередь откройте *едитмовие. cshtml* и *делетемовие. cshtml* и внесите в них одинаковые изменения.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="c1ab9-238">Добавьте строку кода, которая ссылается на страницу макета:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="c1ab9-239">Добавьте строку, чтобы задать заголовок страницы:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="c1ab9-240">или:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="c1ab9-241">Удалите всю избыточную HTML-разметку — по сути, оставьте только биты внутри элемента `<body>` (плюс блок кода вверху).</span><span class="sxs-lookup"><span data-stu-id="c1ab9-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="c1ab9-242">Измените элемент `<h1>`, чтобы он был элементом `<h2>`.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="c1ab9-243">После внесения этих изменений проверьте каждый из них и убедитесь, что они отображаются правильно, а заголовок задан правильно.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="c1ab9-244">Описание идей по страницам макета</span><span class="sxs-lookup"><span data-stu-id="c1ab9-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="c1ab9-245">В этом учебнике вы создали страницу *\_Layout. cshtml* и использовали метод `RenderBody` для слияния содержимого из другой страницы.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="c1ab9-246">Это базовый шаблон для использования макетов на веб-страницах.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="c1ab9-247">Страницы макета имеют дополнительные функции, которые мы не можем обнаружить.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="c1ab9-248">Например, можно вложить страницы макета — одна страница макета может в свою очередь ссылаться на другую.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="c1ab9-249">Вложенные макеты могут быть полезны при работе с подразделами сайта, для которых требуются разные макеты.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="c1ab9-250">Кроме того, можно использовать дополнительные методы (например, `RenderSection`) для настройки именованных разделов на странице макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="c1ab9-251">Сочетание страниц макета и *CSS* -файлов является мощным.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="c1ab9-252">Как вы увидите в следующем ряде руководств, в WebMatrix можно создать сайт на основе *шаблона*, который предоставляет сайт с предварительно созданными функциями.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="c1ab9-253">Шаблоны хорошо используют страницы макета и CSS для создания веб-сайтов, которые выглядят великолепно и имеют такие функции, как меню.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="c1ab9-254">Ниже приведен снимок экрана домашней страницы с сайта на основе шаблона, в котором отображаются функции, использующие страницы макета и CSS:</span><span class="sxs-lookup"><span data-stu-id="c1ab9-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![Макет, созданный шаблоном сайта WebMatrix с отображением заголовка, области навигации, области содержимого, необязательного раздела и ссылок для входа](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="c1ab9-256">Полный список для страницы фильмов (обновлен для использования страницы макета)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="c1ab9-257">Полный список страниц для страницы "Добавление фильма" (обновлен для макета)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="c1ab9-258">Полный список страниц для страницы удаления фильмов (обновлен для макета)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="c1ab9-259">Полный список страниц для страницы "изменение фильма" (обновлен для макета)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="c1ab9-260">Далее</span><span class="sxs-lookup"><span data-stu-id="c1ab9-260">Coming Up Next</span></span>

<span data-ttu-id="c1ab9-261">В следующем руководстве вы узнаете, как опубликовать свой сайт в Интернете, чтобы все пользователи могли его видеть.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c1ab9-262">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c1ab9-262">Additional Resources</span></span>

- <span data-ttu-id="c1ab9-263">[Создание единообразного внешнего вида](https://go.microsoft.com/fwlink/?LinkID=202891) — статья, которая предоставляет более подробные сведения о работе с макетами.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="c1ab9-264">Здесь также описано, как передать значение на страницу макета, которая показывает или скрывает часть содержимого.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="c1ab9-265">[Вложенные страницы макета с Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Майк бринд в блогах пример того, как вкладывать страницы макета.</span><span class="sxs-lookup"><span data-stu-id="c1ab9-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="c1ab9-266">(Содержит загрузку страниц.)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c1ab9-267">[Назад](deleting-data.md)
> [Вперед](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="c1ab9-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
