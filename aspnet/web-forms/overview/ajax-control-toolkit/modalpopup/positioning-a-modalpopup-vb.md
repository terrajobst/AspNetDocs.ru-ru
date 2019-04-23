---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: Размещение ModalPopup (VB) | Документация Майкрософт
author: wenz
description: Элемент управления ModalPopup в AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью средств на стороне клиента. Тем не менее не предлагает элемент управления...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: e37d2f4450c697f963d954c2fbb58e3ed20a1566
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59421151"
---
# <a name="positioning-a-modalpopup-vb"></a><span data-ttu-id="0bd62-104">Размещение ModalPopup (VB)</span><span class="sxs-lookup"><span data-stu-id="0bd62-104">Positioning a ModalPopup (VB)</span></span>

<span data-ttu-id="0bd62-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0bd62-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0bd62-106">[Скачать код](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0bd62-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span></span>

> <span data-ttu-id="0bd62-107">Элемент управления ModalPopup в AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью средств на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="0bd62-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="0bd62-108">Однако элемент управления не предоставляет встроенные функциональные возможности для размещения всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="0bd62-108">However the control does not offer a built-in functionality to position the popup.</span></span>


## <a name="overview"></a><span data-ttu-id="0bd62-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="0bd62-109">Overview</span></span>

<span data-ttu-id="0bd62-110">Элемент управления ModalPopup в AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью средств на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="0bd62-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="0bd62-111">Однако элемент управления не предоставляет встроенные функциональные возможности для размещения всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="0bd62-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="0bd62-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="0bd62-112">Steps</span></span>

<span data-ttu-id="0bd62-113">Для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager`.</span><span class="sxs-lookup"><span data-stu-id="0bd62-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="0bd62-114">элемент управления необходимо поместить в любом месте на странице (но в `<form>` элемента):</span><span class="sxs-lookup"><span data-stu-id="0bd62-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="0bd62-115">Добавьте панель, который служит в качестве модального всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="0bd62-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="0bd62-116">Кнопка используется для закрытия всплывающего окна:</span><span class="sxs-lookup"><span data-stu-id="0bd62-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="0bd62-117">Каждый раз, когда всплывающее окно отображается, он должен размещаться в определенное место на странице.</span><span class="sxs-lookup"><span data-stu-id="0bd62-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="0bd62-118">Для выполнения этой задачи будет создана функция JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="0bd62-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="0bd62-119">Сначала выполняется попытка доступа к панели.</span><span class="sxs-lookup"><span data-stu-id="0bd62-119">It first tries to access the panel.</span></span> <span data-ttu-id="0bd62-120">Выполняется успешно, положение панели задается с помощью CSS и JavaScript (изменение будет положение всплывающего окна в).</span><span class="sxs-lookup"><span data-stu-id="0bd62-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="0bd62-121">Тем не менее `ModalPopupExtender` управления также пытается положение всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="0bd62-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="0bd62-122">Таким образом код JavaScript многократно всплывающее окно, каждую десятую долю секунды.</span><span class="sxs-lookup"><span data-stu-id="0bd62-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

<span data-ttu-id="0bd62-123">Как вы видите, возвращаемое значение `setTimeout()` метод JavaScript сохраняется в глобальной переменной.</span><span class="sxs-lookup"><span data-stu-id="0bd62-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="0bd62-124">Это позволяет остановить повторное размещение всплывающего окна по требованию, с помощью `clearTimeout()` метод:</span><span class="sxs-lookup"><span data-stu-id="0bd62-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

<span data-ttu-id="0bd62-125">Теперь осталось сделать лишь для вызова этих функций всякий раз, когда соответствующие браузера.</span><span class="sxs-lookup"><span data-stu-id="0bd62-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="0bd62-126">`movePanel()` Функция JavaScript должен вызываться при нажатии кнопки, который запускает панели:</span><span class="sxs-lookup"><span data-stu-id="0bd62-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

<span data-ttu-id="0bd62-127">И `stopMoving()` функции вступает в действие, когда всплывающее окно закрывается, это может быть предприняты в `ModalPopupExtender` управления:</span><span class="sxs-lookup"><span data-stu-id="0bd62-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]


<span data-ttu-id="0bd62-128">[![Появится модальное всплывающее окно в указанной позиции](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0bd62-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="0bd62-129">Появится модальное всплывающее окно в указанной позиции ([Просмотр полноразмерного изображения](positioning-a-modalpopup-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0bd62-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0bd62-130">Назад</span><span class="sxs-lookup"><span data-stu-id="0bd62-130">Previous</span></span>](handling-postbacks-from-a-modalpopup-vb.md)
