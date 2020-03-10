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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446010"
---
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="9907c-104">Перетаскивание с помощью элемента управления ReorderList (C#)</span><span class="sxs-lookup"><span data-stu-id="9907c-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="9907c-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9907c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9907c-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="9907c-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="9907c-107">Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="9907c-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="9907c-108">Текущий порядок списка должен быть сохранен на сервере.</span><span class="sxs-lookup"><span data-stu-id="9907c-108">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="9907c-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="9907c-109">Overview</span></span>

<span data-ttu-id="9907c-110">Элемент управления `ReorderList` в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="9907c-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="9907c-111">Текущий порядок списка должен быть сохранен на сервере.</span><span class="sxs-lookup"><span data-stu-id="9907c-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="9907c-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="9907c-112">Steps</span></span>

<span data-ttu-id="9907c-113">Элемент управления `ReorderList` поддерживает привязку данных из базы данных к списку.</span><span class="sxs-lookup"><span data-stu-id="9907c-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="9907c-114">Что самое главное, он также поддерживает запись изменений в порядок элемента списка обратно в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="9907c-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="9907c-115">В этом образце в качестве хранилища данных используется Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="9907c-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="9907c-116">База данных — это необязательная (и бесплатная) часть установки Visual Studio, включая экспресс-выпуск.</span><span class="sxs-lookup"><span data-stu-id="9907c-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="9907c-117">Он также доступен в виде отдельной загрузки в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="9907c-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="9907c-118">В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9907c-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="9907c-119">Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.</span><span class="sxs-lookup"><span data-stu-id="9907c-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="9907c-120">Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="9907c-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="9907c-121">Подключитесь к серверу, дважды щелкните `Databases` и создайте новую базу данных (щелкните правой кнопкой мыши и выберите `New Database`) с именем `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="9907c-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="9907c-122">В этой базе данных создайте новую таблицу с именем `AJAX` со следующими четырьмя столбцами:</span><span class="sxs-lookup"><span data-stu-id="9907c-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="9907c-123">`id` (первичный ключ, целое число, идентификатор, не NULL)</span><span class="sxs-lookup"><span data-stu-id="9907c-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="9907c-124">`char` (char (1), NULL)</span><span class="sxs-lookup"><span data-stu-id="9907c-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="9907c-125">`description` (varchar (50), NULL)</span><span class="sxs-lookup"><span data-stu-id="9907c-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="9907c-126">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="9907c-126">`position` (int, NULL)</span></span>

<span data-ttu-id="9907c-127">[![макета таблицы AJAX](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9907c-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="9907c-128">Макет таблицы AJAX ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9907c-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>

<span data-ttu-id="9907c-129">Затем заполните таблицу парой значений.</span><span class="sxs-lookup"><span data-stu-id="9907c-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="9907c-130">Обратите внимание, что столбец `position` содержит порядок сортировки элементов.</span><span class="sxs-lookup"><span data-stu-id="9907c-130">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="9907c-131">[![начальных данных в таблице AJAX](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="9907c-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="9907c-132">Начальные данные в таблице AJAX ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9907c-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>

<span data-ttu-id="9907c-133">Следующий шаг требует создания элемента управления `SqlDataSource` для взаимодействия с новой базой данных и ее таблицей.</span><span class="sxs-lookup"><span data-stu-id="9907c-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="9907c-134">Источник данных должен поддерживать команды SQL `SELECT` и `UPDATE`.</span><span class="sxs-lookup"><span data-stu-id="9907c-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="9907c-135">При последующем изменении порядка элементов списка элемент управления `ReorderList` автоматически отправляет два значения в команду `Update` источника данных: новую точку и идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="9907c-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="9907c-136">Таким образом, источнику данных требуется `<UpdateParameters>` раздел для этих двух значений:</span><span class="sxs-lookup"><span data-stu-id="9907c-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="9907c-137">Элементу управления `ReorderList` необходимо задать следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="9907c-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="9907c-138">`AllowReorder`: можно ли переупорядочивать элементы списка</span><span class="sxs-lookup"><span data-stu-id="9907c-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="9907c-139">`DataSourceID`: идентификатор источника данных</span><span class="sxs-lookup"><span data-stu-id="9907c-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="9907c-140">`DataKeyField`: имя первичного ключевого столбца в источнике данных</span><span class="sxs-lookup"><span data-stu-id="9907c-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="9907c-141">`SortOrderField`: столбец источника данных, предоставляющий порядок сортировки для элементов списка.</span><span class="sxs-lookup"><span data-stu-id="9907c-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="9907c-142">В разделах `<DragHandleTemplate>` и `<ItemTemplate>` макет списка можно настраивать.</span><span class="sxs-lookup"><span data-stu-id="9907c-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="9907c-143">Кроме того, привязка данных возможна с помощью метода `Eval()`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9907c-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="9907c-144">Следующие сведения о стиле CSS (указанные в разделе `<DragHandleTemplate>` элемента управления `ReorderList`) гарантирует, что указатель мыши изменится соответствующим образом при наведении на маркер перетаскивания:</span><span class="sxs-lookup"><span data-stu-id="9907c-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="9907c-145">Наконец, элемент управления `ScriptManager` инициализирует ASP.NET AJAX для страницы:</span><span class="sxs-lookup"><span data-stu-id="9907c-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="9907c-146">Запустите этот пример в браузере и разместите элементы списка чуть выше.</span><span class="sxs-lookup"><span data-stu-id="9907c-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="9907c-147">Затем перезагрузите страницу и (или) просмотрите базу данных.</span><span class="sxs-lookup"><span data-stu-id="9907c-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="9907c-148">Измененные позиции сохранены и также отражаются по значениям в столбце `position` базы данных, а все без кода — с помощью разметки.</span><span class="sxs-lookup"><span data-stu-id="9907c-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="9907c-149">[![данные в базе данных изменяются в соответствии с новым порядком элементов списка](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="9907c-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="9907c-150">Данные в базе данных изменяются в соответствии с новым порядком элементов списка ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-cs/_static/image9.png)).</span><span class="sxs-lookup"><span data-stu-id="9907c-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9907c-151">[Назад](using-postbacks-with-reorderlist-cs.md)
> [Вперед](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9907c-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
