---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Создание приложения MVC 5 с помощью Facebook, Twitter, LinkedIn и Google OAuth2 Sign-OnC#() | Документация Майкрософт
author: Rick-Anderson
description: В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5, которое позволяет пользователям выполнять вход с использованием OAuth 2,0 с учетными данными из внешнего й...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456510"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="022c7-103">Создание приложения ASP.NET MVC 5 с единым входом с помощью учетных данных Facebook, Twitter, LinkedIn и Google OAuth2 (C#)</span><span class="sxs-lookup"><span data-stu-id="022c7-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="022c7-104">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="022c7-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="022c7-105">В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5, которое позволяет пользователям входить в систему с помощью [OAuth 2,0](http://oauth.net/2/) с учетными данными от внешнего поставщика проверки подлинности, например Facebook, Twitter, LinkedIn, Microsoft или Google.</span><span class="sxs-lookup"><span data-stu-id="022c7-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="022c7-106">Для простоты в этом учебнике рассматривается работа с учетными данными из Facebook и Google.</span><span class="sxs-lookup"><span data-stu-id="022c7-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="022c7-107">Включение этих учетных данных на веб-сайтах обеспечивает значительное преимущество, поскольку миллионы пользователей уже имеют учетные записи с этими внешними поставщиками.</span><span class="sxs-lookup"><span data-stu-id="022c7-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="022c7-108">Эти пользователи могут быть более наклонными для регистрации на сайте, если им не нужно создавать и запоминать новый набор учетных данных.</span><span class="sxs-lookup"><span data-stu-id="022c7-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="022c7-109">См. также [приложение ASP.NET MVC 5 с использованием SMS и двухфакторной проверки подлинности по электронной почте](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="022c7-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="022c7-110">В этом учебнике также показано, как добавить данные профиля для пользователя и как использовать API членства для добавления ролей.</span><span class="sxs-lookup"><span data-stu-id="022c7-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="022c7-111">Этот учебник написан на [Рик Андерсон (](https://blogs.msdn.com/rickAndy) (следуйте указаниям в Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="022c7-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="022c7-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="022c7-112">Getting Started</span></span>

