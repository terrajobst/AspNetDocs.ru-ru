---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: Использование элемента управления "ползунок" с автоматической обратной передачей (VB) | Документация Майкрософт
author: wenz
description: Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно установить ползунок автозаписи...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598563"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a>Использование элемента управления "ползунок" с автоматической обратной передачей (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)

> Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно сделать автообратную передачу ползунка после изменения ее значения.

## <a name="overview"></a>Обзор

Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно сделать автообратную передачу ползунка после изменения ее значения.

## <a name="steps"></a>Шаги

Чтобы сделать ползунок автоматически обратным при изменении, в обоих текстовых полях требуется атрибут `AutoPostBack="true"`: текстовое поле, которое станет самим ползунком, и текстовое поле, содержащее положение ползунка. Ниже приведена необходимая разметка для этого:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

Элемент управления `SliderExtender` из набора средств ASP.NET AJAX Control Toolkit назначает функции ползунка для двух текстовых полей:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

Позже будет использоваться дополнительный элемент Label для информирования пользователя о обратной передаче:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

Наконец, `ScriptManager` элемент управления ASP.NET AJAX загружает необходимый код JavaScript для работы набора средств управления:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

Теперь ползунок передается обратно. на стороне сервера это событие может быть перехвачено и обработано в следующих случаях:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

[![перемещение ползунка инициирует обратную передачу](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)

Перемещение ползунка активирует обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-the-slider-control-with-auto-postback-vb/_static/image3.png))

[![затем Дата этого изменения записывается в метку](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)

Затем Дата этого изменения записывается в метку ([щелкните, чтобы просмотреть изображение с полным размером](using-the-slider-control-with-auto-postback-vb/_static/image6.png)).

> [!div class="step-by-step"]
> [Назад](databinding-the-slider-control-cs.md)
> [Вперед](databinding-the-slider-control-vb.md)
