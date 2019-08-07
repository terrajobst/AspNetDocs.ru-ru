---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: Добавление контроллера | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6b38d757d37374b14979f8a079a46158ff64f9c3
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810773"
---
# <a name="adding-a-controller"></a><span data-ttu-id="31e9b-102">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="31e9b-102">Adding a Controller</span></span>

<span data-ttu-id="31e9b-103">по [Рик Андерсон (]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="31e9b-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="31e9b-104">MVC означает *модель-представление-контроллер*.</span><span class="sxs-lookup"><span data-stu-id="31e9b-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="31e9b-105">MVC — это шаблон для разработки приложений, которые хорошо спроектированы, тестируемы и просты в обслуживании.</span><span class="sxs-lookup"><span data-stu-id="31e9b-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="31e9b-106">Приложения на основе MVC содержат:</span><span class="sxs-lookup"><span data-stu-id="31e9b-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="31e9b-107">Оделс **M** : Классы, представляющие данные приложения и использующие логику проверки для применения бизнес-правил для этих данных.</span><span class="sxs-lookup"><span data-stu-id="31e9b-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="31e9b-108">**V** редставления: Файлы шаблонов, используемые приложением для динамического создания ответов HTML.</span><span class="sxs-lookup"><span data-stu-id="31e9b-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="31e9b-109">Управляемые **C** : Классы, обрабатывающие входящие запросы браузера, извлекают данные модели, а затем указывают шаблоны представлений, которые возвращают ответ в браузер.</span><span class="sxs-lookup"><span data-stu-id="31e9b-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="31e9b-110">Мы покажем все эти концепции в этой серии руководств и покажем, как их использовать для создания приложения.</span><span class="sxs-lookup"><span data-stu-id="31e9b-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="31e9b-111">Начнем с создания класса Controller.</span><span class="sxs-lookup"><span data-stu-id="31e9b-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="31e9b-112">В **Обозреватель решений**щелкните правой кнопкой мыши папку *Controllers* и выберите команду **добавить**, а затем — **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="31e9b-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="31e9b-113">В диалоговом окне **Добавление шаблона** щелкните элемент **контроллер MVC 5 — пустой**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="31e9b-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="31e9b-114">Присвойте новому контроллеру имя "HelloWorldController" и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="31e9b-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![добавить контроллер](adding-a-controller/_static/image3.png)

<span data-ttu-id="31e9b-116">Обратите внимание, что в **Обозреватель решений** создан новый файл с именем *HelloWorldController.CS* и Новая папка *виевс\хелловорлд*.</span><span class="sxs-lookup"><span data-stu-id="31e9b-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="31e9b-117">Контроллер открыт в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="31e9b-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="31e9b-118">Замените содержимое файла следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="31e9b-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="31e9b-119">В качестве примера методы контроллера будут возвращать строку HTML.</span><span class="sxs-lookup"><span data-stu-id="31e9b-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="31e9b-120">Контроллеру присваивается `HelloWorldController` имя, а первым методу `Index`присваивается имя.</span><span class="sxs-lookup"><span data-stu-id="31e9b-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="31e9b-121">Давайте выберем его из браузера.</span><span class="sxs-lookup"><span data-stu-id="31e9b-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="31e9b-122">Запустите приложение (нажмите клавишу F5 или CTRL + F5).</span><span class="sxs-lookup"><span data-stu-id="31e9b-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="31e9b-123">В браузере добавьте &quot;HelloWorld&quot; к пути в адресной строке.</span><span class="sxs-lookup"><span data-stu-id="31e9b-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="31e9b-124">(Например, на рисунке ниже `http://localhost:1234/HelloWorld.`) страница в браузере будет выглядеть, как на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="31e9b-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="31e9b-125">В приведенном выше методе код возвратил строку напрямую.</span><span class="sxs-lookup"><span data-stu-id="31e9b-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="31e9b-126">Вы сообщили системе, что просто возвращали какой-либо код HTML.</span><span class="sxs-lookup"><span data-stu-id="31e9b-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="31e9b-127">ASP.NET MVC вызывает различные классы контроллеров (и различные методы действий в них) в зависимости от входящего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="31e9b-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="31e9b-128">Логика маршрутизации URL-адресов по умолчанию, используемая ASP.NET MVC, использует следующий формат для определения того, какой код вызывать:</span><span class="sxs-lookup"><span data-stu-id="31e9b-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="31e9b-129">Формат маршрутизации задается в файле *Start/\_раутеконфиг. CS приложения* .</span><span class="sxs-lookup"><span data-stu-id="31e9b-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="31e9b-130">При запуске приложения и отсутствии сегментов URL-адреса по умолчанию используется "домашний" контроллер и метод действия "index", указанный в разделе по умолчанию приведенного выше кода.</span><span class="sxs-lookup"><span data-stu-id="31e9b-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="31e9b-131">Первая часть URL-адреса определяет класс контроллера для выполнения.</span><span class="sxs-lookup"><span data-stu-id="31e9b-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="31e9b-132">Поэтому */хелловорлд* сопоставляется с `HelloWorldController` классом.</span><span class="sxs-lookup"><span data-stu-id="31e9b-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="31e9b-133">Вторая часть URL-адреса определяет метод действия для выполняемого класса.</span><span class="sxs-lookup"><span data-stu-id="31e9b-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="31e9b-134">Поэтому */хелловорлд/индекс* `Index` приведет к выполнению метода `HelloWorldController` класса.</span><span class="sxs-lookup"><span data-stu-id="31e9b-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="31e9b-135">Обратите внимание, что нам пришлось бы перейти к `Index` /хелловорлд, а метод использовался по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="31e9b-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="31e9b-136">Это обусловлено тем, что `Index` метод с именем является методом по умолчанию, который будет вызываться на контроллере, если он не указан явно.</span><span class="sxs-lookup"><span data-stu-id="31e9b-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="31e9b-137">В третьей части сегмента URL-адреса (`Parameters`) указываются данные маршрута.</span><span class="sxs-lookup"><span data-stu-id="31e9b-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="31e9b-138">Далее в этом руководстве мы увидим данные маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="31e9b-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="31e9b-139">Перейдите по адресу `http://localhost:xxxx/HelloWorld/Welcome`.</span><span class="sxs-lookup"><span data-stu-id="31e9b-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="31e9b-140">Метод выполняет операцию и возвращает строку &quot;, которая является методом действия приветствия... `Welcome` &quot;.</span><span class="sxs-lookup"><span data-stu-id="31e9b-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="31e9b-141">По умолчанию используется `/[Controller]/[ActionName]/[Parameters]`сопоставление MVC.</span><span class="sxs-lookup"><span data-stu-id="31e9b-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="31e9b-142">Для этого URL-адреса заданы контроллер `HelloWorld` и метод действия `Welcome`.</span><span class="sxs-lookup"><span data-stu-id="31e9b-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="31e9b-143">Часть URL-адреса `[Parameters]` на данный момент еще не использовалась.</span><span class="sxs-lookup"><span data-stu-id="31e9b-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="31e9b-144">Давайте немного изменим пример, чтобы вы могли передать некоторые сведения о параметрах с URL-адреса на контроллер (например, */хелловорлд/велкоме? Name = Скотт&amp;нумтимес = 4*).</span><span class="sxs-lookup"><span data-stu-id="31e9b-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="31e9b-145">`Welcome` Измените метод, включив в него два параметра, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="31e9b-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="31e9b-146">Обратите внимание, что в C# коде используется функция необязательного параметра, `numTimes` указывающая, что параметру по умолчанию будет присвоено значение 1, если для этого параметра не передается никакого значения.</span><span class="sxs-lookup"><span data-stu-id="31e9b-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="31e9b-147">Примечание по безопасности. В приведенном выше коде используется [HttpUtility. HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) для защиты приложения от вредоносных входных данных (а именно — JavaScript).</span><span class="sxs-lookup"><span data-stu-id="31e9b-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="31e9b-148">Дополнительные сведения см. в практическом руководстве по [ Защита от эксплойтов сценариев в веб-приложении путем применения кодировки HTML к](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)строкам.</span><span class="sxs-lookup"><span data-stu-id="31e9b-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="31e9b-149">Запустите приложение и перейдите по URL-адресу примера`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`().</span><span class="sxs-lookup"><span data-stu-id="31e9b-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="31e9b-150">Вы можете попробовать различные значения `name` и `numtimes` в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="31e9b-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="31e9b-151">[Система привязки модели MVC ASP.NET](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) автоматически сопоставляет именованные параметры из строки запроса в адресной строке с параметрами в методе.</span><span class="sxs-lookup"><span data-stu-id="31e9b-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="31e9b-152">В приведенном выше примере сегмент URL-адреса `Parameters`() не используется `name` , параметры и `numTimes` передаются как [строки запроса](http://en.wikipedia.org/wiki/Query_string).</span><span class="sxs-lookup"><span data-stu-id="31e9b-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="31e9b-153">Подстановочный знак ?</span><span class="sxs-lookup"><span data-stu-id="31e9b-153">The ?</span></span> <span data-ttu-id="31e9b-154">(вопросительный знак) в приведенном выше URL-адресе — это разделитель, и следуют строки запроса.</span><span class="sxs-lookup"><span data-stu-id="31e9b-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="31e9b-155">Символ &amp; разделяет строки запроса.</span><span class="sxs-lookup"><span data-stu-id="31e9b-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="31e9b-156">Замените метод приветствия следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="31e9b-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="31e9b-157">Запустите приложение и введите следующий URL-адрес:`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="31e9b-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="31e9b-158">На этот раз третий сегмент URL-адреса соответствует параметру `ID.` `Welcome` маршрута метод действия содержит параметр (`ID`) `RegisterRoutes` , соответствующий спецификации URL-адреса в методе.</span><span class="sxs-lookup"><span data-stu-id="31e9b-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="31e9b-159">В приложениях ASP.NET MVC обычно передаются параметры в виде данных маршрута (как мы делали с помощью приведенного выше идентификатора), чем передача их в виде строк запроса.</span><span class="sxs-lookup"><span data-stu-id="31e9b-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="31e9b-160">Можно также добавить маршрут для передачи `name` параметров и `numtimes` in в качестве данных маршрута в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="31e9b-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="31e9b-161">В файле *старт\раутеконфиг.КС\_приложения* Добавьте маршрут Hello:</span><span class="sxs-lookup"><span data-stu-id="31e9b-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="31e9b-162">Запустите приложение и перейдите к `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span><span class="sxs-lookup"><span data-stu-id="31e9b-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="31e9b-163">Для многих приложений MVC маршрут по умолчанию работает нормально.</span><span class="sxs-lookup"><span data-stu-id="31e9b-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="31e9b-164">Далее в этом руководстве вы узнаете, как передавать данные с помощью связывателя модели, и вам не придется изменять маршрут по умолчанию для этого.</span><span class="sxs-lookup"><span data-stu-id="31e9b-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="31e9b-165">В этих примерах контроллер выполняет &quot;VC&quot; -часть MVC, т. е. представление и контроллер работают.</span><span class="sxs-lookup"><span data-stu-id="31e9b-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="31e9b-166">Контроллер возвращает HTML напрямую.</span><span class="sxs-lookup"><span data-stu-id="31e9b-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="31e9b-167">Обычно вы не хотите, чтобы контроллеры возвращали HTML напрямую, так как это очень громоздкий для кода.</span><span class="sxs-lookup"><span data-stu-id="31e9b-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="31e9b-168">Вместо этого мы обычно используем отдельный файл шаблона представления для создания ответа HTML.</span><span class="sxs-lookup"><span data-stu-id="31e9b-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="31e9b-169">Давайте посмотрим, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="31e9b-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="31e9b-170">[Назад](getting-started.md)
> [Вперед](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="31e9b-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
