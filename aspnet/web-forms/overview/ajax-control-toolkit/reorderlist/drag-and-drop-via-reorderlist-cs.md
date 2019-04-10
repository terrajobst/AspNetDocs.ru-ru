---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: Перетаскивание с помощью элемента управления ReorderList (C#) | Документация Майкрософт
author: wenz
description: Элемент управления ReorderList в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания. Текущий порядок элементов в списке должны...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 988aa9252cfd93067888734006e6003347f1fb5e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59414755"
---
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="cc451-104">Перетаскивание с помощью элемента управления ReorderList (C#)</span><span class="sxs-lookup"><span data-stu-id="cc451-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="cc451-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cc451-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cc451-106">[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="cc451-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="cc451-107">Элемент управления ReorderList в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="cc451-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="cc451-108">Текущий порядок элементов в списке должны быть сохранены на сервере.</span><span class="sxs-lookup"><span data-stu-id="cc451-108">The current order of the list shall be persisted on the server.</span></span>


## <a name="overview"></a><span data-ttu-id="cc451-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="cc451-109">Overview</span></span>

<span data-ttu-id="cc451-110">`ReorderList` Элемент управления в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="cc451-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="cc451-111">Текущий порядок элементов в списке должны быть сохранены на сервере.</span><span class="sxs-lookup"><span data-stu-id="cc451-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="cc451-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="cc451-112">Steps</span></span>

<span data-ttu-id="cc451-113">`ReorderList` Элемент управления поддерживает привязку данных из базы данных в список.</span><span class="sxs-lookup"><span data-stu-id="cc451-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="cc451-114">Самое главное она также поддерживает запись изменений порядку элемент списка в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="cc451-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="cc451-115">Этот образец использует Microsoft SQL Server 2005 Express Edition в качестве хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="cc451-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="cc451-116">Базы данных является необязательным (и бесплатной) часть установки Visual Studio, включая экспресс-выпуск.</span><span class="sxs-lookup"><span data-stu-id="cc451-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="cc451-117">Эта схема также доступна для загрузки в разделе [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="cc451-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="cc451-118">В этом примере мы предполагаем, что экземпляр SQL Server 2005 Express Edition называется `SQLEXPRESS` и находится на одном компьютере с веб-сервера; это также настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cc451-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="cc451-119">Если настройки отличаются, вам нужно адаптировать сведения о соединении для базы данных.</span><span class="sxs-lookup"><span data-stu-id="cc451-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="cc451-120">Самый простой способ установить базу данных, — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="cc451-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="cc451-121">Подключитесь к серверу, дважды щелкните `Databases` и создать новую базу данных (щелкните правой кнопкой мыши и выберите `New Database`) вызывается `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="cc451-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="cc451-122">В этой базе данных, создать новую таблицу с именем `AJAX` с следующие четыре столбца:</span><span class="sxs-lookup"><span data-stu-id="cc451-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- `id` <span data-ttu-id="cc451-123">(первичный ключ, integer, удостоверение, not NULL)</span><span class="sxs-lookup"><span data-stu-id="cc451-123">(primary key, integer, identity, not NULL)</span></span>
- `char` <span data-ttu-id="cc451-124">(char(1), NULL)</span><span class="sxs-lookup"><span data-stu-id="cc451-124">(char(1), NULL)</span></span>
- `description` <span data-ttu-id="cc451-125">(varchar(50), NULL)</span><span class="sxs-lookup"><span data-stu-id="cc451-125">(varchar(50), NULL)</span></span>
- `position` <span data-ttu-id="cc451-126">(int, NULL)</span><span class="sxs-lookup"><span data-stu-id="cc451-126">(int, NULL)</span></span>


[![T<span data-ttu-id="cc451-127">макет таблицы AJAX HE]</span><span class="sxs-lookup"><span data-stu-id="cc451-127">he layout of the AJAX table]</span></span>(drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

<span data-ttu-id="cc451-128">Макет таблицы AJAX ([Просмотр полноразмерного изображения](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cc451-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>


<span data-ttu-id="cc451-129">Затем введите таблицы с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="cc451-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="cc451-130">Обратите внимание, что `position` столбец содержит порядок сортировки элементов.</span><span class="sxs-lookup"><span data-stu-id="cc451-130">Note that the `position` column holds the sort order of the elements.</span></span>


[![T<span data-ttu-id="cc451-131">он начальные данные в таблице AJAX]</span><span class="sxs-lookup"><span data-stu-id="cc451-131">he initial data in the AJAX table]</span></span>(drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

<span data-ttu-id="cc451-132">Начальные данные в таблице AJAX ([Просмотр полноразмерного изображения](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="cc451-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>


<span data-ttu-id="cc451-133">Для следующего шага требуется для создания `SqlDataSource` управления для взаимодействия с новой базы данных и соответствующей таблицей.</span><span class="sxs-lookup"><span data-stu-id="cc451-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="cc451-134">Источник данных должен поддерживать `SELECT` и `UPDATE` команды SQL.</span><span class="sxs-lookup"><span data-stu-id="cc451-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="cc451-135">При последующем изменении порядок элементов списка `ReorderList` элемент управления автоматически отправляет два значения в источник данных `Update` команда: новое положение и идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="cc451-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="cc451-136">Таким образом, источника данных требованиям `<UpdateParameters>` раздел для этих двух значений:</span><span class="sxs-lookup"><span data-stu-id="cc451-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="cc451-137">`ReorderList` Управления необходимо задать следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="cc451-137">The `ReorderList` control needs to set the following attributes:</span></span>

- `AllowReorder`<span data-ttu-id="cc451-138">: Можно ли упорядочить элементы списка</span><span class="sxs-lookup"><span data-stu-id="cc451-138">: Whether the list items may be rearranged</span></span>
- `DataSourceID`<span data-ttu-id="cc451-139">: Идентификатор источника данных</span><span class="sxs-lookup"><span data-stu-id="cc451-139">: The ID of the data source</span></span>
- `DataKeyField`<span data-ttu-id="cc451-140">: Имя столбца первичного ключа в источнике данных</span><span class="sxs-lookup"><span data-stu-id="cc451-140">: The name of the primary key column in the data source</span></span>
- `SortOrderField`<span data-ttu-id="cc451-141">: Исходный столбец данных, представляющий порядок сортировки для элементов списка</span><span class="sxs-lookup"><span data-stu-id="cc451-141">: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="cc451-142">В `<DragHandleTemplate>` и `<ItemTemplate>` разделы, макет списка может быть настроена.</span><span class="sxs-lookup"><span data-stu-id="cc451-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="cc451-143">Кроме того, возможна привязка данных с помощью `Eval()` метод, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="cc451-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="cc451-144">Сведения о стиле следующий код CSS (на который указывает ссылка в `<DragHandleTemplate>` раздел `ReorderList` управления) гарантирует, что указатель мыши изменяется соответствующим образом при его наведении маркер перетаскивания:</span><span class="sxs-lookup"><span data-stu-id="cc451-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="cc451-145">Наконец `ScriptManager` управления инициализирует ASP.NET AJAX для страницы:</span><span class="sxs-lookup"><span data-stu-id="cc451-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="cc451-146">Выполнить этот пример в браузере и немного изменить порядок элементов списка.</span><span class="sxs-lookup"><span data-stu-id="cc451-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="cc451-147">Затем перезагрузите страницу и/или посмотрите на базе данных.</span><span class="sxs-lookup"><span data-stu-id="cc451-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="cc451-148">Измененная позиций вестись и также отражаются по значениям в `position` столбца в базе данных, которые все без кода, вы можете просто с помощью разметки.</span><span class="sxs-lookup"><span data-stu-id="cc451-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>


[![T<span data-ttu-id="cc451-149">он данных в базу данных в соответствии с новой порядок элементов списка]</span><span class="sxs-lookup"><span data-stu-id="cc451-149">he data in the database changes according to the new list item order]</span></span>(drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

<span data-ttu-id="cc451-150">Элемент данных при изменениях базы данных в соответствии со списком нового заказа ([Просмотр полноразмерного изображения](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="cc451-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cc451-151">[Назад](using-postbacks-with-reorderlist-cs.md)
> [Вперед](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cc451-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
