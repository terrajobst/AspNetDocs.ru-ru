---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: Выбор одной анимации из списка (Visual Basic) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Платформа также ра...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c60d7cff7c841d23185fbdf07abf0e894b21cf5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029501"
---
<a name="picking-one-animation-out-of-a-list-vb"></a><span data-ttu-id="87563-104">Выбор одной анимации из списка (VB)</span><span class="sxs-lookup"><span data-stu-id="87563-104">Picking One Animation Out Of a List (VB)</span></span>
====================
<span data-ttu-id="87563-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="87563-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="87563-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="87563-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span></span>

> <span data-ttu-id="87563-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="87563-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="87563-108">Платформа также позволяет программисту Выбор одной анимации из списка анимации, в зависимости от оценки кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="87563-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="87563-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="87563-109">Overview</span></span>

<span data-ttu-id="87563-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="87563-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="87563-111">Платформа также позволяет программисту Выбор одной анимации из списка анимации, в зависимости от оценки кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="87563-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="87563-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="87563-112">Steps</span></span>

<span data-ttu-id="87563-113">Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:</span><span class="sxs-lookup"><span data-stu-id="87563-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

<span data-ttu-id="87563-114">Анимация будет применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="87563-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

<span data-ttu-id="87563-115">В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:</span><span class="sxs-lookup"><span data-stu-id="87563-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

<span data-ttu-id="87563-116">Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="87563-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

<span data-ttu-id="87563-117">В рамках `<Animations>` узла, используйте `<OnLoad>` для запуска анимации после полной загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="87563-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="87563-118">Вместо одного из обычных анимаций `<Case>` элемент вступает в действие.</span><span class="sxs-lookup"><span data-stu-id="87563-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="87563-119">Значение атрибута SelectScript вычисляется; Возвращаемое значение должно быть числовым.</span><span class="sxs-lookup"><span data-stu-id="87563-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="87563-120">В зависимости от того, это число, один из subanimations в &lt;случай&gt; выполняется.</span><span class="sxs-lookup"><span data-stu-id="87563-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="87563-121">Например, если SelectScript равно 2, Control Toolkit выполняется третий анимации в &lt;случай&gt; (перечисление начинается с 0).</span><span class="sxs-lookup"><span data-stu-id="87563-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="87563-122">Следующая разметка определяет три subanimations: Изменение размера ширины и изменение размера Высота исчезновение. Код JavaScript (`Math.floor(3 * Math.random())`) затем выбирает число от 0 до 2, так, что выполняется одно из трех анимации:</span><span class="sxs-lookup"><span data-stu-id="87563-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]


<span data-ttu-id="87563-123">[![Одна из возможных три анимации: Получает ширину панели](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="87563-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span></span>

<span data-ttu-id="87563-124">Одна из возможных три анимации: Получает ширину панели ([Просмотр полноразмерного изображения](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="87563-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="87563-125">[Назад](animation-depending-on-a-condition-vb.md)
> [Вперед](animating-in-response-to-user-interaction-vb.md)</span><span class="sxs-lookup"><span data-stu-id="87563-125">[Previous](animation-depending-on-a-condition-vb.md)
[Next](animating-in-response-to-user-interaction-vb.md)</span></span>
