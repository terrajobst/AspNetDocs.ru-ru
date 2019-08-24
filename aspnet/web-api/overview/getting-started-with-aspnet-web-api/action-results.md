---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Результаты действия в веб-API 2 — ASP.NET 4. x
author: MikeWasson
description: Описывает, как веб-API ASP.NET преобразует возвращаемое значение из действия контроллера в ответное сообщение HTTP в ASP.NET 4. x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 1eaaf8e87168096683212fa66d3ddf415ad6b22b
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000721"
---
# <a name="action-results-in-web-api-2"></a>Результаты действий в веб-API 2

В этом разделе описано, как веб-API ASP.NET преобразует возвращаемое значение из действия контроллера в сообщение ответа HTTP.

Действие контроллера веб-API может возвращать следующие значения:

1. void
2. **HttpResponseMessage**
3. **ихттпактионресулт**
4. Другой тип

В зависимости от того, какое из этих данных возвращается, веб-API использует другой механизм для создания ответа HTTP.

| Возвращаемый тип | Как веб-API создает ответ |
| --- | --- |
| void | Возврат пустого значения 204 (без содержимого) |
| **HttpResponseMessage** | Преобразование непосредственно в ответное сообщение HTTP. |
| **ихттпактионресулт** | Вызовите **ExecuteAsync** , чтобы создать **HttpResponseMessage**, а затем преобразуйте его в ответное сообщение HTTP. |
| Другой тип | Запишите сериализованное возвращаемое значение в текст ответа. Возвращает 200 (ОК). |

В оставшейся части этого раздела каждый параметр описан более подробно.

## <a name="void"></a>void

Если возвращаемый тип — `void`, веб-API просто возвращает пустой ответ HTTP с кодом состояния 204 (нет содержимого).

Пример контроллера:

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP-ответ:

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

Если действие возвращает [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), веб-API преобразует возвращаемое значение непосредственно в ответное сообщение HTTP, используя свойства объекта **HttpResponseMessage** для заполнения ответа.

Этот параметр обеспечивает большой контроль над ответным сообщением. Например, следующее действие контроллера задает заголовок Cache-Control.

[!code-csharp[Main](action-results/samples/sample3.cs)]

Ответ

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

При передаче модели предметной области в метод **Креатереспонсе** веб-API использует [модуль форматирования мультимедиа](../formats-and-model-binding/media-formatters.md) для записи сериализованной модели в текст ответа.

[!code-csharp[Main](action-results/samples/sample5.cs)]

Веб-API использует заголовок Accept в запросе для выбора модуля форматирования. Дополнительные сведения см. в разделе [Согласование содержимого](../formats-and-model-binding/content-negotiation.md).

## <a name="ihttpactionresult"></a>ихттпактионресулт

Интерфейс **ихттпактионресулт** появился в веб-API 2. По сути, он определяет фабрику **HttpResponseMessage** . Ниже приведены некоторые преимущества использования интерфейса **ихттпактионресулт** .

- Упрощает [модульное тестирование](../testing-and-debugging/unit-testing-controllers-in-web-api.md) контроллеров.
- Перемещает общую логику для создания HTTP-ответов в отдельные классы.
- Делает цель действия контроллера более четкой, скрывая низкоуровневые сведения о создании ответа.

**Ихттпактионресулт** содержит единственный метод **ExecuteAsync**, который асинхронно создает экземпляр **HttpResponseMessage** .

[!code-csharp[Main](action-results/samples/sample6.cs)]

Если действие контроллера возвращает **ихттпактионресулт**, веб-API вызывает метод **ExecuteAsync** для создания **HttpResponseMessage**. Затем он преобразует **HttpResponseMessage** в сообщение HTTP-ответа.

Ниже приведена простая реализация **ихттпактионресулт** , которая создает ответ в виде обычного текста:

[!code-csharp[Main](action-results/samples/sample7.cs)]

Пример действия контроллера:

[!code-csharp[Main](action-results/samples/sample8.cs)]

Ответ

[!code-console[Main](action-results/samples/sample9.cmd)]

Чаще всего используются реализации **ихттпактионресулт** , определенные в пространстве имен **[System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** . Класс **ApiController** определяет вспомогательные методы, которые возвращают эти встроенные результаты действия.

В следующем примере, если запрос не соответствует существующему ИДЕНТИФИКАТОРу продукта, контроллер вызывает [ApiController. NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) для создания ответа 404 (не найдено). В противном случае контроллер вызывает [ApiController. ОК](https://msdn.microsoft.com/library/dn314591.aspx), который создает ответ 200 (ОК), содержащий продукт.

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>Другие типы возвращаемых значения

Для всех остальных возвращаемых типов веб-API использует [модуль форматирования мультимедиа](../formats-and-model-binding/media-formatters.md) для сериализации возвращаемого значения. Веб-API записывает сериализованное значение в текст ответа. Код состояния отклика — 200 (ОК).

[!code-csharp[Main](action-results/samples/sample11.cs)]

Недостаток этого подхода заключается в том, что нельзя напрямую возвращать код ошибки, например 404. Однако можно создать **хттпреспонсиксцептион** для кодов ошибок. Дополнительные сведения см. [в разделе Обработка исключений в веб-API ASP.NET](../error-handling/exception-handling.md).

Веб-API использует заголовок Accept в запросе для выбора модуля форматирования. Дополнительные сведения см. в разделе [Согласование содержимого](../formats-and-model-binding/content-negotiation.md).

Пример запроса

[!code-console[Main](action-results/samples/sample12.cmd)]

Пример ответа

[!code-console[Main](action-results/samples/sample13.cmd)]
