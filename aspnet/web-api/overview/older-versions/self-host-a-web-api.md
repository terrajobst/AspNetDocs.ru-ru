---
uid: web-api/overview/older-versions/self-host-a-web-api
title: Веб-API ASP.NET 1 (C#) — ASP.NET 4. x.
author: MikeWasson
description: В руководстве с кодом показано, как разместить веб-API внутри консольного приложения.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421374"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="f94aa-103">Самостоятельный веб-API ASP.NET 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="f94aa-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="f94aa-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f94aa-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="f94aa-105">В этом руководстве показано, как разместить веб-API внутри консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="f94aa-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="f94aa-106">Для веб-API ASP.NET не требуются службы IIS.</span><span class="sxs-lookup"><span data-stu-id="f94aa-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="f94aa-107">Веб-API можно самостоятельно разместить в собственном процессе узла.</span><span class="sxs-lookup"><span data-stu-id="f94aa-107">You can self-host a web API in your own host process.</span></span> 
> 
> <span data-ttu-id="f94aa-108">**Новые приложения должны использовать OWIN для веб-API с самостоятельным размещением.**</span><span class="sxs-lookup"><span data-stu-id="f94aa-108">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="f94aa-109">См. раздел [Использование OWIN для самостоятельного размещения веб-API ASP.NET 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="f94aa-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f94aa-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="f94aa-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f94aa-111">Веб-API 1</span><span class="sxs-lookup"><span data-stu-id="f94aa-111">Web API 1</span></span>
> - <span data-ttu-id="f94aa-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f94aa-112">Visual Studio 2012</span></span>

## <a name="create-the-console-application-project"></a><span data-ttu-id="f94aa-113">Создание проекта консольного приложения</span><span class="sxs-lookup"><span data-stu-id="f94aa-113">Create the Console Application Project</span></span>

<span data-ttu-id="f94aa-114">Запустите Visual Studio и выберите **создать проект** на **начальной** странице.</span><span class="sxs-lookup"><span data-stu-id="f94aa-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="f94aa-115">Либо в меню **файл** выберите **создать** , а затем — **проект**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="f94aa-116">В области **шаблоны** выберите **Установленные шаблоны** и разверните узел  **C# визуального** элемента.</span><span class="sxs-lookup"><span data-stu-id="f94aa-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="f94aa-117">В **разделе C#визуальный** элемент выберите **Windows**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="f94aa-118">В списке шаблонов проектов выберите **консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="f94aa-119">Присвойте проекту имя &quot;резидент&quot; и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="f94aa-120">Настройка целевой платформы (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="f94aa-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="f94aa-121">Если вы используете Visual Studio 2010, измените целевую платформу на .NET Framework 4,0.</span><span class="sxs-lookup"><span data-stu-id="f94aa-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="f94aa-122">(По умолчанию шаблон проекта предназначен для [клиентского профиля .NET Framework](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span><span class="sxs-lookup"><span data-stu-id="f94aa-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="f94aa-123">В обозреватель решений щелкните правой кнопкой мыши проект и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="f94aa-124">В раскрывающемся списке **Целевая платформа** измените целевую платформу на .NET Framework 4,0.</span><span class="sxs-lookup"><span data-stu-id="f94aa-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="f94aa-125">При появлении запроса на применение изменений нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="f94aa-126">Установка диспетчера пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="f94aa-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="f94aa-127">Диспетчер пакетов NuGet — это самый простой способ добавления сборок веб-API в проект non-ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f94aa-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="f94aa-128">Чтобы проверить, установлен ли диспетчер пакетов NuGet, откройте меню **Сервис** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f94aa-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="f94aa-129">Если отображается пункт меню **Диспетчер пакетов NuGet**, то у вас есть диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="f94aa-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="f94aa-130">Чтобы установить диспетчер пакетов NuGet, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f94aa-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="f94aa-131">Запустите среду Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f94aa-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="f94aa-132">Откройте меню **Средства** и выберите пункт **Расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="f94aa-133">В диалоговом окне **расширения и обновления** выберите в **сети**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="f94aa-134">Если вы не видите "Диспетчер пакетов NuGet", в поле поиска введите "Диспетчер пакетов NuGet".</span><span class="sxs-lookup"><span data-stu-id="f94aa-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="f94aa-135">Выберите Диспетчер пакетов NuGet и нажмите кнопку **скачать**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="f94aa-136">После завершения скачивания вам будет предложено установить.</span><span class="sxs-lookup"><span data-stu-id="f94aa-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="f94aa-137">После завершения установки может быть предложено перезапустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f94aa-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="f94aa-138">Добавление пакета NuGet для веб-API</span><span class="sxs-lookup"><span data-stu-id="f94aa-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="f94aa-139">После установки диспетчера пакетов NuGet добавьте в проект пакет самообслуживания веб-API.</span><span class="sxs-lookup"><span data-stu-id="f94aa-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="f94aa-140">В меню **Сервис** выберите **Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="f94aa-141">*Примечание*. Если вы не видите этот пункт меню, убедитесь, что диспетчер пакетов NuGet установлен правильно.</span><span class="sxs-lookup"><span data-stu-id="f94aa-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="f94aa-142">Выберите **Управление пакетами NuGet для решения**</span><span class="sxs-lookup"><span data-stu-id="f94aa-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="f94aa-143">В диалоговом окне **Управление пакетами NugGet** выберите в **сети**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="f94aa-144">В поле поиска введите &quot;Microsoft. AspNet. WebApi. резидент&quot;.</span><span class="sxs-lookup"><span data-stu-id="f94aa-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="f94aa-145">Выберите веб-API ASP.NET пакет самообслуживания и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="f94aa-146">После установки пакета нажмите кнопку **Закрыть** , чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="f94aa-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="f94aa-147">Убедитесь, что установлен пакет с именем Microsoft. AspNet. WebApi. резидент, а не Аспнетвебапи. резидент.</span><span class="sxs-lookup"><span data-stu-id="f94aa-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="f94aa-148">Создание модели и контроллера</span><span class="sxs-lookup"><span data-stu-id="f94aa-148">Create the Model and Controller</span></span>

<span data-ttu-id="f94aa-149">В этом руководстве используются те же классы модели и контроллера, что и в [Начало работы](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) руководстве.</span><span class="sxs-lookup"><span data-stu-id="f94aa-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="f94aa-150">Добавьте открытый класс с именем `Product`.</span><span class="sxs-lookup"><span data-stu-id="f94aa-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="f94aa-151">Добавьте открытый класс с именем `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="f94aa-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="f94aa-152">Производные от класса **System. Web. http. ApiController**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="f94aa-153">Дополнительные сведения о коде в этом контроллере см. в руководстве по [Начало работы](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) .</span><span class="sxs-lookup"><span data-stu-id="f94aa-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="f94aa-154">Этот контроллер определяет три действия GET:</span><span class="sxs-lookup"><span data-stu-id="f94aa-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="f94aa-155">URI</span><span class="sxs-lookup"><span data-stu-id="f94aa-155">URI</span></span> | <span data-ttu-id="f94aa-156">Description</span><span class="sxs-lookup"><span data-stu-id="f94aa-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f94aa-157">/апи/продуктс</span><span class="sxs-lookup"><span data-stu-id="f94aa-157">/api/products</span></span> | <span data-ttu-id="f94aa-158">Получение списка всех продуктов.</span><span class="sxs-lookup"><span data-stu-id="f94aa-158">Get a list of all products.</span></span> |
| <span data-ttu-id="f94aa-159">*идентификатор* /АПИ/Продуктс/</span><span class="sxs-lookup"><span data-stu-id="f94aa-159">/api/products/*id*</span></span> | <span data-ttu-id="f94aa-160">Получение продукта по ИДЕНТИФИКАТОРу.</span><span class="sxs-lookup"><span data-stu-id="f94aa-160">Get a product by ID.</span></span> |
| <span data-ttu-id="f94aa-161">/АПИ/Продуктс/? Category =*Категория*</span><span class="sxs-lookup"><span data-stu-id="f94aa-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="f94aa-162">Получение списка продуктов по категориям.</span><span class="sxs-lookup"><span data-stu-id="f94aa-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="f94aa-163">Размещение веб-API</span><span class="sxs-lookup"><span data-stu-id="f94aa-163">Host the Web API</span></span>

<span data-ttu-id="f94aa-164">Откройте файл Program.cs и добавьте следующие операторы using:</span><span class="sxs-lookup"><span data-stu-id="f94aa-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="f94aa-165">Добавьте следующий код в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="f94aa-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="f94aa-166">Используемых Добавление резервирования пространства имен URL-адресов HTTP</span><span class="sxs-lookup"><span data-stu-id="f94aa-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="f94aa-167">Это приложение прослушивает `http://localhost:8080/`.</span><span class="sxs-lookup"><span data-stu-id="f94aa-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="f94aa-168">По умолчанию для прослушивания определенного HTTP-адреса требуются права администратора.</span><span class="sxs-lookup"><span data-stu-id="f94aa-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="f94aa-169">При запуске этого учебника может возникнуть ошибка: "HTTP не удалось зарегистрировать URL-адрес http://+:8080/" существует два способа избежать этой ошибки:</span><span class="sxs-lookup"><span data-stu-id="f94aa-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="f94aa-170">Запустите Visual Studio с повышенными правами администратора или</span><span class="sxs-lookup"><span data-stu-id="f94aa-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="f94aa-171">С помощью программы Netsh. exe предоставьте учетной записи разрешения на резервирование URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="f94aa-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="f94aa-172">Чтобы использовать программу Netsh. exe, откройте командную строку с правами администратора и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f94aa-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="f94aa-173">где *компьютер* — ваша учетная запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="f94aa-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="f94aa-174">После завершения самостоятельного размещения обязательно удалите резервирование.</span><span class="sxs-lookup"><span data-stu-id="f94aa-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="f94aa-175">Вызов веб-API из клиентского приложения (C#)</span><span class="sxs-lookup"><span data-stu-id="f94aa-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="f94aa-176">Давайте напишем простое консольное приложение, вызывающее веб-API.</span><span class="sxs-lookup"><span data-stu-id="f94aa-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="f94aa-177">Добавьте в решение новый проект консольного приложения:</span><span class="sxs-lookup"><span data-stu-id="f94aa-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="f94aa-178">В обозреватель решений щелкните решение правой кнопкой мыши и выберите команду **Добавить новый проект**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="f94aa-179">Создайте новое консольное приложение с именем &quot;ClientApp&quot;.</span><span class="sxs-lookup"><span data-stu-id="f94aa-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="f94aa-180">Используйте диспетчер пакетов NuGet, чтобы добавить пакет библиотек веб-API ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="f94aa-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="f94aa-181">В меню Сервис выберите **Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="f94aa-182">Выберите **Управление пакетами NuGet для решения**</span><span class="sxs-lookup"><span data-stu-id="f94aa-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="f94aa-183">В диалоговом окне **Управление пакетами NuGet** выберите в **сети**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="f94aa-184">В поле поиска введите &quot;Microsoft. AspNet. WebApi. Client&quot;.</span><span class="sxs-lookup"><span data-stu-id="f94aa-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="f94aa-185">Выберите пакет клиентских библиотек Microsoft ASP.NET веб-API и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="f94aa-186">Добавьте ссылку в ClientApp в проект резидент:</span><span class="sxs-lookup"><span data-stu-id="f94aa-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="f94aa-187">В обозреватель решений щелкните правой кнопкой мыши проект ClientApp.</span><span class="sxs-lookup"><span data-stu-id="f94aa-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="f94aa-188">Выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="f94aa-189">В диалоговом окне **Диспетчер ссылок** в разделе **решение**выберите **проекты**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="f94aa-190">Выберите проект резидент.</span><span class="sxs-lookup"><span data-stu-id="f94aa-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="f94aa-191">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="f94aa-192">Откройте файл Client/Program. cs.</span><span class="sxs-lookup"><span data-stu-id="f94aa-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="f94aa-193">Добавьте следующий оператор **using** :</span><span class="sxs-lookup"><span data-stu-id="f94aa-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="f94aa-194">Добавьте статический экземпляр **HttpClient** :</span><span class="sxs-lookup"><span data-stu-id="f94aa-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="f94aa-195">Добавьте следующие методы, чтобы вывести список всех продуктов, составить список продуктов по ИДЕНТИФИКАТОРу и составить список продуктов по категориям.</span><span class="sxs-lookup"><span data-stu-id="f94aa-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="f94aa-196">Каждый из этих методов следует одному и тому же шаблону:</span><span class="sxs-lookup"><span data-stu-id="f94aa-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="f94aa-197">Вызовите **HttpClient. Async** для отправки запроса GET соответствующему URI.</span><span class="sxs-lookup"><span data-stu-id="f94aa-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="f94aa-198">Вызовите **HttpResponseMessage. енсуресукцессстатускоде**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="f94aa-199">Этот метод создает исключение, если состояние ответа HTTP является кодом ошибки.</span><span class="sxs-lookup"><span data-stu-id="f94aa-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="f94aa-200">Вызовите **реадасасинк&lt;t&gt;** , чтобы десериализовать тип CLR из HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="f94aa-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="f94aa-201">Этот метод является методом расширения, определенным в **System .NET. http. хттпконтентекстенсионс**.</span><span class="sxs-lookup"><span data-stu-id="f94aa-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="f94aa-202">Методы **реадасасинк** и **Async** являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="f94aa-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="f94aa-203">Они возвращают объекты **задач** , представляющие асинхронную операцию.</span><span class="sxs-lookup"><span data-stu-id="f94aa-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="f94aa-204">Получение свойства **result** блокирует поток до завершения операции.</span><span class="sxs-lookup"><span data-stu-id="f94aa-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="f94aa-205">Дополнительные сведения об использовании HttpClient, в том числе о том, как выполнять неблокирующие вызовы, см. в разделе [вызов веб-API из клиента .NET](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="f94aa-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="f94aa-206">Перед вызовом этих методов задайте для свойства BaseAddress экземпляра HttpClient значение "`http://localhost:8080`".</span><span class="sxs-lookup"><span data-stu-id="f94aa-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="f94aa-207">Пример:</span><span class="sxs-lookup"><span data-stu-id="f94aa-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="f94aa-208">Он должен вывести следующее.</span><span class="sxs-lookup"><span data-stu-id="f94aa-208">This should output the following.</span></span> <span data-ttu-id="f94aa-209">(Не забудьте сначала запустить приложение резидент.)</span><span class="sxs-lookup"><span data-stu-id="f94aa-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
