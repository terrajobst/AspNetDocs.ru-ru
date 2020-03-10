---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: Добавление содержимого в систему управления версиями | Документация Майкрософт
author: jrjlee
description: В этом разделе объясняется, как добавить содержимое в систему управления версиями в Team Foundation Server (TFS) 2010. В нем описывается добавление решений и проектов в командную проекцию...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515112"
---
# <a name="adding-content-to-source-control"></a><span data-ttu-id="4dd43-104">Добавление содержимого в систему управления версиями</span><span class="sxs-lookup"><span data-stu-id="4dd43-104">Adding Content to Source Control</span></span>

<span data-ttu-id="4dd43-105">кто [Джейсон Иванов](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="4dd43-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="4dd43-106">Скачать в формате PDF</span><span class="sxs-lookup"><span data-stu-id="4dd43-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="4dd43-107">В этом разделе объясняется, как добавить содержимое в систему управления версиями в Team Foundation Server (TFS) 2010.</span><span class="sxs-lookup"><span data-stu-id="4dd43-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="4dd43-108">В нем описывается добавление решений и проектов в командный проект в TFS, а также объясняется Добавление внешних зависимостей, таких как платформы или сборки, в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>

<span data-ttu-id="4dd43-109">Этот раздел является частью серии руководств, основанных на требованиях Enterprise к развертыванию вымышленной компании Fabrikam, Inc. В этой серии руководств используется пример решения&#x2014; [диспетчера контактов](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;для представления веб-приложения с реалистичным уровнем сложности, включая приложение ASP.NET MVC 3, службу Windows Communication Foundation (WCF) и проект базы данных.</span><span class="sxs-lookup"><span data-stu-id="4dd43-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="4dd43-110">Обзор задач</span><span class="sxs-lookup"><span data-stu-id="4dd43-110">Task Overview</span></span>

<span data-ttu-id="4dd43-111">В большинстве случаев каждый член группы разработчиков должен иметь возможность добавлять содержимое в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="4dd43-112">Чтобы добавить решение в систему управления версиями в TFS, необходимо выполнить следующие общие действия:</span><span class="sxs-lookup"><span data-stu-id="4dd43-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="4dd43-113">Подключитесь к командному проекту.</span><span class="sxs-lookup"><span data-stu-id="4dd43-113">Connect to a team project.</span></span>
- <span data-ttu-id="4dd43-114">Сопоставьте структуру папок командного проекта на сервере со структурой папок на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="4dd43-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="4dd43-115">Добавьте решение и его содержимое в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="4dd43-116">Добавьте все внешние зависимости в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="4dd43-117">В этом разделе будет показано, как выполнять эти процедуры.</span><span class="sxs-lookup"><span data-stu-id="4dd43-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="4dd43-118">В задачах и пошаговых руководствах этого раздела предполагается, что вы уже создали новый командный проект Team Foundation Server для управления содержимым.</span><span class="sxs-lookup"><span data-stu-id="4dd43-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="4dd43-119">Дополнительные сведения о создании нового командного проекта см. в разделе [Создание командного проекта в TFS](creating-a-team-project-in-tfs.md).</span><span class="sxs-lookup"><span data-stu-id="4dd43-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="4dd43-120">Кто выполняет эти процедуры?</span><span class="sxs-lookup"><span data-stu-id="4dd43-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="4dd43-121">В большинстве случаев каждый член группы разработчиков должен иметь возможность добавлять и изменять содержимое в конкретных командных проектах.</span><span class="sxs-lookup"><span data-stu-id="4dd43-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="4dd43-122">Подключение к командному проекту и создание сопоставления папок</span><span class="sxs-lookup"><span data-stu-id="4dd43-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="4dd43-123">Перед добавлением содержимого в систему управления версиями необходимо подключиться к командному проекту и создать сопоставление между структурой папок на сервере и файловой системе на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="4dd43-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="4dd43-124">**Подключение к командному проекту и привязка локального пути**</span><span class="sxs-lookup"><span data-stu-id="4dd43-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="4dd43-125">На рабочей станции разработчика откройте Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="4dd43-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="4dd43-126">В Visual Studio в меню **команда** выберите пункт **подключиться к Team Foundation Server**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4dd43-127">Если подключение к серверу TFS уже настроено, можно опустить шаги 3-6.</span><span class="sxs-lookup"><span data-stu-id="4dd43-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="4dd43-128">В диалоговом окне **Подключение к командному проекту** щелкните **серверы**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="4dd43-129">В диалоговом окне **Добавление или удаление Team Foundation Server** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="4dd43-130">В диалоговом окне **добавление Team Foundation Server** укажите сведения об экземпляре TFS и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="4dd43-131">В диалоговом окне " **Добавление или удаление Team Foundation Server** " нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="4dd43-132">В диалоговом окне **Подключение к командному проекту** выберите экземпляр TFS, к которому необходимо подключиться, выберите коллекцию командных проектов, выберите командный проект, в который необходимо добавить, и нажмите кнопку **подключить**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="4dd43-133">В окне **Team Explorer** разверните свой командный проект, а затем дважды щелкните **элемент система управления версиями**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="4dd43-134">На вкладке **Обозреватель управления исходным кодом** выберите пункт **не сопоставлено**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="4dd43-135">В диалоговом окне **Map** в поле **Локальная папка** перейдите к папке (или создайте) локальную папку, которая будет использоваться в качестве корневой папки для командного проекта, и нажмите кнопку **Map**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="4dd43-136">Когда появится запрос на скачивание исходных файлов, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="4dd43-137">На этом этапе вы сопоставили серверную папку для командного проекта с локальной папкой на рабочей станции разработчика.</span><span class="sxs-lookup"><span data-stu-id="4dd43-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="4dd43-138">Вы также загрузили любое существующее содержимое из командного проекта в локальную структуру папок.</span><span class="sxs-lookup"><span data-stu-id="4dd43-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="4dd43-139">Теперь можно приступить к добавлению собственного содержимого в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="4dd43-140">Добавление проектов и решений в систему управления версиями</span><span class="sxs-lookup"><span data-stu-id="4dd43-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="4dd43-141">Чтобы добавить проекты и решения в систему управления версиями, сначала необходимо переместить их в сопоставленную папку для командного проекта на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="4dd43-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="4dd43-142">Затем можно вернуть содержимое для синхронизации дополнений с сервером.</span><span class="sxs-lookup"><span data-stu-id="4dd43-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="4dd43-143">**Добавление проектов в систему управления версиями**</span><span class="sxs-lookup"><span data-stu-id="4dd43-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="4dd43-144">На рабочей станции разработчика переместите проекты и решения в соответствующее расположение в структуре сопоставленных папок для командного проекта.</span><span class="sxs-lookup"><span data-stu-id="4dd43-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4dd43-145">Многие организации будут иметь предпочтительный подход к организации проектов и решений в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="4dd43-146">Рекомендации по структурированию папок см. в разделе [руководство. структурирование папок системы управления версиями в Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span><span class="sxs-lookup"><span data-stu-id="4dd43-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="4dd43-147">Откройте решение в Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="4dd43-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="4dd43-148">В окне **Обозреватель решений** щелкните решение правой кнопкой мыши и выберите пункт **Добавить решение в систему управления версиями**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="4dd43-149">В некоторых случаях в зависимости от того, как ваша организация любит структурировать содержимое в TFS, может потребоваться отдельно добавить проекты в систему управления версиями, чтобы обеспечить более точный контроль над способом организации исходного кода.</span><span class="sxs-lookup"><span data-stu-id="4dd43-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="4dd43-150">Убедитесь, что на вкладке **Обозреватель управления исходным кодом** отображается содержимое, добавленное в структуру папок сервера для командного проекта.</span><span class="sxs-lookup"><span data-stu-id="4dd43-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="4dd43-151">На вкладке **Обозреватель управления исходным кодом** отображается содержимое без дополнительных запросов, так как решение Добавлено в сопоставленную папку в локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="4dd43-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="4dd43-152">Если решение находилось в несопоставленном расположении, вам будет предложено указать расположение папок как в TFS, так и в локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="4dd43-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="4dd43-153">На вкладке **Обозреватель управления исходным кодом** в области **папки** щелкните правой кнопкой мыши командный проект (например, **ContactManager**) и выберите пункт **Вернуть ожидающие изменения**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="4dd43-154">В диалоговом окне **Возврат — исходные файлы** введите комментарий и нажмите кнопку **вернуть**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="4dd43-155">На этом этапе вы добавили решение в систему управления версиями в TFS.</span><span class="sxs-lookup"><span data-stu-id="4dd43-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="4dd43-156">Добавление внешних зависимостей в систему управления версиями</span><span class="sxs-lookup"><span data-stu-id="4dd43-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="4dd43-157">При добавлении проекта или решения в систему управления версиями будут также добавлены все файлы и папки в проекте или решении.</span><span class="sxs-lookup"><span data-stu-id="4dd43-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="4dd43-158">Однако в большинстве случаев проекты и решения также полагаются на внешние зависимости, например локальные сборки, для правильной работы.</span><span class="sxs-lookup"><span data-stu-id="4dd43-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="4dd43-159">Необходимо добавить все такие ресурсы в систему управления версиями, чтобы позволить Team Build и другим членам группы разработчиков успешно выполнить сборку кода.</span><span class="sxs-lookup"><span data-stu-id="4dd43-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="4dd43-160">Например, структура папок для примера решения диспетчера контактов включает папку Packages.</span><span class="sxs-lookup"><span data-stu-id="4dd43-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="4dd43-161">Он содержит сборку и различные вспомогательные ресурсы для ADO.NET Entity Framework 4,1.</span><span class="sxs-lookup"><span data-stu-id="4dd43-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="4dd43-162">Папка Packages не является частью решения диспетчера контактов, но решение не будет успешно собрано без него.</span><span class="sxs-lookup"><span data-stu-id="4dd43-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="4dd43-163">Чтобы команда Team Build выполнила сборку решения, необходимо добавить папку Packages в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="4dd43-164">Включение папки Packages является типичным, что происходит при добавлении Entity Framework или аналогичных ресурсов в решение с помощью расширения NuGet для Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="4dd43-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>

<span data-ttu-id="4dd43-165">**Добавление содержимого, не относящегося к проекту, в систему управления версиями**</span><span class="sxs-lookup"><span data-stu-id="4dd43-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="4dd43-166">Убедитесь, что добавляемые элементы (например, папка Packages) находятся в соответствующем месте в сопоставленной папке в локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="4dd43-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="4dd43-167">В Visual Studio 2010 в окне **Team Explorer** разверните свой командный проект, а затем дважды щелкните **элемент система управления версиями**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="4dd43-168">На вкладке **Обозреватель управления исходным кодом** в области **папки** выберите папку, содержащую элемент или элементы, которые требуется добавить.</span><span class="sxs-lookup"><span data-stu-id="4dd43-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="4dd43-169">Нажмите кнопку **Добавить элементы в папку** .</span><span class="sxs-lookup"><span data-stu-id="4dd43-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="4dd43-170">В диалоговом окне **Добавить в систему управления версиями** выберите папку или элементы, которые необходимо добавить, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="4dd43-171">На вкладке **Исключенные элементы** выберите все необходимые элементы, которые были автоматически исключены (например, сборки), а затем щелкните **включить элементы**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="4dd43-172">На вкладке **добавляемые элементы** убедитесь, что указаны все файлы, которые необходимо включить в список, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="4dd43-173">В окне **Обозреватель управления исходным кодом** нажмите кнопку **вернуть** .</span><span class="sxs-lookup"><span data-stu-id="4dd43-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="4dd43-174">В диалоговом окне **Возврат — исходные файлы** введите комментарий и нажмите кнопку **вернуть**.</span><span class="sxs-lookup"><span data-stu-id="4dd43-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="4dd43-175">На этом этапе вы добавили внешние зависимости для решения в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4dd43-176">Заключение</span><span class="sxs-lookup"><span data-stu-id="4dd43-176">Conclusion</span></span>

<span data-ttu-id="4dd43-177">В этом разделе описывается подключение к командному проекту, привязка структуры папок и добавление содержимого в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4dd43-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="4dd43-178">Дополнительные сведения о работе с элементами в системе управления версиями см. в разделе [использование системы управления версиями](https://msdn.microsoft.com/library/ms181368.aspx).</span><span class="sxs-lookup"><span data-stu-id="4dd43-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="4dd43-179">В следующем разделе [Настройка сервера сборки TFS для веб-развертывания](configuring-a-tfs-build-server-for-web-deployment.md)описывается подготовка сервера Team Build в TFS для создания и развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="4dd43-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="4dd43-180">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4dd43-180">Further Reading</span></span>

<span data-ttu-id="4dd43-181">Более подробные сведения о работе с системой управления версиями в TFS см. в разделе [использование системы управления версиями](https://msdn.microsoft.com/library/ms181368.aspx).</span><span class="sxs-lookup"><span data-stu-id="4dd43-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4dd43-182">[Назад](creating-a-team-project-in-tfs.md)
> [Вперед](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="4dd43-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
