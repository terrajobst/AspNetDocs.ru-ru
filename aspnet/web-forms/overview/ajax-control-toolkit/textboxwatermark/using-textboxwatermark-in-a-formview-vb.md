---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: Использование элемента управления textboxwatermark в FormView (VB) | Документация Майкрософт
author: wenz
description: Элемент управления элемента управления textboxwatermark в наборе средств AJAX Control Toolkit расширяет текстовое поле, чтобы текст отображался в поле. Когда пользователь щелкает в поле, он...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: 1dd17ed57383680122c4ca613ca71f6682dec40e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598319"
---
# <a name="using-textboxwatermark-in-a-formview-vb"></a>Использование элемента управления TextBoxWatermark в элементе управления FormView (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)

> Элемент управления элемента управления textboxwatermark в наборе средств AJAX Control Toolkit расширяет текстовое поле, чтобы текст отображался в поле. Когда пользователь щелкает в поле, он очищается. Если пользователь оставляет поле без ввода текста, заполняется предварительно заполненный текст. Это также возможно в элементе управления FormView.

## <a name="overview"></a>Обзор

Элемент управления `TextBoxWatermark` в наборе средств AJAX Control Toolkit расширяет текстовое поле, позволяя отображать текст в поле. Когда пользователь щелкает в поле, он очищается. Если пользователь оставляет поле без ввода текста, заполняется предварительно заполненный текст. Это также возможно в элементе управления `FormView`.

## <a name="steps"></a>Шаги

Во-первых, требуется источник данных. В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition. База данных является необязательной частью установки Visual Studio (включая экспресс-выпуск) и доступна как отдельная загрузка в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). База данных AdventureWorks входит в состав примеров SQL Server 2005 и образцов баз данных (скачать в [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединить файл базы данных `AdventureWorks.mdf`.

В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию. Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

Затем добавьте к странице источник данных, поддерживающий `DELETE`, `INSERT` и `UPDATE` инструкций SQL. При использовании помощника Visual Studio для создания источника данных обратите внимание, что ошибка в текущей версии не предшествует имени таблицы (`Vendor`) с `Purchasing`. В следующей разметке показан правильный синтаксис:

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

Запомните имя источника данных (`ID`), так как оно будет использоваться в свойстве `DataSourceID` элемента управления `FormView`. Раздел `<InsertItemTemplate>` `FormView` содержит текстовое поле, которое расширяется элементом управления `TextBoxWatermarkExtender`. Убедитесь, что расширитель находится внутри шаблона, а не за его пределами.

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

Теперь, когда пользователь переходит в режим вставки элемента управления `FormView`, текстовое поле нового поставщика заполняется с помощью элемента управления `TextBoxWatermarkExtender`. Щелчок внутри текстового поля позволяет скрыть текст заполнителя.

[![, что водяной знак в поле поступает от расширителя](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)

Водяной знак в поле берется из расширителя ([щелкните, чтобы просмотреть изображение с полным размером](using-textboxwatermark-in-a-formview-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](using-textboxwatermark-with-validation-controls-cs.md)
> [Вперед](using-textboxwatermark-with-validation-controls-vb.md)
