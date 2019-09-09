---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: Учебник. Создание более сложной модели данных для приложения ASP.NET MVC
author: tdykstra
description: В этом учебнике вы добавите больше сущностей и связей и настроите модель данных, указав правила форматирования, проверки и сопоставления базы данных.
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 46f7f3c9-274f-4649-811d-92222a9b27e2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 933354b09eb4674e6f523f8a65816410521f026f
ms.sourcegitcommit: aa3c2efd56466fc6bdc387ee01ad6f50a261665b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/26/2019
ms.locfileid: "70020993"
---
# <a name="tutorial-create-a-more-complex-data-model-for-an-aspnet-mvc-app"></a>Учебник. Создание более сложной модели данных для приложения ASP.NET MVC

В предыдущих руководствах вы работали с простой моделью данных, состоящей из трех сущностей. В этом учебнике вы добавите дополнительные сущности и связи и настроите модель данных, указав правила форматирования, проверки и сопоставления базы данных. В этой статье описаны два способа настройки модели данных: путем добавления атрибутов в классы сущностей и добавления кода в класс контекста базы данных.

По завершении работы классы сущностей сформируют готовую модель данных, приведенную на следующем рисунке:

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Настройка модели данных
> * Обновить сущность Student
> * Создание сущности Instructor
> * Создание сущности OfficeAssignment
> * Изменение сущности курса
> * Создание сущности Department
> * Изменение сущности Enrollment
> * Добавить код в контекст базы данных
> * Начальное заполнение базы данных тестовыми данными
> * Добавление миграции
> * Обновление базы данных

## <a name="prerequisites"></a>Предварительные требования

* [Code First миграций и развертывание](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-the-data-model"></a>Настройка модели данных

В этом разделе вы узнаете, как настроить модель данных с помощью атрибутов, которые указывают правила форматирования, проверки и сопоставления базы данных. Затем в нескольких следующих разделах вы создадите полную `School` модель данных, добавив атрибуты в уже созданные классы и создав новые классы для остальных типов сущностей в модели.

### <a name="the-datatype-attribute"></a>Атрибут DataType

Сейчас для дат зачисления студентов учащихся все веб-страницы отображают время и дату, хотя для этого поля достаточно одной даты. Используя атрибуты заметок к данным, вы можете внести в код одно изменение, позволяющее исправить формат отображения в каждом представлении, где отображаются эти данные. Чтобы рассмотреть соответствующий пример, вы добавите атрибут в свойство `EnrollmentDate` класса `Student`.

В *моделс\студент.КС*добавьте `using` инструкцию для `System.ComponentModel.DataAnnotations` `DataType` пространстваимен`DisplayFormat` и добавьте к свойствуатрибутыи,какпоказановследующемпримере:`EnrollmentDate`

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,12-13)]

Атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) используется для указания более конкретного типа данных, чем внутренний тип базы данных. В этом случае требуется отслеживать только дату, а не дату и время. [Перечисление DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) предоставляет множество типов данных, таких как *Date, Time, PhoneNumber, Currency, EmailAddress* и др. Атрибут `DataType` также обеспечивает автоматическое предоставление функций для определенных типов в приложении. Например `mailto:` , можно создать ссылку для [DataType. EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), а также можно указать средство выбора даты для [типа данных. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) в браузерах, поддерживающих [HTML5](http://html5.org/). Атрибуты [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) создают атрибуты HTML 5 [Data-](http://ejohn.org/blog/html-5-data-attributes/) (произносит *штрих данных*), которые могут быть понятны браузерам HTML 5. Атрибуты [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) не обеспечивают никакой проверки.

`DataType.Date` не задает формат отображаемой даты. По умолчанию поле данных отображается в соответствии с форматами по умолчанию, основанными на [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)сервера.

С помощью атрибута `DisplayFormat` можно явно указать формат даты:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

`ApplyFormatInEditMode` Параметр указывает, что указанное форматирование также должно применяться при отображении значения в текстовом поле для редактирования. (Для некоторых полей, например для денежных значений, может потребоваться не использовать символ валюты в текстовом поле для редактирования.)

Атрибут [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) можно использовать отдельно, но обычно рекомендуется использовать атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) . Атрибут передает *семантику* данных, в отличие от того, как она отображается на экране, и предоставляет следующие преимущества, которые не получаются `DisplayFormat`. `DataType`

