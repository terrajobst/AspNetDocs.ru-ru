---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: Анимация в зависимости от условия (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Является ли анимация...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484170"
---
# <a name="animation-depending-on-a-condition-c"></a>Анимация в зависимости от условия (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Выполняется ли анимация, а также может зависеть от условия в виде кода JavaScript.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Выполняется ли анимация, а также может зависеть от условия в виде кода JavaScript.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и обязательную `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы. Вместо одной из обычных анимаций элемент `<Condition>` поступает в игру. Код JavaScript, предоставленный в качестве значения атрибута `ConditionScript`, выполняется во время выполнения. Если значение равно true, анимация выполняется, в противном случае — нет. Следующая разметка предоставляет две анимации, каждая из которых выполняется в 50% случаев при случайном. Так как в `<OnLoad>`может быть только одна анимация, две `<Condition>` анимации объединяются с помощью элемента `<Sequence>`:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

Обратите внимание, что знак "меньше" (`<`) в атрибуте `ConditionScript` должен быть экранированным (). При запуске этого скрипта не выполняется ни анимация, ни одно из двух операций.

[![панель вытекает без изменения размера, поэтому выполняется вторая анимация, первая — не](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)

Панель вытекает без изменения размера, поэтому вторая анимация выполняется, а первая — нет ([щелкните, чтобы просмотреть изображение с полным размером](animation-depending-on-a-condition-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](executing-several-animations-after-each-other-cs.md)
> [Вперед](picking-one-animation-out-of-a-list-cs.md)
