---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: Обновление связанных данных с помощью Entity Framework в приложении ASP.NET MVC (6 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d29cb172d642b67947b461d1a7e55d01872bb8c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468288"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>Обновление связанных данных с помощью Entity Framework в приложении ASP.NET MVC (6 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущем учебнике отображаются связанные данные. в этом учебнике вы обновите связанные данные. Для большинства связей это можно сделать, обновив соответствующие поля внешнего ключа. Для связей «многие ко многим» Entity Framework не раскрывает таблицу соединений напрямую, поэтому необходимо явно добавлять и удалять сущности в соответствующих свойствах навигации.

На следующих рисунках изображены страницы, с которыми вы будете работать.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>Настройка страниц создания и редактирования для курсов

Создаваемая сущность курса должна иметь связь с существующей кафедрой. Чтобы упростить эту задачу, шаблонный код включает методы контроллеров, а также представления "Create" (Создание) и "Edit" (Редактирование) с раскрывающимся списком для выбора кафедры. Раскрывающийся список задает `Course.DepartmentID` свойство внешнего ключа, и это все Entity Framework потребности для загрузки свойства навигации `Department` с соответствующей сущностью `Department`. Вы будете использовать этот шаблонный код, немного его изменив, чтобы добавить обработку ошибок и сортировку раскрывающегося списка.

В *CourseController.CS*удалите четыре метода `Edit` и `Create` и замените их следующим кодом:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

Метод `PopulateDepartmentsDropDownList` возвращает список всех отделов, отсортированных по имени, создает коллекцию `SelectList` для раскрывающегося списка и передает коллекцию в представление в свойстве `ViewBag`. Этот метод принимает необязательный параметр `selectedDepartment`, позволяющий вызывающему коду указать элемент, который будет выбран при отрисовке раскрывающегося списка. Представление передаст имя `DepartmentID` [вспомогательному модулю `DropDownList`](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), а вспомогательный объект будет искать `SelectList` с именем `DepartmentID`в объекте `ViewBag`.

Метод `HttpGet` `Create` вызывает метод `PopulateDepartmentsDropDownList`, не устанавливая выбранный элемент, так как для нового курса этот отдел еще не установлен:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Метод `HttpGet` `Edit` задает выбранный элемент на основе идентификатора отдела, который уже назначен для изменяемого курса.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

Методы `HttpPost` для `Create` и `Edit` также содержат код, который задает выбранный элемент при повторном отображении страницы после ошибки:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Этот код гарантирует, что при повторном отображении страницы для отображения сообщения об ошибке выбранный отдел останется выбранным.

В *виевс\каурсе\креате.кштмл*Добавьте выделенный код, чтобы создать новое поле номера курса перед полем **Title** . Как объясняется в предыдущем учебнике, поля первичного ключа по умолчанию не обопределяются, но этот первичный ключ имеет смысл, поэтому пользователь должен иметь возможность ввести значение ключа.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

В *виевс\каурсе\едит.кштмл*, *виевс\каурсе\делете.кштмл*и *виевс\каурсе\детаилс.кштмл*добавьте поле номера курса перед полем **Title** . Так как это первичный ключ, он отображается, но его нельзя изменить.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

Запустите страницу **создать** (откройте страницу "Индекс курса" и щелкните **создать**) и введите данные для нового курса:

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

Нажмите кнопку **Создать**. Откроется страница индекс курса с новым курсом, добавленным в список. Название кафедры в списке страницы индекса поступает из свойства навигации, показывая, что связь установлена правильно.

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Откройте страницу **редактирования** (откройте страницу "Индекс курса" и щелкните **изменить** в курсе).

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Измените данные на странице и нажмите кнопку **Save** (Сохранить). Отобразится страница индекса курса с обновленными данными курса.

## <a name="adding-an-edit-page-for-instructors"></a>Добавление страницы редактирования для инструкторов

При редактировании записи преподавателя может потребоваться обновить назначенный преподавателю кабинет. Сущность `Instructor` имеет связь "один к нулю" или "одна к одному" с сущностью `OfficeAssignment`, что означает, что необходимо выполнять следующие ситуации:

- Если пользователь очищает назначение Office и изначально имел значение, необходимо удалить и удалить сущность `OfficeAssignment`.
- Если пользователь вводит значение назначения Office и изначально был пустым, необходимо создать новую сущность `OfficeAssignment`.
- Если пользователь изменяет значение назначения Office, необходимо изменить значение в существующей сущности `OfficeAssignment`.

Откройте *InstructorController.CS* и взгляните на метод `HttpGet` `Edit`:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Шаблон кода здесь не нужен. Настраивает данные для раскрывающегося списка, но вам понадобится текстовое поле. Замените этот метод следующим кодом:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Этот код удаляет оператор `ViewBag` и добавляет безотлагательную загрузку для связанной сущности `OfficeAssignment`. Вы не можете выполнить безотлагательную загрузку с помощью метода `Find`, поэтому вместо выбора инструктора используются методы `Where` и `Single`.

Замените метод `HttpPost` `Edit` следующим кодом. который обрабатывает обновления назначений Office:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Код делает следующее:

- Получает текущую сущность `Instructor` из базы данных, используя безотложную загрузку для свойства навигации `OfficeAssignment`. Это то же самое, что и в методе `HttpGet` `Edit`.
- Обновляет извлеченную сущность `Instructor`, используя значения из связывателя модели. Использование перегрузки [трюпдатемодел](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) позволяет *список разрешений* свойства, которые необходимо включить. Это предотвращает избыточное размещение, как описано во [втором учебнике](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- Если расположение офиса пусто, присваивает свойству `Instructor.OfficeAssignment` значение null, чтобы связанная строка в таблице `OfficeAssignment` была удалена.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- Сохраняет изменения в базу данных.

В *виевс\инструктор\едит.кштмл*после элементов `div` для поля **Дата найма** добавьте новое поле для редактирования расположения офиса:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

Запустите страницу (выберите вкладку **инструкторы** и нажмите кнопку **изменить** на инструкторе). Измените значение **Office Location** (Расположение кабинета) и нажмите кнопку **Save** (Сохранить).

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>Добавление назначений курсов на страницу редактирования инструкторов

Преподаватели могут вести любое число курсов. Теперь вы улучшите страницу редактирования преподавателя, добавив возможность изменять назначения курсов с помощью группы флажков, как показано на следующем снимке экрана:

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

Отношение между сущностями `Course` и `Instructor` является "многие ко многим". Это означает, что у вас нет прямого доступа к таблице соединений. Вместо этого вы добавите и удалите сущности в свойстве навигации `Instructor.Courses`.

Пользовательский интерфейс, позволяющий изменить назначенные для преподавателя курсы, представляет собой группу флажков. Отображается флажок для каждого курса в базе данных, а флажки для курсов, назначенных данному преподавателю, установлены. Пользователь может устанавливать и снимать флажки, изменяя назначения курсов. Если количество курсов было гораздо больше, вы, вероятно, захотите использовать другой метод представления данных в представлении, но для создания или удаления связей следует использовать один и тот же метод управления свойствами навигации.

Чтобы предоставить данные в представлении для списка флажков, нужно использовать класс модели представления. Создайте *AssignedCourseData.CS* в папке *ViewModels* и замените имеющийся код следующим кодом:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

В *InstructorController.CS*замените метод `HttpGet` `Edit` следующим кодом. Изменения выделены.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

Код добавляет безотложную загрузку для свойства навигации `Courses` и вызывает новый метод `PopulateAssignedCourseData` для предоставления сведений массиву флажков с помощью класса модели представления `AssignedCourseData`.

Код в методе `PopulateAssignedCourseData` считывает все `Course` сущности, чтобы загрузить список курсов с помощью класса модели представления. Для каждого курса код проверяет, существует ли этот курс в свойстве навигации `Courses` преподавателя. Чтобы создать эффективный поиск при проверке того, назначен ли курс инструктору, курсы, назначенные преподавателю, помещаются в коллекцию наборов [хэширования](https://msdn.microsoft.com/library/bb359438.aspx) . Для курсов, назначенных преподавателем, свойству `Assigned` присвоено значение `true`. Представление будет использовать это свойство, чтобы определить, какие флажки нужно отображать как выбранные. Наконец, список передается в представление в свойстве `ViewBag`.

Добавьте код, выполняемый, когда пользователь нажимает кнопку **Save** (Сохранить). Замените метод `HttpPost` `Edit` следующим кодом, который вызывает новый метод, который обновляет свойство навигации `Courses` сущности `Instructor`. Изменения выделены.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

Так как представление не содержит коллекцию сущностей `Course`, связыватель модели не может автоматически обновить свойство навигации `Courses`. Вместо использования связывателя модели для обновления свойства навигации по курсам это можно сделать в новом методе `UpdateInstructorCourses`. Поэтому нужно исключить свойство `Courses` из привязки модели. Это не требует внесения каких-либо изменений в код, вызывающий [трюпдатемодел](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) , так как используется перегрузка *список разрешений* , а `Courses` нет в списке включения.

Если флажки не выбраны, код в `UpdateInstructorCourses` инициализирует `Courses` свойство навигации пустой коллекцией:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

После этого код в цикле проходит по всем курсам в базе данных и сравнивает каждый из них с теми, которые сейчас назначены преподавателю, в противоположность тем, которые были выбраны в представлении. Чтобы упростить эффективную подстановку, последние две коллекции хранятся в объектах `HashSet`.

Если флажок для курса был установлен, но курс отсутствует в свойстве навигации `Instructor.Courses`, этот курс добавляется в коллекцию в свойстве навигации.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

Если флажок для курса не был установлен, но курс присутствует в свойстве навигации `Instructor.Courses`, этот курс удаляется из свойства навигации.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

В *виевс\инструктор\едит.кштмл*добавьте поле **Courses** с массивом флажков, добавив следующий выделенный код сразу после элементов `div` для поля `OfficeAssignment`:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

Этот код создает таблицу HTML с тремя столбцами. Каждый столбец содержит флажок, за которым идет заголовок с номером и названием курса. Все флажки имеют одно и то же имя ("selectedCourses"), которое информирует связыватель модели о том, что они должны рассматриваться как группа. Для атрибута `value` каждого флажка задано значение `CourseID.` при публикации страницы, связыватель модели передает массив контроллеру, который состоит из `CourseID` значений только выбранных флажков.

При первоначальном отображении флажков, которые предназначены для курсов, назначенных преподавателю, имеют `checked` атрибуты, которые выбирают их (отображает отмеченные).

После изменения назначений курсов необходимо проверить изменения при возврате сайта на страницу `Index`. Поэтому необходимо добавить столбец в таблицу на этой странице. В этом случае вам не нужно использовать объект `ViewBag`, так как отображаемая информация уже находится в свойстве навигации `Courses` сущности `Instructor`, которую вы передаете на страницу в качестве модели.

В *виевс\инструктор\индекс.кштмл*добавьте заголовок **курсов** сразу после заголовка **Office** , как показано в следующем примере:

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

Затем добавьте новую ячейку сведений сразу после ячейки сведений о местонахождении Office:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

Чтобы просмотреть курсы, назначенные каждому инструктору, выполните страницу " **индекс инструктора** ".

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

Щелкните **изменить** на лекторе, чтобы открыть страницу изменение.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

Измените некоторые назначения курсов и нажмите кнопку **сохранить**. Вносимые вами изменения отражаются на странице индекса.

 Примечание. подход, выполняемый для изменения данных курса преподавателя, хорошо работает при наличии ограниченного числа курсов. Для коллекций большего размера следовало бы применять другой пользовательский интерфейс и другой метод обновления.  

## <a name="update-the-delete-method"></a>Обновление метода Delete

Измените код в методе HttpPost DELETE, чтобы запись назначения Office (если она есть) была удалена при удалении преподавателя:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

При попытке удалить лектора, назначенного Отделу от имени администратора, вы получите ошибку ссылочной целостности. См. [текущую версию этого руководства](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) для дополнительного кода, который будет автоматически удалять лектора из любого отдела, в котором лектор назначен в качестве администратора.

## <a name="summary"></a>Сводка

Вы завершили это введение в работе с связанными данными. До сих пор в этих учебниках вы выполнили полный спектр операций CRUD, но вы не работали с проблемами параллелизма. В следующем учебнике будет представлен раздел параллелизма, описаны варианты его обработки и добавлена обработка параллелизма для кода CRUD, который вы уже написали для одного типа сущности.

Ссылки на другие Entity Framework ресурсы можно найти в конце [последнего учебника этой серии](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).

> [!div class="step-by-step"]
> [Назад](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Вперед](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
