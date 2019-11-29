---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: Изменение анимации с помощью кода на стороне клиента (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимация также может...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606984"
---
# <a name="changing-an-animation-using-client-side-code-c"></a>Изменение анимаций с помощью клиентского кода (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимацию также можно изменить с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимацию также можно изменить с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

Фактическая анимация запускается с помощью кнопки HTML:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

Обратите внимание, что в элементе управления `AnimationExtender` нет `<Animations>` узла. Пользовательский код JavaScript используется для предоставления анимаций, используемых с элементом управления.

Как и в случае с API сервера `AnimationExtender`, еще нет простого способа присвоить анимацию расширительу. Однако расширитель предоставляет несколько методов для чтения и записи анимации, зарегистрированной с различными событиями (`OnClick`, `OnLoad`и т. д.). Далее приводятся некоторые примеры.

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

Формат возвращаемого значения функций `get_*()` и формат аргумента для функций `set_*()` являются строкой JSON, предоставляя объектное представление того, что будет иметь XML-разметка. В настоящее время невозможно передать объект в, но можно считать объект из заданной анимации (`get_OnXXXBehavior()` методы).

Ниже приведена строка JSON (без кавычек и отформатированных), представляющая анимацию, активируемую кнопкой, но анимирование панели путем изменения ее размера и исчезновения ее в то же время:

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

Следующий код JavaScript назначает этот JSON-скрипта `OnClick` анимации текущего расширителя и выполняет его:

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

[![анимация выполняется немедленно, без щелчка мышью (и с очень маленькой разметкой)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)

Анимация выполняется немедленно, без щелчка мышью (и с очень маленькой разметкой) ([щелкните, чтобы просмотреть изображение с полным размером](changing-an-animation-using-client-side-code-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](executing-animations-using-client-side-code-cs.md)
> [Вперед](animating-an-updatepanel-control-cs.md)
