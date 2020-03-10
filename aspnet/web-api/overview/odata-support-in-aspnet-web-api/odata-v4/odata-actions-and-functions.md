---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: Действия и функции в OData v4 с использованием веб-API ASP.NET 2,2 | Документация Майкрософт
author: MikeWasson
description: В OData действия и функции позволяют добавлять поведений на стороне сервера, которые не просто определяются как операции CRUD для сущностей. В этом руководстве показано, как...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448062"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>Действия и функции в OData v4 с использованием веб-API ASP.NET 2,2

по [Майк Уоссон](https://github.com/MikeWasson)

> В OData действия и функции позволяют добавлять поведений на стороне сервера, которые не просто определяются как операции CRUD для сущностей. В этом руководстве показано, как добавлять действия и функции в конечную точку OData v4 с помощью веб-API 2,2. Руководство по построению в учебнике [Создание конечной точки OData v4 с помощью веб-API ASP.NET 2](create-an-odata-v4-endpoint.md)
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
> - Веб-API 2,2
> - OData v4
> - Visual Studio 2013 (Скачайте Visual Studio 2017 [здесь](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>Учебные версии
>
> Сведения для OData версии 3 см. [в разделе действия OData в веб-API ASP.NET 2](../odata-v3/odata-actions.md).

Различие между *действиями* и *функциями* заключается в том, что действия могут иметь побочные эффекты, а функции — нет. Действия и функции могут возвращать данные. Ниже перечислены некоторые способы использования действий.

- Сложные транзакции.
- Одновременное управление несколькими сущностями.
- Разрешение обновления только для определенных свойств сущности.
- Отправка данных, которые не являются сущностями.

Функции полезны для возврата сведений, которые не соответствуют непосредственно сущности или коллекции.

Действие (или функция) может ориентироваться на одну сущность или коллекцию. В терминологии OData это *Привязка*. Можно также иметь &quot;непривязанные&quot; действия или функции, которые вызываются как статические операции в службе.

## <a name="example-adding-an-action"></a>Пример. Добавление действия

Давайте определим действие для расчета частоты продукта.

> [!NOTE]
> В этом руководстве описано, [как создать конечную точку OData v4 с помощью веб-API ASP.NET 2](create-an-odata-v4-endpoint.md) .

Сначала добавьте модель `ProductRating` для представления оценок.

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

Также добавьте **DbSet** в класс `ProductsContext`, чтобы EF создаст таблицу оценок в базе данных.

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>Добавление действия в модель EDM

В WebApiConfig.cs добавьте следующий код:

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

Метод **ентититипеконфигуратион. Action** добавляет действие в модель EDM. Метод **Parameter** задает типизированный параметр для действия.

Этот код также задает пространство имен для модели EDM. Пространство имен имеет значение, так как универсальный код ресурса (URI) действия включает полное имя действия:

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> В типичной конфигурации IIS точка в этом URL-адресе приведет к возврату ошибки 404. Это можно разрешить, добавив следующий раздел в файл Web. config:

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>Добавление метода контроллера для действия

Чтобы включить&quot; &quot;Rate, добавьте следующий метод для `ProductsController`:

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

Обратите внимание, что имя метода совпадает с именем действия. Атрибут **[HttpPost]** указывает, что метод является методом HTTP POST.

Чтобы вызвать действие, клиент отправляет запрос HTTP POST, подобный следующему:

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

Действие&quot; Rate &quot;привязано к экземплярам продукта, поэтому универсальный код ресурса (URI) для действия — это полное имя действия, добавляемое к универсальному коду ресурса (URI) сущности. (Помните, что мы устанавливаем пространство имен EDM &quot;Продуктсервице&quot;, поэтому полное имя действия — &quot;Продуктсервице. rate&quot;.)

Текст запроса содержит параметры действия в виде полезных данных JSON. Веб-API автоматически преобразует полезные данные JSON в объект **одатаактионпараметерс** , который представляет собой просто словарь значений параметров. Используйте этот словарь для доступа к параметрам в методе контроллера.

Если клиент отправляет параметры действия в неправильном формате, значение **ModelState. IsValid** равно false. Установите этот флаг в метод контроллера и верните ошибку, если параметр **IsValid** имеет значение false.

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>Пример. Добавление функции

Теперь добавим функцию OData, которая возвращает самый ресурсоемкий продукт. Как и раньше, первым шагом является добавление функции в EDM. В WebApiConfig.cs добавьте следующий код.

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

В этом случае функция привязана к коллекции Products, а не к отдельным экземплярам продукта. Клиенты вызывают функцию, отправив запрос GET:

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

Ниже приведен метод контроллера для этой функции.

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

Обратите внимание, что имя метода совпадает с именем функции. Атрибут **[HttpGet]** указывает, что метод является методом HTTP GET.

Ответ HTTP:

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>Пример. Добавление непривязанной функции

Предыдущий пример — функция, привязанная к коллекции. В следующем примере мы создадим *несвязанную* функцию. Несвязанные функции вызываются как статические операции со службой. Функция в этом примере будет возвращать налог на продажу для данного почтового индекса.

В файле WebApiConfig добавьте функцию в модель EDM:

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

Обратите внимание, что **функция** вызывается непосредственно в **одатамоделбуилдер**, а не в типе сущности или коллекции. Это указывает построителю моделей, что функция не привязана.

Ниже приведен метод контроллера, реализующий функцию:

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

Не имеет значения, какой контроллер веб-API будет размещен в. Его можно разместить в `ProductsController`или определить отдельный контроллер. Атрибут **[одатарауте]** определяет шаблон URI для функции.

Вот пример запроса клиента:

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

HTTP-ответ:

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
