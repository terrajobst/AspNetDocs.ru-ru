---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Размещение OWIN в рабочей роли Azure | Документация Майкрософт
author: MikeWasson
description: В этом руководстве показано, как самостоятельно размещать OWIN в рабочей роли Microsoft Azure. Открытый веб-интерфейс для .NET (OWIN) определяет абстракцию между веб-сервером .NET...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472398"
---
# <a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="fceb8-104">Размещение OWIN в рабочей роли Azure</span><span class="sxs-lookup"><span data-stu-id="fceb8-104">Host OWIN in an Azure Worker Role</span></span>

<span data-ttu-id="fceb8-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fceb8-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="fceb8-106">В этом руководстве показано, как самостоятельно размещать OWIN в рабочей роли Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fceb8-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
>
> <span data-ttu-id="fceb8-107">[Открытый веб-интерфейс для .NET](http://owin.org/) (OWIN) определяет абстракцию между веб-серверами и веб-приложениями .NET.</span><span class="sxs-lookup"><span data-stu-id="fceb8-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="fceb8-108">OWIN отделяет веб-приложение от сервера, что делает OWIN идеальным для самостоятельного размещения веб-приложения в собственном процессе вне служб IIS, например в рабочей роли Azure.</span><span class="sxs-lookup"><span data-stu-id="fceb8-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="fceb8-109">В этом руководстве вы узнаете, как самостоятельно размещать приложения OWIN в рабочей роли Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fceb8-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="fceb8-110">Дополнительные сведения о рабочих ролях см. в статье [модели выполнения Azure](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span><span class="sxs-lookup"><span data-stu-id="fceb8-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fceb8-111">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="fceb8-111">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="fceb8-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="fceb8-112">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [<span data-ttu-id="fceb8-113">Пакет Azure SDK для .NET 2,3</span><span class="sxs-lookup"><span data-stu-id="fceb8-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="fceb8-114">Microsoft. Owin. резидент 2.1.0</span><span class="sxs-lookup"><span data-stu-id="fceb8-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="fceb8-115">Создание проекта Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fceb8-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="fceb8-116">Запустите Visual Studio с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="fceb8-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="fceb8-117">Права администратора необходимы для локальной отладки приложения с помощью эмулятора вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="fceb8-117">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="fceb8-118">В меню **файл** выберите пункт **создать**, а затем выберите пункт **проект**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="fceb8-119">На странице **Установленные шаблоны**в разделе C#визуальный элемент щелкните **облако** , а затем щелкните **облачная служба Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="fceb8-120">Присвойте проекту имя "AzureApp" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="fceb8-121">В диалоговом окне **новая облачная служба Windows Azure** дважды щелкните **Рабочая роль**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="fceb8-122">Оставьте имя по умолчанию ("WorkerRole1").</span><span class="sxs-lookup"><span data-stu-id="fceb8-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="fceb8-123">На этом шаге Рабочая роль добавляется в решение.</span><span class="sxs-lookup"><span data-stu-id="fceb8-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="fceb8-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="fceb8-125">Созданное решение Visual Studio содержит два проекта:</span><span class="sxs-lookup"><span data-stu-id="fceb8-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="fceb8-126">&quot;AzureApp&quot; определяет роли и конфигурацию для приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="fceb8-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="fceb8-127">&quot;WorkerRole1&quot; содержит код для рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="fceb8-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="fceb8-128">Как правило, приложение Azure может содержать несколько ролей, хотя в этом учебнике используется одна роль.</span><span class="sxs-lookup"><span data-stu-id="fceb8-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="fceb8-129">Добавление пакетов с самостоятельным размещением OWIN</span><span class="sxs-lookup"><span data-stu-id="fceb8-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="fceb8-130">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем щелкните **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-130">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="fceb8-131">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fceb8-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="fceb8-132">Добавление конечной точки HTTP</span><span class="sxs-lookup"><span data-stu-id="fceb8-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="fceb8-133">В обозреватель решений разверните проект AzureApp.</span><span class="sxs-lookup"><span data-stu-id="fceb8-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="fceb8-134">Разверните узел роли, щелкните правой кнопкой мыши WorkerRole1 и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="fceb8-135">Выберите **Конечные точки** и нажмите кнопку **Добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="fceb8-136">В раскрывающемся списке **протокол** выберите "http".</span><span class="sxs-lookup"><span data-stu-id="fceb8-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="fceb8-137">В окне **Общий порт** и **частный порт**введите 80.</span><span class="sxs-lookup"><span data-stu-id="fceb8-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="fceb8-138">Эти номера портов могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="fceb8-138">These port numbers can be different.</span></span> <span data-ttu-id="fceb8-139">Общедоступный порт используется клиентами при отправке запроса роли.</span><span class="sxs-lookup"><span data-stu-id="fceb8-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="fceb8-140">Создание класса запуска OWIN</span><span class="sxs-lookup"><span data-stu-id="fceb8-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="fceb8-141">В обозреватель решений щелкните правой кнопкой мыши проект WorkerRole1 и выберите **добавить** / **класс** , чтобы добавить новый класс.</span><span class="sxs-lookup"><span data-stu-id="fceb8-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="fceb8-142">Назовите класс `Startup`.</span><span class="sxs-lookup"><span data-stu-id="fceb8-142">Name the class `Startup`.</span></span>

<span data-ttu-id="fceb8-143">Замените весь стандартный код следующим:</span><span class="sxs-lookup"><span data-stu-id="fceb8-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="fceb8-144">Метод расширения `UseWelcomePage` добавляет в приложение простую HTML-страницу, чтобы убедиться, что сайт работает.</span><span class="sxs-lookup"><span data-stu-id="fceb8-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="fceb8-145">Запуск узла OWIN</span><span class="sxs-lookup"><span data-stu-id="fceb8-145">Start the OWIN Host</span></span>

<span data-ttu-id="fceb8-146">Откройте файл WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="fceb8-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="fceb8-147">Этот класс определяет код, который выполняется при запуске и остановке рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="fceb8-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="fceb8-148">Добавьте следующую инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="fceb8-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="fceb8-149">Добавьте элемент **IDisposable** в класс `WorkerRole`:</span><span class="sxs-lookup"><span data-stu-id="fceb8-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="fceb8-150">В методе `OnStart` добавьте следующий код для запуска узла:</span><span class="sxs-lookup"><span data-stu-id="fceb8-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="fceb8-151">Метод **webapp. Start** запускает узел OWIN.</span><span class="sxs-lookup"><span data-stu-id="fceb8-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="fceb8-152">Имя класса `Startup` является параметром типа для метода.</span><span class="sxs-lookup"><span data-stu-id="fceb8-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="fceb8-153">По соглашению узел будет вызывать метод `Configure` этого класса.</span><span class="sxs-lookup"><span data-stu-id="fceb8-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="fceb8-154">Переопределите `OnStop`, чтобы освободить экземпляр *\_ного приложения* :</span><span class="sxs-lookup"><span data-stu-id="fceb8-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="fceb8-155">Ниже приведен полный код для WorkerRole.cs:</span><span class="sxs-lookup"><span data-stu-id="fceb8-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="fceb8-156">Выполните сборку решения и нажмите клавишу F5, чтобы запустить приложение локально в эмуляторе вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="fceb8-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="fceb8-157">В зависимости от параметров брандмауэра может потребоваться разрешить эмулятор через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="fceb8-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="fceb8-158">Эмулятор вычислений назначает конечной точке локальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="fceb8-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="fceb8-159">IP-адрес можно найти, просмотрев пользовательский интерфейс эмулятора вычислений.</span><span class="sxs-lookup"><span data-stu-id="fceb8-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="fceb8-160">Щелкните правой кнопкой мыши значок эмулятора в области уведомлений панели задач и выберите пункт **отобразить пользовательский интерфейс эмулятора вычислений**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="fceb8-161">Найдите IP-адрес в разделе развертывания службы, развертывание [ИД], сведения о службе.</span><span class="sxs-lookup"><span data-stu-id="fceb8-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="fceb8-162">Откройте веб-браузер и перейдите по *адресу*http:\/\/Address, где *Address* — это IP-адрес, назначенный эмулятором вычислений. Например, `http://127.0.0.1:80`.</span><span class="sxs-lookup"><span data-stu-id="fceb8-162">Open a web browser and navigate to http:\/\/*address*, where *address* is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="fceb8-163">Вы должны увидеть страницу приветствия OWIN:</span><span class="sxs-lookup"><span data-stu-id="fceb8-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="fceb8-164">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="fceb8-164">Deploy to Azure</span></span>

<span data-ttu-id="fceb8-165">Для этого шага необходимо иметь учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="fceb8-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="fceb8-166">Если у вас ее еще нет, вы можете создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="fceb8-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fceb8-167">Дополнительные сведения см. в статье [Microsoft Azure Бесплатная пробная версия](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fceb8-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="fceb8-168">В обозреватель решений щелкните правой кнопкой мыши проект AzureApp.</span><span class="sxs-lookup"><span data-stu-id="fceb8-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="fceb8-169">Нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="fceb8-170">Если вы не вошли в учетную запись Azure, щелкните **войти**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="fceb8-171">После входа выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="fceb8-172">Введите имя для облачной службы и выберите регион.</span><span class="sxs-lookup"><span data-stu-id="fceb8-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="fceb8-173">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="fceb8-174">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="fceb8-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="fceb8-175">В окне Журнал действий Azure отображается ход развертывания.</span><span class="sxs-lookup"><span data-stu-id="fceb8-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="fceb8-176">При развертывании приложения перейдите к `http://appname.cloudapp.net/`, где *AppName* — это имя вашей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="fceb8-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fceb8-177">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fceb8-177">Additional Resources</span></span>

- [<span data-ttu-id="fceb8-178">Обзор проекта Katana</span><span class="sxs-lookup"><span data-stu-id="fceb8-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="fceb8-179">Проект Katana на GitHub</span><span class="sxs-lookup"><span data-stu-id="fceb8-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
