---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: Создание модульных тестов для ASP.NET приложений MVCC#() | Документация Майкрософт
author: StephenWalther
description: Узнайте, как создавать модульные тесты для действий контроллера. В этом руководстве Стивен Вальтер демонстрирует, как проверить, возвращает ли действие контроллера парти...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506094"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a>Создание модульных тестов для приложений ASP.NET MVC (C#)

по [Стивен Вальтер](https://github.com/StephenWalther)

[Скачать в формате PDF](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> Узнайте, как создавать модульные тесты для действий контроллера. В этом руководстве Стивен Вальтер демонстрирует, как проверить, возвращает ли действие контроллера определенное представление, возвращает определенный набор данных или возвращает другой тип результата действия.

Цель этого руководства — продемонстрировать, как можно написать модульные тесты для контроллеров в приложениях ASP.NET MVC. Мы обсудим, как создать три различных типа модульных тестов. Вы узнаете, как протестировать представление, возвращенное действием контроллера, как проверить данные представления, возвращаемые действием контроллера, и как проверить, выполняет ли одно действие контроллера перенаправление к действию второго контроллера.

## <a name="creating-the-controller-under-test"></a>Создание тестируемого контроллера

Начнем с создания контроллера, который мы планируем тестировать. Контроллер с именем `ProductController`содержится в листинге 1.

**Листинг 1 — `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

`ProductController` содержит два метода действия с именами `Index()` и `Details()`. Оба метода действия возвращают представление. Обратите внимание, что действие `Details()` принимает параметр с именем ID.

## <a name="testing-the-view-returned-by-a-controller"></a>Тестирование представления, возвращенного контроллером

Представьте, что мы хотим проверить, возвращает ли `ProductController` правильное представление. Мы хотим убедиться, что при вызове действия `ProductController.Details()` возвращается подробное представление. Тестовый класс в листинге 2 содержит модульный тест для проверки представления, возвращаемого действием `ProductController.Details()`.

**Листинг 2 — `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

Класс в листинге 2 содержит метод теста с именем `TestDetailsView()`. Этот метод содержит три строки кода. В первой строке кода создается новый экземпляр класса `ProductController`. Вторая строка кода вызывает метод действия `Details()` контроллера. Наконец, последняя строка кода проверяет, является ли представление, возвращаемое действием `Details()`, представлением подробностей.

Свойство `ViewResult.ViewName` представляет имя представления, возвращаемого контроллером. Одно большое предупреждение о тестировании этого свойства. Контроллер может вернуть представление двумя способами. Контроллер может явно вернуть представление следующим образом:

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

Кроме того, имя представления можно вывести из имени действия контроллера следующим образом:

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

Это действие контроллера также возвращает представление с именем `Details`. Однако имя представления выводится из имени действия. Если требуется проверить имя представления, необходимо явно вернуть имя представления из действия контроллера.

Модульный тест можно запустить в листинге 2, введя сочетание клавиш **CTRL + R, A** или нажав кнопку **запустить все тесты в решении** (см. рис. 1). Если тест пройден, вы увидите результаты теста окно на рис. 2.

[![выполнить все тесты в решении](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

**Рис. 01**. выполнение всех тестов в решении ([щелкните, чтобы просмотреть изображение с полным размером](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))

[![успешно.](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

**Рис. 02**. успешное завершение! ([Щелкните, чтобы просмотреть изображение с полным размером](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))

## <a name="testing-the-view-data-returned-by-a-controller"></a>Тестирование данных представления, возвращенных контроллером

Контроллер MVC передает данные в представление, используя нечто, именуемое *`View Data`* . Например, представьте, что необходимо отобразить сведения о конкретном продукте при вызове действия `ProductController Details()`. В этом случае можно создать экземпляр класса `Product` (определенный в модели) и передать его в представление `Details`, используя преимущества `View Data`.

Измененная `ProductController` в листинге 3 включает обновленное `Details()` действие, возвращающее продукт.

**Листинг 3 — `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

Во-первых, `Details()` действие создает новый экземпляр класса `Product`, представляющий портативный компьютер. Затем экземпляр класса `Product` передается в качестве второго параметра методу `View()`.

Модульные тесты можно создавать для проверки того, содержатся ли ожидаемые данные в данных представления. Модульный тест в листинге 4 проверяет, возвращается ли продукт, представляющий портативный компьютер, при вызове метода действия `ProductController Details()`.

**Листинг 4 — `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

В листинге 4 метод `TestDetailsView()` проверяет возвращаемые данные представления, вызывая метод `Details()`. `ViewData` предоставляется как свойство на `ViewResult`, возвращаемое путем вызова метода `Details()`. Свойство `ViewData.Model` содержит продукт, переданный в представление. Тест просто проверяет наличие имени ноутбука в продукте, содержащемся в данных представления.

## <a name="testing-the-action-result-returned-by-a-controller"></a>Проверка результата действия, возвращенного контроллером

Более сложное действие контроллера может возвращать различные типы результатов действий в зависимости от значений параметров, переданных в действие контроллера. Действие контроллера может возвращать разнообразные типы результатов действий, включая `ViewResult`, `RedirectToRouteResult`или `JsonResult`.

Например, измененное действие `Details()` в листинге 5 возвращает представление `Details` при передаче действительного идентификатора продукта в действие. Если передать недопустимый идентификатор продукта — идентификатор со значением меньше 1, вы будете перенаправлены к действию `Index()`.

**Листинг 5 — `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

Поведение `Details()` действия можно проверить с помощью модульного теста в листинге 6. Модульный тест в листинге 6 проверяет, что вы перенаправлены в представление `Index`, когда в метод `Details()` передается идентификатор со значением-1.

**Листинг 6 — `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

При вызове метода `RedirectToAction()` в действии контроллера действие контроллера возвращает `RedirectToRouteResult`. Тест проверяет, будет ли `RedirectToRouteResult` перенаправлять пользователя в действие контроллера с именем `Index`.

## <a name="summary"></a>Сводка

В этом руководстве вы узнали, как создавать модульные тесты для действий контроллера MVC. Во-первых, вы узнали, как проверить, возвращено ли правильное представление действием контроллера. Вы узнали, как использовать свойство `ViewResult.ViewName` для проверки имени представления.

Далее мы рассмотрели, как можно протестировать содержимое `View Data`. Вы узнали, как проверить, был ли правильный продукт возвращен в `View Data` после вызова действия контроллера.

Наконец, мы рассмотрели, как можно проверить, возвращаются ли различные типы результатов действий из действия контроллера. Вы узнали, как проверить, возвращает ли контроллер `ViewResult` или `RedirectToRouteResult`.

> [!div class="step-by-step"]
> [Дальше](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