- Поддержка функций HTML5 в браузере (отображение элемента управления календарем, соответствующего языковому стандарту символа валюты, ссылок электронной почты, проверки на стороне клиента и т. д.).
- По умолчанию браузер будет отображать данные с использованием правильного формата в зависимости от [языкового стандарта](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).
- Атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) может включать MVC для выбора правильного шаблона поля для отрисовки данных ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) использует строковый шаблон). Дополнительные сведения см. в статье о [шаблонах ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)Михаил Уилсон (. (Хотя написано для MVC 2, эта статья по-прежнему применяется к текущей версии ASP.NET MVC.)

При использовании `DataType` атрибута с полем даты необходимо также `DisplayFormat` указать атрибут, чтобы обеспечить правильное отображение поля в браузерах Chrome. Дополнительные сведения см. в [этом потоке StackOverflow](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).

Дополнительные сведения об обработке других форматов даты в MVC см. в статье Введение в [MVC 5: Изучение методов изменения и представления](../introduction/examining-the-edit-methods-and-edit-view.md) редактирования и поиск на странице для &quot;интернационализации&quot;.

Снова запустите страницу индекса учащихся и обратите внимание, что время для дат регистрации больше не отображается. То же самое будет справедливо для любого представления, использующего `Student` модель.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>Стрингленгсаттрибуте

С помощью атрибутов также можно указать правила проверки данных и сообщения об ошибках проверки. [Атрибут StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) задает максимальную длину в базе данных и обеспечивает проверку на стороне клиента и на стороне сервера для ASP.NET MVC. В этом атрибуте также можно указать минимальную длину строки, но это минимальное значение не влияет на схему базы данных.

Предположим, вы хотите сделать так, чтобы пользователи не вводили больше 50 символов для имени. Чтобы добавить это ограничение, добавьте атрибуты [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) в `LastName` свойства и `FirstMidName` , как показано в следующем примере:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

Атрибут [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) не запрещает пользователю вводить пробелы в качестве имени. Атрибут [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) можно использовать для применения ограничений к входным данным. Например, следующий код требует, чтобы первый символ был в верхнем регистре, а остальные символы были в алфавитном порядке:

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

Атрибут [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) предоставляет аналогичные функции атрибуту [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , но не поддерживает проверку на стороне клиента.

Запустите приложение и перейдите на вкладку **students (учащиеся** ). Появляется следующее сообщение об ошибке:

*Модель, которая является резервной моделью контекста "SchoolContext", изменилась с момента создания базы данных. Для обновления базы данных ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)) рекомендуется использовать Code First migrations.*

Модель базы данных изменилась таким образом, что требует изменения в схеме базы данных, а Entity Framework обнаружил, что. Вы будете использовать миграции для обновления схемы без потери данных, добавленных в базу данных с помощью пользовательского интерфейса. Если были изменены данные, созданные `Seed` методом, то они будут переведены обратно в исходное состояние из-за метода [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) , используемого в `Seed` методе. ([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) эквивалентен операции «Upsert» в терминологии базы данных.)

Введите в консоли диспетчера пакетов (PMC) следующие команды:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

Команда создает файл с именем  *&lt;&gt;timeStamp\_MaxLengthOnNames.cs.* `add-migration` Он содержит в методе `Up` код, который обновит базу данных в соответствии с текущей моделью данных. Команда `update-database` запустила этот код.

Отметка времени, добавленная в начало имени файла миграции, используется Entity Framework для упорядочения миграции. Перед выполнением `update-database` команды можно создать несколько миграций, после чего все миграции будут применены в том порядке, в котором они были созданы.

Запустите страницу **создать** и введите любое имя длиннее 50 символов. При нажатии кнопки **создать**проверка на стороне клиента отображает сообщение об ошибке: *Поле LastName должно быть строкой с максимальной длиной 50.*

### <a name="the-column-attribute"></a>Атрибут Column

Вы также можете использовать атрибуты, чтобы управлять сопоставлением классов и свойств с базой данных. Предположим, что вы использовали имя `FirstMidName` для поля имени, так как это поле также может содержать отчество. Но вам нужно, чтобы столбец базы данных назывался `FirstName`, так как к этому имени привыкли пользователи, которые будут составлять нерегламентированные запросы к базе данных. Чтобы выполнить это сопоставление, можно использовать атрибут `Column`.

