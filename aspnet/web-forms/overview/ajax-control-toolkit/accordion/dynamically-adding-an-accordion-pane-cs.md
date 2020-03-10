---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: Динамическое добавление панели «Гармошка»C#() | Документация Майкрософт
author: wenz
description: Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 2834f56bd77c412923f4a8f382e670727f70eae4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497982"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a>Динамическое добавление панели «Гармошка»C#()

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)

> Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются внутри самой страницы, но для достижения того же результата можно использовать код на стороне сервера.

## <a name="overview"></a>Обзор

Элемент управления "гармошка" в наборе средств AJAX Control Toolkit предоставляет несколько панелей и позволяет пользователю отображать один из них за раз. Панели обычно объявляются внутри самой страницы, но для достижения того же результата можно использовать код на стороне сервера.

## <a name="steps"></a>Шаги

Элемент управления "гармошка" предоставляет все важные свойства коду на стороне сервера. Помимо прочего, свойство `Panes` предоставляет доступ к коллекции панелей, составляющих гармошка. Каждая панель имеет тип `AccordionPane`. Таким образом, упрощена создание такой области:

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

Свойство `HeaderContainer` `AccordionPane` предоставляет доступ к элементам управления ASP.NET в разделе заголовка панели. Свойство `ContentContainer` `AccordionPane` выполняет то же самое для раздела содержимого панели. Это позволяет ASP.NET коду добавлять содержимое на панели:

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

Наконец, необходимо добавить панели в `Panes` коллекцию элементов:

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

Ниже приведен полный код на стороне сервера, который добавляет две панели в элемент управления "гармошка":

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

Единственным отсутствующим элементом является сам объект, который зависит от наличия элемента управления `ScriptManager` ASP.NET:

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

Чтобы завершить этот пример, два класса CSS, упоминаемые в элементе управления "гармошка", предоставляют сведения о стиле для браузера:

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

[![данные в элементе "гармошка" были динамически добавлены с помощью кода на стороне сервера](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

Данные в элементе "гармошка" были динамически добавлены кодом на стороне сервера ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-adding-an-accordion-pane-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](databinding-to-an-accordion-cs.md)
> [Вперед](databinding-to-an-accordion-vb.md)
