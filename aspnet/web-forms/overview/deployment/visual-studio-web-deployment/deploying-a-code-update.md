---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'ASP.NET веб-развертывание с помощью Visual Studio: развертывание обновления кода | Документация Майкрософт'
author: tdykstra
description: В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика, Усин...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457644"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="40110-103">ASP.NET веб-развертывание с помощью Visual Studio: развертывание обновления кода</span><span class="sxs-lookup"><span data-stu-id="40110-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>

<span data-ttu-id="40110-104">от [Tom Dykstra)](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="40110-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="40110-105">Скачать начальный проект</span><span class="sxs-lookup"><span data-stu-id="40110-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="40110-106">В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика с помощью Visual Studio 2012 или Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="40110-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="40110-107">Сведения о ряде см. в [первом руководстве по ряду](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="40110-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="40110-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="40110-108">Overview</span></span>

<span data-ttu-id="40110-109">После первоначального развертывания работа по обслуживанию и разработке веб-узла будет продолжена, и до тех пор, когда потребуется развернуть обновление.</span><span class="sxs-lookup"><span data-stu-id="40110-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="40110-110">В этом руководстве описывается процесс развертывания обновления кода приложения.</span><span class="sxs-lookup"><span data-stu-id="40110-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="40110-111">Обновление, которое реализуется и развертывается в этом руководстве, не затрагивает изменение базы данных. в следующем руководстве вы увидите, что отличается от развертывания изменений базы данных.</span><span class="sxs-lookup"><span data-stu-id="40110-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="40110-112">Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="40110-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="40110-113">Измените код</span><span class="sxs-lookup"><span data-stu-id="40110-113">Make a code change</span></span>

<span data-ttu-id="40110-114">В качестве простого примера обновления для приложения вы добавите на страницу **инструкторов** список курсов, которые научились выбранному преподавателю.</span><span class="sxs-lookup"><span data-stu-id="40110-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="40110-115">Если вы запустили страницу **инструкторов** , то увидите, что в сетке есть ссылки **SELECT** , но они не выполняют никаких действий, чем сделать фон строки серым.</span><span class="sxs-lookup"><span data-stu-id="40110-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![Страница инструкторов с выделенным фрагментом](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="40110-117">Теперь вы добавите код, который выполняется при нажатии ссылки **SELECT** и отображает список курсов, которые научились выбранному преподавателю.</span><span class="sxs-lookup"><span data-stu-id="40110-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="40110-118">В *инструкторах. aspx*добавьте следующую разметку сразу после элемента управления `Label` **еррормессажелабел** :</span><span class="sxs-lookup"><span data-stu-id="40110-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="40110-119">Запустите страницу и выберите лектора.</span><span class="sxs-lookup"><span data-stu-id="40110-119">Run the page and select an instructor.</span></span> <span data-ttu-id="40110-120">Вы увидите список курсов, которые научились этим преподавателем.</span><span class="sxs-lookup"><span data-stu-id="40110-120">You see a list of courses taught by that instructor.</span></span>

    ![Страница инструкторов с учеными курсами](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="40110-122">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="40110-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="40110-123">Развертывание обновления кода в тестовой среде</span><span class="sxs-lookup"><span data-stu-id="40110-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="40110-124">Прежде чем можно будет использовать профили публикации для развертывания в тестовой, промежуточной и рабочей среде, необходимо изменить параметры публикации базы данных.</span><span class="sxs-lookup"><span data-stu-id="40110-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="40110-125">Вам больше не нужно запускать скрипты предоставления и развертывания данных для базы данных членства.</span><span class="sxs-lookup"><span data-stu-id="40110-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="40110-126">Откройте мастер **публикации веб-сайта** , щелкнув правой кнопкой мыши проект ContosoUniversity и выбрав **Publish (опубликовать**).</span><span class="sxs-lookup"><span data-stu-id="40110-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="40110-127">Щелкните профиль **тестирования** в раскрывающемся списке **профиль** .</span><span class="sxs-lookup"><span data-stu-id="40110-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="40110-128">Перейдите на вкладку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="40110-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="40110-129">В разделе **DefaultConnection** в разделе " **базы данных** " снимите флажок **обновить базу данных** .</span><span class="sxs-lookup"><span data-stu-id="40110-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="40110-130">Перейдите на вкладку **профиль** и выберите профиль **промежуточного хранения** в раскрывающемся списке **профиль** .</span><span class="sxs-lookup"><span data-stu-id="40110-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="40110-131">Когда появится запрос, нужно ли сохранить изменения, внесенные в профиль **тестирования** , нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="40110-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="40110-132">Внесите те же изменения в промежуточный профиль.</span><span class="sxs-lookup"><span data-stu-id="40110-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="40110-133">Повторите эту процедуру, чтобы внести те же изменения в рабочем профиле.</span><span class="sxs-lookup"><span data-stu-id="40110-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="40110-134">Закройте мастер **публикации веб-сайта** .</span><span class="sxs-lookup"><span data-stu-id="40110-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="40110-135">Развертывание в тестовой среде теперь является простым запуском публикации одним щелчком.</span><span class="sxs-lookup"><span data-stu-id="40110-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="40110-136">Чтобы ускорить этот процесс, можно использовать панель инструментов **веб-публикация одним щелчком** .</span><span class="sxs-lookup"><span data-stu-id="40110-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="40110-137">В меню **вид** выберите **панели инструментов** , а затем выберите **веб-публикация одним щелчком**.</span><span class="sxs-lookup"><span data-stu-id="40110-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="40110-139">В **Обозреватель решений**выберите проект ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="40110-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="40110-140">на панели инструментов **веб-публикация одним щелчком** выберите профиль **тестовой** публикации, а затем щелкните **Опубликовать веб-сайт** (значок со стрелками влево и вправо).</span><span class="sxs-lookup"><span data-stu-id="40110-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="40110-142">Visual Studio развертывает обновленное приложение, и браузер автоматически открывается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="40110-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="40110-143">Запустите страницу инструкторы и выберите лектора, чтобы убедиться, что обновление успешно развернуто.</span><span class="sxs-lookup"><span data-stu-id="40110-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="40110-144">Обычно вы также выполняете регрессионное тестирование (то есть протестируйте остальную часть сайта, чтобы убедиться, что новое изменение не привело к нарушению существующих функций).</span><span class="sxs-lookup"><span data-stu-id="40110-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="40110-145">Но в этом учебнике вы пропустите этот шаг и продолжите развертывание обновления в промежуточной и рабочей средах.</span><span class="sxs-lookup"><span data-stu-id="40110-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="40110-146">При повторном развертывании веб-развертывание автоматически определяет, какие файлы были изменены, и копирует только измененные файлы на сервер.</span><span class="sxs-lookup"><span data-stu-id="40110-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="40110-147">По умолчанию веб-развертывание использует даты последнего изменения для файлов, чтобы определить, какие из них изменились.</span><span class="sxs-lookup"><span data-stu-id="40110-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="40110-148">Некоторые системы управления версиями изменяют дату файла даже в том случае, если не изменить содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="40110-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="40110-149">В этом случае может потребоваться настроить веб-развертывание для использования контрольных сумм файлов, чтобы определить, какие файлы были изменены.</span><span class="sxs-lookup"><span data-stu-id="40110-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="40110-150">Дополнительные сведения см. в разделе [почему все файлы были повторно развернуты, хотя я не изменил их?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) в разделе часто задаваемых вопросов о развертывании ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="40110-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="40110-151">Перевести приложение в автономный режим во время развертывания</span><span class="sxs-lookup"><span data-stu-id="40110-151">Take the application offline during deployment</span></span>

<span data-ttu-id="40110-152">Изменение, которое вы развертываете, теперь является простым изменением одной страницы.</span><span class="sxs-lookup"><span data-stu-id="40110-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="40110-153">Но иногда вы развертываете большие изменения или развертываете код и базу данных, и сайт может работать неправильно, если пользователь запрашивает страницу до завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="40110-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="40110-154">Чтобы запретить пользователям доступ к сайту во время развертывания, можно использовать *приложение\_автономный htm* -файл.</span><span class="sxs-lookup"><span data-stu-id="40110-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="40110-155">При помещении файла с именем *app\_offline. htm* в корневую папку приложения IIS автоматически отображает этот файл вместо запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="40110-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="40110-156">Чтобы предотвратить доступ во время развертывания, вы поместили *приложение\_offline. htm* в корневую папку, запустите процесс развертывания, а затем удалите *приложение\_offline. htm* после успешного развертывания.</span><span class="sxs-lookup"><span data-stu-id="40110-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="40110-157">Можно настроить веб-развертывание для автоматического размещения на сервере приложения по умолчанию *\_автономного файла. htm* , когда он начнет развертывание и удалить его после завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="40110-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="40110-158">Чтобы сделать это, необходимо добавить следующий XML-элемент в файл профиля публикации (. pubxml):</span><span class="sxs-lookup"><span data-stu-id="40110-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="40110-159">В этом учебнике вы узнаете, как создать и использовать пользовательское *приложение\_автономном htm* -файле.</span><span class="sxs-lookup"><span data-stu-id="40110-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="40110-160">Использование *приложения\_автономно. htm* на промежуточном сайте не требуется, так как у вас нет пользователей, обращающихся к промежуточному сайту.</span><span class="sxs-lookup"><span data-stu-id="40110-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="40110-161">Но рекомендуется использовать промежуточное хранение, чтобы протестировать все, как вы планируете развертывать в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="40110-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-app_offlinehtm"></a><span data-ttu-id="40110-162">Создание\_приложений в автономном режиме. htm</span><span class="sxs-lookup"><span data-stu-id="40110-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="40110-163">В **Обозреватель решений**щелкните решение правой кнопкой мыши и выберите команду **Добавить**, а затем щелкните **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="40110-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="40110-164">Создайте **HTML-страницу** с именем *app\_offline. htm* (удалите окончательный параметр l в расширении *. HTML* , создаваемом Visual Studio по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="40110-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="40110-165">Замените разметку шаблона следующей разметкой:</span><span class="sxs-lookup"><span data-stu-id="40110-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="40110-166">Сохраните файл и закройте его.</span><span class="sxs-lookup"><span data-stu-id="40110-166">Save and close the file.</span></span>

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="40110-167">Копировать приложение\_offline. htm в корневую папку веб-сайта</span><span class="sxs-lookup"><span data-stu-id="40110-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="40110-168">Для копирования файлов на веб-сайт можно использовать любой инструмент FTP.</span><span class="sxs-lookup"><span data-stu-id="40110-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="40110-169">[FileZilla](http://filezilla-project.org/) — это популярное средство FTP, которое отображается на снимках экрана.</span><span class="sxs-lookup"><span data-stu-id="40110-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="40110-170">Для использования средства FTP требуются три вещи: URL-адрес FTP, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="40110-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="40110-171">URL-адрес отображается на странице панели мониторинга веб-сайта в портал управления Azure, а имя пользователя и пароль для FTP можно найти в файле *. publishsettings* , скачанном ранее.</span><span class="sxs-lookup"><span data-stu-id="40110-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="40110-172">Следующие шаги показывают, как получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="40110-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="40110-173">В портал управления Azure щелкните вкладку **веб-сайты** и выберите промежуточный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="40110-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="40110-174">На странице **панель мониторинга** прокрутите вниз, чтобы найти имя узла FTP в разделе **краткий обзор** .</span><span class="sxs-lookup"><span data-stu-id="40110-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![Имя узла FTP](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="40110-176">Откройте промежуточный файл *. publishsettings* в блокноте или в другом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="40110-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="40110-177">Найдите элемент `publishProfile` для профиля FTP.</span><span class="sxs-lookup"><span data-stu-id="40110-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="40110-178">Скопируйте значения `userName` и `userPWD`.</span><span class="sxs-lookup"><span data-stu-id="40110-178">Copy the `userName` and `userPWD` values.</span></span>

    ![Учетные данные FTP](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="40110-180">Откройте средство FTP и войдите по URL-адресу FTP.</span><span class="sxs-lookup"><span data-stu-id="40110-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="40110-181">Скопируйте *приложение\_offline. htm* из папки решения в папку */site/wwwroot* на промежуточном сайте.</span><span class="sxs-lookup"><span data-stu-id="40110-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![Копировать app_offline](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="40110-183">Перейдите к URL-адресу промежуточного сайта.</span><span class="sxs-lookup"><span data-stu-id="40110-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="40110-184">Вы увидите, что теперь вместо домашней страницы отображается страница *приложение\_автономно. htm.*</span><span class="sxs-lookup"><span data-stu-id="40110-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![app_offline htm в окне браузера](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="40110-186">Теперь все готово для развертывания в промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="40110-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="40110-187">Развертывание обновления кода для промежуточного хранения и рабочей среды</span><span class="sxs-lookup"><span data-stu-id="40110-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="40110-188">На панели инструментов **веб-публикация одним щелчком** выберите профиль **промежуточной** публикации и щелкните **Опубликовать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="40110-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="40110-189">Visual Studio развертывает обновленное приложение и открывает браузер на домашней странице сайта.</span><span class="sxs-lookup"><span data-stu-id="40110-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="40110-190">Откроется *приложение\_автономный htm* -файл.</span><span class="sxs-lookup"><span data-stu-id="40110-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="40110-191">Прежде чем можно будет проверить успешность развертывания, необходимо удалить *приложение\_автономный htm* -файл.</span><span class="sxs-lookup"><span data-stu-id="40110-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="40110-192">Вернитесь к своему средству FTP и удалите **приложение\_offline. htm** с промежуточного сайта.</span><span class="sxs-lookup"><span data-stu-id="40110-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="40110-193">В браузере откройте страницу инструкторы на промежуточном сайте и выберите лектора, чтобы проверить успешность развертывания обновления.</span><span class="sxs-lookup"><span data-stu-id="40110-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="40110-194">Выполните ту же процедуру для рабочей среды, что и для промежуточного хранения.</span><span class="sxs-lookup"><span data-stu-id="40110-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="40110-195">Просмотр изменений и развертывание конкретных файлов</span><span class="sxs-lookup"><span data-stu-id="40110-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="40110-196">Visual Studio 2012 также дает возможность развертывать отдельные файлы.</span><span class="sxs-lookup"><span data-stu-id="40110-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="40110-197">Для выбранного файла можно просмотреть различия между локальной версией и развернутой версией, развернуть файл в целевой среде или скопировать файл из целевой среды в локальный проект.</span><span class="sxs-lookup"><span data-stu-id="40110-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="40110-198">В этом разделе руководства вы узнаете, как использовать эти функции.</span><span class="sxs-lookup"><span data-stu-id="40110-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="40110-199">Внесение изменений в развертывание</span><span class="sxs-lookup"><span data-stu-id="40110-199">Make a change to deploy</span></span>

1. <span data-ttu-id="40110-200">Откройте *содержимое/site. CSS*и найдите блок для тега `body`.</span><span class="sxs-lookup"><span data-stu-id="40110-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="40110-201">Измените значение `background-color` с `#fff` на `darkblue`.</span><span class="sxs-lookup"><span data-stu-id="40110-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="40110-202">Просмотр изменений в окне предварительного просмотра публикации</span><span class="sxs-lookup"><span data-stu-id="40110-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="40110-203">При использовании мастера **публикации веб-сайта** для публикации проекта можно увидеть, какие изменения будут опубликованы, дважды щелкнув файл в окне **предварительного просмотра** .</span><span class="sxs-lookup"><span data-stu-id="40110-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="40110-204">Щелкните правой кнопкой мыши проект ContosoUniversity и выберите пункт **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="40110-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="40110-205">В раскрывающемся списке **профиль** выберите профиль **тестовой** публикации.</span><span class="sxs-lookup"><span data-stu-id="40110-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="40110-206">Щелкните **Предварительный просмотр**, а затем — **начать предварительный просмотр**.</span><span class="sxs-lookup"><span data-stu-id="40110-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="40110-207">В области **просмотра** дважды щелкните **site. CSS**.</span><span class="sxs-lookup"><span data-stu-id="40110-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![Дважды щелкните site. CSS](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="40110-209">В диалоговом окне **Предварительный просмотр изменений** отображается предварительный просмотр изменений, которые будут развернуты.</span><span class="sxs-lookup"><span data-stu-id="40110-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![Предварительный просмотр изменений в site. CSS](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="40110-211">Если дважды щелкнуть файл *Web. config* , в диалоговом окне **Просмотр изменений** отобразятся результаты преобразований конфигурации сборки и преобразования профиля публикации.</span><span class="sxs-lookup"><span data-stu-id="40110-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="40110-212">На этом этапе вы не выполнили никаких действий, которые приведут к изменению файла *Web. config* на сервере, поэтому вы не увидите никаких изменений.</span><span class="sxs-lookup"><span data-stu-id="40110-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="40110-213">Однако окно **Просмотр изменений** неправильно отображает два изменения.</span><span class="sxs-lookup"><span data-stu-id="40110-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="40110-214">Похоже, что будут удалены два XML-элемента.</span><span class="sxs-lookup"><span data-stu-id="40110-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="40110-215">Эти элементы добавляются процессом публикации при выборе **Code First migrations выполнить в приложении** для класса контекста Code First.</span><span class="sxs-lookup"><span data-stu-id="40110-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="40110-216">Сравнение выполняется до того, как процесс публикации добавляет эти элементы, поэтому они выглядят как удаленные, хотя они не будут удалены.</span><span class="sxs-lookup"><span data-stu-id="40110-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="40110-217">Эта ошибка будет исправлена в следующем выпуске.</span><span class="sxs-lookup"><span data-stu-id="40110-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="40110-218">Щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="40110-218">Click **Close**.</span></span>
6. <span data-ttu-id="40110-219">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="40110-219">Click **Publish**.</span></span>
7. <span data-ttu-id="40110-220">Когда браузер откроется на домашней странице тестового сайта, нажмите клавиши CTRL + F5, чтобы вызвать жесткое обновление, чтобы увидеть результат изменения CSS.</span><span class="sxs-lookup"><span data-stu-id="40110-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![Воздействие изменения CSS](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="40110-222">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="40110-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="40110-223">Публикация конкретных файлов из обозреватель решений</span><span class="sxs-lookup"><span data-stu-id="40110-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="40110-224">Предположим, вам не нравится синий фон, и вы хотите вернуться к исходному цвету.</span><span class="sxs-lookup"><span data-stu-id="40110-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="40110-225">В этом разделе вы восстановите исходные параметры, опубликовав конкретный файл непосредственно из **Обозреватель решений**.</span><span class="sxs-lookup"><span data-stu-id="40110-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="40110-226">Откройте *содержимое/site. CSS* и восстановите параметр `background-color` в значение `#fff`.</span><span class="sxs-lookup"><span data-stu-id="40110-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="40110-227">В **Обозреватель решений**щелкните правой кнопкой мыши файл *Content/site. CSS* .</span><span class="sxs-lookup"><span data-stu-id="40110-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="40110-228">В контекстном меню отображаются три варианта публикации.</span><span class="sxs-lookup"><span data-stu-id="40110-228">The context menu shows three publish options.</span></span>

    ![Параметры публикации из обозреватель решений](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="40110-230">Щелкните **Предварительный просмотр изменений в site. CSS**.</span><span class="sxs-lookup"><span data-stu-id="40110-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="40110-231">Откроется окно, в котором отображаются различия между локальным файлом и его версией в целевой среде.</span><span class="sxs-lookup"><span data-stu-id="40110-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Дифф-контент/site. CSS](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="40110-233">В **Обозреватель решений**щелкните правой кнопкой мыши **site. CSS** и выберите **опубликовать site. CSS**.</span><span class="sxs-lookup"><span data-stu-id="40110-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="40110-234">Окно **действия веб-публикации** показывает, что файл опубликован.</span><span class="sxs-lookup"><span data-stu-id="40110-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![Окно действия веб-публикации](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="40110-236">Откройте браузер по URL-адресу `http://localhost/contosouniversity`, а затем нажмите клавиши CTRL + F5, чтобы вызвать жесткое обновление, чтобы увидеть результат изменения CSS.</span><span class="sxs-lookup"><span data-stu-id="40110-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![Домашняя страница с обычным CSS](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="40110-238">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="40110-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="40110-239">Сводка</span><span class="sxs-lookup"><span data-stu-id="40110-239">Summary</span></span>

<span data-ttu-id="40110-240">Теперь вы видели несколько способов развертывания обновления приложения, которое не затрагивает изменение базы данных, и вы узнали, как просмотреть изменения, чтобы проверить, что именно будет обновлено.</span><span class="sxs-lookup"><span data-stu-id="40110-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="40110-241">На странице инструкторов теперь есть раздел « **курсы** обучения».</span><span class="sxs-lookup"><span data-stu-id="40110-241">The Instructors page now has a **Courses Taught** section.</span></span>

![Страница инструкторов с учеными курсами](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="40110-243">В следующем учебнике показано, как развернуть изменение базы данных. вы добавите поле «ДеньРождения» в базу данных и на страницу инструкторов.</span><span class="sxs-lookup"><span data-stu-id="40110-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="40110-244">[Назад](deploying-to-production.md)
> [Вперед](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="40110-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
