---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: Обработка обратных передач из элемента управления Popup с помощью UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Необходимо уделить особое внимание...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: dd045ae56696c7944df98cf805ba812fde1bb4ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496638"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a><span data-ttu-id="7f408-104">Обработка операций обратной передачи из элемента управления Popup с помощью элемента управления UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="7f408-104">Handling Postbacks from A Popup Control With an UpdatePanel (VB)</span></span>

<span data-ttu-id="7f408-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7f408-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7f408-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7f408-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span></span>

> <span data-ttu-id="7f408-107">Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="7f408-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="7f408-108">При возникновении обратной передачи в таком всплывающем окне необходимо уделить особое внимание.</span><span class="sxs-lookup"><span data-stu-id="7f408-108">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="overview"></a><span data-ttu-id="7f408-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="7f408-109">Overview</span></span>

<span data-ttu-id="7f408-110">Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="7f408-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="7f408-111">При возникновении обратной передачи в таком всплывающем окне необходимо уделить особое внимание.</span><span class="sxs-lookup"><span data-stu-id="7f408-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="7f408-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="7f408-112">Steps</span></span>

<span data-ttu-id="7f408-113">При использовании `PopupControl` с обратной передачей `UpdatePanel` может препятствовать обновлению страницы, вызванной обратной передачей.</span><span class="sxs-lookup"><span data-stu-id="7f408-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="7f408-114">В следующей разметке определяется несколько важных элементов:</span><span class="sxs-lookup"><span data-stu-id="7f408-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="7f408-115">Элемент управления `ScriptManager`, обеспечивающий работу набора элементов управления AJAX ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7f408-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="7f408-116">Два элемента управления `TextBox`, которые будут активировать всплывающее окно</span><span class="sxs-lookup"><span data-stu-id="7f408-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="7f408-117">Элемент управления `Panel`, который будет служить в качестве всплывающего</span><span class="sxs-lookup"><span data-stu-id="7f408-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="7f408-118">На панели элемент управления `Calendar` внедрен в элемент управления `UpdatePanel`</span><span class="sxs-lookup"><span data-stu-id="7f408-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="7f408-119">Два элемента управления `PopupControlExtender`, которые присваивают панель текстовым полям</span><span class="sxs-lookup"><span data-stu-id="7f408-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="7f408-120">Обратите внимание, что задан атрибут `OnSelectionChanged` элемента управления `Calendar`.</span><span class="sxs-lookup"><span data-stu-id="7f408-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="7f408-121">Таким образом, когда пользователь выбирает дату в календаре, происходит обратная передача и выполняется `c1_SelectionChanged()` метод на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="7f408-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="7f408-122">В этом методе необходимо получить текущую дату и записать ее обратно в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="7f408-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="7f408-123">Синтаксис для этого выглядит следующим образом: сначала необходимо создать прокси-объект для `PopupControlExtender` на странице.</span><span class="sxs-lookup"><span data-stu-id="7f408-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="7f408-124">ASP.NET AJAX Control Toolkit предлагает метод `GetProxyForCurrentPopup()`.</span><span class="sxs-lookup"><span data-stu-id="7f408-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="7f408-125">Объект, возвращаемый этим методом, поддерживает `Commit()` метод, который отправляет значение обратно в элемент управления, который инициировал всплывающее окно (а не элемент управления, вызвавший вызов метода!).</span><span class="sxs-lookup"><span data-stu-id="7f408-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="7f408-126">Следующий код предоставляет выбранную дату в качестве аргумента для метода `Commit()`, что приводит к тому, что код записывает выбранную дату обратно в текстовое поле:</span><span class="sxs-lookup"><span data-stu-id="7f408-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="7f408-127">Теперь при выборе календарной даты выбранная дата отображается в соответствующем текстовом поле, создавая элемент управления выбора даты, который в настоящее время можно найти на многих веб-сайтах.</span><span class="sxs-lookup"><span data-stu-id="7f408-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>

<span data-ttu-id="7f408-128">[![календарь появляется, когда пользователь щелкает текстовое поле](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7f408-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="7f408-129">Календарь появляется, когда пользователь щелкает текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="7f408-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="7f408-130">[![, щелкнув дату, помещает ее в текстовое поле](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="7f408-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="7f408-131">Если щелкнуть дату, она помещается в текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7f408-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7f408-132">[Назад](using-multiple-popup-controls-vb.md)
> [Вперед](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7f408-132">[Previous](using-multiple-popup-controls-vb.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span></span>
