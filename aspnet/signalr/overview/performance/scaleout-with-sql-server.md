---
uid: signalr/overview/performance/scaleout-with-sql-server
title: Масштабирование SignalR с помощью SQL Server | Документация Майкрософт
author: bradygaster
description: Версии программного обеспечения, используемые в этом разделе, Visual Studio 2013 .NET 4,5 SignalR версии 2 в предыдущих версиях этого раздела для получения сведений о более ранних версиях...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467742"
---
# <a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="4b7d5-103">Масштабирование SignalR с помощью SQL Server</span><span class="sxs-lookup"><span data-stu-id="4b7d5-103">SignalR Scaleout with SQL Server</span></span>

<span data-ttu-id="4b7d5-104">по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="4b7d5-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="4b7d5-105">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="4b7d5-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="4b7d5-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4b7d5-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="4b7d5-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="4b7d5-107">.NET 4.5</span></span>
> - <span data-ttu-id="4b7d5-108">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="4b7d5-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="4b7d5-109">Предыдущие версии этого раздела</span><span class="sxs-lookup"><span data-stu-id="4b7d5-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="4b7d5-110">Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="4b7d5-111">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="4b7d5-111">Questions and comments</span></span>
>
> <span data-ttu-id="4b7d5-112">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="4b7d5-113">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="4b7d5-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="4b7d5-114">В этом руководстве вы будете использовать SQL Server для распространения сообщений в приложении SignalR, которое развернуто в двух отдельных экземплярах IIS.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="4b7d5-115">Вы также можете запустить этот учебник на одном тестовом компьютере, но чтобы получить полный результат, необходимо развернуть приложение SignalR на двух или более серверах.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="4b7d5-116">Необходимо также установить SQL Server на одном из серверов или на отдельном выделенном сервере.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="4b7d5-117">Другой вариант — Запустить руководство с помощью виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="4b7d5-118">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4b7d5-118">Prerequisites</span></span>

<span data-ttu-id="4b7d5-119">Microsoft SQL Server 2005 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="4b7d5-120">Объединительная плата поддерживает как настольные, так и серверные версии SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="4b7d5-121">Он не поддерживает SQL Server Compact выпуска или базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="4b7d5-122">(Если приложение размещено в Azure, вместо него следует рассмотреть объединительную плату служебной шины.)</span><span class="sxs-lookup"><span data-stu-id="4b7d5-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="4b7d5-123">Обзор</span><span class="sxs-lookup"><span data-stu-id="4b7d5-123">Overview</span></span>

