---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: Обработка обратных передач из элемента управления Popup без UpdatePanel (C#) | Документация Майкрософт
author: wenz
description: Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Когда обратная передача происходит в SU...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496506"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a><span data-ttu-id="e7aac-104">Обработка операций обратной передачи из элемента управления Popup без использования элемента управления UpdatePanel (C#)</span><span class="sxs-lookup"><span data-stu-id="e7aac-104">Handling Postbacks from A Popup Control Without an UpdatePanel (C#)</span></span>

<span data-ttu-id="e7aac-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e7aac-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e7aac-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e7aac-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span></span>

> <span data-ttu-id="e7aac-107">Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="e7aac-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="e7aac-108">Если обратная передача происходит на такой панели и на странице есть несколько панелей, трудно определить, какая панель была нажата.</span><span class="sxs-lookup"><span data-stu-id="e7aac-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="e7aac-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="e7aac-109">Overview</span></span>

<span data-ttu-id="e7aac-110">Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="e7aac-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="e7aac-111">Если обратная передача происходит на такой панели и на странице есть несколько панелей, трудно определить, какая панель была нажата.</span><span class="sxs-lookup"><span data-stu-id="e7aac-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="e7aac-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="e7aac-112">Steps</span></span>

<span data-ttu-id="e7aac-113">При использовании `PopupControl` с обратной передачей, но без `UpdatePanel` на странице, набор элементов управления не предлагает способ определить, какой клиентский элемент инициировал всплывающее окно, которое, в свою очередь, вызвало обратную передачу.</span><span class="sxs-lookup"><span data-stu-id="e7aac-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="e7aac-114">Но небольшой хитростью является обходной путь для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="e7aac-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="e7aac-115">Во-первых, вот основная настройка: два текстовых поля, которые вызывают одно и то же всплывающее окно, календарь.</span><span class="sxs-lookup"><span data-stu-id="e7aac-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="e7aac-116">Два `PopupControlExtenders` поместит текстовые поля и всплывающее окно вместе.</span><span class="sxs-lookup"><span data-stu-id="e7aac-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="e7aac-117">Основная идея состоит в том, чтобы добавить скрытое поле формы в элемент &lt;`form`&gt;, содержащий текстовое поле, которое запустило всплывающее окно:</span><span class="sxs-lookup"><span data-stu-id="e7aac-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="e7aac-118">При загрузке страницы код JavaScript добавляет обработчик событий в оба текстовых поля: каждый раз, когда пользователь щелкает текстовое поле, его имя записывается в скрытое поле формы:</span><span class="sxs-lookup"><span data-stu-id="e7aac-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

<span data-ttu-id="e7aac-119">В коде на стороне сервера значение скрытого поля должно быть считано.</span><span class="sxs-lookup"><span data-stu-id="e7aac-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="e7aac-120">Поскольку скрытые поля формы просты для управления, утвержденный список способов проверки скрытые значения является обязательным.</span><span class="sxs-lookup"><span data-stu-id="e7aac-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="e7aac-121">После определения правильного текстового поля в него записывается дата из календаря.</span><span class="sxs-lookup"><span data-stu-id="e7aac-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

<span data-ttu-id="e7aac-122">[![календарь появляется, когда пользователь щелкает текстовое поле](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e7aac-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="e7aac-123">Календарь появляется, когда пользователь щелкает текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="e7aac-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span></span>

<span data-ttu-id="e7aac-124">[![, щелкнув дату, помещает ее в текстовое поле](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e7aac-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="e7aac-125">Если щелкнуть дату, она помещается в текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e7aac-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e7aac-126">[Назад](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [Вперед](using-multiple-popup-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e7aac-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
[Next](using-multiple-popup-controls-vb.md)</span></span>
