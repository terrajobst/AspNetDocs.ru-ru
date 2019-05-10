---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Использование веб-API 2 с Entity Framework 6 | Документация Майкрософт
author: MikeWasson
description: Этот учебник поможет, что основы создания веб-приложения с помощью ASP.NET Web API серверной части. В этом руководстве используется Entity Framework 6 для макета данных...
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65126289"
---
# <a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="b3906-104">Использование веб-API 2 с Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="b3906-104">Using Web API 2 with Entity Framework 6</span></span>

[<span data-ttu-id="b3906-105">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="b3906-105">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="b3906-106">В этом учебнике вы что основы создания веб-приложения с помощью ASP.NET Web API серверной части.</span><span class="sxs-lookup"><span data-stu-id="b3906-106">This tutorial teaches you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="b3906-107">В руководстве используется Entity Framework 6 для уровня данных и Knockout.js для клиентского приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b3906-107">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="b3906-108">Этом руководстве также показано, как развернуть приложение в веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="b3906-108">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b3906-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="b3906-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="b3906-110">Веб-API 2.1</span><span class="sxs-lookup"><span data-stu-id="b3906-110">Web API 2.1</span></span>
> - <span data-ttu-id="b3906-111">Visual Studio 2017 (скачать Visual Studio 2017 [здесь](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="b3906-111">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="b3906-112">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="b3906-112">Entity Framework 6</span></span>
> - <span data-ttu-id="b3906-113">.NET 4.7</span><span class="sxs-lookup"><span data-stu-id="b3906-113">.NET 4.7</span></span>
> - <span data-ttu-id="b3906-114">[Knockout.js](http://knockoutjs.com/) 3.1</span><span class="sxs-lookup"><span data-stu-id="b3906-114">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>

<span data-ttu-id="b3906-115">Этом руководстве используется ASP.NET Web API 2 с Entity Framework 6 создание веб-приложения, который управляет серверной базы данных.</span><span class="sxs-lookup"><span data-stu-id="b3906-115">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="b3906-116">Ниже приведен снимок экрана приложения, который будет создан.</span><span class="sxs-lookup"><span data-stu-id="b3906-116">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="b3906-117">Приложение использует разработки одностраничное приложение (SPA).</span><span class="sxs-lookup"><span data-stu-id="b3906-117">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="b3906-118">«Одностраничного приложения» — это общий термин для веб-приложения, который загружает единственную HTML-страницу и затем обновляет страницу динамически, вместо загрузки новых страниц.</span><span class="sxs-lookup"><span data-stu-id="b3906-118">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="b3906-119">После загрузки начальной страницы приложение взаимодействует с сервером с помощью запросов AJAX.</span><span class="sxs-lookup"><span data-stu-id="b3906-119">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="b3906-120">AJAX запрашивает возвращаемых данных JSON, которые приложение использует для обновления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b3906-120">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="b3906-121">AJAX – не Новинка, но на сегодняшний день существует платформ JavaScript, которые упрощают создание и обслуживание большого сложные приложения SPA.</span><span class="sxs-lookup"><span data-stu-id="b3906-121">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="b3906-122">В этом руководстве используется [Knockout.js](http://knockoutjs.com/), но вы можете использовать любую платформу клиента JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b3906-122">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="b3906-123">Ниже приведены основные строительные блоки для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="b3906-123">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="b3906-124">ASP.NET MVC создает HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="b3906-124">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="b3906-125">Веб-API ASP.NET обрабатывает запросы AJAX и возвращает данные JSON.</span><span class="sxs-lookup"><span data-stu-id="b3906-125">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="b3906-126">Knockout.js привязывает данные HTML-элементов для данных JSON.</span><span class="sxs-lookup"><span data-stu-id="b3906-126">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="b3906-127">Платформа Entity Framework обращается к базе данных.</span><span class="sxs-lookup"><span data-stu-id="b3906-127">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="b3906-128">Это приложение работает в Azure см. в разделе</span><span class="sxs-lookup"><span data-stu-id="b3906-128">See this app running on Azure</span></span>

<span data-ttu-id="b3906-129">Вы действительно хотите см. по завершении сайт, запущенный в качестве активного веб-приложения?</span><span class="sxs-lookup"><span data-stu-id="b3906-129">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="b3906-130">Полную версию приложения можно развернуть учетную запись Azure, нажав кнопку ниже.</span><span class="sxs-lookup"><span data-stu-id="b3906-130">You can deploy a complete version of the app to your Azure account by selecting the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="b3906-131">Требуется учетная запись Azure для развертывания этого решения в Azure.</span><span class="sxs-lookup"><span data-stu-id="b3906-131">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="b3906-132">Если у вас еще нет учетной записи, у вас есть следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="b3906-132">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="b3906-133">[Открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -вы получаете кредиты можно использовать для опробования платных служб Azure и даже в том случае, если они используются, вы сохраняете учетную запись и использовать бесплатные службы Azure.</span><span class="sxs-lookup"><span data-stu-id="b3906-133">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="b3906-134">[Активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -ваша подписка MSDN предоставляет вам кредиты каждый месяц, который можно использовать для оплаты служб Azure.</span><span class="sxs-lookup"><span data-stu-id="b3906-134">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="b3906-135">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="b3906-135">Create the project</span></span>

<span data-ttu-id="b3906-136">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b3906-136">Open Visual Studio.</span></span> <span data-ttu-id="b3906-137">Из **файл** меню, выберите **New**, а затем выберите **проекта**.</span><span class="sxs-lookup"><span data-stu-id="b3906-137">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="b3906-138">(Или выберите **новый проект** на начальной странице.)</span><span class="sxs-lookup"><span data-stu-id="b3906-138">(Or select **New Project** on the Start page.)</span></span>

<span data-ttu-id="b3906-139">В **новый проект** диалоговом окне выберите **Web** в левой области и **веб-приложение ASP.NET (.NET Framework)** в средней области.</span><span class="sxs-lookup"><span data-stu-id="b3906-139">In the **New Project** dialog, select **Web** in the left pane and **ASP.NET Web Application (.NET Framework)** in the middle pane.</span></span> <span data-ttu-id="b3906-140">Назовите проект **BookService** и выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b3906-140">Name the project **BookService** and select **OK**.</span></span>

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

<span data-ttu-id="b3906-141">В **новый проект ASP.NET** диалоговом окне выберите **веб-API** шаблона.</span><span class="sxs-lookup"><span data-stu-id="b3906-141">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

<span data-ttu-id="b3906-142">Нажмите кнопку **ОК**, чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="b3906-142">Select **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="b3906-143">Настройте параметры Azure (необязательно)</span><span class="sxs-lookup"><span data-stu-id="b3906-143">Configure Azure settings (optional)</span></span>

<span data-ttu-id="b3906-144">После создания проекта, вы можете развернуть веб-приложениях службы приложений Azure в любое время.</span><span class="sxs-lookup"><span data-stu-id="b3906-144">After you create the project, you can choose to deploy to Azure App Service Web Apps at any time.</span></span> 

1. <span data-ttu-id="b3906-145">В обозревателе решений щелкните правой кнопкой мыши проект и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="b3906-145">In Solution Explorer, right-click on your project and select **Publish**.</span></span>

2. <span data-ttu-id="b3906-146">В появившемся окне выберите **запустить**.</span><span class="sxs-lookup"><span data-stu-id="b3906-146">In the window that appears, select **Start**.</span></span> <span data-ttu-id="b3906-147">**Выберите целевой объект публикации** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b3906-147">The **Pick a publish target** dialog box appears.</span></span>

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. <span data-ttu-id="b3906-148">Выберите **Создать профиль**.</span><span class="sxs-lookup"><span data-stu-id="b3906-148">Select **Create Profile**.</span></span> <span data-ttu-id="b3906-149">Появится диалоговое окно **Создание службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="b3906-149">The **Create App Service** dialog box appears.</span></span>

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   <span data-ttu-id="b3906-150">Примите значения по умолчанию, или ввести другие значения для имени приложения, группу ресурсов, размещения плана, подписки Azure и географическом регионе.</span><span class="sxs-lookup"><span data-stu-id="b3906-150">Accept the defaults, or enter different values for the application name, resource group, hosting plan, Azure subscription, and geographical region.</span></span> 

4. <span data-ttu-id="b3906-151">Выберите **создать базу данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="b3906-151">Select **Create a SQL database**.</span></span> <span data-ttu-id="b3906-152">**Настройка SQL Server** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b3906-152">The **Configure SQL Server** dialog box appears.</span></span> 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   <span data-ttu-id="b3906-153">Примите значения по умолчанию или ввести другие значения.</span><span class="sxs-lookup"><span data-stu-id="b3906-153">Accept the defaults or enter different values.</span></span> <span data-ttu-id="b3906-154">Введите **имя пользователя администратора** и **пароль администратора** новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="b3906-154">Enter an **Administrator Username** and **Administrator Password** for your new database.</span></span> <span data-ttu-id="b3906-155">Выберите **ОК** после завершения.</span><span class="sxs-lookup"><span data-stu-id="b3906-155">Select **OK** when you're done.</span></span> <span data-ttu-id="b3906-156">**Создать службу приложений** странице отобразится.</span><span class="sxs-lookup"><span data-stu-id="b3906-156">The **Create App Service** page reappears.</span></span>

5. <span data-ttu-id="b3906-157">Выберите **создать** для создания профиля.</span><span class="sxs-lookup"><span data-stu-id="b3906-157">Select **Create** to create your profile.</span></span> <span data-ttu-id="b3906-158">Сообщение отображается в правом нижнем углу, в том, что развертывание находится в процессе выполнения.</span><span class="sxs-lookup"><span data-stu-id="b3906-158">A message appears in the lower-right corner indicating that deployment is in progress.</span></span> <span data-ttu-id="b3906-159">Через некоторое короткое время **публикации** снова появляется окно.</span><span class="sxs-lookup"><span data-stu-id="b3906-159">After a short while, the **Publish** window reappears.</span></span>

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    <span data-ttu-id="b3906-160">Профиль, созданный для развертывания приложения теперь доступна.</span><span class="sxs-lookup"><span data-stu-id="b3906-160">The profile you created to deploy the app is now available.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="b3906-161">Вперед</span><span class="sxs-lookup"><span data-stu-id="b3906-161">Next</span></span>](part-2.md)
