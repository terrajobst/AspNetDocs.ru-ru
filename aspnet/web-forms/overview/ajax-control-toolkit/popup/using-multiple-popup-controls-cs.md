---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: Использование нескольких элементов управления PopupC#() | Документация Майкрософт
author: wenz
description: Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Также можно использовать m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611659"
---
# <a name="using-multiple-popup-controls-c"></a>Использование нескольких элементов управления Popup (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)

> Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. На одной странице также можно использовать несколько элементов управления Popup.

## <a name="overview"></a>Обзор

Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. На одной странице также можно использовать несколько элементов управления Popup.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

Затем добавьте панель, которая выступает в качестве всплывающего. В текущем сценарии панель содержит элемент управления `Calendar`. Чтобы избежать обновления страниц, вызванных обратными передачами календаря, панель помещается в элемент управления `UpdatePanel`:

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

Страница также содержит два текстовых поля. Для каждого текстового поля всплывающее окно календаря появляется после активации текстового поля.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

Теперь расширьте каждое из двух текстовых полей с помощью `PopupControlExtender`. Атрибут `TargetControlID` предоставляет идентификатор элемента управления, привязанного к расширителю. Атрибут `PopupControlID` содержит идентификатор всплывающей панели. В этом случае оба расширителя отображают одну и ту же панель, но также могут быть разными панелями.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

Теперь, когда вы щелкнули текстовое поле, под полем появляется календарь, позволяющий выбрать дату. (Чтобы получить выбранную дату обратно в текстовые поля, появятся различные учебники.)

[![календарь появляется, когда пользователь щелкает текстовое поле](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)

Календарь появляется, когда пользователь щелкает текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](using-multiple-popup-controls-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Вперед](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
