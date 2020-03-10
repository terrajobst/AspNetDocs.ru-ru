---
uid: whitepapers/aspnet-and-iis6
title: Запуск ASP.NET 1,1 с IIS 6,0 | Документация Майкрософт
author: rick-anderson
description: Хотя Windows Server 2003 включает как IIS 6,0, так и ASP.NET 1,1, эти компоненты по умолчанию отключены. В этом техническом документе описано, как включить IIS 6,0...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419850"
---
# <a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="7e95d-104">Запуск ASP.NET 1.1 со службами IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="7e95d-104">Running ASP.NET 1.1 with IIS 6.0</span></span>

> <span data-ttu-id="7e95d-105">Хотя Windows Server 2003 включает как IIS 6,0, так и ASP.NET 1,1, эти компоненты по умолчанию отключены.</span><span class="sxs-lookup"><span data-stu-id="7e95d-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="7e95d-106">В этом техническом документе описано, как включить службы IIS 6,0 и ASP.NET 1,1, а также рекомендации по нескольким параметрам конфигурации, чтобы обеспечить оптимальную производительность служб IIS и ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7e95d-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="7e95d-107">Применяется к ASP.NET 1,1 и IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="7e95d-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>

<span data-ttu-id="7e95d-108">ASP.NET 1,1 поставляется с Windows Server 2003, который также включает последнюю версию Internet Information Server (IIS) версии 6,0.</span><span class="sxs-lookup"><span data-stu-id="7e95d-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="7e95d-109">Службы IIS 6,0 и ASP.NET 1,1 разработаны для беспрепятственной интеграции и ASP.NET теперь по умолчанию используют новую модель рабочего процесса IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="7e95d-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="7e95d-110">ASP.NET 1,1 не устанавливается по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7e95d-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="7e95d-111">В отличие от предыдущих версий серверных операционных систем Майкрософт, сервер IIS не включен по умолчанию. и не является ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="7e95d-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="7e95d-112">Существует два варианта включения служб IIS.</span><span class="sxs-lookup"><span data-stu-id="7e95d-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="7e95d-113">Включение служб IIS, параметр #1-мастер настройки сервера</span><span class="sxs-lookup"><span data-stu-id="7e95d-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="7e95d-114">В состав Windows Server 2003 входит новый мастер настройки сервера, позволяющий правильно настроить сервер в нужном режиме.</span><span class="sxs-lookup"><span data-stu-id="7e95d-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="7e95d-115">Чтобы запустить мастер, заметьте, что для запуска мастера необходимо войти в систему с правами администратора. перейти к: запуск | Программы | Средства администрирования и выберите "настроить сервер".</span><span class="sxs-lookup"><span data-stu-id="7e95d-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="7e95d-116">После выбора вы увидите экран мастера настройки сервера:</span><span class="sxs-lookup"><span data-stu-id="7e95d-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="7e95d-117">Нажмите кнопку "далее &gt;":</span><span class="sxs-lookup"><span data-stu-id="7e95d-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="7e95d-118">Нажмите кнопку "далее &gt;".</span><span class="sxs-lookup"><span data-stu-id="7e95d-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="7e95d-119">На этом экране необходимо выбрать "сервер приложений (IIS, ASP.NET)" в качестве параметров для настройки.</span><span class="sxs-lookup"><span data-stu-id="7e95d-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="7e95d-120">Нажмите кнопку "далее &gt;".</span><span class="sxs-lookup"><span data-stu-id="7e95d-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="7e95d-121">После выбора настройки сервера в качестве сервера приложений на экране отобразится запрос на ввод дополнительных возможностей, которые следует установить.</span><span class="sxs-lookup"><span data-stu-id="7e95d-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="7e95d-122">По умолчанию ни один из этих параметров не выбран.</span><span class="sxs-lookup"><span data-stu-id="7e95d-122">Neither option is selected by default.</span></span> <span data-ttu-id="7e95d-123">Чтобы включить ASP.NET автоматически, необходимо выбрать параметр "включить ASP. NET ".</span><span class="sxs-lookup"><span data-stu-id="7e95d-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="7e95d-124">Нажмите кнопку "далее &gt;".</span><span class="sxs-lookup"><span data-stu-id="7e95d-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="7e95d-125">На этом экране отображаются параметры, которые необходимо установить.</span><span class="sxs-lookup"><span data-stu-id="7e95d-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="7e95d-126">Нажмите кнопку "далее &gt;".</span><span class="sxs-lookup"><span data-stu-id="7e95d-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="7e95d-127">Вы увидите этот экран во время установки выбранных параметров.</span><span class="sxs-lookup"><span data-stu-id="7e95d-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="7e95d-128">Обычные диалоговые окна отображаются, когда устанавливаются службы.</span><span class="sxs-lookup"><span data-stu-id="7e95d-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="7e95d-129">Кроме того, вам может быть предложено указать расположение установочного компакт-диска Windows 2003 Server.</span><span class="sxs-lookup"><span data-stu-id="7e95d-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="7e95d-130">По завершении нажмите кнопку "далее &gt;".</span><span class="sxs-lookup"><span data-stu-id="7e95d-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="7e95d-131">Нажмите кнопку "Готово" — теперь Windows Server 2003 настроен для поддержки IIS 6,0 и ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="7e95d-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="7e95d-132">Включение служб IIS, #2 параметров — Настройка IIS и ASP.NET вручную</span><span class="sxs-lookup"><span data-stu-id="7e95d-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="7e95d-133">Если вы не хотите использовать мастер настройки сервера, можно дополнительно установить IIS 6,0 и ASP.NET 1,1 с помощью компонента "Установка и удаление программ" на панели управления.</span><span class="sxs-lookup"><span data-stu-id="7e95d-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="7e95d-134">Сначала откройте панель управления:</span><span class="sxs-lookup"><span data-stu-id="7e95d-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="7e95d-135">Затем нажмите кнопку "Добавить/удалить компоненты Windows", которая откроет мастер компонентов Windows:</span><span class="sxs-lookup"><span data-stu-id="7e95d-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="7e95d-136">Выделите и проверьте "сервер приложений", а затем щелкните "сведения".</span><span class="sxs-lookup"><span data-stu-id="7e95d-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="7e95d-137">переключатель</span><span class="sxs-lookup"><span data-stu-id="7e95d-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="7e95d-138">Чтобы установить ASP.NET, установите флажок "ASP. NET ".</span><span class="sxs-lookup"><span data-stu-id="7e95d-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="7e95d-139">Нажмите кнопку "ОК", чтобы вернуться к мастеру компонентов Windows.</span><span class="sxs-lookup"><span data-stu-id="7e95d-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="7e95d-140">Чтобы начать установку, нажмите кнопку "далее &gt;" в мастере компонентов Windows:</span><span class="sxs-lookup"><span data-stu-id="7e95d-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="7e95d-141">Обычные диалоговые окна отображаются, когда устанавливаются службы.</span><span class="sxs-lookup"><span data-stu-id="7e95d-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="7e95d-142">Кроме того, вам может быть предложено указать расположение установочного компакт-диска Windows 2003 Server.</span><span class="sxs-lookup"><span data-stu-id="7e95d-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="7e95d-143">После завершения установки вы увидите последний экран мастера компонентов Windows:</span><span class="sxs-lookup"><span data-stu-id="7e95d-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="7e95d-144">Службы IIS 6,0 и ASP.NET 1,1 теперь настроены и доступны.</span><span class="sxs-lookup"><span data-stu-id="7e95d-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="7e95d-145">Рекомендуемые параметры</span><span class="sxs-lookup"><span data-stu-id="7e95d-145">Recommended Settings</span></span>

