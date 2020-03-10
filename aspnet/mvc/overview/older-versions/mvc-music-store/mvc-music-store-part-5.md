---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: Часть 5. Редактирование форм и шаблонов | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. В части 5 описывается редактирование форм и шаблонов.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450912"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="00209-104">Часть 5. изменение форм и шаблонов</span><span class="sxs-lookup"><span data-stu-id="00209-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="00209-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="00209-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="00209-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="00209-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="00209-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="00209-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="00209-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="00209-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="00209-109">В части 5 описывается редактирование форм и шаблонов.</span><span class="sxs-lookup"><span data-stu-id="00209-109">Part 5 covers Edit Forms and Templating.</span></span>

<span data-ttu-id="00209-110">В прошлом разделе мы загрузили данные из нашей базы данных и выводили их на экран.</span><span class="sxs-lookup"><span data-stu-id="00209-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="00209-111">В этой главе мы также разберем возможность редактирования данных.</span><span class="sxs-lookup"><span data-stu-id="00209-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="00209-112">Создание Стореманажерконтроллер</span><span class="sxs-lookup"><span data-stu-id="00209-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="00209-113">Начнем с создания нового контроллера с именем **стореманажерконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="00209-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="00209-114">Для этого контроллера мы будем использовать преимущества функций формирования шаблонов, доступных в обновлении инструментов ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="00209-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="00209-115">Задайте параметры для диалогового окна Добавление контроллера, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="00209-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="00209-116">При нажатии кнопки Добавить вы увидите, что механизм формирования шаблонов ASP.NET MVC 3 выполняет хороший объем работы за вас:</span><span class="sxs-lookup"><span data-stu-id="00209-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="00209-117">Он создает новый Стореманажерконтроллер с локальной переменной Entity Framework</span><span class="sxs-lookup"><span data-stu-id="00209-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="00209-118">Она добавляет папку Стореманажер в папку Views проекта.</span><span class="sxs-lookup"><span data-stu-id="00209-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="00209-119">Он добавляет представление Create. cshtml, DELETE. cshtml, Details. cshtml, Edit. cshtml и index. cshtml, строго типизированное в класс альбома.</span><span class="sxs-lookup"><span data-stu-id="00209-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="00209-120">Новый класс контроллера Стореманажер включает действия CRUD (создание, чтение, обновление, удаление), которые узнают, как работать с классом модели альбома и использовать наш контекст Entity Framework для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="00209-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="00209-121">Изменение шаблона представления</span><span class="sxs-lookup"><span data-stu-id="00209-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="00209-122">Важно помнить, что хотя этот код был создан для нас, он является стандартным кодом MVC ASP.NET, как мы написали в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="00209-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="00209-123">Она призвана сэкономить время, затрачиваемое на написание стандартного кода контроллера и создание строго типизированных представлений вручную, но это не тот тип создаваемого кода, с которым вы могли бы ознакомиться с ужасные предупреждениями о том, как не должны изменить приведен.</span><span class="sxs-lookup"><span data-stu-id="00209-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="00209-124">Это ваш код, и вы должны изменить его.</span><span class="sxs-lookup"><span data-stu-id="00209-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="00209-125">Итак, давайте начнем с быстрого редактирования в представление индекса Стореманажер (/Виевс/стореманажер/индекс.кштмл).</span><span class="sxs-lookup"><span data-stu-id="00209-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="00209-126">В этом представлении отображается таблица со списком альбомов в магазине с ссылками Edit/Details/DELETE и включает общие свойства альбома.</span><span class="sxs-lookup"><span data-stu-id="00209-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="00209-127">Мы удалим поле Албумартурл, так как оно не очень полезно в этом дисплее.</span><span class="sxs-lookup"><span data-stu-id="00209-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="00209-128">В &lt;таблице&gt; в разделе кода представления удалите элементы &lt;TH&gt; и &lt;TD&gt;, окружающие ссылки на Албумартурл, как показано в выделенных ниже строках:</span><span class="sxs-lookup"><span data-stu-id="00209-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="00209-129">Измененный код представления будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="00209-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="00209-130">Первый взгляд на Store Manager</span><span class="sxs-lookup"><span data-stu-id="00209-130">A first look at the Store Manager</span></span>

