---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: Общие сведения о контроллере MVC ASP.NET (VB) | Документация Майкрософт
author: StephenWalther
description: В этом руководстве Стивен Вальтер содержит сведения о ASP.NET контроллерах MVC. Вы узнаете, как создавать новые контроллеры и возвращать различные типы действия Res...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486924"
---
# <a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="9572e-104">Общие сведения о контроллерах в ASP.NET MVC (VB)</span><span class="sxs-lookup"><span data-stu-id="9572e-104">ASP.NET MVC Controller Overview (VB)</span></span>

<span data-ttu-id="9572e-105">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="9572e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="9572e-106">В этом руководстве Стивен Вальтер содержит сведения о ASP.NET контроллерах MVC.</span><span class="sxs-lookup"><span data-stu-id="9572e-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="9572e-107">Вы узнаете, как создавать новые контроллеры и возвращать различные типы результатов действий.</span><span class="sxs-lookup"><span data-stu-id="9572e-107">You learn how to create new controllers and return different types of action results.</span></span>

<span data-ttu-id="9572e-108">В этом руководстве рассматривается раздел контроллеров MVC ASP.NET, действия контроллера и результаты действий.</span><span class="sxs-lookup"><span data-stu-id="9572e-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="9572e-109">По завершении работы с этим руководством вы узнаете, как использовать контроллеры для управления взаимодействием посетителя с веб-сайтом ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9572e-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="9572e-110">Основные сведения об контроллерах</span><span class="sxs-lookup"><span data-stu-id="9572e-110">Understanding Controllers</span></span>

<span data-ttu-id="9572e-111">Контроллеры MVC отвечают за реагирование на запросы к веб-сайту ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9572e-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="9572e-112">Каждый запрос браузера сопоставляется с определенным контроллером.</span><span class="sxs-lookup"><span data-stu-id="9572e-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="9572e-113">Например, представьте, что в адресную строку браузера введен следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="9572e-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="9572e-114">В этом случае вызывается контроллер с именем Продуктконтроллер.</span><span class="sxs-lookup"><span data-stu-id="9572e-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="9572e-115">Продуктконтроллер отвечает за создание ответа на запрос браузера.</span><span class="sxs-lookup"><span data-stu-id="9572e-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="9572e-116">Например, контроллер может вернуть конкретное представление обратно в браузер, или контроллер может перенаправить пользователя на другой контроллер.</span><span class="sxs-lookup"><span data-stu-id="9572e-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="9572e-117">В листинге 1 содержится простой контроллер с именем Продуктконтроллер.</span><span class="sxs-lookup"><span data-stu-id="9572e-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="9572e-118">**Listing1 — Контроллерс\продуктконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="9572e-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="9572e-119">Как видно из листинга 1, контроллер является просто классом (Visual Basic .NET или C# классом).</span><span class="sxs-lookup"><span data-stu-id="9572e-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="9572e-120">Контроллер — это класс, производный от базового класса System. Web. MVC. Controller.</span><span class="sxs-lookup"><span data-stu-id="9572e-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="9572e-121">Поскольку контроллер наследуется от этого базового класса, контроллер наследует несколько полезных методов бесплатно (мы обсудим эти методы чуть позже).</span><span class="sxs-lookup"><span data-stu-id="9572e-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="9572e-122">Основные сведения о действиях контроллера</span><span class="sxs-lookup"><span data-stu-id="9572e-122">Understanding Controller Actions</span></span>

<span data-ttu-id="9572e-123">Контроллер предоставляет действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="9572e-123">A controller exposes controller actions.</span></span> <span data-ttu-id="9572e-124">Действие — это метод контроллера, который вызывается при вводе определенного URL-адреса в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="9572e-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="9572e-125">Например, представьте, что вы выполните запрос для следующего URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="9572e-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="9572e-126">В этом случае метод Index () вызывается для класса Продуктконтроллер.</span><span class="sxs-lookup"><span data-stu-id="9572e-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="9572e-127">В качестве примера действия контроллера используется метод Index ().</span><span class="sxs-lookup"><span data-stu-id="9572e-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="9572e-128">Действие контроллера должно быть открытым методом класса Controller.</span><span class="sxs-lookup"><span data-stu-id="9572e-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="9572e-129">По умолчанию методы Visual Basic.NET являются открытыми методами.</span><span class="sxs-lookup"><span data-stu-id="9572e-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="9572e-130">Следует понимать, что любой открытый метод, добавляемый в класс контроллера, предоставляется как действие контроллера автоматически (необходимо соблюдать осторожность, так как действие контроллера может быть вызвано любым пользователем в Вселенной, просто введя правильный URL-адрес в адресную строку браузера).</span><span class="sxs-lookup"><span data-stu-id="9572e-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="9572e-131">Действие контроллера должно удовлетворять некоторым дополнительным требованиям.</span><span class="sxs-lookup"><span data-stu-id="9572e-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="9572e-132">Метод, используемый в качестве действия контроллера, не может быть перегружен.</span><span class="sxs-lookup"><span data-stu-id="9572e-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="9572e-133">Кроме того, действие контроллера не может быть статическим методом.</span><span class="sxs-lookup"><span data-stu-id="9572e-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="9572e-134">Кроме того, в качестве действия контроллера можно использовать практически любой метод.</span><span class="sxs-lookup"><span data-stu-id="9572e-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="9572e-135">Основные сведения о результатах действия</span><span class="sxs-lookup"><span data-stu-id="9572e-135">Understanding Action Results</span></span>

