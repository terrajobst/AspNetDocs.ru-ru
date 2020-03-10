---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: Обработка обратных передач из элемента управления Popup с помощью UpdatePanel (C#) | Документация Майкрософт
author: wenz
description: Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Необходимо уделить особое внимание...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b9e58d68b3d6c5d01ceaba6c01653e9574b541b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496668"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a>Обработка операций обратной передачи из элемента управления Popup с помощью элемента управления UpdatePanel (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)

> Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. При возникновении обратной передачи в таком всплывающем окне необходимо уделить особое внимание.

## <a name="overview"></a>Обзор

Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. При возникновении обратной передачи в таком всплывающем окне необходимо уделить особое внимание.

## <a name="steps"></a>Шаги

При использовании `PopupControl` с обратной передачей `UpdatePanel` может препятствовать обновлению страницы, вызванной обратной передачей. В следующей разметке определяется несколько важных элементов:

- Элемент управления `ScriptManager`, обеспечивающий работу набора элементов управления AJAX ASP.NET
- Два элемента управления `TextBox`, которые будут активировать всплывающее окно
- Элемент управления `Panel`, который будет служить в качестве всплывающего
- На панели элемент управления `Calendar` внедрен в элемент управления `UpdatePanel`
- Два элемента управления `PopupControlExtender`, которые присваивают панель текстовым полям

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

Обратите внимание, что задан атрибут `OnSelectionChanged` элемента управления `Calendar`. Таким образом, когда пользователь выбирает дату в календаре, происходит обратная передача и выполняется `c1_SelectionChanged()` метод на стороне сервера. В этом методе необходимо получить текущую дату и записать ее обратно в текстовое поле.

Синтаксис для этого выглядит следующим образом: сначала необходимо создать прокси-объект для `PopupControlExtender` на странице. ASP.NET AJAX Control Toolkit предлагает метод `GetProxyForCurrentPopup()`. Объект, возвращаемый этим методом, поддерживает `Commit()` метод, который отправляет значение обратно в элемент управления, который инициировал всплывающее окно (а не элемент управления, вызвавший вызов метода!). Следующий код предоставляет выбранную дату в качестве аргумента для метода `Commit()`, что приводит к тому, что код записывает выбранную дату обратно в текстовое поле:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

Теперь при выборе календарной даты выбранная дата отображается в соответствующем текстовом поле, создавая элемент управления выбора даты, который в настоящее время можно найти на многих веб-сайтах.

[![календарь появляется, когда пользователь щелкает текстовое поле](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

Календарь появляется, когда пользователь щелкает текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png)).

[![, щелкнув дату, помещает ее в текстовое поле](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

Если щелкнуть дату, она помещается в текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Назад](using-multiple-popup-controls-cs.md)
> [Вперед](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
