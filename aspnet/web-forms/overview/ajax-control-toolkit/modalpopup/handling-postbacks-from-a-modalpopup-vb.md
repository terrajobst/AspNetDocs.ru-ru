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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606638"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a>Обработка обратных передач из ModalPopup (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)

> Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. При создании обратной передачи во всплывающем окне необходимо соблюдать особое внимание.

## <a name="overview"></a>Обзор

Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. При создании обратной передачи во всплывающем окне необходимо соблюдать особое внимание.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

Затем добавьте панель, которая выступает в качестве модального всплывающего окна. Здесь пользователь может ввести имя и адрес электронной почты. Кнопка используется для закрытия всплывающего окна и сохранения данных. Обратите внимание, что атрибут `OnClick` задан таким образом, что при нажатии на эту кнопку происходит обратная передача:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

Сама страница состоит из двух меток для одних и тех же сведений: имя и адрес электронной почты. Кнопка используется для запуска модального всплывающего окна:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

Чтобы отобразить всплывающее окно, добавьте элемент управления `ModalPopupExtender`. Задайте атрибуту `PopupControlID` идентификатор панели и `TargetControlID` ИДЕНТИФИКАТОРу кнопки:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

Теперь при нажатии кнопки `Save` в модальном всплывающем окне выполняется метод `SaveData()` на стороне сервера. Там можно сохранить введенные данные в хранилище данных. В целях простоты новые данные просто выводятся в метке:

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

Кроме того, элементы управления TextBox в модальном всплывающем окне должны быть заполнены текущим именем и сообщением электронной почты. Однако это необходимо только в том случае, если обратная передача не выполняется. При наличии обратной передачи функция ViewState ASP.NET автоматически заполняет текстовые поля соответствующими значениями.

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

[![модальное всплывающее окно вызывает обратную передачу](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)

Модальное всплывающее окно вызывает обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](using-modalpopup-with-a-repeater-control-vb.md)
> [Вперед](positioning-a-modalpopup-vb.md)
