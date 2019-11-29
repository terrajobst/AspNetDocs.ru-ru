---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: Анимация в ответ на взаимодействие с пользователем (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимация может иметь вид звезды...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599871"
---
# <a name="animating-in-response-to-user-interaction-c"></a><span data-ttu-id="c493c-104">Анимация в ответ на взаимодействие пользователя (C#)</span><span class="sxs-lookup"><span data-stu-id="c493c-104">Animating in Response To User Interaction (C#)</span></span>

<span data-ttu-id="c493c-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c493c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c493c-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c493c-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span></span>

> <span data-ttu-id="c493c-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="c493c-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c493c-108">Анимации могут запускаться автоматически или могут запускаться пользователем, например, при щелчке мышью.</span><span class="sxs-lookup"><span data-stu-id="c493c-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="c493c-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="c493c-109">Overview</span></span>

<span data-ttu-id="c493c-110">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="c493c-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c493c-111">Анимации могут запускаться автоматически или могут запускаться пользователем, например, при щелчке мышью.</span><span class="sxs-lookup"><span data-stu-id="c493c-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="c493c-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="c493c-112">Steps</span></span>

<span data-ttu-id="c493c-113">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="c493c-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

<span data-ttu-id="c493c-114">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c493c-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

<span data-ttu-id="c493c-115">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="c493c-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

<span data-ttu-id="c493c-116">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:</span><span class="sxs-lookup"><span data-stu-id="c493c-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

<span data-ttu-id="c493c-117">В `<Animations>` узле существует пять способов запуска анимации с помощью взаимодействия с пользователем (отсутствующий элемент — `<OnLoad>` что выполняется после полной загрузки страницы целиком):</span><span class="sxs-lookup"><span data-stu-id="c493c-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="c493c-118">`<OnClick>` (щелчок мышью в элементе управления)</span><span class="sxs-lookup"><span data-stu-id="c493c-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="c493c-119">`<OnHoverOut>` (мышь выходит за пределы элемента управления)</span><span class="sxs-lookup"><span data-stu-id="c493c-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="c493c-120">`<OnHoverOver>` (наведение указателя мыши на элемент управления, остановка `<OnHoverOut>`ной анимации)</span><span class="sxs-lookup"><span data-stu-id="c493c-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="c493c-121">`<OnMouseOut>` (мышь выходит за пределы элемента управления)</span><span class="sxs-lookup"><span data-stu-id="c493c-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="c493c-122">`<OnMouseOver>` (наведение указателя мыши на элемент управления, но не останавливает анимацию `<OnMouseOut>`)</span><span class="sxs-lookup"><span data-stu-id="c493c-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="c493c-123">В этом сценарии используется `<OnClick>`.</span><span class="sxs-lookup"><span data-stu-id="c493c-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="c493c-124">Когда пользователь щелкает эту панель, он изменяется и постепенно исчезает.</span><span class="sxs-lookup"><span data-stu-id="c493c-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

<span data-ttu-id="c493c-125">[![щелчок мышью запускает анимацию](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c493c-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span></span>

<span data-ttu-id="c493c-126">Щелчок мышью запускает анимацию ([щелкните, чтобы просмотреть изображение с полным размером](animating-in-response-to-user-interaction-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c493c-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c493c-127">[Назад](picking-one-animation-out-of-a-list-cs.md)
> [Вперед](disabling-actions-during-animation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c493c-127">[Previous](picking-one-animation-out-of-a-list-cs.md)
[Next](disabling-actions-during-animation-cs.md)</span></span>
