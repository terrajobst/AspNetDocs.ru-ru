---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4, часть 5 | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework. Пример приложения:...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78423870"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4. часть 5

от [Tom Dykstra)](https://github.com/tdykstra)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Сведения о серии руководств см. в [первом учебнике серии](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="working-with-related-data-continued"></a>Работа с связанными данными, продолжение

В предыдущем учебном курсе было начато использование элемента управления `EntityDataSource` для работы с связанными данными. В свойствах навигации отображается несколько уровней иерархии и измененных данных. В этом учебнике вы продолжите работать с связанными данными, добавив и удалив связи и добавив новую сущность, которая имеет связь с существующей сущностью.

Вы создадите страницу, которая добавляет курсы, назначенные отделам. Отделы уже существуют, и при создании нового курса одновременно устанавливается связь между ним и существующим подразделением.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

Вы также создадите страницу, которая работает со связью "многие ко многим", назначая лектора курсу (Добавление связи между двумя выбранными сущностями) или удаление лектора из курса (Удаление связи между двумя сущностями, которые вы Выберите). В базе данных Добавление связи между преподавателем и курсом приводит к добавлению новой строки в таблицу ассоциаций `CourseInstructor`. Удаление связи включает удаление строки из таблицы связей `CourseInstructor`. Однако это можно сделать в Entity Framework, установив свойства навигации, не ссылаясь на `CourseInstructor` таблицу явным образом.

[![image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>Добавление сущности с отношением к существующей сущности

Создайте новую веб-страницу с именем *каурсесадд. aspx* , которая использует главную страницу *site. master* , и добавьте следующую разметку в элемент управления `Content` с именем `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

Эта разметка создает элемент управления `EntityDataSource`, который выбирает курсы, которые позволяют вставлять и задают обработчик для события `Inserting`. Вы будете использовать обработчик для обновления свойства навигации `Department` при создании новой сущности `Course`.

Разметка также создает `DetailsView` элемент управления, используемый для добавления новых сущностей `Course`. Разметка использует привязанные поля для `Course` свойств сущности. Необходимо ввести значение `CourseID`, так как это не создаваемое системой поле идентификатора. Вместо этого указывается номер курса, который необходимо указать вручную при создании курса.

Для свойства навигации `Department` используется поле шаблона, так как свойства навигации нельзя использовать с элементами управления `BoundField`. Поле шаблона содержит раскрывающийся список для выбора отдела. Раскрывающийся список привязан к `Departments` набору сущностей с помощью `Eval`, а не `Bind`, опять же, поскольку нельзя напрямую привязывать свойства навигации для их обновления. Необходимо указать обработчик для события `Init` элемента управления `DropDownList`, чтобы можно было сохранить ссылку на элемент управления для использования в коде, который обновляет внешний ключ `DepartmentID`.

В *CoursesAdd.aspx.CS* сразу после объявления разделяемого класса добавьте поле класса для хранения ссылки на элемент управления `DepartmentsDropDownList`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

Добавьте обработчик для события `Init` элемента управления `DepartmentsDropDownList`, чтобы можно было сохранить ссылку на элемент управления. Это позволяет получить значение, введенное пользователем, и использовать его для обновления значения `DepartmentID` сущности `Course`.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

Добавьте обработчик для события `Inserting` элемента управления `DetailsView`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

Когда пользователь нажимает кнопку `Insert`, событие `Inserting` возникает перед вставкой новой записи. Код в обработчике получает `DepartmentID` из элемента управления `DropDownList` и использует его для задания значения, которое будет использоваться для свойства `DepartmentID` сущности `Course`.

Entity Framework позаботится о добавлении этого курса в свойство навигации `Courses` связанной сущности `Department`. Он также добавляет отдел к свойству навигации `Department` сущности `Course`.

Запустите страницу.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

Введите идентификатор, заголовок, число кредитов и выберите отдел, а затем нажмите кнопку **Вставить**.

Запустите страницу *Courses. aspx* и выберите тот же отдел, чтобы увидеть новый курс.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>Работа со связями «многие ко многим»

Отношение между `Courses` набором сущностей и `People`ным набором сущностей является связью «многие ко многим». Сущность `Course` имеет свойство навигации с именем `People`, которое может содержать ноль, одну или несколько связанных `Person` сущностей (представляющих инструкторов, назначенных для изучения этого курса). И сущность `Person` имеет свойство навигации с именем `Courses`, которое может содержать ноль, одну или несколько связанных `Course` сущностей (представляющих курсы, которым назначается инструктор). Один инструктор может обучать несколько курсов, и один курс может обучаться несколькими преподавателями. В этом разделе пошагового руководства вы добавите и удалите связи между `Person` и `Course` сущностями, обновив свойства навигации связанных сущностей.

Создайте новую веб-страницу с именем *инструкторскаурсес. aspx* , которая использует главную страницу *site. master* , и добавьте следующую разметку в элемент управления `Content` с именем `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

Эта разметка создает элемент управления `EntityDataSource`, который извлекает имя и `PersonID` сущностей `Person` для преподавателей. Элемент управления `DropDrownList` привязан к элементу управления `EntityDataSource`. Элемент управления `DropDownList` задает обработчик для события `DataBound`. Этот обработчик используется для привязки двух раскрывающихся списков, отображающих курсы.

Разметка также создает следующую группу элементов управления, которая будет использоваться для назначения курса выбранному инструктору.

- Элемент управления `DropDownList` для выбора курса, который нужно назначить. Этот элемент управления будет заполнен курсами, которые в настоящее время не назначены выбранному преподавателю.
- Элемент управления `Button` для запуска назначения.
- Элемент управления `Label` для вывода сообщения об ошибке в случае сбоя назначения.

Наконец, разметка также создает группу элементов управления, которые будут использоваться для удаления курса от выбранного преподавателя.

В *InstructorsCourses.aspx.CS*добавьте инструкцию using:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

Добавьте метод для заполнения двух раскрывающихся списков, в которых отображаются курсы:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

Этот код получает все курсы из набора сущностей `Courses` и получает курсы из свойства навигации `Courses` сущности `Person` для выбранного преподавателя. Затем он определяет, какие курсы назначены этому инструктору, и заполняет раскрывающиеся списки соответствующим образом.

Добавьте обработчик для события `Click` кнопки `Assign`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

Этот код получает `Person` сущность для выбранного преподавателя, получает `Course` сущность для выбранного курса и добавляет выбранный курс в свойство навигации `Courses` сущности `Person` преподавателя. Затем он сохраняет изменения в базе данных и повторно заполняет раскрывающиеся списки, чтобы результаты могли быть просмотрены немедленно.

Добавьте обработчик для события `Click` кнопки `Remove`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

Этот код получает `Person` сущность для выбранного преподавателя, получает `Course` сущность для выбранного курса и удаляет выбранный курс из свойства навигации `Courses` сущности `Person`. Затем он сохраняет изменения в базе данных и повторно заполняет раскрывающиеся списки, чтобы результаты могли быть просмотрены немедленно.

Добавьте код в метод `Page_Load`, который гарантирует, что сообщения об ошибках не видны, когда нет ошибок для отчета, и добавьте обработчики для событий `DataBound` и `SelectedIndexChanged` раскрывающегося списка инструкторов, чтобы заполнить раскрывающиеся списки курсов:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

Запустите страницу.

[![image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

Выберите лектора. Раскрывающийся список <strong>назначить курс</strong> содержит курсы, которые не изучаются преподавателем, а в раскрывающемся списке <strong>удалить курс</strong> отображаются курсы, которым лектор уже назначен. В разделе <strong>назначение курса</strong> выберите курс и нажмите кнопку <strong>назначить</strong>. Курс будет перемещен в раскрывающийся список <strong>удалить курс</strong> . Выберите курс в разделе <strong>Удаление курса</strong> и нажмите кнопку <strong>Удалить</strong><em>.</em> Курс переходит в раскрывающийся список <strong>назначить курс</strong> .

Теперь вы видели несколько способов работы с связанными данными. В следующем учебнике вы узнаете, как использовать наследование в модели данных, чтобы улучшить удобство обслуживания приложения.

> [!div class="step-by-step"]
> [Назад](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [Вперед](the-entity-framework-and-aspnet-getting-started-part-6.md)
