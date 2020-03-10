---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: Исполнение нескольких анимаций после друг другаC#() | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет запускать серьезность...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: e378ac038796dbd44e89d099532b9e186dcf673f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497826"
---
# <a name="executing-several-animations-after-each-other-c"></a><span data-ttu-id="7c047-104">Выполнение нескольких анимаций друг за другом (C#)</span><span class="sxs-lookup"><span data-stu-id="7c047-104">Executing Several Animations after Each Other (C#)</span></span>

<span data-ttu-id="7c047-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7c047-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7c047-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7c047-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span></span>

> <span data-ttu-id="7c047-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="7c047-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7c047-108">Он позволяет запускать несколько анимаций один за другим.</span><span class="sxs-lookup"><span data-stu-id="7c047-108">It allows to run several animations one after the other.</span></span>

<span data-ttu-id="7c047-109">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="7c047-109">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7c047-110">Он позволяет запускать несколько анимаций один за другим.</span><span class="sxs-lookup"><span data-stu-id="7c047-110">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="7c047-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="7c047-111">Steps</span></span>

<span data-ttu-id="7c047-112">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="7c047-112">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

<span data-ttu-id="7c047-113">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7c047-113">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

<span data-ttu-id="7c047-114">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="7c047-114">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

<span data-ttu-id="7c047-115">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и обязательную `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="7c047-115">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

<span data-ttu-id="7c047-116">В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="7c047-116">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="7c047-117">Как правило, `<OnLoad>` принимает только одну анимацию.</span><span class="sxs-lookup"><span data-stu-id="7c047-117">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="7c047-118">Платформа анимации позволяет объединить несколько анимаций в одну с помощью элемента `<Sequence>`.</span><span class="sxs-lookup"><span data-stu-id="7c047-118">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="7c047-119">Все анимации в `<Sequence>` выполняются один за другим.</span><span class="sxs-lookup"><span data-stu-id="7c047-119">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="7c047-120">Ниже приведена возможная разметка для элемента управления `AnimationExtender`, которая сначала делает панель шире, а затем уменьшает ее высоту:</span><span class="sxs-lookup"><span data-stu-id="7c047-120">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

<span data-ttu-id="7c047-121">При запуске этого скрипта панель сначала становится шире, а затем уменьшается.</span><span class="sxs-lookup"><span data-stu-id="7c047-121">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="7c047-122">[![сначала ширина увеличивается](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7c047-122">[![First the width is increased](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span></span>

<span data-ttu-id="7c047-123">Сначала увеличивается ширина ([щелкните, чтобы просмотреть изображение с полным размером](executing-several-animations-after-each-other-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7c047-123">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image3.png))</span></span>

<span data-ttu-id="7c047-124">[![будет уменьшена высота](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="7c047-124">[![Then the height is decreased](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span></span>

<span data-ttu-id="7c047-125">Затем уменьшается высота ([щелкните, чтобы просмотреть изображение с полным размером](executing-several-animations-after-each-other-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7c047-125">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7c047-126">[Назад](executing-several-animations-at-the-same-time-cs.md)
> [Вперед](animation-depending-on-a-condition-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7c047-126">[Previous](executing-several-animations-at-the-same-time-cs.md)
[Next](animation-depending-on-a-condition-cs.md)</span></span>
