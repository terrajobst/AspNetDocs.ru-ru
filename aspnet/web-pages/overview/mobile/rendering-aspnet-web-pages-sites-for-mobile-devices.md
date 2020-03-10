---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: Подготовка сайтов веб-страницы ASP.NET (Razor) для мобильных устройств | Документация Майкрософт
author: Rick-Anderson
description: 'В этой статье описывается создание страниц на веб-сайте веб-страницы ASP.NET (Razor), который будет правильно отображаться на мобильных устройствах. Что вы узнаете: как вы...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454356"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="b6ec4-104">Подготовка сайтов веб-страницы ASP.NET (Razor) для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="b6ec4-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="b6ec4-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b6ec4-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b6ec4-106">В этой статье описывается создание страниц на веб-сайте веб-страницы ASP.NET (Razor), который будет правильно отображаться на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="b6ec4-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="b6ec4-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="b6ec4-108">Использование соглашения об именовании для указания того, что страница разработана специально для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b6ec4-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="b6ec4-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b6ec4-110">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="b6ec4-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="b6ec4-111">Этот учебник также работает с веб-страницы ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="b6ec4-112">Веб-страницы ASP.NET позволяет создавать пользовательские экраны для отображения содержимого на мобильных или других устройствах.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="b6ec4-113">Самым простым способом создания страницы для конкретного устройства на веб-страницы ASP.NET сайте является использование такого шаблона именования файлов: *filename. Mobile. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="b6ec4-114">Можно создать две версии страницы (например, One с именем *MyFile. cshtml* и один с именем *MyFile. Mobile. cshtml*).</span><span class="sxs-lookup"><span data-stu-id="b6ec4-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="b6ec4-115">Во время выполнения, когда мобильное устройство запрашивает *MyFile. cshtml*, ASP.NET визуализирует содержимое из *MyFile. Mobile. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="b6ec4-116">В противном случае отображается *MyFile. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="b6ec4-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="b6ec4-117">В следующем примере показано, как включить отрисовку для мобильных устройств, добавив страницу содержимого на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="b6ec4-118">Элемент «страница *. cshtml* » содержит содержимое и боковую панель навигации.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="b6ec4-119">Параметр "элемент *. Mobile. cshtml* " содержит то же содержимое, но не имеет боковой панели.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="b6ec4-120">На веб-страницы ASP.NET сайте создайте файл с именем "код страницы *. cshtml* " и замените текущее содержимое следующей разметкой.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="b6ec4-121">Создайте файл с именем " *. Mobile. cshtml* " и замените имеющееся содержимое следующей разметкой.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="b6ec4-122">Обратите внимание, что мобильная версия страницы не охватывает раздел навигации для лучшей отрисовки на меньшем экране.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="b6ec4-123">Запустите браузер для настольных систем и перейдите по адресу "^ *. cshtml*".</span><span class="sxs-lookup"><span data-stu-id="b6ec4-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="b6ec4-124">![мобилеситес-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b6ec4-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="b6ec4-125">Запустите браузер для мобильных устройств (или эмулятор мобильного устройства) и перейдите по адресу "^ *. cshtml*".</span><span class="sxs-lookup"><span data-stu-id="b6ec4-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="b6ec4-126">(Обратите внимание, что вы не включаете *. Mobile.*</span><span class="sxs-lookup"><span data-stu-id="b6ec4-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="b6ec4-127">как часть URL-адреса.) Несмотря на то, что запрос имеет значение "No @ *. cshtml*", ASP.NET визуализирует. *Mobile. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![мобилеситес-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="b6ec4-129">Для тестирования страниц мобильных устройств можно использовать симулятор мобильных устройств, работающий на настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="b6ec4-130">Это средство позволяет тестировать веб-страницы так, как они будут выглядеть на мобильных устройствах (то есть обычно с значительно меньшей областью отображения).</span><span class="sxs-lookup"><span data-stu-id="b6ec4-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="b6ec4-131">Одним из примеров симулятора является [надстройка агента пользователя](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) для Mozilla Firefox, которая позволяет эмулировать различные мобильные браузеры из классической версии Firefox.</span><span class="sxs-lookup"><span data-stu-id="b6ec4-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="b6ec4-132">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b6ec4-132">Additional Resources</span></span>

<span data-ttu-id="b6ec4-133">[Эмулятор Windows Phone](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="b6ec4-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
