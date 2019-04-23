---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: Заполнение списка с помощью CascadingDropDown (VB) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 663dfc76dc3d07dbe9ddca002dc07cb3f9acdb1c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59419344"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="7695b-103">Заполнение списка с помощью CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="7695b-103">Filling a List Using CascadingDropDown (VB)</span></span>

<span data-ttu-id="7695b-104">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7695b-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7695b-105">[Скачать код](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7695b-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="7695b-106">Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в другой DropDownList.</span><span class="sxs-lookup"><span data-stu-id="7695b-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="7695b-107">(К примеру, один список содержит список штатов США, и следующий список заполняется крупнейших городов в этом состоянии.) Первая трудность заключается для решения — фактически заполнение раскрывающегося списка, с помощью этого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="7695b-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>


## <a name="overview"></a><span data-ttu-id="7695b-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="7695b-108">Overview</span></span>

<span data-ttu-id="7695b-109">Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в другой DropDownList.</span><span class="sxs-lookup"><span data-stu-id="7695b-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="7695b-110">(К примеру, один список содержит список штатов США, и следующий список заполняется крупнейших городов в этом состоянии.) Первая трудность заключается для решения — фактически заполнение раскрывающегося списка, с помощью этого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="7695b-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="7695b-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="7695b-111">Steps</span></span>

<span data-ttu-id="7695b-112">Для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления необходимо поместить в любом месте на странице (но в `<form>` элемента):</span><span class="sxs-lookup"><span data-stu-id="7695b-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="7695b-113">Затем необходим элемент управления DropDownList:</span><span class="sxs-lookup"><span data-stu-id="7695b-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="7695b-114">Для этого списка расширитель CascadingDropDown добавляется.</span><span class="sxs-lookup"><span data-stu-id="7695b-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="7695b-115">Он отправит асинхронный запрос к веб-службу, которая будет возвращать список записей для отображения в списке.</span><span class="sxs-lookup"><span data-stu-id="7695b-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="7695b-116">Чтобы это работало должны быть заданы следующие атрибуты CascadingDropDown:</span><span class="sxs-lookup"><span data-stu-id="7695b-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="7695b-117">`ServicePath`: URL-адрес веб-службы, предоставляя элементов списка</span><span class="sxs-lookup"><span data-stu-id="7695b-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="7695b-118">`ServiceMethod`: Веб-метода доставки элементов списка</span><span class="sxs-lookup"><span data-stu-id="7695b-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="7695b-119">`TargetControlID`: Идентификатор списка, раскрывающегося списка</span><span class="sxs-lookup"><span data-stu-id="7695b-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="7695b-120">`Category`: Сведения о категории, которая отправляется при вызове метода веб-</span><span class="sxs-lookup"><span data-stu-id="7695b-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="7695b-121">`PromptText`: Текст, отображаемый при асинхронной загрузкой данных с сервера</span><span class="sxs-lookup"><span data-stu-id="7695b-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="7695b-122">Далее приведена разметка для `CascadingDropDown` элемент.</span><span class="sxs-lookup"><span data-stu-id="7695b-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="7695b-123">Единственное различие между C# и VB — имя связанного веб-службы:</span><span class="sxs-lookup"><span data-stu-id="7695b-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="7695b-124">Код JavaScript, поступающие от `CascadingDropDown` расширения вызывает метод веб-службы со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="7695b-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="7695b-125">Это важный аспект, метод должен возвращать массив объектов типа `CascadingDropDownNameValue` (определяется по ASP.NET AJAX Control Toolkit).</span><span class="sxs-lookup"><span data-stu-id="7695b-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="7695b-126">В `CascadingDropDownNameValue` конструктор, первый текстовый элемент списка, а затем его значение должно быть указано, так же, как `<option value="VALUE">NAME</option>` в HTML.</span><span class="sxs-lookup"><span data-stu-id="7695b-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="7695b-127">Вот некоторые примеры данных:</span><span class="sxs-lookup"><span data-stu-id="7695b-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="7695b-128">Загрузку страницы в браузере будет активировать списка, чтобы заполнить трех поставщиков.</span><span class="sxs-lookup"><span data-stu-id="7695b-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>


<span data-ttu-id="7695b-129">[![Список заполняется автоматически](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7695b-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="7695b-130">Список заполняется автоматически ([Просмотр полноразмерного изображения](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7695b-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7695b-131">[Назад](using-auto-postback-with-cascadingdropdown-cs.md)
> [Вперед](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7695b-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
