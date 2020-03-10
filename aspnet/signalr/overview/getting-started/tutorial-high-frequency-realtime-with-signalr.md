---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: Учебник. Создание приложения с высокой частотой в реальном времени с помощью SignalR 2 | Документация Майкрософт
author: bradygaster
description: В этом руководстве показано, как создать веб-приложение, которое использует SignalR ASP.NET для предоставления высокоскоростной функции обмена сообщениями.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450120"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a><span data-ttu-id="9ddbe-103">Учебник. Создание приложения с высокой частотой в реальном времени с помощью SignalR 2</span><span class="sxs-lookup"><span data-stu-id="9ddbe-103">Tutorial: Create high-frequency real-time app with SignalR 2</span></span>

<span data-ttu-id="9ddbe-104">В этом руководстве показано, как создать веб-приложение, использующее ASP.NET SignalR 2 для обеспечения высокой функциональности обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="9ddbe-105">В этом случае "обмен сообщениями с высокой частотой" означает, что сервер отправляет обновления с фиксированной скоростью.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-105">In this case, "high-frequency messaging" means the server sends updates at a fixed rate.</span></span> <span data-ttu-id="9ddbe-106">Вы отправляете до 10 сообщений за секунду.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-106">You send up to 10 messages a second.</span></span>

<span data-ttu-id="9ddbe-107">Создаваемое приложение отображает фигуру, которую пользователи могут перетаскивать.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-107">The application you create displays a shape that users can drag.</span></span> <span data-ttu-id="9ddbe-108">Сервер обновляет расположение фигуры во всех подключенных браузерах в соответствии с положением перетаскивания фигуры с помощью времени обновления.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-108">The server updates the position of the shape in all connected browsers to match the position of the dragged shape using timed updates.</span></span>

<span data-ttu-id="9ddbe-109">Основные понятия, представленные в этом руководстве, представляют собой приложения в режиме реального времени и другие приложения моделирования.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-109">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>

<span data-ttu-id="9ddbe-110">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ddbe-111">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="9ddbe-111">Set up the project</span></span>
> * <span data-ttu-id="9ddbe-112">Создание базового приложения</span><span class="sxs-lookup"><span data-stu-id="9ddbe-112">Create the base application</span></span>
> * <span data-ttu-id="9ddbe-113">Сопоставлять с концентратором при запуске приложения</span><span class="sxs-lookup"><span data-stu-id="9ddbe-113">Map to the hub when app starts</span></span>
> * <span data-ttu-id="9ddbe-114">Добавление клиента</span><span class="sxs-lookup"><span data-stu-id="9ddbe-114">Add the client</span></span>
> * <span data-ttu-id="9ddbe-115">Запустите приложение</span><span class="sxs-lookup"><span data-stu-id="9ddbe-115">Run the app</span></span>
> * <span data-ttu-id="9ddbe-116">Добавление цикла клиента</span><span class="sxs-lookup"><span data-stu-id="9ddbe-116">Add the client loop</span></span>
> * <span data-ttu-id="9ddbe-117">Добавление цикла сервера</span><span class="sxs-lookup"><span data-stu-id="9ddbe-117">Add the server loop</span></span>
> * <span data-ttu-id="9ddbe-118">Добавить плавную анимацию</span><span class="sxs-lookup"><span data-stu-id="9ddbe-118">Add smooth animation</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="9ddbe-119">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9ddbe-119">Prerequisites</span></span>

* <span data-ttu-id="9ddbe-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) с рабочей нагрузкой **ASP.NET и веб-разработка**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="9ddbe-121">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="9ddbe-121">Set up the project</span></span>

<span data-ttu-id="9ddbe-122">В этом разделе вы создадите проект в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-122">In this section, you create the project in Visual Studio 2017.</span></span>

<span data-ttu-id="9ddbe-123">В этом разделе показано, как с помощью Visual Studio 2017 создать пустое веб-приложение ASP.NET и добавить SignalR и библиотеку jQuery. UI.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-123">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application and add the SignalR and jQuery.UI libraries.</span></span>

