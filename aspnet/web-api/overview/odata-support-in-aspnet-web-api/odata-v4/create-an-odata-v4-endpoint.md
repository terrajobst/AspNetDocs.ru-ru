---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: Создание конечной точки OData v4 с помощью веб-API ASP.NET 2,2 | Документация Майкрософт
author: MikeWasson
description: Open Data Protocol (OData) — это протокол доступа к данным для Интернета. OData обеспечивает единообразный способ запроса и обработки наборов данных с помощью операций CRUD...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484500"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a>Создание конечной точки OData v4 с помощью веб-API ASP.NET 

> Open Data Protocol (OData) — это протокол доступа к данным для Интернета. OData обеспечивает единообразный способ запроса и обработки наборов данных с помощью операций CRUD (создание, чтение, обновление и удаление).
>
> Веб-API ASP.NET поддерживает протокол версии v3 и v4. Можно даже иметь конечную точку V4, которая работает параллельно с конечной точкой v3.
>
> В этом руководстве показано, как создать конечную точку OData V4, которая поддерживает операции CRUD.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
> - Веб-API 5,2
> - OData v4
> - Visual Studio 2017 (загрузить Visual Studio 2017 [здесь](https://visualstudio.microsoft.com/downloads/))
> - Entity Framework 6
> - 4\.7.2 .NET
>
> ## <a name="tutorial-versions"></a>Учебные версии
>
> Сведения о OData версии 3 см. в разделе [Создание конечной точки OData v3](../odata-v3/creating-an-odata-endpoint.md).

## <a name="create-the-visual-studio-project"></a>Создание проекта Visual Studio

В Visual Studio в меню **файл** выберите пункт **создать** &gt; **проект**.

Разверните узел **установленные** &gt; **Visual C#**  &gt; **Web**и выберите шаблон **веб-приложение ASP.NET (.NET Framework)** . Присвойте проекту имя &quot;Продуктсервице&quot;.

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

Нажмите кнопку **ОК**.

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

Выберите шаблон **Пустой**. В разделе **Добавление папок и основных ссылок для:** выберите **веб-API**. Нажмите кнопку **ОК**.

## <a name="install-the-odata-packages"></a>Установка пакетов OData

В меню **Сервис**  последовательно выберите пункты **Диспетчер пакетов NuGet** &gt; **Консоль диспетчера пакетов**. В окне консоли диспетчера пакетов введите:

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

Эта команда устанавливает последние пакеты NuGet OData.

## <a name="add-a-model-class"></a>Добавление класса модели

*Модель* — это объект, представляющий сущность данных в приложении.

В обозревателе решений щелкните правой кнопкой мыши папку Models. В контекстном меню выберите **добавить** &gt; **класс**.

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> По соглашению классы модели помещаются в папку Models, но вам не нужно следовать этому соглашению в своих проектах.

Назовите класс `Product`. В файле Product.cs замените стандартный код следующим:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

Свойство `Id` — это ключ сущности. Клиенты могут запрашивать сущности по ключу. Например, чтобы получить продукт с ИДЕНТИФИКАТОРом 5, URI `/Products(5)`. Свойство `Id` также будет первичным ключом в серверной базе данных.

## <a name="enable-entity-framework"></a>Включить Entity Framework

В этом руководстве мы будем использовать Entity Framework (EF) Code First для создания серверной базы данных.

> [!NOTE]
> Для веб-API OData не требуется EF. Используйте любой уровень доступа к данным, который может переводить сущности базы данных в модели.

Сначала установите пакет NuGet для EF. В меню **Сервис**  последовательно выберите пункты **Диспетчер пакетов NuGet** &gt; **Консоль диспетчера пакетов**. В окне консоли диспетчера пакетов введите:

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

Откройте файл Web. config и добавьте следующий раздел в элемент **Configuration** после элемента **configSections** .

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

Этот параметр добавляет строку подключения для базы данных LocalDB. Эта база данных будет использоваться при локальном запуске приложения.

Затем добавьте класс с именем `ProductsContext` в папку Models:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

В конструкторе `"name=ProductsContext"` выдает имя строки подключения.

## <a name="configure-the-odata-endpoint"></a>Настройка конечной точки OData

Откройте файл App\_Start/WebApiConfig. cs. Добавьте следующие операторы **using** :

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

Затем добавьте следующий код в метод **Register** :

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

Этот код выполняет два действия:

- Создает EDM (модель EDM).
- Добавляет маршрут.

EDM — это абстрактная модель данных. Модель EDM используется для создания документа метаданных службы. Класс **одатаконвентионмоделбуилдер** создает модель EDM с использованием соглашений об именовании по умолчанию. Этот подход требует наименьшего кода. Если требуется больший контроль над EDM, можно использовать класс **одатамоделбуилдер** для создания модели EDM путем явного добавления свойств, ключей и свойств навигации.

*Маршрут* сообщает веб-API о МАРШРУТИЗАЦИИ запросов HTTP к конечной точке. Чтобы создать маршрут OData V4, вызовите метод расширения **маподатасервицерауте** .

Если в приложении есть несколько конечных точек OData, создайте отдельный маршрут для каждого из них. Присвойте каждому маршруту уникальное имя маршрута и префикс.

## <a name="add-the-odata-controller"></a>Добавление контроллера OData

*Контроллер* — это класс, который обрабатывает HTTP-запросы. Для каждого набора сущностей в службе OData создается отдельный контроллер. В этом руководстве вы создадите один контроллер для сущности `Product`.

В обозреватель решений щелкните правой кнопкой мыши папку Controllers и выберите пункт **добавить** &gt; **класс**. Назовите класс `ProductsController`.

> [!NOTE]
> В версии этого руководства для OData v3 используется формирование шаблонов для **добавления контроллеров** . В настоящее время формирование шаблонов для OData v4 не предусмотрено.

Замените стандартный код в ProductsController.cs следующим кодом.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

Контроллер использует класс `ProductsContext` для доступа к базе данных с помощью EF. Обратите внимание, что контроллер переопределяет метод **Dispose** для удаления **продуктсконтекст**.

Это начальная точка контроллера. Далее мы добавим методы для всех операций CRUD.

## <a name="query-the-entity-set"></a>Запрос набора сущностей

Добавьте следующие методы для `ProductsController`.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

Версия метода `Get` без параметров возвращает коллекцию всех продуктов. Метод `Get` с параметром *ключа* ищет продукт по ключу (в данном случае свойство `Id`).

Атрибут **[енаблекуери]** позволяет клиентам изменять запрос с помощью параметров запроса, таких как $filter, $sort и $Page. Дополнительные сведения см. в разделе [Поддержка параметров запросов OData](../supporting-odata-query-options.md).

## <a name="add-an-entity-to-the-entity-set"></a>Добавление сущности в набор сущностей

Чтобы позволить клиентам добавлять новый продукт в базу данных, добавьте следующий метод для `ProductsController`.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a>Обновление сущности

OData поддерживает две различные семантики для обновления сущности, исправления и размещения.

- ИСПРАВЛЕНИЕ выполняет частичное обновление. Клиент указывает только обновляемые свойства.
- Постановка заменяет всю сущность.

Недостаток метода размещения заключается в том, что клиент должен отправлять значения для всех свойств сущности, включая неизменяемые значения. В [спецификации OData](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) указывается, что это исправление является предпочтительным.

В любом случае ниже приведен код для методов PATCH и РАЗМЕСТИЛ:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

В случае исправления контроллер использует тип **разностного&lt;t&gt;** для отслеживания изменений.

## <a name="delete-an-entity"></a>Удаление сущности

Чтобы разрешить клиентам удалять продукт из базы данных, добавьте следующий метод для `ProductsController`.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
