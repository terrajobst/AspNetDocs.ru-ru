---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: Создание модели с проверками бизнес-правил | Документация Майкрософт
author: microsoft
description: На шаге 3 показано, как создать модель, которую можно использовать для запроса и обновления базы данных для нашего приложения NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435582"
---
# <a name="build-a-model-with-business-rule-validations"></a>Создание модели с проверками бизнес-правил

по [Майкрософт](https://github.com/microsoft)

[Скачать в формате PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Это шаг 3 из бесплатного [учебника по NerdDinner приложению](introducing-the-nerddinner-tutorial.md) , в котором рассматривается создание небольшого, но полного веб-приложения с использованием ASP.NET MVC 1.
> 
> На шаге 3 показано, как создать модель, которую можно использовать для запроса и обновления базы данных для нашего приложения NerdDinner.
> 
> Если вы используете ASP.NET MVC 3, мы рекомендуем следовать руководствам по [Начало работы в MVC 3 или в приложении для](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [музыкального магазина MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) .

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner. этап 3. Создание модели

В инфраструктуре "модель-представление-контроллер" термин "модель" относится к объектам, представляющим данные приложения, а также к соответствующей логике предметной области, которая интегрирует проверку и бизнес-правила с ним. Эта модель во многом зависит от «сердца» приложения на основе MVC, и, как мы увидим позднее, поймет его поведение.

Платформа ASP.NET MVC поддерживает использование любой технологии доступа к данным, и разработчики могут выбирать из множества разнообразных возможностей данных .NET для реализации их моделей, в том числе: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, Вилсонорм или только необработанные ADO. NET DataReaders или наборы данных.

Для нашего приложения NerdDinner мы будем использовать LINQ to SQL, чтобы создать простую модель, которая полностью соответствует нашей структуре базы данных, и добавляет некоторую пользовательскую логику проверки и бизнес-правила. Затем мы реализуем класс репозитория, который помогает абстрактно использовать реализацию сохраняемости данных из остальной части приложения и позволяет нам легко выполнять модульное тестирование.

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL является ORM (реляционным модулем сопоставления объектов), который поставляется в составе .NET 3,5.

LINQ to SQL предоставляет простой способ сопоставлять таблицы базы данных с классами .NET, к которым можно выполнять код. Для нашего NerdDinner приложения мы будем использовать его для преобразования таблиц диннерс и RSVP в базе данных в классы ужин и RSVP. Столбцы таблиц диннерс и RSVP будут соответствовать свойствам в классах Dinner и RSVP. Каждый объект Dinner and RSVP будет представлять отдельную строку в таблицах диннерс или RSVP в базе данных.

LINQ to SQL позволяет нам избегать ручного создания инструкций SQL для получения и обновления объектов Dinner и RSVP с данными базы данных. Вместо этого мы определим классы Dinner and RSVP, способ сопоставления с базой данных и связи между ними. После этого LINQ to SQL позаботится о создании соответствующей логики выполнения SQL, которая будет использоваться во время выполнения при взаимодействии и использовании.

Мы можем использовать поддержку языка LINQ в VB и C# писать выразительные запросы, которые извлекают объекты Dinner и RSVP из базы данных. Это уменьшает объем кода данных, который нам нужно написать, и позволяет создавать реальные приложения.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>Добавление LINQ to SQL классов в наш проект

Начнем с того, что щелкните правой кнопкой мыши папку "Models" в нашем проекте и выберите команду **Добавить-&gt;создать элемент** меню:

![](build-a-model-with-business-rule-validations/_static/image1.png)

Откроется диалоговое окно "Добавление нового элемента". Фильтрация по категории "данные" и выбор в ней шаблона "LINQ to SQL классы".

![](build-a-model-with-business-rule-validations/_static/image2.png)

Мы назовем элемент «NerdDinner» и надолжим кнопку «Add» (Добавить). Visual Studio добавит файл NerdDinner. dbml в каталог \Моделс, а затем откроет LINQ to SQL реляционный конструктор объектов:

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>Создание классов модели данных с помощью LINQ to SQL

LINQ to SQL позволяет быстро создавать классы модели данных из существующей схемы базы данных. Для этого мы откроем базу данных NerdDinner в обозреватель сервера и выбираем таблицы, которые нужно моделировать.

![](build-a-model-with-business-rule-validations/_static/image4.png)

Затем можно перетащить таблицы на поверхность конструктора LINQ to SQL. Когда мы делаем это, LINQ to SQL автоматически создаст классы ужин и RSVP, используя схему таблиц (со свойствами класса, которые сопоставляются со столбцами таблицы базы данных):

![](build-a-model-with-business-rule-validations/_static/image5.png)

По умолчанию конструктор LINQ to SQL автоматически задает имена таблиц и столбцов "перевод" при создании классов на основе схемы базы данных. Например: таблица "диннерс" в нашем примере выше привела к классу "ужин". Такое именование классов помогает сделать наши модели совместимыми с соглашениями об именовании .NET, и я обычно находим, что конструктор самостоятельно решает эту проблему (особенно при добавлении большого числа таблиц). Однако если вам не нравится имя класса или свойства, создаваемого конструктором, вы всегда можете переопределить его и изменить его на любое нужное имя. Это можно сделать, изменив имя сущности или свойства в строке в конструкторе или изменив его с помощью сетки свойств.

По умолчанию LINQ to SQLный конструктор также проверяет связи первичного и внешнего ключей таблиц, и на их основе автоматически создает по умолчанию связи связей между различными создаваемыми классами модели. Например, при перетаскивании таблиц диннерс и RSVP в конструктор LINQ to SQL связь «один ко многим» между двумя была определена на основе того факта, что таблица RSVP имела внешний ключ к таблице диннерс (это обозначается стрелкой в элементе конструктор):

![](build-a-model-with-business-rule-validations/_static/image6.png)

Приведенная выше Ассоциация приведет к тому, что LINQ to SQL добавить в класс RSVP строго типизированное свойство "ужин", которое разработчики могут использовать для доступа к обеду, связанному с заданным RSVP. Кроме того, класс ужин будет иметь свойство сбора "RSVP", которое позволяет разработчикам извлекать и обновлять объекты RSVP, связанные с конкретным обедом.

Ниже показан пример IntelliSense в Visual Studio, когда мы создаем новый объект RSVP и добавляем его в коллекцию RSVP-оповещений компании Dinner. Обратите внимание, что LINQ to SQL автоматически добавила в объект ужин коллекцию "RSVP":

![](build-a-model-with-business-rule-validations/_static/image7.png)

Добавив объект RSVP в коллекцию RSVP-партнеров компании Dinner The, мы сообщаем LINQ to SQL связать связь внешнего ключа между компанией Dinner and the RSVP в нашей базе данных:

![](build-a-model-with-business-rule-validations/_static/image8.png)

Если вы не хотите, чтобы конструктор был смоделирован или назывался ассоциацией таблиц, его можно переопределить. Просто щелкните стрелку взаимосвязи в конструкторе и получите доступ к его свойствам через сетку свойств, чтобы переименовать, удалить или изменить ее. Однако для нашего приложения NerdDinner правила взаимосвязей по умолчанию хорошо подходят для создаваемых классов модели данных, и мы можем использовать поведение по умолчанию.

### <a name="nerddinnerdatacontext-class"></a>Класс Нерддиннердатаконтекст

Visual Studio автоматически создаст классы .NET, представляющие модели и связи базы данных, определенные с помощью конструктора LINQ to SQL. Для каждого файла конструктора LINQ to SQL, добавленного в решение, также создается LINQ to SQL класс DataContext. Так как мы назвали наш LINQ to SQL элемент класса «NerdDinner», созданный класс DataContext будет называться «Нерддиннердатаконтекст». Этот класс Нерддиннердатаконтекст является основным способом взаимодействия с базой данных.

Наш класс Нерддиннердатаконтекст предоставляет два свойства — "диннерс" и "RSVP", которые представляют две таблицы, смоделированные в базе данных. Можно использовать C# для записи запросов LINQ к этим свойствам для запроса и получения объектов Dinner и RSVP из базы данных.

В следующем коде показано, как создать экземпляр объекта Нерддиннердатаконтекст и выполнить запрос LINQ к нему для получения последовательности диннерс, которая возникает в будущем. Visual Studio предоставляет полную IntelliSense при написании запроса LINQ, а возвращенные из него объекты являются строго типизированными, а также поддерживают IntelliSense:

![](build-a-model-with-business-rule-validations/_static/image9.png)

Помимо предоставления запроса на получение объектов Dinner and RSVP, Нерддиннердатаконтекст также автоматически отслеживает все изменения, внесенные в объекты Dinnered и RSVP. Эту функцию можно использовать для простого сохранения изменений в базе данных, не требуя написания явного кода обновления SQL.

Например, в приведенном ниже коде показано, как использовать запрос LINQ для получения одного объекта Dinner из базы данных, обновления двух свойств ужина и сохранения изменений обратно в базу данных:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

Объект Нерддиннердатаконтекст в приведенном выше коде автоматически отследится от изменений свойств, внесенных в объект ужин, полученный из него. При вызове метода "SubmitChanges ()" будет выполнена соответствующая инструкция SQL "UPDATE" в базе данных для сохранения обновленных значений.

### <a name="creating-a-dinnerrepository-class"></a>Создание класса Диннеррепоситори

Для небольших приложений иногда удобно, чтобы контроллеры работали непосредственно с LINQ to SQL классом DataContext и внедрять запросы LINQ в контроллеры. Однако по мере того, как приложения получают больший размер, этот подход довольно громоздким для обслуживания и тестирования. Это также может привести к дублированию одних и тех же запросов LINQ в нескольких местах.

Один из подходов, позволяющих упростить обслуживание и тестирование приложений, заключается в использовании шаблона "репозитория". Класс репозитория помогает инкапсулировать запросы данных и логику сохраняемости, а также абстрагирует сведения о реализации сохраняемости данных из приложения. В дополнение к очистке кода приложения использование шаблона репозитория упрощает изменение реализаций хранилища данных в будущем и помогает выполнять модульное тестирование приложения, не требуя наличия реальной базы данных.

Для нашего приложения NerdDinner мы определим класс Диннеррепоситори с указанной ниже сигнатурой:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*Примечание. Далее в этой главе мы извлеким интерфейс Идиннеррепоситори из этого класса и разберем на наших контроллерах внедрение зависимостей. Тем не менее, начните с простого и просто начните работу непосредственно с классом Диннеррепоситори.*

Чтобы реализовать этот класс, щелкните правой кнопкой мыши папку Models и выберите команду **Добавить-&gt;создать элемент** меню. В диалоговом окне "Добавление нового элемента" мы выберем шаблон "class" и назовем имя файла "DinnerRepository.cs":

![](build-a-model-with-business-rule-validations/_static/image10.png)

Затем мы можем реализовать наш класс Диннеррепоситори, используя приведенный ниже код.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>Извлечение, обновление, вставка и удаление с помощью класса Диннеррепоситори

Теперь, когда мы создали наш класс Диннеррепоситори, рассмотрим несколько примеров кода, демонстрирующих распространенные задачи, которые мы можем сделать с ним:

#### <a name="querying-examples"></a>Примеры запросов

Приведенный ниже код извлекает один обед, используя значение Диннерид:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

Приведенный ниже код извлекает все предстоящие диннерс и циклы по ним:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>Примеры для вставки и обновления

В приведенном ниже коде показано добавление двух новых диннерс. Добавление или изменение репозитория не фиксируется в базе данных до тех пор, пока для него не будет вызван метод Save (). LINQ to SQL автоматически заключает все изменения в транзакции базы данных, так что все изменения происходят или ни одна из них не выполняется при сохранении репозитория:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

Приведенный ниже код извлекает существующий объект Dinnered и изменяет на нем два свойства. Изменения записываются обратно в базу данных, когда в нашем репозитории вызывается метод Save ():

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

Приведенный ниже код извлекает обед, а затем добавляет в него RSVP. Это делается с помощью коллекции RSVP для объекта Dinner, который LINQ to SQL создан для нас (поскольку существует связь «первичный-ключ — внешний ключ» между двумя объектами в базе данных). Это изменение сохраняется в базе данных как новая строка таблицы RSVP при вызове метода "Save ()" в репозитории:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Пример удаления

Приведенный ниже код извлекает существующий объект ужин, а затем помечает его как удаляемый. При вызове метода "Save ()" в репозитории он будет фиксировать удаление в базе данных:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>Интеграция проверки и логики бизнес-правил с классами модели

Интеграция проверки и логики бизнес-правил является ключевой частью любого приложения, которое работает с данными.

#### <a name="schema-validation"></a>Проверка схемы

Когда классы модели определяются с помощью конструктора LINQ to SQL, типы данных свойств в классах модели данные соответствуют типам данных таблицы базы. Например: если столбец «Евентдате» в таблице диннерс имеет значение «DateTime», то класс модели данных, созданный LINQ to SQL, будет иметь тип «DateTime» (встроенный тип данных .NET). Это означает, что при попытке присвоить ему целочисленное или логическое значение из кода произойдет ошибка компиляции, и при попытке неявного преобразования недействительного типа строки во время выполнения будет выводиться сообщение об ошибке.

LINQ to SQL также автоматически обрабатывает escape-значения SQL при использовании строк, что позволяет защитить вас от атак путем внедрения кода SQL при его использовании.

#### <a name="validation-and-business-rule-logic"></a>Логика проверки и бизнес-правил

Проверка схемы полезна в первую очередь, но она редко бывает достаточной. В большинстве реальных сценариев требуется возможность указывать расширенную логику проверки, которая может охватывать несколько свойств, выполнять код и часто имеет осведомленность о состоянии модели (например, создается/упдатед/делетед или в определенном для домена состоянии, например "Архивировано"). Существует множество различных шаблонов и платформ, которые можно использовать для определения и применения правил проверки к классам модели, и существует несколько платформ на основе .NET, которые можно использовать для помощи в этом. В приложениях ASP.NET MVC можно использовать практически любой из них.

Для нашего приложения NerdDinner мы будем использовать сравнительно простой и прямолинейный шаблон, где мы предоставляем свойство IsValid и метод Жетрулевиолатионс () для нашего объекта модели Dinner. Свойство IsValid возвратит значение true или false в зависимости от того, являются ли допустимыми все проверки и бизнес-правила. Метод Жетрулевиолатионс () возвратит список любых ошибок правил.

Мы реализуем IsValid и Жетрулевиолатионс () для нашей компании, добавив «частичный класс» в наш проект. Разделяемые классы можно использовать для добавления методов, свойств и событий в классы, поддерживаемые конструктором VS (например, класс Dinner, созданный конструктором LINQ to SQL), и помогает избежать перепутать средство с нашим кодом. Можно добавить в наш проект новый разделяемый класс, щелкнув правой кнопкой мыши папку \Моделс, а затем выбрав команду "добавить новый элемент". Затем можно выбрать шаблон "класс" в диалоговом окне "Добавление нового элемента" и присвоить ему имя Dinner.cs.

![](build-a-model-with-business-rule-validations/_static/image11.png)

Нажатие кнопки "Добавить" добавит файл Dinner.cs в наш проект и откроет его в интегрированной среде разработки. Затем можно реализовать базовую платформу применения правил или проверки, используя приведенный ниже код.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

Несколько замечаний о приведенном выше коде:

- Класс ужин предшествует ключевому слову "partial" — это означает, что код, содержащийся в нем, будет сочетаться с классом, созданным или обслуживаемым конструктором LINQ to SQL и скомпилированным в один класс.
- Класс Рулевиолатион — это вспомогательный класс, который будет добавлен в проект, позволяющий предоставлять дополнительные сведения о нарушении правил.
- Метод компании Dinner. Жетрулевиолатионс () приводит к вычислению нашей проверки и бизнес-правил (мы будем их реализовывать чуть позже). Затем он возвращает последовательность объектов Рулевиолатион, которые предоставляют дополнительные сведения об ошибках правил.
- Свойство "ужин. IsValid" предоставляет удобное вспомогательное свойство, которое указывает, имеет ли объект ужин какие-либо активные Рулевиолатионс. Он может быть заранее проверен разработчиком с помощью объекта Dinner в любое время (и не создает исключение).
- Частичный метод компании Dinner. OnValidate () является обработчиком, который LINQ to SQL предоставляет, что позволяет получать уведомления всякий раз, когда объект Dinner собирается сохраняться в базе данных. Приведенная выше реализация OnValidate () гарантирует, что ужин не Рулевиолатионс перед сохранением. Если он находится в недопустимом состоянии, вызывается исключение, которое приведет к LINQ to SQL прервать транзакцию.

Такой подход обеспечивает простую платформу, в которую можно интегрировать проверку и бизнес-правила. Теперь давайте добавим приведенные ниже правила в метод Жетрулевиолатионс ():

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

Мы используем функцию yield return C# в, чтобы вернуть последовательность любых рулевиолатионс. Первые шесть проверок правил выше просто обеспечивают, что строковые свойства в ужине не могут иметь значение null или быть пустыми. Последнее правило является несколько более интересным и вызывает вспомогательный метод Фоневалидатор. Исвалиднумбер (), который можно добавить в наш проект, чтобы проверить, соответствует ли формат номера Контактфоне странам компании Dinner.

Мы можем использовать. Поддержка регулярных выражений NET для реализации этой поддержки проверки телефона. Ниже приведена простая реализация Фоневалидатор, которую можно добавить в наш проект, что позволяет добавлять проверки шаблона регулярных выражений, зависящих от страны:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>Обработка нарушений проверки и бизнес-логики

Теперь, когда мы добавили приведенный выше код проверки и бизнес-правила, каждый раз при попытке создать или обновить обед будут оценены и применены правила логики проверки.

Разработчики могут написать код, подобный приведенному ниже, чтобы заранее определить, является ли объект ужин допустимым, и получить список всех нарушений в нем без вызова исключений.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

При попытке сохранить ужин в недопустимом состоянии будет вызвано исключение при вызове метода Save () для Диннеррепоситори. Это происходит потому, что LINQ to SQL автоматически вызывает разделяемый метод Dinner. OnValidate (), прежде чем он сохраняет изменения компании Dinnered, и мы добавили код в ужин. OnValidate (), чтобы вызвать исключение, если на обеде существуют какие-либо нарушения правил. Мы можем перехватить это исключение и в активном состоянии получить список нарушений для исправления:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

Так как наши проверки и бизнес-правила реализуются на уровне модели, а не на уровне пользовательского интерфейса, они будут применены и использованы во всех сценариях приложения. Позже мы можем изменить или добавить бизнес-правила, и весь код, который работает с нашими объектами компании, учитывает их.

Благодаря возможности изменять бизнес-правила в одном месте, не внося этих изменений в приложения и логику пользовательского интерфейса, это знакомство с хорошо написанным приложением и преимущество, которое может помочь платформе MVC.

### <a name="next-step"></a>Следующий шаг

Теперь у нас есть модель, которую можно использовать для запроса и обновления нашей базы данных.

Теперь добавим в проект некоторые контроллеры и представления, которые можно использовать для создания пользовательского интерфейса HTML.

> [!div class="step-by-step"]
> [Назад](create-a-database.md)
> [Вперед](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
