---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: Одновременное исполнение нескольких анимаций (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет запускать серьезность...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575354"
---
# <a name="executing-several-animations-at-the-same-time-c"></a><span data-ttu-id="7cea5-104">Одновременное исполнение нескольких анимаций (C#)</span><span class="sxs-lookup"><span data-stu-id="7cea5-104">Executing Several Animations at The Same Time (C#)</span></span>

<span data-ttu-id="7cea5-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7cea5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7cea5-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7cea5-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span></span>

> <span data-ttu-id="7cea5-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="7cea5-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7cea5-108">Он позволяет параллельно запускать несколько анимаций.</span><span class="sxs-lookup"><span data-stu-id="7cea5-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="7cea5-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="7cea5-109">Overview</span></span>

<span data-ttu-id="7cea5-110">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="7cea5-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7cea5-111">Он позволяет параллельно запускать несколько анимаций.</span><span class="sxs-lookup"><span data-stu-id="7cea5-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="7cea5-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="7cea5-112">Steps</span></span>

<span data-ttu-id="7cea5-113">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="7cea5-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

<span data-ttu-id="7cea5-114">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7cea5-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

<span data-ttu-id="7cea5-115">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="7cea5-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

<span data-ttu-id="7cea5-116">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:</span><span class="sxs-lookup"><span data-stu-id="7cea5-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

<span data-ttu-id="7cea5-117">В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="7cea5-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="7cea5-118">Как правило, `<OnLoad>` принимает только одну анимацию.</span><span class="sxs-lookup"><span data-stu-id="7cea5-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="7cea5-119">Платформа анимации позволяет объединить несколько анимаций в одну с помощью элемента `<Parallel>`.</span><span class="sxs-lookup"><span data-stu-id="7cea5-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="7cea5-120">Все анимации в `<Parallel>` выполняются одновременно.</span><span class="sxs-lookup"><span data-stu-id="7cea5-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="7cea5-121">Ниже приведена возможная разметка для элемента управления `AnimationExtender`, плавное уменьшение и изменение размера панели.</span><span class="sxs-lookup"><span data-stu-id="7cea5-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

<span data-ttu-id="7cea5-122">И действительно: при запуске этого скрипта панель отображается, затем изменяется размер (больше, чем утраивается ее ширина и вдвое высота) и плавно исчезает.</span><span class="sxs-lookup"><span data-stu-id="7cea5-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="7cea5-123">[![панель вытекает и изменяет ее размер (включая содержимое, благодаря подсистеме рендеринга в браузере).](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7cea5-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span></span>

<span data-ttu-id="7cea5-124">Панель вытекает и изменяет ее размер (включая содержимое, благодаря подсистеме рендеринга в браузере) ([щелкните, чтобы просмотреть изображение с полным размером](executing-several-animations-at-the-same-time-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="7cea5-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7cea5-125">[Назад](adding-animation-to-a-control-cs.md)
> [Вперед](executing-several-animations-after-each-other-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7cea5-125">[Previous](adding-animation-to-a-control-cs.md)
[Next](executing-several-animations-after-each-other-cs.md)</span></span>
