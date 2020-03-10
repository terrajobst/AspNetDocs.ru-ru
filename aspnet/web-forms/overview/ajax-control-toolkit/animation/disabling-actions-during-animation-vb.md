---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: Отключение действий во время анимации (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он также поддерживает действие...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430932"
---
# <a name="disabling-actions-during-animation-vb"></a><span data-ttu-id="fbeba-104">Отключение действий во время анимации (VB)</span><span class="sxs-lookup"><span data-stu-id="fbeba-104">Disabling Actions during Animation (VB)</span></span>

<span data-ttu-id="fbeba-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fbeba-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fbeba-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fbeba-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span></span>

> <span data-ttu-id="fbeba-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="fbeba-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fbeba-108">Он также поддерживает действия, например щелчки мыши.</span><span class="sxs-lookup"><span data-stu-id="fbeba-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="fbeba-109">Однако когда щелчок мыши запускает анимацию, желательно отключить щелчки мыши во время анимации.</span><span class="sxs-lookup"><span data-stu-id="fbeba-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="fbeba-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="fbeba-110">Overview</span></span>

<span data-ttu-id="fbeba-111">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="fbeba-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fbeba-112">Он также поддерживает действия, например щелчки мыши.</span><span class="sxs-lookup"><span data-stu-id="fbeba-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="fbeba-113">Однако когда щелчок мыши запускает анимацию, желательно отключить щелчки мыши во время анимации.</span><span class="sxs-lookup"><span data-stu-id="fbeba-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="fbeba-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="fbeba-114">Steps</span></span>

<span data-ttu-id="fbeba-115">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="fbeba-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

<span data-ttu-id="fbeba-116">Анимация будет применена к HTML-кнопке следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fbeba-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

<span data-ttu-id="fbeba-117">Обратите внимание, что элемент управления HTML используется вместо веб-элемента управления, так как не нужно, чтобы кнопка была создана обратной передачей. Он просто запускает анимацию на стороне клиента для нас.</span><span class="sxs-lookup"><span data-stu-id="fbeba-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="fbeba-118">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:</span><span class="sxs-lookup"><span data-stu-id="fbeba-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

<span data-ttu-id="fbeba-119">В `<Animations>` узле `<OnClick>` является правым элементом для управления щелчком мыши.</span><span class="sxs-lookup"><span data-stu-id="fbeba-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="fbeba-120">Однако во время анимации кнопка может быть нажата.</span><span class="sxs-lookup"><span data-stu-id="fbeba-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="fbeba-121">Элемент `<EnableAction>` может позаботиться об этом.</span><span class="sxs-lookup"><span data-stu-id="fbeba-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="fbeba-122">Параметр `Enabled="false"` отключает кнопку как часть анимации.</span><span class="sxs-lookup"><span data-stu-id="fbeba-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="fbeba-123">Так как мы используем несколько отдельных анимаций (отключив кнопку и фактические анимации), элемент `<Parallel>` необходим для объединения одной анимации в одну.</span><span class="sxs-lookup"><span data-stu-id="fbeba-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="fbeba-124">Ниже приведена полная разметка для `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="fbeba-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

<span data-ttu-id="fbeba-125">Кроме того, можно было бы снова включить кнопку после анимации, используя следующий XML-элемент в конце списка:</span><span class="sxs-lookup"><span data-stu-id="fbeba-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

<span data-ttu-id="fbeba-126">Однако в данном сценарии это будет бесполезно, так как кнопка исчезает и не отображается в конце анимации.</span><span class="sxs-lookup"><span data-stu-id="fbeba-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="fbeba-127">[![кнопка отключена сразу после запуска анимации](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fbeba-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span></span>

<span data-ttu-id="fbeba-128">Кнопка будет отключена сразу после запуска анимации ([щелкните, чтобы просмотреть изображение с полным размером](disabling-actions-during-animation-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="fbeba-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fbeba-129">[Назад](animating-in-response-to-user-interaction-vb.md)
> [Вперед](triggering-an-animation-in-another-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fbeba-129">[Previous](animating-in-response-to-user-interaction-vb.md)
[Next](triggering-an-animation-in-another-control-vb.md)</span></span>
