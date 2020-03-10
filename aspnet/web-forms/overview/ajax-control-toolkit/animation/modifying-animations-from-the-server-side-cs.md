---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: Изменение анимации со стороны сервера (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации также могут быть...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 0594efea9598a6c2461a72f789b5bd5f8ece23da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483894"
---
# <a name="modifying-animations-from-the-server-side-c"></a>Изменение анимации со стороны сервера (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации также можно изменить на стороне сервера

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации также можно изменить на стороне сервера

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

Остальная часть кода выполняется на стороне сервера и не использует разметку; Вместо этого он использует код для создания элемента управления `AnimationExtender`:

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

Однако набор элементов управления в настоящее время не предоставляет доступ к API для создания отдельных анимаций. Однако можно задать для свойства анимации `AnimationExtender`строку, содержащую XML-разметку, используемую при декларативном назначении анимации. Чтобы создать XML-файл, который не должен содержать элемент `<Animations>` можно использовать поддержку XML .NET Framework или, как показано в следующем коде, просто укажите строку:

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

Наконец, добавьте элемент управления `AnimationExtender` на текущую страницу в элементе `<form runat="server">`, убедившись, что анимация включена и выполняется:

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]

[![анимация создается с помощью кода/VB на стороне C#сервера](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)

Анимация создается с помощью кода/VB на стороне C#сервера ([щелкните, чтобы просмотреть изображение с полным размером](modifying-animations-from-the-server-side-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](triggering-an-animation-in-another-control-cs.md)
> [Вперед](executing-animations-using-client-side-code-cs.md)
