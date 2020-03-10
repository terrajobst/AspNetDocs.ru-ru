---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: Управление свойствами DropShadow из клиентского кода (C#) | Документация Майкрософт
author: wenz
description: Настройка интерфейса правки элемента управления DataList
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 790f0d881e43518600968d6c175d4eaa53d0e5f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497430"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a>Обработка свойств DropShadow из клиентского кода (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)

> Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Свойства этого расширителя также можно изменить с помощью клиентского кода JavaScript.

## <a name="overview"></a>Обзор

Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Свойства этого расширителя также можно изменить с помощью клиентского кода JavaScript.

## <a name="steps"></a>Шаги

Код начинается с панели, содержащей несколько строк текста:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

Связанный класс CSS предоставляет панели хороший цвет фона:

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

`DropShadowExtender` добавляется для расширения панели с эффектом тени, для параметра Opacity устанавливается значение 50%:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

Затем элемент управления `ScriptManager` AJAX ASP.NET позволяет набору элементов управления работать:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

Другая панель содержит две ссылки JavaScript для настройки непрозрачности тени. ссылка «минус» уменьшает прозрачность тени, а ссылка «плюс» увеличивает ее.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

После этого функция JavaScript `changeOpacity()` должна сначала найти элемент управления `DropShadowExtender` на странице. ASP.NET AJAX определяет метод `$find()` для точности этой задачи. Затем метод `get_Opacity()` извлекает текущую непрозрачность, метод `set_Opacity()` задает его. Затем код JavaScript помещает текущее значение непрозрачности в элемент `<label>`:

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]

[![на стороне клиента изменяется непрозрачность](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)

Непрозрачность изменяется на стороне клиента ([щелкните, чтобы просмотреть изображение с полным размером](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [Вперед](adjusting-the-z-index-of-a-dropshadow-vb.md)
