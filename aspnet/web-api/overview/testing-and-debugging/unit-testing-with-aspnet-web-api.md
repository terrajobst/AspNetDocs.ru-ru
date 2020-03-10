---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: Модульное тестирование веб-API ASP.NET 2 | Документация Майкрософт
author: Rick-Anderson
description: В этом руководстве и приложении показано, как создавать простые модульные тесты для приложения веб-API 2. В этом учебнике показано, как включить proj модульного теста...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446988"
---
# <a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="07ed9-104">Модульное тестирование веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="07ed9-104">Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="07ed9-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="07ed9-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="07ed9-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="07ed9-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="07ed9-107">В этом руководстве и приложении показано, как создавать простые модульные тесты для приложения веб-API 2.</span><span class="sxs-lookup"><span data-stu-id="07ed9-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="07ed9-108">В этом руководстве показано, как включить проект модульного теста в решение и написать методы теста, которые проверяют возвращенные значения из метода контроллера.</span><span class="sxs-lookup"><span data-stu-id="07ed9-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
>
> <span data-ttu-id="07ed9-109">В этом учебнике предполагается, что вы знакомы с основными концепциями веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="07ed9-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="07ed9-110">Вводное руководство см. в разделе [Начало работы с веб-API ASP.NET 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="07ed9-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> <span data-ttu-id="07ed9-111">Модульные тесты в этом разделе намеренно ограничены простыми сценариями данных.</span><span class="sxs-lookup"><span data-stu-id="07ed9-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="07ed9-112">Дополнительные сведения о модульном тестировании для расширенных сценариев данных см. в разделе [макет Entity Framework при модульном тестировании веб-API ASP.NET 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="07ed9-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="07ed9-113">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="07ed9-113">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="07ed9-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="07ed9-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="07ed9-115">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="07ed9-115">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="07ed9-116">В этом разделе</span><span class="sxs-lookup"><span data-stu-id="07ed9-116">In this topic</span></span>

