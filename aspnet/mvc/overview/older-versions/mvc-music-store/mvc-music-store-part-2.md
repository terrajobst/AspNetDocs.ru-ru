---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: Часть 2. контроллеры | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. Часть 2 охватывает контроллеры.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451194"
---
# <a name="part-2-controllers"></a><span data-ttu-id="83ed0-104">Часть 2. контроллеры</span><span class="sxs-lookup"><span data-stu-id="83ed0-104">Part 2: Controllers</span></span>

<span data-ttu-id="83ed0-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="83ed0-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="83ed0-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="83ed0-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="83ed0-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="83ed0-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="83ed0-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="83ed0-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="83ed0-109">Часть 2 охватывает контроллеры.</span><span class="sxs-lookup"><span data-stu-id="83ed0-109">Part 2 covers Controllers.</span></span>

<span data-ttu-id="83ed0-110">В традиционных веб-платформах входящие URL-адреса обычно сопоставлены с файлами на диске.</span><span class="sxs-lookup"><span data-stu-id="83ed0-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="83ed0-111">Например: запрос URL-адреса, например "/Продуктс.аспкс" или "/Продуктс.ФП", может обрабатываться файлом Products. aspx или Products. php.</span><span class="sxs-lookup"><span data-stu-id="83ed0-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="83ed0-112">Веб-платформы MVC сопоставляют URL-адреса с кодом сервера немного иным образом.</span><span class="sxs-lookup"><span data-stu-id="83ed0-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="83ed0-113">Вместо сопоставления входящих URL-адресов с файлами они вместо этого сопоставляют URL-адреса с методами в классах.</span><span class="sxs-lookup"><span data-stu-id="83ed0-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="83ed0-114">Эти классы называются "контроллерами", они отвечают за обработку входящих HTTP-запросов, обработку входных данных пользователя, получение и сохранение данных, а также определение ответа на отправку клиенту (отображение HTML-кода, скачивание файла, перенаправление в другой URL-адрес и т. д.).</span><span class="sxs-lookup"><span data-stu-id="83ed0-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="83ed0-115">Добавление HomeController</span><span class="sxs-lookup"><span data-stu-id="83ed0-115">Adding a HomeController</span></span>

<span data-ttu-id="83ed0-116">Мы начнем приложение музыкального магазина MVC, добавив класс контроллера, который будет работать с URL-адресами на домашней странице нашего сайта.</span><span class="sxs-lookup"><span data-stu-id="83ed0-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="83ed0-117">Мы будем следовать соглашениям об именовании ASP.NET MVC по умолчанию и назовем его HomeController.</span><span class="sxs-lookup"><span data-stu-id="83ed0-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="83ed0-118">Щелкните правой кнопкой мыши папку Controllers в обозреватель решений и выберите "Добавить", а затем — "контроллер...". кнопки</span><span class="sxs-lookup"><span data-stu-id="83ed0-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="83ed0-119">Откроется диалоговое окно "Добавление контроллера".</span><span class="sxs-lookup"><span data-stu-id="83ed0-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="83ed0-120">Присвойте контроллеру имя "HomeController" и нажмите кнопку Добавить.</span><span class="sxs-lookup"><span data-stu-id="83ed0-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="83ed0-121">Будет создан новый файл HomeController.cs со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="83ed0-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="83ed0-122">Чтобы начать как можно скорее, мы заменяем метод Index простым методом, который просто возвращает строку.</span><span class="sxs-lookup"><span data-stu-id="83ed0-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="83ed0-123">Мы сделаем два изменения:</span><span class="sxs-lookup"><span data-stu-id="83ed0-123">We'll make two changes:</span></span>

- <span data-ttu-id="83ed0-124">Измените метод, чтобы он возвращал строку, а не ActionResult</span><span class="sxs-lookup"><span data-stu-id="83ed0-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="83ed0-125">Измените оператор return, чтобы он возвращал "Привет от домашнего"</span><span class="sxs-lookup"><span data-stu-id="83ed0-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="83ed0-126">Теперь метод должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="83ed0-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="83ed0-127">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="83ed0-127">Running the Application</span></span>

