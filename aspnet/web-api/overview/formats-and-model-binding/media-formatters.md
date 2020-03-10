---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: Модули форматирования мультимедиа в веб-API ASP.NET 2 — ASP.NET 4. x
author: MikeWasson
description: Описание поддержки дополнительных форматов мультимедиа в веб-API ASP.NET для ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448944"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a>Модули форматирования мультимедиа в веб-API ASP.NET 2

по [Майк Уоссон](https://github.com/MikeWasson)

В этом руководстве показано, как поддерживать дополнительные форматы мультимедиа в веб-API ASP.NET.

## <a name="internet-media-types"></a>Типы медиа Интернета

Тип носителя, также называемый типом MIME, определяет формат фрагмента данных. В протоколе HTTP типы носителей описывают формат текста сообщения. Тип мультимедиа состоит из двух строк: типа и подтипа. Пример:

- text/html
- image/png
- приложение/json

Если сообщение HTTP содержит текст сущности, заголовок Content-Type определяет формат текста сообщения. Это указывает получателю, как анализировать содержимое текста сообщения.

Например, если HTTP-ответ содержит изображение PNG, то ответ может иметь следующие заголовки.

[!code-console[Main](media-formatters/samples/sample1.cmd)]

Когда клиент отправляет сообщение запроса, он может включать заголовок Accept. Заголовок Accept сообщает серверу, какой тип носителя требуется клиенту с сервера. Пример:

[!code-console[Main](media-formatters/samples/sample2.cmd)]

Этот заголовок сообщает серверу, что клиенту требуется HTML, XHTML или XML.

Тип носителя определяет, как веб-API сериализует и десериализует текст сообщения HTTP. Веб-API имеет встроенную поддержку данных XML, JSON, BSON и Form-UrlEncoded, и вы можете поддерживать дополнительные типы мультимедиа, написав *модуль форматирования мультимедиа*.

Чтобы создать модуль форматирования мультимедиа, сделайте его производным от одного из следующих классов:

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx). Этот класс использует асинхронные методы чтения и записи.
- [Буффередмедиатипеформаттер](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx). Этот класс является производным от **MediaTypeFormatter** , но использует синхронные методы чтения и записи.

Наследование от **буффередмедиатипеформаттер** проще, поскольку асинхронный код отсутствует, но это также означает, что вызывающий поток может блокироваться во время ввода-вывода.

## <a name="example-creating-a-csv-media-formatter"></a>Пример. Создание модуля форматирования мультимедиа CSV

В следующем примере показан модуль форматирования типа мультимедиа, который может сериализовать объект Product в формат значений с разделителями-запятыми (CSV). В этом примере используется тип продукта, определенный в руководстве [Создание веб-API, поддерживающего операции CRUD](../older-versions/creating-a-web-api-that-supports-crud-operations.md). Ниже приведено определение объекта Product:

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

Чтобы реализовать модуль форматирования CSV, определите класс, производный от **буффередмедиатипеформаттер**:

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

В конструкторе добавьте типы носителей, поддерживаемые модулем форматирования. В этом примере модуль форматирования поддерживает один тип носителя, &quot;&quot;Text/CSV:

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

Переопределите метод **канвритетипе** , чтобы указать типы, которые модуль форматирования может сериализовать:

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

В этом примере модуль форматирования может сериализовать отдельные `Product`ные объекты, а также коллекции `Product` объектов.

Аналогичным образом Переопределите метод **канреадтипе** , чтобы указать типы, которые модуль форматирования может десериализовать. В этом примере модуль форматирования не поддерживает десериализацию, поэтому метод просто возвращает **значение false**.

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

Наконец, переопределите метод **вритетостреам** . Этот метод сериализует тип, записывая его в поток. Если модуль форматирования поддерживает десериализацию, также следует переопределить метод **реадфромстреам** .

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>Добавление модуля форматирования мультимедиа в конвейер веб-API

Чтобы добавить модуль форматирования типов мультимедиа в конвейер веб-API, используйте свойство **форматеры** объекта **HttpConfiguration** .

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>Кодировки символов

При необходимости модуль форматирования мультимедиа может поддерживать несколько кодировок символов, таких как UTF-8 или ISO 8859-1.

В конструкторе добавьте один или несколько типов [System. Text. Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) в коллекцию **суппортеденкодингс** . Сначала укажите кодировку по умолчанию.

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

В методах **вритетостреам** и **Реадфромстреам** вызовите [MediaTypeFormatter. селектчарактеренкодинг](https://msdn.microsoft.com/library/hh969054.aspx) , чтобы выбрать предпочтительную кодировку символов. Этот метод сопоставляет заголовки запроса со списком поддерживаемых кодировок. Используйте возвращенную **кодировку** при чтении или записи из потока:

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