Атрибут `Column` указывает, что при создании базы данных столбец таблицы `Student`, сопоставляемый со свойством `FirstMidName`, будет называться `FirstName`. Другими словами, когда ваш код ссылается на `Student.FirstMidName`, данные будут браться из столбца `FirstName` таблицы `Student` или обновляться в нем. Если не указать имена столбцов, им будет присвоено имя, совпадающее с именем свойства.

В файле *Student.CS* добавьте `using` инструкцию для [System. ComponentModel. DataColumns. Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) и добавьте атрибут имени столбца к `FirstMidName` свойству, как показано в следующем выделенном коде:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

Добавление [атрибута Column](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) изменяет модель резервного SchoolContext, поэтому она не соответствует базе данных. Введите следующие команды в PMC, чтобы создать еще одну миграцию:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

В **Обозреватель сервера**Откройте конструктор таблиц *учащихся* , дважды щелкнув таблицу *Student* .

На следующем рисунке показано исходное имя столбца, которое было до применения первых двух миграций. В дополнение к имени столбца, изменяющегося `FirstMidName` с `FirstName`на, имена двух столбцов с `MAX` длиной изменились на 50 символов.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

Можно также сделать изменения сопоставления базы данных с помощью [API Fluent](https://msdn.microsoft.com/data/jj591617), как будет показано далее в этом руководстве.

> [!NOTE]
> Если попытаться выполнить компиляцию до создания всех классов сущностей в следующих разделах, могут возникнуть ошибки компилятора.

## <a name="update-student-entity"></a>Обновить сущность Student

В *моделс\студент.КС*замените код, добавленный ранее, следующим кодом. Изменения выделены.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=11,13,15,18,22,25-32)]

### <a name="the-required-attribute"></a>Обязательный атрибут

[Обязательный атрибут](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) делает свойства имени обязательными полями. `Required attribute` Не требуется для таких типов значений, как DateTime, int, Double и float. Типам значений не может быть присвоено значение null, поэтому они по сути рассматриваются как обязательные поля. 

Для применения `MinimumLength` нужно использовать атрибут `Required` с `MinimumLength`.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs?highlight=2)]

`MinimumLength` и `Required` разрешают использовать пробелы при проверке. `RegularExpression` Используйте атрибут для полного Управлением по строке.

### <a name="the-display-attribute"></a>Атрибут дисплея

Атрибут `Display` указывает, что заголовки для текстовых полей должны иметь вид "First Name" (Имя), "Last Name" (Фамилия), "Full Name" (Полное имя) и "Enrollment Date" (Дата зачисления) вместо имени свойства в каждом экземпляре (в котором не используется пробел для разделения слов).

### <a name="the-fullname-calculated-property"></a>Вычисляемое свойство FullName

`FullName` — это вычисляемое свойство, которое возвращает значение, созданное путем объединения двух других свойств. Поэтому он имеет только `get` метод доступа, и в базе данных не будет создаваться ни один `FullName` столбец.

## <a name="create-instructor-entity"></a>Создание сущности Instructor

Создайте *моделс\инструктор.КС*, заменив Код шаблона следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs)]

Обратите внимание, что некоторые свойства являются одинаковыми в сущностях `Student` и `Instructor`. В руководстве по [реализации наследования](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) далее в этой серии вы выполните рефакторинг данного кода, чтобы устранить избыточность.

В одной строке можно разместить несколько атрибутов, поэтому можно также написать класс Instructor следующим образом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>Свойства навигации по курсам и OfficeAssignment

