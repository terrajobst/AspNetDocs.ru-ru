---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: Часть 4. Перечисление продуктов | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств описаны все действия, предпринимаемые для создайте пример приложения Tailspin Spyworks. Часть 4 охватывает список продуктов с GridView контракту...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: ca7eccd684473d9a1ec4a8adfd8690b291fe702f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043271"
---
<a name="part-4-listing-products"></a>Часть 4. Публикация продуктов
====================
по [(Joe Stagner)](https://github.com/JoeStagner)

> Tailspin Spyworks демонстрирует, как чрезвычайно прост процесс создания мощных и масштабируемых приложений для платформы .NET. Он демонстрирует способы использования новые возможности в ASP.NET 4 для создание Интернет-магазина, включая покупок, извлечения и администрирования.
> 
> В этой серии руководств описаны все действия, предпринимаемые для создайте пример приложения Tailspin Spyworks. Часть 4 охватывает список продуктов с помощью элемента управления GridView.


## <a id="_Toc260221670"></a>  Список продуктов с помощью элемента управления GridView

Давайте начнем реализация наших ProductsList.aspx страницы «Щелкните правой кнопкой» на наше решение и выбрав пункт «Добавить» и «Новый элемент».

![](tailspin-spyworks-part-4/_static/image1.jpg)

Выберите «Веб-формы с помощью главного страница» и введите имя страницы ProductsList.aspx».

Нажмите кнопку «Добавить».

![](tailspin-spyworks-part-4/_static/image2.jpg)

Затем выберите папку «Стили», где мы разместили на страницу Site.Master и выберите его из окна «Содержимое папки».

![](tailspin-spyworks-part-4/_static/image3.jpg)

Нажмите кнопку «ОК», чтобы создать страницу.

Наши базы данных заполняется данные о продуктах, как показано ниже.

![](tailspin-spyworks-part-4/_static/image4.jpg)

После создания нашу страницу еще раз мы будем использовать источник данных сущности для доступа к этим данным продукта, но в данном экземпляре, нам необходимо выбрать сущности «продукт», и нам нужно ограничить элементы, которые возвращаются только теми, для выбранной категории.

Для выполнения этой задачи мы скажем EntityDataSource для автоматического создания в предложении WHERE мы также укажем WhereParameter.

Как вы помните, что когда мы создавали пунктов меню в нашей «меню категории продукта» мы динамическим образом строится ссылку, добавив CatagoryID в строку запроса для каждого канала. Вы будете уведомлены об источнике данных сущности для параметра WHERE являются производными этого параметра строки запроса.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

Затем мы настроим элемент управления ListView для отображения списка продуктов. Чтобы создать оптимальный способ осуществления покупок, мы будем сжатой несколько функций краткими каждого отдельного продукта, отображаемый в наших ListVew.

- Имя продукта будет ссылка на подробные сведения о продукте.
- Отображается цена продукта.
- Изображение продукта будет выведен список динамически выберем изображение из каталога каталог образов в нашем приложении.
- Мы добавим ссылку, чтобы сразу же добавить конкретного продукта в корзину для покупок.

Далее приведена разметка для наш экземпляр элемента управления ListView.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

Мы создаем динамически несколько ссылок для каждого отображаемого продукта.

Кроме того прежде чем мы протестировать собственную новую страницу необходимо создать структуру каталогов для продукта изображений каталога следующим образом.

![](tailspin-spyworks-part-4/_static/image1.png)

После доступны наши образы продукта можно проверить страницы со списком наших продуктов.

![](tailspin-spyworks-part-4/_static/image5.jpg)

На домашней странице веб-узла щелкните одну из ссылок списка категорий.

![](tailspin-spyworks-part-4/_static/image6.jpg)

Теперь нам нужно реализовать ProductDetials.apsx страницу и функцию AddToCart.

Используйте файл -&gt;создать, чтобы создать имя страницы ProductDetails.aspx, с помощью главной страницы узла, как это было сделано ранее.

Мы будем использовать элемент управления EntityDataSource снова получить доступ к определенной записи продукта в базе данных, и мы будем использовать элемент управления ASP.NET FormView для отображения данных продукта следующим образом.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

Не беспокойтесь, если форматирование выглядит немного странно для вас. Приведенный выше код разметки оставляет место в формат вывода для несколько возможностей, которые мы реализуем позже.

Корзина для покупок будет представлять более сложная логика в приложении. Чтобы приступить к работе, используйте файл -&gt;создать, чтобы создать страница с именем MyShoppingCart.aspx.

Обратите внимание на то, что мы не следует выбирать имя ShoppingCart.aspx.

Наши база данных содержит таблицу с именем «ShoppingCart». При создании модели EDM для каждой таблицы в базе данных был создан класс. Таким образом в модели EDM создается класс сущностей с именем «ShoppingCart». Нам удалось изменить модель так, мы может использовать это имя для нашей корзину для покупок реализации или расширить его для наших потребностей, но мы будет выбрать вместо этого просто выберите имя, которое позволит избежать конфликта.

Также стоит отметить, что мы создадим простой корзины для покупок и внедрение корзины для покупок логику с отображением корзину для покупок. Мы также можно реализовать Корзина никак не связано бизнес-уровне.

> [!div class="step-by-step"]
> [Назад](tailspin-spyworks-part-3.md)
> [Вперед](tailspin-spyworks-part-5.md)