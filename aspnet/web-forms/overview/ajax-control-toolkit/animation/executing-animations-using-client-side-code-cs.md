---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: Запуск анимации с помощью кода на стороне клиентаC#() | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Выполнение анимации...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: b6ba1553b9c8c51d5d6ae1679e53f9cc1d17b769
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484026"
---
# <a name="executing-animations-using-client-side-code-c"></a>Выполнение анимаций с помощью клиентского кода (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Выполнение анимации также может быть запущено с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Выполнение анимации также может быть запущено с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

В `<Animations>` узле используйте `<OnClick>` для запуска анимации после того, как пользователь щелкнет панель. Добавьте две анимации для выполнения параллельно:

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

В целях демонстрации эта анимация (и любая другая анимация, созданная с помощью набора средств управления) выполняется с помощью кода JavaScript после выполнения страницы. Прежде всего нам нужен доступ к элементу управления `AnimationExtender`. Библиотека ASP.NET AJAX предоставляет функцию `$find()` для этой задачи:

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

Элемент управления `AnimationExtender` предоставляет богатый API, включая методы с именами, идентичными обработчикам событий, используемым в XML-разметке: `OnClick()`, `OnLoad()`и т. д. Например, вызов метода `OnClick()` выполняет анимацию в элементе `<OnClick>` элемента управления `AnimationExtender`:

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

Ниже приведен полный код JavaScript на стороне клиента, который имитирует щелчок на панели после полной загрузки страницы. Обратите внимание, что используется имя `pageLoad()` функции, которое вызывается ASP.NET AJAX после загрузки страницы и всех включенных библиотек JavaScript.

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]

[![анимация выполняется немедленно, без щелчка мышью](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)

Анимация выполняется немедленно без щелчка мышью ([щелкните, чтобы просмотреть изображение с полным размером](executing-animations-using-client-side-code-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](modifying-animations-from-the-server-side-cs.md)
> [Вперед](changing-an-animation-using-client-side-code-cs.md)
