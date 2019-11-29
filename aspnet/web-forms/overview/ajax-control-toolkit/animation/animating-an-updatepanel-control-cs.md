---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: Анимация элемента управления UpdatePanel (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599907"
---
# <a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="d6957-104">Анимация элемента управления UpdatePanel (C#)</span><span class="sxs-lookup"><span data-stu-id="d6957-104">Animating an UpdatePanel Control (C#)</span></span>

<span data-ttu-id="d6957-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d6957-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d6957-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="d6957-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="d6957-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="d6957-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d6957-108">Для содержимого UpdatePanel существует специальный расширитель, который сильно зависит от платформы анимации: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="d6957-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="d6957-109">В этом руководстве показано, как настроить подобную анимацию для UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="d6957-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="d6957-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="d6957-110">Overview</span></span>

<span data-ttu-id="d6957-111">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="d6957-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d6957-112">Для содержимого `UpdatePanel`существует специальный расширитель, который сильно зависит от платформы анимации: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="d6957-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="d6957-113">В этом руководстве показано, как настроить такую анимацию для `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="d6957-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="d6957-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="d6957-114">Steps</span></span>

<span data-ttu-id="d6957-115">Первым шагом является включение `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и использовать набор элементов управления.</span><span class="sxs-lookup"><span data-stu-id="d6957-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="d6957-116">Анимация в этом сценарии будет применена к веб-элементу управления ASP.NET `Wizard`, размещенному в `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="d6957-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="d6957-117">Три (случайные) шага предоставляют достаточно параметров для активации обратных передач:</span><span class="sxs-lookup"><span data-stu-id="d6957-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="d6957-118">Разметка, необходимая для элемента управления `UpdatePanelAnimationExtender`, очень похожа на разметку, используемую для `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="d6957-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="d6957-119">В атрибуте `TargetControlID` мы предоставляем `ID` `UpdatePanel` для анимации. в элементе управления `UpdatePanelAnimationExtender` элемент `<Animations>` содержит XML-разметку для анимаций.</span><span class="sxs-lookup"><span data-stu-id="d6957-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="d6957-120">Однако существует одно отличие: количество событий и обработчиков событий ограничено в сравнении с `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="d6957-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="d6957-121">Для `UpdatePanels`существует только два из них:</span><span class="sxs-lookup"><span data-stu-id="d6957-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="d6957-122">`<OnUpdated>` при обновлении UpdatePanel</span><span class="sxs-lookup"><span data-stu-id="d6957-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="d6957-123">`<OnUpdating>` при начале обновления UpdatePanel</span><span class="sxs-lookup"><span data-stu-id="d6957-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="d6957-124">В этом сценарии новое содержимое `UpdatePanel` (после обратной передачи) будет постепенно передаваться.</span><span class="sxs-lookup"><span data-stu-id="d6957-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="d6957-125">Это необходимая разметка для этого:</span><span class="sxs-lookup"><span data-stu-id="d6957-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="d6957-126">Теперь, когда обратная передача происходит в UpdatePanel, новое содержимое панели плавно перестало отображаться.</span><span class="sxs-lookup"><span data-stu-id="d6957-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="d6957-127">[![следующем шаге мастера происходит снижение яркости](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d6957-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="d6957-128">Следующий шаг мастера поменяется ([щелкните, чтобы просмотреть изображение с полным размером](animating-an-updatepanel-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d6957-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d6957-129">[Назад](changing-an-animation-using-client-side-code-cs.md)
> [Вперед](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="d6957-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
