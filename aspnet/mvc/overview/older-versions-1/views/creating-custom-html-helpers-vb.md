---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Создание настраиваемых вспомогательных методов HTML (Visual Basic) | Документация Майкрософт
author: microsoft
description: Целью данного учебника — продемонстрировать, как можно создать пользовательские вспомогательных методов HTML, который можно использовать внутри представлений MVC. Используя преимущества вспомогательный метод HTML...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: e62e47bceddc516af7aa18fc66ed4ca4d704d277
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034951"
---
<a name="creating-custom-html-helpers-vb"></a>Создание настраиваемых вспомогательных методов HTML (VB)
====================
по [Microsoft](https://github.com/microsoft)

[Загрузить PDF-файл](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> Целью данного учебника — продемонстрировать, как можно создать пользовательские вспомогательных методов HTML, который можно использовать внутри представлений MVC. Используя преимущества вспомогательных методов HTML, можно уменьшить объем длительного ввода HTML-тегов, что необходимо выполнить, чтобы создать стандартную страницу HTML.


Целью данного учебника — продемонстрировать, как можно создать пользовательские вспомогательных методов HTML, который можно использовать внутри представлений MVC. Используя преимущества вспомогательных методов HTML, можно уменьшить объем длительного ввода HTML-тегов, что необходимо выполнить, чтобы создать стандартную страницу HTML.

В первой части этого руководства я опишу некоторые из существующих вспомогательных методов HTML, включенный в состав ASP.NET MVC framework. Затем я опишу два метода создания настраиваемых вспомогательных методов HTML: Я описывается создание настраиваемых вспомогательных методов HTML, создавая общий метод и путем создания метода расширения.

## <a name="understanding-html-helpers"></a>Основные сведения о вспомогательных методов HTML

Вспомогательный метод HTML — это метод, возвращает строку. Строка может представлять любой тип содержимого, которое. Например, можно использовать вспомогательные методы HTML для визуализации стандартный HTML-теги HTML `<input>` и `<img>` теги. Также можно использовать вспомогательные методы HTML для отображения более сложного содержимого, например с вкладками или HTML-таблицы базы данных.

Платформа ASP.NET MVC включает следующий набор стандартных вспомогательных методов HTML (это не полный список):

- Html.ActionLink()
- Html.BeginForm()
- Html.CheckBox()
- Html.DropDownList()
- Html.EndForm()
- Html.Hidden()
- Html.ListBox()
- Html.Password()
- Html.RadioButton()
- Html.TextArea()
- Html.TextBox()

Например рассмотрим формы в листинге 1. Эта форма подготавливается к просмотру с помощью двух стандартных вспомогательных методов HTML (см. рис. 1). Используемый этой формой `Html.BeginForm()` и `Html.TextBox()` вспомогательные методы.


[![Страница отображается с помощью вспомогательных методов HTML](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**Рис 01**: Страница отображается с помощью вспомогательных методов HTML ([Просмотр полноразмерного изображения](creating-custom-html-helpers-vb/_static/image3.png))


**Листинг 1. `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

`Html.BeginForm()` Вспомогательный метод используется для создания HTML-код открывающей и закрывающей `<form>` теги. Обратите внимание, что `Html.BeginForm()` был вызван в с помощью инструкции. Оператор using гарантирует, что `<form>` тег закрывается в конце, используя блок.

Если вы предпочитаете, вместо создания с помощью блока, можно вызвать Html.EndForm() вспомогательный метод для закрытия `<form>` тега. Использование подхода к созданию открывающий и закрытие `<form>` тег, который наиболее интуитивно понятно вам.

`Html.TextBox()` Вспомогательные методы, используются для визуализации HTML в листинге 1 `<input>` теги. Если выбрать Просмотр исходного кода в браузере отобразится исходный код HTML в листинге 2. Обратите внимание на то, что источник содержит стандартный HTML-теги.

> [!IMPORTANT]
> Обратите внимание, что `Html.TextBox()`-HTML вспомогательный визуализируется с `<%= %>` теги вместо `<% %>` теги. Если вы не включаете знак равенства, ничего не возвращает выводятся в браузер.

Платформа ASP.NET MVC содержит небольшой набор вспомогательных функций. Скорее всего потребуется расширить платформа MVC с помощью пользовательских вспомогательных методов HTML. В оставшейся части этого руководства вы узнаете два метода создания настраиваемых вспомогательных методов HTML.

**Листинг 2. `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>Создание вспомогательных методов HTML с помощью общих методов

Чтобы создать новый вспомогательный метод HTML проще всего создать общий метод, который возвращает строку. Представим, к примеру, что вам потребуется создать новый вспомогательный метод HTML, который выводит HTML- `<label>` тега. Для подготовки к просмотру, можно использовать класс в листинге 2 `<label>`.

**Листинг 2. `Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

Нет ничего особенного классу в листинге 2. `Label()` Метод просто возвращает строку.

Представление измененного индекса в листинге 3 использует `LabelHelper` для отрисовки HTML `<label>` теги. Обратите внимание, что представление содержит `<%@ imports %>` директива, которая импортирует пространство имен Application1.Helpers.

**Листинг 2. `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Создание вспомогательных методов HTML с помощью методов расширения

Если вы хотите создать вспомогательные методы HTML, которые работают так же как стандартный вспомогательных методов HTML, включены в платформе ASP.NET MVC, то необходимо создать методы расширения. Методы расширения позволяют добавлять новые методы в существующий класс. При создании метода вспомогательный метод HTML, можно добавить новые методы `HtmlHelper` класса, представленного параметром свойства Html представления.

Модуль Visual Basic в листинге 3 добавляет метод расширения с именем `Label()` для `HtmlHelper` класса. Существует несколько моментов, которые следует заметить, сведения об этом модуле. Во-первых, обратите внимание, что модуль дополняется `<Extension()>` атрибута. Чтобы использовать этот атрибут, необходимо импортировать `System.Runtime.CompilerServices` пространства имен

Во-вторых, обратите внимание, что первый параметр `Label()` представляет метод `HtmlHelper` класса. Первый параметр метода расширения указывает класс, который расширяет метод расширения.

**Листинг 3. `Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

После создания метода расширения и успешной сборки приложения, метод расширения отображается в Intellisense в Visual Studio как и все другие методы класса (см. рис. 2). Единственная разница в расширения методы отображаются с символом "специальный" рядом с ними (значок стрелки вниз).


[![С помощью метода расширения Html.Label()](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**Рис. 02**: С помощью метода расширения Html.Label() ([Просмотр полноразмерного изображения](creating-custom-html-helpers-vb/_static/image6.png))


Измененный представление Index в листинге 4 используется метод расширения Html.Label() для подготовки к просмотру все его &lt;метка&gt; теги.

**Листинг 4. `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>Сводка

В этом руководстве вы узнали, два метода создания настраиваемых вспомогательных методов HTML. Во-первых, вы узнали, как можно создавать пользовательские `Label()` вспомогательный метод HTML, создав общий метод, который возвращает строку. Далее вы узнали, как можно создавать пользовательские `Label()` метод вспомогательный метод HTML, создав метод расширения для `HtmlHelper` класса.

В этом учебнике я сосредоточился на создании метод очень простой вспомогательный метод HTML. Учтите, что вспомогательный метод HTML могут быть настолько сложный, как требуется. Вы можете создавать вспомогательные функции HTML, отображения форматированное содержимое, например представления в виде дерева, меню или таблиц базы данных.

> [!div class="step-by-step"]
> [Назад](asp-net-mvc-views-overview-vb.md)
> [Вперед](using-the-tagbuilder-class-to-build-html-helpers-vb.md)