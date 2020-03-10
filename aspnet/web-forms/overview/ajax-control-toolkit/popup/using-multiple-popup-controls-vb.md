---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: Использование нескольких элементов управления Popup (VB) | Документация Майкрософт
author: wenz
description: Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Также можно использовать m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: e1f4ff64e9fdf48ea63b75c97acd53a64b5ab5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496326"
---
# <a name="using-multiple-popup-controls-vb"></a>Использование нескольких элементов управления Popup (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)

> Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. На одной странице также можно использовать несколько элементов управления Popup.

## <a name="overview"></a>Обзор

Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. На одной странице также можно использовать несколько элементов управления Popup.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

Затем добавьте панель, которая выступает в качестве всплывающего. В текущем сценарии панель содержит элемент управления `Calendar`. Чтобы избежать обновления страниц, вызванных обратными передачами календаря, панель помещается в элемент управления `UpdatePanel`:

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

Страница также содержит два текстовых поля. Для каждого текстового поля всплывающее окно календаря появляется после активации текстового поля.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

Теперь расширьте каждое из двух текстовых полей с помощью `PopupControlExtender`. Атрибут `TargetControlID` предоставляет идентификатор элемента управления, привязанного к расширителю. Атрибут `PopupControlID` содержит идентификатор всплывающей панели. В этом случае оба расширителя отображают одну и ту же панель, но также могут быть разными панелями.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

Теперь, когда вы щелкнули текстовое поле, под полем появляется календарь, позволяющий выбрать дату. (Чтобы получить выбранную дату обратно в текстовые поля, появятся различные учебники.)

[![календарь появляется, когда пользователь щелкает текстовое поле](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)

Календарь появляется, когда пользователь щелкает текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](using-multiple-popup-controls-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [Вперед](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
