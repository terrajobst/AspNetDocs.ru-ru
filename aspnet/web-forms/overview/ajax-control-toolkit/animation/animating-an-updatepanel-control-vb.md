---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: Анимация элемента управления UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d66dda923940a328c0757049c9d8bfa3b2d2b9fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431016"
---
# <a name="animating-an-updatepanel-control-vb"></a><span data-ttu-id="fb899-104">Анимация элемента управления UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="fb899-104">Animating an UpdatePanel Control (VB)</span></span>

<span data-ttu-id="fb899-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fb899-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fb899-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fb899-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span></span>

> <span data-ttu-id="fb899-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="fb899-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fb899-108">Для содержимого UpdatePanel существует специальный расширитель, который сильно зависит от платформы анимации: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="fb899-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="fb899-109">В этом руководстве показано, как настроить подобную анимацию для UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="fb899-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="fb899-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="fb899-110">Overview</span></span>

<span data-ttu-id="fb899-111">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="fb899-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fb899-112">Для содержимого `UpdatePanel`существует специальный расширитель, который сильно зависит от платформы анимации: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="fb899-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="fb899-113">В этом руководстве показано, как настроить такую анимацию для `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="fb899-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="fb899-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="fb899-114">Steps</span></span>

<span data-ttu-id="fb899-115">Первым шагом является включение `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и использовать набор элементов управления.</span><span class="sxs-lookup"><span data-stu-id="fb899-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

<span data-ttu-id="fb899-116">Анимация в этом сценарии будет применена к веб-элементу управления ASP.NET `Wizard`, размещенному в `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="fb899-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="fb899-117">Три (случайные) шага предоставляют достаточно параметров для активации обратных передач:</span><span class="sxs-lookup"><span data-stu-id="fb899-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

<span data-ttu-id="fb899-118">Разметка, необходимая для элемента управления `UpdatePanelAnimationExtender`, очень похожа на разметку, используемую для `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="fb899-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="fb899-119">В атрибуте `TargetControlID` мы предоставляем `ID` `UpdatePanel` для анимации. в элементе управления `UpdatePanelAnimationExtender` элемент `<Animations>` содержит XML-разметку для анимаций.</span><span class="sxs-lookup"><span data-stu-id="fb899-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="fb899-120">Однако существует одно отличие: количество событий и обработчиков событий ограничено в сравнении с `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="fb899-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="fb899-121">Для `UpdatePanels`существует только два из них:</span><span class="sxs-lookup"><span data-stu-id="fb899-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="fb899-122">`<OnUpdated>` при обновлении UpdatePanel</span><span class="sxs-lookup"><span data-stu-id="fb899-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="fb899-123">`<OnUpdating>` при начале обновления UpdatePanel</span><span class="sxs-lookup"><span data-stu-id="fb899-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="fb899-124">В этом сценарии новое содержимое `UpdatePanel` (после обратной передачи) будет постепенно передаваться.</span><span class="sxs-lookup"><span data-stu-id="fb899-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="fb899-125">Это необходимая разметка для этого:</span><span class="sxs-lookup"><span data-stu-id="fb899-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

<span data-ttu-id="fb899-126">Теперь, когда обратная передача происходит в UpdatePanel, новое содержимое панели плавно перестало отображаться.</span><span class="sxs-lookup"><span data-stu-id="fb899-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="fb899-127">[![следующем шаге мастера происходит снижение яркости](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fb899-127">[![The next wizard step is fading in](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="fb899-128">Следующий шаг мастера поменяется ([щелкните, чтобы просмотреть изображение с полным размером](animating-an-updatepanel-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fb899-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fb899-129">[Назад](changing-an-animation-using-client-side-code-vb.md)
> [Вперед](dynamically-controlling-updatepanel-animations-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fb899-129">[Previous](changing-an-animation-using-client-side-code-vb.md)
[Next](dynamically-controlling-updatepanel-animations-vb.md)</span></span>
