---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Вспомогательное приложение Twitter с веб-страницы ASP.NET | Документация Майкрософт
author: Rick-Anderson
description: В этом разделе и приложении показано, как добавить вспомогательную функцию Twitter в проект WebMatrix 3. Он содержит вспомогательный код Twitter и показывает, как вызвать вспомогательную функцию...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518622"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="3f2c2-104">Добавление вспомогательного приложения Twitter с помощью веб-страниц ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3f2c2-104">Twitter Helper with ASP.NET Web Pages</span></span>

<span data-ttu-id="3f2c2-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3f2c2-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f2c2-106">Вспомогательные методы Twitter устарели.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-106">Twitter Helpers are obsolete.</span></span> <span data-ttu-id="3f2c2-107">Сведения о новейших средствах взаимодействия Twitter для веб-сайтов см. в [обзоре Twitter для веб-сайтов](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span><span class="sxs-lookup"><span data-stu-id="3f2c2-107">For Twitter's latest engagement tools for websites, see [Twitter for Websites Overview](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span></span>

> <span data-ttu-id="3f2c2-108">В этом разделе и приложении показано, как добавить вспомогательную функцию Twitter в проект WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-108">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="3f2c2-109">Он содержит вспомогательный код Twitter и показывает, как вызывать вспомогательные методы.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-109">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="3f2c2-110">Этот код для файла Twitter. cshtml был разработан **Тиан Pan** Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-110">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3f2c2-111">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="3f2c2-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3f2c2-112">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="3f2c2-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="3f2c2-113">Этот учебник также работает с веб-страницы ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="introduction"></a><span data-ttu-id="3f2c2-114">Введение</span><span class="sxs-lookup"><span data-stu-id="3f2c2-114">Introduction</span></span>

<span data-ttu-id="3f2c2-115">В этом разделе показано, как добавить в приложение вспомогательную функцию Twitter и использовать синтаксис Razor для вызова вспомогательных методов.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-115">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="3f2c2-116">Помощник Twitter упрощает включение в приложение кнопок и мини-приложений Twitter.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-116">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="3f2c2-117">Чтобы использовать мини-приложение Twitter, например временную шкалу пользователя или результаты поиска для хэш-тега, необходимо сначала создать мини-приложение [в Twitter](https://twitter.com/settings/widgets).</span><span class="sxs-lookup"><span data-stu-id="3f2c2-117">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="3f2c2-118">После создания мини-приложения вы получите его идентификатор. Идентификатор мини-приложения передается в качестве параметра при вызове вспомогательных методов, которые отображают мини-приложение.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-118">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="3f2c2-119">Этот раздел написан для версии 1,1 API Twitter.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-119">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="3f2c2-120">Непосредственно добавив в проект вспомогательный код Twitter, вы можете обновить вспомогательный код при изменении API Twitter.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-120">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="3f2c2-121">Дополнительные сведения об установке WebMatrix см. в разделе [Введение в веб-страницы ASP.NET 2-Начало работы](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f2c2-121">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="3f2c2-122">Добавление вспомогательного метода Twitter в проект</span><span class="sxs-lookup"><span data-stu-id="3f2c2-122">Add Twitter Helper to your project</span></span>

<span data-ttu-id="3f2c2-123">Чтобы добавить вспомогательный модуль Twitter, сначала добавьте папку с именем **App\_Code** в проект.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-123">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="3f2c2-124">Затем создайте файл с именем **Twitter. cshtml**.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-124">Then, create a file named **Twitter.cshtml**.</span></span>

![Папка App_Code](twitter-helper/_static/image1.png)

<span data-ttu-id="3f2c2-126">Замените код по умолчанию в Twitter. cshtml следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-126">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="3f2c2-127">Вызов методов Twitter с веб-страниц</span><span class="sxs-lookup"><span data-stu-id="3f2c2-127">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="3f2c2-128">В следующем примере показано, как использовать вспомогательные методы Twitter на странице в проекте.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-128">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="3f2c2-129">В проекте потребуется заменить значения параметров значениями, относящимися к вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-129">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="3f2c2-130">Вы можете использовать предоставленные идентификаторы мини-приложений, чтобы узнать, как работают методы, но вам потребуется создать собственные мини-приложения для проекта.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-130">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="3f2c2-131">Не все указанные ниже параметры являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-131">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="3f2c2-132">Необязательные параметры используются для настройки отображения кнопки или мини-приложения.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-132">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="3f2c2-133">Например, для кнопки "Далее" требуется только имя пользователя, но в примере показано, как включить число подписчиков и указать размер кнопки и языка.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-133">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="3f2c2-134">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="3f2c2-134">See the results</span></span>

<span data-ttu-id="3f2c2-135">Приведенный выше код создает следующие кнопки и мини-приложения.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-135">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="3f2c2-136">Эти кнопки и мини-приложения являются полнофункциональными, а не снимками экрана.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-136">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="3f2c2-137">Кнопка Далее отображается на испанском языке, так как для параметра Language задано значение **ES**.</span><span class="sxs-lookup"><span data-stu-id="3f2c2-137">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="3f2c2-138">Кнопка "Далее"</span><span class="sxs-lookup"><span data-stu-id="3f2c2-138">Follow Button</span></span>

<span data-ttu-id="3f2c2-139">[Следовать @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="3f2c2-139">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="3f2c2-140">Кнопка твита</span><span class="sxs-lookup"><span data-stu-id="3f2c2-140">Tweet Button</span></span>

<span data-ttu-id="3f2c2-141">[Твит](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="3f2c2-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="3f2c2-142">Временная шкала пользователя (профиль)</span><span class="sxs-lookup"><span data-stu-id="3f2c2-142">User Timeline (Profile)</span></span>

<span data-ttu-id="3f2c2-143">[Твиты по @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="3f2c2-143">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="3f2c2-144">Избранное</span><span class="sxs-lookup"><span data-stu-id="3f2c2-144">Favorites</span></span>

<span data-ttu-id="3f2c2-145">[Избранные твиты по @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="3f2c2-145">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="3f2c2-146">Список</span><span class="sxs-lookup"><span data-stu-id="3f2c2-146">List</span></span>

<span data-ttu-id="3f2c2-147">[Твиты из @Microsoft/MS\_\_](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="3f2c2-147">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="3f2c2-148">Поиск</span><span class="sxs-lookup"><span data-stu-id="3f2c2-148">Search</span></span>

<span data-ttu-id="3f2c2-149">[Твиты о &quot;#asp&quot;.net](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="3f2c2-149">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
