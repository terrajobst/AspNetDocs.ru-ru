---
uid: single-page-application/overview/templates/emberjs-template
title: Шаблон Ембержс | Документация Майкрософт
author: xqiu
description: Шаблон EmberJS
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467160"
---
# <a name="emberjs-template"></a><span data-ttu-id="e4365-103">Шаблон EmberJS</span><span class="sxs-lookup"><span data-stu-id="e4365-103">EmberJS template</span></span>

<span data-ttu-id="e4365-104">по [Ксинянг КИУ](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="e4365-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="e4365-105">Шаблон Ембержс MVC написан на (Nathan Тоттен, Thiago Сантос и Ксинянг КИУ.</span><span class="sxs-lookup"><span data-stu-id="e4365-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="e4365-106">Скачивание шаблона MVC Ембержс</span><span class="sxs-lookup"><span data-stu-id="e4365-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)

<span data-ttu-id="e4365-107">Шаблон Ембержс SPA предназначен для быстрого создания интерактивных веб-приложений на стороне клиента с помощью Ембержс.</span><span class="sxs-lookup"><span data-stu-id="e4365-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="e4365-108">"Одностраничное приложение" (SPA) — это общий термин для веб-приложения, которое загружает одну HTML-страницу и обновляет страницу динамически, вместо того, чтобы загружать новые страницы.</span><span class="sxs-lookup"><span data-stu-id="e4365-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="e4365-109">После начальной загрузки страницы Протокол SPA обращается к серверу через запросы AJAX.</span><span class="sxs-lookup"><span data-stu-id="e4365-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="e4365-110">AJAX не является ничего новым, но на сегодняшний день существуют платформы JavaScript, упрощающие создание и обслуживание большого сложного приложения SPA.</span><span class="sxs-lookup"><span data-stu-id="e4365-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="e4365-111">Кроме того, HTML 5 и CSS3 упрощают создание многофункциональных интерфейсов пользователя.</span><span class="sxs-lookup"><span data-stu-id="e4365-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="e4365-112">Шаблон Ембержс SPA использует библиотеку JavaScript [Ember](http://emberjs.com/) для обработки обновлений страницы из запросов AJAX.</span><span class="sxs-lookup"><span data-stu-id="e4365-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="e4365-113">Ember. js использует привязку данных для синхронизации страницы с последними данными.</span><span class="sxs-lookup"><span data-stu-id="e4365-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="e4365-114">Таким образом, вам не нужно писать код, который проходит через данные JSON и обновляет модель DOM.</span><span class="sxs-lookup"><span data-stu-id="e4365-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="e4365-115">Вместо этого в HTML-коде помещаются декларативные атрибуты, указывающие Ember. js, как представлять данные.</span><span class="sxs-lookup"><span data-stu-id="e4365-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="e4365-116">На стороне сервера шаблон Ембержс практически идентичен [шаблону KNOCKOUTJS Spa](../introduction/knockoutjs-template.md).</span><span class="sxs-lookup"><span data-stu-id="e4365-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="e4365-117">Он использует ASP.NET MVC для обслуживания документов HTML и веб-API ASP.NET для обработки запросов AJAX от клиента.</span><span class="sxs-lookup"><span data-stu-id="e4365-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="e4365-118">Дополнительные сведения об этих аспектах шаблона см. в документации по [шаблону KnockoutJS](../introduction/knockoutjs-template.md) .</span><span class="sxs-lookup"><span data-stu-id="e4365-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="e4365-119">В этом разделе рассматриваются различия между шаблоном маскирования и шаблоном Ембержс.</span><span class="sxs-lookup"><span data-stu-id="e4365-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="e4365-120">Создание проекта шаблона Ембержс SPA</span><span class="sxs-lookup"><span data-stu-id="e4365-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="e4365-121">Скачайте и установите шаблон, нажав кнопку Загрузить выше.</span><span class="sxs-lookup"><span data-stu-id="e4365-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="e4365-122">Возможно, потребуется перезапустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4365-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="e4365-123">В области **шаблоны** выберите **Установленные шаблоны** и разверните узел  **C# визуального** элемента.</span><span class="sxs-lookup"><span data-stu-id="e4365-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="e4365-124">В **разделе C#визуальный** элемент выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="e4365-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="e4365-125">В списке шаблонов проектов выберите **ASP.NET MVC 4 веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="e4365-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="e4365-126">Задайте для проекта имя и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e4365-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="e4365-127">В мастере **создания проектов** выберите **проект EMBER. js Spa**.</span><span class="sxs-lookup"><span data-stu-id="e4365-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="e4365-128">Общие сведения о шаблоне SPA Ембержс</span><span class="sxs-lookup"><span data-stu-id="e4365-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="e4365-129">Шаблон Ембержс использует сочетание jQuery, Ember. js, заголовки. js для создания плавного интерактивного пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e4365-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="e4365-130">Ember. js — это библиотека JavaScript, которая использует шаблон MVC на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e4365-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="e4365-131">*Шаблон*, написанный на языке шаблонов заголовки, описывает пользовательский интерфейс приложения.</span><span class="sxs-lookup"><span data-stu-id="e4365-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="e4365-132">В режиме выпуска [компилятор заголовки](https://github.com/Myslik/csharp-ember-handlebars) используется для объединения и компиляции шаблона заголовки.</span><span class="sxs-lookup"><span data-stu-id="e4365-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="e4365-133">*Модель* хранит данные приложения, полученные с сервера (списки задач и элементы TODO).</span><span class="sxs-lookup"><span data-stu-id="e4365-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="e4365-134">*Контроллер* хранит состояние приложения.</span><span class="sxs-lookup"><span data-stu-id="e4365-134">A *controller* stores application state.</span></span> <span data-ttu-id="e4365-135">Контроллеры часто представляют данные модели соответствующим шаблонам.</span><span class="sxs-lookup"><span data-stu-id="e4365-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="e4365-136">*Представление* преобразует события-примитивы из приложения и передает их контроллеру.</span><span class="sxs-lookup"><span data-stu-id="e4365-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="e4365-137">*Маршрутизатор* управляет состоянием приложения, обеспечивая синхронизацию URL-адресов и шаблонов.</span><span class="sxs-lookup"><span data-stu-id="e4365-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="e4365-138">Кроме того, библиотеку данных Ember можно использовать для синхронизации объектов JSON (полученных с сервера через API RESTFUL) и клиентских моделей.</span><span class="sxs-lookup"><span data-stu-id="e4365-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="e4365-139">Шаблон Ембержс SPA организует скрипты на восемь уровней:</span><span class="sxs-lookup"><span data-stu-id="e4365-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="e4365-140">webapi\_Adapter. js, webapi\_сериализатор. js: расширяет библиотеку данных Ember для работы с веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e4365-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="e4365-141">Scripts/helps. js: определяет новые вспомогательные методы Ember заголовки.</span><span class="sxs-lookup"><span data-stu-id="e4365-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="e4365-142">Scripts/App. js: создает приложение и настраивает адаптер и сериализатор.</span><span class="sxs-lookup"><span data-stu-id="e4365-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="e4365-143">Scripts/App/Models/\*. js: определяет модели.</span><span class="sxs-lookup"><span data-stu-id="e4365-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="e4365-144">Scripts/app/views/\*. js: определяет представления.</span><span class="sxs-lookup"><span data-stu-id="e4365-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="e4365-145">Scripts/App/Controllers/\*. js: определяет контроллеры.</span><span class="sxs-lookup"><span data-stu-id="e4365-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="e4365-146">Scripts/App/Routes, Scripts/App/Router. js: определяет маршруты.</span><span class="sxs-lookup"><span data-stu-id="e4365-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="e4365-147">Templates/\*. ХБС: определяет шаблоны заголовки.</span><span class="sxs-lookup"><span data-stu-id="e4365-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="e4365-148">Рассмотрим некоторые из этих сценариев более подробно.</span><span class="sxs-lookup"><span data-stu-id="e4365-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="e4365-149">Модели</span><span class="sxs-lookup"><span data-stu-id="e4365-149">Models</span></span>

<span data-ttu-id="e4365-150">Модели определяются в папке Scripts/App/Models.</span><span class="sxs-lookup"><span data-stu-id="e4365-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="e4365-151">Существует два файла модели: todoItem. js и todoList. js.</span><span class="sxs-lookup"><span data-stu-id="e4365-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="e4365-152">**TODO. Model. js** определяет модели на стороне клиента (браузер) для списков задач.</span><span class="sxs-lookup"><span data-stu-id="e4365-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="e4365-153">Существует два класса модели: todoItem и todoList.</span><span class="sxs-lookup"><span data-stu-id="e4365-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="e4365-154">В Ember модели являются подклассами DS. Моделировать.</span><span class="sxs-lookup"><span data-stu-id="e4365-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="e4365-155">Модель может иметь свойства с атрибутами:</span><span class="sxs-lookup"><span data-stu-id="e4365-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="e4365-156">Модели могут определять связи с другими моделями:</span><span class="sxs-lookup"><span data-stu-id="e4365-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="e4365-157">Модели могут иметь вычисленные свойства, которые привязаны к другим свойствам:</span><span class="sxs-lookup"><span data-stu-id="e4365-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="e4365-158">Модели могут иметь функции наблюдателя, которые вызываются при изменении наблюдаемого свойства:</span><span class="sxs-lookup"><span data-stu-id="e4365-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="e4365-159">Представления</span><span class="sxs-lookup"><span data-stu-id="e4365-159">Views</span></span>

<span data-ttu-id="e4365-160">Представления определяются в папке Scripts/app/views.</span><span class="sxs-lookup"><span data-stu-id="e4365-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="e4365-161">Представление преобразует события из пользовательского интерфейса приложения.</span><span class="sxs-lookup"><span data-stu-id="e4365-161">A view translates events from the application UI.</span></span> <span data-ttu-id="e4365-162">Обработчик событий может выполнить обратный вызов функций контроллера или просто вызвать контекст данных напрямую.</span><span class="sxs-lookup"><span data-stu-id="e4365-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="e4365-163">Например, следующий код находится в представлении views/Тодоитемедитвиев. js.</span><span class="sxs-lookup"><span data-stu-id="e4365-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="e4365-164">Он определяет обработку событий для текстового поля ввода.</span><span class="sxs-lookup"><span data-stu-id="e4365-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="e4365-165">Контроллер</span><span class="sxs-lookup"><span data-stu-id="e4365-165">Controller</span></span>

<span data-ttu-id="e4365-166">Контроллеры определяются в папке Scripts/App/Controllers.</span><span class="sxs-lookup"><span data-stu-id="e4365-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="e4365-167">Чтобы представить одну модель, расширьте `Ember.ObjectController`:</span><span class="sxs-lookup"><span data-stu-id="e4365-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="e4365-168">Контроллер также может представлять коллекцию моделей путем расширения `Ember.ArrayController`.</span><span class="sxs-lookup"><span data-stu-id="e4365-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="e4365-169">Например, TodoListController представляет массив объектов `todoList`.</span><span class="sxs-lookup"><span data-stu-id="e4365-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="e4365-170">Контроллер сортирует по todoList ИДЕНТИФИКАТОРу в порядке убывания:</span><span class="sxs-lookup"><span data-stu-id="e4365-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="e4365-171">Контроллер определяет функцию с именем `addTodoList`, которая создает новый todoList и добавляет ее в массив.</span><span class="sxs-lookup"><span data-stu-id="e4365-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="e4365-172">Чтобы увидеть, как вызывается эта функция, откройте файл шаблона с именем Тодолисттемплате. HTML в папке Templates.</span><span class="sxs-lookup"><span data-stu-id="e4365-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="e4365-173">Следующий код шаблона привязывает кнопку к функции `addTodoList`:</span><span class="sxs-lookup"><span data-stu-id="e4365-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="e4365-174">Контроллер также содержит свойство `error`, содержащее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="e4365-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="e4365-175">Ниже приведен код шаблона для вывода сообщения об ошибке (также в Тодолисттемплате. HTML):</span><span class="sxs-lookup"><span data-stu-id="e4365-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="e4365-176">Маршруты</span><span class="sxs-lookup"><span data-stu-id="e4365-176">Routes</span></span>

<span data-ttu-id="e4365-177">Router. js определяет маршруты и шаблон по умолчанию для отображения, настраивает состояние приложения и сопоставляет URL-адреса с маршрутами:</span><span class="sxs-lookup"><span data-stu-id="e4365-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="e4365-178">Тодолистрауте. js загружает данные для Тодолистрауте, переопределяя функцию Сетупконтроллер:</span><span class="sxs-lookup"><span data-stu-id="e4365-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="e4365-179">Ember использует соглашения об именовании для сопоставления URL-адресов, имен маршрутов, контроллеров и шаблонов.</span><span class="sxs-lookup"><span data-stu-id="e4365-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="e4365-180">Дополнительные сведения см. в разделе [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) в документации по ембержс.</span><span class="sxs-lookup"><span data-stu-id="e4365-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="e4365-181">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="e4365-181">Templates</span></span>

<span data-ttu-id="e4365-182">Папка Templates содержит четыре шаблона:</span><span class="sxs-lookup"><span data-stu-id="e4365-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="e4365-183">Application. ХБС: шаблон по умолчанию, отображаемый при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="e4365-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="e4365-184">About. ХБС: шаблон для маршрута "/абаут".</span><span class="sxs-lookup"><span data-stu-id="e4365-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="e4365-185">index. ХБС: шаблон для корневого маршрута "/".</span><span class="sxs-lookup"><span data-stu-id="e4365-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="e4365-186">todoList. ХБС — шаблон для маршрута «/Тодо».</span><span class="sxs-lookup"><span data-stu-id="e4365-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="e4365-187">\_панель навигации. ХБС. шаблон определяет меню переходов.</span><span class="sxs-lookup"><span data-stu-id="e4365-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="e4365-188">Шаблон приложения действует как Главная страница.</span><span class="sxs-lookup"><span data-stu-id="e4365-188">The application template acts like a master page.</span></span> <span data-ttu-id="e4365-189">Он содержит заголовок, нижний колонтитул и "{{Outlet}}" для вставки других шаблонов в зависимости от маршрута.</span><span class="sxs-lookup"><span data-stu-id="e4365-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="e4365-190">Дополнительные сведения о шаблонах приложений в Ember см. в разделе [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span><span class="sxs-lookup"><span data-stu-id="e4365-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="e4365-191">Шаблон "/Тодолист" содержит два выражения цикла.</span><span class="sxs-lookup"><span data-stu-id="e4365-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="e4365-192">Внешний цикл `{{#each controller}}`, а цикл внутри — `{{#each todos}}`.</span><span class="sxs-lookup"><span data-stu-id="e4365-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="e4365-193">В следующем коде показан встроенный `Ember.Checkbox` представление, настраиваемый `App.TodoItemEditView`и ссылка с `deleteTodo` действием.</span><span class="sxs-lookup"><span data-stu-id="e4365-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="e4365-194">Класс `HtmlHelperExtensions`, определенный в Controllers/Хтмлхелперекстенсионс. cs, определяет вспомогательную функцию для кэширования и вставки файлов шаблонов при установке для **Debug** значения **true** в файле Web. config.</span><span class="sxs-lookup"><span data-stu-id="e4365-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="e4365-195">Эта функция вызывается из файла представления ASP.NET MVC, определенного в Views/Home/App. cshtml:</span><span class="sxs-lookup"><span data-stu-id="e4365-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="e4365-196">Функция, вызываемая без аргументов, отображает все файлы шаблонов в папке шаблонов.</span><span class="sxs-lookup"><span data-stu-id="e4365-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="e4365-197">Можно также указать вложенную папку или конкретный файл шаблона.</span><span class="sxs-lookup"><span data-stu-id="e4365-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="e4365-198">Если параметр **Debug** имеет **значение false** в файле Web. config, приложение включает элемент пакета «~/бундлес/темплатес».</span><span class="sxs-lookup"><span data-stu-id="e4365-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="e4365-199">Этот элемент пакета добавляется в BundleConfig.cs с помощью библиотеки компилятора заголовки:</span><span class="sxs-lookup"><span data-stu-id="e4365-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
