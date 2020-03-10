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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466836"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a>Использование HoverMenu с элементом управления Repeater (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)

> Элемент управления HoverMenu в наборе AJAX Control Toolkit предоставляет простой всплывающий экран: при наведении указателя мыши на элемент в указанной позиции появляется всплывающее окно. Этот элемент управления также можно использовать в элементе Repeater.

## <a name="overview"></a>Обзор

Элемент управления `HoverMenu` в наборе средств AJAX Control Toolkit предоставляет простой всплывающий экран: при наведении указателя мыши на элемент в заданной позиции появляется всплывающее окно. Этот элемент управления также можно использовать в элементе Repeater.

## <a name="steps"></a>Шаги

Во-первых, требуется источник данных. В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition. База данных является необязательной частью установки Visual Studio (включая экспресс-выпуск) и доступна как отдельная загрузка в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). База данных AdventureWorks входит в состав примеров SQL Server 2005 и образцов баз данных (скачать в [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединить файл базы данных `AdventureWorks.mdf`.

В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию. Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

Затем добавьте источник данных на страницу. Чтобы использовать ограниченный объем данных, мы выбираем только первые пять записей в таблице «Поставщик» базы данных AdventureWorks. При использовании помощника Visual Studio для создания источника данных обратите внимание, что ошибка в текущей версии не предшествует имени таблицы (`Vendor`) с `Purchasing`. В следующей разметке показан правильный синтаксис:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

Затем добавьте панель, которая выступает в качестве модального всплывающего окна:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

Теперь `HoverMenuExtender` поступает в игру. Чтобы каждый элемент в источнике данных получит собственное всплывающее окно, расширитель должен быть размещен в `<ItemTemplate>` разделе Repeater. Ниже приводится пример разметки:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

Теперь каждый элемент в источнике данных отображает всплывающее окно справа (`PopupPosition` атрибут) после задержки 50 миллисекунд (атрибут`PopDelay`).

[![наведение указателя мыши рядом с каждым элементом в элементе Repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

Всплывающее меню отображается рядом с каждым элементом в элементе Repeater ([щелкните, чтобы просмотреть изображение с полным размером](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Дальше](using-hovermenu-with-a-repeater-control-vb.md)
