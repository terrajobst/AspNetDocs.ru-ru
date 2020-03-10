---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: Поддержка BSON в веб-API ASP.NET 2,1-ASP.NET 4. x
author: MikeWasson
description: показывает, как использовать BSON в контроллере веб-API (на стороне сервера) и в клиентском приложении .NET для ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: ccbc0372120301b1cd8d4cdc86bd9fba9404d8ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504684"
---
# <a name="bson-support-in-aspnet-web-api-21"></a>Поддержка BSON в веб-API ASP.NET 2,1

по [Майк Уоссон](https://github.com/MikeWasson)

В этом разделе показано, как использовать BSON в контроллере веб-API (на стороне сервера) и в клиентском приложении .NET. В веб-API 2,1 введена поддержка BSON. 

## <a name="what-is-bson"></a>Что такое BSON?

[BSON](http://bsonspec.org/) — это формат двоичной сериализации. "BSON" означает "двоичный JSON", но BSON и JSON сериализуются совершенно иначе. BSON — это «JSON-Like», поскольку объекты представлены как пары «имя-значение», аналогичные формату JSON. В отличие от JSON, числовые типы данных хранятся в виде байтов, а не строк.

BSON был разработан для упрощения, легкого сканирования и быстрого кодирования и декодирования.

- BSON сравним по размеру с JSON. В зависимости от конкретных данных полезные данные BSON могут занять меньше или больше пространства, чем полезные данные JSON. Для сериализации двоичных данных, таких как файл изображения, BSON меньше JSON, так как двоичные данные не кодируются в Base64.
- Документы BSON легко сканировать, поскольку элементы имеют префикс поля длины, поэтому средство синтаксического анализа может пропускать элементы без их декодирования.
- Кодирование и декодирование являются эффективными, так как числовые типы данных хранятся в виде чисел, а не строк.

Собственные клиенты, такие как клиентские приложения .NET, могут воспользоваться преимуществами BSON вместо текстовых форматов, таких как JSON или XML. Для клиентов браузеров, вероятно, потребуется использовать JSON, так как JavaScript может напрямую преобразовывать полезные данные JSON.

К счастью, веб-API использует [Согласование содержимого](content-negotiation.md), поэтому API может поддерживать оба формата и позволить клиенту выбрать.

## <a name="enabling-bson-on-the-server"></a>Включение BSON на сервере

В конфигурации веб-API добавьте **бсонмедиатипеформаттер** в коллекцию форматеров.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

Теперь, если клиент запрашивает "Application/BSON", веб-API будет использовать модуль форматирования BSON.

Чтобы связать BSON с другими типами мультимедиа, добавьте их в коллекцию Суппортедмедиатипес. Следующий код добавляет "application/vnd. contoso" к поддерживаемым типам носителей:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>Пример сеанса HTTP

В этом примере мы будем использовать следующий класс Model и простой контроллер веб-API:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

Клиент может отправить следующий HTTP-запрос:

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

Ответ:

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

Здесь я заменил двоичные данные на &quot;.&quot; символов. На следующем снимке экрана из Fiddler показаны необработанные шестнадцатеричные значения.

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>Использование BSON с HttpClient

Клиентские приложения .NET могут использовать модуль форматирования BSON с **HttpClient**. Дополнительные сведения о **HttpClient**см. в разделе [вызов веб-API из клиента .NET](../advanced/calling-a-web-api-from-a-net-client.md).

Следующий код отправляет запрос GET, который принимает BSON, а затем десериализует полезные данные BSON в ответе.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

Чтобы запросить BSON с сервера, задайте для заголовка Accept значение "Application/BSON":

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

Чтобы десериализовать текст ответа, используйте **бсонмедиатипеформаттер**. Этот модуль форматирования не находится в коллекции модулей форматирования по умолчанию, поэтому его необходимо указать при чтении текста ответа:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

В следующем примере показано, как отправить запрос POST, содержащий BSON.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

Большая часть этого кода аналогична предыдущему примеру. Но в методе **Async** укажите **бсонмедиатипеформаттер** в качестве модуля форматирования:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>Сериализация примитивных типов верхнего уровня

Каждый документ BSON представляет собой список пар «ключ-значение». Спецификация BSON не определяет синтаксис для сериализации одного необработанного значения, такого как целое число или строка.

Чтобы обойти это ограничение, **бсонмедиатипеформаттер** рассматривает примитивные типы как особый случай. Перед сериализацией он преобразует значение в пару "ключ-значение" с ключом "value". Например, предположим, что контроллер API возвращает целое число:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

Перед сериализацией модуль форматирования BSON преобразует его в следующую пару "ключ-значение":

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

При десериализации модуль форматирования преобразует данные обратно в исходное значение. Однако клиенты, использующие другое средство синтаксического анализа BSON, должны обработать этот случай, если ваш веб-API возвращает необработанные значения. Как правило, рекомендуется возвращать структурированные данные, а не необработанные значения.

## <a name="additional-resources"></a>Дополнительные ресурсы

[Пример BSON веб-API](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[Модули форматирования мультимедиа](media-formatters.md)
