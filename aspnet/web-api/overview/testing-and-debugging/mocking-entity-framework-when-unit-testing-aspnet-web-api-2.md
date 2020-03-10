---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Имитация Entity Framework при модульном тестировании веб-API ASP.NET 2 | Документация Майкрософт
author: Rick-Anderson
description: В этом руководстве и приложении показано, как создавать модульные тесты для приложения Web API 2, которое использует Entity Framework. В нем показано, как изменить...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447090"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>Имитация Entity Framework при модульном тестировании веб-API ASP.NET 2

от [Tom фитзмаккен](https://github.com/tfitzmac)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> В этом руководстве и приложении показано, как создавать модульные тесты для приложения Web API 2, которое использует Entity Framework. В нем показано, как изменить сформированный контроллер, чтобы включить передачу объекта контекста для тестирования и создать тестовые объекты, работающие с Entity Framework.
>
> Общие сведения о модульном тестировании с помощью веб-API ASP.NET см. [в разделе модульное тестирование с помощью веб-API ASP.NET 2](unit-testing-with-aspnet-web-api.md).
>
> В этом учебнике предполагается, что вы знакомы с основными концепциями веб-API ASP.NET. Вводное руководство см. в разделе [Начало работы с веб-API ASP.NET 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Веб-API 2

## <a name="in-this-topic"></a>В этом разделе

Этот раздел состоит из следующих подразделов.

- [Предварительные требования](#prereqs)
- [Скачать код](#download)
- [Создание приложения с помощью проекта модульного теста](#appwithunittest)
- [Создание класса Model](#modelclass)
- [Добавление контроллера](#controller)
- [Добавить внедрение зависимостей](#dependency)
- [Установка пакетов NuGet в тестовом проекте](#testpackages)
- [Создать контекст теста](#testcontext)
- [Создание тестов](#tests)
- [Выполнение тестов](#runtests)

Если вы уже выполнили действия по [модульному тестированию с веб-API ASP.NET 2](unit-testing-with-aspnet-web-api.md), можно перейти к разделу [Добавление контроллера](#controller).

<a id="prereqs"></a>
## <a name="prerequisites"></a>предварительные требования

Visual Studio 2017 Community, Professional или Enterprise Edition

<a id="download"></a>
## <a name="download-code"></a>Скачать код

Скачайте [завершенный проект](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11). Загружаемый проект включает код модульного теста для этого раздела и раздел [модульного тестирования веб-API ASP.NET 2](unit-testing-with-aspnet-web-api.md) .

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>Создание приложения с помощью проекта модульного теста

Вы можете создать проект модульного теста при создании приложения или добавить проект модульного теста в существующее приложение. В этом руководстве показано, как создать проект модульного теста при создании приложения.

Создайте новое веб-приложение ASP.NET с именем **стореапп**.

В окнах Новый проект ASP.NET выберите **пустой** шаблон и добавьте папки и основные ссылки для веб-API. Выберите параметр **Добавить модульные тесты** . Проект модульного теста автоматически называется **стореапп. Tests**. Это имя можно не заключить.

![Создание проекта модульного теста](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

После создания приложения вы увидите, что он содержит два проекта — **стореапп** и **стореапп. Tests**.

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>Создание класса Model

В проекте Стореапп добавьте файл класса в папку **Models** с именем **Product.CS**. Замените содержимое файла на код, приведенный ниже.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

Создайте решение.

<a id="controller"></a>
## <a name="add-the-controller"></a>Добавление контроллера

Щелкните правой кнопкой мыши папку Controllers и выберите **Добавить** и создать шаблонный **элемент**. Выберите контроллер веб-API 2 с действиями с помощью Entity Framework.

![Добавить новый контроллер](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

Задайте следующие значения:

- Имя контроллера: **продуктконтроллер**
- Класс модели: **Product**
- Класс контекста данных: [кнопка " **создать контекст данных** ", которая заполняет значения, показанные ниже]

![Указание контроллера](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

Нажмите кнопку **Добавить** , чтобы создать контроллер с автоматически созданным кодом. Код включает методы для создания, извлечения, обновления и удаления экземпляров класса Product. В следующем коде показан метод добавления продукта. Обратите внимание, что метод возвращает экземпляр **ихттпактионресулт**.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

Ихттпактионресулт — это одна из новых возможностей веб-API 2, которая упрощает разработку модульных тестов.

В следующем разделе вы настроите созданный код, чтобы упростить передачу тестовых объектов на контроллер.

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>Добавить внедрение зависимостей

В настоящее время класс Продуктконтроллер жестко закодирован для использования экземпляра класса Стореаппконтекст. Шаблон, именуемый внедрением зависимостей, будет использоваться для изменения приложения и удаления этой жесткой зависимости. Нарушая эту зависимость, можно передать макет объекта при тестировании.

Щелкните правой кнопкой мыши папку **Models** и добавьте новый интерфейс с именем **истореаппконтекст**.

Замените код следующим кодом.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

Откройте файл StoreAppContext.cs и внесите следующие выделенные изменения. Важно отметить следующие важные изменения.

- Класс Стореаппконтекст реализует интерфейс Истореаппконтекст
- Реализован метод Маркасмодифиед

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

Откройте файл ProductController.cs. Измените существующий код в соответствии с выделенным кодом. Эти изменения нарушают зависимость от Стореаппконтекст и позволяют другим классам передавать другой объект для класса контекста. Это изменение позволит передать контекст теста во время модульных тестов.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

Есть еще одно изменение, которое необходимо внести в Продуктконтроллер. В методе **путпродукт** замените строку, которая задает состояние сущности, измененной с помощью вызова метода маркасмодифиед.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

Создайте решение.

Теперь вы готовы к настройке тестового проекта.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>Установка пакетов NuGet в тестовом проекте

Если для создания приложения используется пустой шаблон, проект модульного теста (Стореапп. Tests) не включает установленные пакеты NuGet. Другие шаблоны, например шаблон веб-API, включают некоторые пакеты NuGet в проект модульного теста. Для работы с этим руководством необходимо включить в тестовый проект пакет Entity Framework и пакет Microsoft ASP.NET Web API 2 Core.

Щелкните правой кнопкой мыши проект Стореапп. Tests и выберите пункт **Управление пакетами NuGet**. Чтобы добавить пакеты в проект, необходимо выбрать проект Стореапп. Tests.

![Управление пакетами](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

В веб-пакетах найдите и установите пакет EntityFramework (версии 6,0 или более поздней). Если кажется, что пакет EntityFramework уже установлен, возможно, вместо проекта Стореапп. Tests был выбран проект Стореапп.

![добавить Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

Найдите и установите Microsoft ASP.NET основной пакет веб-API 2.

![Установка основного пакета веб-API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

Закройте окно Управление пакетами NuGet.

<a id="testcontext"></a>
## <a name="create-test-context"></a>Создать контекст теста

Добавьте класс с именем **тестдбсет** в тестовый проект. Этот класс служит базовым классом для набора проверочных данных. Замените код следующим кодом.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

Добавьте класс с именем **тестпродуктдбсет** в тестовый проект, содержащий следующий код.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

Добавьте класс с именем **тестстореаппконтекст** и замените существующий код следующим кодом.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>Создание тестов

По умолчанию тестовый проект содержит пустой тестовый файл с именем **UnitTest1.CS**. В этом файле показаны атрибуты, используемые для создания методов теста. В этом руководстве вы можете удалить этот файл, так как вы добавите новый тестовый класс.

Добавьте класс с именем **тестпродуктконтроллер** в тестовый проект. Замените код следующим кодом.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>Выполнение тестов

Теперь все готово для выполнения тестов. Будет протестирован весь метод, помеченный атрибутом **TestMethod** . В пункте меню **тест** выполните тесты.

![Запуск тестов](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

Откройте окно **обозревателя тестов** и обратите внимание на результаты тестов.

![результаты теста](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
