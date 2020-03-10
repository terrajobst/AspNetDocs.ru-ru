---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
title: Активация анимации в другом элементе управления (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Как правило, запуск...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5d99c2b-d8ee-413c-80d5-c120cffb0a4c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
msc.type: authoredcontent
ms.openlocfilehash: e0a1f8986047da04db6fde8e54b6fd0ac6ee2603
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430794"
---
# <a name="triggering-an-animation-in-another-control-c"></a>Запуск анимации в другом элементе управления (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Как правило, запуск анимации запускается путем взаимодействия пользователя с тем же элементом управления. Однако можно также взаимодействовать с одним элементом управления и затем выполнять анимацию другого элемента управления.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Как правило, запуск анимации запускается путем взаимодействия пользователя с тем же элементом управления. Однако можно также взаимодействовать с одним элементом управления и затем выполнять анимацию другого элемента управления.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](triggering-an-animation-in-another-control-cs/samples/sample3.css)]

Чтобы начать анимацию панели, используется кнопка HTML. Обратите внимание, что `<input type="button" />` фавауредся поверх `<asp:Button />`, поскольку не требуется обратная передача при нажатии пользователем этой кнопки.

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample4.aspx)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную. Важно присвоить `TargetControlID` ИДЕНТИФИКАТОРу кнопки (элементу, запускающему анимацию), а не ИДЕНТИФИКАТОРу панели (анимированный элемент).

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample5.aspx)]

В `<Animations>` узле поместите анимацию как обычно. Чтобы изменения были изменены на панели, а не на кнопке, установите атрибут `AnimationTarget` для каждого элемента анимации в `AnimationExtender`. Значение для `AnimationTarget` — это идентификатор панели, разумеется. Таким образом, анимация происходит с панелью, а не с кнопкой запуска. Ниже приведена `AnimationExtender`ная разметка для этого сценария:

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample6.aspx)]

Обратите внимание на особый порядок, в котором отображаются отдельные анимации. Во первых, кнопка становится неактивной после запуска анимации. Так как в элементе `<EnableAction>` отсутствует атрибут `AnimationTarget`, эта анимация применяется к исходному элементу управления: кнопке. Следующие два этапа анимации должны выполняться параллельно (`<Parallel>` элемент). Для обоих атрибутов `AnimationTarget` задано значение `"Panel1"`, что позволяет анимировать панель, а не кнопку.

[![нажатии кнопки мыши запускает анимацию панели](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)

Щелчок мышью на кнопке запускает анимацию панели ([щелкните, чтобы просмотреть изображение с полным размером](triggering-an-animation-in-another-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](disabling-actions-during-animation-cs.md)
> [Вперед](modifying-animations-from-the-server-side-cs.md)
