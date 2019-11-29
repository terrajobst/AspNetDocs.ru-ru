---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: Создание числового элемента управления "вверх/вниз" с помощью серверной части веб-службы (VB) | Документация Майкрософт
author: wenz
description: Вместо того, чтобы позволить пользователю вводить значение в флажок, числовой элемент управления "вверх/вниз" (который существует в Windows и других операционных системах) может доказать, что с...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 2bf6e1b27180589d39e308de62b5be1f47fa8fe2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606368"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>Создание числового поля со стрелками "вверх/вниз" с помощью серверной веб-службы (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> Вместо того, чтобы позволить пользователю вводить значение в флажок, числовой элемент управления "вверх/вниз" (который существует в Windows и других операционных системах) может оказаться более удобным. По умолчанию элемент управления NumericUpDown всегда увеличивает или уменьшает значение на 1, но веб-служба подтверждает большую гибкость.

## <a name="overview"></a>Обзор

Вместо того, чтобы позволить пользователю вводить значение в флажок, числовой элемент управления "вверх/вниз" (который существует в Windows и других операционных системах) может оказаться более удобным. По умолчанию элемент управления `NumericUpDown` всегда увеличивает или уменьшает значение на 1, но веб-служба подтверждает большую гибкость.

## <a name="steps"></a>Шаги

Набор средств ASP.NET AJAX Control Toolkit содержит расширитель `NumericUpDown`, который автоматически добавляет две кнопки в текстовое поле: одно для увеличения его значения, одно для его уменьшения. Однако элемент управления также поддерживает вызов веб-службы (или вызов метода страницы). При нажатии кнопки вверх или вниз код JavaScript подключается к веб-серверу и выполняет метод. Сигнатура метода является следующей:

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

Аргумент `current` — это текущее значение в текстовом поле; атрибут `tag` — это дополнительные данные контекста, которые можно задать в качестве свойства расширителя `NumericUpDown` (но это необязательно).

В этом примере числовой элемент управления "вверх/вниз" должен допускать только те значения, которые являются степенями двух: 1, 2, 4, 8, 16, 32, 64 и т. д. Поэтому метод, выполняемый, когда пользователь хочет увеличить значение, должен удвоить старое значение. другой метод должен разделить значение на два. Вот полная веб-служба:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

Наконец, создайте новую страницу ASP.NET. Обычно требуется элемент управления `ScriptManager`, `TextBox` и элемент управления `NumericUpDownExtender`. В последнем случае необходимо предоставить сведения о веб-службе:

- `ServiceDownMethod`ное имя веб-метода или метода страницы
- `ServiceDownPath` путь к веб-службе с помощью метода пониженной службы; пропускать при использовании метода страницы
- `ServiceUpMethod` имя метода веб-метода или страницы
- `ServiceUpPath` путь к веб-службе с помощью метода up Service; пропускать при использовании метода страницы

Ниже приведена полная разметка для страницы.

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

При запуске страницы обратите внимание на то, как значение в текстовом поле всегда удваивается при нажатии кнопки вверху и при нажатии нижней кнопки уменьшается вдвое.

[![отображаются только цифры, которые являются степенью 2](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

Отображаются только цифры, которые являются степенью 2 ([щелкните, чтобы просмотреть изображение с полным размером](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
