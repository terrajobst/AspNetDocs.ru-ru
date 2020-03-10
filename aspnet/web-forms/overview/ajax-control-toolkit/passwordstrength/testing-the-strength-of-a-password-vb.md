---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: Проверка надежности пароля (VB) | Документация Майкрософт
author: wenz
description: Пароли требуются почти в любом месте, чтобы отложенные пользователи могли выбирать простые пароли, которые легко прерывать работу. Элемент управления Пассвордстренгс в ASP. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: b614e1788eeafc175dd792ec6d3e4619f9ea2b7a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508974"
---
# <a name="testing-the-strength-of-a-password-vb"></a>Тестирование надежности пароля (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)

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

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

Запуск страницы и ввод в конец: только после ввода строчных букв, прописных букв, цифр и символов пароль считается недопустимым.

[![теперь пароль (достаточно) хорошо](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

Теперь пароль (достаточно) хорошо ([щелкните, чтобы просмотреть изображение с полным размером](testing-the-strength-of-a-password-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](testing-the-strength-of-a-password-cs.md)
