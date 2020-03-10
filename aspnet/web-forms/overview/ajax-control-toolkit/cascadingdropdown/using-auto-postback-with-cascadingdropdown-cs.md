---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: Использование автоматической обратной передачи с помощьюC#CascadingDropDown () | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430686"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a>Использование автоматической обратной передачи с помощью CascadingDropDown (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)

> Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. Однако при использовании элемента управления CascadingDropDown, ASP. Функция автообратной передачи элемента управления DropDownList не работает, так как асинхронная загрузка данных в список создает обратную передачу (не нужно). Этот результат можно избежать с помощью кода JavaScript.

## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. (Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Однако при использовании элемента управления CascadingDropDown, ASP. Функция автообратной передачи элемента управления DropDownList не работает, так как асинхронная загрузка данных в список создает обратную передачу (не нужно). Этот результат можно избежать с помощью кода JavaScript.

## <a name="steps"></a>Шаги

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но внутри &lt;`form`&gt;):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

Затем требуется элемент управления DropDownList:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

Для этого списка добавляется расширитель CascadingDropDown, предоставляющий URL-адрес и сведения о методе:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

Затем расширитель CascadingDropDown асинхронно вызывает веб-службу со следующей сигнатурой метода:

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

Метод возвращает массив типа CascadingDropDown value. Конструктор типа сначала ждет заголовок записи списка, а затем значение (атрибут HTML `value`).

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

Загрузка страницы в браузере приведет к заполнению раскрывающегося списка тремя поставщиками, второй из которых выбран заранее. Кроме того, ASP.NET определяет метод `__doPostBack()` JavaScript. После загрузки страницы этот вызов JavaScript добавляется в раскрывающийся список, но только в том случае, если в нем есть элементы. Если в списке нет элементов, набор элементов управления в данный момент загружает их, поэтому код JavaScript использует время ожидания и пытается повторить попытку в течение половины секунды.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

Таким образом, обратная передача выполняется только в том случае, если в списке есть элементы, и пользователь выбирает запись.

[![выборе элемента списка вызывает обратную передачу](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)

Выбор элемента списка вызывает обратную передачу ([щелкните, чтобы просмотреть изображение с полным размером](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](presetting-list-entries-with-cascadingdropdown-cs.md)
> [Вперед](filling-a-list-using-cascadingdropdown-vb.md)
