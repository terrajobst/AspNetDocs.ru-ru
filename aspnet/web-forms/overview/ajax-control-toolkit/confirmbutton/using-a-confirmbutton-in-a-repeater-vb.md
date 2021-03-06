---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: Использование ConfirmButton в элементе Repeater (VB) | Документация Майкрософт
author: wenz
description: Расширитель ConfirmButton в наборе средств AJAX Control Toolkit создает всплывающее окно да/нет при нажатии пользователем кнопки (включая элемент управления LinkButton). Только если да —...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 001233d866d8a731d93d6900f714cd2060f3d08c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497544"
---
# <a name="using-a-confirmbutton-in-a-repeater-vb"></a>Использование ConfirmButton в элементе управления Repeater (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)

> Расширитель ConfirmButton в наборе средств AJAX Control Toolkit создает всплывающее окно да/нет при нажатии пользователем кнопки (включая элемент управления LinkButton). Действие кнопки выполняется, только если выбрано значение Да, и в противном случае — отменено. Это также возможно в элементе Repeater.

## <a name="overview"></a>Обзор

Расширитель ConfirmButton в наборе средств AJAX Control Toolkit создает всплывающее окно да/нет при нажатии пользователем кнопки (включая элемент управления LinkButton). Действие кнопки выполняется, только если выбрано значение Да, и в противном случае — отменено. Это также возможно в элементе Repeater.

## <a name="steps"></a>Шаги

Во-первых, требуется источник данных. В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition. База данных является необязательной частью установки Visual Studio (включая экспресс-выпуск) и доступна как отдельная загрузка в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). База данных AdventureWorks входит в состав примеров SQL Server 2005 и образцов баз данных (скачать в [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединить файл базы данных `AdventureWorks.mdf`.

В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию. Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

Затем требуется источник данных. Для простоты извлекаются только первые пять записей в таблице поставщиков AdventureWorks. Обратите внимание, что при использовании мастера Visual Studio для создания источника данных имя таблицы (`Vendors`) в настоящее время не имеет корректного префикса `Purchasing`. Ниже приведена правильная разметка.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

Затем этот источник данных можно использовать в элементе Repeater. Как обычно, метод `DataBinder.Eval()` извлекает данные из источника данных. Затем элемент управления `ConfirmButtonExtender` должен быть помещен в раздел `<ItemTemplate>` Repeater, чтобы он появился для каждой записи в источнике данных.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]

[![рядом с каждой записью из источника данных появляется кнопка подтвердить.](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)

Кнопка подтверждения отображается рядом с каждой записью из источника данных ([щелкните, чтобы просмотреть изображение с полным размером](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](using-a-confirmbutton-in-a-repeater-cs.md)
