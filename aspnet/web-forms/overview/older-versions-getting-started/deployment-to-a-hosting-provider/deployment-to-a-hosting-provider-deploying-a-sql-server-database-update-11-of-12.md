---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание обновления базы данных SQL Server-11 из 12 | Документация Майкрософт'
author: tdykstra
description: В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78423978"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="d18c6-103">Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание обновления базы данных SQL Server-11 из 12</span><span class="sxs-lookup"><span data-stu-id="d18c6-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>

<span data-ttu-id="d18c6-104">от [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d18c6-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d18c6-105">Скачать начальный проект</span><span class="sxs-lookup"><span data-stu-id="d18c6-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="d18c6-106">В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web.</span><span class="sxs-lookup"><span data-stu-id="d18c6-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="d18c6-107">При установке обновления веб-публикации можно также использовать Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="d18c6-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="d18c6-108">Введение в серию см. [в первом учебнике серии](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="d18c6-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="d18c6-109">Руководство, в котором показаны функции развертывания, появившиеся после выпуска версии-КАНДИДАТа Visual Studio 2012, демонстрирует развертывание SQL Server выпусков, отличных от SQL Server Compact, и демонстрация развертывания на веб-сайтах Windows Azure см. в разделе [ASP.NET Web Deploying using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d18c6-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="d18c6-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="d18c6-110">Overview</span></span>

<span data-ttu-id="d18c6-111">В этом руководстве показано, как развернуть обновление базы данных в полной SQL Server базе данных.</span><span class="sxs-lookup"><span data-stu-id="d18c6-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="d18c6-112">Поскольку Code First Migrations выполняет всю работу по обновлению базы данных, процесс практически идентичен тому, что вы делали для SQL Server Compact в учебнике [развертывание обновления базы данных](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) .</span><span class="sxs-lookup"><span data-stu-id="d18c6-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="d18c6-113">Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="d18c6-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="d18c6-114">Добавление нового столбца в таблицу</span><span class="sxs-lookup"><span data-stu-id="d18c6-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="d18c6-115">В этом разделе учебника вы измените базу данных и внесите соответствующие изменения в код, а затем протестируйте их в Visual Studio, чтобы подготовиться к развертыванию в тестовой и рабочей средах.</span><span class="sxs-lookup"><span data-stu-id="d18c6-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="d18c6-116">Это изменение включает добавление `OfficeHours` столбца в сущность `Instructor` и отображение новых сведений на веб-странице **инструкторов** .</span><span class="sxs-lookup"><span data-stu-id="d18c6-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="d18c6-117">В проекте ContosoUniversity. DAL откройте *Instructor.CS* и добавьте следующее свойство между свойствами `HireDate` и `Courses`:</span><span class="sxs-lookup"><span data-stu-id="d18c6-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="d18c6-118">Обновите класс инициализатора таким образом, чтобы он выполнив новый столбец с тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="d18c6-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="d18c6-119">Откройте *Migrations\Configuration.CS* и замените блок кода, который начинается `var instructors = new List<Instructor>`, на следующий блок кода, включающий новый столбец:</span><span class="sxs-lookup"><span data-stu-id="d18c6-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="d18c6-120">В проекте ContosoUniversity откройте *инструкторы. aspx* и добавьте новое поле шаблона для Office Hours непосредственно перед закрывающим тегом `</Columns>` в первом элементе управления `GridView`:</span><span class="sxs-lookup"><span data-stu-id="d18c6-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="d18c6-121">Создайте решение.</span><span class="sxs-lookup"><span data-stu-id="d18c6-121">Build the solution.</span></span>

<span data-ttu-id="d18c6-122">Откройте окно **консоли диспетчера пакетов** и выберите в качестве **проекта по умолчанию**ContosoUniversity. DAL.</span><span class="sxs-lookup"><span data-stu-id="d18c6-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="d18c6-123">Введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="d18c6-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="d18c6-124">Запустите приложение и выберите страницу **инструкторы** .</span><span class="sxs-lookup"><span data-stu-id="d18c6-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="d18c6-125">Загрузка страницы занимает немного больше времени, чем обычно, поскольку Entity Framework повторно создает базу данных и заполняет ее тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="d18c6-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="d18c6-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d18c6-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="d18c6-127">Развертывание обновления базы данных в тестовой среде</span><span class="sxs-lookup"><span data-stu-id="d18c6-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="d18c6-128">При использовании Code First Migrations метод развертывания изменения базы данных на SQL Server аналогичен для SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="d18c6-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="d18c6-129">Однако необходимо изменить профиль публикации теста, так как он все еще настроен для миграции с SQL Server Compact на SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d18c6-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="d18c6-130">Первым шагом является удаление преобразований строки подключения, созданных в предыдущем руководстве.</span><span class="sxs-lookup"><span data-stu-id="d18c6-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="d18c6-131">Они больше не нужны, так как вы задаете преобразования строки подключения в профиле публикации, как это делалось перед настройкой вкладки **Пакет/Публикация SQL** для миграции на SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d18c6-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="d18c6-132">Откройте файл *Web. Test. config* и удалите элемент `connectionStrings`.</span><span class="sxs-lookup"><span data-stu-id="d18c6-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="d18c6-133">Единственным оставшимся преобразование в файле *Web. Test. config* является `Environment` значение в элементе `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="d18c6-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="d18c6-134">Теперь можно обновить профиль публикации и опубликовать его в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d18c6-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="d18c6-135">Откройте мастер **публикации веб-сайта** и перейдите на вкладку **профиль** .</span><span class="sxs-lookup"><span data-stu-id="d18c6-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="d18c6-136">Выберите профиль **тестовой** публикации.</span><span class="sxs-lookup"><span data-stu-id="d18c6-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="d18c6-137">Перейдите на вкладку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="d18c6-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="d18c6-138">Щелкните **включить новые улучшения публикации базы данных**.</span><span class="sxs-lookup"><span data-stu-id="d18c6-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="d18c6-139">В поле Строка подключения для **SchoolContext**введите то же значение, которое использовалось в файле преобразования *Web. Test. config* в предыдущем руководстве:</span><span class="sxs-lookup"><span data-stu-id="d18c6-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="d18c6-140">Выберите **выполнить Code First migrations (выполняется при запуске приложения)** .</span><span class="sxs-lookup"><span data-stu-id="d18c6-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="d18c6-141">(В вашей версии Visual Studio этот флажок может быть помечен как **применить Code First migrations**.)</span><span class="sxs-lookup"><span data-stu-id="d18c6-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="d18c6-142">В поле Строка подключения для **DefaultConnection**введите то же значение, которое использовалось в файле преобразования *Web. Test. config* в предыдущем руководстве:</span><span class="sxs-lookup"><span data-stu-id="d18c6-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="d18c6-143">Не снимайте флажок **обновлять базу данных** .</span><span class="sxs-lookup"><span data-stu-id="d18c6-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="d18c6-144">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="d18c6-144">Click **Publish**.</span></span>

<span data-ttu-id="d18c6-145">Visual Studio развертывает изменения кода в тестовой среде и открывает браузер на домашней странице университета Contoso.</span><span class="sxs-lookup"><span data-stu-id="d18c6-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="d18c6-146">Выберите страницу инструкторы.</span><span class="sxs-lookup"><span data-stu-id="d18c6-146">Select the Instructors page.</span></span>

<span data-ttu-id="d18c6-147">Когда приложение запускает эту страницу, оно пытается получить доступ к базе данных.</span><span class="sxs-lookup"><span data-stu-id="d18c6-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="d18c6-148">Code First Migrations проверяет, является ли база данных текущей, и обнаруживает, что последняя миграция еще не применена.</span><span class="sxs-lookup"><span data-stu-id="d18c6-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="d18c6-149">Code First Migrations применяет последнюю миграцию, запускает метод `Seed`, а затем страница выполняется в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="d18c6-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="d18c6-150">Вы увидите новый столбец Office Hours с заполненными данными.</span><span class="sxs-lookup"><span data-stu-id="d18c6-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="d18c6-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d18c6-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="d18c6-152">Развертывание обновления базы данных в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="d18c6-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="d18c6-153">Также необходимо изменить профиль публикации для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="d18c6-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="d18c6-154">В этом случае вы удалите существующий профиль и создадите новый, импортировав обновленный файл. publishsettings.</span><span class="sxs-lookup"><span data-stu-id="d18c6-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="d18c6-155">Обновленный файл будет содержать строку подключения для SQL Server базы данных по адресу Цитаниум.</span><span class="sxs-lookup"><span data-stu-id="d18c6-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="d18c6-156">Как было показано при развертывании в тестовой среде, в файле преобразования *Web. Production. config* больше не требуются преобразования строки соединения.</span><span class="sxs-lookup"><span data-stu-id="d18c6-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="d18c6-157">Откройте этот файл и удалите элемент `connectionStrings`.</span><span class="sxs-lookup"><span data-stu-id="d18c6-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="d18c6-158">Остальные преобразования предназначены для `Environment` значения в элементе `appSettings` и элемента `location`, который предоставляет доступ к отчетам об ошибках ELMAH.</span><span class="sxs-lookup"><span data-stu-id="d18c6-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="d18c6-159">Перед созданием нового профиля публикации для рабочей среды Скачайте обновленный файл publishsettings так же, как и ранее в учебнике [развертывание в рабочей среде](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) .</span><span class="sxs-lookup"><span data-stu-id="d18c6-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="d18c6-160">(На панели управления Цитаниум щелкните **веб-сайты**, а затем щелкните веб-сайт **contosouniversity.com** .</span><span class="sxs-lookup"><span data-stu-id="d18c6-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="d18c6-161">Выберите вкладку **веб-публикация** и нажмите кнопку **скачать профиль публикации для этого веб-сайта**.) Причина заключается в том, чтобы получить строку подключения к базе данных в publishsettings-файле.</span><span class="sxs-lookup"><span data-stu-id="d18c6-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="d18c6-162">Строка подключения была недоступна при первой загрузке файла, так как вы все еще используете SQL Server Compact и еще не создали базу данных SQL Server в Цитаниум.</span><span class="sxs-lookup"><span data-stu-id="d18c6-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="d18c6-163">Теперь можно обновить профиль публикации и опубликовать его в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d18c6-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="d18c6-164">Откройте мастер **публикации веб-сайта** и перейдите на вкладку **профиль** .</span><span class="sxs-lookup"><span data-stu-id="d18c6-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="d18c6-165">Щелкните **Управление профилями**, а затем удалите рабочий профиль.</span><span class="sxs-lookup"><span data-stu-id="d18c6-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="d18c6-166">Закройте мастер **публикации веб-сайта** , чтобы сохранить это изменение.</span><span class="sxs-lookup"><span data-stu-id="d18c6-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="d18c6-167">Снова откройте мастер **публикации веб-сайта** и нажмите кнопку **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="d18c6-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="d18c6-168">На вкладке **Подключение** измените **URL-адрес назначения** на соответствующее значение, если используется временный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d18c6-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="d18c6-169">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d18c6-169">Click **Next**.</span></span>

<span data-ttu-id="d18c6-170">На вкладке **Параметры** щелкните **включить новые улучшения публикации базы данных**.</span><span class="sxs-lookup"><span data-stu-id="d18c6-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="d18c6-171">В раскрывающемся списке Строка подключения для **SchoolContext**выберите строку подключения цитаниум.</span><span class="sxs-lookup"><span data-stu-id="d18c6-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="d18c6-173">Выберите **выполнить миграцию Code First (выполняется при запуске приложения)** .</span><span class="sxs-lookup"><span data-stu-id="d18c6-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="d18c6-174">В раскрывающемся списке Строка подключения для **DefaultConnection**выберите строку подключения цитаниум.</span><span class="sxs-lookup"><span data-stu-id="d18c6-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="d18c6-175">Перейдите на вкладку **профиль** , щелкните **Управление профилями**и переименуйте профиль с "contosouniversity.com-веб-развертывание" на "Production".</span><span class="sxs-lookup"><span data-stu-id="d18c6-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="d18c6-176">Закройте профиль публикации, чтобы сохранить изменения, а затем откройте его снова.</span><span class="sxs-lookup"><span data-stu-id="d18c6-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="d18c6-177">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="d18c6-177">Click **Publish**.</span></span> <span data-ttu-id="d18c6-178">(Для реального рабочего веб-сайта можно скопировать *приложение\_offline. htm* в рабочую среду и разместить его в папке проекта перед публикацией, а затем удалить его после завершения развертывания.)</span><span class="sxs-lookup"><span data-stu-id="d18c6-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="d18c6-179">Visual Studio развертывает изменения кода в тестовой среде и открывает браузер на домашней странице университета Contoso.</span><span class="sxs-lookup"><span data-stu-id="d18c6-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="d18c6-180">Выберите страницу инструкторы.</span><span class="sxs-lookup"><span data-stu-id="d18c6-180">Select the Instructors page.</span></span>

<span data-ttu-id="d18c6-181">Code First Migrations обновляет базу данных так же, как в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d18c6-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="d18c6-182">Вы увидите новый столбец Office Hours с заполненными данными.</span><span class="sxs-lookup"><span data-stu-id="d18c6-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="d18c6-184">Обновление приложения, которое включало изменение базы данных, успешно развернуто с помощью SQL Server базы данных.</span><span class="sxs-lookup"><span data-stu-id="d18c6-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="d18c6-185">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="d18c6-185">More Information</span></span>

<span data-ttu-id="d18c6-186">Эта серия руководств по развертыванию веб-приложения ASP.NET для сторонних поставщиков услуг размещения завершается.</span><span class="sxs-lookup"><span data-stu-id="d18c6-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="d18c6-187">Дополнительные сведения о любом из разделов, рассмотренных в этих учебниках, см. на странице [ASP.NET Deployment (схема содержимого развертывания](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) ) на веб-сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="d18c6-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="d18c6-188">Благодарности</span><span class="sxs-lookup"><span data-stu-id="d18c6-188">Acknowledgements</span></span>

<span data-ttu-id="d18c6-189">Я хотел бы поблагодарить следующих людей, которые внесли значительные вклады в содержание этой серии руководств:</span><span class="sxs-lookup"><span data-stu-id="d18c6-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="d18c6-190">Альберто ПоблаЦион, MVP &amp; MCT, Испания</span><span class="sxs-lookup"><span data-stu-id="d18c6-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="d18c6-191">Жарод Фергюсон, MVP по разработке платформы данных США</span><span class="sxs-lookup"><span data-stu-id="d18c6-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="d18c6-192">Харша Миттал, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d18c6-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="d18c6-193">Кристина Олсон, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d18c6-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="d18c6-194">Майк Поуп, Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d18c6-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="d18c6-195">Мохит Сривастава, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d18c6-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="d18c6-196">Раффаеле Риалди, Италия</span><span class="sxs-lookup"><span data-stu-id="d18c6-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="d18c6-197">Рик Андерсон (, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d18c6-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="d18c6-198">[Саид Хашими, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="d18c6-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="d18c6-199">[Скотт Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="d18c6-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="d18c6-200">[Скотт Хантер, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="d18c6-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="d18c6-201">Срđан Боžовиć, Сербия</span><span class="sxs-lookup"><span data-stu-id="d18c6-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="d18c6-202">[Вишал Джоши, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="d18c6-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d18c6-203">[Назад](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [Вперед](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="d18c6-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
