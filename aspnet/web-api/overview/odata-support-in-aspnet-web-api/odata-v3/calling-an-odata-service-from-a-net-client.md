---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: Вызов службы OData из клиента .NET (C#) | Документация Майкрософт
author: MikeWasson
description: В этом руководстве показано, как вызвать службу OData из C# клиентского приложения. Версии программного обеспечения, используемые в руководстве Visual Studio 2013 (работает с Visual S...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600396"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a>Вызов службы OData из клиента .NET (C#)

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> В этом руководстве показано, как вызвать службу OData из C# клиентского приложения.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (работает с Visual Studio 2012)
> - [Библиотека клиентов служб данных WCF](https://msdn.microsoft.com/library/cc668772.aspx)
> - Веб-API 2. (Пример службы OData создается с помощью веб-API 2, но клиентское приложение не зависит от веб-API.)

В этом руководстве я расскажу о создании клиентского приложения, которое вызывает службу OData. Служба OData предоставляет следующие сущности:

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

В следующих статьях описывается реализация службы OData в веб-API. (Однако вам не нужно читать их для понимания этого руководства.)

- [Создание конечной точки OData в веб-API 2](creating-an-odata-endpoint.md)
- [Связи сущностей OData в веб-API 2](working-with-entity-relations.md)
- [Действия OData в веб-API 2](odata-actions.md)

## <a name="generate-the-service-proxy"></a>Создание прокси-сервера службы

Первым шагом является создание прокси-сервера службы. Прокси-сервер службы — это класс .NET, который определяет методы для доступа к службе OData. Прокси-сервер преобразует вызовы метода в HTTP-запросы.

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

Для начала откройте проект службы OData в Visual Studio. Нажмите клавиши CTRL + F5, чтобы запустить службу локально в IIS Express. Запишите локальный адрес, включая номер порта, который назначается Visual Studio. Этот адрес потребуется при создании учетной записи-посредника.

Затем откройте другой экземпляр Visual Studio и создайте проект консольного приложения. Консольное приложение будет клиентским приложением OData. (Можно также добавить проект в то же решение, что и служба.)

> [!NOTE]
> Остальные шаги относятся к проекту консоли.

В обозреватель решений щелкните правой кнопкой мыши **ссылки** и выберите **Добавление ссылки на службу**.

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

В диалоговом окне **Добавление ссылки на службу** введите адрес службы OData:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

где *Port* — номер порта.

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

В качестве **пространства имен**введите "продуктсервице". Этот параметр определяет пространство имен прокси-класса.

Нажмите **Перейти**. Visual Studio считывает документ метаданных OData для обнаружения сущностей в службе.

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

Нажмите кнопку **ОК** , чтобы добавить класс прокси в проект.

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>Создание экземпляра класса прокси службы

В методе `Main` создайте новый экземпляр класса-посредника следующим образом:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

Опять же, используйте фактический номер порта, на котором запущена служба. При развертывании службы будет использоваться универсальный код ресурса (URI) динамической службы. Вам не нужно обновлять прокси-сервер.

Следующий код добавляет обработчик событий, который выводит URI запроса в окно консоли. Этот шаг не является обязательным, но интересно увидеть коды URI для каждого запроса.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>Запрос к службе

Следующий код возвращает список продуктов из службы OData.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

Обратите внимание, что вам не нужно писать код для отправки HTTP-запроса или синтаксического анализа ответа. Прокси-класс выполняет это автоматически при перечислении коллекции `Container.Products` в цикле **foreach** .

При запуске приложения выходные данные должны выглядеть следующим образом:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

Чтобы получить сущность по ИДЕНТИФИКАТОРу, используйте предложение `where`.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

В оставшейся части этого раздела я не буду показывать всю функцию `Main`, просто код, необходимый для вызова службы.

## <a name="apply-query-options"></a>Применить параметры запроса

OData определяет [Параметры запроса](../supporting-odata-query-options.md) , которые можно использовать для фильтрации, сортировки, данных страницы и т. д. В прокси-сервере службы эти параметры можно применять с помощью различных выражений LINQ.

В этом разделе я продемонстрирую краткие примеры. Дополнительные сведения см. в разделе [рекомендации по LINQ (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) на сайте MSDN.

### <a name="filtering-filter"></a>Фильтрация ($filter)

Чтобы отфильтровать, используйте предложение `where`. В следующем примере производится фильтрация по категории продуктов.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

Этот код соответствует следующему запросу OData.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

Обратите внимание, что прокси-сервер преобразует предложение `where` в выражение `$filter` OData.

### <a name="sorting-orderby"></a>Сортировка ($orderby)

Для сортировки используйте предложение `orderby`. В следующем примере выполняется сортировка по цене, от самого высокого до самого низкого.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

Ниже приведен соответствующий запрос OData.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>Разбиение на страницы на стороне клиента ($skip и $top)

Для больших наборов сущностей клиенту может потребоваться ограничить количество результатов. Например, клиент может отображать 10 записей за раз. Это называется *страничным обменом на стороне клиента*. (Имеется также [страничный обмен на стороне сервера](../supporting-odata-query-options.md#server-paging), где сервер ограничивает количество результатов.) Для выполнения разбиения на страницы на стороне клиента используйте методы LINQ **Skip** и **Take** . Следующий пример пропускает первые 40 результатов и принимает следующий 10.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

Ниже приведен соответствующий запрос OData.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>Выберите ($select) и разверните ($expand)

Чтобы включить связанные сущности, используйте метод `DataServiceQuery<t>.Expand`. Например, чтобы включить `Supplier` для каждой `Product`:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

Ниже приведен соответствующий запрос OData.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

Чтобы изменить форму ответа, используйте предложение **SELECT** LINQ. В следующем примере возвращается только имя каждого продукта без других свойств.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

Ниже приведен соответствующий запрос OData.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Предложение SELECT может включать связанные сущности. В этом случае не вызывайте **expand**; в этом случае прокси-сервер автоматически включает расширение. В следующем примере показано получение имени и поставщика каждого продукта.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

Ниже приведен соответствующий запрос OData. Обратите внимание, что он включает параметр **$expand** .

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

Дополнительные сведения о $select и $expand см. [в разделе использование $SELECT, $Expand и $value в веб-API 2](../using-select-expand-and-value.md).

## <a name="add-a-new-entity"></a>Добавить новую сущность

Чтобы добавить новую сущность в набор сущностей, вызовите `AddToEntitySet`, где *EntitySet* — это имя набора сущностей. Например, `AddToProducts` добавляет новую `Product` в набор сущностей `Products`. При создании прокси-сервера WCF Data Services автоматически создает эти методы строго типизированных **AddTo** .

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

Чтобы добавить ссылку между двумя сущностями, используйте методы **AddLink** и **сетлинк** . Следующий код добавляет нового поставщика и новый продукт, а затем создает связи между ними.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

Используйте **AddLink** , если свойство навигации является коллекцией. В этом примере мы добавляем продукт в коллекцию `Products` поставщика.

Используйте **сетлинк** , если свойство навигации является одной сущностью. В этом примере мы задаете свойство `Supplier` для продукта.

## <a name="update--patch"></a>Обновление или исправление

Чтобы обновить сущность, вызовите метод **UpdateObject** .

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

Обновление выполняется при вызове метода **SaveChanges**. По умолчанию WCF отправляет HTTP-запрос на СЛИЯНИе. Параметр **патчонупдате** сообщает WCF, что вместо этого ОТПРАВЛЯЕТСЯ исправление HTTP.

> [!NOTE]
> Почему исправления и СЛИЯНИе? В исходной спецификации HTTP 1,1 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) не определен ни один метод HTTP с семантикой "частичного обновления". Для поддержки частичных обновлений спецификация OData определила метод MERGE. В 2010 [RFC 5789](http://tools.ietf.org/html/rfc5789) ОПРЕДЕЛИЛ метод исправления для частичных обновлений. Некоторые журналы из этой [записи блога](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) можно прочитать в блоге WCF Data Services. Сейчас исправление является предпочтительным по сравнению с СЛИЯНИем. Контроллер OData, созданный с помощью формирования шаблонов веб-API, поддерживает оба метода.

Если требуется заменить всю сущность (семантика вставки), укажите параметр **реплацеонупдате** . Это приводит к тому, что WCF отправляет запрос HTTP-размещения.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>Удаление сущности

Чтобы удалить сущность, вызовите **DeleteObject**.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>Вызов действия OData

В OData [действия](odata-actions.md) — это способ добавления поведений на стороне сервера, которые не просто определяются как операции CRUD с сущностями.

Хотя в документе метаданных OData описываются действия, прокси-класс не создает для них строго типизированные методы. Действие OData по-прежнему можно вызывать с помощью универсального метода **EXECUTE** . Тем не менее необходимо знать типы данных параметров и возвращаемое значение.

Например, `RateProduct` действие принимает параметр с именем "Оценка" типа `Int32` и возвращает `double`. В следующем коде показано, как вызвать это действие.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

Дополнительные сведения см. в разделе[вызов операций и действий службы](https://msdn.microsoft.com/library/hh230677.aspx).

Один из вариантов — расширить класс **контейнера** , чтобы предоставить строго типизированный метод, который вызывает действие:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
