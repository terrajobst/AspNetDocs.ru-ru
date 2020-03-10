---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: Учебник. чат в режиме реального времени с SignalR 2 и MVC 5 | Документация Майкрософт
author: bradygaster
description: В этом руководстве показано, как использовать ASP.NET SignalR 2 для создания приложения разговора в режиме реального времени. Вы добавляете SignalR в приложение MVC 5.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431622"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a><span data-ttu-id="8d026-104">Учебник. чат в режиме реального времени с SignalR 2 и MVC 5</span><span class="sxs-lookup"><span data-stu-id="8d026-104">Tutorial: Real-time chat with SignalR 2 and MVC 5</span></span>

<span data-ttu-id="8d026-105">В этом руководстве показано, как использовать ASP.NET SignalR 2 для создания приложения разговора в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="8d026-105">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="8d026-106">Вы добавляете SignalR в приложение MVC 5 и создаете представление чата для отправки и отображения сообщений.</span><span class="sxs-lookup"><span data-stu-id="8d026-106">You add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>

<span data-ttu-id="8d026-107">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="8d026-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d026-108">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="8d026-108">Set up the project</span></span>
> * <span data-ttu-id="8d026-109">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="8d026-109">Run the sample</span></span>
> * <span data-ttu-id="8d026-110">Анализ кода</span><span class="sxs-lookup"><span data-stu-id="8d026-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="8d026-111">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d026-111">Prerequisites</span></span>

* <span data-ttu-id="8d026-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) с рабочей нагрузкой **ASP.NET и веб-разработка**.</span><span class="sxs-lookup"><span data-stu-id="8d026-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="8d026-113">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="8d026-113">Set up the Project</span></span>

<span data-ttu-id="8d026-114">В этом разделе показано, как использовать Visual Studio 2017 и SignalR 2 для создания пустого приложения ASP.NET MVC 5, добавления библиотеки SignalR и создания приложения для разговора.</span><span class="sxs-lookup"><span data-stu-id="8d026-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="8d026-115">В Visual Studio создайте приложение C# ASP.NET, которое предназначено для .NET Framework 4,5, назовите его сигналрчат и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="8d026-115">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![Создание веб-сайта](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. <span data-ttu-id="8d026-117">В **новом ASP.NET веб-приложение — сигналрмвкчат**выберите **MVC** и щелкните **изменить проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="8d026-117">In **New ASP.NET Web Application - SignalRMvcChat**, select **MVC** and then select **Change Authentication**.</span></span>

