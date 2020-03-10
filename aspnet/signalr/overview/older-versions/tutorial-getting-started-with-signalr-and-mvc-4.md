---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: Учебник. начало работы с SignalR 1. x и MVC 4 | Документация Майкрософт
author: bradygaster
description: Используйте ASP.NET SignalR и ASP.NET MVC 4 для создания приложения разговора в режиме реального времени.
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468072"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="f7c83-103">Учебник. начало работы с SignalR 1. x и MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7c83-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>

<span data-ttu-id="f7c83-104">[Патрик Флетчера](https://github.com/pfletcher), [Тим тибкен](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="f7c83-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="f7c83-105">В этом руководстве показано, как использовать SignalR ASP.NET для создания приложения разговора в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="f7c83-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="f7c83-106">Вы добавите SignalR в приложение MVC 4 и создадите представление чата для отправки и отображения сообщений.</span><span class="sxs-lookup"><span data-stu-id="f7c83-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="f7c83-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="f7c83-107">Overview</span></span>

<span data-ttu-id="f7c83-108">В этом учебнике рассказывается о разработке веб-приложений в режиме реального времени с помощью ASP.NET SignalR и ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f7c83-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="f7c83-109">В этом руководстве используется тот же код приложения разговора, что и в [Начало работыном руководстве](tutorial-getting-started-with-signalr.md), но показано, как добавить его в приложение MVC 4, основанное на шаблоне Интернета.</span><span class="sxs-lookup"><span data-stu-id="f7c83-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="f7c83-110">В этом разделе вы узнаете о следующих задачах разработки SignalR:</span><span class="sxs-lookup"><span data-stu-id="f7c83-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="f7c83-111">Добавление библиотеки SignalR в приложение MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f7c83-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="f7c83-112">Создание класса концентратора для отправки содержимого клиентам.</span><span class="sxs-lookup"><span data-stu-id="f7c83-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="f7c83-113">Использование библиотеки jQuery SignalR на веб-странице для отправки сообщений и вывода обновлений из центра.</span><span class="sxs-lookup"><span data-stu-id="f7c83-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="f7c83-114">На следующем снимке экрана показано завершенное приложение разговора, выполняемое в браузере.</span><span class="sxs-lookup"><span data-stu-id="f7c83-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![Экземпляры чата](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="f7c83-116">Священ</span><span class="sxs-lookup"><span data-stu-id="f7c83-116">Sections:</span></span>

- [<span data-ttu-id="f7c83-117">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="f7c83-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="f7c83-118">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="f7c83-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="f7c83-119">Изучение кода</span><span class="sxs-lookup"><span data-stu-id="f7c83-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="f7c83-120">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="f7c83-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="f7c83-121">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="f7c83-121">Set up the Project</span></span>

<span data-ttu-id="f7c83-122">Предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="f7c83-122">Prerequisites:</span></span>

- <span data-ttu-id="f7c83-123">Visual Studio 2010 с пакетом обновления 1 (SP1), Visual Studio 2012 или Visual Studio 2012 Express.</span><span class="sxs-lookup"><span data-stu-id="f7c83-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="f7c83-124">Если у вас нет Visual Studio, см. [ASP.net downloads](https://www.asp.net/downloads) , чтобы получить бесплатное средство visual Studio 2012 Express Development Tool.</span><span class="sxs-lookup"><span data-stu-id="f7c83-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="f7c83-125">Для Visual Studio 2010 установите [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span><span class="sxs-lookup"><span data-stu-id="f7c83-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="f7c83-126">В этом разделе показано, как создать приложение ASP.NET MVC 4, добавить библиотеку SignalR и создать приложение Chat.</span><span class="sxs-lookup"><span data-stu-id="f7c83-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="f7c83-127">В Visual Studio создайте приложение ASP.NET MVC 4, назовите его Сигналрчат и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="f7c83-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f7c83-128">В VS 2010 выберите **.NET Framework 4** в элементе управления "раскрывающийся список версий платформы".</span><span class="sxs-lookup"><span data-stu-id="f7c83-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="f7c83-129">Код SignalR выполняется в .NET Framework версиях 4 и 4,5.</span><span class="sxs-lookup"><span data-stu-id="f7c83-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![Создание веб-сайта MVC](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. <span data-ttu-id="f7c83-131">Выберите шаблон Интернет-приложение, снимите флажок **создать проект модульного теста**и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="f7c83-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

         ![Создание веб-сайта MVC](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. <span data-ttu-id="f7c83-133">Откройте **меню сервис > диспетчер пакетов NuGet > консоль диспетчера пакетов** и выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f7c83-133">Open the **Tools > NuGet Package Manager > Package Manager Console** and run the following command.</span></span> <span data-ttu-id="f7c83-134">На этом шаге в проект добавляется набор файлов скриптов и ссылок на сборки, которые позволяют использовать функции SignalR.</span><span class="sxs-lookup"><span data-stu-id="f7c83-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. <span data-ttu-id="f7c83-135">В **Обозреватель решений** разверните папку скрипты.</span><span class="sxs-lookup"><span data-stu-id="f7c83-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="f7c83-136">Обратите внимание, что библиотеки скриптов для SignalR были добавлены в проект.</span><span class="sxs-lookup"><span data-stu-id="f7c83-136">Note that script libraries for SignalR have been added to the project.</span></span>

         ![Ссылки на библиотеки](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. <span data-ttu-id="f7c83-138">В **Обозреватель решений**щелкните правой кнопкой мыши проект, выберите **Добавить | Создать папку**и добавить новую папку с именем " **концентраторы**".</span><span class="sxs-lookup"><span data-stu-id="f7c83-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
      6. <span data-ttu-id="f7c83-139">Щелкните правой кнопкой мыши папку **концентраторы** и выберите команду **Добавить |** И создайте новый C# класс с именем **ChatHub.CS**.</span><span class="sxs-lookup"><span data-stu-id="f7c83-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="f7c83-140">Этот класс будет использоваться в качестве концентратора сервера SignalR, который отправляет сообщения всем клиентам.</span><span class="sxs-lookup"><span data-stu-id="f7c83-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="f7c83-141">Если вы используете Visual Studio 2012 и установили [обновление ASP.NET and Web Tools 2012,2](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), можно использовать новый шаблон элемента SignalR, чтобы создать класс Hub.</span><span class="sxs-lookup"><span data-stu-id="f7c83-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="f7c83-142">Для этого щелкните правой кнопкой мыши папку **концентраторы** и выберите **Добавить | Новый элемент**, выберите **класс концентратора SignalR (v1)** и назовите класс **ChatHub.CS**.</span><span class="sxs-lookup"><span data-stu-id="f7c83-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>

1. <span data-ttu-id="f7c83-143">Замените код в классе **часуб** следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="f7c83-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="f7c83-144">Откройте файл **Global. asax** для проекта и добавьте вызов метода `RouteTable.Routes.MapHubs();` в качестве первой строки кода в методе `Application_Start`.</span><span class="sxs-lookup"><span data-stu-id="f7c83-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="f7c83-145">Этот код регистрирует маршрут по умолчанию для концентраторов SignalR и должен вызываться перед регистрацией других маршрутов.</span><span class="sxs-lookup"><span data-stu-id="f7c83-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="f7c83-146">Завершенный метод `Application_Start` выглядит, как в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f7c83-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="f7c83-147">Измените класс `HomeController`, найденный в **Controllers/HomeController. CS** , и добавьте в класс следующий метод.</span><span class="sxs-lookup"><span data-stu-id="f7c83-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="f7c83-148">Этот метод возвращает представление **разговора** , которое будет создано на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="f7c83-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="f7c83-149">Щелкните правой кнопкой мыши только что созданный метод `Chat` и выберите команду **Добавить представление** , чтобы создать новый файл представления.</span><span class="sxs-lookup"><span data-stu-id="f7c83-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="f7c83-150">В диалоговом окне **Добавление представления** убедитесь, что флажок установлен для **использования макета или главной страницы** (снимите другие флажки), а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="f7c83-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![Добавление представления](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="f7c83-152">Измените новый файл представления с именем **Chat. cshtml**.</span><span class="sxs-lookup"><span data-stu-id="f7c83-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="f7c83-153">После тега &lt;H2&gt; вставьте следующий раздел &lt;div&gt; и `@section scripts` блок кода на страницу.</span><span class="sxs-lookup"><span data-stu-id="f7c83-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="f7c83-154">Этот скрипт позволяет странице отсылать сообщения в чате и отображать сообщения с сервера.</span><span class="sxs-lookup"><span data-stu-id="f7c83-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="f7c83-155">Полный код для представления разговора представлен в следующем блоке кода.</span><span class="sxs-lookup"><span data-stu-id="f7c83-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f7c83-156">При добавлении в проект Visual Studio SignalR и других библиотек сценариев диспетчер пакетов может устанавливать более новые версии сценариев, чем показано в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="f7c83-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="f7c83-157">Убедитесь, что ссылки на скрипты в коде соответствуют версиям библиотек скриптов, установленных в проекте.</span><span class="sxs-lookup"><span data-stu-id="f7c83-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="f7c83-158">**Сохраните все** для проекта.</span><span class="sxs-lookup"><span data-stu-id="f7c83-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="f7c83-159">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="f7c83-159">Run the Sample</span></span>

1. <span data-ttu-id="f7c83-160">Нажмите клавишу F5, чтобы запустить проект в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="f7c83-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="f7c83-161">В адресной строке браузера добавьте **/Хоме/чат** в URL-адрес страницы по умолчанию для проекта.</span><span class="sxs-lookup"><span data-stu-id="f7c83-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="f7c83-162">Страница разговора загружается в экземпляр браузера и запрашивает имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="f7c83-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![Введите имя пользователя](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="f7c83-164">Введите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="f7c83-164">Enter a user name.</span></span>
4. <span data-ttu-id="f7c83-165">Скопируйте URL-адрес из строки адреса браузера и используйте его, чтобы открыть два других экземпляра браузера.</span><span class="sxs-lookup"><span data-stu-id="f7c83-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="f7c83-166">В каждом экземпляре браузера введите уникальное имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="f7c83-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="f7c83-167">В каждом экземпляре браузера добавьте комментарий и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="f7c83-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="f7c83-168">Комментарии должны отображаться во всех экземплярах браузера.</span><span class="sxs-lookup"><span data-stu-id="f7c83-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f7c83-169">Это простое приложение разговора не поддерживает контекст обсуждения на сервере.</span><span class="sxs-lookup"><span data-stu-id="f7c83-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="f7c83-170">Центр передает комментарии всем текущим пользователям.</span><span class="sxs-lookup"><span data-stu-id="f7c83-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="f7c83-171">Пользователи, которые присоединяются к обсуждению позже, увидят сообщения, добавленные с момента присоединение.</span><span class="sxs-lookup"><span data-stu-id="f7c83-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="f7c83-172">На следующем снимке экрана показано приложение разговора, выполняемое в браузере.</span><span class="sxs-lookup"><span data-stu-id="f7c83-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![Браузеры чатов](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="f7c83-174">В **Обозреватель решений**просмотрите узел **документы скрипта** для работающего приложения.</span><span class="sxs-lookup"><span data-stu-id="f7c83-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="f7c83-175">Этот узел отображается в режиме отладки, если в качестве браузера используется Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f7c83-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="f7c83-176">Существует файл скрипта **с именем** Hubs, динамически формируемый библиотекой SignalR во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="f7c83-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="f7c83-177">Этот файл управляет обменом данными между скриптом jQuery и кодом на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="f7c83-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="f7c83-178">Если используется браузер, отличный от Internet Explorer, можно также получить доступ к файлу динамических **концентраторов** , перейдя к нему напрямую, например http://mywebsite/signalr/hubs.</span><span class="sxs-lookup"><span data-stu-id="f7c83-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![Созданный скрипт концентратора](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="f7c83-180">Изучение кода</span><span class="sxs-lookup"><span data-stu-id="f7c83-180">Examine the Code</span></span>

<span data-ttu-id="f7c83-181">Приложение разговора SignalR демонстрирует две основные задачи разработки SignalR: создание концентратора в качестве основного объекта координации на сервере и использование библиотеки jQuery SignalR для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="f7c83-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="f7c83-182">Концентраторы SignalR</span><span class="sxs-lookup"><span data-stu-id="f7c83-182">SignalR Hubs</span></span>

<span data-ttu-id="f7c83-183">В примере кода класс **часуб** является производным от класса **Microsoft. AspNet. SignalR. Hub** .</span><span class="sxs-lookup"><span data-stu-id="f7c83-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="f7c83-184">Наследование от класса **Hub** — это удобный способ создания приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="f7c83-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="f7c83-185">Вы можете создавать открытые методы в классе Hub, а затем обращаться к этим методам, вызывая их из скриптов jQuery на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="f7c83-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="f7c83-186">В коде разговора клиенты вызывают метод **часуб. Send** для отправки нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="f7c83-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="f7c83-187">Концентратор, в свою очередь, отправляет сообщение всем клиентам, вызывая **Clients. ALL. аддневмессажетопаже**.</span><span class="sxs-lookup"><span data-stu-id="f7c83-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="f7c83-188">Метод **Send** демонстрирует несколько основных понятий:</span><span class="sxs-lookup"><span data-stu-id="f7c83-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="f7c83-189">Объявите открытые методы в концентраторе, чтобы клиенты могли их вызывать.</span><span class="sxs-lookup"><span data-stu-id="f7c83-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="f7c83-190">Используйте свойство **Microsoft. AspNet. SignalR. Hub. Clients** для доступа ко всем клиентам, подключенным к этому концентратору.</span><span class="sxs-lookup"><span data-stu-id="f7c83-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="f7c83-191">Вызовите функцию jQuery на клиенте (например, функцию `addNewMessageToPage`) для обновления клиентов.</span><span class="sxs-lookup"><span data-stu-id="f7c83-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="f7c83-192">SignalR и jQuery</span><span class="sxs-lookup"><span data-stu-id="f7c83-192">SignalR and jQuery</span></span>

<span data-ttu-id="f7c83-193">В файле представления **Chat. cshtml** в образце кода показано, как использовать библиотеку jQuery SignalR для взаимодействия с концентратором SignalR.</span><span class="sxs-lookup"><span data-stu-id="f7c83-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="f7c83-194">Основными задачами в коде является создание ссылки на автоматически созданный прокси-сервер для концентратора, объявление функции, которую сервер может вызывать для отправки содержимого клиентам, и запуск соединения для отправки сообщений в концентратор.</span><span class="sxs-lookup"><span data-stu-id="f7c83-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="f7c83-195">Следующий код объявляет прокси-сервер для концентратора.</span><span class="sxs-lookup"><span data-stu-id="f7c83-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="f7c83-196">В jQuery ссылка на серверный класс и его члены находятся в неоднородном регистре.</span><span class="sxs-lookup"><span data-stu-id="f7c83-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="f7c83-197">Пример кода ссылается C# на класс **часуб** в jQuery как **часуб**.</span><span class="sxs-lookup"><span data-stu-id="f7c83-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="f7c83-198">Если вы хотите сослаться на класс `ChatHub` в jQuery с использованием обычного регистра Pascal, как C#в этом случае, измените файл класса ChatHub.cs.</span><span class="sxs-lookup"><span data-stu-id="f7c83-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="f7c83-199">Добавьте оператор `using` для ссылки на пространство имен `Microsoft.AspNet.SignalR.Hubs`.</span><span class="sxs-lookup"><span data-stu-id="f7c83-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="f7c83-200">Затем добавьте атрибут `HubName` в класс `ChatHub`, например `[HubName("ChatHub")]`.</span><span class="sxs-lookup"><span data-stu-id="f7c83-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="f7c83-201">Наконец, обновите ссылку jQuery на класс `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="f7c83-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>

<span data-ttu-id="f7c83-202">В следующем коде показано, как создать функцию обратного вызова в скрипте.</span><span class="sxs-lookup"><span data-stu-id="f7c83-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="f7c83-203">Класс концентратора на сервере вызывает эту функцию для отправки обновлений содержимого на каждый клиент.</span><span class="sxs-lookup"><span data-stu-id="f7c83-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="f7c83-204">Необязательный вызов функции `htmlEncode` показывает способ кодирования содержимого сообщения в формате HTML перед его отображением на странице, как способ предотвращения внедрения скрипта.</span><span class="sxs-lookup"><span data-stu-id="f7c83-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="f7c83-205">В следующем коде показано, как открыть подключение к концентратору.</span><span class="sxs-lookup"><span data-stu-id="f7c83-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="f7c83-206">Код запускает соединение, а затем передает ему функцию для управления событием щелчка на кнопке **Send** на странице разговора.</span><span class="sxs-lookup"><span data-stu-id="f7c83-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="f7c83-207">Такой подход гарантирует, что соединение будет установлено до выполнения обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="f7c83-207">This approach ensures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="f7c83-208">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f7c83-208">Next Steps</span></span>

<span data-ttu-id="f7c83-209">Вы узнали, что SignalR — это платформа для создания веб-приложений в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="f7c83-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="f7c83-210">Вы также узнали о нескольких задачах разработки SignalR: как добавить SignalR в приложение ASP.NET, как создать класс Hub, а также как отправлять и получать сообщения от концентратора.</span><span class="sxs-lookup"><span data-stu-id="f7c83-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="f7c83-211">Чтобы узнать о более сложных концепциях разработки SignalR, посетите следующие сайты с исходным кодом и ресурсами SignalR:</span><span class="sxs-lookup"><span data-stu-id="f7c83-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="f7c83-212">Проект SignalR</span><span class="sxs-lookup"><span data-stu-id="f7c83-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="f7c83-213">GitHub и примеры SignalR</span><span class="sxs-lookup"><span data-stu-id="f7c83-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="f7c83-214">Вики-сайт SignalR</span><span class="sxs-lookup"><span data-stu-id="f7c83-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
