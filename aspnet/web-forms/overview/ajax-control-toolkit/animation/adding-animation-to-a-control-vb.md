---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: Добавление анимации в элемент управления (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. В этом руководстве показано, как...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484128"
---
# <a name="adding-animation-to-a-control-vb"></a>Добавление анимации в элемент управления (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. В этом руководстве показано, как настроить подобную анимацию.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. В этом руководстве показано, как настроить подобную анимацию.

## <a name="steps"></a>Шаги

Первым шагом является включение `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и использовать набор элементов управления.

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

Анимация в этом сценарии будет применена к панели текста, которая выглядит следующим образом:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

Связанный класс CSS для панели определяет цвет фона и ширину:

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

Далее требуется `AnimationExtender`. После предоставления `ID` и обычного `runat="server"`атрибут `TargetControlID` должен быть установлен на элемент управления для анимации в нашем случае, панель:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

Вся анимация применяется декларативно с использованием синтаксиса XML, к сожалению, в настоящее время не полностью поддерживается IntelliSense в Visual Studio. Корневой узел `<Animations>;` в пределах этого узла; разрешено несколько событий, которые определяют, когда происходит анимация (-ов):

- `OnClick` (щелчок мышью)
- `OnHoverOut` (когда мышь покидает элемент управления)
- `OnHoverOver` (при наведении указателя мыши на элемент управления, остановка `OnHoverOut`ной анимации)
- `OnLoad` (при загрузке страницы)
- `OnMouseOut` (когда мышь покидает элемент управления)
- `OnMouseOver` (при наведении указателя мыши на элемент управления, не останавливая `OnMouseOut` анимацию)

Платформа поставляется с набором анимаций, каждый из которых представлен собственным XML-элементом. Выбор осуществляется следующим образом:

- `<Color>` (изменение цвета)
- `<FadeIn>` (снижение)
- `<FadeOut>` (плавное уменьшение)
- `<Property>` (изменение свойства элемента управления)
- `<Pulse>` (пулсатинг)
- `<Resize>` (изменение размера)
- `<Scale>` (пропорциональное изменение размера)

В этом примере панель будет исчезать. Анимация должна принимать 1,5 секунд (`Duration` атрибут), отображая 24 кадра (шаги анимации) в секунду (`Fps` атрибут). Ниже приведена полная разметка для элемента управления `AnimationExtender`.

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

При выполнении этого сценария панель отображается и постепенно исчезает в течение одной и половины секунд.

[![панель выходит из затухания](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

Панель выйдет из режима исчезновения ([щелкните, чтобы просмотреть изображение с полным размером](adding-animation-to-a-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](dynamically-controlling-updatepanel-animations-cs.md)
> [Вперед](executing-several-animations-at-the-same-time-vb.md)
