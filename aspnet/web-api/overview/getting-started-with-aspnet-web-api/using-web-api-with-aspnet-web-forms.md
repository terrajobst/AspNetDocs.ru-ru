---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Использование веб-API с помощью веб-форм ASP.NET — ASP.NET 4.x
author: MikeWasson
description: Руководства с кодом шаг за шагом, чтобы добавить веб-API в приложение форм ASP.NET для ASP.NET 4.x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422581"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="6de07-103">Использование веб-API с помощью веб-форм ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6de07-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="6de07-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6de07-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="6de07-105">Этот учебник поможет выполнить шаги, чтобы добавить веб-API, на традиционное приложение веб-форм ASP.NET в ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="6de07-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="6de07-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="6de07-106">Overview</span></span>

<span data-ttu-id="6de07-107">Несмотря на то, что веб-API ASP.NET поставляется в комплекте с ASP.NET MVC, это легко реализовать веб-API, на традиционное приложение веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6de07-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="6de07-108">Чтобы использовать веб-API в приложении Web Forms, существует два основных этапа:</span><span class="sxs-lookup"><span data-stu-id="6de07-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="6de07-109">Добавить контроллер веб-API, который является производным от **ApiController** класса.</span><span class="sxs-lookup"><span data-stu-id="6de07-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="6de07-110">Добавление таблицы маршрутов для **приложения\_запустить** метод.</span><span class="sxs-lookup"><span data-stu-id="6de07-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="6de07-111">Создать проект веб-форм</span><span class="sxs-lookup"><span data-stu-id="6de07-111">Create a Web Forms Project</span></span>

<span data-ttu-id="6de07-112">Запустите Visual Studio и выберите **новый проект** из **запустить** страницы.</span><span class="sxs-lookup"><span data-stu-id="6de07-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="6de07-113">Или с **файл** меню, выберите **New** и затем **проекта**.</span><span class="sxs-lookup"><span data-stu-id="6de07-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="6de07-114">В **шаблоны** области выберите **установленные шаблоны** и разверните **Visual C#** узла.</span><span class="sxs-lookup"><span data-stu-id="6de07-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="6de07-115">В разделе **Visual C#** выберите **Web**.</span><span class="sxs-lookup"><span data-stu-id="6de07-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="6de07-116">В списке шаблонов проектов выберите **приложения веб-форм ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="6de07-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="6de07-117">Введите имя для проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6de07-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="6de07-118">Создание модели и контроллера</span><span class="sxs-lookup"><span data-stu-id="6de07-118">Create the Model and Controller</span></span>

<span data-ttu-id="6de07-119">В этом учебнике используется те же классы модели и контроллера, как [Приступая к работе](tutorial-your-first-web-api.md) руководства.</span><span class="sxs-lookup"><span data-stu-id="6de07-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="6de07-120">Во-первых добавьте класс модели.</span><span class="sxs-lookup"><span data-stu-id="6de07-120">First, add a model class.</span></span> <span data-ttu-id="6de07-121">В **обозревателе решений**, щелкните правой кнопкой мыши проект и выберите **Добавление класса**.</span><span class="sxs-lookup"><span data-stu-id="6de07-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="6de07-122">Имя класса продуктов и добавьте следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="6de07-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="6de07-123">Добавьте контроллер Web API в проект., объект *контроллера* — объект, который обрабатывает HTTP-запросы для веб-API.</span><span class="sxs-lookup"><span data-stu-id="6de07-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="6de07-124">В **обозревателе решений** щелкните проект правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="6de07-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="6de07-125">Выберите **Добавление нового элемента**.</span><span class="sxs-lookup"><span data-stu-id="6de07-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="6de07-126">В разделе **установленные шаблоны**, разверните **Visual C#** и выберите **Web**.</span><span class="sxs-lookup"><span data-stu-id="6de07-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="6de07-127">Выберите из списка шаблонов, **класс контроллера веб-API**.</span><span class="sxs-lookup"><span data-stu-id="6de07-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="6de07-128">Имя контроллера «ProductsController» и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="6de07-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="6de07-129">**Добавление нового элемента** мастер создаст файл с именем ProductsController.cs.</span><span class="sxs-lookup"><span data-stu-id="6de07-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="6de07-130">Удалить методы, которые включены в мастере и добавьте следующие методы:</span><span class="sxs-lookup"><span data-stu-id="6de07-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="6de07-131">Дополнительные сведения о коде в этом контроллере, см. в разделе [Приступая к работе](tutorial-your-first-web-api.md) руководства.</span><span class="sxs-lookup"><span data-stu-id="6de07-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="6de07-132">Добавить сведения о маршрутизации</span><span class="sxs-lookup"><span data-stu-id="6de07-132">Add Routing Information</span></span>

<span data-ttu-id="6de07-133">Далее мы добавим URI маршрут таким образом, URI-адреса формы &quot;/API/продукты/&quot; направляются к контроллеру.</span><span class="sxs-lookup"><span data-stu-id="6de07-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="6de07-134">В **обозревателе решений**, дважды щелкните файл Global.asax, чтобы открыть файл с выделенным кодом Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="6de07-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="6de07-135">Добавьте следующий **с помощью** инструкции.</span><span class="sxs-lookup"><span data-stu-id="6de07-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="6de07-136">Затем добавьте следующий код, чтобы **приложения\_запустить** метод:</span><span class="sxs-lookup"><span data-stu-id="6de07-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="6de07-137">Дополнительные сведения о таблицы маршрутизации, см. в разделе [маршрутизации в ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="6de07-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="6de07-138">Добавление AJAX на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="6de07-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="6de07-139">Это все необходимое для создания веб-API, в которой клиенты могут обращаться.</span><span class="sxs-lookup"><span data-stu-id="6de07-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="6de07-140">Теперь давайте добавим страницу HTML, который использует jQuery для вызова API.</span><span class="sxs-lookup"><span data-stu-id="6de07-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="6de07-141">Убедитесь, что главной странице (например, *Site.Master*) включает в себя `ContentPlaceHolder` с `ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="6de07-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="6de07-142">Откройте файл Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="6de07-142">Open the file Default.aspx.</span></span> <span data-ttu-id="6de07-143">Замените стандартный текст, который находится в области основного содержимого, как показано:</span><span class="sxs-lookup"><span data-stu-id="6de07-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="6de07-144">Затем добавьте ссылку на исходный файл jQuery в `HeaderContent` разделе:</span><span class="sxs-lookup"><span data-stu-id="6de07-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="6de07-145">Примечание. Можно легко добавить ссылку на сценарий, перетащив файл из **обозревателе решений** в окне редактора кода.</span><span class="sxs-lookup"><span data-stu-id="6de07-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="6de07-146">Под jQuery тег сценария добавьте следующий блок сценария:</span><span class="sxs-lookup"><span data-stu-id="6de07-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="6de07-147">При загрузке документа, выполняющий запрос AJAX к &quot;api/products&quot;.</span><span class="sxs-lookup"><span data-stu-id="6de07-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="6de07-148">Запрос возвращает список продуктов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="6de07-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="6de07-149">Сценарий добавляет сведения о продукте в таблице HTML.</span><span class="sxs-lookup"><span data-stu-id="6de07-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="6de07-150">При запуске приложения, он должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6de07-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
