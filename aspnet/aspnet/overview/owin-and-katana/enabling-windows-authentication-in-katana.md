---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Включение проверки подлинности Windows в Katana | Документация Майкрософт
author: MikeWasson
description: 'В этой статье показано, как включить проверку подлинности Windows в Katana. В нем рассматриваются два сценария: Использование IIS для размещения Katana и использование HttpListener для самостоятельного размещения Kat...'
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500298"
---
# <a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="019bc-104">Включение проверки подлинности Windows в Katana</span><span class="sxs-lookup"><span data-stu-id="019bc-104">Enabling Windows Authentication in Katana</span></span>

<span data-ttu-id="019bc-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="019bc-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="019bc-106">В этой статье показано, как включить проверку подлинности Windows в Katana.</span><span class="sxs-lookup"><span data-stu-id="019bc-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="019bc-107">В нем рассматриваются два сценария: Использование IIS для размещения Katana и использование HttpListener для самостоятельного размещения Katana в пользовательском процессе.</span><span class="sxs-lookup"><span data-stu-id="019bc-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="019bc-108">Спасибо Барри Доррансом, Дэвид Матсон и Крис Росс (для ознакомления с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="019bc-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>

<span data-ttu-id="019bc-109">Katana — это реализация [OWIN](http://owin.org/)Майкрософт с открытым веб-интерфейсом для .NET.</span><span class="sxs-lookup"><span data-stu-id="019bc-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="019bc-110">Вы можете ознакомиться с введением в OWIN и Katana [здесь](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="019bc-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="019bc-111">Архитектура OWIN имеет несколько уровней:</span><span class="sxs-lookup"><span data-stu-id="019bc-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="019bc-112">Узел. управляет процессом, в котором выполняется конвейер OWIN.</span><span class="sxs-lookup"><span data-stu-id="019bc-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="019bc-113">Сервер: открывает сетевой сокет и прослушивает запросы.</span><span class="sxs-lookup"><span data-stu-id="019bc-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="019bc-114">По промежуточного слоя: обрабатывает HTTP-запрос и ответ.</span><span class="sxs-lookup"><span data-stu-id="019bc-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="019bc-115">В настоящее время Katana предоставляет два сервера, оба из которых поддерживают встроенную проверку подлинности Windows:</span><span class="sxs-lookup"><span data-stu-id="019bc-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="019bc-116">**Microsoft. Owin. host. SystemWeb**.</span><span class="sxs-lookup"><span data-stu-id="019bc-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="019bc-117">Использует службы IIS с конвейером ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="019bc-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="019bc-118">**Microsoft. Owin. host. HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="019bc-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="019bc-119">Использует [System .NET. HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="019bc-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="019bc-120">Этот сервер в настоящее время является параметром по умолчанию при размещении в собственном расположении Katana.</span><span class="sxs-lookup"><span data-stu-id="019bc-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="019bc-121">Katana в настоящее время не предоставляет по промежуточного слоя OWIN для проверки подлинности Windows, так как эта функция уже доступна на серверах.</span><span class="sxs-lookup"><span data-stu-id="019bc-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>

## <a name="windows-authentication-in-iis"></a><span data-ttu-id="019bc-122">Проверка подлинности Windows в IIS</span><span class="sxs-lookup"><span data-stu-id="019bc-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="019bc-123">С помощью Microsoft. Owin. host. SystemWeb можно просто включить проверку подлинности Windows в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="019bc-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="019bc-124">Начнем с создания нового приложения ASP.NET с помощью шаблона проекта "ASP.NET Empty веб-приложение".</span><span class="sxs-lookup"><span data-stu-id="019bc-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="019bc-125">Затем добавьте пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="019bc-125">Next, add NuGet packages.</span></span> <span data-ttu-id="019bc-126">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="019bc-126">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="019bc-127">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="019bc-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="019bc-128">Теперь добавьте класс с именем `Startup` со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="019bc-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="019bc-129">Это все, что необходимо для создания приложения "Hello World" для OWIN, работающего на IIS.</span><span class="sxs-lookup"><span data-stu-id="019bc-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="019bc-130">Нажмите клавишу F5, чтобы начать отладку приложения.</span><span class="sxs-lookup"><span data-stu-id="019bc-130">Press F5 to debug the application.</span></span> <span data-ttu-id="019bc-131">Вы должны увидеть текст "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="019bc-131">You should see "Hello World!"</span></span> <span data-ttu-id="019bc-132">в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="019bc-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="019bc-133">Далее мы будем включать проверку подлинности Windows в IIS Express.</span><span class="sxs-lookup"><span data-stu-id="019bc-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="019bc-134">В меню **вид** выберите пункт **свойства**.</span><span class="sxs-lookup"><span data-stu-id="019bc-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="019bc-135">Щелкните имя проекта в обозреватель решений, чтобы просмотреть свойства проекта.</span><span class="sxs-lookup"><span data-stu-id="019bc-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="019bc-136">В окне **Свойства** задайте для параметра **Анонимная проверка подлинности** значение **отключено** и установите для параметра **Проверка подлинности Windows** значение **включено**.</span><span class="sxs-lookup"><span data-stu-id="019bc-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="019bc-137">При запуске приложения из Visual Studio IIS Express потребуется учетные данные пользователя Windows.</span><span class="sxs-lookup"><span data-stu-id="019bc-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="019bc-138">Это можно увидеть с помощью [Fiddler](http://fiddler2.com/home) или другого средства отладки HTTP.</span><span class="sxs-lookup"><span data-stu-id="019bc-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="019bc-139">Ниже приведен пример HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="019bc-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="019bc-140">Заголовки WWW-Authenticate в этом ответе указывают, что сервер поддерживает протокол [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) , использующий Kerberos или NTLM.</span><span class="sxs-lookup"><span data-stu-id="019bc-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="019bc-141">Затем при развертывании приложения на сервере выполните следующие [действия](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) , чтобы включить проверку подлинности Windows в службах IIS на этом сервере.</span><span class="sxs-lookup"><span data-stu-id="019bc-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="019bc-142">Проверка подлинности Windows в HttpListener</span><span class="sxs-lookup"><span data-stu-id="019bc-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="019bc-143">Если вы используете Microsoft. Owin. host. HttpListener для самостоятельного размещения Katana, вы можете включить проверку подлинности Windows непосредственно в экземпляре **HttpListener** .</span><span class="sxs-lookup"><span data-stu-id="019bc-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="019bc-144">Сначала создайте консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="019bc-144">First, create a new console application.</span></span> <span data-ttu-id="019bc-145">Затем добавьте пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="019bc-145">Next, add NuGet packages.</span></span> <span data-ttu-id="019bc-146">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="019bc-146">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="019bc-147">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="019bc-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="019bc-148">Теперь добавьте класс с именем `Startup` со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="019bc-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="019bc-149">Этот класс реализует тот же самый пример "Hello World" из ранее, но также устанавливает проверку подлинности Windows в качестве схемы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="019bc-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="019bc-150">В функции `Main` запустите конвейер OWIN:</span><span class="sxs-lookup"><span data-stu-id="019bc-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="019bc-151">Вы можете отправить запрос в Fiddler, чтобы убедиться, что приложение использует проверку подлинности Windows:</span><span class="sxs-lookup"><span data-stu-id="019bc-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="019bc-152">См. также</span><span class="sxs-lookup"><span data-stu-id="019bc-152">Related Topics</span></span>

[<span data-ttu-id="019bc-153">Обзор проекта Katana</span><span class="sxs-lookup"><span data-stu-id="019bc-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="019bc-154">System.Net.HttpListener;</span><span class="sxs-lookup"><span data-stu-id="019bc-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="019bc-155">Основные сведения о проверке подлинности в OWIN Forms в MVC 5</span><span class="sxs-lookup"><span data-stu-id="019bc-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
