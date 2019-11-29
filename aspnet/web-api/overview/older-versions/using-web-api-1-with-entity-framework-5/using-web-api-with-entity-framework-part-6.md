---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: Часть 6. Создание контроллеров продуктов и заказов | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600028"
---
# <a name="part-6-creating-product-and-order-controllers"></a>Часть 6. Создание контроллеров продуктов и заказов

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a>Добавление контроллера продуктов

Административный контроллер предназначен для пользователей с правами администратора. Клиенты, с другой стороны, могут просматривать продукты, но не могут создавать, обновлять или удалять их.

Можно легко ограничить доступ к методам POST, WHERE и DELETE, не открывая методы Get. Но взгляните на данные, возвращаемые для продукта:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

Свойство `ActualCost` не должно быть видимым для клиентов! Решение заключается в определении *объекта передачи данных* (DTO), который включает подмножество свойств, которые должны быть видимыми для клиентов. Для `ProductDTO` экземпляров мы будем использовать LINQ to Project `Product` Instances.

Добавьте класс с именем `ProductDTO` в папку Models.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

Теперь добавьте контроллер. В обозреватель решений щелкните правой кнопкой мыши папку Controllers. Нажмите кнопку **Добавить**, а затем выберите **контроллер**. В диалоговом окне **Добавление контроллера введите** имя контроллера &quot;продуктсконтроллер&quot;. В разделе **шаблон**выберите **пустой контроллер API**.

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

Замените все в исходном файле следующим кодом:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

Контроллер по-прежнему использует `OrdersContext` для запроса к базе данных. Но вместо того, чтобы возвращать экземпляры `Product` напрямую, мы вызываем `MapProducts` для проецирования их на экземпляры `ProductDTO`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

Метод `MapProducts` возвращает **IQueryable**, поэтому мы можем составить результат с другими параметрами запроса. Это можно увидеть в методе `GetProduct`, который добавляет к запросу предложение **WHERE** :

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a>Добавление контроллера заказов

Затем добавьте контроллер, позволяющий пользователям создавать и просматривать заказы.

Мы начнем с другого DTO. В обозреватель решений щелкните правой кнопкой мыши папку Models и добавьте класс с именем `OrderDTO` использовать следующую реализацию:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

Теперь добавьте контроллер. В обозреватель решений щелкните правой кнопкой мыши папку Controllers. Нажмите кнопку **Добавить**, а затем выберите **контроллер**. В диалоговом окне **Добавление контроллера** задайте следующие параметры.

- В разделе **имя контроллера**введите "ордерсконтроллер".
- В разделе **шаблон**выберите "контроллер API с действиями чтения и записи, используя Entity Framework".
- В разделе **класс модели**выберите&quot;порядок &quot;(Продуктсторе. Models).
- В разделе **класс контекста данных**выберите &quot;Ордерсконтекст (Продуктсторе. Models)&quot;.

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

Нажмите кнопку **Добавить**. При этом добавляется файл с именем OrdersController.cs. Далее необходимо изменить реализацию контроллера по умолчанию.

Сначала удалите методы `PutOrder` и `DeleteOrder`. В этом примере клиенты не могут изменять или удалять существующие заказы. В реальных приложениях для обработки таких случаев потребуется много серверной логики. (Например, был ли уже отгружен заказ?)

Измените метод `GetOrders`, чтобы возвращались только заказы, принадлежащие пользователю.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

Измените метод `GetOrder` следующим образом:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

Ниже приведены изменения, внесенные в метод.

- Возвращаемое значение — это `OrderDTO` экземпляр, а не `Order`.
- При запросе базы данных для заказа мы используем метод [дбкуери. include](https://msdn.microsoft.com/library/gg696395) для получения связанных `OrderDetail` и `Product` сущностей.
- Мы будем сводить результаты с помощью проекции.

HTTP-ответ будет содержать массив продуктов с количествами:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

Этот формат легче использовать для клиентов, чем исходный граф объектов, который содержит вложенные сущности (Order, Details и Products).

Последний метод, который следует рассмотреть `PostOrder`. Сейчас этот метод принимает `Order` экземпляр. Но рассмотрим, что произойдет, если клиент отправляет текст запроса следующим образом:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

Это хорошо структурированный порядок, который Entity Framework, в своюмся случае, будет куда-то вставить в базу данных. Но она содержит сущность Product, которая ранее не существовала. Клиент только что создал новый продукт в нашей базе данных! Это будет неожиданным для отдела выполнения заказов, когда он увидит заказ на Koala. Мораль — это, по сути, тщательный анализ данных, принимаемых в запросе POST или Request.

Чтобы избежать этой проблемы, измените метод `PostOrder` для получения экземпляра `OrderDTO`. Для создания `Order`используйте `OrderDTO`.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

Обратите внимание, что мы используем свойства `ProductID` и `Quantity` и будем пропускать все значения, отправленные клиентом по названию или цене продукта. Если идентификатор продукта недействителен, он нарушает ограничение внешнего ключа в базе данных, и вставка завершится ошибкой, как это должно произойти.

Ниже приведен полный метод `PostOrder`.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

Наконец, добавьте к контроллеру атрибут **авторизации** :

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

Теперь только зарегистрированные пользователи могут создавать или просматривать заказы.

> [!div class="step-by-step"]
> [Назад](using-web-api-with-entity-framework-part-5.md)
> [Вперед](using-web-api-with-entity-framework-part-7.md)
