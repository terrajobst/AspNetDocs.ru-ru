---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: Создание доступных для чтения URL-адресов на сайтах веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой статье описывается маршрутизация на веб-сайте веб-страницы ASP.NET (Razor) и объясняется, как это позволяет использовать URL-адреса, которые более удобочитаемы и лучше подходят для SEO. Что вы...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509910"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="c21bc-104">Создание доступных для чтения URL-адресов на сайтах веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="c21bc-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="c21bc-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c21bc-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c21bc-106">В этой статье описывается маршрутизация на веб-сайте веб-страницы ASP.NET (Razor) и объясняется, как это позволяет использовать URL-адреса, которые более удобочитаемы и лучше подходят для SEO.</span><span class="sxs-lookup"><span data-stu-id="c21bc-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="c21bc-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="c21bc-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c21bc-108">Как ASP.NET использует маршрутизацию, чтобы использовать более удобочитаемые и доступные для поиска URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c21bc-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c21bc-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="c21bc-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c21bc-110">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="c21bc-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="c21bc-111">Этот учебник также работает с веб-страницы ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="c21bc-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-routing"></a><span data-ttu-id="c21bc-112">О маршрутизации</span><span class="sxs-lookup"><span data-stu-id="c21bc-112">About Routing</span></span>

<span data-ttu-id="c21bc-113">URL-адреса страниц сайта могут оказать влияние на то, насколько хорошо работает сайт.</span><span class="sxs-lookup"><span data-stu-id="c21bc-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="c21bc-114">URL-адрес, &quot;понятный&quot; может облегчить пользователям работу с сайтом.</span><span class="sxs-lookup"><span data-stu-id="c21bc-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="c21bc-115">Он также может помочь в оптимизации поисковой системы для сайта.</span><span class="sxs-lookup"><span data-stu-id="c21bc-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="c21bc-116">Веб-сайты ASP.NET включают возможность автоматического использования удобных URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="c21bc-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="c21bc-117">ASP.NET позволяет создавать понятные URL-адреса, описывающие действия пользователя, а не указывать на файл на сервере.</span><span class="sxs-lookup"><span data-stu-id="c21bc-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="c21bc-118">Рассмотрим эти URL-адреса для вымышленного блога:</span><span class="sxs-lookup"><span data-stu-id="c21bc-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="c21bc-119">Сравните эти URL-адреса со следующими:</span><span class="sxs-lookup"><span data-stu-id="c21bc-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="c21bc-120">В первой паре пользователю нужно было бы убедиться, что блог отображается с помощью страницы *Blog. cshtml* , а затем создать строку запроса, которая получает нужную категорию или диапазон дат.</span><span class="sxs-lookup"><span data-stu-id="c21bc-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="c21bc-121">Второй набор примеров гораздо проще в восприятии и создании.</span><span class="sxs-lookup"><span data-stu-id="c21bc-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="c21bc-122">URL-адреса для первого примера также указывают непосредственно на конкретный файл (*Blog. cshtml*).</span><span class="sxs-lookup"><span data-stu-id="c21bc-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="c21bc-123">Если по какой-либо причине блог был перемещен в другую папку на сервере или если блог был переписан для использования другой страницы, то ссылки будут неправильными.</span><span class="sxs-lookup"><span data-stu-id="c21bc-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="c21bc-124">Второй набор URL-адресов не указывает на определенную страницу, поэтому даже в случае изменения реализации или расположения блога эти URL-адреса будут действительны.</span><span class="sxs-lookup"><span data-stu-id="c21bc-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="c21bc-125">В веб-страницы ASP.NET можно создать более понятные URL-адреса, аналогичные тем, которые приведены в приведенных выше примерах, так как ASP.NET использует *маршрутизацию*.</span><span class="sxs-lookup"><span data-stu-id="c21bc-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="c21bc-126">Маршрутизация создает логическое сопоставление URL-адреса со страницей (или страницами), которая может выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="c21bc-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="c21bc-127">Так как сопоставление является логическим (не физическим, в определенный файл), маршрутизация обеспечивает большую гибкость в определении URL-адресов для сайта.</span><span class="sxs-lookup"><span data-stu-id="c21bc-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="c21bc-128">Принцип работы маршрутизации</span><span class="sxs-lookup"><span data-stu-id="c21bc-128">How Routing Works</span></span>

