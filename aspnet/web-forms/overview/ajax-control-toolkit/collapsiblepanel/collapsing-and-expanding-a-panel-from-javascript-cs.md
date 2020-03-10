---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: Свертывание и развертывание панели из JavaScript (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и развертывать...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: bed14d82394d28336493bec10e31ddb4d411a192
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497718"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-c"></a>Свертывание и развертывание панели из кода JavaScript (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)

> Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и расширять ее. Эти два действия также можно активировать из пользовательского кода JavaScript.

## <a name="overview"></a>Обзор

Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и расширять ее. Эти два действия также можно активировать из пользовательского кода JavaScript.

## <a name="steps"></a>Шаги

Во-первых, создайте новую страницу ASP.NET и включите `ScriptManager` в один элемент `<form>`. Это загружает библиотеку ASP.NET AJAX, которая необходима для набора средств управления.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

Затем создайте панель с текстом, чтобы можно было увидеть эффекты свертывания и развертывания:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

Как видите, панель ссылается на класс CSS, показанный здесь (и, по сути, определяет цвет фона и ширину панели):

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

Элементу управления `CollapsiblePanelExtender` требуется атрибут `TargetControlID`, чтобы набор средств знал, какую панель нужно свернуть или развернуть по запросу:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

К сожалению, в настоящее время расширитель не предоставляет определенный API для свертывания или развертывания панели, но некоторые недокументированные методы будут делаться. Во-первых, добавьте на страницу три кнопки HTML, которые затем активируют клиентский сценарий JavaScript, чтобы свернуть или развернуть содержимое панели:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

В коде JavaScript на стороне клиента (запущенном с `<script type="text/javascript">`) для доступа к `CollapsiblePanelExtender`необходимо использовать метод `$find()`. `$find("cpe")` вернет ссылку на него. С этой стороны, конкретные методы решают поставленную задачу.

Метод для открытия (расширения) панели называется `_doOpen()`; в следующем коде реализуется функция `doOpen()`, вызываемая при нажатии первой кнопки:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

Для закрытия или свертывания панели необходимо выполнить метод `_doClose()`. Таким образом, когда пользователь нажимает на вторую кнопку, вызывается следующий код JavaScript:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

Третья кнопка переключает состояние панели: с свернутого на развернутое и наоборот. `CollapsiblePanelExtender` предоставляет метод `toggle()`, который точно соответствует: изменяет состояние панели. Однако существует и другой подход (который внутренне используется методом `toggle()`): метод `get_Collapsed()` `CollapsiblePanelExtender()` указывающее, свернута ли панель. В зависимости от возвращаемого значения этой функции панель разворачивается (`_doOpen()` метод) или сворачивается (`_doClose()`).

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]

[![третья кнопка изменяет состояние панели: с свернутого на расширенное и обратно.](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)

Третья кнопка изменяет состояние панели: с свернутого на развернутое и обратное ([щелкните, чтобы просмотреть изображение с полным размером](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Дальше](collapsing-and-expanding-a-panel-from-javascript-vb.md)
