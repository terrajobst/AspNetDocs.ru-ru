---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4, часть 4 | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework. Пример приложения:...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518286"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4. часть 4

от [Tom Dykstra)](https://github.com/tdykstra)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Сведения о серии руководств см. в [первом учебнике серии](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="working-with-related-data"></a>Работа с связанными данными

В предыдущем учебнике для фильтрации, сортировки и группирования данных использовался элемент управления `EntityDataSource`. В этом учебнике будут показаны и обновлены связанные данные.

Вы создадите страницу инструкторов, на которой отображается список инструкторов. При выборе лектора вы увидите список курсов, которые научились этим инструктором. При выборе курса отображаются сведения о курсе и список учащихся, зарегистрированных в курсе. Вы можете изменить имя преподавателя, дату найма и назначение Office. Назначение Office — это отдельный набор сущностей, доступ к которому осуществляется через свойство навигации.

Основные данные можно связать с подробными данными в разметке или в коде. В этой части руководства вы будете использовать оба метода.

[![image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>Отображение и обновление связанных сущностей в элементе управления GridView

Создайте новую веб-страницу с именем *инструкторы. aspx* , которая использует главную страницу *site. master* , и добавьте следующую разметку в элемент управления `Content` с именем `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

Эта разметка создает элемент управления `EntityDataSource`, который выбирает инструкторы и включает обновления. Элемент `div` настраивает разметку для отображения слева, чтобы можно было добавить столбец в дальнейшем.

Между разметкой `EntityDataSource` и закрывающим тегом `</div>` добавьте следующую разметку, которая создает элемент управления `GridView` и элемент управления `Label`, который будет использоваться для сообщений об ошибках:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

Этот `GridView` элемент управления позволяет выбрать строку, выделить выделенную строку светло-серым цветом фона и указать обработчики (которые будут созданы позже) для событий `SelectedIndexChanged` и `Updating`. Он также указывает `PersonID` для свойства `DataKeyNames`, чтобы значение ключа выбранной строки можно было передать другому элементу управления, который будет добавлен позже.

Последний столбец содержит назначение Office для преподавателей, которое хранится в свойстве навигации сущности `Person`, так как оно поступает из связанной сущности. Обратите внимание, что элемент `EditItemTemplate` указывает `Eval` вместо `Bind`, так как элемент управления `GridView` не может напрямую выполнить привязку к свойствам навигации, чтобы обновить их. Вы обновите назначение Office в коде. Для этого вам потребуется ссылка на элемент управления `TextBox`, и вы получите и сохраните его в событии `Init` элемента управления `TextBox`.

После элемента управления `GridView` — элемент управления `Label`, используемый для сообщений об ошибках. Свойство `Visible` элемента управления `false`, а состояние представления отключено, поэтому метка будет отображаться только в том случае, если код делает его видимым в ответ на ошибку.

Откройте файл *Instructors.aspx.CS* и добавьте следующую инструкцию `using`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

Добавьте поле закрытого класса сразу после объявления разделяемого класса, чтобы оно содержало ссылку на текстовое поле назначения Office.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

Добавьте заглушку для обработчика событий `SelectedIndexChanged`, который вы добавите в дальнейшем код. Также добавьте обработчик для события `Init` элемента управления "Назначение Office `TextBox`", чтобы можно было сохранить ссылку на элемент управления `TextBox`. Эта ссылка используется для получения значения, введенного пользователем для обновления сущности, связанной со свойством навигации.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

Для обновления свойства `Location` связанной сущности `OfficeAssignment` используется событие `Updating` элемента управления `GridView`. Добавьте следующий обработчик для события `Updating`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

Этот код выполняется, когда пользователь нажимает кнопку " **Обновить** " в `GridView` строке. Код использует LINQ to Entities для получения `OfficeAssignment` сущности, связанной с текущей сущностью `Person`, используя `PersonID` выбранной строки из аргумента события.

Затем код принимает одно из следующих действий в зависимости от значения в элементе управления `InstructorOfficeTextBox`:

- Если текстовое поле имеет значение и отсутствует `OfficeAssignment` сущность для обновления, она создается.
- Если текстовое поле имеет значение и имеется сущность `OfficeAssignment`, она обновляет значение свойства `Location`.
- Если текстовое поле пусто и сущность `OfficeAssignment` существует, она удаляет сущность.

После этого изменения сохраняются в базе данных. При возникновении исключения отображается сообщение об ошибке.

Запустите страницу.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

Нажмите кнопку **изменить** и все поля изменяются на текстовые поля.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

Измените любое из этих значений, включая **Назначение Office**. Нажмите кнопку **Обновить** , и вы увидите, что изменения отражены в списке.

## <a name="displaying-related-entities-in-a-separate-control"></a>Отображение связанных сущностей в отдельном элементе управления

Каждый инструктор может обучать один или несколько курсов, поэтому вы добавите элемент управления `EntityDataSource` и `GridView`, чтобы получить список курсов, связанных с тем, какой лектор выбран в `GridView` управления инструкторами. Чтобы создать заголовок и элемент управления `EntityDataSource` для сущностей «курсы», добавьте следующую разметку между сообщением об ошибке `Label` элемента управления и закрывающим тегом `</div>`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

Параметр `Where` содержит значение `PersonID` инструктора, строка которого выбрана в элементе управления `InstructorsGridView`. Свойство `Where` содержит команду подзапроса выборки, которая получает все связанные `Person` сущности из свойства навигации `People` сущности `Course` и выбирает сущность `Course`, только если одна из связанных `Person` сущностей содержит выбранное значение `PersonID`.

Чтобы создать элемент управления `GridView`, добавьте следующую разметку сразу после элемента управления `CoursesEntityDataSource` (перед закрывающим тегом `</div>`):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

Так как никакие курсы не будут отображаться, если лектор не выбран, включается элемент `EmptyDataTemplate`.

Запустите страницу.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

Выберите лектора с одним или несколькими назначенными курсами, курс или курсы отобразятся в списке. (Примечание. Несмотря на то, что схема базы данных допускает несколько курсов, в тестовых данных, предоставляемых вместе с базой данных, инструктор на самом деле не имеет более одного курса. Вы можете вручную добавить курсы в базу данных с помощью окна **Обозреватель сервера** или страницы *каурсесадд. aspx* , которое вы добавите в более поздний учебник.)

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

Элемент управления `CoursesGridView` отображает только несколько полей курса. Чтобы отобразить все сведения о курсе, вы будете использовать элемент управления `DetailsView` для курса, который выбирает пользователь. В *инструкторах. aspx*добавьте следующую разметку после закрывающего тега `</div>` (убедитесь, что эта разметка размещается **после** закрывающего тега div, а не перед ним):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

Эта разметка создает элемент управления `EntityDataSource`, привязанный к `Courses` набору сущностей. Свойство `Where` выбирает курс, используя значение `CourseID` выбранной строки в элементе управления Courses `GridView`. В разметке указывается обработчик события `Selected`, который будет использоваться позже для отображения оценок учащихся, которые находятся на другом уровне иерархии.

В *Instructors.aspx.CS*создайте следующую заглушку для метода `CourseDetailsEntityDataSource_Selected`. (Вы заполните эту заглушку позже в этом руководстве. сейчас она понадобится, чтобы страница была скомпилирована и выполнена.)

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

Запустите страницу.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

Изначально нет сведений о курсе, так как курс не выбран. Выберите лектора с назначенным курсом, а затем выберите курс, чтобы просмотреть подробные сведения.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>Использование события EntityDataSource "Selected" для вывода связанных данных

Наконец, необходимо отобразить всех зарегистрированных учащихся и их оценки для выбранного курса. Для этого используется событие `Selected` элемента управления `EntityDataSource`, привязанного к курсу `DetailsView`.

В *инструкторах. aspx*добавьте следующую разметку после элемента управления `DetailsView`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

Эта разметка создает элемент управления `ListView`, который отображает список учащихся и их оценки для выбранного курса. Не указан источник данных, поскольку элемент управления будет связан в коде. Элемент `EmptyDataTemplate` предоставляет сообщение, которое отображается, если курс не выбран — в этом случае нет учащихся для показа. Элемент `LayoutTemplate` создает HTML-таблицу для вывода списка, а `ItemTemplate` определяет отображаемые столбцы. ИДЕНТИФИКАТОР учащегося и уровень учащегося относятся к сущности `StudentGrade`, а имя учащегося — из сущности `Person`, которую Entity Framework сделать доступной в свойстве навигации `Person` сущности `StudentGrade`.

В *Instructors.aspx.CS*замените метод `CourseDetailsEntityDataSource_Selected` создана с помощью следующего кода:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

Аргумент события для этого события предоставляет выбранные данные в виде коллекции, которая будет содержать нулевые элементы, если ничего не выбрано, или один элемент, если выбрана сущность `Course`. Если выбрана сущность `Course`, код использует метод `First` для преобразования коллекции в один объект. Затем он получает `StudentGrade` сущности из свойства навигации, преобразует их в коллекцию и привязывает элемент управления `GradesListView` к коллекции.

Это достаточно для отображения оценок, но необходимо убедиться, что сообщение в шаблоне пустых данных отображается при первом отображении страницы, и если курс не выбран. Для этого создайте следующий метод, который будет вызываться из двух мест:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

Вызовите этот новый метод из метода `Page_Load`, чтобы отобразить пустой шаблон данных при первом отображении страницы. И вызывайте его из метода `InstructorsGridView_SelectedIndexChanged`, так как это событие возникает при выборе инструктора, что означает, что новые курсы загружаются в курсы `GridView` управления и пока не выбрано ни одного. Ниже приведены два вызова.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

Запустите страницу.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

Выберите лектора с назначенным курсом, а затем выберите курс.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

Теперь вы видели несколько способов работы с взаимосвязанными данными. В следующем руководстве вы узнаете, как добавить связи между существующими сущностями, как удалить связи и как добавить новую сущность, имеющую связь с существующей сущностью.

> [!div class="step-by-step"]
> [Назад](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [Вперед](the-entity-framework-and-aspnet-getting-started-part-5.md)