<span data-ttu-id="00209-131">Теперь запустите приложение и перейдите к/Стореманажер/..</span><span class="sxs-lookup"><span data-stu-id="00209-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="00209-132">Отобразится только что измененный индекс Store Manager, в котором отображается список альбомов в магазине со ссылками на изменения, сведения и удаление.</span><span class="sxs-lookup"><span data-stu-id="00209-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="00209-133">Если щелкнуть ссылку "Изменить", откроется форма редактирования с полями для альбома, включая раскрывающиеся списки для жанра и исполнителя.</span><span class="sxs-lookup"><span data-stu-id="00209-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="00209-134">В нижней части щелкните ссылку "назад на список", а затем щелкните ссылку сведения для альбома.</span><span class="sxs-lookup"><span data-stu-id="00209-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="00209-135">Отображаются подробные сведения об отдельном альбоме.</span><span class="sxs-lookup"><span data-stu-id="00209-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="00209-136">Опять же, щелкните ссылку вернуться к списку, а затем щелкните ссылку удалить.</span><span class="sxs-lookup"><span data-stu-id="00209-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="00209-137">Откроется диалоговое окно подтверждения, в котором отобразятся сведения об альбоме и будет предложено подтвердить удаление.</span><span class="sxs-lookup"><span data-stu-id="00209-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="00209-138">Нажав кнопку Удалить внизу, вы удалите альбом и вернетесь на страницу индекса, на которой будет показан удаленный альбом.</span><span class="sxs-lookup"><span data-stu-id="00209-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="00209-139">Мы не работаем с менеджером магазина, но у нас есть рабочий контроллер и код представления для начала операций CRUD.</span><span class="sxs-lookup"><span data-stu-id="00209-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="00209-140">Просмотр кода контроллера Store Manager</span><span class="sxs-lookup"><span data-stu-id="00209-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="00209-141">Контроллер Store Manager содержит хороший объем кода.</span><span class="sxs-lookup"><span data-stu-id="00209-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="00209-142">Давайте вернемся сверху вниз.</span><span class="sxs-lookup"><span data-stu-id="00209-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="00209-143">Контроллер включает в себя некоторые стандартные пространства имен для контроллера MVC, а также ссылку на пространство имен Models.</span><span class="sxs-lookup"><span data-stu-id="00209-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="00209-144">Контроллер имеет частный экземпляр Мусиксторинтитиес, используемый каждым из действий контроллера для доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="00209-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="00209-145">Действия индекса и сведений диспетчера магазина</span><span class="sxs-lookup"><span data-stu-id="00209-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="00209-146">Представление индекса получает список альбомов, включая сведения о жанрах и исполнителях каждого альбома, как было показано ранее при работе с методом обзора магазина.</span><span class="sxs-lookup"><span data-stu-id="00209-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="00209-147">Представление индекса следует за ссылками на связанные объекты, чтобы они могли отображать название жанра каждого альбома и имя исполнителя, поэтому контроллер является эффективным и запрашивает эти сведения в исходном запросе.</span><span class="sxs-lookup"><span data-stu-id="00209-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="00209-148">Действие контроллера сведений контроллера Стореманажер работает точно так же, как и действие "сведения о контроллере хранилища", которое мы написали ранее — запрос для альбома по ИДЕНТИФИКАТОРу с помощью метода Find (), а затем возвращает его в представление.</span><span class="sxs-lookup"><span data-stu-id="00209-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="00209-149">Методы действия Create</span><span class="sxs-lookup"><span data-stu-id="00209-149">The Create Action Methods</span></span>