<span data-ttu-id="9572e-136">Действие контроллера возвращает нечто, называемое *результатом действия*.</span><span class="sxs-lookup"><span data-stu-id="9572e-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="9572e-137">Результат действия — это то, что действие контроллера возвращает в ответ на запрос браузера.</span><span class="sxs-lookup"><span data-stu-id="9572e-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="9572e-138">Платформа ASP.NET MVC поддерживает несколько типов результатов действий, в том числе:</span><span class="sxs-lookup"><span data-stu-id="9572e-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="9572e-139">Виевресулт — представляет HTML и разметку.</span><span class="sxs-lookup"><span data-stu-id="9572e-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="9572e-140">EmptyResult — нет результата.</span><span class="sxs-lookup"><span data-stu-id="9572e-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="9572e-141">Редиректресулт — представляет перенаправление на новый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9572e-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="9572e-142">JsonResult — представляет нотация объектов JavaScriptный результат, который можно использовать в приложении AJAX.</span><span class="sxs-lookup"><span data-stu-id="9572e-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="9572e-143">JavaScriptResult — представляет скрипт JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9572e-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="9572e-144">Контентресулт — представляет текстовый результат.</span><span class="sxs-lookup"><span data-stu-id="9572e-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="9572e-145">Филеконтентресулт — представляет загружаемый файл (с двоичным содержимым).</span><span class="sxs-lookup"><span data-stu-id="9572e-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="9572e-146">FilePathResult — представляет загружаемый файл (с путем).</span><span class="sxs-lookup"><span data-stu-id="9572e-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="9572e-147">Филестреамресулт — представляет загружаемый файл (с файловым потоком).</span><span class="sxs-lookup"><span data-stu-id="9572e-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="9572e-148">Все эти результаты действия наследуются от базового класса ActionResult.</span><span class="sxs-lookup"><span data-stu-id="9572e-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="9572e-149">В большинстве случаев действие контроллера возвращает Виевресулт.</span><span class="sxs-lookup"><span data-stu-id="9572e-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="9572e-150">Например, действие контроллера индекса в листинге 2 Возвращает Виевресулт.</span><span class="sxs-lookup"><span data-stu-id="9572e-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="9572e-151">**Листинг 2. Контроллерс\букконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="9572e-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="9572e-152">Когда действие возвращает Виевресулт, в браузер возвращается HTML.</span><span class="sxs-lookup"><span data-stu-id="9572e-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="9572e-153">Метод Index () в листинге 2 возвращает в браузер представление с именем index.</span><span class="sxs-lookup"><span data-stu-id="9572e-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="9572e-154">Обратите внимание, что действие index () в листинге 2 не возвращает Виевресулт ().</span><span class="sxs-lookup"><span data-stu-id="9572e-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="9572e-155">Вместо этого вызывается метод View () базового класса контроллера.</span><span class="sxs-lookup"><span data-stu-id="9572e-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="9572e-156">Как правило, результат действия не возвращается напрямую.</span><span class="sxs-lookup"><span data-stu-id="9572e-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="9572e-157">Вместо этого вызывается один из следующих методов базового класса контроллера:</span><span class="sxs-lookup"><span data-stu-id="9572e-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="9572e-158">View — возвращает результат действия Виевресулт.</span><span class="sxs-lookup"><span data-stu-id="9572e-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="9572e-159">Redirect — возвращает результат действия Редиректресулт.</span><span class="sxs-lookup"><span data-stu-id="9572e-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="9572e-160">Редиректтоактион — возвращает результат действия Редиректтораутересулт.</span><span class="sxs-lookup"><span data-stu-id="9572e-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="9572e-161">Редиректторауте — возвращает результат действия Редиректтораутересулт.</span><span class="sxs-lookup"><span data-stu-id="9572e-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="9572e-162">JSON — возвращает результат действия JsonResult.</span><span class="sxs-lookup"><span data-stu-id="9572e-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="9572e-163">JavaScriptResult — возвращает JavaScriptResult.</span><span class="sxs-lookup"><span data-stu-id="9572e-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="9572e-164">Content — возвращает результат действия Контентресулт.</span><span class="sxs-lookup"><span data-stu-id="9572e-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="9572e-165">File — возвращает Филеконтентресулт, FilePathResult или Филестреамресулт в зависимости от параметров, переданных в метод.</span><span class="sxs-lookup"><span data-stu-id="9572e-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="9572e-166">Таким образом, если вы хотите вернуть представление в браузер, вызовите метод View ().</span><span class="sxs-lookup"><span data-stu-id="9572e-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="9572e-167">Если вы хотите перенаправить пользователя из одного действия контроллера в другое, вызовите метод Редиректтоактион ().</span><span class="sxs-lookup"><span data-stu-id="9572e-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="9572e-168">Например, действие Details () в листинге 3 либо отображает представление, либо перенаправляет пользователя в действие index () в зависимости от того, имеет ли параметр ID значение.</span><span class="sxs-lookup"><span data-stu-id="9572e-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="9572e-169">**Листинг 3-Кустомерконтроллер. vb**</span><span class="sxs-lookup"><span data-stu-id="9572e-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="9572e-170">Результат действия Контентресулт — Специальный.</span><span class="sxs-lookup"><span data-stu-id="9572e-170">The ContentResult action result is special.</span></span> <span data-ttu-id="9572e-171">Результат действия Контентресулт можно использовать для возврата результата действия в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="9572e-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="9572e-172">Например, метод Index () в листинге 4 возвращает сообщение в виде обычного текста, а не в виде HTML.</span><span class="sxs-lookup"><span data-stu-id="9572e-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="9572e-173">**Листинг 4. Контроллерс\статусконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="9572e-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="9572e-174">статусконтроллер</span><span class="sxs-lookup"><span data-stu-id="9572e-174">StatusController</span></span>
> 
> 
> <span data-ttu-id="9572e-175">System. Web. MVC. Controller</span><span class="sxs-lookup"><span data-stu-id="9572e-175">System.Web.Mvc.Controller</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="9572e-176">При вызове действия Статусконтроллер. index () представление не возвращается.</span><span class="sxs-lookup"><span data-stu-id="9572e-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="9572e-177">Вместо этого необработанный текст "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="9572e-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="9572e-178">возвращается в браузер.</span><span class="sxs-lookup"><span data-stu-id="9572e-178">is returned to the browser.</span></span>

