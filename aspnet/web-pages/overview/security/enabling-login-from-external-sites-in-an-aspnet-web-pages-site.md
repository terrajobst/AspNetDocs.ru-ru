---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: Вход с использованием внешних сайтов на сайте веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой статье объясняется, как войти на сайт веб-страницы ASP.NET (Razor) с помощью Facebook, Google, Twitter, Yahoo и других сайтов, то есть о поддержке...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518790"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="9817c-103">Вход с использованием внешних сайтов на сайте веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="9817c-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="9817c-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9817c-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9817c-105">В этой статье объясняется, как войти на сайт веб-страницы ASP.NET (Razor) с помощью Facebook, Google, Twitter, Yahoo и других сайтов, то есть как поддерживать OAuth и OpenID Connect на сайте.</span><span class="sxs-lookup"><span data-stu-id="9817c-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="9817c-106">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="9817c-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="9817c-107">Включение входа с других сайтов при использовании шаблона сайта WebMatrix Starter.</span><span class="sxs-lookup"><span data-stu-id="9817c-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="9817c-108">Это функция ASP.NET, представленная в статье:</span><span class="sxs-lookup"><span data-stu-id="9817c-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="9817c-109">Вспомогательный метод `OAuthWebSecurity`.</span><span class="sxs-lookup"><span data-stu-id="9817c-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9817c-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="9817c-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="9817c-111">Веб-страницы ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="9817c-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="9817c-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="9817c-112">WebMatrix 3</span></span>

