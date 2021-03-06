---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: Изменение анимации со стороны сервера (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации также могут быть...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483870"
---
# <a name="modifying-animations-from-the-server-side-vb"></a>Изменение анимации со стороны сервера (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации также можно изменить на стороне сервера

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Анимации также можно изменить на стороне сервера

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

Остальная часть кода выполняется на стороне сервера и не использует разметку; Вместо этого он использует код для создания элемента управления `AnimationExtender`:

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

Однако набор элементов управления в настоящее время не предоставляет доступ к API для создания отдельных анимаций. Однако можно задать для свойства анимации `AnimationExtender`строку, содержащую XML-разметку, используемую при декларативном назначении анимации. Чтобы создать XML-файл, который не должен содержать элемент `<Animations>` можно использовать поддержку XML .NET Framework или, как показано в следующем коде, просто укажите строку:

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

Наконец, добавьте элемент управления `AnimationExtender` на текущую страницу в элементе `<form runat="server">`, убедившись, что анимация включена и выполняется:

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

[![анимация создается с помощью кода/VB на стороне C#сервера](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)

Анимация создается с помощью кода/VB на стороне C#сервера ([щелкните, чтобы просмотреть изображение с полным размером](modifying-animations-from-the-server-side-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](triggering-an-animation-in-another-control-vb.md)
> [Вперед](executing-animations-using-client-side-code-vb.md)