<span data-ttu-id="9572e-179">Если действие контроллера возвращает результат, который не является результатом действия (например, дата или целое число), то результат упаковывается в Контентресулт автоматически.</span><span class="sxs-lookup"><span data-stu-id="9572e-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="9572e-180">Например, при вызове действия Index () Воркконтроллер в листинге 5 Дата возвращается как Контентресулт автоматически.</span><span class="sxs-lookup"><span data-stu-id="9572e-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="9572e-181">**Листинг 5-Воркконтроллер. vb**</span><span class="sxs-lookup"><span data-stu-id="9572e-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="9572e-182">Действие index () в листинге 5 возвращает объект DateTime.</span><span class="sxs-lookup"><span data-stu-id="9572e-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="9572e-183">Платформа ASP.NET MVC преобразует объект DateTime в строку и автоматически заключает значение DateTime в Контентресулт.</span><span class="sxs-lookup"><span data-stu-id="9572e-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="9572e-184">Браузер получает дату и время в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="9572e-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="9572e-185">Сводка</span><span class="sxs-lookup"><span data-stu-id="9572e-185">Summary</span></span>

<span data-ttu-id="9572e-186">Цель этого руководства — познакомиться с основными понятиями ASP.NET контроллеров MVC, действиями контроллера и результатами действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="9572e-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="9572e-187">В первом разделе вы узнали, как добавлять новые контроллеры в проект MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9572e-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="9572e-188">Далее вы узнали, как открытые методы контроллера предоставляются в совокупности как действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="9572e-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="9572e-189">Наконец, мы обсуждали различные типы результатов действий, которые могут быть возвращены действием контроллера.</span><span class="sxs-lookup"><span data-stu-id="9572e-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="9572e-190">В частности, мы рассмотрели, как вернуть Виевресулт, Редиректтоактионресулт и Контентресулт из действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="9572e-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9572e-191">[Назад](creating-a-custom-route-constraint-cs.md)
> [Вперед](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9572e-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
