---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Создание взаимоисключающих флажков (VB) | Документация Майкрософт
author: wenz
description: 'Если можно выбрать только один из наборов параметров, обычно используются переключатели. Однако существует недостаток: один переключатель в группе,...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: f33936dd4d71f6bbf08f02966eefe44c8c152eba
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606466"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a>Создание взаимоисключающих флажков (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> Если можно выбрать только один из наборов параметров, обычно используются переключатели. Несмотря на то, что один переключатель в группе выбран, снять флажок все переключатели невозможно. Флажки в любое время можно снять, но они не являются взаимоисключающими. В этом учебнике лучше использовать оба подхода: флажки, которые являются взаимоисключающими.

## <a name="overview"></a>Обзор

Если можно выбрать только один из наборов параметров, обычно используются переключатели. Несмотря на то, что один переключатель в группе выбран, снять флажок все переключатели невозможно. Флажки в любое время можно снять, но они не являются взаимоисключающими. В этом учебнике лучше использовать оба подхода: флажки, которые являются взаимоисключающими.

## <a name="steps"></a>Шаги

Набор средств управления ASP.NET AJAX содержит расширитель Мутуаллексклусивечеккбокс. Это позволяет программистам назначать любой флажок имени группы (`Key` атрибут). Из всех флажков в одной группе можно выбрать только один из них.

Начнем с установки двух флажков на новой странице ASP.NET. Для демонстрации принципа может быть больше, но два из них достаточно:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

Для обоих флажков на странице должен быть размещен элемент управления Мутуаллексклусивечеккбоксекстендер. Оба ключевых атрибута должны иметь одинаковое значение, так же как атрибуты значений элементов переключателя HTML должны быть идентичны, чтобы обозначить группу, к которой они принадлежат. Свойство TargetControlID расширителя указывает на идентификатор флажка.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

Наконец, включите ASP.NET AJAX `ScriptManager`, необходимый для всех элементов набора средств управления AJAX ASP.NET:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

Сохраните и запустите страницу. Вы можете установить флажки и снять флажки, однако в этом случае оба флажка не будут установлены.

[![только один флажок можно проверить за раз](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

Только один флажок может быть проверен за раз ([щелкните, чтобы просмотреть изображение с полным размером](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](creating-mutually-exclusive-checkboxes-cs.md)
