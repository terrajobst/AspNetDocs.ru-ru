---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: Добавление анимации в элемент управления (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. В этом руководстве показано, как...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607173"
---
# <a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="d8477-104">Добавление анимации в элемент управления (VB)</span><span class="sxs-lookup"><span data-stu-id="d8477-104">Adding Animation to a Control (VB)</span></span>

<span data-ttu-id="d8477-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d8477-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d8477-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d8477-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="d8477-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="d8477-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d8477-108">В этом руководстве показано, как настроить подобную анимацию.</span><span class="sxs-lookup"><span data-stu-id="d8477-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="d8477-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="d8477-109">Overview</span></span>

<span data-ttu-id="d8477-110">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="d8477-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d8477-111">В этом руководстве показано, как настроить подобную анимацию.</span><span class="sxs-lookup"><span data-stu-id="d8477-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="d8477-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="d8477-112">Steps</span></span>

<span data-ttu-id="d8477-113">Первым шагом является включение `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и использовать набор элементов управления.</span><span class="sxs-lookup"><span data-stu-id="d8477-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="d8477-114">Анимация в этом сценарии будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d8477-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="d8477-115">Связанный класс CSS для панели определяет цвет фона и ширину:</span><span class="sxs-lookup"><span data-stu-id="d8477-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="d8477-116">Далее требуется `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="d8477-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="d8477-117">После предоставления `ID` и обычного `runat="server"`атрибут `TargetControlID` должен быть установлен на элемент управления для анимации в нашем случае, панель:</span><span class="sxs-lookup"><span data-stu-id="d8477-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="d8477-118">Вся анимация применяется декларативно с использованием синтаксиса XML, к сожалению, в настоящее время не полностью поддерживается IntelliSense в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8477-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="d8477-119">Корневой узел `<Animations>;` в пределах этого узла; разрешено несколько событий, которые определяют, когда происходит анимация (-ов):</span><span class="sxs-lookup"><span data-stu-id="d8477-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="d8477-120">`OnClick` (щелчок мышью)</span><span class="sxs-lookup"><span data-stu-id="d8477-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="d8477-121">`OnHoverOut` (когда мышь покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="d8477-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="d8477-122">`OnHoverOver` (при наведении указателя мыши на элемент управления, остановка `OnHoverOut`ной анимации)</span><span class="sxs-lookup"><span data-stu-id="d8477-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="d8477-123">`OnLoad` (при загрузке страницы)</span><span class="sxs-lookup"><span data-stu-id="d8477-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="d8477-124">`OnMouseOut` (когда мышь покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="d8477-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="d8477-125">`OnMouseOver` (при наведении указателя мыши на элемент управления, не останавливая `OnMouseOut` анимацию)</span><span class="sxs-lookup"><span data-stu-id="d8477-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="d8477-126">Платформа поставляется с набором анимаций, каждый из которых представлен собственным XML-элементом.</span><span class="sxs-lookup"><span data-stu-id="d8477-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="d8477-127">Выбор осуществляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d8477-127">Here is a selection:</span></span>

- <span data-ttu-id="d8477-128">`<Color>` (изменение цвета)</span><span class="sxs-lookup"><span data-stu-id="d8477-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="d8477-129">`<FadeIn>` (снижение)</span><span class="sxs-lookup"><span data-stu-id="d8477-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="d8477-130">`<FadeOut>` (плавное уменьшение)</span><span class="sxs-lookup"><span data-stu-id="d8477-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="d8477-131">`<Property>` (изменение свойства элемента управления)</span><span class="sxs-lookup"><span data-stu-id="d8477-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="d8477-132">`<Pulse>` (пулсатинг)</span><span class="sxs-lookup"><span data-stu-id="d8477-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="d8477-133">`<Resize>` (изменение размера)</span><span class="sxs-lookup"><span data-stu-id="d8477-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="d8477-134">`<Scale>` (пропорциональное изменение размера)</span><span class="sxs-lookup"><span data-stu-id="d8477-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="d8477-135">В этом примере панель будет исчезать. Анимация должна принимать 1,5 секунд (`Duration` атрибут), отображая 24 кадра (шаги анимации) в секунду (`Fps` атрибут).</span><span class="sxs-lookup"><span data-stu-id="d8477-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="d8477-136">Ниже приведена полная разметка для элемента управления `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="d8477-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="d8477-137">При выполнении этого сценария панель отображается и постепенно исчезает в течение одной и половины секунд.</span><span class="sxs-lookup"><span data-stu-id="d8477-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="d8477-138">[![панель выходит из затухания](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d8477-138">[![The panel is fading out](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="d8477-139">Панель выйдет из режима исчезновения ([щелкните, чтобы просмотреть изображение с полным размером](adding-animation-to-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d8477-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d8477-140">[Назад](dynamically-controlling-updatepanel-animations-cs.md)
> [Вперед](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d8477-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>
