---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: Использование обратных передач с помощью элемента управления ReorderList (C#) | Документация Майкрософт
author: wenz
description: Элемент управления ReorderList в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания. Каждый раз, когда отображается список po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 6f8f74b74080104980e1db866d695fe7c6d9d5fc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393357"
---
# <a name="using-postbacks-with-reorderlist-c"></a>Использование обратных передач с помощью элемента управления ReorderList (C#)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)

> Элемент управления ReorderList в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания. Всякий раз, когда отображается список обратную передачу должны сообщить серверу изменения.


## <a name="overview"></a>Обзор

`ReorderList` Элемент управления в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания. Всякий раз, когда отображается список обратную передачу должны сообщить серверу изменения.

## <a name="steps"></a>Шаги

Существует несколько источников данных для `ReorderList` элемента управления. Одним является использование `XmlDataSource` управления:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

Чтобы привязать этот XML-код для `ReorderList` должно иметь значение управления с обратной передачей, следующие атрибуты:

- `DataSourceID`: Идентификатор источника данных
- `SortOrderField`: Свойство, чтобы выполнить сортировку по
- `AllowReorder`: Следует ли разрешить пользователю изменять порядок элементов списка
- `PostBackOnReorder`: Нужно ли создавать обратной передачи, каждый раз, когда изменяется список

Ниже приведен соответствующий разметки для элемента управления.

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

В рамках `ReorderList` может привязать элемент управления, определенных данных из источника данных с помощью `Eval()` метод:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

В случайном положении на странице метку хранения информации, когда произошло последнее изменение порядка:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

Эта метка заполняется с текстом в коде на сервере обработки обратной передачи:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

Наконец, для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления должны быть размещены на странице:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]


[![EИзменение порядка ACH инициирует обратную передачу](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

Каждый переупорядочения инициирует обратную передачу ([Просмотр полноразмерного изображения](using-postbacks-with-reorderlist-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Далее](drag-and-drop-via-reorderlist-cs.md)
