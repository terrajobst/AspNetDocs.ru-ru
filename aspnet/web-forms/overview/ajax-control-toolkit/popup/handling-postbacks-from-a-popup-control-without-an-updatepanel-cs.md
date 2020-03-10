---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: Обработка обратных передач из элемента управления Popup без UpdatePanel (C#) | Документация Майкрософт
author: wenz
description: Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Когда обратная передача происходит в SU...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496506"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>Обработка операций обратной передачи из элемента управления Popup без использования элемента управления UpdatePanel (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Если обратная передача происходит на такой панели и на странице есть несколько панелей, трудно определить, какая панель была нажата.

## <a name="overview"></a>Обзор

Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Если обратная передача происходит на такой панели и на странице есть несколько панелей, трудно определить, какая панель была нажата.

## <a name="steps"></a>Шаги

При использовании `PopupControl` с обратной передачей, но без `UpdatePanel` на странице, набор элементов управления не предлагает способ определить, какой клиентский элемент инициировал всплывающее окно, которое, в свою очередь, вызвало обратную передачу. Но небольшой хитростью является обходной путь для этого сценария.

Во-первых, вот основная настройка: два текстовых поля, которые вызывают одно и то же всплывающее окно, календарь. Два `PopupControlExtenders` поместит текстовые поля и всплывающее окно вместе.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

Основная идея состоит в том, чтобы добавить скрытое поле формы в элемент &lt;`form`&gt;, содержащий текстовое поле, которое запустило всплывающее окно:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

При загрузке страницы код JavaScript добавляет обработчик событий в оба текстовых поля: каждый раз, когда пользователь щелкает текстовое поле, его имя записывается в скрытое поле формы:

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

В коде на стороне сервера значение скрытого поля должно быть считано. Поскольку скрытые поля формы просты для управления, утвержденный список способов проверки скрытые значения является обязательным. После определения правильного текстового поля в него записывается дата из календаря.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

[![календарь появляется, когда пользователь щелкает текстовое поле](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

Календарь появляется, когда пользователь щелкает текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)).

[![, щелкнув дату, помещает ее в текстовое поле](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

Если щелкнуть дату, она помещается в текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Назад](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [Вперед](using-multiple-popup-controls-vb.md)
