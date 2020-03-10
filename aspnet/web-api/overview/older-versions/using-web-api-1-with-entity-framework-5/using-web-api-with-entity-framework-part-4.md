---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: Часть 4. Добавление административного представления | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447882"
---
# <a name="part-4-adding-an-admin-view"></a><span data-ttu-id="02272-102">Часть 4. Добавление административного представления</span><span class="sxs-lookup"><span data-stu-id="02272-102">Part 4: Adding an Admin View</span></span>

<span data-ttu-id="02272-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="02272-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="02272-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="02272-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="02272-105">Добавление представления администратора</span><span class="sxs-lookup"><span data-stu-id="02272-105">Add an Admin View</span></span>

<span data-ttu-id="02272-106">Теперь мы вернемся к клиентской стороне и добавим страницу, которая может использовать данные из административного контроллера.</span><span class="sxs-lookup"><span data-stu-id="02272-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="02272-107">Страница позволяет пользователям создавать, изменять и удалять продукты, отправляя запросы AJAX к контроллеру.</span><span class="sxs-lookup"><span data-stu-id="02272-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="02272-108">В обозреватель решений разверните папку Controllers и откройте файл с именем HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="02272-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="02272-109">Этот файл содержит контроллер MVC.</span><span class="sxs-lookup"><span data-stu-id="02272-109">This file contains an MVC controller.</span></span> <span data-ttu-id="02272-110">Добавьте метод с именем `Admin`:</span><span class="sxs-lookup"><span data-stu-id="02272-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="02272-111">Метод **хттпраутеурл** создает универсальный код ресурса (URI) для веб-API и сохраняет его в контейнере представления для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="02272-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="02272-112">Затем поместите текстовый курсор в метод действия `Admin`, щелкните его правой кнопкой мыши и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="02272-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="02272-113">Откроется диалоговое окно **Добавление представления** .</span><span class="sxs-lookup"><span data-stu-id="02272-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="02272-114">В диалоговом окне **Добавление представления** назовите представление "admin".</span><span class="sxs-lookup"><span data-stu-id="02272-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="02272-115">Установите флажок **создать строго типизированное представление**.</span><span class="sxs-lookup"><span data-stu-id="02272-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="02272-116">В разделе **класс модели**выберите "продукт (Продуктсторе. Models)".</span><span class="sxs-lookup"><span data-stu-id="02272-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="02272-117">Оставьте все остальные параметры в качестве значений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="02272-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="02272-118">При нажатии кнопки **Добавить** добавляется файл admin. cshtml в области Views/Home.</span><span class="sxs-lookup"><span data-stu-id="02272-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="02272-119">Откройте этот файл и добавьте следующий код HTML.</span><span class="sxs-lookup"><span data-stu-id="02272-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="02272-120">Этот HTML определяет структуру страницы, но функции еще не привязаны.</span><span class="sxs-lookup"><span data-stu-id="02272-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="02272-121">Создание ссылки на страницу администрирования</span><span class="sxs-lookup"><span data-stu-id="02272-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="02272-122">В обозреватель решений разверните папку представления, а затем — общую папку.</span><span class="sxs-lookup"><span data-stu-id="02272-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="02272-123">Откройте файл с именем \_Layout. cshtml.</span><span class="sxs-lookup"><span data-stu-id="02272-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="02272-124">Поиск элемента **UL** с ID = "Menu" и ссылки на действие для представления администрирования:</span><span class="sxs-lookup"><span data-stu-id="02272-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="02272-125">В примере проекта я сделал несколько других косметических изменений, например заменить строку "Ваша Эмблема здесь".</span><span class="sxs-lookup"><span data-stu-id="02272-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="02272-126">Они не влияют на функциональность приложения.</span><span class="sxs-lookup"><span data-stu-id="02272-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="02272-127">Вы можете скачать проект и сравнить файлы.</span><span class="sxs-lookup"><span data-stu-id="02272-127">You can download the project and compare the files.</span></span>

<span data-ttu-id="02272-128">Запустите приложение и щелкните ссылку Admin (администратор), которая отображается в верхней части домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="02272-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="02272-129">Страница администрирования должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="02272-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="02272-130">Прямо сейчас страница не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="02272-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="02272-131">В следующем разделе мы будем использовать выколачивание. js для создания динамического пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="02272-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="02272-132">Добавить авторизацию</span><span class="sxs-lookup"><span data-stu-id="02272-132">Add Authorization</span></span>

<span data-ttu-id="02272-133">Страница администрирования в настоящее время доступна для всех, кто посещает сайт.</span><span class="sxs-lookup"><span data-stu-id="02272-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="02272-134">Изменим это значение, чтобы ограничить разрешения администраторам.</span><span class="sxs-lookup"><span data-stu-id="02272-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="02272-135">Для начала добавьте роль "Администратор" и пользователя с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="02272-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="02272-136">В обозреватель решений разверните папку фильтры и откройте файл с именем InitializeSimpleMembershipAttribute.cs.</span><span class="sxs-lookup"><span data-stu-id="02272-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="02272-137">Нахождение конструктора `SimpleMembershipInitializer`.</span><span class="sxs-lookup"><span data-stu-id="02272-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="02272-138">После вызова **инитиализедатабасеконнектион.** добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="02272-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="02272-139">Это быстрый и недействительный способ добавить роль "Администратор" и создать пользователя для роли.</span><span class="sxs-lookup"><span data-stu-id="02272-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="02272-140">В обозреватель решений разверните папку Controllers и откройте файл HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="02272-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="02272-141">Добавьте атрибут **авторизовать** в метод `Admin`.</span><span class="sxs-lookup"><span data-stu-id="02272-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="02272-142">Откройте файл AdminController.cs и добавьте атрибут **авторизовать** во весь класс `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="02272-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="02272-143">MVC и веб-API определяют атрибуты **авторизации** в разных пространствах имен.</span><span class="sxs-lookup"><span data-stu-id="02272-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="02272-144">MVC использует **System. Web. MVC. AuthorizeAttribute**, а веб-API использует **System. Web. http. AuthorizeAttribute**.</span><span class="sxs-lookup"><span data-stu-id="02272-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>

<span data-ttu-id="02272-145">Теперь только администраторы могут просматривать страницу Администратор.</span><span class="sxs-lookup"><span data-stu-id="02272-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="02272-146">Кроме того, при отправке HTTP-запроса на административный контроллер запрос должен содержать файл cookie проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="02272-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="02272-147">В противном случае сервер отправляет ответ HTTP 401 (несанкционированный).</span><span class="sxs-lookup"><span data-stu-id="02272-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="02272-148">Это можно увидеть в Fiddler, отправив запрос GET в `http://localhost:*port*/api/admin`.</span><span class="sxs-lookup"><span data-stu-id="02272-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="02272-149">[Назад](using-web-api-with-entity-framework-part-3.md)
> [Вперед](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="02272-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
