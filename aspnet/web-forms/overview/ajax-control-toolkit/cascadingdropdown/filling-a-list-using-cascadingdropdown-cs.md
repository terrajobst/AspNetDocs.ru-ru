---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: Заполнение списка с помощью CascadingDropDownC#() | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574838"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="8905a-103">Заполнение списка с помощью CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="8905a-103">Filling a List Using CascadingDropDown (C#)</span></span>

<span data-ttu-id="8905a-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8905a-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8905a-105">[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8905a-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="8905a-106">Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList.</span><span class="sxs-lookup"><span data-stu-id="8905a-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="8905a-107">(Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Первая проблема, которую необходимо решить, заключается в том, чтобы заполнить раскрывающийся список с помощью этого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="8905a-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="8905a-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="8905a-108">Overview</span></span>

<span data-ttu-id="8905a-109">Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList.</span><span class="sxs-lookup"><span data-stu-id="8905a-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="8905a-110">(Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Первая проблема, которую необходимо решить, заключается в том, чтобы заполнить раскрывающийся список с помощью этого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="8905a-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="8905a-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="8905a-111">Steps</span></span>

<span data-ttu-id="8905a-112">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):</span><span class="sxs-lookup"><span data-stu-id="8905a-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="8905a-113">Затем требуется элемент управления DropDownList:</span><span class="sxs-lookup"><span data-stu-id="8905a-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="8905a-114">Для этого списка добавляется расширитель CascadingDropDown.</span><span class="sxs-lookup"><span data-stu-id="8905a-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="8905a-115">Он отправляет асинхронный запрос к веб-службе, который затем возвращает список записей, которые будут отображены в списке.</span><span class="sxs-lookup"><span data-stu-id="8905a-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="8905a-116">Чтобы это работало, необходимо задать следующие атрибуты CascadingDropDown:</span><span class="sxs-lookup"><span data-stu-id="8905a-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="8905a-117">`ServicePath`: URL веб-службы, которая доставляет записи списка</span><span class="sxs-lookup"><span data-stu-id="8905a-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="8905a-118">`ServiceMethod`: веб-метод, поставляющий записи списка</span><span class="sxs-lookup"><span data-stu-id="8905a-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="8905a-119">`TargetControlID`: Идентификатор раскрывающегося списка</span><span class="sxs-lookup"><span data-stu-id="8905a-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="8905a-120">`Category`: сведения о категории, которые передаются в веб-метод при вызове</span><span class="sxs-lookup"><span data-stu-id="8905a-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="8905a-121">`PromptText`: текст, отображаемый при асинхронной загрузке данных списка с сервера</span><span class="sxs-lookup"><span data-stu-id="8905a-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="8905a-122">Ниже приведена разметка для элемента `CascadingDropDown`.</span><span class="sxs-lookup"><span data-stu-id="8905a-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="8905a-123">Единственное различие между C# и VB — имя связанной веб-службы:</span><span class="sxs-lookup"><span data-stu-id="8905a-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="8905a-124">Код JavaScript, поступающий из расширителя `CascadingDropDown`, вызывает метод веб-службы со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="8905a-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="8905a-125">Поэтому важным аспектом является то, что метод должен возвращать массив типа `CascadingDropDownNameValue` (определяемый набором средств управления AJAX ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="8905a-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="8905a-126">В конструкторе `CascadingDropDownNameValue` сначала необходимо указать текст записи списка, а затем его значение, как `<option value="VALUE">NAME</option>` бы в HTML.</span><span class="sxs-lookup"><span data-stu-id="8905a-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="8905a-127">Ниже приведено несколько примеров данных.</span><span class="sxs-lookup"><span data-stu-id="8905a-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="8905a-128">При загрузке страницы в браузере список будет заполнен тремя поставщиками.</span><span class="sxs-lookup"><span data-stu-id="8905a-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="8905a-129">[![список заполняется автоматически](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8905a-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="8905a-130">Список заполняется автоматически ([щелкните, чтобы просмотреть изображение с полным размером](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="8905a-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8905a-131">Вперед</span><span class="sxs-lookup"><span data-stu-id="8905a-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
