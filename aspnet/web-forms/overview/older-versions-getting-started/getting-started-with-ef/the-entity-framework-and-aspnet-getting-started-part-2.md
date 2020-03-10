---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4, часть 2 | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework. Пример приложения:...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: bd6a2e29e6f0df04e39be29160e2e08cc99c4706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456450"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4. часть 2

от [Tom Dykstra)](https://github.com/tdykstra)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Сведения о серии руководств см. в [первом учебнике серии](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="the-entitydatasource-control"></a>Элемент управления EntityDataSource

В предыдущем руководстве вы создали веб-сайт, базу данных и модель данных. В этом учебнике вы работаете с `EntityDataSource`ным элементом управления, предоставляемым ASP.NET, чтобы упростить работу с Entity Frameworkной моделью данных. Вы создадите `GridView`ный элемент управления для отображения и редактирования данных учащихся, `DetailsView` элемент управления для добавления новых учащихся и элемент управления `DropDownList` для выбора отдела (который будет использоваться позже для отображения связанных курсов).

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

Обратите внимание, что в этом приложении вы не будете добавлять проверку ввода на страницах, которые обновляют базу данных, а некоторые из них не будут считаться надежными, как это было бы необходимо в рабочем приложении. Это позволяет учебнику посвящено Entity Framework и постоянно получать его слишком долго. Дополнительные сведения о добавлении этих функций в приложение см. в разделе [проверка вводимых пользователем данных в веб-страницы ASP.NET](https://msdn.microsoft.com/library/7kh55542.aspx) и [обработке ошибок в страницах и приложениях ASP.NET](https://msdn.microsoft.com/library/w16865z6.aspx).

## <a name="adding-and-configuring-the-entitydatasource-control"></a>Добавление и настройка элемента управления EntityDataSource

Начнем с настройки элемента управления `EntityDataSource` для чтения сущностей `Person` из `People` набора сущностей.

Убедитесь, что вы открыли Visual Studio и работаете с проектом, созданным в части 1. Если проект не был создан с момента создания модели данных или с момента внесения последнего изменения, создайте проект прямо сейчас. Изменения модели данных не предоставляются конструктору до тех пор, пока проект не будет построен.

Создайте новую веб-страницу с помощью **веб-формы, используя шаблон главной страницы** , и назовите ее *students. aspx*.

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

Укажите *site. master* в качестве главной страницы. На всех страницах, создаваемых для этих учебников, будет использоваться эта эталонная страница.

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

В представлении **исходного кода** добавьте заголовок `h2` в элемент управления `Content` с именем `Content2`, как показано в следующем примере:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

На вкладке **данные** **панели элементов**перетащите элемент управления `EntityDataSource` на страницу, поместите его под заголовком и измените идентификатор на `StudentsEntityDataSource`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

Переключитесь в режим **конструктора** , щелкните смарт-тег элемента управления источника данных, а затем щелкните **Настройка источника данных** , чтобы запустить мастер **настройки источника данных** .

[![image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

На шаге мастера **Настройка ObjectContext** выберите **пункт SchoolEntities** в качестве значения **именованного соединения**и выберите **пункт SchoolEntities** в качестве значения **defaultContainerName** . Затем нажмите кнопку **Далее**.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

Примечание. Если на этом этапе появляется следующее диалоговое окно, необходимо выполнить сборку проекта, прежде чем продолжать работу.

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

На шаге **Настройка выбора данных** выберите **люди** в качестве значения для **EntitySetName**. В разделе **SELECT**убедитесь, что установлен флажок **выбрать** все. Затем выберите параметры для включения обновления и удаления. Когда все будет готово, нажмите кнопку **Готово**.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>Настройка правил базы данных для разрешения удаления

Будет создана страница, позволяющая пользователям удалять учащихся из таблицы `Person`, которая имеет три связи с другими таблицами (`Course`, `StudentGrade`и `OfficeAssignment`). По умолчанию база данных не может удалить строку в `Person`, если в одной из других таблиц есть связанные строки. Сначала можно удалить связанные строки вручную, или же можно настроить базу данных для автоматического удаления при удалении `Person` строки. Для записей учащихся в этом руководстве вы настроите базу данных для автоматического удаления связанных данных. Поскольку студенты могут иметь связанные строки только в таблице `StudentGrade`, необходимо настроить только одну из трех связей.

Если вы используете файл *School. mdf* , скачанный из проекта, который используется в этом руководстве, можно пропустить этот раздел, так как эти изменения конфигурации уже выполнены. Если база данных была создана путем запуска скрипта, настройте базу данных, выполнив следующие процедуры.

В **Обозреватель сервера**откройте диаграмму базы данных, созданную в части 1. Щелкните правой кнопкой мыши связь между `Person` и `StudentGrade` (линия между таблицами), а затем выберите пункт **Свойства**.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

В окне **Свойства** разверните узел **Спецификация вставки и обновления** и установите для свойства **DeleteRule** значение **CASCADE**.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

Сохраните и закройте диаграмму. Если вы запрашиваете, нужно ли обновить базу данных, нажмите кнопку **Да**.

Чтобы гарантировать, что модель сохраняет сущности, синхронизированные в памяти, с тем, что делает база данных, необходимо задать соответствующие правила в модели данных. Откройте *счулмодел. EDMX*, щелкните правой кнопкой мыши линию связи между `Person` и `StudentGrade`, а затем выберите пункт **свойства**.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

В окне **Свойства** присвойте параметру **элемента end1 OnDelete** значение **CASCADE**.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

Сохраните и закройте файл *счулмодел. EDMX* , а затем перестройте проект.

Как правило, при изменении базы данных существует несколько способов синхронизации модели.

- Для внесения определенных типов изменений (например, для добавления или обновления таблиц, представлений или хранимых процедур) щелкните правой кнопкой мыши в конструкторе и выберите **Обновить модель из базы данных** , чтобы конструктор автоматически внесет изменения.
- Повторное создание модели данных.
- Обновите вручную, как это было бы.

В этом случае можно было заново создать модель или обновить таблицы, на которые влияет изменение связи, но после этого потребуется снова изменить имя поля (с `FirstName` на `FirstMidName`).

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>Использование элемента управления GridView для чтения и обновления сущностей

В этом разделе будет использоваться элемент управления `GridView` для просмотра, обновления и удаления учащихся.

Откройте или переключитесь на *students. aspx* и переключитесь в режим **конструктора** . На вкладке **данные** **панели элементов**перетащите элемент управления `GridView` в правой части элемента управления `EntityDataSource`, назовите его `StudentsGridView`, щелкните смарт-тег, а затем выберите **студентсентитидатасаурце** в качестве источника данных.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

Нажмите кнопку **Обновить схему** (нажмите кнопку **Да** , если появится запрос на подтверждение), затем щелкните **включить подкачку**, **включить сортировку**, включить **изменение**и **включить удаление**.

Нажмите кнопку **изменить столбцы**.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

В поле **Выбранные поля** удалите **PersonID**, **LastName**и **HireDate**. Как правило, не отображается ключ записи для пользователей, Дата найма не важна для учащихся, и вы помещаете обе части имени в одно поле, поэтому вам потребуется только одно из полей имени.)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

Выберите поле **FirstMidName** и щелкните **преобразовать это поле в TemplateField**.

Сделайте то же самое для **енроллментдате**.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

Нажмите кнопку **ОК** , а затем переключитесь в представление **исходного кода** . Оставшиеся изменения будут проще в разметке. Разметка элемента управления `GridView` теперь выглядит, как показано в следующем примере.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

Первый столбец после поля Command — это поле шаблона, в котором в настоящее время отображается имя. Измените разметку для этого поля шаблона, как показано в следующем примере:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

В режиме экрана два элемента управления `Label` отображают имя и фамилию. В режиме редактирования предоставляются два текстовых поля, которые позволяют изменить имя и фамилию. Как и в случае с элементами управления `Label` в режиме вывода, выражения `Bind` и `Eval` используются точно так же, как и элементы управления источниками данных ASP.NET, подключающиеся непосредственно к базам данных. Единственное отличие заключается в том, что вместо столбцов базы данных указываются свойства сущности.

Последний столбец — это поле шаблона, в котором отображается дата регистрации. Измените разметку для этого поля, как показано в следующем примере:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

В режиме отображения и редактирования строка форматирования "{0, d}" приводит к тому, что дата отображается в формате "краткий формат даты". (Возможно, ваш компьютер настроен на отображение этого формата по-другому на экранных изображениях, показанных в этом руководстве.)

Обратите внимание, что в каждом из этих полей шаблона конструктор по умолчанию использовал `Bind` выражение, но вы изменили его на `Eval` выражение в `ItemTemplate`ных элементах. `Bind` выражение делает данные доступными в свойствах `GridView` элемента управления в случае, если необходимо получить доступ к данным в коде. На этой странице нет необходимости обращаться к этим данным в коде, поэтому можно использовать `Eval`, что более эффективно. Дополнительные сведения см. [в разделе Получение данных из элементов управления данными](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx).

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>Пересмотр разметки элемента управления EntityDataSource для повышения производительности

В разметке для элемента управления `EntityDataSource` удалите атрибуты `ConnectionString` и `DefaultContainerName` и замените их атрибутом `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`. Это изменение необходимо выполнить каждый раз при создании элемента управления `EntityDataSource`, если не требуется использовать соединение, отличное от жестко заданной в классе контекста объекта. Использование атрибута `ContextTypeName` предоставляет следующие преимущества.

- Повышенная производительность. Когда `EntityDataSource` элемент управления инициализирует модель данных с помощью атрибутов `ConnectionString` и `DefaultContainerName`, она выполняет дополнительную работу по загрузке метаданных при каждом запросе. Это не требуется, если указать атрибут `ContextTypeName`.
- Отложенная загрузка по умолчанию включена в создаваемых классах контекста созданных объектов (например, `SchoolEntities` в этом руководстве) в Entity Framework 4,0. Это означает, что свойства навигации автоматически загружаются вместе с соответствующими данными, когда это необходимо. Более подробно эта отложенная загрузка описывается далее в этом руководстве.
- Все настройки, примененные к классу контекста объекта (в данном случае класс `SchoolEntities`) будут доступны для элементов управления, использующих элемент управления `EntityDataSource`. Настройка класса контекста объекта — это дополнительная тема, которая не рассматривается в этой серии руководств. Дополнительные сведения см. в разделе [расширение Entity Framework созданных типов](https://msdn.microsoft.com/library/dd456844.aspx).

Теперь разметка будет выглядеть следующим образом (порядок свойств может отличаться):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

Атрибут `EnableFlattening` ссылается на функцию, которая была необходима в более ранних версиях Entity Framework, поскольку внешние ключевые столбцы не были представлены как свойства сущности. Текущая версия позволяет использовать *связи по внешнему ключу*. Это означает, что свойства внешнего ключа доступны для всех ассоциаций, кроме связей «многие ко многим». Если сущности имеют свойства внешнего ключа и не имеют [сложных типов](https://msdn.microsoft.com/library/bb738472.aspx), можно оставить для этого атрибута значение `False`. Не удаляйте атрибут из разметки, так как значение по умолчанию — `True`. Дополнительные сведения см. в разделе [сведение объектов (EntityDataSource)](https://msdn.microsoft.com/library/ee404746.aspx).

Запустите страницу, и вы увидите список учащихся и сотрудников (вы будете отфильтровать только учащихся в следующем руководстве). Имя и фамилия отображаются вместе.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

Чтобы отсортировать отображение, щелкните имя столбца.

Нажмите кнопку **изменить** в любой строке. Отображаются текстовые поля, в которых можно изменить имя и фамилию.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

Также будет доступна кнопка **Удалить** . Нажмите кнопку Удалить для строки, имеющей дату регистрации, и строка исчезнет. (Строки без даты регистрации представляют инструкторы, и вы можете получить ошибку ссылочной целостности. В следующем руководстве вы отфильтруем этот список, чтобы включить только учащихся.)

## <a name="displaying-data-from-a-navigation-property"></a>Отображение данных из свойства навигации

Теперь предположим, что необходимо выяснить, сколько курсов зарегистрировано каждым студентом. Entity Framework предоставляет эти сведения в свойстве навигации `StudentGrades` сущности `Person`. Поскольку структура базы данных не позволяет зарегистрировать учащихся в курсе, не прибегая к категории «назначено», в этом учебнике можно предположить, что строка в `StudentGrade` строке таблицы, связанной с курсом, аналогична регистрации в курсе. (Свойство навигации `Courses` предназначено только для инструкторов.)

При использовании атрибута `ContextTypeName` элемента управления `EntityDataSource` Entity Framework автоматически извлекает сведения о свойстве навигации при доступе к этому свойству. Это называется *отложенной загрузкой*. Однако это может оказаться неэффективным, так как при каждом последующем обращении к базе данных возникает отдельный вызов. Если вам нужны данные из свойства навигации для каждой сущности, возвращаемой элементом управления `EntityDataSource`, более эффективным будет получение связанных данных вместе с самой сущностью в одном вызове к базе данных. Это называется *безотлагательной загрузкой*и указывается упреждающая загрузка для свойства навигации путем установки свойства `Include` элемента управления `EntityDataSource`.

В файле *students. aspx*необходимо отобразить количество курсов для каждого учащегося, поэтому рекомендуется использовать безотлагательную загрузку. Если вы выводили отображение всех учащихся, но показываете количество курсов только для некоторых из них (что потребует написания кода в дополнение к разметке), отложенная загрузка может быть лучшим выбором.

Откройте или перейдите к *students. aspx*, переключитесь в режим **конструктора** , выберите `StudentsEntityDataSource`и в окне **свойств** задайте для свойства **включить** значение **студентградес**. (Если вы хотите получить несколько свойств навигации, можно указать их имена, разделенные запятыми, например **студентградес, Courses**.)

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

Переключитесь в представление **исходного кода** . В элементе управления `StudentsGridView` после последнего элемента `asp:TemplateField` добавьте следующее новое поле шаблона:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

В `Eval` выражении можно ссылаться на `StudentGrades`свойства навигации. Поскольку это свойство содержит коллекцию, оно имеет свойство `Count`, которое можно использовать для просмотра числа курсов, в которых регистрируется учащийся. В следующем учебнике вы узнаете, как отображать данные из свойств навигации, содержащих отдельные сущности, а не коллекции. (Обратите внимание, что нельзя использовать элементы `BoundField` для вывода данных из свойств навигации.)

Запустите эту страницу, и теперь вы увидите, сколько курсов каждый учащийся зарегистрирован в.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>Использование элемента управления DetailsView для вставки сущностей

Следующим шагом является создание страницы с элементом управления `DetailsView`, который позволяет добавлять новых учащихся. Закройте браузер и создайте новую веб-страницу с помощью главной страницы *site. master* . Назовите страницу *студентсадд. aspx*, а затем переключитесь в представление **исходного кода** .

Добавьте следующую разметку, чтобы заменить существующую разметку для элемента управления `Content` с именем `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

Эта разметка создает элемент управления `EntityDataSource`, аналогичный тому, который был создан в файле *students. aspx*, но включает вставку. Как и в случае с элементом управления `GridView`, привязанные поля элемента управления `DetailsView` кодируются точно так же, как для элемента управления данными, который подключается непосредственно к базе данных, за исключением того, что они ссылаются на свойства сущности. В этом случае элемент управления `DetailsView` используется только для вставки строк, поэтому для режима по умолчанию задано значение `Insert`.

Запустите страницу и добавьте нового учащегося.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

После вставки нового учащегося ничего не произойдет, но если теперь запустить *students. aspx*, вы увидите новые сведения об учащихся.

## <a name="displaying-data-in-a-drop-down-list"></a>Отображение данных в раскрывающемся списке

На следующих шагах выполняется привязка элемента управления `DropDownList` к набору сущностей с помощью элемента управления `EntityDataSource`. В этой части руководства вы не будете многого делать с этим списком. Однако в последующих частях вы будете использовать список, чтобы позволить пользователям выбрать отдел для показа курсов, связанных с этим подразделением.

Создайте новую веб-страницу с именем *Courses. aspx*. В представлении **исходного кода** добавьте заголовок в элемент управления `Content` с именем `Content2`.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

В режиме **конструктора** добавьте элемент управления `EntityDataSource` на страницу, как это делалось ранее, за исключением того, что это имя `DepartmentsEntityDataSource`. Выберите **отделы** в качестве значения **EntitySetName** и выберите только свойства **DepartmentID** и **Name** .

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

На вкладке " **стандартные** " **панели элементов**перетащите элемент управления `DropDownList` на страницу, присвойте ему имя `DepartmentsDropDownList`, щелкните смарт-тег и выберите **пункт Выбрать источник данных** , чтобы запустить **Мастер настройки DataSource**.

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

На шаге **Выбор источника данных** в качестве источника данных выберите **Департментсентитидатасаурце** , щелкните **Обновить схему**, а затем выберите **имя** в качестве поля данных для вывода и **DepartmentID** в качестве поля данных значения. Нажмите кнопку **ОК**.

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

Метод, используемый для привязки элемента управления с помощью Entity Framework, совпадает с другими элементами управления источниками данных ASP.NET, за исключением того, что вы указываете сущности и свойства сущности.

Переключитесь в представление **источника** и добавьте "выбрать отдел:" непосредственно перед элементом управления `DropDownList`.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

Как напоминание, измените разметку для элемента управления `EntityDataSource` на этом этапе, заменив атрибуты `ConnectionString` и `DefaultContainerName` атрибутом `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`. Часто лучше подождать, пока вы создали привязанный к данным элемент управления, связанный с элементом управления источника данных, прежде чем изменять разметку элемента управления `EntityDataSource`, так как после внесения изменений конструктор не предоставит параметр **Обновить схему** в элементе управления с привязкой к данным.

Запустите страницу, чтобы выбрать отдел из раскрывающегося списка.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

Это завершает вводные сведения об использовании элемента управления `EntityDataSource`. Работа с этим элементом управления обычно не отличается от работы с другими элементами управления источниками данных ASP.NET, за исключением ссылок на сущности и свойства, а не на таблицы и столбцы. Единственное исключение — когда требуется получить доступ к свойствам навигации. В следующем учебнике вы увидите, что синтаксис, используемый с элементом управления `EntityDataSource`, также может отличаться от других элементов управления источниками данных при фильтрации, группировании и упорядочении данных.

> [!div class="step-by-step"]
> [Назад](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [Вперед](the-entity-framework-and-aspnet-getting-started-part-3.md)
