---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: Анимация в ответ на взаимодействие с пользователем (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимация может иметь вид звезды...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497904"
---
# <a name="animating-in-response-to-user-interaction-c"></a>Анимация в ответ на взаимодействие пользователя (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации могут запускаться автоматически или могут запускаться пользователем, например, при щелчке мышью.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации могут запускаться автоматически или могут запускаться пользователем, например, при щелчке мышью.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

В `<Animations>` узле существует пять способов запуска анимации с помощью взаимодействия с пользователем (отсутствующий элемент — `<OnLoad>` что выполняется после полной загрузки страницы целиком):

- `<OnClick>` (щелчок мышью в элементе управления)
- `<OnHoverOut>` (мышь выходит за пределы элемента управления)
- `<OnHoverOver>` (наведение указателя мыши на элемент управления, остановка `<OnHoverOut>`ной анимации)
- `<OnMouseOut>` (мышь выходит за пределы элемента управления)
- `<OnMouseOver>` (наведение указателя мыши на элемент управления, но не останавливает анимацию `<OnMouseOut>`)

В этом сценарии используется `<OnClick>`. Когда пользователь щелкает эту панель, он изменяется и постепенно исчезает.

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

[![щелчок мышью запускает анимацию](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

Щелчок мышью запускает анимацию ([щелкните, чтобы просмотреть изображение с полным размером](animating-in-response-to-user-interaction-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](picking-one-animation-out-of-a-list-cs.md)
> [Вперед](disabling-actions-during-animation-cs.md)
