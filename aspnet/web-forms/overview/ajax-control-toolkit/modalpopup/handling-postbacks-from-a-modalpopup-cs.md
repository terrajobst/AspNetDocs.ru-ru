---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: Обработка обратных передач из ModalPopup (C#) | Документация Майкрософт
author: wenz
description: Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. При торговом терминале необходимо уделить особое внимание.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599104"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a><span data-ttu-id="36d62-104">Обработка обратных передач из ModalPopup (C#)</span><span class="sxs-lookup"><span data-stu-id="36d62-104">Handling Postbacks from a ModalPopup (C#)</span></span>

<span data-ttu-id="36d62-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="36d62-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="36d62-106">[Скачать код](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="36d62-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span></span>

> <span data-ttu-id="36d62-107">Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="36d62-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="36d62-108">При создании обратной передачи во всплывающем окне необходимо соблюдать особое внимание.</span><span class="sxs-lookup"><span data-stu-id="36d62-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="36d62-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="36d62-109">Overview</span></span>

<span data-ttu-id="36d62-110">Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="36d62-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="36d62-111">При создании обратной передачи во всплывающем окне необходимо соблюдать особое внимание.</span><span class="sxs-lookup"><span data-stu-id="36d62-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="36d62-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="36d62-112">Steps</span></span>

<span data-ttu-id="36d62-113">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):</span><span class="sxs-lookup"><span data-stu-id="36d62-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="36d62-114">Затем добавьте панель, которая выступает в качестве модального всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="36d62-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="36d62-115">Здесь пользователь может ввести имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="36d62-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="36d62-116">Кнопка используется для закрытия всплывающего окна и сохранения данных.</span><span class="sxs-lookup"><span data-stu-id="36d62-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="36d62-117">Обратите внимание, что атрибут `OnClick` задан таким образом, что при нажатии на эту кнопку происходит обратная передача:</span><span class="sxs-lookup"><span data-stu-id="36d62-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="36d62-118">Сама страница состоит из двух меток для одних и тех же сведений: имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="36d62-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="36d62-119">Кнопка используется для запуска модального всплывающего окна:</span><span class="sxs-lookup"><span data-stu-id="36d62-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

<span data-ttu-id="36d62-120">Чтобы отобразить всплывающее окно, добавьте элемент управления `ModalPopupExtender`.</span><span class="sxs-lookup"><span data-stu-id="36d62-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="36d62-121">Задайте атрибуту `PopupControlID` идентификатор панели и `TargetControlID` ИДЕНТИФИКАТОРу кнопки:</span><span class="sxs-lookup"><span data-stu-id="36d62-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

<span data-ttu-id="36d62-122">Теперь при нажатии кнопки `Save` в модальном всплывающем окне выполняется метод `SaveData()` на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="36d62-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="36d62-123">Там можно сохранить введенные данные в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="36d62-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="36d62-124">В целях простоты новые данные просто выводятся в метке:</span><span class="sxs-lookup"><span data-stu-id="36d62-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

<span data-ttu-id="36d62-125">Кроме того, элементы управления TextBox в модальном всплывающем окне должны быть заполнены текущим именем и сообщением электронной почты.</span><span class="sxs-lookup"><span data-stu-id="36d62-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="36d62-126">Однако это необходимо только в том случае, если обратная передача не выполняется.</span><span class="sxs-lookup"><span data-stu-id="36d62-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="36d62-127">При наличии обратной передачи функция ViewState ASP.NET автоматически заполняет текстовые поля соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="36d62-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

<span data-ttu-id="36d62-128">[![модальное всплывающее окно вызывает обратную передачу](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="36d62-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="36d62-129">Модальное всплывающее окно вызывает обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="36d62-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="36d62-130">[Назад](using-modalpopup-with-a-repeater-control-cs.md)
> [Вперед](positioning-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="36d62-130">[Previous](using-modalpopup-with-a-repeater-control-cs.md)
[Next](positioning-a-modalpopup-cs.md)</span></span>
