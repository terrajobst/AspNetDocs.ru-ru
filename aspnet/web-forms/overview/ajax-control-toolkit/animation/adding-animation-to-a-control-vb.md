---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: Добавление анимации в элемент управления (Visual Basic) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. В этом руководстве показано как...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: c55bbeb383b15f4dc9cb95d25905cade1e8c5c29
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418902"
---
# <a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="0db2b-104">Добавление анимации в элемент управления (VB)</span><span class="sxs-lookup"><span data-stu-id="0db2b-104">Adding Animation to a Control (VB)</span></span>

<span data-ttu-id="0db2b-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0db2b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0db2b-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0db2b-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="0db2b-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="0db2b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0db2b-108">Этом руководстве показано, как настроить такой анимации.</span><span class="sxs-lookup"><span data-stu-id="0db2b-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="0db2b-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="0db2b-109">Overview</span></span>

<span data-ttu-id="0db2b-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="0db2b-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0db2b-111">Этом руководстве показано, как настроить такой анимации.</span><span class="sxs-lookup"><span data-stu-id="0db2b-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="0db2b-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="0db2b-112">Steps</span></span>

<span data-ttu-id="0db2b-113">Первым шагом является обычным образом, чтобы включить `ScriptManager` на странице, ASP.NET AJAX library загружается и может использоваться набор элементов управления:</span><span class="sxs-lookup"><span data-stu-id="0db2b-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="0db2b-114">Анимация в этом сценарии будут применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0db2b-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="0db2b-115">Связанный класс CSS для панели определяет цвет фона и шириной:</span><span class="sxs-lookup"><span data-stu-id="0db2b-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="0db2b-116">Далее, необходимо `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="0db2b-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="0db2b-117">После предоставления `ID` и обычные `runat="server"`, `TargetControlID` атрибута необходимо задать для элемента управления для анимации в нашем случае панели:</span><span class="sxs-lookup"><span data-stu-id="0db2b-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="0db2b-118">Всего применяется анимация декларативно, используя синтаксис XML, к сожалению в настоящее время не полностью поддерживается технологией IntelliSense в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0db2b-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="0db2b-119">Корневым узлом является `<Animations>;` в этот узел, несколько событий разрешены определяющие при анимации take(s) месте:</span><span class="sxs-lookup"><span data-stu-id="0db2b-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- `OnClick` <span data-ttu-id="0db2b-120">(щелчка мыши)</span><span class="sxs-lookup"><span data-stu-id="0db2b-120">(mouse click)</span></span>
- `OnHoverOut` <span data-ttu-id="0db2b-121">(когда указатель мыши покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="0db2b-121">(when the mouse leaves a control)</span></span>
- `OnHoverOver` <span data-ttu-id="0db2b-122">(при наведении указателя мыши над элементом управления, остановка `OnHoverOut` анимации)</span><span class="sxs-lookup"><span data-stu-id="0db2b-122">(when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- `OnLoad` <span data-ttu-id="0db2b-123">(когда страницы загрузки)</span><span class="sxs-lookup"><span data-stu-id="0db2b-123">(when the page has been loaded)</span></span>
- `OnMouseOut` <span data-ttu-id="0db2b-124">(когда указатель мыши покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="0db2b-124">(when the mouse leaves a control)</span></span>
- `OnMouseOver` <span data-ttu-id="0db2b-125">(при наведении указателя мыши над элементом управления, не останавливает `OnMouseOut` анимации)</span><span class="sxs-lookup"><span data-stu-id="0db2b-125">(when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="0db2b-126">Платформа framework поставляется с набором анимации, каждый из них, представленный собственным XML-элементом.</span><span class="sxs-lookup"><span data-stu-id="0db2b-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="0db2b-127">Ниже указаны:</span><span class="sxs-lookup"><span data-stu-id="0db2b-127">Here is a selection:</span></span>

- `<Color>` <span data-ttu-id="0db2b-128">(Изменение цвета)</span><span class="sxs-lookup"><span data-stu-id="0db2b-128">(changing a color)</span></span>
- `<FadeIn>` <span data-ttu-id="0db2b-129">(плавный переход)</span><span class="sxs-lookup"><span data-stu-id="0db2b-129">(fading in)</span></span>
- `<FadeOut>` <span data-ttu-id="0db2b-130">(исчезновение)</span><span class="sxs-lookup"><span data-stu-id="0db2b-130">(fading out)</span></span>
- `<Property>` <span data-ttu-id="0db2b-131">(изменение свойства элемента управления)</span><span class="sxs-lookup"><span data-stu-id="0db2b-131">(changing a control's property)</span></span>
- `<Pulse>` <span data-ttu-id="0db2b-132">(pulsating)</span><span class="sxs-lookup"><span data-stu-id="0db2b-132">(pulsating)</span></span>
- `<Resize>` <span data-ttu-id="0db2b-133">(изменение размера)</span><span class="sxs-lookup"><span data-stu-id="0db2b-133">(changing the size)</span></span>
- `<Scale>` <span data-ttu-id="0db2b-134">(Пропорциональное изменение размера)</span><span class="sxs-lookup"><span data-stu-id="0db2b-134">(proportionally changing the size)</span></span>

<span data-ttu-id="0db2b-135">В этом примере панели должны скрывать. Анимация должна осуществляться 1,5 секунды (`Duration` атрибут), отображение 24 (анимации шаги) кадров в секунду (`Fps` атрибут).</span><span class="sxs-lookup"><span data-stu-id="0db2b-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="0db2b-136">Вот полная разметка для `AnimationExtender` управления:</span><span class="sxs-lookup"><span data-stu-id="0db2b-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="0db2b-137">При выполнении этого скрипта панели отображается и исчезает в один с половиной секунд.</span><span class="sxs-lookup"><span data-stu-id="0db2b-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


[![T<span data-ttu-id="0db2b-138">панель HE исчезновение]</span><span class="sxs-lookup"><span data-stu-id="0db2b-138">he panel is fading out]</span></span>(adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

<span data-ttu-id="0db2b-139">Исчезновение панели ([Просмотр полноразмерного изображения](adding-animation-to-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0db2b-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0db2b-140">[Назад](dynamically-controlling-updatepanel-animations-cs.md)
> [Вперед](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0db2b-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>
