---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: Анимация элемента управления UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d66dda923940a328c0757049c9d8bfa3b2d2b9fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607079"
---
# <a name="animating-an-updatepanel-control-vb"></a>Анимация элемента управления UpdatePanel (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого UpdatePanel существует специальный расширитель, который сильно зависит от платформы анимации: UpdatePanelAnimation. В этом руководстве показано, как настроить подобную анимацию для UpdatePanel.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого `UpdatePanel`существует специальный расширитель, который сильно зависит от платформы анимации: `UpdatePanelAnimation`. В этом руководстве показано, как настроить такую анимацию для `UpdatePanel`.

## <a name="steps"></a>Шаги

Первым шагом является включение `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и использовать набор элементов управления.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

Анимация в этом сценарии будет применена к веб-элементу управления ASP.NET `Wizard`, размещенному в `UpdatePanel`. Три (случайные) шага предоставляют достаточно параметров для активации обратных передач:

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

Разметка, необходимая для элемента управления `UpdatePanelAnimationExtender`, очень похожа на разметку, используемую для `AnimationExtender`. В атрибуте `TargetControlID` мы предоставляем `ID` `UpdatePanel` для анимации. в элементе управления `UpdatePanelAnimationExtender` элемент `<Animations>` содержит XML-разметку для анимаций. Однако существует одно отличие: количество событий и обработчиков событий ограничено в сравнении с `AnimationExtender`. Для `UpdatePanels`существует только два из них:

- `<OnUpdated>` при обновлении UpdatePanel
- `<OnUpdating>` при начале обновления UpdatePanel

В этом сценарии новое содержимое `UpdatePanel` (после обратной передачи) будет постепенно передаваться. Это необходимая разметка для этого:

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

Теперь, когда обратная передача происходит в UpdatePanel, новое содержимое панели плавно перестало отображаться.

[![следующем шаге мастера происходит снижение яркости](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)

Следующий шаг мастера поменяется ([щелкните, чтобы просмотреть изображение с полным размером](animating-an-updatepanel-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](changing-an-animation-using-client-side-code-vb.md)
> [Вперед](dynamically-controlling-updatepanel-animations-vb.md)
