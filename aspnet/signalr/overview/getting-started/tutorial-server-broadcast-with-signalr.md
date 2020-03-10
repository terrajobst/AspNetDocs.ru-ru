---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: Учебник. широковещательная рассылка сервера с помощью SignalR 2 | Документация Майкрософт
author: tdykstra
description: В этом руководстве показано, как создать веб-приложение, использующее ASP.NET SignalR 2 для предоставления функций серверной широковещательной рассылки.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431244"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="2b449-103">Учебник. серверное вещание с SignalR 2</span><span class="sxs-lookup"><span data-stu-id="2b449-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="2b449-104">В этом руководстве показано, как создать веб-приложение, использующее ASP.NET SignalR 2 для предоставления функций серверной широковещательной рассылки.</span><span class="sxs-lookup"><span data-stu-id="2b449-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="2b449-105">Серверное вещание означает, что сервер запускает обмен данными, отправляемый клиентам.</span><span class="sxs-lookup"><span data-stu-id="2b449-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="2b449-106">Приложение, которое будет создано в этом учебнике, имитирует биржевое биржевое, типичный сценарий для серверной функции вещания.</span><span class="sxs-lookup"><span data-stu-id="2b449-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="2b449-107">Периодически сервер обновляет цены на акции и передает обновления на все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="2b449-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="2b449-108">В браузере числа и символы в столбцах **Change** и **%** динамически изменяются в ответ на уведомления с сервера.</span><span class="sxs-lookup"><span data-stu-id="2b449-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="2b449-109">Если открыть дополнительные браузеры для одного и того же URL-адреса, все они будут отображать одни и те же данные и одни и те же изменения данных одновременно.</span><span class="sxs-lookup"><span data-stu-id="2b449-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Создание веб-сайта](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="2b449-111">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="2b449-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b449-112">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="2b449-112">Create the project</span></span>
> * <span data-ttu-id="2b449-113">Настройка кода сервера</span><span class="sxs-lookup"><span data-stu-id="2b449-113">Set up the server code</span></span>
> * <span data-ttu-id="2b449-114">Проверка серверного кода</span><span class="sxs-lookup"><span data-stu-id="2b449-114">Examine the server code</span></span>
> * <span data-ttu-id="2b449-115">Настройка клиентского кода</span><span class="sxs-lookup"><span data-stu-id="2b449-115">Set up the client code</span></span>
> * <span data-ttu-id="2b449-116">Изучение кода клиента</span><span class="sxs-lookup"><span data-stu-id="2b449-116">Examine the client code</span></span>
> * <span data-ttu-id="2b449-117">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="2b449-117">Test the application</span></span>
> * <span data-ttu-id="2b449-118">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="2b449-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b449-119">Если вы не хотите поработать с этапами создания приложения, можно установить пакет SignalR. Sample в новом пустом проекте веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2b449-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="2b449-120">Если пакет NuGet устанавливается без выполнения действий, описанных в этом руководстве, необходимо выполнить инструкции из файла *readme. txt* .</span><span class="sxs-lookup"><span data-stu-id="2b449-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="2b449-121">Чтобы запустить пакет, необходимо добавить класс запуска OWIN, который вызывает метод `ConfigureSignalR` в установленном пакете.</span><span class="sxs-lookup"><span data-stu-id="2b449-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="2b449-122">Если не добавить класс запуска OWIN, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2b449-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="2b449-123">См. раздел [Установка образца стокктиккер в](#install-the-stockticker-sample) этой статье.</span><span class="sxs-lookup"><span data-stu-id="2b449-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b449-124">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2b449-124">Prerequisites</span></span>

* <span data-ttu-id="2b449-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) с рабочей нагрузкой **ASP.NET и веб-разработка**.</span><span class="sxs-lookup"><span data-stu-id="2b449-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="2b449-126">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="2b449-126">Create the project</span></span>

<span data-ttu-id="2b449-127">В этом разделе показано, как с помощью Visual Studio 2017 создать пустое веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2b449-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="2b449-128">В Visual Studio создайте веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2b449-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Создание веб-сайта](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="2b449-130">В окне **New ASP.NET Web Application-SignalR. стокктиккер** оставьте **пустым** выбранным и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2b449-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="2b449-131">Настройка кода сервера</span><span class="sxs-lookup"><span data-stu-id="2b449-131">Set up the server code</span></span>

<span data-ttu-id="2b449-132">В этом разделе вы настроите код, который выполняется на сервере.</span><span class="sxs-lookup"><span data-stu-id="2b449-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="2b449-133">Создание класса акции</span><span class="sxs-lookup"><span data-stu-id="2b449-133">Create the Stock class</span></span>

<span data-ttu-id="2b449-134">Начнем с создания класса « *складская* модель», который будет использоваться для хранения и передачи информации о акции.</span><span class="sxs-lookup"><span data-stu-id="2b449-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="2b449-135">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **класс**.</span><span class="sxs-lookup"><span data-stu-id="2b449-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="2b449-136">Назовите класс *фондовой* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="2b449-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="2b449-137">Замените код в файле *Stock.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2b449-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="2b449-138">Два свойства, которые вы задаете при создании акций, `Symbol` (например, MSFT для Майкрософт) и `Price`.</span><span class="sxs-lookup"><span data-stu-id="2b449-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="2b449-139">Другие свойства зависят от того, как и когда задается `Price`.</span><span class="sxs-lookup"><span data-stu-id="2b449-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="2b449-140">При первом задании `Price`значение распространяется на `DayOpen`.</span><span class="sxs-lookup"><span data-stu-id="2b449-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="2b449-141">После этого при установке `Price`приложение вычисляет значения свойств `Change` и `PercentChange` на основе разницы между `Price` и `DayOpen`.</span><span class="sxs-lookup"><span data-stu-id="2b449-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="2b449-142">Создание классов Стокктиккерхуб и Стокктиккер</span><span class="sxs-lookup"><span data-stu-id="2b449-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="2b449-143">Для обработки взаимодействия "сервер-клиент" вы будете использовать API концентратора SignalR.</span><span class="sxs-lookup"><span data-stu-id="2b449-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="2b449-144">Класс `StockTickerHub`, производный от класса SignalR `Hub`, будет выполнять получение подключений и вызовов методов от клиентов.</span><span class="sxs-lookup"><span data-stu-id="2b449-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="2b449-145">Также необходимо сохранить данные на бирже и запустить объект `Timer`.</span><span class="sxs-lookup"><span data-stu-id="2b449-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="2b449-146">Объект `Timer` периодически будет запускать обновления цен независимо от клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="2b449-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="2b449-147">Эти функции нельзя разместить в `Hub` классе, так как концентраторы являются временными.</span><span class="sxs-lookup"><span data-stu-id="2b449-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="2b449-148">Приложение создает `Hub` экземпляр класса для каждой задачи в концентраторе, например соединения и вызовы от клиента к серверу.</span><span class="sxs-lookup"><span data-stu-id="2b449-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="2b449-149">Таким образом, механизм, который хранит данные на бирже, обновляет цены и выполняет широковещательную рассылку, должен выполняться в отдельном классе.</span><span class="sxs-lookup"><span data-stu-id="2b449-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="2b449-150">Класс будет назван `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2b449-150">You'll name the class `StockTicker`.</span></span>

![Вещание от Стокктиккер](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="2b449-152">Необходимо, чтобы на сервере выполнялся только один экземпляр `StockTicker` класса, поэтому необходимо настроить ссылку из каждого экземпляра `StockTickerHub` на одноэлементный экземпляр `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2b449-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="2b449-153">Класс `StockTicker` должен выполнять широковещательную рассылку на клиентах, так как он содержит данные о акции и инициирует обновления, но `StockTicker` не является `Hub`ным классом.</span><span class="sxs-lookup"><span data-stu-id="2b449-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="2b449-154">Класс `StockTicker` должен получить ссылку на объект контекста подключения концентратора SignalR.</span><span class="sxs-lookup"><span data-stu-id="2b449-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="2b449-155">Затем он может использовать объект контекста подключения SignalR для передачи клиентам.</span><span class="sxs-lookup"><span data-stu-id="2b449-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="2b449-156">Создание StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="2b449-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="2b449-157">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="2b449-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="2b449-158">В окне **Добавить новый элемент-SignalR. стокктиккер**выберите **установлено** > **Visual C#**  > **Web** > **SignalR** , а затем выберите **класс концентратора SignalR (v2)** .</span><span class="sxs-lookup"><span data-stu-id="2b449-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="2b449-159">Назовите класс *стокктиккерхуб* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="2b449-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="2b449-160">На этом шаге создается файл класса *StockTickerHub.CS* .</span><span class="sxs-lookup"><span data-stu-id="2b449-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="2b449-161">Одновременно он добавляет набор файлов скриптов и ссылок на сборки, которые поддерживают SignalR для проекта.</span><span class="sxs-lookup"><span data-stu-id="2b449-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="2b449-162">Замените код в файле *StockTickerHub.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2b449-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="2b449-163">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="2b449-163">Save the file.</span></span>

<span data-ttu-id="2b449-164">Приложение использует класс [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) для определения методов, которые клиенты могут вызывать на сервере.</span><span class="sxs-lookup"><span data-stu-id="2b449-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="2b449-165">Вы определяете один метод: `GetAllStocks()`.</span><span class="sxs-lookup"><span data-stu-id="2b449-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="2b449-166">Когда клиент изначально подключается к серверу, он вызывает этот метод, чтобы получить список всех акций с текущими ценами.</span><span class="sxs-lookup"><span data-stu-id="2b449-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="2b449-167">Метод может выполняться синхронно и возвращать `IEnumerable<Stock>`, так как он возвращает данные из памяти.</span><span class="sxs-lookup"><span data-stu-id="2b449-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="2b449-168">Если методу пришлось бы получать данные, выполняя что-либо, которое может привести к ожиданиям, например при поиске базы данных или вызове веб-службы, необходимо указать `Task<IEnumerable<Stock>>` как возвращаемое значение, чтобы включить асинхронную обработку.</span><span class="sxs-lookup"><span data-stu-id="2b449-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="2b449-169">Дополнительные сведения см. [в разделе ASP.NET SignalR Hubs Guide-Server-on to Execute On асинхронное выполнение](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span><span class="sxs-lookup"><span data-stu-id="2b449-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="2b449-170">Атрибут `HubName` указывает, как приложение будет ссылаться на концентратор в коде JavaScript на клиенте.</span><span class="sxs-lookup"><span data-stu-id="2b449-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="2b449-171">Имя по умолчанию на клиенте, если этот атрибут не используется, является camelCase версией имени класса, которая в данном случае будет `stockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="2b449-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="2b449-172">Как вы увидите позже при создании класса `StockTicker`, приложение создает одноэлементный экземпляр этого класса в его статическом свойстве `Instance`.</span><span class="sxs-lookup"><span data-stu-id="2b449-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="2b449-173">Этот одноэлементный экземпляр `StockTicker` находится в памяти независимо от того, сколько клиентов подключается или отключается.</span><span class="sxs-lookup"><span data-stu-id="2b449-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="2b449-174">Этот экземпляр использует метод `GetAllStocks()` для возврата текущих данных об акциях.</span><span class="sxs-lookup"><span data-stu-id="2b449-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="2b449-175">Создание StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="2b449-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="2b449-176">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **класс**.</span><span class="sxs-lookup"><span data-stu-id="2b449-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="2b449-177">Назовите класс *стокктиккер* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="2b449-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="2b449-178">Замените код в файле *StockTicker.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2b449-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="2b449-179">Так как все потоки будут выполнять один и тот же экземпляр Стокктиккер кода, класс Стокктиккер должен быть потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="2b449-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="2b449-180">Проверка серверного кода</span><span class="sxs-lookup"><span data-stu-id="2b449-180">Examine the server code</span></span>

<span data-ttu-id="2b449-181">При изучении серверного кода он поможет понять, как работает приложение.</span><span class="sxs-lookup"><span data-stu-id="2b449-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="2b449-182">Сохранение одноэлементного экземпляра в статическом поле</span><span class="sxs-lookup"><span data-stu-id="2b449-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="2b449-183">Код инициализирует статическое поле `_instance`, которое выполняет резервное копирование свойства `Instance` с помощью экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="2b449-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="2b449-184">Поскольку конструктор является частным, единственным экземпляром класса, который может создать приложение.</span><span class="sxs-lookup"><span data-stu-id="2b449-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="2b449-185">Приложение использует [отложенную инициализацию](/dotnet/framework/performance/lazy-initialization) для поля `_instance`.</span><span class="sxs-lookup"><span data-stu-id="2b449-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="2b449-186">Это не из соображений производительности.</span><span class="sxs-lookup"><span data-stu-id="2b449-186">It's not for performance reasons.</span></span> <span data-ttu-id="2b449-187">Необходимо убедиться, что создание экземпляра является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="2b449-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="2b449-188">Каждый раз, когда клиент подключается к серверу, новый экземпляр класса Стокктиккерхуб, выполняющийся в отдельном потоке, получает одноэлементный экземпляр Стокктиккер из статического свойства `StockTicker.Instance`, как было показано ранее в классе `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="2b449-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="2b449-189">Хранение данных о акции в ConcurrentDictionary</span><span class="sxs-lookup"><span data-stu-id="2b449-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="2b449-190">Конструктор инициализирует `_stocks` коллекцию с помощью некоторых примеров биржевых данных, а `GetAllStocks` возвращает акции.</span><span class="sxs-lookup"><span data-stu-id="2b449-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="2b449-191">Как было показано ранее, эта коллекция акций возвращается с помощью `StockTickerHub.GetAllStocks`, который является серверным методом в классе `Hub`, который может вызываться клиентами.</span><span class="sxs-lookup"><span data-stu-id="2b449-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="2b449-192">Коллекция Stocks определяется как тип [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) для потокобезопасности.</span><span class="sxs-lookup"><span data-stu-id="2b449-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="2b449-193">В качестве альтернативы можно использовать объект [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) и явным образом заблокировать словарь при внесении в него изменений.</span><span class="sxs-lookup"><span data-stu-id="2b449-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="2b449-194">Для этого примера приложения можно сохранить данные приложения в памяти и потерять данные, когда приложение уничтожает экземпляр `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2b449-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="2b449-195">В реальном приложении вы бы работали с внутренним хранилищем данных, например с базой данных.</span><span class="sxs-lookup"><span data-stu-id="2b449-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="2b449-196">Периодическое обновление цен на акции</span><span class="sxs-lookup"><span data-stu-id="2b449-196">Periodically updating stock prices</span></span>

<span data-ttu-id="2b449-197">Конструктор запускает `Timer` объект, который периодически вызывает методы, которые обновляют цены на акции на случайном уровне.</span><span class="sxs-lookup"><span data-stu-id="2b449-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="2b449-198">`Timer` вызывает `UpdateStockPrices`, который в параметре state передает значение null.</span><span class="sxs-lookup"><span data-stu-id="2b449-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="2b449-199">Перед обновлением цен приложение принимает блокировку на объект `_updateStockPricesLock`.</span><span class="sxs-lookup"><span data-stu-id="2b449-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="2b449-200">Код проверяет, обновил ли другой поток цены, а затем вызывает `TryUpdateStockPrice` для каждой акции в списке.</span><span class="sxs-lookup"><span data-stu-id="2b449-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="2b449-201">Метод `TryUpdateStockPrice` определяет, следует ли изменить цену акции и сколько ее изменить.</span><span class="sxs-lookup"><span data-stu-id="2b449-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="2b449-202">Если цена акций изменяется, приложение вызывает `BroadcastStockPrice`, чтобы транслировать изменение цены акций на все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="2b449-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="2b449-203">Флаг `_updatingStockPrices`, обозначенный как [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) , чтобы обеспечить потокобезопасность.</span><span class="sxs-lookup"><span data-stu-id="2b449-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="2b449-204">В реальном приложении метод `TryUpdateStockPrice` вызовет веб-службу для поиска цены.</span><span class="sxs-lookup"><span data-stu-id="2b449-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="2b449-205">В этом коде приложение использует генератор случайных чисел для внесения изменений случайным образом.</span><span class="sxs-lookup"><span data-stu-id="2b449-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="2b449-206">Получение контекста SignalR, чтобы класс Стокктиккер мог выполнить широковещательную рассылку клиентам</span><span class="sxs-lookup"><span data-stu-id="2b449-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="2b449-207">Поскольку изменения цен происходят в объекте `StockTicker`, это объект, который должен вызывать метод `updateStockPrice` на всех подключенных клиентах.</span><span class="sxs-lookup"><span data-stu-id="2b449-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="2b449-208">В `Hub` классе имеется API для вызова клиентских методов, но `StockTicker` не является производным от класса `Hub` и не имеет ссылки на какой-либо объект `Hub`.</span><span class="sxs-lookup"><span data-stu-id="2b449-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="2b449-209">Для вещания подключенным клиентам класс `StockTicker` должен получить экземпляр контекста SignalR для `StockTickerHub` класса и использовать его для вызова методов на клиентах.</span><span class="sxs-lookup"><span data-stu-id="2b449-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="2b449-210">Код получает ссылку на контекст SignalR при создании экземпляра одноэлементного класса, передает эту ссылку конструктору, а конструктор помещает его в свойство `Clients`.</span><span class="sxs-lookup"><span data-stu-id="2b449-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="2b449-211">Существует две причины, по которым вы хотите получить контекст только один раз: Получение контекста является дорогостоящей задачей и получение ее после однократное обеспечение того, что приложение сохраняет предполагаемый порядок сообщений, отправляемых клиентам.</span><span class="sxs-lookup"><span data-stu-id="2b449-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="2b449-212">Получение свойства `Clients` контекста и помещение его в свойство `StockTickerClient` позволяет написать код для вызова методов клиента, которые выглядят так же, как в классе `Hub`.</span><span class="sxs-lookup"><span data-stu-id="2b449-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="2b449-213">Например, чтобы выполнить вещание на всех клиентах, можно написать `Clients.All.updateStockPrice(stock)`.</span><span class="sxs-lookup"><span data-stu-id="2b449-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="2b449-214">Метод `updateStockPrice`, который вы вызываете в `BroadcastStockPrice`, еще не существует.</span><span class="sxs-lookup"><span data-stu-id="2b449-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="2b449-215">Он будет добавлен позже при написании кода, выполняемого на клиенте.</span><span class="sxs-lookup"><span data-stu-id="2b449-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="2b449-216">Ссылку на `updateStockPrice` можно найти в этом разделе, поскольку `Clients.All` является динамическим. Это означает, что приложение будет оценивать выражение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2b449-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="2b449-217">При выполнении этого вызова метода SignalR отправляет клиенту имя метода и значение параметра, а если у клиента есть метод с именем `updateStockPrice`, приложение будет вызывать этот метод и передавать ему значение параметра.</span><span class="sxs-lookup"><span data-stu-id="2b449-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="2b449-218">`Clients.All` означает отправку на все клиенты.</span><span class="sxs-lookup"><span data-stu-id="2b449-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="2b449-219">SignalR предоставляет другие возможности для указания клиентов или групп клиентов для отправки.</span><span class="sxs-lookup"><span data-stu-id="2b449-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="2b449-220">Дополнительные сведения см. в разделе [хубконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="2b449-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="2b449-221">Регистрация маршрута SignalR</span><span class="sxs-lookup"><span data-stu-id="2b449-221">Register the SignalR route</span></span>

<span data-ttu-id="2b449-222">Серверу необходимо указать, какой URL-адрес следует перехватить, и направить его в SignalR.</span><span class="sxs-lookup"><span data-stu-id="2b449-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="2b449-223">Для этого добавьте класс запуска OWIN:</span><span class="sxs-lookup"><span data-stu-id="2b449-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="2b449-224">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="2b449-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="2b449-225">В окне **Добавление нового элемента-SignalR. стокктиккер** выберите **установленный** > **Visual C#**  > **Web** , а затем выберите **класс запуска OWIN**.</span><span class="sxs-lookup"><span data-stu-id="2b449-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="2b449-226">Назовите класс *Startup* и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2b449-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="2b449-227">Замените код по умолчанию в файле *Startup.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2b449-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="2b449-228">Настройка кода сервера завершена.</span><span class="sxs-lookup"><span data-stu-id="2b449-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="2b449-229">В следующем разделе вы настроите клиент.</span><span class="sxs-lookup"><span data-stu-id="2b449-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="2b449-230">Настройка клиентского кода</span><span class="sxs-lookup"><span data-stu-id="2b449-230">Set up the client code</span></span>

<span data-ttu-id="2b449-231">В этом разделе вы настроите код, который выполняется на клиенте.</span><span class="sxs-lookup"><span data-stu-id="2b449-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="2b449-232">Создание HTML-страницы и файла JavaScript</span><span class="sxs-lookup"><span data-stu-id="2b449-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="2b449-233">На странице HTML будут отображены данные, а в файле JavaScript будут упорядочены данные.</span><span class="sxs-lookup"><span data-stu-id="2b449-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="2b449-234">Создание Стокктиккер. HTML</span><span class="sxs-lookup"><span data-stu-id="2b449-234">Create StockTicker.html</span></span>

<span data-ttu-id="2b449-235">Сначала нужно добавить HTML-клиент.</span><span class="sxs-lookup"><span data-stu-id="2b449-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="2b449-236">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **HTML-страницу**.</span><span class="sxs-lookup"><span data-stu-id="2b449-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="2b449-237">Назовите файл *стокктиккер* и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2b449-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="2b449-238">Замените код по умолчанию в файле *стокктиккер. HTML* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2b449-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="2b449-239">HTML создает таблицу с пятью столбцами, строкой заголовка и строкой данных с одной ячейкой, охватывающей все пять столбцов.</span><span class="sxs-lookup"><span data-stu-id="2b449-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="2b449-240">В строке данных отображается "Загрузка..." моментально при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="2b449-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="2b449-241">Код JavaScript удалит эту строку и добавит в нее строки с данными, полученными с сервера.</span><span class="sxs-lookup"><span data-stu-id="2b449-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="2b449-242">Теги скрипта определяют:</span><span class="sxs-lookup"><span data-stu-id="2b449-242">The script tags specify:</span></span>

    * <span data-ttu-id="2b449-243">Файл скрипта jQuery.</span><span class="sxs-lookup"><span data-stu-id="2b449-243">The jQuery script file.</span></span>

    * <span data-ttu-id="2b449-244">Основной файл скрипта SignalR.</span><span class="sxs-lookup"><span data-stu-id="2b449-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="2b449-245">Файл скрипта прокси SignalR.</span><span class="sxs-lookup"><span data-stu-id="2b449-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="2b449-246">Файл скрипта Стокктиккер, который будет создан позже.</span><span class="sxs-lookup"><span data-stu-id="2b449-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="2b449-247">Приложение динамически создает файл скрипта прокси-сервера SignalR.</span><span class="sxs-lookup"><span data-stu-id="2b449-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="2b449-248">Он указывает URL-адрес "/сигналр/хубс" и определяет методы прокси для методов в классе Hub, в данном случае для `StockTickerHub.GetAllStocks`.</span><span class="sxs-lookup"><span data-stu-id="2b449-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="2b449-249">При желании этот файл JavaScript можно создать вручную с помощью [служебных программ SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span><span class="sxs-lookup"><span data-stu-id="2b449-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="2b449-250">Не забудьте отключить динамическое создание файлов при вызове метода `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="2b449-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="2b449-251">В **Обозреватель решений**разверните узел **сценарии**.</span><span class="sxs-lookup"><span data-stu-id="2b449-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="2b449-252">Библиотеки скриптов для jQuery и SignalR отображаются в проекте.</span><span class="sxs-lookup"><span data-stu-id="2b449-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2b449-253">Диспетчер пакетов установит более позднюю версию сценариев SignalR.</span><span class="sxs-lookup"><span data-stu-id="2b449-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="2b449-254">Обновите ссылки на скрипт в блоке кода, чтобы они соответствовали версиям файлов скриптов в проекте.</span><span class="sxs-lookup"><span data-stu-id="2b449-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="2b449-255">В **Обозреватель решений**щелкните правой кнопкой мыши *стокктиккер. HTML*и выберите **задать в качестве начальной страницы**.</span><span class="sxs-lookup"><span data-stu-id="2b449-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="2b449-256">Создание Стокктиккер. js</span><span class="sxs-lookup"><span data-stu-id="2b449-256">Create StockTicker.js</span></span>

<span data-ttu-id="2b449-257">Теперь создайте файл JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2b449-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="2b449-258">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **файл JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="2b449-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="2b449-259">Назовите файл *стокктиккер* и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2b449-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="2b449-260">Добавьте следующий код в файл *стокктиккер. js* :</span><span class="sxs-lookup"><span data-stu-id="2b449-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="2b449-261">Изучение кода клиента</span><span class="sxs-lookup"><span data-stu-id="2b449-261">Examine the client code</span></span>

<span data-ttu-id="2b449-262">Если изучить клиентский код, он поможет узнать, как клиентский код взаимодействует с серверным кодом, чтобы обеспечить работу приложения.</span><span class="sxs-lookup"><span data-stu-id="2b449-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="2b449-263">Идет запуск подключения</span><span class="sxs-lookup"><span data-stu-id="2b449-263">Starting the connection</span></span>

<span data-ttu-id="2b449-264">`$.connection` ссылается на прокси-серверы SignalR.</span><span class="sxs-lookup"><span data-stu-id="2b449-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="2b449-265">Код получает ссылку на прокси-сервер для класса `StockTickerHub` и помещает его в переменную `ticker`.</span><span class="sxs-lookup"><span data-stu-id="2b449-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="2b449-266">Имя прокси-сервера — это имя, заданное атрибутом `HubName`:</span><span class="sxs-lookup"><span data-stu-id="2b449-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="2b449-267">После определения всех переменных и функций последняя строка кода в файле инициализирует подключение SignalR, вызывая функцию SignalR `start`.</span><span class="sxs-lookup"><span data-stu-id="2b449-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="2b449-268">Функция `start` выполняется асинхронно и возвращает [отложенный объект jQuery](http://api.jquery.com/category/deferred-object/).</span><span class="sxs-lookup"><span data-stu-id="2b449-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="2b449-269">Функцию done можно вызвать, чтобы указать функцию, вызываемую при завершении асинхронного действия приложением.</span><span class="sxs-lookup"><span data-stu-id="2b449-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="2b449-270">Получение всех акций</span><span class="sxs-lookup"><span data-stu-id="2b449-270">Getting all the stocks</span></span>

<span data-ttu-id="2b449-271">Функция `init` вызывает функцию `getAllStocks` на сервере и использует сведения, возвращаемые сервером для обновления таблицы запасов.</span><span class="sxs-lookup"><span data-stu-id="2b449-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="2b449-272">Обратите внимание, что по умолчанию необходимо использовать Камелкасинг на клиенте, даже если на сервере используется имя метода Pascal.</span><span class="sxs-lookup"><span data-stu-id="2b449-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="2b449-273">Правило Камелкасинг применяется только к методам, а не к объектам.</span><span class="sxs-lookup"><span data-stu-id="2b449-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="2b449-274">Например, вы ссылаетесь на `stock.Symbol` и `stock.Price`, а не на `stock.symbol` или `stock.price`.</span><span class="sxs-lookup"><span data-stu-id="2b449-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="2b449-275">В методе `init` приложение создает HTML для строки таблицы для каждого объекта, полученного с сервера, вызывая `formatStock` для форматирования свойств объекта `stock`, а затем вызывая `supplant` для замены заполнителей в переменной `rowTemplate` значениями свойства `stock` объекта.</span><span class="sxs-lookup"><span data-stu-id="2b449-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="2b449-276">Затем полученный код HTML добавляется в таблицу запасов.</span><span class="sxs-lookup"><span data-stu-id="2b449-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="2b449-277">Вызовите `init`, передав его в качестве функции `callback`, которая выполняется после завершения асинхронной функции `start`.</span><span class="sxs-lookup"><span data-stu-id="2b449-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="2b449-278">Если вы вызывали `init` как отдельную инструкцию JavaScript после вызова `start`, функция завершится ошибкой, так как она будет выполняться немедленно, не дожидаясь завершения установки соединения функцией start.</span><span class="sxs-lookup"><span data-stu-id="2b449-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="2b449-279">В этом случае функция `init` будет пытаться вызвать функцию `getAllStocks`, прежде чем приложение установит соединение с сервером.</span><span class="sxs-lookup"><span data-stu-id="2b449-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="2b449-280">Получение обновленных цен на акции</span><span class="sxs-lookup"><span data-stu-id="2b449-280">Getting updated stock prices</span></span>

<span data-ttu-id="2b449-281">Когда сервер изменяет цену на акцию, он вызывает `updateStockPrice` на подключенных клиентах.</span><span class="sxs-lookup"><span data-stu-id="2b449-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="2b449-282">Приложение добавляет функцию в свойство клиента прокси-сервера `stockTicker`, чтобы сделать его доступным для вызовов с сервера.</span><span class="sxs-lookup"><span data-stu-id="2b449-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="2b449-283">Функция `updateStockPrice` форматирует объект, полученный с сервера, в строку таблицы таким же образом, как и в функции `init`.</span><span class="sxs-lookup"><span data-stu-id="2b449-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="2b449-284">Вместо того чтобы добавлять строку в таблицу, она находит текущую строку складского запаса в таблице и заменяет эту строку новой.</span><span class="sxs-lookup"><span data-stu-id="2b449-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="2b449-285">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="2b449-285">Test the application</span></span>

<span data-ttu-id="2b449-286">Вы можете протестировать приложение, чтобы убедиться, что оно работает.</span><span class="sxs-lookup"><span data-stu-id="2b449-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="2b449-287">Вы увидите, что все окна браузера отображаются в реальной таблице акций с неизменными ценами акций.</span><span class="sxs-lookup"><span data-stu-id="2b449-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="2b449-288">На панели инструментов включите **отладку скриптов** , а затем нажмите кнопку Воспроизведение, чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="2b449-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![Снимок экрана: Включение режима отладки пользователем и выбор воспроизведения.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="2b449-290">Откроется окно браузера, в котором отображается **Таблица текущих запасов**.</span><span class="sxs-lookup"><span data-stu-id="2b449-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="2b449-291">В таблице «акции» первоначально отображается «загрузка...» После короткого времени приложение отобразит начальные данные о акции, а затем цены на акции начнут изменяться.</span><span class="sxs-lookup"><span data-stu-id="2b449-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="2b449-292">Скопируйте URL-адрес из браузера, откройте два других браузера и вставьте URL-адреса в адреса строки.</span><span class="sxs-lookup"><span data-stu-id="2b449-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="2b449-293">Начальное отображение запасов аналогично первому браузеру, и изменения происходят одновременно.</span><span class="sxs-lookup"><span data-stu-id="2b449-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="2b449-294">Закройте все браузеры, откройте новый браузер и перейдите к тому же URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="2b449-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="2b449-295">Одноэлементный объект Стокктиккер продолжает выполняться на сервере.</span><span class="sxs-lookup"><span data-stu-id="2b449-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="2b449-296">В **таблице «Live Stock** » показано, что акции продолжают изменяться.</span><span class="sxs-lookup"><span data-stu-id="2b449-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="2b449-297">Вы не видите начальную таблицу с нулевыми рисунками изменений.</span><span class="sxs-lookup"><span data-stu-id="2b449-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="2b449-298">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="2b449-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="2b449-299">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="2b449-299">Enable logging</span></span>

<span data-ttu-id="2b449-300">SignalR имеет встроенную функцию ведения журнала, которую можно включить на клиенте, чтобы помочь в устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="2b449-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="2b449-301">В этом разделе описано, как включить ведение журнала, и просмотреть примеры, демонстрирующие, как журналы указывают, какие из следующих методов транспорта использует SignalR:</span><span class="sxs-lookup"><span data-stu-id="2b449-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="2b449-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), поддерживаемые службами IIS 8 и текущими браузерами.</span><span class="sxs-lookup"><span data-stu-id="2b449-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="2b449-303">[События, отправленные сервером](http://en.wikipedia.org/wiki/Server-sent_events), поддерживаются обозревателями, отличными от Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="2b449-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="2b449-304">[Непрерывная рамка](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), поддерживаемая Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="2b449-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="2b449-305">[Длинный опрос Ajax](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), поддерживаемый всеми браузерами.</span><span class="sxs-lookup"><span data-stu-id="2b449-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="2b449-306">Для любого заданного соединения SignalR выбирает лучший метод транспортировки, который поддерживает сервер и клиент.</span><span class="sxs-lookup"><span data-stu-id="2b449-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="2b449-307">Откройте *стокктиккер. js*.</span><span class="sxs-lookup"><span data-stu-id="2b449-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="2b449-308">Добавьте эту выделенную строку кода, чтобы включить ведение журнала непосредственно перед кодом, который инициализирует подключение в конце файла:</span><span class="sxs-lookup"><span data-stu-id="2b449-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="2b449-309">Нажмите клавишу **F5**, чтобы запустить проект.</span><span class="sxs-lookup"><span data-stu-id="2b449-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="2b449-310">Откройте окно средств разработчика в браузере и выберите консоль, чтобы просмотреть журналы.</span><span class="sxs-lookup"><span data-stu-id="2b449-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="2b449-311">Может потребоваться обновить страницу, чтобы просмотреть журналы SignalR, согласования транспортного метода для нового подключения.</span><span class="sxs-lookup"><span data-stu-id="2b449-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="2b449-312">Если вы используете Internet Explorer 10 в Windows 8 (IIS 8), метод транспорта — это **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="2b449-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="2b449-313">Если вы используете Internet Explorer 10 в Windows 7 (IIS 7,5), то транспортным методом является **IFRAME**.</span><span class="sxs-lookup"><span data-stu-id="2b449-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="2b449-314">Если вы используете Firefox 19 в Windows 8 (IIS 8), метод транспорта — это **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="2b449-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="2b449-315">В браузере Firefox установите надстройку Firebug, чтобы получить окно консоли.</span><span class="sxs-lookup"><span data-stu-id="2b449-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="2b449-316">Если вы используете Firefox 19 в Windows 7 (IIS 7,5), метод перевозки является **серверными** событиями.</span><span class="sxs-lookup"><span data-stu-id="2b449-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="2b449-317">Установка образца Стокктиккер</span><span class="sxs-lookup"><span data-stu-id="2b449-317">Install the StockTicker sample</span></span>

<span data-ttu-id="2b449-318">[Пакет Microsoft. AspNet. SignalR. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) устанавливает приложение стокктиккер.</span><span class="sxs-lookup"><span data-stu-id="2b449-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="2b449-319">Пакет NuGet содержит больше возможностей, чем упрощенная версия, созданная с нуля.</span><span class="sxs-lookup"><span data-stu-id="2b449-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="2b449-320">В этом разделе руководства вы установите пакет NuGet и ознакомьтесь с новыми функциями и кодом, который их реализует.</span><span class="sxs-lookup"><span data-stu-id="2b449-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b449-321">Если пакет устанавливается без выполнения предыдущих шагов этого руководства, необходимо добавить в проект класс запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="2b449-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="2b449-322">Этот шаг объясняется в этом файле readme. txt для пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="2b449-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="2b449-323">Установите пакет NuGet с SignalR. Sample.</span><span class="sxs-lookup"><span data-stu-id="2b449-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="2b449-324">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2b449-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="2b449-325">В **диспетчере пакетов NuGet: SignalR. стокктиккер**нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="2b449-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="2b449-326">В **источнике пакета**выберите **NuGet.org**.</span><span class="sxs-lookup"><span data-stu-id="2b449-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="2b449-327">Введите *SignalR. Sample* в поле поиска и выберите **Microsoft. AspNet. signalr. Sample** > **установить**.</span><span class="sxs-lookup"><span data-stu-id="2b449-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="2b449-328">В **Обозреватель решений**разверните папку *SignalR. Sample* .</span><span class="sxs-lookup"><span data-stu-id="2b449-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="2b449-329">Установка пакета SignalR. SAMPLED создала папку и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="2b449-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="2b449-330">В папке *SignalR. Sample* щелкните правой кнопкой мыши *стокктиккер. HTML*и выберите **задать в качестве начальной страницы**.</span><span class="sxs-lookup"><span data-stu-id="2b449-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2b449-331">Установка SignalR. пример пакета NuGet может изменить версию jQuery в папке *Scripts* .</span><span class="sxs-lookup"><span data-stu-id="2b449-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="2b449-332">Новый файл *стокктиккер. HTML* , устанавливаемый пакетом в папке *SignalR. Sample* , будет синхронизирован с версией jQuery, устанавливаемой пакетом, но если вы хотите снова запустить исходный файл *стокктиккер. HTML* , то, возможно, потребуется сначала обновить ссылку JQuery в теге script.</span><span class="sxs-lookup"><span data-stu-id="2b449-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="2b449-333">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="2b449-333">Run the application</span></span>

 <span data-ttu-id="2b449-334">В таблице, которую вы видели в первом приложении, приходилось использовать полезные функции.</span><span class="sxs-lookup"><span data-stu-id="2b449-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="2b449-335">В полном приложении для биржевых котировок отображаются новые функции: окно с горизонтальной прокруткой, которое показывает биржевые данные и акции, изменяющие цвет по мере увеличения и падения.</span><span class="sxs-lookup"><span data-stu-id="2b449-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="2b449-336">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="2b449-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="2b449-337">При первом запуске приложения «Market» является «закрытым», и отображается статическая таблица и окно, которое не прокручивается.</span><span class="sxs-lookup"><span data-stu-id="2b449-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="2b449-338">Выберите **Открыть рыночный**.</span><span class="sxs-lookup"><span data-stu-id="2b449-338">Select **Open Market**.</span></span>

    ![Снимок экрана: Live Tick.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="2b449-340">В реальном времени поле " **Биржевая сводка** " начинает прокручиваться по горизонтали, и сервер начинает периодически рассылать изменения цены акций на случайном уровне.</span><span class="sxs-lookup"><span data-stu-id="2b449-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="2b449-341">При каждом изменении цены на акцию приложение обновляет как **таблицу запасов в реальном** времени, так и **действующее биржевое деление**.</span><span class="sxs-lookup"><span data-stu-id="2b449-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="2b449-342">Если изменение цены на фондовой бирже положительно, приложение отображает акции с зеленым фоном.</span><span class="sxs-lookup"><span data-stu-id="2b449-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="2b449-343">Если изменение отрицательное, приложение отображает на бумаге красный фон.</span><span class="sxs-lookup"><span data-stu-id="2b449-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="2b449-344">Выберите **закрыть рыночный**.</span><span class="sxs-lookup"><span data-stu-id="2b449-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="2b449-345">Обновление таблицы останавливается.</span><span class="sxs-lookup"><span data-stu-id="2b449-345">The table updates stop.</span></span>

    * <span data-ttu-id="2b449-346">Деление останавливает прокрутку.</span><span class="sxs-lookup"><span data-stu-id="2b449-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="2b449-347">Выберите **сбросить**.</span><span class="sxs-lookup"><span data-stu-id="2b449-347">Select **Reset**.</span></span>

    * <span data-ttu-id="2b449-348">Все данные о запасах сбрасываются.</span><span class="sxs-lookup"><span data-stu-id="2b449-348">All stock data is reset.</span></span>

    * <span data-ttu-id="2b449-349">Приложение восстанавливает начальное состояние до начала изменения цены.</span><span class="sxs-lookup"><span data-stu-id="2b449-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="2b449-350">Скопируйте URL-адрес из браузера, откройте два других браузера и вставьте URL-адреса в адреса строки.</span><span class="sxs-lookup"><span data-stu-id="2b449-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="2b449-351">Вы увидите, что одни и те же данные динамически обновляются в каждом браузере.</span><span class="sxs-lookup"><span data-stu-id="2b449-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="2b449-352">При выборе любого из элементов управления все браузеры реагируют одинаково в одно и то же время.</span><span class="sxs-lookup"><span data-stu-id="2b449-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="2b449-353">Отображение биржевых котировок в реальном времени</span><span class="sxs-lookup"><span data-stu-id="2b449-353">Live Stock Ticker display</span></span>

<span data-ttu-id="2b449-354">В **реальном времени** отображается неупорядоченный список в элементе `<div>`, форматированном в одну строку в стиле CSS.</span><span class="sxs-lookup"><span data-stu-id="2b449-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="2b449-355">Приложение инициализирует и обновляет Tick так же, как и таблица: заменяя заполнители в строке шаблона `<li>` и динамически добавляя элементы `<li>` в элемент `<ul>`.</span><span class="sxs-lookup"><span data-stu-id="2b449-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="2b449-356">Приложение включает прокрутку с помощью функции jQuery `animate` для изменения левого поля неупорядоченного списка в `<div>`.</span><span class="sxs-lookup"><span data-stu-id="2b449-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="2b449-357">SignalR. пример Стокктиккер. HTML</span><span class="sxs-lookup"><span data-stu-id="2b449-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="2b449-358">HTML-код биржевых котировок:</span><span class="sxs-lookup"><span data-stu-id="2b449-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="2b449-359">SignalR. Sample Стокктиккер. CSS</span><span class="sxs-lookup"><span data-stu-id="2b449-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="2b449-360">Код CSS для биржевых котировок:</span><span class="sxs-lookup"><span data-stu-id="2b449-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="2b449-361">SignalR. Sample SignalR. Стокктиккер. js</span><span class="sxs-lookup"><span data-stu-id="2b449-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="2b449-362">Код jQuery, который выполняет прокрутку:</span><span class="sxs-lookup"><span data-stu-id="2b449-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="2b449-363">Дополнительные методы на сервере, который может вызывать клиент</span><span class="sxs-lookup"><span data-stu-id="2b449-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="2b449-364">Для обеспечения гибкости приложения существуют дополнительные методы, которые может вызывать приложение.</span><span class="sxs-lookup"><span data-stu-id="2b449-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="2b449-365">SignalR. пример StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="2b449-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="2b449-366">Класс `StockTickerHub` определяет четыре дополнительных метода, которые может вызывать клиент:</span><span class="sxs-lookup"><span data-stu-id="2b449-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="2b449-367">Приложение вызывает `OpenMarket`, `CloseMarket`и `Reset` в ответ на кнопки в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="2b449-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="2b449-368">Они демонстрируют шаблон одного клиента, запускающего изменение состояния, немедленно распространяемого на все клиенты.</span><span class="sxs-lookup"><span data-stu-id="2b449-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="2b449-369">Каждый из этих методов вызывает метод в классе `StockTicker`, который вызывает изменение состояния рынка, а затем передает новое состояние.</span><span class="sxs-lookup"><span data-stu-id="2b449-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="2b449-370">SignalR. пример StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="2b449-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="2b449-371">В классе `StockTicker` приложение поддерживает состояние рынка со свойством `MarketState`, возвращающим значение перечисления `MarketState`.</span><span class="sxs-lookup"><span data-stu-id="2b449-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="2b449-372">Каждый из методов, изменяющих состояние рынка, выполняет это в блоке блокировки, так как класс `StockTicker` должен быть потокобезопасным:</span><span class="sxs-lookup"><span data-stu-id="2b449-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="2b449-373">Чтобы убедиться в том, что этот код является потокобезопасным, `_marketState` поле, которое обеспечивает свойство `MarketState`, назначенное `volatile`:</span><span class="sxs-lookup"><span data-stu-id="2b449-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="2b449-374">Методы `BroadcastMarketStateChange` и `BroadcastMarketReset` похожи на метод Броадкастстоккприце, который вы уже видели, за исключением того, что они вызывают различные методы, определенные на клиенте:</span><span class="sxs-lookup"><span data-stu-id="2b449-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="2b449-375">Дополнительные функции на клиенте, который может вызывать сервер</span><span class="sxs-lookup"><span data-stu-id="2b449-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="2b449-376">Функция `updateStockPrice` теперь обрабатывает как таблицу, так и отображение импульсов и использует `jQuery.Color` для красных и зеленых цветов Flash.</span><span class="sxs-lookup"><span data-stu-id="2b449-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="2b449-377">Новые функции в *SignalR. стокктиккер. js* включают и отключают кнопки на основе состояния рынка.</span><span class="sxs-lookup"><span data-stu-id="2b449-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="2b449-378">Они также останавливают или начинают прямую прокрутку **биржевых котировок** .</span><span class="sxs-lookup"><span data-stu-id="2b449-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="2b449-379">Так как многие функции добавляются в `ticker.client`, приложение использует [функцию расширения jQuery](http://api.jquery.com/jQuery.extend/) для их добавления.</span><span class="sxs-lookup"><span data-stu-id="2b449-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="2b449-380">Дополнительные настройки клиента после установления соединения</span><span class="sxs-lookup"><span data-stu-id="2b449-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="2b449-381">После установления подключения клиент имеет некоторую дополнительную работу:</span><span class="sxs-lookup"><span data-stu-id="2b449-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="2b449-382">Выясните, открыт или закрыт ли данный рынк, чтобы вызвать соответствующую функцию `marketOpened` или `marketClosed`.</span><span class="sxs-lookup"><span data-stu-id="2b449-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="2b449-383">Присоедините вызовы серверных методов к кнопкам.</span><span class="sxs-lookup"><span data-stu-id="2b449-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="2b449-384">Методы сервера не привязаны к кнопкам до тех пор, пока приложение не установит подключение.</span><span class="sxs-lookup"><span data-stu-id="2b449-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="2b449-385">Так что код не может вызывать методы сервера, прежде чем они будут доступны.</span><span class="sxs-lookup"><span data-stu-id="2b449-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b449-386">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2b449-386">Additional resources</span></span>

<span data-ttu-id="2b449-387">В этом учебнике вы узнали, как программировать приложение SignalR, которое передает сообщения с сервера на все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="2b449-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="2b449-388">Теперь можно периодически выполнять широковещательную трансляцию сообщений и в ответ на уведомления от любого клиента.</span><span class="sxs-lookup"><span data-stu-id="2b449-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="2b449-389">Концепцию многопотокового одноэлементного экземпляра можно использовать для сохранения состояния сервера в сценариях Интернет-игр с несколькими игроками.</span><span class="sxs-lookup"><span data-stu-id="2b449-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="2b449-390">Пример см. в разделе [игра по воссозданию на основе SignalR](https://github.com/NTaylorMullen/ShootR).</span><span class="sxs-lookup"><span data-stu-id="2b449-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="2b449-391">Учебники, в которых показаны одноранговые сценарии связи, см. в разделе [Начало работы с SignalR](introduction-to-signalr.md) и [обновлением в режиме реального времени с помощью SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="2b449-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="2b449-392">Дополнительные сведения о SignalR см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="2b449-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="2b449-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="2b449-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="2b449-394">Проект SignalR</span><span class="sxs-lookup"><span data-stu-id="2b449-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="2b449-395">GitHub и примеры SignalR</span><span class="sxs-lookup"><span data-stu-id="2b449-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="2b449-396">Вики-сайт SignalR</span><span class="sxs-lookup"><span data-stu-id="2b449-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="2b449-397">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b449-397">Next steps</span></span>

<span data-ttu-id="2b449-398">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="2b449-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b449-399">Создал проект</span><span class="sxs-lookup"><span data-stu-id="2b449-399">Created the project</span></span>
> * <span data-ttu-id="2b449-400">Настройка кода сервера</span><span class="sxs-lookup"><span data-stu-id="2b449-400">Set up the server code</span></span>
> * <span data-ttu-id="2b449-401">Анализ кода сервера</span><span class="sxs-lookup"><span data-stu-id="2b449-401">Examined the server code</span></span>
> * <span data-ttu-id="2b449-402">Настройка клиентского кода</span><span class="sxs-lookup"><span data-stu-id="2b449-402">Set up the client code</span></span>
> * <span data-ttu-id="2b449-403">Анализ кода клиента</span><span class="sxs-lookup"><span data-stu-id="2b449-403">Examined the client code</span></span>
> * <span data-ttu-id="2b449-404">тестирование приложения.</span><span class="sxs-lookup"><span data-stu-id="2b449-404">Tested the application</span></span>
> * <span data-ttu-id="2b449-405">Ведение журнала включено</span><span class="sxs-lookup"><span data-stu-id="2b449-405">Enabled logging</span></span>

<span data-ttu-id="2b449-406">Перейдите к следующей статье, чтобы узнать, как создать веб-приложение в режиме реального времени, использующее ASP.NET SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="2b449-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2b449-407">Создание веб-приложения в режиме реального времени с помощью SignalR</span><span class="sxs-lookup"><span data-stu-id="2b449-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
