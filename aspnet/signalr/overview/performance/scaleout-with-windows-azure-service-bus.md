---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Масштабирование SignalR с помощью служебной шины Azure | Документация Майкрософт
author: bradygaster
description: Версии программного обеспечения, используемые в этом разделе, Visual Studio 2013 .NET 4,5 SignalR версии 2 предыдущих версий этого раздела для версии SignalR 1. x этой статьи,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467736"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="e2569-103">Масштабирование SignalR с помощью служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="e2569-103">SignalR Scaleout with Azure Service Bus</span></span>

<span data-ttu-id="e2569-104">по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="e2569-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="e2569-105">В этом руководстве вы развернете приложение SignalR в веб-роли Windows Azure, используя объединительную плату служебной шины для распространения сообщений на каждый экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="e2569-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="e2569-106">(Вы также можете использовать объединительную плату служебной шины с [веб-приложениями в службе приложений Azure](https://docs.microsoft.com/azure/app-service-web/).)</span><span class="sxs-lookup"><span data-stu-id="e2569-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="e2569-107">Предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="e2569-107">Prerequisites:</span></span>

- <span data-ttu-id="e2569-108">Учетная запись Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e2569-108">A Windows Azure account.</span></span>
- <span data-ttu-id="e2569-109">[Пакет Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="e2569-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="e2569-110">Visual Studio 2012 или 2013.</span><span class="sxs-lookup"><span data-stu-id="e2569-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="e2569-111">Объединительная плата служебной шины также совместима с [служебной шиной для Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)версии 1,1.</span><span class="sxs-lookup"><span data-stu-id="e2569-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="e2569-112">Однако она несовместима с Service Bus версии 1,0 для Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e2569-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="e2569-113">Цены</span><span class="sxs-lookup"><span data-stu-id="e2569-113">Pricing</span></span>

<span data-ttu-id="e2569-114">Объединительная плата служебной шины использует разделы для отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="e2569-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="e2569-115">Последние сведения о ценах см. в статье [служебная шина](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="e2569-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="e2569-116">На момент написания этой статьи вы можете отправить 1 000 000 сообщений в месяц для менее $1.</span><span class="sxs-lookup"><span data-stu-id="e2569-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="e2569-117">Объединительная плата отправляет сообщение служебной шины для каждого вызова метода концентратора SignalR.</span><span class="sxs-lookup"><span data-stu-id="e2569-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="e2569-118">Кроме того, существуют некоторые управляющие сообщения для соединений, отключений, объединения или покидает группы и т. д.</span><span class="sxs-lookup"><span data-stu-id="e2569-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="e2569-119">В большинстве приложений большая часть трафика сообщений будет вызывать метод концентратора.</span><span class="sxs-lookup"><span data-stu-id="e2569-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="e2569-120">Обзор</span><span class="sxs-lookup"><span data-stu-id="e2569-120">Overview</span></span>

<span data-ttu-id="e2569-121">Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.</span><span class="sxs-lookup"><span data-stu-id="e2569-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="e2569-122">Создайте новое пространство имен служебной шины с помощью портал Azure Windows.</span><span class="sxs-lookup"><span data-stu-id="e2569-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="e2569-123">Добавьте следующие пакеты NuGet в приложение:</span><span class="sxs-lookup"><span data-stu-id="e2569-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="e2569-124">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="e2569-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - <span data-ttu-id="e2569-125">[Microsoft. ASPNET. SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) или [Microsoft. AspNet. SignalR. servicebus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="e2569-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) or [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span></span>
3. <span data-ttu-id="e2569-126">Создание приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="e2569-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="e2569-127">Добавьте следующий код в Startup.cs, чтобы настроить объединительную плату:</span><span class="sxs-lookup"><span data-stu-id="e2569-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="e2569-128">Этот код настраивает для объединительной платы значения по умолчанию для [топиккаунт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) и [макскуеуеленгс](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span><span class="sxs-lookup"><span data-stu-id="e2569-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="e2569-129">Сведения об изменении этих значений см. в разделе [производительность SignalR: метрики масштабирования](signalr-performance.md#scaleout_metrics).</span><span class="sxs-lookup"><span data-stu-id="e2569-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="e2569-130">Для каждого приложения выберите другое значение для параметра "YourAppName".</span><span class="sxs-lookup"><span data-stu-id="e2569-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="e2569-131">Не используйте одинаковое значение в нескольких приложениях.</span><span class="sxs-lookup"><span data-stu-id="e2569-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="e2569-132">Создание служб Azure</span><span class="sxs-lookup"><span data-stu-id="e2569-132">Create the Azure Services</span></span>

<span data-ttu-id="e2569-133">Создайте облачную службу, как описано в статье [Создание и развертывание облачной службы](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="e2569-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="e2569-134">Выполните действия, описанные в разделе "как создать облачную службу с помощью быстрого создания".</span><span class="sxs-lookup"><span data-stu-id="e2569-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="e2569-135">В этом руководстве не требуется отправлять сертификат.</span><span class="sxs-lookup"><span data-stu-id="e2569-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="e2569-136">Создайте новое пространство имен служебной шины, как описано в разделе [Использование разделов и подписок служебной шины](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="e2569-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="e2569-137">Выполните действия, описанные в разделе "Создание пространства имен службы".</span><span class="sxs-lookup"><span data-stu-id="e2569-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="e2569-138">Обязательно выберите один и тот же регион для облачной службы и пространства имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="e2569-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="e2569-139">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2569-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="e2569-140">Запустите среду Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2569-140">Start Visual Studio.</span></span> <span data-ttu-id="e2569-141">В меню **Файл** выберите **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="e2569-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="e2569-142">В диалоговом окне **Новый проект** разверните узел **визуальный C#** элемент.</span><span class="sxs-lookup"><span data-stu-id="e2569-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="e2569-143">В разделе **Установленные шаблоны**выберите **облако** , а затем выберите **облачная служба Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="e2569-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="e2569-144">Примите значение по умолчанию .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="e2569-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="e2569-145">Присвойте приложению имя Чатсервице и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e2569-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="e2569-146">В диалоговом окне **новая облачная служба Windows Azure** выберите ASP.NET веб-роль.</span><span class="sxs-lookup"><span data-stu-id="e2569-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="e2569-147">Нажмите кнопку со стрелкой вправо ( **&gt;** ), чтобы добавить роль в решение.</span><span class="sxs-lookup"><span data-stu-id="e2569-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="e2569-148">Наведите указатель мыши на новую роль, чтобы увидеть значок карандаша.</span><span class="sxs-lookup"><span data-stu-id="e2569-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="e2569-149">Щелкните этот значок, чтобы переименовать роль.</span><span class="sxs-lookup"><span data-stu-id="e2569-149">Click this icon to rename the role.</span></span> <span data-ttu-id="e2569-150">Присвойте роли имя "Сигналрчат" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e2569-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="e2569-151">В диалоговом окне **Новый проект ASP.NET** выберите **MVC**и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="e2569-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="e2569-152">Мастер проектов создает два проекта:</span><span class="sxs-lookup"><span data-stu-id="e2569-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="e2569-153">Чатсервице: этот проект является приложением Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e2569-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="e2569-154">Он определяет роли Azure и другие параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2569-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="e2569-155">Сигналрчат: этот проект является проектом ASP.NET MVC 5.</span><span class="sxs-lookup"><span data-stu-id="e2569-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="e2569-156">Создание приложения разговора SignalR</span><span class="sxs-lookup"><span data-stu-id="e2569-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="e2569-157">Чтобы создать приложение для разговора, выполните действия, описанные в руководстве [Начало работы с SignalR и MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="e2569-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="e2569-158">Используйте NuGet для установки необходимых библиотек.</span><span class="sxs-lookup"><span data-stu-id="e2569-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="e2569-159">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="e2569-159">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="e2569-160">В окне **консоли диспетчера пакетов** введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e2569-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="e2569-161">Используйте параметр `-ProjectName`, чтобы установить пакеты в проект MVC ASP.NET, а не в проект Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e2569-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="e2569-162">Настройка объединительной платы</span><span class="sxs-lookup"><span data-stu-id="e2569-162">Configure the Backplane</span></span>

<span data-ttu-id="e2569-163">В файл Startup.cs приложения добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="e2569-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="e2569-164">Теперь необходимо получить строку подключения к служебной шине.</span><span class="sxs-lookup"><span data-stu-id="e2569-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="e2569-165">В портал Azure выберите созданное пространство имен служебной шины и щелкните значок ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="e2569-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="e2569-166">Скопируйте строку подключения в буфер обмена, а затем вставьте ее в переменную *ConnectionString* .</span><span class="sxs-lookup"><span data-stu-id="e2569-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="e2569-167">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="e2569-167">Deploy to Azure</span></span>

<span data-ttu-id="e2569-168">В обозреватель решений разверните папку **роли** в проекте чатсервице.</span><span class="sxs-lookup"><span data-stu-id="e2569-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="e2569-169">Щелкните правой кнопкой мыши роль Сигналрчат и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="e2569-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="e2569-170">Перейдите на вкладку **Конфигурация** . В разделе **экземпляры** выберите 2.</span><span class="sxs-lookup"><span data-stu-id="e2569-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="e2569-171">Можно также задать размер виртуальной машины **очень маленький**.</span><span class="sxs-lookup"><span data-stu-id="e2569-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="e2569-172">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="e2569-172">Save the changes.</span></span>

<span data-ttu-id="e2569-173">В обозреватель решений щелкните правой кнопкой мыши проект Чатсервице.</span><span class="sxs-lookup"><span data-stu-id="e2569-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="e2569-174">Нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e2569-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="e2569-175">Если вы впервые публикуете в Windows Azure, вы должны скачать свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="e2569-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="e2569-176">В мастере **публикации** щелкните "войти для загрузки учетных данных".</span><span class="sxs-lookup"><span data-stu-id="e2569-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="e2569-177">Будет предложено войти в портал Azure Windows и скачать файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="e2569-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="e2569-178">Щелкните **Импорт** и выберите скачанный файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="e2569-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="e2569-179">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e2569-179">Click **Next**.</span></span> <span data-ttu-id="e2569-180">В диалоговом окне **Параметры публикации** в разделе **облачная служба**выберите созданную ранее облачную службу.</span><span class="sxs-lookup"><span data-stu-id="e2569-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="e2569-181">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e2569-181">Click **Publish**.</span></span> <span data-ttu-id="e2569-182">Развертывание приложения и запуск виртуальных машин может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e2569-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="e2569-183">Теперь при запуске приложения для разговора экземпляры роли обмениваются данными через служебную шину Azure, используя раздел служебной шины.</span><span class="sxs-lookup"><span data-stu-id="e2569-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="e2569-184">Раздел — это очередь сообщений, которая разрешает несколько подписчиков.</span><span class="sxs-lookup"><span data-stu-id="e2569-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="e2569-185">Объединительная плата автоматически создает раздел и подписки.</span><span class="sxs-lookup"><span data-stu-id="e2569-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="e2569-186">Чтобы просмотреть подписки и действия с сообщениями, откройте портал Azure, выберите пространство имен служебной шины и щелкните "разделы".</span><span class="sxs-lookup"><span data-stu-id="e2569-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="e2569-187">Отображение действия сообщения на панели мониторинга займет несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e2569-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="e2569-188">SignalR управляет временем существования раздела.</span><span class="sxs-lookup"><span data-stu-id="e2569-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="e2569-189">Пока приложение развернуто, не пытайтесь вручную удалить разделы или изменить параметры в разделе.</span><span class="sxs-lookup"><span data-stu-id="e2569-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e2569-190">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="e2569-190">Troubleshooting</span></span>

<span data-ttu-id="e2569-191">**System. InvalidOperationException "единственным поддерживаемым IsolationLevel является" IsolationLevel. Serializable ".**</span><span class="sxs-lookup"><span data-stu-id="e2569-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="e2569-192">Эта ошибка может возникать, если на уровне транзакции для операции задано значение, отличное от `Serializable`.</span><span class="sxs-lookup"><span data-stu-id="e2569-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="e2569-193">Убедитесь, что никакие операции не выполняются с другими уровнями транзакций.</span><span class="sxs-lookup"><span data-stu-id="e2569-193">Verify that no operations are being performed with other transaction levels.</span></span>
