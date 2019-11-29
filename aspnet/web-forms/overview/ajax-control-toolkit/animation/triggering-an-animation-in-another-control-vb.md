---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: Активация анимации в другом элементе управления (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Как правило, запуск...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575035"
---
# <a name="triggering-an-animation-in-another-control-vb"></a>Запуск анимации в другом элементе управления (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Как правило, запуск анимации запускается путем взаимодействия пользователя с тем же элементом управления. Однако можно также взаимодействовать с одним элементом управления и затем выполнять анимацию другого элемента управления.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Как правило, запуск анимации запускается путем взаимодействия пользователя с тем же элементом управления. Однако можно также взаимодействовать с одним элементом управления и затем выполнять анимацию другого элемента управления.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` на странице. затем загружается библиотека ASP.NET AJAX, что позволяет использовать набор средств управления.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

Анимация будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

В связанном классе CSS для панели задайте хороший цвет фона, а также задайте фиксированную ширину панели:

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

Чтобы начать анимацию панели, используется кнопка HTML. Обратите внимание, что `<input type="button" />` фавауредся поверх `<asp:Button />`, поскольку не требуется обратная передача при нажатии пользователем этой кнопки.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

Затем добавьте `AnimationExtender` на страницу, указав `ID`, атрибут `TargetControlID` и `runat="server"`обязательную. Важно присвоить `TargetControlID` ИДЕНТИФИКАТОРу кнопки (элементу, запускающему анимацию), а не ИДЕНТИФИКАТОРу панели (анимированный элемент).

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

В `<Animations>` узле поместите анимацию как обычно. Чтобы изменения были изменены на панели, а не на кнопке, установите атрибут `AnimationTarget` для каждого элемента анимации в `AnimationExtender`. Значение для `AnimationTarget` — это идентификатор панели, разумеется. Таким образом, анимация происходит с панелью, а не с кнопкой запуска. Ниже приведена `AnimationExtender`ная разметка для этого сценария:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

Обратите внимание на особый порядок, в котором отображаются отдельные анимации. Во первых, кнопка становится неактивной после запуска анимации. Так как в элементе `<EnableAction>` отсутствует атрибут `AnimationTarget`, эта анимация применяется к исходному элементу управления: кнопке. Следующие два этапа анимации должны выполняться параллельно (`<Parallel>` элемент). Для обоих атрибутов `AnimationTarget` задано значение `"Panel1"`, что позволяет анимировать панель, а не кнопку.

[![нажатии кнопки мыши запускает анимацию панели](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

Щелчок мышью на кнопке запускает анимацию панели ([щелкните, чтобы просмотреть изображение с полным размером](triggering-an-animation-in-another-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](disabling-actions-during-animation-vb.md)
> [Вперед](modifying-animations-from-the-server-side-vb.md)
