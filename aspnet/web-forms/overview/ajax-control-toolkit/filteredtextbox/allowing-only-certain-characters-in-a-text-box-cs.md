---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: Разрешение только некоторых символов в текстовом поле (C#) | Документация Майкрософт
author: wenz
description: Элементы управления проверки ASP.NET могут гарантировать, что вводимые пользователем данные допускаются только в определенных символах. Однако это по-прежнему не мешает пользователям вводить недопустимые...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: d1e367becd574e31d24fca8545f76b1ed3c4d85e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446358"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a><span data-ttu-id="47268-104">Разрешение только некоторых символов в текстовом поле (C#)</span><span class="sxs-lookup"><span data-stu-id="47268-104">Allowing Only Certain Characters in a Text Box (C#)</span></span>

<span data-ttu-id="47268-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="47268-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="47268-106">[Скачать код](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="47268-106">[Download Code](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span></span>

> <span data-ttu-id="47268-107">Элементы управления проверки ASP.NET могут гарантировать, что вводимые пользователем данные допускаются только в определенных символах.</span><span class="sxs-lookup"><span data-stu-id="47268-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="47268-108">Однако это по-прежнему не мешает пользователям вводить недопустимые символы и пытаться отправить форму.</span><span class="sxs-lookup"><span data-stu-id="47268-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="47268-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="47268-109">Overview</span></span>

<span data-ttu-id="47268-110">Элементы управления проверки ASP.NET могут гарантировать, что вводимые пользователем данные допускаются только в определенных символах.</span><span class="sxs-lookup"><span data-stu-id="47268-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="47268-111">Однако это по-прежнему не мешает пользователям вводить недопустимые символы и пытаться отправить форму.</span><span class="sxs-lookup"><span data-stu-id="47268-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="47268-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="47268-112">Steps</span></span>

<span data-ttu-id="47268-113">Набор средств ASP.NET AJAX Control Toolkit содержит элемент управления `FilteredTextBox`, расширяющий текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="47268-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="47268-114">После активации в поле может быть вставлен только определенный набор символов.</span><span class="sxs-lookup"><span data-stu-id="47268-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="47268-115">Чтобы это работало, сначала необходимо использовать ASP.NET AJAX `ScriptManager`, который загружает библиотеки JavaScript, которые также используются набором средств управления AJAX ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="47268-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

<span data-ttu-id="47268-116">Затем нам нужно текстовое поле:</span><span class="sxs-lookup"><span data-stu-id="47268-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

<span data-ttu-id="47268-117">Наконец, элемент управления `FilteredTextBoxExtender` позаботится об ограничении символов, которые разрешено вводить пользователю.</span><span class="sxs-lookup"><span data-stu-id="47268-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="47268-118">Сначала присвойте атрибуту `TargetControlID` `ID` элемента управления `TextBox`.</span><span class="sxs-lookup"><span data-stu-id="47268-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="47268-119">Затем выберите одно из доступных значений `FilterType`:</span><span class="sxs-lookup"><span data-stu-id="47268-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="47268-120">`Custom` по умолчанию; необходимо предоставить список допустимых символов</span><span class="sxs-lookup"><span data-stu-id="47268-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="47268-121">`LowercaseLetters` только строчные буквы</span><span class="sxs-lookup"><span data-stu-id="47268-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="47268-122">`Numbers` только цифры</span><span class="sxs-lookup"><span data-stu-id="47268-122">`Numbers` digits only</span></span>
- <span data-ttu-id="47268-123">`UppercaseLetters` только прописные буквы</span><span class="sxs-lookup"><span data-stu-id="47268-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="47268-124">Если используется `Custom FilterType`, необходимо задать свойство `ValidChars` и предоставить список символов, которые могут быть введены.</span><span class="sxs-lookup"><span data-stu-id="47268-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="47268-125">Кстати: при попытке вставить текст в текстовое поле удаляются все недопустимые символы.</span><span class="sxs-lookup"><span data-stu-id="47268-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="47268-126">Ниже приведена разметка для элемента управления `FilteredTextBoxExtender`, которая допускает только цифры (что также было бы возможно с `FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="47268-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

<span data-ttu-id="47268-127">Запустите страницу и попытайтесь ввести букву, если JavaScript включен, он не будет работать. Однако на странице цифры отображаются.</span><span class="sxs-lookup"><span data-stu-id="47268-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="47268-128">Однако обратите внимание, что `FilteredTextBox` защиты не является маркированным: Если включен JavaScript, любые данные могут быть введены в текстовое поле, поэтому необходимо использовать дополнительные средства проверки, например ASP. Элементы управления проверки NET.</span><span class="sxs-lookup"><span data-stu-id="47268-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="47268-129">[![могут быть указаны только цифры](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="47268-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span></span>

<span data-ttu-id="47268-130">Можно указать только цифры ([щелкните, чтобы просмотреть изображение с полным размером](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="47268-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="47268-131">Дальше</span><span class="sxs-lookup"><span data-stu-id="47268-131">Next</span></span>](allowing-only-certain-characters-in-a-text-box-vb.md)