<span data-ttu-id="c21bc-129">Когда ASP.NET обрабатывает запрос, он считывает URL-адрес, чтобы определить, как его маршрутизировать.</span><span class="sxs-lookup"><span data-stu-id="c21bc-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="c21bc-130">ASP.NET пытается сопоставить отдельные сегменты URL-адреса с файлами на диске, идущие слева направо.</span><span class="sxs-lookup"><span data-stu-id="c21bc-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="c21bc-131">При наличии совпадения все остальные данные URL-адреса передаются на страницу в качестве *сведений о пути*.</span><span class="sxs-lookup"><span data-stu-id="c21bc-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="c21bc-132">Представьте себе, что кто-то выполняет запрос с помощью этого URL:</span><span class="sxs-lookup"><span data-stu-id="c21bc-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="c21bc-133">Поиск выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c21bc-133">The search goes like this:</span></span>

1. <span data-ttu-id="c21bc-134">Существует ли файл с путем и именем */а/б/к.кштмл*?</span><span class="sxs-lookup"><span data-stu-id="c21bc-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="c21bc-135">Если это так, запустите эту страницу и передайте в нее сведения.</span><span class="sxs-lookup"><span data-stu-id="c21bc-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="c21bc-136">В противном случае...</span><span class="sxs-lookup"><span data-stu-id="c21bc-136">Otherwise ...</span></span>
2. <span data-ttu-id="c21bc-137">Существует ли файл с путем и именем */а/б.кштмл*?</span><span class="sxs-lookup"><span data-stu-id="c21bc-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="c21bc-138">Если это так, запустите эту страницу и передайте в нее значение `c`.</span><span class="sxs-lookup"><span data-stu-id="c21bc-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="c21bc-139">В противном случае...</span><span class="sxs-lookup"><span data-stu-id="c21bc-139">Otherwise …</span></span>
3. <span data-ttu-id="c21bc-140">Существует ли файл с путем и именем */а.кштмл*?</span><span class="sxs-lookup"><span data-stu-id="c21bc-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="c21bc-141">Если это так, запустите эту страницу и передайте в нее значение `b/c`.</span><span class="sxs-lookup"><span data-stu-id="c21bc-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="c21bc-142">Если поиск не нашел точных соответствий для файлов *. cshtml* в указанных папках, ASP.NET продолжит поиск этих файлов в свою очередь:</span><span class="sxs-lookup"><span data-stu-id="c21bc-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="c21bc-143">*/а/б/к/дефаулт.кштмл* (нет сведений о пути).</span><span class="sxs-lookup"><span data-stu-id="c21bc-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="c21bc-144">*/а/б/к/индекс.кштмл* (нет сведений о пути).</span><span class="sxs-lookup"><span data-stu-id="c21bc-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="c21bc-145">Чтобы быть ясным, запросы к конкретным страницам (т. е. запросы, включающие расширение имени файла *. cshtml* ) работают точно так же, как и следовало бы ожидать.</span><span class="sxs-lookup"><span data-stu-id="c21bc-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="c21bc-146">Запрос, подобный `http://www.contoso.com/a/b.cshtml`, просто выполнит страницу *b. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="c21bc-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>

<span data-ttu-id="c21bc-147">На странице можно получить сведения о пути с помощью свойства `UrlData` страницы, которое является словарем.</span><span class="sxs-lookup"><span data-stu-id="c21bc-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="c21bc-148">Представьте, что у вас есть файл с именем *виевкустомерс. cshtml* , и ваш сайт получает этот запрос:</span><span class="sxs-lookup"><span data-stu-id="c21bc-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="c21bc-149">Как описано в приведенных выше правилах, запрос будет отправлен на страницу.</span><span class="sxs-lookup"><span data-stu-id="c21bc-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="c21bc-150">На странице можно использовать следующий код для получения и вывода сведений о пути (в данном случае это значение &quot;1000&quot;):</span><span class="sxs-lookup"><span data-stu-id="c21bc-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="c21bc-151">Поскольку маршрутизация не включает полные имена файлов, может быть неоднозначность при наличии страниц с одинаковыми именами, но разными расширениями имен файлов (например, *MyPage. cshtml* и *MyPage. HTML*).</span><span class="sxs-lookup"><span data-stu-id="c21bc-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="c21bc-152">Чтобы избежать проблем с маршрутизацией, рекомендуется убедиться в отсутствии страниц на сайте, имена которых отличаются только расширением.</span><span class="sxs-lookup"><span data-stu-id="c21bc-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c21bc-153">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c21bc-153">Additional Resources</span></span>

<span data-ttu-id="c21bc-154">[WebMatrix — URL-адреса, урлдата и маршрутизация для SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span><span class="sxs-lookup"><span data-stu-id="c21bc-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="c21bc-155">В этой записи блога от Mike Бринд содержатся некоторые дополнительные сведения о том, как работает маршрутизация в веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c21bc-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