`Courses` и `OfficeAssignment` — это свойства навигации. Как было объяснено ранее, они обычно определяются как [Виртуальные](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) , чтобы они могли воспользоваться преимуществами Entity Framework функции, именуемой [отложенной загрузкой](https://msdn.microsoft.com/magazine/hh205756.aspx). Кроме того, если свойство навигации может содержать несколько сущностей, его тип должен реализовывать интерфейс [ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx) . Например, [IList&lt;t&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx) имеет квалификаторы, но не [&lt;IEnumerable t&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx) , так как `IEnumerable<T>` не реализует [Add](https://msdn.microsoft.com/library/63ywd54z.aspx).

Инструктор может обучать любое количество курсов, поэтому `Courses` оно определяется как `Course` коллекция сущностей.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

Наши бизнес-правила могут иметь не более одного офиса, поэтому `OfficeAssignment` он определен как единая `OfficeAssignment` сущность (что может быть `null` , если Office не назначен).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-officeassignment-entity"></a>Создание сущности OfficeAssignment

Создайте *моделс\оффицеассигнмент.КС* со следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

Создайте проект, который сохраняет изменения и проверяет, не были ли сделаны ошибки копирования и вставки, которые компилятор может перехватить.

### <a name="the-key-attribute"></a>Ключевой атрибут

Между `Instructor` `OfficeAssignment` сущностями и существуют связи «один к нулю» или «один к одному». Назначение Office существует только в отношении лектора, которому он назначен, поэтому его первичный ключ также является внешним ключом для `Instructor` сущности. Но Entity Framework `InstructorID` не удается автоматически распознать как первичный ключ этой сущности, так как ее имя не `ID` соответствует соглашению об именовании или имени *класса* `ID` . Таким образом, атрибут `Key` используется для определения ее в качестве ключа:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

Можно также использовать атрибут, `Key` если сущность имеет собственный первичный ключ, но вы хотите присвоить свойству имя, отличное `classnameID` от `ID`или. По умолчанию EF рассматривает ключ как не созданный базой данных, так как столбец предназначен для идентифицирующего отношения.

### <a name="the-foreignkey-attribute"></a>Атрибут Фореигнкэй

При наличии связи "один к нулю" или "один к одному" между двумя сущностями (например, между `OfficeAssignment` и `Instructor`), EF не может определить, какой элемент связи является участником, а какой — зависимым. Связи «один к одному» имеют ссылочное свойство навигации в каждом классе для другого класса. [Атрибут фореигнкэй](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) можно применить к зависимому классу для установления связи. Если опустить [атрибут фореигнкэй](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), при попытке создать миграцию появится следующее сообщение об ошибке:

*Не удалось определить основной элемент ассоциации между типами "ContosoUniversity. Models. OfficeAssignment" и "ContosoUniversity. Models. Instructor". Основной элемент ассоциации должен быть явно настроен с помощью API-интерфейса Fluent связи или заметок к данным.*

Далее в этом руководстве вы узнаете, как настроить эту связь с помощью API Fluent.

### <a name="the-instructor-navigation-property"></a>Свойство навигации преподавателя

Сущность имеет свойство навигации `OfficeAssignment` , допускающее значение null (так как инструктор может не иметь `OfficeAssignment` назначения Office), а сущность имеет свойство навигации `Instructor` , не допускающее значения NULL (так как назначение Office не может `Instructor` Существует без инструктора `InstructorID` — не допускает значения NULL. Если сущность имеет связанную `OfficeAssignment` сущность, каждая сущность будет иметь ссылку на другую в своем свойстве навигации. `Instructor`

Можно добавить `[Required]` атрибут в свойство навигации инструктора, чтобы указать, что должен быть связанный инструктор, но это не нужно делать, так как внешний ключ InstructorID (который также является ключом к этой таблице) не допускает значения NULL.

## <a name="modify-the-course-entity"></a>Изменение сущности курса

В *моделс\каурсе.КС*замените код, который вы добавили ранее, следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

Сущность Course имеет свойство `DepartmentID` внешнего ключа, которое указывает на связанную `Department` `Department` сущность и имеет свойство навигации. Платформа Entity Framework не требует добавлять свойство внешнего ключа в модель данных при наличии свойства навигации для связанной сущности. EF автоматически создает внешние ключи в базе данных везде, где они нужны. Однако наличие внешнего ключа в модели данных позволяет сделать обновления проще и эффективнее. Например, при выборе сущности курса для изменения `Department` сущность имеет значение null, если она не загружается, поэтому при обновлении сущности Course необходимо сначала `Department` получить сущность. Если свойство `DepartmentID` внешнего ключа включено в модель данных, то перед обновлением не нужно `Department` выбирать сущность.

### <a name="the-databasegenerated-attribute"></a>Атрибут Датабасеженератед

[Атрибут датабасеженератед](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) с `CourseID` параметром [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) в свойстве указывает, что значения первичного ключа предоставляются пользователем, а не создаются базой данных.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

По умолчанию Entity Framework предполагает, что значения первичного ключа создаются базой данных. Именно это и требуется для большинства сценариев. Однако для `Course` сущностей вы будете использовать номер курса, указанный пользователем, например серии 1000 для одного отдела, серии 2000 для другого отдела и т. д.

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа и свойства навигации в `Course` сущности соответствуют следующим связям:

- Курс назначается одной кафедре, поэтому по указанным выше причинам имеется внешний ключ `DepartmentID` и свойство навигации `Department`.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- На курс может быть зачислено любое количество учащихся, поэтому свойство навигации `Enrollments` является коллекцией:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- Курс могут вести несколько преподавателей, поэтому свойство навигации `Instructors` является коллекцией:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="create-the-department-entity"></a>Создание сущности Department

Создайте *моделс\департмент.КС* со следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Атрибут Column

Ранее для изменения сопоставления имен столбцов использовался [атрибут Column](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) . В коде для `Department` сущности `Column` используется атрибут для изменения сопоставления типов данных SQL, чтобы столбец был определен с использованием SQL Server типа [money](https://msdn.microsoft.com/library/ms179882.aspx) в базе данных:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

Сопоставление столбцов обычно не является обязательным, поскольку Entity Framework обычно выбирает соответствующий тип данных SQL Server в зависимости от типа CLR, определенного для свойства. Тип `decimal` среды CLR сопоставляется с типом `decimal` SQL Server. Но в этом случае известно, что столбец будет хранить денежные суммы, а тип данных [money](https://msdn.microsoft.com/library/ms179882.aspx) более подходит для этого. Дополнительные сведения о типах данных CLR и их соответствии с SQL Server типами данных см. в разделе [SqlClient для Entity Framework](https://msdn.microsoft.com/library/bb896344.aspx).

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа и навигации отражают следующие связи:

- Кафедра может иметь или не иметь администратора, и администратор всегда является преподавателем. Поэтому свойство включается в качестве внешнего ключа `Instructor` сущности, а после обозначения `int` типа, чтобы пометить свойство как допускающее значение null, добавляется вопросительный знак. `InstructorID` Свойство навигации имеет имя `Administrator` , но `Instructor` содержит сущность:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- У отдела может быть много курсов, поэтому есть `Courses` свойство навигации:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > По соглашению Entity Framework разрешает каскадное удаление для внешних ключей, не допускающих значение null, и связей многие ко многим. Это может привести к циклическим правилам каскадного удаления, которые вызывают исключение при попытке добавить миграцию. Например, если вы не определили `Department.InstructorID` свойство как допускающее значение null, вы получите следующее сообщение об исключении: "Ссылочная связь приведет к неразрешенной циклической ссылке". Если для бизнес-правил `InstructorID` требуется свойство, которое не допускает значения NULL, для отключения каскадного удаления на связи необходимо использовать следующую инструкцию fluent API:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modify-the-enrollment-entity"></a>Изменение сущности Enrollment

 В *моделс\енроллмент.КС*замените код, который вы добавили ранее, следующим кодом.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=1,15)]

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа и навигации отражают следующие связи:

- Запись зачисления предназначена для одного курса, поэтому доступно свойство первичного ключа `CourseID` и свойство навигации `Course`:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs)]
- Запись зачисления предназначена для одного учащегося, поэтому доступно свойство первичного ключа `StudentID` и свойство навигации `Student`:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]