<span data-ttu-id="7e95d-146">При запуске ASP.NET 1,1 с IIS 6,0 для достижения оптимальной производительности из ASP.NET рекомендуется использовать несколько параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7e95d-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="7e95d-147">Настройка ограничений памяти для рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="7e95d-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="7e95d-148">Настройка повторного запуска рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="7e95d-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="7e95d-149">Настройка ограничений памяти для рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="7e95d-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="7e95d-150">По умолчанию IIS 6,0 не устанавливает ограничение на объем памяти, который может использовать IIS.</span><span class="sxs-lookup"><span data-stu-id="7e95d-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="7e95d-151">Сценарии. Функция кэширования в сети основана на ограничении памяти, поэтому кэш может заранее удалить неиспользуемые элементы из памяти.</span><span class="sxs-lookup"><span data-stu-id="7e95d-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="7e95d-152">Рекомендуется настроить функцию повторного использования памяти в IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="7e95d-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="7e95d-153">Настройка этого открытого диспетчера службы IIS (Start | Программы | Администрирование | Службы IIS).</span><span class="sxs-lookup"><span data-stu-id="7e95d-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="7e95d-154">После открытия разверните папку "пулы приложений":</span><span class="sxs-lookup"><span data-stu-id="7e95d-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="7e95d-155">Для каждого пула приложений:</span><span class="sxs-lookup"><span data-stu-id="7e95d-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="7e95d-156">Щелкните правой кнопкой мыши пул приложений, например "DefaultAppPool", и выберите "Свойства":</span><span class="sxs-lookup"><span data-stu-id="7e95d-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="7e95d-157">Затем включите повторное использование памяти, щелкнув "максимальный объем используемой памяти (в мегабайтах)": ".</span><span class="sxs-lookup"><span data-stu-id="7e95d-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="7e95d-158">Значение не должно быть больше объема физической (невиртуальной) памяти на сервере, а оптимальное приближение — 60% от физической памяти, т. е. для сервера с физической памятью 512 МБ выберите 310.</span><span class="sxs-lookup"><span data-stu-id="7e95d-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="7e95d-159">Кроме того, при использовании пространства адресов размером 2 ГБ рекомендуется не более 800MB.</span><span class="sxs-lookup"><span data-stu-id="7e95d-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="7e95d-160">Если адресное пространство памяти сервера равно 3 ГБ, максимальный предел памяти для рабочего процесса может быть таким же, как 1, 800MB:</span><span class="sxs-lookup"><span data-stu-id="7e95d-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="7e95d-161">Нажмите кнопку "Применить" и "ОК", чтобы закрыть диалоговое окно свойств.</span><span class="sxs-lookup"><span data-stu-id="7e95d-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="7e95d-162">Повторите эти действия для всех доступных пулов приложений.</span><span class="sxs-lookup"><span data-stu-id="7e95d-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="7e95d-163">Настройка повторного использования рабочих ролей</span><span class="sxs-lookup"><span data-stu-id="7e95d-163">Configuring worker recycling</span></span>

