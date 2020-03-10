---
uid: signalr/overview/performance/scaleout-with-redis
title: Масштабирование SignalR с помощью Redis | Документация Майкрософт
author: bradygaster
description: Версии программного обеспечения, используемые в этом разделе, Visual Studio 2013 .NET 4,5 SignalR версии 2 в предыдущих версиях этого раздела для получения сведений о более ранних версиях...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467778"
---
# <a name="signalr-scaleout-with-redis"></a><span data-ttu-id="b379d-103">Масштабирование SignalR с помощью Redis</span><span class="sxs-lookup"><span data-stu-id="b379d-103">SignalR Scaleout with Redis</span></span>

<span data-ttu-id="b379d-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b379d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="b379d-105">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="b379d-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="b379d-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b379d-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="b379d-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b379d-107">.NET 4.5</span></span>
> - <span data-ttu-id="b379d-108">SignalR версии 2,4</span><span class="sxs-lookup"><span data-stu-id="b379d-108">SignalR version 2.4</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="b379d-109">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="b379d-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="b379d-110">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="b379d-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="b379d-111">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="b379d-111">Questions and comments</span></span>
>
> <span data-ttu-id="b379d-112">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b379d-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b379d-113">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="b379d-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="b379d-114">В этом руководстве вы будете использовать [Redis](http://redis.io/) для распространения сообщений в приложении SignalR, которое развернуто на двух отдельных экземплярах IIS.</span><span class="sxs-lookup"><span data-stu-id="b379d-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="b379d-115">Redis — это хранилище "ключ — значение" в памяти.</span><span class="sxs-lookup"><span data-stu-id="b379d-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="b379d-116">Она также поддерживает систему обмена сообщениями с моделью публикации и подписки.</span><span class="sxs-lookup"><span data-stu-id="b379d-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="b379d-117">Для пересылки сообщений на другие серверы в объединительной плате Redis SignalR используется функция Pub/Re-in.</span><span class="sxs-lookup"><span data-stu-id="b379d-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="b379d-118">В рамках этого руководства вы будете использовать три сервера:</span><span class="sxs-lookup"><span data-stu-id="b379d-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="b379d-119">Два сервера под Windows, которые будут использоваться для развертывания приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="b379d-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="b379d-120">Один сервер под управлением Linux, который будет использоваться для запуска Redis.</span><span class="sxs-lookup"><span data-stu-id="b379d-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="b379d-121">Для снимков экрана в этом учебнике я использовал Ubuntu 12,04 TLS.</span><span class="sxs-lookup"><span data-stu-id="b379d-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="b379d-122">Если у вас нет трех физических серверов, можно создать виртуальные машины в Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b379d-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="b379d-123">Другой вариант — создать виртуальные машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="b379d-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="b379d-124">Хотя в этом учебнике используется официальная реализация Redis, в MSOpenTech также есть [порт Windows Redis](https://github.com/MSOpenTech/redis) .</span><span class="sxs-lookup"><span data-stu-id="b379d-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="b379d-125">Установка и настройка различаются, но в противном случае шаги одинаковы.</span><span class="sxs-lookup"><span data-stu-id="b379d-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b379d-126">Масштабирование SignalR с помощью Redis не поддерживает кластеры Redis.</span><span class="sxs-lookup"><span data-stu-id="b379d-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="b379d-127">Обзор</span><span class="sxs-lookup"><span data-stu-id="b379d-127">Overview</span></span>

<span data-ttu-id="b379d-128">Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.</span><span class="sxs-lookup"><span data-stu-id="b379d-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="b379d-129">Установите Redis и запустите сервер Redis.</span><span class="sxs-lookup"><span data-stu-id="b379d-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="b379d-130">Добавьте следующие пакеты NuGet в приложение:</span><span class="sxs-lookup"><span data-stu-id="b379d-130">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="b379d-131">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="b379d-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="b379d-132">Microsoft. AspNet. SignalR. Стаккексчанжередис</span><span class="sxs-lookup"><span data-stu-id="b379d-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. <span data-ttu-id="b379d-133">Создание приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="b379d-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="b379d-134">Добавьте следующий код в Startup.cs, чтобы настроить объединительную плату:</span><span class="sxs-lookup"><span data-stu-id="b379d-134">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="b379d-135">Ubuntu на Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b379d-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="b379d-136">С помощью Windows Hyper-V вы можете легко создать виртуальную машину Ubuntu на Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b379d-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="b379d-137">Скачайте ISO-образ Ubuntu с [http://www.ubuntu.com](http://www.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="b379d-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="b379d-138">В Hyper-V добавьте новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="b379d-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="b379d-139">На шаге **Подключить виртуальный жесткий диск** выберите **создать виртуальный жесткий диск**.</span><span class="sxs-lookup"><span data-stu-id="b379d-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="b379d-140">На шаге **Параметры установки** выберите **файл образа (. ISO)** , нажмите кнопку **Обзор**и перейдите к ISO-образ установки Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b379d-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="b379d-141">Установка Redis</span><span class="sxs-lookup"><span data-stu-id="b379d-141">Install Redis</span></span>

<span data-ttu-id="b379d-142">Выполните действия, описанные в [http://redis.io/download](http://redis.io/download) , чтобы скачать и создать Redis.</span><span class="sxs-lookup"><span data-stu-id="b379d-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="b379d-143">Это приведет к сборке двоичных файлов Redis в каталоге `src`.</span><span class="sxs-lookup"><span data-stu-id="b379d-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="b379d-144">По умолчанию Redis не требует пароля.</span><span class="sxs-lookup"><span data-stu-id="b379d-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="b379d-145">Чтобы задать пароль, измените файл `redis.conf`, который находится в корневом каталоге исходного кода.</span><span class="sxs-lookup"><span data-stu-id="b379d-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="b379d-146">(Создайте резервную копию файла, прежде чем изменять его!) Добавьте следующую директиву в `redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="b379d-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="b379d-147">Теперь запустите сервер Redis:</span><span class="sxs-lookup"><span data-stu-id="b379d-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="b379d-148">Откройте порт 6379. это порт по умолчанию, который прослушивается Redis.</span><span class="sxs-lookup"><span data-stu-id="b379d-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="b379d-149">(Номер порта можно изменить в файле конфигурации.)</span><span class="sxs-lookup"><span data-stu-id="b379d-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="b379d-150">Создание приложения SignalR</span><span class="sxs-lookup"><span data-stu-id="b379d-150">Create the SignalR Application</span></span>

<span data-ttu-id="b379d-151">Создайте приложение SignalR, следуя одному из следующих учебников:</span><span class="sxs-lookup"><span data-stu-id="b379d-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="b379d-152">Начало работы с SignalR 2,0</span><span class="sxs-lookup"><span data-stu-id="b379d-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="b379d-153">Начало работы с SignalR 2,0 и MVC 5</span><span class="sxs-lookup"><span data-stu-id="b379d-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="b379d-154">Далее мы изменим приложение разговора для поддержки масштабирования с помощью Redis.</span><span class="sxs-lookup"><span data-stu-id="b379d-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="b379d-155">Сначала добавьте `Microsoft.AspNet.SignalR.StackExchangeRedis` пакет NuGet в проект.</span><span class="sxs-lookup"><span data-stu-id="b379d-155">First, add the `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet package to your project.</span></span> <span data-ttu-id="b379d-156">В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="b379d-156">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b379d-157">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b379d-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="b379d-158">Затем откройте файл Startup.cs.</span><span class="sxs-lookup"><span data-stu-id="b379d-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="b379d-159">Добавьте следующий код в метод **конфигурации** :</span><span class="sxs-lookup"><span data-stu-id="b379d-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="b379d-160">"Server" — имя сервера, на котором работает Redis.</span><span class="sxs-lookup"><span data-stu-id="b379d-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="b379d-161">*порт* — номер порта.</span><span class="sxs-lookup"><span data-stu-id="b379d-161">*port* is the port number</span></span>
- <span data-ttu-id="b379d-162">Password — это пароль, определенный в файле Redis. conf.</span><span class="sxs-lookup"><span data-stu-id="b379d-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="b379d-163">AppName — любая строка.</span><span class="sxs-lookup"><span data-stu-id="b379d-163">"AppName" is any string.</span></span> <span data-ttu-id="b379d-164">SignalR создает канал Pub/Redis с таким именем.</span><span class="sxs-lookup"><span data-stu-id="b379d-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="b379d-165">Пример:</span><span class="sxs-lookup"><span data-stu-id="b379d-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="b379d-166">Развертывание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b379d-166">Deploy and Run the Application</span></span>

<span data-ttu-id="b379d-167">Подготовьте экземпляры Windows Server к развертыванию приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="b379d-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="b379d-168">Добавьте роль IIS.</span><span class="sxs-lookup"><span data-stu-id="b379d-168">Add the IIS role.</span></span> <span data-ttu-id="b379d-169">Включите функции разработки приложений, включая протокол WebSocket.</span><span class="sxs-lookup"><span data-stu-id="b379d-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="b379d-170">Также включите службу управления (указанную в разделе "средства управления").</span><span class="sxs-lookup"><span data-stu-id="b379d-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="b379d-171">**Установите веб-развертывание 3,0.**</span><span class="sxs-lookup"><span data-stu-id="b379d-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="b379d-172">При запуске диспетчера IIS будет предложено установить веб-платформу Майкрософт, или вы можете [скачать установщик](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="b379d-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="b379d-173">В установщике платформы найдите веб-развертывание и установите веб-развертывание 3,0.</span><span class="sxs-lookup"><span data-stu-id="b379d-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="b379d-174">Убедитесь, что служба веб-управления запущена.</span><span class="sxs-lookup"><span data-stu-id="b379d-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="b379d-175">В противном случае запустите службу.</span><span class="sxs-lookup"><span data-stu-id="b379d-175">If not, start the service.</span></span> <span data-ttu-id="b379d-176">(Если служба веб-управления не отображается в списке служб Windows, убедитесь, что служба управления установлена при добавлении роли IIS.)</span><span class="sxs-lookup"><span data-stu-id="b379d-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="b379d-177">По умолчанию служба веб-управления прослушивает порт TCP 8172.</span><span class="sxs-lookup"><span data-stu-id="b379d-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="b379d-178">В брандмауэре Windows создайте новое правило для входящего трафика, разрешающее TCP-трафик через порт 8172.</span><span class="sxs-lookup"><span data-stu-id="b379d-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="b379d-179">Дополнительные сведения см. в разделе [Настройка правил брандмауэра](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="b379d-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="b379d-180">(Если вы размещаете виртуальные машины в Azure, это можно сделать непосредственно в портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b379d-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="b379d-181">См. раздел [Настройка конечных точек для виртуальной машины](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="b379d-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="b379d-182">Теперь все готово для развертывания проекта Visual Studio с компьютера разработки на сервере.</span><span class="sxs-lookup"><span data-stu-id="b379d-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="b379d-183">В обозреватель решений щелкните решение правой кнопкой мыши и выберите пункт **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b379d-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="b379d-184">Более подробную документацию по веб-развертыванию см. в разделе [веб-развертывание Map Web для Visual Studio и ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="b379d-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="b379d-185">При развертывании приложения на двух серверах можно открыть каждый экземпляр в отдельном окне браузера и увидеть, что каждый из них получает сообщения SignalR от другого.</span><span class="sxs-lookup"><span data-stu-id="b379d-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="b379d-186">(Конечно, в рабочей среде два сервера будут находиться за подсистемой балансировки нагрузки.)</span><span class="sxs-lookup"><span data-stu-id="b379d-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="b379d-187">Если вы хотите просмотреть сообщения, отправленные в Redis, можно использовать клиент **Redis-CLI** , который устанавливается вместе с Redis.</span><span class="sxs-lookup"><span data-stu-id="b379d-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
