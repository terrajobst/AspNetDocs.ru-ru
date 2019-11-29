---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: Запуск анимации с помощью кода на стороне клиента (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Выполнение анимации...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575482"
---
# <a name="executing-animations-using-client-side-code-vb"></a><span data-ttu-id="37088-104">Выполнение анимаций с помощью клиентского кода (VB)</span><span class="sxs-lookup"><span data-stu-id="37088-104">Executing Animations Using Client-Side Code (VB)</span></span>

<span data-ttu-id="37088-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="37088-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="37088-106">[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="37088-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span></span>

> <span data-ttu-id="37088-107">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="37088-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="37088-108">Выполнение анимации также может быть запущено с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="37088-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="37088-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="37088-109">Overview</span></span>

<span data-ttu-id="37088-110">Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="37088-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="37088-111">Выполнение анимации также может быть запущено с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="37088-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="37088-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="37088-112">Steps</span></span>

<span data-ttu-id="37088-113">Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.</span><span class="sxs-lookup"><span data-stu-id="37088-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="37088-114">Анимация будет применена к панели текста, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="37088-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="37088-115">В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:</span><span class="sxs-lookup"><span data-stu-id="37088-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="37088-116">Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:</span><span class="sxs-lookup"><span data-stu-id="37088-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="37088-117">В `<Animations>` узле используйте `<OnClick>` для запуска анимации после того, как пользователь щелкнет панель.</span><span class="sxs-lookup"><span data-stu-id="37088-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="37088-118">Добавьте две анимации для выполнения параллельно:</span><span class="sxs-lookup"><span data-stu-id="37088-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

<span data-ttu-id="37088-119">В целях демонстрации эта анимация (и любая другая анимация, созданная с помощью набора средств управления) выполняется с помощью кода JavaScript после выполнения страницы.</span><span class="sxs-lookup"><span data-stu-id="37088-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="37088-120">Прежде всего нам нужен доступ к элементу управления `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="37088-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="37088-121">Библиотека ASP.NET AJAX предоставляет функцию `$find()` для этой задачи:</span><span class="sxs-lookup"><span data-stu-id="37088-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

<span data-ttu-id="37088-122">Элемент управления `AnimationExtender` предоставляет богатый API, включая методы с именами, идентичными обработчикам событий, используемым в XML-разметке: `OnClick()`, `OnLoad()`и т. д.</span><span class="sxs-lookup"><span data-stu-id="37088-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="37088-123">Например, вызов метода `OnClick()` выполняет анимацию в элементе `<OnClick>` элемента управления `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="37088-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

<span data-ttu-id="37088-124">Ниже приведен полный код JavaScript на стороне клиента, который имитирует щелчок на панели после полной загрузки страницы. Обратите внимание, что используется имя `pageLoad()` функции, которое вызывается ASP.NET AJAX после загрузки страницы и всех включенных библиотек JavaScript.</span><span class="sxs-lookup"><span data-stu-id="37088-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

<span data-ttu-id="37088-125">[![анимация выполняется немедленно, без щелчка мышью](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="37088-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="37088-126">Анимация выполняется немедленно без щелчка мышью ([щелкните, чтобы просмотреть изображение с полным размером](executing-animations-using-client-side-code-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="37088-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="37088-127">[Назад](modifying-animations-from-the-server-side-vb.md)
> [Вперед](changing-an-animation-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="37088-127">[Previous](modifying-animations-from-the-server-side-vb.md)
[Next](changing-an-animation-using-client-side-code-vb.md)</span></span>
