---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: Отношения сущностей в OData v4 с использованием веб-API ASP.NET 2,2 | Документация Майкрософт
author: MikeWasson
description: 'Большинство наборов данных определяют связи между сущностями: у клиентов есть заказы. книги имеют авторов; продукты имеют поставщики. С помощью OData клиенты могут перемещаться по...'
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484464"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>Отношения сущностей в OData v4 с использованием веб-API ASP.NET 2,2

по [Майк Уоссон](https://github.com/MikeWasson)

> Большинство наборов данных определяют связи между сущностями: у клиентов есть заказы. книги имеют авторов; продукты имеют поставщики. С помощью OData клиенты могут перемещаться по связям сущностей. С учетом продукта можно найти поставщика. Также можно создавать и удалять связи. Например, можно задать поставщика для продукта.
>
> В этом руководстве показано, как поддерживать эти операции в OData v4 с помощью веб-API ASP.NET. Руководство по построению в руководстве по [созданию конечной точки OData v4 с помощью веб-API ASP.NET 2](create-an-odata-v4-endpoint.md).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
> - Веб-API 2,1
> - OData v4
> - Visual Studio 2013 (Скачайте Visual Studio 2017 [здесь](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - Entity Framework 6
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>Учебные версии
>
> Сведения для OData версии 3 см. [в разделе Поддержка связей сущностей в OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).

## <a name="add-a-supplier-entity"></a>Добавление сущности поставщика

> [!NOTE]
> Руководство по построению в руководстве по [созданию конечной точки OData v4 с помощью веб-API ASP.NET 2](create-an-odata-v4-endpoint.md).

Во-первых, нам нужна связанная сущность. Добавьте класс с именем `Supplier` в папку Models.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

Добавьте свойство навигации в класс `Product`:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

Добавьте новый **DbSet** в класс `ProductsContext`, чтобы Entity Framework включала таблицу поставщика в базе данных.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

В WebApiConfig.cs добавьте поставщики &quot;&quot; набор сущностей в модель EDM:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>Добавление контроллера поставщиков

Добавьте класс `SuppliersController` в папку Controllers.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

Я не буду показывать, как добавить операции CRUD для этого контроллера. Эти шаги те же, что и для контроллера Products (см. раздел [Создание конечной точки OData v4](create-an-odata-v4-endpoint.md)).

## <a name="getting-related-entities"></a>Получение связанных сущностей

Чтобы получить поставщик для продукта, клиент отправляет запрос GET:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

Для поддержки этого запроса добавьте в класс `ProductsController` следующий метод:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

Этот метод использует соглашение об именовании по умолчанию

- Имя метода: Жеткс, где X — это свойство навигации.
- Имя параметра: *ключ*

Если следовать этому соглашению об именовании, веб-API автоматически сопоставляет запрос HTTP методу контроллера.

Пример HTTP-запроса:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

Пример HTTP-ответа:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>Получение связанной коллекции

В предыдущем примере продукт имеет одного поставщика. Свойство навигации также может возвращать коллекцию. Следующий код получает продукты для поставщика:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

В этом случае метод возвращает **IQueryable** , а не **синглересулт&lt;t&gt;**

Пример HTTP-запроса:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

Пример HTTP-ответа:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>Создание связи между сущностями

OData поддерживает создание или удаление связей между двумя существующими сущностями. В терминологии OData версии 4 отношение является &quot;ссылкой&quot;. (В OData v3 связь называлась *ссылкой*. Различия в протоколе не важны для работы с этим руководством.)

Ссылка имеет собственный URI с формой `/Entity/NavigationProperty/$ref`. Например, ниже приведен URI для обращения к ссылке между продуктом и его поставщиком.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

Чтобы добавить связь, клиент отправляет запрос POST или помещается по этому адресу.

- Помещайте, если свойство навигации является одной сущностью, например `Product.Supplier`.
- POST, если свойство навигации является коллекцией, например `Supplier.Products`.

Текст запроса содержит URI другой сущности в отношении. Ниже приведен пример запроса:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

В этом примере клиент отправляет запрос на размещение в `/Products(6)/Supplier/$ref`, который является $ref URI для `Supplier` продукта с ИДЕНТИФИКАТОРом 6. Если запрос выполнен, сервер отправляет ответ 204 (без содержимого):

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

Ниже приведен метод контроллера для добавления отношения к `Product`.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

Параметр *navigationProperty* указывает, какую связь следует задать. (Если в сущности имеется более одного свойства навигации, можно добавить дополнительные операторы `case`.)

Параметр *Link* содержит универсальный код ресурса (URI) поставщика. Веб-API автоматически анализирует текст запроса, чтобы получить значение для этого параметра.

Для поиска поставщика требуется идентификатор (или ключ), который является частью параметра *Link* . Для этого используйте следующий вспомогательный метод:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

По сути, этот метод использует библиотеку OData для разделения пути URI на сегменты, поиска сегмента, содержащего ключ, и преобразования ключа в правильный тип.

## <a name="deleting-a-relationship-between-entities"></a>Удаление связи между сущностями

Чтобы удалить связь, клиент отправляет запрос HTTP DELETE в URI $ref:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

Ниже приведен метод контроллера для удаления связи между продуктом и поставщиком.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

В этом случае `Product.Supplier` является &quot;1&quot; окончании отношения «один ко многим», поэтому связь можно удалить, просто установив `Product.Supplier` в `null`.

В &quot;многих&quot; конец связи, клиент должен указать, какую связанную сущность следует удалить. Для этого клиент отправляет универсальный код ресурса (URI) связанной сущности в строке запроса запроса. Например, чтобы удалить «Product 1» из «поставщика 1»:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

Для поддержки этой функции в веб-API необходимо включить дополнительный параметр в метод `DeleteRef`. Ниже приведен метод контроллера для удаления продукта из отношения `Supplier.Products`.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

Ключевым *параметром* является ключ для поставщика, а параметр *релатедкэй* — ключ продукта, который удаляется из связи `Products`. Обратите внимание, что веб-API автоматически получает ключ из строки запроса.
