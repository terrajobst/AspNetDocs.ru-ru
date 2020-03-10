---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: Часть 1. Обзор и создание проекта | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447936"
---
# <a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="2dce1-102">Часть 1. Обзор и создание проекта</span><span class="sxs-lookup"><span data-stu-id="2dce1-102">Part 1: Overview and Creating the Project</span></span>

<span data-ttu-id="2dce1-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2dce1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="2dce1-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="2dce1-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="2dce1-105">Entity Framework — это платформа объектно-реляционного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="2dce1-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="2dce1-106">Он сопоставляет объекты домена в коде с сущностями в реляционной базе данных.</span><span class="sxs-lookup"><span data-stu-id="2dce1-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="2dce1-107">В большинстве случаев вам не нужно беспокоиться о уровне базы данных, так как Entity Framework подбирается за вас.</span><span class="sxs-lookup"><span data-stu-id="2dce1-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="2dce1-108">Код манипулирует объектами, и изменения сохраняются в базе данных.</span><span class="sxs-lookup"><span data-stu-id="2dce1-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="2dce1-109">О учебнике</span><span class="sxs-lookup"><span data-stu-id="2dce1-109">About the Tutorial</span></span>

<span data-ttu-id="2dce1-110">В этом руководстве вы создадите простое приложение Store.</span><span class="sxs-lookup"><span data-stu-id="2dce1-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="2dce1-111">Приложение состоит из двух основных частей.</span><span class="sxs-lookup"><span data-stu-id="2dce1-111">There are two main parts to the application.</span></span> <span data-ttu-id="2dce1-112">Обычные пользователи могут просматривать продукты и создавать заказы:</span><span class="sxs-lookup"><span data-stu-id="2dce1-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="2dce1-113">Администраторы могут создавать, удалять и изменять продукты:</span><span class="sxs-lookup"><span data-stu-id="2dce1-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="2dce1-114">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="2dce1-114">Skills You'll Learn</span></span>

<span data-ttu-id="2dce1-115">В этом учебнике вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="2dce1-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="2dce1-116">Использование Entity Framework с веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2dce1-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="2dce1-117">Использование маскирования. js для создания динамического пользовательского интерфейса клиента.</span><span class="sxs-lookup"><span data-stu-id="2dce1-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="2dce1-118">Использование проверки подлинности с помощью форм с веб-API для проверки подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="2dce1-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="2dce1-119">Хотя это руководство является автономным, вы можете сначала ознакомиться со следующими учебниками:</span><span class="sxs-lookup"><span data-stu-id="2dce1-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="2dce1-120">Первое приложение веб-интерфейса API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2dce1-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="2dce1-121">Создание веб-API, поддерживающего операции CRUD</span><span class="sxs-lookup"><span data-stu-id="2dce1-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="2dce1-122">Некоторые знания о [ASP.NET MVC](../../../../mvc/index.md) также полезны.</span><span class="sxs-lookup"><span data-stu-id="2dce1-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="2dce1-123">Обзор</span><span class="sxs-lookup"><span data-stu-id="2dce1-123">Overview</span></span>

<span data-ttu-id="2dce1-124">На высоком уровне ниже приведена архитектура приложения.</span><span class="sxs-lookup"><span data-stu-id="2dce1-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="2dce1-125">ASP.NET MVC создает HTML-страницы для клиента.</span><span class="sxs-lookup"><span data-stu-id="2dce1-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="2dce1-126">Веб-API ASP.NET предоставляет операции CRUD с данными (продукты и заказы).</span><span class="sxs-lookup"><span data-stu-id="2dce1-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="2dce1-127">Entity Framework преобразует C# модели, используемые веб-API, в сущности базы данных.</span><span class="sxs-lookup"><span data-stu-id="2dce1-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="2dce1-128">На следующей схеме показано, как объекты предметной области представлены на различных уровнях приложения: уровень базы данных, объектная модель и, наконец, формат подключения, который используется для передачи данных клиенту по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="2dce1-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="2dce1-129">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2dce1-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="2dce1-130">Проект Tutorial можно создать с помощью Visual Web Developer Express или полной версии Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2dce1-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="2dce1-131">На **начальной** странице нажмите кнопку **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="2dce1-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="2dce1-132">В области **шаблоны** выберите **Установленные шаблоны** и разверните узел  **C# визуального** элемента.</span><span class="sxs-lookup"><span data-stu-id="2dce1-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="2dce1-133">В **разделе C#визуальный** элемент выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="2dce1-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="2dce1-134">В списке шаблонов проектов выберите **ASP.NET MVC 4 веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="2dce1-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="2dce1-135">Присвойте проекту имя "Продуктсторе" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2dce1-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="2dce1-136">В диалоговом окне **Новый проект ASP.NET MVC 4** выберите **Интернет приложение** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2dce1-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="2dce1-137">Шаблон "Интернет приложение" создает приложение ASP.NET MVC, которое поддерживает проверку подлинности с помощью форм.</span><span class="sxs-lookup"><span data-stu-id="2dce1-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="2dce1-138">Если запустить приложение сейчас, у него уже есть некоторые функции:</span><span class="sxs-lookup"><span data-stu-id="2dce1-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="2dce1-139">Новые пользователи могут зарегистрироваться, щелкнув ссылку "регистрация" в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="2dce1-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="2dce1-140">Зарегистрированные пользователи могут войти, щелкнув ссылку "вход".</span><span class="sxs-lookup"><span data-stu-id="2dce1-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="2dce1-141">Сведения о членстве сохраняются в базе данных, которая создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="2dce1-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="2dce1-142">Дополнительные сведения о проверке подлинности в ASP.NET MVC см. в разделе [Пошаговое руководство. Использование проверки подлинности с помощью форм в ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span><span class="sxs-lookup"><span data-stu-id="2dce1-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="2dce1-143">Обновить CSS файл</span><span class="sxs-lookup"><span data-stu-id="2dce1-143">Update the CSS File</span></span>

<span data-ttu-id="2dce1-144">Этот шаг является косметическим, но при этом страницы отображаются как предыдущие снимки экрана.</span><span class="sxs-lookup"><span data-stu-id="2dce1-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="2dce1-145">В обозреватель решений разверните папку содержимое и откройте файл с именем site. CSS.</span><span class="sxs-lookup"><span data-stu-id="2dce1-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="2dce1-146">Добавьте следующие стили CSS:</span><span class="sxs-lookup"><span data-stu-id="2dce1-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="2dce1-147">Дальше</span><span class="sxs-lookup"><span data-stu-id="2dce1-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
