---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: Борьба программы-роботы (C#) | Документация Майкрософт
author: wenz
description: Автоматическая программы-роботы Пластер блогов и другие веб-сайты с нежелательной почтой, Отправка форм комментариев без участия пользователя. Элемент управления Нобот в ASP.NET AJAX Con...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: fef55edf12a024e4dd66e2a18ea371ab4dac861f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606450"
---
# <a name="fighting-bots-c"></a><span data-ttu-id="90b9e-104">Борьба с ботами (C#)</span><span class="sxs-lookup"><span data-stu-id="90b9e-104">Fighting Bots (C#)</span></span>

<span data-ttu-id="90b9e-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="90b9e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="90b9e-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="90b9e-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span></span>

> <span data-ttu-id="90b9e-107">Автоматическая программы-роботы Пластер блогов и другие веб-сайты с нежелательной почтой, Отправка форм комментариев без участия пользователя.</span><span class="sxs-lookup"><span data-stu-id="90b9e-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="90b9e-108">Элемент управления Нобот в наборе средств управления AJAX ASP.NET может помочь в борьбе с этими программы-роботы.</span><span class="sxs-lookup"><span data-stu-id="90b9e-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="overview"></a><span data-ttu-id="90b9e-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="90b9e-109">Overview</span></span>

<span data-ttu-id="90b9e-110">Автоматическая программы-роботы Пластер блогов и другие веб-сайты с нежелательной почтой, Отправка форм комментариев без участия пользователя.</span><span class="sxs-lookup"><span data-stu-id="90b9e-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="90b9e-111">Элемент управления Нобот в наборе средств управления AJAX ASP.NET может помочь в борьбе с этими программы-роботы.</span><span class="sxs-lookup"><span data-stu-id="90b9e-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="90b9e-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="90b9e-112">Steps</span></span>

<span data-ttu-id="90b9e-113">Один из распространенных подходов к отказаться от программы-роботы — использовать Каптчас полностью автоматизированный открытый тест Turing для информирования компьютеров и людей друг от друга.</span><span class="sxs-lookup"><span data-stu-id="90b9e-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="90b9e-114">Тестирование Turing было первоначально протестировать, где нужно было решить, является ли партнер по соединению человеком или компьютером.</span><span class="sxs-lookup"><span data-stu-id="90b9e-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="90b9e-115">В Интернете CAPTCHA обычно состоит из изображения с искаженными буквами.</span><span class="sxs-lookup"><span data-stu-id="90b9e-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="90b9e-116">Идея состоит в том, что только человек может читать буквы на изображении, в то время как алгоритмы OCR завершатся ошибкой.</span><span class="sxs-lookup"><span data-stu-id="90b9e-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="90b9e-117">Этот подход имеет несколько преимуществ и недостатков, но его обсуждение выходит за рамки данного руководства.</span><span class="sxs-lookup"><span data-stu-id="90b9e-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="90b9e-118">Однако в наборе средств ASP.NET AJAX Control Toolkit есть элемент управления, обеспечивающий подобный подход: `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="90b9e-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="90b9e-119">Это проще преодолеть, чем CAPTCHA, но очень легко использовать и году на веб-сайтах, например в блогах, где они считаются успешными, если большинство нежелательных попыток нежелательной почты отменяются, что может сделать элемент управления `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="90b9e-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="90b9e-120">`NoBot` перехватывает обратную передачу текущей веб-формы ASP.NET при соблюдении хотя бы одного из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="90b9e-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="90b9e-121">Браузеру не удается решить головоломку JavaScript (например, при деактивации JavaScript)</span><span class="sxs-lookup"><span data-stu-id="90b9e-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="90b9e-122">Пользователь отправил форму на быструю</span><span class="sxs-lookup"><span data-stu-id="90b9e-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="90b9e-123">IP-адрес клиента передавал форму слишком часто в течение определенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="90b9e-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="90b9e-124">Чтобы проверить эти условия, элементу управления `NoBot` требуются эти атрибуты (все они являются необязательными):</span><span class="sxs-lookup"><span data-stu-id="90b9e-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="90b9e-125">`ResponseMinimumDelaySeconds` минимальное количество секунд между обратными передачами</span><span class="sxs-lookup"><span data-stu-id="90b9e-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="90b9e-126">`CutoffWindowSeconds` интервал времени, в течение которого обратная передача с одного IP-адреса является мерами</span><span class="sxs-lookup"><span data-stu-id="90b9e-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="90b9e-127">`CutoffMaximumInstances` максимальное количество секунд на интервал времени</span><span class="sxs-lookup"><span data-stu-id="90b9e-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="90b9e-128">Следующая разметка требует, чтобы по крайней мере две секунды пройдут между обратными передачами и что в течение 30-секундного интервала было только пять обратных передач или меньше.</span><span class="sxs-lookup"><span data-stu-id="90b9e-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

<span data-ttu-id="90b9e-129">Затем, как обычно, необходимо включить `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и воспользоваться набором элементов управления:</span><span class="sxs-lookup"><span data-stu-id="90b9e-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

<span data-ttu-id="90b9e-130">Так как большая часть проверок `NoBot` выполняется на стороне сервера, необходимо проверить результат таких проверок.</span><span class="sxs-lookup"><span data-stu-id="90b9e-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="90b9e-131">Это можно сделать, вызвав метод `IsValid()` метода `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="90b9e-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="90b9e-132">Он имеет один аргумент (в виде `out` параметра или`ByRef`), который имеет тип `NoBotState`.</span><span class="sxs-lookup"><span data-stu-id="90b9e-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="90b9e-133">Его строковое представление содержит причину сбоя проверки и `Valid` в противном случае.</span><span class="sxs-lookup"><span data-stu-id="90b9e-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="90b9e-134">Следующий код выводит сообщение в соответствии с результатом `NoBot`:</span><span class="sxs-lookup"><span data-stu-id="90b9e-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

<span data-ttu-id="90b9e-135">Наконец, необходимо отправить форму и элемент Label для вывода сообщения, и все готово.</span><span class="sxs-lookup"><span data-stu-id="90b9e-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

<span data-ttu-id="90b9e-136">При запуске этого скрипта и отключении JavaScript или отправке формы в течение первых двух секунд или при отправке формы семь раз в течение тридцати секунд появляется сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="90b9e-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="90b9e-137">Тем не менее следует использовать этот элемент управления в разумном объеме, поскольку активирован JavaScript только около 90-95% пользователей, поэтому 5-10% пользователей не сможет протестировать `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="90b9e-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>

<span data-ttu-id="90b9e-138">[![это сообщение об ошибке могло быть вызвано программой-роботом](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="90b9e-138">[![This error message could have been caused by a bot](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span></span>

<span data-ttu-id="90b9e-139">Это сообщение об ошибке могло быть вызвано программой-роботом ([щелкните, чтобы просмотреть изображение с полным размером](fighting-bots-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="90b9e-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="90b9e-140">Вперед</span><span class="sxs-lookup"><span data-stu-id="90b9e-140">Next</span></span>](fighting-bots-vb.md)
