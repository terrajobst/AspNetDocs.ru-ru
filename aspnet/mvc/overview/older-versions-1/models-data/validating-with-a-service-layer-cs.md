---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: Проверка с помощью слоя служб (C#) | Документация Майкрософт
author: StephenWalther
description: Узнайте, как переместить логику проверки из действий контроллера в отдельный слой служб. В этом руководстве Стивен Вальтер объясняет, как это делать...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: da1a1c9cc79a452eb0d7597810e86f7bcf6cd179
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436608"
---
# <a name="validating-with-a-service-layer-c"></a>Проверка с помощью уровня службы (C#)

по [Стивен Вальтер](https://github.com/StephenWalther)

> Узнайте, как переместить логику проверки из действий контроллера в отдельный слой служб. В этом руководстве Стивен Вальтер содержит сведения о том, как можно обеспечить четкое разделение проблем, изолируя уровень службы на уровне контроллера.

Цель этого руководства — описать один метод выполнения проверки в приложении MVC ASP.NET. В этом руководстве вы узнаете, как переместить логику проверки из контроллеров в отдельный слой служб.

## <a name="separating-concerns"></a>Отделение проблем

При создании приложения ASP.NET MVC не следует размещать логику базы данных в действиях контроллера. Смешивание базы данных и логики контроллера делает приложение более сложным для обслуживания с течением времени. Рекомендуется размещать всю логику базы данных в отдельном слое репозитория.

Например, листинг 1 содержит простой репозиторий с именем Продуктрепоситори. Репозиторий продукта содержит весь код доступа к данным для приложения. В список также входит интерфейс Ипродуктрепоситори, реализованный в репозитории продуктов.

**Листинг 1 — Моделс\продуктрепоситори.КС**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

Контроллер в листинге 2 использует слой репозитория в действиях index () и Create (). Обратите внимание, что этот контроллер не содержит логику базы данных. Создание слоя репозитория позволяет поддерживать четкое разделение проблем. Контроллеры отвечают за логику управления потоком приложений, и репозиторий отвечает за логику доступа к данным.

**Листинг 2. Контроллерс\продуктконтроллер.КС**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a>Создание слоя служб

Таким образом, логика управления потоком приложения принадлежит контроллеру, а логика доступа к данным — в репозитории. В этом случае, где вы помещаете логику проверки? Одним из вариантов является размещение логики проверки на *уровне служб*.

Слой служб — это дополнительный уровень в приложении ASP.NET MVC, исправляет связь между контроллером и слоем репозитория. Слой служб содержит бизнес-логику. В частности, он содержит логику проверки.

Например, уровень службы продукта в листинге 3 имеет метод Креатепродукт (). Метод Креатепродукт () вызывает метод Валидатепродукт () для проверки нового продукта перед передачей продукта в репозиторий продукта.

**Листинг 3. Моделс\продуктсервице.КС**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

Контроллер продукта был обновлен в листинге 4 для использования слоя служб вместо слоя репозитория. Уровень контроллера взаимодействует со слоем служб. Слой служб обращается к слою репозитория. Каждый уровень имеет отдельную ответственность.

**Листинг 4. Контроллерс\продуктконтроллер.КС**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

Обратите внимание, что служба продукта создается в конструкторе контроллера продукта. При создании службы продукта словарь состояния модели передается в службу. Служба продукта использует состояние модели для передачи сообщений об ошибках проверки обратно в контроллер.

## <a name="decoupling-the-service-layer"></a>Отделение слоя служб

Не удалось изолировать уровни контроллера и службы в одном отношении. Уровни контроллера и службы взаимодействуют через состояние модели. Иными словами, уровень служб зависит от конкретной функции платформы MVC ASP.NET.

Мы хотим, чтобы уровень служб был как можно более изолирован от уровня контроллера. Теоретически, мы должны иметь возможность использовать слой служб с приложением любого типа, а не только ASP.NET приложение MVC. Например, в будущем может потребоваться построить внешний интерфейс WPF для нашего приложения. Мы должны найти способ удаления зависимости от состояния модели MVC ASP.NET из уровня служб.

В листинге 5 слой служб был обновлен так, чтобы он больше не использовал состояние модели. Вместо этого используется любой класс, реализующий интерфейс Ивалидатиондиктионари.

**Листинг 5 — Моделс\продуктсервице.КС (отделено)**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

Интерфейс Ивалидатиондиктионари определен в листинге 6. Этот простой интерфейс имеет один метод и одно свойство.

**Листинг 6. Моделс\ивалидатиондиктионари.КС**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

Класс в листинге 7 с именем класса Моделстатевраппер реализует интерфейс Ивалидатиондиктионари. Можно создать экземпляр класса Моделстатевраппер, передав в конструктор словарь состояния модели.

**Листинг 7 — Моделс\моделстатевраппер.КС**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

Наконец, обновленный контроллер в листинге 8 использует Моделстатевраппер при создании слоя служб в конструкторе.

**Листинг 8. Контроллерс\продуктконтроллер.КС**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

Использование интерфейса Ивалидатиондиктионари и класса Моделстатевраппер позволяет полностью изолировать наш уровень служб от нашего уровня контроллера. Уровень службы больше не зависит от состояния модели. Можно передать любой класс, реализующий интерфейс Ивалидатиондиктионари, в слой службы. Например, приложение WPF может реализовать интерфейс Ивалидатиондиктионари с помощью простого класса коллекции.

## <a name="summary"></a>Сводка

Цель этого учебника — обсудить один из подходов к выполнению проверки в приложении ASP.NET MVC. В этом руководстве вы узнали, как переместить всю логику проверки из контроллеров в отдельный слой служб. Вы также узнали, как изолировать слой служб от своего уровня контроллера, создав класс Моделстатевраппер.

> [!div class="step-by-step"]
> [Назад](validating-with-the-idataerrorinfo-interface-cs.md)
> [Вперед](validation-with-the-data-annotation-validators-cs.md)
