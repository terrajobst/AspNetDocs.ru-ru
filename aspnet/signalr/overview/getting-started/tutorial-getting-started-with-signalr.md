---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: Учебник. чат в режиме реального времени с SignalR 2 | Документация Майкрософт
author: bradygaster
description: В этом учебнике содержатся сведения об использовании SignalR для создания приложения разговора в режиме реального времени. Вы добавляете SignalR в пустое веб-приложение ASP.NET.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431568"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="c7e0d-104">Учебник. чат в режиме реального времени с SignalR 2</span><span class="sxs-lookup"><span data-stu-id="c7e0d-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="c7e0d-105">В этом руководстве показано, как использовать SignalR для создания приложения разговора в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="c7e0d-106">Вы добавляете SignalR в пустое веб-приложение ASP.NET и создаете HTML-страницу для отправки и вывода сообщений.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="c7e0d-107">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="c7e0d-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7e0d-108">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="c7e0d-108">Set up the project</span></span>
> * <span data-ttu-id="c7e0d-109">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="c7e0d-109">Run the sample</span></span>
> * <span data-ttu-id="c7e0d-110">Анализ кода</span><span class="sxs-lookup"><span data-stu-id="c7e0d-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="c7e0d-111">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7e0d-111">Prerequisites</span></span>

* <span data-ttu-id="c7e0d-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) с рабочей нагрузкой **ASP.NET и веб-разработка**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="c7e0d-113">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="c7e0d-113">Set up the Project</span></span>

