---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: Часть 3. представления и ViewModels | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. В части 3 представлены представления и ViewModels.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451134"
---
# <a name="part-3-views-and-viewmodels"></a><span data-ttu-id="9f6c8-104">Часть 3. представления и ViewModels</span><span class="sxs-lookup"><span data-stu-id="9f6c8-104">Part 3: Views and ViewModels</span></span>

<span data-ttu-id="9f6c8-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="9f6c8-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="9f6c8-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="9f6c8-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="9f6c8-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="9f6c8-109">В части 3 представлены представления и ViewModels.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-109">Part 3 covers Views and ViewModels.</span></span>

<span data-ttu-id="9f6c8-110">Пока мы только что возвращали строки из действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="9f6c8-111">Это удобный способ понять, как работают контроллеры, но это не то, как вы хотите создать реальное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="9f6c8-112">Нам нужен лучший способ создания HTML-кода обратно в браузерах, посещающих наш сайт. он позволяет использовать файлы шаблонов для упрощения настройки обратной передачи содержимого HTML.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="9f6c8-113">Именно это и есть представления.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="9f6c8-114">Добавление шаблона представления</span><span class="sxs-lookup"><span data-stu-id="9f6c8-114">Adding a View template</span></span>

<span data-ttu-id="9f6c8-115">Чтобы использовать шаблон представления, мы изменим метод индекса HomeController, чтобы он возвращал ActionResult, и имел возвращаемое представление (), как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="9f6c8-116">Приведенное выше изменение указывает, что вместо возврата строки мы хотим использовать "View" для создания результата.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="9f6c8-117">Теперь мы добавим в наш проект соответствующий шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="9f6c8-118">Для этого поместите текстовый курсор в метод действия индекса, щелкните его правой кнопкой мыши и выберите "добавить представление".</span><span class="sxs-lookup"><span data-stu-id="9f6c8-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="9f6c8-119">Откроется диалоговое окно Добавление представления:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="9f6c8-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9f6c8-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="9f6c8-121">Диалоговое окно "Добавление представления" позволяет быстро и легко создавать файлы шаблонов представления.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="9f6c8-122">По умолчанию диалоговое окно "добавить представление" предварительно заполняет имя создаваемого шаблона представления, чтобы оно соответствовало тому методу действия, который будет его использовать.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="9f6c8-123">Так как мы использовали контекстное меню "добавить представление" в методе действия Index () нашего HomeController, в диалоговом окне "добавить представление" выше указано "index", как имя представления, предварительно заполненное по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="9f6c8-124">Изменять параметры этого диалогового окна не требуется, поэтому нажмите кнопку Добавить.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="9f6c8-125">При нажатии кнопки Добавить Visual Web Developer создаст новый шаблон представления index. cshtml для нас в каталоге \Виевс\хоме, создавая папку, если она еще не создана.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="9f6c8-126">Имя и расположение папки в файле index. cshtml важны и следуют соглашениям об именовании ASP.NET MVC по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="9f6c8-127">Имя каталога \Виевс\хоме соответствует контроллеру, который называется HomeController.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="9f6c8-128">Имя шаблона представления — index соответствует методу действия контроллера, который будет отображать представление.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="9f6c8-129">ASP.NET MVC позволяет нам избегать явного указания имени или расположения шаблона представления при использовании этого соглашения об именовании для возвращения представления.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="9f6c8-130">По умолчанию шаблон представления \Виевс\хоме\индекс.кштмл отображается при написании кода, подобного приведенному ниже, в HomeController:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="9f6c8-131">Visual Web Developer создал и открыл шаблон представления index. cshtml после нажатия кнопки "Добавить" в диалоговом окне "Добавление представления".</span><span class="sxs-lookup"><span data-stu-id="9f6c8-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="9f6c8-132">Содержимое index. cshtml показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="9f6c8-133">Это представление использует синтаксис Razor, что более наглядно, чем обработчик представлений веб-форм, используемый в веб-формах ASP.NET и предыдущих версиях ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="9f6c8-134">Обработчик представлений веб-форм по-прежнему доступен в ASP.NET MVC 3, но многие разработчики обнаружили, что подсистема представлений Razor очень хорошо подходит для разработки ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="9f6c8-135">Первые три строки задают заголовок страницы с помощью ViewBag. Title.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="9f6c8-136">Мы рассмотрим, как это работает в ближайшее время, но сначала будем обновлять текст заголовка текста и просматривать страницу.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="9f6c8-137">Обновите тег &lt;H2&gt;, чтобы сказать: «это Домашняя страница», как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="9f6c8-138">При запуске приложения отображается новый текст, отображаемый на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="9f6c8-139">Использование макета для общих элементов сайта</span><span class="sxs-lookup"><span data-stu-id="9f6c8-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="9f6c8-140">Большинство веб-сайтов имеют содержимое, которое совместно используется несколькими страницами: Навигация, нижние колонтитулы, изображения логотипа, ссылки на таблицы стилей и т. д. Подсистема представлений Razor упрощает управление с помощью страницы с именем \_Layout. cshtml, которая автоматически создается для нас в папке/Виевс/Шаред.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="9f6c8-141">Дважды щелкните эту папку, чтобы просмотреть ее содержимое, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="9f6c8-142">Содержимое наших индивидуальных представлений будет отображаться командой @RenderBody() и любым общим содержимым, которое мы хотим использовать вне области, которое можно добавить в разметку \_Layout. cshtml.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="9f6c8-143">Нам потребуется, чтобы в нашем музыкальном магазине MVC имелся общий заголовок со ссылками на нашу домашнюю страницу и область хранения на всех страницах сайта, поэтому мы добавим его в шаблон непосредственно перед инструкцией @RenderBody().</span><span class="sxs-lookup"><span data-stu-id="9f6c8-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="9f6c8-144">Обновление таблицы стилей</span><span class="sxs-lookup"><span data-stu-id="9f6c8-144">Updating the StyleSheet</span></span>

