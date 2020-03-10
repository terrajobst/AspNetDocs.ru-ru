---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: Добавление проверки в модель (C#) | Документация Майкрософт
author: Rick-Anderson
description: Создание контроллера
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 19d86dc0df931a9d135e46209559892b77626cf6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498828"
---
# <a name="adding-validation-to-the-model-c"></a>Добавление проверки в модель (C#)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Обновленная версия этого учебника доступна [здесь](../../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.
> 
> 
> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:
> 
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Для этого раздела доступен проект Visual C# Web Developer с исходным кодом. [Скачайте C# версию](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Если вы предпочитаете Visual Basic, переключитесь на [Visual Basic версию](../vb/intro-to-aspnet-mvc-3.md) этого учебника.

В этом разделе вы добавите логику проверки к модели `Movie`, и вы убедитесь, что правила проверки применяются каждый раз, когда пользователь попытается создать или изменить фильм с помощью приложения.

## <a name="keeping-things-dry"></a>Поддержание СУХИх вещей

Один из основных принципов проектирования ASP.NET MVC — сухой ("принцип"Не повторяйся""). ASP.NET MVC позволяет указать функциональные возможности или поведение только один раз, после чего они будут отражены в любом приложении. Это сокращает объем кода, который необходимо написать, и делает написанный код гораздо проще в обслуживании.

Поддержка проверки, предоставляемая ASP.NET MVC и Entity Framework Code First, является хорошим примером принципа сухой в действии. Правила проверки можно декларативно задавать в одном месте (в классе Model), а затем эти правила применяются везде в приложении.

Рассмотрим, как можно воспользоваться преимуществами этой поддержки проверки в приложении Movie.

## <a name="adding-validation-rules-to-the-movie-model"></a>Добавление правил проверки к модели фильмов

Начнем с добавления логики проверки к классу `Movie`.

Откройте файл *Movie.cs*. Добавьте в начало файла инструкцию `using`, которая ссылается на пространство имен [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) :

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

Пространство имен является частью .NET Framework. Он предоставляет встроенный набор атрибутов проверки, которые можно декларативно применять к любому классу или свойству.

Теперь обновите класс `Movie`, чтобы воспользоваться преимуществами встроенных [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)и [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) атрибутов проверки. Используйте следующий код в качестве примера того, где применять атрибуты.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

Атрибуты проверки определяют поведение для свойств модели, к которым они применяются. Атрибут `Required` указывает, что свойство должно иметь значение. в этом примере фильм должен иметь значения для свойств `Title`, `ReleaseDate`, `Genre`и `Price`, чтобы быть допустимыми. Атрибут `Range` ограничивает диапазон значений. Атрибут `StringLength` позволяет задать максимальную и при необходимости минимальную длину строкового свойства.

Code First гарантирует, что правила проверки, указанные в классе модели, будут применены, прежде чем приложение сохранит изменения в базе данных. Например, приведенный ниже код вызывает исключение при вызове метода `SaveChanges`, так как отсутствуют несколько обязательных `Movie` значений свойств и цена равна нулю (за пределами допустимого диапазона).

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

Если правила проверки автоматически принудительно применяются .NET Framework помогает сделать приложение более надежным. Это также гарантирует, что в любом случае будут выполнены все проверки и в базе данных не будут случайно оставлены поврежденные данные.

Ниже приведен полный листинг кода для обновленного файла *Movie.CS* :

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>Пользовательский интерфейс ошибки проверки в ASP.NET MVC

Повторно запустите приложение и перейдите по URL-адресу */Movies* .

Щелкните ссылку **создать фильм** , чтобы добавить новый фильм. Заполните форму недопустимыми значениями и нажмите кнопку " **создать** ".

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

Обратите внимание, что форма автоматически использовала цвет фона для выделения текстовых полей, содержащих недопустимые данные, и выдает соответствующее сообщение об ошибке проверки рядом с каждым из них. Сообщения об ошибках соответствуют строкам ошибок, указанным при создании заметки к `Movie` классу. Эти ошибки применяются как на стороне клиента (с помощью JavaScript), так и на стороне сервера (если пользователь отключил JavaScript).

Настоящим преимуществом является то, что вам не пришлось изменять одну строку кода в классе `MoviesController` или в представлении *Create. cshtml* , чтобы включить этот пользовательский интерфейс проверки. Контроллер и представления, созданные ранее в этом учебнике, автоматически задают правила проверки, заданные с помощью атрибутов класса модели `Movie`.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Как выполняется проверка в методе создания представления и создания действия

Вам может быть интересно, как пользовательский интерфейс проверки создается без обновления кода контроллера или представлений. В следующем листинге показано, как выглядят методы `Create` в классе `MovieController`. Они не изменяются из того, как вы создали их ранее в этом руководстве.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

Первый метод действия отображает начальную форму создания. Второй обрабатывает форму Post. Второй метод `Create` вызывает `ModelState.IsValid`, чтобы проверить, имеются ли в фильме ошибки проверки. При вызове этого метода оцениваются все атрибуты проверки, которые были применены к объекту. Если объект содержит ошибки проверки, метод `Create` повторно отображает форму. Если ошибок нет, метод сохраняет новый фильм в базе данных.

Ниже приведен шаблон представления *Create. cshtml* , сформированный ранее в этом руководстве. Он используется в показанных выше методах действия для отображения исходной формы и повторного вывода формы в случае ошибки.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

Обратите внимание, что в коде используется вспомогательный метод `Html.EditorFor` для вывода элемента `<input>` для каждого свойства `Movie`. Рядом с этим вспомогательным модулем вызывается вспомогательный метод `Html.ValidationMessageFor`. Эти два вспомогательных метода работают с объектом модели, который передается контроллером в представление (в данном случае это объект `Movie`). Они автоматически ищут атрибуты проверки, указанные в модели, и отображают сообщения об ошибках соответствующим образом.

Все, что хорошо замечательно в этом подходе, заключается в том, что ни контроллер, ни шаблон создания представления не знают о фактических правилах проверки, которые применяются, или о конкретных сообщениях об ошибках. Правила проверки и строки ошибок указываются только в классе `Movie`.

Если вы хотите изменить логику проверки позже, это можно сделать в одном месте. Вам не придется беспокоиться о несогласованности применения правил в различных частях приложения, поскольку вся логика проверки будет определена в одном месте и начнет применяться по всему приложению. Это позволяет максимально оптимизировать код и обеспечить удобство его совершенствования и поддержки. Кроме того, таким образом вы будете полностью соблюдать требования принципа "Не повторяйся".

## <a name="adding-formatting-to-the-movie-model"></a>Добавление форматирования в модель фильмов

Откройте файл *Movie.cs*. Пространство имен [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) предоставляет атрибуты форматирования в дополнение к встроенному набору атрибутов проверки. Вы примените атрибут [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) и значение перечисления [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) к дате выпуска и к полям цены. В следующем коде показаны свойства `ReleaseDate` и `Price` с соответствующим атрибутом [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) .

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

Кроме того, можно явно задать значение [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) . В следующем коде показано свойство Дата выпуска со строкой формата даты (а именно, "d"). Этот параметр используется для указания, что вы не хотите использовать время в качестве части даты выпуска.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

Следующий код форматирует свойство `Price` как денежное.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

Ниже приведен полный класс `Movie`.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

Запустите приложение и перейдите к контроллеру `Movies`.

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

В следующей части этой серии мы рассмотрим приложение и внесем ряд изменений в автоматически создаваемые методы `Details` и `Delete`.

> [!div class="step-by-step"]
> [Назад](adding-a-new-field.md)
> [Вперед](improving-the-details-and-delete-methods.md)
