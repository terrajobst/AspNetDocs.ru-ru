---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: Тестирование надежности пароля (Visual Basic) | Документация Майкрософт
author: wenz
description: Таким образом, чтобы отложенной Пользователи склонны выберите простые пароли, которые легко взломать пароли в любом месте, являются обязательными. Элемент управления PasswordStrength в ASP. Н...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: e64b79b1ce477fca439dd0db519371ed11446c52
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115253"
---
# <a name="testing-the-strength-of-a-password-vb"></a>Тестирование надежности пароля (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)

> Таким образом, чтобы отложенной Пользователи склонны выберите простые пароли, которые легко взломать пароли в любом месте, являются обязательными. PasswordStrength управления в ASP.NET AJAX Control Toolkit можно проверить, насколько хорошо работает пароль.

## <a name="overview"></a>Обзор

Таким образом, чтобы отложенной Пользователи склонны выберите простые пароли, которые легко взломать пароли в любом месте, являются обязательными. `PasswordStrength` Элемента управления в ASP.NET AJAX Control Toolkit можно проверить, насколько хорошо работает пароль.

## <a name="steps"></a>Шаги

`PasswordStrength` Управления расширяет текстовое поле и проверяет, является ли пароль в нем достаточно хорошо. Он предлагает множество возможностей с помощью атрибутов; Ниже приведены лишь некоторые из них.

- `MinimumNumericCharacters` Минимальное число цифр в пароле
- `MinimumSymbolCharacters` Минимальное число специальных символов (не буквы и цифры) в пароле
- `PreferredPasswordLength` Минимальная длина пароля
- `RequiresUpperAndLowerCaseCharacters` нужно ли использовать прописные и строчные буквы пароль

`StrengthIndicatorType` Предоставляет информацию, как представлять стойкость пароля, как текст (значение `"Text"`) или в качестве своего рода индикатор хода выполнения (значение `"BarIndicator"`). В `DisplayPosition` атрибут, настройкой где отображаются сведения. Ниже приведен полный пример, включая ASP.NET AJAX `ScriptManager` управления `PasswordStrength` управления и, конечно, текстовое поле, где пользователь может ввести пароль. Для целей демонстрации поле последняя форма является регулярное текстовое поле, а не поле пароля, чтобы вы могли видеть во время разработки, при вводе.

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

Откройте страницу и введите сейчас: Только после ввода строчные буквы, прописные буквы, цифры и символы, считается как неразрывный пароль.

[![Теперь пароль (), неплохо](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

Теперь пароль (), неплохо ([Просмотр полноразмерного изображения](testing-the-strength-of-a-password-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](testing-the-strength-of-a-password-cs.md)
