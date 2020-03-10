---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Начало работы с Entity Framework 4,0 Database First и ASP.NET 4 Web Forms, часть 8 | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework. Пример приложения:...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473508"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4. часть 8

от [Tom Dykstra)](https://github.com/tdykstra)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Сведения о серии руководств см. в [первом учебнике серии](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>Использование функций платформа динамических данных для форматирования и проверки данных

В предыдущем учебнике были реализованы хранимые процедуры. В этом учебнике показано, как платформа динамических данных функции предоставляют следующие преимущества.

- Поля автоматически отформатированы для вывода на основе их типа данных.
- Поля автоматически проверяются на основе их типа данных.
- Можно добавить метаданные в модель данных, чтобы настроить форматирование и поведение проверки. После этого можно добавить правила форматирования и проверки в одном месте, и они будут автоматически применяться везде, где вы обращаетесь к полям с помощью платформа динамических данных элементов управления.

Чтобы увидеть, как это работает, вы измените элементы управления, используемые для отображения и редактирования полей в существующей странице *students. aspx* , и добавьте метаданные форматирования и проверки в поля имя и Дата `Student`ного типа сущности.

[![image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>Использование элементов управления Динамикфиелд и DynamicControl

Откройте страницу *students. aspx* и в элементе управления `StudentsGridView` замените **имя** и **дату регистрации** `TemplateField` элементами следующей разметкой:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

В этой разметке в поле "имя учащегося" используются `DynamicControl` элементы управления `TextBox` и `Label`, а в качестве даты регистрации используется элемент управления `DynamicField`. Строки формата не указаны.

Добавьте элемент управления `ValidationSummary` после элемента управления `StudentsGridView`.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

В элементе управления `SearchGridView` замените разметку для столбцов " **имя** " и " **Дата регистрации** ", как в элементе управления `StudentsGridView`, за исключением элемента `EditItemTemplate`. Элемент `Columns` элемента управления `SearchGridView` теперь содержит следующую разметку:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

Откройте *students.aspx.CS* и добавьте следующую инструкцию `using`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

Добавьте обработчик для события `Init` страницы:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

Этот код указывает, что платформа динамических данных предоставит форматирование и проверку в этих элементах управления с привязкой к данным для полей `Student` сущности. Если при запуске страницы появляется сообщение об ошибке, как в следующем примере, это обычно означает, что вы забыли вызвать метод `EnableDynamicData` в `Page_Init`:

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

Запустите страницу.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

В столбце **Дата регистрации** время отображается вместе с датой, так как тип свойства — `DateTime`. Это будет исправлено позже.

Теперь обратите внимание, что платформа динамических данных автоматически обеспечивает базовую проверку данных. Например, щелкните **изменить**, очистите поле Дата, нажмите кнопку **Обновить**, и вы увидите, что платформа динамических данных автоматически сделает это обязательное поле, поскольку значение не допускает значения NULL в модели данных. На странице отображается звездочка после поля и сообщение об ошибке в элементе управления `ValidationSummary`:

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

Можно опустить элемент управления `ValidationSummary`, так как можно также удерживать указатель мыши над звездочкой, чтобы увидеть сообщение об ошибке:

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

Платформа динамических данных также будет проверять, что данные, указанные в поле **Дата регистрации** , являются допустимой датой:

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

Как видите, это общее сообщение об ошибке. В следующем разделе вы узнаете, как настраивать сообщения, а также правила проверки и форматирования.

## <a name="adding-metadata-to-the-data-model"></a>Добавление метаданных в модель данных

Как правило, необходимо настроить функциональные возможности, предоставляемые платформа динамических данных. Например, можно изменить отображение данных и содержимое сообщений об ошибках. Обычно правила проверки данных также настраиваются для предоставления дополнительных функциональных возможностей, чем платформа динамических данных, предоставляемых автоматически на основе типов данных. Для этого создаются разделяемые классы, соответствующие типам сущностей.

В **Обозреватель решений**щелкните правой кнопкой мыши проект **ContosoUniversity** , выберите **Добавить ссылку**и добавьте ссылку на `System.ComponentModel.DataAnnotations`.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

В папке *DAL* создайте новый файл класса, назовите его *Student.CS*и замените в нем код шаблона следующим кодом.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

Этот код создает разделяемый класс для `Student` сущности. Атрибут `MetadataType`, применяемый к этому разделяемому классу, определяет класс, который используется для указания метаданных. Класс метаданных может иметь любое имя, но использование имени сущности и "Metadata" является распространенной практикой.

Атрибуты, применяемые к свойствам в классе метаданных, определяют форматирование, проверку, правила и сообщения об ошибках. Приведенные здесь атрибуты будут иметь следующие результаты.

- `EnrollmentDate` будет отображаться как дата (без времени).
- Длина обоих полей имени не должна превышать 25 символов, и предоставляется настраиваемое сообщение об ошибке.
- Оба поля имени являются обязательными, и предоставляется пользовательское сообщение об ошибке.

Снова запустите страницу *students. aspx* , и вы увидите, что даты теперь отображаются без указания времени:

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

Измените строку и попытайтесь очистить значения в полях имя. Звездочки, указывающие, что ошибки полей появляются сразу после выхода из поля, перед нажатием кнопки **Обновить**. При нажатии кнопки **Обновить**на странице отображается указанный текст сообщения об ошибке.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

Попробуйте ввести имена длиной более 25 символов, нажмите кнопку **Обновить**, и на странице отобразится указанный текст сообщения об ошибке.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

Теперь, когда вы настроили эти правила форматирования и проверки в метаданных модели данных, правила будут автоматически применены на каждой странице, которая отображает или разрешает изменения в этих полях, при условии использования элементов управления `DynamicControl` или `DynamicField`. Это сокращает объем избыточного кода, который необходимо написать, что упрощает программирование и тестирование, а также обеспечивает согласованность форматирования и проверки данных в рамках всего приложения.

## <a name="more-information"></a>Дополнительные сведения

В конце этой серии учебников по начало работы с Entity Framework. Для получения дополнительных сведений о том, как использовать Entity Framework, перейдите к [первому руководству в следующей Entity Framework серии руководств](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) или посетите следующие сайты:

- [Вопросы и ответы по Entity Framework](http://www.ef-faq.org/introduction.html)
- [Блог группы разработчиков Entity Framework](https://blogs.msdn.com/b/adonet/)
- [Entity Framework в библиотеке MSDN](https://msdn.microsoft.com/library/bb399572.aspx)
- [Entity Framework в центре разработчиков данных MSDN](https://msdn.microsoft.com/data/ef.aspx)
- [Общие сведения об элементе управления веб-сервера EntityDataSource в библиотеке MSDN](https://msdn.microsoft.com/library/cc488502.aspx)
- [Справочник по API элемента управления EntityDataSource в библиотеке MSDN](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [Форумы Entity Framework на MSDN](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [Блог Юлия Лерман](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [Назад](the-entity-framework-and-aspnet-getting-started-part-7.md)
