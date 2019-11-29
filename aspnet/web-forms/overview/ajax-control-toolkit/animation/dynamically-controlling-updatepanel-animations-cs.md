---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: Динамическое управление анимациямиC#UpdatePanel () | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606804"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a><span data-ttu-id="7b02e-104">Динамическое управление анимациями UpdatePanel (C#)</span><span class="sxs-lookup"><span data-stu-id="7b02e-104">Dynamically Controlling UpdatePanel Animations (C#)</span></span>

<span data-ttu-id="7b02e-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7b02e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7b02e-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7b02e-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span></span>

> <span data-ttu-id="7b02e-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="7b02e-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7b02e-108">Для содержимого UpdatePanel существует специальный расширитель, который сильно зависит от платформы анимации: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="7b02e-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="7b02e-109">Он также может работать вместе с триггерами UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="7b02e-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="7b02e-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="7b02e-110">Overview</span></span>

<span data-ttu-id="7b02e-111">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="7b02e-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7b02e-112">Для содержимого `UpdatePanel`существует специальный расширитель, который сильно зависит от платформы анимации: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="7b02e-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="7b02e-113">Он также может работать вместе с триггерами `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="7b02e-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="7b02e-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="7b02e-114">Steps</span></span>

<span data-ttu-id="7b02e-115">Первым шагом является включение `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и использовать набор элементов управления.</span><span class="sxs-lookup"><span data-stu-id="7b02e-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

<span data-ttu-id="7b02e-116">Анимация в этом сценарии будет применена к отображению текущего времени.</span><span class="sxs-lookup"><span data-stu-id="7b02e-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="7b02e-117">Эти сведения можно записать в метку с помощью метода `Page_Load()` или (для простоты) используется следующий встроенный код:</span><span class="sxs-lookup"><span data-stu-id="7b02e-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

<span data-ttu-id="7b02e-118">Кроме того, создается кнопка для активации обновления времени.</span><span class="sxs-lookup"><span data-stu-id="7b02e-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

<span data-ttu-id="7b02e-119">Затем этот код помещается в раздел `<ContentTemplate>` элемента `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="7b02e-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="7b02e-120">Атрибут `UpdateMode` панели должен иметь значение `"Conditional"`, так как только триггеры могут обновлять содержимое панели.</span><span class="sxs-lookup"><span data-stu-id="7b02e-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="7b02e-121">В разделе `<Triggers>` `UpdatePanel`создается триггер асинхронной обратной передачи, связанный с событием `Click` кнопки.</span><span class="sxs-lookup"><span data-stu-id="7b02e-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="7b02e-122">Таким же, если пользователь нажимает кнопку, `UpdatePanel` обновляется.</span><span class="sxs-lookup"><span data-stu-id="7b02e-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="7b02e-123">Ниже приведена разметка для элемента управления `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="7b02e-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

<span data-ttu-id="7b02e-124">Наконец, необходимо настроить `UpdatePanelAnimationExtender`: присвойте атрибуту `TargetControlID` идентификатор панели и определите анимацию в расширителье.</span><span class="sxs-lookup"><span data-stu-id="7b02e-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="7b02e-125">Плавное появление имеет смысл, что создает привлекательное визуальное внимание на обновленное время.</span><span class="sxs-lookup"><span data-stu-id="7b02e-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="7b02e-126">Разметка расширителя может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7b02e-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

<span data-ttu-id="7b02e-127">Запустите файл в браузере.</span><span class="sxs-lookup"><span data-stu-id="7b02e-127">Run the file in the browser.</span></span> <span data-ttu-id="7b02e-128">При каждом нажатии кнопки текущее время отображается на панели, а в течение одной секунды всегда выводится на экран.</span><span class="sxs-lookup"><span data-stu-id="7b02e-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="7b02e-129">[![текущее время помещается в плавность](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7b02e-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span></span>

<span data-ttu-id="7b02e-130">Текущее время отображается в виде затухания ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7b02e-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7b02e-131">[Назад](animating-an-updatepanel-control-cs.md)
> [Вперед](adding-animation-to-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7b02e-131">[Previous](animating-an-updatepanel-control-cs.md)
[Next](adding-animation-to-a-control-vb.md)</span></span>
