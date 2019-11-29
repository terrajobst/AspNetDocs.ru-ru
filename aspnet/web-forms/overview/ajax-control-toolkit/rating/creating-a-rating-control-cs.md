---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: Создание элемента управления рейтингомC#() | Документация Майкрософт
author: wenz
description: Многие веб-сайты, от электронной коммерции до сайтов сообщества, предлагают пользователям оценивать статьи или элементы. Обычно это требует некоторых усилий при написании кода, но у нас есть...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611588"
---
# <a name="creating-a-rating-control-c"></a><span data-ttu-id="06904-104">Создание элемента управления Rating (C#)</span><span class="sxs-lookup"><span data-stu-id="06904-104">Creating a Rating Control (C#)</span></span>

<span data-ttu-id="06904-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="06904-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="06904-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="06904-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="06904-107">Многие веб-сайты, от электронной коммерции до сайтов сообщества, предлагают пользователям оценивать статьи или элементы.</span><span class="sxs-lookup"><span data-stu-id="06904-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="06904-108">Для этого обычно требуются некоторые усилия по написанию кода, но у нас есть набор элементов управления для нашей реализации.</span><span class="sxs-lookup"><span data-stu-id="06904-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="overview"></a><span data-ttu-id="06904-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="06904-109">Overview</span></span>

<span data-ttu-id="06904-110">Многие веб-сайты, от электронной коммерции до сайтов сообщества, предлагают пользователям оценивать статьи или элементы.</span><span class="sxs-lookup"><span data-stu-id="06904-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="06904-111">Для этого обычно требуются некоторые усилия по написанию кода, но у нас есть набор элементов управления для нашей реализации.</span><span class="sxs-lookup"><span data-stu-id="06904-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="06904-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="06904-112">Steps</span></span>

<span data-ttu-id="06904-113">Во-первых, требуется (по крайней мере) два типа изображений: одно для заполненного элемента рейтинга, а другое — для пустого элемента рейтинга.</span><span class="sxs-lookup"><span data-stu-id="06904-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="06904-114">Элемент рейтинга обычно является звездочкой или смайликом.</span><span class="sxs-lookup"><span data-stu-id="06904-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="06904-115">В этом сценарии вы найдете три файла, смайлик. png и Empty. png и смилэй-Доне. png как часть загружаемого исходного кода для этого руководства.</span><span class="sxs-lookup"><span data-stu-id="06904-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="06904-116">Затем создайте новый файл ASP.NET и начните с добавления к нему элемента управления `ScriptManager`:</span><span class="sxs-lookup"><span data-stu-id="06904-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="06904-117">Затем добавьте элемент управления `Rating` из набора средств управления AJAX ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="06904-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="06904-118">Для этого примера необходимо задать следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="06904-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="06904-119">`CurrentRating` используемую начальную оценку</span><span class="sxs-lookup"><span data-stu-id="06904-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="06904-120">`MaxRating` максимальную оценку</span><span class="sxs-lookup"><span data-stu-id="06904-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="06904-121">`EmptyStarCssClass` класс CSS для использования при пустом элементе рейтинга (звездочка)</span><span class="sxs-lookup"><span data-stu-id="06904-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="06904-122">`FilledStarCssClass` класс CSS, используемый при заполнении элемента рейтинга (Star)</span><span class="sxs-lookup"><span data-stu-id="06904-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="06904-123">`StarCssClass` класс CSS, используемый для видимой статистики</span><span class="sxs-lookup"><span data-stu-id="06904-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="06904-124">`WaitingStarCssClass` класс CSS для использования при отправке на сервер оценки типа "звезда"</span><span class="sxs-lookup"><span data-stu-id="06904-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="06904-125">Ниже приведена разметка, которая создает элемент управления рейтингом с пятью элементами (смайликами), которые изначально не заполнены:</span><span class="sxs-lookup"><span data-stu-id="06904-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="06904-126">Теперь для трех ссылочных классов CSS необходимо отобразить соответствующие файлы изображений, что легко сделать с помощью CSS:</span><span class="sxs-lookup"><span data-stu-id="06904-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="06904-127">Убедитесь, что заданы ширина и высота трех изображений, иначе отображение может показаться немного запутанным.</span><span class="sxs-lookup"><span data-stu-id="06904-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="06904-128">Наконец, результат оценки должен отображаться для пользователя (или, по крайней мере, сохраненного в базе данных).</span><span class="sxs-lookup"><span data-stu-id="06904-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="06904-129">Поэтому добавьте метку для вывода текстового сообщения и кнопку Отправить, чтобы отправить форму оценки на сервер:</span><span class="sxs-lookup"><span data-stu-id="06904-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="06904-130">В коде на стороне сервера получите доступ к элементу управления рейтингом с помощью его `ID` а затем получите доступ к его свойству `CurrentRating`, которое является числом выбранных элементов рейтинга, в нашем примере — значение от 0 до 5.</span><span class="sxs-lookup"><span data-stu-id="06904-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="06904-131">Сохраните страницу и загрузите ее в браузере.</span><span class="sxs-lookup"><span data-stu-id="06904-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="06904-132">При наведении указателя мыши на элементы рейтинга (изначально пустые) возникает воздействие на JavaScript: изменение оценки.</span><span class="sxs-lookup"><span data-stu-id="06904-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="06904-133">Если щелкнуть набор звезд, текущая оценка сохраняется.</span><span class="sxs-lookup"><span data-stu-id="06904-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="06904-134">Наконец, при отправке формы код на стороне сервера выводит выбранную оценку.</span><span class="sxs-lookup"><span data-stu-id="06904-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>

<span data-ttu-id="06904-135">[![создания системы оценок с минимальным кодом](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="06904-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="06904-136">Создание системы оценок с минимальным кодом ([щелкните, чтобы просмотреть изображение с полным размером](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="06904-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="06904-137">Вперед</span><span class="sxs-lookup"><span data-stu-id="06904-137">Next</span></span>](creating-a-rating-control-vb.md)
