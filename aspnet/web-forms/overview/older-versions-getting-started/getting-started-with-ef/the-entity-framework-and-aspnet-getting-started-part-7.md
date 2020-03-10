---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Начало работы с Entity Framework 4,0 Database First и ASP.NET 4 Web Forms, часть 7 | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework. Пример приложения:...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78488526"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>Начало работы с Entity Framework 4,0 Database First и ASP.NET 4 Web Forms, часть 7

от [Tom Dykstra)](https://github.com/tdykstra)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Сведения о серии руководств см. в [первом учебнике серии](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="using-stored-procedures"></a>Использование хранимых процедур

В предыдущем руководстве был реализован шаблон наследования «таблица на иерархию». В этом учебнике показано, как использовать хранимые процедуры для повышения управляемости доступа к базе данных.

Entity Framework позволяет указать, что для доступа к базе данных следует использовать хранимые процедуры. Для любого типа сущности можно указать хранимую процедуру, которая будет использоваться для создания, обновления или удаления сущностей этого типа. Затем в модели данных можно добавить ссылки на хранимые процедуры, которые можно использовать для выполнения таких задач, как получение наборов сущностей.

Использование хранимых процедур является общим требованием для доступа к базе данных. В некоторых случаях администратор базы данных может потребовать, чтобы весь доступ к базе данных пройдет через хранимые процедуры по соображениям безопасности. В других случаях может потребоваться создать бизнес-логику в некоторых процессах, которые Entity Framework использует при обновлении базы данных. Например, при удалении сущности может потребоваться скопировать ее в архивную базу данных. Или при обновлении строки может потребоваться записать строку в таблицу журнала, в которой записывается, кто внес изменения. Эти виды задач можно выполнять в хранимой процедуре, которая вызывается каждый раз, когда Entity Framework удаляет сущность или обновляет сущность.

Как и в предыдущем учебнике, новые страницы создаваться не будут. Вместо этого вы измените способ, которым Entity Framework будет получать доступ к базе данных для некоторых уже созданных страниц.

В этом учебнике вы создадите в базе данных хранимые процедуры для вставки `Student` и `Instructor` сущностей. Вы добавите их в модель данных, и вы укажете, что Entity Framework должны использовать их для добавления `Student` и `Instructor` сущностей в базу данных. Вы также создадите хранимую процедуру, которую можно использовать для получения сущностей `Course`.

## <a name="creating-stored-procedures-in-the-database"></a>Создание хранимых процедур в базе данных

(Если вы используете файл *School. mdf* из проекта, доступного для загрузки в этом руководстве, этот раздел можно пропустить, так как хранимые процедуры уже существуют.)

В **Обозреватель сервера**разверните *School. mdf*, щелкните правой кнопкой мыши **хранимые процедуры**и выберите команду **Добавить новую хранимую процедуру**.

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

Скопируйте следующие инструкции SQL и вставьте их в окно хранимой процедуры, заменив скелет хранимой процедуры.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` сущности имеют четыре свойства: `PersonID`, `LastName`, `FirstName`и `EnrollmentDate`. База данных автоматически создает значение идентификатора, а хранимая процедура принимает параметры для других трех. Хранимая процедура возвращает значение ключа записи новой строки, чтобы Entity Framework можно было отследить это в версии сущности, которая хранится в памяти.

Сохраните и закройте окно хранимой процедуры.

Создайте `InsertInstructor` хранимую процедуру таким же образом, используя следующие инструкции SQL:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

Также создайте `Update` хранимые процедуры для сущностей `Student` и `Instructor`. (В базе данных уже имеется `DeletePerson` хранимая процедура, которая будет работать как в `Instructor`, так и в `Student` сущностях.)

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

В этом учебнике будут сопоставлены все три функции — INSERT, Update и DELETE — для каждого типа сущности. Entity Framework версии 4 позволяет сопоставить одну или две из этих функций с хранимыми процедурами без сопоставления с другими, за одним исключением: Если функция Update сопоставлена, но не функция DELETE, Entity Framework выдаст исключение при попытка удаления сущности. В Entity Framework версии 3,5 Эта возможность не была настолько гибкой при сопоставлении хранимых процедур. Если сопоставлена одна функция, необходимо сопоставить все три.

Чтобы создать хранимую процедуру, которая считывает, а не обновляет данные, создайте ее, выбирающую все `Course` сущности, используя следующие инструкции SQL:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>Добавление хранимых процедур в модель данных

Теперь хранимые процедуры определены в базе данных, но они должны быть добавлены в модель данных, чтобы сделать их доступными для Entity Framework. Откройте *счулмодел. EDMX*, щелкните правой кнопкой мыши область конструктора и выберите пункт **Обновить модель из базы данных**. На вкладке **Добавить** в диалоговом окне **Выбор объектов базы данных** разверните узел **хранимые процедуры**, выберите вновь созданные хранимые процедуры и `DeletePerson` хранимую процедуру, а затем нажмите кнопку **Готово**.

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>Сопоставление хранимых процедур

В конструкторе моделей данных щелкните сущность `Student` правой кнопкой мыши и выберите пункт **сопоставление хранимых процедур**.

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

Откроется окно **сведения о сопоставлении** , в котором можно указать хранимые процедуры, которые Entity Framework должны использовать для вставки, обновления и удаления сущностей этого типа.

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

Установите для функции **INSERT** значение **инсертстудент**. В окне отображается список параметров хранимой процедуры, каждый из которых должен быть сопоставлен со свойством сущности. Две из них сопоставляются автоматически, так как имена совпадают. Отсутствует свойство сущности с именем `FirstName`, поэтому необходимо вручную выбрать `FirstMidName` из раскрывающегося списка, в котором будут показаны доступные свойства сущности. (Это связано с тем, что имя свойства `FirstName` было изменено на `FirstMidName` в первом учебнике.)

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

В том же окне " **сведения о сопоставлении** " сопоставьте функцию `Update` с хранимой процедурой `UpdateStudent` (убедитесь, что вы указали `FirstMidName` в качестве значения параметра для `FirstName`, как это было сделано для хранимой процедуры `Insert`) и функции `Delete` в хранимой процедуре `DeletePerson`.

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

Выполните ту же процедуру, чтобы связать хранимые процедуры вставки, обновления и удаления для инструкторов с сущностью `Instructor`.

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

Для хранимых процедур, которые считывают, а не обновляют данные, используйте окно **обозревателя моделей** , чтобы связать хранимую процедуру с возвращаемым типом сущности. В конструкторе моделей данных щелкните правой кнопкой мыши область конструктора и выберите пункт **Обозреватель моделей**. Откройте узел **счулмодел. Store** , а затем откройте узел **хранимые процедуры** . Затем щелкните правой кнопкой мыши хранимую процедуру `GetCourses` и выберите команду **Добавить импорт функции**.

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

В диалоговом окне **Добавление импорта функции** в разделе **возвращает коллекцию** выбранных **сущностей**, а затем выберите `Course` в качестве возвращаемого типа сущности. Закончив, нажмите кнопку **OK**. Сохраните файл *EDMX* и закройте его.

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>Использование хранимых процедур INSERT, Update и DELETE

Хранимые процедуры для вставки, обновления и удаления данных используются Entity Framework автоматически после добавления их в модель данных и их сопоставления с соответствующими сущностями. Теперь можно запустить страницу *студентсадд. aspx* и каждый раз при создании учащегося, Entity Framework будет использовать хранимую процедуру `InsertStudent` для добавления новой строки в таблицу `Student`.

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

Запустите страницу *students. aspx* , и в списке появится новый учащийся.

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

Измените имя, чтобы убедиться, что функция Update работает, а затем удалите учащуюся, чтобы убедиться, что функция удаления работает.

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>Использование хранимых процедур SELECT

Entity Framework не выполняет автоматически хранимые процедуры, такие как `GetCourses`, и их нельзя использовать с элементом управления `EntityDataSource`. Чтобы использовать их, их следует вызывать из кода.

Откройте файл *InstructorsCourses.aspx.CS* . Метод `PopulateDropDownLists` использует запрос LINQ-to-Entities для получения всех сущностей Course, чтобы он мог пройти по списку и определить, к каким из них назначен лектор и какие из них не назначены:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

Введите здесь следующий код:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

Теперь страница использует хранимую процедуру `GetCourses` для получения списка всех курсов. Запустите страницу, чтобы убедиться, что она работает, как и раньше.

(Свойства навигации сущностей, извлекаемых хранимой процедурой, могут не быть автоматически заполнены данными, относящимися к этим сущностям, в зависимости от параметров `ObjectContext` по умолчанию. Дополнительные сведения см. в разделе [Загрузка связанных объектов](https://msdn.microsoft.com/library/bb896272.aspx) в библиотеке MSDN.)

В следующем руководстве вы узнаете, как использовать функции платформа динамических данных, чтобы упростить программирование и тестирование правил форматирования и проверки данных. Вместо того чтобы задавать для каждого правила веб-страницы, такие как строки формата данных и указывать, является ли поле обязательным, можно указать такие правила в метаданных модели данных, и они будут автоматически применены на каждой странице.

> [!div class="step-by-step"]
> [Назад](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [Вперед](the-entity-framework-and-aspnet-getting-started-part-8.md)
