---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Использование HoverMenu с элементом управления Repeater (C#) | Документация Майкрософт
author: wenz
description: 'Элемент управления HoverMenu в наборе AJAX Control Toolkit предоставляет простой всплывающий экран: при наведении указателя мыши на элемент появляется всплывающее окно с заданной кнопкой...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606692"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="3afd3-103">Использование HoverMenu с элементом управления Repeater (C#)</span><span class="sxs-lookup"><span data-stu-id="3afd3-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="3afd3-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3afd3-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3afd3-105">[Скачать код](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3afd3-105">[Download Code](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="3afd3-106">Элемент управления HoverMenu в наборе AJAX Control Toolkit предоставляет простой всплывающий экран: при наведении указателя мыши на элемент в указанной позиции появляется всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="3afd3-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="3afd3-107">Этот элемент управления также можно использовать в элементе Repeater.</span><span class="sxs-lookup"><span data-stu-id="3afd3-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="3afd3-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="3afd3-108">Overview</span></span>

<span data-ttu-id="3afd3-109">Элемент управления `HoverMenu` в наборе средств AJAX Control Toolkit предоставляет простой всплывающий экран: при наведении указателя мыши на элемент в заданной позиции появляется всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="3afd3-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="3afd3-110">Этот элемент управления также можно использовать в элементе Repeater.</span><span class="sxs-lookup"><span data-stu-id="3afd3-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="3afd3-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="3afd3-111">Steps</span></span>

<span data-ttu-id="3afd3-112">Во-первых, требуется источник данных.</span><span class="sxs-lookup"><span data-stu-id="3afd3-112">First of all, a data source is required.</span></span> <span data-ttu-id="3afd3-113">В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="3afd3-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="3afd3-114">База данных является необязательной частью установки Visual Studio (включая экспресс-выпуск) и доступна как отдельная загрузка в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="3afd3-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="3afd3-115">База данных AdventureWorks входит в состав примеров SQL Server 2005 и образцов баз данных (скачать в [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="3afd3-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="3afd3-116">Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединить файл базы данных `AdventureWorks.mdf`.</span><span class="sxs-lookup"><span data-stu-id="3afd3-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="3afd3-117">В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3afd3-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="3afd3-118">Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.</span><span class="sxs-lookup"><span data-stu-id="3afd3-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="3afd3-119">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):</span><span class="sxs-lookup"><span data-stu-id="3afd3-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="3afd3-120">Затем добавьте источник данных на страницу.</span><span class="sxs-lookup"><span data-stu-id="3afd3-120">Then, add a data source to the page.</span></span> <span data-ttu-id="3afd3-121">Чтобы использовать ограниченный объем данных, мы выбираем только первые пять записей в таблице «Поставщик» базы данных AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="3afd3-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="3afd3-122">При использовании помощника Visual Studio для создания источника данных обратите внимание, что ошибка в текущей версии не предшествует имени таблицы (`Vendor`) с `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="3afd3-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="3afd3-123">В следующей разметке показан правильный синтаксис:</span><span class="sxs-lookup"><span data-stu-id="3afd3-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="3afd3-124">Затем добавьте панель, которая выступает в качестве модального всплывающего окна:</span><span class="sxs-lookup"><span data-stu-id="3afd3-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="3afd3-125">Теперь `HoverMenuExtender` поступает в игру.</span><span class="sxs-lookup"><span data-stu-id="3afd3-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="3afd3-126">Чтобы каждый элемент в источнике данных получит собственное всплывающее окно, расширитель должен быть размещен в `<ItemTemplate>` разделе Repeater.</span><span class="sxs-lookup"><span data-stu-id="3afd3-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="3afd3-127">Ниже приводится пример разметки:</span><span class="sxs-lookup"><span data-stu-id="3afd3-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="3afd3-128">Теперь каждый элемент в источнике данных отображает всплывающее окно справа (`PopupPosition` атрибут) после задержки 50 миллисекунд (атрибут`PopDelay`).</span><span class="sxs-lookup"><span data-stu-id="3afd3-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="3afd3-129">[![наведение указателя мыши рядом с каждым элементом в элементе Repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3afd3-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="3afd3-130">Всплывающее меню отображается рядом с каждым элементом в элементе Repeater ([щелкните, чтобы просмотреть изображение с полным размером](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="3afd3-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3afd3-131">Вперед</span><span class="sxs-lookup"><span data-stu-id="3afd3-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
