---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: Настройка Z-индекса DropShadow (VB) | Документация Майкрософт
author: wenz
description: Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Однако эта тень иногда конфликтует с другими элементами управления, для программа...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: 10495a9590ce1f25e9e3fa218ac5144268f50711
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574183"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-vb"></a><span data-ttu-id="087e6-104">Настройка Z-индекса DropShadow (VB)</span><span class="sxs-lookup"><span data-stu-id="087e6-104">Adjusting the Z-Index of a DropShadow (VB)</span></span>

<span data-ttu-id="087e6-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="087e6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="087e6-106">[Скачать код](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="087e6-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span></span>

> <span data-ttu-id="087e6-107">Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью.</span><span class="sxs-lookup"><span data-stu-id="087e6-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="087e6-108">Однако эта тень иногда конфликтует с другими элементами управления, например с элементом управления меню ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="087e6-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="087e6-109">Когда появляется запись меню, она отображается позади тени.</span><span class="sxs-lookup"><span data-stu-id="087e6-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="overview"></a><span data-ttu-id="087e6-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="087e6-110">Overview</span></span>

<span data-ttu-id="087e6-111">Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью.</span><span class="sxs-lookup"><span data-stu-id="087e6-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="087e6-112">Однако эта тень иногда конфликтует с другими элементами управления, например с элементом управления меню ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="087e6-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="087e6-113">Когда появляется запись меню, она отображается позади тени.</span><span class="sxs-lookup"><span data-stu-id="087e6-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="087e6-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="087e6-114">Steps</span></span>

<span data-ttu-id="087e6-115">Код начнется с самой панели, содержащей достаточно текста, чтобы панель содержит достаточно текста для отображения результата:</span><span class="sxs-lookup"><span data-stu-id="087e6-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

<span data-ttu-id="087e6-116">Другая панель размещается непосредственно перед панелью `panelShadow`.</span><span class="sxs-lookup"><span data-stu-id="087e6-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="087e6-117">Он содержит меню с горизонтальной ориентацией, чтобы на панели `dropShadow` появлялись записи меню (или просто: в):</span><span class="sxs-lookup"><span data-stu-id="087e6-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

<span data-ttu-id="087e6-118">Затем добавляется `DropShadowExtender` для расширения панели `panelShadow` с эффектом тени:</span><span class="sxs-lookup"><span data-stu-id="087e6-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

<span data-ttu-id="087e6-119">Наконец, элемент управления `ScriptManager` AJAX ASP.NET позволяет набору элементов управления работать:</span><span class="sxs-lookup"><span data-stu-id="087e6-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

<span data-ttu-id="087e6-120">При запуске этого скрипта пункты меню отображаются под панелью.</span><span class="sxs-lookup"><span data-stu-id="087e6-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="087e6-121">Однако в меню используется класс CSS `panel`, где необходимо определить две вещи, чтобы элементы отображались перед другой панелью:</span><span class="sxs-lookup"><span data-stu-id="087e6-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="087e6-122">Относительное положение</span><span class="sxs-lookup"><span data-stu-id="087e6-122">Relative positioning</span></span>
- <span data-ttu-id="087e6-123">Положительный z-индекс</span><span class="sxs-lookup"><span data-stu-id="087e6-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

<span data-ttu-id="087e6-124">Затем элемент управления "`DropShadowExtender`" больше не конфликтует с элементом управления Menu.</span><span class="sxs-lookup"><span data-stu-id="087e6-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>

<span data-ttu-id="087e6-125">[![до: запись меню не отображается](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="087e6-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span></span>

<span data-ttu-id="087e6-126">До: запись меню не отображается ([щелкните, чтобы просмотреть изображение с полным размером](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="087e6-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span></span>

<span data-ttu-id="087e6-127">[![после: появится запись меню](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="087e6-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span></span>

<span data-ttu-id="087e6-128">После: появится запись меню ([щелкните, чтобы просмотреть изображение с полным размером](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="087e6-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="087e6-129">[Назад](manipulating-dropshadow-properties-from-client-code-cs.md)
> [Вперед](manipulating-dropshadow-properties-from-client-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="087e6-129">[Previous](manipulating-dropshadow-properties-from-client-code-cs.md)
[Next](manipulating-dropshadow-properties-from-client-code-vb.md)</span></span>
