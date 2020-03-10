---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
title: Начало работы с Entity Framework 4,0 Database First и веб-формами ASP.NET 4 | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 5cb00916-8f46-491f-be25-4739a615d619
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
msc.type: authoredcontent
ms.openlocfilehash: fd88b32ad2a65e5b4c7ead15f0d6dc5dc6e97e75
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511680"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms"></a>Начало работы с Entity Framework 4,0 Database First и веб-формами ASP.NET 4

от [Tom Dykstra)](https://github.com/tdykstra)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Пример приложения — это веб-сайт для вымышленного университета Contoso. На нем предусмотрены различные функции, в том числе прием учащихся, создание курсов и назначение преподавателей.
> 
> В учебнике показаны примеры C#в. [Загружаемый образец](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) содержит код как в, C# так и в Visual Basic.
> 
> ## <a name="database-first"></a>База данных как основа
> 
> Существует три способа работы с данными в Entity Framework: *Database First*, *Model First*и *Code First*. Это руководство предназначено для Database First. Сведения о различиях между этими рабочими процессами и рекомендации по выбору наиболее подходящего сценария см. в разделе [рабочие процессы разработки Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="web-forms"></a>Веб-формы
> 
> В этой серии руководств используется модель веб-форм ASP.NET и предполагается, что вы умеете работать с веб-формами ASP.NET в Visual Studio. Если это не так, см. статью [Начало работы с веб-формами ASP.NET 4,5](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Если вы предпочитаете работать с платформой MVC ASP.NET, см. статью [Начало работы с Entity Framework с помощью ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).
> 
> ## <a name="software-versions"></a>Версии программного обеспечения
> 
> | **Показано в руководстве** | **Также работает с** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express для Web. Руководство не было протестировано в более поздних версиях Visual Studio. В выборе меню, диалоговых окнах и шаблонах существует много различий. |
> | .NET 4 | .NET 4,5 обратно совместима с .NET 4, но руководство не было протестировано с .NET 4,5. |
> | Entity Framework 4 | Руководство не было протестировано в более поздних версиях Entity Framework. Начиная с Entity Framework 5, EF использует по умолчанию `DbContext API`, который был представлен в EF 4,1. Элемент управления EntityDataSource предназначен для использования API `ObjectContext`. Сведения об использовании элемента управления EntityDataSource с API `DbContext` см. в [этой записи блога](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx). |
> 
> ## <a name="questions"></a>Вопросы
> 
> Если у вас есть вопросы, которые не связаны непосредственно с этим руководством, вы можете опубликовать их на [форуме по ASP.NET Entity Framework](https://forums.asp.net/1227.aspx), на [форуме Entity Framework и LINQ to Entities](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)или [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Обзор

Приложение, которое вы будете создавать в этих учебниках, — это простой веб-сайт университета.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image1.png)

Пользователи приложения могут просматривать и обновлять сведения об учащихся, курсах и преподавателях. Ниже показаны несколько экранов, которые вы создадите.

[![Image30](the-entity-framework-and-aspnet-getting-started-part-1/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image3.png)

[![Image37](the-entity-framework-and-aspnet-getting-started-part-1/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image5.png)

[![Image31](the-entity-framework-and-aspnet-getting-started-part-1/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image7.png)

[![Image32](the-entity-framework-and-aspnet-getting-started-part-1/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image9.png)

## <a name="creating-the-web-application"></a>Создание веб-приложения

Чтобы начать работу с руководством, откройте Visual Studio и создайте новый проект веб-приложения ASP.NET с помощью шаблона **веб-приложения ASP.NET** .

[![image01](the-entity-framework-and-aspnet-getting-started-part-1/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image11.png)

Этот шаблон создает проект веб-приложения, который уже содержит таблицу стилей и главные страницы:

[![Image02](the-entity-framework-and-aspnet-getting-started-part-1/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image13.png)

Откройте файл *site. master* и измените "мое приложение ASP.NET" на "Contoso университет".

[!code-html[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample1.html)]

Найдите элемент управления *Menu* с именем `NavigationMenu` и замените его следующей разметкой, которая добавляет пункты меню для создаваемых страниц.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample2.aspx)]

Откройте страницу *Default. aspx* и измените элемент управления `Content` с именем `BodyContent` на следующий:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample3.aspx)]

Теперь у вас есть простая домашняя страница со ссылками на различные страницы, которые будут создаваться:

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image15.png)

## <a name="creating-the-database"></a>Создание базы данных

В этих учебниках используется конструктор моделей данных Entity Framework для автоматического создания модели данных на основе существующей базы данных (часто называется подходом « *база данных-первый* »). Альтернативой, которая не рассматривается в этой серии руководств, является создание модели данных вручную, а затем создание конструктором скриптов, создающих базу данных (подход *модели-First* ).

Для метода First базы данных, используемого в этом руководстве, необходимо добавить базу данных на сайт. Самый простой способ — сначала загрузить проект с этим руководством. Затем щелкните правой кнопкой мыши папку *Данные приложения\_* , выберите команду **Добавить существующий элемент**и выберите файл базы данных *School. mdf* из скачанного проекта.

Альтернативой является соблюдение инструкций по [созданию образца базы данных School](https://msdn.microsoft.com/library/bb399731.aspx). Независимо от того, скачивается база данных или создается, скопируйте файл *School. mdf* из следующей папки в *приложение приложения\_данные* :

`%PROGRAMFILES%\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA`

(В этом расположении *MDF* -файла предполагается, что вы используете SQL Server 2008 Express.)

При создании базы данных из скрипта выполните следующие действия, чтобы создать диаграмму базы данных.

1. В **Обозреватель сервера**раскройте узлы **подключения к данным**, *School. mdf*, щелкните правой кнопкой мыши **диаграммы баз данных**и выберите команду **Добавить новую диаграмму**.

    [![Image35](the-entity-framework-and-aspnet-getting-started-part-1/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image17.png)
2. Выберите все таблицы и нажмите кнопку **Добавить**.

    [![Image36](the-entity-framework-and-aspnet-getting-started-part-1/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image19.png)

    SQL Server создает диаграмму базы данных, которая показывает таблицы, столбцы в таблицах и связи между таблицами. Можно переместить таблицы, чтобы упорядочить их, но вам нравится.
3. Сохраните диаграмму как «Счулдиаграм» и закройте ее.

Если вы скачиваете файл *School. mdf* , который сопровождается этим руководством, можно просмотреть диаграмму базы данных, дважды щелкнув **Счулдиаграм** в разделе **схемы базы данных** в **Обозреватель сервера**.

[![Image38](the-entity-framework-and-aspnet-getting-started-part-1/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image21.png)

Схема выглядит примерно так (таблицы могут находиться в разных расположениях от показанных здесь):

[![Image04](the-entity-framework-and-aspnet-getting-started-part-1/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image23.png)

## <a name="creating-the-entity-framework-data-model"></a>Создание модели данных Entity Framework

Теперь можно создать Entity Frameworkную модель данных из этой базы данных. Модель данных можно создать в корневой папке приложения, но в этом учебнике вы поместите его в папку с именем *DAL* (для уровня доступа к данным).

В **Обозреватель решений**добавьте папку проекта с именем *DAL* (убедитесь, что она находится под проектом, а не под решением).

Щелкните правой кнопкой мыши папку *DAL* и выберите **Добавить** и **новый элемент**. В разделе **Установленные шаблоны**выберите **данные**, выберите шаблон **ADO.NET EDM** , назовите его *счулмодел. EDMX*и нажмите кнопку **Добавить**.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-1/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image25.png)

Запустится мастер EDM. На первом шаге мастера параметр **создать из базы данных** выбран по умолчанию. Щелкните **Далее**.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-1/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image27.png)

На шаге **Выбор подключения к данным** оставьте значения по умолчанию и нажмите кнопку **Далее**. База данных School выбирается по умолчанию, а параметр подключения сохраняется в файле *Web. config* как **пункт SchoolEntities**.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-1/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image29.png)

На шаге мастера **Выбор объектов базы данных** выберите все таблицы, кроме `sysdiagrams` (которая была создана для созданной ранее схемы), а затем нажмите кнопку **Готово**.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-1/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image31.png)

После завершения создания модели Visual Studio отобразит графическое представление объектов Entity Framework (сущностей), соответствующих таблицам базы данных. (Как и в случае диаграммы базы данных, расположение отдельных элементов может отличаться от того, что вы видите на этом рисунке. При необходимости можно перетаскивать элементы вокруг рисунка.)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-1/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image33.png)

## <a name="exploring-the-entity-framework-data-model"></a>Изучение модели данных Entity Framework

Вы видите, что схема сущностей очень похожа на диаграмму базы данных с несколькими различиями. Одно отличие заключается в добавлении символов в конце каждой ассоциации, указывающей тип ассоциации (связи между таблицами называются ассоциациями сущностей в модели данных):

- Ассоциация «один к нулю» представляется «1» и «0.. 1».

    [![Image39](the-entity-framework-and-aspnet-getting-started-part-1/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image35.png)

    В этом случае сущность `Person` может быть связана с сущностью `OfficeAssignment` и не может быть связанной с ней. Сущность `OfficeAssignment` должна быть связана с сущностью `Person`. Другими словами, инструктор может быть назначен для офиса, а любой офис может быть назначен только одному преподавателю.
- Ассоциация "один ко многим" представляется "1" и "\*".

    [![Image40](the-entity-framework-and-aspnet-getting-started-part-1/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image37.png)

    В этом случае сущность `Person` может иметь и не иметь связанных сущностей `StudentGrade`. Сущность `StudentGrade` должна быть связана с одной сущностью `Person`. `StudentGrade` сущности фактически представляют зарегистрированные курсы в этой базе данных; Если учащийся зарегистрирован в курсе, но еще не существует, свойство `Grade` имеет значение null. Другими словами, студент не может быть зарегистрирован в каких-либо курсах, может быть зарегистрирован в одном курсе или может быть зарегистрирован в нескольких курсах. Каждая категория в зарегистрированном курсе относится только к одному студенту.
- Ассоциация "многие ко многим" представлена "\*" и "\*".

    [![Image41](the-entity-framework-and-aspnet-getting-started-part-1/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image39.png)

    В этом случае сущность `Person` может иметь и не иметь связанных сущностей `Course`, а также обратная связь имеет значение true: `Course` сущность может иметь или не иметь связанные сущности `Person`. Другими словами, инструктор может обучать несколько курсов, и курс может обучаться нескольким преподавателям. (В этой базе данных эта связь относится только к инструкторам; она не связывает учащихся с курсами. Студенты связаны с курсами по таблице Студентградес.)

Еще одно различие между диаграммой базы данных и моделью данных — это дополнительный раздел **свойств навигации** для каждой сущности. Свойство навигации сущности ссылается на связанные сущности. Например, свойство `Courses` в сущности `Person` содержит коллекцию всех `Course` сущностей, связанных с этой сущностью `Person`.

[![Image12](the-entity-framework-and-aspnet-getting-started-part-1/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image41.png)

Еще одним различием между базой данных и моделью данных является отсутствие `CourseInstructor` таблицы взаимосвязей, используемой в базе данных для связывания `Person` и `Course` таблиц в связи «многие ко многим». Свойства навигации позволяют получать связанные сущности `Course` из сущности `Person` и связанных сущностей `Person` из сущности `Course`, поэтому нет необходимости представлять таблицу взаимосвязей в модели данных.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-1/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image43.png)

Для целей этого учебника Предположим, что столбец `FirstName` таблицы `Person` фактически содержит имя и отчество человека. Необходимо изменить имя поля, чтобы оно отражало это, но администратору базы данных (DBA) может не понадобиться изменить базу данных. Можно изменить имя свойства `FirstName` в модели данных, оставляя эквивалентную базу данных неизменной.

В конструкторе щелкните правой кнопкой мыши элемент **FirstName** в `Person` сущности и выберите команду **Переименовать**.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-1/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image45.png)

Введите новое имя "FirstMidName". Это изменяет способ ссылки на столбец в коде, не изменяя базу данных.

[![Image29](the-entity-framework-and-aspnet-getting-started-part-1/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image47.png)

Обозреватель моделей предоставляет другой способ просмотра структуры базы данных, структуры модели данных и сопоставления между ними. Чтобы увидеть его, щелкните правой кнопкой мыши пустую область в конструкторе сущностей и выберите пункт **Обозреватель моделей**.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-1/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image49.png)

В области **Обозреватель моделей** отображается представление в виде дерева. (Панель « **Обозреватель моделей** » может быть закреплена с панелью « **Обозреватель решений** ».) Узел **счулмодел** представляет структуру модели данных, а узел **счулмодел. Store** представляет структуру базы данных.

[![Image26](the-entity-framework-and-aspnet-getting-started-part-1/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image51.png)

Разверните **счулмодел. Store** , чтобы просмотреть таблицы, разверните **таблицы или представления** , чтобы просмотреть таблицы, а затем разверните узел **Course** , чтобы просмотреть столбцы в таблице.

[![Image19](the-entity-framework-and-aspnet-getting-started-part-1/_static/image54.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image53.png)

Разверните узел **счулмодел**, разверните узел **типы сущностей**, а затем разверните узел **Course** , чтобы просмотреть сущности и свойства в сущностях.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-1/_static/image56.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image55.png)

В конструкторе или на панели **обозревателя моделей** можно увидеть, как Entity Framework связывает объекты двух моделей. Щелкните правой кнопкой мыши сущность `Person` и выберите пункт **Сопоставление таблиц**.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-1/_static/image58.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image57.png)

Откроется окно **сведения о сопоставлении** . Обратите внимание, что это окно позволяет увидеть, что столбец базы данных `FirstName` сопоставлен с `FirstMidName`, который был переименован в модели данных.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-1/_static/image60.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image59.png)

Entity Framework использует XML для хранения сведений о базе данных, модели данных и сопоставлении между ними. Файл *счулмодел. EDMX* на самом деле представляет собой XML-файл, содержащий эти сведения. Конструктор визуализирует данные в графическом формате, но файл можно также просмотреть в формате XML, щелкнув правой кнопкой мыши *EDMX* -файл в **Обозреватель решений**, выбрав команду **Открыть с помощью**и выбрав **Редактор XML (текстовый)** . (Конструктор моделей данных и редактор XML — это лишь два разных способа открытия и работы с одним и тем же файлом, поэтому конструктор нельзя открыть и открыть файл в редакторе XML одновременно.)

Теперь вы создали веб-сайт, базу данных и модель данных. В следующем пошаговом руководстве вы начнете работать с данными, используя модель данных и элемент управления `EntityDataSource` ASP.NET.

> [!div class="step-by-step"]
> [Дальше](the-entity-framework-and-aspnet-getting-started-part-2.md)
