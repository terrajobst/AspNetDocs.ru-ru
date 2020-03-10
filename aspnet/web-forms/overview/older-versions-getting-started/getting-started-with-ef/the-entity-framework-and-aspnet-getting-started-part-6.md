---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4. часть 6 | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework. Пример приложения:...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 8bfbe74f90eb03ea9aab7610842ef2578e80d113
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454920"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4. часть 6

от [Tom Dykstra)](https://github.com/tdykstra)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Сведения о серии руководств см. в [первом учебнике серии](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="implementing-table-per-hierarchy-inheritance"></a>Реализация наследования типа «одна таблица на иерархию»

В предыдущем руководстве вы работали с связанными данными, добавляя и удаляя связи и добавляя новую сущность, имеющую связь с существующей сущностью. В этом учебнике демонстрируется, как реализовать наследование в модели данных.

В объектно-ориентированном программировании можно использовать наследование, чтобы упростить работу с связанными классами. Например, можно создать классы `Instructor` и `Student`, производные от базового класса `Person`. Вы можете создавать одни и те же структуры наследования между сущностями в Entity Framework.

В этой части руководства вы не создадите новые веб-страницы. Вместо этого необходимо добавить Производные сущности в модель данных и изменить существующие страницы для использования новых сущностей.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>Таблица на иерархию и наследование типа «таблица на тип»

База данных может хранить сведения о связанных объектах в одной таблице или в нескольких таблицах. Например, в `School` базе данных `Person` таблица содержит сведения о студентах и преподавателях в одной таблице. Некоторые из столбцов относятся только к преподавателям (`HireDate`), только к учащимся (`EnrollmentDate`) и к обеим (`LastName`, `FirstName`).

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

Можно настроить Entity Framework для создания сущностей `Instructor` и `Student`, которые наследуют от сущности `Person`. Этот шаблон создания структуры наследования сущностей из одной таблицы базы данных называется наследованием типа «одна *таблица на иерархию* ».

Для курсов `School` база данных использует другой шаблон. Онлайн-курсы и курсы на сайте хранятся в отдельных таблицах, каждый из которых имеет внешний ключ, указывающий на `Course` таблицу. Сведения, общие для обоих типов курсов, хранятся только в таблице `Course`.

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

Модель данных Entity Framework можно настроить таким образом, чтобы сущности `OnlineCourse` и `OnsiteCourse` наследовались от сущности `Course`. Этот шаблон создания структуры наследования сущностей из отдельных таблиц для каждого типа, при котором каждая отдельная таблица, ссылающаяся обратно на таблицу, в которой хранятся данные, общие для всех типов, называется наследованием *таблицы на тип* (TPT).

Шаблоны наследования, как правило, обеспечивают лучшую производительность в Entity Framework, чем шаблоны наследования TPT, так как шаблоны TPT могут привести к созданию сложных запросов JOIN. В этом пошаговом руководстве показано, как реализовать наследование «подтаблица». Это можно сделать, выполнив следующие действия.

- Создание `Instructor` и `Student` типов сущностей, производных от `Person`.
- Переместите свойства, относящиеся к производным сущностям из сущности `Person`, в производные сущности.
- Задайте ограничения для свойств в производных типах.
- Сделайте `Person` сущностью абстрактной сущностью.
- Сопоставьте каждую производную сущность с `Person` таблицей с условием, определяющим, как определить, представляет ли строка `Person` производный тип.

## <a name="adding-instructor-and-student-entities"></a>Добавление сущностей инструкторов и учащихся

Откройте файл <em>счулмодел. EDMX</em> , щелкните правой кнопкой мыши незанятую область в конструкторе, выберите <strong>Добавить</strong>, а затем выберите <strong>сущность</strong><em>.</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

В диалоговом окне **Добавление сущности** назовите сущность `Instructor` и присвойте параметру **базового типа** значение `Person`.

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

Нажмите кнопку **ОК**. Конструктор создает сущность `Instructor`, производную от сущности `Person`. Новая сущность еще не имеет свойств.

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

Повторите процедуру, чтобы создать сущность `Student`, которая также является производной от `Person`.

Только преподаватели имеют даты найма, поэтому необходимо переместить это свойство из сущности `Person` в сущность `Instructor`. В `Person` сущности щелкните правой кнопкой мыши свойство `HireDate` и выберите команду **Вырезать**. Затем щелкните правой кнопкой мыши **Свойства** в сущности `Instructor` и выберите команду **Вставить**.

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

Дата найма `Instructor` сущности не может быть неопределенной. Щелкните правой кнопкой мыши свойство `HireDate`, выберите пункт **Свойства**, а затем в окне **свойства** измените `Nullable` на `False`.

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

Повторите процедуру, чтобы переместить свойство `EnrollmentDate` из сущности `Person` в сущность `Student`. Убедитесь, что для свойства `EnrollmentDate` также задано значение `False` `Nullable`.

Теперь, когда сущность `Person` имеет только те свойства, которые являются общими для `Instructor` и `Student` сущностей (помимо свойств навигации, которые вы не перемещаете), сущность может использоваться только в качестве базовой сущности в структуре наследования. Поэтому необходимо убедиться, что она никогда не будет рассматриваться как независимая сущность. Щелкните правой кнопкой мыши сущность `Person`, выберите пункт **Свойства**, а затем в окне **Свойства** измените значение свойства **abstract** на **true**.

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>Сопоставление сущностей инструктора и учащихся с таблицей Person

Теперь необходимо сообщить Entity Framework, как различать `Instructor` и `Student` сущности в базе данных.

Щелкните правой кнопкой мыши сущность `Instructor` и выберите пункт **Сопоставление таблиц**. В окне **сведения о сопоставлении** щелкните **Добавить таблицу или представление** и выберите **Person**.

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

Нажмите кнопку **Добавить условие**, а затем выберите **HireDate**.

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

Измените **оператор** на **is** , а **значение или свойство** — на **NOT NULL**.

[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

Повторите процедуру для сущности `Students`, указав, что эта сущность сопоставляется с `Person` таблицей, если столбец `EnrollmentDate` не равен null. Затем сохраните и закройте модель данных.

Выполните сборку проекта, чтобы создать новые сущности в качестве классов и сделать их доступными в конструкторе.

## <a name="using-the-instructor-and-student-entities"></a>Использование сущностей преподавателей и учащихся

При создании веб-страниц, работающих с данными учащихся и преподавателей, вы привязываете их к `Person` набору сущностей и фильтруете по свойству `HireDate` или `EnrollmentDate`, чтобы ограничить возвращаемые данные студентам или преподавателям. Однако теперь при привязке каждого элемента управления источниками данных к `Person` набору сущностей можно указать, что должны быть выбраны только типы сущностей `Student` или `Instructor`. Поскольку Entity Framework знает, как отличать учащихся и преподавателей в `Person`ном наборе сущностей, вы можете удалить параметры свойства `Where`, введенные вручную.

В конструкторе Visual Studio можно указать тип сущности, который должен выбрать элемент управления `EntityDataSource` в раскрывающемся списке **EntityTypeFilter** мастера `Configure Data Source`, как показано в следующем примере.

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

Кроме того, в окне " **Свойства** " можно удалить значения `Where` предложения, которые больше не нужны, как показано в следующем примере.

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

Однако, поскольку разметка для `EntityDataSource` элементов управления была изменена для использования атрибута `ContextTypeName`, мастер **настройки источника данных** нельзя запустить в уже созданных элементах управления `EntityDataSource`. Поэтому необходимо внести необходимые изменения, изменив вместо этого разметку.

Откройте страницу *students. aspx* . В элементе управления `StudentsEntityDataSource` удалите атрибут `Where` и добавьте атрибут `EntityTypeFilter="Student"`. Теперь разметка будет выглядеть следующим образом:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

Установка атрибута `EntityTypeFilter` гарантирует, что элемент управления `EntityDataSource` выберет только указанный тип сущности. Если требуется получить как `Student`, так `Instructor` типы сущностей, этот атрибут задавать не нужно. (Можно получить несколько типов сущностей с одним `EntityDataSource` элементом управления, только если вы используете элемент управления для доступа к данным только для чтения. Если для вставки, обновления или удаления сущностей используется элемент управления `EntityDataSource`, и если набор сущностей, к которому он привязан, может содержать несколько типов, то можно работать только с одним типом сущности, и необходимо задать этот атрибут.)

Повторите процедуру для элемента управления `SearchEntityDataSource`, за исключением удаления только части атрибута `Where`, которая выбирает `Student` сущностей вместо того, чтобы полностью удалить свойство. Открывающий тег элемента управления теперь будет выглядеть следующим образом:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

Запустите страницу, чтобы убедиться, что она все еще работает, как и раньше.

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

Обновите следующие страницы, созданные в предыдущих учебных курсах, чтобы они использовали новые `Student` и `Instructor` сущности вместо сущностей `Person`, затем запустите их, чтобы убедиться, что они работают, как раньше:

- В *студентсадд. aspx*добавьте `EntityTypeFilter="Student"` в элемент управления `StudentsEntityDataSource`. Теперь разметка будет выглядеть следующим образом: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- В файле *About. aspx*добавьте `EntityTypeFilter="Student"` в элемент управления `StudentStatisticsEntityDataSource` и удалите `Where="it.EnrollmentDate is not null"`. Теперь разметка будет выглядеть следующим образом: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- В *инструкторах. aspx* и *инструкторскаурсес. aspx*добавьте `EntityTypeFilter="Instructor"` в элемент управления `InstructorsEntityDataSource` и удалите `Where="it.HireDate is not null"`. Разметка в *инструкторах. aspx* теперь напоминает следующий пример: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    Разметка в *инструкторскаурсес. aspx* теперь будет выглядеть следующим образом:

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

В результате этих изменений вы улучшили удобство обслуживания приложения Contoso университета несколькими способами. Вы переместили выборку и логику проверки из слоя пользовательского интерфейса (разметки*ASPX* ) и сделали ее неотъемлемой частью уровня доступа к данным. Это помогает изолировать код приложения от изменений, которые могут быть внесены в будущем для схемы базы данных или модели данных. Например, можно принять решение о том, что учащиеся могут быть приняты на работу в качестве вспомогательных средств преподавателей и, следовательно, получат дату найма. Затем можно добавить новое свойство, чтобы отличать учащихся от инструкторов и обновлять модель данных. Код в веб-приложении не должен изменяться, за исключением тех случаев, когда требуется отобразить дату найма для учащихся. Еще одно преимущество добавления `Instructor` и `Student` сущностей заключается в том, что код более понятен, чем когда бы он ссылался на `Person` объекты, которые фактически являются студентами или преподавателями.

Теперь вы видели один из способов реализации шаблона наследования в Entity Framework. В следующем руководстве вы узнаете, как использовать хранимые процедуры, чтобы получить более полный контроль над тем, как Entity Framework обращается к базе данных.

> [!div class="step-by-step"]
> [Назад](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [Вперед](the-entity-framework-and-aspnet-getting-started-part-7.md)
