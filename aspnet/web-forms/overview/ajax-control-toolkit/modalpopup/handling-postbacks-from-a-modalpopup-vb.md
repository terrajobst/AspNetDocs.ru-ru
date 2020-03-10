---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: Обработка обратных передач из ModalPopup (VB) | Документация Майкрософт
author: wenz
description: Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. При торговом терминале необходимо уделить особое внимание.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: df0b71b3e336a0d230869623473bdac24b3dd07b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504024"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a><span data-ttu-id="e8799-104">Обработка обратных передач из ModalPopup (VB)</span><span class="sxs-lookup"><span data-stu-id="e8799-104">Handling Postbacks from a ModalPopup (VB)</span></span>

<span data-ttu-id="e8799-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e8799-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e8799-106">[Скачать код](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e8799-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span></span>

> <span data-ttu-id="e8799-107">Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="e8799-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="e8799-108">При создании обратной передачи во всплывающем окне необходимо соблюдать особое внимание.</span><span class="sxs-lookup"><span data-stu-id="e8799-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="e8799-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="e8799-109">Overview</span></span>

<span data-ttu-id="e8799-110">Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="e8799-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="e8799-111">При создании обратной передачи во всплывающем окне необходимо соблюдать особое внимание.</span><span class="sxs-lookup"><span data-stu-id="e8799-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="e8799-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="e8799-112">Steps</span></span>

<span data-ttu-id="e8799-113">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):</span><span class="sxs-lookup"><span data-stu-id="e8799-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="e8799-114">Затем добавьте панель, которая выступает в качестве модального всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="e8799-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="e8799-115">Здесь пользователь может ввести имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="e8799-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="e8799-116">Кнопка используется для закрытия всплывающего окна и сохранения данных.</span><span class="sxs-lookup"><span data-stu-id="e8799-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="e8799-117">Обратите внимание, что атрибут `OnClick` задан таким образом, что при нажатии на эту кнопку происходит обратная передача:</span><span class="sxs-lookup"><span data-stu-id="e8799-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="e8799-118">Сама страница состоит из двух меток для одних и тех же сведений: имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="e8799-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="e8799-119">Кнопка используется для запуска модального всплывающего окна:</span><span class="sxs-lookup"><span data-stu-id="e8799-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

<span data-ttu-id="e8799-120">Чтобы отобразить всплывающее окно, добавьте элемент управления `ModalPopupExtender`.</span><span class="sxs-lookup"><span data-stu-id="e8799-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="e8799-121">Задайте атрибуту `PopupControlID` идентификатор панели и `TargetControlID` ИДЕНТИФИКАТОРу кнопки:</span><span class="sxs-lookup"><span data-stu-id="e8799-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

<span data-ttu-id="e8799-122">Теперь при нажатии кнопки `Save` в модальном всплывающем окне выполняется метод `SaveData()` на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="e8799-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="e8799-123">Там можно сохранить введенные данные в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="e8799-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="e8799-124">В целях простоты новые данные просто выводятся в метке:</span><span class="sxs-lookup"><span data-stu-id="e8799-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

<span data-ttu-id="e8799-125">Кроме того, элементы управления TextBox в модальном всплывающем окне должны быть заполнены текущим именем и сообщением электронной почты.</span><span class="sxs-lookup"><span data-stu-id="e8799-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="e8799-126">Однако это необходимо только в том случае, если обратная передача не выполняется.</span><span class="sxs-lookup"><span data-stu-id="e8799-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="e8799-127">При наличии обратной передачи функция ViewState ASP.NET автоматически заполняет текстовые поля соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="e8799-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

<span data-ttu-id="e8799-128">[![модальное всплывающее окно вызывает обратную передачу](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e8799-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="e8799-129">Модальное всплывающее окно вызывает обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e8799-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e8799-130">[Назад](using-modalpopup-with-a-repeater-control-vb.md)
> [Вперед](positioning-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e8799-130">[Previous](using-modalpopup-with-a-repeater-control-vb.md)
[Next](positioning-a-modalpopup-vb.md)</span></span>
