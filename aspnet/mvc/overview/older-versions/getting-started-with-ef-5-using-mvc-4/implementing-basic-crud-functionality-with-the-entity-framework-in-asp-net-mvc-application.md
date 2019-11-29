---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: Реализация базовых функций CRUD с помощью Entity Framework в приложении ASP.NET MVC (2 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: eba146d2975e0dcf243facf7c205c4acfe40b6f6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595325"
---
# <a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>Реализация базовых функций CRUD с помощью Entity Framework в приложении ASP.NET MVC (2 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущем учебном курсе было создано приложение MVC, которое хранит и отображает данные с помощью Entity Framework и SQL Server LocalDB. В этом учебнике вы просматриваете и настраиваете код CRUD (создание, чтение, обновление и удаление), который автоматически создается формированием шаблонов MVC в контроллерах и представлениях.

> [!NOTE]
> Широко распространена практика реализации шаблона репозитория, позволяющего создать уровень абстракции между контроллером и уровнем доступа к данным. Чтобы не усложнять эти учебники, вы не будете реализовывать репозиторий до последующего учебника в этой серии.

В этом руководстве вы создадите следующие веб-страницы:

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>Создание страницы сведений

Шаблонный код для `Index`ной страницы учащихся оставил свойство `Enrollments`, так как это свойство содержит коллекцию. На странице `Details` отобразится содержимое коллекции в таблице HTML.

 В *контроллерс\студентконтроллер.КС*метод действия для представления `Details` использует метод `Find` для получения одной `Student` сущности. 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 Значение ключа передается в метод в качестве параметра `id` и берется из данных маршрута в гиперссылке **Details** на странице индекса. 

1. Откройте *виевс\студент\детаилс.кштмл*. Каждое поле отображается с помощью вспомогательного метода `DisplayFor`, как показано в следующем примере: 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. После поля `EnrollmentDate` и непосредственно перед закрывающим тегом `fieldset` добавьте код для отображения списка регистраций, как показано в следующем примере:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    Этот код циклически обрабатывает сущности в свойстве навигации `Enrollments`. Для каждой сущности `Enrollment` в свойстве отображается название и оценка курса. Заголовок курса извлекается из `Course` сущности, которая хранится в свойстве навигации `Course` сущности `Enrollments`. Все эти данные извлекаются из базы данных автоматически, когда это необходимо. (Иными словами, вы используете отложенную загрузку здесь. Не указана *упреждающая загрузка* для свойства навигации `Courses`, поэтому при первом обращении к этому свойству запрос отправляется в базу данных для получения данных. Дополнительные сведения о отложенной загрузке и безотлагательной загрузке см. в руководстве по [чтению связанных данных](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) далее в этой серии.)
3. Запустите страницу, выбрав вкладку **students (учащиеся** ) и щелкнув ссылку **Details (сведения** ) для Александр Carson. Откроется список курсов и оценок для выбранного учащегося:

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>Обновление страницы создания

1. В *контроллерс\студентконтроллер.КС*замените метод действия `HttpPost``Create` следующим кодом, чтобы добавить `try-catch` блок и [атрибут привязки](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) в шаблонный метод: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    Этот код добавляет сущность `Student`, созданную связывателем модели MVC ASP.NET, в `Students` набор сущностей, а затем сохраняет изменения в базе данных. (*Связыватель модели* относится к функции MVC ASP.NET, которая упрощает работу с данными, передаваемыми с помощью формы. связыватель модели преобразует отправленные значения формы в типы CLR и передает их в метод действия в параметрах. В этом случае связыватель модели создает экземпляр `Student` сущности, используя значения свойств из коллекции `Form`.)

    Атрибут `ValidateAntiForgeryToken` помогает предотвратить атаки [подделки межсайтовых запросов](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) .

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.cshtml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. Запустите страницу, выбрав вкладку **students (учащиеся** ) и нажав кнопку **создать**.

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    Некоторые проверки данных работают по умолчанию. Введите имена и недопустимую дату и нажмите кнопку **создать** , чтобы просмотреть сообщение об ошибке.

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    В следующем выделенном коде показана проверка модели.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    Измените дату на допустимое значение, например 9/1/2005, и нажмите кнопку **создать** , чтобы увидеть новый учащийся на странице **индекса** .

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>Обновление страницы редактирования записей

В *контроллерс\студентконтроллер.КС*метод `HttpGet` `Edit` (то есть без атрибута `HttpPost`) использует метод `Find` для получения выбранной `Student` сущности, как показано в методе `Details`. Изменять этот метод не нужно.

Однако замените метод действия `HttpPost` `Edit` следующим кодом, чтобы добавить блок `try-catch` и [атрибут BIND](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx):

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

Этот код похож на тот, который вы видели в методе `HttpPost` `Create`. Однако вместо добавления сущности, созданной связывателем модели, в набор сущностей этот код задает для сущности флаг, указывающий, что она была изменена. При вызове метода [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) [измененный](https://msdn.microsoft.com/library/system.data.entitystate.aspx) флаг заставляет Entity Framework создавать инструкции SQL для обновления строки базы данных. Будут обновлены все столбцы строки базы данных, включая те, которые не изменялись пользователем, а конфликты параллелизма игнорируются. (Вы узнаете, как работать с параллелизмом в последующем учебнике этой серии.)

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>Состояния сущностей и методы присоединения и SaveChanges

Контекст базы данных отслеживает состояние синхронизации сущностей в памяти с соответствующими им строками в базе данных. Данные отслеживания определяют, что происходит при вызове метода `SaveChanges`. Например, при передаче новой сущности в метод [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) состояние этой сущности задается равным `Added`. Затем при вызове метода [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) контекст базы данных выдает команду SQL `INSERT`.

Сущность может находиться в одном из[следующих состояний](https://msdn.microsoft.com/library/system.data.entitystate.aspx):

- `Added`. Сущность еще не существует в базе данных. Метод `SaveChanges` должен выдать инструкцию `INSERT`.
- `Unchanged`. С этой сущностью не нужно выполнять никакие действия с помощью метода `SaveChanges`. Это начальный статус сущности, который она имеет при чтении из базы данных.
- `Modified`. Были изменены значения некоторых или всех свойств сущности. Метод `SaveChanges` должен выдать инструкцию `UPDATE`.
- `Deleted`. Сущность отмечена для удаления. Метод `SaveChanges` должен выдать инструкцию `DELETE`.
- `Detached`. Сущность не отслеживается контекстом базы данных.

В классическом приложении изменения состояния обычно осуществляются автоматически. В приложении типа Desktop вы читаете сущность и вносите изменения в некоторые значения ее свойств. В этом случае состояние сущности автоматически изменится на `Modified`. Затем при вызове `SaveChanges`Entity Framework создает инструкцию SQL `UPDATE`, которая обновляет только те фактические свойства, которые были изменены.

Отключенная природа веб-приложений не допускает такой непрерывной последовательности. [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) , считывающий сущность, удаляется после отрисовки страницы. При вызове метода действия `HttpPost` `Edit` выполняется новый запрос и создается новый экземпляр [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx), поэтому необходимо вручную задать для состояния сущности значение `Modified.` затем при вызове `SaveChanges`Entity Framework обновляет все столбцы строки базы данных, поскольку контекст не может определить, какие свойства были изменены.

Если необходимо, чтобы инструкция SQL `Update` выполняла обновление только тех полей, которые пользователь фактически изменил, можно сохранить исходные значения каким-либо образом (например, скрытые поля), чтобы они были доступны при вызове метода `HttpPost` `Edit`. Затем можно создать `Student` сущность, используя исходные значения, вызвать метод `Attach` с исходной версией сущности, обновить значения сущности до новых значений, а затем вызвать `SaveChanges.` дополнительные сведения см. в разделе [состояния сущностей и SaveChanges](https://msdn.microsoft.com/data/jj592676) и [локальные данные](https://msdn.microsoft.com/data/jj592872) в центре разработчиков данных MSDN.

Код в *виевс\студент\едит.кштмл* похож на тот, что вы видели в *Create. cshtml*, и никаких изменений не требуется.

Запустите страницу, выбрав вкладку **students (учащиеся** ), а затем щелкнув гиперссылку **Edit (изменить** ).

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

Измените определенные данные и нажмите кнопку **Save** (Сохранить). Измененные данные отображаются на странице индекс.

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>Обновление страницы удаления

В *контроллерс\студентконтроллер.КС*код шаблона для метода `Delete` `HttpGet` использует метод `Find` для получения выбранной сущности `Student`, как было показано в методах `Details` и `Edit`. Тем не менее, чтобы реализовать настраиваемое сообщение об ошибке при сбое вызова метода `SaveChanges`, необходимо добавить некоторые функции в этот метод и соответствующее ему представление.

Как и в случае с операциями обновления и создания, операции удаления требуют двух методов действия. Метод, который вызывается в ответ на запрос GET, отображает представление, которое дает пользователю возможность утверждать или отменять операцию удаления. Если пользователь подтверждает ее, создается запрос POST. В этом случае вызывается метод `HttpPost` `Delete`, а затем этот метод фактически выполняет операцию удаления.

Вы добавите блок `try-catch` в метод `HttpPost` `Delete`, чтобы обрабатывались ошибки, которые могут возникнуть при обновлении базы данных. При возникновении ошибки метод `HttpPost` `Delete` вызывает метод `HttpGet` `Delete`, передавая ему параметр, указывающий, что произошла ошибка. Затем метод `HttpGet Delete` повторно отображает страницу подтверждения вместе с сообщением об ошибке, предоставляя пользователю возможность отменить операцию или повторить попытку.

1. Замените метод действия `HttpGet` `Delete` следующим кодом, который управляет отчетами об ошибках: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    Этот код принимает [необязательный](https://msdn.microsoft.com/library/dd264739.aspx) логический параметр, указывающий, был ли он вызван после сбоя сохранения изменений. Этот параметр `false`, если метод `HttpGet` `Delete` вызывается без предыдущего сбоя. Если метод вызывается методом `HttpPost` `Delete` в ответ на ошибку обновления базы данных, параметр имеет значение `true` и в представление передается сообщение об ошибке.
2. Замените метод действия `HttpPost` `Delete` (с именем `DeleteConfirmed`) следующим кодом, который выполняет фактическую операцию удаления и перехватывает все ошибки обновления базы данных.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     Этот код извлекает выбранную сущность, а затем вызывает метод [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) , чтобы задать для сущности состояние `Deleted`. При вызове `SaveChanges` создается команда SQL `DELETE`. Вы также изменили имя метода действия с `DeleteConfirmed` на `Delete`. Шаблонный код с именем `HttpPost` метод `Delete` `DeleteConfirmed`, чтобы присвоить методу `HttpPost` уникальную сигнатуру. (Среда CLR требует, чтобы перегруженные методы имели различные параметры метода.) Теперь, когда сигнатуры уникальны, можно придерживаться соглашения MVC и использовать одно и то же имя для методов `HttpPost` и `HttpGet` DELETE.

     Если повышение производительности в большом объеме приложения является приоритетным, можно избежать ненужного SQL-запроса для получения строки, заменив строки кода, вызывающие методы `Find` и `Remove`, следующим кодом, как показано в желтом фрагменте.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     Этот код создает экземпляр `Student` сущности, используя только значение первичного ключа, а затем устанавливает состояние сущности `Deleted`. Это все, что платформе Entity Framework необходимо для удаления сущности.

     Как уже отмечалось, метод `HttpGet` `Delete` не удаляет данные. При выполнении операции удаления в ответ на запрос GET (или, при выполнении любой операции изменения, операции создания или любой другой операции, которая изменяет данные) создается угроза безопасности. Дополнительные сведения см. в разделе [ASP.NET MVC Tip #46 — не используйте ссылки DELETE, так как они создают бреши в системе безопасности](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) в блоге Стивен Вальтер.
3. В *виевс\студент\делете.кштмл*добавьте сообщение об ошибке между заголовком `h2` и заголовком `h3`, как показано в следующем примере:

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     Запустите страницу, выбрав вкладку **students (учащиеся** ) и щелкнув гиперссылку **Delete (удалить** ):

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. Щелкните **Delete** (Удалить). Отображается страница Index (Указатель), на которой удаленный учащийся будет отсутствовать. (Вы увидите пример кода обработки ошибок в действии в учебнике [Обработка параллелизма](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) далее в этой серии.)

## <a name="ensuring-that-database-connections-are-not-left-open"></a>Проверка того, что подключения к базе данных не остались открытыми

Чтобы убедиться, что подключения к базе данных правильно закрыты, и ресурсы, которые они содержат, были освобождены, вы увидите, что экземпляр контекста удален. Именно поэтому шаблонный код предоставляет метод [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) в конце класса `StudentController` в *StudentController.CS*, как показано в следующем примере:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

Базовый класс `Controller` уже реализует интерфейс `IDisposable`, поэтому этот код просто добавляет переопределение в метод `Dispose(bool)` для явного удаления экземпляра контекста.

## <a name="summary"></a>Сводка

Теперь у вас есть полный набор страниц, которые выполняют простые операции CRUD для сущностей `Student`. Вы использовали вспомогательные методы MVC для создания элементов пользовательского интерфейса для полей данных. Дополнительные сведения о вспомогательных средствах MVC см. в разделе [Подготовка формы с помощью вспомогательных функций HTML](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx) (страница предназначена для MVC 3, но по-прежнему ОТНОСИТСЯ к MVC 4).

В следующем учебнике вы развернете функциональные возможности страницы индекса, добавив сортировку и разбиение по страницам.

Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Назад](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [Вперед](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
