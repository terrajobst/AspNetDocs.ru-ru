---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: Исполнение нескольких анимаций после друг другаC#() | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет запускать серьезность...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: e378ac038796dbd44e89d099532b9e186dcf673f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575450"
---
# <a name="executing-several-animations-after-each-other-c"></a>Выполнение нескольких анимаций друг за другом (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет запускать несколько анимаций один за другим.

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Он позволяет запускать несколько анимаций один за другим.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и обязательную `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

В `<Animations>` узле используйте `<OnLoad>` для запуска анимации после полной загрузки страницы. Как правило, `<OnLoad>` принимает только одну анимацию. Платформа анимации позволяет объединить несколько анимаций в одну с помощью элемента `<Sequence>`. Все анимации в `<Sequence>` выполняются один за другим. Ниже приведена возможная разметка для элемента управления `AnimationExtender`, которая сначала делает панель шире, а затем уменьшает ее высоту:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

При запуске этого скрипта панель сначала становится шире, а затем уменьшается.

[![сначала ширина увеличивается](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)

Сначала увеличивается ширина ([щелкните, чтобы просмотреть изображение с полным размером](executing-several-animations-after-each-other-cs/_static/image3.png))

[![будет уменьшена высота](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)

Затем уменьшается высота ([щелкните, чтобы просмотреть изображение с полным размером](executing-several-animations-after-each-other-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Назад](executing-several-animations-at-the-same-time-cs.md)
> [Вперед](animation-depending-on-a-condition-cs.md)