<span data-ttu-id="00209-150">Методы действия Create немного отличаются от тех, которые мы видели до сих пор, так как они обрабатывают входные данные формы.</span><span class="sxs-lookup"><span data-stu-id="00209-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="00209-151">Когда пользователь впервые посещает/Стореманажер/креате/, отображается пустая форма.</span><span class="sxs-lookup"><span data-stu-id="00209-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="00209-152">На этой HTML-странице будет содержаться &lt;форма&gt; элемент, содержащий элементы ввода раскрывающегося списка и текстового поля, где можно ввести сведения о альбоме.</span><span class="sxs-lookup"><span data-stu-id="00209-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="00209-153">После того как пользователь заполнит значения формы альбома, они смогут нажать кнопку "Сохранить", чтобы отправить эти изменения обратно в приложение, чтобы сохранить его в базе данных.</span><span class="sxs-lookup"><span data-stu-id="00209-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="00209-154">Когда пользователь нажимает кнопку "Save" (сохранить), &lt;форма,&gt; выполняет HTTP-POST по адресу URL/Стореманажер/креате/и отправляет &lt;форму&gt; значений в составе HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="00209-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="00209-155">ASP.NET MVC позволяет легко разбивать логику этих двух сценариев вызова URL-адресов, позволяя реализовать два отдельных метода действия "создать" в нашем классе Стореманажерконтроллер — один для обработки начального HTTP-GET — для обзора URL-адреса/Стореманажер/креате/, а другой — для обработки HTTP-POST отправленных изменений.</span><span class="sxs-lookup"><span data-stu-id="00209-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="00209-156">Передача данных в представление с помощью ViewBag</span><span class="sxs-lookup"><span data-stu-id="00209-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="00209-157">Мы использовали ViewBag ранее в этом руководстве, но не говорили о нем.</span><span class="sxs-lookup"><span data-stu-id="00209-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="00209-158">ViewBag позволяет передавать данные в представление без использования строго типизированного объекта модели.</span><span class="sxs-lookup"><span data-stu-id="00209-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="00209-159">В этом случае наше действие изменить HTTP-GET Controller должно передать в форму список жанров и исполнителей, чтобы заполнить раскрывающиеся списки, а самый простой способ — вернуть их в виде ViewBag элементов.</span><span class="sxs-lookup"><span data-stu-id="00209-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="00209-160">ViewBag — это динамический объект, то есть вы можете ввести ViewBag. foo или ViewBag. Йоурнамехере без написания кода для определения этих свойств.</span><span class="sxs-lookup"><span data-stu-id="00209-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="00209-161">В этом случае код контроллера использует ViewBag. GenreId и ViewBag. Артистид, чтобы значения раскрывающегося списка, переданные в форму, были GenreId и Артистид, которые являются свойствами альбома, которые будут заданы.</span><span class="sxs-lookup"><span data-stu-id="00209-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="00209-162">Эти раскрывающиеся значения возвращаются в форму с помощью объекта SelectList, который создается исключительно для этой цели.</span><span class="sxs-lookup"><span data-stu-id="00209-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="00209-163">Это делается с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="00209-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="00209-164">Как видно из кода метода действия, для создания этого объекта используются три параметра:</span><span class="sxs-lookup"><span data-stu-id="00209-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="00209-165">Список элементов, которые будут отображены в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="00209-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="00209-166">Обратите внимание, что это не просто строка — мы передаем список жанров.</span><span class="sxs-lookup"><span data-stu-id="00209-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="00209-167">Следующим параметром, передаваемым в SelectList, является выбранное значение.</span><span class="sxs-lookup"><span data-stu-id="00209-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="00209-168">Таким способом SelectList знает, как предварительно выбрать элемент в списке.</span><span class="sxs-lookup"><span data-stu-id="00209-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="00209-169">Это будет проще понять при рассмотрении формы редактирования, которая очень похожа на.</span><span class="sxs-lookup"><span data-stu-id="00209-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="00209-170">Последний параметр — это отображаемое свойство.</span><span class="sxs-lookup"><span data-stu-id="00209-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="00209-171">В этом случае это означает, что свойство Genre.Name будет отображаться для пользователя.</span><span class="sxs-lookup"><span data-stu-id="00209-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="00209-172">С учетом этого, действие HTTP-GET Create довольно простое — два Селектлистс добавляются в ViewBag, и объект модели не передается в форму (поскольку он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="00209-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="00209-173">Вспомогательные методы HTML для отображения раскрывающихся элементов в представлении создания</span><span class="sxs-lookup"><span data-stu-id="00209-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="00209-174">Поскольку мы говорили о том, как раскрывающиеся значения передаются в представление, давайте кратко рассмотрим представление, чтобы увидеть, как эти значения отображаются.</span><span class="sxs-lookup"><span data-stu-id="00209-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="00209-175">В коде представления (/Виевс/стореманажер/креате.кштмл) вы увидите следующий вызов для отображения раскрывающегося списка жанра.</span><span class="sxs-lookup"><span data-stu-id="00209-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="00209-176">Это называется вспомогательным модулем HTML — служебным методом, который выполняет общую задачу представления.</span><span class="sxs-lookup"><span data-stu-id="00209-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="00209-177">Вспомогательные методы HTML очень полезны для обеспечения краткости и удобочитаемости нашего кода представления.</span><span class="sxs-lookup"><span data-stu-id="00209-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="00209-178">Вспомогательный элемент HTML. DropDownList предоставляется ASP.NET MVC, но, как мы увидим, можно создать собственные вспомогательные методы для просмотра кода, который мы будем использовать в нашем приложении.</span><span class="sxs-lookup"><span data-stu-id="00209-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="00209-179">Вызов HTML. DropDownList должен задаваться двумя объектами — где можно получить список и какое значение (если оно есть) должно быть заранее выбрано.</span><span class="sxs-lookup"><span data-stu-id="00209-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="00209-180">Первый параметр, GenreId, указывает DropDownList найти значение с именем GenreId либо в модели, либо в ViewBag.</span><span class="sxs-lookup"><span data-stu-id="00209-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="00209-181">Второй параметр используется для указания значения, которое будет отображаться как изначально выбранное в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="00209-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="00209-182">Так как эта форма является формой создания, нет значения для предвыбора и передается String. Empty.</span><span class="sxs-lookup"><span data-stu-id="00209-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="00209-183">Обработка отправленных значений формы</span><span class="sxs-lookup"><span data-stu-id="00209-183">Handling the Posted Form values</span></span>

<span data-ttu-id="00209-184">Как обсуждалось ранее, существует два метода действий, связанных с каждой формой.</span><span class="sxs-lookup"><span data-stu-id="00209-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="00209-185">Первый обрабатывает запрос HTTP-GET и отображает форму.</span><span class="sxs-lookup"><span data-stu-id="00209-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="00209-186">Второй обрабатывает запрос HTTP-POST, который содержит отправленные значения формы.</span><span class="sxs-lookup"><span data-stu-id="00209-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="00209-187">Обратите внимание, что действие контроллера имеет атрибут [HttpPost], который сообщает ASP.NET MVC о том, что он должен отвечать только на запросы HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="00209-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="00209-188">Это действие имеет четыре обязанности:</span><span class="sxs-lookup"><span data-stu-id="00209-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="00209-189">Чтение значений формы</span><span class="sxs-lookup"><span data-stu-id="00209-189">Read the form values</span></span>
- 2. <span data-ttu-id="00209-190">Проверить, прошли ли значения формы правила проверки</span><span class="sxs-lookup"><span data-stu-id="00209-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="00209-191">Если отправка формы допустима, сохраните данные и отобразите обновленный список.</span><span class="sxs-lookup"><span data-stu-id="00209-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="00209-192">Если отправка формы является недопустимой, повторно отобразите форму с ошибками проверки.</span><span class="sxs-lookup"><span data-stu-id="00209-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="00209-193">Считывание значений формы с помощью привязки модели</span><span class="sxs-lookup"><span data-stu-id="00209-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="00209-194">Действие контроллера обрабатывает отправку формы, которая включает значения для GenreId и Артистид (из раскрывающегося списка) и значения текстового поля для Title, Price и Албумартурл.</span><span class="sxs-lookup"><span data-stu-id="00209-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="00209-195">Хотя доступ к значениям формы Возможен напрямую, лучшим подходом является использование возможностей привязки модели, встроенных в ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="00209-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="00209-196">Когда действие контроллера принимает тип модели в качестве параметра, ASP.NET MVC попытается заполнить объект этого типа, используя входные данные формы (а также значения маршрута и строки запроса).</span><span class="sxs-lookup"><span data-stu-id="00209-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="00209-197">Это достигается путем поиска значений, имена которых соответствуют свойствам объекта Model, например при задании значения GenreId нового объекта альбома выполняется поиск входных данных с именем GenreId.</span><span class="sxs-lookup"><span data-stu-id="00209-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="00209-198">При создании представлений с помощью стандартных методов в ASP.NET MVC формы всегда отображаются с использованием имен свойств в качестве имен входных полей, поэтому имена полей будут просто соответствовать.</span><span class="sxs-lookup"><span data-stu-id="00209-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="00209-199">Проверка модели</span><span class="sxs-lookup"><span data-stu-id="00209-199">Validating the Model</span></span>

<span data-ttu-id="00209-200">Модель проверяется с помощью простого вызова ModelState. IsValid.</span><span class="sxs-lookup"><span data-stu-id="00209-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="00209-201">Мы еще не добавили правила проверки в наш класс «альбом». это будет сделано немного, так что сейчас эта проверка не требует много усилий.</span><span class="sxs-lookup"><span data-stu-id="00209-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="00209-202">Важно то, что эта проверка Моделстат. IsValid будет адаптирована к правилам проверки, которые мы поместили в нашей модели, поэтому будущие изменения правил проверки не потребует обновления кода действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="00209-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="00209-203">Сохранение отправленных значений</span><span class="sxs-lookup"><span data-stu-id="00209-203">Saving the submitted values</span></span>

<span data-ttu-id="00209-204">Если отправка формы проходит проверку, пора сохранить значения в базе данных.</span><span class="sxs-lookup"><span data-stu-id="00209-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="00209-205">При использовании Entity Framework необходимо только добавить модель в коллекцию альбомов и вызвать метод SaveChanges.</span><span class="sxs-lookup"><span data-stu-id="00209-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="00209-206">Entity Framework создает соответствующие команды SQL для сохранения значения.</span><span class="sxs-lookup"><span data-stu-id="00209-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="00209-207">После сохранения данных мы перенаправляем обратно в список альбомов, чтобы мы могли увидеть наше обновление.</span><span class="sxs-lookup"><span data-stu-id="00209-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="00209-208">Это делается путем возвращения Редиректтоактион с именем действия контроллера, которое требуется отобразить.</span><span class="sxs-lookup"><span data-stu-id="00209-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="00209-209">В данном случае это метод index.</span><span class="sxs-lookup"><span data-stu-id="00209-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="00209-210">Отображение недопустимых отправок формы с ошибками проверки</span><span class="sxs-lookup"><span data-stu-id="00209-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="00209-211">В случае недопустимого ввода в форму раскрывающиеся значения добавляются в ViewBag (как в случае HTTP-GET), а привязанные значения модели передаются обратно в представление для отображения.</span><span class="sxs-lookup"><span data-stu-id="00209-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="00209-212">Ошибки проверки автоматически отображаются с помощью вспомогательного метода HTML @Html.ValidationMessageFor.</span><span class="sxs-lookup"><span data-stu-id="00209-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="00209-213">Тестирование формы создания</span><span class="sxs-lookup"><span data-stu-id="00209-213">Testing the Create Form</span></span>

<span data-ttu-id="00209-214">Чтобы протестировать это, запустите приложение и перейдите к/Стореманажер/креате/. в нем отобразится пустая форма, возвращенная методом Стореконтроллер Create HTTP-GET.</span><span class="sxs-lookup"><span data-stu-id="00209-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="00209-215">Заполните некоторые значения и нажмите кнопку Создать, чтобы отправить форму.</span><span class="sxs-lookup"><span data-stu-id="00209-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="00209-216">Обработка изменений</span><span class="sxs-lookup"><span data-stu-id="00209-216">Handling Edits</span></span>

<span data-ttu-id="00209-217">Пара действий редактирования (HTTP-GET и HTTP-POST) очень похожа на методы действий создания, которые мы только что рассматривали.</span><span class="sxs-lookup"><span data-stu-id="00209-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="00209-218">Так как сценарий редактирования предполагает работу с существующим альбомом, метод Edit HTTP-GET загружает альбом на основе параметра ID, переданного через маршрут.</span><span class="sxs-lookup"><span data-stu-id="00209-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="00209-219">Этот код для получения альбома с помощью Албумид аналогичен тому, который ранее рассматривался в действии контроллера подробностей.</span><span class="sxs-lookup"><span data-stu-id="00209-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="00209-220">Как и в случае с методом Create/HTTP-GET, раскрывающиеся значения возвращаются через ViewBag.</span><span class="sxs-lookup"><span data-stu-id="00209-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="00209-221">Это позволяет нам вернуть альбом в качестве объекта модели в представление (которое строго типизировано в класс альбома) при передаче дополнительных данных (например, списка жанров) через ViewBag.</span><span class="sxs-lookup"><span data-stu-id="00209-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="00209-222">Действие Edit HTTP-POST очень похоже на действие Create HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="00209-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="00209-223">Единственное отличие заключается в том, что вместо добавления нового альбома в базу данных. Коллекция альбомов. мы находим текущий экземпляр альбома при помощи базы данных. Запись (альбом) и установка ее состояния в значение Modified.</span><span class="sxs-lookup"><span data-stu-id="00209-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="00209-224">Это говорит Entity Framework, что мы изменяем существующий альбом, в отличие от создания нового.</span><span class="sxs-lookup"><span data-stu-id="00209-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="00209-225">Мы можем протестировать это, запустив приложение и перейдя по адресу/Стореманжер/, а затем щелкнув ссылку Edit (изменить) для альбома.</span><span class="sxs-lookup"><span data-stu-id="00209-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="00209-226">Отобразится форма редактирования, показанная в методе редактирования HTTP-GET.</span><span class="sxs-lookup"><span data-stu-id="00209-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="00209-227">Заполните некоторые значения и нажмите кнопку Сохранить.</span><span class="sxs-lookup"><span data-stu-id="00209-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="00209-228">При этом форма публикуется, сохраняет значения и возвращает нас в список альбомов, показывая, что значения были обновлены.</span><span class="sxs-lookup"><span data-stu-id="00209-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="00209-229">Обработка удаления</span><span class="sxs-lookup"><span data-stu-id="00209-229">Handling Deletion</span></span>

<span data-ttu-id="00209-230">При удалении используется тот же шаблон, что и при редактировании и создании, при использовании одного действия контроллера для вывода формы подтверждения и еще одно действие контроллера, обрабатывающее отправку формы.</span><span class="sxs-lookup"><span data-stu-id="00209-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="00209-231">Действие "HTTP — получить удаление контроллера" точно аналогично предыдущему действию контроллера данных Store Manager.</span><span class="sxs-lookup"><span data-stu-id="00209-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="00209-232">Мы отображаем форму, которая строго типизирована для типа альбома, с помощью шаблона удалить содержимое представления.</span><span class="sxs-lookup"><span data-stu-id="00209-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="00209-233">В шаблоне удаления отображаются все поля модели, но мы можем упростить это немного.</span><span class="sxs-lookup"><span data-stu-id="00209-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="00209-234">Измените код представления в/Виевс/стореманажер/делете.кштмл на следующий.</span><span class="sxs-lookup"><span data-stu-id="00209-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="00209-235">Отобразится упрощенное подтверждение удаления.</span><span class="sxs-lookup"><span data-stu-id="00209-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="00209-236">Нажатие кнопки удалить приводит к обратной передаче формы на сервер, который выполняет действие Делетеконфирмед.</span><span class="sxs-lookup"><span data-stu-id="00209-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="00209-237">Действие "HTTP-после удаления контроллера" выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="00209-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="00209-238">Загружает альбом по ИДЕНТИФИКАТОРу</span><span class="sxs-lookup"><span data-stu-id="00209-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="00209-239">Удаляет его из альбома и сохраняет изменения</span><span class="sxs-lookup"><span data-stu-id="00209-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="00209-240">Перенаправляет на индекс, показывая, что альбом был удален из списка</span><span class="sxs-lookup"><span data-stu-id="00209-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="00209-241">Чтобы проверить это, запустите приложение и перейдите по/Стореманажер.</span><span class="sxs-lookup"><span data-stu-id="00209-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="00209-242">Выберите альбом из списка и щелкните ссылку удалить.</span><span class="sxs-lookup"><span data-stu-id="00209-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="00209-243">Отобразится экран подтверждения удаления.</span><span class="sxs-lookup"><span data-stu-id="00209-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="00209-244">Нажав кнопку Удалить, вы удаляете альбом и возвращает нам страницу индекса Store Manager, на которой показано, что альбом удален.</span><span class="sxs-lookup"><span data-stu-id="00209-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="00209-245">Использование пользовательского вспомогательного метода HTML для усечения текста</span><span class="sxs-lookup"><span data-stu-id="00209-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="00209-246">У нас есть одна потенциальная ошибка на странице индекса Store Manager.</span><span class="sxs-lookup"><span data-stu-id="00209-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="00209-247">Свойства названия и имени исполнителя могут быть достаточно длинными, чтобы они могли создать форматирование таблицы.</span><span class="sxs-lookup"><span data-stu-id="00209-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="00209-248">Мы создадим пользовательский вспомогательный метод HTML, чтобы мы могли легко усекать эти и другие свойства в наших представлениях.</span><span class="sxs-lookup"><span data-stu-id="00209-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="00209-249">Синтаксис @helper Razor значительно упрощает создание собственных вспомогательных функций для использования в представлениях.</span><span class="sxs-lookup"><span data-stu-id="00209-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="00209-250">Откройте представление/Виевс/стореманажер/индекс.кштмл и добавьте следующий код сразу после строки @model.</span><span class="sxs-lookup"><span data-stu-id="00209-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="00209-251">Этот вспомогательный метод принимает строку и максимальную длину для разрешения.</span><span class="sxs-lookup"><span data-stu-id="00209-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="00209-252">Если указанный текст короче указанной длины, вспомогательная функция выводит его как есть.</span><span class="sxs-lookup"><span data-stu-id="00209-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="00209-253">Если он больше, то он усекает текст и визуализирует "..." для оставшейся части.</span><span class="sxs-lookup"><span data-stu-id="00209-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="00209-254">Теперь мы можем использовать наш вспомогательный метод Truncate, чтобы убедиться, что длина названия и свойства имени исполнителя не превышает 25 символов.</span><span class="sxs-lookup"><span data-stu-id="00209-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="00209-255">Ниже представлен полный код представления, в котором используется наш новый вспомогательный модуль Truncate.</span><span class="sxs-lookup"><span data-stu-id="00209-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="00209-256">Теперь при просмотре URL-адреса/Стореманажер/альбомы и заголовки будут храниться ниже максимальной длины.</span><span class="sxs-lookup"><span data-stu-id="00209-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="00209-257">Примечание. в этом примере показан простой случай создания и использования вспомогательного метода в одном представлении.</span><span class="sxs-lookup"><span data-stu-id="00209-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="00209-258">Дополнительные сведения о создании вспомогательных функций, которые можно использовать на сайте, см. в записи блога: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="00209-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="00209-259">[Назад](mvc-music-store-part-4.md)
> [Вперед](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="00209-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
