---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: Изучение шаблонов ASP.NET MVC в модуле поддержки DropDownList | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498360"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>Общие сведения о формировании шаблона вспомогательного приложения DropDownList в ASP.NET MVC

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

В **Обозреватель решений**щелкните правой кнопкой мыши папку *Controllers* и выберите пункт **Добавить контроллер**. Присвойте контроллеру имя **стореманажерконтроллер**. Задайте параметры для диалогового окна **Добавление контроллера** , как показано на рисунке ниже.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

Измените представление *стореманажер\индекс.кштмл* и удалите `AlbumArtUrl`. Удаление `AlbumArtUrl` сделает презентацию более удобочитаемой. Ниже приведен готовый код.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

Откройте файл *контроллерс\стореманажерконтроллер.КС* и найдите метод `Index`. Добавьте предложение `OrderBy`, чтобы альбомы были отсортированы по цене. Полный код приведен ниже.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

Сортировка по цене облегчит тестирование изменений в базе данных. При тестировании методов Edit и Create можно использовать низкую цену, поэтому сохраненные данные будут отображаться первыми.

Откройте файл *стореманажер\едит.кштмл* . Добавьте следующую строку сразу после тега условных обозначений.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

В следующем коде показан контекст этого изменения:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

`AlbumId` требуется для внесения изменений в запись альбома.

Для запуска приложения нажмите сочетание клавиш CTRL+F5. Выберите ссылку **"Администратор"** , а затем щелкните **создать новую** ссылку, чтобы создать новый альбом. Убедитесь, что сведения о диске сохранены. Измените альбом и убедитесь, что внесенные изменения сохраняются.

### <a name="the-album-schema"></a>Схема альбома

Контроллер `StoreManager`, созданный механизмом формирования шаблонов MVC, позволяет получить доступ к альбомам в базе данных музыкального хранилища (создание, чтение, обновление, удаление). Схема для сведений о альбоме показана ниже:

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

В `Albums` таблице не хранится жанр и описание альбома, а также внешний ключ для таблицы `Genres`. Таблица `Genres` содержит название и описание жанра. Аналогичным образом `Albums`ная таблица не содержит имя исполнителей альбома, а внешний ключ к `Artists` таблице. `Artists` таблица содержит имя исполнителя. При просмотре данных в `Albums` таблице можно увидеть, что каждая строка содержит внешний ключ для `Genres` таблицы и внешний ключ к таблице `Artists`. На рисунке ниже показаны некоторые табличные данные из таблицы `Albums`.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML-тег SELECT

Элемент `<select>` HTML (созданный вспомогательным элементом [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) ) используется для вывода полного списка значений (таких как список жанров). Для форм редактирования, когда текущее значение известно, список выбора может отображать текущее значение. Мы видели это ранее, когда мы задали для выбранного значения значение **комедия**. Список выбора идеально подходит для отображения данных категории или внешнего ключа. Элемент `<select>` для внешнего ключа жанра отображает список возможных названий жанров, но при сохранении формы свойство жанра обновляется значением внешнего ключа жанра, а не отображаемым именем жанра. На рисунке ниже выбран жанр — **Disco** , а исполнитель — **Донна летом**.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>Анализ кода с формированием ASP.NET MVC

Откройте файл *контроллерс\стореманажерконтроллер.КС* и найдите метод `HTTP GET Create`.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

Метод `Create` добавляет два объекта [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) в `ViewBag`, один для хранения сведений о жанре, а второй — сведения об исполнителе. Перегрузка конструктора [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) , используемая выше, принимает три аргумента:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *Items*: элемент [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) , содержащий элементы списка. В приведенном выше примере список стилей, возвращаемых `db.Genres`.
2. *датавалуефиелд*: имя свойства в списке **IEnumerable** , которое содержит значение ключа. В приведенном выше примере `GenreId` и `ArtistId`.
3. *TextField*: имя свойства в списке **IEnumerable** , которое содержит отображаемые сведения. В таблице исполнители и жанры используется поле `name`.

Откройте файл *виевс\стореманажер\креате.кштмл* и изучите разметку вспомогательной функции `Html.DropDownList` для поля жанр.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

В первой строке показано, что представление Create принимает `Album`ную модель. В приведенном выше методе `Create` ни одна модель не была передана, поэтому представление получает `Album`ную модель **со значением NULL** . На этом этапе мы создаем новый альбом, поэтому у нас нет данных `Album`.

Перегрузка [HTML. DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) , показанная выше, принимает имя поля для привязки к модели. Он также использует это имя для поиска объекта **ViewBag** , содержащего объект [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) . При использовании этой перегрузки необходимо указать имя объекта **ViewBag SelectList** `GenreId`. Второй параметр (`String.Empty`) — это текст, отображаемый, если элемент не выбран. Это именно то, что нам нужно при создании нового альбома. Если вы удалили второй параметр и использовали следующий код:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

Список выбора будет по умолчанию первым элементом или рок в нашем примере.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

Проверка метода `HTTP POST Create`.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

Эта перегрузка метода `Create` принимает объект `album`, созданный системой привязки модели MVC ASP.NET из значений формы. При отправке нового альбома, если состояние модели является допустимым и ошибки базы данных отсутствуют, новый альбом добавляется в базу данных. На следующем рисунке показано создание нового альбома.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

