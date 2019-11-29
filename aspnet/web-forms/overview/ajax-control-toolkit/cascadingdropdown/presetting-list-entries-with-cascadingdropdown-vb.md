---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: Предустановка записей списка с помощью CascadingDropDown (VB) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599547"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a><span data-ttu-id="b5876-103">Предустановка записей списка с помощью CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="b5876-103">Presetting List Entries with CascadingDropDown (VB)</span></span>

<span data-ttu-id="b5876-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b5876-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b5876-105">[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b5876-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span></span>

> <span data-ttu-id="b5876-106">Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList.</span><span class="sxs-lookup"><span data-stu-id="b5876-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="b5876-107">Небольшое количество кода может быть предвыбрано после динамической загрузки данных в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="b5876-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="overview"></a><span data-ttu-id="b5876-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="b5876-108">Overview</span></span>

<span data-ttu-id="b5876-109">Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList.</span><span class="sxs-lookup"><span data-stu-id="b5876-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="b5876-110">(Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Небольшое количество кода может быть предвыбрано после динамической загрузки данных в элемент списка.</span><span class="sxs-lookup"><span data-stu-id="b5876-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="b5876-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="b5876-111">Steps</span></span>

<span data-ttu-id="b5876-112">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):</span><span class="sxs-lookup"><span data-stu-id="b5876-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="b5876-113">Затем требуется элемент управления DropDownList:</span><span class="sxs-lookup"><span data-stu-id="b5876-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="b5876-114">Для этого списка добавляется расширитель CascadingDropDown, предоставляющий URL-адрес и сведения о методе:</span><span class="sxs-lookup"><span data-stu-id="b5876-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="b5876-115">Затем расширитель CascadingDropDown асинхронно вызывает веб-службу со следующей сигнатурой метода:</span><span class="sxs-lookup"><span data-stu-id="b5876-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="b5876-116">Метод возвращает массив типа CascadingDropDown value.</span><span class="sxs-lookup"><span data-stu-id="b5876-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="b5876-117">Конструктор типа сначала ждет заголовок записи списка, а затем значение (атрибут HTML `value`).</span><span class="sxs-lookup"><span data-stu-id="b5876-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="b5876-118">Если для третьего аргумента задано значение true, элемент списка автоматически выбирается в браузере.</span><span class="sxs-lookup"><span data-stu-id="b5876-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="b5876-119">Загрузка страницы в браузере приведет к заполнению раскрывающегося списка тремя поставщиками, второй из которых выбран заранее.</span><span class="sxs-lookup"><span data-stu-id="b5876-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>

<span data-ttu-id="b5876-120">[![список заполнен и выбран автоматически](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b5876-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="b5876-121">Список заполняется и выбирается автоматически ([щелкните, чтобы просмотреть изображение с полным размером](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="b5876-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b5876-122">[Назад](using-cascadingdropdown-with-a-database-vb.md)
> [Вперед](using-auto-postback-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b5876-122">[Previous](using-cascadingdropdown-with-a-database-vb.md)
[Next](using-auto-postback-with-cascadingdropdown-vb.md)</span></span>
