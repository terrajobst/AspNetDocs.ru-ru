---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: Управление свойствами DropShadow из клиентского кода (VB) | Документация Майкрософт
author: wenz
description: Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Свойства этого расширителя также можно изменить с помощью Жаваскрип клиента...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497412"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a>Обработка свойств DropShadow из клиентского кода (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)

> Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Свойства этого расширителя также можно изменить с помощью клиентского кода JavaScript.

## <a name="overview"></a>Обзор

Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Свойства этого расширителя также можно изменить с помощью клиентского кода JavaScript.

## <a name="steps"></a>Шаги

Код начинается с панели, содержащей несколько строк текста:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

Связанный класс CSS предоставляет панели хороший цвет фона:

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

`DropShadowExtender` добавляется для расширения панели с эффектом тени, для параметра Opacity устанавливается значение 50%:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

Затем элемент управления `ScriptManager` AJAX ASP.NET позволяет набору элементов управления работать:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

Другая панель содержит две ссылки JavaScript для настройки непрозрачности тени. ссылка «минус» уменьшает прозрачность тени, а ссылка «плюс» увеличивает ее.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

После этого функция JavaScript `changeOpacity()` должна сначала найти элемент управления `DropShadowExtender` на странице. ASP.NET AJAX определяет метод `$find()` для точности этой задачи. Затем метод `get_Opacity()` извлекает текущую непрозрачность, метод `set_Opacity()` задает его. Затем код JavaScript помещает текущее значение непрозрачности в элемент `<label>`:

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

[![на стороне клиента изменяется непрозрачность](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)

Непрозрачность изменяется на стороне клиента ([щелкните, чтобы просмотреть изображение с полным размером](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](adjusting-the-z-index-of-a-dropshadow-vb.md)
