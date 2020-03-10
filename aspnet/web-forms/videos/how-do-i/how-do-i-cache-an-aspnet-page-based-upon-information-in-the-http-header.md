---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[Инструкции:]  Кэширование страницы ASP.NET на основе сведений в заголовке HTTP | Документация Майкрософт'
author: rick-anderson
description: В этом видеоролике Крис пикселей показано, как разместить страницу в кэше вывода ASP.NET на основе информации в HTTP-заголовке страницы. Во-первых, потенциальный HTTP верхни...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506976"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="c0f17-104">[Инструкции:]  Кэширование страницы ASP.NET на основе сведений в заголовке HTTP</span><span class="sxs-lookup"><span data-stu-id="c0f17-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>

<span data-ttu-id="c0f17-105">от [Крис пикселей](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="c0f17-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="c0f17-106">В этом видеоролике Крис пикселей показано, как разместить страницу в кэше вывода ASP.NET на основе информации в HTTP-заголовке страницы.</span><span class="sxs-lookup"><span data-stu-id="c0f17-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="c0f17-107">Во-первых, просматриваются потенциальные значения заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="c0f17-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="c0f17-108">Затем создается пример страницы, а затем используется директива OutputCache с атрибутом Варибихеадер, который содержит значение Accept-Language, HTTP-заголовок для управления кэшированием на основе языка браузера пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0f17-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="c0f17-109">Образец страницы отображается в IE, для которого задано значение Английский, а затем в браузере FireFox, для которого настроено использование французского языка.</span><span class="sxs-lookup"><span data-stu-id="c0f17-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="c0f17-110">Наконец, рассматривается возможность перемещения определения кэша в Качепрофиле в файле Web. config.</span><span class="sxs-lookup"><span data-stu-id="c0f17-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="c0f17-111">&#9654;Смотреть видео (12 минут)</span><span class="sxs-lookup"><span data-stu-id="c0f17-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
