---
uid: web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
title: '[Инструкции:] Выберите способ обновления страницы AJAX? | Документы Майкрософт'
author: JoeStagner
description: В этом видеоролике Joe Stagner) сравнивает два основных метода выполнения обновлений страниц в стиле AJAX в приложении ASP.NET. Первый способ — использовать UPD...
ms.author: riande
ms.date: 07/09/2007
ms.assetid: a5e33a7d-ccb2-483f-a955-3d39f72ba4ec
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
msc.type: video
ms.openlocfilehash: 56e3ebfbe0b5af4234791136725de79e38171cc1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78420156"
---
# <a name="how-do-i-choose-between-methods-of-ajax-page-updates"></a><span data-ttu-id="d6f5d-105">[Инструкции:] Выберите способ обновления страницы AJAX?</span><span class="sxs-lookup"><span data-stu-id="d6f5d-105">[How Do I:] Choose Between Methods of AJAX Page Updates?</span></span>

<span data-ttu-id="d6f5d-106">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="d6f5d-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="d6f5d-107">В этом видеоролике Joe Stagner) сравнивает два основных метода выполнения обновлений страниц в стиле AJAX в приложении ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d6f5d-107">In this video Joe Stagner compares the two primary methods of performing AJAX-style page updates in an ASP.NET application.</span></span> <span data-ttu-id="d6f5d-108">Первым методом является использование UpdatePanel, где не требуется записывать дополнительный код на стороне клиента или на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d6f5d-108">The first method is to use an UpdatePanel, where no additional code needs to be written on either the client side or the server side.</span></span> <span data-ttu-id="d6f5d-109">Преимуществом использования UpdatePanel является то, что все работает автоматически.</span><span class="sxs-lookup"><span data-stu-id="d6f5d-109">The benefit of using the UpdatePanel is that everything works automatically.</span></span> <span data-ttu-id="d6f5d-110">Снижение этого заключается в том, что на клиенте требуется большой объем данных, включаемых в запрос AJAX и ответ, и на сервере требуется выполнение полного жизненного цикла страницы.</span><span class="sxs-lookup"><span data-stu-id="d6f5d-110">The penalty is that at the client it requires a lot of data to be included in the AJAX request and response, and at the server it requires a full page lifecycle to be executed.</span></span> <span data-ttu-id="d6f5d-111">Второй способ — использовать обратные вызовы по сети, где дополнительный код должен быть написан как на стороне клиента, так и на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d6f5d-111">The second method is to use network callbacks, where additional code needs to be written on both the client side and the server side.</span></span> <span data-ttu-id="d6f5d-112">Преимущество использования обратных вызовов в сети заключается в том, что на клиенте требуется очень мало данных для включения в запрос AJAX и ответ, а на сервере требуется только вызываемый метод службы.</span><span class="sxs-lookup"><span data-stu-id="d6f5d-112">The benefit of using network callbacks is that at the client it requires very little data to be included in the AJAX request and response, and at the server it requires only the called service method to be executed.</span></span> <span data-ttu-id="d6f5d-113">Штраф — это время и усилия, затрачиваемые на написание необходимого кода.</span><span class="sxs-lookup"><span data-stu-id="d6f5d-113">The penality is the time and effort it takes to write the necessary code.</span></span> <span data-ttu-id="d6f5d-114">Сергей завершает видео, обсуждая, что следует учитывать при выборе между двумя основными методами обновления страницы в стиле AJAX.</span><span class="sxs-lookup"><span data-stu-id="d6f5d-114">Joe concludes the video by discussing what you should consider when choosing between the two primary methods of AJAX-style page updates.</span></span> <span data-ttu-id="d6f5d-115">(В этом видеоролике используется код из [руководства как начать работу с видео ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) и [как выполнить обратный вызов сети на стороне клиента с помощью видео ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) .)</span><span class="sxs-lookup"><span data-stu-id="d6f5d-115">(This video uses the code from the [How Do I Get Started with ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) video and the [How Do I Make Client-Side Network Callbacks with ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) video.)</span></span>

[<span data-ttu-id="d6f5d-116">&#9654;Смотреть видео (11 минут)</span><span class="sxs-lookup"><span data-stu-id="d6f5d-116">&#9654; Watch video (11 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-choose-between-methods-of-ajax-page-updates)

> [!div class="step-by-step"]
> <span data-ttu-id="d6f5d-117">[Назад](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
> [Вперед](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span><span class="sxs-lookup"><span data-stu-id="d6f5d-117">[Previous](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
[Next](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span></span>
