---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: Изменение анимации со стороны сервера (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации также могут быть...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483870"
---
# <a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="add89-104">Изменение анимации со стороны сервера (VB)</span><span class="sxs-lookup"><span data-stu-id="add89-104">Modifying Animations From The Server Side (VB)</span></span>

<span data-ttu-id="add89-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="add89-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="add89-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="add89-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="add89-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="add89-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="add89-108">Анимации также можно изменить на стороне сервера</span><span class="sxs-lookup"><span data-stu-id="add89-108">The animations may also be changed on the server-side</span></span>

## <a name="overview"></a><span data-ttu-id="add89-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="add89-109">Overview</span></span>

<span data-ttu-id="add89-110">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="add89-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="add89-111">Анимации также можно изменить на стороне сервера</span><span class="sxs-lookup"><span data-stu-id="add89-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="add89-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="add89-112">Steps</span></span>

<span data-ttu-id="add89-113">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="add89-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="add89-114">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="add89-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="add89-115">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="add89-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="add89-116">Остальная часть кода выполняется на стороне сервера и не использует разметку; Вместо этого он использует код для создания элемента управления `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="add89-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="add89-117">Однако набор элементов управления в настоящее время не предоставляет доступ к API для создания отдельных анимаций.</span><span class="sxs-lookup"><span data-stu-id="add89-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="add89-118">Однако можно задать для свойства анимации `AnimationExtender`строку, содержащую XML-разметку, используемую при декларативном назначении анимации.</span><span class="sxs-lookup"><span data-stu-id="add89-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="add89-119">Чтобы создать XML-файл, который не должен содержать элемент `<Animations>` можно использовать поддержку XML .NET Framework или, как показано в следующем коде, просто укажите строку:</span><span class="sxs-lookup"><span data-stu-id="add89-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="add89-120">Наконец, добавьте элемент управления `AnimationExtender` на текущую страницу в элементе `<form runat="server">`, убедившись, что анимация включена и выполняется:</span><span class="sxs-lookup"><span data-stu-id="add89-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

<span data-ttu-id="add89-121">[![анимация создается с помощью кода/VB на стороне C#сервера](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="add89-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="add89-122">Анимация создается с помощью кода/VB на стороне C#сервера ([щелкните, чтобы просмотреть изображение с полным размером](modifying-animations-from-the-server-side-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="add89-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="add89-123">[Назад](triggering-an-animation-in-another-control-vb.md)
> [Вперед](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="add89-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
