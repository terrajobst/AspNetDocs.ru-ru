---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: Настройка Z-индекса DropShadow (C#) | Документация Майкрософт
author: wenz
description: Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Однако эта тень иногда конфликтует с другими элементами управления, для программа...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 12bc7f0430f1f30ff964cd9547ee1e9b0aa7423c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497484"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a>Настройка Z-индекса DropShadow (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)

> Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Однако эта тень иногда конфликтует с другими элементами управления, например с элементом управления меню ASP.NET. Когда появляется запись меню, она отображается позади тени.

## <a name="overview"></a>Обзор

Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Однако эта тень иногда конфликтует с другими элементами управления, например с элементом управления меню ASP.NET. Когда появляется запись меню, она отображается позади тени.

## <a name="steps"></a>Шаги

Код начнется с самой панели, содержащей достаточно текста, чтобы панель содержит достаточно текста для отображения результата:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

Другая панель размещается непосредственно перед панелью `panelShadow`. Он содержит меню с горизонтальной ориентацией, чтобы на панели `dropShadow` появлялись записи меню (или просто: в):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

Затем добавляется `DropShadowExtender` для расширения панели `panelShadow` с эффектом тени:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

Наконец, элемент управления `ScriptManager` AJAX ASP.NET позволяет набору элементов управления работать:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

При запуске этого скрипта пункты меню отображаются под панелью. Однако в меню используется класс CSS `panel`, где необходимо определить две вещи, чтобы элементы отображались перед другой панелью:

- Относительное положение
- Положительный z-индекс

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

Затем элемент управления "`DropShadowExtender`" больше не конфликтует с элементом управления Menu.

[![до: запись меню не отображается](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)

До: запись меню не отображается ([щелкните, чтобы просмотреть изображение с полным размером](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))

[![после: появится запись меню](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)

После: появится запись меню ([щелкните, чтобы просмотреть изображение с полным размером](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png)).

> [!div class="step-by-step"]
> [Дальше](manipulating-dropshadow-properties-from-client-code-cs.md)
