---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'ASP.NET веб-развертывание с помощью Visual Studio: развертывание из командной строки | Документация Майкрософт'
author: tdykstra
description: В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика, Усин...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634205"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="1ef82-103">ASP.NET веб-развертывание с помощью Visual Studio: развертывание из командной строки</span><span class="sxs-lookup"><span data-stu-id="1ef82-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="1ef82-104">от [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1ef82-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="1ef82-105">Скачать начальный проект</span><span class="sxs-lookup"><span data-stu-id="1ef82-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="1ef82-106">В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика с помощью Visual Studio 2012 или Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="1ef82-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="1ef82-107">Сведения о ряде см. в [первом руководстве по ряду](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1ef82-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="1ef82-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="1ef82-108">Overview</span></span>

<span data-ttu-id="1ef82-109">В этом руководстве показано, как вызвать конвейер веб-публикации Visual Studio из командной строки.</span><span class="sxs-lookup"><span data-stu-id="1ef82-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="1ef82-110">Это полезно для сценариев, в которых необходимо [автоматизировать процесс развертывания](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) вместо ручного выполнения в Visual Studio, обычно с помощью [системы управления версиями исходного кода](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span><span class="sxs-lookup"><span data-stu-id="1ef82-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="1ef82-111">Внесение изменений в развертывание</span><span class="sxs-lookup"><span data-stu-id="1ef82-111">Make a change to deploy</span></span>

<span data-ttu-id="1ef82-112">В настоящее время на странице About отображается код шаблона.</span><span class="sxs-lookup"><span data-stu-id="1ef82-112">Currently the About page displays the template code.</span></span>

![Страница "о программе" с кодом шаблона](command-line-deployment/_static/image1.png)

<span data-ttu-id="1ef82-114">Вы замените это на код, отображающий сводку по регистрации учащихся.</span><span class="sxs-lookup"><span data-stu-id="1ef82-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="1ef82-115">Откройте страницу *About. aspx* , удалите всю разметку в элементе `MainContent` `Content` и вставьте в нее следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="1ef82-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="1ef82-116">Запустите проект и выберите страницу **About (о программе** ).</span><span class="sxs-lookup"><span data-stu-id="1ef82-116">Run the project and select the **About** page.</span></span>

![Страница About](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="1ef82-118">Развертывание для тестирования с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="1ef82-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="1ef82-119">Вы не будете развертывать еще одно изменение базы данных, поэтому отключите развертывание базы данных Дбдакфкс для базы данных ASPNET-ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="1ef82-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="1ef82-120">Откройте мастер **публикации веб-сайта** и в каждом из трех профилей публикации снимите флажок **обновить базу данных** на вкладке **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="1ef82-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="1ef82-121">На начальной странице Windows 8 выполните поиск **Командная строка разработчика для VS2012**.</span><span class="sxs-lookup"><span data-stu-id="1ef82-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="1ef82-122">Щелкните правой кнопкой мыши значок **Командная строка разработчика для VS2012** и выберите команду **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="1ef82-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="1ef82-123">В командной строке введите следующую команду, заменив путь к файлу решения на путь к файлу решения:</span><span class="sxs-lookup"><span data-stu-id="1ef82-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="1ef82-124">MSBuild создает решение и развертывает его в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1ef82-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![Данные, выводимые в командной строке](command-line-deployment/_static/image3.png)

<span data-ttu-id="1ef82-126">Откройте браузер и перейдите в `http://localhost/ContosoUniversity`, а затем щелкните страницу " **о программе** ", чтобы убедиться, что развертывание прошло успешно.</span><span class="sxs-lookup"><span data-stu-id="1ef82-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="1ef82-127">Если вы еще не создали учащихся в тесте, вы увидите пустую страницу под заголовком **Статистика текста учащегося** .</span><span class="sxs-lookup"><span data-stu-id="1ef82-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="1ef82-128">Перейдите на страницу **учащихся** , нажмите кнопку **Добавить учащийся**и добавьте учащихся, а затем вернитесь на страницу **About** , чтобы просмотреть статистику учащихся.</span><span class="sxs-lookup"><span data-stu-id="1ef82-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![Сведения о странице в тестовой среде](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="1ef82-130">Ключевые параметры командной строки</span><span class="sxs-lookup"><span data-stu-id="1ef82-130">Key command line options</span></span>

<span data-ttu-id="1ef82-131">Введенная команда передала путь к файлу решения и два свойства в MSBuild:</span><span class="sxs-lookup"><span data-stu-id="1ef82-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="1ef82-132">Развертывание решения и развертывание отдельных проектов</span><span class="sxs-lookup"><span data-stu-id="1ef82-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="1ef82-133">Указание файла решения вызывает построение всех проектов в решении.</span><span class="sxs-lookup"><span data-stu-id="1ef82-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="1ef82-134">Если в решении имеется несколько веб-проектов, применяется следующее поведение MSBuild:</span><span class="sxs-lookup"><span data-stu-id="1ef82-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="1ef82-135">Свойства, указанные в командной строке, передаются в каждый проект.</span><span class="sxs-lookup"><span data-stu-id="1ef82-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="1ef82-136">Таким образом, каждый веб-проект должен иметь профиль публикации с указанным именем.</span><span class="sxs-lookup"><span data-stu-id="1ef82-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="1ef82-137">При указании `/p:PublishProfile=Test`каждый веб-проект должен иметь профиль публикации с именем *Test*.</span><span class="sxs-lookup"><span data-stu-id="1ef82-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="1ef82-138">Вы можете успешно опубликовать один проект, если он еще не построен.</span><span class="sxs-lookup"><span data-stu-id="1ef82-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="1ef82-139">Дополнительные сведения см. в описании StackOverflow потока [MSBuild с двумя пакетами](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span><span class="sxs-lookup"><span data-stu-id="1ef82-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="1ef82-140">Если вместо решения указан отдельный проект, необходимо добавить параметр, указывающий версию Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ef82-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="1ef82-141">При использовании Visual Studio 2012 Командная строка будет выглядеть так, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1ef82-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="1ef82-142">Номер версии Visual Studio 2010 — 10,0.</span><span class="sxs-lookup"><span data-stu-id="1ef82-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="1ef82-143">Дополнительные сведения см. в разделе [Совместимость проектов Visual Studio и VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) в блоге Саид Хашими.</span><span class="sxs-lookup"><span data-stu-id="1ef82-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="1ef82-144">Указание профиля публикации</span><span class="sxs-lookup"><span data-stu-id="1ef82-144">Specifying the publish profile</span></span>

<span data-ttu-id="1ef82-145">Профиль публикации можно указать по имени или по полному пути к *pubxml* файлу, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1ef82-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="1ef82-146">Методы веб-публикации, поддерживаемые для публикации из командной строки</span><span class="sxs-lookup"><span data-stu-id="1ef82-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="1ef82-147">Для публикации из командной строки поддерживаются три метода публикации:</span><span class="sxs-lookup"><span data-stu-id="1ef82-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="1ef82-148">`MSDeploy`-Publish с помощью веб-развертывание.</span><span class="sxs-lookup"><span data-stu-id="1ef82-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="1ef82-149">`Package` опубликовать, создав пакет веб-развертывание.</span><span class="sxs-lookup"><span data-stu-id="1ef82-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="1ef82-150">Пакет необходимо установить отдельно от команды MSBuild, которая его создает.</span><span class="sxs-lookup"><span data-stu-id="1ef82-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="1ef82-151">`FileSystem` — публикация путем копирования файлов в указанную папку.</span><span class="sxs-lookup"><span data-stu-id="1ef82-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="1ef82-152">Указание конфигурации и платформы сборки</span><span class="sxs-lookup"><span data-stu-id="1ef82-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="1ef82-153">Конфигурация и платформа сборки должны быть установлены в Visual Studio или в командной строке.</span><span class="sxs-lookup"><span data-stu-id="1ef82-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="1ef82-154">Профили публикации содержат свойства с именами `LastUsedBuildConfiguration` и `LastUsedPlatform`, но эти свойства нельзя задать для определения способа построения проекта.</span><span class="sxs-lookup"><span data-stu-id="1ef82-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="1ef82-155">Дополнительные сведения см. в разделе [MSBuild: как задать свойство конфигурации](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) в блоге Саид Хашими.</span><span class="sxs-lookup"><span data-stu-id="1ef82-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="1ef82-156">Развертывание в промежуточное хранение</span><span class="sxs-lookup"><span data-stu-id="1ef82-156">Deploy to staging</span></span>

<span data-ttu-id="1ef82-157">Чтобы выполнить развертывание в Azure, необходимо добавить пароль в командную строку.</span><span class="sxs-lookup"><span data-stu-id="1ef82-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="1ef82-158">Если вы сохранили пароль в профиле публикации в Visual Studio, он хранился в зашифрованном виде в файле *. pubxml. User* .</span><span class="sxs-lookup"><span data-stu-id="1ef82-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="1ef82-159">Этот файл не доступен для MSBuild при выполнении развертывания из командной строки, поэтому необходимо передать пароль в параметре командной строки.</span><span class="sxs-lookup"><span data-stu-id="1ef82-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="1ef82-160">Скопируйте необходимый пароль из файла *. publishsettings* , скачанного ранее для промежуточного веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="1ef82-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="1ef82-161">Пароль — это значение атрибута `userPWD` для элемента веб-развертывание `publishProfile`.</span><span class="sxs-lookup"><span data-stu-id="1ef82-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![веб-развертывание пароль](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="1ef82-163">На начальной странице Windows 8 найдите **Командная строка разработчика для VS2012**и щелкните значок, чтобы открыть командную строку.</span><span class="sxs-lookup"><span data-stu-id="1ef82-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="1ef82-164">(Вам не нужно открывать его в качестве администратора в этот раз, так как вы не развертываете IIS на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="1ef82-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="1ef82-165">В командной строке введите следующую команду, заменив путь к файлу решения на путь к файлу решения и пароль с паролем:</span><span class="sxs-lookup"><span data-stu-id="1ef82-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="1ef82-166">Обратите внимание, что эта командная строка включает дополнительный параметр: `/p:AllowUntrustedCertificate=true`.</span><span class="sxs-lookup"><span data-stu-id="1ef82-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="1ef82-167">По мере написания этого руководства во время публикации в Azure из командной строки необходимо задать свойство `AllowUntrustedCertificate`.</span><span class="sxs-lookup"><span data-stu-id="1ef82-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="1ef82-168">Когда исправление для этой ошибки будет выпущено, этот параметр не потребуется.</span><span class="sxs-lookup"><span data-stu-id="1ef82-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="1ef82-169">Откройте браузер и перейдите по URL-адресу промежуточного сайта, а затем щелкните страницу **About (сведения** ), чтобы проверить успешность развертывания.</span><span class="sxs-lookup"><span data-stu-id="1ef82-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="1ef82-170">Как было показано ранее для тестовой среды, для просмотра статистики на странице **About** может потребоваться создать несколько учащихся.</span><span class="sxs-lookup"><span data-stu-id="1ef82-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="1ef82-171">Развертывание в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="1ef82-171">Deploy to production</span></span>

<span data-ttu-id="1ef82-172">Процесс развертывания в рабочей среде аналогичен процессу для промежуточного хранения.</span><span class="sxs-lookup"><span data-stu-id="1ef82-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="1ef82-173">Скопируйте необходимый пароль из файла *. publishsettings* , скачанного ранее для рабочего веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="1ef82-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="1ef82-174">Откройте **Командная строка разработчика для VS2012**.</span><span class="sxs-lookup"><span data-stu-id="1ef82-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="1ef82-175">В командной строке введите следующую команду, заменив путь к файлу решения на путь к файлу решения и пароль с паролем:</span><span class="sxs-lookup"><span data-stu-id="1ef82-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="1ef82-176">При работе с реальным рабочим сайтом, если также изменилась база данных, то, как правило, вы копируете *приложение\_автономный htm* -файл на сайт перед развертыванием и удаляете его после успешного развертывания.</span><span class="sxs-lookup"><span data-stu-id="1ef82-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="1ef82-177">Откройте браузер и перейдите по URL-адресу промежуточного сайта, а затем щелкните страницу **About (сведения** ), чтобы проверить успешность развертывания.</span><span class="sxs-lookup"><span data-stu-id="1ef82-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="1ef82-178">Сводка</span><span class="sxs-lookup"><span data-stu-id="1ef82-178">Summary</span></span>

<span data-ttu-id="1ef82-179">Теперь вы развернули обновление приложения с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="1ef82-179">You have now deployed an application update by using the command line.</span></span>

![Сведения о странице в тестовой среде](command-line-deployment/_static/image6.png)

<span data-ttu-id="1ef82-181">В следующем руководстве вы увидите пример расширения конвейера веб-публикации.</span><span class="sxs-lookup"><span data-stu-id="1ef82-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="1ef82-182">В примере показано, как развернуть файлы, которые не включены в проект.</span><span class="sxs-lookup"><span data-stu-id="1ef82-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ef82-183">[Назад](deploying-a-database-update.md)
> [Вперед](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="1ef82-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
