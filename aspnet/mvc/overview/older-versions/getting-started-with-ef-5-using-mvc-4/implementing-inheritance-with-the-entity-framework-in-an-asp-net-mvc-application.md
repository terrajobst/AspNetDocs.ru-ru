---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: Реализация наследования с помощью Entity Framework в приложении ASP.NET MVC (8 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595323"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>Реализация наследования с помощью Entity Framework в приложении ASP.NET MVC (8 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущем учебном курсе были обработаны исключения параллелизма. В этом учебнике демонстрируется, как реализовать наследование в модели данных.

В объектно-ориентированном программировании можно использовать наследование для исключения избыточного кода. В рамках этого учебника вы измените классы `Instructor` и `Student` таким образом, чтобы они были производными от базового класса `Person`, который содержит общие свойства для преподавателей и учащихся, такие как `LastName`. Изменения вносятся в коде, а не на веб-страницах, и автоматически отражаются в базе данных.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>Таблица на иерархию и наследование типа «таблица на тип»

В объектно-ориентированном программировании можно использовать наследование, чтобы упростить работу с связанными классами. Например, классы `Instructor` и `Student` в модели данных `School` совместно используют несколько свойств, что приводит к избыточному коду:

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

Предположим, что вам требуется исключить повторяющийся код для свойств, которые являются общими для сущностей `Instructor` и `Student`. Можно создать `Person` базовый класс, который содержит только общие свойства, а затем сделать сущности `Instructor` и `Student` производными от этого базового класса, как показано на следующем рисунке:

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

Структура наследования может быть представлена в базе данных несколькими способами. У вас может быть `Person` таблица, содержащая сведения о студентах и преподавателях в одной таблице. Некоторые из столбцов могут применяться только к преподавателям (`HireDate`), а только к учащимся (`EnrollmentDate`), к обеим (`LastName`, `FirstName`). Как правило, у вас должен быть столбец *дискриминатора* , указывающий, какой тип представляет каждая строка. Например, в столбце дискриминатора может указываться значение "Instructor" для преподавателей и "Student" для учащихся.

![Таблица на hierarchy_example](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

Этот шаблон создания структуры наследования сущностей из одной таблицы базы данных называется наследованием типа «одна *таблица на иерархию* ».

В качестве альтернативы можно создать базу данных, которая будет иметь приближенный к структуре наследования вид. Например, можно иметь только поля имен в таблице `Person` и иметь отдельные `Instructor` и `Student` таблицы с полями даты.

![Таблица на type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

Такая схема создания таблицы базы данных для каждого класса сущностей называется наследованием *типа «таблица на тип* » (TPT).

Шаблоны наследования, как правило, обеспечивают лучшую производительность в Entity Framework, чем шаблоны наследования TPT, так как шаблоны TPT могут привести к созданию сложных запросов JOIN. В этом учебнике демонстрируется реализация модели наследования "одна таблица на иерархию". Это можно сделать, выполнив следующие действия.

- Создайте класс `Person` и измените классы `Instructor` и `Student`, которые должны быть производными от `Person`.
- Добавление кода сопоставления модели в базу данных в класс контекста базы данных.
- Измените `InstructorID` и `StudentID` ссылки в проекте на `PersonID`.

## <a name="creating-the-person-class"></a>Создание класса Person

 Примечание. Компиляция проекта после создания следующих классов будет невозможна, пока не будут обновлены контроллеры, использующие эти классы. 

В папке *Models* создайте *Person.CS* и замените код шаблона следующим кодом:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

В *Instructor.CS*класс `Instructor` является производным от класса `Person` и удаляет поля ключа и имени. Код будет выглядеть следующим образом:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Внесите аналогичные изменения в *Student.CS*. Класс `Student` будет выглядеть, как в следующем примере:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>Добавление типа сущности Person в модель

В *SchoolContext.CS*добавьте свойство `DbSet` для `Person` типа сущности:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Это все, что требуется платформе Entity Framework для настройки наследования типа "одна таблица на иерархию". Как вы увидите, при повторном создании базы данных она будет содержать `Person`ную таблицу вместо таблиц `Student` и `Instructor`.

## <a name="changing-instructorid-and-studentid-to-personid"></a>Изменение InstructorID и StudentID на PersonID

В *SchoolContext.CS*в заявлении о сопоставлении преподавателя-Course измените `MapRightKey("InstructorID")` на `MapRightKey("PersonID")`:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

Это изменение не требуется; Он просто изменяет имя столбца InstructorID в таблице соединений «многие ко многим». Если вы оставили имя как InstructorID, приложение по-прежнему будет работать правильно. Вот завершенные *SchoolContext.CS*:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

Затем необходимо изменить `InstructorID` на `PersonID` и `StudentID` `PersonID` в течение всего проекта, ***за исключением*** файлов с временными штампами времени в папке *миграции* . Для этого можно найти и открыть только те файлы, которые необходимо изменить, а затем выполнить глобальное изменение открытых файлов. Единственный файл в папке *миграции* , который следует изменить, — это *мигратионс\конфигуратион.КС.*

1. > [!IMPORTANT]
   > Для начала закройте все открытые файлы в Visual Studio.
2. Щелкните **найти и заменить--найти все файлы** в меню **Правка** , а затем найдите все файлы в проекте, содержащие `InstructorID`.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. Откройте каждый файл в окне **Результаты поиска** , ***кроме*** отметки времени &lt;&gt; *\_CS* -файлы миграции в папке *migrations* , дважды щелкнув по одной строке для каждого файла.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. Откройте диалоговое окно **Замена в файлах** и измените **параметр искать во** **всех открытых документах**.
5. Используйте диалоговое окно **Замена в файлах** , чтобы изменить все `InstructorID` на `PersonID.`  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. Найдите все файлы в проекте, содержащие `StudentID`.
7. Откройте каждый файл в окне **Результаты поиска** , ***за исключением*** отметки времени &lt;&gt; *\_файлы миграции \*. CS* в папке *миграции* , дважды щелкнув по одной строке для каждого файла.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. Откройте диалоговое окно **Замена в файлах** и измените **параметр искать во** **всех открытых документах**.
9. Используйте диалоговое окно **Замена в файлах** , чтобы изменить все `StudentID` на `PersonID`.   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. Постройте проект.

(Обратите внимание, что это демонстрирует *недостаток* `classnameID` шаблона именования первичных ключей. Если вы использовали именованный идентификатор первичного ключа без префикса имени класса, переименование *не* потребуется.)

## <a name="create-and-update-a-migrations-file"></a>Создание и обновление файла миграции

В консоли диспетчера пакетов (PMC) введите следующую команду:

`Add-Migration Inheritance`

Выполните команду `Update-Database` в PMC. На этом этапе команда завершится ошибкой, так как у нас есть существующие данные, которые не могут быть обработаны миграцией. Появляется следующее сообщение об ошибке:

*Инструкция ALTER TABLE конфликтует с ограничением внешнего ключа "FK\_dbo. Отдел\_dbo. Пользователь\_PersonID ". Конфликт произошел в базе данных "ContosoUniversity", таблица "dbo. Person ", столбец" PersonID ".*

Откройте *миграцию\&lt; timestamp&gt;\_Inheritance.CS* и замените метод `Up` следующим кодом:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

Выполните команду `update-database` еще раз.

> [!NOTE]
> При переносе данных и внесении изменений в схему можно получить другие ошибки. Если вы получаете ошибки миграции, которые невозможно устранить, можно продолжить работу с руководством, изменив строку подключения в файле *Web. config* или удалив базу данных. Самый простой подход заключается в том, чтобы переименовать базу данных в файле *Web. config* . Например, измените имя базы данных на CU\_Test, как показано в следующем примере:
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> В новой базе данных нет данных для переноса, и выполнение команды `update-database` с большей вероятностью завершится без ошибок. Инструкции по удалению базы данных см. в статье [как удалить базу данных из Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/). Если вы пройдете этот подход, чтобы продолжить работу с руководством, пропустите шаг развертывания в конце этого руководства, так как развернутый сайт будет получать ту же ошибку при автоматическом выполнении миграции. Если вы хотите устранить ошибку миграции, лучшим ресурсом является одна из Entity Framework форумов или StackOverflow.com.

## <a name="testing"></a>Тестирование

Запустите сайт и попробуйте использовать различные страницы. Все работает так же, как и раньше.

В **Обозреватель сервера** разверните **SchoolContext** , а затем **таблицы**, и вы увидите, что таблицы **учащихся** и **преподавателей** были заменены таблицей **Person** . Раскройте таблицу **Person** , и вы увидите, что в ней есть все столбцы, используемые в таблицах **учащихся** и **инструкторов** .

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Щелкните таблицу Person правой кнопкой мыши и выберите команду **Показать данные таблицы**, чтобы просмотреть столбец дискриминатора.

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

На следующей схеме показана структура новой базы данных School:

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>Сводка

Наследование «таблица на иерархию» теперь реализовано для классов `Person`, `Student`и `Instructor`. Дополнительные сведения об этой и других структурах наследования см. в разделе [стратегии сопоставления наследования](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) в блоге Мортеза Манави. В следующем учебнике вы увидите некоторые способы реализации шаблонов репозитория и единиц работы.

Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Назад](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Вперед](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