<span data-ttu-id="4b7d5-124">Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="4b7d5-125">Создайте новую пустую базу данных.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-125">Create a new empty database.</span></span> <span data-ttu-id="4b7d5-126">Объединительная плата создаст необходимые таблицы в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="4b7d5-127">Добавьте следующие пакеты NuGet в приложение:</span><span class="sxs-lookup"><span data-stu-id="4b7d5-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="4b7d5-128">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="4b7d5-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="4b7d5-129">Microsoft. AspNet. SignalR. SqlServer</span><span class="sxs-lookup"><span data-stu-id="4b7d5-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="4b7d5-130">Создание приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="4b7d5-131">Добавьте следующий код в Startup.cs, чтобы настроить объединительную плату:</span><span class="sxs-lookup"><span data-stu-id="4b7d5-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="4b7d5-132">Этот код настраивает для объединительной платы значения по умолчанию для [таблекаунт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) и [макскуеуеленгс](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span><span class="sxs-lookup"><span data-stu-id="4b7d5-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="4b7d5-133">Сведения об изменении этих значений см. в разделе [производительность SignalR: метрики масштабирования](signalr-performance.md#scaleout_metrics).</span><span class="sxs-lookup"><span data-stu-id="4b7d5-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="4b7d5-134">Настройка базы данных</span><span class="sxs-lookup"><span data-stu-id="4b7d5-134">Configure the Database</span></span>

<span data-ttu-id="4b7d5-135">Определите, будет ли приложение использовать проверку подлинности Windows или проверку подлинности SQL Server для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="4b7d5-136">В любом случае убедитесь, что пользователь базы данных имеет разрешения на вход, создание схем и создание таблиц.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="4b7d5-137">Создайте новую базу данных для использования с объединительной платой.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="4b7d5-138">Можно присвоить базе данных любое имя.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-138">You can give the database any name.</span></span> <span data-ttu-id="4b7d5-139">Не нужно создавать таблицы в базе данных; Объединительная плата создаст необходимые таблицы.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="4b7d5-140">Включить Service Broker</span><span class="sxs-lookup"><span data-stu-id="4b7d5-140">Enable Service Broker</span></span>

<span data-ttu-id="4b7d5-141">Рекомендуется включить Service Broker для базы данных объединительной платы.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="4b7d5-142">Service Broker обеспечивает собственную поддержку обмена сообщениями и очередей в SQL Server, что позволяет повысить эффективность получения обновлений на объединительной плате.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="4b7d5-143">(Однако задняя панель также работает без Service Broker.)</span><span class="sxs-lookup"><span data-stu-id="4b7d5-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="4b7d5-144">Чтобы проверить, включена ли Service Broker, запросите столбец **\_Broker\_включен** в представлении каталога **sys. databases** .</span><span class="sxs-lookup"><span data-stu-id="4b7d5-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="4b7d5-145">Чтобы включить Service Broker, используйте следующий запрос SQL:</span><span class="sxs-lookup"><span data-stu-id="4b7d5-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="4b7d5-146">Если этот запрос выглядит как взаимоблокировка, убедитесь, что к базе данных не подключено ни одного приложения.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="4b7d5-147">Если трассировка включена, трассировки также показывают, включена ли Service Broker.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="4b7d5-148">Создание приложения SignalR</span><span class="sxs-lookup"><span data-stu-id="4b7d5-148">Create a SignalR Application</span></span>

<span data-ttu-id="4b7d5-149">Создайте приложение SignalR, следуя одному из следующих учебников:</span><span class="sxs-lookup"><span data-stu-id="4b7d5-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="4b7d5-150">Начало работы с SignalR 2,0</span><span class="sxs-lookup"><span data-stu-id="4b7d5-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="4b7d5-151">Начало работы с SignalR 2,0 и MVC 5</span><span class="sxs-lookup"><span data-stu-id="4b7d5-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="4b7d5-152">Далее мы изменим приложение разговора для поддержки масштабирования с SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="4b7d5-153">Сначала добавьте в проект пакет NuGet SignalR. SqlServer.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="4b7d5-154">В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="4b7d5-155">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4b7d5-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="4b7d5-156">Затем откройте файл Startup.cs.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="4b7d5-157">Добавьте следующий код в метод **Configure** :</span><span class="sxs-lookup"><span data-stu-id="4b7d5-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="4b7d5-158">Развертывание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="4b7d5-158">Deploy and Run the Application</span></span>

<span data-ttu-id="4b7d5-159">Подготовьте экземпляры Windows Server к развертыванию приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="4b7d5-160">Добавьте роль IIS.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-160">Add the IIS role.</span></span> <span data-ttu-id="4b7d5-161">Включите функции разработки приложений, включая протокол WebSocket.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="4b7d5-162">Также включите службу управления (указанную в разделе "средства управления").</span><span class="sxs-lookup"><span data-stu-id="4b7d5-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="4b7d5-163">**Установите веб-развертывание 3,0.**</span><span class="sxs-lookup"><span data-stu-id="4b7d5-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="4b7d5-164">При запуске диспетчера IIS будет предложено установить веб-платформу Майкрософт, или вы можете [скачать установщик](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="4b7d5-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="4b7d5-165">В установщике платформы найдите веб-развертывание и установите веб-развертывание 3,0.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="4b7d5-166">Убедитесь, что служба веб-управления запущена.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="4b7d5-167">В противном случае запустите службу.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-167">If not, start the service.</span></span> <span data-ttu-id="4b7d5-168">(Если служба веб-управления не отображается в списке служб Windows, убедитесь, что служба управления установлена при добавлении роли IIS.)</span><span class="sxs-lookup"><span data-stu-id="4b7d5-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="4b7d5-169">Наконец, откройте порт 8172 для TCP.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="4b7d5-170">Это порт, используемый средством веб-развертывание.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="4b7d5-171">Теперь все готово для развертывания проекта Visual Studio с компьютера разработки на сервере.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="4b7d5-172">В обозреватель решений щелкните решение правой кнопкой мыши и выберите пункт **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="4b7d5-173">Более подробную документацию по веб-развертыванию см. в разделе [веб-развертывание Map Web для Visual Studio и ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="4b7d5-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="4b7d5-174">При развертывании приложения на двух серверах можно открыть каждый экземпляр в отдельном окне браузера и увидеть, что каждый из них получает сообщения SignalR от другого.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="4b7d5-175">(Конечно, в рабочей среде два сервера будут находиться за подсистемой балансировки нагрузки.)</span><span class="sxs-lookup"><span data-stu-id="4b7d5-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="4b7d5-176">После запуска приложения вы увидите, что SignalR автоматически создал таблицы в базе данных:</span><span class="sxs-lookup"><span data-stu-id="4b7d5-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="4b7d5-177">SignalR управляет таблицами.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-177">SignalR manages the tables.</span></span> <span data-ttu-id="4b7d5-178">Пока приложение развернуто, не удаляйте строки, модифицируйте таблицу и т. д.</span><span class="sxs-lookup"><span data-stu-id="4b7d5-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
