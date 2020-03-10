---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: Выборка одной анимации из списка (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Платформа также разре...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 2bc203d694792716bbf4f7d7b8d152c589bf99b1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483846"
---
# <a name="picking-one-animation-out-of-a-list-c"></a><span data-ttu-id="40c00-104">Выбор одной анимации из списка (C#)</span><span class="sxs-lookup"><span data-stu-id="40c00-104">Picking One Animation Out Of a List (C#)</span></span>

<span data-ttu-id="40c00-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="40c00-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="40c00-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="40c00-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span></span>

> <span data-ttu-id="40c00-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="40c00-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="40c00-108">Платформа также позволяет программисту выбрать одну анимацию из списка анимаций в зависимости от оценки кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="40c00-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="40c00-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="40c00-109">Overview</span></span>

<span data-ttu-id="40c00-110">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="40c00-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="40c00-111">Платформа также позволяет программисту выбрать одну анимацию из списка анимаций в зависимости от оценки кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="40c00-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="40c00-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="40c00-112">Steps</span></span>

<span data-ttu-id="40c00-113">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="40c00-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

<span data-ttu-id="40c00-114">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="40c00-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

<span data-ttu-id="40c00-115">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="40c00-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

<span data-ttu-id="40c00-116">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и обязательную `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="40c00-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

<span data-ttu-id="40c00-117">В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="40c00-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="40c00-118">Вместо одной из обычных анимаций элемент `<Case>` поступает в игру.</span><span class="sxs-lookup"><span data-stu-id="40c00-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="40c00-119">Вычисляется значение его атрибута Селектскрипт. Возвращаемое значение должно быть числовым.</span><span class="sxs-lookup"><span data-stu-id="40c00-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="40c00-120">В зависимости от этого числа выполняется одна из вложенных анимаций в &lt;случае&gt;.</span><span class="sxs-lookup"><span data-stu-id="40c00-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="40c00-121">Например, если значение Селектскрипт равно 2, набор элементов управления запускает третью анимацию в &lt;&gt;е (отсчет начинается с 0).</span><span class="sxs-lookup"><span data-stu-id="40c00-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="40c00-122">Следующая разметка определяет три поданимации: изменение размера ширины, изменение высоты и плавность. Затем код JavaScript (`Math.floor(3 * Math.random())`) выбирает число от 0 до 2, чтобы выполнялась одна из трех анимаций:</span><span class="sxs-lookup"><span data-stu-id="40c00-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]

<span data-ttu-id="40c00-123">[![одной из возможных трех анимаций: панель становится шире](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="40c00-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span></span>

<span data-ttu-id="40c00-124">Одна из возможных трех анимаций: панель расширяется ([щелкните, чтобы просмотреть изображение с полным размером](picking-one-animation-out-of-a-list-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="40c00-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="40c00-125">[Назад](animation-depending-on-a-condition-cs.md)
> [Вперед](animating-in-response-to-user-interaction-cs.md)</span><span class="sxs-lookup"><span data-stu-id="40c00-125">[Previous](animation-depending-on-a-condition-cs.md)
[Next](animating-in-response-to-user-interaction-cs.md)</span></span>
