---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: Учебник. Чат в реальном времени с SignalR 2 | Документация Майкрософт
author: bradygaster
description: В этом учебнике содержатся сведения об использовании SignalR для создания приложения разговора в режиме реального времени. Добавление пустой веб-приложения ASP.NET SignalR.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: ecc235454d4b95ce660a4373387f44720826b076
ms.sourcegitcommit: 2d53ed9e4c8b19d3526cbc689bfa8394c9449cec
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905648"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="eb0f4-104">Учебник. Чат в реальном времени с SignalR 2</span><span class="sxs-lookup"><span data-stu-id="eb0f4-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="eb0f4-105">Этом руководстве показано, как использовать SignalR для создания приложения разговора в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="eb0f4-106">Добавьте пустой веб-приложения ASP.NET SignalR и создайте страницу HTML для отправки и отображения сообщений.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="eb0f4-107">В этом учебнике рассмотрены следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb0f4-108">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="eb0f4-108">Set up the project</span></span>
> * <span data-ttu-id="eb0f4-109">Запуск образца</span><span class="sxs-lookup"><span data-stu-id="eb0f4-109">Run the sample</span></span>
> * <span data-ttu-id="eb0f4-110">Изучите код</span><span class="sxs-lookup"><span data-stu-id="eb0f4-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="eb0f4-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="eb0f4-111">Prerequisites</span></span>

* <span data-ttu-id="eb0f4-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) с **ASP.NET и веб-разработка** рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="eb0f4-113">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="eb0f4-113">Set up the Project</span></span>

