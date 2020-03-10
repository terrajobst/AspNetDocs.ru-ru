---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: Использование автоматической обратной передачи с помощью CascadingDropDown (VB) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 5dea23a20aba00af5109f05f18365b89e409a131
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430662"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a><span data-ttu-id="82043-103">Использование автоматической обратной передачи с помощью CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="82043-103">Using Auto-Postback with CascadingDropDown (VB)</span></span>

<span data-ttu-id="82043-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="82043-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="82043-105">[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="82043-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span></span>

> <span data-ttu-id="82043-106">Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList.</span><span class="sxs-lookup"><span data-stu-id="82043-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="82043-107">Однако при использовании элемента управления CascadingDropDown, ASP. Функция автообратной передачи элемента управления DropDownList не работает, так как асинхронная загрузка данных в список создает обратную передачу (не нужно).</span><span class="sxs-lookup"><span data-stu-id="82043-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="82043-108">Этот результат можно избежать с помощью кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="82043-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="82043-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="82043-109">Overview</span></span>

<span data-ttu-id="82043-110">Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList.</span><span class="sxs-lookup"><span data-stu-id="82043-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="82043-111">(Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Однако при использовании элемента управления CascadingDropDown, ASP. Функция автообратной передачи элемента управления DropDownList не работает, так как асинхронная загрузка данных в список создает обратную передачу (не нужно).</span><span class="sxs-lookup"><span data-stu-id="82043-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="82043-112">Этот результат можно избежать с помощью кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="82043-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="82043-113">Шаги</span><span class="sxs-lookup"><span data-stu-id="82043-113">Steps</span></span>

<span data-ttu-id="82043-114">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но внутри &lt;`form`&gt;):</span><span class="sxs-lookup"><span data-stu-id="82043-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="82043-115">Затем требуется элемент управления DropDownList:</span><span class="sxs-lookup"><span data-stu-id="82043-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="82043-116">Для этого списка добавляется расширитель CascadingDropDown, предоставляющий URL-адрес и сведения о методе:</span><span class="sxs-lookup"><span data-stu-id="82043-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="82043-117">Затем расширитель CascadingDropDown асинхронно вызывает веб-службу со следующей сигнатурой метода:</span><span class="sxs-lookup"><span data-stu-id="82043-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="82043-118">Метод возвращает массив типа CascadingDropDown value.</span><span class="sxs-lookup"><span data-stu-id="82043-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="82043-119">Конструктор типа сначала ждет заголовок записи списка, а затем значение (атрибут HTML `value`).</span><span class="sxs-lookup"><span data-stu-id="82043-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="82043-120">Загрузка страницы в браузере приведет к заполнению раскрывающегося списка тремя поставщиками, второй из которых выбран заранее.</span><span class="sxs-lookup"><span data-stu-id="82043-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="82043-121">Кроме того, ASP.NET определяет метод `__doPostBack()` JavaScript.</span><span class="sxs-lookup"><span data-stu-id="82043-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="82043-122">После загрузки страницы этот вызов JavaScript добавляется в раскрывающийся список, но только в том случае, если в нем есть элементы.</span><span class="sxs-lookup"><span data-stu-id="82043-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="82043-123">Если в списке нет элементов, набор элементов управления в данный момент загружает их, поэтому код JavaScript использует время ожидания и пытается повторить попытку в течение половины секунды.</span><span class="sxs-lookup"><span data-stu-id="82043-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

<span data-ttu-id="82043-124">Таким образом, обратная передача выполняется только в том случае, если в списке есть элементы, и пользователь выбирает запись.</span><span class="sxs-lookup"><span data-stu-id="82043-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="82043-125">[![выборе элемента списка вызывает обратную передачу](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="82043-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="82043-126">Выбор элемента списка вызывает обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="82043-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="82043-127">Назад</span><span class="sxs-lookup"><span data-stu-id="82043-127">Previous</span></span>](presetting-list-entries-with-cascadingdropdown-vb.md)
