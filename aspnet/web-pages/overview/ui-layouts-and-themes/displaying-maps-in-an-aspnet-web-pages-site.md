---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: Отображение карт на сайте веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой статье объясняется, как отобразить Интерактивные карты на страницах на веб-сайте веб-страницы ASP.NET (Razor) на основе служб сопоставления, предоставляемых Bing, Google, MA...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518724"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="3668c-103">Отображение карт на сайте веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="3668c-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="3668c-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3668c-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3668c-105">В этой статье объясняется, как отображать Интерактивные карты на страницах на веб-сайте веб-страницы ASP.NET (Razor) на основе служб сопоставления, предоставляемых Bing, Google, Мапкуест и Yahoo.</span><span class="sxs-lookup"><span data-stu-id="3668c-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="3668c-106">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="3668c-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3668c-107">Создание схемы на основе адреса.</span><span class="sxs-lookup"><span data-stu-id="3668c-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="3668c-108">Как создать карту на основе координат широты и долготы.</span><span class="sxs-lookup"><span data-stu-id="3668c-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="3668c-109">Как зарегистрировать учетную запись разработчика карт Bing и получить ключ для использования с картами Bing.</span><span class="sxs-lookup"><span data-stu-id="3668c-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="3668c-110">Это функция ASP.NET, представленная в статье:</span><span class="sxs-lookup"><span data-stu-id="3668c-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="3668c-111">Вспомогательный метод `Maps`.</span><span class="sxs-lookup"><span data-stu-id="3668c-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3668c-112">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="3668c-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3668c-113">Веб-страницы ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="3668c-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="3668c-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="3668c-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="3668c-115">Этот учебник также работает с WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="3668c-115">This tutorial also works with WebMatrix 3.</span></span>

