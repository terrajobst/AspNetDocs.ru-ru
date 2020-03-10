---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: Трассировка в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: Показывает, как включить трассировку в веб-API ASP.NET.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484344"
---
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="8abb7-103">Трассировка в веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="8abb7-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="8abb7-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8abb7-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="8abb7-105">При попытке отладки веб-приложения не заменяется хороший набор журналов трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="8abb7-106">В этом учебнике показано, как включить трассировку в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8abb7-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="8abb7-107">Эту функцию можно использовать для трассировки того, что делает платформа веб-API до и после того, как она вызывает контроллер.</span><span class="sxs-lookup"><span data-stu-id="8abb7-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="8abb7-108">Его также можно использовать для трассировки собственного кода.</span><span class="sxs-lookup"><span data-stu-id="8abb7-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8abb7-109">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="8abb7-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="8abb7-110">[Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (также работает с visual Studio 2015)</span><span class="sxs-lookup"><span data-stu-id="8abb7-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="8abb7-111">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="8abb7-111">Web API 2</span></span>
> - [<span data-ttu-id="8abb7-112">Microsoft. AspNet. WebApi. Tracing</span><span class="sxs-lookup"><span data-stu-id="8abb7-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="8abb7-113">Включение трассировки System. Diagnostics в веб-API</span><span class="sxs-lookup"><span data-stu-id="8abb7-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="8abb7-114">Сначала мы создадим новый проект веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8abb7-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="8abb7-115">В Visual Studio в меню **файл** выберите пункт **создать** > **проект**.</span><span class="sxs-lookup"><span data-stu-id="8abb7-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="8abb7-116">Вразделе Шаблоны **выберите веб** **-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="8abb7-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="8abb7-117">Выберите шаблон проекта веб-API.</span><span class="sxs-lookup"><span data-stu-id="8abb7-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="8abb7-118">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем — **консоль управления пакетами**.</span><span class="sxs-lookup"><span data-stu-id="8abb7-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="8abb7-119">В окне консоли диспетчера пакетов введите следующие команды.</span><span class="sxs-lookup"><span data-stu-id="8abb7-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="8abb7-120">Первая команда устанавливает последний пакет трассировки веб-API.</span><span class="sxs-lookup"><span data-stu-id="8abb7-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="8abb7-121">Он также обновляет основные пакеты веб-API.</span><span class="sxs-lookup"><span data-stu-id="8abb7-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="8abb7-122">Вторая команда обновляет пакет WebApi. WebHost до последней версии.</span><span class="sxs-lookup"><span data-stu-id="8abb7-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="8abb7-123">Если вы хотите ориентироваться на конкретную версию веб-API, используйте флаг-Version при установке пакета трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="8abb7-124">Откройте файл WebApiConfig.cs в папке App\_Start.</span><span class="sxs-lookup"><span data-stu-id="8abb7-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="8abb7-125">Добавьте следующий код в метод **Register** .</span><span class="sxs-lookup"><span data-stu-id="8abb7-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="8abb7-126">Этот код добавляет класс [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) в конвейер веб-API.</span><span class="sxs-lookup"><span data-stu-id="8abb7-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="8abb7-127">Класс **SystemDiagnosticsTraceWriter** записывает трассировки в [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span><span class="sxs-lookup"><span data-stu-id="8abb7-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="8abb7-128">Чтобы просмотреть трассировки, запустите приложение в отладчике.</span><span class="sxs-lookup"><span data-stu-id="8abb7-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="8abb7-129">Откройте браузер и перейдите по адресу `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="8abb7-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="8abb7-130">Инструкции трассировки записываются в окно вывода в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8abb7-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="8abb7-131">(В меню **вид** выберите **выходные данные**).</span><span class="sxs-lookup"><span data-stu-id="8abb7-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="8abb7-132">Поскольку **SystemDiagnosticsTraceWriter** записывает трассировки в **System. Diagnostics. Trace**, можно зарегистрировать дополнительные прослушиватели трассировки. Например, для записи трассировок в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="8abb7-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="8abb7-133">Дополнительные сведения о модулях записи трассировки см. в разделе [прослушиватели трассировки](https://msdn.microsoft.com/library/4y5y10s7.aspx) в MSDN.</span><span class="sxs-lookup"><span data-stu-id="8abb7-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="8abb7-134">Настройка SystemDiagnosticsTraceWriter</span><span class="sxs-lookup"><span data-stu-id="8abb7-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="8abb7-135">В следующем коде показано, как настроить модуль записи трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="8abb7-136">Существует два параметра, которыми можно управлять:</span><span class="sxs-lookup"><span data-stu-id="8abb7-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="8abb7-137">Verbose: при значении false Каждая трассировка содержит минимальную информацию.</span><span class="sxs-lookup"><span data-stu-id="8abb7-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="8abb7-138">Если значение — true, трассировки содержат дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="8abb7-138">If true, traces include more information.</span></span>
- <span data-ttu-id="8abb7-139">Минимумлевел: задает минимальный уровень трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="8abb7-140">Уровни трассировки, по порядку, являются отладкой, информацией, предупреждением, ошибкой и неустранимой.</span><span class="sxs-lookup"><span data-stu-id="8abb7-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="8abb7-141">Добавление трассировок в приложение веб-API</span><span class="sxs-lookup"><span data-stu-id="8abb7-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="8abb7-142">Добавление модуля записи трассировки обеспечивает немедленный доступ к трассировкам, созданным конвейером веб-API.</span><span class="sxs-lookup"><span data-stu-id="8abb7-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="8abb7-143">Для трассировки собственного кода можно также использовать модуль записи трассировки:</span><span class="sxs-lookup"><span data-stu-id="8abb7-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="8abb7-144">Чтобы получить модуль записи трассировки, вызовите **HttpConfiguration. Services. жеттрацевритер**.</span><span class="sxs-lookup"><span data-stu-id="8abb7-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="8abb7-145">С контроллера этот метод доступен через свойство **ApiController. Configuration** .</span><span class="sxs-lookup"><span data-stu-id="8abb7-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="8abb7-146">Чтобы написать трассировку, можно напрямую вызвать метод **итрацевритер. Trace** , но класс [итрацевритерекстенсионс](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) определяет некоторые методы расширения, которые более понятны.</span><span class="sxs-lookup"><span data-stu-id="8abb7-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="8abb7-147">Например, приведенный выше метод **info** создает трассировку со **сведениями**на уровне трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="8abb7-148">Инфраструктура трассировки веб-API</span><span class="sxs-lookup"><span data-stu-id="8abb7-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="8abb7-149">В этом разделе описывается написание пользовательского модуля записи трассировки для веб-API.</span><span class="sxs-lookup"><span data-stu-id="8abb7-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="8abb7-150">Пакет Microsoft. AspNet. WebApi. Tracing построен на основе более общей инфраструктуры трассировки в веб-API.</span><span class="sxs-lookup"><span data-stu-id="8abb7-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="8abb7-151">Вместо использования Microsoft. AspNet. WebApi. Tracing можно также подключить другую библиотеку трассировки и ведения журнала, например [NLog](http://nlog-project.org/) или [log4net](http://logging.apache.org/log4net/).</span><span class="sxs-lookup"><span data-stu-id="8abb7-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="8abb7-152">Чтобы получить трассировку, реализуйте интерфейс **итрацевритер** .</span><span class="sxs-lookup"><span data-stu-id="8abb7-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="8abb7-153">Вот простой пример:</span><span class="sxs-lookup"><span data-stu-id="8abb7-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="8abb7-154">Метод **итрацевритер. Trace** создает трассировку.</span><span class="sxs-lookup"><span data-stu-id="8abb7-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="8abb7-155">Вызывающий объект указывает категорию и уровень трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="8abb7-156">Категория может быть любой определяемой пользователем строкой.</span><span class="sxs-lookup"><span data-stu-id="8abb7-156">The category can be any user-defined string.</span></span> <span data-ttu-id="8abb7-157">Ваша реализация **трассировки** должна выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8abb7-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="8abb7-158">Создайте новый **трацерекорд**.</span><span class="sxs-lookup"><span data-stu-id="8abb7-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="8abb7-159">Инициализируйте его с помощью запроса, категории и уровня трассировки, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8abb7-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="8abb7-160">Эти значения предоставляются вызывающей стороной.</span><span class="sxs-lookup"><span data-stu-id="8abb7-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="8abb7-161">Вызов делегата *трацеактион* .</span><span class="sxs-lookup"><span data-stu-id="8abb7-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="8abb7-162">Внутри этого делегата ожидается, что вызывающий объект заполнит оставшуюся часть **трацерекорд**.</span><span class="sxs-lookup"><span data-stu-id="8abb7-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="8abb7-163">Напишите **трацерекорд**, используя любой способ ведения журнала, который вам нравится.</span><span class="sxs-lookup"><span data-stu-id="8abb7-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="8abb7-164">Пример, показанный здесь, просто вызывает **System. Diagnostics. Trace**.</span><span class="sxs-lookup"><span data-stu-id="8abb7-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="8abb7-165">Настройка модуля записи трассировки</span><span class="sxs-lookup"><span data-stu-id="8abb7-165">Setting the Trace Writer</span></span>

<span data-ttu-id="8abb7-166">Чтобы включить трассировку, необходимо настроить веб-API для использования реализации **итрацевритер** .</span><span class="sxs-lookup"><span data-stu-id="8abb7-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="8abb7-167">Это можно сделать с помощью объекта **HttpConfiguration** , как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="8abb7-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="8abb7-168">Активным может быть только один модуль записи трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-168">Only one trace writer can be active.</span></span> <span data-ttu-id="8abb7-169">По умолчанию веб-API задает &quot;не&quot; трассировку, которая не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="8abb7-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="8abb7-170">(&quot;оператор tracert&quot; не существует, поэтому код трассировки не должен проверять, имеет ли модуль записи трассировки **значение NULL** перед записью трассировки.)</span><span class="sxs-lookup"><span data-stu-id="8abb7-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="8abb7-171">Как работает трассировка веб-API</span><span class="sxs-lookup"><span data-stu-id="8abb7-171">How Web API Tracing Works</span></span>

<span data-ttu-id="8abb7-172">Трассировка в веб-API использует шаблон *фасадной* : когда трассировка включена, веб-API создает оболочку для различных частей конвейера запросов с помощью классов, выполняющих вызовы трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="8abb7-173">Например, при выборе контроллера конвейер использует интерфейс **ихттпконтроллерселектор** .</span><span class="sxs-lookup"><span data-stu-id="8abb7-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="8abb7-174">При включенной трассировке конвейер вставляет класс, который реализует **ихттпконтроллерселектор** , но вызывает реальную реализацию:</span><span class="sxs-lookup"><span data-stu-id="8abb7-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Трассировка веб-API использует шаблон фасадной.](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="8abb7-176">Ниже перечислены преимущества этой схемы.</span><span class="sxs-lookup"><span data-stu-id="8abb7-176">The benefits of this design include:</span></span>

- <span data-ttu-id="8abb7-177">Если не добавить модуль записи трассировки, компоненты трассировки не создаются и не влияют на производительность.</span><span class="sxs-lookup"><span data-stu-id="8abb7-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="8abb7-178">Если заменить службы по умолчанию, такие как **ихттпконтроллерселектор** , собственной пользовательской реализацией, трассировка не будет затронуты, так как трассировка выполняется объектом-оболочкой.</span><span class="sxs-lookup"><span data-stu-id="8abb7-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="8abb7-179">Вы также можете заменить всю платформу трассировки веб-API собственной настраиваемой платформой, заменив службу **итрацеманажер** по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="8abb7-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="8abb7-180">Реализуйте **итрацеманажер. Initialize** для инициализации системы трассировки.</span><span class="sxs-lookup"><span data-stu-id="8abb7-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="8abb7-181">Имейте в виду, что это заменяет *всю* платформу трассировки, включая весь код трассировки, встроенный в веб-API.</span><span class="sxs-lookup"><span data-stu-id="8abb7-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
