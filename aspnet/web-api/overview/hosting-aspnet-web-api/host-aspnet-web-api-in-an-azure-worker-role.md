---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Размещение ASP.NET Web API 2 в рабочей роли Azure - ASP.NET 4.x
author: MikeWasson
description: Учебник. Размещение веб-API ASP.NET в рабочей роли Azure, с помощью OWIN для резидентного размещения платформа веб-API.
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: bfb23aafb814010e8651965dad91ca20a37fd786
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59404628"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="bb1ee-103">Размещение ASP.NET Web API 2 в рабочей роли Azure</span><span class="sxs-lookup"><span data-stu-id="bb1ee-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="bb1ee-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bb1ee-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="bb1ee-105">Этом руководстве показано, как разместить веб-API ASP.NET в рабочей роли Azure, с помощью OWIN для резидентного размещения платформа веб-API.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="bb1ee-106">[Открыть веб-интерфейс .NET](http://owin.org/) (OWIN) определяет абстракции между веб-серверов .NET и веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="bb1ee-107">OWIN отделяет веб-приложения на сервер, который идеально OWIN для резидентного размещения веб-приложения в собственном процессе, за пределами IIS — например, внутри рабочей роли Azure.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="bb1ee-108">В этом руководстве вы используете пакет Microsoft.Owin.Host.HttpListener, предоставляющую HTTP-сервер, который используется для резидентного размещения приложения OWIN.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bb1ee-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="bb1ee-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="bb1ee-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bb1ee-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="bb1ee-111">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="bb1ee-111">Web API 2</span></span>
> - [<span data-ttu-id="bb1ee-112">Пакет Azure SDK для .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="bb1ee-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="bb1ee-113">Создание проекта Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bb1ee-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="bb1ee-114">Запустите Visual Studio с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="bb1ee-115">Для отладки приложения в локальной среде, с помощью эмулятора вычислений Azure требуются права администратора.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-115">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="bb1ee-116">На **файл** меню, щелкните **New**, затем нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="bb1ee-117">Из **установленные шаблоны**, в разделе Visual C#, щелкните **Cloud** и нажмите кнопку **облачной службы Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="bb1ee-118">Присвойте проекту имя «AzureApp» и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="bb1ee-119">В **новая облачная служба Windows Azure** диалоговое окно, дважды щелкните **рабочей роли**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="bb1ee-120">Оставьте имя по умолчанию («WorkerRole1»).</span><span class="sxs-lookup"><span data-stu-id="bb1ee-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="bb1ee-121">Этот шаг добавляет рабочей роли в решение.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="bb1ee-122">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="bb1ee-123">Решение Visual Studio, который создается содержит два проекта:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="bb1ee-124">&quot;AzureApp&quot; определяет роли и конфигурации для приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="bb1ee-125">&quot;WorkerRole1&quot; содержит код для рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="bb1ee-126">Как правило приложение Azure может содержать несколько ролей, несмотря на то, что в этом руководстве используется одна роль.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="bb1ee-127">Добавьте веб-API и пакеты OWIN</span><span class="sxs-lookup"><span data-stu-id="bb1ee-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="bb1ee-128">Из **средства** меню, щелкните **диспетчер пакетов NuGet**, затем нажмите кнопку **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="bb1ee-129">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="bb1ee-130">Добавить конечную точку HTTP</span><span class="sxs-lookup"><span data-stu-id="bb1ee-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="bb1ee-131">В обозревателе решений разверните проект AzureApp.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="bb1ee-132">Разверните узел роли, щелкните правой кнопкой мыши WorkerRole1 и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="bb1ee-133">Нажмите кнопку **конечные точки**, а затем нажмите кнопку **добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="bb1ee-134">В **протокола** раскрывающегося списка выберите «http».</span><span class="sxs-lookup"><span data-stu-id="bb1ee-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="bb1ee-135">В **общий порт** и **частный порт**, введите 80.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="bb1ee-136">Эти номера портов могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-136">These port numbers can be different.</span></span> <span data-ttu-id="bb1ee-137">Общий порт — новые клиенты будут использовать при отправке запроса к роли.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="bb1ee-138">Настройка веб-API для резидентного размещения</span><span class="sxs-lookup"><span data-stu-id="bb1ee-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="bb1ee-139">В обозревателе решений щелкните правой кнопкой мыши проект WorkerRole1 и выберите **добавить** / **класс** для добавления нового класса.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="bb1ee-140">Присвойте классу имя `Startup`.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="bb1ee-141">Замените весь код шаблона в этом файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="bb1ee-142">Добавить контроллер веб-API</span><span class="sxs-lookup"><span data-stu-id="bb1ee-142">Add a Web API Controller</span></span>

<span data-ttu-id="bb1ee-143">Добавьте класс контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="bb1ee-144">Щелкните правой кнопкой мыши проект WorkerRole1 и выберите **добавить** / **класс**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="bb1ee-145">Имя класса TestController.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-145">Name the class TestController.</span></span> <span data-ttu-id="bb1ee-146">Замените весь код шаблона в этом файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="bb1ee-147">Для простоты этот контроллер определяет только два метода GET, возвращающие обычного текста.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="bb1ee-148">Запустить узел OWIN</span><span class="sxs-lookup"><span data-stu-id="bb1ee-148">Start the OWIN Host</span></span>

<span data-ttu-id="bb1ee-149">Откройте файл WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="bb1ee-150">Этот класс определяет код, выполняемый при рабочей роли запущено и остановлено.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="bb1ee-151">Добавьте следующий оператор using:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="bb1ee-152">Добавить **IDisposable** члена `WorkerRole` класса:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="bb1ee-153">В `OnStart` метод, добавьте следующий код для запуска узла:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="bb1ee-154">**WebApp.Start** метод начинает хоста OWIN.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="bb1ee-155">Имя `Startup` класс является параметром типа метода.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="bb1ee-156">По соглашению, главное приложение выполняет вызов `Configure` метод этого класса.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="bb1ee-157">Переопределить `OnStop` для удаления  *\_приложения* экземпляр:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="bb1ee-158">Ниже приведен полный код для WorkerRole.cs:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="bb1ee-159">Выполните сборку решения и нажмите клавишу F5 для запуска приложения локально в эмуляторе вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="bb1ee-160">В зависимости от настроек брандмауэра может потребоваться предоставление эмулятору через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="bb1ee-161">Если вы получаете исключение, как показано ниже, см. раздел [этой записи блога](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) решение этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="bb1ee-162">«Не удалось загрузить файл или сборку "Microsoft.Owin, Version = 2.0.2.0, язык и региональные параметры = neutral, PublicKeyToken = 31bf3856ad364e35" или одну из ее зависимостей.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="bb1ee-163">Определение манифеста расположены сборки не соответствует ссылки на сборку.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="bb1ee-164">(Исключение от HRESULT: 0x80131040)»</span><span class="sxs-lookup"><span data-stu-id="bb1ee-164">(Exception from HRESULT: 0x80131040)"</span></span>


<span data-ttu-id="bb1ee-165">Эмулятор вычислений назначает локальный IP-адрес конечной точки.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="bb1ee-166">IP-адрес можно найти, просмотрев пользовательский Интерфейс эмулятора вычислений.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="bb1ee-167">Щелкните правой кнопкой мыши значок эмулятора в задаче области уведомлений и выберите **Показать пользовательский Интерфейс эмулятора вычислений**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="bb1ee-168">Найти IP-адрес в группе развертывания служб, развертывания [id], сведения о службе.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="bb1ee-169">Откройте веб-браузер и перейдите на http://<em>адрес</em>/test/1, где <em>адрес</em> IP-адрес, назначенный с помощью эмулятора вычислений; например, `http://127.0.0.1:80/test/1`.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="bb1ee-170">Вы увидите ответ от контроллера веб-API:</span><span class="sxs-lookup"><span data-stu-id="bb1ee-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="bb1ee-171">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="bb1ee-171">Deploy to Azure</span></span>

<span data-ttu-id="bb1ee-172">Для выполнения этого шага необходимо иметь учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="bb1ee-173">Если ее еще нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="bb1ee-174">Дополнительные сведения см. в разделе [бесплатной пробной версии Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="bb1ee-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="bb1ee-175">В обозревателе решений щелкните правой кнопкой мыши проект AzureApp.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="bb1ee-176">Нажмите **Публиковать**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="bb1ee-177">Если вы не вошли учетную запись Azure, щелкните **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="bb1ee-178">После входа, выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="bb1ee-179">Введите имя для облачной службы и выбрать регион.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="bb1ee-180">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="bb1ee-181">Нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="bb1ee-182">Окно журнала действий Azure показывает ход выполнения развертывания.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="bb1ee-183">При развертывании приложения, перейдите к http://appname.cloudapp.net/test/1.</span><span class="sxs-lookup"><span data-stu-id="bb1ee-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="bb1ee-184">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bb1ee-184">Additional Resources</span></span>

- [<span data-ttu-id="bb1ee-185">Обзор проекта Katana</span><span class="sxs-lookup"><span data-stu-id="bb1ee-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="bb1ee-186">Проект Katana на GitHub</span><span class="sxs-lookup"><span data-stu-id="bb1ee-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
