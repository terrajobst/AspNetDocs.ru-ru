---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Создание единственного элемента в OData v4 с помощью веб-API 2,2 | Документация Майкрософт
author: rick-anderson
description: В этом разделе показано, как определить одноэлементный экземпляр в конечной точке OData в веб-API 2,2.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504504"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>Создание единственного элемента в OData v4 с помощью веб-API 2,2

по Зое Луо

> Обычно доступ к сущности можно получить только в том случае, если она была инкапсулирована в набор сущностей. Но OData v4 предоставляет два дополнительных параметра: Singleton и Contain, которые поддерживаются WebAPI 2,2.

В этой статье показано, как определить одноэлементный экземпляр в конечной точке OData в веб-API 2,2. Сведения о том, что такое одноэлементное и в чем преимущества его использования, см. в разделе [Использование одноэлементного набора для определения особой сущности](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx). Чтобы создать конечную точку OData v4 в веб-API, см. раздел [Создание конечной точки OData v4 с помощью веб-API ASP.NET 2,2](create-an-odata-v4-endpoint.md). 

Мы создадим одноэлементный экземпляр в проекте веб-API, используя следующую модель данных:

![Модель данных](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

Одноэлементное имя с именем `Umbrella` будет определено на основе типа `Company`, а набор сущностей с именем `Employees` будет определяться на основе типа `Employee`.

Решение, используемое в этом руководстве, можно скачать на [сайте CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).

## <a name="define-the-data-model"></a>Определение модели данных

1. Определите типы CLR.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. Создание модели EDM на основе типов CLR.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    Здесь `builder.Singleton<Company>("Umbrella")` указывает построителю моделей создать одноэлементное множество с именем `Umbrella` в модели EDM.

    Созданные метаданные будут выглядеть следующим образом:

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    Из метаданных можно увидеть, что свойство навигации, `Company` в наборе сущностей `Employees`, привязано к `Umbrella`Singleton. Привязка выполняется автоматически `ODataConventionModelBuilder`, так как только `Umbrella` имеет тип `Company`. Если в модели имеется какая-либо неоднозначность, можно использовать `HasSingletonBinding`, чтобы явно привязать свойство навигации к одноэлементному экземпляру. `HasSingletonBinding` действует так же, как и атрибут `Singleton` в определении типа CLR:

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>Определение одноэлементного контроллера

Как и контроллер EntitySet, одноэлементный контроллер наследуется от `ODataController`, а имя одноэлементного контроллера должно быть `[singletonName]Controller`.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

Для обработки различных типов запросов действия должны быть предварительно определены в контроллере. **Маршрутизация атрибутов** включена по умолчанию в WebApi 2,2. Например, чтобы определить действие по обработке запросов `Revenue` от `Company` с помощью маршрутизации атрибутов, используйте следующую команду:

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

Если вы не хотите определять атрибуты для каждого действия, просто определите действия, следующие за [соглашениями о маршрутизации OData](../odata-routing-conventions.md). Поскольку ключ не требуется для запроса одноэлементного экземпляра, действия, определенные в контроллере Singleton, немного отличаются от действий, определенных в контроллере EntitySet.

Для справки сигнатуры методов для каждого определения действия в одноэлементном контроллере перечислены ниже.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

По сути, это все, что нужно сделать на стороне службы. [Пример проекта](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) содержит весь код для решения и клиента OData, который показывает, как использовать Singleton. Клиент создается, выполнив действия, описанные в разделе [Создание клиентского приложения OData для версии 4](create-an-odata-v4-client-app.md).

. 

*Благодарим вас за первоначальное содержимое этой статьи, Leo Hu.*