<span data-ttu-id="7e95d-164">По умолчанию IIS 6,0 настроен на повторный запуск рабочего процесса каждые 29 часов.</span><span class="sxs-lookup"><span data-stu-id="7e95d-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="7e95d-165">Это немного агрессивно для приложения, в котором выполняется ASP.NET, и рекомендуется отключить автоматический перезапуск рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="7e95d-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="7e95d-166">Чтобы отключить автоматический перезапуск рабочих процессов, сначала откройте диспетчер службы IIS (Start | Программы | Администрирование | Службы IIS).</span><span class="sxs-lookup"><span data-stu-id="7e95d-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="7e95d-167">После открытия разверните папку "пулы приложений":</span><span class="sxs-lookup"><span data-stu-id="7e95d-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="7e95d-168">Для каждого пула приложений:</span><span class="sxs-lookup"><span data-stu-id="7e95d-168">For each application pool:</span></span>

1. <span data-ttu-id="7e95d-169">Щелкните правой кнопкой мыши пул приложений, например "DefaultAppPool", и выберите "Свойства":</span><span class="sxs-lookup"><span data-stu-id="7e95d-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="7e95d-170">Снимите флажок "перезапустить рабочий процесс (в минутах)":</span><span class="sxs-lookup"><span data-stu-id="7e95d-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="7e95d-171">Нажмите кнопку "Применить" и "ОК", чтобы закрыть диалоговое окно свойств.</span><span class="sxs-lookup"><span data-stu-id="7e95d-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="7e95d-172">Повторите эти действия для всех доступных пулов приложений.</span><span class="sxs-lookup"><span data-stu-id="7e95d-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="7e95d-173">Предоставление доступа на запись файловой системе</span><span class="sxs-lookup"><span data-stu-id="7e95d-173">Granting write access to the file system</span></span>

