---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: Создание страниц справки для веб-API ASP.NET-ASP.NET 4. x
author: MikeWasson
description: В этом руководстве с кодом показано, как создавать страницы справки для веб-API ASP.NET в ASP.NET 4. x.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448620"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="2caa2-103">Создание страниц справки для веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2caa2-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="2caa2-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2caa2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2caa2-105">В этом руководстве с кодом показано, как создавать страницы справки для веб-API ASP.NET в ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="2caa2-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="2caa2-106">При создании веб-API часто бывает полезно создать страницу справки, чтобы другие разработчики узнают, как вызывать API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="2caa2-107">Вы можете создать всю документацию вручную, но лучше создавать ее автоматически.</span><span class="sxs-lookup"><span data-stu-id="2caa2-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="2caa2-108">Чтобы упростить эту задачу, веб-API ASP.NET предоставляет библиотеку для автоматического создания страниц справки во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2caa2-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="2caa2-109">Создание страниц справки по API</span><span class="sxs-lookup"><span data-stu-id="2caa2-109">Creating API Help Pages</span></span>

<span data-ttu-id="2caa2-110">Установите [обновление ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="2caa2-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="2caa2-111">Это обновление интегрирует страницы справки в шаблон проекта веб-API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="2caa2-112">Затем создайте новый проект ASP.NET MVC 4 и выберите шаблон проекта веб-API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="2caa2-113">Шаблон проекта создает пример контроллера API с именем `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="2caa2-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="2caa2-114">Шаблон также создает страницы справки API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-114">The template also creates the API help pages.</span></span> <span data-ttu-id="2caa2-115">Все файлы кода для страницы справки помещаются в папку Areas проекта.</span><span class="sxs-lookup"><span data-stu-id="2caa2-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="2caa2-116">При запуске приложения на домашней странице содержится ссылка на страницу справки по API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="2caa2-117">На домашней странице относительный путь —/Хелп.</span><span class="sxs-lookup"><span data-stu-id="2caa2-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="2caa2-118">Эта ссылка открывает страницу сводки API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="2caa2-119">Представление MVC для этой страницы определено в области/Хелппаже/views/Help/index. cshtml.</span><span class="sxs-lookup"><span data-stu-id="2caa2-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="2caa2-120">Эту страницу можно изменить, чтобы изменить макет, введение, заголовок, стили и т. д.</span><span class="sxs-lookup"><span data-stu-id="2caa2-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="2caa2-121">Основная часть страницы — это таблица API-интерфейсов, сгруппированных по контроллеру.</span><span class="sxs-lookup"><span data-stu-id="2caa2-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="2caa2-122">Записи таблицы создаются динамически с помощью интерфейса **иапиексплорер** .</span><span class="sxs-lookup"><span data-stu-id="2caa2-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="2caa2-123">(Подробнее об этом интерфейсе я расскажу чуть позже.) При добавлении нового контроллера API таблица автоматически обновляется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2caa2-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="2caa2-124">В столбце "API" перечислены метод HTTP и относительный URI.</span><span class="sxs-lookup"><span data-stu-id="2caa2-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="2caa2-125">В столбце "Описание" содержится документация по каждому API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="2caa2-126">Изначально документация представляет собой просто текст заполнителя.</span><span class="sxs-lookup"><span data-stu-id="2caa2-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="2caa2-127">В следующем разделе я покажу, как добавить документацию из комментариев XML.</span><span class="sxs-lookup"><span data-stu-id="2caa2-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="2caa2-128">Каждый API имеет ссылку на страницу с более подробными сведениями, включая примеры текстов запросов и ответов.</span><span class="sxs-lookup"><span data-stu-id="2caa2-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="2caa2-129">Добавление страниц справки в существующий проект</span><span class="sxs-lookup"><span data-stu-id="2caa2-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="2caa2-130">Страницы справки можно добавлять в существующий проект веб-API с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="2caa2-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="2caa2-131">Этот параметр полезен при запуске из шаблона проекта, отличного от шаблонов веб-API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="2caa2-132">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="2caa2-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="2caa2-133">В окне [консоли диспетчера пакетов](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) введите одну из следующих команд:</span><span class="sxs-lookup"><span data-stu-id="2caa2-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="2caa2-134">Для **C#** приложения: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="2caa2-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="2caa2-135">Для **Visual Basic** приложения: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="2caa2-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="2caa2-136">Существует два пакета: один для C# и один для Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="2caa2-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="2caa2-137">Обязательно используйте тот, который соответствует вашему проекту.</span><span class="sxs-lookup"><span data-stu-id="2caa2-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="2caa2-138">Эта команда устанавливает необходимые сборки и добавляет представления MVC для страниц справки (расположенных в папке Areas/Хелппаже).</span><span class="sxs-lookup"><span data-stu-id="2caa2-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="2caa2-139">Необходимо вручную добавить ссылку на страницу справки.</span><span class="sxs-lookup"><span data-stu-id="2caa2-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="2caa2-140">Универсальный код ресурса (URI) —/Хелп.</span><span class="sxs-lookup"><span data-stu-id="2caa2-140">The URI is /Help.</span></span> <span data-ttu-id="2caa2-141">Чтобы создать ссылку в представлении Razor, добавьте следующее:</span><span class="sxs-lookup"><span data-stu-id="2caa2-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="2caa2-142">Кроме того, обязательно регистрируйте области.</span><span class="sxs-lookup"><span data-stu-id="2caa2-142">Also, make sure to register areas.</span></span> <span data-ttu-id="2caa2-143">В файле Global. asax добавьте следующий код в метод **\_запуска приложения** , если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="2caa2-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="2caa2-144">Добавление документации по API</span><span class="sxs-lookup"><span data-stu-id="2caa2-144">Adding API Documentation</span></span>

<span data-ttu-id="2caa2-145">По умолчанию страницы справки содержат строки заполнителей для документации.</span><span class="sxs-lookup"><span data-stu-id="2caa2-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="2caa2-146">Для создания документации можно использовать [Комментарии XML-документации](https://msdn.microsoft.com/library/b2s063f7.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2caa2-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="2caa2-147">Чтобы включить эту функцию, откройте файл Areas/Хелппаже/App\_Start/Хелппажеконфиг. cs и раскомментируйте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="2caa2-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="2caa2-148">Теперь включите XML-документацию.</span><span class="sxs-lookup"><span data-stu-id="2caa2-148">Now enable XML documentation.</span></span> <span data-ttu-id="2caa2-149">В обозреватель решений щелкните правой кнопкой мыши проект и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="2caa2-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="2caa2-150">Выберите страницу **Сборка** .</span><span class="sxs-lookup"><span data-stu-id="2caa2-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="2caa2-151">В разделе **выходные данные**проверьте **XML-файл документации**.</span><span class="sxs-lookup"><span data-stu-id="2caa2-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="2caa2-152">В поле ввода введите "App\_Data/XmlDocument. XML".</span><span class="sxs-lookup"><span data-stu-id="2caa2-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="2caa2-153">Затем откройте код контроллера API `ValuesController`, который определен в/Контроллерс/валуесконтроллер.КС.</span><span class="sxs-lookup"><span data-stu-id="2caa2-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="2caa2-154">Добавьте в методы контроллера некоторые комментарии к документации.</span><span class="sxs-lookup"><span data-stu-id="2caa2-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="2caa2-155">Пример:</span><span class="sxs-lookup"><span data-stu-id="2caa2-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="2caa2-156">Совет. Если поместить курсор в строку над методом и ввести три косые черты, Visual Studio автоматически вставит XML-элементы.</span><span class="sxs-lookup"><span data-stu-id="2caa2-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="2caa2-157">Затем можно ввести пустые значения.</span><span class="sxs-lookup"><span data-stu-id="2caa2-157">Then you can fill in the blanks.</span></span>

<span data-ttu-id="2caa2-158">Теперь выполните сборку и запуск приложения еще раз и перейдите на страницу справки.</span><span class="sxs-lookup"><span data-stu-id="2caa2-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="2caa2-159">Строки документации должны присутствовать в таблице API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="2caa2-160">Страница справки считывает строки из XML-файла во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2caa2-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="2caa2-161">(При развертывании приложения необходимо выполнить развертывание XML-файла.)</span><span class="sxs-lookup"><span data-stu-id="2caa2-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="2caa2-162">Внутри</span><span class="sxs-lookup"><span data-stu-id="2caa2-162">Under the Hood</span></span>

<span data-ttu-id="2caa2-163">Страницы справки создаются на основе класса **апиексплорер** , который является частью платформы веб-API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="2caa2-164">Класс **апиексплорер** предоставляет необработанный материал для создания страницы справки.</span><span class="sxs-lookup"><span data-stu-id="2caa2-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="2caa2-165">Для каждого API **апиексплорер** содержит **апидескриптион** , описывающий API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="2caa2-166">Для этой цели "API" определяется как сочетание метода HTTP и относительного URI.</span><span class="sxs-lookup"><span data-stu-id="2caa2-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="2caa2-167">Например, вот несколько различных интерфейсов API:</span><span class="sxs-lookup"><span data-stu-id="2caa2-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="2caa2-168">ПОЛУЧИТЬ/АПИ/Продуктс</span><span class="sxs-lookup"><span data-stu-id="2caa2-168">GET /api/Products</span></span>
- <span data-ttu-id="2caa2-169">ПОЛУЧИТЬ/АПИ/Продуктс/{ИД}</span><span class="sxs-lookup"><span data-stu-id="2caa2-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="2caa2-170">ОПУБЛИКОВАТЬ/АПИ/Продуктс</span><span class="sxs-lookup"><span data-stu-id="2caa2-170">POST /api/Products</span></span>

<span data-ttu-id="2caa2-171">Если действие контроллера поддерживает несколько методов HTTP, **апиексплорер** обрабатывает каждый метод как отдельный API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="2caa2-172">Чтобы скрыть API из **апиексплорер**, добавьте к действию атрибут **апиексплорерсеттингс** и задайте для *игнореапи* значение true.</span><span class="sxs-lookup"><span data-stu-id="2caa2-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="2caa2-173">Можно также добавить этот атрибут к контроллеру, чтобы исключить весь контроллер.</span><span class="sxs-lookup"><span data-stu-id="2caa2-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="2caa2-174">Класс Апиексплорер получает строки документации из интерфейса **идокументатионпровидер** .</span><span class="sxs-lookup"><span data-stu-id="2caa2-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="2caa2-175">Как было показано ранее, Библиотека страниц справки предоставляет **идокументатионпровидер** , который получает документацию из строк XML-документации.</span><span class="sxs-lookup"><span data-stu-id="2caa2-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="2caa2-176">Код находится в/Ареас/хелппаже/ксмлдокументатионпровидер.КС.</span><span class="sxs-lookup"><span data-stu-id="2caa2-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="2caa2-177">Вы можете получить документацию из другого источника, написав собственный **идокументатионпровидер**.</span><span class="sxs-lookup"><span data-stu-id="2caa2-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="2caa2-178">Чтобы подключить ее, вызовите метод расширения **сетдокументатионпровидер** , определенный в **хелппажеконфигуратионекстенсионс**</span><span class="sxs-lookup"><span data-stu-id="2caa2-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="2caa2-179">**Апиексплорер** автоматически вызывает интерфейс **идокументатионпровидер** для получения строк документации для каждого API.</span><span class="sxs-lookup"><span data-stu-id="2caa2-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="2caa2-180">Он сохраняет их в свойстве **Documentation** объектов **апидескриптион** и **апипараметердескриптион** .</span><span class="sxs-lookup"><span data-stu-id="2caa2-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2caa2-181">Next Steps</span><span class="sxs-lookup"><span data-stu-id="2caa2-181">Next Steps</span></span>

<span data-ttu-id="2caa2-182">Вы не ограничены страницами справки, показанными здесь.</span><span class="sxs-lookup"><span data-stu-id="2caa2-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="2caa2-183">На самом деле **апиексплорер** не ограничивается созданием страниц справки.</span><span class="sxs-lookup"><span data-stu-id="2caa2-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="2caa2-184">Яо Хаун ссыл написала некоторые отличные записи в блоге, которые помогут вам обдуматься:</span><span class="sxs-lookup"><span data-stu-id="2caa2-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="2caa2-185">Добавление простого тестового клиента на страницу справки веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2caa2-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="2caa2-186">Обеспечение работы веб-API ASP.NETной страницы справки на самостоятельных размещенных службах</span><span class="sxs-lookup"><span data-stu-id="2caa2-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="2caa2-187">Создание страницы справки (или клиента) во время разработки для веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2caa2-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="2caa2-188">Расширенные настройки страницы справки</span><span class="sxs-lookup"><span data-stu-id="2caa2-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
