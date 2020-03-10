---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: Динамическое управление анимациямиC#UpdatePanel () | Документация Майкрософт
author: wenz
description: Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430902"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a>Динамическое управление анимациями UpdatePanel (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)

> Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого UpdatePanel существует специальный расширитель, который сильно зависит от платформы анимации: UpdatePanelAnimation. Он также может работать вместе с триггерами UpdatePanel.

## <a name="overview"></a>Обзор

Элемент управления Animation в наборе средств ASP.NET AJAX Control Toolkit — это не просто элемент управления, но вся платформа для добавления анимации в элемент управления. Для содержимого `UpdatePanel`существует специальный расширитель, который сильно зависит от платформы анимации: `UpdatePanelAnimation`. Он также может работать вместе с триггерами `UpdatePanel`.

## <a name="steps"></a>Шаги

Первым шагом является включение `ScriptManager` на страницу, чтобы загрузить библиотеку ASP.NET AJAX и использовать набор элементов управления.

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

Анимация в этом сценарии будет применена к отображению текущего времени. Эти сведения можно записать в метку с помощью метода `Page_Load()` или (для простоты) используется следующий встроенный код:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

Кроме того, создается кнопка для активации обновления времени.

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

Затем этот код помещается в раздел `<ContentTemplate>` элемента `UpdatePanel`. Атрибут `UpdateMode` панели должен иметь значение `"Conditional"`, так как только триггеры могут обновлять содержимое панели. В разделе `<Triggers>` `UpdatePanel`создается триггер асинхронной обратной передачи, связанный с событием `Click` кнопки. Таким же, если пользователь нажимает кнопку, `UpdatePanel` обновляется. Ниже приведена разметка для элемента управления `UpdatePanel`.

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

Наконец, необходимо настроить `UpdatePanelAnimationExtender`: присвойте атрибуту `TargetControlID` идентификатор панели и определите анимацию в расширителье. Плавное появление имеет смысл, что создает привлекательное визуальное внимание на обновленное время. Разметка расширителя может выглядеть следующим образом:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

Запустите файл в браузере. При каждом нажатии кнопки текущее время отображается на панели, а в течение одной секунды всегда выводится на экран.

[![текущее время помещается в плавность](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)

Текущее время отображается в виде затухания ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](animating-an-updatepanel-control-cs.md)
> [Вперед](adding-animation-to-a-control-vb.md)
