---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: Анимация в зависимости от условия (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Является ли анимация...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 583ebdbf109beb74b9a425020477183067bbb79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607018"
---
# <a name="animation-depending-on-a-condition-vb"></a><span data-ttu-id="089b8-104">Анимация в зависимости от условия (VB)</span><span class="sxs-lookup"><span data-stu-id="089b8-104">Animation Depending On a Condition (VB)</span></span>

<span data-ttu-id="089b8-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="089b8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="089b8-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="089b8-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span></span>

> <span data-ttu-id="089b8-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="089b8-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="089b8-108">Выполняется ли анимация, а также может зависеть от условия в виде кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="089b8-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="089b8-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="089b8-109">Overview</span></span>

<span data-ttu-id="089b8-110">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="089b8-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="089b8-111">Выполняется ли анимация, а также может зависеть от условия в виде кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="089b8-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="089b8-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="089b8-112">Steps</span></span>

<span data-ttu-id="089b8-113">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="089b8-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

<span data-ttu-id="089b8-114">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="089b8-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

<span data-ttu-id="089b8-115">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="089b8-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

<span data-ttu-id="089b8-116">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и обязательную `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="089b8-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

<span data-ttu-id="089b8-117">В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="089b8-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="089b8-118">Вместо одной из обычных анимаций элемент `<Condition>` поступает в игру.</span><span class="sxs-lookup"><span data-stu-id="089b8-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="089b8-119">Код JavaScript, предоставленный в качестве значения атрибута `ConditionScript`, выполняется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="089b8-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="089b8-120">Если значение равно true, анимация выполняется, в противном случае — нет.</span><span class="sxs-lookup"><span data-stu-id="089b8-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="089b8-121">Следующая разметка предоставляет две анимации, каждая из которых выполняется в 50% случаев при случайном.</span><span class="sxs-lookup"><span data-stu-id="089b8-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="089b8-122">Так как в `<OnLoad>`может быть только одна анимация, две `<Condition>` анимации объединяются с помощью элемента `<Sequence>`:</span><span class="sxs-lookup"><span data-stu-id="089b8-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

<span data-ttu-id="089b8-123">Обратите внимание, что знак "меньше" (`<`) в атрибуте `ConditionScript` должен быть экранированным ().</span><span class="sxs-lookup"><span data-stu-id="089b8-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="089b8-124">При запуске этого скрипта не выполняется ни анимация, ни одно из двух операций.</span><span class="sxs-lookup"><span data-stu-id="089b8-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>

<span data-ttu-id="089b8-125">[![панель вытекает без изменения размера, поэтому выполняется вторая анимация, первая — не](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="089b8-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span></span>

<span data-ttu-id="089b8-126">Панель вытекает без изменения размера, поэтому вторая анимация выполняется, а первая — нет ([щелкните, чтобы просмотреть изображение с полным размером](animation-depending-on-a-condition-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="089b8-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="089b8-127">[Назад](executing-several-animations-after-each-other-vb.md)
> [Вперед](picking-one-animation-out-of-a-list-vb.md)</span><span class="sxs-lookup"><span data-stu-id="089b8-127">[Previous](executing-several-animations-after-each-other-vb.md)
[Next](picking-one-animation-out-of-a-list-vb.md)</span></span>
