---
uid: web-api/overview/error-handling/exception-handling
title: Обработка исключений в веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504702"
---
# <a name="exception-handling-in-aspnet-web-api"></a>Обработка исключений в веб-API ASP.NET

по [Майк Уоссон](https://github.com/MikeWasson)

В этой статье описывается обработка ошибок и исключений в веб-API ASP.NET.

- [хттпреспонсиксцептион](#httpresponserexception)
- [Фильтры исключений](#exception_filters)
- [Регистрация фильтров исключений](#registering_exception_filters)
- [HttpError](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a>хттпреспонсиксцептион

Что происходит, если контроллер веб-API вызывает неперехваченное исключение? По умолчанию большинство исключений преобразуются в HTTP-ответ с кодом состояния 500, внутренняя ошибка сервера.

Тип **хттпреспонсиксцептион** является особым случаем. Это исключение возвращает любой код состояния HTTP, указанный в конструкторе исключений. Например, следующий метод возвращает 404, но не найден, если параметр *ID* является недопустимым.

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

Чтобы получить более полный контроль над ответом, можно также создать все ответное сообщение и включить его в **хттпреспонсиксцептион:** 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a>Фильтры исключений

Вы можете настроить обработку исключений веб-API, написав *фильтр исключений*. Фильтр исключений выполняется, когда метод контроллера создает любое необработанное исключение, которое *не* является исключением **хттпреспонсиксцептион** . Тип **хттпреспонсиксцептион** является особым случаем, так как он предназначен специально для возврата HTTP-ответа.

Фильтры исключений реализуют интерфейс **System. Web. http. Filters. иексцептионфилтер** . Самым простым способом написания фильтра исключений является наследование от класса **System. Web. http. Filters. ексцептионфилтераттрибуте** и переопределение метода, **Кроме** .

> [!NOTE]
> Фильтры исключений в веб-API ASP.NET похожи на те, которые относятся к ASP.NET MVC. Однако они объявляются в отдельном пространстве имен и работают отдельно. В частности, класс **хандлиррораттрибуте** , используемый в MVC, не обрабатывает исключения, созданные контроллерами веб-API.

Ниже приведен фильтр, преобразующий исключения **NotImplementedException** в код состояния HTTP 501, который не реализован:

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

Свойство **Response** объекта **хттпактионексекутедконтекст** содержит ответное сообщение HTTP, которое будет отправлено клиенту.

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a>Регистрация фильтров исключений

Существует несколько способов регистрации фильтра исключений веб-API:

- Для действия
- Для контроллера
- Глобально

Чтобы применить фильтр к определенному действию, добавьте его в качестве атрибута в действие:

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

Чтобы применить фильтр ко всем действиям на контроллере, добавьте фильтр в качестве атрибута в класс Controller:

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

Чтобы применить фильтр глобально ко всем контроллерам веб-API, добавьте экземпляр фильтра в коллекцию **глобалконфигуратион. Configuration. Filters** . В этой коллекции фильтры исключений применяются к любому действию контроллера веб-API.

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

Если вы используете шаблон проекта "веб-приложение ASP.NET MVC 4" для создания проекта, добавьте код конфигурации веб-API в класс `WebApiConfig`, который находится в папке приложения\_Start.

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a>HttpError

Объект **HttpError** обеспечивает единообразный способ возврата сведений об ошибке в тексте ответа. В следующем примере показано, как вернуть код состояния HTTP 404 (не найдено) с **HttpError** в тексте ответа.

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

**Креатиррорреспонсе** — это метод расширения, определенный в классе **System .NET. http. хттпрекуестмессажеекстенсионс** . На внутреннем уровне **креатиррорреспонсе** создает экземпляр **HttpError** , а затем создает **HttpResponseMessage** , содержащий **HttpError**.

В этом примере, если метод выполнен успешно, он возвращает продукт в HTTP-ответе. Но если запрошенный продукт не найден, HTTP-ответ содержит **HttpError** в тексте запроса. Ответ может выглядеть следующим образом:

[!code-console[Main](exception-handling/samples/sample9.cmd)]

Обратите внимание, что в этом примере **HttpError** был СЕРИАЛИЗОВАН в JSON. Одним из преимуществ использования **HttpError** является то, что он проходит через тот же процесс [согласования содержимого](../formats-and-model-binding/content-negotiation.md) и сериализации, что и любая другая строго типизированная модель.

### <a name="httperror-and-model-validation"></a>HttpError и проверка модели

Для проверки модели можно передать состояние модели в **креатиррорреспонсе**, чтобы включить в ответ ошибки проверки:

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

Этот пример может вернуть следующий ответ:

[!code-console[Main](exception-handling/samples/sample11.cmd)]

Дополнительные сведения о проверке модели см. [в разделе Проверка модели в веб-API ASP.NET](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).

### <a name="using-httperror-with-httpresponseexception"></a>Использование HttpError с Хттпреспонсиксцептион

В предыдущих примерах возвращается сообщение **HttpResponseMessage** из действия контроллера, но можно также использовать **Хттпреспонсиксцептион** для возврата **HttpError**. Это позволяет возвращать строго типизированную модель в нормальном случае успеха, при этом возвращая **HttpError** в случае ошибки:

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
