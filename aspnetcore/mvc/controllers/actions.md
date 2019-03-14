---
title: Обработка запросов с помощью контроллеров в ASP.NET Core MVC
author: ardalis
description: ''
ms.author: riande
ms.date: 07/03/2017
uid: mvc/controllers/actions
ms.openlocfilehash: 8289424b3cd3678bea18a25c7850e409795d1577
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57060471"
---
# <a name="handle-requests-with-controllers-in-aspnet-core-mvc"></a>Обработка запросов с помощью контроллеров в ASP.NET Core MVC

Авторы: [Стив Смит](https://ardalis.com/) (Steve Smith) и [Скотт Эдди](https://github.com/scottaddie) (Scott Addie)

Контроллеры, действия и результаты действий являются основополагающей составляющей разработки приложений с помощью ASP.NET Core MVC.

## <a name="what-is-a-controller"></a>Что такое контроллер?

Контроллер используется для определения и группировки набора действий. Действие (или *метод действия*) — это метод на контроллере, обрабатывающий запросы. Контроллеры логически группируют схожие действия. Это объединение действий позволяет коллективно применять общие наборы правил, например маршрутизации, кэширования и авторизации. Запросы сопоставляются с действиями посредством [маршрутизации](xref:mvc/controllers/routing).

По соглашению классы контроллеров:
* размещаются в папке *Controllers* на корневом уровне проекта;
* наследуют от `Microsoft.AspNetCore.Mvc.Controller`.

Контроллер — это допускающий создание экземпляров класс, в котором выполняется хотя бы одно из следующих условий:
* Имя класса имеет суффикс "Controller".
* Класс наследует от класса, имя которого имеет суффикс "Controller".
* Класс декорируется атрибутом `[Controller]`.

С классом контроллера не должен быть связан атрибут `[NonController]`.

Контроллеры должны соответствовать [принципу явных зависимостей](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies). Существует несколько подходов к реализации этого принципа. Если нескольким действиям контроллера требуется одна служба, рекомендуется использовать [внедрение через конструктор](xref:mvc/controllers/dependency-injection#constructor-injection) для запроса этих зависимостей. Если служба требуется только одному методу действия, рекомендуется использовать [внедрение действий](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices) для запроса зависимости.

В рамках шаблона **M****V****C** контроллер отвечает за начальную обработку запроса и создание экземпляра модели. Как правило, бизнес-решения следует выполнять внутри модели.

Контроллер принимает результат обработки модели (если он есть) и возвращает подходящее представление и связанные с ним данные или результат вызова API. Дополнительные сведения см. в разделах [Общие сведения о ASP.NET Core MVC](xref:mvc/overview) и [Начало работы с ASP.NET Core MVC и Visual Studio](xref:tutorials/first-mvc-app/start-mvc).

Контроллер является абстракцией на *уровне пользовательского интерфейса*. Он должен проверить допустимость данных запроса и выбрать возвращаемое представление (или результат для API). В хорошо организованных приложениях он не включает в себя доступ к данным или бизнес-логику напрямую. Вместо этого контроллер делегирует обработку этих обязанностей службам.

## <a name="defining-actions"></a>Определение действий

Открытые методы в контроллере, кроме декорированных с помощью атрибута `[NonAction]`, являются действиями. Параметры для действий привязаны к данным запроса и проверяются с помощью [привязки модели](xref:mvc/models/model-binding). Проверка модели выполняется для всего, что привязано к модели. Значение свойства `ModelState.IsValid` указывает успешность привязки и проверки модели.

Методы действия должны содержать логику для сопоставления запроса с бизнес-фактором. В общем случае бизнес-факторы должны быть представлены в виде служб, к которым контроллер обращается посредством [внедрения зависимостей](xref:mvc/controllers/dependency-injection). После этого действия сопоставляют результат бизнес-операции с состоянием приложения.

Действия могут возвращать любое значение, но часто возвращают экземпляр `IActionResult` (или `Task<IActionResult>` для асинхронных методов), формирующий отклик. Метод действия отвечает за выбор *типа отклика*. Результат действия *осуществляет отклик*.

### <a name="controller-helper-methods"></a>Вспомогательные методы Controller

Контроллеры обычно наследуют от [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller), хотя это не является обязательным. Наследование от `Controller` предоставляет доступ к трем категориям вспомогательных методов:

#### <a name="1-methods-resulting-in-an-empty-response-body"></a>1. Методы, дающие пустой основной текст отклика

Заголовок HTTP-отклика `Content-Type` не включается, так как в тексте отклика нет содержимого для описания.

В этой категории есть два типа результатов: перенаправление и код состояния HTTP.

* **Код состояния HTTP**

    Этот тип возвращает код состояния HTTP. К этому типу вспомогательных методов относятся `BadRequest`, `NotFound` и `Ok`. Например, при выполнении `return BadRequest();` создает код состояния 400. Если такие методы, как `BadRequest`, `NotFound` и `Ok`, перегружены, они больше не могут выступать в качестве ответчиков кода состояния HTTP, так как выполняется согласование содержимого.

* **Перенаправление**

    Этот тип возвращает перенаправление в действие или назначение (с помощью `Redirect`, `LocalRedirect`, `RedirectToAction` или `RedirectToRoute`). Например, `return RedirectToAction("Complete", new {id = 123});` перенаправляет `Complete`, передав анонимный объект.

    Тип результатов перенаправления отличается от кода состояния HTTP, главным образом, добавлением заголовка HTTP-отклика `Location`.

#### <a name="2-methods-resulting-in-a-non-empty-response-body-with-a-predefined-content-type"></a>2. Методы, дающие непустой основной текст отклика с предопределенным типом содержимого

Большинство вспомогательных методов в этой категории имеют свойство `ContentType`, что позволяет задать заголовок отклика `Content-Type` для описания основного текста отклика.

В этой категории есть два типа результатов: [представление](xref:mvc/views/overview) и [форматированный ответ](xref:web-api/advanced/formatting).

* **Вид**

    Этот тип возвращает представление, использующее модель для отрисовки HTML. Например, `return View(customer);` передает модель в представление для привязки данных.

* **Форматированный отклик**

    Этот тип возвращает JSON или аналогичный формат обмена данными для представления объекта определенным образом. Например, `return Json(customer);` сериализует указанный объект в формат JSON.
    
    Другими распространенными методами этого типа являются `File` и `PhysicalFile`. Например, `return PhysicalFile(customerFilePath, "text/xml");` возвращает [PhysicalFileResult](/dotnet/api/microsoft.aspnetcore.mvc.physicalfileresult).

#### <a name="3-methods-resulting-in-a-non-empty-response-body-formatted-in-a-content-type-negotiated-with-the-client"></a>3. Методы, дающие непустой основной текст отклика и отформатированные с типом содержимого, согласованным с клиентом

Эта категория более известна как **согласование содержимого**. [Согласование содержимого](xref:web-api/advanced/formatting#content-negotiation) применяется, когда действие возвращает тип [ObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.objectresult) или что-то отличное от реализации [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult). Действие, которое возвращает значение, отличное от реализации `IActionResult` (например, `object`), также возвращает форматированный отклик.

Другими вспомогательными методами этого типа являются `BadRequest`, `CreatedAtRoute` и `Ok`. Примерами этих методов являются `return BadRequest(modelState);`, `return CreatedAtRoute("routename", values, newobject);` и `return Ok(value);`, соответственно. Обратите внимание, что `BadRequest` и `Ok` выполняют согласование содержимого только при передаче значения. Без передачи значения они выступают в качестве типов результатов для кода состояния HTTP. С другой стороны, метод `CreatedAtRoute` всегда выполняет согласование содержимого, так как все его перегрузки требуют передачи значения.

### <a name="cross-cutting-concerns"></a>Сквозная функциональность

Приложения обычно имеют общие части рабочего процесса. В качестве примера можно привести приложение, которое требует пройти проверку подлинности для доступа к корзине для покупок, или приложение, кэширующее данные на некоторых страницах. Чтобы выполнить логику до или после метода действия, используйте *фильтр*. Использование [фильтров](xref:mvc/controllers/filters) наряду со сквозной функциональностью позволяет уменьшить дублирование.

Большинство атрибутов фильтров, например `[Authorize]`, можно применить на уровне контроллера или действия в зависимости от нужного уровня детализации.

Обработка ошибок и кэширование откликов часто относятся к сквозной функциональности:
   * [Обработка ошибок](xref:mvc/controllers/filters#exception-filters)
   * [Кэширование ответов](xref:performance/caching/response)

Многие сквозные задачи можно обрабатывать с помощью фильтров или настраиваемого [ПО промежуточного слоя](xref:fundamentals/middleware/index).