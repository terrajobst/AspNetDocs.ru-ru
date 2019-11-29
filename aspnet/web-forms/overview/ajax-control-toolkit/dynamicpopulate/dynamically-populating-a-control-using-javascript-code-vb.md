---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: Динамическое заполнение элемента управления с помощью кода JavaScript (VB) | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет результирующее значение целевым элементом управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b2bd5b1571ccebc9baa501b29743aecdb4543fb2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599224"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a>Динамическое заполнение элемента управления с помощью кода JavaScript (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)

> Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы. Можно также активировать заполнение с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="overview"></a>Обзор

Элемент управления `DynamicPopulate` в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы. Можно также активировать заполнение с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="steps"></a>Шаги

Во-первых, вам понадобится ASP.NET Web Service, который реализует метод, вызываемый элементом управления `DynamicPopulateExtender`. Веб-служба реализует метод `getDate()`, который принимает один аргумент типа String, именуемый `contextKey`, поскольку элемент управления `DynamicPopulate` отправляет один фрагмент сведений о контексте при каждом вызове веб-службы. Ниже приведен код (файл `DynamicPopulate.vb.asmx`), который извлекает текущую дату в одном из трех форматов:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

На следующем шаге создайте новый сайт ASP.NET и начните с элемента управления ScriptManager ASP.NET AJAX:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

Затем добавьте элемент управления Label (например, с помощью элемента управления HTML с тем же именем или `<asp:Label />` веб-элемента управления), который позже покажет результат вызова веб-службы.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

Затем включите элемент управления `DynamicPopulateExtender` и укажите сведения о веб-службе, целевой элемент управления, но не имя элемента управления, запускающего заполнение. это будет сделано позже с помощью пользовательского JavaScript!

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

Теперь к части JavaScript. Функция `$find()`, определенная библиотекой AJAX ASP.NET, возвращает ссылку на объекты на стороне сервера из набора средств ASP.NET AJAX Control Toolkit, например `DynamicPopulateExtender`. В текущем файле `$find("dpe")` возвращает ссылку на один элемент управления `DynamicPopulateExtender` на странице. Он предоставляет метод, именуемый `populate()`, который запускает процесс динамического заполнения. Методу `populate()` требуется один аргумент: ключ контекста, который будет использоваться в качестве аргумента для веб-метода `getDate()`. Например, `$find("dpe").populate("format1")` будет заполнять метку текущей датой в формате "месяц-день-год".

Чтобы сделать пример более гибким, пользователь может выбрать один из нескольких форматов даты. Для каждого из них отображается переключатель. Когда пользователь щелкнет переключатель, код JavaScript динамически заполняет метку выбранным форматом даты. Ниже перечислены эти переключатели.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

Обратите внимание на то, что в контексте переключателя выражение JavaScript `this.value` относится к значению текущей кнопки, то есть именно та же информация, с которой может работать метод `getDate()`.

[![нажатии кнопки получает дату с сервера в указанном формате.](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)

При нажатии кнопки извлекается дата с сервера в указанном формате ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](dynamically-populating-a-control-vb.md)
> [Вперед](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)
