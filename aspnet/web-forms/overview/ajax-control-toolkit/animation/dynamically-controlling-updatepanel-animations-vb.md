---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: Динамическое управление анимациями UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 97a52bd75fdf63ad62282afd9df772f0a9e4f931
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430860"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="fcc1b-104">Динамическое управление анимациями UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="fcc1b-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>

<span data-ttu-id="fcc1b-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fcc1b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fcc1b-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fcc1b-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="fcc1b-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fcc1b-108">Для содержимого UpdatePanel существует специальный расширитель, который сильно зависит от платформы анимации: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="fcc1b-109">Он также может работать вместе с триггерами UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="fcc1b-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="fcc1b-110">Overview</span></span>

<span data-ttu-id="fcc1b-111">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fcc1b-112">Для содержимого `UpdatePanel`существует специальный расширитель, который сильно зависит от платформы анимации: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="fcc1b-113">Он также может работать вместе с триггерами `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="fcc1b-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="fcc1b-114">Steps</span></span>

<span data-ttu-id="fcc1b-115">Первым шагом является включение `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и использовать набор элементов управления.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="fcc1b-116">Анимация в этом сценарии будет применена к отображению текущего времени.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="fcc1b-117">Эти сведения можно записать в метку с помощью метода `Page_Load()` или (для простоты) используется следующий встроенный код:</span><span class="sxs-lookup"><span data-stu-id="fcc1b-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="fcc1b-118">Кроме того, создается кнопка для активации обновления времени.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="fcc1b-119">Затем этот код помещается в раздел `<ContentTemplate>` элемента `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="fcc1b-120">Атрибут `UpdateMode` панели должен иметь значение `"Conditional"`, так как только триггеры могут обновлять содержимое панели.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="fcc1b-121">В разделе `<Triggers>` `UpdatePanel`создается триггер асинхронной обратной передачи, связанный с событием `Click` кнопки.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="fcc1b-122">Таким же, если пользователь нажимает кнопку, `UpdatePanel` обновляется.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="fcc1b-123">Ниже приведена разметка для элемента управления `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="fcc1b-124">Наконец, необходимо настроить `UpdatePanelAnimationExtender`: присвойте атрибуту `TargetControlID` идентификатор панели и определите анимацию в расширителье.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="fcc1b-125">Плавное появление имеет смысл, что создает привлекательное визуальное внимание на обновленное время.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="fcc1b-126">Разметка расширителя может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fcc1b-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="fcc1b-127">Запустите файл в браузере.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-127">Run the file in the browser.</span></span> <span data-ttu-id="fcc1b-128">При каждом нажатии кнопки текущее время отображается на панели, а в течение одной секунды всегда выводится на экран.</span><span class="sxs-lookup"><span data-stu-id="fcc1b-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="fcc1b-129">[![текущее время помещается в плавность](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fcc1b-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span></span>

<span data-ttu-id="fcc1b-130">Текущее время отображается в виде затухания ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fcc1b-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fcc1b-131">Назад</span><span class="sxs-lookup"><span data-stu-id="fcc1b-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
