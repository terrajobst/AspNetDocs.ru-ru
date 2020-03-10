---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: Использование обратных передач с элемента управления ReorderList (VB) | Документация Майкрософт
author: wenz
description: Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Каждый раз, когда список переупорядочивается, PO...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 5d6075e40df2c32df6c0d801243eff98fa7790b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445932"
---
# <a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="752f0-104">Использование обратных передач с помощью элемента управления ReorderList (VB)</span><span class="sxs-lookup"><span data-stu-id="752f0-104">Using Postbacks with ReorderList (VB)</span></span>

<span data-ttu-id="752f0-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="752f0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="752f0-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="752f0-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="752f0-107">Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="752f0-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="752f0-108">Каждый раз, когда список переупорядочивается, обратная передача сообщает серверу об изменении.</span><span class="sxs-lookup"><span data-stu-id="752f0-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="752f0-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="752f0-109">Overview</span></span>

<span data-ttu-id="752f0-110">Элемент управления `ReorderList` в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="752f0-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="752f0-111">Каждый раз, когда список переупорядочивается, обратная передача сообщает серверу об изменении.</span><span class="sxs-lookup"><span data-stu-id="752f0-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="752f0-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="752f0-112">Steps</span></span>

<span data-ttu-id="752f0-113">Существует несколько источников данных для элемента управления `ReorderList`.</span><span class="sxs-lookup"><span data-stu-id="752f0-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="752f0-114">Один из них — использовать элемент управления `XmlDataSource`:</span><span class="sxs-lookup"><span data-stu-id="752f0-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="752f0-115">Чтобы привязать этот XML-код к элементу управления `ReorderList` и включить обратные передачи, необходимо задать следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="752f0-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="752f0-116">`DataSourceID`: идентификатор источника данных</span><span class="sxs-lookup"><span data-stu-id="752f0-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="752f0-117">`SortOrderField`: свойство для сортировки</span><span class="sxs-lookup"><span data-stu-id="752f0-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="752f0-118">`AllowReorder`: следует ли разрешить пользователю изменять порядок элементов списка</span><span class="sxs-lookup"><span data-stu-id="752f0-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="752f0-119">`PostBackOnReorder`: следует ли создавать обратную передачу при переупорядочении списка</span><span class="sxs-lookup"><span data-stu-id="752f0-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="752f0-120">Ниже приведена соответствующая разметка для элемента управления.</span><span class="sxs-lookup"><span data-stu-id="752f0-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="752f0-121">В элементе управления `ReorderList` определенные данные из источника данных могут быть привязаны с помощью метода `Eval()`:</span><span class="sxs-lookup"><span data-stu-id="752f0-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="752f0-122">В произвольной позиции на странице метка будет содержать сведения о последнем переупорядочении:</span><span class="sxs-lookup"><span data-stu-id="752f0-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="752f0-123">Эта метка заполняется текстом в коде на стороне сервера, обрабатывая обратную передачу:</span><span class="sxs-lookup"><span data-stu-id="752f0-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="752f0-124">Наконец, чтобы активировать функциональные возможности ASP.NET AJAX и набора средств управления, `ScriptManager` элемент управления должен быть размещен на странице:</span><span class="sxs-lookup"><span data-stu-id="752f0-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

<span data-ttu-id="752f0-125">[![каждый Переупорядочение активирует обратную передачу](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="752f0-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="752f0-126">Каждый Переупорядочение активирует обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-postbacks-with-reorderlist-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="752f0-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="752f0-127">[Назад](drag-and-drop-via-reorderlist-cs.md)
> [Вперед](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="752f0-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
