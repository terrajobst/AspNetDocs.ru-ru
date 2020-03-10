---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Масштабирование SignalR с помощью Redis (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431208"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a><span data-ttu-id="a6c1a-102">Масштабирование SignalR с помощью Redis (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="a6c1a-102">SignalR Scaleout with Redis (SignalR 1.x)</span></span>

<span data-ttu-id="a6c1a-103">по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="a6c1a-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="a6c1a-104">В этом руководстве вы будете использовать [Redis](http://redis.io/) для распространения сообщений в приложении SignalR, которое развернуто на двух отдельных экземплярах IIS.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-104">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="a6c1a-105">Redis — это хранилище "ключ — значение" в памяти.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-105">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="a6c1a-106">Она также поддерживает систему обмена сообщениями с моделью публикации и подписки.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-106">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="a6c1a-107">Для пересылки сообщений на другие серверы в объединительной плате Redis SignalR используется функция Pub/Re-in.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-107">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="a6c1a-108">В рамках этого руководства вы будете использовать три сервера:</span><span class="sxs-lookup"><span data-stu-id="a6c1a-108">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="a6c1a-109">Два сервера под Windows, которые будут использоваться для развертывания приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-109">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="a6c1a-110">Один сервер под управлением Linux, который будет использоваться для запуска Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-110">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="a6c1a-111">Для снимков экрана в этом учебнике я использовал Ubuntu 12,04 TLS.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-111">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="a6c1a-112">Если у вас нет трех физических серверов, можно создать виртуальные машины в Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-112">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="a6c1a-113">Другой вариант — создать виртуальные машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-113">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="a6c1a-114">Хотя в этом учебнике используется официальная реализация Redis, в MSOpenTech также есть [порт Windows Redis](https://github.com/MSOpenTech/redis) .</span><span class="sxs-lookup"><span data-stu-id="a6c1a-114">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="a6c1a-115">Установка и настройка различаются, но в противном случае шаги одинаковы.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-115">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a6c1a-116">Масштабирование SignalR с помощью Redis не поддерживает кластеры Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-116">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="a6c1a-117">Обзор</span><span class="sxs-lookup"><span data-stu-id="a6c1a-117">Overview</span></span>

<span data-ttu-id="a6c1a-118">Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-118">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="a6c1a-119">Установите Redis и запустите сервер Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-119">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="a6c1a-120">Добавьте следующие пакеты NuGet в приложение:</span><span class="sxs-lookup"><span data-stu-id="a6c1a-120">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="a6c1a-121">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="a6c1a-121">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="a6c1a-122">Microsoft. AspNet. SignalR. Redis</span><span class="sxs-lookup"><span data-stu-id="a6c1a-122">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="a6c1a-123">Создание приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-123">Create a SignalR application.</span></span>
4. <span data-ttu-id="a6c1a-124">Добавьте следующий код в Global. asax для настройки объединительной платы:</span><span class="sxs-lookup"><span data-stu-id="a6c1a-124">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="a6c1a-125">Ubuntu на Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a6c1a-125">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="a6c1a-126">С помощью Windows Hyper-V вы можете легко создать виртуальную машину Ubuntu на Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-126">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="a6c1a-127">Скачайте ISO-образ Ubuntu с [http://www.ubuntu.com](http://www.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="a6c1a-127">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="a6c1a-128">В Hyper-V добавьте новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-128">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="a6c1a-129">На шаге **Подключить виртуальный жесткий диск** выберите **создать виртуальный жесткий диск**.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-129">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="a6c1a-130">На шаге **Параметры установки** выберите **файл образа (. ISO)** , нажмите кнопку **Обзор**и перейдите к ISO-образ установки Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-130">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="a6c1a-131">Установка Redis</span><span class="sxs-lookup"><span data-stu-id="a6c1a-131">Install Redis</span></span>

<span data-ttu-id="a6c1a-132">Выполните действия, описанные в [http://redis.io/download](http://redis.io/download) , чтобы скачать и создать Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-132">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="a6c1a-133">Это приведет к сборке двоичных файлов Redis в каталоге `src`.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-133">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="a6c1a-134">По умолчанию Redis не требует пароля.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-134">By default, Redis does not require a password.</span></span> <span data-ttu-id="a6c1a-135">Чтобы задать пароль, измените файл `redis.conf`, который находится в корневом каталоге исходного кода.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-135">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="a6c1a-136">(Создайте резервную копию файла, прежде чем изменять его!) Добавьте следующую директиву в `redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="a6c1a-136">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="a6c1a-137">Теперь запустите сервер Redis:</span><span class="sxs-lookup"><span data-stu-id="a6c1a-137">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="a6c1a-138">Откройте порт 6379. это порт по умолчанию, который прослушивается Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-138">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="a6c1a-139">(Номер порта можно изменить в файле конфигурации.)</span><span class="sxs-lookup"><span data-stu-id="a6c1a-139">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="a6c1a-140">Создание приложения SignalR</span><span class="sxs-lookup"><span data-stu-id="a6c1a-140">Create the SignalR Application</span></span>

<span data-ttu-id="a6c1a-141">Создайте приложение SignalR, следуя одному из следующих учебников:</span><span class="sxs-lookup"><span data-stu-id="a6c1a-141">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="a6c1a-142">начало работы с SignalR</span><span class="sxs-lookup"><span data-stu-id="a6c1a-142">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="a6c1a-143">начало работы с SignalR и MVC 4</span><span class="sxs-lookup"><span data-stu-id="a6c1a-143">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="a6c1a-144">Далее мы изменим приложение разговора для поддержки масштабирования с помощью Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-144">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="a6c1a-145">Сначала добавьте в проект пакет NuGet SignalR. Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-145">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="a6c1a-146">В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-146">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="a6c1a-147">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a6c1a-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="a6c1a-148">Затем откройте файл Global. asax.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-148">Next, open the Global.asax file.</span></span> <span data-ttu-id="a6c1a-149">Добавьте следующий код в метод **\_запуска приложения** :</span><span class="sxs-lookup"><span data-stu-id="a6c1a-149">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="a6c1a-150">"Server" — имя сервера, на котором работает Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-150">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="a6c1a-151">*порт* — номер порта.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-151">*port* is the port number</span></span>
- <span data-ttu-id="a6c1a-152">Password — это пароль, определенный в файле Redis. conf.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-152">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="a6c1a-153">AppName — любая строка.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-153">"AppName" is any string.</span></span> <span data-ttu-id="a6c1a-154">SignalR создает канал Pub/Redis с таким именем.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-154">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="a6c1a-155">Пример:</span><span class="sxs-lookup"><span data-stu-id="a6c1a-155">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="a6c1a-156">Развертывание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="a6c1a-156">Deploy and Run the Application</span></span>

<span data-ttu-id="a6c1a-157">Подготовьте экземпляры Windows Server к развертыванию приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-157">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="a6c1a-158">Добавьте роль IIS.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-158">Add the IIS role.</span></span> <span data-ttu-id="a6c1a-159">Включите функции разработки приложений, включая протокол WebSocket.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-159">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="a6c1a-160">Также включите службу управления (указанную в разделе "средства управления").</span><span class="sxs-lookup"><span data-stu-id="a6c1a-160">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="a6c1a-161">**Установите веб-развертывание 3,0.**</span><span class="sxs-lookup"><span data-stu-id="a6c1a-161">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="a6c1a-162">При запуске диспетчера IIS будет предложено установить веб-платформу Майкрософт, или вы можете [скачать установщик](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="a6c1a-162">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="a6c1a-163">В установщике платформы найдите веб-развертывание и установите веб-развертывание 3,0.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-163">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="a6c1a-164">Убедитесь, что служба веб-управления запущена.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-164">Check that the Web Management Service is running.</span></span> <span data-ttu-id="a6c1a-165">В противном случае запустите службу.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-165">If not, start the service.</span></span> <span data-ttu-id="a6c1a-166">(Если служба веб-управления не отображается в списке служб Windows, убедитесь, что служба управления установлена при добавлении роли IIS.)</span><span class="sxs-lookup"><span data-stu-id="a6c1a-166">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="a6c1a-167">По умолчанию служба веб-управления прослушивает порт TCP 8172.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-167">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="a6c1a-168">В брандмауэре Windows создайте новое правило для входящего трафика, разрешающее TCP-трафик через порт 8172.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-168">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="a6c1a-169">Дополнительные сведения см. в разделе [Настройка правил брандмауэра](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="a6c1a-169">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="a6c1a-170">(Если вы размещаете виртуальные машины в Azure, это можно сделать непосредственно в портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-170">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="a6c1a-171">См. раздел [Настройка конечных точек для виртуальной машины](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="a6c1a-171">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="a6c1a-172">Теперь все готово для развертывания проекта Visual Studio с компьютера разработки на сервере.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-172">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="a6c1a-173">В обозреватель решений щелкните решение правой кнопкой мыши и выберите пункт **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-173">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="a6c1a-174">Более подробную документацию по веб-развертыванию см. в разделе [веб-развертывание Map Web для Visual Studio и ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="a6c1a-174">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="a6c1a-175">При развертывании приложения на двух серверах можно открыть каждый экземпляр в отдельном окне браузера и увидеть, что каждый из них получает сообщения SignalR от другого.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-175">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="a6c1a-176">(Конечно, в рабочей среде два сервера будут находиться за подсистемой балансировки нагрузки.)</span><span class="sxs-lookup"><span data-stu-id="a6c1a-176">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="a6c1a-177">Если вы хотите просмотреть сообщения, отправленные в Redis, можно использовать клиент **Redis-CLI** , который устанавливается вместе с Redis.</span><span class="sxs-lookup"><span data-stu-id="a6c1a-177">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