<span data-ttu-id="7e95d-174">Если приложению требуется доступ на запись в файловой системе и используется NTFS, необходимо изменить список управления доступом (ACL) в папке или файле, чтобы предоставить ASP.NET доступ.</span><span class="sxs-lookup"><span data-stu-id="7e95d-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="7e95d-175">Например, чтобы предоставить ASP.NET доступ на запись к папке c:\inetpub\wwwroot, которая находится в первом открытом обозревателе, и перейдите в каталог:</span><span class="sxs-lookup"><span data-stu-id="7e95d-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="7e95d-176">Затем щелкните правой кнопкой мыши каталог, например wwwroot, и выберите пункт Свойства.</span><span class="sxs-lookup"><span data-stu-id="7e95d-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="7e95d-177">После открытия диалогового окна свойств перейдите на вкладку "безопасность":</span><span class="sxs-lookup"><span data-stu-id="7e95d-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="7e95d-178">Каталог к:\инетпуб\ввврут\ является особым каталогом, в котором для специальной группы IIS 6,0 WPG "\_IIS &amp; Execute" уже предоставлен доступ на чтение, просмотр содержимого папки и разрешение на чтение.</span><span class="sxs-lookup"><span data-stu-id="7e95d-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="7e95d-179">Однако для предоставления разрешения на запись необходимо установить флажок Разрешить для записи:</span><span class="sxs-lookup"><span data-stu-id="7e95d-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="7e95d-180">IIS 6,0 теперь имеет разрешение на запись в эту папку.</span><span class="sxs-lookup"><span data-stu-id="7e95d-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="7e95d-181">Чтобы предоставить разрешения на запись для других папок, выполните следующие действия. Обратите внимание, что может потребоваться добавить группу IIS\_WPG, если она еще не создана.</span><span class="sxs-lookup"><span data-stu-id="7e95d-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="7e95d-182">Предоставление разрешения на запись в IIS\_WPG позволит любому приложению ASP.NET записывать в этот каталог.</span><span class="sxs-lookup"><span data-stu-id="7e95d-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="7e95d-183">Поддержка встроенной проверки подлинности с помощью SQL Server</span><span class="sxs-lookup"><span data-stu-id="7e95d-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="7e95d-184">Встроенная проверка подлинности позволяет SQL Server использовать проверку подлинности Windows NT для проверки SQL Server учетных записей входа.</span><span class="sxs-lookup"><span data-stu-id="7e95d-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="7e95d-185">Это позволяет пользователю обходить стандартный процесс входа SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e95d-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="7e95d-186">При таком подходе сетевой пользователь может получить доступ к SQL Server базе данных без указания отдельной идентификации или пароля, поскольку SQL Server получает сведения о пользователях и паролях из процесса сетевой безопасности Windows NT.</span><span class="sxs-lookup"><span data-stu-id="7e95d-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="7e95d-187">Выбор встроенной проверки подлинности для приложений ASP.NET является хорошим выбором, так как в строке подключения приложения не хранятся учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7e95d-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="7e95d-188">Строка подключения, используемая для подключения к SQL, будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7e95d-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="7e95d-189">Эта строка подключения указывает SQL Server использовать учетные данные Windows приложения, пытающегося получить доступ к SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e95d-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="7e95d-190">В случае с ASP.NET/IIS 6 это будет учетная запись в группе IIS\_WPG.</span><span class="sxs-lookup"><span data-stu-id="7e95d-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="7e95d-191">Чтобы включить встроенную проверку подлинности между SQL Server и ASP.NET, необходимо сначала убедиться, что SQL Server настроена для встроенной проверки подлинности или смешанного режима проверки подлинности. чтобы определить это, обратитесь к администратору базы данных.</span><span class="sxs-lookup"><span data-stu-id="7e95d-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="7e95d-192">Если SQL Server находится в одном из этих двух режимов, можно использовать встроенную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="7e95d-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="7e95d-193">Открыть диспетчер SQL Server Enterprise (Start | Программы | Microsoft SQL Server | Enterprise Manager), выберите соответствующий сервер и разверните папку Безопасность:</span><span class="sxs-lookup"><span data-stu-id="7e95d-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="7e95d-194">Если группа "БУИЛТИНТ\ИИС\_WPG" отсутствует в списке, щелкните имена входа правой кнопкой мыши и выберите "создать login:</span><span class="sxs-lookup"><span data-stu-id="7e95d-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="7e95d-195">В текстовом поле "имя:" введите "[имя сервера или домена] \ИИС\_WPG" или нажмите кнопку "многоточие", чтобы открыть средство выбора пользователей или групп Windows NT:</span><span class="sxs-lookup"><span data-stu-id="7e95d-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="7e95d-196">Выберите группу IIS\_WPG в текущем компьютере и нажмите кнопку "Добавить" и ОК, чтобы закрыть средство выбора.</span><span class="sxs-lookup"><span data-stu-id="7e95d-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="7e95d-197">Необходимо также задать базу данных по умолчанию и разрешения на доступ к базе данных.</span><span class="sxs-lookup"><span data-stu-id="7e95d-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="7e95d-198">Чтобы задать базу данных по умолчанию, выберите в раскрывающемся списке пункт ниже, например Northwind.</span><span class="sxs-lookup"><span data-stu-id="7e95d-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="7e95d-199">Затем перейдите на вкладку доступ к базе данных:</span><span class="sxs-lookup"><span data-stu-id="7e95d-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="7e95d-200">Установите флажок Разрешить для каждой базы данных, доступ к которой требуется разрешить.</span><span class="sxs-lookup"><span data-stu-id="7e95d-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="7e95d-201">Кроме того, необходимо выбрать роли базы данных, после чего проверка владельца\_DB обеспечит наличие у вашего имени входа всех необходимых разрешений для управления и использования выбранной базы данных.</span><span class="sxs-lookup"><span data-stu-id="7e95d-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="7e95d-202">Нажмите кнопку ОК, чтобы закрыть диалоговое окно Свойства.</span><span class="sxs-lookup"><span data-stu-id="7e95d-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="7e95d-203">Теперь приложение ASP.NET настроено для поддержки встроенной проверки подлинности SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e95d-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="7e95d-204">Не запускать ASP.NET 1,0 в собственном режиме IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="7e95d-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="7e95d-205">ASP.NET 1,0 для IIS 6,0 поддерживается только в режиме совместимости IIS 5.</span><span class="sxs-lookup"><span data-stu-id="7e95d-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="7e95d-206">Чтобы настроить ASP.NET 1,0 для работы в режиме совместимости с IIS 5,0, откройте диспетчер служб Интернета и щелкните правой кнопкой мыши веб-сайты и выберите пункт Свойства:</span><span class="sxs-lookup"><span data-stu-id="7e95d-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="7e95d-207">Перейти на вкладку "служба" и проверить? Запускать веб-службу в режиме изоляции IIS 5,0?:</span><span class="sxs-lookup"><span data-stu-id="7e95d-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
