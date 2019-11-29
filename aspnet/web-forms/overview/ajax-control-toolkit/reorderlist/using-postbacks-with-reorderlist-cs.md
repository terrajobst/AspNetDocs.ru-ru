---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: Использование обратных передач с элемента управления ReorderList (C#) | Документация Майкрософт
author: wenz
description: Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Каждый раз, когда список переупорядочивается, PO...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: f83201fc6fd458e730b6bb5ffee184d303b52e90
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611391"
---
# <a name="using-postbacks-with-reorderlist-c"></a>Использование обратных передач с помощью элемента управления ReorderList (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)

> Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Каждый раз, когда список переупорядочивается, обратная передача сообщает серверу об изменении.

## <a name="overview"></a>Обзор

Элемент управления `ReorderList` в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Каждый раз, когда список переупорядочивается, обратная передача сообщает серверу об изменении.

## <a name="steps"></a>Шаги

Существует несколько источников данных для элемента управления `ReorderList`. Один из них — использовать элемент управления `XmlDataSource`:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

Чтобы привязать этот XML-код к элементу управления `ReorderList` и включить обратные передачи, необходимо задать следующие атрибуты:

- `DataSourceID`: идентификатор источника данных
- `SortOrderField`: свойство для сортировки
- `AllowReorder`: следует ли разрешить пользователю изменять порядок элементов списка
- `PostBackOnReorder`: следует ли создавать обратную передачу при переупорядочении списка

Ниже приведена соответствующая разметка для элемента управления.

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

В элементе управления `ReorderList` определенные данные из источника данных могут быть привязаны с помощью метода `Eval()`:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

В произвольной позиции на странице метка будет содержать сведения о последнем переупорядочении:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

Эта метка заполняется текстом в коде на стороне сервера, обрабатывая обратную передачу:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

Наконец, чтобы активировать функциональные возможности ASP.NET AJAX и набора средств управления, `ScriptManager` элемент управления должен быть размещен на странице:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

[![каждый Переупорядочение активирует обратную передачу](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

Каждый Переупорядочение активирует обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-postbacks-with-reorderlist-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Вперед](drag-and-drop-via-reorderlist-cs.md)
