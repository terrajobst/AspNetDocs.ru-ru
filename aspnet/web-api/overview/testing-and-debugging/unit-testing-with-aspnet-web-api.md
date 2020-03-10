---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: Модульное тестирование веб-API ASP.NET 2 | Документация Майкрософт
author: Rick-Anderson
description: В этом руководстве и приложении показано, как создавать простые модульные тесты для приложения веб-API 2. В этом учебнике показано, как включить proj модульного теста...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446988"
---
# <a name="unit-testing-aspnet-web-api-2"></a>Модульное тестирование веб-API ASP.NET 2

от [Tom фитзмаккен](https://github.com/tfitzmac)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> В этом руководстве и приложении показано, как создавать простые модульные тесты для приложения веб-API 2. В этом руководстве показано, как включить проект модульного теста в решение и написать методы теста, которые проверяют возвращенные значения из метода контроллера.
>
> В этом учебнике предполагается, что вы знакомы с основными концепциями веб-API ASP.NET. Вводное руководство см. в разделе [Начало работы с веб-API ASP.NET 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).
>
> Модульные тесты в этом разделе намеренно ограничены простыми сценариями данных. Дополнительные сведения о модульном тестировании для расширенных сценариев данных см. в разделе [макет Entity Framework при модульном тестировании веб-API ASP.NET 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).
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
    - [Добавить проект модульного теста при создании приложения](#whencreate)
    - [Добавление проекта модульного теста в существующее приложение](#addtoexisting)
- [Настройка приложения веб-API 2](#setupproject)
- [Установка пакетов NuGet в тестовом проекте](#testpackages)
- [Создание тестов](#tests)
- [Выполнение тестов](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>предварительные требования

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional или Enterprise Edition

<a id="download"></a>
## <a name="download-code"></a>Скачать код

Скачайте [завершенный проект](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11). Загружаемый проект включает код модульного теста для этого раздела и для [Entity Framework при модульном тестировании веб-API ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) разделе.

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>Создание приложения с помощью проекта модульного теста

Вы можете создать проект модульного теста при создании приложения или добавить проект модульного теста в существующее приложение. В этом учебнике показаны оба метода создания проекта модульного теста. Для выполнения действий, описанных в этом руководстве, можно использовать любой из этих подходов.

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>Добавить проект модульного теста при создании приложения

Создайте новое веб-приложение ASP.NET с именем **стореапп**.

![создание проекта](unit-testing-with-aspnet-web-api/_static/image1.png)

В окнах Новый проект ASP.NET выберите **пустой** шаблон и добавьте папки и основные ссылки для веб-API. Выберите параметр **Добавить модульные тесты** . Проект модульного теста автоматически называется **стореапп. Tests**. Это имя можно не заключить.

![Создание проекта модульного теста](unit-testing-with-aspnet-web-api/_static/image2.png)

После создания приложения вы увидите, что он содержит два проекта.

![два проекта](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>Добавление проекта модульного теста в существующее приложение

Если вы не создавали проект модульного теста при создании приложения, вы можете добавить его в любое время. Например, предположим, что у вас уже есть приложение с именем Стореапп и вы хотите добавить модульные тесты. Чтобы добавить проект модульного теста, щелкните решение правой кнопкой мыши и выберите **Добавить** и **Новый проект**.

![Добавить новый проект в решение](unit-testing-with-aspnet-web-api/_static/image4.png)

Выберите **тест** в левой области и выберите **проект модульного теста** для типа проекта. Назовите проект **стореапп. Tests**.

![Добавить проект модульного теста](unit-testing-with-aspnet-web-api/_static/image5.png)

Вы увидите проект модульного теста в решении.

В проекте модульного теста добавьте ссылку на проект в исходный проект.

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>Настройка приложения веб-API 2

В проекте Стореапп добавьте файл класса в папку **Models** с именем **Product.CS**. Замените содержимое файла на код, приведенный ниже.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

Создайте решение.

Щелкните правой кнопкой мыши папку Controllers и выберите **Добавить** и создать шаблонный **элемент**. Выберите **контроллер веб-API 2 — пустой**.

![Добавить новый контроллер](unit-testing-with-aspnet-web-api/_static/image6.png)

Задайте имя контроллера **симплепродуктконтроллер**и нажмите кнопку **Добавить**.

![Указание контроллера](unit-testing-with-aspnet-web-api/_static/image7.png)

Замените существующий код следующим кодом: Чтобы упростить этот пример, данные хранятся в списке, а не в базе данных. Список, определенный в этом классе, представляет рабочие данные. Обратите внимание, что контроллер включает конструктор, который принимает в качестве параметра список объектов Product. Этот конструктор позволяет передавать тестовые данные при модульном тестировании. Контроллер также содержит два **асинхронных** метода для демонстрации асинхронных методов модульного тестирования. Эти асинхронные методы были реализованы путем вызова **Task. FromResult** для сворачивания лишнего кода, но обычно методы будут включать ресурсоемкие операции.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

Метод произведения возвращает экземпляр интерфейса **ихттпактионресулт** . Ихттпактионресулт — это одна из новых возможностей веб-API 2, которая упрощает разработку модульных тестов. Классы, реализующие интерфейс Ихттпактионресулт, находятся в пространстве имен [System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) . Эти классы представляют возможные ответы от запроса действия и соответствуют кодам состояния HTTP.

Создайте решение.

Теперь вы готовы к настройке тестового проекта.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>Установка пакетов NuGet в тестовом проекте

Если для создания приложения используется пустой шаблон, проект модульного теста (Стореапп. Tests) не включает установленные пакеты NuGet. Другие шаблоны, например шаблон веб-API, включают некоторые пакеты NuGet в проект модульного теста. Для работы с этим руководством необходимо включить основной пакет веб-API 2 Microsoft ASP.NET в тестовый проект.

Щелкните правой кнопкой мыши проект Стореапп. Tests и выберите пункт **Управление пакетами NuGet**. Чтобы добавить пакеты в проект, необходимо выбрать проект Стореапп. Tests.

![Управление пакетами](unit-testing-with-aspnet-web-api/_static/image8.png)

Найдите и установите Microsoft ASP.NET основной пакет веб-API 2.

![Установка основного пакета веб-API](unit-testing-with-aspnet-web-api/_static/image9.png)

Закройте окно Управление пакетами NuGet.

<a id="tests"></a>
## <a name="create-tests"></a>Создание тестов

По умолчанию тестовый проект содержит пустой тестовый файл с именем UnitTest1.cs. В этом файле показаны атрибуты, используемые для создания методов теста. Для модульных тестов можно либо использовать этот файл, либо создать собственный файл.

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

В этом руководстве вы создадите собственный тестовый класс. Вы можете удалить файл UnitTest1.cs. Добавьте класс с именем **TestSimpleProductController.CS**и замените код следующим кодом.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>Выполнение тестов

Теперь все готово для выполнения тестов. Будет протестирован весь метод, помеченный атрибутом **TestMethod** . В пункте меню **тест** выполните тесты.

![Запуск тестов](unit-testing-with-aspnet-web-api/_static/image11.png)

Откройте окно **обозревателя тестов** и обратите внимание на результаты тестов.

![результаты теста](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>Сводка

Учебник успешно пройден. Данные в этом учебнике были намеренно упрощены, чтобы сосредоточиться на условиях модульного тестирования. Дополнительные сведения о модульном тестировании для расширенных сценариев данных см. в разделе [макет Entity Framework при модульном тестировании веб-API ASP.NET 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).
