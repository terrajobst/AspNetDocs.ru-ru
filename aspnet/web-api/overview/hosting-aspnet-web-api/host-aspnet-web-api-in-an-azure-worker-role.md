---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Размещение веб-API ASP.NET 2 в рабочей роли Azure — ASP.NET 4. x
author: MikeWasson
description: Руководство. размещение веб-API ASP.NET в рабочей роли Azure с помощью OWIN для самостоятельного размещения платформы веб-API.
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448410"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="2aef7-103">Размещение веб-API ASP.NET 2 в рабочей роли Azure</span><span class="sxs-lookup"><span data-stu-id="2aef7-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="2aef7-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2aef7-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="2aef7-105">В этом руководстве показано, как разместить веб-API ASP.NET в рабочей роли Azure с помощью OWIN для самостоятельного размещения платформы веб-API.</span><span class="sxs-lookup"><span data-stu-id="2aef7-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="2aef7-106">[Открытый веб-интерфейс для .NET](http://owin.org/) (OWIN) определяет абстракцию между веб-серверами и веб-приложениями .NET.</span><span class="sxs-lookup"><span data-stu-id="2aef7-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="2aef7-107">OWIN отделяет веб-приложение от сервера, что делает OWIN идеальным для самостоятельного размещения веб-приложения в собственном процессе вне служб IIS, например в рабочей роли Azure.</span><span class="sxs-lookup"><span data-stu-id="2aef7-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="2aef7-108">В этом руководстве вы будете использовать пакет Microsoft. Owin. host. HttpListener, который предоставляет HTTP-сервер, используемый для самостоятельного размещения приложений OWIN.</span><span class="sxs-lookup"><span data-stu-id="2aef7-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2aef7-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="2aef7-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="2aef7-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2aef7-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2aef7-111">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="2aef7-111">Web API 2</span></span>
> - [<span data-ttu-id="2aef7-112">Пакет Azure SDK для .NET 2,3</span><span class="sxs-lookup"><span data-stu-id="2aef7-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="2aef7-113">Создание проекта Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2aef7-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="2aef7-114">Запустите Visual Studio с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="2aef7-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="2aef7-115">Права администратора необходимы для локальной отладки приложения с помощью эмулятора вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="2aef7-115">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="2aef7-116">В меню **файл** выберите пункт **создать**, а затем выберите пункт **проект**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="2aef7-117">На странице **Установленные шаблоны**в разделе C#визуальный элемент щелкните **облако** , а затем щелкните **облачная служба Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="2aef7-118">Присвойте проекту имя "AzureApp" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="2aef7-119">В диалоговом окне **новая облачная служба Windows Azure** дважды щелкните **Рабочая роль**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="2aef7-120">Оставьте имя по умолчанию ("WorkerRole1").</span><span class="sxs-lookup"><span data-stu-id="2aef7-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="2aef7-121">На этом шаге Рабочая роль добавляется в решение.</span><span class="sxs-lookup"><span data-stu-id="2aef7-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="2aef7-122">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="2aef7-123">Созданное решение Visual Studio содержит два проекта:</span><span class="sxs-lookup"><span data-stu-id="2aef7-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="2aef7-124">&quot;AzureApp&quot; определяет роли и конфигурацию для приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="2aef7-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="2aef7-125">&quot;WorkerRole1&quot; содержит код для рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="2aef7-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="2aef7-126">Как правило, приложение Azure может содержать несколько ролей, хотя в этом учебнике используется одна роль.</span><span class="sxs-lookup"><span data-stu-id="2aef7-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="2aef7-127">Добавление веб-API и пакетов OWIN</span><span class="sxs-lookup"><span data-stu-id="2aef7-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="2aef7-128">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем щелкните **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="2aef7-129">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2aef7-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="2aef7-130">Добавление конечной точки HTTP</span><span class="sxs-lookup"><span data-stu-id="2aef7-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="2aef7-131">В обозреватель решений разверните проект AzureApp.</span><span class="sxs-lookup"><span data-stu-id="2aef7-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="2aef7-132">Разверните узел роли, щелкните правой кнопкой мыши WorkerRole1 и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="2aef7-133">Выберите **Конечные точки** и нажмите кнопку **Добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="2aef7-134">В раскрывающемся списке **протокол** выберите "http".</span><span class="sxs-lookup"><span data-stu-id="2aef7-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="2aef7-135">В окне **Общий порт** и **частный порт**введите 80.</span><span class="sxs-lookup"><span data-stu-id="2aef7-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="2aef7-136">Эти номера портов могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="2aef7-136">These port numbers can be different.</span></span> <span data-ttu-id="2aef7-137">Общедоступный порт используется клиентами при отправке запроса роли.</span><span class="sxs-lookup"><span data-stu-id="2aef7-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="2aef7-138">Настройка веб-API для самостоятельного размещения</span><span class="sxs-lookup"><span data-stu-id="2aef7-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="2aef7-139">В обозреватель решений щелкните правой кнопкой мыши проект WorkerRole1 и выберите **добавить** / **класс** , чтобы добавить новый класс.</span><span class="sxs-lookup"><span data-stu-id="2aef7-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="2aef7-140">Назовите класс `Startup`.</span><span class="sxs-lookup"><span data-stu-id="2aef7-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="2aef7-141">Замените весь стандартный код в этом файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2aef7-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="2aef7-142">Добавление контроллера веб-API</span><span class="sxs-lookup"><span data-stu-id="2aef7-142">Add a Web API Controller</span></span>

<span data-ttu-id="2aef7-143">Затем добавьте класс контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="2aef7-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="2aef7-144">Щелкните правой кнопкой мыши проект WorkerRole1 и выберите **Добавить** **класс** / .</span><span class="sxs-lookup"><span data-stu-id="2aef7-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="2aef7-145">Назовите класс TestController.</span><span class="sxs-lookup"><span data-stu-id="2aef7-145">Name the class TestController.</span></span> <span data-ttu-id="2aef7-146">Замените весь стандартный код в этом файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2aef7-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="2aef7-147">Для простоты этот контроллер просто определяет два метода GET, которые возвращают обычный текст.</span><span class="sxs-lookup"><span data-stu-id="2aef7-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="2aef7-148">Запуск узла OWIN</span><span class="sxs-lookup"><span data-stu-id="2aef7-148">Start the OWIN Host</span></span>

<span data-ttu-id="2aef7-149">Откройте файл WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="2aef7-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="2aef7-150">Этот класс определяет код, который выполняется при запуске и остановке рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="2aef7-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="2aef7-151">Добавьте следующую инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="2aef7-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="2aef7-152">Добавьте элемент **IDisposable** в класс `WorkerRole`:</span><span class="sxs-lookup"><span data-stu-id="2aef7-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="2aef7-153">В методе `OnStart` добавьте следующий код для запуска узла:</span><span class="sxs-lookup"><span data-stu-id="2aef7-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="2aef7-154">Метод **webapp. Start** запускает узел OWIN.</span><span class="sxs-lookup"><span data-stu-id="2aef7-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="2aef7-155">Имя класса `Startup` является параметром типа для метода.</span><span class="sxs-lookup"><span data-stu-id="2aef7-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="2aef7-156">По соглашению узел будет вызывать метод `Configure` этого класса.</span><span class="sxs-lookup"><span data-stu-id="2aef7-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="2aef7-157">Переопределите `OnStop`, чтобы освободить экземпляр *\_ного приложения* :</span><span class="sxs-lookup"><span data-stu-id="2aef7-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="2aef7-158">Ниже приведен полный код для WorkerRole.cs:</span><span class="sxs-lookup"><span data-stu-id="2aef7-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="2aef7-159">Выполните сборку решения и нажмите клавишу F5, чтобы запустить приложение локально в эмуляторе вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="2aef7-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="2aef7-160">В зависимости от параметров брандмауэра может потребоваться разрешить эмулятор через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="2aef7-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="2aef7-161">Если вы получаете исключение, аналогичное приведенному ниже, ознакомьтесь с [этой записью в блоге](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) для решения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="2aef7-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="2aef7-162">«Не удалось загрузить файл или сборку Microsoft. Owin, Version = 2.0.2.0, Culture = Neutral, PublicKeyToken = 31bf3856ad364e35» или одну из ее зависимостей.</span><span class="sxs-lookup"><span data-stu-id="2aef7-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="2aef7-163">Определение манифеста найденной сборки не соответствует ссылке на сборку.</span><span class="sxs-lookup"><span data-stu-id="2aef7-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="2aef7-164">(Исключение из HRESULT: 0x80131040) "</span><span class="sxs-lookup"><span data-stu-id="2aef7-164">(Exception from HRESULT: 0x80131040)"</span></span>

<span data-ttu-id="2aef7-165">Эмулятор вычислений назначает конечной точке локальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="2aef7-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="2aef7-166">IP-адрес можно найти, просмотрев пользовательский интерфейс эмулятора вычислений.</span><span class="sxs-lookup"><span data-stu-id="2aef7-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="2aef7-167">Щелкните правой кнопкой мыши значок эмулятора в области уведомлений панели задач и выберите пункт **отобразить пользовательский интерфейс эмулятора вычислений**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="2aef7-168">Найдите IP-адрес в разделе развертывания службы, развертывание [ИД], сведения о службе.</span><span class="sxs-lookup"><span data-stu-id="2aef7-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="2aef7-169">Откройте веб-браузер и перейдите по<em>адресу http://Address</em>/Test/1, где <em>Address</em> — это IP-адрес, назначенный эмулятором вычислений. Например, `http://127.0.0.1:80/test/1`.</span><span class="sxs-lookup"><span data-stu-id="2aef7-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="2aef7-170">Вы должны увидеть ответ от контроллера веб-API:</span><span class="sxs-lookup"><span data-stu-id="2aef7-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="2aef7-171">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="2aef7-171">Deploy to Azure</span></span>

<span data-ttu-id="2aef7-172">Для этого шага необходимо иметь учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2aef7-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="2aef7-173">Если у вас ее еще нет, вы можете создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2aef7-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2aef7-174">Дополнительные сведения см. в статье [Microsoft Azure Бесплатная пробная версия](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="2aef7-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="2aef7-175">В обозреватель решений щелкните правой кнопкой мыши проект AzureApp.</span><span class="sxs-lookup"><span data-stu-id="2aef7-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="2aef7-176">Нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="2aef7-177">Если вы не вошли в учетную запись Azure, щелкните **войти**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="2aef7-178">После входа выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="2aef7-179">Введите имя для облачной службы и выберите регион.</span><span class="sxs-lookup"><span data-stu-id="2aef7-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="2aef7-180">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="2aef7-181">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="2aef7-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="2aef7-182">В окне Журнал действий Azure отображается ход развертывания.</span><span class="sxs-lookup"><span data-stu-id="2aef7-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="2aef7-183">При развертывании приложения перейдите к http://appname.cloudapp.net/test/1.</span><span class="sxs-lookup"><span data-stu-id="2aef7-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="2aef7-184">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2aef7-184">Additional Resources</span></span>

- [<span data-ttu-id="2aef7-185">Обзор проекта Katana</span><span class="sxs-lookup"><span data-stu-id="2aef7-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="2aef7-186">Проект Katana на GitHub</span><span class="sxs-lookup"><span data-stu-id="2aef7-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
