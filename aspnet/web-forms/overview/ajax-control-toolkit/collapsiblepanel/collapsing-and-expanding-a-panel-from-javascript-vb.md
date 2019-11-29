---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: Свертывание и развертывание панели из JavaScript (VB) | Документация Майкрософт
author: wenz
description: Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и развертывать...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599370"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a>Свертывание и развертывание панели из кода JavaScript (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)

> Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и расширять ее. Эти два действия также можно активировать из пользовательского кода JavaScript.

## <a name="overview"></a>Обзор

Элемент управления Коллапсиблепанел в наборе средств управления AJAX ASP.NET расширяет панель и предоставляет возможность сворачивать ее содержимое и расширять ее. Эти два действия также можно активировать из пользовательского кода JavaScript.

## <a name="steps"></a>Шаги

Во-первых, создайте новую страницу ASP.NET и включите `ScriptManager` в один элемент `<form>`. Это загружает библиотеку ASP.NET AJAX, которая необходима для набора средств управления.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

Затем создайте панель с текстом, чтобы можно было увидеть эффекты свертывания и развертывания:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

Как видите, панель ссылается на класс CSS, показанный здесь (и, по сути, определяет цвет фона и ширину панели):

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

Элементу управления `CollapsiblePanelExtender` требуется атрибут `TargetControlID`, чтобы набор средств знал, какую панель нужно свернуть или развернуть по запросу:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

К сожалению, в настоящее время расширитель не предоставляет определенный API для свертывания или развертывания панели, но некоторые недокументированные методы будут делаться. Во-первых, добавьте на страницу три кнопки HTML, которые затем активируют клиентский сценарий JavaScript, чтобы свернуть или развернуть содержимое панели:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

В коде JavaScript на стороне клиента (запущенном с `<script type="text/javascript">`) для доступа к `CollapsiblePanelExtender`необходимо использовать метод `$find()`. `$find("cpe")` вернет ссылку на него. С этой стороны, конкретные методы решают поставленную задачу.

Метод для открытия (расширения) панели называется `_doOpen()`; в следующем коде реализуется функция `doOpen()`, вызываемая при нажатии первой кнопки:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

Для закрытия или свертывания панели необходимо выполнить метод `_doClose()`. Таким образом, когда пользователь нажимает на вторую кнопку, вызывается следующий код JavaScript:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

Третья кнопка переключает состояние панели: с свернутого на развернутое и наоборот. `CollapsiblePanelExtender` предоставляет метод `toggle()`, который точно соответствует: изменяет состояние панели. Однако существует и другой подход (который внутренне используется методом `toggle()`): метод `get_Collapsed()` `CollapsiblePanelExtender()` указывающее, свернута ли панель. В зависимости от возвращаемого значения этой функции панель разворачивается (`_doOpen()` метод) или сворачивается (`_doClose()`).

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

[![третья кнопка изменяет состояние панели: с свернутого на расширенное и обратно.](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)

Третья кнопка изменяет состояние панели: с свернутого на развернутое и обратное ([щелкните, чтобы просмотреть изображение с полным размером](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](collapsing-and-expanding-a-panel-from-javascript-cs.md)
