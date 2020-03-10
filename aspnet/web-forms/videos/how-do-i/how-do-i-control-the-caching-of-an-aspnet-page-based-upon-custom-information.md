---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[Инструкции:] Управление кэшированием страницы ASP.NET на основе пользовательской информации | Документация Майкрософт'
author: rick-anderson
description: В этом видеоролике Крис пикселей показано, как управлять критериями кэширования страницы ASP.NET на основе пользовательской информации. Создается пример страницы, а затем O...
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506772"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="89655-104">[Инструкции:] Управление кэшированием страницы ASP.NET на основе пользовательских данных</span><span class="sxs-lookup"><span data-stu-id="89655-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="89655-105">от [Крис пикселей](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="89655-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="89655-106">В этом видеоролике Крис пикселей показано, как управлять критериями кэширования страницы ASP.NET на основе пользовательской информации.</span><span class="sxs-lookup"><span data-stu-id="89655-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="89655-107">Создается пример страницы, а затем используется директива OutputCache с атрибутом VaryByCustom, который содержит пользовательское значение.</span><span class="sxs-lookup"><span data-stu-id="89655-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="89655-108">Затем метод Жетварикустомбистринг () переопределяется в модуле Global. asax, который обеспечивает обработку настраиваемого атрибута.</span><span class="sxs-lookup"><span data-stu-id="89655-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="89655-109">В этом методе возвращается строка, однозначно определяющая кэшированную версию страницы.</span><span class="sxs-lookup"><span data-stu-id="89655-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="89655-110">Наконец, существует обсуждение того, как кэширование с использованием пользовательского значения может использоваться несколькими способами для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="89655-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="89655-111">&#9654;Смотреть видео (12 минут)</span><span class="sxs-lookup"><span data-stu-id="89655-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
