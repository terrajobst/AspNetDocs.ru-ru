---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Использование веб-API 2 с Entity Framework 6 | Документация Майкрософт
author: MikeWasson
description: В этом учебнике вы узнаете об основах создания веб-приложения с веб-API ASP.NET серверной частью. В руководстве используется Entity Framework 6 для макета данных...
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504840"
---
# <a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="b23e7-104">Использование веб-API 2 с Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="b23e7-104">Using Web API 2 with Entity Framework 6</span></span>

[<span data-ttu-id="b23e7-105">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="b23e7-105">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="b23e7-106">В этом учебнике приводятся основные сведения о создании веб-приложения с серверной частью веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b23e7-106">This tutorial teaches you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="b23e7-107">В руководстве используется Entity Framework 6 для уровня данных, а для приложения JavaScript на стороне клиента — выколачивание. js.</span><span class="sxs-lookup"><span data-stu-id="b23e7-107">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="b23e7-108">В этом руководстве также показано, как развернуть приложение в веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="b23e7-108">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b23e7-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="b23e7-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="b23e7-110">Веб-API 2,1</span><span class="sxs-lookup"><span data-stu-id="b23e7-110">Web API 2.1</span></span>
> - <span data-ttu-id="b23e7-111">Visual Studio 2017 (загрузить Visual Studio 2017 [здесь](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="b23e7-111">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="b23e7-112">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="b23e7-112">Entity Framework 6</span></span>
> - <span data-ttu-id="b23e7-113">.NET 4.7</span><span class="sxs-lookup"><span data-stu-id="b23e7-113">.NET 4.7</span></span>
> - <span data-ttu-id="b23e7-114">[Выколачивание. js](http://knockoutjs.com/) 3,1</span><span class="sxs-lookup"><span data-stu-id="b23e7-114">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>

<span data-ttu-id="b23e7-115">В этом руководстве используется веб-API ASP.NET 2 с Entity Framework 6 для создания веб-приложения, управляющего серверной базой данных.</span><span class="sxs-lookup"><span data-stu-id="b23e7-115">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="b23e7-116">Ниже приведен снимок экрана приложения, которое будет создано.</span><span class="sxs-lookup"><span data-stu-id="b23e7-116">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="b23e7-117">Приложение использует конструкцию одностраничного приложения (SPA).</span><span class="sxs-lookup"><span data-stu-id="b23e7-117">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="b23e7-118">"Одностраничное приложение" — это общий термин для веб-приложения, которое загружает одну HTML-страницу и обновляет страницу динамически, вместо того, чтобы загружать новые страницы.</span><span class="sxs-lookup"><span data-stu-id="b23e7-118">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="b23e7-119">После начальной загрузки страницы приложение взаимодействует с сервером через запросы AJAX.</span><span class="sxs-lookup"><span data-stu-id="b23e7-119">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="b23e7-120">Запросы AJAX возвращают данные JSON, которые приложение использует для обновления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b23e7-120">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="b23e7-121">AJAX не является новым, но на сегодняшний день существуют платформы JavaScript, упрощающие создание и поддержку большого сложного приложения SPA.</span><span class="sxs-lookup"><span data-stu-id="b23e7-121">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="b23e7-122">В этом руководстве используется [выколачивание. js](http://knockoutjs.com/), но можно использовать любую клиентскую платформу JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b23e7-122">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="b23e7-123">Ниже приведены основные стандартные блоки для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="b23e7-123">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="b23e7-124">ASP.NET MVC создает HTML-страницу.</span><span class="sxs-lookup"><span data-stu-id="b23e7-124">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="b23e7-125">Веб-API ASP.NET обрабатывает запросы AJAX и возвращает данные JSON.</span><span class="sxs-lookup"><span data-stu-id="b23e7-125">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="b23e7-126">Маскирование данных. js. Привязка HTML-элементов к данным JSON.</span><span class="sxs-lookup"><span data-stu-id="b23e7-126">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="b23e7-127">Entity Framework обращается к базе данных.</span><span class="sxs-lookup"><span data-stu-id="b23e7-127">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="b23e7-128">См. приложение, работающее в Azure</span><span class="sxs-lookup"><span data-stu-id="b23e7-128">See this app running on Azure</span></span>

<span data-ttu-id="b23e7-129">Вы хотите увидеть готовый сайт, работающий как активное веб-приложение?</span><span class="sxs-lookup"><span data-stu-id="b23e7-129">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="b23e7-130">Вы можете развернуть полную версию приложения в учетной записи Azure, нажав следующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="b23e7-130">You can deploy a complete version of the app to your Azure account by selecting the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="b23e7-131">Для развертывания этого решения в Azure необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b23e7-131">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="b23e7-132">Если у вас еще нет учетной записи, возможны следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="b23e7-132">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="b23e7-133">[Откройте учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) — вы получаете кредиты, которые можно использовать для пробного использования платных служб Azure, и даже после их использования вы можете удержать учетную запись и использовать бесплатные службы Azure.</span><span class="sxs-lookup"><span data-stu-id="b23e7-133">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="b23e7-134">[Активация преимуществ для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) . Ваша подписка MSDN предоставляет Вам кредиты каждый месяц, который можно использовать для платных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="b23e7-134">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="b23e7-135">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="b23e7-135">Create the project</span></span>

<span data-ttu-id="b23e7-136">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b23e7-136">Open Visual Studio.</span></span> <span data-ttu-id="b23e7-137">В меню **файл** выберите пункт **создать**, а затем выберите **проект**.</span><span class="sxs-lookup"><span data-stu-id="b23e7-137">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="b23e7-138">(Или выберите **создать проект** на начальной странице.)</span><span class="sxs-lookup"><span data-stu-id="b23e7-138">(Or select **New Project** on the Start page.)</span></span>

<span data-ttu-id="b23e7-139">В диалоговом окне **Новый проект** выберите **веб-сайт** в левой области и **веб-приложение ASP.NET (.NET Framework)** в средней области.</span><span class="sxs-lookup"><span data-stu-id="b23e7-139">In the **New Project** dialog, select **Web** in the left pane and **ASP.NET Web Application (.NET Framework)** in the middle pane.</span></span> <span data-ttu-id="b23e7-140">Присвойте проекту имя **буксервице** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b23e7-140">Name the project **BookService** and select **OK**.</span></span>

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

<span data-ttu-id="b23e7-141">В диалоговом окне **Новый проект ASP.NET** выберите шаблон **веб-API** .</span><span class="sxs-lookup"><span data-stu-id="b23e7-141">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

<span data-ttu-id="b23e7-142">Чтобы создать проект, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b23e7-142">Select **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="b23e7-143">Настройка параметров Azure (необязательно)</span><span class="sxs-lookup"><span data-stu-id="b23e7-143">Configure Azure settings (optional)</span></span>

<span data-ttu-id="b23e7-144">После создания проекта вы можете в любое время выбрать развертывание в веб-приложения службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="b23e7-144">After you create the project, you can choose to deploy to Azure App Service Web Apps at any time.</span></span> 

1. <span data-ttu-id="b23e7-145">В обозреватель решений щелкните правой кнопкой мыши проект и выберите **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b23e7-145">In Solution Explorer, right-click on your project and select **Publish**.</span></span>

2. <span data-ttu-id="b23e7-146">В появившемся окне выберите **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="b23e7-146">In the window that appears, select **Start**.</span></span> <span data-ttu-id="b23e7-147">Откроется диалоговое окно **Выбор целевого объекта публикации** .</span><span class="sxs-lookup"><span data-stu-id="b23e7-147">The **Pick a publish target** dialog box appears.</span></span>

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. <span data-ttu-id="b23e7-148">Выберите **Создать профиль**.</span><span class="sxs-lookup"><span data-stu-id="b23e7-148">Select **Create Profile**.</span></span> <span data-ttu-id="b23e7-149">Появится диалоговое окно **Создание службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="b23e7-149">The **Create App Service** dialog box appears.</span></span>

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   <span data-ttu-id="b23e7-150">Примите значения по умолчанию или введите разные значения для имени приложения, группы ресурсов, плана размещения, подписки Azure и географического региона.</span><span class="sxs-lookup"><span data-stu-id="b23e7-150">Accept the defaults, or enter different values for the application name, resource group, hosting plan, Azure subscription, and geographical region.</span></span> 

4. <span data-ttu-id="b23e7-151">Выберите **создать базу данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="b23e7-151">Select **Create a SQL database**.</span></span> <span data-ttu-id="b23e7-152">Откроется диалоговое окно **настройка SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="b23e7-152">The **Configure SQL Server** dialog box appears.</span></span> 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   <span data-ttu-id="b23e7-153">Примите значения по умолчанию или введите другое значение.</span><span class="sxs-lookup"><span data-stu-id="b23e7-153">Accept the defaults or enter different values.</span></span> <span data-ttu-id="b23e7-154">Введите **имя пользователя** и **пароль** администратора для новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="b23e7-154">Enter an **Administrator Username** and **Administrator Password** for your new database.</span></span> <span data-ttu-id="b23e7-155">Когда все будет готово, нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="b23e7-155">Select **OK** when you're done.</span></span> <span data-ttu-id="b23e7-156">Появится страница **Создание службы приложений** .</span><span class="sxs-lookup"><span data-stu-id="b23e7-156">The **Create App Service** page reappears.</span></span>

5. <span data-ttu-id="b23e7-157">Выберите **создать** , чтобы создать профиль.</span><span class="sxs-lookup"><span data-stu-id="b23e7-157">Select **Create** to create your profile.</span></span> <span data-ttu-id="b23e7-158">В правом нижнем углу появится сообщение, указывающее, что развертывание выполняется.</span><span class="sxs-lookup"><span data-stu-id="b23e7-158">A message appears in the lower-right corner indicating that deployment is in progress.</span></span> <span data-ttu-id="b23e7-159">Через некоторое время окно **публикации** появится снова.</span><span class="sxs-lookup"><span data-stu-id="b23e7-159">After a short while, the **Publish** window reappears.</span></span>

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    <span data-ttu-id="b23e7-160">Профиль, созданный для развертывания приложения, теперь доступен.</span><span class="sxs-lookup"><span data-stu-id="b23e7-160">The profile you created to deploy the app is now available.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="b23e7-161">Дальше</span><span class="sxs-lookup"><span data-stu-id="b23e7-161">Next</span></span>](part-2.md)
