---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: Анимация элемента управления UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: a7c40ebe359e21602d9f1de8205e1a7c808acc85
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384257"
---
# <a name="animating-an-updatepanel-control-vb"></a>Анимация элемента управления UpdatePanel (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)

> Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Для содержимого элемента управления UpdatePanel специальные расширения существует, во многом полагается на framework анимации: UpdatePanelAnimation. Этом руководстве показано, как настроить такой анимации для элемента управления UpdatePanel.


## <a name="overview"></a>Обзор

Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Для содержимого `UpdatePanel`, существует специальные расширения, которая основывается на использовании framework анимации: `UpdatePanelAnimation`. Этом руководстве показано, как настроить такой анимацию для `UpdatePanel`.

## <a name="steps"></a>Шаги

Первым шагом является обычным образом, чтобы включить `ScriptManager` на странице, ASP.NET AJAX library загружается и может использоваться набор элементов управления:

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

Анимация в этом сценарии будет применяться к ASP.NET `Wizard` веб-элемента управления, находящихся в `UpdatePanel`. Три шага (произвольному) предоставляют достаточно возможности для запуска операций обратной передачи.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

Разметка, необходимые для `UpdatePanelAnimationExtender` управления очень похож на разметку, используемую для `AnimationExtender`. В `TargetControlID` атрибут, мы предоставляем `ID` из `UpdatePanel` для анимации; в `UpdatePanelAnimationExtender` элемента управления, `<Animations>` элемент содержит XML-разметку для анимации. Однако есть одно различие: Объем события и обработчики событий ограничено по сравнению с `AnimationExtender`. Для `UpdatePanels`, только два из них существует:

- `<OnUpdated>` Когда будет обновлена UpdatePanel
- `<OnUpdating>` Когда UpdatePanel начинает обновление

В этом случае новый содержимое `UpdatePanel` (после обратной отправки) должны появление. Это необходимые средства разметки для этого:

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

Теперь всякий раз, когда происходит обратная передача внутри UpdatePanel, новое содержимое панели Плавное.


[![TСледующий шаг мастера HE: плавный переход](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)

Следующий шаг мастера является плавный переход ([Просмотр полноразмерного изображения](animating-an-updatepanel-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](changing-an-animation-using-client-side-code-vb.md)
> [Вперед](dynamically-controlling-updatepanel-animations-vb.md)
