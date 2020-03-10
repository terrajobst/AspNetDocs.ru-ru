---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: Использование нескольких элементов управления PopupC#() | Документация Майкрософт
author: wenz
description: Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Также можно использовать m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496428"
---
# <a name="using-multiple-popup-controls-c"></a><span data-ttu-id="0a77e-104">Использование нескольких элементов управления Popup (C#)</span><span class="sxs-lookup"><span data-stu-id="0a77e-104">Using Multiple Popup Controls (C#)</span></span>

<span data-ttu-id="0a77e-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0a77e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0a77e-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="0a77e-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="0a77e-107">Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="0a77e-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="0a77e-108">На одной странице также можно использовать несколько элементов управления Popup.</span><span class="sxs-lookup"><span data-stu-id="0a77e-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="0a77e-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="0a77e-109">Overview</span></span>

<span data-ttu-id="0a77e-110">Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="0a77e-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="0a77e-111">На одной странице также можно использовать несколько элементов управления Popup.</span><span class="sxs-lookup"><span data-stu-id="0a77e-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="0a77e-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="0a77e-112">Steps</span></span>

<span data-ttu-id="0a77e-113">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):</span><span class="sxs-lookup"><span data-stu-id="0a77e-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="0a77e-114">Затем добавьте панель, которая выступает в качестве всплывающего.</span><span class="sxs-lookup"><span data-stu-id="0a77e-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="0a77e-115">В текущем сценарии панель содержит элемент управления `Calendar`.</span><span class="sxs-lookup"><span data-stu-id="0a77e-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="0a77e-116">Чтобы избежать обновления страниц, вызванных обратными передачами календаря, панель помещается в элемент управления `UpdatePanel`:</span><span class="sxs-lookup"><span data-stu-id="0a77e-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="0a77e-117">Страница также содержит два текстовых поля.</span><span class="sxs-lookup"><span data-stu-id="0a77e-117">The page also contains two text boxes.</span></span> <span data-ttu-id="0a77e-118">Для каждого текстового поля всплывающее окно календаря появляется после активации текстового поля.</span><span class="sxs-lookup"><span data-stu-id="0a77e-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="0a77e-119">Теперь расширьте каждое из двух текстовых полей с помощью `PopupControlExtender`.</span><span class="sxs-lookup"><span data-stu-id="0a77e-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="0a77e-120">Атрибут `TargetControlID` предоставляет идентификатор элемента управления, привязанного к расширителю.</span><span class="sxs-lookup"><span data-stu-id="0a77e-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="0a77e-121">Атрибут `PopupControlID` содержит идентификатор всплывающей панели.</span><span class="sxs-lookup"><span data-stu-id="0a77e-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="0a77e-122">В этом случае оба расширителя отображают одну и ту же панель, но также могут быть разными панелями.</span><span class="sxs-lookup"><span data-stu-id="0a77e-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="0a77e-123">Теперь, когда вы щелкнули текстовое поле, под полем появляется календарь, позволяющий выбрать дату.</span><span class="sxs-lookup"><span data-stu-id="0a77e-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="0a77e-124">(Чтобы получить выбранную дату обратно в текстовые поля, появятся различные учебники.)</span><span class="sxs-lookup"><span data-stu-id="0a77e-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="0a77e-125">[![календарь появляется, когда пользователь щелкает текстовое поле](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0a77e-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="0a77e-126">Календарь появляется, когда пользователь щелкает текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](using-multiple-popup-controls-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="0a77e-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0a77e-127">Дальше</span><span class="sxs-lookup"><span data-stu-id="0a77e-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
