---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: Учебник. начало работы с SignalR 1. x | Документация Майкрософт
author: bradygaster
description: Используйте ASP.NET SignalR для создания приложения разговора в режиме реального времени на HTML-странице.
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505752"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a><span data-ttu-id="b0d69-103">Учебник. начало работы с SignalR 1. x</span><span class="sxs-lookup"><span data-stu-id="b0d69-103">Tutorial: Getting Started with SignalR 1.x</span></span>

<span data-ttu-id="b0d69-104">[Патрик Флетчера](https://github.com/pfletcher), [Тим тибкен](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="b0d69-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="b0d69-105">В этом учебнике содержатся сведения об использовании SignalR для создания приложения разговора в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="b0d69-105">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="b0d69-106">Вы добавите SignalR в пустое веб-приложение ASP.NET и создадите HTML-страницу для отправки и вывода сообщений.</span><span class="sxs-lookup"><span data-stu-id="b0d69-106">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="b0d69-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="b0d69-107">Overview</span></span>

<span data-ttu-id="b0d69-108">В этом учебнике рассматривается разработка SignalR, в которой показано, как создать простое приложение для разговора на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="b0d69-108">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="b0d69-109">Вы добавите библиотеку SignalR в пустое веб-приложение ASP.NET, создадите класс концентратора для отправки сообщений клиентам и создадите HTML-страницу, позволяющую пользователям отправлять и получать сообщения в чате.</span><span class="sxs-lookup"><span data-stu-id="b0d69-109">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="b0d69-110">Аналогичный учебник, в котором показано, как создать приложение разговора в MVC 4 с помощью представления MVC, см. в разделе [Начало работы с SignalR и MVC 4](index.md).</span><span class="sxs-lookup"><span data-stu-id="b0d69-110">For a similar tutorial that shows how to create a chat application in MVC 4 using an MVC view, see [Getting Started with SignalR and MVC 4](index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b0d69-111">В этом руководстве используется версия SignalR (1. x).</span><span class="sxs-lookup"><span data-stu-id="b0d69-111">This tutorial uses the release (1.x) version of SignalR.</span></span> <span data-ttu-id="b0d69-112">Дополнительные сведения об изменениях в SignalR 1. x и 2,0 см. в разделе [Обновление проектов SignalR 1. x](../releases/upgrading-signalr-1x-projects-to-20.md).</span><span class="sxs-lookup"><span data-stu-id="b0d69-112">For details on changes between SignalR 1.x and 2.0, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<span data-ttu-id="b0d69-113">SignalR — это библиотека .NET с открытым исходным кодом для создания веб-приложений, требующих интерактивного взаимодействия с пользователем или обновления данных в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="b0d69-113">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="b0d69-114">К примерам относятся социальные приложения, многопользовательские игры, Бизнес-совместная работа, Новости, погода или финансовые обновления.</span><span class="sxs-lookup"><span data-stu-id="b0d69-114">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="b0d69-115">Они часто называются приложениями в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="b0d69-115">These are often called real-time applications.</span></span>

<span data-ttu-id="b0d69-116">SignalR упрощает процесс создания приложений в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="b0d69-116">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="b0d69-117">Он включает библиотеку сервера ASP.NET и клиентскую библиотеку JavaScript, чтобы упростить управление подключениями клиента и сервера и отправлять обновления содержимого на клиенты.</span><span class="sxs-lookup"><span data-stu-id="b0d69-117">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="b0d69-118">Библиотеку SignalR можно добавить в существующее приложение ASP.NET для получения функциональных возможностей в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="b0d69-118">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="b0d69-119">В этом учебнике демонстрируются следующие задачи разработки SignalR:</span><span class="sxs-lookup"><span data-stu-id="b0d69-119">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="b0d69-120">Добавление библиотеки SignalR в веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b0d69-120">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="b0d69-121">Создание класса концентратора для отправки содержимого клиентам.</span><span class="sxs-lookup"><span data-stu-id="b0d69-121">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="b0d69-122">Использование библиотеки jQuery SignalR на веб-странице для отправки сообщений и вывода обновлений из центра.</span><span class="sxs-lookup"><span data-stu-id="b0d69-122">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="b0d69-123">На следующем снимке экрана показано приложение разговора, выполняемое в браузере.</span><span class="sxs-lookup"><span data-stu-id="b0d69-123">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="b0d69-124">Каждый новый пользователь может публиковать комментарии и просматривать комментарии, добавленные после того, как пользователь присоединился к разговору.</span><span class="sxs-lookup"><span data-stu-id="b0d69-124">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![Экземпляры чата](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="b0d69-126">Священ</span><span class="sxs-lookup"><span data-stu-id="b0d69-126">Sections:</span></span>

- [<span data-ttu-id="b0d69-127">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="b0d69-127">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="b0d69-128">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="b0d69-128">Run the Sample</span></span>](#run)
- [<span data-ttu-id="b0d69-129">Изучение кода</span><span class="sxs-lookup"><span data-stu-id="b0d69-129">Examine the Code</span></span>](#code)
- [<span data-ttu-id="b0d69-130">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="b0d69-130">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="b0d69-131">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="b0d69-131">Set up the Project</span></span>

<span data-ttu-id="b0d69-132">В этом разделе показано, как создать пустое веб-приложение ASP.NET, добавить SignalR и создать приложение Chat.</span><span class="sxs-lookup"><span data-stu-id="b0d69-132">This section shows how to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="b0d69-133">Предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="b0d69-133">Prerequisites:</span></span>

- <span data-ttu-id="b0d69-134">Visual Studio 2010 с пакетом обновления 1 (SP1) или 2012.</span><span class="sxs-lookup"><span data-stu-id="b0d69-134">Visual Studio 2010 SP1 or 2012.</span></span> <span data-ttu-id="b0d69-135">Если у вас нет Visual Studio, см. [ASP.net downloads](https://www.asp.net/downloads) , чтобы получить бесплатное средство visual Studio 2012 Express Development Tool.</span><span class="sxs-lookup"><span data-stu-id="b0d69-135">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="b0d69-136">[Microsoft ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=279941).</span><span class="sxs-lookup"><span data-stu-id="b0d69-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span></span> <span data-ttu-id="b0d69-137">Для Visual Studio 2012 этот установщик добавляет новые функции ASP.NET, включая шаблоны SignalR, в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0d69-137">For Visual Studio 2012, this installer adds new ASP.NET features including SignalR templates to Visual Studio.</span></span> <span data-ttu-id="b0d69-138">Для Visual Studio 2010 с пакетом обновления 1 (SP1) установщик недоступен, но можно завершить работу с руководством, установив пакет NuGet SignalR, как описано в шагах установки.</span><span class="sxs-lookup"><span data-stu-id="b0d69-138">For Visual Studio 2010 SP1, an installer is not available but you can complete the tutorial by installing the SignalR NuGet package as described in the setup steps.</span></span>

<span data-ttu-id="b0d69-139">Следующие шаги используют Visual Studio 2012 для создания пустого веб-приложения ASP.NET и добавления библиотеки SignalR:</span><span class="sxs-lookup"><span data-stu-id="b0d69-139">The following steps use Visual Studio 2012 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="b0d69-140">В Visual Studio создайте пустое веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b0d69-140">In Visual Studio create an ASP.NET Empty Web Application.</span></span>

    ![Создать пустой веб-сайт](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="b0d69-142">Откройте **консоль диспетчера пакетов** , выбрав **Сервис | Диспетчер пакетов NuGet | Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-142">Open the **Package Manager Console** by selecting **Tools | NuGet Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="b0d69-143">В окне консоли введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0d69-143">Enter the following command into the console window:</span></span>

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    <span data-ttu-id="b0d69-144">Эта команда устанавливает последнюю версию SignalR 1. x.</span><span class="sxs-lookup"><span data-stu-id="b0d69-144">This command installs the latest version of SignalR 1.x.</span></span>
3. <span data-ttu-id="b0d69-145">В **Обозреватель решений**щелкните правой кнопкой мыши проект, выберите **Добавить | Класс**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-145">In **Solution Explorer**, right-click the project, select **Add | Class**.</span></span> <span data-ttu-id="b0d69-146">Назовите новый класс **часуб**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-146">Name the new class **ChatHub**.</span></span>
4. <span data-ttu-id="b0d69-147">В **Обозреватель решений** разверните узел скрипты.</span><span class="sxs-lookup"><span data-stu-id="b0d69-147">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="b0d69-148">Библиотеки скриптов для jQuery и SignalR отображаются в проекте.</span><span class="sxs-lookup"><span data-stu-id="b0d69-148">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    ![Ссылки на библиотеки](tutorial-getting-started-with-signalr/_static/image3.png)
5. <span data-ttu-id="b0d69-150">Замените код в классе **часуб** следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="b0d69-150">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="b0d69-151">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите команду **Добавить | Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-151">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="b0d69-152">В диалоговом окне **Добавление нового элемента** выберите **Глобальный класс приложения** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-152">In the **Add New Item** dialog, select **Global Application Class** and click **Add**.</span></span>

    ![Добавить глобальное](tutorial-getting-started-with-signalr/_static/image4.png)
7. <span data-ttu-id="b0d69-154">Добавьте следующие `using` операторы после указанных операторов `using` в классе Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="b0d69-154">Add the following `using` statements after the provided `using` statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="b0d69-155">Добавьте следующую строку кода в метод `Application_Start` глобального класса, чтобы зарегистрировать маршрут по умолчанию для концентраторов SignalR.</span><span class="sxs-lookup"><span data-stu-id="b0d69-155">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR hubs.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. <span data-ttu-id="b0d69-156">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите команду **Добавить | Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-156">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="b0d69-157">В диалоговом окне **Добавление нового элемента** выберите HTML-страница и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-157">In the **Add New Item** dialog, select Html Page and click **Add**.</span></span>
10. <span data-ttu-id="b0d69-158">В **Обозреватель решений**щелкните правой кнопкой мыши только что СОЗДАНную HTML-страницу и выберите пункт **задать как начальную страницу**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-158">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
11. <span data-ttu-id="b0d69-159">Замените код по умолчанию на странице HTML следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="b0d69-159">Replace the default code in the HTML page with the following code.</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. <span data-ttu-id="b0d69-160">**Сохраните все** для проекта.</span><span class="sxs-lookup"><span data-stu-id="b0d69-160">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="b0d69-161">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="b0d69-161">Run the Sample</span></span>

1. <span data-ttu-id="b0d69-162">Нажмите клавишу F5, чтобы запустить проект в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="b0d69-162">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="b0d69-163">Страница HTML загружается в экземпляр браузера и запрашивает имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="b0d69-163">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![Введите имя пользователя](tutorial-getting-started-with-signalr/_static/image5.png)
2. <span data-ttu-id="b0d69-165">Введите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="b0d69-165">Enter a user name.</span></span>
3. <span data-ttu-id="b0d69-166">Скопируйте URL-адрес из строки адреса браузера и используйте его, чтобы открыть два других экземпляра браузера.</span><span class="sxs-lookup"><span data-stu-id="b0d69-166">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="b0d69-167">В каждом экземпляре браузера введите уникальное имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="b0d69-167">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="b0d69-168">В каждом экземпляре браузера добавьте комментарий и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-168">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="b0d69-169">Комментарии должны отображаться во всех экземплярах браузера.</span><span class="sxs-lookup"><span data-stu-id="b0d69-169">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b0d69-170">Это простое приложение разговора не поддерживает контекст обсуждения на сервере.</span><span class="sxs-lookup"><span data-stu-id="b0d69-170">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="b0d69-171">Центр передает комментарии всем текущим пользователям.</span><span class="sxs-lookup"><span data-stu-id="b0d69-171">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="b0d69-172">Пользователи, которые присоединяются к обсуждению позже, увидят сообщения, добавленные с момента присоединение.</span><span class="sxs-lookup"><span data-stu-id="b0d69-172">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="b0d69-173">На следующем снимке экрана показано приложение разговора, выполняемое в трех экземплярах браузера, все из которых обновляются, когда один экземпляр отправляет сообщение:</span><span class="sxs-lookup"><span data-stu-id="b0d69-173">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![Браузеры чатов](tutorial-getting-started-with-signalr/_static/image6.png)
5. <span data-ttu-id="b0d69-175">В **Обозреватель решений**просмотрите узел **документы скрипта** для работающего приложения.</span><span class="sxs-lookup"><span data-stu-id="b0d69-175">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="b0d69-176">Существует файл скрипта **с именем** Hubs, динамически формируемый библиотекой SignalR во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="b0d69-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="b0d69-177">Этот файл управляет обменом данными между скриптом jQuery и кодом на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="b0d69-177">This file manages the communication between jQuery script and server-side code.</span></span>

    ![Созданный скрипт концентратора](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="b0d69-179">Изучение кода</span><span class="sxs-lookup"><span data-stu-id="b0d69-179">Examine the Code</span></span>

<span data-ttu-id="b0d69-180">Приложение разговора SignalR демонстрирует две основные задачи разработки SignalR: создание концентратора в качестве основного объекта координации на сервере и использование библиотеки jQuery SignalR для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="b0d69-180">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="b0d69-181">Концентраторы SignalR</span><span class="sxs-lookup"><span data-stu-id="b0d69-181">SignalR Hubs</span></span>

<span data-ttu-id="b0d69-182">В примере кода класс **часуб** является производным от класса **Microsoft. AspNet. SignalR. Hub** .</span><span class="sxs-lookup"><span data-stu-id="b0d69-182">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="b0d69-183">Наследование от класса **Hub** — это удобный способ создания приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="b0d69-183">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="b0d69-184">Вы можете создавать открытые методы в классе Hub, а затем обращаться к этим методам, вызывая их из скриптов jQuery на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="b0d69-184">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="b0d69-185">В коде разговора клиенты вызывают метод **часуб. Send** для отправки нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="b0d69-185">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="b0d69-186">Концентратор, в свою очередь, отправляет сообщение всем клиентам, вызывая **Clients. ALL. броадкастмессаже**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-186">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="b0d69-187">Метод **Send** демонстрирует несколько основных понятий:</span><span class="sxs-lookup"><span data-stu-id="b0d69-187">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="b0d69-188">Объявите открытые методы в концентраторе, чтобы клиенты могли их вызывать.</span><span class="sxs-lookup"><span data-stu-id="b0d69-188">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="b0d69-189">Используйте динамическое свойство **Microsoft. AspNet. SignalR. Hub. Clients** для доступа ко всем клиентам, подключенным к этому концентратору.</span><span class="sxs-lookup"><span data-stu-id="b0d69-189">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="b0d69-190">Вызовите функцию jQuery на клиенте (например, функцию `broadcastMessage`) для обновления клиентов.</span><span class="sxs-lookup"><span data-stu-id="b0d69-190">Call a jQuery function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="b0d69-191">SignalR и jQuery</span><span class="sxs-lookup"><span data-stu-id="b0d69-191">SignalR and jQuery</span></span>

<span data-ttu-id="b0d69-192">На странице HTML в образце кода показано, как использовать библиотеку jQuery SignalR для взаимодействия с концентратором SignalR.</span><span class="sxs-lookup"><span data-stu-id="b0d69-192">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="b0d69-193">Основными задачами в коде является объявление прокси-сервера для ссылки на концентратор, объявление функции, которую сервер может вызывать для отправки содержимого клиентам, и запуск соединения для отправки сообщений в концентратор.</span><span class="sxs-lookup"><span data-stu-id="b0d69-193">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="b0d69-194">Следующий код объявляет прокси-сервер для концентратора.</span><span class="sxs-lookup"><span data-stu-id="b0d69-194">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="b0d69-195">В jQuery ссылка на серверный класс и его члены находятся в неоднородном регистре.</span><span class="sxs-lookup"><span data-stu-id="b0d69-195">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="b0d69-196">Пример кода ссылается C# на класс **часуб** в jQuery как **часуб**.</span><span class="sxs-lookup"><span data-stu-id="b0d69-196">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span>

<span data-ttu-id="b0d69-197">В следующем коде показано, как создать функцию обратного вызова в скрипте.</span><span class="sxs-lookup"><span data-stu-id="b0d69-197">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="b0d69-198">Класс концентратора на сервере вызывает эту функцию для отправки обновлений содержимого на каждый клиент.</span><span class="sxs-lookup"><span data-stu-id="b0d69-198">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="b0d69-199">Две строки, которые кодирует содержимое в формате HTML перед отображением, являются необязательными и показывают простой способ предотвращения внедрения скрипта.</span><span class="sxs-lookup"><span data-stu-id="b0d69-199">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

<span data-ttu-id="b0d69-200">В следующем коде показано, как открыть подключение к концентратору.</span><span class="sxs-lookup"><span data-stu-id="b0d69-200">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="b0d69-201">Код запускает соединение, а затем передает ему функцию для управления событием щелчка на кнопке **Send** на странице HTML.</span><span class="sxs-lookup"><span data-stu-id="b0d69-201">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="b0d69-202">Этот подход гарантирует, что соединение будет установлено до выполнения обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="b0d69-202">This approach insures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="b0d69-203">Next Steps</span><span class="sxs-lookup"><span data-stu-id="b0d69-203">Next Steps</span></span>

<span data-ttu-id="b0d69-204">Вы узнали, что SignalR — это платформа для создания веб-приложений в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="b0d69-204">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="b0d69-205">Вы также узнали о нескольких задачах разработки SignalR: как добавить SignalR в приложение ASP.NET, как создать класс Hub, а также как отправлять и получать сообщения от концентратора.</span><span class="sxs-lookup"><span data-stu-id="b0d69-205">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="b0d69-206">Вы можете сделать пример приложения в этом руководстве или других приложениях SignalR, доступных через Интернет, развернув их на поставщик услуг размещения.</span><span class="sxs-lookup"><span data-stu-id="b0d69-206">You can make the sample application in this tutorial or other SignalR applications available over the Internet by deploying them to a hosting provider.</span></span> <span data-ttu-id="b0d69-207">Корпорация Майкрософт предлагает бесплатное веб-размещение для 10 веб-сайтов в бесплатной [пробной учетной записи Windows Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="b0d69-207">Microsoft offers free web hosting for up to 10 web sites in a free [Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="b0d69-208">Пошаговое руководство по развертыванию примера приложения SignalR см. в статье [публикация начало работы образца в качестве веб-сайта Windows Azure](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0d69-208">For a walkthrough on how to deploy the sample SignalR application, see [Publish the SignalR Getting Started Sample as a Windows Azure Web Site](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span></span> <span data-ttu-id="b0d69-209">Подробные сведения о развертывании веб-проекта Visual Studio на веб-сайте Windows Azure см. в статье [развертывание приложения ASP.NET на веб-сайте Windows Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span><span class="sxs-lookup"><span data-stu-id="b0d69-209">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Deploying an ASP.NET Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span> <span data-ttu-id="b0d69-210">(Примечание. транспорт WebSocket в настоящее время не поддерживается для веб-сайтов Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b0d69-210">(Note: The WebSocket transport is not currently supported for Windows Azure Web Sites.</span></span> <span data-ttu-id="b0d69-211">Если транспорт WebSocket недоступен, SignalR использует другие доступные транспорты, как описано в разделе транспорты статьи [Введение в SignalR](index.md).)</span><span class="sxs-lookup"><span data-stu-id="b0d69-211">When WebSocket transport is not available, SignalR uses the other available transports as described in the Transports section of the [Introduction to SignalR topic](index.md).)</span></span>

<span data-ttu-id="b0d69-212">Чтобы узнать о более сложных концепциях разработки SignalR, посетите следующие сайты с исходным кодом и ресурсами SignalR:</span><span class="sxs-lookup"><span data-stu-id="b0d69-212">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="b0d69-213">Проект SignalR</span><span class="sxs-lookup"><span data-stu-id="b0d69-213">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="b0d69-214">GitHub и примеры SignalR</span><span class="sxs-lookup"><span data-stu-id="b0d69-214">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="b0d69-215">Вики-сайт SignalR</span><span class="sxs-lookup"><span data-stu-id="b0d69-215">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
