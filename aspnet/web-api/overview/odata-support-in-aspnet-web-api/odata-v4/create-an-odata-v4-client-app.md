---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: Создание клиентского приложения OData V4 (C#) | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448122"
---
# <a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="98a21-102">Создание клиентского приложения OData v4 (C#)</span><span class="sxs-lookup"><span data-stu-id="98a21-102">Create an OData v4 Client App (C#)</span></span>

<span data-ttu-id="98a21-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="98a21-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="98a21-104">В предыдущем руководстве вы создали базовую службу OData, которая поддерживает операции CRUD.</span><span class="sxs-lookup"><span data-stu-id="98a21-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="98a21-105">Теперь создадим клиент для службы.</span><span class="sxs-lookup"><span data-stu-id="98a21-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="98a21-106">Запустите новый экземпляр Visual Studio и создайте новый проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="98a21-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="98a21-107">В диалоговом окне **Новый проект** выберите **установленные** **шаблоны** &gt; &gt; **Visual C#**  &gt; **Рабочий стол Windows**и выберите шаблон **консольное приложение** .</span><span class="sxs-lookup"><span data-stu-id="98a21-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="98a21-108">Присвойте проекту имя &quot;Продуктсапп&quot;.</span><span class="sxs-lookup"><span data-stu-id="98a21-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="98a21-109">Вы также можете добавить консольное приложение в то же решение Visual Studio, которое содержит службу OData.</span><span class="sxs-lookup"><span data-stu-id="98a21-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>

## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="98a21-110">Установка генератора клиентского кода OData</span><span class="sxs-lookup"><span data-stu-id="98a21-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="98a21-111">Откройте меню **Средства** и выберите пункт **Расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="98a21-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="98a21-112">Выберите в **интернете** &gt; **галерею Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="98a21-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="98a21-113">В поле поиска найдите &quot;генератор кода клиента OData&quot;.</span><span class="sxs-lookup"><span data-stu-id="98a21-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="98a21-114">Нажмите кнопку **скачать** , чтобы установить VSIX.</span><span class="sxs-lookup"><span data-stu-id="98a21-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="98a21-115">Возможно, вам будет предложено перезапустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98a21-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="98a21-116">Локальное выполнение службы OData</span><span class="sxs-lookup"><span data-stu-id="98a21-116">Run the OData Service Locally</span></span>

<span data-ttu-id="98a21-117">Запустите проект Продуктсервице из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98a21-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="98a21-118">По умолчанию Visual Studio запускает браузер в корне приложения.</span><span class="sxs-lookup"><span data-stu-id="98a21-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="98a21-119">Обратите внимание на URI; Это будет необходимо на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="98a21-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="98a21-120">Не закрывайте приложение.</span><span class="sxs-lookup"><span data-stu-id="98a21-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="98a21-121">Если оба проекта помещаются в одно решение, запустите проект Продуктсервице без отладки.</span><span class="sxs-lookup"><span data-stu-id="98a21-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="98a21-122">На следующем шаге необходимо, чтобы служба была запущена при изменении проекта консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="98a21-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>

## <a name="generate-the-service-proxy"></a><span data-ttu-id="98a21-123">Создание прокси-сервера службы</span><span class="sxs-lookup"><span data-stu-id="98a21-123">Generate the Service Proxy</span></span>

<span data-ttu-id="98a21-124">Прокси-сервер службы — это класс .NET, который определяет методы для доступа к службе OData.</span><span class="sxs-lookup"><span data-stu-id="98a21-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="98a21-125">Прокси-сервер преобразует вызовы метода в HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="98a21-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="98a21-126">Класс прокси будет создан путем запуска [шаблона T4](https://msdn.microsoft.com/library/bb126445.aspx).</span><span class="sxs-lookup"><span data-stu-id="98a21-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="98a21-127">Щелкните проект правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="98a21-127">Right-click the project.</span></span> <span data-ttu-id="98a21-128">Щелкните **Добавить** &gt; **Создать элемент**.</span><span class="sxs-lookup"><span data-stu-id="98a21-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="98a21-129">В диалоговом окне **Добавление нового элемента** выберите **визуальные C# элементы** &gt; **код** &gt; **клиент OData**.</span><span class="sxs-lookup"><span data-stu-id="98a21-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="98a21-130">Присвойте шаблону имя &quot;ProductClient.tt&quot;.</span><span class="sxs-lookup"><span data-stu-id="98a21-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="98a21-131">Щелкните **Добавить** и щелкните предупреждение безопасности.</span><span class="sxs-lookup"><span data-stu-id="98a21-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="98a21-132">На этом этапе вы получите ошибку, которую можно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="98a21-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="98a21-133">Visual Studio автоматически запускает шаблон, но сначала необходимо настроить некоторые параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="98a21-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="98a21-134">Откройте файл Продуктклиент. OData. config. В элементе `Parameter` вставьте URI из проекта Продуктсервице (предыдущий шаг).</span><span class="sxs-lookup"><span data-stu-id="98a21-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="98a21-135">Пример:</span><span class="sxs-lookup"><span data-stu-id="98a21-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="98a21-136">Снова запустите шаблон.</span><span class="sxs-lookup"><span data-stu-id="98a21-136">Run the template again.</span></span> <span data-ttu-id="98a21-137">В обозреватель решений щелкните правой кнопкой мыши файл ProductClient.tt и выберите команду **Запустить пользовательский инструмент**.</span><span class="sxs-lookup"><span data-stu-id="98a21-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="98a21-138">Шаблон создает файл кода с именем ProductClient.cs, определяющий прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="98a21-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="98a21-139">При разработке приложения, если вы измените конечную точку OData, снова запустите шаблон, чтобы обновить учетную запись-посредник.</span><span class="sxs-lookup"><span data-stu-id="98a21-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="98a21-140">Использование прокси-сервера службы для вызова службы OData</span><span class="sxs-lookup"><span data-stu-id="98a21-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="98a21-141">Откройте файл Program.cs и замените стандартный код следующим.</span><span class="sxs-lookup"><span data-stu-id="98a21-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="98a21-142">Замените значение *ServiceUri* на URI службы ранее.</span><span class="sxs-lookup"><span data-stu-id="98a21-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="98a21-143">При запуске приложения он должен вывести следующее:</span><span class="sxs-lookup"><span data-stu-id="98a21-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
