---
uid: web-api/overview/security/external-authentication-services
title: Внешние службы проверки подлинностиC#с веб-API ASP.NET () | Документация Майкрософт
author: rmcmurray
description: Описание использования внешних служб проверки подлинности в веб-API ASP.NET.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447420"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="15e76-103">Внешние службы проверки подлинностиC#с веб-API ASP.NET ()</span><span class="sxs-lookup"><span data-stu-id="15e76-103">External Authentication Services with ASP.NET Web API (C#)</span></span>

<span data-ttu-id="15e76-104">Visual Studio 2017 и ASP.NET 4.7.2 расширяют возможности безопасности для [одностраничных приложений](../../../single-page-application/index.md) (SPA) и служб [веб-API](../../index.md) для интеграции с внешними службами проверки подлинности, включая несколько служб OAuth/OpenID Connect и службы проверки подлинности социальных сетей: учетные записи Майкрософт, Twitter, Facebook и Google.</span><span class="sxs-lookup"><span data-stu-id="15e76-104">Visual Studio 2017 and ASP.NET 4.7.2 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>  

### <a name="in-this-walkthrough"></a><span data-ttu-id="15e76-105">В этом пошаговом руководстве</span><span class="sxs-lookup"><span data-stu-id="15e76-105">In this Walkthrough</span></span>

