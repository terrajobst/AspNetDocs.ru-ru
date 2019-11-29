---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: Заполнение списка с помощью CascadingDropDownC#() | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574838"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a>Заполнение списка с помощью CascadingDropDown (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)

> Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. (Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Первая проблема, которую необходимо решить, заключается в том, чтобы заполнить раскрывающийся список с помощью этого элемента управления.

## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. (Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Первая проблема, которую необходимо решить, заключается в том, чтобы заполнить раскрывающийся список с помощью этого элемента управления.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

Затем требуется элемент управления DropDownList:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

Для этого списка добавляется расширитель CascadingDropDown. Он отправляет асинхронный запрос к веб-службе, который затем возвращает список записей, которые будут отображены в списке. Чтобы это работало, необходимо задать следующие атрибуты CascadingDropDown:

- `ServicePath`: URL веб-службы, которая доставляет записи списка
- `ServiceMethod`: веб-метод, поставляющий записи списка
- `TargetControlID`: Идентификатор раскрывающегося списка
- `Category`: сведения о категории, которые передаются в веб-метод при вызове
- `PromptText`: текст, отображаемый при асинхронной загрузке данных списка с сервера

Ниже приведена разметка для элемента `CascadingDropDown`. Единственное различие между C# и VB — имя связанной веб-службы:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

Код JavaScript, поступающий из расширителя `CascadingDropDown`, вызывает метод веб-службы со следующей сигнатурой:

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

Поэтому важным аспектом является то, что метод должен возвращать массив типа `CascadingDropDownNameValue` (определяемый набором средств управления AJAX ASP.NET). В конструкторе `CascadingDropDownNameValue` сначала необходимо указать текст записи списка, а затем его значение, как `<option value="VALUE">NAME</option>` бы в HTML. Ниже приведено несколько примеров данных.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

При загрузке страницы в браузере список будет заполнен тремя поставщиками.

[![список заполняется автоматически](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)

Список заполняется автоматически ([щелкните, чтобы просмотреть изображение с полным размером](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Вперед](using-cascadingdropdown-with-a-database-cs.md)
