---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: Использование ModalPopup с элементом управления Repeater (C#) | Документация Майкрософт
author: wenz
description: Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Также можно использовать этот отдача...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 980f023c9e8256ad5323aaa6cbb6918b04e18974
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598936"
---
# <a name="using-modalpopup-with-a-repeater-control-c"></a>Использование ModalPopup с элементом управления Repeater (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)

> Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Этот элемент управления также можно использовать в элементе Repeater.

## <a name="overview"></a>Обзор

Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Этот элемент управления также можно использовать в элементе Repeater.

## <a name="steps"></a>Шаги

Во-первых, требуется источник данных. В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition. База данных является необязательной частью установки Visual Studio (включая экспресс-выпуск) и доступна как отдельная загрузка в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). База данных AdventureWorks входит в состав примеров SQL Server 2005 и образцов баз данных (скачать в [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединить файл базы данных `AdventureWorks.mdf`. В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию. Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных. Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

Затем добавьте источник данных на страницу. Чтобы использовать ограниченный объем данных, мы выбираем только первые пять записей в таблице «Поставщик» базы данных AdventureWorks. При использовании помощника Visual Studio для создания источника данных обратите внимание, что ошибка в текущей версии не предшествует имени таблицы (`Vendor`) с `Purchasing`. В следующей разметке показан правильный синтаксис:

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

Затем добавьте панель, которая выступает в качестве модального всплывающего окна. Он содержит элемент управления `Button` для повторного закрытия всплывающего окна:

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

Чтобы всплывающее окно работало в элементе управления Repeater, `ModalPopupExtender` должен быть размещен в `<ItemTemplate>` разделе Repeater. Таким образом, панель находится за пределами Repeater, но расширитель находится внутри. Ниже приведена разметка для Repeater:

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

Затем каждый элемент в источнике данных отображается с кнопкой рядом с ней, запускающей модальное всплывающее окно.

[![для каждой записи источника данных можно активировать модальное всплывающее окно](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)

Модальное всплывающее окно можно активировать для каждой записи источника данных ([щелкните, чтобы просмотреть изображение с полным размером](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](launching-a-modal-popup-window-from-server-code-cs.md)
> [Вперед](handling-postbacks-from-a-modalpopup-cs.md)
