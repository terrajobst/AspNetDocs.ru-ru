---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: Масштабирование SignalR с SQL Server (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431130"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a><span data-ttu-id="458e7-102">Масштабирование SignalR с помощью SQL Server (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="458e7-102">SignalR Scaleout with SQL Server (SignalR 1.x)</span></span>

<span data-ttu-id="458e7-103">по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="458e7-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="458e7-104">В этом руководстве вы будете использовать SQL Server для распространения сообщений в приложении SignalR, которое развернуто в двух отдельных экземплярах IIS.</span><span class="sxs-lookup"><span data-stu-id="458e7-104">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="458e7-105">Вы также можете запустить этот учебник на одном тестовом компьютере, но чтобы получить полный результат, необходимо развернуть приложение SignalR на двух или более серверах.</span><span class="sxs-lookup"><span data-stu-id="458e7-105">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="458e7-106">Необходимо также установить SQL Server на одном из серверов или на отдельном выделенном сервере.</span><span class="sxs-lookup"><span data-stu-id="458e7-106">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="458e7-107">Другой вариант — Запустить руководство с помощью виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="458e7-107">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="458e7-108">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="458e7-108">Prerequisites</span></span>

<span data-ttu-id="458e7-109">Microsoft SQL Server 2005 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="458e7-109">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="458e7-110">Объединительная плата поддерживает как настольные, так и серверные версии SQL Server.</span><span class="sxs-lookup"><span data-stu-id="458e7-110">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="458e7-111">Он не поддерживает SQL Server Compact выпуска или базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="458e7-111">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="458e7-112">(Если приложение размещено в Azure, вместо него следует рассмотреть объединительную плату служебной шины.)</span><span class="sxs-lookup"><span data-stu-id="458e7-112">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="458e7-113">Обзор</span><span class="sxs-lookup"><span data-stu-id="458e7-113">Overview</span></span>

<span data-ttu-id="458e7-114">Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.</span><span class="sxs-lookup"><span data-stu-id="458e7-114">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="458e7-115">Создайте новую пустую базу данных.</span><span class="sxs-lookup"><span data-stu-id="458e7-115">Create a new empty database.</span></span> <span data-ttu-id="458e7-116">Объединительная плата создаст необходимые таблицы в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="458e7-116">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="458e7-117">Добавьте следующие пакеты NuGet в приложение:</span><span class="sxs-lookup"><span data-stu-id="458e7-117">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="458e7-118">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="458e7-118">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="458e7-119">Microsoft. AspNet. SignalR. SqlServer</span><span class="sxs-lookup"><span data-stu-id="458e7-119">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="458e7-120">Создание приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="458e7-120">Create a SignalR application.</span></span>
4. <span data-ttu-id="458e7-121">Добавьте следующий код в Global. asax для настройки объединительной платы:</span><span class="sxs-lookup"><span data-stu-id="458e7-121">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a><span data-ttu-id="458e7-122">Настройка базы данных</span><span class="sxs-lookup"><span data-stu-id="458e7-122">Configure the Database</span></span>

<span data-ttu-id="458e7-123">Определите, будет ли приложение использовать проверку подлинности Windows или проверку подлинности SQL Server для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="458e7-123">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="458e7-124">В любом случае убедитесь, что пользователь базы данных имеет разрешения на вход, создание схем и создание таблиц.</span><span class="sxs-lookup"><span data-stu-id="458e7-124">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="458e7-125">Создайте новую базу данных для использования с объединительной платой.</span><span class="sxs-lookup"><span data-stu-id="458e7-125">Create a new database for the backplane to use.</span></span> <span data-ttu-id="458e7-126">Можно присвоить базе данных любое имя.</span><span class="sxs-lookup"><span data-stu-id="458e7-126">You can give the database any name.</span></span> <span data-ttu-id="458e7-127">Не нужно создавать таблицы в базе данных; Объединительная плата создаст необходимые таблицы.</span><span class="sxs-lookup"><span data-stu-id="458e7-127">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="458e7-128">Включить Service Broker</span><span class="sxs-lookup"><span data-stu-id="458e7-128">Enable Service Broker</span></span>

<span data-ttu-id="458e7-129">Рекомендуется включить Service Broker для базы данных объединительной платы.</span><span class="sxs-lookup"><span data-stu-id="458e7-129">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="458e7-130">Service Broker обеспечивает собственную поддержку обмена сообщениями и очередей в SQL Server, что позволяет повысить эффективность получения обновлений на объединительной плате.</span><span class="sxs-lookup"><span data-stu-id="458e7-130">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="458e7-131">(Однако задняя панель также работает без Service Broker.)</span><span class="sxs-lookup"><span data-stu-id="458e7-131">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="458e7-132">Чтобы проверить, включена ли Service Broker, запросите столбец **\_Broker\_включен** в представлении каталога **sys. databases** .</span><span class="sxs-lookup"><span data-stu-id="458e7-132">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="458e7-133">Чтобы включить Service Broker, используйте следующий запрос SQL:</span><span class="sxs-lookup"><span data-stu-id="458e7-133">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="458e7-134">Если этот запрос выглядит как взаимоблокировка, убедитесь, что к базе данных не подключено ни одного приложения.</span><span class="sxs-lookup"><span data-stu-id="458e7-134">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="458e7-135">Если трассировка включена, трассировки также показывают, включена ли Service Broker.</span><span class="sxs-lookup"><span data-stu-id="458e7-135">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="458e7-136">Создание приложения SignalR</span><span class="sxs-lookup"><span data-stu-id="458e7-136">Create a SignalR Application</span></span>

<span data-ttu-id="458e7-137">Создайте приложение SignalR, следуя одному из следующих учебников:</span><span class="sxs-lookup"><span data-stu-id="458e7-137">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="458e7-138">начало работы с SignalR</span><span class="sxs-lookup"><span data-stu-id="458e7-138">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="458e7-139">начало работы с SignalR и MVC 4</span><span class="sxs-lookup"><span data-stu-id="458e7-139">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="458e7-140">Далее мы изменим приложение разговора для поддержки масштабирования с SQL Server.</span><span class="sxs-lookup"><span data-stu-id="458e7-140">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="458e7-141">Сначала добавьте в проект пакет NuGet SignalR. SqlServer.</span><span class="sxs-lookup"><span data-stu-id="458e7-141">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="458e7-142">В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="458e7-142">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="458e7-143">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="458e7-143">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="458e7-144">Затем откройте файл Global. asax.</span><span class="sxs-lookup"><span data-stu-id="458e7-144">Next, open the Global.asax file.</span></span> <span data-ttu-id="458e7-145">Добавьте следующий код в метод **\_запуска приложения** :</span><span class="sxs-lookup"><span data-stu-id="458e7-145">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="458e7-146">Развертывание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="458e7-146">Deploy and Run the Application</span></span>

<span data-ttu-id="458e7-147">Подготовьте экземпляры Windows Server к развертыванию приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="458e7-147">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="458e7-148">Добавьте роль IIS.</span><span class="sxs-lookup"><span data-stu-id="458e7-148">Add the IIS role.</span></span> <span data-ttu-id="458e7-149">Включите функции разработки приложений, включая протокол WebSocket.</span><span class="sxs-lookup"><span data-stu-id="458e7-149">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="458e7-150">Также включите службу управления (указанную в разделе "средства управления").</span><span class="sxs-lookup"><span data-stu-id="458e7-150">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="458e7-151">**Установите веб-развертывание 3,0.**</span><span class="sxs-lookup"><span data-stu-id="458e7-151">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="458e7-152">При запуске диспетчера IIS будет предложено установить веб-платформу Майкрософт, или вы можете [скачать установщик](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="458e7-152">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="458e7-153">В установщике платформы найдите веб-развертывание и установите веб-развертывание 3,0.</span><span class="sxs-lookup"><span data-stu-id="458e7-153">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="458e7-154">Убедитесь, что служба веб-управления запущена.</span><span class="sxs-lookup"><span data-stu-id="458e7-154">Check that the Web Management Service is running.</span></span> <span data-ttu-id="458e7-155">В противном случае запустите службу.</span><span class="sxs-lookup"><span data-stu-id="458e7-155">If not, start the service.</span></span> <span data-ttu-id="458e7-156">(Если служба веб-управления не отображается в списке служб Windows, убедитесь, что служба управления установлена при добавлении роли IIS.)</span><span class="sxs-lookup"><span data-stu-id="458e7-156">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="458e7-157">Наконец, откройте порт 8172 для TCP.</span><span class="sxs-lookup"><span data-stu-id="458e7-157">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="458e7-158">Это порт, используемый средством веб-развертывание.</span><span class="sxs-lookup"><span data-stu-id="458e7-158">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="458e7-159">Теперь все готово для развертывания проекта Visual Studio с компьютера разработки на сервере.</span><span class="sxs-lookup"><span data-stu-id="458e7-159">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="458e7-160">В обозреватель решений щелкните решение правой кнопкой мыши и выберите пункт **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="458e7-160">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="458e7-161">Более подробную документацию по веб-развертыванию см. в разделе [веб-развертывание Map Web для Visual Studio и ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="458e7-161">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="458e7-162">При развертывании приложения на двух серверах можно открыть каждый экземпляр в отдельном окне браузера и увидеть, что каждый из них получает сообщения SignalR от другого.</span><span class="sxs-lookup"><span data-stu-id="458e7-162">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="458e7-163">(Конечно, в рабочей среде два сервера будут находиться за подсистемой балансировки нагрузки.)</span><span class="sxs-lookup"><span data-stu-id="458e7-163">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="458e7-164">После запуска приложения вы увидите, что SignalR автоматически создал таблицы в базе данных:</span><span class="sxs-lookup"><span data-stu-id="458e7-164">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="458e7-165">SignalR управляет таблицами.</span><span class="sxs-lookup"><span data-stu-id="458e7-165">SignalR manages the tables.</span></span> <span data-ttu-id="458e7-166">Пока приложение развернуто, не удаляйте строки, модифицируйте таблицу и т. д.</span><span class="sxs-lookup"><span data-stu-id="458e7-166">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
