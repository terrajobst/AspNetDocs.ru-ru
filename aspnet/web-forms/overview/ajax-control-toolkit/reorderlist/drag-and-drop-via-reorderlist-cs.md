---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: Перетаскивание с помощью элемента управления ReorderList (C#) | Документация Майкрософт
author: wenz
description: Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Текущий порядок списка должен быть...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 2fc6d55a290cbb58bea36d8145d814e337bbd931
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611470"
---
# <a name="drag-and-drop-via-reorderlist-c"></a>Перетаскивание с помощью элемента управления ReorderList (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Текущий порядок списка должен быть сохранен на сервере.

## <a name="overview"></a>Обзор

Элемент управления `ReorderList` в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания. Текущий порядок списка должен быть сохранен на сервере.

## <a name="steps"></a>Шаги

Элемент управления `ReorderList` поддерживает привязку данных из базы данных к списку. Что самое главное, он также поддерживает запись изменений в порядок элемента списка обратно в хранилище данных.

В этом образце в качестве хранилища данных используется Microsoft SQL Server 2005 Express Edition. База данных — это необязательная (и бесплатная) часть установки Visual Studio, включая экспресс-выпуск. Он также доступен в виде отдельной загрузки в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию. Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.

Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ). Подключитесь к серверу, дважды щелкните `Databases` и создайте новую базу данных (щелкните правой кнопкой мыши и выберите `New Database`) с именем `Tutorials`.

В этой базе данных создайте новую таблицу с именем `AJAX` со следующими четырьмя столбцами:

- `id` (первичный ключ, целое число, идентификатор, не NULL)
- `char` (char (1), NULL)
- `description` (varchar (50), NULL)
- `position` (int, NULL)

[![макета таблицы AJAX](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

Макет таблицы AJAX ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-cs/_static/image3.png))

Затем заполните таблицу парой значений. Обратите внимание, что столбец `position` содержит порядок сортировки элементов.

[![начальных данных в таблице AJAX](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

Начальные данные в таблице AJAX ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-cs/_static/image6.png))

Следующий шаг требует создания элемента управления `SqlDataSource` для взаимодействия с новой базой данных и ее таблицей. Источник данных должен поддерживать команды SQL `SELECT` и `UPDATE`. При последующем изменении порядка элементов списка элемент управления `ReorderList` автоматически отправляет два значения в команду `Update` источника данных: новую точку и идентификатор элемента. Таким образом, источнику данных требуется `<UpdateParameters>` раздел для этих двух значений:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

Элементу управления `ReorderList` необходимо задать следующие атрибуты:

- `AllowReorder`: можно ли переупорядочивать элементы списка
- `DataSourceID`: идентификатор источника данных
- `DataKeyField`: имя первичного ключевого столбца в источнике данных
- `SortOrderField`: столбец источника данных, предоставляющий порядок сортировки для элементов списка.

В разделах `<DragHandleTemplate>` и `<ItemTemplate>` макет списка можно настраивать. Кроме того, привязка данных возможна с помощью метода `Eval()`, как показано ниже:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

Следующие сведения о стиле CSS (указанные в разделе `<DragHandleTemplate>` элемента управления `ReorderList`) гарантирует, что указатель мыши изменится соответствующим образом при наведении на маркер перетаскивания:

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

Наконец, элемент управления `ScriptManager` инициализирует ASP.NET AJAX для страницы:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

Запустите этот пример в браузере и разместите элементы списка чуть выше. Затем перезагрузите страницу и (или) просмотрите базу данных. Измененные позиции сохранены и также отражаются по значениям в столбце `position` базы данных, а все без кода — с помощью разметки.

[![данные в базе данных изменяются в соответствии с новым порядком элементов списка](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

Данные в базе данных изменяются в соответствии с новым порядком элементов списка ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-cs/_static/image9.png)).

> [!div class="step-by-step"]
> [Назад](using-postbacks-with-reorderlist-cs.md)
> [Вперед](using-postbacks-with-reorderlist-vb.md)