1. <span data-ttu-id="8d026-118">В окне **Изменение проверки подлинности**выберите **без проверки подлинности** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8d026-118">In **Change Authentication**, select **No Authentication** and click **OK**.</span></span>

    ![Выберите без проверки подлинности](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. <span data-ttu-id="8d026-120">В **новом ASP.NET веб-приложении — сигналрмвкчат**нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8d026-120">In **New ASP.NET Web Application - SignalRMvcChat**, select **OK**.</span></span>

1. <span data-ttu-id="8d026-121">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="8d026-121">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="8d026-122">В окне **Добавить новый элемент — сигналрчат**выберите **установлено** > **Visual C#**  > **Web** > **SignalR** , а затем выберите **класс концентратора SignalR (v2)** .</span><span class="sxs-lookup"><span data-stu-id="8d026-122">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="8d026-123">Назовите класс *часуб* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="8d026-123">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="8d026-124">На этом шаге создается файл класса *ChatHub.CS* и добавляется набор файлов скриптов и ссылок на сборки, которые поддерживают SignalR в проекте.</span><span class="sxs-lookup"><span data-stu-id="8d026-124">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="8d026-125">Замените код в новом файле класса *ChatHub.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="8d026-125">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. <span data-ttu-id="8d026-126">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **класс**.</span><span class="sxs-lookup"><span data-stu-id="8d026-126">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="8d026-127">Присвойте новому классу имя *Startup* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="8d026-127">Name the new class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="8d026-128">Замените код в файле класса *Startup.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="8d026-128">Replace the code in the *Startup.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. <span data-ttu-id="8d026-129">В **Обозреватель решений**выберите **контроллеры** > **HomeController.CS**.</span><span class="sxs-lookup"><span data-stu-id="8d026-129">In **Solution Explorer**, select **Controllers** > **HomeController.cs**.</span></span>

1. <span data-ttu-id="8d026-130">Добавьте этот метод в *HomeController.CS*.</span><span class="sxs-lookup"><span data-stu-id="8d026-130">Add this method to the *HomeController.cs*.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    <span data-ttu-id="8d026-131">Этот метод возвращает представление **чата** , которое вы создадите на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="8d026-131">This method returns the **Chat** view that you create in a later step.</span></span>

1. <span data-ttu-id="8d026-132">В **Обозреватель решений**щелкните правой кнопкой мыши элемент **представления** > **Главная**и выберите **Добавить** >  **представление**.</span><span class="sxs-lookup"><span data-stu-id="8d026-132">In **Solution Explorer**, right-click **Views** > **Home**, and select **Add** >  **View**.</span></span>

1. <span data-ttu-id="8d026-133">В поле **Добавить представление**назовите новое представление **разговора** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d026-133">In **Add View**, name the new view **Chat** and select **Add**.</span></span>

1. <span data-ttu-id="8d026-134">Замените содержимое файла **Chat. cshtml** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="8d026-134">Replace the contents of **Chat.cshtml** with this code:</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. <span data-ttu-id="8d026-135">В **Обозреватель решений**разверните узел **сценарии**.</span><span class="sxs-lookup"><span data-stu-id="8d026-135">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="8d026-136">Библиотеки скриптов для jQuery и SignalR отображаются в проекте.</span><span class="sxs-lookup"><span data-stu-id="8d026-136">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8d026-137">Диспетчер пакетов может установить более позднюю версию сценариев SignalR.</span><span class="sxs-lookup"><span data-stu-id="8d026-137">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="8d026-138">Убедитесь, что ссылки на скрипты в блоке кода соответствуют версиям файлов скриптов в проекте.</span><span class="sxs-lookup"><span data-stu-id="8d026-138">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="8d026-139">Создать скрипт для ссылок из исходного блока кода:</span><span class="sxs-lookup"><span data-stu-id="8d026-139">Script references from the original code block:</span></span>

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. <span data-ttu-id="8d026-140">Если они не совпадают, обновите *CSHTML* .</span><span class="sxs-lookup"><span data-stu-id="8d026-140">If they don't match, update the *.cshtml* file.</span></span>

1. <span data-ttu-id="8d026-141">В строке меню выберите **файл** > **сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="8d026-141">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="8d026-142">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="8d026-142">Run the Sample</span></span>

1. <span data-ttu-id="8d026-143">На панели инструментов включите **отладку скриптов** , а затем нажмите кнопку Воспроизведение, чтобы запустить пример в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="8d026-143">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![Введите имя пользователя](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. <span data-ttu-id="8d026-145">Когда откроется браузер, введите имя для удостоверения разговора.</span><span class="sxs-lookup"><span data-stu-id="8d026-145">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="8d026-146">Скопируйте URL-адрес из браузера, откройте два других браузера и вставьте URL-адреса в адреса строки.</span><span class="sxs-lookup"><span data-stu-id="8d026-146">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="8d026-147">В каждом браузере введите уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="8d026-147">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="8d026-148">Теперь добавьте комментарий и выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="8d026-148">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="8d026-149">Повторите эти действия в других браузерах.</span><span class="sxs-lookup"><span data-stu-id="8d026-149">Repeat that in the other browsers.</span></span> <span data-ttu-id="8d026-150">Комментарии отображаются в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="8d026-150">The comments appear in real time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d026-151">Это простое приложение разговора не поддерживает контекст обсуждения на сервере.</span><span class="sxs-lookup"><span data-stu-id="8d026-151">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="8d026-152">Центр передает комментарии всем текущим пользователям.</span><span class="sxs-lookup"><span data-stu-id="8d026-152">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="8d026-153">Пользователи, которые присоединяются к обсуждению позже, увидят сообщения, добавленные с момента присоединение.</span><span class="sxs-lookup"><span data-stu-id="8d026-153">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="8d026-154">Узнайте, как работает приложение разговора в трех разных браузерах.</span><span class="sxs-lookup"><span data-stu-id="8d026-154">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="8d026-155">При отправке сообщений Tom, Анандом и Ирина все браузеры обновляются в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="8d026-155">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![Все три браузера отображают один и тот же журнал разговора](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. <span data-ttu-id="8d026-157">В **Обозреватель решений**просмотрите узел **документы скрипта** для работающего приложения.</span><span class="sxs-lookup"><span data-stu-id="8d026-157">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="8d026-158">Существует файл скрипта *с именем* Hubs, формируемый библиотекой SignalR во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="8d026-158">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="8d026-159">Этот файл управляет обменом данными между скриптом jQuery и кодом на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="8d026-159">This file manages the communication between jQuery script and server-side code.</span></span>

    ![автоматически сформированный скрипт концентраторов в узле "документы скриптов"](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="8d026-161">Изучение кода</span><span class="sxs-lookup"><span data-stu-id="8d026-161">Examine the Code</span></span>

<span data-ttu-id="8d026-162">Приложение разговора SignalR демонстрирует две основные задачи разработки SignalR.</span><span class="sxs-lookup"><span data-stu-id="8d026-162">The SignalR chat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="8d026-163">В нем показано, как создать центр.</span><span class="sxs-lookup"><span data-stu-id="8d026-163">It shows you how to create a hub.</span></span> <span data-ttu-id="8d026-164">Сервер использует этот центр в качестве основного объекта координации.</span><span class="sxs-lookup"><span data-stu-id="8d026-164">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="8d026-165">Концентратор использует библиотеку jQuery SignalR для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="8d026-165">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="8d026-166">Концентраторы SignalR в ChatHub.cs</span><span class="sxs-lookup"><span data-stu-id="8d026-166">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="8d026-167">В примере кода класс `ChatHub` является производным от класса `Microsoft.AspNet.SignalR.Hub`.</span><span class="sxs-lookup"><span data-stu-id="8d026-167">In the code sample, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="8d026-168">Наследование от класса `Hub` является удобным способом создания приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="8d026-168">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="8d026-169">Вы можете создавать открытые методы в классе Hub, а затем обращаться к этим методам, вызывая их из скриптов на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="8d026-169">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="8d026-170">В коде разговора клиенты вызывают метод `ChatHub.Send` для отправки нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="8d026-170">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="8d026-171">Концентратор, в свою очередь, отправляет сообщение всем клиентам, вызывая `Clients.All.addNewMessageToPage`.</span><span class="sxs-lookup"><span data-stu-id="8d026-171">The hub in turn sends the message to all clients by calling `Clients.All.addNewMessageToPage`.</span></span>

<span data-ttu-id="8d026-172">Метод `Send` демонстрирует несколько основных понятий:</span><span class="sxs-lookup"><span data-stu-id="8d026-172">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="8d026-173">Объявите открытые методы в концентраторе, чтобы клиенты могли их вызывать.</span><span class="sxs-lookup"><span data-stu-id="8d026-173">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="8d026-174">Используйте динамическое свойство `Microsoft.AspNet.SignalR.Hub.Clients` для взаимодействия со всеми клиентами, подключенными к этому концентратору.</span><span class="sxs-lookup"><span data-stu-id="8d026-174">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="8d026-175">Вызовите функцию клиента (например, функцию `addNewMessageToPage`) для обновления клиентов.</span><span class="sxs-lookup"><span data-stu-id="8d026-175">Call a function on the client (like the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a><span data-ttu-id="8d026-176">SignalR и jQuery Chat. cshtml</span><span class="sxs-lookup"><span data-stu-id="8d026-176">SignalR and jQuery Chat.cshtml</span></span>

<span data-ttu-id="8d026-177">В файле представления *Chat. cshtml* в образце кода показано, как использовать библиотеку jQuery SignalR для взаимодействия с концентратором SignalR.</span><span class="sxs-lookup"><span data-stu-id="8d026-177">The *Chat.cshtml* view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span>  <span data-ttu-id="8d026-178">Код содержит множество важных задач.</span><span class="sxs-lookup"><span data-stu-id="8d026-178">The code carries out many important tasks.</span></span> <span data-ttu-id="8d026-179">Он создает ссылку на автоматически сформированный прокси-сервер для концентратора, объявляет функцию, которую сервер может вызывать для отправки содержимого клиентам, и запускает подключение для отправки сообщений в концентратор.</span><span class="sxs-lookup"><span data-stu-id="8d026-179">It creates a reference to the autogenerated proxy for the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="8d026-180">В JavaScript ссылка на серверный класс и его члены находится в camelCase.</span><span class="sxs-lookup"><span data-stu-id="8d026-180">In JavaScript, the reference to the server class and its members is in camelCase.</span></span> <span data-ttu-id="8d026-181">Образец кода ссылается на класс C# `ChatHub` в JavaScript как `chatHub`.</span><span class="sxs-lookup"><span data-stu-id="8d026-181">The code sample references the C# `ChatHub` class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="8d026-182">В этом блоке кода вы создадите функцию обратного вызова в скрипте.</span><span class="sxs-lookup"><span data-stu-id="8d026-182">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="8d026-183">Класс концентратора на сервере вызывает эту функцию для отправки обновлений содержимого на каждый клиент.</span><span class="sxs-lookup"><span data-stu-id="8d026-183">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="8d026-184">Необязательный вызов функции `htmlEncode` показывает способ кодирования содержимого сообщения в формате HTML перед его отображением на странице.</span><span class="sxs-lookup"><span data-stu-id="8d026-184">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page.</span></span> <span data-ttu-id="8d026-185">Это способ предотвращения внедрения скриптов.</span><span class="sxs-lookup"><span data-stu-id="8d026-185">It's a way to prevent script injection.</span></span>

<span data-ttu-id="8d026-186">Этот код открывает подключение к концентратору.</span><span class="sxs-lookup"><span data-stu-id="8d026-186">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> <span data-ttu-id="8d026-187">Такой подход гарантирует установку соединения перед выполнением обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="8d026-187">This approach ensures that you establish a connection before the event handler executes.</span></span>

<span data-ttu-id="8d026-188">Код запускает соединение, а затем передает ему функцию для управления событием щелчка на кнопке **Send** на странице разговора.</span><span class="sxs-lookup"><span data-stu-id="8d026-188">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="8d026-189">Получение кода</span><span class="sxs-lookup"><span data-stu-id="8d026-189">Get the code</span></span>

[<span data-ttu-id="8d026-190">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="8d026-190">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a><span data-ttu-id="8d026-191">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8d026-191">Additional resources</span></span>

<span data-ttu-id="8d026-192">Дополнительные сведения о SignalR см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="8d026-192">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="8d026-193">Проект SignalR</span><span class="sxs-lookup"><span data-stu-id="8d026-193">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="8d026-194">GitHub и примеры SignalR</span><span class="sxs-lookup"><span data-stu-id="8d026-194">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="8d026-195">Вики-сайт SignalR</span><span class="sxs-lookup"><span data-stu-id="8d026-195">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="8d026-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d026-196">Next steps</span></span>

<span data-ttu-id="8d026-197">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="8d026-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d026-198">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="8d026-198">Set up the project</span></span>
> * <span data-ttu-id="8d026-199">Запустили пример</span><span class="sxs-lookup"><span data-stu-id="8d026-199">Ran the sample</span></span>
> * <span data-ttu-id="8d026-200">Анализ кода</span><span class="sxs-lookup"><span data-stu-id="8d026-200">Examined the code</span></span>

<span data-ttu-id="8d026-201">Перейдите к следующей статье, чтобы узнать, как создать веб-приложение, использующее ASP.NET SignalR 2 для обеспечения высокой функциональности обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="8d026-201">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8d026-202">Веб-приложение с высокой частотой обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8d026-202">Web app with high-frequency messaging</span></span>](tutorial-high-frequency-realtime-with-signalr.md)