---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[Инструкции] Элемент управления, кэширование страницы ASP.NET на основе пользовательских сведений | Документация Майкрософт'
author: rick-anderson
description: В этом видео Крис Пелз показывает способ управления критерии для кэширования страницы ASP.NET на основе пользовательских сведений. Пример страницы создается и затем O...
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59381410"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a>[Инструкции] Элемент управления, кэширование страницы ASP.NET на основе пользовательских сведений

по [Крис Пелз](https://twitter.com/chrispels)

В этом видео Крис Пелз показывает способ управления критерии для кэширования страницы ASP.NET на основе пользовательских сведений. Пример страницы создается и используется директива OutputCache VaryByCustom атрибут, который содержит пользовательское значение. Затем метод GetVaryCustomByString() переопределяется в модуль global.asax, который обеспечивает обработку настраиваемого атрибута. В этом методе возвращается строка, однозначно идентифицирующий кэшированная версия страницы. Наконец здесь ведется дискуссия о том, как кэширования с помощью пользовательского значения можно использовать несколькими способами для веб-сайта.

[&#9654;Просмотрите видео (12 минут)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
