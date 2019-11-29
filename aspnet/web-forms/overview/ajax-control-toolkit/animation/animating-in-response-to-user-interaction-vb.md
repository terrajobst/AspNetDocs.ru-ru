---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: Анимация в ответ на взаимодействие с пользователем (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимация может иметь вид звезды...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 629d79505cebd49c2f05333bfbf78166f80fc6cb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607029"
---
# <a name="animating-in-response-to-user-interaction-vb"></a>Анимация в ответ на взаимодействие пользователя (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации могут запускаться автоматически или могут запускаться пользователем, например, при щелчке мышью.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации могут запускаться автоматически или могут запускаться пользователем, например, при щелчке мышью.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

В `<Animations>` узле существует пять способов запуска анимации с помощью взаимодействия с пользователем (отсутствующий элемент — `<OnLoad>` что выполняется после полной загрузки страницы целиком):

- `<OnClick>` (щелчок мышью в элементе управления)
- `<OnHoverOut>` (мышь выходит за пределы элемента управления)
- `<OnHoverOver>` (наведение указателя мыши на элемент управления, остановка `<OnHoverOut>`ной анимации)
- `<OnMouseOut>` (мышь выходит за пределы элемента управления)
- `<OnMouseOver>` (наведение указателя мыши на элемент управления, но не останавливает анимацию `<OnMouseOut>`)

В этом сценарии используется `<OnClick>`. Когда пользователь щелкает эту панель, он изменяется и постепенно исчезает.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

[![щелчок мышью запускает анимацию](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)

Щелчок мышью запускает анимацию ([щелкните, чтобы просмотреть изображение с полным размером](animating-in-response-to-user-interaction-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](picking-one-animation-out-of-a-list-vb.md)
> [Вперед](disabling-actions-during-animation-vb.md)
