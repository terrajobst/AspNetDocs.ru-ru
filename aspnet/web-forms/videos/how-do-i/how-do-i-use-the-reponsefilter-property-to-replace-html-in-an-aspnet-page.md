---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[Инструкции:] Использование свойства ответа. Filter для замены HTML на странице ASP.NET | Документация Майкрософт'
author: rick-anderson
description: В этом видеоролике Крис пикселей показано, как использовать свойство ответ. Filter для перехвата и изменения HTML-кода, отправляемого на страницу. Во-первых, создается образец страницы w...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487998"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[Инструкции:] Использование свойства ответ. Filter для замены HTML на странице ASP.NET

от [Крис пикселей](https://twitter.com/chrispels)

В этом видеоролике Крис пикселей показано, как использовать свойство ответ. Filter для перехвата и изменения HTML-кода, отправляемого на страницу. Во-первых, образец страницы создается с простым текстом. Затем создается пользовательский класс потока, который служит в качестве потока замены для текущего потока, отправляемого в браузер пользователя. В этом классе пользовательского потока содержимое страницы извлекается из потока, изменяется, а затем записывается в поток ответа. В этом классе пользовательского потока метод Write настраивается для замены HTML-кода в базовом потоке ответа, тем самым изменяя то, что отправляется в браузер пользователя. Наконец, новый класс потока назначается свойству Response. Filter в событии Page\_Load, тем самым предоставляя механизм для изменения содержимого страницы.

[&#9654;Смотреть видео (13 минут)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
