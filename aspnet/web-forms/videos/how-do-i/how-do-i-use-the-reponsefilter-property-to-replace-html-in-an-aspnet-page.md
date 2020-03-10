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
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="98f4e-104">[Инструкции:] Использование свойства ответ. Filter для замены HTML на странице ASP.NET</span><span class="sxs-lookup"><span data-stu-id="98f4e-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>

<span data-ttu-id="98f4e-105">от [Крис пикселей](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="98f4e-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="98f4e-106">В этом видеоролике Крис пикселей показано, как использовать свойство ответ. Filter для перехвата и изменения HTML-кода, отправляемого на страницу.</span><span class="sxs-lookup"><span data-stu-id="98f4e-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="98f4e-107">Во-первых, образец страницы создается с простым текстом.</span><span class="sxs-lookup"><span data-stu-id="98f4e-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="98f4e-108">Затем создается пользовательский класс потока, который служит в качестве потока замены для текущего потока, отправляемого в браузер пользователя.</span><span class="sxs-lookup"><span data-stu-id="98f4e-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="98f4e-109">В этом классе пользовательского потока содержимое страницы извлекается из потока, изменяется, а затем записывается в поток ответа.</span><span class="sxs-lookup"><span data-stu-id="98f4e-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="98f4e-110">В этом классе пользовательского потока метод Write настраивается для замены HTML-кода в базовом потоке ответа, тем самым изменяя то, что отправляется в браузер пользователя.</span><span class="sxs-lookup"><span data-stu-id="98f4e-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="98f4e-111">Наконец, новый класс потока назначается свойству Response. Filter в событии Page\_Load, тем самым предоставляя механизм для изменения содержимого страницы.</span><span class="sxs-lookup"><span data-stu-id="98f4e-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="98f4e-112">&#9654;Смотреть видео (13 минут)</span><span class="sxs-lookup"><span data-stu-id="98f4e-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
