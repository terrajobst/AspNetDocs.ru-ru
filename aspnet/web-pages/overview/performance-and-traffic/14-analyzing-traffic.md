---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: Отслеживание информации посетителей (аналитика) для сайта веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: После того как веб-сайт будет загружен, может потребоваться проанализировать трафик веб-сайта.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421458"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="0c0a9-103">Отслеживание информации посетителей (аналитика) для сайта веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="0c0a9-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="0c0a9-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0c0a9-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0c0a9-105">В этой статье описывается, как с помощью вспомогательной службы добавить аналитику веб-сайта на страницы на веб-сайте веб-страницы ASP.NET (Razor).</span><span class="sxs-lookup"><span data-stu-id="0c0a9-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="0c0a9-106">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="0c0a9-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="0c0a9-107">Отправка сведений о трафике веб-сайта поставщику аналитики.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="0c0a9-108">Это функции программирования ASP.NET, представленные в статье:</span><span class="sxs-lookup"><span data-stu-id="0c0a9-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="0c0a9-109">Вспомогательный метод `Analytics`.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0c0a9-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="0c0a9-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0c0a9-111">Веб-страницы ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="0c0a9-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="0c0a9-112">Библиотека вспомогательных веб-функций ASP.NET (пакет NuGet)</span><span class="sxs-lookup"><span data-stu-id="0c0a9-112">ASP.NET Web Helpers Library (NuGet package)</span></span>

