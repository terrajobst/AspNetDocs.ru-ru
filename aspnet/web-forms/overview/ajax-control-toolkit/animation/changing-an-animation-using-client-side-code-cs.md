---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: Изменение анимации с помощью кода на стороне клиента (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимация также может...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484056"
---
# <a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="1fe11-104">Изменение анимаций с помощью клиентского кода (C#)</span><span class="sxs-lookup"><span data-stu-id="1fe11-104">Changing an Animation Using Client-Side Code (C#)</span></span>

<span data-ttu-id="1fe11-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1fe11-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1fe11-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1fe11-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="1fe11-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="1fe11-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1fe11-108">Анимацию также можно изменить с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="1fe11-108">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="1fe11-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="1fe11-109">Overview</span></span>

<span data-ttu-id="1fe11-110">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="1fe11-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1fe11-111">Анимацию также можно изменить с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="1fe11-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="1fe11-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="1fe11-112">Steps</span></span>

<span data-ttu-id="1fe11-113">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="1fe11-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="1fe11-114">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1fe11-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="1fe11-115">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="1fe11-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="1fe11-116">Фактическая анимация запускается с помощью кнопки HTML:</span><span class="sxs-lookup"><span data-stu-id="1fe11-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="1fe11-117">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:</span><span class="sxs-lookup"><span data-stu-id="1fe11-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="1fe11-118">Обратите внимание, что в элементе управления `AnimationExtender` нет `<Animations>` узла.</span><span class="sxs-lookup"><span data-stu-id="1fe11-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="1fe11-119">Пользовательский код JavaScript используется для предоставления анимаций, используемых с элементом управления.</span><span class="sxs-lookup"><span data-stu-id="1fe11-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="1fe11-120">Как и в случае с API сервера `AnimationExtender`, еще нет простого способа присвоить анимацию расширительу.</span><span class="sxs-lookup"><span data-stu-id="1fe11-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="1fe11-121">Однако расширитель предоставляет несколько методов для чтения и записи анимации, зарегистрированной с различными событиями (`OnClick`, `OnLoad`и т. д.).</span><span class="sxs-lookup"><span data-stu-id="1fe11-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="1fe11-122">Ниже приведены некоторые примеры:</span><span class="sxs-lookup"><span data-stu-id="1fe11-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="1fe11-123">Формат возвращаемого значения функций `get_*()` и формат аргумента для функций `set_*()` являются строкой JSON, предоставляя объектное представление того, что будет иметь XML-разметка.</span><span class="sxs-lookup"><span data-stu-id="1fe11-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="1fe11-124">В настоящее время невозможно передать объект в, но можно считать объект из заданной анимации (`get_OnXXXBehavior()` методы).</span><span class="sxs-lookup"><span data-stu-id="1fe11-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="1fe11-125">Ниже приведена строка JSON (без кавычек и отформатированных), представляющая анимацию, активируемую кнопкой, но анимирование панели путем изменения ее размера и исчезновения ее в то же время:</span><span class="sxs-lookup"><span data-stu-id="1fe11-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="1fe11-126">Следующий код JavaScript назначает этот JSON-скрипта `OnClick` анимации текущего расширителя и выполняет его:</span><span class="sxs-lookup"><span data-stu-id="1fe11-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

<span data-ttu-id="1fe11-127">[![анимация выполняется немедленно, без щелчка мышью (и с очень маленькой разметкой)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1fe11-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="1fe11-128">Анимация выполняется немедленно, без щелчка мышью (и с очень маленькой разметкой) ([щелкните, чтобы просмотреть изображение с полным размером](changing-an-animation-using-client-side-code-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="1fe11-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1fe11-129">[Назад](executing-animations-using-client-side-code-cs.md)
> [Вперед](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1fe11-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