С помощью [средства Fiddler](http://www.fiddler2.com/fiddler2/) можно просмотреть значения в опубликованной форме, которые применяют привязка модели MVC для создания объекта альбома.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).

### <a name="refactoring-the-viewbag-selectlist-creation"></a>Рефакторинг создания SelectList ViewBag

Как методы `Edit`, так и метод `HTTP POST Create` имеют идентичный код для настройки **SelectList** в **ViewBag**. В конце [сухой](http://en.wikipedia.org/wiki/Don't_repeat_yourself)мы будем выполнять рефакторинг этого кода. Мы будем использовать этот код с рефакторингом позже.

Создайте новый метод для добавления жанра и исполнителя **SelectList** в **ViewBag**.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

Замените две строки, задавая `ViewBag` в каждом из методов `Create` и `Edit` с помощью вызова метода `SetGenreArtistViewBag`. Ниже приведен готовый код.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

Создайте новый альбом и измените альбом, чтобы проверить работу изменений.

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>Явная передача SelectList в DropDownList

Представления Create и Edit, созданные с помощью формирования шаблонов MVC ASP.NET, используют следующую перегрузку **DropDownList** :

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

Ниже показана разметка `DropDownList` для представления создания.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

Поскольку свойство `ViewBag` для `SelectList` имеет имя `GenreId`, вспомогательный элемент **DropDownList** будет использовать `GenreId`**SelectList** в **ViewBag**. В следующей перегрузке **DropDownList** `SelectList` явно передается.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

Откройте файл *виевс\стореманажер\едит.кштмл* и измените вызов **DropDownList** , чтобы он явно передавался в **SelectList**, используя перегрузку выше. Сделайте это для категории жанр. Завершенный код показан ниже:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

Запустите приложение и щелкните ссылку **администратора** , а затем перейдите к альбому Джаз и выберите ссылку **Edit (изменить** ).

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

Вместо отображения джаз в качестве текущего выбранного жанра отображается рок. Если строковый аргумент (свойство для привязки) и объект **SelectList** имеют одинаковое имя, то выбранное значение не используется. Если выбранное значение не указано, браузеры по умолчанию используют первый элемент в **SelectList**(что является **рок** в примере выше). Это известное ограничение вспомогательного приложения **DropDownList** .

Откройте файл *контроллерс\стореманажерконтроллер.КС* и измените имена объектов **SelectList** на `Genres` и `Artists`. Завершенный код показан ниже:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

Имена жанров и исполнителей лучше названы для категорий, так как они содержат не только идентификатор каждой категории. Рефакторинг, который выполнялся ранее, был оплачен. Вместо изменения **ViewBag** в четырех методах наши изменения были изолированы от метода `SetGenreArtistViewBag`.

Измените вызов **DropDownList** в представлениях Create и Edit, чтобы использовать новые имена **SelectList** . Новая разметка для представления редактирования показана ниже:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

Для представления создания необходимо указать пустую строку, чтобы не отображался первый элемент в SelectList.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

Создайте новый альбом и измените альбом, чтобы проверить работу изменений. Протестируйте код редактирования, выбрав альбом с жанром, отличным от рок.

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>Использование модели представления с вспомогательным модулем DropDownList

Создайте новый класс в папке ViewModels с именем `AlbumSelectListViewModel`. Замените код в классе `AlbumSelectListViewModel` следующим кодом:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

Конструктор `AlbumSelectListViewModel` принимает альбом, список исполнителей и жанров и создает объект, содержащий альбом и `SelectList` для жанров и исполнителей.

Постройте проект, чтобы `AlbumSelectListViewModel` был доступен при создании представления на следующем шаге.

Добавьте в `StoreManagerController`метод `EditVM`. Ниже приведен готовый код.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

Щелкните правой кнопкой мыши `AlbumSelectListViewModel`, выберите **Разрешить**, а затем — **мвкмусиксторе. ViewModels;** .

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

Кроме того, можно добавить следующий оператор using:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

Щелкните правой кнопкой мыши `EditVM` и выберите **Добавить представление**. Используйте параметры, показанные ниже.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

Выберите **Добавить**, а затем замените содержимое файла *виевс\стореманажер\едитвм.кштмл* следующим:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

Разметка `EditVM` очень похожа на исходную разметку `Edit` со следующими исключениями.

- Свойства модели в представлении `Edit` имеют форму `model.property`(например, `model.Title`). Свойства модели в представлении `EditVm` имеют форму `model.Album.property`(например, `model.Album.Title`). Это связано с тем, что представление `EditVM` передается в качестве контейнера для `Album`, а не `Album`, как в представлении `Edit`.
- Второй параметр **DropDownList** взят из модели представления, а не **ViewBag**.
- Вспомогательный модуль **бегинформ** в представлении `EditVM` явно отправляет обратно в метод действия `Edit`. Отправляясь к `Edit` действию, нам не нужно писать `HTTP POST EditVM` действие и использовать `HTTP POST` `Edit`.

Запустите приложение и измените альбом. Измените URL-адрес, чтобы использовать `EditVM`. Измените поле и нажмите кнопку **Save (сохранить** ), чтобы убедиться в том, что код работает.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>Какой подход следует использовать?

Все три показанных подхода приемлемы. Многие разработчики предпочитают явно передавать `SelectList` `DropDownList` с помощью `ViewBag`. Этот подход обладает преимуществом, обеспечивающим гибкость использования более подходящего имени для коллекции. Одним из предостережений является то, что имя объекта `ViewBag SelectList` не может совпадать с именем свойства модели.

Некоторые разработчики предпочитают подход ViewModel. Другие считают, что более подробная разметка и созданный HTML-код для подхода ViewModel имеют недостаток.

В этом разделе мы узнали три подхода к использованию **DropDownList** с данными категорий. В следующем разделе мы покажем, как добавить новую категорию.

> [!div class="step-by-step"]
> [Назад](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [Вперед](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
