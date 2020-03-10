---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: Использование OWIN для самостоятельного размещения веб-API ASP.NET-ASP.NET 4. x
author: rick-anderson
description: Руководство с кодом, демонстрирующим размещение веб-API ASP.NET в консольном приложении.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448332"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="c69d4-103">Использование OWIN для самостоятельного размещения веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c69d4-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 

> <span data-ttu-id="c69d4-104">В этом руководстве показано, как разместить веб-API ASP.NET в консольном приложении, используя OWIN для самостоятельного размещения платформы веб-API.</span><span class="sxs-lookup"><span data-stu-id="c69d4-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="c69d4-105">[Открытый веб-интерфейс для .NET](http://owin.org) (OWIN) определяет абстракцию между веб-серверами и веб-приложениями .NET.</span><span class="sxs-lookup"><span data-stu-id="c69d4-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="c69d4-106">OWIN отделяет веб-приложение от сервера, что делает OWIN идеальным для самостоятельного размещения веб-приложения в собственном процессе вне служб IIS.</span><span class="sxs-lookup"><span data-stu-id="c69d4-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c69d4-107">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="c69d4-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="c69d4-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c69d4-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="c69d4-109">5\.2.7 веб-API</span><span class="sxs-lookup"><span data-stu-id="c69d4-109">Web API 5.2.7</span></span>

> [!NOTE]
> <span data-ttu-id="c69d4-110">Полный исходный код для этого руководства можно найти по адресу [GitHub.com/ASPNET/Samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span><span class="sxs-lookup"><span data-stu-id="c69d4-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="c69d4-111">Создание консольного приложение</span><span class="sxs-lookup"><span data-stu-id="c69d4-111">Create a console application</span></span>

<span data-ttu-id="c69d4-112">В меню **файл** выберите **создать**, а затем выберите **проект**.</span><span class="sxs-lookup"><span data-stu-id="c69d4-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="c69d4-113">В **разделе** **C#Visual**выберите **Рабочий стол Windows** и выберите **консольное приложение (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="c69d4-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="c69d4-114">Присвойте проекту имя "Овинселфхостсампле" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c69d4-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="c69d4-115">Добавление веб-API и пакетов OWIN</span><span class="sxs-lookup"><span data-stu-id="c69d4-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="c69d4-116">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="c69d4-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="c69d4-117">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c69d4-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="c69d4-118">При этом будет установлен пакет WebAPI OWIN резидент и все необходимые OWIN пакеты.</span><span class="sxs-lookup"><span data-stu-id="c69d4-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="c69d4-119">Настройка веб-API для самостоятельного размещения</span><span class="sxs-lookup"><span data-stu-id="c69d4-119">Configure Web API for self-host</span></span>

<span data-ttu-id="c69d4-120">В обозреватель решений щелкните правой кнопкой мыши проект и выберите **добавить** / **класс** , чтобы добавить новый класс.</span><span class="sxs-lookup"><span data-stu-id="c69d4-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="c69d4-121">Назовите класс `Startup`.</span><span class="sxs-lookup"><span data-stu-id="c69d4-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="c69d4-122">Замените весь стандартный код в этом файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c69d4-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="c69d4-123">Добавление контроллера веб-API</span><span class="sxs-lookup"><span data-stu-id="c69d4-123">Add a Web API controller</span></span>

<span data-ttu-id="c69d4-124">Затем добавьте класс контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="c69d4-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="c69d4-125">В обозреватель решений щелкните правой кнопкой мыши проект и выберите **добавить** / **класс** , чтобы добавить новый класс.</span><span class="sxs-lookup"><span data-stu-id="c69d4-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="c69d4-126">Назовите класс `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="c69d4-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="c69d4-127">Замените весь стандартный код в этом файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c69d4-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="c69d4-128">Запуск узла OWIN и создание запроса с помощью HttpClient</span><span class="sxs-lookup"><span data-stu-id="c69d4-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="c69d4-129">Замените весь стандартный код в файле Program.cs следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c69d4-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="c69d4-130">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="c69d4-130">Run the application</span></span>

<span data-ttu-id="c69d4-131">Чтобы запустить приложение, нажмите клавишу F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c69d4-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="c69d4-132">Полученный результат должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="c69d4-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="c69d4-133">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c69d4-133">Additional resources</span></span>

[<span data-ttu-id="c69d4-134">Обзор проекта Katana</span><span class="sxs-lookup"><span data-stu-id="c69d4-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="c69d4-135">Веб-API ASP.NET узла в рабочей роли Azure</span><span class="sxs-lookup"><span data-stu-id="c69d4-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
