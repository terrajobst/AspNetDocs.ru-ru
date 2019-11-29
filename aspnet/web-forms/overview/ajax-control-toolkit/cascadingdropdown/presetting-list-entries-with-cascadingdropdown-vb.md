---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: Предустановка записей списка с помощью CascadingDropDown (VB) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599547"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a>Предустановка записей списка с помощью CascadingDropDown (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)

> Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. Небольшое количество кода может быть предвыбрано после динамической загрузки данных в элемент списка.

## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. (Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Небольшое количество кода может быть предвыбрано после динамической загрузки данных в элемент списка.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но в элементе `<form>`):

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

Затем требуется элемент управления DropDownList:

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

Для этого списка добавляется расширитель CascadingDropDown, предоставляющий URL-адрес и сведения о методе:

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

Затем расширитель CascadingDropDown асинхронно вызывает веб-службу со следующей сигнатурой метода:

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

Метод возвращает массив типа CascadingDropDown value. Конструктор типа сначала ждет заголовок записи списка, а затем значение (атрибут HTML `value`). Если для третьего аргумента задано значение true, элемент списка автоматически выбирается в браузере.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

Загрузка страницы в браузере приведет к заполнению раскрывающегося списка тремя поставщиками, второй из которых выбран заранее.

[![список заполнен и выбран автоматически](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

Список заполняется и выбирается автоматически ([щелкните, чтобы просмотреть изображение с полным размером](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](using-cascadingdropdown-with-a-database-vb.md)
> [Вперед](using-auto-postback-with-cascadingdropdown-vb.md)
