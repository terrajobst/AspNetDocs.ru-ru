---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: Проверка модели в веб-API ASP.NET ASP.NET 4. x
author: MikeWasson
description: Общие сведения о проверке модели в веб-API ASP.NET ASP.NET 4. x.
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448932"
---
# <a name="model-validation-in-aspnet-web-api"></a>Проверка модели в веб-API ASP.NET

по [Майк Уоссон](https://github.com/MikeWasson)

В этой статье показано, как добавлять заметки к моделям, использовать заметки для проверки данных и обрабатывайте ошибки проверки в веб-API. Когда клиент отправляет данные в веб-API, часто требуется проверить данные перед обработкой. 

## <a name="data-annotations"></a>Заметки к данным

В веб-API ASP.NET можно использовать атрибуты из пространства имен [System. ComponentModel. аннотации](/dotnet/api/system.componentmodel.dataannotations) , чтобы задать правила проверки для свойств модели. Рассмотрим следующую модель:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

Если вы использовали проверку модели в ASP.NET MVC, это должно показаться знакомым. **Обязательный** атрибут говорит, что свойство `Name` не должно иметь значение null. Атрибут **Range** говорит, что `Weight` должны быть в диапазоне от 0 до 999.

Предположим, что клиент отправляет запрос POST со следующим представлением JSON:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

Вы видите, что клиент не включал свойство `Name`, которое отмечено как обязательное. Когда веб-API преобразует JSON в экземпляр `Product`, он проверяет `Product` по атрибутам проверки. В действии контроллера можно проверить, является ли модель допустимой:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

Проверка модели не гарантирует, что данные клиента являются безнадежными. На других уровнях приложения может потребоваться дополнительная проверка. (Например, на уровне данных могут применяться ограничения внешнего ключа.) В руководстве [Использование веб-API с Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) рассматриваются некоторые из этих проблем.

**"Под учетной записью"** : Разноска происходит, когда клиент оставляет некоторые свойства. Например, предположим, что клиент отправляет следующее:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

Здесь клиент не указал значения для `Price` или `Weight`. Модуль форматирования JSON присваивает отсутствующим свойствам значение по умолчанию, равное нулю.

![](model-validation-in-aspnet-web-api/_static/image1.png)

Состояние модели является допустимым, поскольку ноль является допустимым значением для этих свойств. Зависит ли проблема от вашего сценария. Например, в операции обновления может потребоваться отличать "ноль" и "Not Set". Чтобы заставить клиентов задать значение, сделайте свойство обнуляемым и задайте **требуемый** атрибут:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

**"Over-Post"** : Клиент также может отправлять *больше* данных, чем ожидалось. Пример:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

В этом случае JSON включает свойство ("Color"), которое не существует в модели `Product`. В этом случае модуль форматирования JSON просто игнорирует это значение. (Модуль форматирования XML делает то же самое.) Избыточная передача вызывает проблемы, если у модели есть свойства, предназначенные только для чтения. Пример:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

Пользователям не нужно обновлять свойство `IsAdmin` и повышать уровень прав для администраторов! Наиболее надежной стратегией является использование класса модели, точно соответствующего тому, что клиенту разрешено передавать:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> В записи блога Михаил Уилсон ("[Проверка входных данных и проверка модели в ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" есть хорошее обсуждение вложений в публикацию и последующей публикации. Несмотря на то, что запись относится к ASP.NET MVC 2, проблемы по-прежнему связаны с Web API.

## <a name="handling-validation-errors"></a>Обработка ошибок проверки

Веб-API не возвращает клиенту ошибку автоматически при сбое проверки. Действие контроллера проверяет состояние модели и отвечает соответствующим образом.

Можно также создать фильтр действий для проверки состояния модели перед вызовом действия контроллера. Пример кода приведен ниже.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

Если проверка модели завершается неудачно, этот фильтр возвращает ответ HTTP, содержащий ошибки проверки. В этом случае действие контроллера не вызывается.

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

Чтобы применить этот фильтр ко всем контроллерам веб-API, добавьте экземпляр фильтра в коллекцию **HttpConfiguration. Filters** во время настройки:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

Другой вариант — задать фильтр в качестве атрибута для отдельных контроллеров или действий контроллера:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
