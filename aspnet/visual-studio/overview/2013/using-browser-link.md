---
uid: visual-studio/overview/2013/using-browser-link
title: Использование ссылки на браузер в Visual Studio 2013 | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505206"
---
# <a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="2a94d-102">Использование ссылки на браузер в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2a94d-102">Using Browser Link in Visual Studio 2013</span></span>

<span data-ttu-id="2a94d-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2a94d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2a94d-104">Ссылка на браузер — это новая функция в Visual Studio 2013, которая создает коммуникационный канал между средой разработки и одним или несколькими веб-браузерами.</span><span class="sxs-lookup"><span data-stu-id="2a94d-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="2a94d-105">Можно использовать ссылку на браузер для обновления веб-приложения одновременно в нескольких браузерах, что полезно для тестирования в разных браузерах.</span><span class="sxs-lookup"><span data-stu-id="2a94d-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="2a94d-106">Обновление браузера</span><span class="sxs-lookup"><span data-stu-id="2a94d-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="2a94d-107">Просмотр панели мониторинга связи с браузером</span><span class="sxs-lookup"><span data-stu-id="2a94d-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="2a94d-108">Включение связи браузера для статических HTML-файлов</span><span class="sxs-lookup"><span data-stu-id="2a94d-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="2a94d-109">Отключение связи с браузером</span><span class="sxs-lookup"><span data-stu-id="2a94d-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="2a94d-110">Как это работает?</span><span class="sxs-lookup"><span data-stu-id="2a94d-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="2a94d-111">Обновление браузера</span><span class="sxs-lookup"><span data-stu-id="2a94d-111">Browser Refresh</span></span>

<span data-ttu-id="2a94d-112">При обновлении браузера можно обновить несколько браузеров, подключенных к Visual Studio, с помощью ссылки браузера.</span><span class="sxs-lookup"><span data-stu-id="2a94d-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="2a94d-113">Чтобы использовать обновление браузера, сначала создайте приложение ASP.NET с помощью любого из шаблонов проекта.</span><span class="sxs-lookup"><span data-stu-id="2a94d-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="2a94d-114">Выполните отладку приложения, нажав клавишу F5 или щелкнув значок со стрелкой на панели инструментов:</span><span class="sxs-lookup"><span data-stu-id="2a94d-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="2a94d-115">Можно также использовать раскрывающийся список для выбора конкретного браузера для отладки.</span><span class="sxs-lookup"><span data-stu-id="2a94d-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="2a94d-116">Для отладки с несколькими браузерами выберите **Обзор с помощью**.</span><span class="sxs-lookup"><span data-stu-id="2a94d-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="2a94d-117">В диалоговом окне **Просмотр с помощью** удерживайте нажатой КЛАВИШу CTRL, чтобы выбрать более одного браузера.</span><span class="sxs-lookup"><span data-stu-id="2a94d-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="2a94d-118">Нажмите кнопку **Обзор** , чтобы выполнить отладку в выбранных браузерах.</span><span class="sxs-lookup"><span data-stu-id="2a94d-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="2a94d-119">Связь с браузером также работает при запуске браузера извне Visual Studio и переходе по URL-адресу приложения.</span><span class="sxs-lookup"><span data-stu-id="2a94d-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="2a94d-120">Элементы управления связью с браузером находятся в раскрывающемся списке со значком круговой стрелки.</span><span class="sxs-lookup"><span data-stu-id="2a94d-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="2a94d-121">Значок стрелки — это кнопка **Обновить** .</span><span class="sxs-lookup"><span data-stu-id="2a94d-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="2a94d-122">Чтобы узнать, какие браузеры подключены, наведите указатель мыши на кнопку **Обновить** во время отладки.</span><span class="sxs-lookup"><span data-stu-id="2a94d-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="2a94d-123">Подключенные браузеры отображаются в окне подсказки.</span><span class="sxs-lookup"><span data-stu-id="2a94d-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="2a94d-124">Чтобы обновить подключенные браузеры, нажмите кнопку " **Обновить** " или нажмите клавиши CTRL + ALT + ВВОД.</span><span class="sxs-lookup"><span data-stu-id="2a94d-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="2a94d-125">Например, на следующем снимке экрана показан проект ASP.NET, созданный с помощью шаблона проекта MVC 5.</span><span class="sxs-lookup"><span data-stu-id="2a94d-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="2a94d-126">Приложение, работающее в двух браузерах, можно увидеть в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="2a94d-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="2a94d-127">В нижней части проекта открыт в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a94d-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="2a94d-128">В Visual Studio я изменил заголовок &lt;H1&gt; для домашней страницы:</span><span class="sxs-lookup"><span data-stu-id="2a94d-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="2a94d-129">При нажатии кнопки " **Обновить** " это изменение отображается в обоих окнах браузера:</span><span class="sxs-lookup"><span data-stu-id="2a94d-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="2a94d-130">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="2a94d-130">**Notes**</span></span>

