---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: Создание взаимоисключающих флажков (C#) | Документация Майкрософт
author: wenz
description: 'Если можно выбрать только один из наборов параметров, обычно используются переключатели. Однако существует недостаток: один переключатель в группе,...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606507"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a>Создание взаимоисключающих флажков (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)

> Если можно выбрать только один из наборов параметров, обычно используются переключатели. Несмотря на то, что один переключатель в группе выбран, снять флажок все переключатели невозможно. Флажки в любое время можно снять, но они не являются взаимоисключающими. В этом учебнике лучше использовать оба подхода: флажки, которые являются взаимоисключающими.

## <a name="overview"></a>Обзор

Если можно выбрать только один из наборов параметров, обычно используются переключатели. Несмотря на то, что один переключатель в группе выбран, снять флажок все переключатели невозможно. Флажки в любое время можно снять, но они не являются взаимоисключающими. В этом учебнике лучше использовать оба подхода: флажки, которые являются взаимоисключающими.

## <a name="steps"></a>Шаги

Набор средств управления ASP.NET AJAX содержит расширитель Мутуаллексклусивечеккбокс. Это позволяет программистам назначать любой флажок имени группы (`Key` атрибут). Из всех флажков в одной группе можно выбрать только один из них.

Начнем с установки двух флажков на новой странице ASP.NET. Для демонстрации принципа может быть больше, но два из них достаточно:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

Для обоих флажков на странице должен быть размещен элемент управления Мутуаллексклусивечеккбоксекстендер. Оба ключевых атрибута должны иметь одинаковое значение, так же как атрибуты значений элементов переключателя HTML должны быть идентичны, чтобы обозначить группу, к которой они принадлежат. Свойство TargetControlID расширителя указывает на идентификатор флажка.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

Наконец, включите ASP.NET AJAX `ScriptManager`, необходимый для всех элементов набора средств управления AJAX ASP.NET:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

Сохраните и запустите страницу. Вы можете установить флажки и снять флажки, однако в этом случае оба флажка не будут установлены.

[![только один флажок можно проверить за раз](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)

Только один флажок может быть проверен за раз ([щелкните, чтобы просмотреть изображение с полным размером](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Вперед](creating-mutually-exclusive-checkboxes-vb.md)