### <a name="many-to-many-relationships"></a>Связи многие ко многим

Существует связь «многие ко многим» между сущностями и `Student` `Course` , а `Enrollment` сущностная функция является таблицей объединения «многие ко многим» *с полезной* нагрузкой в базе данных. Это означает, что `Enrollment` таблица содержит дополнительные данные помимо внешних ключей для соединяемых таблиц (в данном случае первичного ключа `Grade` и свойства).

На следующем рисунке показано, как выглядят эти связи на схеме сущностей. (Эта схема была создана с помощью [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); создание схемы не является частью руководства, оно просто используется в качестве иллюстрации.)

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

Каждая линия связи содержит 1 на одном конце и звездочку (\*) в другой, что означает связь «один ко многим».

Если таблица не включала в себя сведения об оценках, потребуется только поместить два внешних ключа `CourseID` и `StudentID`. `Enrollment` В этом случае он будет соответствовать таблице соединений типа «многие ко многим» *без полезных* данных (или *таблицы чистого объединения*) в базе данных, и для нее не придется создавать класс модели. Сущности `Instructor` и`Course` имеют такой тип связи «многие ко многим», и как можно видеть, между ними нет класса сущностей:

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

Однако в базе данных требуется таблица соединений, как показано в следующей диаграмме базы данных:

