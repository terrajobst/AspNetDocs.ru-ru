---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: Создание более сложной модели данных для приложения ASP.NET MVC (4 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9c19ec47ad98a319ddee17db014c4b15e3734778
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595358"
---
# <a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>Создание более сложной модели данных для приложения ASP.NET MVC (4 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущих руководствах вы работали с простой моделью данных, состоящей из трех сущностей. В этом учебнике вы добавите больше сущностей и связей и настроите модель данных, указав правила форматирования, проверки и сопоставления базы данных. Вы увидите два способа настройки модели данных: путем добавления атрибутов в классы сущностей и добавления кода в класс контекста базы данных.

По завершении работы классы сущностей сформируют готовую модель данных, приведенную на следующем рисунке:

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>Настройка модели данных с использованием атрибутов

В этом разделе вы узнаете, как настроить модель данных с помощью атрибутов, которые указывают правила форматирования, проверки и сопоставления базы данных. Затем в следующих разделах вы создадите полную модель данных `School`, добавив атрибуты к уже созданным классам и создавая новые классы для оставшихся типов сущностей в модели.

### <a name="the-datatype-attribute"></a>Атрибут DataType

Сейчас для дат зачисления студентов учащихся все веб-страницы отображают время и дату, хотя для этого поля достаточно одной даты. Используя атрибуты заметок к данным, вы можете внести в код одно изменение, позволяющее исправить формат отображения в каждом представлении, где отображаются эти данные. Чтобы рассмотреть соответствующий пример, вы добавите атрибут в свойство `EnrollmentDate` класса `Student`.

В *моделс\студент.КС*добавьте оператор `using` для пространства имен `System.ComponentModel.DataAnnotations` и добавьте атрибуты `DataType` и `DisplayFormat` в свойство `EnrollmentDate`, как показано в следующем примере:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

Атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) используется для указания более конкретного типа данных, чем внутренний тип базы данных. В этом случае требуется отслеживать только дату, а не дату и время. [Перечисление DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) предоставляет множество типов данных, таких как *Date, Time, PhoneNumber, Currency, EmailAddress* и др. Атрибут `DataType` также обеспечивает автоматическое предоставление функций для определенных типов в приложении. Например, можно создать ссылку `mailto:` для [DataType. EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), а также можно указать селектор даты для [типа данных. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) в браузерах, поддерживающих [HTML5](http://html5.org/). Атрибуты [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) создают атрибуты HTML 5 [Data-](http://ejohn.org/blog/html-5-data-attributes/) (произносит *штрих данных*), которые могут быть понятны браузерам HTML 5. Атрибуты [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) не обеспечивают никакой проверки.

`DataType.Date` не задает формат отображаемой даты. По умолчанию поле данных отображается в соответствии с форматами по умолчанию, основанными на [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)сервера.

С помощью атрибута `DisplayFormat` можно явно указать формат даты:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

Параметр `ApplyFormatInEditMode` указывает, что указанное форматирование должно также применяться при отображении значения в текстовом поле для редактирования. (Для некоторых полей, например для денежных значений, может потребоваться не использовать символ валюты в текстовом поле для редактирования.)

Атрибут [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) можно использовать отдельно, но обычно рекомендуется использовать атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) . Атрибут `DataType` передает *семантику* данных в отличие от того, как отобразить их на экране, и предоставляет следующие преимущества, не получаемые с помощью `DisplayFormat`:

