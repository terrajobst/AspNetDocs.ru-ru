---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: Общие сведения о фильтрах действий (C#) | Документация Майкрософт
author: microsoft
description: Цель данного руководства — объяснить фильтров действий. Фильтр операции — атрибут, который можно применить к действию контроллера--или всего контроллера...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c7706d8252d5a0271f1b9243fa8eb282f722654
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059091"
---
<a name="understanding-action-filters-c"></a>Общие сведения о фильтрах действий (C#)
====================
по [Microsoft](https://github.com/microsoft)

[Загрузить PDF-файл](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> Цель данного руководства — объяснить фильтров действий. Фильтр операции — атрибут, который можно применить к действию контроллера--или всего контроллера--, изменяет способ, в котором выполняется действие.


## <a name="understanding-action-filters"></a>Общие сведения о фильтрах действий

Цель данного руководства — объяснить фильтров действий. Фильтр операции — атрибут, который можно применить к действию контроллера--или всего контроллера--, изменяет способ, в котором выполняется действие. Платформа ASP.NET MVC включает в себя несколько фильтров действий:

- OutputCache-этот фильтр действий кэширует выходные данные действия контроллера, в течение определенного времени.
- HandleError — это фильтр действий обрабатывает ошибки, возникшие при выполнении действия контроллера.
- Авторизация — этот фильтр действий позволяет ограничить доступ к определенному пользователю или роли.

Также можно создать собственные фильтры настраиваемого действия. Например может потребоваться создание пользовательского фильтра действий, чтобы реализовать пользовательскую систему аутентификации. Или, может потребоваться создание фильтра действий, изменяющих данные представления, возвращаемое в результате действия контроллера.

В этом руководстве вы узнаете, как для создания фильтра действий с нуля. Мы создадим фильтр действий журнала, который записывает различные этапы обработки действия в окне вывода Visual Studio.

### <a name="using-an-action-filter"></a>С помощью фильтра действий

Фильтр операции — атрибут. Большинство фильтров действий можно применить к действию отдельного контроллера или всего контроллера.

Например, контроллер данных в листинге 1 предоставляет действие с именем `Index()` , возвращает текущее время. Это действие снабжен `OutputCache` фильтра действий. Этот фильтр вызывает значение, возвращаемое в результате действия должен быть помещен в кэш на 10 секунд.

**Листинг 1. `Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

При многократном запуске `Index()` действие, введя URL-адрес/Data/индекса в адресную строку браузера и обновление кнопку несколько раз, вы увидите то же время на 10 секунд. Выходные данные `Index()` действие кэшируется на 10 секунд (см. рис. 1).


[![Время кэширования](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**Рис 01**: Время ([Просмотр полноразмерного изображения](understanding-action-filters-cs/_static/image3.png))


В листинге 1 фильтр одно действие — `OutputCache` фильтр действий — применяется к `Index()` метод. Если требуется, можно применить несколько фильтров действий к одному действию. Например, может потребоваться применить оба `OutputCache` и `HandleError` фильтров действий к одному действию.

В листинге 1 `OutputCache` фильтр действий применяется к `Index()` действие. Вы также можете применить этот атрибут, чтобы `DataController` сам по себе класс. В этом случае результат, возвращаемый никаких действий, предоставляемых контроллер будет кэшироваться на 10 секунд.

### <a name="the-different-types-of-filters"></a>Различные типы фильтров

Платформа ASP.NET MVC поддерживает четыре различных типа фильтров:

1. Фильтры авторизации — реализует `IAuthorizationFilter` атрибута.
2. Фильтры действий — реализует `IActionFilter` атрибута.
3. Фильтры — реализует результатов `IResultFilter` атрибута.
4. Фильтры исключений — реализует `IExceptionFilter` атрибута.

Фильтры выполняются в порядке, указанном выше. Например фильтры авторизации всегда выполняются перед фильтров действий и фильтров исключений, всегда выполняются после любого другого типа фильтра.

Фильтры авторизации используются для реализации проверки подлинности и авторизации для действий контроллеров. Например фильтра Authorize является примером фильтра авторизации.

Фильтры действий содержат логику, выполняемую перед и после выполнения действия контроллера. Можно использовать фильтр действий, например, для изменения представления данных, возвращающий действие контроллера.

Фильтры результатов содержат логику, выполняемую перед и после выполнения результат представления. Например, может потребоваться изменить результат представления непосредственно перед визуализации представления в браузер.

Фильтры исключений — это последний тип фильтра для выполнения. Фильтр исключений можно использовать для обработки ошибок, вызванных результатов действий контроллера или действия контроллера. Также можно использовать фильтры исключений для ведения журнала ошибок.

У каждого типа фильтра выполняется в определенном порядке. Если вы хотите управлять порядком, в котором выполняются фильтры одного типа можно задать свойство порядок фильтра.

Является базовым классом для всех фильтров действий `System.Web.Mvc.FilterAttribute` класса. Если вы хотите реализовать определенный тип фильтра, то необходимо создать класс, наследующий от базового класса фильтра и реализует один или несколько `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, или `IExceptionFilter` интерфейсов.

### <a name="the-base-actionfilterattribute-class"></a>Базовый класс ActionFilterAttribute

Для повышения его читаемости для реализации пользовательского фильтра действий, платформа ASP.NET MVC включает в себя базовый `ActionFilterAttribute` класса. Этот класс реализует оба `IActionFilter` и `IResultFilter` интерфейсы и наследует от `Filter` класса.

Терминология здесь не полностью согласована. С технической точки зрения класс, наследуемый от класса ActionFilterAttribute является фильтром действий и фильтра результатов. Тем не менее в том смысле, свободные, фильтр действий word используется для ссылки на любой тип фильтра в платформе ASP.NET MVC.

Базовый `ActionFilterAttribute` класс содержит следующие методы, которые можно переопределить:

- OnActionExecuting — этот метод вызывается перед выполнением действия контроллера.
- OnActionExecuted — этот метод вызывается после выполнения действия контроллера.
- OnResultExecuting — этот метод вызывается до выполнения результата действия контроллера.
- OnResultExecuted — этот метод вызывается после выполнения результата действия контроллера.

В следующем разделе мы рассмотрим, как можно реализовать каждый из этих различных методов.

### <a name="creating-a-log-action-filter"></a>Создание фильтра журнала действий

Чтобы проиллюстрировать, как создать настраиваемого фильтра действий, мы создадим пользовательского фильтра действий, заносящий в журнал на этапах обработки действия контроллера, в окне вывода Visual Studio. Наши `LogActionFilter` содержится в листинге 2.

**Листинг 2. `ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

В листинге 2 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, и `OnResultExecuted()` вызывать все методы `Log()` метод. Имя метода и текущих данных маршрута передается `Log()` метод. `Log()` Метод записывает сообщение в окне вывода Visual Studio (см. рис. 2).


[![Запись в окно вывода Visual Studio](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**Рис. 02**: Запись в окно вывода Visual Studio ([Просмотр полноразмерного изображения](understanding-action-filters-cs/_static/image6.png))


Контроллер Home в листинге 3 показано, как можно применить фильтр журнала действий в класс контроллера целиком. Каждый раз, когда любое из действий, предоставляемых контроллера Home вызываются — либо `Index()` метод или `About()` метод — этапы обработки, действия записываются в окно вывода Visual Studio.

**Листинг 3. `Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>Сводка

В этом руководстве вы ознакомились с фильтров операций ASP.NET MVC. Вы узнали о четыре различных типа фильтров: фильтры авторизации, фильтров действий, фильтров результатов и фильтры исключений. Вы также узнали о базовый `ActionFilterAttribute` класса.

Наконец вы узнали, как выполнить простой фильтр действий. Мы создали фильтр действий журнала, который записывает журнал на этапах обработки действия контроллера, в окне вывода Visual Studio.

> [!div class="step-by-step"]
> [Назад](asp-net-mvc-routing-overview-cs.md)
> [Вперед](improving-performance-with-output-caching-cs.md)