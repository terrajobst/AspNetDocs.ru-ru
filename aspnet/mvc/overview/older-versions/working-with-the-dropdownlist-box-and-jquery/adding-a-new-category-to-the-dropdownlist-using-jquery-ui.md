---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: Добавление новой категории в DropDownList с помощью пользовательского интерфейса jQuery | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 3207079ee468232e5f75b081421241c232936baf
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455728"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="edfb3-102">Добавление новой категории в DropDownList с помощью пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="edfb3-102">Adding a New Category to the DropDownList using jQuery UI</span></span>

<span data-ttu-id="edfb3-103">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="edfb3-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="edfb3-104">Тег HTML `Select` идеально подходит для представления списка фиксированных данных категорий, но часто приходится добавлять новые категории.</span><span class="sxs-lookup"><span data-stu-id="edfb3-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="edfb3-105">Предположим, что нам нужно добавить жанр "Opera" к категориям в нашей базе данных?</span><span class="sxs-lookup"><span data-stu-id="edfb3-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="edfb3-106">В этом разделе мы будем использовать пользовательский интерфейс jQuery, чтобы добавить диалоговое окно, которое можно использовать для добавления новой категории.</span><span class="sxs-lookup"><span data-stu-id="edfb3-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="edfb3-107">На рисунке ниже показано, как пользовательский интерфейс будет отображаться в браузере.</span><span class="sxs-lookup"><span data-stu-id="edfb3-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="edfb3-108">Когда пользователь выбирает ссылку " **Добавить новый жанр** ", всплывающее диалоговое окно предлагает пользователю ввести новое название жанра (и, при необходимости, описание).</span><span class="sxs-lookup"><span data-stu-id="edfb3-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="edfb3-109">На рисунке ниже показано всплывающее диалоговое окно **Добавление жанра** .</span><span class="sxs-lookup"><span data-stu-id="edfb3-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="edfb3-110">Если введено новое имя жанра и нажата кнопка **сохранить** , происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="edfb3-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="edfb3-111">Вызов AJAX отправляет данные в метод Create в контроллере жанра, который сохраняет новый жанр в базе данных и возвращает новые сведения о жанре (название и идентификатор жанра) в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="edfb3-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="edfb3-112">JavaScript добавляет новые данные о жанре в список выбора.</span><span class="sxs-lookup"><span data-stu-id="edfb3-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="edfb3-113">JavaScript делает новый жанр выбранным элементом.</span><span class="sxs-lookup"><span data-stu-id="edfb3-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="edfb3-114">На приведенном ниже рисунке в базу данных был добавлен элемент **Opera** и выбран в раскрывающемся списке **Жанр** .</span><span class="sxs-lookup"><span data-stu-id="edfb3-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="edfb3-115">Откройте файл *виевс\стореманажер\креате.кштмл* и замените разметку жанра следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="edfb3-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="edfb3-116">Частичное представление `_ChooseGenre` будет содержать всю логику для подключения JavaScript и jQuery, которые используются для реализации функции добавления нового жанра.</span><span class="sxs-lookup"><span data-stu-id="edfb3-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="edfb3-117">После завершения кода это будет просто сделать с помощью пользовательского интерфейса исполнителя.</span><span class="sxs-lookup"><span data-stu-id="edfb3-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="edfb3-118">В обозреватель решений щелкните правой кнопкой мыши папку *виевс\стореманажер* и выберите **Добавить**, а затем **Просмотрите**.</span><span class="sxs-lookup"><span data-stu-id="edfb3-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="edfb3-119">В поле **View Name input (имя представления** ) введите `_ChooseGenre` а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="edfb3-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="edfb3-120">Замените разметку в файле *виевс\стореманажер\\_ChooseGenre. cshtml* следующим:</span><span class="sxs-lookup"><span data-stu-id="edfb3-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="edfb3-121">В первой строке объявляется, что в качестве модели передается `Album`, точно такую же инструкцию Model, которая находится в представлении Create.</span><span class="sxs-lookup"><span data-stu-id="edfb3-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="edfb3-122">Следующие несколько строк являются разметкой вспомогательной функции **метки** .</span><span class="sxs-lookup"><span data-stu-id="edfb3-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="edfb3-123">Следующая строка является вызовом модуля **DropDownList** , точно таким же, как в исходном представлении Create.</span><span class="sxs-lookup"><span data-stu-id="edfb3-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="edfb3-124">В следующей строке добавляется ссылка с именем `Add New Genre`и стили наподобие кнопки.</span><span class="sxs-lookup"><span data-stu-id="edfb3-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="edfb3-125">Строка, содержащая `ValidationMessageFor`, копируется непосредственно из представления создания.</span><span class="sxs-lookup"><span data-stu-id="edfb3-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="edfb3-126">Следующие строки:</span><span class="sxs-lookup"><span data-stu-id="edfb3-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="edfb3-127">создает скрытый тег div с ИДЕНТИФИКАТОРом `genreDialog`.</span><span class="sxs-lookup"><span data-stu-id="edfb3-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="edfb3-128">Для подключения к диалоговому окну **Добавление жанра** с идентификатором `genreDialog` в этом div будет использоваться jQuery.</span><span class="sxs-lookup"><span data-stu-id="edfb3-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="edfb3-129">Последние два тега скрипта содержат ссылки на файлы JavaScript, которые будут использоваться для реализации функции добавления нового жанра.</span><span class="sxs-lookup"><span data-stu-id="edfb3-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="edfb3-130">Файл */скриптс/чусеженре.ЖС* предоставляется в проекте, он будет рассмотрен позже в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="edfb3-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="edfb3-131">Запустите приложение и нажмите кнопку **Добавить новый жанр** .</span><span class="sxs-lookup"><span data-stu-id="edfb3-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="edfb3-132">В диалоговом окне **Добавление жанра** введите **Opera** в поле **имя** ввода.</span><span class="sxs-lookup"><span data-stu-id="edfb3-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="edfb3-133">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="edfb3-133">Click the **Save** button.</span></span> <span data-ttu-id="edfb3-134">Вызов AJAX создает категорию Opera, а затем заполняет раскрывающийся список с помощью Opera и устанавливает Opera в качестве выбранного жанра.</span><span class="sxs-lookup"><span data-stu-id="edfb3-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="edfb3-135">Введите имя исполнителя, название и Цена, а затем нажмите кнопку **создать** .</span><span class="sxs-lookup"><span data-stu-id="edfb3-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="edfb3-136">Если ввести цену меньше $8,99, в верхней части представления индекса появится новый альбом.</span><span class="sxs-lookup"><span data-stu-id="edfb3-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="edfb3-137">Убедитесь, что новая запись альбома сохранена в базе данных.</span><span class="sxs-lookup"><span data-stu-id="edfb3-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="edfb3-138">Попробуйте создать новый жанр только с одной буквой.</span><span class="sxs-lookup"><span data-stu-id="edfb3-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="edfb3-139">Следующий код в файле *моделс\женре.КС* задает минимальную и максимальную длину имени жанра.</span><span class="sxs-lookup"><span data-stu-id="edfb3-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="edfb3-140">Отчеты о проверке на стороне клиента необходимо ввести строку от 2 до 20 символов.</span><span class="sxs-lookup"><span data-stu-id="edfb3-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="edfb3-141">Проверка добавления нового жанра в базу данных и списка выбора.</span><span class="sxs-lookup"><span data-stu-id="edfb3-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="edfb3-142">Откройте файл *скриптс\чусеженре.ЖС* и изучите код.</span><span class="sxs-lookup"><span data-stu-id="edfb3-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="edfb3-143">Во второй строке используется идентификатор `genreDialog` для создания диалогового окна в теге DIV в файле *виевс\стореманажер\\_ChooseGenre. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="edfb3-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="edfb3-144">Большинство именованных параметров говорят сами за себя.</span><span class="sxs-lookup"><span data-stu-id="edfb3-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="edfb3-145">Параметр `autoOpen` имеет значение false, при нажатии кнопки **создать жанр** диалоговое окно открывается явно (это описано в последнем случае).</span><span class="sxs-lookup"><span data-stu-id="edfb3-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="edfb3-146">В диалоговом окне есть две кнопки: **сохранить** и **отменить**.</span><span class="sxs-lookup"><span data-stu-id="edfb3-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="edfb3-147">Кнопка **Отмена** закрывает диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="edfb3-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="edfb3-148">В следующем коде показана функция **Save** для кнопки.</span><span class="sxs-lookup"><span data-stu-id="edfb3-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="edfb3-149">`var createGenreForm` выбирается из идентификатора `createGenreForm`.</span><span class="sxs-lookup"><span data-stu-id="edfb3-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="edfb3-150">Идентификатор `createGenreForm` был задан в следующем коде, обнаруженном в файле *виевс\женре\\_CreateGenre. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="edfb3-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="edfb3-151">Вспомогательная перегрузка [HTML. бегинформ](https://msdn.microsoft.com/library/dd492714.aspx) , используемая в файле *виевс\женре\\_CreateGenre. cshtml* , создает HTML с атрибутом Action, содержащим URL-адрес для отправки формы.</span><span class="sxs-lookup"><span data-stu-id="edfb3-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="edfb3-152">Это можно увидеть, отобразив страницу Создание альбома в браузере и выбрав пункт Показать исходный код в браузере.</span><span class="sxs-lookup"><span data-stu-id="edfb3-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="edfb3-153">В следующей разметке показан созданный код HTML, содержащий тег form.</span><span class="sxs-lookup"><span data-stu-id="edfb3-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="edfb3-154">Строка jQuery `$.post` делает вызов AJAX атрибутом Action (`/StoreManager/Create`) и передает данные из диалогового окна **создание жанра** .</span><span class="sxs-lookup"><span data-stu-id="edfb3-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="edfb3-155">Данные состоят из имени нового жанра и необязательного описания.</span><span class="sxs-lookup"><span data-stu-id="edfb3-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="edfb3-156">При успешном вызове AJAX в разметку Select добавляется новое имя и значение жанра, а для нового жанра устанавливается выбранное значение.</span><span class="sxs-lookup"><span data-stu-id="edfb3-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="edfb3-157">Так как это динамически создаваемая разметка, вы не можете увидеть новый параметр SELECT, просмотрев исходный код в браузере.</span><span class="sxs-lookup"><span data-stu-id="edfb3-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="edfb3-158">Новый HTML-код можно увидеть с помощью средств разработчика F12 9 для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="edfb3-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="edfb3-159">Чтобы просмотреть новый параметр SELECT, в Internet Explorer 9 нажмите клавишу F12, чтобы запустить средства разработчика F12.</span><span class="sxs-lookup"><span data-stu-id="edfb3-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="edfb3-160">Перейдите на страницу создания и добавьте новый жанр, чтобы выбрать новый жанр в списке жанр выбор.</span><span class="sxs-lookup"><span data-stu-id="edfb3-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="edfb3-161">В средствах разработчика F12:</span><span class="sxs-lookup"><span data-stu-id="edfb3-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="edfb3-162">Перейдите на вкладку HTML.</span><span class="sxs-lookup"><span data-stu-id="edfb3-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="edfb3-163">Нажмите значок обновления.</span><span class="sxs-lookup"><span data-stu-id="edfb3-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="edfb3-164">В поле поиска введите GenreID.</span><span class="sxs-lookup"><span data-stu-id="edfb3-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="edfb3-165">С помощью следующего значка</span><span class="sxs-lookup"><span data-stu-id="edfb3-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="edfb3-166">Перейдите к следующему тегу SELECT:</span><span class="sxs-lookup"><span data-stu-id="edfb3-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="edfb3-167">Разверните Последнее значение параметра.</span><span class="sxs-lookup"><span data-stu-id="edfb3-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="edfb3-168">В следующем коде в файле *скриптс\чусеженре.ЖС* показано, как кнопка **Добавить новый жанра** будет подключена к событию Click и как будет создано диалоговое окно **Добавление нового жанра** .</span><span class="sxs-lookup"><span data-stu-id="edfb3-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="edfb3-169">В первой строке создается функция Click, присоединенная к кнопке **Добавить новый жанр** .</span><span class="sxs-lookup"><span data-stu-id="edfb3-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="edfb3-170">Следующая разметка из файла Виевс\стореманажер\\_ChooseGenre. cshtml показывает, как создается кнопка **Добавить новый жанр** :</span><span class="sxs-lookup"><span data-stu-id="edfb3-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="edfb3-171">Метод Load создает и открывает диалоговое окно Добавление жанра и вызывает метод jQuery `parse`, чтобы клиентская проверка находилась на данных, вводимых в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="edfb3-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="edfb3-172">В этом разделе вы узнали, как создать диалоговое окно, которое можно использовать для добавления новых данных категорий в список выбора.</span><span class="sxs-lookup"><span data-stu-id="edfb3-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="edfb3-173">Вы можете выполнить ту же процедуру для создания пользовательского интерфейса, чтобы добавить нового исполнителя в список выбора исполнителя.</span><span class="sxs-lookup"><span data-stu-id="edfb3-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="edfb3-174">В этом учебнике представлен обзор работы с **DropDownList**модуля поддержки HTML ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="edfb3-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="edfb3-175">Дополнительные сведения о работе с **DropDownList**см. в разделе "Дополнительные ссылки" ниже.</span><span class="sxs-lookup"><span data-stu-id="edfb3-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="edfb3-176">Свяжитесь с нами, если учебник полезен.</span><span class="sxs-lookup"><span data-stu-id="edfb3-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="edfb3-177">Rick.Anderson[at]Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="edfb3-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="edfb3-178">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="edfb3-178">Additional References</span></span>