- Браузер может включить функции HTML5 (например, отобразить элемент управления "Календарь", соответствующий языковой стандарт символ валюты, ссылки электронной почты и т. д.).
- По умолчанию браузер будет отображать данные с использованием правильного формата в зависимости от [языкового стандарта](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).
- С помощью атрибута [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) можно выбрать подходящий шаблон поля для подготовки к просмотру данных ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) , если он используется, использует строковый шаблон). Дополнительные сведения см. в статье о [шаблонах ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)Михаил Уилсон (. (Хотя написано для MVC 2, эта статья по-прежнему применяется к текущей версии ASP.NET MVC.)

При использовании атрибута `DataType` с полем даты необходимо также указать атрибут `DisplayFormat`, чтобы обеспечить правильное отображение поля в браузерах Chrome. Дополнительные сведения см. в [этом потоке StackOverflow](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).

Снова запустите страницу индекса учащихся и обратите внимание, что время для дат регистрации больше не отображается. То же самое будет справедливо для любого представления, использующего модель `Student`.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>Стрингленгсаттрибуте

Можно также указать правила проверки данных и сообщения с помощью атрибутов. Предположим, вы хотите сделать так, чтобы пользователи не вводили больше 50 символов для имени. Чтобы добавить это ограничение, добавьте атрибуты [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) в свойства `LastName` и `FirstMidName`, как показано в следующем примере:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

Атрибут [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) не запрещает пользователю вводить пробелы в качестве имени. Атрибут [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) можно использовать для применения ограничений к входным данным. Например, следующий код требует, чтобы первый символ был в верхнем регистре, а остальные символы были в алфавитном порядке:

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

Атрибут [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) предоставляет аналогичные функции атрибуту [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , но не поддерживает проверку на стороне клиента.

Запустите приложение и перейдите на вкладку **students (учащиеся** ). Появляется следующее сообщение об ошибке:

*Модель, которая является резервной моделью контекста "SchoolContext", изменилась с момента создания базы данных. Рекомендуется использовать Code First Migrations для обновления базы данных ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

Модель базы данных изменилась таким образом, что требует изменения в схеме базы данных, а Entity Framework обнаружил, что. Вы будете использовать миграции для обновления схемы без потери данных, добавленных в базу данных с помощью пользовательского интерфейса. Если были изменены данные, созданные методом `Seed`, который будет возвращен в исходное состояние из-за метода [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) , используемого в методе `Seed`. ([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) эквивалентен операции «Upsert» в терминологии базы данных.)

Введите в консоли диспетчера пакетов (PMC) следующие команды:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

Команда `add-migration MaxLengthOnNames` создает файл с именем *&lt;timeStamp&gt;\_MaxLengthOnNames.CS*. Этот файл содержит код, который будет обновлять базу данных в соответствии с текущей моделью данных. Отметка времени, добавленная в начало имени файла миграции, используется Entity Framework для упорядочения миграции. После создания нескольких миграций, при удалении базы данных или при развертывании проекта с помощью миграций все миграции применяются в том порядке, в котором они были созданы.

Запустите страницу **создать** и введите любое имя длиннее 50 символов. Как только вы превысит 50 символов, проверка на стороне клиента немедленно выводит сообщение об ошибке.

![Ошибка Val на стороне клиента](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>Атрибут Column

Вы также можете использовать атрибуты, чтобы управлять сопоставлением классов и свойств с базой данных. Предположим, что вы использовали имя `FirstMidName` для поля имени, так как это поле также может содержать отчество. Но вам нужно, чтобы столбец базы данных назывался `FirstName`, так как к этому имени привыкли пользователи, которые будут составлять нерегламентированные запросы к базе данных. Чтобы выполнить это сопоставление, можно использовать атрибут `Column`.

Атрибут `Column` указывает, что при создании базы данных столбец таблицы `Student`, сопоставляемый со свойством `FirstMidName`, будет называться `FirstName`. Другими словами, когда ваш код ссылается на `Student.FirstMidName`, данные будут браться из столбца `FirstName` таблицы `Student` или обновляться в нем. Если не указать имена столбцов, им будет присвоено имя, совпадающее с именем свойства.

Добавьте инструкцию using для [System. ComponentModel. аннотации. Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) и атрибут имени столбца в свойство `FirstMidName`, как показано в следующем выделенном коде:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

Добавление [атрибута Column](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) изменяет модель резервного SchoolContext, поэтому она не соответствует базе данных. Введите следующие команды в PMC, чтобы создать еще одну миграцию:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

В **Обозреватель сервера** (**Обозреватель базы данных** если вы используете Express для Интернета), дважды щелкните таблицу *учащихся* .

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

На следующем рисунке показано исходное имя столбца, которое было до применения первых двух миграций. Помимо имени столбца, изменяющегося с `FirstMidName` на `FirstName`, имена столбцов с `MAX` длиной изменились до 50 символов.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

Можно также сделать изменения сопоставления базы данных с помощью [API Fluent](https://msdn.microsoft.com/data/jj591617), как будет показано далее в этом руководстве.

> [!NOTE]
> При попытке выполнить компиляцию до завершения создания всех этих классов сущностей могут возникнуть ошибки компилятора.

## <a name="create-the-instructor-entity"></a>Создание сущности Instructor

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

Создайте *моделс\инструктор.КС*, заменив Код шаблона следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

Обратите внимание, что некоторые свойства являются одинаковыми в сущностях `Student` и `Instructor`. В руководстве по [реализации наследования](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) далее в этой серии будет выполнен рефакторинг с использованием наследования для устранения этой избыточности.

### <a name="the-required-and-display-attributes"></a>Обязательные и отображаемые атрибуты

Атрибуты свойства `LastName` указывают, что это обязательное поле, заголовок текстового поля должен иметь имя "Фамилия" (вместо имени свойства, которое должно быть "LastName" без пробела) и длина значения не может превышать 50 символов.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

[Атрибут StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) задает максимальную длину в базе данных и обеспечивает проверку на стороне клиента и на стороне сервера для ASP.NET MVC. В этом атрибуте также можно указать минимальную длину строки, но это минимальное значение не влияет на схему базы данных. [Обязательный атрибут](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) не требуется для таких типов значений, как DateTime, int, Double и float. Типам значений не может быть присвоено значение null, поэтому они по сути являются обязательными. Можно удалить [необходимый атрибут](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) и заменить его параметром минимальной длины для атрибута `StringLength`:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

В одной строке можно разместить несколько атрибутов, поэтому можно также написать класс Instructor следующим образом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>Вычисляемое свойство FullName

`FullName` — это вычисляемое свойство, которое возвращает значение, созданное путем объединения двух других свойств. Поэтому он имеет только `get` метод доступа, и в базе данных не будет создаваться `FullName` столбца.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>Свойства навигации по курсам и OfficeAssignment

`Courses` и `OfficeAssignment` — это свойства навигации. Как было объяснено ранее, они обычно определяются как [Виртуальные](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) , чтобы они могли воспользоваться преимуществами Entity Framework функции, именуемой [отложенной загрузкой](https://msdn.microsoft.com/magazine/hh205756.aspx). Кроме того, если свойство навигации может содержать несколько сущностей, его тип должен реализовывать интерфейс [ICollection&lt;t&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) . (Например, [IList&lt;t&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) квалификаторы, но не [IEnumerable&lt;t&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) , так как `IEnumerable<T>` не реализует [Add](https://msdn.microsoft.com/library/63ywd54z.aspx).

Инструктор может обучать любое количество курсов, поэтому `Courses` определяется как коллекция сущностей `Course`. Наши бизнес-правила состояния инструктора могут иметь только не более одного офиса, поэтому `OfficeAssignment` определяется как единая `OfficeAssignment` сущность (которая может быть `null`, если Office не назначен).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>Создание сущности OfficeAssignment

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

Создайте *моделс\оффицеассигнмент.КС* со следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

Создайте проект, который сохраняет изменения и проверяет, не были ли сделаны ошибки копирования и вставки, которые компилятор может перехватить.

### <a name="the-key-attribute"></a>Ключевой атрибут

Между `Instructor` и `OfficeAssignment` сущностями существует связь "один к нулю" или "один к одному". Назначение Office существует только в отношении инструктора, которому он назначен, и поэтому его первичный ключ также является внешним ключом для `Instructor` сущности. Но Entity Framework не может автоматически распознать `InstructorID` как первичный ключ этой сущности, так как ее имя не соответствует соглашению об именовании `ID` или *classname* `ID`. Таким образом, атрибут `Key` используется для определения ее в качестве ключа:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

Можно также использовать атрибут `Key`, если сущность имеет собственный первичный ключ, но вы хотите присвоить свойству имя, отличное от `classnameID` или `ID`. По умолчанию EF рассматривает ключ как не созданный базой данных, так как столбец предназначен для идентифицирующего отношения.

### <a name="the-foreignkey-attribute"></a>Атрибут Фореигнкэй

При наличии связи "один к нулю" или "один к одному" между двумя сущностями (например, между `OfficeAssignment` и `Instructor`) EF не может определить, какой элемент связи является участником, а какой — от конца. Связи «один к одному» имеют ссылочное свойство навигации в каждом классе для другого класса. [Атрибут фореигнкэй](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) можно применить к зависимому классу для установления связи. Если опустить [атрибут фореигнкэй](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), при попытке создать миграцию появится следующее сообщение об ошибке:

Не удалось определить основной элемент ассоциации между типами "ContosoUniversity. Models. OfficeAssignment" и "ContosoUniversity. Models. Instructor". Основной элемент ассоциации должен быть явно настроен с помощью API-интерфейса Fluent связи или заметок к данным.

Далее в этом руководстве мы покажем, как настроить эту связь с помощью API Fluent.

### <a name="the-instructor-navigation-property"></a>Свойство навигации преподавателя

Сущность `Instructor` имеет свойство навигации `OfficeAssignment`, допускающее значение null (так как инструктор может не иметь назначения Office), а сущность `OfficeAssignment` имеет свойство навигации `Instructor`, не допускающее значения NULL (поскольку назначение Office не может существовать без инструктора, `InstructorID` не допускает значения NULL). Если сущность `Instructor` имеет связанную сущность `OfficeAssignment`, каждая сущность будет иметь ссылку на другую в своем свойстве навигации.

Можно добавить атрибут `[Required]` в свойстве навигации инструктора, чтобы указать, что должен быть связанный инструктор, но это не нужно делать, так как внешний ключ InstructorID (который также является ключом к этой таблице) не допускает значения NULL.

## <a name="modify-the-course-entity"></a>Изменение сущности Course

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

В *моделс\каурсе.КС*замените код, который вы добавили ранее, следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

Сущность Course имеет свойство внешнего ключа, `DepartmentID` которое указывает на связанную сущность `Department` и имеет свойство навигации `Department`. Платформа Entity Framework не требует добавлять свойство внешнего ключа в модель данных при наличии свойства навигации для связанной сущности. EF автоматически создает внешние ключи в базе данных везде, где они нужны. Однако наличие внешнего ключа в модели данных позволяет сделать обновления проще и эффективнее. Например, при выборке сущности курса для изменения `Department` сущность имеет значение null, если она не загружается, поэтому при обновлении сущности Course необходимо сначала получить сущность `Department`. Если свойство внешнего ключа `DepartmentID` включено в модель данных, то перед обновлением не нужно получать сущность `Department`.

### <a name="the-databasegenerated-attribute"></a>Атрибут Датабасеженератед

[Атрибут датабасеженератед](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) с параметром [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) в свойстве `CourseID` указывает, что значения первичного ключа предоставляются пользователем, а не создаются базой данных.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

По умолчанию Entity Framework предполагает, что значения первичного ключа создаются базой данных. Именно это и требуется для большинства сценариев. Однако для `Course`ных сущностей вы будете использовать номер курса, указанный пользователем, например, серии 1000 для одного отдела, серии 2000 для другого отдела и т. д.

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа и свойства навигации в сущности `Course` соответствуют следующим связям:

- Курс назначается одной кафедре, поэтому по указанным выше причинам имеется внешний ключ `DepartmentID` и свойство навигации `Department`. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- На курс может быть зачислено любое количество учащихся, поэтому свойство навигации `Enrollments` является коллекцией: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- Курс могут вести несколько преподавателей, поэтому свойство навигации `Instructors` является коллекцией: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>Создание сущности отдела

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

Создайте *моделс\департмент.КС* со следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Атрибут Column

Ранее для изменения сопоставления имен столбцов использовался [атрибут Column](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) . В коде для `Department` сущности атрибут `Column` используется для изменения сопоставления типов данных SQL, чтобы столбец был определен с использованием SQL Server типа [money](https://msdn.microsoft.com/library/ms179882.aspx) в базе данных:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

Сопоставление столбцов обычно не является обязательным, поскольку Entity Framework обычно выбирает соответствующий тип данных SQL Server в зависимости от типа CLR, определенного для свойства. Тип `decimal` среды CLR сопоставляется с типом `decimal` SQL Server. Но в этом случае известно, что столбец будет хранить денежные суммы, а тип данных [money](https://msdn.microsoft.com/library/ms179882.aspx) более подходит для этого.

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа и навигации отражают следующие связи:

- Кафедра может иметь или не иметь администратора, и администратор всегда является преподавателем. Поэтому `InstructorID` свойство включается в качестве внешнего ключа `Instructor` сущности, а после обозначения типа `int` добавляется вопросительный знак, чтобы пометить свойство как допускающее значение null. Свойство навигации называется `Administrator` но содержит сущность `Instructor`: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- В отделе может быть много курсов, поэтому имеется `Courses` свойство навигации: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > По соглашению Entity Framework разрешает каскадное удаление для внешних ключей, не допускающих значение null, и связей многие ко многим. Это может привести к созданию циклических правил каскадного удаления, что вызовет исключение при выполнении кода инициализатора. Например, если вы не определили свойство `Department.InstructorID` как допускающее значение null, при выполнении инициализатора будет получено следующее сообщение об исключении: "ссылочная связь приведет к неразрешенной циклической ссылке". Если бизнес-правила требуют `InstructorID` свойства как не допускающие значения NULL, для отключения каскадного удаления в отношении необходимо использовать следующий API-интерфейс Fluent. 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modifying-the-student-entity"></a>Изменение сущности Student

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

В *моделс\студент.КС*замените код, добавленный ранее, следующим кодом. Изменения выделены.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>Сущность регистрации

 В *моделс\енроллмент.КС*замените код, который вы добавили ранее, следующим кодом.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа и навигации отражают следующие связи:

- Запись зачисления предназначена для одного курса, поэтому доступно свойство первичного ключа `CourseID` и свойство навигации `Course`: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- Запись зачисления предназначена для одного учащегося, поэтому доступно свойство первичного ключа `StudentID` и свойство навигации `Student`: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>Связи многие ко многим

Существует связь «многие ко многим» между сущностями `Student` и `Course`, а `Enrollment` функции сущности в качестве таблицы соединений «многие ко многим» *с полезной* нагрузкой в базе данных. Это означает, что `Enrollment`ная таблица содержит дополнительные данные помимо внешних ключей для соединяемых таблиц (в данном случае это первичный ключ и свойство `Grade`).

На следующем рисунке показано, как выглядят эти связи на схеме сущностей. (Эта схема была создана с помощью [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); создание схемы не является частью руководства, оно просто используется в качестве иллюстрации.)

![Student-Course_many-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

Каждая линия связи содержит 1 на одном конце и звездочку (\*) на другом, что означает связь «один ко многим».

Если `Enrollment`ная таблица не включала в себя сведения об оценках, потребуется только поместить два внешних ключа `CourseID` и `StudentID`. В этом случае он будет соответствовать таблице соединений типа «многие ко многим» *без полезных* данных (или *таблицы чистого объединения*) в базе данных, и для нее не придется создавать класс модели. Сущности `Instructor` и `Course` имеют такой тип связи «многие ко многим», и как можно видеть, между ними нет класса сущностей:

![Instructor-Course_many-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

Однако в базе данных требуется таблица соединений, как показано в следующей диаграмме базы данных:

![Instructor-Course_many-many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

Entity Framework автоматически создает таблицу `CourseInstructor`, и вы читаете и обновляете ее косвенно, считывая и обновив свойства навигации `Instructor.Courses` и `Course.Instructors`.

## <a name="entity-diagram-showing-relationships"></a>Схема сущностей, показывающая связи

Ниже показана схема, создаваемая средствами Entity Framework Power Tools для завершенной модели School.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

Помимо линий связи «многие ко многим» (\* для \*) и линий связи «один ко многим» (от 1 до \*), здесь можно увидеть линию связи «один к нулю» или «один к одному» (от 1 до 0.. 1) между сущностями `Instructor` и `OfficeAssignment` и линией связи «ноль или один ко многим» (0.. 1 to \*) между сущностями инструктора и отдел.

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>Настройка модели данных путем добавления кода в контекст базы данных

Далее предстоит добавить новые сущности в класс `SchoolContext` и настроить некоторые сопоставления с помощью вызовов [API Fluent](https://msdn.microsoft.com/data/jj591617) . (API — это "Fluent", так как часто используется для объединения ряда вызовов методов в одну инструкцию.)

В этом учебнике вы будете использовать API Fluent только для сопоставления базы данных, которое нельзя сделать с помощью атрибутов. Однако текучий API позволяет задать большинство правил форматирования, проверки и сопоставления, которые можно указать с помощью атрибутов. Некоторые атрибуты, такие как `MinimumLength`, невозможно применить с текучим API. Как упоминалось ранее, `MinimumLength` не изменяет схему, она применяет правило проверки на стороне клиента и сервера.

Некоторые разработчики предпочитают использовать текучий API монопольно, чтобы оставить свои классы сущностей "чистыми". Атрибуты и текучий API можно смешивать, и существует несколько конфигураций, которые можно реализовать только с помощью текучего API. На практике рекомендуется выбрать один из этих двух подходов и использовать его максимально согласованно.

Чтобы добавить новые сущности в модель данных и выполнить сопоставление базы данных, которое не выполнялось с помощью атрибутов, замените код в *дал\счулконтекст.КС* следующим кодом:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

Новая инструкция в методе [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) настраивает таблицу соединений "многие ко многим":

- Для связи «многие ко многим» между сущностями «`Instructor`» и «`Course`» в коде указываются имена таблиц и столбцов для соединяемой таблицы. Code First можете настроить связь "многие ко многим" без этого кода, но если вы не называете ее, вы получите имена по умолчанию, например `InstructorInstructorID` для столбца `InstructorID`.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

В следующем коде приведен пример того, как можно было использовать fluent API вместо атрибутов для указания связи между сущностями `Instructor` и `OfficeAssignment`.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

Дополнительные сведения о том, какие операторы fluent API выполняются в фоновом режиме, см. в записи блога о [API Fluent](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) .

## <a name="seed-the-database-with-test-data"></a>Заполнение базы данных тестовыми данными

Замените код в файле *Migrations\Configuration.CS* следующим кодом, чтобы предоставить начальные данные для новых сущностей, которые вы создали.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

Как было показано в первом учебном курсе, большая часть этого кода просто обновляет или создает новые объекты сущностей и загружает демонстрационные данные в свойства, необходимые для тестирования. Однако обратите внимание, что обрабатывается сущность `Course`, которая имеет связь "многие ко многим" с сущностью `Instructor`.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

При создании `Course`ного объекта свойство навигации `Instructors` инициализируется как пустая коллекция с помощью `Instructors = new List<Instructor>()`кода. Это позволяет добавлять `Instructor` сущности, связанные с этим `Course`, с помощью метода `Instructors.Add`. Если не создать пустой список, вы не сможете добавить эти связи, так как свойство `Instructors` будет иметь значение NULL и не будет иметь метод `Add`. Можно также добавить инициализацию списка в конструктор.

## <a name="add-a-migration-and-update-the-database"></a>Добавление миграции и обновление базы данных

В PMC введите команду `add-migration`:

`PM> add-Migration Chap4`

При попытке обновить базу данных на этом этапе вы получите следующую ошибку:

*Инструкция ALTER TABLE конфликтует с ограничением внешнего ключа "FK\_dbo. Курс\_dbo. Отдел\_DepartmentID ". Конфликт произошел в базе данных "ContosoUniversity", таблица "dbo. Department ", столбец" DepartmentID ".*

Измените &lt;*timestamp&gt;\_файл Chap4.CS* и внесите следующие изменения в код (вы добавите инструкцию SQL и измените инструкцию `AddColumn`):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

(Убедитесь, что вы заметите или удалите существующую `AddColumn` строку при добавлении новой строки, или при вводе команды `update-database` возникнет ошибка.)

Иногда при выполнении миграции с существующими данными необходимо вставить данные заглушки в базу данных, чтобы удовлетворить ограничения внешнего ключа, и это именно то, что сейчас выполняется. Созданный код добавляет внешний ключ `DepartmentID`, не допускающий значения NULL, в таблицу `Course`. Если в таблице `Course` уже есть строки при выполнении кода, операция `AddColumn` завершится ошибкой, так как SQL Server не знает, какое значение следует разместить в столбце, которое не может иметь значение null. Поэтому вы изменили код, чтобы присвоить новому столбцу значение по умолчанию, и вы создали Отдел-заглушку с именем "Temp", который будет использоваться в качестве Отдела по умолчанию. В результате, если при выполнении этого кода существуют `Course` строки, все они будут связаны с временным подразделением.

При выполнении метода `Seed` вставляет строки в таблицу `Department` и связывает существующие строки `Course` с этими новыми `Department` строками. Если вы еще не добавили какие-либо курсы в пользовательский интерфейс, вам больше не потребуется "Temp" или значение по умолчанию в столбце "`Course.DepartmentID`". Чтобы позволить кому-либо добавить курсы с помощью приложения, необходимо также обновить код метода `Seed`, чтобы убедиться, что все `Course` строки (не только те, которые вставлены предыдущими запусками метода `Seed`) имеют допустимые `DepartmentID` значения, прежде чем удалять значение по умолчанию из столбца и удалять временный отдел.

Завершив изменение &lt;*timestamp&gt;\_файл Chap4.CS* , введите команду `update-database` в PMC, чтобы выполнить миграцию.

> [!NOTE]
> При переносе данных и внесении изменений в схему можно получить другие ошибки. При возникновении ошибок миграции, которые невозможно разрешить, можно изменить строку подключения в файле *Web. config* или удалить базу данных. Самый простой подход заключается в том, чтобы переименовать базу данных в файле *Web. config* . Например, измените имя базы данных на CU\_Test, как показано ниже:
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
> В новой базе данных нет данных для переноса, и выполнение команды `update-database` с большей вероятностью завершится без ошибок. Инструкции по удалению базы данных см. в статье [как удалить базу данных из Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).

Откройте базу данных в **Обозреватель сервера** , как было сделано ранее, и разверните узел **таблицы** , чтобы увидеть, что все таблицы созданы. (Если вы по-прежнему открыли **Обозреватель сервера** ранее, нажмите кнопку **Обновить** .)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

Не был создан класс модели для таблицы `CourseInstructor`. Как упоминалось ранее, это таблица соединений для связи «многие ко многим» между сущностями «`Instructor`» и «`Course`».

Щелкните правой кнопкой мыши таблицу `CourseInstructor` и выберите команду " **отобразить данные таблицы** ", чтобы убедиться, что она содержит данные в результате `Instructor` сущностей, добавленных в свойство навигации `Course.Instructors`.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>Сводка

Теперь у вас есть более сложная модель данных и соответствующая база данных. В следующем учебнике вы узнаете о различных способах доступа к связанным данным.

Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Назад](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Вперед](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
