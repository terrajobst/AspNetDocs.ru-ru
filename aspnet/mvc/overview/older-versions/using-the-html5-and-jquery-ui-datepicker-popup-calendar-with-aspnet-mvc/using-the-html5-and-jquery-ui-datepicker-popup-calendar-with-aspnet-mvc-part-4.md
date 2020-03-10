---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 4 | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в ASP.NET МВ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433254"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 4

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в веб-приложении ASP.NET MVC.

### <a name="adding-a-template-for-editing-dates"></a>Добавление шаблона для редактирования дат

В этом разделе вы создадите шаблон для редактирования дат, который будет применяться, когда ASP.NET MVC отображает пользовательский интерфейс для редактирования свойств модели, которые помечены перечислением " **Дата** " атрибута [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) . Шаблон будет отображать только дату; время не будет отображаться. В шаблоне вы будете использовать всплывающий календарь [DatePicker в jQuery](http://jqueryui.com/demos/datepicker/) , чтобы предоставить способ редактирования дат.

Чтобы начать, откройте файл *Movie.CS* и добавьте атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) с перечислением **Date** в свойство `ReleaseDate`, как показано в следующем коде:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

Этот код приводит к тому, что поле `ReleaseDate` отображается без времени в обоих шаблонах отображения и при изменении шаблонов. Если приложение содержит шаблон *Date. cshtml* в папке *виевс\шаред\едитортемплатес* или в папке *виевс\мовиес\едитортемплатес* , этот шаблон будет использоваться для отрисовки любого свойства `DateTime` при редактировании. В противном случае встроенная система шаблонов ASP.NET будет отображать свойство как дату.

Для запуска приложения нажмите сочетание клавиш CTRL+F5. Выберите ссылку изменить, чтобы убедиться, что поле ввода для даты выпуска показывает только дату.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

В **Обозреватель решений**разверните папку *представления* , разверните *общую* папку, а затем щелкните правой кнопкой мыши папку *виевс\шаред\едитортемплатес* .

Нажмите кнопку **Добавить**, а затем — **вид**. Откроется диалоговое окно **Добавление представления** .

В поле **имя представления** введите &quot;Date&quot;.

Установите флажок **создать как частичное представление** . Убедитесь, что не установлены флажки **использовать макет или эталонную страницу** и **создать строго типизированное представление** .

Нажмите кнопку **Добавить**. Создается шаблон *виевс\шаред\едитортемплатес\дате.кштмл* .

Добавьте следующий код в шаблон *виевс\шаред\едитортемплатес\дате.кштмл* .

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

