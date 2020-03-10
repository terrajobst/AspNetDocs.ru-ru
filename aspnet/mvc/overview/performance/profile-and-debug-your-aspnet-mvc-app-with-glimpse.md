---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: Профилирование и отладка приложения ASP.NET MVC с помощью краткого описания | Документация Майкрософт
author: Rick-Anderson
description: Краткое описание — это расширяющееся и растущее семейство пакетов NuGet с открытым кодом, которое предоставляет подробные сведения о производительности, отладке и диагностике для ASP.NET a...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432900"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="4594e-103">Профилирование и отладка приложения ASP.NET MVC с помощью Glimpse</span><span class="sxs-lookup"><span data-stu-id="4594e-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>

<span data-ttu-id="4594e-104">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4594e-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="4594e-105">Краткое описание — это расширяющееся и растущее семейство пакетов NuGet с открытым кодом, которое предоставляет подробные сведения о производительности, отладке и диагностике для приложений ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4594e-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="4594e-106">Это тривиальный способ установки, упрощения и быстрого ускорения, а также отображает ключевые метрики производительности в нижней части каждой страницы.</span><span class="sxs-lookup"><span data-stu-id="4594e-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="4594e-107">Она позволяет детализировать приложение, если вам нужно узнать, что происходит на сервере.</span><span class="sxs-lookup"><span data-stu-id="4594e-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="4594e-108">В кратком обзоре содержится очень важная информация, которую мы рекомендуем использовать на протяжении всего цикла разработки, включая тестовую среду Azure.</span><span class="sxs-lookup"><span data-stu-id="4594e-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="4594e-109">Хотя [Fiddler](http://www.telerik.com/fiddler) и [средства разработки F-12](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) предоставляют представление на стороне клиента, в кратком обзоре представлено подробное представление о сервере.</span><span class="sxs-lookup"><span data-stu-id="4594e-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="4594e-110">В этом учебнике основное внимание уделяется использованию пакетов ASP.NET MVC и EF, но доступны многие другие пакеты.</span><span class="sxs-lookup"><span data-stu-id="4594e-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="4594e-111">Где это возможно, я буду ссылаться на соответствующие [документы с краткими](http://getglimpse.com/Docs/) сведениями, которые я могу поддерживать.</span><span class="sxs-lookup"><span data-stu-id="4594e-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="4594e-112">«Краткий обзор» — это проект с открытым исходным кодом. Вы также можете участвовать в исходном коде и документах.</span><span class="sxs-lookup"><span data-stu-id="4594e-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>

