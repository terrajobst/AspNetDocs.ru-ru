---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: Привязка данных элемента управления SliderC#() | Документация Майкрософт
author: wenz
description: Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно привязать текущую поситио...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ef547573f17f3265ad72717d3d3bbc622fd6894e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445914"
---
# <a name="databinding-the-slider-control-c"></a><span data-ttu-id="3dd45-104">Привязка данных элемента управления Slider (C#)</span><span class="sxs-lookup"><span data-stu-id="3dd45-104">Databinding the Slider Control (C#)</span></span>

<span data-ttu-id="3dd45-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3dd45-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3dd45-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3dd45-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span></span>

> <span data-ttu-id="3dd45-107">Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши.</span><span class="sxs-lookup"><span data-stu-id="3dd45-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="3dd45-108">Можно привязать текущую положение ползунка к другому элементу управления ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3dd45-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="overview"></a><span data-ttu-id="3dd45-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="3dd45-109">Overview</span></span>

<span data-ttu-id="3dd45-110">Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши.</span><span class="sxs-lookup"><span data-stu-id="3dd45-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="3dd45-111">Можно привязать текущую положение ползунка к другому элементу управления ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3dd45-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="3dd45-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="3dd45-112">Steps</span></span>

<span data-ttu-id="3dd45-113">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):</span><span class="sxs-lookup"><span data-stu-id="3dd45-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

<span data-ttu-id="3dd45-114">Затем добавьте на страницу два элемента управления `TextBox`.</span><span class="sxs-lookup"><span data-stu-id="3dd45-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="3dd45-115">Один из них будет преобразован в графический ползунок, а другой будет содержать положение ползунка.</span><span class="sxs-lookup"><span data-stu-id="3dd45-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

<span data-ttu-id="3dd45-116">Следующий шаг уже является последним.</span><span class="sxs-lookup"><span data-stu-id="3dd45-116">The next step is already the final step.</span></span> <span data-ttu-id="3dd45-117">Элемент управления `SliderExtender` из набора средств управления AJAX ASP.NET делает ползунок из первого текстового поля и автоматически обновляет второе текстовое поле при изменении положения ползунка.</span><span class="sxs-lookup"><span data-stu-id="3dd45-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="3dd45-118">Чтобы это работало, атрибуту `TargetControlID` `SliderExtender`должен быть присвоен идентификатор первого текстового поля. атрибуту `BoundControlID` должен быть присвоен идентификатор второго текстового поля.</span><span class="sxs-lookup"><span data-stu-id="3dd45-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

<span data-ttu-id="3dd45-119">Как видно в браузере, привязка данных работает в обоих направлениях: ввод нового значения в текстовое поле обновляет положение ползунка.</span><span class="sxs-lookup"><span data-stu-id="3dd45-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="3dd45-120">Если сделать второе текстовое поле только для чтения, можно добавить слабую защиту в текстовое поле, чтобы пользователь не мог вручную обновить значение в нем.</span><span class="sxs-lookup"><span data-stu-id="3dd45-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>

<span data-ttu-id="3dd45-121">[Ползунок и текстовое поле ![синхронизированы](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3dd45-121">[![Slider and text box are in sync](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="3dd45-122">Ползунок и текстовое поле синхронизированы ([щелкните, чтобы просмотреть изображение с полным размером](databinding-the-slider-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3dd45-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3dd45-123">[Назад](using-the-slider-control-with-auto-postback-cs.md)
> [Вперед](using-the-slider-control-with-auto-postback-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3dd45-123">[Previous](using-the-slider-control-with-auto-postback-cs.md)
[Next](using-the-slider-control-with-auto-postback-vb.md)</span></span>
