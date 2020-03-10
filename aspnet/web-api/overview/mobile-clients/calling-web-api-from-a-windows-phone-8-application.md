---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Вызов веб-API из приложения Windows Phone 8 (C#) — ASP.NET 4. x
author: rmcmurray
description: Руководство с кодом. Создайте веб-API ASP.NETное приложение в ASP.NET 4. x, которое предоставляет каталог книг для приложения Windows Phone 8.
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498216"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="0a33a-103">Вызов веб-API из приложения Windows Phone 8 (C#)</span><span class="sxs-lookup"><span data-stu-id="0a33a-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>

<span data-ttu-id="0a33a-104">[Роберт мкмуррай](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="0a33a-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="0a33a-105">В этом учебнике вы узнаете, как создать комплексный сценарий, состоящий из веб-API ASP.NET приложения, которое предоставляет каталог книг для приложения Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="0a33a-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="0a33a-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="0a33a-106">Overview</span></span>

<span data-ttu-id="0a33a-107">Службы RESTFUL, такие как веб-API ASP.NET упрощают создание приложений на основе HTTP для разработчиков путем абстракции архитектуры для приложений на стороне сервера и на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="0a33a-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="0a33a-108">Вместо создания собственного протокола на основе сокетов для обмена данными разработчики веб-API просто должны опубликовать необходимые методы HTTP для своего приложения (например, GET, POST, WHERE, DELETE) и разработчикам клиентских приложений требуется только использовать методы HTTP, необходимые для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="0a33a-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="0a33a-109">В этом комплексном руководстве вы узнаете, как использовать веб-API для создания следующих проектов:</span><span class="sxs-lookup"><span data-stu-id="0a33a-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="0a33a-110">В [первой части этого руководства](#STEP1)вы создадите веб-API ASP.NET приложение, которое поддерживает все операции создания, чтения, обновления и удаления (CRUD) для управления каталогом книг.</span><span class="sxs-lookup"><span data-stu-id="0a33a-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="0a33a-111">Это приложение будет использовать [Образец XML-файла (Books. XML)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) из MSDN.</span><span class="sxs-lookup"><span data-stu-id="0a33a-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="0a33a-112">Во [второй части этого руководства](#STEP2)вы создадите интерактивное приложение Windows Phone 8, которое получает данные из приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="0a33a-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="0a33a-113">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0a33a-113">Prerequisites</span></span>

- <span data-ttu-id="0a33a-114">Visual Studio 2013 с установленным пакетом SDK для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="0a33a-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="0a33a-115">Windows 8 или более поздняя версия в 64-разрядной системе с установленным Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0a33a-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="0a33a-116">Список дополнительных требований см. в разделе *требования к системе* на странице скачивания [Windows Phone SDK 8,0](https://www.microsoft.com/download/details.aspx?id=35471) .</span><span class="sxs-lookup"><span data-stu-id="0a33a-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="0a33a-117">Если вы собираетесь проверить подключение между веб-API и Windows Phone 8 проектами в локальной системе, необходимо выполнить инструкции из статьи *[Подключение эмулятора Windows Phone 8 к приложениям веб-API на локальном компьютере](https://go.microsoft.com/fwlink/?LinkId=324014)* , чтобы настроить среду тестирования.</span><span class="sxs-lookup"><span data-stu-id="0a33a-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="0a33a-118">Шаг 1. Создание проекта веб-API в книжном магазине</span><span class="sxs-lookup"><span data-stu-id="0a33a-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="0a33a-119">Первым этапом этого комплексного руководства является создание проекта веб-API, поддерживающего все операции CRUD. Обратите внимание, что вы добавите проект Windows Phone приложения в это решение на [шаге 2](#STEP2) этого руководства.</span><span class="sxs-lookup"><span data-stu-id="0a33a-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="0a33a-120">Откройте **Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="0a33a-121">Последовательно выберите пункты **файл**, **создать**и **проект**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="0a33a-122">Когда откроется диалоговое окно **Новый проект** , разверните узел **установленные**, затем **шаблоны**, **визуальный C#** элемент и **веб-узел**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="0a33a-123">Щелкните изображение, чтобы развернуть</span><span class="sxs-lookup"><span data-stu-id="0a33a-123">Click image to expand</span></span>                                                                |

4. <span data-ttu-id="0a33a-124">Выделите **веб-приложение ASP.NET**, введите **Bookstore** в поле имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="0a33a-125">Когда откроется диалоговое окно **Новый проект ASP.NET** , выберите шаблон **веб-API** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="0a33a-126">Щелкните изображение, чтобы развернуть</span><span class="sxs-lookup"><span data-stu-id="0a33a-126">Click image to expand</span></span>                                                                |

6. <span data-ttu-id="0a33a-127">После открытия проекта веб-API удалите пример контроллера из проекта:</span><span class="sxs-lookup"><span data-stu-id="0a33a-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="0a33a-128">Разверните папку **контроллеры** в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="0a33a-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="0a33a-129">Щелкните правой кнопкой мыши файл **ValuesController.CS** и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="0a33a-130">При появлении запроса на подтверждение удаления нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="0a33a-131">Добавьте файл данных XML в проект веб-API. Этот файл содержит содержимое каталога книжного магазина:</span><span class="sxs-lookup"><span data-stu-id="0a33a-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="0a33a-132">Щелкните правой кнопкой мыши папку **данных приложения\_** в обозревателе решений, выберите пункт **Добавить**, а затем щелкните **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="0a33a-133">При отображении диалогового окна **Добавление нового элемента** выделите шаблон **XML-файла** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="0a33a-134">Присвойте файлу имя **Books. XML**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="0a33a-135">При открытии файла **Books. XML** замените код в файле XML-кодом из образца файла **Books. XML** на сайте MSDN:</span><span class="sxs-lookup"><span data-stu-id="0a33a-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="0a33a-136">Сохраните и закройте XML-файл.</span><span class="sxs-lookup"><span data-stu-id="0a33a-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="0a33a-137">Добавьте модель книжного магазина в проект веб-API. Эта модель содержит логику создания, чтения, обновления и удаления (CRUD) для приложения Bookstore:</span><span class="sxs-lookup"><span data-stu-id="0a33a-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="0a33a-138">Щелкните правой кнопкой мыши папку **модели** в обозревателе решений, выберите **Добавить**, а затем — **класс**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="0a33a-139">Когда откроется диалоговое окно **Добавление нового элемента** , назовите файл класса **BookDetails.CS**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="0a33a-140">При открытии файла **BookDetails.CS** замените код в файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="0a33a-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="0a33a-141">Сохраните и закройте файл **BookDetails.CS** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="0a33a-142">Добавьте контроллер Bookstore в проект веб-API:</span><span class="sxs-lookup"><span data-stu-id="0a33a-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="0a33a-143">Щелкните правой кнопкой мыши папку **Controllers** в обозревателе решений, выберите **Добавить**, а затем щелкните **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="0a33a-144">Когда откроется диалоговое окно **Добавление шаблона** , выделите **контроллер Web API 2 — пустой**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="0a33a-145">Когда откроется диалоговое окно **Добавление контроллера** , назовите контроллер **буксконтроллер**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="0a33a-146">При открытии файла **BooksController.CS** замените код в файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="0a33a-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="0a33a-147">Сохраните и закройте файл **BooksController.CS** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="0a33a-148">Создайте приложение веб-API для проверки на наличие ошибок.</span><span class="sxs-lookup"><span data-stu-id="0a33a-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="0a33a-149">Шаг 2. Добавление проекта каталога Windows Phone 8 в книжном магазине</span><span class="sxs-lookup"><span data-stu-id="0a33a-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="0a33a-150">Следующим этапом этого сквозного сценария является создание приложения каталога для Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="0a33a-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="0a33a-151">Это приложение будет использовать шаблон *приложения Windows Phone с привязкой* к данным для пользовательского интерфейса по умолчанию и будет использовать приложение веб-API, созданное на [шаге 1](#STEP1) этого учебника в качестве источника данных.</span><span class="sxs-lookup"><span data-stu-id="0a33a-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="0a33a-152">Щелкните правой кнопкой мыши решение **Bookstore** в в обозревателе решений, затем щелкните **Добавить**, а затем — **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="0a33a-153">Когда откроется диалоговое окно **Создание проекта** , разверните узел **установленные**, а **затем C#Visual** и затем **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="0a33a-154">Выделите **Windows Phone приложение с привязкой к данным**, введите **буккаталог** в поле имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="0a33a-155">Добавьте пакет NuGet Json.NET в проект **буккаталог** :</span><span class="sxs-lookup"><span data-stu-id="0a33a-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="0a33a-156">Щелкните правой кнопкой мыши **ссылки** на проект **буккаталог** в обозревателе решений и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="0a33a-157">Когда откроется диалоговое окно **Управление пакетами NuGet** , разверните раздел **Online** и выделите **NuGet.org**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="0a33a-158">Введите **JSON.NET** в поле поиска и щелкните значок поиска.</span><span class="sxs-lookup"><span data-stu-id="0a33a-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="0a33a-159">Выделите **JSON.NET** в результатах поиска и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="0a33a-160">После завершения установки нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="0a33a-161">Добавьте модель **букдетаилс** в проект **буккаталог** . Он содержит универсальную модель класса Bookstore:</span><span class="sxs-lookup"><span data-stu-id="0a33a-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="0a33a-162">Щелкните правой кнопкой мыши проект **буккаталог** в обозревателе решений, нажмите кнопку **Добавить**, а затем выберите пункт **создать папку**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="0a33a-163">Назовите новые **модели**папок.</span><span class="sxs-lookup"><span data-stu-id="0a33a-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="0a33a-164">Щелкните правой кнопкой мыши папку **модели** в обозревателе решений, выберите **Добавить**, а затем — **класс**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="0a33a-165">Когда откроется диалоговое окно **Добавление нового элемента** , назовите файл класса **BookDetails.CS**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="0a33a-166">При открытии файла **BookDetails.CS** замените код в файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="0a33a-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="0a33a-167">Сохраните и закройте файл **BookDetails.CS** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="0a33a-168">Обновите класс **MainViewModel.CS** , чтобы включить функции для взаимодействия с приложением веб-API книжного магазина:</span><span class="sxs-lookup"><span data-stu-id="0a33a-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="0a33a-169">Разверните папку **ViewModels** в обозревателе решений, а затем дважды щелкните файл **MainViewModel.CS** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="0a33a-170">При открытии файла **MainViewModel.CS** замените код в файле следующим кодом. Обратите внимание, что необходимо обновить значение `apiUrl`ной константы с помощью фактического URL-адреса вашего Web API:</span><span class="sxs-lookup"><span data-stu-id="0a33a-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="0a33a-171">Сохраните и закройте файл **MainViewModel.CS** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="0a33a-172">Обновите файл **MainPage. XAML** , чтобы настроить имя приложения:</span><span class="sxs-lookup"><span data-stu-id="0a33a-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="0a33a-173">Дважды щелкните файл **MainPage. XAML** в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="0a33a-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="0a33a-174">При открытии файла **MainPage. XAML** нахождение следующих строк кода:</span><span class="sxs-lookup"><span data-stu-id="0a33a-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="0a33a-175">Замените эти строки следующим:</span><span class="sxs-lookup"><span data-stu-id="0a33a-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="0a33a-176">Сохраните и закройте файл **MainPage. XAML** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="0a33a-177">Обновите файл **детаилспаже. XAML** , чтобы настроить отображаемые элементы:</span><span class="sxs-lookup"><span data-stu-id="0a33a-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="0a33a-178">Дважды щелкните файл **детаилспаже. XAML** в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="0a33a-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="0a33a-179">При открытии файла **детаилспаже. XAML** нахождение следующих строк кода:</span><span class="sxs-lookup"><span data-stu-id="0a33a-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="0a33a-180">Замените эти строки следующим:</span><span class="sxs-lookup"><span data-stu-id="0a33a-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="0a33a-181">Сохраните и закройте файл **детаилспаже. XAML** .</span><span class="sxs-lookup"><span data-stu-id="0a33a-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="0a33a-182">Создайте приложение Windows Phone для проверки на наличие ошибок.</span><span class="sxs-lookup"><span data-stu-id="0a33a-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="0a33a-183">Шаг 3. Тестирование комплексного решения</span><span class="sxs-lookup"><span data-stu-id="0a33a-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="0a33a-184">Как упоминалось в разделе " *Предварительные требования* " этого руководства, при тестировании подключения между проектами веб-api и Windows Phone 8 в локальной системе необходимо выполнить инструкции из статьи *[подключение эмулятора Windows Phone 8 к ПРИЛОЖЕНИЯМ веб-API на локальном компьютере](https://go.microsoft.com/fwlink/?LinkId=324014)* , чтобы настроить среду тестирования.</span><span class="sxs-lookup"><span data-stu-id="0a33a-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="0a33a-185">После настройки тестовой среды необходимо задать приложение Windows Phone в качестве запускаемого проекта.</span><span class="sxs-lookup"><span data-stu-id="0a33a-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="0a33a-186">Для этого выделите приложение **буккаталог** в обозревателе решений и нажмите кнопку **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="0a33a-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="0a33a-187">Щелкните изображение, чтобы развернуть</span><span class="sxs-lookup"><span data-stu-id="0a33a-187">Click image to expand</span></span> |

<span data-ttu-id="0a33a-188">При нажатии клавиши F5 Visual Studio запустит эмулятор Windows Phone, в котором будет отображаться &quot;подождите&quot; сообщение, пока данные приложения будут получены из веб-API:</span><span class="sxs-lookup"><span data-stu-id="0a33a-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="0a33a-189">Щелкните изображение, чтобы развернуть</span><span class="sxs-lookup"><span data-stu-id="0a33a-189">Click image to expand</span></span> |

<span data-ttu-id="0a33a-190">Если все прошло успешно, должен отобразиться каталог:</span><span class="sxs-lookup"><span data-stu-id="0a33a-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="0a33a-191">Щелкните изображение, чтобы развернуть</span><span class="sxs-lookup"><span data-stu-id="0a33a-191">Click image to expand</span></span> |

<span data-ttu-id="0a33a-192">Если коснуться любого названия книги, в приложении отобразится описание книги:</span><span class="sxs-lookup"><span data-stu-id="0a33a-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="0a33a-193">Щелкните изображение, чтобы развернуть</span><span class="sxs-lookup"><span data-stu-id="0a33a-193">Click image to expand</span></span> |

<span data-ttu-id="0a33a-194">Если приложение не может взаимодействовать с веб-API, отобразится сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="0a33a-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="0a33a-195">Щелкните изображение, чтобы развернуть</span><span class="sxs-lookup"><span data-stu-id="0a33a-195">Click image to expand</span></span> |

<span data-ttu-id="0a33a-196">Если коснуться сообщения об ошибке, будут отображаться дополнительные сведения об ошибке:</span><span class="sxs-lookup"><span data-stu-id="0a33a-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="0a33a-197">Щелкните изображение, чтобы развернуть</span><span class="sxs-lookup"><span data-stu-id="0a33a-197">Click image to expand</span></span>                                                                 |
