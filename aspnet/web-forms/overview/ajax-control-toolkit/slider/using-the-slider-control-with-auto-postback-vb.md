---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: Использование элемента управления "ползунок" с автоматической обратной передачей (VB) | Документация Майкрософт
author: wenz
description: Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно установить ползунок автозаписи...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598563"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="132a5-104">Использование элемента управления "ползунок" с автоматической обратной передачей (VB)</span><span class="sxs-lookup"><span data-stu-id="132a5-104">Using the Slider Control With Auto-Postback (VB)</span></span>

<span data-ttu-id="132a5-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="132a5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="132a5-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="132a5-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="132a5-107">Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши.</span><span class="sxs-lookup"><span data-stu-id="132a5-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="132a5-108">Можно сделать автообратную передачу ползунка после изменения ее значения.</span><span class="sxs-lookup"><span data-stu-id="132a5-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="132a5-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="132a5-109">Overview</span></span>

<span data-ttu-id="132a5-110">Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши.</span><span class="sxs-lookup"><span data-stu-id="132a5-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="132a5-111">Можно сделать автообратную передачу ползунка после изменения ее значения.</span><span class="sxs-lookup"><span data-stu-id="132a5-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="132a5-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="132a5-112">Steps</span></span>

<span data-ttu-id="132a5-113">Чтобы сделать ползунок автоматически обратным при изменении, в обоих текстовых полях требуется атрибут `AutoPostBack="true"`: текстовое поле, которое станет самим ползунком, и текстовое поле, содержащее положение ползунка.</span><span class="sxs-lookup"><span data-stu-id="132a5-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="132a5-114">Ниже приведена необходимая разметка для этого:</span><span class="sxs-lookup"><span data-stu-id="132a5-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="132a5-115">Элемент управления `SliderExtender` из набора средств ASP.NET AJAX Control Toolkit назначает функции ползунка для двух текстовых полей:</span><span class="sxs-lookup"><span data-stu-id="132a5-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="132a5-116">Позже будет использоваться дополнительный элемент Label для информирования пользователя о обратной передаче:</span><span class="sxs-lookup"><span data-stu-id="132a5-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="132a5-117">Наконец, `ScriptManager` элемент управления ASP.NET AJAX загружает необходимый код JavaScript для работы набора средств управления:</span><span class="sxs-lookup"><span data-stu-id="132a5-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="132a5-118">Теперь ползунок передается обратно. на стороне сервера это событие может быть перехвачено и обработано в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="132a5-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

<span data-ttu-id="132a5-119">[![перемещение ползунка инициирует обратную передачу](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="132a5-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="132a5-120">Перемещение ползунка активирует обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="132a5-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>

<span data-ttu-id="132a5-121">[![затем Дата этого изменения записывается в метку](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="132a5-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="132a5-122">Затем Дата этого изменения записывается в метку ([щелкните, чтобы просмотреть изображение с полным размером](using-the-slider-control-with-auto-postback-vb/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="132a5-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="132a5-123">[Назад](databinding-the-slider-control-cs.md)
> [Вперед](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="132a5-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
