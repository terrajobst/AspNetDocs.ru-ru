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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606250"
---
# <a name="testing-the-strength-of-a-password-vb"></a><span data-ttu-id="69727-104">Тестирование надежности пароля (VB)</span><span class="sxs-lookup"><span data-stu-id="69727-104">Testing the Strength of a Password (VB)</span></span>

<span data-ttu-id="69727-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="69727-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="69727-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="69727-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span></span>

> <span data-ttu-id="69727-107">Пароли требуются почти в любом месте, чтобы отложенные пользователи могли выбирать простые пароли, которые легко прерывать работу.</span><span class="sxs-lookup"><span data-stu-id="69727-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="69727-108">Элемент управления Пассвордстренгс в наборе средств управления AJAX ASP.NET может проверить, насколько хорош пароль.</span><span class="sxs-lookup"><span data-stu-id="69727-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="overview"></a><span data-ttu-id="69727-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="69727-109">Overview</span></span>

<span data-ttu-id="69727-110">Пароли требуются почти в любом месте, чтобы отложенные пользователи могли выбирать простые пароли, которые легко прерывать работу.</span><span class="sxs-lookup"><span data-stu-id="69727-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="69727-111">Элемент управления `PasswordStrength` в наборе средств управления AJAX ASP.NET может проверить, насколько хорош пароль.</span><span class="sxs-lookup"><span data-stu-id="69727-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="69727-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="69727-112">Steps</span></span>

<span data-ttu-id="69727-113">Элемент управления `PasswordStrength` расширяет текстовое поле и проверяет, достаточно ли в нем пароля.</span><span class="sxs-lookup"><span data-stu-id="69727-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="69727-114">Он предлагает множество вариантов через атрибуты. Вот лишь некоторые из них:</span><span class="sxs-lookup"><span data-stu-id="69727-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="69727-115">`MinimumNumericCharacters` минимальное количество числовых символов, необходимое для пароля</span><span class="sxs-lookup"><span data-stu-id="69727-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="69727-116">`MinimumSymbolCharacters` минимальное число символов (не букв и цифр), необходимое для пароля</span><span class="sxs-lookup"><span data-stu-id="69727-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="69727-117">`PreferredPasswordLength` минимальной длины пароля</span><span class="sxs-lookup"><span data-stu-id="69727-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="69727-118">`RequiresUpperAndLowerCaseCharacters`, должен ли пароль использовать как прописные, так и строчные буквы</span><span class="sxs-lookup"><span data-stu-id="69727-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="69727-119">`StrengthIndicatorType` предоставляет сведения о том, как представлять стойкость пароля в виде текста (значение `"Text"`) или в виде индикатора выполнения (value `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="69727-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="69727-120">В атрибуте `DisplayPosition` вы настраиваете место отображения информации.</span><span class="sxs-lookup"><span data-stu-id="69727-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="69727-121">Ниже приведен полный пример, включая элемент управления `ScriptManager` AJAX ASP.NET, элемент управления `PasswordStrength` и само собой текстовое поле, в котором пользователь может ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="69727-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="69727-122">В целях демонстрации Последнее поле формы является обычным текстовым полем, а не полем пароля, что позволяет увидеть во время разработки то, что вы вводите.</span><span class="sxs-lookup"><span data-stu-id="69727-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

<span data-ttu-id="69727-123">Запуск страницы и ввод в конец: только после ввода строчных букв, прописных букв, цифр и символов пароль считается недопустимым.</span><span class="sxs-lookup"><span data-stu-id="69727-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>

<span data-ttu-id="69727-124">[![теперь пароль (достаточно) хорошо](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="69727-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span></span>

<span data-ttu-id="69727-125">Теперь пароль (достаточно) хорошо ([щелкните, чтобы просмотреть изображение с полным размером](testing-the-strength-of-a-password-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="69727-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="69727-126">Назад</span><span class="sxs-lookup"><span data-stu-id="69727-126">Previous</span></span>](testing-the-strength-of-a-password-cs.md)