Первая строка объявляет модель типом `DateTime`. Хотя вам не нужно объявлять тип модели в шаблонах редактирования и отображения, рекомендуется, чтобы во время компиляции была выполнена проверка модели, передаваемой в представление. (Другое преимущество заключается в том, что вы получаете IntelliSense для модели в представлении в Visual Studio.) Если тип модели не объявлен, ASP.NET MVC считает его [динамическим](https://msdn.microsoft.com/library/dd264741.aspx) типом и не проверяет тип во время компиляции. Если вы объявили модель как тип `DateTime`, она станет строго типизированной.

Вторая строка представляет собой литеральную HTML-разметку, которая отображает &quot;с использованием шаблона даты&quot; до поля даты. Эта строка будет временно использоваться для проверки того, что шаблон даты используется.

Следующая строка представляет собой вспомогательный элемент [HTML. TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) , который визуализирует `input` поле, которое является текстовым полем. Третий параметр для вспомогательного метода использует анонимный тип, чтобы задать для текстового поля класс `datefield` и тип для `date`. (Поскольку `class` является зарезервированным C#в, необходимо использовать `@`ный символ для экранирования атрибута `class` в C# средстве синтаксического анализа.)

Тип `date` является входным типом HTML5, который позволяет браузерам, поддерживающим HTML5, визуализировать элемент управления "Календарь HTML5". Позже вы добавите JavaScript для подключения к элементу DatePicker, который будет использоваться в элементе `Html.TextBox`, используя класс `datefield`.

Для запуска приложения нажмите сочетание клавиш CTRL+F5. Можно проверить, что свойство `ReleaseDate` в представлении редактирования использует шаблон редактирования, поскольку шаблон отображает &quot;шаблон даты&quot; непосредственно перед полем ввода текста `ReleaseDate`, как показано на рисунке ниже.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

В браузере просмотрите исходный код страницы. (Например, щелкните страницу правой кнопкой мыши и выберите пункт **Просмотр источника**.) В следующем примере показана часть разметки для страницы, в которой показаны атрибуты `class` и `type` в отображаемом HTML-коде.

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

Вернитесь к шаблону *виевс\шаред\едитортемплатес\дате.кштмл* и удалите &quot;с помощью шаблона даты&quot; разметки. Теперь готовый шаблон выглядит следующим образом:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>Добавление всплывающего календаря DatePicker пользовательского интерфейса jQuery с помощью NuGet

В этом разделе вы добавите в шаблон "Дата-изменение" всплывающий календарь [DatePicker пользовательского интерфейса jQuery](http://jqueryui.com/demos/datepicker/) . Библиотека [пользовательского интерфейса jQuery](http://jqueryui.com/) обеспечивает поддержку анимации, дополнительных эффектов и настраиваемых мини-приложений. Она построена на основе библиотеки jQuery JavaScript Library. Всплывающий календарь DatePicker позволяет легко и естественным образом вводить даты с помощью календаря вместо ввода строки. Всплывающий календарь также ограничивает число пользователей юридическими датами — обычный ввод текста для даты позволяет ввести нечто вроде `2/33/1999` (Февраль 33rd, 1999), но всплывающий календарь [DatePicker в jQuery](http://jqueryui.com/demos/datepicker/) не допускает этого.

Сначала необходимо установить библиотеки пользовательского интерфейса jQuery. Для этого вы будете использовать NuGet, который является диспетчером пакетов, включенным в версии с пакетом обновления 1 (SP1) Visual Studio 2010 и Visual Web Developer.

В Visual Web Developer в меню **Сервис** выберите **Диспетчер пакетов NuGet** , а затем щелкните **Управление пакетами NuGet**.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

Примечание. Если в меню " **Сервис** " не отображается команда **Диспетчер пакетов NuGet** , необходимо установить NuGet, следуя инструкциям на странице [Установка NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) на веб-сайте NuGet.   
  
Если вы используете Visual Studio вместо Visual Web Developer, в меню **Сервис** выберите **Диспетчер пакетов NuGet** , а затем щелкните **Добавить ссылку на пакет библиотеки**.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

В диалоговом окне **MVCMovie — Управление пакетами NuGet** щелкните вкладку в **Интернете** слева, а затем введите &quot;jQuery. UI&quot; в поле поиска. Выберите команду j **запрос мини-приложений пользовательского интерфейса: DatePicker**, а затем нажмите кнопку **установить** .

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet добавляет эти отладочные версии и минифицированные версии ядра пользовательского интерфейса jQuery и средство выбора даты пользовательского интерфейса jQuery в проект:

- *jQuery. UI. Core. js*
- *jQuery. UI. Core. min. js*
- *jQuery. UI. DatePicker. js*
- *jQuery. UI. DatePicker. min. js*

Примечание. отладочные версии (файлы без расширения *. min. js* ) полезны для отладки, но на рабочем сайте можно включать только версии минифицированные.

Чтобы фактически использовать средство выбора даты jQuery, необходимо создать скрипт jQuery, который будет подключать мини-приложение календаря к шаблону редактирования. В **Обозреватель решений**щелкните правой кнопкой мыши папку *сценарии* и выберите **Добавить**, затем **новый элемент**и **файл JScript**. Назовите файл *датепиккерреади. js*.

Добавьте следующий код в файл *датепиккерреади. js* :

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

Если вы не знакомы с jQuery, вот краткое объяснение того, что это делает: первая строка — это функция &quot;jQuery&quot;, которая вызывается после загрузки всех элементов DOM на странице. Во второй строке выбираются все элементы DOM, имена которых имеют имя класса `datefield`, а затем вызывается функция `datepicker` для каждого из них. (Не забывайте, что вы добавили класс `datefield` в шаблон *виевс\шаред\едитортемплатес\дате.кштмл* ранее в этом руководстве.)

Затем откройте файл *Views\Shared\\_layout. cshtml* . Необходимо добавить ссылки на следующие файлы, которые являются обязательными, чтобы можно было использовать элемент выбора даты:

- *Content/themes/Base/jQuery. UI. Core. CSS*
- *Content/themes/Base/jQuery. UI. DatePicker. CSS*
- *Содержимое/темы/базовый/jQuery. UI. Theme. CSS*
- *jQuery. UI. Core. min. js*
- *jQuery. UI. DatePicker. min. js*
- *Датепиккерреади. js*

В следующем примере показан фактический код, который необходимо добавить в нижнюю часть элемента `head` в файле *Views\Shared\\_layout. cshtml* .

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

Ниже приведен полный раздел `head`.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[Вспомогательный метод содержимого URL-адреса](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) преобразует путь ресурса в абсолютный путь. Для правильной ссылки на эти ресурсы при выполнении приложения в службах IIS необходимо использовать `@URL.Content`.

Для запуска приложения нажмите сочетание клавиш CTRL+F5. Выберите ссылку изменить, а затем поместите точку вставки в поле **ReleaseDate** . Откроется всплывающий календарь jQuery UI.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

Как и большинство элементов управления jQuery, DatePicker позволяет легко настроить его. Дополнительные сведения см. в разделе [визуальная настройка: проектирование темы пользовательского интерфейса jQuery](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) на сайте [пользовательского интерфейса jQuery](http://learn.jquery.com/jquery-ui/getting-started/) .

### <a name="supporting-the-html5-date-input-control"></a>Поддержка элемента управления вводом даты HTML5

Так как больше браузеров поддерживают HTML5, необходимо использовать собственные входные данные HTML5, например элемент ввода `date`, и не использовать календарь jQuery UI. Вы можете добавить в приложение логику для автоматического использования элементов управления HTML5, если они поддерживаются браузером. Для этого замените содержимое файла *датепиккерреади. js* следующим:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

Первая строка этого скрипта использует Modernizr, чтобы проверить, поддерживается ли ввод даты HTML5. Если он не поддерживается, то вместо него подключается средство выбора даты пользовательского интерфейса jQuery. ([Modernizr](http://www.modernizr.com/docs/) — это библиотека JavaScript с открытым исходным кодом, которая определяет доступность собственных реализаций HTML5 и CSS3. Modernizr входит в любые новые проекты ASP.NET MVC, которые вы создадите.)

После внесения этого изменения можно протестировать его с помощью браузера, поддерживающего HTML5, например Opera 11. Запустите приложение с помощью браузера, совместимого с HTML5, и измените запись фильма. Вместо всплывающего календаря jQuery UI используется элемент управления даты HTML5:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

Так как новые версии браузеров реализуют HTML5 постепенно, хорошим подходом для этого является добавление кода на веб-сайт, который поддерживает широкий спектр возможностей поддержки HTML5. Например, ниже показан более надежный скрипт *датепиккерреади. js* , позволяющий веб-сайту поддерживать браузеры, которые только частично поддерживают управление датой HTML5.

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

Этот сценарий выбирает HTML5 `input` элементы типа `date`, которые не поддерживают элемент управления даты HTML5 полностью. Для этих элементов он подключается к календарному меню пользовательского интерфейса jQuery, а затем изменяет атрибут `type` с `date` на `text`. Изменив атрибут `type` с `date` на `text`, отключается поддержка частичной даты HTML5. Еще более надежный сценарий *датепиккерреади. js* можно найти по адресу [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).

### <a name="adding-nullable-dates-to-the-templates"></a>Добавление в шаблоны дат, допускающих значения NULL

Если вы используете один из существующих шаблонов дат и передайте дату null, вы получите ошибку времени выполнения. Чтобы сделать шаблоны дат более надежными, вы измените их, чтобы они обрабатывали значения NULL. Для поддержки дат, допускающих значения NULL, измените код в *виевс\шаред\дисплайтемплатес\датетиме.кштмл* следующим образом:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

Если модель имеет **значение NULL**, код возвращает пустую строку.

Измените код в файле *виевс\шаред\едитортемплатес\дате.кштмл* следующим образом:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

При выполнении этого кода, если модель не имеет значение null, используется значение `DateTime` модели. Если модель имеет значение null, вместо нее используется текущая дата.

### <a name="wrapup"></a>врапуп

В этом учебнике были рассмотрены основы ASP.NET шаблонов, а также показано, как использовать всплывающий календарь DatePicker для jQuery в приложении ASP.NET MVC. Дополнительные сведения см. в следующих ресурсах:

- Сведения о локализации см. в блоге Ражиш [Жкуерюи DatePicker в ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).
- Дополнительные сведения о пользовательском интерфейсе jQuery см. в статье о ПОЛЬЗОВАТЕЛЬСКОМ интерфейсе [jQuery](http://docs.jquery.com/UI).
- Сведения о локализации элемента управления DatePicker см. в разделе [UI/DatePicker/Localization](http://docs.jquery.com/UI/Datepicker/Localization).
- Дополнительные сведения о шаблонах MVC ASP.NET см. в статье о [шаблонах ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)в блоге Михаил Уилсон (. Несмотря на то, что серия была написана для ASP.NET MVC 2, материал по-прежнему применяется к текущей версии ASP.NET MVC.

> [!div class="step-by-step"]
> [Назад](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
