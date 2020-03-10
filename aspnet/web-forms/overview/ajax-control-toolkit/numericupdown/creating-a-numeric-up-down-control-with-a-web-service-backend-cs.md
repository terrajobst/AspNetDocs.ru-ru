---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: Создание числового элемента управления "вверх/вниз" с помощью серверной части веб-службы (C#) | Документация Майкрософт
author: wenz
description: Вместо того, чтобы позволить пользователю вводить значение в флажок, числовой элемент управления "вверх/вниз" (который существует в Windows и других операционных системах) может доказать, что с...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 816a840b9e93b95a049c3a4cb792e9deeab28983
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509016"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="6f2ff-103">Создание числового поля со стрелками "вверх/вниз" с помощью серверной веб-службы (C#)</span><span class="sxs-lookup"><span data-stu-id="6f2ff-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>

<span data-ttu-id="6f2ff-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6f2ff-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6f2ff-105">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6f2ff-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="6f2ff-106">Вместо того, чтобы позволить пользователю вводить значение в флажок, числовой элемент управления "вверх/вниз" (который существует в Windows и других операционных системах) может оказаться более удобным.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="6f2ff-107">По умолчанию элемент управления NumericUpDown всегда увеличивает или уменьшает значение на 1, но веб-служба подтверждает большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="6f2ff-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="6f2ff-108">Overview</span></span>

<span data-ttu-id="6f2ff-109">Вместо того, чтобы позволить пользователю вводить значение в флажок, числовой элемент управления "вверх/вниз" (который существует в Windows и других операционных системах) может оказаться более удобным.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="6f2ff-110">По умолчанию элемент управления `NumericUpDown` всегда увеличивает или уменьшает значение на 1, но веб-служба подтверждает большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="6f2ff-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="6f2ff-111">Steps</span></span>

<span data-ttu-id="6f2ff-112">Набор средств ASP.NET AJAX Control Toolkit содержит расширитель `NumericUpDown`, который автоматически добавляет две кнопки в текстовое поле: одно для увеличения его значения, одно для его уменьшения.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="6f2ff-113">Однако элемент управления также поддерживает вызов веб-службы (или вызов метода страницы).</span><span class="sxs-lookup"><span data-stu-id="6f2ff-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="6f2ff-114">При нажатии кнопки вверх или вниз код JavaScript подключается к веб-серверу и выполняет метод.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="6f2ff-115">Сигнатура метода является следующей:</span><span class="sxs-lookup"><span data-stu-id="6f2ff-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="6f2ff-116">Аргумент `current` — это текущее значение в текстовом поле; атрибут `tag` — это дополнительные данные контекста, которые можно задать в качестве свойства расширителя `NumericUpDown` (но это необязательно).</span><span class="sxs-lookup"><span data-stu-id="6f2ff-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="6f2ff-117">В этом примере числовой элемент управления "вверх/вниз" должен допускать только те значения, которые являются степенями двух: 1, 2, 4, 8, 16, 32, 64 и т. д.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="6f2ff-118">Поэтому метод, выполняемый, когда пользователь хочет увеличить значение, должен удвоить старое значение. другой метод должен разделить значение на два.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="6f2ff-119">Вот полная веб-служба:</span><span class="sxs-lookup"><span data-stu-id="6f2ff-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="6f2ff-120">Наконец, создайте новую страницу ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="6f2ff-121">Обычно требуется элемент управления `ScriptManager`, `TextBox` и элемент управления `NumericUpDownExtender`.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="6f2ff-122">В последнем случае необходимо предоставить сведения о веб-службе:</span><span class="sxs-lookup"><span data-stu-id="6f2ff-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="6f2ff-123">`ServiceDownMethod`ное имя веб-метода или метода страницы</span><span class="sxs-lookup"><span data-stu-id="6f2ff-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="6f2ff-124">`ServiceDownPath` путь к веб-службе с помощью метода пониженной службы; пропускать при использовании метода страницы</span><span class="sxs-lookup"><span data-stu-id="6f2ff-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="6f2ff-125">`ServiceUpMethod` имя метода веб-метода или страницы</span><span class="sxs-lookup"><span data-stu-id="6f2ff-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="6f2ff-126">`ServiceUpPath` путь к веб-службе с помощью метода up Service; пропускать при использовании метода страницы</span><span class="sxs-lookup"><span data-stu-id="6f2ff-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="6f2ff-127">Ниже приведена полная разметка для страницы.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="6f2ff-128">При запуске страницы обратите внимание на то, как значение в текстовом поле всегда удваивается при нажатии кнопки вверху и при нажатии нижней кнопки уменьшается вдвое.</span><span class="sxs-lookup"><span data-stu-id="6f2ff-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>

<span data-ttu-id="6f2ff-129">[![отображаются только цифры, которые являются степенью 2](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f2ff-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span></span>

<span data-ttu-id="6f2ff-130">Отображаются только цифры, которые являются степенью 2 ([щелкните, чтобы просмотреть изображение с полным размером](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6f2ff-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6f2ff-131">Дальше</span><span class="sxs-lookup"><span data-stu-id="6f2ff-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
