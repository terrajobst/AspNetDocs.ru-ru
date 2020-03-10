---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: Запуск модального всплывающего окна из серверногоC#кода () | Документация Майкрософт
author: wenz
description: Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Однако в некоторых сценариях требуется, чтобы t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: fec0ce2cdd24333f65201301718440e1a09d930e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496980"
---
# <a name="launching-a-modal-popup-window-from-server-code-c"></a><span data-ttu-id="ee135-104">Запуск модального всплывающего окна из серверного кода (C#)</span><span class="sxs-lookup"><span data-stu-id="ee135-104">Launching a Modal Popup Window from Server Code (C#)</span></span>

<span data-ttu-id="ee135-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ee135-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ee135-106">[Скачать код](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ee135-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span></span>

> <span data-ttu-id="ee135-107">Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="ee135-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="ee135-108">Однако в некоторых сценариях требуется, чтобы открытие модального всплывающего окна вызывалось на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="ee135-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="overview"></a><span data-ttu-id="ee135-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="ee135-109">Overview</span></span>

<span data-ttu-id="ee135-110">Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="ee135-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="ee135-111">Однако в некоторых сценариях требуется, чтобы открытие модального всплывающего окна вызывалось на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="ee135-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="ee135-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="ee135-112">Steps</span></span>

<span data-ttu-id="ee135-113">Прежде всего, для демонстрации работы элемента управления ModalPopup требуется веб-элемент управления ASP.NET Button.</span><span class="sxs-lookup"><span data-stu-id="ee135-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="ee135-114">Добавьте такую кнопку в элемент &lt;Form&gt; на новой странице:</span><span class="sxs-lookup"><span data-stu-id="ee135-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

<span data-ttu-id="ee135-115">Затем требуется разметка для всплывающего окна, которое необходимо создать.</span><span class="sxs-lookup"><span data-stu-id="ee135-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="ee135-116">Определите его как элемент управления `<asp:Panel>` и убедитесь, что он включает элемент управления "Кнопка".</span><span class="sxs-lookup"><span data-stu-id="ee135-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="ee135-117">Элемент управления ModalPopup предлагает функциональные возможности, позволяющие сделать такую кнопку закрытой. в противном случае нет простого способа разрешить его.</span><span class="sxs-lookup"><span data-stu-id="ee135-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

<span data-ttu-id="ee135-118">Затем добавьте элемент управления ModalPopup из набора средств AJAX для ASP.NET на страницу.</span><span class="sxs-lookup"><span data-stu-id="ee135-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="ee135-119">Задайте свойства для кнопки, которая загружает элемент управления, кнопку, которая исчезает, и идентификатор фактического всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="ee135-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

<span data-ttu-id="ee135-120">Как и для всех веб-страниц на основе ASP.NET AJAX; Диспетчер скриптов необходим для загрузки необходимых библиотек JavaScript для различных целевых браузеров:</span><span class="sxs-lookup"><span data-stu-id="ee135-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

<span data-ttu-id="ee135-121">Запустите пример в браузере.</span><span class="sxs-lookup"><span data-stu-id="ee135-121">Run the example in the browser.</span></span> <span data-ttu-id="ee135-122">При нажатии кнопки появляется модальное всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="ee135-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="ee135-123">Чтобы добиться того же результата с помощью кода на стороне сервера, требуется новая кнопка:</span><span class="sxs-lookup"><span data-stu-id="ee135-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

<span data-ttu-id="ee135-124">Как видите, нажатие кнопки приводит к созданию обратной передачи и выполнению метода `ServerButton_Click()` на сервере.</span><span class="sxs-lookup"><span data-stu-id="ee135-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="ee135-125">В этом методе функция JavaScript с именем `launchModal()` выполняется как точная, функция JavaScript будет выполняться после загрузки страницы:</span><span class="sxs-lookup"><span data-stu-id="ee135-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

<span data-ttu-id="ee135-126">Задача `launchModal()` заключается в отображении ModalPopup.</span><span class="sxs-lookup"><span data-stu-id="ee135-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="ee135-127">Функция `launchModal()` выполняется после загрузки полной HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="ee135-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="ee135-128">Однако в этот момент платформа ASP.NET AJAX еще не была полностью загружена.</span><span class="sxs-lookup"><span data-stu-id="ee135-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="ee135-129">Таким образом, функция `launchModal()` просто задает переменную, которую элемент управления ModalPopup должен показывать позже:</span><span class="sxs-lookup"><span data-stu-id="ee135-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

<span data-ttu-id="ee135-130">`pageLoad()` функция JavaScript — это специальная функция, которая выполняется после полной загрузки ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="ee135-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="ee135-131">Поэтому мы добавим код в эту функцию для отображения элемента управления ModalPopup, но только при вызове `launchModal()` до:</span><span class="sxs-lookup"><span data-stu-id="ee135-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

<span data-ttu-id="ee135-132">Функция `$find()` ищет именованный элемент на странице и ожидает идентификатор на стороне сервера в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="ee135-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="ee135-133">Таким образом, `$find("mpe")` Возвращает клиентское представление элемента управления ModalPopup; его `show()` метод позволяет отображать всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="ee135-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>

<span data-ttu-id="ee135-134">[![модальное всплывающее окно появляется при нажатии одной из кнопок](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ee135-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="ee135-135">Модальное всплывающее окно появляется при нажатии одной из кнопок ([щелкните, чтобы просмотреть изображение с полным размером](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="ee135-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ee135-136">Дальше</span><span class="sxs-lookup"><span data-stu-id="ee135-136">Next</span></span>](using-modalpopup-with-a-repeater-control-cs.md)
