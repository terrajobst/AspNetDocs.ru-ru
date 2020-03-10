---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: Одновременное исполнение нескольких анимаций (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет запускать серьезность...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483972"
---
# <a name="executing-several-animations-at-the-same-time-c"></a>Одновременное исполнение нескольких анимаций (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет параллельно запускать несколько анимаций.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет параллельно запускать несколько анимаций.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы. Как правило, `<OnLoad>` принимает только одну анимацию. Платформа анимации позволяет объединить несколько анимаций в одну с помощью элемента `<Parallel>`. Все анимации в `<Parallel>` выполняются одновременно.

Ниже приведена возможная разметка для элемента управления `AnimationExtender`, плавное уменьшение и изменение размера панели.

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

И действительно: при запуске этого скрипта панель отображается, затем изменяется размер (больше, чем утраивается ее ширина и вдвое высота) и плавно исчезает.

[![панель вытекает и изменяет ее размер (включая содержимое, благодаря подсистеме рендеринга в браузере).](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)

Панель вытекает и изменяет ее размер (включая содержимое, благодаря подсистеме рендеринга в браузере) ([щелкните, чтобы просмотреть изображение с полным размером](executing-several-animations-at-the-same-time-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](adding-animation-to-a-control-cs.md)
> [Вперед](executing-several-animations-after-each-other-cs.md)
