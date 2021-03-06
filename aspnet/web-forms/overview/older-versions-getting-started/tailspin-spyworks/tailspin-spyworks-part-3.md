---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: Часть 3. меню «Макет» и «Категория» | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 3 описывается добавление макета и меню категорий.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519102"
---
# <a name="part-3-layout-and-category-menu"></a>Часть 3. меню «Макет» и «Категория»

кем [Джо Stagner)](https://github.com/JoeStagner)

> В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET. Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.
> 
> В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 3 описывается добавление макета и меню категорий.

## <a id="_Toc260221669"></a>Добавление макета и меню категорий

На главной странице сайта мы добавим div для столбца с левой стороны, который будет содержать меню нашей категории продуктов.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

Обратите внимание, что для класса CSS, который мы добавили в файл style. CSS, будет предоставлено нужное соответствие и другое форматирование.

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

Меню категории продуктов будет динамически создано во время выполнения путем запроса к базе данных Commerce для существующих категорий продуктов и создания пунктов меню и соответствующих ссылок.

Для этого мы будем использовать два ASP. Мощные элементы управления данными .NET. Элемент управления "источник данных сущности" и элемент управления "ListView".

![](tailspin-spyworks-part-3/_static/image1.jpg)

Давайте перейдем к «представлению конструктора» и используем для настройки элементов управления вспомогательными командами.

![](tailspin-spyworks-part-3/_static/image2.jpg)

Давайте присвойте свойству идентификатора EntityDataSource значение EDS\_категории\_меню и щелкните "настроить источник данных".

![](tailspin-spyworks-part-3/_static/image3.jpg)

Выберите подключение Коммерцеентитиес, которое было создано для нас при создании модели источников данных сущностей для нашей базы данных Commerce, и нажмите кнопку "Далее".

![](tailspin-spyworks-part-3/_static/image4.jpg)

Выберите имя набора сущностей "категории" и оставьте остальные параметры по умолчанию. Нажмите кнопку "Готово".

Теперь давайте зададим свойство ID экземпляра элемента управления ListView, который мы поместили на странице в ListView\_Продуктсмену и активируйте его вспомогательную функцию.

![](tailspin-spyworks-part-3/_static/image5.jpg)

Несмотря на то, что можно использовать параметры управления для форматирования отображения и форматирования элементов данных, для создания нашего меню потребуется только простая разметка, поэтому мы будем вводить код в представлении исходного кода.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

Обратите внимание на инструкцию eval: &lt;% # eval ("CategoryName")%&gt;

Синтаксис ASP.NET &lt;% #%&gt; является сокращенным соглашением, которое указывает среде выполнения выполнить все, что содержится в, и выводит результаты "в строке".

Инструкция eval ("CategoryName") указывает, что для текущей записи в привязанной коллекции элементов данных необходимо получить значение имен элементов модели сущности "CategoryName". Это краткий синтаксис для очень мощной функции.

Теперь можно запустить приложение.

![](tailspin-spyworks-part-3/_static/image6.jpg)

Обратите внимание, что теперь меню «Категория продукта» отображается, а при наведении указателя мыши на один из пунктов меню «Категория» ссылка на пункт меню будет указывать на страницу, которой мы еще не реализовали с именем Продуктслист. aspx и что мы создали динамический аргумент строки запроса, содержащий  Идентификатор категории.

> [!div class="step-by-step"]
> [Назад](tailspin-spyworks-part-2.md)
> [Вперед](tailspin-spyworks-part-4.md)
