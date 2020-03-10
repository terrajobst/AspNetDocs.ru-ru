---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: Свертывание и развертывание панели из JavaScript (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и развертывать...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430596"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a><span data-ttu-id="3c9eb-103">Свертывание и развертывание панели из кода JavaScript (VB)</span><span class="sxs-lookup"><span data-stu-id="3c9eb-103">Collapsing and Expanding a Panel from JavaScript (VB)</span></span>

<span data-ttu-id="3c9eb-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3c9eb-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3c9eb-105">[Скачать код](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="3c9eb-105">[Download Code](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span></span>

> <span data-ttu-id="3c9eb-106">Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и расширять ее.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="3c9eb-107">Эти два действия также можно активировать из пользовательского кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-107">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="3c9eb-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="3c9eb-108">Overview</span></span>

<span data-ttu-id="3c9eb-109">Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и расширять ее.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="3c9eb-110">Эти два действия также можно активировать из пользовательского кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="3c9eb-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="3c9eb-111">Steps</span></span>

<span data-ttu-id="3c9eb-112">Во-первых, создайте новую страницу ASP.NET и включите `ScriptManager` в один элемент `<form>`.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="3c9eb-113">Это загружает библиотеку ASP.NET AJAX, которая необходима для набора средств управления.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="3c9eb-114">Затем создайте панель с текстом, чтобы можно было увидеть эффекты свертывания и развертывания:</span><span class="sxs-lookup"><span data-stu-id="3c9eb-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="3c9eb-115">Как видите, панель ссылается на класс CSS, показанный здесь (и, по сути, определяет цвет фона и ширину панели):</span><span class="sxs-lookup"><span data-stu-id="3c9eb-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

<span data-ttu-id="3c9eb-116">Элементу управления `CollapsiblePanelExtender` требуется атрибут `TargetControlID`, чтобы набор средств знал, какую панель нужно свернуть или развернуть по запросу:</span><span class="sxs-lookup"><span data-stu-id="3c9eb-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

<span data-ttu-id="3c9eb-117">К сожалению, в настоящее время расширитель не предоставляет определенный API для свертывания или развертывания панели, но некоторые недокументированные методы будут делаться.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="3c9eb-118">Во-первых, добавьте на страницу три кнопки HTML, которые затем активируют клиентский сценарий JavaScript, чтобы свернуть или развернуть содержимое панели:</span><span class="sxs-lookup"><span data-stu-id="3c9eb-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="3c9eb-119">В коде JavaScript на стороне клиента (запущенном с `<script type="text/javascript">`) для доступа к `CollapsiblePanelExtender`необходимо использовать метод `$find()`.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="3c9eb-120">`$find("cpe")` вернет ссылку на него.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="3c9eb-121">С этой стороны, конкретные методы решают поставленную задачу.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="3c9eb-122">Метод для открытия (расширения) панели называется `_doOpen()`; в следующем коде реализуется функция `doOpen()`, вызываемая при нажатии первой кнопки:</span><span class="sxs-lookup"><span data-stu-id="3c9eb-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

<span data-ttu-id="3c9eb-123">Для закрытия или свертывания панели необходимо выполнить метод `_doClose()`.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="3c9eb-124">Таким образом, когда пользователь нажимает на вторую кнопку, вызывается следующий код JavaScript:</span><span class="sxs-lookup"><span data-stu-id="3c9eb-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

<span data-ttu-id="3c9eb-125">Третья кнопка переключает состояние панели: с свернутого на развернутое и наоборот.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="3c9eb-126">`CollapsiblePanelExtender` предоставляет метод `toggle()`, который точно соответствует: изменяет состояние панели.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="3c9eb-127">Однако существует и другой подход (который внутренне используется методом `toggle()`): метод `get_Collapsed()` `CollapsiblePanelExtender()` указывающее, свернута ли панель.</span><span class="sxs-lookup"><span data-stu-id="3c9eb-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="3c9eb-128">В зависимости от возвращаемого значения этой функции панель разворачивается (`_doOpen()` метод) или сворачивается (`_doClose()`).</span><span class="sxs-lookup"><span data-stu-id="3c9eb-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

<span data-ttu-id="3c9eb-129">[![третья кнопка изменяет состояние панели: с свернутого на расширенное и обратно.](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3c9eb-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="3c9eb-130">Третья кнопка изменяет состояние панели: с свернутого на развернутое и обратное ([щелкните, чтобы просмотреть изображение с полным размером](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="3c9eb-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3c9eb-131">Назад</span><span class="sxs-lookup"><span data-stu-id="3c9eb-131">Previous</span></span>](collapsing-and-expanding-a-panel-from-javascript-cs.md)
