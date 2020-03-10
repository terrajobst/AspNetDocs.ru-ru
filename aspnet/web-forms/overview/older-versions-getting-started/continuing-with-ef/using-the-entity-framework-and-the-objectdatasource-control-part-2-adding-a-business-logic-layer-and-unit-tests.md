---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: С помощью Entity Framework 4,0 и элемента управления ObjectDataSource, часть 2. Добавление уровня бизнес-логики и модульных тестов | Документация Майкрософт
author: tdykstra
description: Эта серия руководств основана на веб-приложении университета Contoso, которое создается начало работы с руководством по Entity Framework 4,0. Он...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 24344cc33d7c26d7c408db26c0530ef2c708a7d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439956"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>Использование Entity Framework 4,0 и элемента управления ObjectDataSource, часть 2. Добавление уровня бизнес-логики и модульных тестов

от [Tom Dykstra)](https://github.com/tdykstra)

> Эта серия руководств основана на веб-приложении университета Contoso, которое создается [Начало работы с руководством по Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) . Если вы не выполнили предыдущие учебники, в качестве отправной точки для этого учебника вы можете скачать созданное [приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Вы также можете [скачать приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , созданное с помощью полной серии руководств. Если у вас есть вопросы о учебниках, их можно опубликовать на [форуме ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).

В предыдущем учебном курсе было создано n-уровневое веб-приложение с помощью Entity Framework и элемента управления `ObjectDataSource`. В этом учебнике показано, как добавить бизнес-логику, разделив уровень бизнес-логики (BLL) и уровень доступа к данным (DAL), и покажет, как создавать автоматические модульные тесты для слоя BLL.

В этом учебнике вы выполните следующие задачи:

- Создайте интерфейс репозитория, объявляющий необходимые методы доступа к данным.
- Реализуйте интерфейс репозитория в классе репозитория.
- Создайте класс бизнес-логики, который вызывает класс репозитория для выполнения функций доступа к данным.
- Подключите элемент управления `ObjectDataSource` к классу бизнес-логики, а не к классу репозитория.
- Создайте проект модульного теста и класс репозитория, который использует коллекции в памяти для своего хранилища данных.
- Создайте модульный тест для бизнес-логики, которую необходимо добавить к классу Business Logic, а затем запустите тест и посмотрите на ошибку.
- Реализуйте бизнес-логику в классе логики бизнеса, а затем повторно запустите модульный тест и посмотрите на него.

Вы будете работать с страницами *Departments. aspx* и *департментсадд. aspx* , созданными в предыдущем руководстве.

## <a name="creating-a-repository-interface"></a>Создание интерфейса репозитория

Начнем с создания интерфейса репозитория.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

В папке *DAL* создайте новый файл класса, назовите его *ISchoolRepository.CS*и замените существующий код следующим кодом:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

Интерфейс определяет один метод для каждого метода CRUD (создание, чтение, обновление, удаление), созданного в классе репозитория.

В классе `SchoolRepository` в *SchoolRepository.CS*укажите, что этот класс реализует интерфейс `ISchoolRepository`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>Создание класса бизнес-логики

Далее предстоит создать класс бизнес-логики. Это можно сделать, чтобы добавить бизнес-логику, которая будет выполняться элементом управления `ObjectDataSource`, хотя это пока не будет сделано. Сейчас новый класс бизнес-логики будет выполнять те же операции CRUD, что и репозиторий.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

Создайте новую папку и назовите ее *BLL*. (В реальном приложении уровень бизнес-логики обычно реализуется как библиотека классов — отдельный проект, но для упрощения этого учебника классы BLL будут храниться в папке проекта.)

В папке *BLL* создайте новый файл класса, назовите его *SchoolBL.CS*и замените существующий код следующим кодом:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

Этот код создает те же методы CRUD, которые вы видели ранее в классе репозитория, но вместо доступа к методам Entity Framework напрямую он вызывает методы класса репозитория.

Переменная класса, содержащая ссылку на класс репозитория, определяется как тип интерфейса, а код, который создает экземпляр класса репозитория, содержится в двух конструкторах. Конструктор без параметров будет использоваться элементом управления `ObjectDataSource`. Он создает экземпляр класса `SchoolRepository`, который был создан ранее. Другой конструктор позволяет любому коду, который создает класс бизнес-логики, передавать любой объект, реализующий интерфейс репозитория.

Методы CRUD, которые вызывают класс репозитория и два конструктора, позволяют использовать класс бизнес-логики с любым выбранным внутренним хранилищем данных. Классу бизнес-логики не нужно знать, как класс, который он вызывает, сохраняет данные. (Это часто называется *сохраняемостью игнорирования*.) Это упрощает модульное тестирование, так как вы можете подключить класс бизнес-логики к реализации репозитория, которая использует что-то простое, как `List` коллекции в памяти для хранения данных.

> [!NOTE]
> Технически объекты сущностей по-прежнему не поддерживают сохранение — игнорирующих, так как они создаются из классов, наследующих от класса `EntityObject` Entity Framework. Для полного сохранения игнорирования можно использовать *простые старые объекты CLR*или *POCO*вместо объектов, которые наследуются от класса `EntityObject`. Использование POCO выходит за рамки данного учебника. Дополнительные сведения см. в разделе [пригодность для тестирования и Entity Framework 4,0](https://msdn.microsoft.com/library/ff714955.aspx) на веб-сайте MSDN.)

Теперь можно подключить элементы управления `ObjectDataSource` к классу бизнес-логики, а не к репозиторию и убедиться, что все работает как раньше.

В *Departments. aspx* и *департментсадд. aspx*измените каждое вхождение `TypeName="ContosoUniversity.DAL.SchoolRepository"` на `TypeName="ContosoUniversity.BLL.SchoolBL`". (Существует четыре экземпляра.)

Запустите страницы *Departments. aspx* и *департментсадд. aspx* , чтобы убедиться, что они все еще работают, как и раньше.

[![image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>Создание проекта модульных тестов и реализация репозитория

Добавьте новый проект в решение с помощью шаблона **тестового проекта** и назовите его `ContosoUniversity.Tests`.

В тестовом проекте добавьте ссылку на `System.Data.Entity` и добавьте ссылку на проект `ContosoUniversity`.

Теперь можно создать класс репозитория, который будет использоваться с модульными тестами. Хранилище данных для этого репозитория будет находиться в пределах класса.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

В тестовом проекте создайте новый файл класса, назовите его *MockSchoolRepository.CS*и замените существующий код следующим кодом:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

Этот класс репозитория имеет те же методы CRUD, что и тот, который обращается к Entity Framework напрямую, но они работают с `List` коллекциями в памяти, а не с базой данных. Это упрощает для тестового класса настройку и проверку модульных тестов для класса бизнес-логики.

## <a name="creating-unit-tests"></a>Создание модульных тестов

Шаблон **тестового** проекта создал класс модульного теста-заглушки, и ваша следующая задача — изменить этот класс, добавив в него методы модульного теста для бизнес-логики, которую необходимо добавить в класс Business Logic.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

В университете Contoso любой отдельный инструктор может быть только администратором одного отдела, и вам нужно добавить бизнес-логику для применения этого правила. Вы начнете с добавления тестов и выполнения тестов, чтобы увидеть их сбой. Затем вы добавите код и перезапустите тесты, ожидающие проверки.

Откройте файл *UnitTest1.CS* и добавьте инструкции `using` для уровней бизнес-логики и доступа к данным, созданных в проекте ContosoUniversity:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

Замените метод `TestMethod1` следующими методами:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

Метод `CreateSchoolBL` создает экземпляр класса репозитория, созданный для проекта модульного теста, который затем передается в новый экземпляр класса бизнес-логики. Затем метод использует класс бизнес-логики для вставки трех отделов, которые можно использовать в методах теста.

Методы теста проверяют, что класс бизнес-логики создает исключение, если кто-то пытается вставить новый отдел с тем же администратором, что и существующий отдел, или если кто-то пытается обновить администратора отдела, указав для него идентификатор человека. кто уже является администратором другого отдела.

Вы еще не создали класс Exception, поэтому этот код не будет компилироваться. Чтобы скомпилировать его, щелкните правой кнопкой мыши `DuplicateAdministratorException` и выберите **создать**, а затем — **класс**.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

Будет создан класс в тестовом проекте, который можно удалить после создания класса Exception в основном проекте. и реализовали бизнес-логику.

Запустите тестовый проект. Как и ожидалось, тесты завершаются ошибкой.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>Добавление бизнес-логики для выполнения теста

Далее вы реализуете бизнес-логику, которая делает невозможным задание в качестве администратора отдела, который уже является администратором другого отдела. Исключение создается на уровне бизнес-логики, а затем перехватывается на уровне представления, если пользователь редактирует отдел и нажимает кнопку **Обновить** после выбора пользователя, который уже является администратором. (Преподаватели можно также удалить из раскрывающегося списка, который уже является администратором, прежде чем визуализировать страницу, но цель этой задачи — работать с уровнем бизнес-логики.)

Начните с создания класса исключений, который будет создаваться, когда пользователь пытается сделать лектора администратором нескольких отделов. В основном проекте создайте новый файл класса в папке *BLL* , назовите его *DuplicateAdministratorException.CS*и замените существующий код следующим кодом:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

Теперь удалите временный файл *DuplicateAdministratorException.CS* , созданный в тестовом проекте ранее, чтобы иметь возможность компилировать.

В основном проекте откройте файл *SchoolBL.CS* и добавьте следующий метод, содержащий логику проверки. (Код ссылается на метод, который вы создадите позже.)

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

Этот метод вызывается при вставке или обновлении сущностей `Department`, чтобы проверить, имеет ли другой отдел тот же администратор.

Код вызывает метод для поиска в базе данных `Department` сущности, которая имеет то же значение `Administrator` свойства, что и сущность, вставляемую или обновляемую. Если он найден, код создает исключение. Проверка не требуется, если вставляемая или обновляемая сущность не имеет `Administrator` значения, и исключение не создается, если метод вызывается во время обновления, а найденная сущность `Department` соответствует обновляемой сущности `Department`.

Вызовите новый метод из методов `Insert` и `Update`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

В *ISchoolRepository.CS*добавьте следующее объявление для нового метода доступа к данным:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

В *SchoolRepository.CS*добавьте следующую инструкцию `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

В *SchoolRepository.CS*добавьте следующий новый метод доступа к данным:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

Этот код извлекает `Department` сущности с указанным администратором. Должен быть найден только один отдел (если таковой имеется). Однако, поскольку в базе данных не встроено ограничение, тип возвращаемого значения — это коллекция в случае, если найдено несколько отделов.

По умолчанию, когда контекст объекта получает сущности из базы данных, он отслеживает их в диспетчере состояний объектов. Параметр `MergeOption.NoTracking` указывает, что это отслеживание не будет выполняться для этого запроса. Это необходимо, поскольку запрос может вернуть точную сущность, которую вы пытаетесь обновить, а затем вы не сможете присоединить эту сущность. Например, если изменить отдел журнала на странице *Departments. aspx* и оставить администратора без изменений, этот запрос вернет сведения о штатном отделе. Если `NoTracking` не задано, контекст объекта уже будет иметь сущность «журнал отделов» в диспетчере состояний объектов. Затем, когда вы подключаете сущность в виде журнала, созданную повторно из состояния представления, контекст объекта вызовет исключение, которое говорит `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`.

(В качестве альтернативы указанию `MergeOption.NoTracking`можно создать новый контекст объекта только для этого запроса. Поскольку новый контекст объекта будет иметь собственный диспетчер состояний объектов, конфликт при вызове метода `Attach` будет отсутствовать. Новый контекст объекта будет совместно использовать метаданные и подключение к базе данных с исходным контекстом объекта, поэтому снижение производительности этого альтернативного подхода будет минимальным. При этом подходе, показанном здесь, введен параметр `NoTracking`, который можно использовать в других контекстах. Параметр `NoTracking` обсуждается далее в последующем учебнике этой серии.)

В тестовом проекте добавьте новый метод доступа к данным в *MockSchoolRepository.CS*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

Этот код использует LINQ для выполнения того же выбора данных, который `ContosoUniversity` репозитории проекта использует LINQ to Entities для.

Снова запустите тестовый проект. Результат на этот раз положительный.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>Обработка исключений ObjectDataSource

В проекте `ContosoUniversity` запустите страницу *departmentss. aspx* и попытайтесь изменить администратора отдела на того, кто уже является администратором другого отдела. (Помните, что вы можете изменять только те отделы, которые были добавлены в этом руководстве, так как база данных предварительно загружена с недопустимыми данными.) Появится следующая страница ошибки сервера:

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

Пользователи не должны видеть эту страницу ошибки, поэтому необходимо добавить код обработки ошибок. Откройте элемент *departmentss. aspx* и укажите обработчик для события `OnUpdated` `DepartmentsObjectDataSource`. Открывающий тег `ObjectDataSource` теперь напоминает следующий пример.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

В *Departments.aspx.CS*добавьте следующую инструкцию `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

Добавьте следующий обработчик для события `Updated`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

Если `ObjectDataSource` элемент управления перехватывает исключение при попытке выполнить обновление, оно передает исключение в аргументе события (`e`) в этот обработчик. Код в обработчике проверяет, является ли исключение дублирующим исключением администратора. Если это так, код создает проверяющий элемент управления, который содержит сообщение об ошибке для отображаемого элемента управления `ValidationSummary`.

Запустите страницу и попытайтесь сделать администратора двух отделов еще раз. На этот раз элемент управления `ValidationSummary` отображает сообщение об ошибке.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

Внесите аналогичные изменения на странице *департментсадд. aspx* . В *департментсадд. aspx*укажите обработчик для события `OnInserted` `DepartmentsObjectDataSource`. Полученная разметка будет выглядеть примерно так:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

В *DepartmentsAdd.aspx.CS*Добавьте ту же инструкцию `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

Добавьте следующий обработчик событий:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

Теперь можно протестировать страницу *DepartmentsAdd.aspx.CS* , чтобы убедиться, что она также правильно обрабатывает попытки сделать одного пользователя администратором более одного отдела.

Это завершает вводные сведения о реализации шаблона репозитория для использования элемента управления `ObjectDataSource` с Entity Framework. Дополнительные сведения о шаблоне репозитория и пригодности для тестирования см. в техническом документе MSDN [testing и Entity Framework 4,0](https://msdn.microsoft.com/library/ff714955.aspx).

В следующем учебнике вы узнаете, как добавить в приложение функции сортировки и фильтрации.

> [!div class="step-by-step"]
> [Назад](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [Вперед](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
