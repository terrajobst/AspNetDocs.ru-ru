---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: Предустановка записей списка с помощью CascadingDropDownC#() | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bb4a51092534e6fddbd40f868c53c58d12eef2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574683"
---
# <a name="presetting-list-entries-with-cascadingdropdown-c"></a>Предустановка записей списка с помощью CascadingDropDown (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)

> Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. Небольшое количество кода может быть предвыбрано после динамической загрузки данных в элемент списка.

## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. (Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Небольшое количество кода может быть предвыбрано после динамической загрузки данных в элемент списка.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

Затем требуется элемент управления DropDownList:

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

Для этого списка добавляется расширитель CascadingDropDown, предоставляющий URL-адрес и сведения о методе:

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

Затем расширитель CascadingDropDown асинхронно вызывает веб-службу со следующей сигнатурой метода:

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

Метод возвращает массив типа CascadingDropDown value. Конструктор типа сначала ждет заголовок записи списка, а затем значение (атрибут HTML `value`). Если для третьего аргумента задано значение true, элемент списка автоматически выбирается в браузере.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

Загрузка страницы в браузере приведет к заполнению раскрывающегося списка тремя поставщиками, второй из которых выбран заранее.

[![список заполнен и выбран автоматически](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)

Список заполняется и выбирается автоматически ([щелкните, чтобы просмотреть изображение с полным размером](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](using-cascadingdropdown-with-a-database-cs.md)
> [Вперед](using-auto-postback-with-cascadingdropdown-cs.md)
