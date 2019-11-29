---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: Отключение действий во время анимации (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он также поддерживает действие...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606816"
---
# <a name="disabling-actions-during-animation-vb"></a>Отключение действий во время анимации (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он также поддерживает действия, например щелчки мыши. Однако когда щелчок мыши запускает анимацию, желательно отключить щелчки мыши во время анимации.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он также поддерживает действия, например щелчки мыши. Однако когда щелчок мыши запускает анимацию, желательно отключить щелчки мыши во время анимации.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

Анимация будет применена к HTML-кнопке следующим образом:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

Обратите внимание, что элемент управления HTML используется вместо веб-элемента управления, так как не нужно, чтобы кнопка была создана обратной передачей. Он просто запускает анимацию на стороне клиента для нас.

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

В `<Animations>` узле `<OnClick>` является правым элементом для управления щелчком мыши. Однако во время анимации кнопка может быть нажата. Элемент `<EnableAction>` может позаботиться об этом. Параметр `Enabled="false"` отключает кнопку как часть анимации. Так как мы используем несколько отдельных анимаций (отключив кнопку и фактические анимации), элемент `<Parallel>` необходим для объединения одной анимации в одну. Ниже приведена полная разметка для `AnimationExtender`.

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

Кроме того, можно было бы снова включить кнопку после анимации, используя следующий XML-элемент в конце списка:

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

Однако в данном сценарии это будет бесполезно, так как кнопка исчезает и не отображается в конце анимации.

[![кнопка отключена сразу после запуска анимации](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)

Кнопка будет отключена сразу после запуска анимации ([щелкните, чтобы просмотреть изображение с полным размером](disabling-actions-during-animation-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](animating-in-response-to-user-interaction-vb.md)
> [Вперед](triggering-an-animation-in-another-control-vb.md)
