---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'ASP.NET веб-развертывание с помощью Visual Studio: развертывание обновления базы данных | Документация Майкрософт'
author: tdykstra
description: В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика, Усин...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440790"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="c187e-103">Веб-развертывание ASP.NET с помощью Visual Studio: развертывание обновления базы данных</span><span class="sxs-lookup"><span data-stu-id="c187e-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>

<span data-ttu-id="c187e-104">от [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c187e-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="c187e-105">Скачать начальный проект</span><span class="sxs-lookup"><span data-stu-id="c187e-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="c187e-106">В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика с помощью Visual Studio 2012 или Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="c187e-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="c187e-107">Сведения о ряде см. в [первом руководстве по ряду](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c187e-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="c187e-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="c187e-108">Overview</span></span>

<span data-ttu-id="c187e-109">В этом руководстве вы вносите изменения в базу данных и связанную с ней изменения кода, тестируете изменения в Visual Studio, а затем развертываете обновление в тестовой, промежуточной и рабочей средах.</span><span class="sxs-lookup"><span data-stu-id="c187e-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="c187e-110">Сначала в руководстве показано, как обновить базу данных, управляемую с помощью Code First Migrations, а затем в дальнейшем будет показано, как обновить базу данных с помощью поставщика Дбдакфкс.</span><span class="sxs-lookup"><span data-stu-id="c187e-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="c187e-111">Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c187e-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="c187e-112">Развертывание обновления базы данных с помощью Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="c187e-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="c187e-113">В этом разделе вы добавите столбец даты рождения в базовый класс `Person` для сущностей `Student` и `Instructor`.</span><span class="sxs-lookup"><span data-stu-id="c187e-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="c187e-114">Затем вы обновите страницу, на которой отображаются данные о преподавателе, чтобы отобразить новый столбец.</span><span class="sxs-lookup"><span data-stu-id="c187e-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="c187e-115">Наконец, вы развертываете изменения для тестирования, промежуточного хранения и рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="c187e-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="c187e-116">Добавление столбца в таблицу в базе данных приложения</span><span class="sxs-lookup"><span data-stu-id="c187e-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="c187e-117">В проекте *ContosoUniversity. DAL* откройте *Person.CS* и добавьте следующее свойство в конце класса `Person` (после него должны быть две закрывающие фигурные скобки):</span><span class="sxs-lookup"><span data-stu-id="c187e-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="c187e-118">Затем обновите метод `Seed` таким образом, чтобы он выдает значение для нового столбца.</span><span class="sxs-lookup"><span data-stu-id="c187e-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="c187e-119">Откройте *Migrations\Configuration.CS* и замените блок кода, который начинается `var instructors = new List<Instructor>`, на следующий блок кода, содержащий сведения о дате рождения:</span><span class="sxs-lookup"><span data-stu-id="c187e-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="c187e-120">Выполните сборку решения, а затем откройте окно **консоли диспетчера пакетов** .</span><span class="sxs-lookup"><span data-stu-id="c187e-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="c187e-121">Убедитесь, что ContosoUniversity. DAL по-прежнему выбран в качестве **проекта по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="c187e-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="c187e-122">В окне **консоли диспетчера пакетов** выберите **ContosoUniversity. DAL** в качестве **проекта по умолчанию**, а затем введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c187e-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="c187e-123">По завершении этой команды Visual Studio открывает файл класса, который определяет новый класс `DbMigration`, а в методе `Up` можно увидеть код, создающий новый столбец.</span><span class="sxs-lookup"><span data-stu-id="c187e-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="c187e-124">Метод `Up` создает столбец при реализации изменения, а метод `Down` удаляет столбец при откате изменения.</span><span class="sxs-lookup"><span data-stu-id="c187e-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="c187e-126">Выполните сборку решения, а затем введите следующую команду в окне **консоли диспетчера пакетов** (убедитесь, что проект CONTOSOUNIVERSITY. DAL по-прежнему выбран):</span><span class="sxs-lookup"><span data-stu-id="c187e-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="c187e-127">Entity Framework выполняет метод `Up`, а затем выполняет метод `Seed`.</span><span class="sxs-lookup"><span data-stu-id="c187e-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="c187e-128">Отображение нового столбца на странице инструкторов</span><span class="sxs-lookup"><span data-stu-id="c187e-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="c187e-129">В проекте ContosoUniversity откройте *инструкторы. aspx* и добавьте новое поле шаблона, чтобы отобразить дату рождения.</span><span class="sxs-lookup"><span data-stu-id="c187e-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="c187e-130">Добавьте его между ними для даты найма и назначения Office:</span><span class="sxs-lookup"><span data-stu-id="c187e-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="c187e-131">(Если отступы кода не синхронизированы, можно нажать сочетание клавиш CTRL-K и CTRL-D, чтобы автоматически переформатировать файл.)</span><span class="sxs-lookup"><span data-stu-id="c187e-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="c187e-132">Запустите приложение и щелкните ссылку **инструкторы** .</span><span class="sxs-lookup"><span data-stu-id="c187e-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="c187e-133">Когда страница загрузится, вы увидите, что в ней есть новое поле даты рождения.</span><span class="sxs-lookup"><span data-stu-id="c187e-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![Страница инструкторов с ДеньРождения](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="c187e-135">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="c187e-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="c187e-136">Развертывание обновления базы данных</span><span class="sxs-lookup"><span data-stu-id="c187e-136">Deploy the database update</span></span>

1. <span data-ttu-id="c187e-137">В **Обозреватель решений** выберите проект ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="c187e-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="c187e-138">На панели инструментов **веб-публикация одним щелчком** выберите профиль **тестовой** публикации и щелкните **Опубликовать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="c187e-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="c187e-139">(Если панель инструментов отключена, выберите проект ContosoUniversity в **Обозреватель решений**.)</span><span class="sxs-lookup"><span data-stu-id="c187e-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="c187e-140">Visual Studio развертывает обновленное приложение, и браузер открывается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="c187e-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="c187e-141">Запустите страницу **инструкторы** , чтобы убедиться, что обновление успешно развернуто.</span><span class="sxs-lookup"><span data-stu-id="c187e-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="c187e-142">Когда приложение пытается получить доступ к базе данных для этой страницы, Code First обновляет схему базы данных и выполняет метод `Seed`.</span><span class="sxs-lookup"><span data-stu-id="c187e-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="c187e-143">При отображении страницы отображается столбец ожидаемая **Дата рождения** с датами в нем.</span><span class="sxs-lookup"><span data-stu-id="c187e-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="c187e-144">На панели инструментов **веб-публикация одним щелчком** выберите профиль **промежуточной** публикации, а затем щелкните **Опубликовать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="c187e-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="c187e-145">Запустите страницу **инструкторов** в промежуточной среде, чтобы убедиться, что обновление успешно развернуто.</span><span class="sxs-lookup"><span data-stu-id="c187e-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="c187e-146">На панели инструментов **веб-публикация одним щелчком** выберите профиль **рабочей** публикации и нажмите кнопку **Опубликовать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="c187e-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="c187e-147">Запустите страницу **инструкторов** в рабочей среде, чтобы убедиться, что обновление успешно развернуто.</span><span class="sxs-lookup"><span data-stu-id="c187e-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="c187e-148">Для реального обновления производственного приложения, включающего изменение базы данных, обычно приложение переводится в автономный режим во время развертывания с помощью *приложения\_автономно. htm*, как было показано в предыдущем руководстве.</span><span class="sxs-lookup"><span data-stu-id="c187e-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="c187e-149">Развертывание обновления базы данных с помощью поставщика Дбдакфкс</span><span class="sxs-lookup"><span data-stu-id="c187e-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="c187e-150">В этом разделе вы добавите столбец *комментариев* в *пользовательскую* таблицу в базе данных членства и создадите страницу, позволяющую отображать и редактировать комментарии для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="c187e-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="c187e-151">Затем вы развертываете изменения для тестирования, промежуточного хранения и рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="c187e-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="c187e-152">Добавление столбца в таблицу в базе данных членства</span><span class="sxs-lookup"><span data-stu-id="c187e-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="c187e-153">В Visual Studio откройте **Обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c187e-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="c187e-154">Разверните узел **(LocalDB) \v11.0**, разверните узел **базы данных**, разверните узел **ASPNET-ContosoUniversity** (не **ASPNET-ContosoUniversity-произв**.), а затем разверните узел **таблицы**.</span><span class="sxs-lookup"><span data-stu-id="c187e-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="c187e-155">Если вы не видите **(LocalDB) \v11.0** в узле **SQL Server** , щелкните правой кнопкой мыши узел **SQL Server** и выберите команду **Добавить SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c187e-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="c187e-156">В диалоговом окне **соединение с сервером** введите *(LocalDB) \v11.0* в качестве **имени сервера**и нажмите кнопку **подключить**.</span><span class="sxs-lookup"><span data-stu-id="c187e-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="c187e-157">Если вы не видите элемент **ASPNET-ContosoUniversity**, запустите проект и войдите в систему, используя учетные данные *администратора* (пароль — *девпвд*), а затем обновите окно **Обозреватель объектов SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="c187e-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="c187e-158">Щелкните правой кнопкой мыши таблицу **Пользователи** и выберите пункт **Конструктор представлений**.</span><span class="sxs-lookup"><span data-stu-id="c187e-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![Конструктор представлений SSOX](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="c187e-160">В конструкторе добавьте столбец *Comments* и сделайте его *nvarchar (128)* и Nullable, а затем нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="c187e-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![Добавление столбца комментариев](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="c187e-162">В поле **Предварительный просмотр обновлений базы данных** щелкните **обновить базу данных**.</span><span class="sxs-lookup"><span data-stu-id="c187e-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![Предварительный просмотр обновлений базы данных](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="c187e-164">Создание страницы для просмотра и изменения нового столбца</span><span class="sxs-lookup"><span data-stu-id="c187e-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="c187e-165">В **Обозреватель решений**щелкните правой кнопкой мыши папку **учетной записи** в проекте ContosoUniversity, выберите **Добавить**, а затем щелкните **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="c187e-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="c187e-166">Создайте новую **веб-форму с помощью главной страницы** и назовите ее *userInfo. aspx*.</span><span class="sxs-lookup"><span data-stu-id="c187e-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="c187e-167">Примите файл *site. master* по умолчанию в качестве главной страницы.</span><span class="sxs-lookup"><span data-stu-id="c187e-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="c187e-168">Скопируйте следующую разметку в элемент `MainContent` `Content` (последний из 3 `Content` элементов):</span><span class="sxs-lookup"><span data-stu-id="c187e-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="c187e-169">Щелкните правой кнопкой мыши страницу *userInfo. aspx* и выберите пункт **Просмотр в браузере**.</span><span class="sxs-lookup"><span data-stu-id="c187e-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="c187e-170">Войдите в систему с учетными данными *администратора* ( *девпвд*) и добавьте к пользователю комментарии, чтобы убедиться, что страница работает правильно.</span><span class="sxs-lookup"><span data-stu-id="c187e-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![Страница UserInfo](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="c187e-172">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="c187e-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="c187e-173">Развертывание обновления базы данных</span><span class="sxs-lookup"><span data-stu-id="c187e-173">Deploy the database update</span></span>

<span data-ttu-id="c187e-174">Чтобы выполнить развертывание с помощью поставщика Дбдакфкс, необходимо просто выбрать параметр **обновить базу данных** в профиле публикации.</span><span class="sxs-lookup"><span data-stu-id="c187e-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="c187e-175">Однако для первоначального развертывания при использовании этого параметра вы также настроили некоторые дополнительные скрипты SQL для выполнения: они все еще находятся в профиле, и вам нужно будет предотвратить их повторное выполнение.</span><span class="sxs-lookup"><span data-stu-id="c187e-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="c187e-176">Откройте мастер **публикации веб-сайта** , щелкнув правой кнопкой мыши проект ContosoUniversity и выбрав **Publish (опубликовать**).</span><span class="sxs-lookup"><span data-stu-id="c187e-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="c187e-177">Выберите профиль **тестирования** .</span><span class="sxs-lookup"><span data-stu-id="c187e-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="c187e-178">Перейдите на вкладку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="c187e-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="c187e-179">В разделе **DefaultConnection**выберите **обновить базу данных**.</span><span class="sxs-lookup"><span data-stu-id="c187e-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="c187e-180">Отключите дополнительные скрипты, которые были настроены для выполнения начального развертывания:</span><span class="sxs-lookup"><span data-stu-id="c187e-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="c187e-181">Щелкните **настроить обновления базы данных**.</span><span class="sxs-lookup"><span data-stu-id="c187e-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="c187e-182">В диалоговом окне **Настройка обновлений базы данных** снимите флажки для *GRANT. SQL* и *АСПнет-Дата-дев. SQL*.</span><span class="sxs-lookup"><span data-stu-id="c187e-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="c187e-183">Щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="c187e-183">Click **Close**.</span></span>
6. <span data-ttu-id="c187e-184">Перейдите на вкладку **Предварительный просмотр** .</span><span class="sxs-lookup"><span data-stu-id="c187e-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="c187e-185">В разделе **базы данных** и справа от **DefaultConnection**щелкните ссылку **Предварительная версия базы данных** .</span><span class="sxs-lookup"><span data-stu-id="c187e-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![Предварительная версия базы данных](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="c187e-187">В окне предварительного просмотра отображается скрипт, который будет выполняться в целевой базе данных, чтобы схема базы данных совпадала со схемой базы данных источника.</span><span class="sxs-lookup"><span data-stu-id="c187e-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="c187e-188">Скрипт включает команду ALTER TABLE, которая добавляет новый столбец.</span><span class="sxs-lookup"><span data-stu-id="c187e-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="c187e-189">Закройте диалоговое окно **Предварительный просмотр базы данных** и нажмите кнопку **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c187e-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="c187e-190">Visual Studio развертывает обновленное приложение, и браузер открывается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="c187e-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="c187e-191">Запустите страницу UserInfo (добавьте *учетную запись/UserInfo. aspx* к URL-адресу домашней страницы), чтобы убедиться, что обновление успешно развернуто.</span><span class="sxs-lookup"><span data-stu-id="c187e-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="c187e-192">Вам потребуется войти в систему, введя *Admin* and *девпвд*.</span><span class="sxs-lookup"><span data-stu-id="c187e-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="c187e-193">Данные в таблицах не развертываются по умолчанию, и вы не настроили скрипт развертывания данных для выполнения, поэтому вы не найдете комментарий, добавленный при разработке.</span><span class="sxs-lookup"><span data-stu-id="c187e-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="c187e-194">Теперь можно добавить новый комментарий в промежуточной среде, чтобы убедиться, что изменение было развернуто в базе данных, и страница работает правильно.</span><span class="sxs-lookup"><span data-stu-id="c187e-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="c187e-195">Выполните ту же процедуру для развертывания в промежуточной и рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c187e-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="c187e-196">Не забудьте отключить дополнительные сценарии.</span><span class="sxs-lookup"><span data-stu-id="c187e-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="c187e-197">Единственная разница по сравнению с профилем тестирования заключается в том, что в промежуточном и рабочем профилях будет отключен только один скрипт, так как они были настроены для запуска только *АСПнет-прод-Дата. SQL*.</span><span class="sxs-lookup"><span data-stu-id="c187e-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="c187e-198">Учетные данные для промежуточного хранения и рабочей среды — Admin и продпвд.</span><span class="sxs-lookup"><span data-stu-id="c187e-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="c187e-199">Для реального обновления производственного приложения, включающего изменение базы данных, обычно приложение переводится в автономный режим во время развертывания путем отправки приложения *\_автономно. htm* перед публикацией и удалением в дальнейшем, как было показано в [предыдущем руководстве](deploying-a-code-update.md).</span><span class="sxs-lookup"><span data-stu-id="c187e-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="c187e-200">Сводка</span><span class="sxs-lookup"><span data-stu-id="c187e-200">Summary</span></span>

<span data-ttu-id="c187e-201">Теперь вы развернули обновление приложения, которое включало изменение базы данных, с помощью Code First Migrations и поставщика Дбдакфкс.</span><span class="sxs-lookup"><span data-stu-id="c187e-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![Страница инструкторов с ДеньРождения](deploying-a-database-update/_static/image8.png)

![Страница UserInfo](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="c187e-204">В следующем учебнике показано, как выполнять развертывания с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="c187e-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c187e-205">[Назад](deploying-a-code-update.md)
> [Вперед](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="c187e-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
