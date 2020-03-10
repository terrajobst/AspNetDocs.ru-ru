---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: Изменение анимации с помощью кода на стороне клиента (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимация также может...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: cce0a5a901f71edd40eada59ac7eeba93222e2b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430992"
---
# <a name="changing-an-animation-using-client-side-code-vb"></a>Изменение анимаций с помощью клиентского кода (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимацию также можно изменить с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимацию также можно изменить с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

Фактическая анимация запускается с помощью кнопки HTML:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

Обратите внимание, что в элементе управления `AnimationExtender` нет `<Animations>` узла. Пользовательский код JavaScript используется для предоставления анимаций, используемых с элементом управления.

Как и в случае с API сервера `AnimationExtender`, еще нет простого способа присвоить анимацию расширительу. Однако расширитель предоставляет несколько методов для чтения и записи анимации, зарегистрированной с различными событиями (`OnClick`, `OnLoad`и т. д.). Ниже приведены некоторые примеры:

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

Формат возвращаемого значения функций `get_*()` и формат аргумента для функций `set_*()` являются строкой JSON, предоставляя объектное представление того, что будет иметь XML-разметка. В настоящее время невозможно передать объект в, но можно считать объект из заданной анимации (`get_OnXXXBehavior()` методы).

Ниже приведена строка JSON (без кавычек и отформатированных), представляющая анимацию, активируемую кнопкой, но анимирование панели путем изменения ее размера и исчезновения ее в то же время:

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

Следующий код JavaScript назначает этот JSON-скрипта `OnClick` анимации текущего расширителя и выполняет его:

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]

[![анимация выполняется немедленно, без щелчка мышью (и с очень маленькой разметкой)](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)

Анимация выполняется немедленно, без щелчка мышью (и с очень маленькой разметкой) ([щелкните, чтобы просмотреть изображение с полным размером](changing-an-animation-using-client-side-code-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](executing-animations-using-client-side-code-vb.md)
> [Вперед](animating-an-updatepanel-control-vb.md)
