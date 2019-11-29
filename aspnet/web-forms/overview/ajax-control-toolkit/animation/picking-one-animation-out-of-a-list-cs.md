---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: Выборка одной анимации из списка (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Платформа также разре...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 2bc203d694792716bbf4f7d7b8d152c589bf99b1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575121"
---
# <a name="picking-one-animation-out-of-a-list-c"></a>Выбор одной анимации из списка (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Платформа также позволяет программисту выбрать одну анимацию из списка анимаций в зависимости от оценки кода JavaScript.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Платформа также позволяет программисту выбрать одну анимацию из списка анимаций в зависимости от оценки кода JavaScript.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и обязательную `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы. Вместо одной из обычных анимаций элемент `<Case>` поступает в игру. Вычисляется значение его атрибута Селектскрипт. Возвращаемое значение должно быть числовым. В зависимости от этого числа выполняется одна из вложенных анимаций в &lt;случае&gt;. Например, если значение Селектскрипт равно 2, набор элементов управления запускает третью анимацию в &lt;&gt;е (отсчет начинается с 0).

Следующая разметка определяет три поданимации: изменение размера ширины, изменение высоты и плавность. Затем код JavaScript (`Math.floor(3 * Math.random())`) выбирает число от 0 до 2, чтобы выполнялась одна из трех анимаций:

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]

[![одной из возможных трех анимаций: панель становится шире](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)

Одна из возможных трех анимаций: панель расширяется ([щелкните, чтобы просмотреть изображение с полным размером](picking-one-animation-out-of-a-list-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](animation-depending-on-a-condition-cs.md)
> [Вперед](animating-in-response-to-user-interaction-cs.md)
