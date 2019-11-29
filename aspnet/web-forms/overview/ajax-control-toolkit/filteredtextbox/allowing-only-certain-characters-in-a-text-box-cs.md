---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: Разрешение только некоторых символов в текстовом поле (C#) | Документация Майкрософт
author: wenz
description: Элементы управления проверки ASP.NET могут гарантировать, что вводимые пользователем данные допускаются только в определенных символах. Однако это по-прежнему не мешает пользователям вводить недопустимые...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: d1e367becd574e31d24fca8545f76b1ed3c4d85e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611747"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a>Разрешение только некоторых символов в текстовом поле (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)

> Элементы управления проверки ASP.NET могут гарантировать, что вводимые пользователем данные допускаются только в определенных символах. Однако это по-прежнему не мешает пользователям вводить недопустимые символы и пытаться отправить форму.

## <a name="overview"></a>Обзор

Элементы управления проверки ASP.NET могут гарантировать, что вводимые пользователем данные допускаются только в определенных символах. Однако это по-прежнему не мешает пользователям вводить недопустимые символы и пытаться отправить форму.

## <a name="steps"></a>Шаги

Набор средств ASP.NET AJAX Control Toolkit содержит элемент управления `FilteredTextBox`, расширяющий текстовое поле. После активации в поле может быть вставлен только определенный набор символов.

Чтобы это работало, сначала необходимо использовать ASP.NET AJAX `ScriptManager`, который загружает библиотеки JavaScript, которые также используются набором средств управления AJAX ASP.NET.

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

Затем нам нужно текстовое поле:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

Наконец, элемент управления `FilteredTextBoxExtender` позаботится об ограничении символов, которые разрешено вводить пользователю. Сначала присвойте атрибуту `TargetControlID` `ID` элемента управления `TextBox`. Затем выберите одно из доступных значений `FilterType`:

- `Custom` по умолчанию; необходимо предоставить список допустимых символов
- `LowercaseLetters` только строчные буквы
- `Numbers` только цифры
- `UppercaseLetters` только прописные буквы

Если используется `Custom FilterType`, необходимо задать свойство `ValidChars` и предоставить список символов, которые могут быть введены. Кстати: при попытке вставить текст в текстовое поле удаляются все недопустимые символы.

Ниже приведена разметка для элемента управления `FilteredTextBoxExtender`, которая допускает только цифры (что также было бы возможно с `FilterType="Numbers"`):

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

Запустите страницу и попытайтесь ввести букву, если JavaScript включен, он не будет работать. Однако на странице цифры отображаются. Однако обратите внимание, что `FilteredTextBox` защиты не является маркированным: Если включен JavaScript, любые данные могут быть введены в текстовое поле, поэтому необходимо использовать дополнительные средства проверки, например ASP. Элементы управления проверки NET.

[![могут быть указаны только цифры](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)

Можно указать только цифры ([щелкните, чтобы просмотреть изображение с полным размером](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Вперед](allowing-only-certain-characters-in-a-text-box-vb.md)
