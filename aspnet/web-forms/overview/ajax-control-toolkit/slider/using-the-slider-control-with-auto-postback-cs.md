---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: Использование элемента управления "ползунок" с автоматическойC#обратной передачей () | Документация Майкрософт
author: wenz
description: Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно установить ползунок автозаписи...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445830"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a>Использование элемента управления Slider с автоматической обратной передачей (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)

> Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно сделать автообратную передачу ползунка после изменения ее значения.

## <a name="overview"></a>Обзор

Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно сделать автообратную передачу ползунка после изменения ее значения.

## <a name="steps"></a>Шаги

Чтобы сделать ползунок автоматически обратным при изменении, в обоих текстовых полях требуется атрибут `AutoPostBack="true"`: текстовое поле, которое станет самим ползунком, и текстовое поле, содержащее положение ползунка. Ниже приведена необходимая разметка для этого:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

Элемент управления `SliderExtender` из набора средств ASP.NET AJAX Control Toolkit назначает функции ползунка для двух текстовых полей:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

Позже будет использоваться дополнительный элемент Label для информирования пользователя о обратной передаче:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

Наконец, `ScriptManager` элемент управления ASP.NET AJAX загружает необходимый код JavaScript для работы набора средств управления:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

Теперь ползунок передается обратно. на стороне сервера это событие может быть перехвачено и обработано в следующих случаях:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

[![перемещение ползунка инициирует обратную передачу](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)

Перемещение ползунка активирует обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-the-slider-control-with-auto-postback-cs/_static/image3.png))

[![затем Дата этого изменения записывается в метку](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)

Затем Дата этого изменения записывается в метку ([щелкните, чтобы просмотреть изображение с полным размером](using-the-slider-control-with-auto-postback-cs/_static/image6.png)).

> [!div class="step-by-step"]
> [Дальше](databinding-the-slider-control-cs.md)