- <span data-ttu-id="2a94d-131">Чтобы включить связь с браузером, задайте `debug=true` в элементе [&gt;компиляции&lt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) в файле Web. config проекта.</span><span class="sxs-lookup"><span data-stu-id="2a94d-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="2a94d-132">Приложение должно выполняться на локальном узле.</span><span class="sxs-lookup"><span data-stu-id="2a94d-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="2a94d-133">Приложение должно быть предназначено для .NET 4,0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2a94d-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="2a94d-134">Просмотр панели мониторинга связи с браузером</span><span class="sxs-lookup"><span data-stu-id="2a94d-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="2a94d-135">На панели мониторинга связи с браузером отображаются сведения о соединениях с гиперссылками в браузере.</span><span class="sxs-lookup"><span data-stu-id="2a94d-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="2a94d-136">Чтобы просмотреть панель мониторинга, выберите раскрывающееся меню ссылки браузера (маленькая стрелка рядом с кнопкой **Обновить** ).</span><span class="sxs-lookup"><span data-stu-id="2a94d-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="2a94d-137">Затем щелкните **панель мониторинга связи с браузером**.</span><span class="sxs-lookup"><span data-stu-id="2a94d-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="2a94d-138">На панели мониторинга перечислены подключенные браузеры и URL-адрес, на который перешел каждый браузер.</span><span class="sxs-lookup"><span data-stu-id="2a94d-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="2a94d-139">В разделе **Предварительные требования** показаны все шаги, необходимые для включения связи браузера для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="2a94d-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="2a94d-140">Например, на следующем снимке экрана показан проект, в котором для параметра "Отладка" в файле Web. config задано значение false.</span><span class="sxs-lookup"><span data-stu-id="2a94d-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="2a94d-141">Включение связи браузера для статических HTML-файлов</span><span class="sxs-lookup"><span data-stu-id="2a94d-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="2a94d-142">Чтобы включить связь браузера для статических HTML-файлов, добавьте следующий код в файл Web. config.</span><span class="sxs-lookup"><span data-stu-id="2a94d-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="2a94d-143">Для повышения производительности следует удалить этот параметр при публикации проекта.</span><span class="sxs-lookup"><span data-stu-id="2a94d-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="2a94d-144">Отключение связи с браузером</span><span class="sxs-lookup"><span data-stu-id="2a94d-144">Disabling Browser Link</span></span>

<span data-ttu-id="2a94d-145">Связь с браузером включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2a94d-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="2a94d-146">Отключить ее можно несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="2a94d-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="2a94d-147">В раскрывающемся меню ссылки браузера снимите флажок **включить связь с браузером**.</span><span class="sxs-lookup"><span data-stu-id="2a94d-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="2a94d-148">В файле Web. config добавьте ключ с именем "VS: Енаблебровсерлинк" со значением "false" в разделе appSettings.</span><span class="sxs-lookup"><span data-stu-id="2a94d-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="2a94d-149">В файле Web. config задайте для параметра Отладка значение false.</span><span class="sxs-lookup"><span data-stu-id="2a94d-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="2a94d-150">Как это работает?</span><span class="sxs-lookup"><span data-stu-id="2a94d-150">How Does It Work?</span></span>

<span data-ttu-id="2a94d-151">Связь с браузером использует [SignalR](../../../signalr/index.md) для создания коммуникационного канала между Visual Studio и браузером.</span><span class="sxs-lookup"><span data-stu-id="2a94d-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="2a94d-152">Если связь с браузером включена, Visual Studio выступает в качестве сервера SignalR, к которому могут подключаться несколько клиентов (браузеров).</span><span class="sxs-lookup"><span data-stu-id="2a94d-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="2a94d-153">Связь с браузером также регистрирует модуль HTTP с помощью ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2a94d-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="2a94d-154">Этот модуль внедряет специальные &lt;скрипта&gt; ссылки на каждый запрос страницы с сервера.</span><span class="sxs-lookup"><span data-stu-id="2a94d-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="2a94d-155">Чтобы просмотреть ссылки на скрипты, выберите в браузере пункт "Просмотреть исходный код".</span><span class="sxs-lookup"><span data-stu-id="2a94d-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="2a94d-156">Исходные файлы не изменяются.</span><span class="sxs-lookup"><span data-stu-id="2a94d-156">Your source files are not modified.</span></span> <span data-ttu-id="2a94d-157">Модуль HTTP динамически вставляет ссылки на скрипты.</span><span class="sxs-lookup"><span data-stu-id="2a94d-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="2a94d-158">Так как код на стороне браузера является всего лишь JavaScript, он работает во всех браузерах, [поддерживаемых SignalR](../../../signalr/overview/getting-started/supported-platforms.md), без необходимости использования подключаемого модуля браузера.</span><span class="sxs-lookup"><span data-stu-id="2a94d-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