1. <span data-ttu-id="9ddbe-124">В Visual Studio создайте веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-124">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Создание веб-сайта](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. <span data-ttu-id="9ddbe-126">В окне **Создание веб-приложения ASP.NET — мовешапедемо** оставьте **пустым** выбранным и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-126">In the **New ASP.NET Web Application - MoveShapeDemo** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="9ddbe-127">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-127">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="9ddbe-128">В окне **Добавить новый элемент — мовешапедемо**выберите **установлено** > **Visual C#**  > **Web** > **SignalR** , а затем выберите **класс концентратора SignalR (v2)** .</span><span class="sxs-lookup"><span data-stu-id="9ddbe-128">In **Add New Item - MoveShapeDemo**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="9ddbe-129">Назовите класс *мовешапехуб* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-129">Name the class *MoveShapeHub* and add it to the project.</span></span>

    <span data-ttu-id="9ddbe-130">На этом шаге создается файл класса *MoveShapeHub.CS* .</span><span class="sxs-lookup"><span data-stu-id="9ddbe-130">This step creates the *MoveShapeHub.cs* class file.</span></span> <span data-ttu-id="9ddbe-131">Одновременно он добавляет набор файлов скриптов и ссылок на сборки, которые поддерживают SignalR для проекта.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-131">Simultaneously, it adds  a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="9ddbe-132">Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-132">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="9ddbe-133">В **консоли диспетчера пакетов**выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-133">In **Package Manager Console**, run this command:</span></span>

    ```console
    Install-Package jQuery.UI.Combined
    ```

    <span data-ttu-id="9ddbe-134">Команда устанавливает библиотеку пользовательского интерфейса jQuery.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-134">The command installs the jQuery UI library.</span></span> <span data-ttu-id="9ddbe-135">Он используется для анимации фигуры.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-135">You use it to animate the shape.</span></span>