<span data-ttu-id="9f6c8-145">Шаблон пустого проекта содержит очень упрощенный файл CSS, который содержит только стили, используемые для вывода сообщений проверки.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="9f6c8-146">Наш конструктор предоставил некоторые дополнительные CSS и изображения для определения внешнего вида и оформления нашего веб-узла, поэтому мы добавим их сейчас.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="9f6c8-147">Обновленный файл CSS и изображения включены в каталог содержимого Мвкмусиксторе-Ассетс. zip, который доступен в [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="9f6c8-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="9f6c8-148">Мы выберем оба из них в проводнике Windows и разместите их в папке содержимого нашего решения в Visual Web Developer, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="9f6c8-149">Вам будет предложено подтвердить, нужно ли перезаписать существующий файл Site. CSS.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="9f6c8-150">Нажмите кнопку Да.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="9f6c8-151">Теперь папка содержимого приложения будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="9f6c8-152">Теперь выполним запуск приложения и посмотрим, как наши изменения выглядят на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="9f6c8-153">Давайте посмотрим, что изменилось: метод действия индекса HomeController, найденный и отображающий шаблон \Виевс\хоме\индекс.кштмлвиев, несмотря на то, что наш код называется «Return View ()», так как наш шаблон представления, за которым следует стандартное соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="9f6c8-154">На домашней странице отображается простое приветственное сообщение, которое определено в шаблоне представления \Виевс\хоме\индекс.кштмл.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="9f6c8-155">Домашняя страница использует наш шаблон \_Layout. cshtml, поэтому приветственное сообщение содержится в макете HTML для стандартного сайта.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="9f6c8-156">Использование модели для передачи информации в наше представление</span><span class="sxs-lookup"><span data-stu-id="9f6c8-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="9f6c8-157">Шаблон представления, который просто отображает жестко закодированный код HTML, не будет создавать очень интересный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="9f6c8-158">Чтобы создать динамический веб-сайт, мы хотим передать информацию из наших действий контроллера в шаблоны представлений.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="9f6c8-159">В шаблоне модель-представление-контроллер термин модель относится к объектам, которые представляют данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="9f6c8-160">Часто объекты модели соответствуют таблицам в базе данных, но им не нужно.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="9f6c8-161">Методы действия контроллера, возвращающие ActionResult, могут передавать объект модели в представление.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="9f6c8-162">Это позволяет контроллеру очищать всю информацию, необходимую для создания ответа, а затем передавать эту информацию в шаблон представления для использования при формировании соответствующего HTML-ответа.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="9f6c8-163">Это проще понять, просматривая его в действии, поэтому приступим к работе.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="9f6c8-164">Сначала мы создадим некоторые классы модели для представления жанров и альбомов в магазине.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="9f6c8-165">Начнем с создания класса жанра.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="9f6c8-166">Щелкните правой кнопкой мыши папку Models в проекте, выберите пункт "добавить класс" и назовите файл "Genre.cs".</span><span class="sxs-lookup"><span data-stu-id="9f6c8-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="9f6c8-167">Затем добавьте свойство имени общедоступной строки в созданный класс:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="9f6c8-168">*Примечание. на случай, если вы заинтересовались, в нотации C#{Get; Set;} используется функция автоматического внедрения свойств. Это дает нам преимущества свойства, не требуя объявления резервного поля.*</span><span class="sxs-lookup"><span data-stu-id="9f6c8-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="9f6c8-169">Затем выполните те же действия, чтобы создать класс альбома (с именем Album.cs) с заголовком и свойством жанра:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="9f6c8-170">Теперь мы можем изменить Стореконтроллер, чтобы использовать представления, отображающие динамическую информацию из нашей модели.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="9f6c8-171">If-для демонстрационных целей прямо сейчас мы назвали наши альбомы на основе идентификатора запроса. Эти сведения можно отобразить, как показано в приведенном ниже представлении.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="9f6c8-172">Мы начнем с изменения действия Store Details, чтобы показать сведения об одном альбоме.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="9f6c8-173">Добавьте оператор "using" в начало класса **стореконтроллерс** , чтобы включить пространство имен Мвкмусиксторе. Models, поэтому нам не нужно вводить Мвкмусиксторе. Models. альбом каждый раз, когда нужно использовать класс альбома.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="9f6c8-174">Раздел "using" этого класса теперь должен выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="9f6c8-175">Далее мы изменим действие контроллера сведений таким образом, чтобы оно возвращало ActionResult, а не строку, как в случае с методом индекса HomeController.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="9f6c8-176">Теперь можно изменить логику, чтобы вернуть объект альбома в представление.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="9f6c8-177">Далее в этом учебнике мы будем получать данные из базы данных, но сейчас мы будем использовать фиктивные данные для начала работы.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="9f6c8-178">*Примечание. Если вы не знакомы с C#, можно предположить, что использование var означает, что наша переменная альбома имеет позднюю привязку. Это неверно: C# компилятор использует определение типа на основе того, что мы присваиваем переменной, чтобы определить, что альбом имеет тип "альбом" и компилирует переменную локального альбома в качестве типа альбома, поэтому мы получаем проверку во время компиляции и поддержку редактора кода Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="9f6c8-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="9f6c8-179">Теперь создадим шаблон представления, который использует наш альбом для создания ответа HTML.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="9f6c8-180">Прежде чем делать это, необходимо выполнить сборку проекта, чтобы диалоговое окно добавления представления знало о новом созданном классе альбома.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="9f6c8-181">Чтобы построить проект, выберите пункт меню Отладка ⇨ сборка Мвкмусиксторе (для дополнительного кредита можно использовать сочетание клавиш CTRL + SHIFT + B для построения проекта).</span><span class="sxs-lookup"><span data-stu-id="9f6c8-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="9f6c8-182">Теперь, когда мы настроили наши вспомогательные классы, мы готовы к созданию нашего шаблона представления.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="9f6c8-183">Щелкните правой кнопкой мыши в методе Details и выберите "добавить представление..." в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="9f6c8-184">Мы создадим новый шаблон представления, как мы делали раньше с HomeController.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="9f6c8-185">Так как мы создаем его из Стореконтроллер, он будет создан по умолчанию в \Виевс\сторе\индекс.кштмл-файле.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="9f6c8-186">В отличие от ранее, будет установлен флажок "создать строго типизированное представление".</span><span class="sxs-lookup"><span data-stu-id="9f6c8-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="9f6c8-187">Затем мы будем выбирать наш класс «альбом» в разделе «View Data-Class» Drop-довнлист.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="9f6c8-188">Это приведет к созданию в диалоговом окне "Добавление представления" шаблона представления, ожидающего, что объект альбома будет передан ему для использования.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="9f6c8-189">При нажатии кнопки "Добавить" будет создан шаблон представления \Виевс\сторе\детаилс.кштмл, содержащий следующий код.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="9f6c8-190">Обратите внимание на первую строку, которая указывает, что это представление строго типизировано для нашего класса альбома.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="9f6c8-191">Подсистема представления Razor понимает, что ей был передан объект альбома, поэтому мы можем легко получить доступ к свойствам модели и даже воспользоваться преимуществами IntelliSense в редакторе Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="9f6c8-192">Обновите тег &lt;H2&gt;, чтобы отобразить свойство заголовка альбома, изменив эту строку следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="9f6c8-193">Обратите внимание, что IntelliSense активируется при вводе точки после ключевого слова @Model, отображая свойства и методы, поддерживаемые классом альбома.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="9f6c8-194">Теперь повторно запустите наш проект и перейдите по URL-адресу/Store/Details/5.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="9f6c8-195">Мы увидим сведения о следующем альбоме, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="9f6c8-196">Теперь мы сделаем аналогичное обновление для метода действия обзора хранилища.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="9f6c8-197">Обновите метод, чтобы он возвращал ActionResult, и измените логику метода таким образом, чтобы он создавал новый объект жанра и возвращал его в представление.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="9f6c8-198">Щелкните правой кнопкой мыши метод browse и выберите "добавить представление..." в контекстном меню добавьте строго типизированное представление добавление строго типизированного в класс жанра.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="9f6c8-199">Обновите элемент &lt;H2&gt; в коде представления (в/Виевс/Сторе/бровсе.кштмл), чтобы отобразить сведения о жанре.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="9f6c8-200">Теперь перейдем к нашему проекту и перейду к/Сторе/бровсе? Жанр = URL-адрес Disco.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="9f6c8-201">Появится страница Обзор, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="9f6c8-202">Наконец, сделаем немного более сложное обновление метода действия **индекса Store** и просмотр, чтобы отобразить список всех жанров в нашем магазине.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="9f6c8-203">Это делается с помощью списка жанров в качестве объекта модели, а не только для одного жанра.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="9f6c8-204">Щелкните правой кнопкой мыши метод действия сохранить индекс и выберите Добавить представление как прежде, выберите жанр в качестве класса модели и нажмите кнопку Добавить.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="9f6c8-205">Сначала мы изменим объявление @model, чтобы указать, что представление будет ожидать несколько объектов жанра, а не только один.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="9f6c8-206">Измените первую строку/Сторе/индекс.кштмл на Read следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="9f6c8-207">Это указывает ядру представления Razor, что он будет работать с объектом модели, который может содержать несколько объектов-жанров.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="9f6c8-208">Мы используем&lt;жанра IEnumerable&gt; а не список&lt;жанр&gt;, так как он более универсальный, что позволяет нам изменить наш тип модели позже на любой тип объектов, поддерживающий интерфейс IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="9f6c8-209">Далее мы выполним перебор объектов жанра в модели, как показано в приведенном ниже коде представления.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="9f6c8-210">Обратите внимание, что у нас есть полная поддержка IntelliSense по мере ввода этого кода, поэтому при вводе «@Model».</span><span class="sxs-lookup"><span data-stu-id="9f6c8-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="9f6c8-211">Мы видим все методы и свойства, поддерживаемые IEnumerable типа жанра.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="9f6c8-212">В рамках цикла foreach Visual Web Developer знает, что каждый элемент относится к типу жанра, поэтому мы видим IntelliSense для каждого типа жанра.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSense for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="9f6c8-213">Затем функция формирования шаблонов проверила объект жанра и определила, что каждый из них будет иметь свойство Name, поэтому он просматривает и записывает их. Он также создает ссылки Edit, Details и DELETE для каждого отдельного элемента.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="9f6c8-214">Мы будем использовать их позже в нашем Менеджере магазина, но теперь нам хотелось бы иметь простой список.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="9f6c8-215">При запуске приложения и переходе к/Store видно, что отображается количество и список жанров.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="9f6c8-216">Добавление ссылок между страницами</span><span class="sxs-lookup"><span data-stu-id="9f6c8-216">Adding Links between pages</span></span>

<span data-ttu-id="9f6c8-217">Наш URL-адрес/Store, в котором в настоящее время перечислены жанры, просто отображает имена жанров простым текстом.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="9f6c8-218">Давайте изменим это так, чтобы вместо обычного текста имена жанров были связаны с соответствующим URL-адресом/Сторе/бровсе, поэтому при щелчке по жанру музыки, например "Disco", будет выполнен переход к URL-адресу/Сторе/бровсе? жанр = Disco.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="9f6c8-219">Мы можем обновить наш шаблон представления \Виевс\сторе\индекс.кштмл, чтобы вывести эти ссылки с помощью кода, как показано ниже **(не вводите это в, мы будем улучшать его)** :</span><span class="sxs-lookup"><span data-stu-id="9f6c8-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="9f6c8-220">Это работает, но может привести к возникновению проблем позже, так как оно полагается на жестко закодированную строку.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="9f6c8-221">Например, если мы хотим переименовать контроллер, нам придется искать ссылки, которые необходимо обновить, в нашем коде.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="9f6c8-222">Альтернативным подходом, который мы можем использовать, является использование преимуществ вспомогательного метода HTML.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="9f6c8-223">ASP.NET MVC включает вспомогательные методы HTML, доступные из нашего кода шаблона представления для выполнения различных распространенных задач, как это происходит.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="9f6c8-224">Вспомогательный метод HTML. ActionLink () особенно полезен и упрощает создание HTML-&lt;&gt; ссылок и позаботится о том, что URL-пути правильно кодируются URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="9f6c8-225">В HTML. ActionLink () имеется несколько различных перегрузок, позволяющих указать столько сведений, сколько требуется для ссылок.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="9f6c8-226">В самом простом случае вы получите только текст ссылки и метод действия, чтобы переходить по гиперссылке на клиенте.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="9f6c8-227">Например, можно создать ссылку на метод Index ()/Сторе/на странице сведений о магазине, щелкнув текст ссылки "переход к индексу магазина", используя следующий вызов:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="9f6c8-228">*Примечание. в этом случае нам не нужно указывать имя контроллера, так как мы просто связываемся с другим действием в том же контроллере, который готовит текущее представление.*</span><span class="sxs-lookup"><span data-stu-id="9f6c8-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="9f6c8-229">Однако наши ссылки на страницу обзора должны передать параметр, поэтому мы будем использовать другую перегрузку метода HTML. ActionLink, принимающую три параметра:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="9f6c8-230">Текст ссылки, в котором отображается название жанра</span><span class="sxs-lookup"><span data-stu-id="9f6c8-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="9f6c8-231">Имя действия контроллера (обзор)</span><span class="sxs-lookup"><span data-stu-id="9f6c8-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="9f6c8-232">Значения параметров маршрута, в которых указывается как имя (жанр), так и значение (название жанра).</span><span class="sxs-lookup"><span data-stu-id="9f6c8-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="9f6c8-233">Поместив все вместе, мы будем писать эти ссылки на представление индекса магазина:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="9f6c8-234">Теперь, когда мы снова выполним проект и доступ к URL-адресу/Сторе/, мы увидим список жанров.</span><span class="sxs-lookup"><span data-stu-id="9f6c8-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="9f6c8-235">Каждый жанр является гиперссылкой. когда вы ее щелкнули, мы отпустим свой URL-адрес/Сторе/бровсе? жанр = *[жанр]* .</span><span class="sxs-lookup"><span data-stu-id="9f6c8-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="9f6c8-236">HTML-код для списка жанров выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9f6c8-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> <span data-ttu-id="9f6c8-237">[Назад](mvc-music-store-part-2.md)
> [Вперед](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="9f6c8-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
