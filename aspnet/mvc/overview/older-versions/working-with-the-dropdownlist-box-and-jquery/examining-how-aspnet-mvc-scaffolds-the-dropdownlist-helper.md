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
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457613"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="9339e-102">Общие сведения о формировании шаблона вспомогательного приложения DropDownList в ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="9339e-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>

<span data-ttu-id="9339e-103">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9339e-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9339e-104">В **Обозреватель решений**щелкните правой кнопкой мыши папку *Controllers* и выберите пункт **Добавить контроллер**.</span><span class="sxs-lookup"><span data-stu-id="9339e-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="9339e-105">Присвойте контроллеру имя **стореманажерконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="9339e-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="9339e-106">Задайте параметры для диалогового окна **Добавление контроллера** , как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="9339e-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="9339e-107">Измените представление *стореманажер\индекс.кштмл* и удалите `AlbumArtUrl`.</span><span class="sxs-lookup"><span data-stu-id="9339e-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="9339e-108">Удаление `AlbumArtUrl` сделает презентацию более удобочитаемой.</span><span class="sxs-lookup"><span data-stu-id="9339e-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="9339e-109">Ниже приведен готовый код.</span><span class="sxs-lookup"><span data-stu-id="9339e-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="9339e-110">Откройте файл *контроллерс\стореманажерконтроллер.КС* и найдите метод `Index`.</span><span class="sxs-lookup"><span data-stu-id="9339e-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="9339e-111">Добавьте предложение `OrderBy`, чтобы альбомы были отсортированы по цене.</span><span class="sxs-lookup"><span data-stu-id="9339e-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="9339e-112">Полный код приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="9339e-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="9339e-113">Сортировка по цене облегчит тестирование изменений в базе данных.</span><span class="sxs-lookup"><span data-stu-id="9339e-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="9339e-114">При тестировании методов Edit и Create можно использовать низкую цену, поэтому сохраненные данные будут отображаться первыми.</span><span class="sxs-lookup"><span data-stu-id="9339e-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="9339e-115">Откройте файл *стореманажер\едит.кштмл* .</span><span class="sxs-lookup"><span data-stu-id="9339e-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="9339e-116">Добавьте следующую строку сразу после тега условных обозначений.</span><span class="sxs-lookup"><span data-stu-id="9339e-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="9339e-117">В следующем коде показан контекст этого изменения:</span><span class="sxs-lookup"><span data-stu-id="9339e-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="9339e-118">`AlbumId` требуется для внесения изменений в запись альбома.</span><span class="sxs-lookup"><span data-stu-id="9339e-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="9339e-119">Нажмите CTRL+F5, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9339e-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="9339e-120">Выберите ссылку **"Администратор"** , а затем щелкните **создать новую** ссылку, чтобы создать новый альбом.</span><span class="sxs-lookup"><span data-stu-id="9339e-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="9339e-121">Убедитесь, что сведения о диске сохранены.</span><span class="sxs-lookup"><span data-stu-id="9339e-121">Verify the album information was saved.</span></span> <span data-ttu-id="9339e-122">Измените альбом и убедитесь, что внесенные изменения сохраняются.</span><span class="sxs-lookup"><span data-stu-id="9339e-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="9339e-123">Схема альбома</span><span class="sxs-lookup"><span data-stu-id="9339e-123">The Album Schema</span></span>

<span data-ttu-id="9339e-124">Контроллер `StoreManager`, созданный механизмом формирования шаблонов MVC, позволяет получить доступ к альбомам в базе данных музыкального хранилища (создание, чтение, обновление, удаление).</span><span class="sxs-lookup"><span data-stu-id="9339e-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="9339e-125">Схема для сведений о альбоме показана ниже:</span><span class="sxs-lookup"><span data-stu-id="9339e-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="9339e-126">В `Albums` таблице не хранится жанр и описание альбома, а также внешний ключ для таблицы `Genres`.</span><span class="sxs-lookup"><span data-stu-id="9339e-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="9339e-127">Таблица `Genres` содержит название и описание жанра.</span><span class="sxs-lookup"><span data-stu-id="9339e-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="9339e-128">Аналогичным образом `Albums`ная таблица не содержит имя исполнителей альбома, а внешний ключ к `Artists` таблице.</span><span class="sxs-lookup"><span data-stu-id="9339e-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="9339e-129">`Artists` таблица содержит имя исполнителя.</span><span class="sxs-lookup"><span data-stu-id="9339e-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="9339e-130">При просмотре данных в `Albums` таблице можно увидеть, что каждая строка содержит внешний ключ для `Genres` таблицы и внешний ключ к таблице `Artists`.</span><span class="sxs-lookup"><span data-stu-id="9339e-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="9339e-131">На рисунке ниже показаны некоторые табличные данные из таблицы `Albums`.</span><span class="sxs-lookup"><span data-stu-id="9339e-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="9339e-132">HTML-тег SELECT</span><span class="sxs-lookup"><span data-stu-id="9339e-132">The HTML Select Tag</span></span>

