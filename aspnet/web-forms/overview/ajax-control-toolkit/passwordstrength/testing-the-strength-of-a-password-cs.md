---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: Проверка надежности пароля (C#) | Документация Майкрософт
author: wenz
description: Пароли требуются почти в любом месте, чтобы отложенные пользователи могли выбирать простые пароли, которые легко прерывать работу. Элемент управления Пассвордстренгс в ASP. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: e55eab9feebc18f39dd40c59cfb423208296b6c5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598852"
---
# <a name="testing-the-strength-of-a-password-c"></a>Тестирование надежности пароля (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)

> Пароли требуются почти в любом месте, чтобы отложенные пользователи могли выбирать простые пароли, которые легко прерывать работу. Элемент управления Пассвордстренгс в наборе средств управления AJAX ASP.NET может проверить, насколько хорош пароль.

## <a name="overview"></a>Обзор

Пароли требуются почти в любом месте, чтобы отложенные пользователи могли выбирать простые пароли, которые легко прерывать работу. Элемент управления `PasswordStrength` в наборе средств управления AJAX ASP.NET может проверить, насколько хорош пароль.

## <a name="steps"></a>Шаги

Элемент управления `PasswordStrength` расширяет текстовое поле и проверяет, достаточно ли в нем пароля. Он предлагает множество вариантов через атрибуты. Вот лишь некоторые из них:

- `MinimumNumericCharacters` минимальное количество числовых символов, необходимое для пароля
- `MinimumSymbolCharacters` минимальное число символов (не букв и цифр), необходимое для пароля
- `PreferredPasswordLength` минимальной длины пароля
- `RequiresUpperAndLowerCaseCharacters`, должен ли пароль использовать как прописные, так и строчные буквы

`StrengthIndicatorType` предоставляет сведения о том, как представлять стойкость пароля в виде текста (значение `"Text"`) или в виде индикатора выполнения (value `"BarIndicator"`). В атрибуте `DisplayPosition` вы настраиваете место отображения информации. Ниже приведен полный пример, включая элемент управления `ScriptManager` AJAX ASP.NET, элемент управления `PasswordStrength` и само собой текстовое поле, в котором пользователь может ввести пароль. В целях демонстрации Последнее поле формы является обычным текстовым полем, а не полем пароля, что позволяет увидеть во время разработки то, что вы вводите.

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

Запуск страницы и ввод в конец: только после ввода строчных букв, прописных букв, цифр и символов пароль считается недопустимым.

[![теперь пароль (достаточно) хорошо](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

Теперь пароль (достаточно) хорошо ([щелкните, чтобы просмотреть изображение с полным размером](testing-the-strength-of-a-password-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Вперед](testing-the-strength-of-a-password-vb.md)
