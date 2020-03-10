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
# <a name="how-do-i-work-with-urls-in-aspnet-routing"></a>Инструкции. Работа с URL-адресами в маршрутизации ASP.NET

от [Крис пикселей](https://twitter.com/chrispels)

В этом видеоролике Крис пикселей показано, как указать URL-адреса на сайте, использующем маршрутизацию ASP.NET. Сначала создается веб-сайт, а маршрутизация определяется в глобальном классе приложения (. asax). Затем создается пример веб-страницы и URL-адрес, основанный на определенном маршруте, добавляется на страницу с помощью стандартного метода "жестко кодированный", например "~/статс/виситорс". Затем на страницу добавляется другая ссылка, которая динамически создает тот же URL-адрес в разметке с помощью метода RouteValue, который принимает имя маршрута и параметры. Один и тот же URL-адрес затем реализуется с помощью кода, а не разметки непосредственно на странице. Исходный маршрут и расположение физической страницы затем изменяются, в результате чего жестко закодированная ссылка перестает работать, в то время как динамически формируемые ссылки работают правильно. Наконец, будет обсуждаться значение динамически создаваемых ссылок.

[&#9654;Смотреть видео (20 минут)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-work-with-urls-in-aspnet-routing)

> [!div class="step-by-step"]
> [Назад](how-do-i-use-routing-with-aspnet-web-forms.md)
