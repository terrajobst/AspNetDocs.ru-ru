---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Использование AJAX для доставки динамических обновлений | Документация Майкрософт
author: microsoft
description: На шаге 10 реализована поддержка пользователей, вошедших в систему, в RSVP по интересу к Конференции на обед с использованием подхода на основе AJAX, интегрированного в сведения о обеде...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486312"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="91146-103">Использование AJAX для доставки динамических обновлений</span><span class="sxs-lookup"><span data-stu-id="91146-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="91146-104">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="91146-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="91146-105">Скачать в формате PDF</span><span class="sxs-lookup"><span data-stu-id="91146-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="91146-106">Это шаг 10 из бесплатного [учебника по приложению "NerdDinner"](introducing-the-nerddinner-tutorial.md) , в котором рассматривается создание небольшого, но полного веб-приложения с использованием ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="91146-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="91146-107">На шаге 10 реализована поддержка пользователей, вошедших в систему, в RSVP по интересу к Конференции на обед с использованием подхода на основе AJAX, интегрированного на странице сведений о обеде.</span><span class="sxs-lookup"><span data-stu-id="91146-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="91146-108">Если вы используете ASP.NET MVC 3, мы рекомендуем следовать руководствам по [Начало работы в MVC 3 или в приложении для](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [музыкального магазина MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="91146-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="91146-109">NerdDinner шаг 10. принятие RSVP</span><span class="sxs-lookup"><span data-stu-id="91146-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="91146-110">Теперь мы реализуем поддержку пользователей, вошедших в систему, в службу RSVP по интересу к Конференции в обеде.</span><span class="sxs-lookup"><span data-stu-id="91146-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="91146-111">Это можно сделать с помощью подхода на основе AJAX, интегрированного на странице сведений о обеде.</span><span class="sxs-lookup"><span data-stu-id="91146-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="91146-112">Указывает, является ли пользователь RSVP</span><span class="sxs-lookup"><span data-stu-id="91146-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="91146-113">Пользователи могут посетить URL-адрес */диннерс/детаилс/[ID*], чтобы просмотреть сведения об определенном обеде:</span><span class="sxs-lookup"><span data-stu-id="91146-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="91146-114">Метод действия Details () реализуется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="91146-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="91146-115">Первым шагом в реализации поддержки RSVP будет Добавление вспомогательного метода "Исусеррегистеред (username)" в наш объект Dinner (в рамках созданного ранее разделяемого класса Dinner.cs).</span><span class="sxs-lookup"><span data-stu-id="91146-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="91146-116">Этот вспомогательный метод возвращает значение true или false в зависимости от того, является ли пользователь RSVP в настоящее время обедом:</span><span class="sxs-lookup"><span data-stu-id="91146-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="91146-117">Затем можно добавить следующий код в шаблон представления Details. aspx, чтобы отобразить соответствующее сообщение, указывающее, зарегистрирован ли пользователь или нет для события:</span><span class="sxs-lookup"><span data-stu-id="91146-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="91146-118">И теперь, когда пользователь посещает обед, для которого зарегистрировано, он увидит следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="91146-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="91146-119">И когда они посещают обед, они не зарегистрированы для них, они увидят следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="91146-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="91146-120">Реализация метода действия Register</span><span class="sxs-lookup"><span data-stu-id="91146-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="91146-121">Теперь добавим функции, необходимые для предоставления пользователям RSVP на обед со страницы сведений.</span><span class="sxs-lookup"><span data-stu-id="91146-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="91146-122">Чтобы реализовать это, мы создадим новый класс "Рсвпконтроллер", щелкнув правой кнопкой мыши каталог \Controllers и выбрав команду меню Добавить контроллер&gt;.</span><span class="sxs-lookup"><span data-stu-id="91146-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="91146-123">Мы реализуем метод действия Register (зарегистрировать) в новом классе Рсвпконтроллер, который принимает идентификатор для компании в качестве аргумента, извлекает соответствующий объект Dinner, проверяет, находится ли вошедший в систему пользователь в списке зарегистрированных для него пользователей, а также если не добавляет для них объект RSVP:</span><span class="sxs-lookup"><span data-stu-id="91146-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="91146-124">Обратите внимание, что мы возвращаем простую строку в качестве выходных данных метода действия.</span><span class="sxs-lookup"><span data-stu-id="91146-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="91146-125">Мы могли бы внедрить это сообщение в шаблон представления, но так как это так мало, мы просто используем вспомогательный метод Content () в базовом классе контроллера и возвращаем строковое сообщение, подобное приведенному выше.</span><span class="sxs-lookup"><span data-stu-id="91146-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="91146-126">Вызов метода действия Рсвпфоревент с помощью AJAX</span><span class="sxs-lookup"><span data-stu-id="91146-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="91146-127">Мы будем использовать AJAX для вызова метода действия Register из нашего подробного представления.</span><span class="sxs-lookup"><span data-stu-id="91146-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="91146-128">Реализовать это довольно просто.</span><span class="sxs-lookup"><span data-stu-id="91146-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="91146-129">Сначала мы добавим две ссылки на библиотеку скриптов:</span><span class="sxs-lookup"><span data-stu-id="91146-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="91146-130">Первая библиотека ссылается на основную библиотеку сценариев ASP.NET AJAX на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="91146-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="91146-131">Этот файл приблизительно 24k в размере (сжатый) и содержит основные функциональные возможности AJAX на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="91146-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="91146-132">Вторая библиотека содержит служебные функции, которые интегрируются с встроенными вспомогательными методами AJAX ASP.NET MVC (которые мы будем использовать вскоре).</span><span class="sxs-lookup"><span data-stu-id="91146-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="91146-133">Затем можно обновить код шаблона представления, который мы добавили ранее, чтобы вместо вывода сообщения "вы не зарегистрировались для этого события" мы отпустим ссылку, которая при отправке выполняет вызов AJAX, который вызывает наш метод действия Рсвпфоревент на нашем контроллере RSVP. и RSVP:</span><span class="sxs-lookup"><span data-stu-id="91146-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="91146-134">Использованный выше вспомогательный метод Ajax. ActionLink () встроен в ASP.NET MVC и похож на вспомогательный метод HTML. ActionLink (), за исключением того, что вместо выполнения стандартной навигации он выполняет вызов AJAX к методу действия при щелчке ссылки.</span><span class="sxs-lookup"><span data-stu-id="91146-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="91146-135">Выше мы вызываем метод действия Register на контроллере RSVP и передаем Диннерид в качестве параметра ID.</span><span class="sxs-lookup"><span data-stu-id="91146-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="91146-136">Окончательный параметр Ажаксоптионс, который мы передаем, указывает, что мы хотим взять содержимое, возвращенное из метода действия, и обновить HTML &lt;div&gt; на странице, идентификатор которой — "рсвпмсг".</span><span class="sxs-lookup"><span data-stu-id="91146-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="91146-137">Теперь, когда пользователь переходит на обед, который не зарегистрирован для, он увидит ссылку на RSVP для него:</span><span class="sxs-lookup"><span data-stu-id="91146-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="91146-138">Если щелкнуть ссылку "RSVP для этого события", он сделает вызов AJAX методу действия Register на контроллере RSVP, а после завершения он увидит обновленное сообщение, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="91146-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="91146-139">Пропускная способность сети и трафик, задействованные при выполнении этого вызова AJAX, действительно являются легковесными.</span><span class="sxs-lookup"><span data-stu-id="91146-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="91146-140">Когда пользователь щелкает ссылку "RSVP для этого события", к URL-адресу */Dinners/Register/1* , который выглядит следующим образом в сети, выполняется небольшой запрос HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="91146-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="91146-141">Ответ метода действия Register — это просто:</span><span class="sxs-lookup"><span data-stu-id="91146-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="91146-142">Этот упрощенный вызов работает быстро и будет работать даже через медленную сеть.</span><span class="sxs-lookup"><span data-stu-id="91146-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="91146-143">Добавление анимации jQuery</span><span class="sxs-lookup"><span data-stu-id="91146-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="91146-144">Реализованная функциональность AJAX работает хорошо и быстро.</span><span class="sxs-lookup"><span data-stu-id="91146-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="91146-145">Иногда это может произойти быстро, но пользователь может не заметить, что ссылка RSVP заменена новым текстом.</span><span class="sxs-lookup"><span data-stu-id="91146-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="91146-146">Чтобы сделать результат чуть более очевидным, мы можем добавить простую анимацию, чтобы привлечь внимание к сообщению об обновлении.</span><span class="sxs-lookup"><span data-stu-id="91146-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="91146-147">Шаблон проекта MVC по умолчанию ASP.NET включает jQuery — отличную (и очень популярную) библиотеку JavaScript с открытым исходным кодом, которая также поддерживается корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="91146-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="91146-148">jQuery предоставляет ряд функций, включая удобную библиотеку выбора и эффектов HTML DOM.</span><span class="sxs-lookup"><span data-stu-id="91146-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="91146-149">Чтобы использовать jQuery, сначала добавьте ссылку на скрипт.</span><span class="sxs-lookup"><span data-stu-id="91146-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="91146-150">Так как мы будем использовать jQuery в различных местах сайта, мы добавим ссылку на скрипт в файле главной основной страницы Site. master, чтобы все страницы могли его использовать.</span><span class="sxs-lookup"><span data-stu-id="91146-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="91146-151">*Совет. Убедитесь, что установлено исправление JavaScript IntelliSense для VS 2008 с пакетом обновления 1 (SP1), которое обеспечивает расширенную поддержку IntelliSense для файлов JavaScript (включая jQuery). Его можно загрузить с: http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="91146-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="91146-152">Код, написанный с помощью JQuery, часто использует глобальный метод JavaScript "$ ()", который получает один или несколько HTML-элементов с помощью селектора CSS.</span><span class="sxs-lookup"><span data-stu-id="91146-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="91146-153">Например, *$ ("#rsvpmsg")* выбирает любой HTML-элемент с идентификатором рсвпмсг, а *$ (". что")* выберет все элементы с именем класса CSS "что".</span><span class="sxs-lookup"><span data-stu-id="91146-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="91146-154">Кроме того, можно написать более сложные запросы, например "вернуть все отмеченные переключатели", используя запрос Selector, например: *$ ("input [@type= Radio] [@checked]")* .</span><span class="sxs-lookup"><span data-stu-id="91146-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="91146-155">После выбора элементов можно вызывать методы для них, чтобы предпринять действия, такие как скрытие: *$ ("#rsvpmsg"). Hide ();*</span><span class="sxs-lookup"><span data-stu-id="91146-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="91146-156">Для нашего сценария RSVP мы определим простую функцию JavaScript с именем «Аниматерсвпмессаже», которая выбирает «рсвпмсг» &lt;div&gt; и анимируется размер текстового содержимого.</span><span class="sxs-lookup"><span data-stu-id="91146-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="91146-157">Приведенный ниже код запускает маленький текст, а затем приводит к увеличению времени в течение 400 миллисекунд:</span><span class="sxs-lookup"><span data-stu-id="91146-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="91146-158">После успешного завершения вызова AJAX можно подключить эту функцию JavaScript, передав ее имя в вспомогательный метод Ajax. ActionLink () (через свойство события Ажаксоптионс "onsuccesss"):</span><span class="sxs-lookup"><span data-stu-id="91146-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="91146-159">Теперь, когда вы щелкнули ссылку "RSVP для этого события" и вызов AJAX завершается успешно, переданное сообщение о содержимом будет анимироваться и увеличиваться:</span><span class="sxs-lookup"><span data-stu-id="91146-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="91146-160">Кроме предоставления события "onsuccesss", объект Ажаксоптионс предоставляет события onSuccess, onsuccesss и onSuccess, которые можно обменять (вместе с различными другими свойствами и полезными параметрами).</span><span class="sxs-lookup"><span data-stu-id="91146-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="91146-161">Очистка — рефакторинг частичного представления RSVP</span><span class="sxs-lookup"><span data-stu-id="91146-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="91146-162">Наш шаблон подробного представления начинается очень долго, что сверхурочно сделает его более трудным для понимания.</span><span class="sxs-lookup"><span data-stu-id="91146-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="91146-163">Чтобы помочь улучшить удобочитаемость кода, давайте создадим частичное представление — Рсвпстатус. ascx, которое инкапсулирует весь код представления RSVP для нашей страницы сведений.</span><span class="sxs-lookup"><span data-stu-id="91146-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="91146-164">Это можно сделать, щелкнув правой кнопкой мыши папку \Виевс\диннерс и выбрав команду меню Добавить-&gt;представление.</span><span class="sxs-lookup"><span data-stu-id="91146-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="91146-165">Мы будем брать объект обеда в качестве строго типизированного ViewModel.</span><span class="sxs-lookup"><span data-stu-id="91146-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="91146-166">Затем можно скопировать и вставить в него содержимое RSVP из нашего представления Details. aspx.</span><span class="sxs-lookup"><span data-stu-id="91146-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="91146-167">После этого давайте также создадим другое частичное представление — Едитандделетелинкс. ascx, которое инкапсулирует наш код представления ссылок Edit и DELETE.</span><span class="sxs-lookup"><span data-stu-id="91146-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="91146-168">Кроме того, мы будем брать объект ужина в качестве строго типизированного ViewModel, а затем копировать и вставлять в него логику "изменить и удалить" из представления Details. aspx.</span><span class="sxs-lookup"><span data-stu-id="91146-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="91146-169">Теперь наш шаблон подробного представления может включать два вызова метода HTML. Рендерпартиал () в нижней части:</span><span class="sxs-lookup"><span data-stu-id="91146-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="91146-170">Это делает средство очистки кода недоступным для чтения и сопровождения.</span><span class="sxs-lookup"><span data-stu-id="91146-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="91146-171">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="91146-171">Next Step</span></span>

<span data-ttu-id="91146-172">Теперь рассмотрим, как можно использовать AJAX еще дальше и добавить в наше приложение поддержку интерактивного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="91146-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="91146-173">[Назад](secure-applications-using-authentication-and-authorization.md)
> [Вперед](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="91146-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
