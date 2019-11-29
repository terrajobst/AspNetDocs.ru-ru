---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: Использование обратных передач с элемента управления ReorderList (VB) | Документация Майкрософт
author: wenz
description: Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Каждый раз, когда список переупорядочивается, PO...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 5d6075e40df2c32df6c0d801243eff98fa7790b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611373"
---
# <a name="using-postbacks-with-reorderlist-vb"></a>Использование обратных передач с помощью элемента управления ReorderList (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)

> Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Каждый раз, когда список переупорядочивается, обратная передача сообщает серверу об изменении.

## <a name="overview"></a>Обзор

Элемент управления `ReorderList` в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Каждый раз, когда список переупорядочивается, обратная передача сообщает серверу об изменении.

## <a name="steps"></a>Шаги

Существует несколько источников данных для элемента управления `ReorderList`. Один из них — использовать элемент управления `XmlDataSource`:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

Чтобы привязать этот XML-код к элементу управления `ReorderList` и включить обратные передачи, необходимо задать следующие атрибуты:

- `DataSourceID`: идентификатор источника данных
- `SortOrderField`: свойство для сортировки
- `AllowReorder`: следует ли разрешить пользователю изменять порядок элементов списка
- `PostBackOnReorder`: следует ли создавать обратную передачу при переупорядочении списка

Ниже приведена соответствующая разметка для элемента управления.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

В элементе управления `ReorderList` определенные данные из источника данных могут быть привязаны с помощью метода `Eval()`:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

В произвольной позиции на странице метка будет содержать сведения о последнем переупорядочении:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

Эта метка заполняется текстом в коде на стороне сервера, обрабатывая обратную передачу:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

Наконец, чтобы активировать функциональные возможности ASP.NET AJAX и набора средств управления, `ScriptManager` элемент управления должен быть размещен на странице:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

[![каждый Переупорядочение активирует обратную передачу](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

Каждый Переупорядочение активирует обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-postbacks-with-reorderlist-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](drag-and-drop-via-reorderlist-cs.md)
> [Вперед](drag-and-drop-via-reorderlist-vb.md)
