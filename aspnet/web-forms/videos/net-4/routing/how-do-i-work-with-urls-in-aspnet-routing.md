---
uid: web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
title: Инструкции. Работа с URL-адресами в маршрутизации ASP.NET | Документы Майкрософт
author: rick-anderson
description: В этом видеоролике Крис пикселей показано, как указать URL-адреса на сайте, использующем маршрутизацию ASP.NET. Сначала создается веб-сайт, а маршрутизация определяется в GL...
ms.author: riande
ms.date: 10/15/2010
ms.assetid: 08f9d0a7-cfa0-4914-a672-8a64295d7ba8
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
msc.type: video
ms.openlocfilehash: eb1060fd9cc9469dc2b1d2e918823316c36840cb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455694"
---
# <a name="how-do-i-work-with-urls-in-aspnet-routing"></a><span data-ttu-id="c90e5-105">Инструкции. Работа с URL-адресами в маршрутизации ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c90e5-105">How Do I: Work with URLs in ASP.NET Routing?</span></span>

<span data-ttu-id="c90e5-106">от [Крис пикселей](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="c90e5-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="c90e5-107">В этом видеоролике Крис пикселей показано, как указать URL-адреса на сайте, использующем маршрутизацию ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c90e5-107">In this video Chris Pels shows how to specify URLs in a web site that utilizes ASP.NET routing.</span></span> <span data-ttu-id="c90e5-108">Сначала создается веб-сайт, а маршрутизация определяется в глобальном классе приложения (. asax).</span><span class="sxs-lookup"><span data-stu-id="c90e5-108">First, a web site is created and routing is defined in the Global Application Class (.asax).</span></span> <span data-ttu-id="c90e5-109">Затем создается пример веб-страницы и URL-адрес, основанный на определенном маршруте, добавляется на страницу с помощью стандартного метода "жестко кодированный", например "~/статс/виситорс".</span><span class="sxs-lookup"><span data-stu-id="c90e5-109">Next, a sample web page is created and a URL based upon a defined route is added to the page using the standard "hard coded" approach, e.g., "~/Stats/Visitors".</span></span> <span data-ttu-id="c90e5-110">Затем на страницу добавляется другая ссылка, которая динамически создает тот же URL-адрес в разметке с помощью метода RouteValue, который принимает имя маршрута и параметры.</span><span class="sxs-lookup"><span data-stu-id="c90e5-110">Another link is then added to the page which dynamically generates the same URL in markup using the RouteValue method which accepts the route name and parameters.</span></span> <span data-ttu-id="c90e5-111">Один и тот же URL-адрес затем реализуется с помощью кода, а не разметки непосредственно на странице.</span><span class="sxs-lookup"><span data-stu-id="c90e5-111">The same URL is then implemented using code rather than markup directly in the page.</span></span> <span data-ttu-id="c90e5-112">Исходный маршрут и расположение физической страницы затем изменяются, в результате чего жестко закодированная ссылка перестает работать, в то время как динамически формируемые ссылки работают правильно.</span><span class="sxs-lookup"><span data-stu-id="c90e5-112">The original route and physical page location are then changed, resulting in the hard coded link no longer working whereas both dynamically generated links function properly.</span></span> <span data-ttu-id="c90e5-113">Наконец, будет обсуждаться значение динамически создаваемых ссылок.</span><span class="sxs-lookup"><span data-stu-id="c90e5-113">Finally, the value of dynamically generated links is then discussed.</span></span>

[<span data-ttu-id="c90e5-114">&#9654;Смотреть видео (20 минут)</span><span class="sxs-lookup"><span data-stu-id="c90e5-114">&#9654; Watch video (20 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-work-with-urls-in-aspnet-routing)

> [!div class="step-by-step"]
> [<span data-ttu-id="c90e5-115">Назад</span><span class="sxs-lookup"><span data-stu-id="c90e5-115">Previous</span></span>](how-do-i-use-routing-with-aspnet-web-forms.md)