<span data-ttu-id="0c0a9-113">Аналитика — это общий термин для технологий, которые измеряют трафик на веб-сайте, чтобы вы могли понять, как люди используют этот сайт.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="0c0a9-114">Доступны многие службы аналитики, включая службы из Google, Yahoo, Статкаунтер и других.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="0c0a9-115">Способ работы с аналитикой заключается в том, что вы регистрируетесь в учетной записи с поставщиком аналитики, в которой выполняется регистрация сайта, который необходимо отвестиь. Поставщик отправляет вам фрагмент кода JavaScript, который включает идентификатор или код отслеживания для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="0c0a9-116">Фрагмент кода JavaScript добавляется на веб-страницы сайта, которые необходимо отслеживанию. (Обычно фрагмент анализа добавляется в нижний колонтитул или страницу макета или в другую разметку HTML, которая отображается на каждой странице сайта.) Когда пользователь запрашивает страницу, содержащую один из этих фрагментов кода JavaScript, фрагмент отправляет сведения о текущей странице поставщику аналитики, который записывает различные сведения о странице.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="0c0a9-117">Если вы хотите просмотреть статистику вашего сайта, войдите на веб-сайт поставщика аналитики.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="0c0a9-118">Затем можно просмотреть все виды отчетов о вашем сайте, например:</span><span class="sxs-lookup"><span data-stu-id="0c0a9-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="0c0a9-119">Число просмотров страниц для отдельных страниц.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-119">The number of page views for individual pages.</span></span> <span data-ttu-id="0c0a9-120">Это говорит вам (примерно), сколько людей посещает сайт, а какие страницы на вашем сайте являются наиболее популярными.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="0c0a9-121">Как долго люди тратят на определенные страницы.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-121">How long people spend on specific pages.</span></span> <span data-ttu-id="0c0a9-122">Это может сообщать вам о том, что домашняя страница сохраняет интерес людей.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="0c0a9-123">Какие сайты находились до посещения вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="0c0a9-124">Это поможет понять, поступает ли трафик из ссылок, от поиска и т. д.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="0c0a9-125">Когда пользователи посещают ваш сайт и как долго они остаются.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="0c0a9-126">В каких странах находятся ваши посетители.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="0c0a9-127">Какие браузеры и операционные системы используют посетители.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="0c0a9-129">Использование вспомогательного метода для добавления аналитики на страницу</span><span class="sxs-lookup"><span data-stu-id="0c0a9-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="0c0a9-130">Веб-страницы ASP.NET включает несколько вспомогательных функций аналитики (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`и `Analytics.GetStatCounterHtml`), которые упрощают управление фрагментами кода JavaScript, используемыми для аналитики.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="0c0a9-131">Вместо того чтобы понять, как и где поместить код JavaScript, достаточно добавить вспомогательную функцию на страницу.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="0c0a9-132">Единственными сведениями, которые необходимо предоставить, являются имя учетной записи, идентификатор или код отслеживания.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="0c0a9-133">(Для Статкаунтер также необходимо указать несколько дополнительных значений.)</span><span class="sxs-lookup"><span data-stu-id="0c0a9-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="0c0a9-134">В этой процедуре вы создадите страницу макета, использующую вспомогательную функцию `GetGoogleHtml`.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="0c0a9-135">Если у вас уже есть учетная запись с одним из других поставщиков аналитики, можно использовать эту учетную запись и при необходимости внести незначительные изменения.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="0c0a9-136">При создании учетной записи аналитики необходимо зарегистрировать URL-адрес сайта, который требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="0c0a9-137">Если вы тестируете все на локальном компьютере, вы не отслеживаете фактический трафик (единственный трафик), поэтому вы не сможете записывать и просматривать статистику сайта.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="0c0a9-138">Но эта процедура показывает, как добавить вспомогательную функцию аналитики на страницу.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="0c0a9-139">При публикации сайта активный сайт будет передавать сведения поставщику аналитики.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-139">When you publish your site, the live site will send information to your analytics provider.</span></span>

1. <span data-ttu-id="0c0a9-140">Добавьте библиотеку вспомогательных веб-функций ASP.NET на веб-сайт, как описано в разделе [Установка вспомогательных функций на веб-страницы ASP.net сайте](https://go.microsoft.com/fwlink/?LinkId=252372), если вы еще не добавили его.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="0c0a9-141">Создайте учетную запись с помощью Google Analytics и запишите имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="0c0a9-142">Создайте страницу макета с именем *Analytics. cshtml* и добавьте следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="0c0a9-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="0c0a9-143">Необходимо поместить вызов вспомогательного метода `Analytics` в тексте веб-страницы (перед тегом `</body>`).</span><span class="sxs-lookup"><span data-stu-id="0c0a9-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="0c0a9-144">В противном случае браузер не будет выполнять скрипт.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="0c0a9-145">Если вы используете другой поставщик аналитики, воспользуйтесь одним из следующих вспомогательных функций:</span><span class="sxs-lookup"><span data-stu-id="0c0a9-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="0c0a9-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="0c0a9-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="0c0a9-147">(Статкаунтер) `@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="0c0a9-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="0c0a9-148">Замените `myaccount` именем учетной записи, идентификатора или кода отслеживания, созданного на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="0c0a9-149">Запустите страницу в браузере.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-149">Run the page in the browser.</span></span> <span data-ttu-id="0c0a9-150">(Перед выполнением страницы убедитесь, что она выбрана в рабочей области **файлы** .)</span><span class="sxs-lookup"><span data-stu-id="0c0a9-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="0c0a9-151">В браузере просмотрите источник страницы.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-151">In the browser, view the page source.</span></span> <span data-ttu-id="0c0a9-152">Вы сможете увидеть готовый аналитический код:</span><span class="sxs-lookup"><span data-stu-id="0c0a9-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="0c0a9-153">Войдите на сайт Google Analytics и просмотрите статистику для своего сайта.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="0c0a9-154">Если вы используете страницу на активном сайте, вы увидите запись, которая записывает посетить страницу.</span><span class="sxs-lookup"><span data-stu-id="0c0a9-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="0c0a9-155">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0c0a9-155">Additional Resources</span></span>

- [<span data-ttu-id="0c0a9-156">Сайт Google Analytics</span><span class="sxs-lookup"><span data-stu-id="0c0a9-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="0c0a9-157">Сайт веб-аналитики Yahoo!</span><span class="sxs-lookup"><span data-stu-id="0c0a9-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="0c0a9-158">Сайт Статкаунтер</span><span class="sxs-lookup"><span data-stu-id="0c0a9-158">StatCounter site</span></span>](http://statcounter.com/)
