---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: Привязка данных к элементу управления Slider (VB) | Документация Майкрософт
author: wenz
description: Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно привязать текущую поситио...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508902"
---
# <a name="databinding-the-slider-control-vb"></a>Привязка данных элемента управления Slider (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)

> Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно привязать текущую положение ползунка к другому элементу управления ASP.NET.

## <a name="overview"></a>Обзор

Элемент управления "ползунок" в наборе средств AJAX Control Toolkit предоставляет графический ползунок, который можно контролировать с помощью мыши. Можно привязать текущую положение ползунка к другому элементу управления ASP.NET.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

Затем добавьте на страницу два элемента управления `TextBox`. Один из них будет преобразован в графический ползунок, а другой будет содержать положение ползунка.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

Следующий шаг уже является последним. Элемент управления `SliderExtender` из набора средств управления AJAX ASP.NET делает ползунок из первого текстового поля и автоматически обновляет второе текстовое поле при изменении положения ползунка. Чтобы это работало, атрибуту `TargetControlID` `SliderExtender`должен быть присвоен идентификатор первого текстового поля. атрибуту `BoundControlID` должен быть присвоен идентификатор второго текстового поля.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

Как видно в браузере, привязка данных работает в обоих направлениях: ввод нового значения в текстовое поле обновляет положение ползунка. Если сделать второе текстовое поле только для чтения, можно добавить слабую защиту в текстовое поле, чтобы пользователь не мог вручную обновить значение в нем.

[Ползунок и текстовое поле ![синхронизированы](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

Ползунок и текстовое поле синхронизированы ([щелкните, чтобы просмотреть изображение с полным размером](databinding-the-slider-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](using-the-slider-control-with-auto-postback-vb.md)
