---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[Инструкции] Использование свойства Reponse.Filter для замены HTML на странице ASP.NET | Документация Майкрософт'
author: rick-anderson
description: В этом видео Крис Пелз показано использование свойства Reponse.Filter для перехвата и изменения HTML, отправляемого на страницу. Во-первых пример страницы создается w...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59403432"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="6d4da-104">[Инструкции] Использование свойства Reponse.Filter для замены HTML на странице ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6d4da-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>

<span data-ttu-id="6d4da-105">по [Крис Пелз](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="6d4da-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="6d4da-106">В этом видео Крис Пелз показано использование свойства Reponse.Filter для перехвата и изменения HTML, отправляемого на страницу.</span><span class="sxs-lookup"><span data-stu-id="6d4da-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="6d4da-107">Во-первых пример страницы создается простой текст.</span><span class="sxs-lookup"><span data-stu-id="6d4da-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="6d4da-108">Затем создается пользовательский класс Stream, служащий поток замены для текущего потока, отправляемого в браузер пользователя.</span><span class="sxs-lookup"><span data-stu-id="6d4da-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="6d4da-109">В этом классе пользовательского потока содержимого страницы извлекаются из потока, изменении и записать в поток ответа.</span><span class="sxs-lookup"><span data-stu-id="6d4da-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="6d4da-110">В этот пользовательский класс Stream метод Write настроено таким образом, чтобы заменить код HTML в базовый поток ответа, тем самым изменяя отправки в браузер пользователя.</span><span class="sxs-lookup"><span data-stu-id="6d4da-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="6d4da-111">Наконец, новый класс потока назначается свойство Response.Filter на странице\_событию загрузки, тем самым предоставляя механизм для изменения содержимого страницы.</span><span class="sxs-lookup"><span data-stu-id="6d4da-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="6d4da-112">&#9654;Просмотрите видео (13 минут)</span><span class="sxs-lookup"><span data-stu-id="6d4da-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