1. <span data-ttu-id="9ddbe-136">В **Обозреватель решений**разверните узел скрипты.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-136">In **Solution Explorer**, expand the Scripts node.</span></span>

    ![Ссылки на библиотеку скриптов](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    <span data-ttu-id="9ddbe-138">Библиотеки скриптов для jQuery, Жкуерюи и SignalR отображаются в проекте.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-138">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

## <a name="create-the-base-application"></a><span data-ttu-id="9ddbe-139">Создание базового приложения</span><span class="sxs-lookup"><span data-stu-id="9ddbe-139">Create the base application</span></span>

<span data-ttu-id="9ddbe-140">В этом разделе вы создадите приложение браузера.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-140">In this section, you create a browser application.</span></span> <span data-ttu-id="9ddbe-141">Приложение отправляет расположение фигуры на сервер при каждом событии перемещения мыши.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-141">The app sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="9ddbe-142">Сервер передает эти сведения всем остальным подключенным клиентам в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-142">The server broadcasts this information to all other connected clients in real time.</span></span> <span data-ttu-id="9ddbe-143">Дополнительные сведения об этом приложении см. в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-143">You learn more about this application in later sections.</span></span>

1. <span data-ttu-id="9ddbe-144">Откройте файл *MoveShapeHub.CS* .</span><span class="sxs-lookup"><span data-stu-id="9ddbe-144">Open the *MoveShapeHub.cs* file.</span></span>

1. <span data-ttu-id="9ddbe-145">Замените код в файле *MoveShapeHub.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-145">Replace the code in the *MoveShapeHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="9ddbe-146">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-146">Save the file.</span></span>

<span data-ttu-id="9ddbe-147">Класс `MoveShapeHub` является реализацией концентратора SignalR.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-147">The `MoveShapeHub` class is an implementation of a SignalR hub.</span></span> <span data-ttu-id="9ddbe-148">Как и в [Начало работы с](tutorial-getting-started-with-signalr.md) руководством по SignalR, центр имеет метод, который клиенты напрямую вызывают.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-148">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients call directly.</span></span> <span data-ttu-id="9ddbe-149">В этом случае клиент отправляет объект с новыми координатами X и Y фигуры на сервер.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-149">In this case, the client sends an object with the new X and Y coordinates of the shape to the server.</span></span> <span data-ttu-id="9ddbe-150">Эти координаты посылаются на все остальные подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-150">Those coordinates get broadcasted to all other connected clients.</span></span> <span data-ttu-id="9ddbe-151">SignalR автоматически сериализует этот объект с помощью JSON.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-151">SignalR automatically serializes this object using JSON.</span></span>

<span data-ttu-id="9ddbe-152">Приложение отправляет клиенту объект `ShapeModel`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-152">The app sends the `ShapeModel` object to the client.</span></span> <span data-ttu-id="9ddbe-153">Он содержит элементы для хранения расположения фигуры.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-153">It has members to store the position of the shape.</span></span> <span data-ttu-id="9ddbe-154">Версия объекта на сервере также имеет член для отслеживания хранения данных клиента.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-154">The version of the object on the server also has a member to track which client's data is being stored.</span></span> <span data-ttu-id="9ddbe-155">Этот объект не позволяет серверу отправлять данные клиента обратно.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-155">This object prevents the server from sending a client's data back to itself.</span></span> <span data-ttu-id="9ddbe-156">Этот элемент использует атрибут `JsonIgnore`, чтобы приложение не было выполнять сериализацию данных и отправлять их обратно клиенту.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-156">This member uses the `JsonIgnore` attribute to keep the application from serializing the data and sending it back to the client.</span></span>

## <a name="map-to-the-hub-when-app-starts"></a><span data-ttu-id="9ddbe-157">Сопоставлять с концентратором при запуске приложения</span><span class="sxs-lookup"><span data-stu-id="9ddbe-157">Map to the hub when app starts</span></span>

<span data-ttu-id="9ddbe-158">Затем настройте сопоставление с концентратором при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-158">Next, you set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="9ddbe-159">В SignalR 2 при добавлении класса Startup OWIN создается сопоставление.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-159">In SignalR 2, adding an OWIN startup class creates the mapping.</span></span>

1. <span data-ttu-id="9ddbe-160">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-160">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="9ddbe-161">В **меню Добавить новый элемент — мовешапедемо** выберите **установлено** > **Visual C#**  > **Web** , а затем выберите **класс запуска OWIN**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-161">In **Add New Item - MoveShapeDemo** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="9ddbe-162">Назовите класс *Startup* и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-162">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="9ddbe-163">Замените код по умолчанию в файле *Startup.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-163">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<span data-ttu-id="9ddbe-164">Класс запуска OWIN вызывает `MapSignalR`, когда приложение выполняет метод `Configuration`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-164">The OWIN startup class calls `MapSignalR` when the app executes the `Configuration` method.</span></span> <span data-ttu-id="9ddbe-165">Приложение добавляет класс в процесс запуска OWIN с помощью атрибута сборки `OwinStartup`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-165">The app adds the class to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

## <a name="add-the-client"></a><span data-ttu-id="9ddbe-166">Добавление клиента</span><span class="sxs-lookup"><span data-stu-id="9ddbe-166">Add the client</span></span>

<span data-ttu-id="9ddbe-167">Добавьте HTML-страницу для клиента.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-167">Add the HTML page for the client.</span></span>

1. <span data-ttu-id="9ddbe-168">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **HTML-страницу**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-168">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="9ddbe-169">Присвойте странице имя **по умолчанию** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-169">Name the page **Default** and select **OK**.</span></span>

1. <span data-ttu-id="9ddbe-170">В **Обозреватель решений**щелкните правой кнопкой мыши *Default. HTML* и выберите **задать в качестве начальной страницы**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-170">In **Solution Explorer**, right-click *Default.html* and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="9ddbe-171">Замените код по умолчанию в файле *Default. HTML* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-171">Replace the default code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. <span data-ttu-id="9ddbe-172">В **Обозреватель решений**разверните узел **сценарии**.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-172">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="9ddbe-173">Библиотеки скриптов для jQuery и SignalR отображаются в проекте.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-173">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9ddbe-174">Диспетчер пакетов устанавливает более позднюю версию сценариев SignalR.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-174">The package manager installs a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="9ddbe-175">Обновите ссылки на скрипт в блоке кода, чтобы они соответствовали версиям файлов скриптов в проекте.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-175">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

<span data-ttu-id="9ddbe-176">Этот код HTML и JavaScript создает красный `div` с именем `shape`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-176">This HTML and JavaScript code creates a red `div` called `shape`.</span></span> <span data-ttu-id="9ddbe-177">Он обеспечивает поведение перетаскивания фигуры с помощью библиотеки jQuery и использует событие `drag` для отправки расположения фигуры на сервер.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-177">It enables the shape's dragging behavior using the jQuery library and uses the `drag` event to send the shape's position to the server.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="9ddbe-178">Запустите приложение</span><span class="sxs-lookup"><span data-stu-id="9ddbe-178">Run the app</span></span>

<span data-ttu-id="9ddbe-179">Вы можете запустить приложение, чтобы се'е его работу.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-179">You can run the app to se\`e it work.</span></span> <span data-ttu-id="9ddbe-180">При перетаскивании формы вокруг окна браузера фигура также перемещается в другие браузеры.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-180">When you drag the shape around a browser window, the shape moves in the other browsers too.</span></span>

1. <span data-ttu-id="9ddbe-181">На панели инструментов включите **отладку скриптов** , а затем нажмите кнопку Воспроизведение, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-181">In the toolbar, turn on **Script Debugging** and then select the play button to run the application in Debug mode.</span></span>

    ![Снимок экрана: Включение режима отладки пользователем и выбор воспроизведения.](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    <span data-ttu-id="9ddbe-183">Открывается окно браузера с красной фигурой в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-183">A browser window opens with the red shape in the upper-right corner.</span></span>

1. <span data-ttu-id="9ddbe-184">Скопируйте URL-адрес страницы.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-184">Copy the page's URL.</span></span>

1. <span data-ttu-id="9ddbe-185">Откройте другой браузер и вставьте URL-адрес в адресную строку.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-185">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="9ddbe-186">Перетащите фигуру в одно из окон браузера.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-186">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="9ddbe-187">Форма в другом окне браузера выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-187">The shape in the other browser window follows.</span></span>

<span data-ttu-id="9ddbe-188">Хотя приложение работает с помощью этого метода, это не рекомендуемая модель программирования.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-188">While the application functions using this method, it's not a recommended programming model.</span></span> <span data-ttu-id="9ddbe-189">Нет верхнего предела числа отправляемых сообщений.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-189">There's no upper limit to the number of messages getting sent.</span></span> <span data-ttu-id="9ddbe-190">В результате клиенты и сервер перегружаются с помощью сообщений и снижает производительность.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-190">As a result, the clients and server get overwhelmed with messages and performance degrades.</span></span> <span data-ttu-id="9ddbe-191">Кроме того, приложение отображает несвязанную анимацию на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-191">Also, the app displays a disjointed animation on the client.</span></span> <span data-ttu-id="9ddbe-192">Эта жерки анимация происходит потому, что фигура мгновенно перемещается каждым методом.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-192">This jerky animation happens because the shape moves instantly by each method.</span></span> <span data-ttu-id="9ddbe-193">Это лучше, если фигура плавно перемещается в каждое новое место.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-193">It's better if the shape moves smoothly to each new location.</span></span> <span data-ttu-id="9ddbe-194">Далее вы узнаете, как устранить эти проблемы.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-194">Next, you learn how to fix those issues.</span></span>

## <a name="add-the-client-loop"></a><span data-ttu-id="9ddbe-195">Добавление цикла клиента</span><span class="sxs-lookup"><span data-stu-id="9ddbe-195">Add the client loop</span></span>

<span data-ttu-id="9ddbe-196">При отправке расположения фигуры при каждом событии перемещения мыши создается ненужный объем сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-196">Sending the location of the shape on every mouse move event creates an unnecessary amount of network traffic.</span></span> <span data-ttu-id="9ddbe-197">Приложение должно регулировать сообщения от клиента.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-197">The app needs to throttle the messages from the client.</span></span>

<span data-ttu-id="9ddbe-198">Используйте функцию `setInterval` JavaScript, чтобы настроить цикл, который отправляет новые сведения о положении на сервер с фиксированной частотой.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-198">Use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="9ddbe-199">Этот цикл является базовым представлением "цикла игры".</span><span class="sxs-lookup"><span data-stu-id="9ddbe-199">This loop is a basic representation of a "game loop."</span></span> <span data-ttu-id="9ddbe-200">Это многократно именуемая функция, которая управляет всеми функциями игры.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-200">It's a repeatedly called function that drives all the functionality of a game.</span></span>

1. <span data-ttu-id="9ddbe-201">Замените код клиента в файле *Default. HTML* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-201">Replace the client code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > <span data-ttu-id="9ddbe-202">Необходимо снова заменить ссылки на скрипт.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-202">You have to replace the script references again.</span></span> <span data-ttu-id="9ddbe-203">Они должны соответствовать версиям скриптов в проекте.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-203">They must match the versions of the scripts in the project.</span></span>

    <span data-ttu-id="9ddbe-204">Этот новый код добавляет функцию `updateServerModel`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-204">This new code adds the `updateServerModel` function.</span></span> <span data-ttu-id="9ddbe-205">Он вызывается с фиксированной частотой.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-205">It gets called on a fixed frequency.</span></span> <span data-ttu-id="9ddbe-206">Функция отправляет данные о положении на сервер, когда флаг `moved` указывает на наличие новых данных о расположении для отправки.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-206">The function sends the position data to the server whenever the `moved` flag indicates that there's new position data to send.</span></span>

1. <span data-ttu-id="9ddbe-207">Нажмите кнопку Воспроизведение, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-207">Select the play button to start the application</span></span>

1. <span data-ttu-id="9ddbe-208">Скопируйте URL-адрес страницы.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-208">Copy the page's URL.</span></span>

1. <span data-ttu-id="9ddbe-209">Откройте другой браузер и вставьте URL-адрес в адресную строку.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-209">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="9ddbe-210">Перетащите фигуру в одно из окон браузера.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-210">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="9ddbe-211">Форма в другом окне браузера выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-211">The shape in the other browser window follows.</span></span>

<span data-ttu-id="9ddbe-212">Так как приложение регулирует количество сообщений, отправляемых на сервер, анимация не будет отображаться как гладкие.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-212">Since the app throttles the number of messages that get sent to the server, the animation won't appear as smooth did at first.</span></span>

## <a name="add-the-server-loop"></a><span data-ttu-id="9ddbe-213">Добавление цикла сервера</span><span class="sxs-lookup"><span data-stu-id="9ddbe-213">Add the server loop</span></span>

<span data-ttu-id="9ddbe-214">В текущем приложении сообщения, отправленные с сервера клиенту, отправляются так часто, как они получены.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-214">In the current application, messages sent from the server to the client go out as often as they're received.</span></span> <span data-ttu-id="9ddbe-215">Этот сетевой трафик представляет аналогичную проблему, как видно на клиенте.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-215">This network traffic presents a similar problem as we see on the client.</span></span>

<span data-ttu-id="9ddbe-216">Приложение может отсылать сообщения чаще, чем требуется.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-216">The app can send messages more often than they're needed.</span></span> <span data-ttu-id="9ddbe-217">Соединение может передаваться в результате.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-217">The connection can become flooded as a result.</span></span> <span data-ttu-id="9ddbe-218">В этом разделе описывается, как обновить сервер, чтобы добавить таймер, который регулирует скорость исходящих сообщений.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-218">This section describes how to update the server to add a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="9ddbe-219">Замените содержимое `MoveShapeHub.cs` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-219">Replace the contents of `MoveShapeHub.cs` with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. <span data-ttu-id="9ddbe-220">Нажмите кнопку Воспроизведение, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-220">Select the play button to start the application.</span></span>

1. <span data-ttu-id="9ddbe-221">Скопируйте URL-адрес страницы.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-221">Copy the page's URL.</span></span>

1. <span data-ttu-id="9ddbe-222">Откройте другой браузер и вставьте URL-адрес в адресную строку.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-222">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="9ddbe-223">Перетащите фигуру в одно из окон браузера.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-223">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="9ddbe-224">Этот код расширяет возможности клиента, добавляя класс `Broadcaster`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-224">This code expands the client to add the `Broadcaster` class.</span></span> <span data-ttu-id="9ddbe-225">Новый класс регулирует исходящие сообщения, используя класс `Timer` из .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-225">The new class throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

<span data-ttu-id="9ddbe-226">Хорошо понять, что концентратор является транзитным.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-226">It's good to learn that the hub itself is transitory.</span></span> <span data-ttu-id="9ddbe-227">Он создается каждый раз, когда это необходимо.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-227">It's created every time it's needed.</span></span> <span data-ttu-id="9ddbe-228">Поэтому приложение создает `Broadcaster` как одноэлементный.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-228">So the app creates the `Broadcaster` as a singleton.</span></span> <span data-ttu-id="9ddbe-229">Она использует отложенную инициализацию, чтобы отложить создание `Broadcaster`до ее необходимости.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-229">It uses lazy initialization to defer the `Broadcaster`'s creation until it's needed.</span></span> <span data-ttu-id="9ddbe-230">Это гарантирует, что приложение создает первый экземпляр концентратора полностью перед запуском таймера.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-230">That guarantees that the app creates the first hub instance completely before starting the timer.</span></span>

<span data-ttu-id="9ddbe-231">После этого вызов функции `UpdateShape` клиентов перемещается из метода `UpdateModel` концентратора.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-231">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method.</span></span> <span data-ttu-id="9ddbe-232">Он больше не вызывается немедленно при получении приложением входящих сообщений.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-232">It's no longer called immediately whenever the app receives incoming messages.</span></span> <span data-ttu-id="9ddbe-233">Вместо этого приложение отправляет сообщения клиентам с частотой 25 вызовов в секунду.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-233">Instead, the app sends the messages to the clients at a rate of 25 calls per second.</span></span> <span data-ttu-id="9ddbe-234">Процесс управляется таймером `_broadcastLoop` в классе `Broadcaster`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-234">The process is  managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

<span data-ttu-id="9ddbe-235">Наконец, вместо непосредственного вызова метода клиента из концентратора `Broadcaster` классу необходимо получить ссылку на текущий центр `_hubContext`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-235">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to get a reference to the currently operating `_hubContext` hub.</span></span> <span data-ttu-id="9ddbe-236">Он получает ссылку с `GlobalHost`.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-236">It gets the reference with the `GlobalHost`.</span></span>

## <a name="add-smooth-animation"></a><span data-ttu-id="9ddbe-237">Добавить плавную анимацию</span><span class="sxs-lookup"><span data-stu-id="9ddbe-237">Add smooth animation</span></span>

<span data-ttu-id="9ddbe-238">Приложение почти готово, но мы можем сделать еще одно улучшение.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-238">The application is almost finished, but we could make one more improvement.</span></span> <span data-ttu-id="9ddbe-239">Приложение перемещает форму на клиенте в ответ на сообщения сервера.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-239">The app moves the shape on the client in response to server messages.</span></span> <span data-ttu-id="9ddbe-240">Вместо задания позиции фигуры в новом расположении, заданном сервером, используйте функцию `animate` библиотеки пользовательского интерфейса JQuery.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-240">Instead of setting the position of the shape to the new location given by the server, use the JQuery UI library's `animate` function.</span></span> <span data-ttu-id="9ddbe-241">Она может плавно перемещать фигуру между текущей и новой позицией.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-241">It can move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="9ddbe-242">Обновите метод `updateShape` клиента в файле *Default. HTML* , чтобы он был похож на выделенный код:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-242">Update the client's `updateShape` method in the *Default.html* file to look like the highlighted code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. <span data-ttu-id="9ddbe-243">Нажмите кнопку Воспроизведение, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-243">Select the play button to start the application.</span></span>

1. <span data-ttu-id="9ddbe-244">Скопируйте URL-адрес страницы.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-244">Copy the page's URL.</span></span>

1. <span data-ttu-id="9ddbe-245">Откройте другой браузер и вставьте URL-адрес в адресную строку.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-245">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="9ddbe-246">Перетащите фигуру в одно из окон браузера.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-246">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="9ddbe-247">Перемещение фигуры в другом окне выглядит менее жерки.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-247">The movement of the shape in the other window appears less jerky.</span></span> <span data-ttu-id="9ddbe-248">Приложение интерполирует свое перемещение с течением времени, а не устанавливается один раз для каждого входящего сообщения.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-248">The app interpolates its movement over time rather than being set once per incoming message.</span></span>

<span data-ttu-id="9ddbe-249">Этот код перемещает фигуру из старого расположения в новое.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-249">This code moves the shape from the old location to the new one.</span></span> <span data-ttu-id="9ddbe-250">Сервер задает расположение фигуры на протяжении интервала анимации.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-250">The server gives the position of the shape over the course of the animation interval.</span></span> <span data-ttu-id="9ddbe-251">В этом случае это 100 миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-251">In this case, that's 100 milliseconds.</span></span> <span data-ttu-id="9ddbe-252">Приложение очищает любую предыдущую анимацию, запущенную на фигуре, до начала новой анимации.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-252">The app clears any previous animation running on the shape before the new animation starts.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="9ddbe-253">Получение кода</span><span class="sxs-lookup"><span data-stu-id="9ddbe-253">Get the code</span></span>

[<span data-ttu-id="9ddbe-254">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="9ddbe-254">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a><span data-ttu-id="9ddbe-255">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9ddbe-255">Additional resources</span></span>

<span data-ttu-id="9ddbe-256">Парадигма связи, которую вы только что изучили, полезна для разработки Интернет-игр и других симуляций, таких как [игра «прокрутка», созданная с помощью SignalR](https://shootr.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="9ddbe-256">The communication paradigm you just learned about is useful for developing online games and other simulations, like [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="9ddbe-257">Дополнительные сведения о SignalR см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-257">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="9ddbe-258">Проект SignalR</span><span class="sxs-lookup"><span data-stu-id="9ddbe-258">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="9ddbe-259">GitHub и примеры SignalR</span><span class="sxs-lookup"><span data-stu-id="9ddbe-259">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="9ddbe-260">Вики-сайт SignalR</span><span class="sxs-lookup"><span data-stu-id="9ddbe-260">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="9ddbe-261">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ddbe-261">Next steps</span></span>

<span data-ttu-id="9ddbe-262">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="9ddbe-262">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ddbe-263">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="9ddbe-263">Set up the project</span></span>
> * <span data-ttu-id="9ddbe-264">Создано базовое приложение</span><span class="sxs-lookup"><span data-stu-id="9ddbe-264">Created the base application</span></span>
> * <span data-ttu-id="9ddbe-265">Сопоставлено с концентратором при запуске приложения</span><span class="sxs-lookup"><span data-stu-id="9ddbe-265">Mapped to the hub when app starts</span></span>
> * <span data-ttu-id="9ddbe-266">Добавлен клиент</span><span class="sxs-lookup"><span data-stu-id="9ddbe-266">Added the client</span></span>
> * <span data-ttu-id="9ddbe-267">Запустили приложение</span><span class="sxs-lookup"><span data-stu-id="9ddbe-267">Ran the app</span></span>
> * <span data-ttu-id="9ddbe-268">Добавлен цикл клиента</span><span class="sxs-lookup"><span data-stu-id="9ddbe-268">Added the client loop</span></span>
> * <span data-ttu-id="9ddbe-269">Добавлен цикл сервера</span><span class="sxs-lookup"><span data-stu-id="9ddbe-269">Added the server loop</span></span>
> * <span data-ttu-id="9ddbe-270">Добавлена гладкая анимация</span><span class="sxs-lookup"><span data-stu-id="9ddbe-270">Added smooth animation</span></span>

<span data-ttu-id="9ddbe-271">Перейдите к следующей статье, чтобы узнать, как создать веб-приложение, использующее ASP.NET SignalR 2 для предоставления функций серверной широковещательной рассылки.</span><span class="sxs-lookup"><span data-stu-id="9ddbe-271">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9ddbe-272">SignalR 2 и трансляция сервера</span><span class="sxs-lookup"><span data-stu-id="9ddbe-272">SignalR 2 and server broadcasting</span></span>](tutorial-server-broadcast-with-signalr.md)