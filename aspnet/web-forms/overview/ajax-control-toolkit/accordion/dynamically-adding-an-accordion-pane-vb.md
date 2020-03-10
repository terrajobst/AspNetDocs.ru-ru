---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: Динамическое добавление панели «гармошка» (VB) | Документация Майкрософт
author: wenz
description: Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: be48db5ea3de4af46b0f864cc9e73d2f518294a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484146"
---
# <a name="dynamically-adding-an-accordion-pane-vb"></a>Динамическое добавление панели «гармошка» (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)

> Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются внутри самой страницы, но для достижения того же результата можно использовать код на стороне сервера.

## <a name="overview"></a>Обзор

Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются внутри самой страницы, но для достижения того же результата можно использовать код на стороне сервера.

## <a name="steps"></a>Шаги

Элемент управления "гармошка" предоставляет все важные свойства коду на стороне сервера. Помимо прочего, свойство `Panes` предоставляет доступ к коллекции панелей, составляющих гармошка. Каждая панель имеет тип `AccordionPane`. Таким образом, упрощена создание такой области:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

Свойство `HeaderContainer` `AccordionPane` предоставляет доступ к элементам управления ASP.NET в разделе заголовка панели. Свойство `ContentContainer` `AccordionPane` выполняет то же самое для раздела содержимого панели. Это позволяет ASP.NET коду добавлять содержимое на панели:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

Наконец, необходимо добавить панели в `Panes` коллекцию элементов:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

Ниже приведен полный код на стороне сервера, который добавляет две панели в элемент управления "гармошка":

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

Единственным отсутствующим элементом является сам объект, который зависит от наличия элемента управления `ScriptManager` ASP.NET:

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

Чтобы завершить этот пример, два класса CSS, упоминаемые в элементе управления "гармошка", предоставляют сведения о стиле для браузера:

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]

[![данные в элементе "гармошка" были динамически добавлены с помощью кода на стороне сервера](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)

Данные в элементе "гармошка" были динамически добавлены кодом на стороне сервера ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-adding-an-accordion-pane-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](databinding-to-an-accordion-vb.md)
