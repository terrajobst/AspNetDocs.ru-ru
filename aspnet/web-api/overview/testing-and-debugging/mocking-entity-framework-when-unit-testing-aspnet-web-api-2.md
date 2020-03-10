---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Имитация Entity Framework при модульном тестировании веб-API ASP.NET 2 | Документация Майкрософт
author: Rick-Anderson
description: В этом руководстве и приложении показано, как создавать модульные тесты для приложения Web API 2, которое использует Entity Framework. В нем показано, как изменить...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447090"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="d3a37-104">Имитация Entity Framework при модульном тестировании веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="d3a37-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="d3a37-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d3a37-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="d3a37-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="d3a37-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="d3a37-107">В этом руководстве и приложении показано, как создавать модульные тесты для приложения Web API 2, которое использует Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d3a37-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="d3a37-108">В нем показано, как изменить сформированный контроллер, чтобы включить передачу объекта контекста для тестирования и создать тестовые объекты, работающие с Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d3a37-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="d3a37-109">Общие сведения о модульном тестировании с помощью веб-API ASP.NET см. [в разделе модульное тестирование с помощью веб-API ASP.NET 2](unit-testing-with-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="d3a37-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="d3a37-110">В этом учебнике предполагается, что вы знакомы с основными концепциями веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d3a37-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="d3a37-111">Вводное руководство см. в разделе [Начало работы с веб-API ASP.NET 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="d3a37-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d3a37-112">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="d3a37-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="d3a37-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d3a37-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="d3a37-114">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="d3a37-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="d3a37-115">В этом разделе</span><span class="sxs-lookup"><span data-stu-id="d3a37-115">In this topic</span></span>

<span data-ttu-id="d3a37-116">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="d3a37-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="d3a37-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3a37-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="d3a37-118">Скачать код</span><span class="sxs-lookup"><span data-stu-id="d3a37-118">Download code</span></span>](#download)
- [<span data-ttu-id="d3a37-119">Создание приложения с помощью проекта модульного теста</span><span class="sxs-lookup"><span data-stu-id="d3a37-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="d3a37-120">Создание класса Model</span><span class="sxs-lookup"><span data-stu-id="d3a37-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="d3a37-121">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="d3a37-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="d3a37-122">Добавить внедрение зависимостей</span><span class="sxs-lookup"><span data-stu-id="d3a37-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="d3a37-123">Установка пакетов NuGet в тестовом проекте</span><span class="sxs-lookup"><span data-stu-id="d3a37-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="d3a37-124">Создать контекст теста</span><span class="sxs-lookup"><span data-stu-id="d3a37-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="d3a37-125">Создание тестов</span><span class="sxs-lookup"><span data-stu-id="d3a37-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="d3a37-126">Выполнение тестов</span><span class="sxs-lookup"><span data-stu-id="d3a37-126">Run tests</span></span>](#runtests)

<span data-ttu-id="d3a37-127">Если вы уже выполнили действия по [модульному тестированию с веб-API ASP.NET 2](unit-testing-with-aspnet-web-api.md), можно перейти к разделу [Добавление контроллера](#controller).</span><span class="sxs-lookup"><span data-stu-id="d3a37-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="d3a37-128">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3a37-128">Prerequisites</span></span>

<span data-ttu-id="d3a37-129">Visual Studio 2017 Community, Professional или Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="d3a37-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="d3a37-130">Скачать код</span><span class="sxs-lookup"><span data-stu-id="d3a37-130">Download code</span></span>

<span data-ttu-id="d3a37-131">Скачайте [завершенный проект](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span><span class="sxs-lookup"><span data-stu-id="d3a37-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="d3a37-132">Загружаемый проект включает код модульного теста для этого раздела и раздел [модульного тестирования веб-API ASP.NET 2](unit-testing-with-aspnet-web-api.md) .</span><span class="sxs-lookup"><span data-stu-id="d3a37-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="d3a37-133">Создание приложения с помощью проекта модульного теста</span><span class="sxs-lookup"><span data-stu-id="d3a37-133">Create application with unit test project</span></span>

<span data-ttu-id="d3a37-134">Вы можете создать проект модульного теста при создании приложения или добавить проект модульного теста в существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="d3a37-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="d3a37-135">В этом руководстве показано, как создать проект модульного теста при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="d3a37-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="d3a37-136">Создайте новое веб-приложение ASP.NET с именем **стореапп**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="d3a37-137">В окнах Новый проект ASP.NET выберите **пустой** шаблон и добавьте папки и основные ссылки для веб-API.</span><span class="sxs-lookup"><span data-stu-id="d3a37-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="d3a37-138">Выберите параметр **Добавить модульные тесты** .</span><span class="sxs-lookup"><span data-stu-id="d3a37-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="d3a37-139">Проект модульного теста автоматически называется **стореапп. Tests**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="d3a37-140">Это имя можно не заключить.</span><span class="sxs-lookup"><span data-stu-id="d3a37-140">You can keep this name.</span></span>

![Создание проекта модульного теста](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="d3a37-142">После создания приложения вы увидите, что он содержит два проекта — **стореапп** и **стореапп. Tests**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="d3a37-143">Создание класса Model</span><span class="sxs-lookup"><span data-stu-id="d3a37-143">Create the model class</span></span>

<span data-ttu-id="d3a37-144">В проекте Стореапп добавьте файл класса в папку **Models** с именем **Product.CS**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="d3a37-145">Замените содержимое файла на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="d3a37-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="d3a37-146">Создайте решение.</span><span class="sxs-lookup"><span data-stu-id="d3a37-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="d3a37-147">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="d3a37-147">Add the controller</span></span>

<span data-ttu-id="d3a37-148">Щелкните правой кнопкой мыши папку Controllers и выберите **Добавить** и создать шаблонный **элемент**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="d3a37-149">Выберите контроллер веб-API 2 с действиями с помощью Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d3a37-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![Добавить новый контроллер](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="d3a37-151">Задайте следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d3a37-151">Set the following values:</span></span>

- <span data-ttu-id="d3a37-152">Имя контроллера: **продуктконтроллер**</span><span class="sxs-lookup"><span data-stu-id="d3a37-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="d3a37-153">Класс модели: **Product**</span><span class="sxs-lookup"><span data-stu-id="d3a37-153">Model class: **Product**</span></span>
- <span data-ttu-id="d3a37-154">Класс контекста данных: [кнопка " **создать контекст данных** ", которая заполняет значения, показанные ниже]</span><span class="sxs-lookup"><span data-stu-id="d3a37-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![Указание контроллера](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="d3a37-156">Нажмите кнопку **Добавить** , чтобы создать контроллер с автоматически созданным кодом.</span><span class="sxs-lookup"><span data-stu-id="d3a37-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="d3a37-157">Код включает методы для создания, извлечения, обновления и удаления экземпляров класса Product.</span><span class="sxs-lookup"><span data-stu-id="d3a37-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="d3a37-158">В следующем коде показан метод добавления продукта.</span><span class="sxs-lookup"><span data-stu-id="d3a37-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="d3a37-159">Обратите внимание, что метод возвращает экземпляр **ихттпактионресулт**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="d3a37-160">Ихттпактионресулт — это одна из новых возможностей веб-API 2, которая упрощает разработку модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="d3a37-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="d3a37-161">В следующем разделе вы настроите созданный код, чтобы упростить передачу тестовых объектов на контроллер.</span><span class="sxs-lookup"><span data-stu-id="d3a37-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="d3a37-162">Добавить внедрение зависимостей</span><span class="sxs-lookup"><span data-stu-id="d3a37-162">Add dependency injection</span></span>

<span data-ttu-id="d3a37-163">В настоящее время класс Продуктконтроллер жестко закодирован для использования экземпляра класса Стореаппконтекст.</span><span class="sxs-lookup"><span data-stu-id="d3a37-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="d3a37-164">Шаблон, именуемый внедрением зависимостей, будет использоваться для изменения приложения и удаления этой жесткой зависимости.</span><span class="sxs-lookup"><span data-stu-id="d3a37-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="d3a37-165">Нарушая эту зависимость, можно передать макет объекта при тестировании.</span><span class="sxs-lookup"><span data-stu-id="d3a37-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="d3a37-166">Щелкните правой кнопкой мыши папку **Models** и добавьте новый интерфейс с именем **истореаппконтекст**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="d3a37-167">Замените код следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="d3a37-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="d3a37-168">Откройте файл StoreAppContext.cs и внесите следующие выделенные изменения.</span><span class="sxs-lookup"><span data-stu-id="d3a37-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="d3a37-169">Важно отметить следующие важные изменения.</span><span class="sxs-lookup"><span data-stu-id="d3a37-169">The important changes to note are:</span></span>

- <span data-ttu-id="d3a37-170">Класс Стореаппконтекст реализует интерфейс Истореаппконтекст</span><span class="sxs-lookup"><span data-stu-id="d3a37-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="d3a37-171">Реализован метод Маркасмодифиед</span><span class="sxs-lookup"><span data-stu-id="d3a37-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="d3a37-172">Откройте файл ProductController.cs.</span><span class="sxs-lookup"><span data-stu-id="d3a37-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="d3a37-173">Измените существующий код в соответствии с выделенным кодом.</span><span class="sxs-lookup"><span data-stu-id="d3a37-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="d3a37-174">Эти изменения нарушают зависимость от Стореаппконтекст и позволяют другим классам передавать другой объект для класса контекста.</span><span class="sxs-lookup"><span data-stu-id="d3a37-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="d3a37-175">Это изменение позволит передать контекст теста во время модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="d3a37-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="d3a37-176">Есть еще одно изменение, которое необходимо внести в Продуктконтроллер.</span><span class="sxs-lookup"><span data-stu-id="d3a37-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="d3a37-177">В методе **путпродукт** замените строку, которая задает состояние сущности, измененной с помощью вызова метода маркасмодифиед.</span><span class="sxs-lookup"><span data-stu-id="d3a37-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="d3a37-178">Создайте решение.</span><span class="sxs-lookup"><span data-stu-id="d3a37-178">Build the solution.</span></span>

<span data-ttu-id="d3a37-179">Теперь вы готовы к настройке тестового проекта.</span><span class="sxs-lookup"><span data-stu-id="d3a37-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="d3a37-180">Установка пакетов NuGet в тестовом проекте</span><span class="sxs-lookup"><span data-stu-id="d3a37-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="d3a37-181">Если для создания приложения используется пустой шаблон, проект модульного теста (Стореапп. Tests) не включает установленные пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3a37-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="d3a37-182">Другие шаблоны, например шаблон веб-API, включают некоторые пакеты NuGet в проект модульного теста.</span><span class="sxs-lookup"><span data-stu-id="d3a37-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="d3a37-183">Для работы с этим руководством необходимо включить в тестовый проект пакет Entity Framework и пакет Microsoft ASP.NET Web API 2 Core.</span><span class="sxs-lookup"><span data-stu-id="d3a37-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="d3a37-184">Щелкните правой кнопкой мыши проект Стореапп. Tests и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="d3a37-185">Чтобы добавить пакеты в проект, необходимо выбрать проект Стореапп. Tests.</span><span class="sxs-lookup"><span data-stu-id="d3a37-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![Управление пакетами](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="d3a37-187">В веб-пакетах найдите и установите пакет EntityFramework (версии 6,0 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="d3a37-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="d3a37-188">Если кажется, что пакет EntityFramework уже установлен, возможно, вместо проекта Стореапп. Tests был выбран проект Стореапп.</span><span class="sxs-lookup"><span data-stu-id="d3a37-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![добавить Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="d3a37-190">Найдите и установите Microsoft ASP.NET основной пакет веб-API 2.</span><span class="sxs-lookup"><span data-stu-id="d3a37-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![Установка основного пакета веб-API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="d3a37-192">Закройте окно Управление пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3a37-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="d3a37-193">Создать контекст теста</span><span class="sxs-lookup"><span data-stu-id="d3a37-193">Create test context</span></span>

<span data-ttu-id="d3a37-194">Добавьте класс с именем **тестдбсет** в тестовый проект.</span><span class="sxs-lookup"><span data-stu-id="d3a37-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="d3a37-195">Этот класс служит базовым классом для набора проверочных данных.</span><span class="sxs-lookup"><span data-stu-id="d3a37-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="d3a37-196">Замените код следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="d3a37-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="d3a37-197">Добавьте класс с именем **тестпродуктдбсет** в тестовый проект, содержащий следующий код.</span><span class="sxs-lookup"><span data-stu-id="d3a37-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="d3a37-198">Добавьте класс с именем **тестстореаппконтекст** и замените существующий код следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="d3a37-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="d3a37-199">Создание тестов</span><span class="sxs-lookup"><span data-stu-id="d3a37-199">Create tests</span></span>

<span data-ttu-id="d3a37-200">По умолчанию тестовый проект содержит пустой тестовый файл с именем **UnitTest1.CS**.</span><span class="sxs-lookup"><span data-stu-id="d3a37-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="d3a37-201">В этом файле показаны атрибуты, используемые для создания методов теста.</span><span class="sxs-lookup"><span data-stu-id="d3a37-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="d3a37-202">В этом руководстве вы можете удалить этот файл, так как вы добавите новый тестовый класс.</span><span class="sxs-lookup"><span data-stu-id="d3a37-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="d3a37-203">Добавьте класс с именем **тестпродуктконтроллер** в тестовый проект.</span><span class="sxs-lookup"><span data-stu-id="d3a37-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="d3a37-204">Замените код следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="d3a37-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="d3a37-205">Выполнение тестов</span><span class="sxs-lookup"><span data-stu-id="d3a37-205">Run tests</span></span>

<span data-ttu-id="d3a37-206">Теперь все готово для выполнения тестов.</span><span class="sxs-lookup"><span data-stu-id="d3a37-206">You are now ready to run the tests.</span></span> <span data-ttu-id="d3a37-207">Будет протестирован весь метод, помеченный атрибутом **TestMethod** .</span><span class="sxs-lookup"><span data-stu-id="d3a37-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="d3a37-208">В пункте меню **тест** выполните тесты.</span><span class="sxs-lookup"><span data-stu-id="d3a37-208">From the **Test** menu item, run the tests.</span></span>

![Запуск тестов](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="d3a37-210">Откройте окно **обозревателя тестов** и обратите внимание на результаты тестов.</span><span class="sxs-lookup"><span data-stu-id="d3a37-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![результаты теста](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
