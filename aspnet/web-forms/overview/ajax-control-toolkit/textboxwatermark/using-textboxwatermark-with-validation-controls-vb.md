---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: Использование элемента управления textboxwatermark с элементами управления проверки (VB) | Документация Майкрософт
author: wenz
description: Элемент управления элемента управления textboxwatermark в наборе средств AJAX Control Toolkit расширяет текстовое поле, чтобы текст отображался в поле. Когда пользователь щелкает в поле, он...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 141cae26c9e52be510e2a5a8f816cbac977dcf3d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597241"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a><span data-ttu-id="01b76-104">Использование элемента управления TextBoxWatermark с проверяющими элементами управления (VB)</span><span class="sxs-lookup"><span data-stu-id="01b76-104">Using TextBoxWatermark With Validation Controls (VB)</span></span>

<span data-ttu-id="01b76-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="01b76-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="01b76-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="01b76-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span></span>

> <span data-ttu-id="01b76-107">Элемент управления элемента управления textboxwatermark в наборе средств AJAX Control Toolkit расширяет текстовое поле, чтобы текст отображался в поле.</span><span class="sxs-lookup"><span data-stu-id="01b76-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="01b76-108">Когда пользователь щелкает в поле, он очищается.</span><span class="sxs-lookup"><span data-stu-id="01b76-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="01b76-109">Если пользователь оставляет поле без ввода текста, заполняется предварительно заполненный текст.</span><span class="sxs-lookup"><span data-stu-id="01b76-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="01b76-110">Это может конфликтовать с элементами управления проверки ASP.NET на той же странице, но эти проблемы можно преодолеть.</span><span class="sxs-lookup"><span data-stu-id="01b76-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="overview"></a><span data-ttu-id="01b76-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="01b76-111">Overview</span></span>

<span data-ttu-id="01b76-112">Элемент управления `TextBoxWatermark` в наборе средств AJAX Control Toolkit расширяет текстовое поле, позволяя отображать текст в поле.</span><span class="sxs-lookup"><span data-stu-id="01b76-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="01b76-113">Когда пользователь щелкает в поле, он очищается.</span><span class="sxs-lookup"><span data-stu-id="01b76-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="01b76-114">Если пользователь оставляет поле без ввода текста, заполняется предварительно заполненный текст.</span><span class="sxs-lookup"><span data-stu-id="01b76-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="01b76-115">Это может конфликтовать с элементами управления проверки ASP.NET на той же странице, но эти проблемы можно преодолеть.</span><span class="sxs-lookup"><span data-stu-id="01b76-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="01b76-116">Шаги</span><span class="sxs-lookup"><span data-stu-id="01b76-116">Steps</span></span>

<span data-ttu-id="01b76-117">Базовая настройка образца состоит из следующих элементов: элемент управления `TextBox` с водяным знаком с помощью элемента управления `TextBoxWatermarkExtender`.</span><span class="sxs-lookup"><span data-stu-id="01b76-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="01b76-118">Кнопка активирует обратную передачу и затем будет использоваться для активации элементов управления проверки на странице.</span><span class="sxs-lookup"><span data-stu-id="01b76-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="01b76-119">Кроме того, для инициализации ASP.NET AJAX требуется элемент управления `ScriptManager`:</span><span class="sxs-lookup"><span data-stu-id="01b76-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="01b76-120">Теперь добавьте элемент управления `RequiredFieldValidator`, который проверяет, есть ли в поле текст при отправке формы.</span><span class="sxs-lookup"><span data-stu-id="01b76-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="01b76-121">Свойству `InitialValue` проверяющего элемента управления должно быть присвоено то же значение, которое используется в `TextBoxWatermarkExtender`ном элементе. при отправке формы значение неизмененного текстового поля — это значение водяного знака в нем:</span><span class="sxs-lookup"><span data-stu-id="01b76-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="01b76-122">Однако существует одна проблема, связанная с этим подходом: Если клиент отключает JavaScript, текстовое поле не заполняется текстом водяного знака, поэтому `RequiredFieldValidator` не запускает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="01b76-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="01b76-123">Поэтому требуется второй элемент управления `RequiredFieldValidator`, проверяющий наличие пустого текстового поля (без атрибута `InitialValue`).</span><span class="sxs-lookup"><span data-stu-id="01b76-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="01b76-124">Поскольку оба проверяющего элемента управления используют `Display`=`"Dynamic"`, конечный пользователь не может отличить внешний вид, в котором были запущены два проверяющих элемента управления. Вместо этого он выглядит как есть только один из них.</span><span class="sxs-lookup"><span data-stu-id="01b76-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="01b76-125">Наконец, добавьте некоторый серверный код для вывода текста в поле, если средство проверки не выдавало сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="01b76-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="01b76-126">[![проверяющей элемент управления сообщает, что в поле нет текста](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="01b76-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="01b76-127">Проверяющий элемент управления сообщает, что в поле нет текста ([щелкните, чтобы просмотреть изображение с полным размером](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="01b76-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="01b76-128">Назад</span><span class="sxs-lookup"><span data-stu-id="01b76-128">Previous</span></span>](using-textboxwatermark-in-a-formview-vb.md)