<span data-ttu-id="c7e0d-114">В этом разделе показано, как использовать Visual Studio 2017 и SignalR 2 для создания пустого веб-приложения ASP.NET, добавления SignalR и создания приложения для разговора.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="c7e0d-115">В Visual Studio создайте веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Создание веб-сайта](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="c7e0d-117">В окне **New ASP.NET Project-сигналрчат** оставьте **пустым** выбранным и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="c7e0d-118">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="c7e0d-119">В окне **Добавить новый элемент — сигналрчат**выберите **установлено** > **Visual C#**  > **Web** > **SignalR** , а затем выберите **класс концентратора SignalR (v2)** .</span><span class="sxs-lookup"><span data-stu-id="c7e0d-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="c7e0d-120">Назовите класс *часуб* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="c7e0d-121">На этом шаге создается файл класса *ChatHub.CS* и добавляется набор файлов скриптов и ссылок на сборки, которые поддерживают SignalR в проекте.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="c7e0d-122">Замените код в новом файле класса *ChatHub.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c7e0d-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="c7e0d-123">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="c7e0d-124">В **меню Добавить новый элемент — сигналрчат** выберите **установлено** > **Visual C#**  > **Web** , а затем выберите **класс запуска OWIN**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="c7e0d-125">Присвойте классу имя *запуска* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="c7e0d-126">Замените код по умолчанию в классе *Startup* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c7e0d-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="c7e0d-127">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **HTML-страницу**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="c7e0d-128">Назовите новый *индекс* страницы и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="c7e0d-129">В **Обозреватель решений**щелкните правой кнопкой мыши СОЗДАНную HTML-страницу и выберите **задать в качестве начальной страницы**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="c7e0d-130">Замените код по умолчанию на странице HTML следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c7e0d-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="c7e0d-131">В **Обозреватель решений**разверните узел **сценарии**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="c7e0d-132">Библиотеки скриптов для jQuery и SignalR отображаются в проекте.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c7e0d-133">Диспетчер пакетов может установить более позднюю версию сценариев SignalR.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="c7e0d-134">Убедитесь, что ссылки на скрипты в блоке кода соответствуют версиям файлов скриптов в проекте.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="c7e0d-135">Создать скрипт для ссылок из исходного блока кода:</span><span class="sxs-lookup"><span data-stu-id="c7e0d-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="c7e0d-136">Если они не совпадают, обновите *HTML-* файл.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="c7e0d-137">В строке меню выберите **файл** > **сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="c7e0d-138">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="c7e0d-138">Run the Sample</span></span>

1. <span data-ttu-id="c7e0d-139">На панели инструментов включите **отладку скриптов** , а затем нажмите кнопку Воспроизведение, чтобы запустить пример в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![Введите имя пользователя](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="c7e0d-141">Когда откроется браузер, введите имя для удостоверения разговора.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="c7e0d-142">Скопируйте URL-адрес из браузера, откройте два других браузера и вставьте URL-адреса в адреса строки.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="c7e0d-143">В каждом браузере введите уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="c7e0d-144">Теперь добавьте комментарий и выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="c7e0d-145">Повторите эти действия в других браузерах.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="c7e0d-146">Комментарии отображаются в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7e0d-147">Это простое приложение разговора не поддерживает контекст обсуждения на сервере.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="c7e0d-148">Центр передает комментарии всем текущим пользователям.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="c7e0d-149">Пользователи, которые присоединяются к обсуждению позже, увидят сообщения, добавленные с момента присоединение.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="c7e0d-150">Узнайте, как работает приложение разговора в трех разных браузерах.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="c7e0d-151">При отправке сообщений Tom, Анандом и Ирина все браузеры обновляются в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="c7e0d-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![Все три браузера отображают один и тот же журнал разговора](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="c7e0d-153">В **Обозреватель решений**просмотрите узел **документы скрипта** для работающего приложения.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="c7e0d-154">Существует файл скрипта *с именем* Hubs, формируемый библиотекой SignalR во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="c7e0d-155">Этот файл управляет обменом данными между скриптом jQuery и кодом на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![автоматически сформированный скрипт концентраторов в узле "документы скриптов"](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="c7e0d-157">Изучение кода</span><span class="sxs-lookup"><span data-stu-id="c7e0d-157">Examine the Code</span></span>

<span data-ttu-id="c7e0d-158">Приложение Сигналрчат демонстрирует две основные задачи разработки SignalR.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="c7e0d-159">В нем показано, как создать центр.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-159">It shows you how to create a hub.</span></span> <span data-ttu-id="c7e0d-160">Сервер использует этот центр в качестве основного объекта координации.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="c7e0d-161">Концентратор использует библиотеку jQuery SignalR для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="c7e0d-162">Концентраторы SignalR в ChatHub.cs</span><span class="sxs-lookup"><span data-stu-id="c7e0d-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="c7e0d-163">В приведенном выше примере кода класс `ChatHub` является производным от класса `Microsoft.AspNet.SignalR.Hub`.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="c7e0d-164">Наследование от класса `Hub` является удобным способом создания приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="c7e0d-165">Вы можете создать открытые методы в классе Hub, а затем использовать эти методы, вызвав их из скриптов на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="c7e0d-166">В коде разговора клиенты вызывают метод `ChatHub.Send` для отправки нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="c7e0d-167">Затем концентратор отправляет сообщение всем клиентам, вызывая `Clients.All.broadcastMessage`.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="c7e0d-168">Метод `Send` демонстрирует несколько основных понятий:</span><span class="sxs-lookup"><span data-stu-id="c7e0d-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="c7e0d-169">Объявите открытые методы в концентраторе, чтобы клиенты могли их вызывать.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="c7e0d-170">Используйте динамическое свойство `Microsoft.AspNet.SignalR.Hub.Clients` для взаимодействия со всеми клиентами, подключенными к этому концентратору.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="c7e0d-171">Вызовите функцию клиента (например, функцию `broadcastMessage`) для обновления клиентов.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="c7e0d-172">SignalR и jQuery в index. HTML</span><span class="sxs-lookup"><span data-stu-id="c7e0d-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="c7e0d-173">На странице *index. HTML* в образце кода показано, как использовать библиотеку jQuery SignalR для взаимодействия с концентратором SignalR.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="c7e0d-174">Код содержит множество важных задач.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-174">The code carries out many important tasks.</span></span> <span data-ttu-id="c7e0d-175">Он объявляет прокси-сервер для ссылки на центр, объявляет функцию, которую сервер может вызывать для отправки содержимого клиентам, и начинает подключение для отправки сообщений в концентратор.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="c7e0d-176">В JavaScript ссылка на серверный класс и его члены должны быть camelCase.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="c7e0d-177">Пример кода ссылается C# на класс *часуб* в JavaScript как `chatHub`.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="c7e0d-178">В этом блоке кода вы создадите функцию обратного вызова в скрипте.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="c7e0d-179">Класс концентратора на сервере вызывает эту функцию для отправки обновлений содержимого на каждый клиент.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="c7e0d-180">Две строки, которые кодирует содержимое в формате HTML перед отображением, являются необязательными и показывают хороший способ предотвратить внедрение скрипта.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="c7e0d-181">Этот код открывает подключение к концентратору.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="c7e0d-182">Такой подход гарантирует, что код установит соединение перед выполнением обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="c7e0d-183">Код запускает соединение, а затем передает ему функцию для управления событием щелчка на кнопке **Send** на странице HTML.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="c7e0d-184">Получение кода</span><span class="sxs-lookup"><span data-stu-id="c7e0d-184">Get the code</span></span>

[<span data-ttu-id="c7e0d-185">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="c7e0d-185">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="c7e0d-186">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c7e0d-186">Additional resources</span></span>

<span data-ttu-id="c7e0d-187">Дополнительные сведения о SignalR см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="c7e0d-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="c7e0d-188">Проект SignalR</span><span class="sxs-lookup"><span data-stu-id="c7e0d-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="c7e0d-189">GitHub и примеры SignalR</span><span class="sxs-lookup"><span data-stu-id="c7e0d-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="c7e0d-190">Вики-сайт SignalR</span><span class="sxs-lookup"><span data-stu-id="c7e0d-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="c7e0d-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7e0d-191">Next steps</span></span>

<span data-ttu-id="c7e0d-192">В этом руководстве вы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7e0d-193">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="c7e0d-193">Set up the project</span></span>
> * <span data-ttu-id="c7e0d-194">Запустили пример</span><span class="sxs-lookup"><span data-stu-id="c7e0d-194">Ran the sample</span></span>
> * <span data-ttu-id="c7e0d-195">Анализ кода</span><span class="sxs-lookup"><span data-stu-id="c7e0d-195">Examined the code</span></span>

<span data-ttu-id="c7e0d-196">Перейдите к следующей статье, чтобы узнать, как использовать SignalR и MVC 5.</span><span class="sxs-lookup"><span data-stu-id="c7e0d-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e0d-197">SignalR 2 и MVC 5</span><span class="sxs-lookup"><span data-stu-id="c7e0d-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)