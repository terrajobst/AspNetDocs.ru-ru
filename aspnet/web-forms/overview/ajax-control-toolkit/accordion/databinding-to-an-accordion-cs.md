---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: Привязка данных к гармошка (C#) | Документация Майкрософт
author: wenz
description: Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c28cc958a1de9844627ae16175a5aed153993a8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607263"
---
# <a name="databinding-to-an-accordion-c"></a>Привязка данных к Accordion (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)

> Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются внутри самой страницы, но привязка к источнику данных обеспечивает большую гибкость.

## <a name="overview"></a>Обзор

Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются внутри самой страницы, но привязка к источнику данных обеспечивает большую гибкость.

## <a name="steps"></a>Шаги

Во-первых, требуется источник данных. В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition. База данных является необязательной частью установки Visual Studio (включая экспресс-выпуск) и доступна как отдельная загрузка в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). База данных AdventureWorks входит в состав примеров SQL Server 2005 и образцов баз данных (скачать в [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединить файл базы данных `AdventureWorks.mdf`.

В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию. Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

Затем добавьте источник данных на страницу. Чтобы использовать ограниченный объем данных, мы выбираем только первые пять записей в таблице «Поставщик» базы данных AdventureWorks. При использовании помощника Visual Studio для создания источника данных обратите внимание, что ошибка в текущей версии не предшествует имени таблицы (`Vendor`) с `Purchasing`. В следующей разметке показан правильный синтаксис:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

Запомните имя (ID) источника данных. Эта очень идентификация затем должна использоваться в свойстве `DataSourceID` элемента управления "гармошка":

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

В элементе управления "гармошка" можно указать шаблоны для различных частей элемента управления, включая заголовок (`<HeaderTemplate>`) и содержимое (`<ContentTemplate>`). В этих элементах просто выводятся данные из источника данных с помощью метода `DataBinder.Eval()`:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

При загрузке страницы источник данных должен быть привязан к элементу Гармошка с помощью этого кода на стороне сервера:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

Чтобы завершить этот пример, необходимо определить два класса CSS, на которые ссылается элемент управления "гармошка" (в его свойствах `HeaderCssClass` и `ContentCssClass`). Добавьте следующую разметку в раздел `<head>` страницы:

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]

[![данные в элементе "гармошка" поступают непосредственно из источника данных](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)

Данные в элементе "гармошка" поступают непосредственно из источника данных ([щелкните, чтобы просмотреть изображение с полным размером](databinding-to-an-accordion-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Вперед](dynamically-adding-an-accordion-pane-cs.md)
