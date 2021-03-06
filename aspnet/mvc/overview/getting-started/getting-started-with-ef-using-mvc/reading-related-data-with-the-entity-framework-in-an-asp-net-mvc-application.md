---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: Руководство. чтение связанных данных с помощью EF в приложении ASP.NET MVC
description: В этом учебнике вы прочитаете и отображаете связанные данные, то есть данные, которые Entity Framework загружает в свойства навигации.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445657"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a>Руководство. чтение связанных данных с помощью EF в приложении ASP.NET MVC

В предыдущем руководстве вы выполнили модель данных School. В этом учебнике вы прочитаете и отображаете связанные данные, то есть данные, которые Entity Framework загружает в свойства навигации.

На следующих рисунках изображены страницы, с которыми вы будете работать.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET MVC 5 с помощью Entity Framework 6 Code First и Visual Studio. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Загрузка связанных данных
> * Создание страницы курсов
> * Создание страницы преподавателей

## <a name="prerequisites"></a>Необходимые компоненты

* [Создание более сложной модели данных](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a>Загрузка связанных данных

Существует несколько способов, с помощью которых Entity Framework может загружать связанные данные в свойства навигации сущности:

- *Отложенная загрузка*. При первом чтении сущности связанные данные не извлекаются. Однако при первой попытке доступа к свойству навигации необходимые для этого свойства навигации данные извлекаются автоматически. В результате в базу данных отправляются несколько запросов — одна для самой сущности, а другая — каждый раз, когда необходимо извлечь связанные данные для сущности. Класс `DbContext` включает отложенную загрузку по умолчанию.

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *Безотложная загрузка*. При чтении сущности связанные данные извлекаются вместе с ней. Обычно такая загрузка представляет собой одиночный запрос с соединением, который получает все необходимые данные. Вы указываете безотлагательную загрузку с помощью метода `Include`.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *Явная загрузка*. Это похоже на отложенную загрузку за исключением того, что вы явно извлечете связанные данные в коде. Это не происходит автоматически при доступе к свойству навигации. Связанные данные загружаются вручную путем получения записи диспетчера состояний объектов для сущности и вызова метода [Collection. Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) для коллекций или метода [Reference. Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) для свойств, которые содержат одну сущность. (В следующем примере, если вы хотите загрузить свойство навигации администратора, замените `Collection(x => x.Courses)` `Reference(x => x.Administrator)`.) Обычно явная загрузка используется только в том случае, если отложенная загрузка отключена.

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

Поскольку они не извлекают значения свойств немедленно, отложенная загрузка и явная загрузка также называются *отложенной загрузкой*.

### <a name="performance-considerations"></a>Особенности производительности

Если известно, что связанные данные потребуются для каждой полученной сущности, то безотложная загрузка обычно обеспечивает наилучшую производительность, поскольку одиночный запрос к базе данных обычно эффективнее нескольких отдельных запросов для каждой полученной сущности. Например, в приведенных выше примерах Предположим, что у каждого отдела есть десять связанных курсов. Пример безотлагательной загрузки приведет к созданию всего одного запроса (join) и единого кругового пути к базе данных. Примеры отложенной загрузки и явной загрузки приведут к одиннадцати запросов и одиннадцати круговых путей к базе данных. При высокой задержке дополнительные циклы приема-передачи данных особенно сильно влияют на производительность.

С другой стороны, в некоторых сценариях отложенная загрузка более эффективна. Упреждающая загрузка может привести к созданию очень сложного объединения, что SQL Server не может эффективно обрабатываться. Или, если необходимо получить доступ к свойствам навигации сущности только для подмножества обрабатываемых сущностей, отложенная загрузка может работать лучше, так как безотлагательная загрузка получит больше данных, чем требуется. Если важна производительность, то для выбора наилучшего решения рекомендуется протестировать производительность для обоих случаев.

Отложенная загрузка может маскировать код, который вызывает проблемы с производительностью. Например, код, который не указывает безотлагательную или явную загрузку, но обрабатывает большой объем сущностей и использует несколько свойств навигации в каждой итерации, может оказаться очень неэффективным (из-за большого количества обращений к базе данных). Приложение, которое хорошо работает при разработке с использованием локального SQL Server, может столкнуться с проблемами производительности при перемещении в базу данных SQL Azure из-за увеличенной задержки и отложенной загрузки. Профилирование запросов к базе данных с реалистичной тестовой нагрузкой поможет определить, подходит ли отложенная загрузка. Дополнительные сведения см. в статье [пояснения Entity Framework стратегий: Загрузка связанных данных](https://msdn.microsoft.com/magazine/hh205756.aspx) и [использование Entity Framework для сокращения задержки сети до SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).

### <a name="disable-lazy-loading-before-serialization"></a>Отключить отложенную загрузку перед сериализацией

Если вы оставляете отложенную загрузку во время сериализации, вы можете запрашивать значительно больше данных, чем планировалось. Сериализация обычно работает путем доступа к каждому свойству в экземпляре типа. Доступ к свойству вызывает отложенную загрузку, и эти объекты с отложенной загрузкой сериализуются. Затем процесс сериализации обращается к каждому свойству сущностей с отложенной загрузкой, что может вызвать еще более отложенную загрузку и сериализацию. Чтобы предотвратить эту реакцию на цепочку размещения, отключите отложенную загрузку, прежде чем выполнять сериализацию сущности.

Сериализация также может быть усложнена классами прокси, используемыми Entity Framework, как описано в [руководстве по расширенным сценариям](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies).

Одним из способов избежать проблем с сериализацией является сериализация объектов передаваемых данных (DTO) вместо объектов сущностей, как показано в руководстве по [использованию веб-API с Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) .

Если вы не используете DTO, можно отключить отложенную загрузку и избежать проблем прокси-сервера, [отключив создание прокси-сервера](https://msdn.microsoft.com/data/jj592886.aspx).

Ниже приведены некоторые другие [способы отключения отложенной загрузки](https://msdn.microsoft.com/data/jj574232).

- Для конкретных свойств навигации опустить ключевое слово `virtual` при объявлении свойства.
- Для всех свойств навигации установите для `LazyLoadingEnabled` значение `false`, добавьте следующий код в конструктор класса контекста:

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a>Создание страницы курсов

Сущность `Course` включает свойство навигации, которое содержит `Department`ную сущность отдела, которому назначен курс. Чтобы отобразить имя назначенного отдела в списке курсов, необходимо получить свойство `Name` из сущности `Department`, которая находится в свойстве навигации `Course.Department`.

Создайте контроллер с именем `CourseController` (не Каурсесконтроллер) для типа сущности `Course`, используя те же параметры **контроллера MVC 5 с представлениями, используя Entity Frameworkный** механизм формирования шаблонов, который выполнялся ранее для контроллера `Student`.

| Параметр | значения |
| ------- | ----- |
| Класс Model | Выберите **курс (ContosoUniversity. Models)** . |
| Класс контекста данных | Выберите **SchoolContext (ContosoUniversity. DAL)** . |
| Имя контроллера | Введите *каурсеконтроллер*. Опять же, не *каурсесконтроллер* с *s*. При выборе **курса (ContosoUniversity. Models)** значение **имени контроллера** заполняется автоматически. Необходимо изменить значение. |

Оставьте другие значения по умолчанию и добавьте контроллер.

Откройте *контроллерс\каурсеконтроллер.КС* и взгляните на метод `Index`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

В автоматически сформированном шаблоне установлена безотложная загрузка свойства навигации `Department` при помощи метода `Include`.

Откройте *виевс\каурсе\индекс.кштмл* и замените код шаблона следующим кодом. Изменения выделены:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

Мы внесли следующие изменения в код шаблона:

- Изменен заголовок с **индекса** на **курсы**.
- Добавлен столбец **Number** (Номер), отображающий значение свойства `CourseID`. По умолчанию первичные ключи не имеют шаблонов, так как обычно они не имеют смысла для конечных пользователей. Однако в нашем случае первичный ключ имеет смысл, и мы хотим его отобразить.
- Переместил столбец **Department** на правую сторону и изменил его заголовок. Шаблон правильно выбрал для вывода свойства `Name` из сущности `Department`, но здесь на странице курса заголовок столбца должен быть " **Отдел** ", а не " **имя**".

Обратите внимание, что для столбца отдел в шаблонном коде отображается свойство `Name` сущности `Department`, которая загружается в свойство навигации `Department`.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

Запустите страницу (перейдите на вкладку **курсы** на домашней странице университета Contoso), чтобы просмотреть список с названиями отделов.

## <a name="create-an-instructors-page"></a>Создание страницы преподавателей

В этом разделе вы создадите контроллер и представление для сущности `Instructor`, чтобы отобразить страницу инструкторов. Эта страница считывает и отображает связанные данные следующим образом:

- В списке преподавателей отображаются связанные данные из сущности `OfficeAssignment`. Между сущностями `Instructor` и `OfficeAssignment` действует связь один к нулю или к одному. Вы будете использовать безотлагательную загрузку для сущностей `OfficeAssignment`. Как упоминалось ранее, безотложная загрузка обычно эффективнее при получении связанных данных для всех строк главной таблицы. В нашем случае мы хотим отобразить принадлежность к кабинету для каждого преподавателя.
- Когда пользователь выбирает преподавателя, отображаются связанные сущности `Course`. Между сущностями `Instructor` и `Course` действует связь многие ко многим. Вы будете использовать безотлагательную загрузку для сущностей `Course` и связанных с ними сущностей `Department`. В этом случае отложенная загрузка может быть более эффективной, так как вам нужны курсы только для выбранного преподавателя. Этот пример, однако, показывает, как использовать безотложную загрузку для свойств навигации сущностей, которые сами находятся в свойствах навигации.
- Когда пользователь выбирает курс, отображаются связанные данные из `Enrollments` набора сущностей. Между сущностями `Course` и `Enrollment` действует связь один ко многим. Вы добавите явную загрузку для сущностей `Enrollment` и связанных с ними сущностей `Student`. (Явная загрузка не требуется, так как отложенная загрузка включена, но в этом примере показано, как выполнить явную загрузку.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>Создание модели представления для представления индекса инструктора

На странице инструкторы показаны три различные таблицы. Таким образом, мы создаем модель представления, которая включает три свойства, каждое из которых содержит данные из одной таблицы.

В папке *ViewModels* создайте *InstructorIndexData.CS* и замените имеющийся код следующим кодом:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>Создание контроллера и представлений преподавателя

Создание контроллера `InstructorController` (не Инструкторсконтроллер) с помощью операции чтения и записи EF:

| Параметр | значения |
| ------- | ----- |
| Класс Model | Выберите **Instructor (ContosoUniversity. Models)** . |
| Класс контекста данных | Выберите **SchoolContext (ContosoUniversity. DAL)** . |
| Имя контроллера | Введите *инструкторконтроллер*. Опять же, не *инструкторсконтроллер* с *s*. При выборе **курса (ContosoUniversity. Models)** значение **имени контроллера** заполняется автоматически. Необходимо изменить значение. |

Оставьте другие значения по умолчанию и добавьте контроллер.

Откройте *контроллерс\инструкторконтроллер.КС* и добавьте оператор `using` для пространства имен `ViewModels`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

Шаблонный код в методе `Index` указывает безотлагательную загрузку только для свойства навигации `OfficeAssignment`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Замените метод `Index` следующим кодом, чтобы загрузить дополнительные связанные данные и разместить их в модели представления:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Метод принимает необязательные данные маршрута (`id`) и параметр строки запроса (`courseID`), который предоставляет значения ИДЕНТИФИКАТОРов выбранного преподавателя и выбранного курса, а также передает все необходимые данные в представление. Параметры передаются гиперссылками **Select** на странице.

Код начинается с создания экземпляра модели представления и помещения его в список преподавателей. В коде указывается упреждающая загрузка для `Instructor.OfficeAssignment` и свойства навигации `Instructor.Courses`.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

Второй метод `Include` загружает курсы, и для каждого загруженного курса выполняется упреждающая загрузка для свойства навигации `Course.Department`.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

Как упоминалось ранее, безотлагательная загрузка не требуется, но выполняется для повышения производительности. Так как для представления всегда требуется сущность `OfficeAssignment`, ее более эффективно получить в том же запросе. `Course` сущности необходимы, когда лектор выбран на веб-странице, поэтому безотлагательная загрузка лучше, чем ленивая, только в том случае, если страница отображается чаще, если курс выбран по меньшей мере.

Если был выбран идентификатор преподавателя, выбранный лектор извлекается из списка инструкторов в модели представления. Затем свойство `Courses` модели представления загружается с сущностями `Course` из свойства навигации `Courses`ного преподавателя.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

Метод `Where` Возвращает коллекцию, но в данном случае условия, передаваемые этому методу, приводят к возврату только одной сущности `Instructor`. Метод `Single` Преобразует коллекцию в единую `Instructor` сущность, которая предоставляет доступ к свойству `Courses` этой сущности.

Если известно, что коллекция будет содержать только один элемент, то для коллекции используется [единственный](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) метод. Метод `Single` создает исключение, если переданный в него набор пуст или если коллекция содержит более одного элемента. Альтернативой является [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), который возвращает значение по умолчанию (`null` в данном случае), если коллекция пуста. Однако в этом случае, что может привести к исключению (при попытке найти свойство `Courses` в `null` ссылке), и сообщение об исключении будет менее ясно указывать на причину проблемы. При вызове метода `Single` можно также передать условие `Where`, а не вызывать метод `Where` отдельно:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

вместо следующего кода:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

Далее, если был выбран курс, то он получается из списка курсов модели представления. Затем свойство `Enrollments` модели представления загружается с сущностями `Enrollment` из свойства навигации `Enrollments` этого курса.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>Изменение представления индекса преподавателя

В *виевс\инструктор\индекс.кштмл*замените код шаблона следующим кодом. Изменения выделены:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

Мы внесли следующие изменения в существующий код:

- Изменили класс модели на `InstructorIndexData`.
- Изменили заголовок страницы с **Index** на **Instructors**.
- Добавлен столбец **Office** , отображающий `item.OfficeAssignment.Location` только в том случае, если `item.OfficeAssignment` не имеет значение null. (Поскольку это связь "один к нулю" или "одна к одному", то связанная сущность `OfficeAssignment` может отсутствовать.)

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- Добавлен код, который динамически добавляет `class="success"` в элемент `tr` выбранного преподавателя. Это задает цвет фона для выбранной строки с помощью класса [начальной загрузки](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) .

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- Добавлен новый `ActionLink` с меткой **SELECT** непосредственно перед другими ссылками в каждой строке, что приводит к отправке выбранного идентификатора лектора в метод `Index`.

Запустите приложение и перейдите на вкладку **инструкторы** . На странице отображается `Location` свойство связанных сущностей `OfficeAssignment` и пустая ячейка таблицы, если нет связанной сущности `OfficeAssignment`.

В файле *виевс\инструктор\индекс.кштмл* после закрывающего элемента `table` (в конце файла) добавьте следующий код. Этот код отображает список связанных с преподавателем курсов, когда преподаватель выбран.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

Этот код считывает свойство `Courses` модели представления для отображения списка курсов. Он также предоставляет `Select`ную гиперссылку, которая отправляет идентификатор выбранного курса в метод действия `Index`.

Запустите страницу и выберите лектора. Вы увидите сетку, которая отображает курсы, назначенные выбранному преподавателю, и для каждого курса отобразится имя связанного факультета.

После только что добавленного блока кода добавьте следующий код. Он отображает список студентов, которые зачислены на курс при выборе этого курса.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

Этот код считывает свойство `Enrollments` модели представления, чтобы отобразить список учащихся, зарегистрированных в курсе.

Запустите страницу и выберите лектора. Затем выберите курс, чтобы увидеть список зачисленных студентов и их оценки.

### <a name="adding-explicit-loading"></a>Добавление явной загрузки

Откройте *InstructorController.CS* и посмотрите, как метод `Index` получает список регистраций для выбранного курса:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

При получении списка инструкторов вы указали безотлагательную загрузку для свойства навигации `Courses` и для свойства `Department` каждого курса. Затем вы помещаете `Courses` коллекцию в модель представления, и теперь доступ к свойству навигации `Enrollments` из одной сущности в этой коллекции. Поскольку для свойства навигации `Course.Enrollments` не указана безотлагательная загрузка, данные из этого свойства отображаются на странице в результате отложенной загрузки.

Если вы отключили отложенную загрузку, не изменяя код каким бы то ни было другим способом, свойство `Enrollments` будет иметь значение NULL вне зависимости от количества регистраций, которые фактически имелися в курсе. В этом случае, чтобы загрузить свойство `Enrollments`, необходимо указать либо безотлагательную загрузку, либо явную загрузку. Вы уже знаете, как выполнить безотлагательную загрузку. Чтобы увидеть пример явной загрузки, замените метод `Index` следующим кодом, который явно загружает свойство `Enrollments`. Измененный код выделяется.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

После получения выбранной `Course` сущности новый код явно загружает свойство навигации `Enrollments` курса:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

Затем он явным образом загружает сущность `Student`, связанную с сущностью `Enrollment`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

Обратите внимание, что для загрузки свойства коллекции используется метод `Collection`, но для свойства, содержащего только одну сущность, используется метод `Reference`.

Запустите страницу индекс преподавателя, и вы увидите, что на странице нет различий, хотя вы изменили то, как извлекаются данные.

## <a name="get-the-code"></a>Получите код

[Скачать завершенный проект](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Дополнительные ресурсы

Ссылки на другие ресурсы Entity Framework можно найти в [ресурсах, рекомендуемых для доступа к данным ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Следующие шаги

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Дополнительные сведения о загрузке связанных данных
> * Создание страницы курсов
> * Создание страницы преподавателей

В следующем руководстве описано, как обновить связанные данные.

> [!div class="nextstepaction"]
> [Обновление связанных данных](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
