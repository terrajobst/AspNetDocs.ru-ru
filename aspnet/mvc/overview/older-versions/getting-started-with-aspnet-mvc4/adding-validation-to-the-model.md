---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: Добавление проверки в модель | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленную версию этого учебника доступен здесь, использующий ASP.NET MVC 5 и Visual Studio 2013. Это более безопасное и гораздо проще выполнить и демонстрационных версий...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 5819d789f31b9452d40ae3aa7f821f101ae126ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049481"
---
<a name="adding-validation-to-the-model"></a>Добавление проверки в модель
====================
по [Рик Андерсон]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > Обновленную версию этого учебника доступен [здесь](../../getting-started/introduction/getting-started.md) , использующий ASP.NET MVC 5 и Visual Studio 2013. Она более безопасные, гораздо проще следовать и показаны дополнительные возможности.


В этом разделе вы добавите логику проверки `Movie` модель также вы убедитесь, что правила проверки применяются каждый раз, пользователь пытается создать или изменить фильм в приложении.

## <a name="keeping-things-dry"></a>Чтобы оставить "не повторяйся"

Одним из основных принципов разработки ASP.NET MVC является DRY (&quot;Don't Repeat Yourself&quot;). ASP.NET MVC рекомендует указать функциональные возможности или поведение только один раз, а затем их в приложении. Это уменьшает объем кода, необходимые для записи и делает код, который вы пишете менее подверженной ошибкам и упрощает поддержку.

Поддержка проверки, реализуемая ASP.NET MVC и Entity Framework Code First является отличным примером принципа "не повторяйся" в действии. Правила проверки декларативно определяются в одном месте (в классе модели) и затем применяются везде в приложении.

Давайте рассмотрим, как можно воспользоваться преимуществами этой поддержки проверки в приложении фильма.

## <a name="adding-validation-rules-to-the-movie-model"></a>Добавление правил проверки к модели фильма

Сначала вы создадите добавить некоторую логику проверки для `Movie` класса.

Откройте файл *Movie.cs*. Добавить `using` инструкция в верхней части файла, который ссылается на [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) пространство имен:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

Обратите внимание, что пространство имен не содержит `System.Web`. Класс DataAnnotations предоставляет набор встроенных атрибутов проверки, которые можно декларативно применяются к любому классу или свойству.

Теперь обновите `Movie` класса, чтобы воспользоваться преимуществами встроенных [ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), и [ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) атрибуты проверки . Используйте следующий код в качестве примера применения атрибутов.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

Запустите приложение и снова появится следующая ошибка времени выполнения:

***Модель, поддерживающая контекст «MovieDBContext» изменилось с момента создания базы данных. Рассмотрите возможность использования Code First Migrations для обновления базы данных ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).***

Мы будем использовать миграции для обновления схемы. Выполните сборку решения, а затем откройте **консоль диспетчера пакетов** окна и введите следующие команды:

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

По завершении этой команды Visual Studio открывает файл класса, который определяет новый `DbMIgration` производный класс с указанным именем (*AddDataAnnotationsMig*) и в `Up` метода вы увидите код, который обновляется ограничения схемы. `Title` И `Genre` поля больше не допускают значение NULL (то есть необходимо ввести значение) и `Rating` поле имеет длину не более 5.

Атрибуты проверки определяют поведение для свойств модели, к которым они применяются. `Required` Атрибут указывает, что свойство должно иметь значение; в этом образце фильм должен иметь значения для `Title`, `ReleaseDate`, `Genre`, и `Price` свойства, чтобы быть допустимыми. Атрибут `Range` ограничивает диапазон значений. Атрибут `StringLength` позволяет задать максимальную и при необходимости минимальную длину строкового свойства. Встроенные типы (такие как `decimal, int, float, DateTime`) требуются по умолчанию и нет необходимости `Required` атрибута.

Код сначала гарантирует, что правила проверки, определенные на класс модели применяются, прежде чем приложение сохраняет изменения в базе данных. Например, приведенный ниже код приведет к возникновению исключения при `SaveChanges` вызывается метод, так как некоторые необходимые `Movie` значения свойств отсутствуют, и стоимость равна нулю (что находится вне допустимого диапазона).

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

