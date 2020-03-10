---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Публикация приложения в службе приложений Azure Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504762"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="c12c9-102">Публикация приложения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c12c9-102">Publish the App to Azure Azure App Service</span></span>

<span data-ttu-id="c12c9-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c12c9-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c12c9-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="c12c9-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="c12c9-105">На последнем шаге вы опубликуете приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="c12c9-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="c12c9-106">В обозреватель решений щелкните правой кнопкой мыши проект и выберите **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c12c9-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="c12c9-107">При нажатии кнопки **опубликовать** открывается диалоговое окно **Публикация веб-сайта** .</span><span class="sxs-lookup"><span data-stu-id="c12c9-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="c12c9-108">Если вы вернули **узел в облаке** при первом создании проекта, подключение и параметры уже настроены.</span><span class="sxs-lookup"><span data-stu-id="c12c9-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="c12c9-109">В этом случае просто перейдите на вкладку **Параметры** и установите флажок &quot;выполнить Code First migrations&quot;.</span><span class="sxs-lookup"><span data-stu-id="c12c9-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="c12c9-110">(Если вы не проверите **размещение в облаке** в начале, выполните действия, описанные в [следующем разделе](#new-website).)</span><span class="sxs-lookup"><span data-stu-id="c12c9-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="c12c9-111">Чтобы развернуть приложение, нажмите кнопку **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c12c9-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="c12c9-112">Ход публикации можно просмотреть в окне **действия веб-публикации** .</span><span class="sxs-lookup"><span data-stu-id="c12c9-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="c12c9-113">(В меню **вид** выберите **другие окна**, а затем — **действие веб-публикации**.)</span><span class="sxs-lookup"><span data-stu-id="c12c9-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="c12c9-114">Когда Visual Studio завершит развертывание приложения, браузер по умолчанию автоматически откроет URL-адрес развернутого веб-сайта, а созданное приложение будет запущено в облаке.</span><span class="sxs-lookup"><span data-stu-id="c12c9-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="c12c9-115">URL-адрес в адресной строке браузера показывает, что сайт загружается из Интернета.</span><span class="sxs-lookup"><span data-stu-id="c12c9-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="c12c9-116">Развертывание на новом веб-сайте</span><span class="sxs-lookup"><span data-stu-id="c12c9-116">Deploying to a New Website</span></span>

<span data-ttu-id="c12c9-117">Если вы не устанавливали **узел в облаке** при создании проекта, вы можете настроить новое веб-приложение сейчас.</span><span class="sxs-lookup"><span data-stu-id="c12c9-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="c12c9-118">В обозреватель решений щелкните правой кнопкой мыши проект и выберите **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c12c9-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="c12c9-119">Перейдите на вкладку **профиль** и щелкните **Microsoft Azure веб-сайты**.</span><span class="sxs-lookup"><span data-stu-id="c12c9-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="c12c9-120">Если вы не вошли в Azure, вам будет предложено выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="c12c9-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="c12c9-121">В диалоговом окне **существующие веб-сайты** нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="c12c9-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="c12c9-122">Введите имя сайта.</span><span class="sxs-lookup"><span data-stu-id="c12c9-122">Enter a site name.</span></span> <span data-ttu-id="c12c9-123">Выберите подписку Azure и регион.</span><span class="sxs-lookup"><span data-stu-id="c12c9-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="c12c9-124">В разделе **сервер базы данных**выберите **создать новый сервер**или выберите существующий сервер.</span><span class="sxs-lookup"><span data-stu-id="c12c9-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="c12c9-125">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c12c9-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="c12c9-126">Перейдите на вкладку **Параметры** и установите флажок &quot;выполнить Code First migrations&quot;.</span><span class="sxs-lookup"><span data-stu-id="c12c9-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="c12c9-127">Затем нажать кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c12c9-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c12c9-128">Назад</span><span class="sxs-lookup"><span data-stu-id="c12c9-128">Previous</span></span>](part-9.md)
