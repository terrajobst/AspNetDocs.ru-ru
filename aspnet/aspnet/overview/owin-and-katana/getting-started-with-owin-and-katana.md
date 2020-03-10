---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: начало работы с OWIN и Katana | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472446"
---
# <a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="fff56-102">Начало работы с OWIN и Katana</span><span class="sxs-lookup"><span data-stu-id="fff56-102">Getting Started with OWIN and Katana</span></span>

<span data-ttu-id="fff56-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fff56-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fff56-104">[Открытый веб-интерфейс для .NET (OWIN)](http://owin.org/) определяет абстракцию между веб-серверами и веб-приложениями .NET.</span><span class="sxs-lookup"><span data-stu-id="fff56-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="fff56-105">Отделив веб-сервер от приложения, OWIN упрощает создание по промежуточного слоя для разработки веб-приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="fff56-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="fff56-106">Кроме того, OWIN упрощает перенос веб-приложений на другие узлы&#8212;, например для размещения в службе Windows или в другом процессе.</span><span class="sxs-lookup"><span data-stu-id="fff56-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="fff56-107">OWIN является спецификацией, принадлежащей сообществом, а не реализацией.</span><span class="sxs-lookup"><span data-stu-id="fff56-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="fff56-108">Проект Katana — это набор компонентов OWIN с открытым исходным кодом, разработанный корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="fff56-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="fff56-109">Общие сведения о OWIN и Katana см. [в обзоре проекта Katana](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="fff56-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="fff56-110">В этой статье я буду сразу перейти к коду, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="fff56-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="fff56-111">В этом руководстве используется [версия-кандидат Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566), но можно также использовать Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="fff56-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="fff56-112">Некоторые шаги отличаются в Visual Studio 2012, о которых я расмечу ниже.</span><span class="sxs-lookup"><span data-stu-id="fff56-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="fff56-113">Размещение OWIN в IIS</span><span class="sxs-lookup"><span data-stu-id="fff56-113">Host OWIN in IIS</span></span>

<span data-ttu-id="fff56-114">В этом разделе мы будем размещать OWIN в IIS.</span><span class="sxs-lookup"><span data-stu-id="fff56-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="fff56-115">Этот параметр обеспечивает гибкость и компонуемости конвейера OWIN вместе с развитым набором функций IIS.</span><span class="sxs-lookup"><span data-stu-id="fff56-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="fff56-116">При использовании этого параметра приложение OWIN выполняется в конвейере запросов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fff56-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="fff56-117">Сначала создайте новый проект веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fff56-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="fff56-118">(В Visual Studio 2012 используйте тип проекта ASP.NET Empty веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="fff56-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="fff56-119">В диалоговом окне **Новый проект ASP.NET** выберите **пустой** шаблон.</span><span class="sxs-lookup"><span data-stu-id="fff56-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="fff56-120">Добавление пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="fff56-120">Add NuGet Packages</span></span>

<span data-ttu-id="fff56-121">Затем добавьте необходимые пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="fff56-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="fff56-122">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="fff56-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="fff56-123">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fff56-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="fff56-124">Добавление класса запуска</span><span class="sxs-lookup"><span data-stu-id="fff56-124">Add a Startup Class</span></span>

<span data-ttu-id="fff56-125">Затем добавьте класс запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="fff56-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="fff56-126">В обозреватель решений щелкните правой кнопкой мыши проект и выберите **Добавить**, а затем выберите **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="fff56-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="fff56-127">В диалоговом окне **Добавление нового элемента** выберите **класс запуска Owin**.</span><span class="sxs-lookup"><span data-stu-id="fff56-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="fff56-128">Дополнительные сведения о настройке класса Startup см. в разделе [Обнаружение класса запуска OWIN](owin-startup-class-detection.md).</span><span class="sxs-lookup"><span data-stu-id="fff56-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="fff56-129">Добавьте в метод `Startup1.Configuration` следующий код:</span><span class="sxs-lookup"><span data-stu-id="fff56-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="fff56-130">Этот код добавляет к конвейеру OWIN простую часть по промежуточного слоя, реализованную в виде функции, получающей экземпляр **Microsoft. OWIN. иовинконтекст** .</span><span class="sxs-lookup"><span data-stu-id="fff56-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="fff56-131">Когда сервер получает HTTP-запрос, конвейер OWIN вызывает по промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="fff56-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="fff56-132">По промежуточного слоя задает тип содержимого для ответа и записывает текст ответа.</span><span class="sxs-lookup"><span data-stu-id="fff56-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="fff56-133">Шаблон класса Startup OWIN доступен в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="fff56-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="fff56-134">Если вы используете Visual Studio 2012, просто добавьте новый пустой класс с именем `Startup1`и вставьте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="fff56-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="fff56-135">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="fff56-135">Run the Application</span></span>

<span data-ttu-id="fff56-136">Нажмите клавишу F5, чтобы начать отладку.</span><span class="sxs-lookup"><span data-stu-id="fff56-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="fff56-137">Visual Studio откроет окно браузера для `http://localhost:*port*/`.</span><span class="sxs-lookup"><span data-stu-id="fff56-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="fff56-138">Страница должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fff56-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="fff56-139">OWIN с самостоятельным размещением в консольном приложении</span><span class="sxs-lookup"><span data-stu-id="fff56-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="fff56-140">Это приложение легко преобразовать из IIS, размещенного в собственном размещении, в пользовательском процессе.</span><span class="sxs-lookup"><span data-stu-id="fff56-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="fff56-141">При размещении IIS службы IIS действуют как как HTTP-сервер, так и как процесс, в котором размещена служба.</span><span class="sxs-lookup"><span data-stu-id="fff56-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="fff56-142">В собственном размещении приложение создает процесс и использует класс **HttpListener** в качестве HTTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="fff56-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="fff56-143">Создайте новое консольное приложение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fff56-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="fff56-144">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fff56-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="fff56-145">Добавьте класс `Startup1` из части 1 этого учебника в проект.</span><span class="sxs-lookup"><span data-stu-id="fff56-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="fff56-146">Вам не нужно изменять этот класс.</span><span class="sxs-lookup"><span data-stu-id="fff56-146">You don't need to modify this class.</span></span>

<span data-ttu-id="fff56-147">Реализуйте метод `Main` приложения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="fff56-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="fff56-148">При запуске консольного приложения сервер начинает прослушивание `http://localhost:9000`.</span><span class="sxs-lookup"><span data-stu-id="fff56-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="fff56-149">При переходе по этому адресу в веб-браузере отображается страница "Hello World".</span><span class="sxs-lookup"><span data-stu-id="fff56-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="fff56-150">Добавить диагностику OWIN</span><span class="sxs-lookup"><span data-stu-id="fff56-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="fff56-151">Пакет Microsoft. Owin. Diagnostics содержит по промежуточного слоя, которое перехватывает необработанные исключения и отображает HTML-страницу со сведениями об ошибке.</span><span class="sxs-lookup"><span data-stu-id="fff56-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="fff56-152">Эта страница работает примерно так же, как страница ошибок ASP.NET, которая иногда называется «[желтым экраном смерти](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)» (исод).</span><span class="sxs-lookup"><span data-stu-id="fff56-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="fff56-153">Как и ИСОД, страница ошибки Katana полезна во время разработки, но ее рекомендуется отключить в рабочем режиме.</span><span class="sxs-lookup"><span data-stu-id="fff56-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="fff56-154">Чтобы установить пакет диагностики в проекте, введите в окне консоли диспетчера пакетов следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fff56-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="fff56-155">Измените код в методе `Startup1.Configuration` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fff56-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="fff56-156">Теперь используйте сочетание клавиш CTRL + F5 для запуска приложения без отладки, чтобы Visual Studio не нарушала исключение.</span><span class="sxs-lookup"><span data-stu-id="fff56-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="fff56-157">Приложение ведет себя так же, как и раньше, пока вы не перейдите к `http://localhost/fail`, после чего приложение создаст исключение.</span><span class="sxs-lookup"><span data-stu-id="fff56-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="fff56-158">По промежуточного слоя страницы ошибки будет перехватывать исключение и отображать HTML-страницу со сведениями об ошибке.</span><span class="sxs-lookup"><span data-stu-id="fff56-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="fff56-159">Можно щелкнуть вкладки, чтобы просмотреть стек, строку запроса, файлы cookie, заголовок запроса и переменные среды OWIN.</span><span class="sxs-lookup"><span data-stu-id="fff56-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="fff56-160">Next Steps</span><span class="sxs-lookup"><span data-stu-id="fff56-160">Next Steps</span></span>

- [<span data-ttu-id="fff56-161">Определение класса запуска OWIN</span><span class="sxs-lookup"><span data-stu-id="fff56-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="fff56-162">Использование OWIN для самостоятельного размещения веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fff56-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="fff56-163">Использование OWIN для самостоятельного размещения SignalR</span><span class="sxs-lookup"><span data-stu-id="fff56-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
