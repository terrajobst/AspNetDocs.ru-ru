---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: Часть 7. Создание главной страницы | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599991"
---
# <a name="part-7-creating-the-main-page"></a>Часть 7. Создание главной страницы

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>Создание главной страницы

В этом разделе вы создадите страницу основного приложения. Эта страница будет более сложной, чем страница администрирования, поэтому мы будем использовать ее в нескольких шагах. Кстати, вы увидите некоторые более сложные методы маскирования. js. Вот базовый макет страницы:

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- "Products" содержит массив продуктов.
- "Корзина" содержит массив продуктов с количествами. При выборе пункта "добавить в корзину" обновляется корзина.
- "Orders" содержит массив идентификаторов заказов.
- "Details" содержит сведения о заказе — массив элементов (продукты с количествами).

Начнем с определения базовой структуры в формате HTML без привязки данных или скрипта. Откройте файл Views/Home/Index. cshtml и замените все содержимое следующим:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

Затем добавьте раздел Scripts и создайте пустую модель представления:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

В зависимости от проекта, разработанного ранее, нашей модели представления требуется observable для продуктов, корзин, заказов и сведений. Добавьте следующие переменные в объект `AppViewModel`:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

Пользователи могут добавлять элементы из списка продуктов в корзину и удалять элементы из корзины. Чтобы инкапсулировать эти функции, мы создадим еще один класс представления — модель, представляющий продукт. Добавьте следующий код в файл `AppViewModel`:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

Класс `ProductViewModel` содержит две функции, которые используются для перемещения продукта в корзину и из нее: `addItemToCart` добавляет одну единицу продукта в корзину и `removeAllFromCart` удаляет все количества продуктов.

Пользователи могут выбрать существующий заказ и получить сведения о заказе. Мы будем инкапсулировать эту функцию в другую модель представления:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel` инициализируется заказом и извлекает сведения о заказе путем отправки запроса AJAX на сервер.

Кроме того, обратите внимание на свойство `total` в `OrderDetailsViewModel`. Это свойство является особым видом наблюдаемого, называемого [вычисленным наблюдаемым](http://knockoutjs.com/documentation/computedObservables.html). Как следует из названия, вычисленный наблюдаемый объект позволяет выполнить привязку данных к вычисленному значению&#8212;в данном случае, а также к общей стоимости заказа.

Затем добавьте эти функции в `AppViewModel`:

- `resetCart` удаляет все элементы из корзины.
- `getDetails` получает сведения о заказе (путем помещения нового `OrderDetailsViewModel` в список `details`).
- `createOrder` создает новый заказ и очищает корзину.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

Наконец, инициализируйте модель представления, делая запросы AJAX для продуктов и заказов:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

Ладно, это большой объем кода, но мы создали его пошаговым образом, поэтому будем надеяться, что проектирование ясно. Теперь к HTML можно добавить несколько привязок маскирования. js.

**Продуктов**

Ниже приведены привязки для списка продуктов.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

Это перебирает массив Products и отображает имя и цену. Кнопка "добавить в порядок" отображается только в том случае, если пользователь вошел в систему.

Кнопка "добавить в заказ" вызывает `addItemToCart` в экземпляре `ProductViewModel` для продукта. Это демонстрирует удобную функцию файла выколачивание. js: когда модель представления содержит другие модели представления, можно применить привязки к внутренней модели. В этом примере привязки в `foreach` применяются к каждому из экземпляров `ProductViewModel`. Этот подход намного более понятен, чем помещение всех функциональных возможностей в одну модель представления.

**Покупатель**

Ниже приведены привязки для корзины.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

Это перебирает массив корзины и отображает имя, цену и количество. Обратите внимание, что ссылка "Удалить" и кнопка "создать заказ" привязаны к функциям модели представления.

**Перемещен**

Ниже приведены привязки для списка Orders:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

Будет выполнена итерация по заказам и показан идентификатор заказа. Событие щелчка по ссылке привязано к функции `getDetails`.

**Сведения о заказе**

Ниже приведены привязки для сведений о заказе.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

Это перебирает элементы в порядке и отображает продукт, цену и количество. Окружающий элемент DIV отображается только в том случае, если массив Details содержит один или несколько элементов.

## <a name="conclusion"></a>Заключение

В этом руководстве вы создали приложение, которое использует Entity Framework для взаимодействия с базой данных и веб-API ASP.NET для предоставления общедоступного интерфейса поверх уровня данных. Мы используем ASP.NET MVC 4 для подготовки к просмотру страниц HTML, а также маскирования. js Plus jQuery, чтобы обеспечить динамическое взаимодействие без перегрузок страниц.

Дополнительные ресурсы:

- [Схема содержимого ASP.NET доступа к данным](https://msdn.microsoft.com/library/6759sth4.aspx)
- [Центр разработчиков Entity Framework](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [Назад](using-web-api-with-entity-framework-part-6.md)
