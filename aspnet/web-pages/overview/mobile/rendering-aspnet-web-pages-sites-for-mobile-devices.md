---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: Отрисовки ASP.NET Web Pages (Razor) сайтов для мобильных устройств | Документация Майкрософт
author: Rick-Anderson
description: 'В этой статье описывается создание страниц на сайте веб-страниц ASP.NET (Razor), будут отображаться правильно на мобильных устройствах. Вы узнаете, как: Как вы...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: dbcd25331387f8606343e551302bc3ed1f9b2c25
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59379512"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="fdfb3-104">Подготовка к просмотру ASP.NET Web Pages (Razor) сайтов для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="fdfb3-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="fdfb3-105">по [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fdfb3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="fdfb3-106">В этой статье описывается создание страниц на сайте веб-страниц ASP.NET (Razor), будут отображаться правильно на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="fdfb3-107">Вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="fdfb3-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="fdfb3-108">Как использовать соглашения об именовании позволяет указать, что страницы разработан специально для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fdfb3-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="fdfb3-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fdfb3-110">Веб-страниц ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="fdfb3-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="fdfb3-111">Этот учебник также работает с ASP.NET Web Pages 2.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="fdfb3-112">Веб-страницы ASP.NET позволяет создавать пользовательские отображение для отображения содержимого на мобильный или других устройств.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="fdfb3-113">Самый простой способ создать страницу конкретного устройства, на сайте веб-страниц ASP.NET — с помощью шаблона именования файлов следующим образом: *FileName.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="fdfb3-114">Можно создать две версии страницы (например, один с именем *MyFile.cshtml* и один с именем *MyFile.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="fdfb3-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="fdfb3-115">Во время выполнения, когда мобильное устройство запрашивает *MyFile.cshtml*, ASP.NET отображает содержимое из *MyFile.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="fdfb3-116">В противном случае *MyFile.cshtml* визуализации.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="fdfb3-117">Приведенный ниже показано, как включить отрисовку мобильных устройств, добавив страницу содержимого для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="fdfb3-118">*Page1.cshtml* содержит содержимое, а также боковая панель навигации.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="fdfb3-119">*Page1.Mobile.cshtml* с тем же содержимым, но пропускает боковой панели.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="fdfb3-120">На сайте веб-страниц ASP.NET, создайте файл с именем *Page1.cshtml* и замените текущее содержимое следующей разметкой.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="fdfb3-121">Создайте файл с именем *Page1.Mobile.cshtml* и замените существующее содержимое следующей разметкой.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="fdfb3-122">Обратите внимание на то, что мобильную версию страницы пропускает раздел перехода для повышения подготовки к просмотру на экране меньшего размера.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="fdfb3-123">Запустите классический браузер и перейдите к *Page1.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="fdfb3-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fdfb3-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="fdfb3-125">Запустите браузер мобильного устройства (или эмулятор мобильных устройств) и перейдите к *Page1.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="fdfb3-126">(Обратите внимание, что отсутствует *.mobile.*</span><span class="sxs-lookup"><span data-stu-id="fdfb3-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="fdfb3-127">как часть URL-адрес.) Несмотря на то, что этот запрос поступает в *Page1.cshtml*, ASP.NET отображает *Page1.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="fdfb3-129">Чтобы протестировать страницах для мобильных устройств, можно использовать имитатор мобильных устройств, который выполняется на настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="fdfb3-130">Эта программа предназначена для тестирования веб-страниц, так как они выглядели на мобильных устройствах (то есть обычно намного меньше с область отображается).</span><span class="sxs-lookup"><span data-stu-id="fdfb3-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="fdfb3-131">Одним из примеров симулятор является [надстройки переключателя между агентом пользователя](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) для Mozilla Firefox, которая позволяет моделировать различные браузеры для мобильных устройств из версии Firefox для настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="fdfb3-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="fdfb3-132">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fdfb3-132">Additional Resources</span></span>


<span data-ttu-id="fdfb3-133">[Эмулятор Windows Phone](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="fdfb3-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