Наличие правил проверки, автоматически применяются в .NET Framework помогает сделать приложение более надежным. Это также гарантирует, что в любом случае будут выполнены все проверки и в базе данных не будут случайно оставлены поврежденные данные.

Ниже приведен полный листинг кода для обновленного *Movie.cs* файла:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>Ошибка проверки пользовательского интерфейса в ASP.NET MVC

Повторно запустите приложение и перейдите к */Movies* URL-адрес.

Нажмите кнопку **Create New** ссылку, чтобы добавить новый фильм. Заполните форму какие-либо недопустимые значения и нажмите кнопку **создать** кнопки.

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> Поддержка проверки jQuery для английского, используйте запятую (&quot;,&quot;) для десятичной запятой, необходимо включить *globalize.js* и конкретными *cultures/globalize.cultures.js* файла (из [ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) и JavaScript, чтобы использовать `Globalize.parseFloat`. В следующем коде показано изменения в файл Views\Movies\Edit.cshtml для работы с &quot;fr-FR&quot; языка и региональных параметров:


[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

Обратите внимание на то, как формы автоматически использовал цвет красную границу для выделения текстовые поля, которые содержат недопустимые данные и испускаемого сообщение об ошибке соответствующей проверкой рядом с каждого из них. Эти ошибки применяются как на стороне клиента (с помощью JavaScript и jQuery), так и на стороне сервера (если пользователь отключает JavaScript).

Реальные преимущество в том, что вам не нужно менять ни единой строчки кода в `MoviesController` класса или в *Create.cshtml* для реализации этой проверки пользовательского интерфейса. В контроллере и представлениях, создаваемых в рамках этого руководства, автоматически применяются правила проверки, для определения которых к свойствам класса модели `Movie` были применены атрибуты.

Вы могли заметить, для свойств `Title` и `Genre`, атрибут required не применяется принудительно до отправки формы (попадания **создать** кнопку), или введите текст в поле ввода и удалили ее. Для поля которого изначально пуста (например, поля представления создания) и содержит только обязательный атрибут и нет других атрибутов проверки, необходимо выполнить следующую команду, чтобы активировать проверки действий.

1. Вкладки в поле.
2. Введите любой текст.
3. Выйдите из поля с помощью клавиши TAB.
4. Перейти обратно в поле.
5. Удалите текст.
6. Выйдите из поля с помощью клавиши TAB.

Приведенную выше последовательность будет активировать проверку без обращения «отправить». Просто нажатие кнопки отправки без полей ввода активирует проверки на стороне клиента. Данные формы передаются на сервер только после того, как будут устранены любые ошибки на стороне клиента. Вы можете проверить это, установите точку останова в методе HTTP Post или с помощью [инструмента fiddler](http://fiddler2.com/fiddler2/) или IE 9 [средства разработчика F12](https://msdn.microsoft.com/ie/aa740478).

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Проверка происходит в создания, просмотра и создания метода действия

Вам может быть интересно, как пользовательский интерфейс проверки создается без обновления кода контроллера или представлений. Далее показан что `Create` методы в `MovieController` выглядят класса. Они изменились по сравнению с как вы создали их ранее в этом учебнике.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

Первый метод действия `Create` (HTTP GET) отображает исходную форму создания. Вторая версия (`[HttpPost]`) обрабатывает передачу формы. Второй метод `Create` (версия `HttpPost`) вызывает `ModelState.IsValid`, который определяет наличие ошибок проверки в фильме. При вызове этого метода оцениваются все атрибуты проверки, которые были применены к объекту. При наличии ошибок проверки в объекте метод `Create` повторно отображает форму. Если ошибок нет, метод сохраняет новый фильм в базе данных. В нашем примере фильма, мы используем **форма не передается на сервер, при наличии ошибок проверки, обнаруженные на стороне клиента; второй** `Create` **никогда не вызывается метод**. Если отключить JavaScript в браузере, проверка клиента отключена и HTTP POST `Create` вызовы методов `ModelState.IsValid` для проверки, имеет ли фильм ошибок проверки.

Вы можете установить точку останова в метод `HttpPost Create` и убедиться, что он не вызывается и данные формы не передаются, если на стороне клиента присутствуют ошибки проверки. Если отключить JavaScript в браузере и отправить форму с ошибками, будет достигнута точка останова. Без JavaScript вы по-прежнему будете получать полную проверку. Ниже показано, как отключить JavaScript в Internet Explorer.

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

На следующем рисунке показано, как отключить JavaScript в браузере FireFox.

![](adding-validation-to-the-model/_static/image5.png)

Ниже показано, как отключить JavaScript с браузером Chrome.

![](adding-validation-to-the-model/_static/image6.png)

Ниже приведен *Create.cshtml* шаблон представления, сформированного ранее в этом руководстве. Он используется в показанных выше методах действия для отображения исходной формы и повторного вывода формы в случае ошибки.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

Обратите внимание на то, как в коде используется `Html.EditorFor` вспомогательный метод для вывода `<input>` для каждого элемента `Movie` свойство. Рядом с этого вспомогательного объекта представляет собой вызов `Html.ValidationMessageFor` вспомогательный метод. Эти два вспомогательных метода работы с объектом модели, который передается с помощью контроллера в представление (в этом случае `Movie` объекта). Они автоматически выполняют поиск атрибутов проверки, указанные на модели и отображение сообщения об ошибках соответствующим образом.

Замечательный об этом подходе то, что ни контроллер, ни шаблон представления создать ничего не знают о применяемых правилах проверки или отображаемых сообщениях об ошибках. Правила проверки и строки ошибок указываются только в классе `Movie`. Такие же правила проверки автоматически применяются к представления изменения и любым другим представлениям, можно создать, изменить модель.

Если вы хотите изменить логику проверки позже, вы ее можно сделать в одном месте, добавив атрибуты проверки в модель (в этом примере `movie` класса). Вам не придется беспокоиться о несогласованности применения правил в различных частях приложения, поскольку вся логика проверки будет определена в одном месте и начнет применяться по всему приложению. Это позволяет максимально оптимизировать код и обеспечить удобство его совершенствования и поддержки. Кроме того, таким образом вы будете полностью соблюдать требования принципа "Не повторяйся".

## <a name="adding-formatting-to-the-movie-model"></a>Добавление форматирования к модели фильма

Откройте файл *Movie.cs* и проверьте класс `Movie`. [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) Пространство имен предоставляет атрибуты форматирования в дополнение к набору встроенных атрибутов проверки. Мы уже использовали [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) значение перечисления для даты выпуска и поля цены. В следующем коде показан `ReleaseDate` и `Price` свойства с соответствующим [ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) атрибута.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) Атрибуты не являются атрибуты проверки, они используются для указаний обработчик представлений для визуализации HTML. В примере выше `DataType.Date` атрибут отображает фильма даты в виде даты, без времени. Например, следующая [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) атрибуты не проверки формата данных:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

Атрибуты, указанные выше только предоставить подсказки для обработчик представлений для форматирования данных (а также другие атрибуты, такие как &lt;&gt; для URL-адреса и &lt;a href =&quot;mailto:EmailAddress.com&quot; &gt; для электронной почты. Можно использовать [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) атрибута для проверки формата данных.

Альтернативный подход к использованию `DataType` атрибуты, можно явно задать [ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx) значение. В следующем коде показано свойство даты выпуска с помощью строки формата даты (а именно, &quot;d&quot;). Это используется для указания, что вы не хотите времени как часть даты выпуска.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

Полный `Movie` класса приведен ниже.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

Запустите приложение и перейдите к `Movies` контроллера. Дата выпуска и цена хорошо форматируются. На рисунке ниже показана дата выпуска и цен с помощью &quot;fr-FR&quot; как язык и региональные параметры.

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

На следующем рисунке показаны те же данные, отображаются с языком и региональными параметрами по умолчанию (на английском языке для США).

![](adding-validation-to-the-model/_static/image8.png)

В следующей части этой серии мы рассмотрим приложение и внесем ряд изменений в автоматически создаваемые методы `Details` и `Delete`.

> [!div class="step-by-step"]
> [Назад](adding-a-new-field-to-the-movie-model-and-table.md)
> [Вперед](examining-the-details-and-delete-methods.md)