<span data-ttu-id="eb0f4-114">В этом разделе показано, как использовать Visual Studio 2017 и SignalR 2 для создания пустой веб-приложения ASP.NET, добавьте SignalR и создание приложения чата.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="eb0f4-115">В Visual Studio создайте веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Создание веб-](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="eb0f4-117">В **новый проект ASP.NET — SignalRChat** окне оставьте **пустой** затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="eb0f4-118">В **обозревателе решений**, щелкните правой кнопкой мыши проект и выберите **добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="eb0f4-119">В **Добавление нового элемента — SignalRChat**выберите **установленные** > **Visual C#**   >  **Web**  >  **SignalR** , а затем выберите **класс концентратора SignalR (v2)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="eb0f4-120">Назовите класс *ChatHub* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="eb0f4-121">На этом шаге создается *ChatHub.cs* файла и добавляет набор файлов сценариев и ссылки на сборки, которые поддерживают SignalR в проект.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="eb0f4-122">Замените код в новом *ChatHub.cs* файл класса следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="eb0f4-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="eb0f4-123">В **обозревателе решений**, щелкните правой кнопкой мыши проект и выберите **добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="eb0f4-124">В **Добавление нового элемента — SignalRChat** выберите **установленные** > **Visual C#**   >  **Web** и затем Выберите **класс запуска OWIN**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="eb0f4-125">Назовите класс *запуска* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="eb0f4-126">Замените код по умолчанию в *запуска* класса следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="eb0f4-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="eb0f4-127">В **обозревателе решений**, щелкните правой кнопкой мыши проект и выберите **добавить** > **HTML-страницу**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="eb0f4-128">Имя новой страницы *индекс* и выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="eb0f4-129">В **обозревателе решений**, щелкните правой кнопкой мыши созданную HTML-страницы и выберите **задать в качестве начальной страницы**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="eb0f4-130">Замените код по умолчанию в HTML-страницы этот код:</span><span class="sxs-lookup"><span data-stu-id="eb0f4-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="eb0f4-131">В **обозревателе решений**, разверните **сценариев**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="eb0f4-132">Библиотеки скрипта для jQuery и SignalR, отображаются в проект.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="eb0f4-133">Диспетчер пакетов может установить более позднюю версию сценариев SignalR.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="eb0f4-134">Убедитесь, что ссылки на скрипты в блоке кода соответствуют версиям файлов сценариев в проекте.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="eb0f4-135">Ссылки на скрипты из исходного блока кода:</span><span class="sxs-lookup"><span data-stu-id="eb0f4-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="eb0f4-136">Если они не совпадают, обновите *.html* файл.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="eb0f4-137">В строке меню выберите **файл** > **сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="eb0f4-138">Запуск образца</span><span class="sxs-lookup"><span data-stu-id="eb0f4-138">Run the Sample</span></span>

1. <span data-ttu-id="eb0f4-139">На панели инструментов, включите **отладки скриптов** и затем нажмите кнопку воспроизведения, чтобы запустить пример в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![Введите имя пользователя](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="eb0f4-141">Когда откроется браузер, введите имя для вашего удостоверения чата.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="eb0f4-142">Скопируйте URL-адрес из браузера, откройте два других браузеров и вставьте URL-адреса в панели адрес.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="eb0f4-143">В каждом браузере введите уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="eb0f4-144">Теперь добавьте комментарий и выберите **отправки**.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="eb0f4-145">Повторите, в других браузерах.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="eb0f4-146">Комментарии отображаются в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb0f4-147">Это приложение на простом чате не ведет контекста обсуждения на сервере.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="eb0f4-148">Концентратор осуществляет широковещательную передачу комментарии для всех текущих пользователей.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="eb0f4-149">Пользователи, беседа позже будет видеть сообщения добавлены с момента их присоединения к.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="eb0f4-150">См. в разделе, запуск приложения чата в трех различных браузерах.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="eb0f4-151">Когда Tom Ананд и Сьюзан отправляют сообщения, все браузеры обновление в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="eb0f4-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![Все три браузеры отображают же журнала разговора](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="eb0f4-153">В **обозревателе решений**, проверять **документы скриптов** узел для запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="eb0f4-154">Файл скрипта с именем *концентраторов* , библиотека SignalR создает во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="eb0f4-155">Этот файл управляет обменом данных между jQuery-сценарий и код на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![автоматически созданное концентраторов сценария в узел документов скриптов](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="eb0f4-157">Изучите код</span><span class="sxs-lookup"><span data-stu-id="eb0f4-157">Examine the Code</span></span>

<span data-ttu-id="eb0f4-158">Приложение SignalRChat демонстрирует две основные задачи разработки SignalR.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="eb0f4-159">Оно показано, как создать концентратор.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-159">It shows you how to create a hub.</span></span> <span data-ttu-id="eb0f4-160">Сервер использует этот концентратор как объект основного координации.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="eb0f4-161">Концентратор использует библиотеку jQuery SignalR для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="eb0f4-162">Концентраторы SignalR в ChatHub.cs</span><span class="sxs-lookup"><span data-stu-id="eb0f4-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="eb0f4-163">В приведенном выше примере кода `ChatHub` класс является производным от `Microsoft.AspNet.SignalR.Hub` класса.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="eb0f4-164">Наследование от `Hub` класс является эффективным методом для построения приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="eb0f4-165">Можно создавать открытые методы в классе концентратора и затем использовать их, вызвав их из сценариев на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="eb0f4-166">В коде чата, клиенты вызывают `ChatHub.Send` метод для отправки нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="eb0f4-167">Концентратор затем отправляет сообщение всем клиентам, вызвав `Clients.All.broadcastMessage`.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="eb0f4-168">`Send` Метод демонстрирует несколько вещей понятия:</span><span class="sxs-lookup"><span data-stu-id="eb0f4-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="eb0f4-169">Объявления открытых методов концентратора, таким образом, клиенты могут вызывать их.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="eb0f4-170">Используйте `Microsoft.AspNet.SignalR.Hub.Clients` динамических свойств для взаимодействия со всеми клиентами, подключенных к этому концентратору.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="eb0f4-171">Вызов функции на стороне клиента (например `broadcastMessage` функции) для обновления клиентов.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="eb0f4-172">SignalR и jQuery в index.html</span><span class="sxs-lookup"><span data-stu-id="eb0f4-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="eb0f4-173">*Index.html* страницы в примере кода показано, как использовать библиотеку jQuery SignalR для взаимодействия с центром SignalR.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="eb0f4-174">Код выполняет ряд важных задач.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-174">The code carries out many important tasks.</span></span> <span data-ttu-id="eb0f4-175">Он объявляется прокси-сервер для ссылки на концентратор, объявляет функцию, сервер может обратиться к содержимому Push-уведомлений для клиентов, что он запускает подключение для отправки сообщений в концентратор.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="eb0f4-176">В JavaScript должно быть camelCase ссылку на класс сервера и его членах.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="eb0f4-177">Ссылки на код примера C# *ChatHub* класс в JavaScript в виде `chatHub`.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="eb0f4-178">В этот блок кода как создать функцию обратного вызова в скрипте.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="eb0f4-179">Класс концентратора на сервере вызывает эту функцию для отправки обновлений содержимого для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="eb0f4-180">Две строки, HTML-кодирование содержимого перед его отображением являются необязательными и Показать хороший способ предотвратить внедрение скрипта.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="eb0f4-181">Этот код открывает соединение с концентратором.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="eb0f4-182">Такой подход гарантирует, что код устанавливает соединение перед выполнением обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="eb0f4-183">Код запускает подключение, а затем передает его функции, чтобы обрабатывать событие щелчка на **отправки** кнопку в HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="eb0f4-184">Получение кода</span><span class="sxs-lookup"><span data-stu-id="eb0f4-184">Get the code</span></span>

[<span data-ttu-id="eb0f4-185">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="eb0f4-185">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="eb0f4-186">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="eb0f4-186">Additional resources</span></span>

<span data-ttu-id="eb0f4-187">Дополнительные сведения о SignalR см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="eb0f4-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="eb0f4-188">Проект SignalR</span><span class="sxs-lookup"><span data-stu-id="eb0f4-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="eb0f4-189">SignalR Github и примерами</span><span class="sxs-lookup"><span data-stu-id="eb0f4-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="eb0f4-190">Вики-сайте SignalR</span><span class="sxs-lookup"><span data-stu-id="eb0f4-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="eb0f4-191">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="eb0f4-191">Next steps</span></span>

<span data-ttu-id="eb0f4-192">В этом руководстве вы:</span><span class="sxs-lookup"><span data-stu-id="eb0f4-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb0f4-193">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="eb0f4-193">Set up the project</span></span>
> * <span data-ttu-id="eb0f4-194">Запустили пример</span><span class="sxs-lookup"><span data-stu-id="eb0f4-194">Ran the sample</span></span>
> * <span data-ttu-id="eb0f4-195">Проверить код</span><span class="sxs-lookup"><span data-stu-id="eb0f4-195">Examined the code</span></span>

<span data-ttu-id="eb0f4-196">Перейдите к следующей статье, чтобы сведения об использовании SignalR и MVC 5.</span><span class="sxs-lookup"><span data-stu-id="eb0f4-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="eb0f4-197">SignalR 2 и MVC 5</span><span class="sxs-lookup"><span data-stu-id="eb0f4-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)