---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: Чтение связанных данных с помощью Entity Framework в приложении ASP.NET MVC (5 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e1752022b66952783039fbea0c2880e2f9be6ef8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595214"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a>Чтение связанных данных с помощью Entity Framework в приложении ASP.NET MVC (5 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущем руководстве вы выполнили модель данных School. В этом учебнике вы прочитаете и отображаете связанные данные, то есть данные, которые Entity Framework загружает в свойства навигации.

На следующих рисунках изображены страницы, с которыми вы будете работать.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>Отложенная, безотлагательная и явная загрузка связанных данных

Существует несколько способов, с помощью которых Entity Framework может загружать связанные данные в свойства навигации сущности:

- *Отложенная загрузка*. При первом чтении сущности связанные данные не извлекаются. Однако при первой попытке доступа к свойству навигации необходимые для этого свойства навигации данные извлекаются автоматически. В результате в базу данных отправляются несколько запросов — одна для самой сущности, а другая — каждый раз, когда необходимо извлечь связанные данные для сущности. 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *Безотложная загрузка*. При чтении сущности связанные данные извлекаются вместе с ней. Обычно такая загрузка представляет собой одиночный запрос с соединением, который получает все необходимые данные. Вы указываете безотлагательную загрузку с помощью метода `Include`.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *Явная загрузка*. Это похоже на отложенную загрузку за исключением того, что вы явно извлечете связанные данные в коде. Это не происходит автоматически при доступе к свойству навигации. Связанные данные загружаются вручную путем получения записи диспетчера состояний объектов для сущности и вызова метода `Collection.Load` для коллекций или метода `Reference.Load` для свойств, содержащих одну сущность. (В следующем примере, если вы хотите загрузить свойство навигации администратора, замените `Collection(x => x.Courses)` `Reference(x => x.Administrator)`.)

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

Поскольку они не извлекают значения свойств немедленно, отложенная загрузка и явная загрузка также называются *отложенной загрузкой*.

Как правило, если известно, что для каждой полученной сущности необходимы связанные данные, безотлагательная загрузка обеспечивает наилучшую производительность, поскольку один запрос, отправленный в базу данных, обычно более эффективен, чем отдельные запросы для каждой полученной сущности. Например, в приведенных выше примерах Предположим, что у каждого отдела есть десять связанных курсов. Пример безотлагательной загрузки приведет к созданию всего одного запроса (join) и единого кругового пути к базе данных. Примеры отложенной загрузки и явной загрузки приведут к одиннадцати запросов и одиннадцати круговых путей к базе данных. При высокой задержке дополнительные циклы приема-передачи данных особенно сильно влияют на производительность.

С другой стороны, в некоторых сценариях отложенная загрузка более эффективна. Упреждающая загрузка может привести к созданию очень сложного объединения, что SQL Server не может эффективно обрабатываться. Или, если необходимо получить доступ к свойствам навигации сущности только для подмножества обрабатываемых сущностей, отложенная загрузка может работать лучше, поскольку безотлагательная загрузка будет извлекать больше данных, чем требуется. Если важна производительность, то для выбора наилучшего решения рекомендуется протестировать производительность для обоих случаев.

Обычно явная загрузка используется только в том случае, если отложенная загрузка отключена. Один из сценариев, когда следует отключить отложенную загрузку, — во время сериализации. Отложенная загрузка и сериализация не занимают много времени, и если вы не следите за тем, чтобы запросить значительно больше данных, чем планировалось, если включена отложенная загрузка. Сериализация обычно работает путем доступа к каждому свойству в экземпляре типа. Доступ к свойству вызывает отложенную загрузку, и эти объекты с отложенной загрузкой сериализуются. Затем процесс сериализации обращается к каждому свойству сущностей с отложенной загрузкой, что может вызвать еще более отложенную загрузку и сериализацию. Чтобы предотвратить эту реакцию на цепочку размещения, отключите отложенную загрузку, прежде чем выполнять сериализацию сущности.

Класс контекста базы данных по умолчанию выполняет отложенную загрузку. Отложенную загрузку можно отключить двумя способами.

- Для конкретных свойств навигации опустить ключевое слово `virtual` при объявлении свойства.
- Для всех свойств навигации задайте для параметра `LazyLoadingEnabled` значение `false`. Например, можно разместить следующий код в конструкторе класса контекста: 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Отложенная загрузка может маскировать код, который вызывает проблемы с производительностью. Например, код, который не указывает безотлагательную или явную загрузку, но обрабатывает большой объем сущностей и использует несколько свойств навигации в каждой итерации, может оказаться очень неэффективным (из-за большого количества обращений к базе данных). Приложение, которое хорошо работает при разработке с использованием локального SQL Server, может столкнуться с проблемами производительности при перемещении в базу данных SQL Azure из-за увеличенной задержки и отложенной загрузки. Профилирование запросов к базе данных с реалистичной тестовой нагрузкой поможет определить, подходит ли отложенная загрузка. Дополнительные сведения см. в статье [пояснения Entity Framework стратегий: Загрузка связанных данных](https://msdn.microsoft.com/magazine/hh205756.aspx) и [использование Entity Framework для сокращения задержки сети до SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).

## <a name="create-a-courses-index-page-that-displays-department-name"></a>Создание страницы индекса курсов, в которой отображается название отдела

Сущность `Course` включает свойство навигации, которое содержит `Department`ную сущность отдела, которому назначен курс. Чтобы отобразить имя назначенного отдела в списке курсов, необходимо получить свойство `Name` из сущности `Department`, которая находится в свойстве навигации `Course.Department`.

Создайте контроллер с именем `CourseController` для типа сущности `Course`, используя те же параметры, которые были выполнены ранее для контроллера `Student`, как показано на следующем рисунке (за исключением того, что в отличие от изображения, класс контекста находится в пространстве имен DAL, а не в пространстве имен Models):

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

Откройте *контроллерс\каурсеконтроллер.КС* и взгляните на метод `Index`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

В автоматически сформированном шаблоне установлена безотложная загрузка свойства навигации `Department` при помощи метода `Include`.

Откройте *виевс\каурсе\индекс.кштмл* и замените существующий код следующим кодом. Изменения выделены:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

Мы внесли следующие изменения в код шаблона:

- Изменен заголовок с **индекса** на **курсы**.
- Перемещены строки слева.
- Добавлен столбец под **номером** заголовка, который показывает значение свойства `CourseID`. (По умолчанию первичные ключи не имеют шаблонов, так как обычно они не имеют смысла для конечных пользователей. Однако в этом случае первичный ключ имеет смысл и его необходимо отобразить.)
- Изменен заголовок последнего столбца с **DepartmentID** (имя внешнего ключа для сущности `Department`) на **отдел**.

Обратите внимание, что для последнего столбца сформированный код отображает свойство `Name` сущности `Department`, которая загружается в свойство `Department` навигации:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

Запустите страницу (перейдите на вкладку **курсы** на домашней странице университета Contoso), чтобы просмотреть список с названиями отделов.

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a>Создание страницы индекса инструкторов, в которой показаны курсы и регистрации

В этом разделе вы создадите контроллер и представление для сущности `Instructor`, чтобы отобразить страницу индекса инструкторов:

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Эта страница считывает и отображает связанные данные следующим образом:

- В списке преподавателей отображаются связанные данные из сущности `OfficeAssignment`. Между сущностями `Instructor` и `OfficeAssignment` действует связь один к нулю или к одному. Вы будете использовать безотлагательную загрузку для сущностей `OfficeAssignment`. Как упоминалось ранее, безотложная загрузка обычно эффективнее при получении связанных данных для всех строк главной таблицы. В нашем случае мы хотим отобразить принадлежность к кабинету для каждого преподавателя.
- Когда пользователь выбирает преподавателя, отображаются связанные сущности `Course`. Между сущностями `Instructor` и `Course` действует связь многие ко многим. Вы будете использовать безотлагательную загрузку для сущностей `Course` и связанных с ними сущностей `Department`. В этом случае отложенная загрузка может быть более эффективной, так как вам нужны курсы только для выбранного преподавателя. Этот пример, однако, показывает, как использовать безотложную загрузку для свойств навигации сущностей, которые сами находятся в свойствах навигации.
- Когда пользователь выбирает курс, отображаются связанные данные из `Enrollments` набора сущностей. Между сущностями `Course` и `Enrollment` действует связь один ко многим. Вы добавите явную загрузку для сущностей `Enrollment` и связанных с ними сущностей `Student`. (Явная загрузка не требуется, так как отложенная загрузка включена, но в этом примере показано, как выполнить явную загрузку.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>Создание модели представления для представления индекса инструктора

На странице «индекс преподавателя» показаны три различные таблицы. Таким образом, мы создаем модель представления, которая включает три свойства, каждое из которых содержит данные из одной таблицы.

В папке *ViewModels* создайте *InstructorIndexData.CS* и замените имеющийся код следующим кодом:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a>Добавление стиля для выбранных строк

Чтобы пометить выбранные строки, требуется другой цвет фона. Чтобы предоставить стиль для этого пользовательского интерфейса, добавьте следующий выделенный код в раздел `/* info and errors */` в *контент\сите.КСС*, как показано ниже:

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a>Создание контроллера и представлений преподавателя

Создайте контроллер `InstructorController`, как показано на следующем рисунке.

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

Откройте *контроллерс\инструкторконтроллер.КС* и добавьте оператор `using` для пространства имен `ViewModels`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Шаблонный код в методе `Index` указывает безотлагательную загрузку только для свойства навигации `OfficeAssignment`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Замените метод `Index` следующим кодом, чтобы загрузить дополнительные связанные данные и разместить их в модели представления:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Метод принимает необязательные данные маршрута (`id`) и параметр строки запроса (`courseID`), который предоставляет значения ИДЕНТИФИКАТОРов выбранного преподавателя и выбранного курса, а также передает все необходимые данные в представление. Параметры передаются гиперссылками **Select** на странице.

> [!TIP]
> 
> **Данные маршрута**
> 
> Данные маршрута — это данные, которые связыватель модели обнаружил в сегменте URL-адреса, указанном в таблице маршрутизации. Например, маршрут по умолчанию определяет сегменты `controller`, `action`и `id`:
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> В следующем URL-адресе карта маршрута по умолчанию `Instructor` как `controller`, `Index` как `action` и 1 в качестве `id`. Это значения данных маршрута.
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> "? courseID = 2021" — это значение строки запроса. Связыватель модели также будет работать при передаче `id` как значения строки запроса:
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> URL-адреса создаются `ActionLink` инструкциями в представлении Razor. В следующем коде параметр `id` соответствует маршруту по умолчанию, поэтому `id` добавляется в данные маршрута.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> В следующем коде `courseID` не соответствует параметру в маршруте по умолчанию, поэтому он добавляется как строка запроса.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

Код начинается с создания экземпляра модели представления и помещения его в список преподавателей. В коде указывается упреждающая загрузка для `Instructor.OfficeAssignment` и свойства навигации `Instructor.Courses`.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

Второй метод `Include` загружает курсы, и для каждого загруженного курса выполняется упреждающая загрузка для свойства навигации `Course.Department`.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

Как упоминалось ранее, безотлагательная загрузка не требуется, но выполняется для повышения производительности. Так как для представления всегда требуется сущность `OfficeAssignment`, ее более эффективно получить в том же запросе. `Course` сущности необходимы, когда лектор выбран на веб-странице, поэтому безотлагательная загрузка лучше, чем ленивая, только в том случае, если страница отображается чаще, если курс выбран по меньшей мере.

Если был выбран идентификатор преподавателя, выбранный лектор извлекается из списка инструкторов в модели представления. Затем свойство `Courses` модели представления загружается с сущностями `Course` из свойства навигации `Courses`ного преподавателя.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

Метод `Where` Возвращает коллекцию, но в данном случае условия, передаваемые этому методу, приводят к возврату только одной сущности `Instructor`. Метод `Single` Преобразует коллекцию в единую `Instructor` сущность, которая предоставляет доступ к свойству `Courses` этой сущности.

Если известно, что коллекция будет содержать только один элемент, то для коллекции используется [единственный](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) метод. Метод `Single` создает исключение, если переданный в него набор пуст или если коллекция содержит более одного элемента. Альтернативой является [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), который возвращает значение по умолчанию (`null` в данном случае), если коллекция пуста. Однако в этом случае, что может привести к исключению (при попытке найти свойство `Courses` в `null` ссылке), и сообщение об исключении будет менее ясно указывать на причину проблемы. При вызове метода `Single` можно также передать условие `Where`, а не вызывать метод `Where` отдельно:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

Вместо этого:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

Далее, если был выбран курс, то он получается из списка курсов модели представления. Затем свойство `Enrollments` модели представления загружается с сущностями `Enrollment` из свойства навигации `Enrollments` этого курса.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a>Изменение представления индекса инструктора

В *виевс\инструктор\индекс.кштмл*замените существующий код следующим кодом. Изменения выделены:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

Мы внесли следующие изменения в существующий код:

- Изменили класс модели на `InstructorIndexData`.
- Изменили заголовок страницы с **Index** на **Instructors**.
- Столбцы связи строк перемещены влево.
- Удален столбец **FullName** .
- Добавлен столбец **Office** , отображающий `item.OfficeAssignment.Location` только в том случае, если `item.OfficeAssignment` не имеет значение null. (Поскольку это связь "один к нулю" или "одна к одному", то связанная сущность `OfficeAssignment` может отсутствовать.) 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- Добавлен код, который динамически добавляет `class="selectedrow"` в элемент `tr` выбранного преподавателя. Это задает цвет фона для выбранной строки с помощью созданного ранее класса CSS. (Атрибут `valign` будет полезен в следующем учебнике при добавлении столбца с несколькими строками в таблицу.) 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- Добавлен новый `ActionLink` с меткой **SELECT** непосредственно перед другими ссылками в каждой строке, что приводит к отправке выбранного идентификатора лектора в метод `Index`.

Запустите приложение и перейдите на вкладку **инструкторы** . На странице отображается `Location` свойство связанных сущностей `OfficeAssignment` и пустая ячейка таблицы, если нет связанной сущности `OfficeAssignment`.

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

В файле *виевс\инструктор\индекс.кштмл* после закрывающего элемента `table` (в конце файла) добавьте следующий выделенный код. При выборе лектора отображается список курсов, связанных с преподавателем.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

Этот код считывает свойство `Courses` модели представления для отображения списка курсов. Он также предоставляет `Select`ную гиперссылку, которая отправляет идентификатор выбранного курса в метод действия `Index`.

> [!NOTE]
> *CSS* -файл кэшируется браузерами. Если вы не видите изменения при запуске приложения, выполните жесткое обновление (удерживая нажатой клавишу CTRL при нажатии кнопки **Обновить** или нажмите клавиши CTRL + F5).

Запустите страницу и выберите лектора. Вы увидите сетку, которая отображает курсы, назначенные выбранному преподавателю, и для каждого курса отобразится имя связанного факультета.

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

После только что добавленного блока кода добавьте следующий код. Он отображает список студентов, которые зачислены на курс при выборе этого курса.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

Этот код считывает свойство `Enrollments` модели представления, чтобы отобразить список учащихся, зарегистрированных в курсе.

Запустите страницу и выберите лектора. Затем выберите курс, чтобы увидеть список зачисленных студентов и их оценки.

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a>Добавление явной загрузки

Откройте *InstructorController.CS* и посмотрите, как метод `Index` получает список регистраций для выбранного курса:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

При получении списка инструкторов вы указали безотлагательную загрузку для свойства навигации `Courses` и для свойства `Department` каждого курса. Затем вы помещаете `Courses` коллекцию в модель представления, и теперь доступ к свойству навигации `Enrollments` из одной сущности в этой коллекции. Поскольку для свойства навигации `Course.Enrollments` не указана безотлагательная загрузка, данные из этого свойства отображаются на странице в результате отложенной загрузки.

Если вы отключили отложенную загрузку, не изменяя код каким бы то ни было другим способом, свойство `Enrollments` будет иметь значение NULL вне зависимости от количества регистраций, которые фактически имелися в курсе. В этом случае, чтобы загрузить свойство `Enrollments`, необходимо указать либо безотлагательную загрузку, либо явную загрузку. Вы уже знаете, как выполнить безотлагательную загрузку. Чтобы увидеть пример явной загрузки, замените метод `Index` следующим кодом, который явно загружает свойство `Enrollments`. Измененный код выделяется.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

После получения выбранной `Course` сущности новый код явно загружает свойство навигации `Enrollments` курса:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

Затем он явным образом загружает сущность `Student`, связанную с сущностью `Enrollment`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

Обратите внимание, что для загрузки свойства коллекции используется метод `Collection`, но для свойства, содержащего только одну сущность, используется метод `Reference`. Вы можете запустить страницу индекса инструктора, и вы не увидите никаких различий в том, что отображается на странице, хотя вы изменили способ извлечения данных.

## <a name="summary"></a>Сводка

Теперь вы использовали все три способа (Lazy, безотлагательные и явные) для загрузки связанных данных в свойства навигации. В следующем руководстве вы узнаете, как обновлять связанные данные.

Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Назад](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [Вперед](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
