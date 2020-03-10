---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Настройка решения диспетчера контактов | Документация Майкрософт
author: jrjlee
description: В этом разделе описывается загрузка и настройка решения диспетчера контактов для локального запуска на рабочей станции разработчика.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511164"
---
# <a name="setting-up-the-contact-manager-solution"></a><span data-ttu-id="849ad-103">Настройка решения диспетчера контактов</span><span class="sxs-lookup"><span data-stu-id="849ad-103">Setting Up the Contact Manager Solution</span></span>

<span data-ttu-id="849ad-104">кто [Джейсон Иванов](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="849ad-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="849ad-105">Скачать в формате PDF</span><span class="sxs-lookup"><span data-stu-id="849ad-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="849ad-106">В этом разделе описывается загрузка и настройка решения диспетчера контактов для локального запуска на рабочей станции разработчика.</span><span class="sxs-lookup"><span data-stu-id="849ad-106">This topic describes how to download and configure the Contact Manager solution to run locally on a developer workstation.</span></span>

## <a name="system-requirements"></a><span data-ttu-id="849ad-107">Требования к системе</span><span class="sxs-lookup"><span data-stu-id="849ad-107">System Requirements</span></span>

<span data-ttu-id="849ad-108">Для локального запуска решения диспетчера контактов и выполнения других задач, описанных в этом руководстве, необходимо установить это программное обеспечение на рабочую станцию разработчика:</span><span class="sxs-lookup"><span data-stu-id="849ad-108">To run the Contact Manager solution locally and to perform the other tasks described in this tutorial, you'll need to install this software on your developer workstation:</span></span>

- <span data-ttu-id="849ad-109">Visual Studio 2010 с пакетом обновления 1 (SP1), Premium или Ultimate Edition</span><span class="sxs-lookup"><span data-stu-id="849ad-109">Visual Studio 2010 Service Pack 1, Premium or Ultimate Edition</span></span>
- <span data-ttu-id="849ad-110">Internet Information Services (IIS) 7.5 Express</span><span class="sxs-lookup"><span data-stu-id="849ad-110">Internet Information Services (IIS) 7.5 Express</span></span>
- <span data-ttu-id="849ad-111">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="849ad-111">SQL Server Express 2008 R2</span></span>
- <span data-ttu-id="849ad-112">Средство веб-развертывания IIS (веб-развертывание) 2,1 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="849ad-112">IIS Web Deployment Tool (Web Deploy) 2.1 or later</span></span>
- <span data-ttu-id="849ad-113">ASP.NET 4,0</span><span class="sxs-lookup"><span data-stu-id="849ad-113">ASP.NET 4.0</span></span>
- <span data-ttu-id="849ad-114">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="849ad-114">ASP.NET MVC 3</span></span>
- <span data-ttu-id="849ad-115">.NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="849ad-115">.NET Framework 4</span></span>
- <span data-ttu-id="849ad-116">.NET Framework 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="849ad-116">.NET Framework 3.5 SP1</span></span>

<span data-ttu-id="849ad-117">За исключением Visual Studio 2010, вы можете скачать и установить последние версии всех этих продуктов и компонентов с помощью [установщика веб-платформы](https://go.microsoft.com/?linkid=9805118).</span><span class="sxs-lookup"><span data-stu-id="849ad-117">With the exception of Visual Studio 2010, you can download and install the latest versions of all of these products and components through the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

## <a name="download-and-extract-the-solution"></a><span data-ttu-id="849ad-118">Скачивание и извлечение решения</span><span class="sxs-lookup"><span data-stu-id="849ad-118">Download and Extract the Solution</span></span>

<span data-ttu-id="849ad-119">Вы можете скачать пример приложения диспетчера контактов из коллекции кода MSDN [здесь](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span><span class="sxs-lookup"><span data-stu-id="849ad-119">You can download the Contact Manager sample application from the MSDN Code Gallery [here](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span></span>

## <a name="configure-and-run-the-solution"></a><span data-ttu-id="849ad-120">Настройка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="849ad-120">Configure and Run the Solution</span></span>

<span data-ttu-id="849ad-121">Чтобы настроить и запустить решение диспетчера контактов на локальном компьютере, необходимо выполнить следующие общие действия:</span><span class="sxs-lookup"><span data-stu-id="849ad-121">To configure and run the Contact Manager solution on your local machine, you'll need to perform these high-level steps:</span></span>

1. <span data-ttu-id="849ad-122">Если вы еще не сделали этого, создайте локальную базу данных служб приложений ASP.NET с включенными функциями управления членством и ролями.</span><span class="sxs-lookup"><span data-stu-id="849ad-122">If you don't have one already, create a local ASP.NET application services database with the membership and role management features enabled.</span></span>
2. <span data-ttu-id="849ad-123">Измените строки подключения в файлах *Web. config* , чтобы они указывали на локальный экземпляр SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="849ad-123">Edit connection strings in the *web.config* files to point to your local SQL Server Express instance.</span></span>
3. <span data-ttu-id="849ad-124">Запустите решение из Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="849ad-124">Run the solution from Visual Studio 2010.</span></span>

<span data-ttu-id="849ad-125">Оставшаяся часть этого раздела содержит дополнительные рекомендации по выполнению каждой из этих задач.</span><span class="sxs-lookup"><span data-stu-id="849ad-125">The remainder of this section provides more guidance on how to complete each of these tasks.</span></span>

<span data-ttu-id="849ad-126">**Создание базы данных служб приложений**</span><span class="sxs-lookup"><span data-stu-id="849ad-126">**To create the application services database**</span></span>

1. <span data-ttu-id="849ad-127">Откройте командную строку Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="849ad-127">Open a Visual Studio 2010 command prompt.</span></span> <span data-ttu-id="849ad-128">Для этого в меню **Пуск** наведите указатель на пункт **все программы**, выберите **Microsoft Visual Studio 2010**, щелкните **инструменты Visual Studio**и выберите пункт **Командная строка Visual Studio (2010)** .</span><span class="sxs-lookup"><span data-stu-id="849ad-128">To do this, on the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt (2010)**.</span></span>
2. <span data-ttu-id="849ad-129">В командной строке введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="849ad-129">At the command prompt, type this command, and then press Enter:</span></span>

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. <span data-ttu-id="849ad-130">Используйте параметр **– C** , чтобы указать строку подключения для сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="849ad-130">Use the **–C** switch to specify the connection string for your database server.</span></span>
    2. <span data-ttu-id="849ad-131">Используйте параметр **– A** , чтобы указать компоненты служб приложений, которые необходимо добавить в базу данных.</span><span class="sxs-lookup"><span data-stu-id="849ad-131">Use the **–A** switch to specify the application services features you want to add to the database.</span></span> <span data-ttu-id="849ad-132">В этом случае **m** указывает, что вы хотите добавить поддержку для поставщика членства, а **r** указывает, что вы хотите добавить поддержку для диспетчера ролей.</span><span class="sxs-lookup"><span data-stu-id="849ad-132">In this case, **m** indicates that you want to add support for the membership provider and **r** indicates that you want to add support for the role manager.</span></span>
    3. <span data-ttu-id="849ad-133">Используйте параметр **– d** , чтобы указать имя для базы данных служб приложений.</span><span class="sxs-lookup"><span data-stu-id="849ad-133">Use the **–d** switch to specify a name for your application services database.</span></span> <span data-ttu-id="849ad-134">Если этот параметр не задан, программа создаст базу данных с именем по умолчанию **aspnetdb**.</span><span class="sxs-lookup"><span data-stu-id="849ad-134">If you omit this switch, the utility will create a database with the default name of **aspnetdb**.</span></span>
3. <span data-ttu-id="849ad-135">После успешного создания базы данных в командной строке отобразится подтверждение.</span><span class="sxs-lookup"><span data-stu-id="849ad-135">When the database has been created successfully, the command prompt will show a confirmation.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="849ad-136">Дополнительные сведения о служебной программе ASPNET\_регскл см. в статье [ASP.NET SQL Server Registration Tool (aspnet\_регскл. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="849ad-136">For more information on the aspnet\_regsql utility, see [ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span></span>

<span data-ttu-id="849ad-137">Следующий шаг — убедиться, что строки подключения в точке решения диспетчера контактов указывают на локальный экземпляр SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="849ad-137">The next step is to make sure that the connection strings in the Contact Manager solution point to your local instance of SQL Server Express.</span></span>

<span data-ttu-id="849ad-138">**Обновление строк подключения**</span><span class="sxs-lookup"><span data-stu-id="849ad-138">**To update the connection strings**</span></span>

1. <span data-ttu-id="849ad-139">Откройте решение диспетчера контактов в Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="849ad-139">Open the Contact Manager solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="849ad-140">В окне **Обозреватель решений** разверните проект **ContactManager. MVC** , а затем дважды щелкните узел **Web. config** .</span><span class="sxs-lookup"><span data-stu-id="849ad-140">In the **Solution Explorer** window, expand the **ContactManager.Mvc** project, and then double-click the **Web.config** node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="849ad-141">Проект ContactManager. MVC содержит два файла *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="849ad-141">The ContactManager.Mvc project includes two *web.config* files.</span></span> <span data-ttu-id="849ad-142">Необходимо изменить файл уровня проекта.</span><span class="sxs-lookup"><span data-stu-id="849ad-142">You need to edit the project-level file.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. <span data-ttu-id="849ad-143">Убедитесь, что в элементе **connectionStrings** строка подключения с именем **ApplicationServices** указывает на локальную базу данных служб приложений ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="849ad-143">In the **connectionStrings** element, verify that the connection string named **ApplicationServices** points to your local ASP.NET application services database.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. <span data-ttu-id="849ad-144">В окне **Обозреватель решений** разверните проект **ContactManager. Service** , а затем дважды щелкните узел **Web. config** .</span><span class="sxs-lookup"><span data-stu-id="849ad-144">In the **Solution Explorer** window, expand the **ContactManager.Service** project, and then double-click the **Web.config** node.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. <span data-ttu-id="849ad-145">В элементе **connectionStrings** в строке подключения с именем **ContactManagerContext**убедитесь, что для свойства **источник данных** задан локальный экземпляр SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="849ad-145">In the **connectionStrings** element, in the connection string named **ContactManagerContext**, verify that the **Data Source** property is set to your local instance of SQL Server Express.</span></span> <span data-ttu-id="849ad-146">В строке подключения никаких других изменений не требуется.</span><span class="sxs-lookup"><span data-stu-id="849ad-146">You don't need to change anything else in the connection string.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. <span data-ttu-id="849ad-147">Сохраните все открытые файлы.</span><span class="sxs-lookup"><span data-stu-id="849ad-147">Save all open files.</span></span>

<span data-ttu-id="849ad-148">Теперь вы можете запустить решение диспетчера контактов на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="849ad-148">You should now be ready to run the Contact Manager solution on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="849ad-149">Если выполнить эти действия без предварительного создания базы данных служб приложений, ASP.NET создаст базу данных при первой попытке создать пользователя.</span><span class="sxs-lookup"><span data-stu-id="849ad-149">If you follow these steps without first creating an application services database, ASP.NET will create the database the first time you attempt to create a user.</span></span> <span data-ttu-id="849ad-150">Однако создание базы данных вручную обеспечивает гораздо больший контроль над набором функций служб приложений, которые требуется поддерживать.</span><span class="sxs-lookup"><span data-stu-id="849ad-150">However, manually creating the database gives you a lot more control over the application services feature set you want to support.</span></span>

<span data-ttu-id="849ad-151">**Запуск решения диспетчера контактов**</span><span class="sxs-lookup"><span data-stu-id="849ad-151">**To run the Contact Manager solution**</span></span>

1. <span data-ttu-id="849ad-152">В Visual Studio 2010 нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="849ad-152">In Visual Studio 2010, press F5.</span></span>
2. <span data-ttu-id="849ad-153">Internet Explorer запустит и запросит URL-адрес приложения диспетчера контактов ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="849ad-153">Internet Explorer starts up and requests the URL of the Contact Manager ASP.NET MVC 3 application.</span></span> <span data-ttu-id="849ad-154">По умолчанию приложение отображает страницу **все контакты** .</span><span class="sxs-lookup"><span data-stu-id="849ad-154">By default, the application displays the **All Contacts** page.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. <span data-ttu-id="849ad-155">Добавьте несколько контактов, а затем убедитесь, что приложение работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="849ad-155">Add a few contacts, and then verify that the application works as expected.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. <span data-ttu-id="849ad-156">Перейдите к `http://localhost:50114/Account/Register` (измените URL-адрес, если приложение размещено на другом порте).</span><span class="sxs-lookup"><span data-stu-id="849ad-156">Browse to `http://localhost:50114/Account/Register` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="849ad-157">Добавьте имя пользователя, адрес электронной почты и пароль и убедитесь, что вы можете успешно зарегистрировать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="849ad-157">Add a user name, email address, and password, and verify that you're able to register an account successfully.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. <span data-ttu-id="849ad-158">Перейдите к `http://localhost:50114/Account/LogOn` (измените URL-адрес, если приложение размещено на другом порте).</span><span class="sxs-lookup"><span data-stu-id="849ad-158">Browse to `http://localhost:50114/Account/LogOn` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="849ad-159">Убедитесь, что вы можете войти в систему, используя только что созданную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="849ad-159">Verify that you're able to log on using the account you just created.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. <span data-ttu-id="849ad-160">Закройте Internet Explorer, чтобы завершить отладку.</span><span class="sxs-lookup"><span data-stu-id="849ad-160">Close Internet Explorer to stop debugging.</span></span>

## <a name="conclusion"></a><span data-ttu-id="849ad-161">Заключение</span><span class="sxs-lookup"><span data-stu-id="849ad-161">Conclusion</span></span>

<span data-ttu-id="849ad-162">На этом этапе решение диспетчера контактов должно быть полностью настроено для запуска на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="849ad-162">At this point, the Contact Manager solution should be fully configured to run on your local machine.</span></span> <span data-ttu-id="849ad-163">Решение можно использовать в качестве ссылки при работе с другими подразделами этого учебника.</span><span class="sxs-lookup"><span data-stu-id="849ad-163">You can use the solution as a reference when you work through the other topics in this tutorial.</span></span>

<span data-ttu-id="849ad-164">В следующем разделе, посвященном [файлу проекта](understanding-the-project-file.md), объясняется, как можно использовать пользовательские файлы проекта Microsoft Build Engine (MSBuild) в решении диспетчера контактов для управления процессом развертывания.</span><span class="sxs-lookup"><span data-stu-id="849ad-164">The next topic, [Understanding the Project File](understanding-the-project-file.md), explains how you can use the custom Microsoft Build Engine (MSBuild) project files within the Contact Manager solution to control the deployment process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="849ad-165">[Назад](the-contact-manager-solution.md)
> [Вперед](understanding-the-project-file.md)</span><span class="sxs-lookup"><span data-stu-id="849ad-165">[Previous](the-contact-manager-solution.md)
[Next](understanding-the-project-file.md)</span></span>