<span data-ttu-id="83ed0-128">Теперь давайте запустим сайт.</span><span class="sxs-lookup"><span data-stu-id="83ed0-128">Now let's run the site.</span></span> <span data-ttu-id="83ed0-129">Мы можем запустить наш веб-сервер и испытать сайт, используя любой из следующих средств:</span><span class="sxs-lookup"><span data-stu-id="83ed0-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="83ed0-130">Выбор пункта меню "Отладка ⇨ начать отладку"</span><span class="sxs-lookup"><span data-stu-id="83ed0-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="83ed0-131">Нажмите кнопку с зеленой стрелкой на панели инструментов ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="83ed0-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="83ed0-132">Используйте сочетание клавиш F5.</span><span class="sxs-lookup"><span data-stu-id="83ed0-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="83ed0-133">При использовании любого из описанных выше действий будет выполнена компиляция нашего проекта, а затем ASP.NET Development Server, который был встроен в Visual Web Developer для запуска.</span><span class="sxs-lookup"><span data-stu-id="83ed0-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="83ed0-134">В нижнем углу экрана появится уведомление, указывающее, что ASP.NET Development Server запущено, и отобразит номер порта, под которым он выполняется.</span><span class="sxs-lookup"><span data-stu-id="83ed0-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="83ed0-135">Visual Web Developer будет автоматически открывать окно браузера, URL-адрес которого указывает на наш веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="83ed0-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="83ed0-136">Это позволит нам быстро испытать наше веб-приложение:</span><span class="sxs-lookup"><span data-stu-id="83ed0-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="83ed0-137">Итак, это было довольно быстро — мы создали новый веб-сайт, добавили функцию с тремя строками и получили текст в браузере.</span><span class="sxs-lookup"><span data-stu-id="83ed0-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="83ed0-138">Не Rocket наука, но это начало.</span><span class="sxs-lookup"><span data-stu-id="83ed0-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="83ed0-139">*Примечание. Visual Web Developer включает в себя ASP.NET Development Server, который запустит ваш веб-сайт на случайном номере "порт". На снимке экрана выше сайт выполняется на `http://localhost:26641/`, поэтому используется порт 26641. Ваш номер порта будет другим. Когда мы говорим об URL-адресе, подобном/Сторе/бровсе, в этом учебнике, который будет идти после номера порта. Если номер порта 26641, то переход по адресу/Сторе/бровсе означает, что `http://localhost:26641/Store/Browse`.*</span><span class="sxs-lookup"><span data-stu-id="83ed0-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="83ed0-140">Добавление Стореконтроллер</span><span class="sxs-lookup"><span data-stu-id="83ed0-140">Adding a StoreController</span></span>

<span data-ttu-id="83ed0-141">Мы добавили простой HomeController, который реализует домашнюю страницу нашего сайта.</span><span class="sxs-lookup"><span data-stu-id="83ed0-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="83ed0-142">Теперь добавим еще один контроллер, который мы будем использовать для реализации функций обзора нашего музыкального магазина.</span><span class="sxs-lookup"><span data-stu-id="83ed0-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="83ed0-143">Наш контроллер магазина будет поддерживать три сценария:</span><span class="sxs-lookup"><span data-stu-id="83ed0-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="83ed0-144">Страница со списком жанров музыки в нашем музыкальном магазине</span><span class="sxs-lookup"><span data-stu-id="83ed0-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="83ed0-145">Страница просмотра со списком всех альбомов музыки в определенном жанре</span><span class="sxs-lookup"><span data-stu-id="83ed0-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="83ed0-146">Страница сведений, на которой отображаются сведения о конкретном музыкальном альбоме</span><span class="sxs-lookup"><span data-stu-id="83ed0-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="83ed0-147">Начнем с добавления нового класса Стореконтроллер.</span><span class="sxs-lookup"><span data-stu-id="83ed0-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="83ed0-148">Если вы еще не сделали этого, закройте приложение, закрыв браузер или выбрав пункт меню Отладка ⇨ отключить отладку.</span><span class="sxs-lookup"><span data-stu-id="83ed0-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="83ed0-149">Теперь добавьте новый Стореконтроллер.</span><span class="sxs-lookup"><span data-stu-id="83ed0-149">Now add a new StoreController.</span></span> <span data-ttu-id="83ed0-150">Как и в случае с HomeController, это можно сделать, щелкнув правой кнопкой мыши папку Controllers в обозреватель решений и выбрав пункт меню Добавить контроллер&gt;.</span><span class="sxs-lookup"><span data-stu-id="83ed0-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="83ed0-151">Наш новый Стореконтроллер уже имеет метод "index".</span><span class="sxs-lookup"><span data-stu-id="83ed0-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="83ed0-152">Мы будем использовать этот метод "index" для реализации страницы списка, в которой перечислены все жанры в нашем музыкальном магазине.</span><span class="sxs-lookup"><span data-stu-id="83ed0-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="83ed0-153">Мы также добавим два дополнительных метода для реализации двух других сценариев, которые мы хотим использовать нашим Стореконтроллер: обзор и сведения.</span><span class="sxs-lookup"><span data-stu-id="83ed0-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="83ed0-154">Эти методы (индекс, обзор и сведения) в контроллере называются "действиями контроллера", и, как уже говорилось с методом действия HomeController. index (), их заданием является реагирование на запросы URL-адресов и (вообще говоря) определение содержимого должен быть отправлен обратно браузеру или пользователю, вызвавшему URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="83ed0-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="83ed0-155">Мы начнем нашу реализацию Стореконтроллер, изменив метод Сеиндекс (), чтобы возвращалась строка "Привет из Store. index ()", и мы добавим аналогичные методы для просмотра () и подробностей ():</span><span class="sxs-lookup"><span data-stu-id="83ed0-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="83ed0-156">Запустите проект еще раз и просмотрите следующие URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="83ed0-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="83ed0-157">/Store</span><span class="sxs-lookup"><span data-stu-id="83ed0-157">/Store</span></span>
- <span data-ttu-id="83ed0-158">/сторе/бровсе</span><span class="sxs-lookup"><span data-stu-id="83ed0-158">/Store/Browse</span></span>
- <span data-ttu-id="83ed0-159">/сторе/детаилс</span><span class="sxs-lookup"><span data-stu-id="83ed0-159">/Store/Details</span></span>