<span data-ttu-id="3668c-116">На веб-страницах карты можно отображать на странице с помощью `Maps` вспомогательного метода.</span><span class="sxs-lookup"><span data-stu-id="3668c-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="3668c-117">Карты можно создавать на основе адреса или набора координат долготы и широты.</span><span class="sxs-lookup"><span data-stu-id="3668c-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="3668c-118">Класс `Maps` позволяет вызывать популярные обработчики карт, включая Bing, Google, Мапкуест и Yahoo.</span><span class="sxs-lookup"><span data-stu-id="3668c-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="3668c-119">Действия по добавлению сопоставления со страницей одинаковы независимо от того, какие обработчики карты вызываются.</span><span class="sxs-lookup"><span data-stu-id="3668c-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="3668c-120">Просто добавьте ссылку на файл JavaScript, которая предоставляет доступные методы для отображения схемы, а затем вызовите методы вспомогательного метода `Maps`.</span><span class="sxs-lookup"><span data-stu-id="3668c-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="3668c-121">Вы выбираете службу Map, основанную на используемом вспомогательном методе `Maps`.</span><span class="sxs-lookup"><span data-stu-id="3668c-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="3668c-122">Можно использовать любой из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3668c-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="3668c-123">Установка необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="3668c-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="3668c-124">Чтобы отобразить карты, необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="3668c-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="3668c-125">Вспомогательный метод `Maps`.</span><span class="sxs-lookup"><span data-stu-id="3668c-125">The `Maps` helper.</span></span> <span data-ttu-id="3668c-126">Этот вспомогательный метод находится в версии 2 библиотеки веб-помощников ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3668c-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="3668c-127">Если вы еще не добавили библиотеку, ее можно установить на сайте в качестве пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="3668c-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="3668c-128">Дополнительные сведения см. [в разделе Установка вспомогательных функций на веб-страницы ASP.net сайте](https://go.microsoft.com/fwlink/?LinkId=252372).</span><span class="sxs-lookup"><span data-stu-id="3668c-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="3668c-129">(В коллекции найдите пакет `microsoft-web-helpers`).</span><span class="sxs-lookup"><span data-stu-id="3668c-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="3668c-130">Библиотека jQuery.</span><span class="sxs-lookup"><span data-stu-id="3668c-130">The jQuery library.</span></span> <span data-ttu-id="3668c-131">Некоторые шаблоны сайтов WebMatrix уже содержат библиотеки jQuery в своих папках *сценариев* .</span><span class="sxs-lookup"><span data-stu-id="3668c-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="3668c-132">Если эти библиотеки отсутствуют, вы можете скачать последнюю библиотеку jQuery непосредственно с сайта [jQuery.org](http://jQuery.org) .</span><span class="sxs-lookup"><span data-stu-id="3668c-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="3668c-133">Или можно создать новый сайт с помощью шаблона (например, шаблона **начального сайта** ), а затем скопировать файлы jQuery с этого сайта на текущий сайт.</span><span class="sxs-lookup"><span data-stu-id="3668c-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="3668c-134">Наконец, если вы хотите использовать карты Bing, сначала необходимо создать (бесплатную) учетную запись и получить ключ.</span><span class="sxs-lookup"><span data-stu-id="3668c-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="3668c-135">Чтобы получить ключ, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3668c-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="3668c-136">Создайте учетную запись для [учетной записи разработчика карт Bing](https://www.microsoft.com/maps/developers/web.aspx).</span><span class="sxs-lookup"><span data-stu-id="3668c-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="3668c-137">Необходимо также иметь учетная запись Майкрософт (Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="3668c-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="3668c-138">Вы можете указать, что вы хотите использовать ключ для **оценки или тестирования**.</span><span class="sxs-lookup"><span data-stu-id="3668c-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="3668c-139">Если вы тестируете функцию сопоставления на своем компьютере с помощью WebMatrix и IIS Express, перейдите в рабочую область **сайт** и запишите URL-адрес сайта (например, `http://localhost:50408`, хотя номер порта, скорее всего, будет отличаться).</span><span class="sxs-lookup"><span data-stu-id="3668c-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="3668c-140">Этот адрес *localhost* можно использовать в качестве сайта при регистрации.</span><span class="sxs-lookup"><span data-stu-id="3668c-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="3668c-141">После регистрации учетной записи перейдите в центр учетных записей карт Bing и щелкните **создать или просмотреть ключи**:</span><span class="sxs-lookup"><span data-stu-id="3668c-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![сопоставление — 2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="3668c-143">Запишите ключ, создаваемый Bing.</span><span class="sxs-lookup"><span data-stu-id="3668c-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="3668c-144">Создание схемы на основе адреса (с помощью Google)</span><span class="sxs-lookup"><span data-stu-id="3668c-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="3668c-145">В следующем примере показано, как создать страницу, которая визуализирует карту на основе адреса.</span><span class="sxs-lookup"><span data-stu-id="3668c-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="3668c-146">В этом примере показано, как использовать карты Google.</span><span class="sxs-lookup"><span data-stu-id="3668c-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="3668c-147">Создайте файл с именем *мападдресс. cshtml* в корневом каталоге сайта.</span><span class="sxs-lookup"><span data-stu-id="3668c-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="3668c-148">Эта страница создаст карту на основе адреса, который вы передали.</span><span class="sxs-lookup"><span data-stu-id="3668c-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="3668c-149">Скопируйте следующий код в файл, перезаписав имеющееся содержимое.</span><span class="sxs-lookup"><span data-stu-id="3668c-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="3668c-150">Обратите внимание на следующие возможности страницы:</span><span class="sxs-lookup"><span data-stu-id="3668c-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="3668c-151">Элемент `<script>` в элементе `<head>`.</span><span class="sxs-lookup"><span data-stu-id="3668c-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="3668c-152">В примере элемент `<script>` ссылается на файл *жкуери-1.6.4. min. js* , который представляет собой минифицированные (сжатую) версию библиотеки jQuery версии 1.6.4.</span><span class="sxs-lookup"><span data-stu-id="3668c-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="3668c-153">Обратите внимание, что в ссылке предполагается, что *JS* -файл находится в папке *Scripts* вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="3668c-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="3668c-154">Если вы используете другую версию библиотеки jQuery, просто убедитесь, что вы указали на эту версию правильно.</span><span class="sxs-lookup"><span data-stu-id="3668c-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="3668c-155">Вызов `@Maps.GetGoogleHtml` в тексте страницы.</span><span class="sxs-lookup"><span data-stu-id="3668c-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="3668c-156">Для отображения адреса необходимо передать строку адреса.</span><span class="sxs-lookup"><span data-stu-id="3668c-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="3668c-157">Методы других механизмов карт работают аналогичным образом (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span><span class="sxs-lookup"><span data-stu-id="3668c-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="3668c-158">Запустите страницу и введите адрес.</span><span class="sxs-lookup"><span data-stu-id="3668c-158">Run the page and enter an address.</span></span> <span data-ttu-id="3668c-159">На странице отображается карта на основе Google Maps, которая показывает указанное расположение.</span><span class="sxs-lookup"><span data-stu-id="3668c-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![сопоставление — 1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="3668c-161">Создание карты на основе координат широты и долготы (с помощью Bing)</span><span class="sxs-lookup"><span data-stu-id="3668c-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="3668c-162">В этом примере показано, как создать карту на основе координат.</span><span class="sxs-lookup"><span data-stu-id="3668c-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="3668c-163">В этом примере показано, как использовать карты Bing и как включить ключ Bing.</span><span class="sxs-lookup"><span data-stu-id="3668c-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="3668c-164">(Карту можно создать на основе координат с помощью других механизмов карт, не используя ключ Bing.)</span><span class="sxs-lookup"><span data-stu-id="3668c-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="3668c-165">Создайте файл с именем *мапкурдинатес. cshtml* в корневом каталоге сайта и замените имеющееся содержимое следующим кодом и разметкой:</span><span class="sxs-lookup"><span data-stu-id="3668c-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="3668c-166">Замените `your-key-here` ключом Bing Maps, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="3668c-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="3668c-167">Запустите страницу *мапкурдинатес. cshtml* , введите координаты широты и долготы, а затем щелкните **Map!** .</span><span class="sxs-lookup"><span data-stu-id="3668c-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="3668c-168">.</span><span class="sxs-lookup"><span data-stu-id="3668c-168">button.</span></span> <span data-ttu-id="3668c-169">(Если вы не знакомы с координатами, попробуйте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="3668c-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="3668c-170">Это расположение в кампусе Microsoft Redmond.)</span><span class="sxs-lookup"><span data-stu-id="3668c-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="3668c-171">Широта: 47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="3668c-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="3668c-172">Долгота:-122.158317565918</span><span class="sxs-lookup"><span data-stu-id="3668c-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="3668c-173">Страница отображается с использованием указанных координат.</span><span class="sxs-lookup"><span data-stu-id="3668c-173">The page is displayed using the coordinates that you specified.</span></span>

     ![Сопоставление — 3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="3668c-175">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3668c-175">Additional Resources</span></span>

[<span data-ttu-id="3668c-176">Справочник по API Microsoft. Maps</span><span class="sxs-lookup"><span data-stu-id="3668c-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
