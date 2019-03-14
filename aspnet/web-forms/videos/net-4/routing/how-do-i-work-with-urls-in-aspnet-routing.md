---
uid: web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
title: 'Инструкции: Работать с URL-адресами в маршрутизации ASP.NET? | Документы Майкрософт'
author: rick-anderson
description: В этом видео Крис Пелз показано, как указать URL-адреса для веб-сайта, использующего маршрутизации ASP.NET. Во-первых создается веб-сайта и маршрутизация определяется в ГК...
ms.author: riande
ms.date: 10/15/2010
ms.assetid: 08f9d0a7-cfa0-4914-a672-8a64295d7ba8
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
msc.type: video
ms.openlocfilehash: d9b0e086cceba5e2f7d372fb193eeeca891b5eb1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035091"
---
<a name="how-do-i-work-with-urls-in-aspnet-routing"></a>Инструкции: Работать с URL-адресами в маршрутизации ASP.NET?
====================
по [Крис Пелз](https://twitter.com/chrispels)

В этом видео Крис Пелз показано, как указать URL-адреса для веб-сайта, использующего маршрутизации ASP.NET. Во-первых создается веб-сайта и маршрутизация определяется в глобальный класс приложения (.asax). Затем создается пример веб-страницы и URL-адрес, на основе определенному маршруту добавляется на страницу, используя стандартный «жестко запрограммированный» подход, например, «~/Stats/Visitors». Затем другую ссылку добавляется на страницу, который динамически создает же URL-адрес в разметке, с помощью метода RouteValue, который принимает имя маршрута и параметры. Же URL-адрес затем реализуется с помощью кода, а не разметку непосредственно в страницу. Затем изменяются исходный маршрут и расположение физической страницы, в результате чего жестко запрограммированные ссылки больше не работает, тогда как оба динамически создаются работы ссылок должным образом. Наконец затем рассматривается значение динамически генерируемые ссылки обеспечивают доступ.

[&#9654;Просмотрите видео (20 минут)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-work-with-urls-in-aspnet-routing)

> [!div class="step-by-step"]
> [Назад](how-do-i-use-routing-with-aspnet-web-forms.md)
