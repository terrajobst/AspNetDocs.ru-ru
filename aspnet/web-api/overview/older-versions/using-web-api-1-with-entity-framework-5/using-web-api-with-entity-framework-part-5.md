---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: Часть 5. Создание динамического пользовательского интерфейса с помощью маскирования. js | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599997"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>Часть 5. Создание динамического пользовательского интерфейса с помощью маскирования. js

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>Создание динамического пользовательского интерфейса с помощью Knockout.js

В этом разделе мы будем использовать маскирование. js для добавления функциональных возможностей в административное представление.

[Выколачивание. js](http://knockoutjs.com/) — это библиотека JavaScript, которая позволяет легко привязывать элементы управления HTML к данным. В маскировании. js используется шаблон Model-View-ViewModel (MVVM).

- *Модель* — это серверное представление данных в бизнес-домене (в нашем случае это продукты и заказы).
- *Представление* — это уровень представления (HTML).
- *Модель представления* — это объект JavaScript, который содержит данные модели. Модель представления — это абстракция кода пользовательского интерфейса. Он не имеет сведений о представлении HTML. Вместо этого он представляет абстрактные функции представления, например "список элементов".

Представление привязано к данным в модели представления. Обновления модели представления автоматически отражаются в представлении. Модель представления также получает события из представления, такие как нажатия кнопки, и выполняет операции с моделью, например создание заказа.

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

Сначала мы определим модель представления. После этого мы будем привязывать разметку HTML к модели представления.

Добавьте следующий раздел Razor в Admin. cshtml:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

Этот раздел можно добавить в любое место в файле. Когда представление отображается, раздел появляется в нижней части страницы HTML, прямо перед закрывающим тегом &lt;/боди&gt;.

Весь скрипт для этой страницы будет находиться внутри тега script, указанного комментарием:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

Сначала определите класс представление-модель:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**KO. обсерваблеаррай** — это особый тип объекта в маскировании, который называется *наблюдаемым*. Из [документации по выколачивание. js](http://knockoutjs.com/documentation/observables.html)можно наблюдать за объектом JavaScript, который может уведомлять подписчиков об изменениях. При изменении содержимого наблюдаемого изменения представление автоматически обновляется для соответствия.

Чтобы заполнить массив `products`, выполните запрос AJAX к веб-API. Помните, что мы сохранили базовый URI для API в контейнере представлений (см. [часть 4](using-web-api-with-entity-framework-part-4.md) учебника).

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

Затем добавьте функции в модель представления для создания, обновления и удаления продуктов. Эти функции отправляют вызовы AJAX в веб-API и используют результаты для обновления модели представления.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

Теперь самая важная часть: когда модель DOM полностью загружена, вызовите функцию **KO. апплибиндингс** и передайте новый экземпляр `ProductsViewModel`:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

Метод **KO. апплибиндингс** активирует маскирование и подсоединяет модель представления к представлению.

Теперь, когда у нас есть модель представления, можно создать привязки. В выколачивание. js это можно сделать, добавив атрибуты `data-bind` в элементы HTML. Например, чтобы привязать список HTML к массиву, используйте привязку `foreach`:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

Привязка `foreach` выполняет итерацию по массиву и создает дочерние элементы для каждого объекта в массиве. Привязки к дочерним элементам могут ссылаться на свойства объектов Array.

Добавьте следующие привязки в список "обновить продукты":

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

Элемент `<li>` находится в области привязки **foreach** . Это означает, что выколачивание будет визуализировать элемент один раз для каждого продукта в массиве `products`. Все привязки в элементе `<li>` ссылаются на этот экземпляр продукта. Например, `$data.Name` ссылается на свойство `Name` в продукте.

Чтобы задать значения для текстовых входов, используйте привязку `value`. Кнопки привязаны к функциям в представлении "модель" с помощью привязки `click`. Экземпляр продукта передается в качестве параметра каждой функции. Дополнительные сведения см. в [документации по выколачивание. js](http://knockoutjs.com/documentation/observables.html) с хорошим описанием различных привязок.

Затем добавьте привязку для события **Submit** в форму Добавление продукта:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

Эта привязка вызывает функцию `create` в модели представления для создания нового продукта.

Ниже приведен полный код представления администрирования.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

Запустите приложение, войдите в систему с помощью учетной записи администратора и щелкните ссылку Admin (администратор). Вы должны увидеть список продуктов и иметь возможность создавать, обновлять или удалять продукты.

> [!div class="step-by-step"]
> [Назад](using-web-api-with-entity-framework-part-4.md)
> [Вперед](using-web-api-with-entity-framework-part-6.md)