<span data-ttu-id="9339e-133">Элемент `<select>` HTML (созданный вспомогательным элементом [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) ) используется для вывода полного списка значений (таких как список жанров).</span><span class="sxs-lookup"><span data-stu-id="9339e-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="9339e-134">Для форм редактирования, когда текущее значение известно, список выбора может отображать текущее значение.</span><span class="sxs-lookup"><span data-stu-id="9339e-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="9339e-135">Мы видели это ранее, когда мы задали для выбранного значения значение **комедия**.</span><span class="sxs-lookup"><span data-stu-id="9339e-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="9339e-136">Список выбора идеально подходит для отображения данных категории или внешнего ключа.</span><span class="sxs-lookup"><span data-stu-id="9339e-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="9339e-137">Элемент `<select>` для внешнего ключа жанра отображает список возможных названий жанров, но при сохранении формы свойство жанра обновляется значением внешнего ключа жанра, а не отображаемым именем жанра.</span><span class="sxs-lookup"><span data-stu-id="9339e-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="9339e-138">На рисунке ниже выбран жанр — **Disco** , а исполнитель — **Донна летом**.</span><span class="sxs-lookup"><span data-stu-id="9339e-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="9339e-139">Анализ кода с формированием ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="9339e-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="9339e-140">Откройте файл *контроллерс\стореманажерконтроллер.КС* и найдите метод `HTTP GET Create`.</span><span class="sxs-lookup"><span data-stu-id="9339e-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="9339e-141">Метод `Create` добавляет два объекта [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) в `ViewBag`, один для хранения сведений о жанре, а второй — сведения об исполнителе.</span><span class="sxs-lookup"><span data-stu-id="9339e-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="9339e-142">Перегрузка конструктора [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) , используемая выше, принимает три аргумента:</span><span class="sxs-lookup"><span data-stu-id="9339e-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="9339e-143">*Items*: элемент [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) , содержащий элементы списка.</span><span class="sxs-lookup"><span data-stu-id="9339e-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="9339e-144">В приведенном выше примере список стилей, возвращаемых `db.Genres`.</span><span class="sxs-lookup"><span data-stu-id="9339e-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="9339e-145">*датавалуефиелд*: имя свойства в списке **IEnumerable** , которое содержит значение ключа.</span><span class="sxs-lookup"><span data-stu-id="9339e-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="9339e-146">В приведенном выше примере `GenreId` и `ArtistId`.</span><span class="sxs-lookup"><span data-stu-id="9339e-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="9339e-147">*TextField*: имя свойства в списке **IEnumerable** , которое содержит отображаемые сведения.</span><span class="sxs-lookup"><span data-stu-id="9339e-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="9339e-148">В таблице исполнители и жанры используется поле `name`.</span><span class="sxs-lookup"><span data-stu-id="9339e-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="9339e-149">Откройте файл *виевс\стореманажер\креате.кштмл* и изучите разметку вспомогательной функции `Html.DropDownList` для поля жанр.</span><span class="sxs-lookup"><span data-stu-id="9339e-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="9339e-150">В первой строке показано, что представление Create принимает `Album`ную модель.</span><span class="sxs-lookup"><span data-stu-id="9339e-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="9339e-151">В приведенном выше методе `Create` ни одна модель не была передана, поэтому представление получает `Album`ную модель **со значением NULL** .</span><span class="sxs-lookup"><span data-stu-id="9339e-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="9339e-152">На этом этапе мы создаем новый альбом, поэтому у нас нет данных `Album`.</span><span class="sxs-lookup"><span data-stu-id="9339e-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="9339e-153">Перегрузка [HTML. DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) , показанная выше, принимает имя поля для привязки к модели.</span><span class="sxs-lookup"><span data-stu-id="9339e-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="9339e-154">Он также использует это имя для поиска объекта **ViewBag** , содержащего объект [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9339e-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="9339e-155">При использовании этой перегрузки необходимо указать имя объекта **ViewBag SelectList** `GenreId`.</span><span class="sxs-lookup"><span data-stu-id="9339e-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="9339e-156">Второй параметр (`String.Empty`) — это текст, отображаемый, если элемент не выбран.</span><span class="sxs-lookup"><span data-stu-id="9339e-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="9339e-157">Это именно то, что нам нужно при создании нового альбома.</span><span class="sxs-lookup"><span data-stu-id="9339e-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="9339e-158">Если вы удалили второй параметр и использовали следующий код:</span><span class="sxs-lookup"><span data-stu-id="9339e-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="9339e-159">Список выбора будет по умолчанию первым элементом или рок в нашем примере.</span><span class="sxs-lookup"><span data-stu-id="9339e-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="9339e-160">Проверка метода `HTTP POST Create`.</span><span class="sxs-lookup"><span data-stu-id="9339e-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="9339e-161">Эта перегрузка метода `Create` принимает объект `album`, созданный системой привязки модели MVC ASP.NET из значений формы.</span><span class="sxs-lookup"><span data-stu-id="9339e-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="9339e-162">При отправке нового альбома, если состояние модели является допустимым и ошибки базы данных отсутствуют, новый альбом добавляется в базу данных.</span><span class="sxs-lookup"><span data-stu-id="9339e-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="9339e-163">На следующем рисунке показано создание нового альбома.</span><span class="sxs-lookup"><span data-stu-id="9339e-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="9339e-164">С помощью [средства Fiddler](http://www.fiddler2.com/fiddler2/) можно просмотреть значения в опубликованной форме, которые применяют привязка модели MVC для создания объекта альбома.</span><span class="sxs-lookup"><span data-stu-id="9339e-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="9339e-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span><span class="sxs-lookup"><span data-stu-id="9339e-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="9339e-166">Рефакторинг создания SelectList ViewBag</span><span class="sxs-lookup"><span data-stu-id="9339e-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="9339e-167">Как методы `Edit`, так и метод `HTTP POST Create` имеют идентичный код для настройки **SelectList** в **ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="9339e-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="9339e-168">В конце [сухой](http://en.wikipedia.org/wiki/Don't_repeat_yourself)мы будем выполнять рефакторинг этого кода.</span><span class="sxs-lookup"><span data-stu-id="9339e-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="9339e-169">Мы будем использовать этот код с рефакторингом позже.</span><span class="sxs-lookup"><span data-stu-id="9339e-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="9339e-170">Создайте новый метод для добавления жанра и исполнителя **SelectList** в **ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="9339e-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="9339e-171">Замените две строки, задавая `ViewBag` в каждом из методов `Create` и `Edit` с помощью вызова метода `SetGenreArtistViewBag`.</span><span class="sxs-lookup"><span data-stu-id="9339e-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="9339e-172">Ниже приведен готовый код.</span><span class="sxs-lookup"><span data-stu-id="9339e-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="9339e-173">Создайте новый альбом и измените альбом, чтобы проверить работу изменений.</span><span class="sxs-lookup"><span data-stu-id="9339e-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="9339e-174">Явная передача SelectList в DropDownList</span><span class="sxs-lookup"><span data-stu-id="9339e-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="9339e-175">Представления Create и Edit, созданные с помощью формирования шаблонов MVC ASP.NET, используют следующую перегрузку **DropDownList** :</span><span class="sxs-lookup"><span data-stu-id="9339e-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="9339e-176">Ниже показана разметка `DropDownList` для представления создания.</span><span class="sxs-lookup"><span data-stu-id="9339e-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="9339e-177">Поскольку свойство `ViewBag` для `SelectList` имеет имя `GenreId`, вспомогательный элемент **DropDownList** будет использовать `GenreId`**SelectList** в **ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="9339e-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="9339e-178">В следующей перегрузке **DropDownList** `SelectList` явно передается.</span><span class="sxs-lookup"><span data-stu-id="9339e-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="9339e-179">Откройте файл *виевс\стореманажер\едит.кштмл* и измените вызов **DropDownList** , чтобы он явно передавался в **SelectList**, используя перегрузку выше.</span><span class="sxs-lookup"><span data-stu-id="9339e-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="9339e-180">Сделайте это для категории жанр.</span><span class="sxs-lookup"><span data-stu-id="9339e-180">Do this for the Genre category.</span></span> <span data-ttu-id="9339e-181">Завершенный код показан ниже:</span><span class="sxs-lookup"><span data-stu-id="9339e-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="9339e-182">Запустите приложение и щелкните ссылку **администратора** , а затем перейдите к альбому Джаз и выберите ссылку **Edit (изменить** ).</span><span class="sxs-lookup"><span data-stu-id="9339e-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="9339e-183">Вместо отображения джаз в качестве текущего выбранного жанра отображается рок.</span><span class="sxs-lookup"><span data-stu-id="9339e-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="9339e-184">Если строковый аргумент (свойство для привязки) и объект **SelectList** имеют одинаковое имя, то выбранное значение не используется.</span><span class="sxs-lookup"><span data-stu-id="9339e-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="9339e-185">Если выбранное значение не указано, браузеры по умолчанию используют первый элемент в **SelectList**(что является **рок** в примере выше).</span><span class="sxs-lookup"><span data-stu-id="9339e-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="9339e-186">Это известное ограничение вспомогательного приложения **DropDownList** .</span><span class="sxs-lookup"><span data-stu-id="9339e-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="9339e-187">Откройте файл *контроллерс\стореманажерконтроллер.КС* и измените имена объектов **SelectList** на `Genres` и `Artists`.</span><span class="sxs-lookup"><span data-stu-id="9339e-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="9339e-188">Завершенный код показан ниже:</span><span class="sxs-lookup"><span data-stu-id="9339e-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="9339e-189">Имена жанров и исполнителей лучше названы для категорий, так как они содержат не только идентификатор каждой категории.</span><span class="sxs-lookup"><span data-stu-id="9339e-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="9339e-190">Рефакторинг, который выполнялся ранее, был оплачен.</span><span class="sxs-lookup"><span data-stu-id="9339e-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="9339e-191">Вместо изменения **ViewBag** в четырех методах наши изменения были изолированы от метода `SetGenreArtistViewBag`.</span><span class="sxs-lookup"><span data-stu-id="9339e-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="9339e-192">Измените вызов **DropDownList** в представлениях Create и Edit, чтобы использовать новые имена **SelectList** .</span><span class="sxs-lookup"><span data-stu-id="9339e-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="9339e-193">Новая разметка для представления редактирования показана ниже:</span><span class="sxs-lookup"><span data-stu-id="9339e-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="9339e-194">Для представления создания необходимо указать пустую строку, чтобы не отображался первый элемент в SelectList.</span><span class="sxs-lookup"><span data-stu-id="9339e-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="9339e-195">Создайте новый альбом и измените альбом, чтобы проверить работу изменений.</span><span class="sxs-lookup"><span data-stu-id="9339e-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="9339e-196">Протестируйте код редактирования, выбрав альбом с жанром, отличным от рок.</span><span class="sxs-lookup"><span data-stu-id="9339e-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="9339e-197">Использование модели представления с вспомогательным модулем DropDownList</span><span class="sxs-lookup"><span data-stu-id="9339e-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="9339e-198">Создайте новый класс в папке ViewModels с именем `AlbumSelectListViewModel`.</span><span class="sxs-lookup"><span data-stu-id="9339e-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="9339e-199">Замените код в классе `AlbumSelectListViewModel` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9339e-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="9339e-200">Конструктор `AlbumSelectListViewModel` принимает альбом, список исполнителей и жанров и создает объект, содержащий альбом и `SelectList` для жанров и исполнителей.</span><span class="sxs-lookup"><span data-stu-id="9339e-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="9339e-201">Постройте проект, чтобы `AlbumSelectListViewModel` был доступен при создании представления на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="9339e-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="9339e-202">Добавьте в `StoreManagerController`метод `EditVM`.</span><span class="sxs-lookup"><span data-stu-id="9339e-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="9339e-203">Ниже приведен готовый код.</span><span class="sxs-lookup"><span data-stu-id="9339e-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="9339e-204">Щелкните правой кнопкой мыши `AlbumSelectListViewModel`, выберите **Разрешить**, а затем — **мвкмусиксторе. ViewModels;** .</span><span class="sxs-lookup"><span data-stu-id="9339e-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="9339e-205">Кроме того, можно добавить следующий оператор using:</span><span class="sxs-lookup"><span data-stu-id="9339e-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="9339e-206">Щелкните правой кнопкой мыши `EditVM` и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="9339e-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="9339e-207">Используйте параметры, показанные ниже.</span><span class="sxs-lookup"><span data-stu-id="9339e-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="9339e-208">Выберите **Добавить**, а затем замените содержимое файла *виевс\стореманажер\едитвм.кштмл* следующим:</span><span class="sxs-lookup"><span data-stu-id="9339e-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="9339e-209">Разметка `EditVM` очень похожа на исходную разметку `Edit` со следующими исключениями.</span><span class="sxs-lookup"><span data-stu-id="9339e-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="9339e-210">Свойства модели в представлении `Edit` имеют форму `model.property`(например, `model.Title`).</span><span class="sxs-lookup"><span data-stu-id="9339e-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="9339e-211">Свойства модели в представлении `EditVm` имеют форму `model.Album.property`(например, `model.Album.Title`).</span><span class="sxs-lookup"><span data-stu-id="9339e-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="9339e-212">Это связано с тем, что представление `EditVM` передается в качестве контейнера для `Album`, а не `Album`, как в представлении `Edit`.</span><span class="sxs-lookup"><span data-stu-id="9339e-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="9339e-213">Второй параметр **DropDownList** взят из модели представления, а не **ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="9339e-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="9339e-214">Вспомогательный модуль **бегинформ** в представлении `EditVM` явно отправляет обратно в метод действия `Edit`.</span><span class="sxs-lookup"><span data-stu-id="9339e-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="9339e-215">Отправляясь к `Edit` действию, нам не нужно писать `HTTP POST EditVM` действие и использовать `HTTP POST` `Edit`.</span><span class="sxs-lookup"><span data-stu-id="9339e-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="9339e-216">Запустите приложение и измените альбом.</span><span class="sxs-lookup"><span data-stu-id="9339e-216">Run the application and edit an album.</span></span> <span data-ttu-id="9339e-217">Измените URL-адрес, чтобы использовать `EditVM`.</span><span class="sxs-lookup"><span data-stu-id="9339e-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="9339e-218">Измените поле и нажмите кнопку **Save (сохранить** ), чтобы убедиться в том, что код работает.</span><span class="sxs-lookup"><span data-stu-id="9339e-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="9339e-219">Какой подход следует использовать?</span><span class="sxs-lookup"><span data-stu-id="9339e-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="9339e-220">Все три показанных подхода приемлемы.</span><span class="sxs-lookup"><span data-stu-id="9339e-220">All three approaches shown are acceptable.</span></span> <span data-ttu-id="9339e-221">Многие разработчики предпочитают явно передавать `SelectList` `DropDownList` с помощью `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="9339e-221">Many developers prefer to explicitly pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="9339e-222">Этот подход обладает преимуществом, обеспечивающим гибкость использования более подходящего имени для коллекции.</span><span class="sxs-lookup"><span data-stu-id="9339e-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="9339e-223">Одним из предостережений является то, что имя объекта `ViewBag SelectList` не может совпадать с именем свойства модели.</span><span class="sxs-lookup"><span data-stu-id="9339e-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="9339e-224">Некоторые разработчики предпочитают подход ViewModel.</span><span class="sxs-lookup"><span data-stu-id="9339e-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="9339e-225">Другие считают, что более подробная разметка и созданный HTML-код для подхода ViewModel имеют недостаток.</span><span class="sxs-lookup"><span data-stu-id="9339e-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="9339e-226">В этом разделе мы узнали три подхода к использованию **DropDownList** с данными категорий.</span><span class="sxs-lookup"><span data-stu-id="9339e-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="9339e-227">В следующем разделе мы покажем, как добавить новую категорию.</span><span class="sxs-lookup"><span data-stu-id="9339e-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9339e-228">[Назад](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [Вперед](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="9339e-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
