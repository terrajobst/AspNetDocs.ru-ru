---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: Использование элемента управления textboxwatermark с элементами управления проверки (VB) | Документация Майкрософт
author: wenz
description: Элемент управления элемента управления textboxwatermark в наборе средств AJAX Control Toolkit расширяет текстовое поле, чтобы текст отображался в поле. Когда пользователь щелкает в поле, он...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 141cae26c9e52be510e2a5a8f816cbac977dcf3d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597241"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>Использование элемента управления TextBoxWatermark с проверяющими элементами управления (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> Элемент управления элемента управления textboxwatermark в наборе средств AJAX Control Toolkit расширяет текстовое поле, чтобы текст отображался в поле. Когда пользователь щелкает в поле, он очищается. Если пользователь оставляет поле без ввода текста, заполняется предварительно заполненный текст. Это может конфликтовать с элементами управления проверки ASP.NET на той же странице, но эти проблемы можно преодолеть.

## <a name="overview"></a>Обзор

Элемент управления `TextBoxWatermark` в наборе средств AJAX Control Toolkit расширяет текстовое поле, позволяя отображать текст в поле. Когда пользователь щелкает в поле, он очищается. Если пользователь оставляет поле без ввода текста, заполняется предварительно заполненный текст. Это может конфликтовать с элементами управления проверки ASP.NET на той же странице, но эти проблемы можно преодолеть.

## <a name="steps"></a>Шаги

Базовая настройка образца состоит из следующих элементов: элемент управления `TextBox` с водяным знаком с помощью элемента управления `TextBoxWatermarkExtender`. Кнопка активирует обратную передачу и затем будет использоваться для активации элементов управления проверки на странице. Кроме того, для инициализации ASP.NET AJAX требуется элемент управления `ScriptManager`:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

Теперь добавьте элемент управления `RequiredFieldValidator`, который проверяет, есть ли в поле текст при отправке формы. Свойству `InitialValue` проверяющего элемента управления должно быть присвоено то же значение, которое используется в `TextBoxWatermarkExtender`ном элементе. при отправке формы значение неизмененного текстового поля — это значение водяного знака в нем:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

Однако существует одна проблема, связанная с этим подходом: Если клиент отключает JavaScript, текстовое поле не заполняется текстом водяного знака, поэтому `RequiredFieldValidator` не запускает сообщение об ошибке. Поэтому требуется второй элемент управления `RequiredFieldValidator`, проверяющий наличие пустого текстового поля (без атрибута `InitialValue`).

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

Поскольку оба проверяющего элемента управления используют `Display`=`"Dynamic"`, конечный пользователь не может отличить внешний вид, в котором были запущены два проверяющих элемента управления. Вместо этого он выглядит как есть только один из них.

Наконец, добавьте некоторый серверный код для вывода текста в поле, если средство проверки не выдавало сообщение об ошибке:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

[![проверяющей элемент управления сообщает, что в поле нет текста](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

Проверяющий элемент управления сообщает, что в поле нет текста ([щелкните, чтобы просмотреть изображение с полным размером](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](using-textboxwatermark-in-a-formview-vb.md)