<span data-ttu-id="022c7-113">Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="022c7-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="022c7-114">Установите Visual Studio [2013 с обновлением 3](https://go.microsoft.com/fwlink/?LinkId=390521) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="022c7-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="022c7-115">Дополнительные сведения о Dropbox, GitHub, LinkedIn, Instagram, buffer, Salesforce, STEAM, обмене стеками, Трипит, Твитч, Twitter, Yahoo! и др. см. в этом [образце проекта](https://github.com/matthewdunsdon/oauthforaspnet).</span><span class="sxs-lookup"><span data-stu-id="022c7-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="022c7-116">Необходимо установить Visual Studio [2013 с обновлением 3](https://go.microsoft.com/fwlink/?LinkId=390521) или более поздней версии, чтобы использовать Google OAuth 2 и локально выполнять отладку без предупреждений SSL.</span><span class="sxs-lookup"><span data-stu-id="022c7-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="022c7-117">Нажмите кнопку **создать проект** на **начальной** странице, либо можно воспользоваться меню, выбрать **файл**, а затем **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="022c7-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="022c7-118">Создание первого приложения</span><span class="sxs-lookup"><span data-stu-id="022c7-118">Creating Your First Application</span></span>

<span data-ttu-id="022c7-119">Щелкните **создать проект**, выберите элемент **Visual C#**  слева, затем — **веб** , а затем выберите **веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="022c7-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="022c7-120">Присвойте проекту имя "Мвкаус" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="022c7-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="022c7-121">В диалоговом окне **Новый проект ASP.NET** щелкните **MVC**.</span><span class="sxs-lookup"><span data-stu-id="022c7-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="022c7-122">Если проверка подлинности не является **отдельной учетной записью пользователя**, нажмите кнопку **изменить проверку подлинности** и выберите **отдельные учетные записи пользователей**.</span><span class="sxs-lookup"><span data-stu-id="022c7-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="022c7-123">Проверив **размещение в облаке**, приложение будет легко размещаться в Azure.</span><span class="sxs-lookup"><span data-stu-id="022c7-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="022c7-124">Если вы выбрали **узел в облаке**, заполните диалоговое окно настройки.</span><span class="sxs-lookup"><span data-stu-id="022c7-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="022c7-125">Использование NuGet для обновления по промежуточного слоя OWIN</span><span class="sxs-lookup"><span data-stu-id="022c7-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="022c7-126">Используйте диспетчер пакетов NuGet для обновления по [промежуточного слоя OWIN](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span><span class="sxs-lookup"><span data-stu-id="022c7-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="022c7-127">В меню слева выберите **обновления** .</span><span class="sxs-lookup"><span data-stu-id="022c7-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="022c7-128">Можно нажать кнопку " **Обновить все** " или выполнить поиск только пакетов OWIN (показанных на следующем рисунке):</span><span class="sxs-lookup"><span data-stu-id="022c7-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="022c7-129">На рисунке ниже показаны только пакеты OWIN:</span><span class="sxs-lookup"><span data-stu-id="022c7-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="022c7-130">В консоли диспетчера пакетов (PMC) можно ввести команду `Update-Package`, которая будет обновлять все пакеты.</span><span class="sxs-lookup"><span data-stu-id="022c7-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="022c7-131">Нажмите клавишу **F5** или **CTRL + F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="022c7-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="022c7-132">На рисунке ниже показан номер порта 1234.</span><span class="sxs-lookup"><span data-stu-id="022c7-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="022c7-133">При запуске приложения вы увидите другой номер порта.</span><span class="sxs-lookup"><span data-stu-id="022c7-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="022c7-134">В зависимости от размера окна браузера может потребоваться щелкнуть значок навигации, чтобы просмотреть ссылки **Домашняя страница**, **сведения о** **контакте**, **Регистрация** и **Вход** .</span><span class="sxs-lookup"><span data-stu-id="022c7-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="022c7-135">Настройка SSL в проекте</span><span class="sxs-lookup"><span data-stu-id="022c7-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="022c7-136">Для подключения к поставщикам проверки подлинности, таким как Google и Facebook, необходимо настроить IIS-Express для использования SSL.</span><span class="sxs-lookup"><span data-stu-id="022c7-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="022c7-137">Важно использовать SSL после входа в систему, а не отменять его на HTTP, файл cookie для входа является как секретным именем пользователя и паролем, и без использования SSL вы отправляете его в виде открытого текста по каналу передачи.</span><span class="sxs-lookup"><span data-stu-id="022c7-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="022c7-138">Кроме того, вы уже предоставили время для выполнения подтверждения и обеспечения безопасности канала (который представляет собой основную часть того, что делает HTTPS медленнее, чем HTTP) до выполнения конвейера MVC, поэтому перенаправление обратно на HTTP после входа в систему не сделает текущий запрос или будущее. запросы выполняются гораздо быстрее.</span><span class="sxs-lookup"><span data-stu-id="022c7-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="022c7-139">В **Обозреватель решений**щелкните проект **мвкаус** .</span><span class="sxs-lookup"><span data-stu-id="022c7-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="022c7-140">Нажмите клавишу F4, чтобы отобразить свойства проекта.</span><span class="sxs-lookup"><span data-stu-id="022c7-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="022c7-141">Кроме того, в меню **вид** можно выбрать **окно свойства**.</span><span class="sxs-lookup"><span data-stu-id="022c7-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="022c7-142">Измените значение по **протоколу SSL с Enabled** на true.</span><span class="sxs-lookup"><span data-stu-id="022c7-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="022c7-143">Скопируйте URL-адрес SSL (который будет `https://localhost:44300/`, если не созданы другие проекты SSL).</span><span class="sxs-lookup"><span data-stu-id="022c7-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="022c7-144">В **Обозреватель решений**щелкните правой кнопкой мыши проект **мвкаус** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="022c7-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="022c7-145">Перейдите на вкладку **веб** и вставьте URL-адрес SSL в поле **URL-адрес проекта** .</span><span class="sxs-lookup"><span data-stu-id="022c7-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="022c7-146">Сохраните файл (CTL + S).</span><span class="sxs-lookup"><span data-stu-id="022c7-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="022c7-147">Этот URL-адрес потребуется для настройки приложений проверки подлинности Facebook и Google.</span><span class="sxs-lookup"><span data-stu-id="022c7-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="022c7-148">Добавьте атрибут [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) к контроллеру `Home`, чтобы все запросы должны использовать HTTPS.</span><span class="sxs-lookup"><span data-stu-id="022c7-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="022c7-149">Более безопасный подход заключается в добавлении фильтра [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) в приложение.</span><span class="sxs-lookup"><span data-stu-id="022c7-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="022c7-150">См. раздел &quot;Защита приложения с помощью SSL и атрибута авторизации&quot; в моем руководстве [Создание приложения ASP.NET MVC с проверкой подлинности и базой данных SQL и развертывание в службе приложений Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="022c7-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="022c7-151">Ниже показана часть контроллера Home.</span><span class="sxs-lookup"><span data-stu-id="022c7-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="022c7-152">Для запуска приложения нажмите сочетание клавиш CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="022c7-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="022c7-153">Если вы установили сертификат ранее, можно пропустить оставшуюся часть этого раздела и перейти к [созданию приложения Google для OAuth 2 и подключению приложения к проекту](#goog). в противном случае следуйте инструкциям, чтобы доверять самозаверяющий сертификат, который IIS Express создан.</span><span class="sxs-lookup"><span data-stu-id="022c7-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="022c7-154">Прочтите диалоговое окно **Security Warning (предупреждение системы безопасности** ) и нажмите кнопку **Да** , если хотите установить сертификат, представляющий localhost.</span><span class="sxs-lookup"><span data-stu-id="022c7-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="022c7-155">В IE откроется *Главная* страница без предупреждений SSL.</span><span class="sxs-lookup"><span data-stu-id="022c7-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="022c7-156">Google Chrome также принимает сертификат и будет отображать HTTPS-содержимое без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="022c7-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="022c7-157">Firefox использует собственное хранилище сертификатов, поэтому отобразится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="022c7-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="022c7-158">Для нашего приложения можно безопасно щелкнуть **я понимаю риски**.</span><span class="sxs-lookup"><span data-stu-id="022c7-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="022c7-159">Создание приложения Google для OAuth 2 и подключение приложения к проекту</span><span class="sxs-lookup"><span data-stu-id="022c7-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="022c7-160">Текущие инструкции Google OAuth см. [в разделе Настройка проверки подлинности Google в ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="022c7-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="022c7-161">Перейдите к [Консоли разработчиков Google](https://console.developers.google.com/).</span><span class="sxs-lookup"><span data-stu-id="022c7-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="022c7-162">Если вы еще не создали проект, выберите **учетные данные** на вкладке слева и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="022c7-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="022c7-163">На вкладке слева щелкните **учетные данные**.</span><span class="sxs-lookup"><span data-stu-id="022c7-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="022c7-164">Щелкните **создать учетные данные** , а затем — **идентификатор клиента OAuth**.</span><span class="sxs-lookup"><span data-stu-id="022c7-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="022c7-165">В диалоговом окне **создать идентификатор клиента** следует использовать **веб-приложение** по умолчанию для типа приложения.</span><span class="sxs-lookup"><span data-stu-id="022c7-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="022c7-166">Установите для **полномочных источников JavaScript** URL-адрес SSL, который вы использовали ранее (`https://localhost:44300/`, если не созданы другие проекты SSL).</span><span class="sxs-lookup"><span data-stu-id="022c7-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="022c7-167">Задайте для подходящего **URI перенаправления** значение:</span><span class="sxs-lookup"><span data-stu-id="022c7-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="022c7-168">Щелкните элемент меню экрана согласия OAuth, а затем укажите адрес электронной почты и название продукта.</span><span class="sxs-lookup"><span data-stu-id="022c7-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="022c7-169">Завершив заполнение формы, нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="022c7-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="022c7-170">Щелкните пункт меню Библиотека, найдите **Google + API**, щелкните его и нажмите включить.</span><span class="sxs-lookup"><span data-stu-id="022c7-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="022c7-171">На рисунке ниже показаны включенные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="022c7-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="022c7-172">В диспетчере API Google API посетите вкладку **учетные данные** , чтобы получить **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="022c7-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="022c7-173">Скачайте, чтобы сохранить JSON-файл с секретами приложения.</span><span class="sxs-lookup"><span data-stu-id="022c7-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="022c7-174">Скопируйте и вставьте **ClientID** и **ClientSecret** в метод `UseGoogleAuthentication`, находящийся в файле *Startup.auth.CS* в папке *App_Start* .</span><span class="sxs-lookup"><span data-stu-id="022c7-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="022c7-175">Значения **ClientID** и **ClientSecret** , показанные ниже, являются примерами и не работают.</span><span class="sxs-lookup"><span data-stu-id="022c7-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="022c7-176">Безопасность — никогда не храните конфиденциальные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="022c7-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="022c7-177">Учетная запись и учетные данные добавляются в приведенный выше код для упрощения примера.</span><span class="sxs-lookup"><span data-stu-id="022c7-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="022c7-178">См. рекомендации [по развертыванию паролей и других конфиденциальных данных в ASP.NET и службе приложений Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="022c7-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="022c7-179">Нажмите **CTRL+F5** , чтобы построить и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="022c7-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="022c7-180">Щелкните ссылку **Войти в систему** .</span><span class="sxs-lookup"><span data-stu-id="022c7-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="022c7-181">В разделе **использовать другую службу для входа**щелкните **Google**.</span><span class="sxs-lookup"><span data-stu-id="022c7-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="022c7-182">Если вы пропустили какие-либо из описанных выше действий, возникнет ошибка HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="022c7-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="022c7-183">Выполните приведенные выше действия.</span><span class="sxs-lookup"><span data-stu-id="022c7-183">Recheck your steps above.</span></span> <span data-ttu-id="022c7-184">Если вы пропустили требуемый параметр (например, **Название продукта**), добавьте недостающий элемент и сохраните его. Проверка подлинности может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="022c7-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="022c7-185">Вы будете перенаправлены на сайт Google, на который вы будете вводить свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="022c7-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="022c7-186">После ввода учетных данных появится запрос на получение разрешений для веб-приложения, которое было только что создано:</span><span class="sxs-lookup"><span data-stu-id="022c7-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="022c7-187">Нажмите кнопку **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="022c7-187">Click **Accept**.</span></span> <span data-ttu-id="022c7-188">Теперь вы будете перенаправлены обратно на страницу **регистрации** приложения мвкаус, где можно зарегистрировать учетную запись Google.</span><span class="sxs-lookup"><span data-stu-id="022c7-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="022c7-189">Вы можете изменить имя регистрации локального адреса электронной почты, используемое для учетной записи Gmail, но в общем случае необходимо использовать псевдоним электронной почты по умолчанию (то есть тот, который использовался для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="022c7-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="022c7-190">Щелкните **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="022c7-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="022c7-191">Создание приложения в Facebook и подключение приложения к проекту</span><span class="sxs-lookup"><span data-stu-id="022c7-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="022c7-192">Текущие инструкции по проверке подлинности Facebook OAuth2 см. в статье [Настройка проверки подлинности Facebook](/aspnet/core/security/authentication/social/facebook-logins) .</span><span class="sxs-lookup"><span data-stu-id="022c7-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="022c7-193">Проверка данных членства</span><span class="sxs-lookup"><span data-stu-id="022c7-193">Examine the Membership Data</span></span>

<span data-ttu-id="022c7-194">В меню **вид** выберите пункт **Обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="022c7-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="022c7-195">Разверните узел **DefaultConnection (мвкаус)** , разверните узел **таблицы**, щелкните правой кнопкой мыши элемент **AspNetUsers** и выберите команду **отобразить данные таблицы**.</span><span class="sxs-lookup"><span data-stu-id="022c7-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![данные таблицы aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="022c7-197">Добавление данных профиля в класс User</span><span class="sxs-lookup"><span data-stu-id="022c7-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="022c7-198">В этом разделе вы добавите дату рождения и домашний город в пользовательские данные во время регистрации, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="022c7-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![reg с помощью домашнего города и Бдай](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="022c7-200">Откройте файл *моделс\идентитимоделс.КС* и добавьте свойства Дата рождения и домашний город:</span><span class="sxs-lookup"><span data-stu-id="022c7-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="022c7-201">Откройте файл *моделс\аккаунтвиевмоделс.КС* и задайте свойства Дата рождения и домашний город в `ExternalLoginConfirmationViewModel`.</span><span class="sxs-lookup"><span data-stu-id="022c7-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="022c7-202">Откройте файл *контроллерс\аккаунтконтроллер.КС* и добавьте код для даты рождения и домашнего города в метод действия `ExternalLoginConfirmation`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="022c7-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="022c7-203">Добавьте дату рождения и домашний город в файл *виевс\аккаунт\екстерналлогинконфирматион.кштмл* :</span><span class="sxs-lookup"><span data-stu-id="022c7-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="022c7-204">Удалите базу данных членства, чтобы снова зарегистрировать свою учетную запись Facebook в приложении, и убедитесь, что вы можете добавить новую дату рождения и сведения личного профиля города.</span><span class="sxs-lookup"><span data-stu-id="022c7-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="022c7-205">В **Обозреватель решений**щелкните значок **Показывать все файлы** , щелкните правой кнопкой мыши *добавить\_дата\аспнет-мвкаус-&lt;датестамп&gt;. mdf* и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="022c7-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="022c7-206">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем щелкните **консоль диспетчера пакетов** (PMC).</span><span class="sxs-lookup"><span data-stu-id="022c7-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="022c7-207">Введите следующие команды в PMC.</span><span class="sxs-lookup"><span data-stu-id="022c7-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="022c7-208">Включение и миграция</span><span class="sxs-lookup"><span data-stu-id="022c7-208">Enable-Migrations</span></span>
2. <span data-ttu-id="022c7-209">Инициализация добавления и миграции</span><span class="sxs-lookup"><span data-stu-id="022c7-209">Add-Migration Init</span></span>
3. <span data-ttu-id="022c7-210">Обновление базы данных</span><span class="sxs-lookup"><span data-stu-id="022c7-210">Update-Database</span></span>

<span data-ttu-id="022c7-211">Запустите приложение и используйте FaceBook и Google для входа и регистрации некоторых пользователей.</span><span class="sxs-lookup"><span data-stu-id="022c7-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="022c7-212">Проверка данных членства</span><span class="sxs-lookup"><span data-stu-id="022c7-212">Examine the Membership Data</span></span>

<span data-ttu-id="022c7-213">В меню **вид** выберите пункт **Обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="022c7-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="022c7-214">Щелкните правой кнопкой мыши **AspNetUsers** и выберите команду " **отобразить данные таблицы**".</span><span class="sxs-lookup"><span data-stu-id="022c7-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="022c7-215">Ниже показаны поля `HomeTown` и `BirthDate`.</span><span class="sxs-lookup"><span data-stu-id="022c7-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="022c7-216">Выход из приложения и вход с другой учетной записью</span><span class="sxs-lookup"><span data-stu-id="022c7-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="022c7-217">Если вы входите в приложение с помощью Facebook, а затем выйдете из сети и попытаетесь войти еще раз с другой учетной записью Facebook (используя тот же браузер), вы сразу же войдете в предыдущую учетную запись Facebook, которую вы использовали.</span><span class="sxs-lookup"><span data-stu-id="022c7-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="022c7-218">Чтобы использовать другую учетную запись, перейдите в Facebook и выйдите из Facebook.</span><span class="sxs-lookup"><span data-stu-id="022c7-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="022c7-219">То же правило применяется к любому другому поставщику проверки подлинности стороннего производителя.</span><span class="sxs-lookup"><span data-stu-id="022c7-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="022c7-220">Кроме того, можно войти в систему с другой учетной записью, используя другой браузер.</span><span class="sxs-lookup"><span data-stu-id="022c7-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="022c7-221">Next Steps</span><span class="sxs-lookup"><span data-stu-id="022c7-221">Next Steps</span></span>

<span data-ttu-id="022c7-222">См. статью [Знакомство с поставщиками безопасности Yahoo и LinkedIn OAuth для OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) с помощью Джерри Пелсер для Yahoo и LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="022c7-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="022c7-223">Чтобы включить кнопки входа в социальных сетях, см. Джерри кнопки входа в систему ASP.NET MVC 5.</span><span class="sxs-lookup"><span data-stu-id="022c7-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="022c7-224">Следуйте указаниям [в моем руководстве создание приложения ASP.NET MVC с проверкой подлинности и базой данных SQL и развертывание в службе приложений Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), которое продолжится в этом руководстве и демонстрирует следующее:</span><span class="sxs-lookup"><span data-stu-id="022c7-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="022c7-225">Развертывание приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="022c7-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="022c7-226">Как защитить приложение с помощью ролей.</span><span class="sxs-lookup"><span data-stu-id="022c7-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="022c7-227">Как защитить приложение с помощью фильтров [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) и [авторизации](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) .</span><span class="sxs-lookup"><span data-stu-id="022c7-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="022c7-228">Как использовать API членства для добавления пользователей и ролей.</span><span class="sxs-lookup"><span data-stu-id="022c7-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="022c7-229">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что мы можем улучшить.</span><span class="sxs-lookup"><span data-stu-id="022c7-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="022c7-230">Вы также можете запросить новые темы [, как показано в разделе как с кодом](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span><span class="sxs-lookup"><span data-stu-id="022c7-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="022c7-231">Вы можете даже попросить и проголосовать за новые функции, которые будут добавлены в ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="022c7-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="022c7-232">Например, можно проголосовать за средство для [создания пользователей и ролей и управления ими.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="022c7-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="022c7-233">Хорошее описание работы служб внешней аутентификации ASP.NET см. в статье о [внешних службах аутентификации](https://asp.net/web-api/overview/security/external-authentication-services)Роберт мкмуррай.</span><span class="sxs-lookup"><span data-stu-id="022c7-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="022c7-234">Статья Роберт также подробно рассказывает о включении проверки подлинности Майкрософт и Twitter.</span><span class="sxs-lookup"><span data-stu-id="022c7-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="022c7-235">Отличное [руководство по EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Tom Dykstra) демонстрирует работу с Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="022c7-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
