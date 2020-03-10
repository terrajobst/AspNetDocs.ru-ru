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
# <a name="launching-a-modal-popup-window-from-server-code-c"></a>Запуск модального всплывающего окна из серверного кода (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)

> Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Однако в некоторых сценариях требуется, чтобы открытие модального всплывающего окна вызывалось на стороне сервера.

## <a name="overview"></a>Обзор

Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Однако в некоторых сценариях требуется, чтобы открытие модального всплывающего окна вызывалось на стороне сервера.

## <a name="steps"></a>Шаги

Прежде всего, для демонстрации работы элемента управления ModalPopup требуется веб-элемент управления ASP.NET Button. Добавьте такую кнопку в элемент &lt;Form&gt; на новой странице:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

Затем требуется разметка для всплывающего окна, которое необходимо создать. Определите его как элемент управления `<asp:Panel>` и убедитесь, что он включает элемент управления "Кнопка". Элемент управления ModalPopup предлагает функциональные возможности, позволяющие сделать такую кнопку закрытой. в противном случае нет простого способа разрешить его.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

Затем добавьте элемент управления ModalPopup из набора средств AJAX для ASP.NET на страницу. Задайте свойства для кнопки, которая загружает элемент управления, кнопку, которая исчезает, и идентификатор фактического всплывающего окна.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

Как и для всех веб-страниц на основе ASP.NET AJAX; Диспетчер скриптов необходим для загрузки необходимых библиотек JavaScript для различных целевых браузеров:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

Запустите пример в браузере. При нажатии кнопки появляется модальное всплывающее окно. Чтобы добиться того же результата с помощью кода на стороне сервера, требуется новая кнопка:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

Как видите, нажатие кнопки приводит к созданию обратной передачи и выполнению метода `ServerButton_Click()` на сервере. В этом методе функция JavaScript с именем `launchModal()` выполняется как точная, функция JavaScript будет выполняться после загрузки страницы:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

Задача `launchModal()` заключается в отображении ModalPopup. Функция `launchModal()` выполняется после загрузки полной HTML-страницы. Однако в этот момент платформа ASP.NET AJAX еще не была полностью загружена. Таким образом, функция `launchModal()` просто задает переменную, которую элемент управления ModalPopup должен показывать позже:

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

`pageLoad()` функция JavaScript — это специальная функция, которая выполняется после полной загрузки ASP.NET AJAX. Поэтому мы добавим код в эту функцию для отображения элемента управления ModalPopup, но только при вызове `launchModal()` до:

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

Функция `$find()` ищет именованный элемент на странице и ожидает идентификатор на стороне сервера в качестве параметра. Таким образом, `$find("mpe")` Возвращает клиентское представление элемента управления ModalPopup; его `show()` метод позволяет отображать всплывающее окно.

[![модальное всплывающее окно появляется при нажатии одной из кнопок](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)

Модальное всплывающее окно появляется при нажатии одной из кнопок ([щелкните, чтобы просмотреть изображение с полным размером](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Дальше](using-modalpopup-with-a-repeater-control-cs.md)
