---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: Использование элемента управления "ползунок" с автоматическойC#обратной передачей () | Документация Майкрософт
author: wenz
description: Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно установить ползунок автозаписи...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445830"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="b315b-104">Использование элемента управления Slider с автоматической обратной передачей (C#)</span><span class="sxs-lookup"><span data-stu-id="b315b-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="b315b-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b315b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b315b-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b315b-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="b315b-107">Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши.</span><span class="sxs-lookup"><span data-stu-id="b315b-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="b315b-108">Можно сделать автообратную передачу ползунка после изменения ее значения.</span><span class="sxs-lookup"><span data-stu-id="b315b-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="b315b-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="b315b-109">Overview</span></span>

<span data-ttu-id="b315b-110">Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши.</span><span class="sxs-lookup"><span data-stu-id="b315b-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="b315b-111">Можно сделать автообратную передачу ползунка после изменения ее значения.</span><span class="sxs-lookup"><span data-stu-id="b315b-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="b315b-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="b315b-112">Steps</span></span>

<span data-ttu-id="b315b-113">Чтобы сделать ползунок автоматически обратным при изменении, в обоих текстовых полях требуется атрибут `AutoPostBack="true"`: текстовое поле, которое станет самим ползунком, и текстовое поле, содержащее положение ползунка.</span><span class="sxs-lookup"><span data-stu-id="b315b-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="b315b-114">Ниже приведена необходимая разметка для этого:</span><span class="sxs-lookup"><span data-stu-id="b315b-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="b315b-115">Элемент управления `SliderExtender` из набора средств ASP.NET AJAX Control Toolkit назначает функции ползунка для двух текстовых полей:</span><span class="sxs-lookup"><span data-stu-id="b315b-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="b315b-116">Позже будет использоваться дополнительный элемент Label для информирования пользователя о обратной передаче:</span><span class="sxs-lookup"><span data-stu-id="b315b-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="b315b-117">Наконец, `ScriptManager` элемент управления ASP.NET AJAX загружает необходимый код JavaScript для работы набора средств управления:</span><span class="sxs-lookup"><span data-stu-id="b315b-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="b315b-118">Теперь ползунок передается обратно. на стороне сервера это событие может быть перехвачено и обработано в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="b315b-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

<span data-ttu-id="b315b-119">[![перемещение ползунка инициирует обратную передачу](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b315b-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="b315b-120">Перемещение ползунка активирует обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b315b-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>

<span data-ttu-id="b315b-121">[![затем Дата этого изменения записывается в метку](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b315b-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="b315b-122">Затем Дата этого изменения записывается в метку ([щелкните, чтобы просмотреть изображение с полным размером](using-the-slider-control-with-auto-postback-cs/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="b315b-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b315b-123">Дальше</span><span class="sxs-lookup"><span data-stu-id="b315b-123">Next</span></span>](databinding-the-slider-control-cs.md)