![Instructor-Course_many-to-many_relationship_tables](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

Entity Framework автоматически создает `CourseInstructor` таблицу, и вы читаете и обновляете ее косвенно, считывая и `Instructor.Courses` обновив свойства `Course.Instructors` навигации и.

## <a name="entity-relationship-diagram"></a>Диаграмма отношений сущностей

Ниже показана схема, создаваемая средствами Entity Framework Power Tools для завершенной модели School.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

Помимо линий связи «многие ко многим» (\* в \*) и линий связи «один ко многим» (от 1 до \*), можно увидеть линию связи «один к нулю» или «один к одному» (от 1 `Instructor` до 0.. 1) между и `OfficeAssignment` сущности и линия связи "ноль или один ко многим" (от 0.. 1 до \*) между сущностями инструктора и отдел.

## <a name="add-code-to-database-context"></a>Добавить код в контекст базы данных

Далее предстоит добавить новые сущности в `SchoolContext` класс и настроить некоторые сопоставления с помощью вызовов [API Fluent](https://msdn.microsoft.com/data/jj591617) . API — это "Fluent", так как часто используется для объединения ряда вызовов методов в одну инструкцию, как показано в следующем примере:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

В этом учебнике вы будете использовать API Fluent только для сопоставления базы данных, которое нельзя сделать с помощью атрибутов. Однако текучий API позволяет задать большинство правил форматирования, проверки и сопоставления, которые можно указать с помощью атрибутов. Некоторые атрибуты, такие как `MinimumLength`, невозможно применить с текучим API. Как упоминалось ранее `MinimumLength` , не изменяет схему, она применяет правило проверки на стороне клиента и сервера.

Некоторые разработчики предпочитают использовать текучий API монопольно, чтобы оставить свои классы сущностей "чистыми". Атрибуты и текучий API можно смешивать, и существует несколько конфигураций, которые можно реализовать только с помощью текучего API. На практике рекомендуется выбрать один из этих двух подходов и использовать его максимально согласованно.

Чтобы добавить новые сущности в модель данных и выполнить сопоставление базы данных, которое не выполнялось с помощью атрибутов, замените код в *дал\счулконтекст.КС* следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

Новая инструкция в методе [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) настраивает таблицу соединений "многие ко многим":

- Для связи «многие ко многим» между `Instructor` сущностями и `Course` в коде указываются имена таблиц и столбцов для соединяемой таблицы. Code First можете настроить связь "многие ко многим" без этого кода, но если не вызвать ее, то `InstructorInstructorID` `InstructorID` для столбца будут получены имена по умолчанию, например.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

В следующем коде приведен пример того, как можно было использовать fluent API вместо атрибутов для указания связи между `Instructor` сущностями и. `OfficeAssignment`

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

Дополнительные сведения о том, какие операторы fluent API выполняются в фоновом режиме, см. в записи блога о [API Fluent](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) .

## <a name="seed-database-with-test-data"></a>Начальное заполнение базы данных тестовыми данными

Замените код в файле *Migrations\Configuration.CS* следующим кодом, чтобы предоставить начальные данные для новых сущностей, которые вы создали.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

Как было показано в первом учебном курсе, большая часть этого кода просто обновляет или создает новые объекты сущностей и загружает демонстрационные данные в свойства, необходимые для тестирования. Обратите внимание, что `Course` обрабатывается сущность с отношением « `Instructor` многие ко многим» с сущностью.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

При создании `Course` объекта свойство `Instructors` навигации инициализируется как пустая коллекция с помощью кода `Instructors = new List<Instructor>()`. Это дает возможность добавлять `Instructor` сущности, связанные с этим `Course` , с помощью `Instructors.Add` метода. Если не создать пустой список, вы не сможете добавить эти связи, так как `Instructors` свойство будет иметь значение NULL и `Add` не будет иметь метода. Можно также добавить инициализацию списка в конструктор.

## <a name="add-a-migration"></a>Добавление миграции

В PMC введите `add-migration` команду (еще не `update-database` выполнять команду):

`add-Migration ComplexDataModel`

Если попытаться выполнить команду `update-database` на этом этапе (пока этого делать не нужно), возникнет следующая ошибка:

*Инструкция ALTER TABLE конфликтует с ограничением внешнего ключа "FK\_dbo. Курс\_dbo. DepartmentID\_отдела ". Конфликт произошел в базе данных "ContosoUniversity", таблица "dbo. Department ", столбец" DepartmentID ".*

Иногда при выполнении миграции с существующими данными необходимо вставить данные заглушки в базу данных для удовлетворения ограничений внешнего ключа, и это будет сделано. Созданный код в методе комплексдатамодел `Up` добавляет к `Course` таблице внешний ключ, `DepartmentID` не допускающий значения NULL. Поскольку при выполнении кода в `Course` таблице уже есть строки `AddColumn` , операция завершится ошибкой, так как SQL Server не знает, какое значение следует разместить в столбце, которое не может иметь значение null. Поэтому необходимо изменить код, чтобы присвоить новому столбцу значение по умолчанию, и создать отдел-заглушку с именем "Temp", который будет использоваться в качестве Отдела по умолчанию. В результате все существующие `Course` строки будут связаны с "временным" подразделением `Up` после выполнения метода. Их можно связать с правильными отделами в `Seed` методе.

Измените файл *timestamp\_ComplexDataModel.cs, закомментируйте строку кода, которая добавляет столбец DepartmentID в таблицу Course, и добавьте следующий выделенный код (строка с комментарием также&gt;* &lt; выделенные):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

При выполнении `Department` `Course` `Department` метода он вставит строки в таблицу и будет связывать существующие строки с новыми строками. `Seed` Если вы еще не добавили какие-либо курсы в пользовательский интерфейс, вам больше не потребуется "Temp" или значение по умолчанию для `Course.DepartmentID` столбца. Чтобы позволить кому-либо добавить курсы с помощью приложения, необходимо также обновить `Seed` код метода, чтобы убедиться, что все `Course` строки (а не только те, которые были вставлены в предыдущих запусках `Seed` метода) имеют Допустимые `DepartmentID` значения, прежде чем удалить значение по умолчанию из столбца и удалить временный отдел.

## <a name="update-the-database"></a>Обновление базы данных

Завершив редактирование &lt;файла *timestamp&gt;\_ComplexDataModel.CS* , введите `update-database` команду в PMC, чтобы выполнить миграцию.

[!code-powershell[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.ps1)]

> [!NOTE]
> При переносе данных и внесении изменений в схему можно получить другие ошибки. Если вы получаете ошибки миграции, которые не удается устранить, измените имя базы данных в строке подключения или удалите базу данных. Самый простой подход заключается в том, чтобы переименовать базу данных в файле *Web. config* . В следующем примере показано имя, измененное на\_Cu Test:
>
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample36.xml?highlight=1)]
>
> В новой базе данных нет данных для переноса, и `update-database` выполнение команды, скорее всего, завершится без ошибок. Инструкции по удалению базы данных см. в статье [как удалить базу данных из Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).
>
> Если это не удается, можно попробовать повторно инициализировать базу данных, введя следующую команду в PMC:
>
> `update-database -TargetMigration:0`