- <span data-ttu-id="edfb3-179">[ASP.NET MVC — руководство по каскадным раскрывающимся спискам](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) с помощью [Раду енука](https://weblogs.asp.net/raduenuca/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="edfb3-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="edfb3-180">[Выбрано](https://harvesthq.github.com/chosen/) Подключаемый модуль JavaScript, поддерживающий множественный выбор и фильтрацию.</span><span class="sxs-lookup"><span data-stu-id="edfb3-180">[Chosen](https://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="edfb3-181">Участники</span><span class="sxs-lookup"><span data-stu-id="edfb3-181">Contributors</span></span>

- [<span data-ttu-id="edfb3-182">Раду Енука</span><span class="sxs-lookup"><span data-stu-id="edfb3-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="edfb3-183">Жан-Сéбастиен Гаупил</span><span class="sxs-lookup"><span data-stu-id="edfb3-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="edfb3-184">Михаил Уилсон (</span><span class="sxs-lookup"><span data-stu-id="edfb3-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="edfb3-185">Рецензенты</span><span class="sxs-lookup"><span data-stu-id="edfb3-185">Reviewers</span></span>

- <span data-ttu-id="edfb3-186">Жан-Сéбастиен Гаупил</span><span class="sxs-lookup"><span data-stu-id="edfb3-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="edfb3-187">Михаил Уилсон (</span><span class="sxs-lookup"><span data-stu-id="edfb3-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="edfb3-188">Майк Поуп</span><span class="sxs-lookup"><span data-stu-id="edfb3-188">Mike Pope</span></span>
- <span data-ttu-id="edfb3-189">Tom Dykstra)</span><span class="sxs-lookup"><span data-stu-id="edfb3-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="edfb3-190">Назад</span><span class="sxs-lookup"><span data-stu-id="edfb3-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
