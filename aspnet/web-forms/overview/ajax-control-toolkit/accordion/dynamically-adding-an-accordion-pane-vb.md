---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: Динамическое добавление панели «гармошка» (VB) | Документация Майкрософт
author: wenz
description: Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: be48db5ea3de4af46b0f864cc9e73d2f518294a4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607212"
---
# <a name="dynamically-adding-an-accordion-pane-vb"></a><span data-ttu-id="6088f-104">Динамическое добавление панели «гармошка» (VB)</span><span class="sxs-lookup"><span data-stu-id="6088f-104">Dynamically Adding An Accordion Pane (VB)</span></span>

<span data-ttu-id="6088f-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6088f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6088f-106">[Скачать код](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="6088f-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span></span>

> <span data-ttu-id="6088f-107">Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз.</span><span class="sxs-lookup"><span data-stu-id="6088f-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="6088f-108">Панели обычно объявляются внутри самой страницы, но для достижения того же результата можно использовать код на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="6088f-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="6088f-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="6088f-109">Overview</span></span>

<span data-ttu-id="6088f-110">Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз.</span><span class="sxs-lookup"><span data-stu-id="6088f-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="6088f-111">Панели обычно объявляются внутри самой страницы, но для достижения того же результата можно использовать код на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="6088f-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="6088f-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="6088f-112">Steps</span></span>

<span data-ttu-id="6088f-113">Элемент управления "гармошка" предоставляет все важные свойства коду на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="6088f-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="6088f-114">Помимо прочего, свойство `Panes` предоставляет доступ к коллекции панелей, составляющих гармошка.</span><span class="sxs-lookup"><span data-stu-id="6088f-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="6088f-115">Каждая панель имеет тип `AccordionPane`.</span><span class="sxs-lookup"><span data-stu-id="6088f-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="6088f-116">Таким образом, упрощена создание такой области:</span><span class="sxs-lookup"><span data-stu-id="6088f-116">It is therefore trivial to create such a pane:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

<span data-ttu-id="6088f-117">Свойство `HeaderContainer` `AccordionPane` предоставляет доступ к элементам управления ASP.NET в разделе заголовка панели. Свойство `ContentContainer` `AccordionPane` выполняет то же самое для раздела содержимого панели.</span><span class="sxs-lookup"><span data-stu-id="6088f-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="6088f-118">Это позволяет ASP.NET коду добавлять содержимое на панели:</span><span class="sxs-lookup"><span data-stu-id="6088f-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

<span data-ttu-id="6088f-119">Наконец, необходимо добавить панели в `Panes` коллекцию элементов:</span><span class="sxs-lookup"><span data-stu-id="6088f-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

<span data-ttu-id="6088f-120">Ниже приведен полный код на стороне сервера, который добавляет две панели в элемент управления "гармошка":</span><span class="sxs-lookup"><span data-stu-id="6088f-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

<span data-ttu-id="6088f-121">Единственным отсутствующим элементом является сам объект, который зависит от наличия элемента управления `ScriptManager` ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="6088f-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

<span data-ttu-id="6088f-122">Чтобы завершить этот пример, два класса CSS, упоминаемые в элементе управления "гармошка", предоставляют сведения о стиле для браузера:</span><span class="sxs-lookup"><span data-stu-id="6088f-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]

<span data-ttu-id="6088f-123">[![данные в элементе "гармошка" были динамически добавлены с помощью кода на стороне сервера](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6088f-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span></span>

<span data-ttu-id="6088f-124">Данные в элементе "гармошка" были динамически добавлены кодом на стороне сервера ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-adding-an-accordion-pane-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="6088f-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6088f-125">Назад</span><span class="sxs-lookup"><span data-stu-id="6088f-125">Previous</span></span>](databinding-to-an-accordion-vb.md)