Откройте базу данных в **Обозреватель сервера** , как было сделано ранее, и разверните узел **таблицы** , чтобы увидеть, что все таблицы созданы. (Если вы по-прежнему открыли **Обозреватель сервера** ранее, нажмите кнопку **Обновить** .)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image16.png)

Не был создан класс модели для `CourseInstructor` таблицы. Как упоминалось ранее, это таблица соединений для связи «многие ко многим» между `Instructor` сущностями и. `Course`

Щелкните правой кнопкой мыши `CourseInstructor` таблицу и выберите команду " **отобразить данные таблицы** ", чтобы убедиться в том, что она содержит данные `Instructor` в результате сущностей, `Course.Instructors` добавленных в свойство навигации.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image17.png)

## <a name="get-the-code"></a>Получите код

[Скачать завершенный проект](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Дополнительные ресурсы

Ссылки на другие ресурсы Entity Framework можно найти в [ресурсах, рекомендуемых для доступа к данным ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Следующие шаги

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Настройка модели данных
> * Обновленная сущность Student
> * Создание сущности Instructor
> * Создание сущности OfficeAssignment
> * Изменена сущность курса
> * Создание сущности отдела
> * Изменение сущности регистрации
> * Код добавлен в контекст базы данных
> * Начальное заполнение базы данных тестовыми данными
> * Добавление миграции
> * Обновление базы данных

Перейдите к следующей статье, чтобы узнать, как читать и отображать связанные данные, загружаемые Entity Framework в свойства навигации.

> [!div class="nextstepaction"]
> [Чтение связанных данных](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
