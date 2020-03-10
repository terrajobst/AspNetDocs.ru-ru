---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: Использование вспомогательного приложения DropDownList с ASP.NET MVC | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 6375bb2be158cea18309ffa71c71ac3e67bc91ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433080"
---
# <a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>Использование вспомогательного приложения DropDownList в ASP.NET MVC

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

В этом учебнике рассматриваются основы работы с вспомогательным приложением [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) и вспомогательным модулем [ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) в веб-приложении ASP.NET MVC. Для работы с руководством можно использовать Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1). это бесплатная версия Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:

- [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)<a id="post"></a>
- [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)

Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack). В этом учебнике предполагается, что вы выполнили учебное руководство [по ASP.NET MVC](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или руководство по[ASP.NETу музыкальному магазину MVC](../mvc-music-store/mvc-music-store-part-1.md) или знакомы с ASP.NET MVC. Это руководство начинается с измененного проекта из руководства по [ASP.NETу музыкальному хранилищу MVC](../mvc-music-store/mvc-music-store-part-1.md) . Вы можете скачать начальный проект по следующей ссылке, чтобы [скачать C# версию](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829).

Для этого раздела доступен проект Visual Web Developer с C# исходным кодом завершенного учебника. [Скачайте](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d).

### <a name="what-youll-build"></a>Что вы создадите

Вы создадите методы и представления действий, которые используют вспомогательную функцию [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) для выбора категории. Кроме того, **jQuery** будет использоваться для добавления диалогового окна «Вставка категории», которое может использоваться при необходимости создания новой категории (например, «жанр» или «исполнитель»). Ниже приведен снимок экрана с представлением создание, показывающее ссылки для добавления нового жанра и добавления нового исполнителя.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>Чему вы научитесь

В этом учебнике вы узнаете:

- Использование вспомогательного метода [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) для выбора данных категории.
- Добавление диалогового окна **jQuery** для добавления новых категорий.

### <a name="getting-started"></a>Приступая к работе

Начните с скачивания начального проекта со следующей ссылкой [загрузить](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829). В проводнике Windows щелкните правой кнопкой мыши файл *DDL\_Starter. zip* и выберите пункт Свойства. В диалоговом окне **Свойства DDL\_Starter. zip** выберите Разблокировать.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

Щелкните правой кнопкой мыши файл DDL\_Starter. zip и выберите **извлечь все** , чтобы распаковать файл. Откройте файл *стартмусиксторе. sln* в Visual web Developer 2010 Express («Visual Web Developer» или «vWD» для краткой) или Visual Studio 2010.

Нажмите клавиши CTRL + F5, чтобы запустить приложение, и щелкните ссылку **проверить** .

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

Выберите ссылку **выбрать категорию фильмов (простая)** . Отобразится список выбора типа фильма с комедия выбранным значением.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

Щелкните правой кнопкой мыши в браузере и выберите Просмотреть источник. Отобразится HTML для страницы. В приведенном ниже коде показан HTML-код для элемента SELECT.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

Можно увидеть, что каждый элемент в списке выбора имеет значение (0 для Action, 1 для драма, 2 для комедия и 3 для вымышленной науки) и отображаемое имя (Action, драма, комедия и научные вымышление). Приведенный выше код является стандартным HTML для списка выбора.

Измените список выбора на драма и нажмите кнопку **Submit (отправить** ). URL-адрес в браузере `http://localhost:2468/Home/CategoryChosen?MovieType=1`, и откроется страница с **выбранным параметром: 1**.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

Откройте файл *Controllers\HomeController.CS* и изучите метод `SelectCategory`.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

Вспомогательная функция [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) , используемая для создания списка HTML-выбора, требует, чтобы объект **IEnumerable&lt;селектлиститем &gt;** явно или неявно. То есть можно передать **ienumerable&lt;селектлиститем &gt;** явно в вспомогательную функцию [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) , или добавить **&gt;IEnumerable&lt;селектлиститем** в [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) , используя то же имя для **селектлиститем** в качестве свойства модели. Передача **селектлиститем** неявно и явно рассматривается в следующей части руководства. В приведенном выше коде показан самый простой способ создания объекта **IEnumerable&lt;селектлиститем &gt;** и заполнения его текстом и значениями. Обратите внимание, что для свойства `Comedy`[Селектлиститем](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) [выбрано](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx) **значение true.** при этом отображаемый список выбора будет показывать **комедия** в качестве выбранного элемента списка.

Объект **IEnumerable&lt;селектлиститем &gt;** , созданный выше, добавляется в [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) с именем мовиетипе. Вот как мы передаем **IEnumerable&lt;селектлиститем &gt;** неявно к вспомогательному модулю [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) , показанному ниже.

Откройте файл *виевс\хоме\селекткатегори.кштмл* и изучите разметку.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

В третьей строке мы устанавливаем макет views/Shared/\_Simple\_Layout. cshtml, который является упрощенной версией стандартного файла макета. Это делается для того, чтобы сделать видимым и отображаемым HTML-код простым.

В этом примере не изменяется состояние приложения, поэтому мы будем отправлять данные с помощью **HTTP Get**, а не **HTTP POST**. [Дополнительные сведения о выборе HTTP GET или POST см. в разделе "краткий контрольный список](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)W3C". Поскольку мы не изменим приложение и публикуя форму, мы используем перегрузку [HTML. бегинформ](https://msdn.microsoft.com/library/dd460344.aspx) , которая позволяет указать метод действия, контроллер и метод формы (**HTTP POST** или **HTTP Get**). Обычно представления содержат перегрузку [HTML. бегинформ](https://msdn.microsoft.com/library/dd505244.aspx) , которая не принимает параметров. Значение No версии параметра по умолчанию используется для публикации данных формы в версии того же метода и контроллера действия.

В следующей строке

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

передает строковый аргумент в вспомогательную функцию **DropDownList** . Эта строка «Мовиетипе» в нашем примере выполняет два действия:

- Он предоставляет ключ для вспомогательного метода **DropDownList** , чтобы найти элемент **IEnumerable&lt;Селектлиститем &gt;** в **ViewBag**.
- Он привязан к данным элемента формы Мовиетипе. Если метод Submit имеет значение **HTTP Get**, `MovieType` будет строкой запроса. Если метод отправки — **HTTP POST**, `MovieType` будет добавлен в текст сообщения. На следующем рисунке показана строка запроса со значением 1.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

В следующем коде показан метод `CategoryChosen`, в который была отправлена форма.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

Вернитесь на тестовую страницу и выберите ссылку **HTML SelectList** . HTML-страница отображает элемент SELECT, аналогичный простой странице теста MVC ASP.NET. Щелкните правой кнопкой мыши окно браузера и выберите пункт **Просмотреть источник**. Разметка HTML для списка выбора по сути идентична. Протестируйте HTML-страницу, она работает так же, как метод действия ASP.NET MVC и ранее протестированные.

### <a name="improving-the-movie-select-list-with-enums"></a>Улучшение списка выбора фильмов с перечислениями

Если категории в приложении исправлены и не изменятся, можно воспользоваться преимуществами перечислений, чтобы сделать код более надежным и простым в расширении. При добавлении новой категории создается правильное значение категории. Позволяет избежать ошибок копирования и вставки при добавлении новой категории, но при этом не забудьте обновить значение категории.

Откройте файл *Controllers\HomeController.CS* и изучите следующий код:

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[Перечисление](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx) `eMovieCategories` захватывает четыре типа фильмов. Метод `SetViewBagMovieType` создает **&gt;IEnumerable&lt;селектлиститем** из **перечисления**`eMovieCategories`и задает свойство `Selected` из параметра `selectedMovie`. Метод действия `SelectCategoryEnum` использует то же представление, что и метод действия `SelectCategory`.

Перейдите на страницу тест и щелкните ссылку `Select Movie Category (Enum)`. На этот раз вместо отображаемого значения (числа) отображается строка, представляющая перечисление.

### <a name="posting-enum-values"></a>Отправка значений перечисления

HTML-формы обычно используются для отправки данных на сервер. В следующем коде показаны `HTTP GET` и `HTTP POST` версии метода `SelectCategoryEnumPost`.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

Передав перечисление `eMovieCategories` в метод `POST`, можно извлечь значение перечисления и строку перечисления. Запустите пример и перейдите на страницу тест. Щелкните ссылку `Select Movie Category(Enum Post)`. Выберите тип фильма, а затем нажмите кнопку Отправить. На экране отображаются как значение, так и имя типа фильма.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>Создание элемента выбора с несколькими разделами

Вспомогательный метод HTML [ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) визуализирует элемент `<select>` HTML с помощью атрибута `multiple`, который позволяет пользователям выбрать несколько элементов. Перейдите к тестовой ссылке, а затем щелкните ссылку **множественный выбор страны** . Готовый к просмотру пользовательский интерфейс позволяет выбрать несколько стран. На рисунке ниже выбраны Канада и Китай.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>Проверка кода Мултиселекткаунтри

Изучите следующий код из файла *Controllers\HomeController.CS* .

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

Метод `GetCountries` создает список стран, а затем передает его в конструктор `MultiSelectList`. Перегрузка конструктора `MultiSelectList`, используемая в приведенном выше методе `GetCountries`, принимает четыре параметра:

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *Items*: элемент [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) , содержащий элементы списка. В приведенном выше примере это список стран.
2. *датавалуефиелд*: имя свойства в списке **IEnumerable** , которое содержит значение. В приведенном выше примере это свойство `ID`.
3. *TextField*: имя свойства в списке **IEnumerable** , которое содержит отображаемые сведения. В приведенном выше примере это свойство `name`.
4. *селектедвалуес*: список выбранных значений.

В приведенном выше примере метод `MultiSelectCountry` передает значение `null` для выбранных стран, поэтому при отображении пользовательского интерфейса не выбираются страны. В следующем коде показана разметка Razor, используемая для визуализации представления `MultiSelectCountry`.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

Используемый выше метод [ListBox](https://msdn.microsoft.com/library/dd470200.aspx) вспомогательного метода HTML принимает два параметра: имя свойства для привязки модели и [MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx) , содержащий параметры и значения SELECT. Приведенный выше код `ViewBag.YouSelected` используется для вывода значений стран, выбранных при отправке формы. Изучите перегрузку HTTP POST метода `MultiSelectCountry`.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

Динамическое свойство `ViewBag.YouSelected` содержит выбранные страны, полученные для записи `Countries` в коллекции форм. В этой версии методу «страны» передается список выбранных стран, поэтому при отображении `MultiSelectCountry`ного представления выбранные страны выбираются в пользовательском интерфейсе.

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>Как сделать элемент SELECT понятным с помощью выбранного подключаемого модуля jQuery

[Выбранный](https://harvesthq.github.com/chosen/) подключаемый модуль jQuery можно добавить в HTML-&lt;выберите элемент&gt;, чтобы создать пользовательский интерфейс. На рисунках ниже показано, как [выберет выбранный](https://harvesthq.github.com/chosen/) подключаемый модуль jQuery с `MultiSelectCountry` представлением.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

На двух приведенных ниже изображениях выбрано **Канада** .

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

На приведенном выше рисунке выбран вариант "Канада" и он содержит значок **x** , который можно щелкнуть, чтобы удалить выделенный фрагмент. На рисунке ниже показаны выбранные для Канады, Китая и Японии.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>Подключение выбранного подключаемого модуля jQuery

Следующий раздел упрощает работу, если у вас есть опыт работы с jQuery. Если вы раньше не использовали jQuery, попробуйте выполнить одно из следующих руководств по jQuery.

- [Как jQuery работает](http://docs.jquery.com/Tutorials:How_jQuery_Works) с помощью [Джон Resig)](http://ejohn.org/)
- [Начало работы с jQuery](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery) по [жöрн заефферер](http://bassistance.de/)
- [Реальные примеры jQuery](http://codylindley.com/blogstuff/js/jquery/#) с помощью [Коди линдлэй](http://codylindley.com/)

Выбранный подключаемый модуль включен в учебные и завершенные образцы проектов, сопровождающие этот учебник. В этом учебнике для подключения к пользовательскому интерфейсу необходимо использовать jQuery. Для использования подключаемого модуля jQuery, выбранного в проекте ASP.NET MVC, необходимо выполнить следующие действия.

1. Скачайте выбранный подключаемый модуль из [GitHub](https://github.com/harvesthq/chosen/). Этот шаг выполнен за вас.
2. Добавьте выбранную папку в проект MVC ASP.NET. Добавьте ресурсы из выбранного подключаемого модуля, скачанного на предыдущем шаге, в выбранную папку. Этот шаг выполнен за вас.
3. Подключите выбранный подключаемый модуль к вспомогательному модулю HTML **DropDownList** или **ListBox** .

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>Подключение выбранного подключаемого модуля к представлению Мултиселекткаунтри.

Откройте файл *виевс\хоме\мултиселекткаунтри.кштмл* и добавьте в `Html.ListBox`параметр `htmlAttributes`. Добавляемый параметр содержит имя класса для списка выбора (`@class = "chzn-select"`). Завершенный код показан ниже:

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

В приведенном выше коде мы добавляем атрибут HTML и значение атрибута `class = "chzn-select"`. Класс \@ного символа выше не имеет отношения к подсистеме представлений Razor. `class` является [ C# ключевым словом](https://msdn.microsoft.com/library/x53a06bb.aspx). C#Ключевые слова не могут использоваться в качестве идентификаторов, если они не содержат \@ в качестве префикса. В приведенном выше примере `@class` является допустимым идентификатором, но **класс** — нет, поскольку **класс** является ключевым словом.

Добавьте ссылки на *Выбранные/выбранные. jQuery. js* и *Выбранные/выбранные CSS-* файлы. *Выбранный/выбранный. jQuery. js* и реализует функцию, которая является выбранным подключаемым модулем. *Выбранный/выбранный CSS-* файл предоставляет стиль. Добавьте эти ссылки в нижнюю часть файла *виевс\хоме\мултиселекткаунтри.кштмл* . В следующем коде показано, как создать ссылку на выбранный подключаемый модуль.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

Активируйте выбранный подключаемый модуль, используя имя класса, которое используется в коде **HTML. ListBox** . В приведенном выше примере имя класса — `chzn-select`. Добавьте следующую строку в конец файла представления *виевс\хоме\мултиселекткаунтри.кштмл* . Эта строка активирует выбранный подключаемый модуль.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

Следующая строка представляет собой синтаксис для вызова функции готовности jQuery, которая выбирает элемент DOM с именем класса `chzn-select`.

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

Упакованный набор, возвращенный приведенным выше вызовом, применяет выбранный метод (`.chosen();`), который подключает выбранный подключаемый модуль.

В следующем коде показан завершенный файл представления *виевс\хоме\мултиселекткаунтри.кштмл* .

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

Запустите приложение и перейдите к представлению `MultiSelectCountry`. Попробуйте добавить и удалить страны. Пример загрузки также содержит метод `MultiCountryVM` и представление, в котором реализована функция Мултиселекткаунтри с использованием модели представления вместо **ViewBag**.

В следующем разделе вы узнаете, как механизм формирования шаблонов MVC ASP.NET работает с вспомогательным модулем **DropDownList** .

> [!div class="step-by-step"]
> [Дальше](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
