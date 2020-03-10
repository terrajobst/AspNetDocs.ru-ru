---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: Активация анимации в другом элементе управления (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Как правило, запуск...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430788"
---
# <a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="8b5c9-104">Запуск анимации в другом элементе управления (VB)</span><span class="sxs-lookup"><span data-stu-id="8b5c9-104">Triggering an Animation in another Control (VB)</span></span>

<span data-ttu-id="8b5c9-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8b5c9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8b5c9-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8b5c9-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="8b5c9-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8b5c9-108">Как правило, запуск анимации запускается путем взаимодействия пользователя с тем же элементом управления.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="8b5c9-109">Однако можно также взаимодействовать с одним элементом управления и затем выполнять анимацию другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-109">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="overview"></a><span data-ttu-id="8b5c9-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="8b5c9-110">Overview</span></span>

<span data-ttu-id="8b5c9-111">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8b5c9-112">Как правило, запуск анимации запускается путем взаимодействия пользователя с тем же элементом управления.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="8b5c9-113">Однако можно также взаимодействовать с одним элементом управления и затем выполнять анимацию другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="8b5c9-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="8b5c9-114">Steps</span></span>

<span data-ttu-id="8b5c9-115">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="8b5c9-116">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8b5c9-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="8b5c9-117">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="8b5c9-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="8b5c9-118">Чтобы начать анимацию панели, используется кнопка HTML.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="8b5c9-119">Обратите внимание, что `<input type="button" />` фавауредся поверх `<asp:Button />`, поскольку не требуется обратная передача при нажатии пользователем этой кнопки.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="8b5c9-120">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="8b5c9-121">Важно присвоить `TargetControlID` ИДЕНТИФИКАТОРу кнопки (элементу, запускающему анимацию), а не ИДЕНТИФИКАТОРу панели (анимированный элемент).</span><span class="sxs-lookup"><span data-stu-id="8b5c9-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="8b5c9-122">В `<Animations>` узле поместите анимацию как обычно.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="8b5c9-123">Чтобы изменения были изменены на панели, а не на кнопке, установите атрибут `AnimationTarget` для каждого элемента анимации в `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="8b5c9-124">Значение для `AnimationTarget` — это идентификатор панели, разумеется.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="8b5c9-125">Таким образом, анимация происходит с панелью, а не с кнопкой запуска.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="8b5c9-126">Ниже приведена `AnimationExtender`ная разметка для этого сценария:</span><span class="sxs-lookup"><span data-stu-id="8b5c9-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="8b5c9-127">Обратите внимание на особый порядок, в котором отображаются отдельные анимации.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="8b5c9-128">Во первых, кнопка становится неактивной после запуска анимации.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="8b5c9-129">Так как в элементе `<EnableAction>` отсутствует атрибут `AnimationTarget`, эта анимация применяется к исходному элементу управления: кнопке.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="8b5c9-130">Следующие два этапа анимации должны выполняться параллельно (`<Parallel>` элемент).</span><span class="sxs-lookup"><span data-stu-id="8b5c9-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="8b5c9-131">Для обоих атрибутов `AnimationTarget` задано значение `"Panel1"`, что позволяет анимировать панель, а не кнопку.</span><span class="sxs-lookup"><span data-stu-id="8b5c9-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>

<span data-ttu-id="8b5c9-132">[![нажатии кнопки мыши запускает анимацию панели](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8b5c9-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="8b5c9-133">Щелчок мышью на кнопке запускает анимацию панели ([щелкните, чтобы просмотреть изображение с полным размером](triggering-an-animation-in-another-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8b5c9-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8b5c9-134">[Назад](disabling-actions-during-animation-vb.md)
> [Вперед](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8b5c9-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
