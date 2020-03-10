---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: Перетаскивание с помощью элемента управления ReorderList (VB) | Документация Майкрософт
author: wenz
description: /дата-акцесс/туториалс/мастер-детаил-усинг-а-буллетед-лист-оф-мастер-рекордс-вис-а-детаилс-даталист-вб
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 3f7c5749053d8bf587467fb1939fca05ce2872a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446088"
---
# <a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="791f8-103">Перетаскивание с помощью элемента управления ReorderList (VB)</span><span class="sxs-lookup"><span data-stu-id="791f8-103">Drag and Drop via ReorderList (VB)</span></span>

<span data-ttu-id="791f8-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="791f8-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="791f8-105">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="791f8-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="791f8-106">Элемент управления элемента управления ReorderList в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="791f8-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="791f8-107">Текущий порядок списка должен быть сохранен на сервере.</span><span class="sxs-lookup"><span data-stu-id="791f8-107">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="791f8-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="791f8-108">Overview</span></span>

<span data-ttu-id="791f8-109">Элемент управления `ReorderList` в наборе средств AJAX Control Toolkit предоставляет список, который пользователь может переупорядочить с помощью перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="791f8-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="791f8-110">Текущий порядок списка должен быть сохранен на сервере.</span><span class="sxs-lookup"><span data-stu-id="791f8-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="791f8-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="791f8-111">Steps</span></span>

<span data-ttu-id="791f8-112">Элемент управления `ReorderList` поддерживает привязку данных из базы данных к списку.</span><span class="sxs-lookup"><span data-stu-id="791f8-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="791f8-113">Что самое главное, он также поддерживает запись изменений в порядок элемента списка обратно в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="791f8-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="791f8-114">В этом образце в качестве хранилища данных используется Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="791f8-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="791f8-115">База данных — это необязательная (и бесплатная) часть установки Visual Studio, включая экспресс-выпуск.</span><span class="sxs-lookup"><span data-stu-id="791f8-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="791f8-116">Он также доступен в виде отдельной загрузки в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="791f8-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="791f8-117">В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="791f8-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="791f8-118">Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.</span><span class="sxs-lookup"><span data-stu-id="791f8-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="791f8-119">Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="791f8-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="791f8-120">Подключитесь к серверу, дважды щелкните `Databases` и создайте новую базу данных (щелкните правой кнопкой мыши и выберите `New Database`) с именем `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="791f8-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="791f8-121">В этой базе данных создайте новую таблицу с именем `AJAX` со следующими четырьмя столбцами:</span><span class="sxs-lookup"><span data-stu-id="791f8-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="791f8-122">`id` (первичный ключ, целое число, идентификатор, не NULL)</span><span class="sxs-lookup"><span data-stu-id="791f8-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="791f8-123">`char` (char (1), NULL)</span><span class="sxs-lookup"><span data-stu-id="791f8-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="791f8-124">`description` (varchar (50), NULL)</span><span class="sxs-lookup"><span data-stu-id="791f8-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="791f8-125">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="791f8-125">`position` (int, NULL)</span></span>

<span data-ttu-id="791f8-126">[![макета таблицы AJAX](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="791f8-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="791f8-127">Макет таблицы AJAX ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="791f8-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>

<span data-ttu-id="791f8-128">Затем заполните таблицу парой значений.</span><span class="sxs-lookup"><span data-stu-id="791f8-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="791f8-129">Обратите внимание, что столбец `position` содержит порядок сортировки элементов.</span><span class="sxs-lookup"><span data-stu-id="791f8-129">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="791f8-130">[![начальных данных в таблице AJAX](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="791f8-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="791f8-131">Начальные данные в таблице AJAX ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="791f8-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>

<span data-ttu-id="791f8-132">Следующий шаг требует создания элемента управления `SqlDataSource` для взаимодействия с новой базой данных и ее таблицей.</span><span class="sxs-lookup"><span data-stu-id="791f8-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="791f8-133">Источник данных должен поддерживать команды SQL `SELECT` и `UPDATE`.</span><span class="sxs-lookup"><span data-stu-id="791f8-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="791f8-134">При последующем изменении порядка элементов списка элемент управления `ReorderList` автоматически отправляет два значения в команду `Update` источника данных: новую точку и идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="791f8-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="791f8-135">Таким образом, источнику данных требуется `<UpdateParameters>` раздел для этих двух значений:</span><span class="sxs-lookup"><span data-stu-id="791f8-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="791f8-136">Элементу управления `ReorderList` необходимо задать следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="791f8-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="791f8-137">`AllowReorder`: можно ли переупорядочивать элементы списка</span><span class="sxs-lookup"><span data-stu-id="791f8-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="791f8-138">`DataSourceID`: идентификатор источника данных</span><span class="sxs-lookup"><span data-stu-id="791f8-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="791f8-139">`DataKeyField`: имя первичного ключевого столбца в источнике данных</span><span class="sxs-lookup"><span data-stu-id="791f8-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="791f8-140">`SortOrderField`: столбец источника данных, предоставляющий порядок сортировки для элементов списка.</span><span class="sxs-lookup"><span data-stu-id="791f8-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="791f8-141">В разделах `<DragHandleTemplate>` и `<ItemTemplate>` макет списка можно настраивать.</span><span class="sxs-lookup"><span data-stu-id="791f8-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="791f8-142">Кроме того, привязка данных возможна с помощью метода `Eval()`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="791f8-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="791f8-143">Следующие сведения о стиле CSS (указанные в разделе `<DragHandleTemplate>` элемента управления `ReorderList`) гарантирует, что указатель мыши изменится соответствующим образом при наведении на маркер перетаскивания:</span><span class="sxs-lookup"><span data-stu-id="791f8-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="791f8-144">Наконец, элемент управления `ScriptManager` инициализирует ASP.NET AJAX для страницы:</span><span class="sxs-lookup"><span data-stu-id="791f8-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="791f8-145">Запустите этот пример в браузере и разместите элементы списка чуть выше.</span><span class="sxs-lookup"><span data-stu-id="791f8-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="791f8-146">Затем перезагрузите страницу и (или) просмотрите базу данных.</span><span class="sxs-lookup"><span data-stu-id="791f8-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="791f8-147">Измененные позиции сохранены и также отражаются по значениям в столбце `position` базы данных, а все без кода — с помощью разметки.</span><span class="sxs-lookup"><span data-stu-id="791f8-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="791f8-148">[![данные в базе данных изменяются в соответствии с новым порядком элементов списка](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="791f8-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="791f8-149">Данные в базе данных изменяются в соответствии с новым порядком элементов списка ([щелкните, чтобы просмотреть изображение с полным размером](drag-and-drop-via-reorderlist-vb/_static/image9.png)).</span><span class="sxs-lookup"><span data-stu-id="791f8-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="791f8-150">Назад</span><span class="sxs-lookup"><span data-stu-id="791f8-150">Previous</span></span>](using-postbacks-with-reorderlist-vb.md)