- [<span data-ttu-id="4594e-113">Установка краткого описания</span><span class="sxs-lookup"><span data-stu-id="4594e-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="4594e-114">Включение краткого описания для localhost</span><span class="sxs-lookup"><span data-stu-id="4594e-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="4594e-115">Вкладка временной шкалы</span><span class="sxs-lookup"><span data-stu-id="4594e-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="4594e-116">Привязка модели</span><span class="sxs-lookup"><span data-stu-id="4594e-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="4594e-117">Маршруты</span><span class="sxs-lookup"><span data-stu-id="4594e-117">Routes</span></span>](#route)
- [<span data-ttu-id="4594e-118">Использование краткого описания в Azure</span><span class="sxs-lookup"><span data-stu-id="4594e-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="4594e-119">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4594e-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="4594e-120">Установка краткого описания</span><span class="sxs-lookup"><span data-stu-id="4594e-120">Installing Glimpse</span></span>

<span data-ttu-id="4594e-121">Вы можете установить его с помощью консоли диспетчера пакетов NuGet или консоли **Управление пакетами NuGet** .</span><span class="sxs-lookup"><span data-stu-id="4594e-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="4594e-122">Для этой демонстрации я устанавливаю пакеты Mvc5 и EF6:</span><span class="sxs-lookup"><span data-stu-id="4594e-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![Установка краткого описания из NuGet DLG](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="4594e-124">Поиск *краткого описания. EF*</span><span class="sxs-lookup"><span data-stu-id="4594e-124">Search for *Glimpse.EF*</span></span>

![Краткий обзор EF из NuGet Install DLG](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="4594e-126">Выбрав **установленные пакеты**, можно увидеть установленные зависимые модули:</span><span class="sxs-lookup"><span data-stu-id="4594e-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![Установленные краткие пакеты из диалогового окна](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="4594e-128">Следующие команды устанавливают краткий обзор модулей MVC5 и EF6 из консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="4594e-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="4594e-129">Включение краткого описания для localhost</span><span class="sxs-lookup"><span data-stu-id="4594e-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="4594e-130">Перейдите в раздел http://localhost:&lt;p порт #&gt;/глимпсе.аксд и нажмите кнопку <strong>включить краткий</strong> обзор.</span><span class="sxs-lookup"><span data-stu-id="4594e-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![Страница краткого axd](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="4594e-132">Если панель "Избранное" отображается, можно перетащить кнопки краткого описания и добавить их в качестве закладок:</span><span class="sxs-lookup"><span data-stu-id="4594e-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![Кнопки с краткими обзорами IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="4594e-134">Теперь можно перемещаться по приложению, и в нижней части страницы отображается **заголовков** (HUD).</span><span class="sxs-lookup"><span data-stu-id="4594e-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![Страница диспетчера контактов с HUD](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="4594e-136">На [странице краткий обзор HUD](http://getglimpse.com/Docs/Heads-up-Display) содержатся сведения о времени, показанные выше.</span><span class="sxs-lookup"><span data-stu-id="4594e-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="4594e-137">Ненавязчивые данные производительности, отображаемые HUD, могут немедленно уведомить вас о проблеме, прежде чем перейти к циклу тестирования.</span><span class="sxs-lookup"><span data-stu-id="4594e-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="4594e-138">Если щелкнуть &quot;g&quot; в правом нижнем углу, откроется панель «Обзор»:</span><span class="sxs-lookup"><span data-stu-id="4594e-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![Панель краткого описания](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="4594e-140">На приведенном выше рисунке выбрана [вкладка выполнение](http://getglimpse.com/Docs/Execution-Tab) , в которой отображаются сведения о времени действий и фильтров в конвейере.</span><span class="sxs-lookup"><span data-stu-id="4594e-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="4594e-141">На этапе 6 конвейера можно увидеть [таймер фильтра контрольных](http://www.nuget.org/packages/StopWatch/) данных.</span><span class="sxs-lookup"><span data-stu-id="4594e-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="4594e-142">Хотя мой таймер неплотности может предоставить полезные данные о профиле и времени, он пропустил все время, затраченное на авторизацию и визуализацию представления.</span><span class="sxs-lookup"><span data-stu-id="4594e-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="4594e-143">Вы можете прочитать сведения о своем таймере в [профиле и о том, как приложение ASP.NET MVC будет](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)доступно в Azure.</span><span class="sxs-lookup"><span data-stu-id="4594e-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="4594e-144">На странице [вкладок](http://getglimpse.com/Docs/Tabs) приводятся ссылки на подробные сведения о каждой вкладке.</span><span class="sxs-lookup"><span data-stu-id="4594e-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="4594e-145">Вкладка временной шкалы</span><span class="sxs-lookup"><span data-stu-id="4594e-145">The Timeline tab</span></span>

<span data-ttu-id="4594e-146">Я изменил Dykstra)ный [учебник по EF 6/MVC 5](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) с помощью следующего изменения кода в контроллере инструкторов:</span><span class="sxs-lookup"><span data-stu-id="4594e-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="4594e-147">Приведенный выше код позволяет мне передать строку запроса (`eager`) для управления загрузкой данных.</span><span class="sxs-lookup"><span data-stu-id="4594e-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="4594e-148">На приведенном ниже рисунке используется явная загрузка, и на странице времени отображаются все регистрации, загруженные в метод действия `Index`.</span><span class="sxs-lookup"><span data-stu-id="4594e-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![явная загрузка](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="4594e-150">В следующем коде указан параметр "безотлагательная", и каждая регистрация извлекается после вызова представления `Index`:</span><span class="sxs-lookup"><span data-stu-id="4594e-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![указана безотлагательная](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="4594e-152">Для получения подробных сведений о времени можно навести указатель мыши на отрезок времени:</span><span class="sxs-lookup"><span data-stu-id="4594e-152">You can hover over a time segment to get detailed timing information:</span></span>

![Наведите указатель мыши, чтобы просмотреть подробные сведения о времени](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="4594e-154">Привязка модели</span><span class="sxs-lookup"><span data-stu-id="4594e-154">Model Binding</span></span>

<span data-ttu-id="4594e-155">На [вкладке Привязка модели](http://getglimpse.com/Docs/Model-Binding-Tab) содержится множество сведений, которые помогут понять, как связаны переменные форм и почему некоторые из них не привязаны как можно скорее.</span><span class="sxs-lookup"><span data-stu-id="4594e-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="4594e-156">На рисунке ниже показана **?**</span><span class="sxs-lookup"><span data-stu-id="4594e-156">The image below shows the **?**</span></span> <span data-ttu-id="4594e-157">, который можно щелкнуть для открытия краткой страницы справки для этой функции.</span><span class="sxs-lookup"><span data-stu-id="4594e-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![Представление привязки модели краткого представления](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="4594e-159">Маршруты</span><span class="sxs-lookup"><span data-stu-id="4594e-159">Routes</span></span>

 <span data-ttu-id="4594e-160">Вкладка Общие маршруты поможет вам отлаживать и понимать маршрутизацию.</span><span class="sxs-lookup"><span data-stu-id="4594e-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="4594e-161">На рисунке ниже выбран маршрут продукта (и он отображается зеленым цветом, в кратком соглашении).</span><span class="sxs-lookup"><span data-stu-id="4594e-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="4594e-162">![выбрано имя продукта](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) ограничения маршрута, также отображаются области и маркеры данных.</span><span class="sxs-lookup"><span data-stu-id="4594e-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="4594e-163">Дополнительные сведения см. в разделе [краткие маршруты](http://getglimpse.com/Docs/Routes-Tab) и [Маршрутизация АТРИБУТОВ в ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4594e-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="4594e-164">Использование краткого описания в Azure</span><span class="sxs-lookup"><span data-stu-id="4594e-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="4594e-165">В краткой политике безопасности по умолчанию только данные краткости отображаются только с локального узла.</span><span class="sxs-lookup"><span data-stu-id="4594e-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="4594e-166">Вы можете изменить эту политику безопасности, чтобы просматривать эти данные на удаленном сервере (например, в веб-приложении Azure).</span><span class="sxs-lookup"><span data-stu-id="4594e-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="4594e-167">Для тестовых сред в Azure добавьте выделенную метку в нижнюю часть файла *Web. config* , чтобы включить параметр «краткий обзор»:</span><span class="sxs-lookup"><span data-stu-id="4594e-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.config* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="4594e-168">С учетом этого изменения любой пользователь может видеть данные на удаленном сайте.</span><span class="sxs-lookup"><span data-stu-id="4594e-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="4594e-169">Рассмотрите возможность добавления разметки выше в профиль публикации, чтобы она была развернута только при использовании этого профиля публикации (например, в тестовом профиле Azure). Чтобы ограничить данные краткого представления, мы добавим роль `canViewGlimpseData` и только пользователи этой роли могли просматривать данные о выпуске.</span><span class="sxs-lookup"><span data-stu-id="4594e-169">Consider adding the markup above to a publish profile so it's only deployed an applied when you use that publish profile (for example, your Azure test profile.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="4594e-170">Удалите комментарии из файла *GlimpseSecurityPolicy.CS* и измените вызов [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) с `Administrator` на роль `canViewGlimpseData`:</span><span class="sxs-lookup"><span data-stu-id="4594e-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="4594e-171">Безопасность. Расширенные данные, предоставляемые в кратком обзоре, могут предоставлять безопасность приложения.</span><span class="sxs-lookup"><span data-stu-id="4594e-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="4594e-172">Корпорация Майкрософт не выполнила аудит безопасности "краткий обзор" для использования в приложениях производства.</span><span class="sxs-lookup"><span data-stu-id="4594e-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>

<span data-ttu-id="4594e-173">Дополнительные сведения о добавлении ролей см. в руководстве [Развертывание веб-приложения Secure ASP.NET MVC 5 с помощью членства, OAuth и базы данных SQL в Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) .</span><span class="sxs-lookup"><span data-stu-id="4594e-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="4594e-174">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4594e-174">Additional Resources</span></span>

- [<span data-ttu-id="4594e-175">Развертывание безопасного приложения ASP.NET MVC 5 с членством, OAuth и базой данных SQL в Azure</span><span class="sxs-lookup"><span data-stu-id="4594e-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="4594e-176">[Краткий обзор конфигурации](http://getglimpse.com/Docs/Configuration) — страница документации по настройке вкладок, политика среды выполнения, ведение журнала и многое другое.</span><span class="sxs-lookup"><span data-stu-id="4594e-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
