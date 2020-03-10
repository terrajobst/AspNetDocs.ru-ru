---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: Одновременное исполнение нескольких анимаций (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет запускать серьезность...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: fc11debd06c897c29db56d42167d483f5608cdf8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497802"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a>Одновременное исполнение нескольких анимаций (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет параллельно запускать несколько анимаций.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет параллельно запускать несколько анимаций.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы. Как правило, `<OnLoad>` принимает только одну анимацию. Платформа анимации позволяет объединить несколько анимаций в одну с помощью элемента `<Parallel>`. Все анимации в `<Parallel>` выполняются одновременно.

Ниже приведена возможная разметка для элемента управления `AnimationExtender`, плавное уменьшение и изменение размера панели.

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

И действительно: при запуске этого скрипта панель отображается, затем изменяется размер (больше, чем утраивается ее ширина и вдвое высота) и плавно исчезает.

[![панель вытекает и изменяет ее размер (включая содержимое, благодаря подсистеме рендеринга в браузере).](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)

Панель вытекает и изменяет ее размер (включая содержимое, благодаря подсистеме рендеринга в браузере) ([щелкните, чтобы просмотреть изображение с полным размером](executing-several-animations-at-the-same-time-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](adding-animation-to-a-control-vb.md)
> [Вперед](executing-several-animations-after-each-other-vb.md)