<span data-ttu-id="83ed0-160">Доступ к этим URL-адресам вызовет методы действий в нашем контроллере и возвращает ответы на строки:</span><span class="sxs-lookup"><span data-stu-id="83ed0-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="83ed0-161">Это замечательно, но это просто постоянные строки.</span><span class="sxs-lookup"><span data-stu-id="83ed0-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="83ed0-162">Сделаем их динамическими, чтобы они могли получать информацию из URL-адреса и отображать их в выходных данных страницы.</span><span class="sxs-lookup"><span data-stu-id="83ed0-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="83ed0-163">Сначала мы изменим метод действия обзора, чтобы получить значение строки запроса из URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="83ed0-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="83ed0-164">Это можно сделать, добавив параметр "Жанр" в метод действия.</span><span class="sxs-lookup"><span data-stu-id="83ed0-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="83ed0-165">Когда мы делаем это, ASP.NET MVC автоматически передает любые параметры QueryString или формы POST с именем жанра в метод действия при его вызове.</span><span class="sxs-lookup"><span data-stu-id="83ed0-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="83ed0-166">*Примечание. Мы используем метод служебной программы HttpUtility. HtmlEncode для очистки вводимых пользователем данных. Это не позволяет пользователям внедрять JavaScript в наше представление со ссылкой, такой как/Сторе/бровсе? Жанр =&lt;скрипт&gt;Window. location = 'http://hackersite.com'&lt;/Script&gt;.*</span><span class="sxs-lookup"><span data-stu-id="83ed0-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="83ed0-167">Теперь давайте перейду к/Сторе/бровсе? Жанр = Disco</span><span class="sxs-lookup"><span data-stu-id="83ed0-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="83ed0-168">Теперь измените действие Details, чтобы оно читало и отображало входной параметр с именем ID.</span><span class="sxs-lookup"><span data-stu-id="83ed0-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="83ed0-169">В отличие от нашего предыдущего метода, мы не будем внедрять значение идентификатора в качестве параметра QueryString.</span><span class="sxs-lookup"><span data-stu-id="83ed0-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="83ed0-170">Вместо этого мы будем внедрять его непосредственно в сам URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="83ed0-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="83ed0-171">Например:/Store/Details/5.</span><span class="sxs-lookup"><span data-stu-id="83ed0-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="83ed0-172">ASP.NET MVC позволяет нам без каких-либо усилий настраивать.</span><span class="sxs-lookup"><span data-stu-id="83ed0-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="83ed0-173">По умолчанию соглашением о маршрутизации MVC ASP.NET является обработка сегмента URL-адреса после имени метода действия в виде параметра с именем "ID".</span><span class="sxs-lookup"><span data-stu-id="83ed0-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="83ed0-174">Если метод действия имеет параметр с именем ID, ASP.NET MVC автоматически передаст сегмент URL-адреса в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="83ed0-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="83ed0-175">Запустите приложение и перейдите по/Store/Details/5:</span><span class="sxs-lookup"><span data-stu-id="83ed0-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="83ed0-176">Давайте посмотрим, что мы сделали на данный момент:</span><span class="sxs-lookup"><span data-stu-id="83ed0-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="83ed0-177">Мы создали новый проект ASP.NET MVC в Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="83ed0-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="83ed0-178">Мы обсуждали базовую структуру папок приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="83ed0-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="83ed0-179">Мы узнали, как запустить наш веб-сайт с помощью ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="83ed0-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="83ed0-180">Мы создали два класса контроллера: HomeController и Стореконтроллер.</span><span class="sxs-lookup"><span data-stu-id="83ed0-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="83ed0-181">Мы добавили методы действий в наши контроллеры, которые отвечают на запросы URL-адресов и возвращают текст в браузер.</span><span class="sxs-lookup"><span data-stu-id="83ed0-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="83ed0-182">[Назад](mvc-music-store-part-1.md)
> [Вперед](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="83ed0-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
