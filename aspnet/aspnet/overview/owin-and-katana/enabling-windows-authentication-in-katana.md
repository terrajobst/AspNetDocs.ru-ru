---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Включение проверки подлинности Windows в Katana | Документация Майкрософт
author: MikeWasson
description: В этой статье показано, как включить проверку подлинности Windows в Katana. Он охватывает два сценария. С помощью служб IIS для размещения Katana и с помощью HttpListener для резидентного размещения Kat...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 8afa2c9dfbe03a9874513f7d083adf7608f4218f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041111"
---
<a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="feb19-104">Включение проверки подлинности Windows в Katana</span><span class="sxs-lookup"><span data-stu-id="feb19-104">Enabling Windows Authentication in Katana</span></span>
====================
<span data-ttu-id="feb19-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="feb19-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="feb19-106">В этой статье показано, как включить проверку подлинности Windows в Katana.</span><span class="sxs-lookup"><span data-stu-id="feb19-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="feb19-107">Он охватывает два сценария. С помощью служб IIS для размещения Katana и с помощью HttpListener для резидентного размещения Katana в пользовательском процессе.</span><span class="sxs-lookup"><span data-stu-id="feb19-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="feb19-108">Благодаря Barry Dorrans, Дэвид Matson и Крис Росс за рецензирование этой статьи.</span><span class="sxs-lookup"><span data-stu-id="feb19-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>


