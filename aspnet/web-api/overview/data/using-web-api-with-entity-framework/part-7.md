---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: Создание представления (пользовательский интерфейс) | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448986"
---
# <a name="create-the-view-ui"></a>Создание представления (пользовательский интерфейс)

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://github.com/MikeWasson/BookService)

В этом разделе вы начнете определить HTML для приложения и добавить привязку данных между HTML и моделью представления.

Откройте файл Views/Home/Index. cshtml. Замените все содержимое этого файла следующим.

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

Большая часть элементов `div` существует для стиля [начальной загрузки](http://getbootstrap.com/) . Важные элементы — это объекты с атрибутами `data-bind`. Этот атрибут связывает HTML с моделью представления.

Пример:

[!code-html[Main](part-7/samples/sample2.html)]

В этом примере Привязка &quot;`text`&quot; приводит к тому, что элемент `<p>` отображает значение свойства `error` из модели представления. Помните, что `error` был объявлен как `ko.observable`:

[!code-javascript[Main](part-7/samples/sample3.js)]

Всякий раз, когда новому значению присваивается `error`, выколачивание обновляет текст в элементе `<p>`.

Привязка `foreach` передается в цикл по содержимому массива `books`. Для каждого элемента в массиве выколачивание создает новый элемент &lt;Li&gt;. Привязки в контексте `foreach` ссылаются на свойства элемента массива. Пример:

[!code-html[Main](part-7/samples/sample4.html)]

Здесь привязка `text` считывает свойство Author каждой книги.

Если запустить приложение сейчас, оно должно выглядеть следующим образом:

![](part-7/_static/image1.png)

Список книг загружается асинхронно после загрузки страницы. Сейчас &quot;сведения&quot; ссылок не работают. Мы добавим эту функцию в следующем разделе.

> [!div class="step-by-step"]
> [Назад](part-6.md)
> [Вперед](part-8.md)
