---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Использование веб-API с ASP.NET Web Forms-ASP.NET 4. x
author: MikeWasson
description: Руководство с кодом пошаговым руководством по добавлению веб-API в приложение ASP.NET Forms для ASP.NET 4. x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448536"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="71925-103">Использование веб-API с помощью веб-форм ASP.NET</span><span class="sxs-lookup"><span data-stu-id="71925-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="71925-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="71925-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="71925-105">В этом руководстве описано, как добавить веб-API в традиционное приложение ASP.NET Web Forms в ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="71925-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="71925-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="71925-106">Overview</span></span>

<span data-ttu-id="71925-107">Хотя веб-API ASP.NET упаковывается с помощью ASP.NET MVC, можно легко добавить веб-API в традиционное приложение ASP.NET Web Forms.</span><span class="sxs-lookup"><span data-stu-id="71925-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="71925-108">Для использования веб-API в приложении Web Forms необходимо выполнить два основных действия.</span><span class="sxs-lookup"><span data-stu-id="71925-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="71925-109">Добавьте контроллер веб-API, производный от класса **ApiController** .</span><span class="sxs-lookup"><span data-stu-id="71925-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="71925-110">Добавьте таблицу маршрутов в метод **\_запуска приложения** .</span><span class="sxs-lookup"><span data-stu-id="71925-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="71925-111">Создание проекта веб-форм</span><span class="sxs-lookup"><span data-stu-id="71925-111">Create a Web Forms Project</span></span>

<span data-ttu-id="71925-112">Запустите Visual Studio и выберите **создать проект** на **начальной** странице.</span><span class="sxs-lookup"><span data-stu-id="71925-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="71925-113">Либо в меню **файл** выберите **создать** , а затем — **проект**.</span><span class="sxs-lookup"><span data-stu-id="71925-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="71925-114">В области **шаблоны** выберите **Установленные шаблоны** и разверните узел  **C# визуального** элемента.</span><span class="sxs-lookup"><span data-stu-id="71925-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="71925-115">В **разделе C#визуальный** элемент выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="71925-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="71925-116">В списке шаблонов проектов выберите **ASP.NET Web Forms Application**.</span><span class="sxs-lookup"><span data-stu-id="71925-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="71925-117">Введите имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="71925-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="71925-118">Создание модели и контроллера</span><span class="sxs-lookup"><span data-stu-id="71925-118">Create the Model and Controller</span></span>

<span data-ttu-id="71925-119">В этом руководстве используются те же классы модели и контроллера, что и в [Начало работы](tutorial-your-first-web-api.md) руководстве.</span><span class="sxs-lookup"><span data-stu-id="71925-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="71925-120">Сначала добавьте класс Model.</span><span class="sxs-lookup"><span data-stu-id="71925-120">First, add a model class.</span></span> <span data-ttu-id="71925-121">В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите команду **Добавить класс**.</span><span class="sxs-lookup"><span data-stu-id="71925-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="71925-122">Назовите класс Product и добавьте следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="71925-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="71925-123">Затем добавьте в проект контроллер веб-API. *контроллер* — это объект, который обрабатывает HTTP-запросы к веб API.</span><span class="sxs-lookup"><span data-stu-id="71925-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="71925-124">В **обозревателе решений** щелкните проект правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="71925-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="71925-125">Выберите **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="71925-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="71925-126">В разделе **Установленные шаблоны**разверните **узел C# визуальный** элемент и выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="71925-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="71925-127">Затем в списке шаблонов выберите **класс контроллера веб-API**.</span><span class="sxs-lookup"><span data-stu-id="71925-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="71925-128">Присвойте контроллеру имя "Продуктсконтроллер" и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="71925-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="71925-129">Мастер **добавления нового элемента** создаст файл с именем ProductsController.cs.</span><span class="sxs-lookup"><span data-stu-id="71925-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="71925-130">Удалите методы, добавленные мастером, и добавьте следующие методы.</span><span class="sxs-lookup"><span data-stu-id="71925-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="71925-131">Дополнительные сведения о коде в этом контроллере см. в руководстве по [Начало работы](tutorial-your-first-web-api.md) .</span><span class="sxs-lookup"><span data-stu-id="71925-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="71925-132">Добавление сведений о маршрутизации</span><span class="sxs-lookup"><span data-stu-id="71925-132">Add Routing Information</span></span>

<span data-ttu-id="71925-133">Далее мы добавим маршрут URI, чтобы в контроллере были направляться URI формы &quot;/АПИ/Продуктс/&quot;.</span><span class="sxs-lookup"><span data-stu-id="71925-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="71925-134">В **Обозреватель решений**дважды щелкните Global. asax, чтобы открыть файл кода программной части Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="71925-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="71925-135">Добавьте следующую инструкцию **using** .</span><span class="sxs-lookup"><span data-stu-id="71925-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="71925-136">Затем добавьте следующий код в метод **\_запуска приложения** :</span><span class="sxs-lookup"><span data-stu-id="71925-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="71925-137">Дополнительные сведения о таблицах маршрутизации см. [в разделе Маршрутизация в веб-API ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="71925-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="71925-138">Добавление AJAX на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="71925-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="71925-139">Это все, что необходимо для создания веб-API, к которому могут обращаться клиенты.</span><span class="sxs-lookup"><span data-stu-id="71925-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="71925-140">Теперь добавим HTML-страницу, которая использует jQuery для вызова API.</span><span class="sxs-lookup"><span data-stu-id="71925-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="71925-141">Убедитесь, что эталонная страница (например, *site. master*) содержит `ContentPlaceHolder` с `ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="71925-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="71925-142">Откройте файл Default. aspx.</span><span class="sxs-lookup"><span data-stu-id="71925-142">Open the file Default.aspx.</span></span> <span data-ttu-id="71925-143">Замените стандартный текст в разделе основное содержимое, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="71925-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="71925-144">Затем добавьте ссылку на исходный файл jQuery в раздел `HeaderContent`:</span><span class="sxs-lookup"><span data-stu-id="71925-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="71925-145">Примечание. можно легко добавить ссылку на скрипт, перетащив файл из **Обозреватель решений** в окно редактора кода.</span><span class="sxs-lookup"><span data-stu-id="71925-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="71925-146">Под тегом скрипта jQuery добавьте следующий блок скрипта:</span><span class="sxs-lookup"><span data-stu-id="71925-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="71925-147">Когда документ загружается, этот скрипт делает запрос AJAX для &quot;API и продуктов&quot;.</span><span class="sxs-lookup"><span data-stu-id="71925-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="71925-148">Запрос возвращает список продуктов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="71925-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="71925-149">Сценарий добавляет сведения о продукте в таблицу HTML.</span><span class="sxs-lookup"><span data-stu-id="71925-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="71925-150">При запуске приложения оно должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="71925-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