<span data-ttu-id="feb19-109">Katana — это реализованный корпорацией Майкрософт [OWIN](http://owin.org/), Open Web Interface для .NET.</span><span class="sxs-lookup"><span data-stu-id="feb19-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="feb19-110">Дополнительные общие сведения о OWIN и Katana [здесь](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="feb19-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="feb19-111">Архитектура OWIN имеет несколько уровней:</span><span class="sxs-lookup"><span data-stu-id="feb19-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="feb19-112">Узел: Управляет процессом, в котором выполняется в конвейер OWIN.</span><span class="sxs-lookup"><span data-stu-id="feb19-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="feb19-113">Сервер: Открывает к сетевому сокету и прослушивает запросы.</span><span class="sxs-lookup"><span data-stu-id="feb19-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="feb19-114">По промежуточного слоя: Обрабатывает HTTP-запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="feb19-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="feb19-115">Katana в настоящее время предоставляет два сервера, каждый из которых поддерживает встроенную проверку подлинности Windows:</span><span class="sxs-lookup"><span data-stu-id="feb19-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="feb19-116">**Microsoft.Owin.Host.SystemWeb**.</span><span class="sxs-lookup"><span data-stu-id="feb19-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="feb19-117">Использует IIS с конвейером ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="feb19-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="feb19-118">**Microsoft.Owin.Host.HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="feb19-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="feb19-119">Использует [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="feb19-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="feb19-120">Этот сервер в настоящее время является параметром по умолчанию, при резидентном размещении Katana.</span><span class="sxs-lookup"><span data-stu-id="feb19-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="feb19-121">Katana не поддерживает в настоящее время по промежуточного слоя OWIN для проверки подлинности Windows, так как эта функция уже доступна на серверах.</span><span class="sxs-lookup"><span data-stu-id="feb19-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>

## <a name="windows-authentication-in-iis"></a><span data-ttu-id="feb19-122">Проверка подлинности Windows в IIS</span><span class="sxs-lookup"><span data-stu-id="feb19-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="feb19-123">С помощью Microsoft.Owin.Host.SystemWeb, можно просто включить проверку подлинности Windows в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="feb19-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="feb19-124">Начнем с создания нового приложения ASP.NET, с помощью шаблона проекта «Пустой веб-приложение ASP.NET».</span><span class="sxs-lookup"><span data-stu-id="feb19-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="feb19-125">Добавьте пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="feb19-125">Next, add NuGet packages.</span></span> <span data-ttu-id="feb19-126">Из **средства** меню, выберите **диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="feb19-126">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="feb19-127">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="feb19-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="feb19-128">Теперь добавьте класс с именем `Startup` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="feb19-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="feb19-129">Это все, чтобы создать приложение «Hello world» для OWIN, выполняющегося на сервере IIS.</span><span class="sxs-lookup"><span data-stu-id="feb19-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="feb19-130">Нажмите клавишу F5, чтобы начать отладку приложения.</span><span class="sxs-lookup"><span data-stu-id="feb19-130">Press F5 to debug the application.</span></span> <span data-ttu-id="feb19-131">Вы увидите сообщение «Hello World!»</span><span class="sxs-lookup"><span data-stu-id="feb19-131">You should see "Hello World!"</span></span> <span data-ttu-id="feb19-132">в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="feb19-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="feb19-133">Затем мы будем включите проверку подлинности Windows в IIS Express.</span><span class="sxs-lookup"><span data-stu-id="feb19-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="feb19-134">Из **представление** меню, выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="feb19-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="feb19-135">Щелкните имя проекта в обозревателе решений, чтобы просмотреть свойства проекта.</span><span class="sxs-lookup"><span data-stu-id="feb19-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="feb19-136">В **свойства** окне **анонимную проверку подлинности** для **отключено** и задайте **проверки подлинности Windows** для  **Включить**.</span><span class="sxs-lookup"><span data-stu-id="feb19-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="feb19-137">При запуске приложения из Visual Studio, IIS Express потребуется учетные данные пользователя Windows.</span><span class="sxs-lookup"><span data-stu-id="feb19-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="feb19-138">Это можно увидеть с помощью [Fiddler](http://fiddler2.com/home) или другой средство отладки HTTP.</span><span class="sxs-lookup"><span data-stu-id="feb19-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="feb19-139">Ниже приведен пример ответа HTTP:</span><span class="sxs-lookup"><span data-stu-id="feb19-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="feb19-140">В этом ответе заголовки WWW-Authenticate указывают, что сервер поддерживает [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) протокола, который использует Kerberos или NTLM.</span><span class="sxs-lookup"><span data-stu-id="feb19-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="feb19-141">Позже, при развертывании приложения на сервере, выполните [эти действия](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) для включения проверки подлинности Windows в службах IIS на этом сервере.</span><span class="sxs-lookup"><span data-stu-id="feb19-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="feb19-142">Проверка подлинности Windows в HttpListener</span><span class="sxs-lookup"><span data-stu-id="feb19-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="feb19-143">Если вы используете Microsoft.Owin.Host.HttpListener для резидентного размещения Katana, проверку подлинности Windows можно включить непосредственно на **HttpListener** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="feb19-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="feb19-144">Во-первых создайте новое консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="feb19-144">First, create a new console application.</span></span> <span data-ttu-id="feb19-145">Добавьте пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="feb19-145">Next, add NuGet packages.</span></span> <span data-ttu-id="feb19-146">Из **средства** меню, выберите **диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="feb19-146">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="feb19-147">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="feb19-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="feb19-148">Теперь добавьте класс с именем `Startup` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="feb19-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="feb19-149">Этот класс реализует тот же пример «Hello world», от и до, но он также задает проверку подлинности Windows схемы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="feb19-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="feb19-150">Внутри `Main` функцию, запустите конвейер OWIN:</span><span class="sxs-lookup"><span data-stu-id="feb19-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="feb19-151">Можно отправить запрос в Fiddler, чтобы убедиться, что приложение использует проверку подлинности Windows:</span><span class="sxs-lookup"><span data-stu-id="feb19-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="feb19-152">См. также</span><span class="sxs-lookup"><span data-stu-id="feb19-152">Related Topics</span></span>

[<span data-ttu-id="feb19-153">Обзор проекта Katana</span><span class="sxs-lookup"><span data-stu-id="feb19-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="feb19-154">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="feb19-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="feb19-155">Основные сведения о проверки подлинности форм OWIN в MVC 5</span><span class="sxs-lookup"><span data-stu-id="feb19-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
