---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: Использование автоматической обратной передачи с помощью CascadingDropDown (VB) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 5dea23a20aba00af5109f05f18365b89e409a131
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574475"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a>Использование автоматической обратной передачи с помощью CascadingDropDown (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)

> Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. Однако при использовании элемента управления CascadingDropDown, ASP. Функция автообратной передачи элемента управления DropDownList не работает, так как асинхронная загрузка данных в список создает обратную передачу (не нужно). Этот результат можно избежать с помощью кода JavaScript.

## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. (Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Однако при использовании элемента управления CascadingDropDown, ASP. Функция автообратной передачи элемента управления DropDownList не работает, так как асинхронная загрузка данных в список создает обратную передачу (не нужно). Этот результат можно избежать с помощью кода JavaScript.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но внутри &lt;`form`&gt;):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

Затем требуется элемент управления DropDownList:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

Для этого списка добавляется расширитель CascadingDropDown, предоставляющий URL-адрес и сведения о методе:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

Затем расширитель CascadingDropDown асинхронно вызывает веб-службу со следующей сигнатурой метода:

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

Метод возвращает массив типа CascadingDropDown value. Конструктор типа сначала ждет заголовок записи списка, а затем значение (атрибут HTML `value`).

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

Загрузка страницы в браузере приведет к заполнению раскрывающегося списка тремя поставщиками, второй из которых выбран заранее. Кроме того, ASP.NET определяет метод `__doPostBack()` JavaScript. После загрузки страницы этот вызов JavaScript добавляется в раскрывающийся список, но только в том случае, если в нем есть элементы. Если в списке нет элементов, набор элементов управления в данный момент загружает их, поэтому код JavaScript использует время ожидания и пытается повторить попытку в течение половины секунды.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

Таким образом, обратная передача выполняется только в том случае, если в списке есть элементы, и пользователь выбирает запись.

[![выборе элемента списка вызывает обратную передачу](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)

Выбор элемента списка вызывает обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](presetting-list-entries-with-cascadingdropdown-vb.md)