<span data-ttu-id="07ed9-117">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="07ed9-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="07ed9-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="07ed9-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="07ed9-119">Скачать код</span><span class="sxs-lookup"><span data-stu-id="07ed9-119">Download code</span></span>](#download)
- [<span data-ttu-id="07ed9-120">Создание приложения с помощью проекта модульного теста</span><span class="sxs-lookup"><span data-stu-id="07ed9-120">Create application with unit test project</span></span>](#appwithunittest)
    - [<span data-ttu-id="07ed9-121">Добавить проект модульного теста при создании приложения</span><span class="sxs-lookup"><span data-stu-id="07ed9-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="07ed9-122">Добавление проекта модульного теста в существующее приложение</span><span class="sxs-lookup"><span data-stu-id="07ed9-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="07ed9-123">Настройка приложения веб-API 2</span><span class="sxs-lookup"><span data-stu-id="07ed9-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="07ed9-124">Установка пакетов NuGet в тестовом проекте</span><span class="sxs-lookup"><span data-stu-id="07ed9-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="07ed9-125">Создание тестов</span><span class="sxs-lookup"><span data-stu-id="07ed9-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="07ed9-126">Выполнение тестов</span><span class="sxs-lookup"><span data-stu-id="07ed9-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="07ed9-127">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="07ed9-127">Prerequisites</span></span>

<span data-ttu-id="07ed9-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional или Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="07ed9-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="07ed9-129">Скачать код</span><span class="sxs-lookup"><span data-stu-id="07ed9-129">Download code</span></span>

<span data-ttu-id="07ed9-130">Скачайте [завершенный проект](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span><span class="sxs-lookup"><span data-stu-id="07ed9-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="07ed9-131">Загружаемый проект включает код модульного теста для этого раздела и для [Entity Framework при модульном тестировании веб-API ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) разделе.</span><span class="sxs-lookup"><span data-stu-id="07ed9-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="07ed9-132">Создание приложения с помощью проекта модульного теста</span><span class="sxs-lookup"><span data-stu-id="07ed9-132">Create application with unit test project</span></span>

<span data-ttu-id="07ed9-133">Вы можете создать проект модульного теста при создании приложения или добавить проект модульного теста в существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="07ed9-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="07ed9-134">В этом учебнике показаны оба метода создания проекта модульного теста.</span><span class="sxs-lookup"><span data-stu-id="07ed9-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="07ed9-135">Для выполнения действий, описанных в этом руководстве, можно использовать любой из этих подходов.</span><span class="sxs-lookup"><span data-stu-id="07ed9-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="07ed9-136">Добавить проект модульного теста при создании приложения</span><span class="sxs-lookup"><span data-stu-id="07ed9-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="07ed9-137">Создайте новое веб-приложение ASP.NET с именем **стореапп**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![создание проекта](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="07ed9-139">В окнах Новый проект ASP.NET выберите **пустой** шаблон и добавьте папки и основные ссылки для веб-API.</span><span class="sxs-lookup"><span data-stu-id="07ed9-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="07ed9-140">Выберите параметр **Добавить модульные тесты** .</span><span class="sxs-lookup"><span data-stu-id="07ed9-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="07ed9-141">Проект модульного теста автоматически называется **стореапп. Tests**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="07ed9-142">Это имя можно не заключить.</span><span class="sxs-lookup"><span data-stu-id="07ed9-142">You can keep this name.</span></span>

![Создание проекта модульного теста](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="07ed9-144">После создания приложения вы увидите, что он содержит два проекта.</span><span class="sxs-lookup"><span data-stu-id="07ed9-144">After creating the application, you will see it contains two projects.</span></span>

![два проекта](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="07ed9-146">Добавление проекта модульного теста в существующее приложение</span><span class="sxs-lookup"><span data-stu-id="07ed9-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="07ed9-147">Если вы не создавали проект модульного теста при создании приложения, вы можете добавить его в любое время.</span><span class="sxs-lookup"><span data-stu-id="07ed9-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="07ed9-148">Например, предположим, что у вас уже есть приложение с именем Стореапп и вы хотите добавить модульные тесты.</span><span class="sxs-lookup"><span data-stu-id="07ed9-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="07ed9-149">Чтобы добавить проект модульного теста, щелкните решение правой кнопкой мыши и выберите **Добавить** и **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![Добавить новый проект в решение](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="07ed9-151">Выберите **тест** в левой области и выберите **проект модульного теста** для типа проекта.</span><span class="sxs-lookup"><span data-stu-id="07ed9-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="07ed9-152">Назовите проект **стореапп. Tests**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-152">Name the project **StoreApp.Tests**.</span></span>

![Добавить проект модульного теста](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="07ed9-154">Вы увидите проект модульного теста в решении.</span><span class="sxs-lookup"><span data-stu-id="07ed9-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="07ed9-155">В проекте модульного теста добавьте ссылку на проект в исходный проект.</span><span class="sxs-lookup"><span data-stu-id="07ed9-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="07ed9-156">Настройка приложения веб-API 2</span><span class="sxs-lookup"><span data-stu-id="07ed9-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="07ed9-157">В проекте Стореапп добавьте файл класса в папку **Models** с именем **Product.CS**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="07ed9-158">Замените содержимое файла на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="07ed9-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="07ed9-159">Создайте решение.</span><span class="sxs-lookup"><span data-stu-id="07ed9-159">Build the solution.</span></span>

<span data-ttu-id="07ed9-160">Щелкните правой кнопкой мыши папку Controllers и выберите **Добавить** и создать шаблонный **элемент**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="07ed9-161">Выберите **контроллер веб-API 2 — пустой**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-161">Select **Web API 2 Controller - Empty**.</span></span>

![Добавить новый контроллер](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="07ed9-163">Задайте имя контроллера **симплепродуктконтроллер**и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![Указание контроллера](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="07ed9-165">Замените существующий код следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="07ed9-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="07ed9-166">Чтобы упростить этот пример, данные хранятся в списке, а не в базе данных.</span><span class="sxs-lookup"><span data-stu-id="07ed9-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="07ed9-167">Список, определенный в этом классе, представляет рабочие данные.</span><span class="sxs-lookup"><span data-stu-id="07ed9-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="07ed9-168">Обратите внимание, что контроллер включает конструктор, который принимает в качестве параметра список объектов Product.</span><span class="sxs-lookup"><span data-stu-id="07ed9-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="07ed9-169">Этот конструктор позволяет передавать тестовые данные при модульном тестировании.</span><span class="sxs-lookup"><span data-stu-id="07ed9-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="07ed9-170">Контроллер также содержит два **асинхронных** метода для демонстрации асинхронных методов модульного тестирования.</span><span class="sxs-lookup"><span data-stu-id="07ed9-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="07ed9-171">Эти асинхронные методы были реализованы путем вызова **Task. FromResult** для сворачивания лишнего кода, но обычно методы будут включать ресурсоемкие операции.</span><span class="sxs-lookup"><span data-stu-id="07ed9-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="07ed9-172">Метод произведения возвращает экземпляр интерфейса **ихттпактионресулт** .</span><span class="sxs-lookup"><span data-stu-id="07ed9-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="07ed9-173">Ихттпактионресулт — это одна из новых возможностей веб-API 2, которая упрощает разработку модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="07ed9-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="07ed9-174">Классы, реализующие интерфейс Ихттпактионресулт, находятся в пространстве имен [System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) .</span><span class="sxs-lookup"><span data-stu-id="07ed9-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="07ed9-175">Эти классы представляют возможные ответы от запроса действия и соответствуют кодам состояния HTTP.</span><span class="sxs-lookup"><span data-stu-id="07ed9-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="07ed9-176">Создайте решение.</span><span class="sxs-lookup"><span data-stu-id="07ed9-176">Build the solution.</span></span>

<span data-ttu-id="07ed9-177">Теперь вы готовы к настройке тестового проекта.</span><span class="sxs-lookup"><span data-stu-id="07ed9-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="07ed9-178">Установка пакетов NuGet в тестовом проекте</span><span class="sxs-lookup"><span data-stu-id="07ed9-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="07ed9-179">Если для создания приложения используется пустой шаблон, проект модульного теста (Стореапп. Tests) не включает установленные пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="07ed9-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="07ed9-180">Другие шаблоны, например шаблон веб-API, включают некоторые пакеты NuGet в проект модульного теста.</span><span class="sxs-lookup"><span data-stu-id="07ed9-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="07ed9-181">Для работы с этим руководством необходимо включить основной пакет веб-API 2 Microsoft ASP.NET в тестовый проект.</span><span class="sxs-lookup"><span data-stu-id="07ed9-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="07ed9-182">Щелкните правой кнопкой мыши проект Стореапп. Tests и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="07ed9-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="07ed9-183">Чтобы добавить пакеты в проект, необходимо выбрать проект Стореапп. Tests.</span><span class="sxs-lookup"><span data-stu-id="07ed9-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![Управление пакетами](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="07ed9-185">Найдите и установите Microsoft ASP.NET основной пакет веб-API 2.</span><span class="sxs-lookup"><span data-stu-id="07ed9-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![Установка основного пакета веб-API](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="07ed9-187">Закройте окно Управление пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="07ed9-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="07ed9-188">Создание тестов</span><span class="sxs-lookup"><span data-stu-id="07ed9-188">Create tests</span></span>

<span data-ttu-id="07ed9-189">По умолчанию тестовый проект содержит пустой тестовый файл с именем UnitTest1.cs.</span><span class="sxs-lookup"><span data-stu-id="07ed9-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="07ed9-190">В этом файле показаны атрибуты, используемые для создания методов теста.</span><span class="sxs-lookup"><span data-stu-id="07ed9-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="07ed9-191">Для модульных тестов можно либо использовать этот файл, либо создать собственный файл.</span><span class="sxs-lookup"><span data-stu-id="07ed9-191">For your unit tests, you can either use this file or create your own file.</span></span>

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="07ed9-193">В этом руководстве вы создадите собственный тестовый класс.</span><span class="sxs-lookup"><span data-stu-id="07ed9-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="07ed9-194">Вы можете удалить файл UnitTest1.cs.</span><span class="sxs-lookup"><span data-stu-id="07ed9-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="07ed9-195">Добавьте класс с именем **TestSimpleProductController.CS**и замените код следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="07ed9-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="07ed9-196">Выполнение тестов</span><span class="sxs-lookup"><span data-stu-id="07ed9-196">Run tests</span></span>

<span data-ttu-id="07ed9-197">Теперь все готово для выполнения тестов.</span><span class="sxs-lookup"><span data-stu-id="07ed9-197">You are now ready to run the tests.</span></span> <span data-ttu-id="07ed9-198">Будет протестирован весь метод, помеченный атрибутом **TestMethod** .</span><span class="sxs-lookup"><span data-stu-id="07ed9-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="07ed9-199">В пункте меню **тест** выполните тесты.</span><span class="sxs-lookup"><span data-stu-id="07ed9-199">From the **Test** menu item, run the tests.</span></span>

![Запуск тестов](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="07ed9-201">Откройте окно **обозревателя тестов** и обратите внимание на результаты тестов.</span><span class="sxs-lookup"><span data-stu-id="07ed9-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![результаты теста](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="07ed9-203">Сводка</span><span class="sxs-lookup"><span data-stu-id="07ed9-203">Summary</span></span>

<span data-ttu-id="07ed9-204">Учебник успешно пройден.</span><span class="sxs-lookup"><span data-stu-id="07ed9-204">You have completed this tutorial.</span></span> <span data-ttu-id="07ed9-205">Данные в этом учебнике были намеренно упрощены, чтобы сосредоточиться на условиях модульного тестирования.</span><span class="sxs-lookup"><span data-stu-id="07ed9-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="07ed9-206">Дополнительные сведения о модульном тестировании для расширенных сценариев данных см. в разделе [макет Entity Framework при модульном тестировании веб-API ASP.NET 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="07ed9-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
