---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: Создание командного проекта в TFS | Документация Майкрософт
author: jrjlee
description: В этом разделе описывается создание нового командного проекта в Team Foundation Server (TFS) 2010.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519564"
---
# <a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="1e0fc-103">Создание командного проекта в Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="1e0fc-103">Creating a Team Project in TFS</span></span>

<span data-ttu-id="1e0fc-104">кто [Джейсон Иванов](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="1e0fc-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="1e0fc-105">Скачать в формате PDF</span><span class="sxs-lookup"><span data-stu-id="1e0fc-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="1e0fc-106">В этом разделе описывается создание нового командного проекта в Team Foundation Server (TFS) 2010.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>

<span data-ttu-id="1e0fc-107">Этот раздел является частью серии руководств, основанных на требованиях Enterprise к развертыванию вымышленной компании Fabrikam, Inc. В этой серии руководств используется пример решения&#x2014; [диспетчера контактов](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;для представления веб-приложения с реалистичным уровнем сложности, включая приложение ASP.NET MVC 3, службу Windows Communication Foundation (WCF) и проект базы данных.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="1e0fc-108">Обзор задач</span><span class="sxs-lookup"><span data-stu-id="1e0fc-108">Task Overview</span></span>

<span data-ttu-id="1e0fc-109">Чтобы подготавливать и использовать новый командный проект в TFS, необходимо выполнить следующие общие действия:</span><span class="sxs-lookup"><span data-stu-id="1e0fc-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="1e0fc-110">Предоставьте разрешения пользователю, который будет создавать новый командный проект.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="1e0fc-111">Создайте командный проект.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-111">Create the team project.</span></span>
- <span data-ttu-id="1e0fc-112">Предоставьте разрешения членам команды, которые будут работать над проектом.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="1e0fc-113">Верните некоторое содержимое.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-113">Check in some content.</span></span>

<span data-ttu-id="1e0fc-114">В этом разделе будет показано, как выполнять эти процедуры, а также будут определены пользователи и роли заданий, которые, скорее всего, будут отвечать за каждую процедуру.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="1e0fc-115">Имейте в виду, что в зависимости от структуры Организации каждая из этих задач может быть обязанностью другого человека.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="1e0fc-116">В задачах и пошаговых руководствах этого раздела предполагается, что вы установили и настроили TFS и создали коллекцию командных проектов в рамках процесса настройки.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="1e0fc-117">Дополнительные сведения об этих допущениях и общие сведения о сценарии см. в статье [Настройка сервера сборки TFS для веб-развертывания](configuring-a-tfs-build-server-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="1e0fc-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="1e0fc-118">Предоставление разрешений автору командного проекта</span><span class="sxs-lookup"><span data-stu-id="1e0fc-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="1e0fc-119">Чтобы создать новый командный проект, необходимы следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="1e0fc-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="1e0fc-120">Необходимо иметь разрешение **Создание новых проектов** на уровне приложений TFS.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="1e0fc-121">Обычно это разрешение предоставляется путем добавления пользователей в группу TFS **Администраторы коллекции проектов** .</span><span class="sxs-lookup"><span data-stu-id="1e0fc-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="1e0fc-122">Глобальная группа **Администраторы Team Foundation** также включает это разрешение.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="1e0fc-123">Необходимо иметь разрешение на создание новых сайтов рабочих групп в семействе веб-сайтов SharePoint, которые соответствуют коллекции командных проектов TFS.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="1e0fc-124">Обычно это разрешение предоставляется путем добавления пользователя в группу SharePoint с правами **полного** доступа в семействе веб-сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="1e0fc-125">Если вы используете SQL Server Reporting Services функции, вы должны быть членом роли **диспетчера содержимого Team Foundation** в Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="1e0fc-126">Кто выполняет эти процедуры?</span><span class="sxs-lookup"><span data-stu-id="1e0fc-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="1e0fc-127">Как правило, эти процедуры выполняет пользователь или группа, которые администрируют развертывание TFS.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="1e0fc-128">Так как это набор разрешений с высоким уровнем привилегий, новые командные проекты обычно создаются небольшими подмножествами пользователей, ответственных за администрирование развертывания TFS.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="1e0fc-129">Разработчикам, как правило, не предоставляются разрешения, необходимые для создания новых командных проектов.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="1e0fc-130">Предоставление разрешений в TFS</span><span class="sxs-lookup"><span data-stu-id="1e0fc-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="1e0fc-131">Если вы хотите разрешить пользователю создавать новые командные проекты, первая задача высокого уровня заключается в добавлении пользователя в группу **администраторов коллекции проектов** для коллекции командных проектов.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="1e0fc-132">**Добавление пользователя в группу «Администраторы коллекции проектов»**</span><span class="sxs-lookup"><span data-stu-id="1e0fc-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="1e0fc-133">На сервере TFS в меню **Пуск** наведите указатель на пункт **все программы**, выберите **Microsoft Team Foundation Server 2010**и щелкните **консоль администрирования Team Foundation**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="1e0fc-134">В представлении дерева навигации разверните узел **уровень приложения**и выберите пункт **коллекции командных проектов**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="1e0fc-135">На панели **коллекции командных проектов** выберите коллекцию командных проектов, которой требуется управлять.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="1e0fc-136">На вкладке **Общие** щелкните членство в **группе**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="1e0fc-137">В диалоговом окне **глобальные группы** выберите группу **Администраторы коллекции проектов** , а затем щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="1e0fc-138">В диалоговом окне **Свойства группы Team Foundation Server** выберите пункт **пользователь или группа Windows**, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="1e0fc-139">В диалоговом окне **Выбор пользователей, компьютеров или групп** введите имя пользователя, который будет иметь возможность создавать новые командные проекты, нажмите кнопку **Проверить имена**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="1e0fc-140">В диалоговом окне **Свойства группы Team Foundation Server** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="1e0fc-141">В диалоговом окне **глобальные группы** нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="1e0fc-142">Предоставление разрешений в службах SharePoint Services</span><span class="sxs-lookup"><span data-stu-id="1e0fc-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="1e0fc-143">Далее необходимо предоставить пользователю разрешение на создание новых сайтов команд в семействе веб-сайтов SharePoint, которые соответствуют коллекции командных проектов TFS.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="1e0fc-144">**Предоставление разрешений полного доступа к семейству веб-сайтов SharePoint**</span><span class="sxs-lookup"><span data-stu-id="1e0fc-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="1e0fc-145">В Консоль администрирования Team Foundation Server на странице **коллекции командных проектов** выберите коллекцию командных проектов, которой требуется управлять.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="1e0fc-146">На вкладке **сайт SharePoint** запишите значение текущего URL-адреса **расположения сайта по умолчанию** .</span><span class="sxs-lookup"><span data-stu-id="1e0fc-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="1e0fc-147">Откройте Internet Explorer и перейдите по URL-адресу, записанному на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e0fc-148">Если вы не вошли в Windows как пользователь, создавший коллекцию командных проектов, необходимо войти в SharePoint от имени этого пользователя, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="1e0fc-149">В меню **Действия сайта** выберите пункт **Настройки веб-сайта**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="1e0fc-150">На странице **Параметры сайта** в разделе **Пользователи и разрешения**щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="1e0fc-151">На панели навигации слева щелкните **группы**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="1e0fc-152">На странице **Пользователи и группы: все группы** щелкните **настроить группы для этого сайта**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > <span data-ttu-id="1e0fc-153">Сообщение об ошибке <strong>http 404 не найдено</strong> из-за ошибки с удвоенной кодировкой HTTP.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-153">You may receive an <strong>HTTP 404 Not Found</strong> error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="1e0fc-154">Если это происходит, замените URL-адрес следующим:</span><span class="sxs-lookup"><span data-stu-id="1e0fc-154">If this occurs, replace the URL with this:</span></span>   
   > <span data-ttu-id="1e0fc-155">`[site_collection_URL]/_layouts/permsetup.aspx`. Например:</span><span class="sxs-lookup"><span data-stu-id="1e0fc-155">`[site_collection_URL]/_layouts/permsetup.aspx` For example:</span></span>  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. <span data-ttu-id="1e0fc-156">На странице **Настройка групп для этого сайта** добавьте пользователя, который будет создавать командные проекты, в группу **владельцы** , а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-156">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="1e0fc-157">Дополнительные сведения о том, как разрешить пользователям создавать новые командные проекты в коллекции командных проектов, см. в разделе [Установка разрешений администратора для коллекций командных проектов](https://msdn.microsoft.com/library/dd547204.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e0fc-157">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="1e0fc-158">Создание нового командного проекта и Добавление пользователей</span><span class="sxs-lookup"><span data-stu-id="1e0fc-158">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="1e0fc-159">После получения необходимых разрешений можно использовать окно **Team Explorer** в Visual Studio 2010 для создания нового командного проекта.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-159">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="1e0fc-160">Этот подход предоставляет мастер, собирающий все необходимые сведения и выполняющий необходимые задачи в TFS, SharePoint и SQL Server Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-160">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="1e0fc-161">Кроме того, необходимо предоставить разрешения на новый командный проект членам группы разработчиков, чтобы они добавили и изменяют содержимое.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-161">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="1e0fc-162">Кто выполняет эти процедуры?</span><span class="sxs-lookup"><span data-stu-id="1e0fc-162">Who Performs These Procedures?</span></span>

<span data-ttu-id="1e0fc-163">Обычно эти процедуры выполняются администратором TFS или руководителем группы разработчиков.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-163">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="1e0fc-164">Создание нового командного проекта</span><span class="sxs-lookup"><span data-stu-id="1e0fc-164">Create a New Team Project</span></span>

<span data-ttu-id="1e0fc-165">В следующей процедуре описывается создание нового командного проекта в TFS 2010.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-165">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="1e0fc-166">**Создание нового командного проекта**</span><span class="sxs-lookup"><span data-stu-id="1e0fc-166">**To create a new team project**</span></span>

1. <span data-ttu-id="1e0fc-167">В меню **Пуск** последовательно выберите пункты **все программы**, **Microsoft Visual Studio 2010**, щелкните правой кнопкой мыши **Microsoft Visual Studio 2010**и выберите команду **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-167">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e0fc-168">Если вы не запускаете Visual Studio 2010 в качестве администратора, на последнем шаге мастер создания командного проекта завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-168">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="1e0fc-169">В диалоговом окне **Контроль учетных записей** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-169">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="1e0fc-170">В Visual Studio в меню **команда** выберите пункт **подключиться к Team Foundation Server**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-170">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e0fc-171">Если подключение к серверу TFS уже настроено, можно опустить шаги 4-7.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-171">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="1e0fc-172">В диалоговом окне **Подключение к командному проекту** щелкните **серверы**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-172">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="1e0fc-173">В диалоговом окне **Добавление или удаление Team Foundation Server** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-173">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="1e0fc-174">В диалоговом окне **добавление Team Foundation Server** укажите сведения об экземпляре TFS и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-174">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="1e0fc-175">В диалоговом окне " **Добавление или удаление Team Foundation Server** " нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-175">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="1e0fc-176">В диалоговом окне **Подключение к командному проекту** выберите экземпляр TFS, к которому необходимо подключиться, выберите коллекцию командных проектов, в которую необходимо добавить, и нажмите кнопку **подключить**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-176">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="1e0fc-177">В окне **Team Explorer** щелкните правой кнопкой мыши коллекцию командных проектов и выберите команду **создать командный проект**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-177">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="1e0fc-178">В диалоговом окне **новый командный проект** укажите имя и описание командного проекта, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-178">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e0fc-179">Если командный проект содержит пробелы, вы можете столкнуться с некоторыми проблемами при использовании средства веб-развертывания службы IIS (IIS) (веб-развертывание) для развертывания пакетов из выходного пути.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-179">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="1e0fc-180">Пробелы в пути могут значительно усложнить выполнение веб-развертывание команд.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-180">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="1e0fc-181">На странице **Выбор шаблона процесса** выберите шаблон процесса, который требуется использовать для управления процессом разработки, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-181">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e0fc-182">Дополнительные сведения о шаблонах процессов для TFS см. в разделе [шаблоны процессов и средства](https://msdn.microsoft.com/vstudio/aa718795).</span><span class="sxs-lookup"><span data-stu-id="1e0fc-182">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span></span>
12. <span data-ttu-id="1e0fc-183">На странице **Параметры сайта группы** оставьте параметры по умолчанию без изменений, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-183">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="1e0fc-184">Этот параметр создает или определяет сайт группы SharePoint, связанный с командным проектом TFS.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-184">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="1e0fc-185">Группа разработчиков может использовать этот сайт для управления документацией, участия в обсуждениях, создания вики-страниц и выполнения других задач, не связанных с кодом.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-185">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="1e0fc-186">Дополнительные сведения см. в разделе [взаимодействие между продуктами SharePoint и Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e0fc-186">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="1e0fc-187">На странице **Указание параметров системы управления версиями** оставьте параметры по умолчанию без изменений, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-187">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="1e0fc-188">Этот параметр определяет или создает расположение в иерархии папок TFS, которое будет использоваться в качестве корневой папки для содержимого.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-188">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="1e0fc-189">На странице **Подтверждение параметров командного проекта** нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-189">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="1e0fc-190">После успешного создания нового командного проекта на странице **командный проект создан** нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-190">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="1e0fc-191">Добавление пользователей в командный проект</span><span class="sxs-lookup"><span data-stu-id="1e0fc-191">Add Users to a Team Project</span></span>

<span data-ttu-id="1e0fc-192">Теперь, когда вы создали новый командный проект, вы можете предоставить пользователям разрешения, чтобы они могли начать добавление и совместную работу над содержимым.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-192">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="1e0fc-193">**Добавление пользователей в командный проект**</span><span class="sxs-lookup"><span data-stu-id="1e0fc-193">**To add users to a team project**</span></span>

1. <span data-ttu-id="1e0fc-194">В Visual Studio 2010 в окне **Team Explorer** щелкните правой кнопкой мыши командный проект, укажите пункт **Параметры командного проекта**и выберите пункт членство в **группе**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-194">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="1e0fc-195">Чтобы разрешить пользователю добавлять, изменять и удалять код в системе управления версиями, необходимо добавить его в группу " **Участники** ".</span><span class="sxs-lookup"><span data-stu-id="1e0fc-195">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="1e0fc-196">В диалоговом окне **группы проектов** выберите группу **Участники** и нажмите кнопку **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-196">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="1e0fc-197">В диалоговом окне **Свойства группы Team Foundation Server** выберите пункт **пользователь или группа Windows**, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-197">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="1e0fc-198">В диалоговом окне **Выбор пользователей, компьютеров или групп** введите имя пользователя, которого нужно добавить в командный проект, нажмите кнопку **Проверить имена**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-198">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="1e0fc-199">В диалоговом окне **Свойства группы Team Foundation Server** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-199">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="1e0fc-200">В диалоговом окне **группы проектов** нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-200">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1e0fc-201">Заключение</span><span class="sxs-lookup"><span data-stu-id="1e0fc-201">Conclusion</span></span>

<span data-ttu-id="1e0fc-202">На этом этапе новый командный проект готов к использованию, и группа разработчиков может начать добавление содержимого и совместную работу над процессом разработки.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-202">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="1e0fc-203">Следующий раздел, [добавляющий содержимое в систему управления версиями](adding-content-to-source-control.md), описывает добавление содержимого в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="1e0fc-203">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="1e0fc-204">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="1e0fc-204">Further Reading</span></span>

<span data-ttu-id="1e0fc-205">Более подробные рекомендации по созданию командных проектов в TFS см. в разделе [Создание командного проекта](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="1e0fc-205">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="1e0fc-206">Дополнительные сведения о том, как разрешить пользователям создавать новые командные проекты в коллекции командных проектов, см. в разделе [Установка разрешений администратора для коллекций командных проектов](https://msdn.microsoft.com/library/dd547204.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e0fc-206">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span> <span data-ttu-id="1e0fc-207">Дополнительные сведения о добавлении пользователей в командные проекты см. в разделе [Добавление пользователей в командные проекты](https://msdn.microsoft.com/library/bb558971.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e0fc-207">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/library/bb558971.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1e0fc-208">[Назад](configuring-team-foundation-server-for-web-deployment.md)
> [Вперед](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="1e0fc-208">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
