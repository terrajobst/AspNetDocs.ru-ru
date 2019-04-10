---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: Добавление анимации в элемент управления (C#) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. В этом руководстве показано как...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: e4c6bfe1884d3e066c7b27e07e3a069943793bdd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392291"
---
# <a name="adding-animation-to-a-control-c"></a><span data-ttu-id="1f6b9-104">Добавление анимации в элемент управления (C#)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-104">Adding Animation to a Control (C#)</span></span>

<span data-ttu-id="1f6b9-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1f6b9-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="1f6b9-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="1f6b9-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1f6b9-108">Этом руководстве показано, как настроить такой анимации.</span><span class="sxs-lookup"><span data-stu-id="1f6b9-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="1f6b9-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="1f6b9-109">Overview</span></span>

<span data-ttu-id="1f6b9-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="1f6b9-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1f6b9-111">Этом руководстве показано, как настроить такой анимации.</span><span class="sxs-lookup"><span data-stu-id="1f6b9-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="1f6b9-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="1f6b9-112">Steps</span></span>

<span data-ttu-id="1f6b9-113">Первым шагом является обычным образом, чтобы включить `ScriptManager` на странице, ASP.NET AJAX library загружается и может использоваться набор элементов управления:</span><span class="sxs-lookup"><span data-stu-id="1f6b9-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="1f6b9-114">Анимация в этом сценарии будут применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1f6b9-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="1f6b9-115">Связанный класс CSS для панели определяет цвет фона и шириной:</span><span class="sxs-lookup"><span data-stu-id="1f6b9-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="1f6b9-116">Далее, необходимо `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="1f6b9-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="1f6b9-117">После предоставления `ID` и обычные `runat="server"`, `TargetControlID` атрибута необходимо задать для элемента управления для анимации в нашем случае панели:</span><span class="sxs-lookup"><span data-stu-id="1f6b9-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="1f6b9-118">Всего применяется анимация декларативно, используя синтаксис XML, к сожалению в настоящее время не полностью поддерживается технологией IntelliSense в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f6b9-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="1f6b9-119">Корневым узлом является `<Animations>;` в этот узел, несколько событий разрешены определяющие при анимации take(s) месте:</span><span class="sxs-lookup"><span data-stu-id="1f6b9-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- `OnClick` <span data-ttu-id="1f6b9-120">(щелчка мыши)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-120">(mouse click)</span></span>
- `OnHoverOut` <span data-ttu-id="1f6b9-121">(когда указатель мыши покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-121">(when the mouse leaves a control)</span></span>
- `OnHoverOver` <span data-ttu-id="1f6b9-122">(при наведении указателя мыши над элементом управления, остановка `OnHoverOut` анимации)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-122">(when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- `OnLoad` <span data-ttu-id="1f6b9-123">(когда страницы загрузки)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-123">(when the page has been loaded)</span></span>
- `OnMouseOut` <span data-ttu-id="1f6b9-124">(когда указатель мыши покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-124">(when the mouse leaves a control)</span></span>
- `OnMouseOver` <span data-ttu-id="1f6b9-125">(при наведении указателя мыши над элементом управления, не останавливает `OnMouseOut` анимации)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-125">(when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="1f6b9-126">Платформа framework поставляется с набором анимации, каждый из них, представленный собственным XML-элементом.</span><span class="sxs-lookup"><span data-stu-id="1f6b9-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="1f6b9-127">Ниже указаны:</span><span class="sxs-lookup"><span data-stu-id="1f6b9-127">Here is a selection:</span></span>

- `<Color>` <span data-ttu-id="1f6b9-128">(Изменение цвета)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-128">(changing a color)</span></span>
- `<FadeIn>` <span data-ttu-id="1f6b9-129">(плавный переход)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-129">(fading in)</span></span>
- `<FadeOut>` <span data-ttu-id="1f6b9-130">(исчезновение)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-130">(fading out)</span></span>
- `<Property>` <span data-ttu-id="1f6b9-131">(изменение свойства элемента управления)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-131">(changing a control's property)</span></span>
- `<Pulse>` <span data-ttu-id="1f6b9-132">(pulsating)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-132">(pulsating)</span></span>
- `<Resize>` <span data-ttu-id="1f6b9-133">(изменение размера)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-133">(changing the size)</span></span>
- `<Scale>` <span data-ttu-id="1f6b9-134">(Пропорциональное изменение размера)</span><span class="sxs-lookup"><span data-stu-id="1f6b9-134">(proportionally changing the size)</span></span>

<span data-ttu-id="1f6b9-135">В этом примере панели должны скрывать. Анимация должна осуществляться 1,5 секунды (`Duration` атрибут), отображение 24 (анимации шаги) кадров в секунду (`Fps` атрибут).</span><span class="sxs-lookup"><span data-stu-id="1f6b9-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="1f6b9-136">Вот полная разметка для `AnimationExtender` управления:</span><span class="sxs-lookup"><span data-stu-id="1f6b9-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="1f6b9-137">При выполнении этого скрипта панели отображается и исчезает в один с половиной секунд.</span><span class="sxs-lookup"><span data-stu-id="1f6b9-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


[![T<span data-ttu-id="1f6b9-138">панель HE исчезновение]</span><span class="sxs-lookup"><span data-stu-id="1f6b9-138">he panel is fading out]</span></span>(adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)

<span data-ttu-id="1f6b9-139">Исчезновение панели ([Просмотр полноразмерного изображения](adding-animation-to-a-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1f6b9-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1f6b9-140">Далее</span><span class="sxs-lookup"><span data-stu-id="1f6b9-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