- [<span data-ttu-id="15e76-106">Использование внешних служб проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="15e76-106">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="15e76-107">Создание примера веб-приложения</span><span class="sxs-lookup"><span data-stu-id="15e76-107">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="15e76-108">Включение проверки подлинности Facebook</span><span class="sxs-lookup"><span data-stu-id="15e76-108">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="15e76-109">Включение проверки подлинности Google</span><span class="sxs-lookup"><span data-stu-id="15e76-109">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="15e76-110">Включение проверки подлинности Майкрософт</span><span class="sxs-lookup"><span data-stu-id="15e76-110">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="15e76-111">Включение проверки подлинности Twitter</span><span class="sxs-lookup"><span data-stu-id="15e76-111">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="15e76-112">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="15e76-112">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="15e76-113">Объединение внешних служб проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="15e76-113">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="15e76-114">Настройка IIS Express для использования полного доменного имени</span><span class="sxs-lookup"><span data-stu-id="15e76-114">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="15e76-115">Как получить параметры приложения для проверки подлинности Майкрософт</span><span class="sxs-lookup"><span data-stu-id="15e76-115">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="15e76-116">Необязательно: отключить локальную регистрацию</span><span class="sxs-lookup"><span data-stu-id="15e76-116">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="15e76-117">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="15e76-117">Prerequisites</span></span>

<span data-ttu-id="15e76-118">Для выполнения примеров в этом пошаговом руководстве необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="15e76-118">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="15e76-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="15e76-119">Visual Studio 2017</span></span>
- <span data-ttu-id="15e76-120">Учетная запись разработчика с идентификатором приложения и секретным ключом для одной из следующих служб проверки подлинности социальных сетей:</span><span class="sxs-lookup"><span data-stu-id="15e76-120">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

  - <span data-ttu-id="15e76-121">Учетные записи Майкрософт ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span><span class="sxs-lookup"><span data-stu-id="15e76-121">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
  - <span data-ttu-id="15e76-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span><span class="sxs-lookup"><span data-stu-id="15e76-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
  - <span data-ttu-id="15e76-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span><span class="sxs-lookup"><span data-stu-id="15e76-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>
  - <span data-ttu-id="15e76-124">Google ([https://developers.google.com/](https://developers.google.com))</span><span class="sxs-lookup"><span data-stu-id="15e76-124">Google ([https://developers.google.com/](https://developers.google.com))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="15e76-125">Использование внешних служб проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="15e76-125">Using External Authentication Services</span></span>

<span data-ttu-id="15e76-126">Множество внешних служб проверки подлинности, которые в настоящее время доступны веб-разработчикам, помогают сократить время разработки для создания новых веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="15e76-126">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="15e76-127">Веб-пользователи обычно имеют несколько существующих учетных записей для популярных веб-служб и веб-сайтов социальных сетей, поэтому, когда веб-приложение реализует службы проверки подлинности из внешней веб-службы или веб-сайта социальных сетей, оно сохраняет время разработки, которое было бы затрачено на создание реализации проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="15e76-127">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="15e76-128">Использование внешней службы проверки подлинности экономит пользователей от необходимости создавать другую учетную запись для веб-приложения, а также от необходимости запоминать другое имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="15e76-128">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="15e76-129">В прошлом разработчики имели два варианта: создать собственную реализацию проверки подлинности или изучить интеграцию внешней службы проверки подлинности в свои приложения.</span><span class="sxs-lookup"><span data-stu-id="15e76-129">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="15e76-130">На схеме ниже показан простой поток запросов для агента пользователя (веб-браузера), запрашивающего информацию из веб-приложения, которое настроено для использования внешней службы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="15e76-130">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

<span data-ttu-id="15e76-131">На предыдущей схеме агент пользователя (или веб-браузер в этом примере) выполняет запрос к веб-приложению, которое перенаправляет веб-браузер на внешнюю службу проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="15e76-131">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="15e76-132">Агент пользователя отправляет свои учетные данные внешней службе проверки подлинности, и если агент пользователя успешно прошел проверку подлинности, внешняя служба проверки подлинности перенаправит агент пользователя в исходное веб-приложение с помощью некоторого маркера, который агент пользователя будет передавать в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="15e76-132">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="15e76-133">Веб-приложение будет использовать маркер, чтобы убедиться, что агент пользователя успешно прошел проверку подлинности с помощью внешней службы проверки подлинности, а веб-приложение может использовать маркер для сбора дополнительных сведений об агенте пользователя.</span><span class="sxs-lookup"><span data-stu-id="15e76-133">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="15e76-134">После того, как приложение завершит обработку данных агента пользователя, веб-приложение вернет соответствующий ответ агенту пользователя на основе его параметров авторизации.</span><span class="sxs-lookup"><span data-stu-id="15e76-134">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="15e76-135">Во втором примере агент пользователя согласовывает с веб-приложением и внешним сервером авторизации, а веб-приложение выполняет дополнительное взаимодействие с внешним сервером авторизации для получения дополнительных сведений о пользователе. Субагент</span><span class="sxs-lookup"><span data-stu-id="15e76-135">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

<span data-ttu-id="15e76-136">Visual Studio 2017 и ASP.NET 4.7.2 упрощают интеграцию с внешними службами аутентификации для разработчиков, предоставляя встроенную интеграцию для следующих служб проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="15e76-136">Visual Studio 2017 and ASP.NET 4.7.2 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="15e76-137">Facebook</span><span class="sxs-lookup"><span data-stu-id="15e76-137">Facebook</span></span>
- <span data-ttu-id="15e76-138">Google</span><span class="sxs-lookup"><span data-stu-id="15e76-138">Google</span></span>
- <span data-ttu-id="15e76-139">Учетные записи Майкрософт (учетные записи Windows Live ID)</span><span class="sxs-lookup"><span data-stu-id="15e76-139">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="15e76-140">Twitter</span><span class="sxs-lookup"><span data-stu-id="15e76-140">Twitter</span></span>

<span data-ttu-id="15e76-141">В примерах этого пошагового руководства будет продемонстрировано, как настроить каждую из поддерживаемых внешних служб проверки подлинности с помощью нового шаблона веб-приложения ASP.NET, поставляемого с Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="15e76-141">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="15e76-142">При необходимости может потребоваться добавить полное доменное имя в параметры внешней службы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="15e76-142">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="15e76-143">Это требование основано на ограничениях безопасности для некоторых внешних служб аутентификации, которым требуется полное доменное имя в параметрах приложения, чтобы соответствовать полному доменному имени, используемому клиентами.</span><span class="sxs-lookup"><span data-stu-id="15e76-143">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="15e76-144">(Шаги для этого будут сильно различаться для каждой внешней службы проверки подлинности. для каждой внешней службы проверки подлинности необходимо обратиться к документации, чтобы узнать, является ли это обязательным и как настроить эти параметры.) Если необходимо настроить IIS Express для использования полного доменного имени для тестирования этой среды, см. раздел [настройка IIS Express для использования полного доменного имен](#FQDN) далее в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="15e76-144">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a><span data-ttu-id="15e76-145">Создание примера веб-приложения</span><span class="sxs-lookup"><span data-stu-id="15e76-145">Create a Sample Web Application</span></span>

<span data-ttu-id="15e76-146">Следующие шаги помогут вам создать пример приложения с помощью шаблона веб-приложения ASP.NET. Этот пример приложения будет использоваться для каждой из внешних служб проверки подлинности далее в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="15e76-146">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="15e76-147">Запустите Visual Studio 2017 и выберите **создать проект** на начальной странице.</span><span class="sxs-lookup"><span data-stu-id="15e76-147">Start Visual Studio 2017 and select **New Project** from the Start page.</span></span> <span data-ttu-id="15e76-148">Либо в меню **файл** выберите **создать** , а затем — **проект**.</span><span class="sxs-lookup"><span data-stu-id="15e76-148">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

<span data-ttu-id="15e76-149">Когда откроется диалоговое окно **Создание проекта** , выберите **установлено** и разверните элемент **Visual C#** .</span><span class="sxs-lookup"><span data-stu-id="15e76-149">When the **New Project** dialog box is displayed, select **Installed** and expand **Visual C#**.</span></span> <span data-ttu-id="15e76-150">В **разделе C#визуальный** элемент выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="15e76-150">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="15e76-151">В списке шаблонов проектов выберите **ASP.NET веб-приложение (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="15e76-151">In the list of project templates, select **ASP.NET Web Application (.Net Framework)**.</span></span> <span data-ttu-id="15e76-152">Введите имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="15e76-152">Enter a name for your project and click **OK**.</span></span>

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

<span data-ttu-id="15e76-153">Когда отобразится **Новый проект ASP.NET** , выберите шаблон **одностраничное приложение** и нажмите кнопку **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="15e76-153">When the **New ASP.NET Project** is displayed, select the **Single Page Application** template and click **Create Project**.</span></span>

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

<span data-ttu-id="15e76-154">Подождите, пока Visual Studio 2017 создаст проект.</span><span class="sxs-lookup"><span data-stu-id="15e76-154">Wait as Visual Studio 2017 creates your project.</span></span>

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

<span data-ttu-id="15e76-155">Когда Visual Studio 2017 завершит создание проекта, откройте файл *Startup.auth.CS* , расположенный в папке **app\_Start** .</span><span class="sxs-lookup"><span data-stu-id="15e76-155">When Visual Studio 2017 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="15e76-156">При первом создании проекта ни одна из внешних служб проверки подлинности не включена в файл *Startup.auth.CS* ; Ниже показано, что может напоминать код, и разделы, выделенные для того, чтобы включить внешнюю службу проверки подлинности и соответствующие параметры для использования учетных записей Майкрософт, Twitter, Facebook или Google в приложении ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="15e76-156">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="15e76-157">При нажатии клавиши F5 для сборки и отладки веб-приложения отображается экран входа в систему, где вы увидите, что внешние службы проверки подлинности не определены.</span><span class="sxs-lookup"><span data-stu-id="15e76-157">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

<span data-ttu-id="15e76-158">В следующих разделах вы узнаете, как включить каждую из внешних служб проверки подлинности, предоставляемых с ASP.NET в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="15e76-158">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2017.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="15e76-159">Включение проверки подлинности Facebook</span><span class="sxs-lookup"><span data-stu-id="15e76-159">Enabling Facebook authentication</span></span>

<span data-ttu-id="15e76-160">При использовании проверки подлинности Facebook необходимо создать учетную запись разработчика Facebook, а для работы проекта потребуется идентификатор приложения и секретный ключ из Facebook.</span><span class="sxs-lookup"><span data-stu-id="15e76-160">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="15e76-161">Сведения о создании учетной записи разработчика Facebook и получении идентификатора приложения и секретного ключа см. в разделе [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span><span class="sxs-lookup"><span data-stu-id="15e76-161">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="15e76-162">Получив идентификатор приложения и секретный ключ, выполните следующие действия, чтобы включить проверку подлинности Facebook для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="15e76-162">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="15e76-163">Когда проект откроется в Visual Studio 2017, откройте файл *Startup.auth.CS* .</span><span class="sxs-lookup"><span data-stu-id="15e76-163">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="15e76-164">Откройте раздел кода проверки подлинности Facebook:</span><span class="sxs-lookup"><span data-stu-id="15e76-164">Locate the Facebook authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="15e76-165">Удалите &quot;//&quot; символы, чтобы раскомментировать выделенные строки кода, а затем добавьте идентификатор приложения и секретный ключ.</span><span class="sxs-lookup"><span data-stu-id="15e76-165">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="15e76-166">После добавления этих параметров можно выполнить повторную компиляцию проекта:</span><span class="sxs-lookup"><span data-stu-id="15e76-166">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="15e76-167">При нажатии клавиши F5 для открытия веб-приложения в веб-браузере вы увидите, что Facebook определен как внешняя служба проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="15e76-167">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. <span data-ttu-id="15e76-168">При нажатии кнопки **Facebook** браузер будет перенаправлен на страницу входа Facebook:</span><span class="sxs-lookup"><span data-stu-id="15e76-168">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. <span data-ttu-id="15e76-169">После ввода учетных данных Facebook и нажатия кнопки **войти**ваш веб-браузер перенаправится обратно в веб-приложение, в котором будет предложено ввести **имя пользователя** , которое нужно связать с учетной записью Facebook:</span><span class="sxs-lookup"><span data-stu-id="15e76-169">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. <span data-ttu-id="15e76-170">После того как вы введете имя пользователя и настроили кнопку **Регистрация** , веб-приложение отобразит **домашнюю страницу** по умолчанию для учетной записи Facebook:</span><span class="sxs-lookup"><span data-stu-id="15e76-170">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="15e76-171">Включение проверки подлинности Google</span><span class="sxs-lookup"><span data-stu-id="15e76-171">Enabling Google Authentication</span></span>

<span data-ttu-id="15e76-172">Для использования проверки подлинности Google необходимо создать учетную запись разработчика Google, а для работы с вашим проектом потребуется идентификатор приложения и секретный ключ из Google.</span><span class="sxs-lookup"><span data-stu-id="15e76-172">Using Google authentication requires you to create a Google developer account, and your project will require an application ID and secret key from Google in order to function.</span></span> <span data-ttu-id="15e76-173">Сведения о создании учетной записи разработчика Google и получении идентификатора приложения и секретного ключа см. в разделе [https://developers.google.com](https://developers.google.com).</span><span class="sxs-lookup"><span data-stu-id="15e76-173">For information about creating a Google developer account and obtaining your application ID and secret key, see [https://developers.google.com](https://developers.google.com).</span></span>

<span data-ttu-id="15e76-174">Чтобы включить проверку подлинности Google для веб-приложения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="15e76-174">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="15e76-175">Когда проект откроется в Visual Studio 2017, откройте файл *Startup.auth.CS* .</span><span class="sxs-lookup"><span data-stu-id="15e76-175">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="15e76-176">Откройте раздел кода для проверки подлинности Google:</span><span class="sxs-lookup"><span data-stu-id="15e76-176">Locate the Google authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="15e76-177">Удалите &quot;//&quot; символы, чтобы раскомментировать выделенные строки кода, а затем добавьте идентификатор приложения и секретный ключ.</span><span class="sxs-lookup"><span data-stu-id="15e76-177">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="15e76-178">После добавления этих параметров можно выполнить повторную компиляцию проекта:</span><span class="sxs-lookup"><span data-stu-id="15e76-178">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="15e76-179">При нажатии клавиши F5 для открытия веб-приложения в веб-браузере вы увидите, что Google был определен как внешняя служба проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="15e76-179">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. <span data-ttu-id="15e76-180">При нажатии кнопки **Google** браузер будет перенаправлен на страницу входа в Google:</span><span class="sxs-lookup"><span data-stu-id="15e76-180">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. <span data-ttu-id="15e76-181">После ввода учетных данных Google и нажатия кнопки **войти в**Google появится запрос на подтверждение наличия у веб-приложения разрешений на доступ к учетной записи Google.</span><span class="sxs-lookup"><span data-stu-id="15e76-181">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. <span data-ttu-id="15e76-182">При нажатии кнопки **принять**веб-браузер перенаправится обратно в веб-приложение, в котором будет предложено ввести **имя пользователя** , которое нужно связать с учетной записью Google.</span><span class="sxs-lookup"><span data-stu-id="15e76-182">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. <span data-ttu-id="15e76-183">После того как вы введете имя пользователя и настроили кнопку **Регистрация** , веб-приложение отобразит **домашнюю страницу** по умолчанию для вашей учетной записи Google:</span><span class="sxs-lookup"><span data-stu-id="15e76-183">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="15e76-184">Включение проверки подлинности Майкрософт</span><span class="sxs-lookup"><span data-stu-id="15e76-184">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="15e76-185">Проверка подлинности Майкрософт требует создания учетной записи разработчика, для работы которой требуется идентификатор клиента и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="15e76-185">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="15e76-186">Сведения о создании учетной записи разработчика Майкрософт и получении идентификатора клиента и секрета клиента см. в разделе [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span><span class="sxs-lookup"><span data-stu-id="15e76-186">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="15e76-187">После получения ключа и секрета потребителя выполните следующие действия, чтобы включить проверку подлинности Майкрософт для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="15e76-187">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="15e76-188">Когда проект откроется в Visual Studio 2017, откройте файл *Startup.auth.CS* .</span><span class="sxs-lookup"><span data-stu-id="15e76-188">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="15e76-189">Откройте раздел кода проверки подлинности Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="15e76-189">Locate the Microsoft authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="15e76-190">Удалите &quot;//&quot; символы, чтобы раскомментировать выделенные строки кода, а затем добавьте идентификатор клиента и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="15e76-190">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="15e76-191">После добавления этих параметров можно выполнить повторную компиляцию проекта:</span><span class="sxs-lookup"><span data-stu-id="15e76-191">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="15e76-192">При нажатии клавиши F5 для открытия веб-приложения в веб-браузере вы увидите, что Microsoft определено как внешняя служба проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="15e76-192">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. <span data-ttu-id="15e76-193">При нажатии кнопки " **Microsoft** " браузер будет перенаправлен на страницу входа Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="15e76-193">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. <span data-ttu-id="15e76-194">После ввода учетных данных Майкрософт и нажатия кнопки **войти**вам будет предложено проверить наличие у веб-приложения разрешений на доступ к учетная запись Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="15e76-194">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. <span data-ttu-id="15e76-195">При нажатии кнопки **"Да"** веб-браузер будет перенаправлен обратно в веб-приложение, в котором будет предложено ввести **имя пользователя** , которое нужно связать с учетная запись Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="15e76-195">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. <span data-ttu-id="15e76-196">После того как вы введете имя пользователя и настроили кнопку **Регистрация** , веб-приложение отобразит **домашнюю страницу** по умолчанию для учетная запись Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="15e76-196">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="15e76-197">Включение проверки подлинности Twitter</span><span class="sxs-lookup"><span data-stu-id="15e76-197">Enabling Twitter Authentication</span></span>

<span data-ttu-id="15e76-198">Для проверки подлинности в Twitter необходимо создать учетную запись разработчика, а для ее работы требуется ключ потребителя и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="15e76-198">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="15e76-199">Сведения о создании учетной записи разработчика Twitter и получении ключа потребителя и секрета потребителя см. в разделе [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span><span class="sxs-lookup"><span data-stu-id="15e76-199">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="15e76-200">После получения ключа и секрета потребителя выполните следующие действия, чтобы включить проверку подлинности Twitter для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="15e76-200">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="15e76-201">Когда проект откроется в Visual Studio 2017, откройте файл *Startup.auth.CS* .</span><span class="sxs-lookup"><span data-stu-id="15e76-201">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="15e76-202">Откройте раздел кода проверки подлинности Twitter:</span><span class="sxs-lookup"><span data-stu-id="15e76-202">Locate the Twitter authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="15e76-203">Удалите &quot;//&quot; символы, чтобы раскомментировать выделенные строки кода, а затем добавьте ключ потребителя и секрет потребителя.</span><span class="sxs-lookup"><span data-stu-id="15e76-203">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="15e76-204">После добавления этих параметров можно выполнить повторную компиляцию проекта:</span><span class="sxs-lookup"><span data-stu-id="15e76-204">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="15e76-205">При нажатии клавиши F5 для открытия веб-приложения в веб-браузере вы увидите, что Twitter был определен как внешняя служба проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="15e76-205">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. <span data-ttu-id="15e76-206">При нажатии кнопки **Twitter** браузер будет перенаправлен на страницу входа Twitter:</span><span class="sxs-lookup"><span data-stu-id="15e76-206">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. <span data-ttu-id="15e76-207">После ввода учетных данных Twitter и нажатия кнопки **авторизовать приложение**веб-браузер будет перенаправлен обратно в веб-приложение, в котором будет предложено ввести **имя пользователя** , которое нужно связать с учетной записью Twitter:</span><span class="sxs-lookup"><span data-stu-id="15e76-207">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. <span data-ttu-id="15e76-208">После того как вы введете имя пользователя и настроили кнопку **Регистрация** , в веб-приложении отобразится **Домашняя страница** по умолчанию для учетной записи Twitter:</span><span class="sxs-lookup"><span data-stu-id="15e76-208">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="15e76-209">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="15e76-209">Additional Information</span></span>

<span data-ttu-id="15e76-210">Дополнительные сведения о создании приложений, использующих OAuth и OpenID Connect, см. по следующим URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="15e76-210">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="15e76-211">Объединение внешних служб проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="15e76-211">Combining External Authentication Services</span></span>

<span data-ttu-id="15e76-212">Для большей гибкости можно одновременно определить несколько внешних служб проверки подлинности. Это позволит пользователям веб-приложения использовать учетную запись из любой включенной внешней службы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="15e76-212">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="15e76-213">Настройка IIS Express для использования полного доменного имени</span><span class="sxs-lookup"><span data-stu-id="15e76-213">Configure IIS Express to use a fully qualified domain name</span></span>

<span data-ttu-id="15e76-214">Некоторые внешние поставщики проверки подлинности не поддерживают тестирование приложения с помощью HTTP-адреса, например `http://localhost:port/`.</span><span class="sxs-lookup"><span data-stu-id="15e76-214">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="15e76-215">Чтобы обойти эту ошибку, можно добавить в файл HOSTs статическое сопоставление полного доменного имени (FQDN) и настроить параметры проекта в Visual Studio 2017 для использования полного доменного имени для тестирования и отладки.</span><span class="sxs-lookup"><span data-stu-id="15e76-215">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2017 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="15e76-216">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="15e76-216">To do so, use the following steps:</span></span>

- <span data-ttu-id="15e76-217">Добавьте статическое полное доменное имя, сопоставленное с файлом HOSTs:</span><span class="sxs-lookup"><span data-stu-id="15e76-217">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="15e76-218">Откройте командную строку с повышенными привилегиями в Windows.</span><span class="sxs-lookup"><span data-stu-id="15e76-218">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="15e76-219">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="15e76-219">Type the following command:</span></span>

      <span data-ttu-id="15e76-220"><kbd>Блокнот,%WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="15e76-220"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="15e76-221">Добавьте запись, подобную приведенной ниже, в файл HOSTs:</span><span class="sxs-lookup"><span data-stu-id="15e76-221">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="15e76-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="15e76-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="15e76-223">Сохраните и закройте файл HOSTs.</span><span class="sxs-lookup"><span data-stu-id="15e76-223">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="15e76-224">Настройте проект Visual Studio для использования полного доменного имени:</span><span class="sxs-lookup"><span data-stu-id="15e76-224">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="15e76-225">Когда проект откроется в Visual Studio 2017, откройте меню **проект** и выберите Свойства проекта.</span><span class="sxs-lookup"><span data-stu-id="15e76-225">When your project is open in Visual Studio 2017, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="15e76-226">Например, можно выбрать **Свойства WebApplication1**.</span><span class="sxs-lookup"><span data-stu-id="15e76-226">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="15e76-227">Перейдите на вкладку **веб** .</span><span class="sxs-lookup"><span data-stu-id="15e76-227">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="15e76-228">Введите полное доменное имя для <strong>URL-адреса проекта</strong>.</span><span class="sxs-lookup"><span data-stu-id="15e76-228">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="15e76-229">Например, можно ввести <kbd><http://www.wingtiptoys.com></kbd> , если это сопоставление FQDN, добавленное в файл hosts.</span><span class="sxs-lookup"><span data-stu-id="15e76-229">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="15e76-230">Настройте IIS Express для использования полного доменного имени приложения:</span><span class="sxs-lookup"><span data-stu-id="15e76-230">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="15e76-231">Откройте командную строку с повышенными привилегиями в Windows.</span><span class="sxs-lookup"><span data-stu-id="15e76-231">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="15e76-232">Введите следующую команду, чтобы перейти к папке IIS Express:</span><span class="sxs-lookup"><span data-stu-id="15e76-232">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="15e76-233"><kbd>CD/d &quot;%Програмфилес%\иис Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="15e76-233"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="15e76-234">Введите следующую команду, чтобы добавить полное доменное имя в приложение:</span><span class="sxs-lookup"><span data-stu-id="15e76-234">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="15e76-235"><kbd>Appcmd. exe set config-Section: System. applicationHost/Sites/+&quot;[имя = ' WebApplication1 ']. Bindings. [Protocol = ' http ', bindingInformation = ' \*: 80: www. wingtiptoys. com ']&quot;/commit: APPHOST</kbd></span><span class="sxs-lookup"><span data-stu-id="15e76-235"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="15e76-236">Где **WebApplication1** — имя вашего проекта, а **bindingInformation** содержит номер порта и полное доменное имя, которое вы хотите использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="15e76-236">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="15e76-237">Как получить параметры приложения для проверки подлинности Майкрософт</span><span class="sxs-lookup"><span data-stu-id="15e76-237">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="15e76-238">Связывание приложения с Windows Live для проверки подлинности Майкрософт — это простой процесс.</span><span class="sxs-lookup"><span data-stu-id="15e76-238">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="15e76-239">Если вы еще не связали приложение с Windows Live, можно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="15e76-239">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="15e76-240">Перейдите к [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) и введите имя учетная запись Майкрософт и пароль при появлении запроса, а затем щелкните **войти**:</span><span class="sxs-lookup"><span data-stu-id="15e76-240">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. <span data-ttu-id="15e76-241">Выберите **Добавить приложение** и введите имя приложения при появлении запроса, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="15e76-241">Select **Add an app** and enter the name of your application when prompted, and then click **Create**:</span></span>

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. <span data-ttu-id="15e76-242">Выберите свое приложение в списке **имя** и свойства его приложения.</span><span class="sxs-lookup"><span data-stu-id="15e76-242">Select your app under **Name** and its application properties page appears.</span></span>

4. <span data-ttu-id="15e76-243">Введите домен перенаправления для приложения.</span><span class="sxs-lookup"><span data-stu-id="15e76-243">Enter the redirect domain for your application.</span></span> <span data-ttu-id="15e76-244">Скопируйте **идентификатор приложения** и в разделе **секреты приложения**выберите **создать пароль**.</span><span class="sxs-lookup"><span data-stu-id="15e76-244">Copy the **Application ID** and, under **Application Secrets**, select **Generate Password**.</span></span> <span data-ttu-id="15e76-245">Скопируйте отображаемый пароль.</span><span class="sxs-lookup"><span data-stu-id="15e76-245">Copy the password that appears.</span></span> <span data-ttu-id="15e76-246">ИДЕНТИФИКАТОР и пароль приложения являются ИДЕНТИФИКАТОРом клиента и секретом клиента.</span><span class="sxs-lookup"><span data-stu-id="15e76-246">The application ID and password are your client ID and client secret.</span></span> <span data-ttu-id="15e76-247">Нажмите кнопку **ОК** , а затем **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="15e76-247">Select **Ok** and then **Save**.</span></span>

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="15e76-248">Необязательно: отключить локальную регистрацию</span><span class="sxs-lookup"><span data-stu-id="15e76-248">Optional: Disable Local Registration</span></span>

<span data-ttu-id="15e76-249">Текущая функция локальной регистрации ASP.NET не мешает автоматическим программам (программы-роботы) создавать учетные записи членов. Например, с помощью технологии «Bot-предотвращение» и проверки, такой как [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span><span class="sxs-lookup"><span data-stu-id="15e76-249">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="15e76-250">Поэтому на странице входа необходимо удалить локальную форму входа и ссылку регистрации.</span><span class="sxs-lookup"><span data-stu-id="15e76-250">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="15e76-251">Для этого откройте страницу *\_Login. cshtml* в проекте, а затем закомментируйте строки для локальной панели входа и регистрационной ссылки.</span><span class="sxs-lookup"><span data-stu-id="15e76-251">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="15e76-252">Полученная страница должна выглядеть, как в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="15e76-252">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="15e76-253">После отключения локальной панели входа и ссылки регистрации на странице входа будут отображаться только внешние поставщики проверки подлинности, которые были включены.</span><span class="sxs-lookup"><span data-stu-id="15e76-253">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
