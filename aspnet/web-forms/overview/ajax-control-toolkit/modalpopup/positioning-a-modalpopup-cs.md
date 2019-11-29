---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: Размещение ModalPopup (C#) | Документация Майкрософт
author: wenz
description: Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Однако элемент управления не предлагает...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599015"
---
# <a name="positioning-a-modalpopup-c"></a>Размещение ModalPopup (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)

> Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Однако элемент управления не предоставляет встроенные функции для позиционирования всплывающего окна.

## <a name="overview"></a>Обзор

Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Однако элемент управления не предоставляет встроенные функции для позиционирования всплывающего окна.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, `ScriptManager`. элемент управления должен размещаться в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

Затем добавьте панель, которая выступает в качестве модального всплывающего окна. Кнопка используется для закрытия всплывающего окна:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

При отображении всплывающего окна оно должно располагаться в определенном месте страницы. Для этой задачи создается клиентская функция JavaScript. Сначала он пытается получить доступ к панели. В случае успешности положение панели задается с помощью CSS и JavaScript (измените положение всплывающего окна в нем). Однако элемент управления `ModalPopupExtender` также пытается расположить всплывающее окно. Таким образом, код JavaScript многократно помещает всплывающее окно в каждую десятую часть секунды.

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

Как видите, возвращаемое значение метода `setTimeout()` JavaScript сохраняется в глобальной переменной. Это позволяет предотвратить повторное позиционирование всплывающего окна по запросу с помощью метода `clearTimeout()`:

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

Теперь все, что осталось сделать, — это заставить браузер вызывать эти функции при необходимости. Функция `movePanel()` JavaScript должна вызываться при нажатии кнопки, которая активирует панель:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

При закрытии всплывающего окна функция `stopMoving()` вступает в игру. это может быть вызвано в элементе управления `ModalPopupExtender`:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

[![модальное всплывающее окно отображается в указанной позиции](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)

Модальное всплывающее окно отображается в указанной позиции ([щелкните, чтобы просмотреть изображение с полным размером](positioning-a-modalpopup-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](handling-postbacks-from-a-modalpopup-cs.md)
> [Вперед](launching-a-modal-popup-window-from-server-code-vb.md)
