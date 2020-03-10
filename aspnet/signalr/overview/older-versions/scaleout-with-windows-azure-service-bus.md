---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: Масштабирование SignalR с помощью служебной шины Azure (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449940"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="3078f-102">Масштабирование SignalR с помощью служебной шины Azure (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="3078f-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="3078f-103">по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="3078f-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="3078f-104">В этом руководстве вы развернете приложение SignalR в веб-роли Windows Azure, используя объединительную плату служебной шины для распространения сообщений на каждый экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="3078f-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="3078f-105">Предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="3078f-105">Prerequisites:</span></span>

- <span data-ttu-id="3078f-106">Учетная запись Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="3078f-106">A Windows Azure account.</span></span>
- <span data-ttu-id="3078f-107">[Пакет Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="3078f-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="3078f-108">Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="3078f-108">Visual Studio 2012.</span></span>

<span data-ttu-id="3078f-109">Объединительная плата служебной шины также совместима с [служебной шиной для Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)версии 1,1.</span><span class="sxs-lookup"><span data-stu-id="3078f-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="3078f-110">Однако она несовместима с Service Bus версии 1,0 для Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3078f-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="3078f-111">Цены</span><span class="sxs-lookup"><span data-stu-id="3078f-111">Pricing</span></span>

<span data-ttu-id="3078f-112">Объединительная плата служебной шины использует разделы для отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="3078f-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="3078f-113">Последние сведения о ценах см. в статье [служебная шина](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="3078f-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="3078f-114">На момент написания этой статьи вы можете отправить 1 000 000 сообщений в месяц для менее $1.</span><span class="sxs-lookup"><span data-stu-id="3078f-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="3078f-115">Объединительная плата отправляет сообщение служебной шины для каждого вызова метода концентратора SignalR.</span><span class="sxs-lookup"><span data-stu-id="3078f-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="3078f-116">Кроме того, существуют некоторые управляющие сообщения для соединений, отключений, объединения или покидает группы и т. д.</span><span class="sxs-lookup"><span data-stu-id="3078f-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="3078f-117">В большинстве приложений большая часть трафика сообщений будет вызывать метод концентратора.</span><span class="sxs-lookup"><span data-stu-id="3078f-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="3078f-118">Обзор</span><span class="sxs-lookup"><span data-stu-id="3078f-118">Overview</span></span>

<span data-ttu-id="3078f-119">Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.</span><span class="sxs-lookup"><span data-stu-id="3078f-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="3078f-120">Создайте новое пространство имен служебной шины с помощью портал Azure Windows.</span><span class="sxs-lookup"><span data-stu-id="3078f-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="3078f-121">Добавьте следующие пакеты NuGet в приложение:</span><span class="sxs-lookup"><span data-stu-id="3078f-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="3078f-122">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="3078f-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="3078f-123">Microsoft. AspNet. SignalR. ServiceBus</span><span class="sxs-lookup"><span data-stu-id="3078f-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="3078f-124">Создание приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="3078f-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="3078f-125">Добавьте следующий код в Global. asax для настройки объединительной платы:</span><span class="sxs-lookup"><span data-stu-id="3078f-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="3078f-126">Для каждого приложения выберите другое значение для параметра "YourAppName".</span><span class="sxs-lookup"><span data-stu-id="3078f-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="3078f-127">Не используйте одинаковое значение в нескольких приложениях.</span><span class="sxs-lookup"><span data-stu-id="3078f-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="3078f-128">Создание служб Azure</span><span class="sxs-lookup"><span data-stu-id="3078f-128">Create the Azure Services</span></span>

<span data-ttu-id="3078f-129">Создайте облачную службу, как описано в статье [Создание и развертывание облачной службы](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="3078f-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="3078f-130">Выполните действия, описанные в разделе "как создать облачную службу с помощью быстрого создания".</span><span class="sxs-lookup"><span data-stu-id="3078f-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="3078f-131">В этом руководстве не требуется отправлять сертификат.</span><span class="sxs-lookup"><span data-stu-id="3078f-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="3078f-132">Создайте новое пространство имен служебной шины, как описано в разделе [Использование разделов и подписок служебной шины](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="3078f-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="3078f-133">Выполните действия, описанные в разделе "Создание пространства имен службы".</span><span class="sxs-lookup"><span data-stu-id="3078f-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="3078f-134">Обязательно выберите один и тот же регион для облачной службы и пространства имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="3078f-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="3078f-135">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3078f-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="3078f-136">Запустите среду Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3078f-136">Start Visual Studio.</span></span> <span data-ttu-id="3078f-137">В меню **Файл** выберите **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="3078f-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="3078f-138">В диалоговом окне **Новый проект** разверните узел **визуальный C#** элемент.</span><span class="sxs-lookup"><span data-stu-id="3078f-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="3078f-139">В разделе **Установленные шаблоны**выберите **облако** , а затем выберите **облачная служба Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="3078f-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="3078f-140">Примите значение по умолчанию .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="3078f-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="3078f-141">Присвойте приложению имя Чатсервице и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3078f-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="3078f-142">В диалоговом окне **новая облачная служба Windows Azure** выберите ASP.NET MVC 4 Web Role.</span><span class="sxs-lookup"><span data-stu-id="3078f-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="3078f-143">Нажмите кнопку со стрелкой вправо ( **&gt;** ), чтобы добавить роль в решение.</span><span class="sxs-lookup"><span data-stu-id="3078f-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="3078f-144">Наведите указатель мыши на новую роль, чтобы увидеть значок карандаша.</span><span class="sxs-lookup"><span data-stu-id="3078f-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="3078f-145">Щелкните этот значок, чтобы переименовать роль.</span><span class="sxs-lookup"><span data-stu-id="3078f-145">Click this icon to rename the role.</span></span> <span data-ttu-id="3078f-146">Присвойте роли имя "Сигналрчат" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3078f-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="3078f-147">В мастере **создания проекта ASP.NET MVC 4** выберите **Интернет приложение**.</span><span class="sxs-lookup"><span data-stu-id="3078f-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="3078f-148">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3078f-148">Click **OK**.</span></span> <span data-ttu-id="3078f-149">Мастер проектов создает два проекта:</span><span class="sxs-lookup"><span data-stu-id="3078f-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="3078f-150">Чатсервице: этот проект является приложением Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="3078f-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="3078f-151">Он определяет роли Azure и другие параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3078f-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="3078f-152">Сигналрчат: этот проект является проектом ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="3078f-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="3078f-153">Создание приложения разговора SignalR</span><span class="sxs-lookup"><span data-stu-id="3078f-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="3078f-154">Чтобы создать приложение для разговора, выполните действия, описанные в руководстве [Начало работы с SignalR и MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="3078f-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="3078f-155">Используйте NuGet для установки необходимых библиотек.</span><span class="sxs-lookup"><span data-stu-id="3078f-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="3078f-156">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="3078f-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="3078f-157">В окне **консоли диспетчера пакетов** введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3078f-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="3078f-158">Используйте параметр `-ProjectName`, чтобы установить пакеты в проект MVC ASP.NET, а не в проект Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="3078f-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="3078f-159">Настройка объединительной платы</span><span class="sxs-lookup"><span data-stu-id="3078f-159">Configure the Backplane</span></span>

<span data-ttu-id="3078f-160">Добавьте в файл Global. asax приложения следующий код:</span><span class="sxs-lookup"><span data-stu-id="3078f-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="3078f-161">Теперь необходимо получить строку подключения к служебной шине.</span><span class="sxs-lookup"><span data-stu-id="3078f-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="3078f-162">В портал Azure выберите созданное пространство имен служебной шины и щелкните значок ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="3078f-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="3078f-163">Скопируйте строку подключения в буфер обмена, а затем вставьте ее в переменную *ConnectionString* .</span><span class="sxs-lookup"><span data-stu-id="3078f-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="3078f-164">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="3078f-164">Deploy to Azure</span></span>

<span data-ttu-id="3078f-165">В обозреватель решений разверните папку **роли** в проекте чатсервице.</span><span class="sxs-lookup"><span data-stu-id="3078f-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="3078f-166">Щелкните правой кнопкой мыши роль Сигналрчат и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="3078f-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="3078f-167">Перейдите на вкладку **Конфигурация** . В разделе **экземпляры** выберите 2.</span><span class="sxs-lookup"><span data-stu-id="3078f-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="3078f-168">Можно также задать размер виртуальной машины **очень маленький**.</span><span class="sxs-lookup"><span data-stu-id="3078f-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="3078f-169">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="3078f-169">Save the changes.</span></span>

<span data-ttu-id="3078f-170">В обозреватель решений щелкните правой кнопкой мыши проект Чатсервице.</span><span class="sxs-lookup"><span data-stu-id="3078f-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="3078f-171">Нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="3078f-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="3078f-172">Если вы впервые публикуете в Windows Azure, вы должны скачать свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="3078f-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="3078f-173">В мастере **публикации** щелкните "войти для загрузки учетных данных".</span><span class="sxs-lookup"><span data-stu-id="3078f-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="3078f-174">Будет предложено войти в портал Azure Windows и скачать файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="3078f-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="3078f-175">Щелкните **Импорт** и выберите скачанный файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="3078f-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="3078f-176">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3078f-176">Click **Next**.</span></span> <span data-ttu-id="3078f-177">В диалоговом окне **Параметры публикации** в разделе **облачная служба**выберите созданную ранее облачную службу.</span><span class="sxs-lookup"><span data-stu-id="3078f-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="3078f-178">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="3078f-178">Click **Publish**.</span></span> <span data-ttu-id="3078f-179">Развертывание приложения и запуск виртуальных машин может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="3078f-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="3078f-180">Теперь при запуске приложения для разговора экземпляры роли обмениваются данными через служебную шину Azure, используя раздел служебной шины.</span><span class="sxs-lookup"><span data-stu-id="3078f-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="3078f-181">Раздел — это очередь сообщений, которая разрешает несколько подписчиков.</span><span class="sxs-lookup"><span data-stu-id="3078f-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="3078f-182">Объединительная плата автоматически создает раздел и подписки.</span><span class="sxs-lookup"><span data-stu-id="3078f-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="3078f-183">Чтобы просмотреть подписки и действия с сообщениями, откройте портал Azure, выберите пространство имен служебной шины и щелкните "разделы".</span><span class="sxs-lookup"><span data-stu-id="3078f-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="3078f-184">Отображение действия сообщения на панели мониторинга займет несколько минут.</span><span class="sxs-lookup"><span data-stu-id="3078f-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="3078f-185">SignalR управляет временем существования раздела.</span><span class="sxs-lookup"><span data-stu-id="3078f-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="3078f-186">Пока приложение развернуто, не пытайтесь вручную удалить разделы или изменить параметры в разделе.</span><span class="sxs-lookup"><span data-stu-id="3078f-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>
