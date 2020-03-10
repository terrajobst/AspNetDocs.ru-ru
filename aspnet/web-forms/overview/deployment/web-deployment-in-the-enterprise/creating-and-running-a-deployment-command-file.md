---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: Создание и запуск командного файла развертывания | Документация Майкрософт
author: jrjlee
description: В этом разделе описывается создание командного файла, который позволит запустить развертывание с помощью файлов проекта Microsoft Build Engine (MSBuild) в виде одного шага, Re...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514980"
---
# <a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="2da8e-103">Создание и запуск командного файла развертывания</span><span class="sxs-lookup"><span data-stu-id="2da8e-103">Creating and Running a Deployment Command File</span></span>

<span data-ttu-id="2da8e-104">кто [Джейсон Иванов](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="2da8e-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="2da8e-105">Скачать в формате PDF</span><span class="sxs-lookup"><span data-stu-id="2da8e-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="2da8e-106">В этом разделе описывается создание командного файла, который позволяет запускать развертывание с помощью файлов проекта Microsoft Build Engine (MSBuild) в качестве одношагового, повторяемого процесса.</span><span class="sxs-lookup"><span data-stu-id="2da8e-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>

<span data-ttu-id="2da8e-107">Этот раздел является частью серии руководств, основанных на требованиях Enterprise к развертыванию вымышленной компании Fabrikam, Inc. В этой серии руководств используется пример решения&#x2014; [диспетчера контактов](the-contact-manager-solution.md) &#x2014;для представления веб-приложения с реалистичным уровнем сложности, включая приложение ASP.NET MVC 3, службу Windows Communication Foundation (WCF) и проект базы данных.</span><span class="sxs-lookup"><span data-stu-id="2da8e-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="2da8e-108">Метод развертывания в сердце этих учебников основан на подходе к файлам проекта Split, описанному в разделе [понимание процесса сборки](understanding-the-build-process.md), в котором процесс сборки управляется двумя файлами&#x2014;проекта, содержащими инструкции по сборке, которые применяются к каждой целевой среде, и одна содержит параметры сборки и развертывания, относящиеся к конкретной среде.</span><span class="sxs-lookup"><span data-stu-id="2da8e-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="2da8e-109">Во время сборки файл проекта, зависящий от среды, объединяется в файл проекта независимо от среды, чтобы сформировать полный набор инструкций по сборке.</span><span class="sxs-lookup"><span data-stu-id="2da8e-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="2da8e-110">Обзор процесса</span><span class="sxs-lookup"><span data-stu-id="2da8e-110">Process Overview</span></span>

<span data-ttu-id="2da8e-111">В этом разделе вы узнаете, как создать и запустить командный файл, использующий эти файлы проекта для выполнения повторяемого развертывания в целевой среде.</span><span class="sxs-lookup"><span data-stu-id="2da8e-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="2da8e-112">По сути, командный файл просто должен содержать команду MSBuild, которая:</span><span class="sxs-lookup"><span data-stu-id="2da8e-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="2da8e-113">Указывает MSBuild на выполнение файла *Publish. proj* , независимого от среды.</span><span class="sxs-lookup"><span data-stu-id="2da8e-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="2da8e-114">Сообщает файлу *Publish. proj* , какой файл содержит параметры проекта для конкретной среды и где его найти.</span><span class="sxs-lookup"><span data-stu-id="2da8e-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="2da8e-115">Создание команды MSBuild</span><span class="sxs-lookup"><span data-stu-id="2da8e-115">Create an MSBuild Command</span></span>

<span data-ttu-id="2da8e-116">Как описано в [статье Общие сведения о процессе сборки](understanding-the-build-process.md),&#x2014;файл проекта конкретной среды, например, *env-dev. proj*&#x2014;, предназначен для импорта в независимый от среды файл *Publish. proj* во время сборки.</span><span class="sxs-lookup"><span data-stu-id="2da8e-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="2da8e-117">Вместе эти два файла содержат полный набор инструкций, которые указывают MSBuild, как создать и развернуть решение.</span><span class="sxs-lookup"><span data-stu-id="2da8e-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="2da8e-118">Файл *Publish. proj* использует элемент **Import** для импорта файла проекта, относящегося к конкретной среде.</span><span class="sxs-lookup"><span data-stu-id="2da8e-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

<span data-ttu-id="2da8e-119">Таким образом, при использовании MSBuild. exe для создания и развертывания решения диспетчера контактов необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2da8e-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="2da8e-120">Запустите файл MSBuild. exe в файле *Publish. proj* .</span><span class="sxs-lookup"><span data-stu-id="2da8e-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="2da8e-121">Укажите расположение файла проекта для конкретной среды, указав параметр командной строки с именем **таржетенвпропсфиле**.</span><span class="sxs-lookup"><span data-stu-id="2da8e-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="2da8e-122">Для этого команда MSBuild должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2da8e-122">To do this, your MSBuild command should resemble this:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

<span data-ttu-id="2da8e-123">Отсюда это простой шаг перехода к одношаговому развертыванию с повторяемым шагом.</span><span class="sxs-lookup"><span data-stu-id="2da8e-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="2da8e-124">Все, что нужно сделать, — это добавить команду MSBuild в CMD-файл.</span><span class="sxs-lookup"><span data-stu-id="2da8e-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="2da8e-125">В решении диспетчера контактов папка публикации включает файл с именем *публиш-дев. cmd* , который делает именно это.</span><span class="sxs-lookup"><span data-stu-id="2da8e-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="2da8e-126">Параметр **/ФЛ** указывает MSBuild создать файл журнала с именем *MSBuild. log* в рабочем каталоге, в котором был вызван MSBuild. exe.</span><span class="sxs-lookup"><span data-stu-id="2da8e-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>

<span data-ttu-id="2da8e-127">Чтобы развернуть или повторно развернуть решение диспетчера контактов, достаточно запустить файл *публиш-дев. cmd* .</span><span class="sxs-lookup"><span data-stu-id="2da8e-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="2da8e-128">При запуске файла MSBuild выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2da8e-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="2da8e-129">Создание всех проектов в решении.</span><span class="sxs-lookup"><span data-stu-id="2da8e-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="2da8e-130">Создание развертываемых веб-пакетов для проектов веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="2da8e-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="2da8e-131">Создание DBSCHEMA и деплойманифест файлов для проектов баз данных.</span><span class="sxs-lookup"><span data-stu-id="2da8e-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="2da8e-132">Разверните веб-пакеты на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="2da8e-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="2da8e-133">Разверните базу данных на сервере базы данных.</span><span class="sxs-lookup"><span data-stu-id="2da8e-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="2da8e-134">Запуск развертывания</span><span class="sxs-lookup"><span data-stu-id="2da8e-134">Run the Deployment</span></span>

<span data-ttu-id="2da8e-135">Создав командный файл для целевой среды, вы сможете выполнить полное развертывание, просто запустив файл.</span><span class="sxs-lookup"><span data-stu-id="2da8e-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="2da8e-136">**Развертывание решения диспетчера контактов в тестовой среде**</span><span class="sxs-lookup"><span data-stu-id="2da8e-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="2da8e-137">На рабочей станции разработчика откройте проводник Windows и перейдите к расположению файла *публиш-дев. cmd* .</span><span class="sxs-lookup"><span data-stu-id="2da8e-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="2da8e-138">Дважды щелкните файл, чтобы выполнить его.</span><span class="sxs-lookup"><span data-stu-id="2da8e-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="2da8e-139">Если откроется диалоговое окно **Открытие файла — предупреждение безопасности** , нажмите кнопку **выполнить**.</span><span class="sxs-lookup"><span data-stu-id="2da8e-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="2da8e-140">Если параметры конфигурации и тестовые серверы настроены правильно, в окне командной строки отобразится сообщение **Сборка успешно выполнена** , когда MSBuild завершит обработку файлов проекта.</span><span class="sxs-lookup"><span data-stu-id="2da8e-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="2da8e-141">Если вы развернули решение в этой среде впервые, вам потребуется добавить учетную запись тестового компьютера веб-сервера в базу данных\_объект **записи** **данных,** а также в роли **DB\_Database DataReader** .</span><span class="sxs-lookup"><span data-stu-id="2da8e-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="2da8e-142">Эта процедура описана в разделе [Настройка сервера базы данных для веб-развертывание публикации](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2da8e-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="2da8e-143">Эти разрешения необходимо назначить только при создании базы данных.</span><span class="sxs-lookup"><span data-stu-id="2da8e-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="2da8e-144">По умолчанию процесс сборки не будет воссоздавать базу данных при каждом развертывании&#x2014;, а будет сравнивать существующую базу данных с последней схемой и внести только необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="2da8e-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="2da8e-145">В результате вам нужно только сопоставлять эти роли базы данных при первом развертывании решения.</span><span class="sxs-lookup"><span data-stu-id="2da8e-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="2da8e-146">Откройте Internet Explorer и перейдите по URL-адресу приложения диспетчера контактов (например, `http://testweb1:85/ContactManager/`).</span><span class="sxs-lookup"><span data-stu-id="2da8e-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="2da8e-147">Убедитесь, что приложение работает правильно и вы можете добавить контакты.</span><span class="sxs-lookup"><span data-stu-id="2da8e-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="2da8e-148">Заключение</span><span class="sxs-lookup"><span data-stu-id="2da8e-148">Conclusion</span></span>

<span data-ttu-id="2da8e-149">Создание командного файла, содержащего инструкции MSBuild, обеспечивает быстрый и простой способ создания и развертывания решения с несколькими проектами в определенной целевой среде.</span><span class="sxs-lookup"><span data-stu-id="2da8e-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="2da8e-150">Если требуется многократное развертывание решения в нескольких конечных средах, можно создать несколько командных файлов.</span><span class="sxs-lookup"><span data-stu-id="2da8e-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="2da8e-151">В каждом командном файле команда MSBuild создаст тот же универсальный файл проекта, но будет указывать другой файл проекта для конкретной среды.</span><span class="sxs-lookup"><span data-stu-id="2da8e-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="2da8e-152">Например, командный файл для публикации в среде разработчика или тестирования может содержать следующую команду MSBuild:</span><span class="sxs-lookup"><span data-stu-id="2da8e-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

<span data-ttu-id="2da8e-153">Командный файл для публикации в промежуточной среде может содержать следующую команду MSBuild:</span><span class="sxs-lookup"><span data-stu-id="2da8e-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> <span data-ttu-id="2da8e-154">Рекомендации по настройке файлов проекта для конкретной среды сервера см. в разделе [Настройка свойств развертывания для целевой среды](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span><span class="sxs-lookup"><span data-stu-id="2da8e-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>

<span data-ttu-id="2da8e-155">Можно также настроить процесс сборки для каждой среды, переопределив свойства или задав различные другие параметры в команде MSBuild.</span><span class="sxs-lookup"><span data-stu-id="2da8e-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="2da8e-156">Дополнительные сведения см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).</span><span class="sxs-lookup"><span data-stu-id="2da8e-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2da8e-157">[Назад](deploying-database-projects.md)
> [Вперед](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="2da8e-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