<span data-ttu-id="9817c-113">Веб-страницы ASP.NET включает поддержку поставщиков [OAuth](http://oauth.net/) и [OpenID Connect](http://openid.net/) .</span><span class="sxs-lookup"><span data-stu-id="9817c-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="9817c-114">Используя эти поставщики, можно разрешить пользователям входить на сайт с помощью существующих учетных данных из Facebook, Twitter, Microsoft и Google.</span><span class="sxs-lookup"><span data-stu-id="9817c-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="9817c-115">Например, для входа с использованием учетной записи Facebook пользователи могут просто выбрать значок Facebook, который перенаправит их на страницу входа в Facebook, где вводятся сведения о пользователях.</span><span class="sxs-lookup"><span data-stu-id="9817c-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="9817c-116">Затем они могут связать имя входа Facebook со своей учетной записью на сайте.</span><span class="sxs-lookup"><span data-stu-id="9817c-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="9817c-117">Связанное усовершенствование функций членства в веб-страницах заключается в том, что пользователи могут связывать несколько имен входа (включая имена входа из сайтов социальных сетей) с одной учетной записью на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="9817c-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="9817c-118">На этом рисунке показана страница входа из шаблона **начального сайта** , где пользователь может выбрать значок Facebook, Twitter, Google или Microsoft, чтобы включить вход с внешней учетной записью:</span><span class="sxs-lookup"><span data-stu-id="9817c-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![внешние поставщики](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="9817c-120">Вы можете включить членство OAuth и OpenID Connect, раскомментируя несколько строк кода в шаблоне **начального сайта** .</span><span class="sxs-lookup"><span data-stu-id="9817c-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="9817c-121">Методы и свойства, используемые для работы с поставщиками OAuth и OpenID Connect, находятся в классе `WebMatrix.Security.OAuthWebSecurity`.</span><span class="sxs-lookup"><span data-stu-id="9817c-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="9817c-122">Шаблон **начального сайта** включает в себя полную инфраструктуру членства, полную страницу входа, базу данных членства и весь код, позволяющий пользователям входить на сайт с помощью локальных учетных данных или из другого сайта.</span><span class="sxs-lookup"><span data-stu-id="9817c-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="9817c-123">В этом разделе приводится пример того, как разрешить пользователям входить с внешних сайтов на сайт, основанный на шаблоне **начального сайта** .</span><span class="sxs-lookup"><span data-stu-id="9817c-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="9817c-124">После создания начального сайта вы выполните это действие (см. сведения ниже):</span><span class="sxs-lookup"><span data-stu-id="9817c-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="9817c-125">Для сайтов, использующих поставщик OAuth (Facebook, Twitter и Microsoft), вы создаете приложение на внешнем сайте.</span><span class="sxs-lookup"><span data-stu-id="9817c-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="9817c-126">Это дает вам ключи приложений, необходимые для вызова функции входа для этих сайтов.</span><span class="sxs-lookup"><span data-stu-id="9817c-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="9817c-127">Для сайтов, использующих поставщик OpenID Connect (Google), нет необходимости создавать приложение.</span><span class="sxs-lookup"><span data-stu-id="9817c-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="9817c-128">Для всех этих сайтов необходимо иметь учетную запись для входа в систему и создания приложений для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="9817c-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9817c-129">Приложения Майкрософт принимают только URL-адрес рабочего веб-сайта, поэтому вы не можете использовать URL-адрес локального веб-сайта для проверки имен входа.</span><span class="sxs-lookup"><span data-stu-id="9817c-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="9817c-130">Измените несколько файлов на веб-сайте, чтобы указать соответствующий поставщик проверки подлинности и отправить имя входа на сайт, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="9817c-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="9817c-131">В этой статье приводятся отдельные инструкции по выполнению следующих задач.</span><span class="sxs-lookup"><span data-stu-id="9817c-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="9817c-132">Включение учетных записей Google</span><span class="sxs-lookup"><span data-stu-id="9817c-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="9817c-133">Включение имен для входа в Facebook</span><span class="sxs-lookup"><span data-stu-id="9817c-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="9817c-134">Включение имен для входа в Twitter</span><span class="sxs-lookup"><span data-stu-id="9817c-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="9817c-135">Включение учетных записей Google</span><span class="sxs-lookup"><span data-stu-id="9817c-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="9817c-136">Создайте или откройте веб-страницы ASP.NET сайт, основанный на шаблоне сайта WebMatrix Starter.</span><span class="sxs-lookup"><span data-stu-id="9817c-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="9817c-137">Откройте страницу *\_AppStart. cshtml* и раскомментируйте следующую строку кода.</span><span class="sxs-lookup"><span data-stu-id="9817c-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="9817c-138">Тестирование входа Google</span><span class="sxs-lookup"><span data-stu-id="9817c-138">Testing Google login</span></span>

1. <span data-ttu-id="9817c-139">Запустите страницу *Default. cshtml* сайта и нажмите кнопку **Вход** .</span><span class="sxs-lookup"><span data-stu-id="9817c-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="9817c-140">На странице *Вход* в разделе **использовать другую службу для входа в систему** нажмите кнопку Отправить **Google** или **Yahoo** .</span><span class="sxs-lookup"><span data-stu-id="9817c-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="9817c-141">В этом примере используется имя входа Google.</span><span class="sxs-lookup"><span data-stu-id="9817c-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="9817c-142">Веб-страница перенаправляет запрос на страницу входа в Google.</span><span class="sxs-lookup"><span data-stu-id="9817c-142">The web page redirects the request to the Google login page.</span></span>

    ![Вход Google](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="9817c-144">Введите учетные данные для существующей учетной записи Google.</span><span class="sxs-lookup"><span data-stu-id="9817c-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="9817c-145">Если Google спрашивает, нужно ли разрешить *localhost* использовать данные из учетной записи, нажмите кнопку **Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="9817c-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="9817c-146">Код использует маркер Google для проверки подлинности пользователя, а затем возвращается на эту страницу на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="9817c-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="9817c-147">На этой странице пользователи могут связать свое имя входа Google с существующей учетной записью на веб-сайте или зарегистрировать новую учетную запись на сайте, чтобы связать внешнее имя входа с.</span><span class="sxs-lookup"><span data-stu-id="9817c-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="9817c-149">Нажмите кнопку **связать** .</span><span class="sxs-lookup"><span data-stu-id="9817c-149">Choose the **Associate** button.</span></span> <span data-ttu-id="9817c-150">Браузер вернется на домашнюю страницу приложения.</span><span class="sxs-lookup"><span data-stu-id="9817c-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="9817c-151">Включение имен для входа в Facebook</span><span class="sxs-lookup"><span data-stu-id="9817c-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="9817c-152">Перейдите на [сайт разработчиков Facebook](https://developers.facebook.com/apps) (войдите, если вы еще не вошли в систему).</span><span class="sxs-lookup"><span data-stu-id="9817c-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="9817c-153">Нажмите кнопку **создать новое приложение** , а затем следуйте инструкциям на экране, чтобы ввести имя и создать новое приложение.</span><span class="sxs-lookup"><span data-stu-id="9817c-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="9817c-154">В разделе **выберите, как приложение будет интегрироваться с Facebook**, выберите раздел **веб-сайт** .</span><span class="sxs-lookup"><span data-stu-id="9817c-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="9817c-155">В поле **URL-адрес сайта** введите URL-адрес сайта (например, `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="9817c-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="9817c-156">Поле **домена** является необязательным; его можно использовать для проверки подлинности всего домена (например, *example.com*).</span><span class="sxs-lookup"><span data-stu-id="9817c-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="9817c-157">Если вы используете сайт на локальном компьютере с URL-адресом, например `http://localhost:12345` (где номер является локальным номером порта), это значение можно добавить в поле URL- **адрес сайта** для тестирования сайта.</span><span class="sxs-lookup"><span data-stu-id="9817c-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="9817c-158">Однако при каждом изменении номера порта локального сайта необходимо обновить поле **URL-адрес сайта** приложения.</span><span class="sxs-lookup"><span data-stu-id="9817c-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="9817c-159">Нажмите кнопку **сохранить изменения** .</span><span class="sxs-lookup"><span data-stu-id="9817c-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="9817c-160">Снова перейдите на вкладку **приложения** и просмотрите начальную страницу приложения.</span><span class="sxs-lookup"><span data-stu-id="9817c-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="9817c-161">Скопируйте **идентификатор** приложения и значения **секрета** приложения для приложения и вставьте их во временный текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="9817c-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="9817c-162">Эти значения будут переданы поставщику Facebook в коде веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9817c-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="9817c-163">Выйдите из сайта разработчика Facebook.</span><span class="sxs-lookup"><span data-stu-id="9817c-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="9817c-164">Теперь вы вносите изменения на две страницы веб-сайта, чтобы пользователи могли войти на сайт с помощью учетных записей Facebook.</span><span class="sxs-lookup"><span data-stu-id="9817c-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="9817c-165">Создайте или откройте веб-страницы ASP.NET сайт, основанный на шаблоне сайта WebMatrix Starter.</span><span class="sxs-lookup"><span data-stu-id="9817c-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="9817c-166">Откройте страницу *\_AppStart. cshtml* и раскомментируйте код для поставщика OAuth Facebook.</span><span class="sxs-lookup"><span data-stu-id="9817c-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="9817c-167">Блок кода с некомментарием выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9817c-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="9817c-168">Скопируйте значение **идентификатора приложения** из приложения Facebook в качестве значения параметра `appId` (внутри кавычек).</span><span class="sxs-lookup"><span data-stu-id="9817c-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="9817c-169">Скопируйте значение **секрета приложения** из приложения Facebook в качестве значения параметра `appSecret`.</span><span class="sxs-lookup"><span data-stu-id="9817c-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="9817c-170">Сохраните файл и закройте его.</span><span class="sxs-lookup"><span data-stu-id="9817c-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="9817c-171">Тестирование имени входа Facebook</span><span class="sxs-lookup"><span data-stu-id="9817c-171">Testing Facebook login</span></span>

1. <span data-ttu-id="9817c-172">Запустите веб-страницу *Default. cshtml* и нажмите кнопку **Вход** .</span><span class="sxs-lookup"><span data-stu-id="9817c-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="9817c-173">На странице *Вход* в разделе **использовать другую службу для входа** щелкните значок **Facebook** .</span><span class="sxs-lookup"><span data-stu-id="9817c-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="9817c-174">Веб-страница перенаправляет запрос на страницу входа Facebook.</span><span class="sxs-lookup"><span data-stu-id="9817c-174">The web page redirects the request to the Facebook login page.</span></span>

    ![OAuth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="9817c-176">Войдите в учетную запись Facebook.</span><span class="sxs-lookup"><span data-stu-id="9817c-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="9817c-177">В коде используется маркер Facebook для проверки подлинности, а затем возвращается страница, на которой можно связать имя входа Facebook с именем входа вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="9817c-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="9817c-178">Имя пользователя или адрес электронной почты заполняется в поле " **адрес электронной** почты" в форме.</span><span class="sxs-lookup"><span data-stu-id="9817c-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="9817c-180">Нажмите кнопку **связать** .</span><span class="sxs-lookup"><span data-stu-id="9817c-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="9817c-181">Браузер вернется на домашнюю страницу и вы вошли в систему.</span><span class="sxs-lookup"><span data-stu-id="9817c-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="9817c-182">Включение имен для входа в Twitter</span><span class="sxs-lookup"><span data-stu-id="9817c-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="9817c-183">Перейдите на [сайт разработчиков Twitter](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="9817c-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="9817c-184">Выберите ссылку **создать приложение** , а затем войдите на сайт.</span><span class="sxs-lookup"><span data-stu-id="9817c-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="9817c-185">В форме **Создание приложения** заполните поля **имя** и **Описание** .</span><span class="sxs-lookup"><span data-stu-id="9817c-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="9817c-186">В поле **веб-сайт** введите URL-адрес сайта (например, `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="9817c-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="9817c-187">Если вы тестируете сайт локально (используя URL-адрес, например `http://localhost:12345`), то Twitter может не принять этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9817c-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="9817c-188">Однако вы можете использовать локальный IP-адрес замыкания на себя (например `http://127.0.0.1:12345`).</span><span class="sxs-lookup"><span data-stu-id="9817c-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="9817c-189">Это упрощает процесс тестирования приложения локально.</span><span class="sxs-lookup"><span data-stu-id="9817c-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="9817c-190">Однако каждый раз при изменении номера порта локального сайта необходимо обновить поле **веб-сайта** приложения.</span><span class="sxs-lookup"><span data-stu-id="9817c-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="9817c-191">В поле **URL-адрес обратного вызова** введите URL-адрес страницы на веб-сайте, к которой пользователи будут возвращаться после входа в Twitter.</span><span class="sxs-lookup"><span data-stu-id="9817c-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="9817c-192">Например, чтобы отправить пользователей на домашнюю страницу начального сайта (который распознает состояние, в котором они были зарегистрированы), введите тот же URL-адрес, который вы указали в поле **веб-сайт** .</span><span class="sxs-lookup"><span data-stu-id="9817c-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="9817c-193">Примите условия и нажмите кнопку **создать приложение Twitter** .</span><span class="sxs-lookup"><span data-stu-id="9817c-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="9817c-194">На целевой странице **Мои приложения** выберите созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="9817c-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="9817c-195">На вкладке **сведения** прокрутите вниз и нажмите кнопку **создать маркер доступа** .</span><span class="sxs-lookup"><span data-stu-id="9817c-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="9817c-196">На вкладке **сведения** скопируйте значение **ключа** и **секрета потребителя** для своего приложения и вставьте их во временный текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="9817c-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="9817c-197">Эти значения передаются поставщику Twitter в коде веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9817c-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="9817c-198">Выйдите из сайта Twitter.</span><span class="sxs-lookup"><span data-stu-id="9817c-198">Exit the Twitter site.</span></span>

<span data-ttu-id="9817c-199">Теперь вы вносите изменения на две страницы веб-сайта, чтобы пользователи могли входить на сайт с помощью учетных записей Twitter.</span><span class="sxs-lookup"><span data-stu-id="9817c-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="9817c-200">Создайте или откройте веб-страницы ASP.NET сайт, основанный на шаблоне сайта WebMatrix Starter.</span><span class="sxs-lookup"><span data-stu-id="9817c-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="9817c-201">Откройте страницу *\_AppStart. cshtml* и раскомментируйте код для поставщика OAuth "Twitter".</span><span class="sxs-lookup"><span data-stu-id="9817c-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="9817c-202">Блок кода с некомментарием выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9817c-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="9817c-203">Скопируйте значение **ключа потребителя** из приложения Twitter в качестве значения параметра `consumerKey` (внутри кавычек).</span><span class="sxs-lookup"><span data-stu-id="9817c-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="9817c-204">Скопируйте значение **секрета потребителя** из приложения Twitter в качестве значения параметра `consumerSecret`.</span><span class="sxs-lookup"><span data-stu-id="9817c-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="9817c-205">Сохраните файл и закройте его.</span><span class="sxs-lookup"><span data-stu-id="9817c-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="9817c-206">Тестирование имени входа Twitter</span><span class="sxs-lookup"><span data-stu-id="9817c-206">Testing Twitter login</span></span>

1. <span data-ttu-id="9817c-207">Запустите страницу *Default. cshtml* сайта и нажмите кнопку **Вход** .</span><span class="sxs-lookup"><span data-stu-id="9817c-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="9817c-208">На странице *Вход* в разделе **использовать другую службу для входа** выберите значок **Twitter** .</span><span class="sxs-lookup"><span data-stu-id="9817c-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="9817c-209">Веб-страница перенаправляет запрос на страницу входа Twitter для созданного приложения.</span><span class="sxs-lookup"><span data-stu-id="9817c-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![OAuth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="9817c-211">Войдите в учетную запись Twitter.</span><span class="sxs-lookup"><span data-stu-id="9817c-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="9817c-212">Код использует токен Twitter для проверки подлинности пользователя, а затем возвращает вас на страницу, на которой можно связать имя входа с учетной записью веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9817c-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="9817c-213">Ваше имя или адрес электронной почты заполняется в поле " **адрес электронной** почты" в форме.</span><span class="sxs-lookup"><span data-stu-id="9817c-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="9817c-215">Нажмите кнопку **связать** .</span><span class="sxs-lookup"><span data-stu-id="9817c-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="9817c-216">Браузер вернется на домашнюю страницу и вы вошли в систему.</span><span class="sxs-lookup"><span data-stu-id="9817c-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="9817c-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9817c-217">Additional Resources</span></span>

- [<span data-ttu-id="9817c-218">Настройка поведения в масштабах сайта</span><span class="sxs-lookup"><span data-stu-id="9817c-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="9817c-219">Добавление безопасности и членства на веб-страницы ASP.NET сайте</span><span class="sxs-lookup"><span data-stu-id="9817c-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
