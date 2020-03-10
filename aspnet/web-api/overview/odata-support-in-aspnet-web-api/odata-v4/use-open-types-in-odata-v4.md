---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Открытие типов в OData v4 с помощью веб-API ASP.NET | Документация Майкрософт
author: microsoft
description: В OData v4 открытый тип — это структурированный тип, который содержит динамические свойства в дополнение к любым свойствам, объявленным в определении типа. Открыть...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504582"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Открытие типов в OData v4 с веб-API ASP.NET

по [Майкрософт](https://github.com/microsoft)

> В OData v4 *открытый тип* — это структурированный тип, который содержит динамические свойства в дополнение к любым свойствам, объявленным в определении типа. Открытые типы позволяют повысить гибкость моделей данных. В этом руководстве показано, как использовать открытые типы в веб-API ASP.NET OData.
> 
> В этом учебнике предполагается, что вы уже умеете создавать конечную точку OData в веб-API ASP.NET. Если это не так, начните с чтения сначала [Создайте конечную точку OData v4](create-an-odata-v4-endpoint.md) .
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
> 
> 
> - Веб-API OData 5,3
> - OData v4

Во первых, некоторые термины OData:

- Тип сущности — структурированный тип с ключом.
- Сложный тип: структурированный тип без ключа.
- Открыть тип: тип с динамическими свойствами. Можно открыть как типы сущностей, так и сложные типы.

Значением динамического свойства может быть тип-примитив, сложный тип или тип перечисления. или коллекция любого из этих типов. Дополнительные сведения об открытых типах см. в [спецификации OData v4](http://www.odata.org/documentation/odata-version-4-0/).

## <a name="install-the-web-odata-libraries"></a>Установка библиотек веб-OData

Используйте диспетчер пакетов NuGet для установки последних библиотек веб-API OData. В окне консоли диспетчера пакетов выполните следующие действия.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>Определение типов CLR

Начните с определения моделей EDM в качестве типов CLR.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

При создании EDM (EDM)

- `Category` является типом перечисления.
- `Address` является сложным типом. (У него нет ключа, поэтому он не является типом сущности.)
- `Customer` является типом сущности. (У него есть ключ.)
- `Press` является открытым сложным типом.
- `Book` является открытым типом сущности.

Для создания открытого типа тип CLR должен иметь свойство типа `IDictionary<string, object>`, которое содержит динамические свойства.

## <a name="build-the-edm-model"></a>Построение модели EDM

Если для создания модели EDM используется **одатаконвентионмоделбуилдер** , то `Press` и `Book` автоматически добавляются как открытые типы в зависимости от наличия свойства `IDictionary<string, object>`.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Вы также можете создать EDM явным образом с помощью **одатамоделбуилдер**.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>Добавление контроллера OData

Затем добавьте контроллер OData. В этом руководстве мы будем использовать упрощенный контроллер, который только поддерживает запросы GET и POST, и использует список в памяти для хранения сущностей.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

Обратите внимание, что первый экземпляр `Book` не имеет динамических свойств. Второй экземпляр `Book` имеет следующие динамические свойства:

- "Published": тип-примитив
- "Authors": Коллекция типов-примитивов
- "Осеркатегориес": Коллекция типов перечисления.

Кроме того, свойство `Press` этого экземпляра `Book` имеет следующие динамические свойства:

- "Блог": тип-примитив
- "Address": сложный тип

## <a name="query-the-metadata"></a>Запрос метаданных

Чтобы получить документ метаданных OData, отправьте запрос GET в `~/$metadata`. Текст ответа должен выглядеть следующим образом:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

Из документа метаданных можно увидеть следующее:

- Для типов `Book` и `Press` значение атрибута `OpenType` равно true. Типы `Customer` и `Address` не имеют этого атрибута.
- Тип сущности `Book` имеет три объявленных свойства: ISBN, Title и Press. Метаданные OData не включают свойство `Book.Properties` из класса CLR.
- Аналогичным образом, `Press` сложного типа имеет только два объявленных свойства: Name и category. Метаданные не включают свойство `Press.DynamicProperties` из класса CLR.

## <a name="query-an-entity"></a>Запрос сущности

Чтобы получить книгу с ISBN-значением, равным "978-0-7356-7942-9", отправьте запрос GET в `~/Books('978-0-7356-7942-9')`. Текст ответа должен выглядеть следующим образом. (С отступом, чтобы сделать его более удобочитаемым.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Обратите внимание, что динамические свойства включаются в строку с объявленными свойствами.

## <a name="post-an-entity"></a>Публикация сущности

Чтобы добавить сущность Book, отправьте запрос POST в `~/Books`. Клиент может задавать динамические свойства в полезных данных запроса.

Ниже приведен пример запроса. Обратите внимание на свойства Price и published.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Если задать точку останова в методе контроллера, можно увидеть, что веб-API добавил эти свойства в словарь `Properties`.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Дополнительные ресурсы

[Пример открытого типа OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
