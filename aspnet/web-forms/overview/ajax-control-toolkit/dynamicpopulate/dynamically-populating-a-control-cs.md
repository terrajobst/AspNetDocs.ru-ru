---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
title: Динамическое заполнение элемента управленияC#() | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет результирующее значение целевым элементом управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e1fec43e-1daf-49d2-b0c7-7f1b930455cc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 24f88e44e0f878127314774d4e8846f80133413e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430560"
---
# <a name="dynamically-populating-a-control-c"></a><span data-ttu-id="6add9-103">Динамическое заполнение элемента управления (C#)</span><span class="sxs-lookup"><span data-stu-id="6add9-103">Dynamically Populating a Control (C#)</span></span>

<span data-ttu-id="6add9-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6add9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6add9-105">[Скачать код](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6add9-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)</span></span>

> <span data-ttu-id="6add9-106">Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="6add9-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>

## <a name="overview"></a><span data-ttu-id="6add9-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="6add9-107">Overview</span></span>

<span data-ttu-id="6add9-108">Элемент управления `DynamicPopulate` в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="6add9-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="6add9-109">В этом руководстве показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="6add9-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="6add9-110">Шаги</span><span class="sxs-lookup"><span data-stu-id="6add9-110">Steps</span></span>

<span data-ttu-id="6add9-111">Во-первых, вам понадобится ASP.NET Web Service, который реализует метод, вызываемый `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="6add9-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="6add9-112">Для класса веб-службы требуется атрибут `ScriptService`, определенный в `Microsoft.Web.Script.Services`; в противном случае ASP.NET AJAX не может создать клиентский прокси JavaScript для веб-службы, которая, в свою очередь, необходима для `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="6add9-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="6add9-113">Веб-метод должен рассчитывать на один аргумент типа String, именуемый `contextKey`, поскольку элемент управления `DynamicPopulate` отправляет один фрагмент сведений о контексте при каждом вызове веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6add9-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="6add9-114">Следующая веб-служба возвращает текущую дату в формате, представленном аргументом `contextKey`:</span><span class="sxs-lookup"><span data-stu-id="6add9-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="6add9-115">Затем веб-служба сохраняется как `DynamicPopulate.cs.asmx`.</span><span class="sxs-lookup"><span data-stu-id="6add9-115">The web service is then saved as `DynamicPopulate.cs.asmx`.</span></span> <span data-ttu-id="6add9-116">Кроме того, можно реализовать метод `getDate()` как метод страницы в реальной странице ASP.NET с помощью элемента управления `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="6add9-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="6add9-117">На следующем шаге создайте новый файл ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6add9-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="6add9-118">Как всегда, первым шагом является включение `ScriptManager` на текущую страницу для загрузки библиотеки ASP.NET AJAX и обеспечения работы набора средств управления:</span><span class="sxs-lookup"><span data-stu-id="6add9-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="6add9-119">Затем добавьте элемент управления Label (например, с помощью элемента управления HTML с тем же именем или &lt;`asp:Label` /&gt; веб-элемент управления), который позже покажет результат вызова веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6add9-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample3.aspx)]

<span data-ttu-id="6add9-120">Кнопка HTML (как HTML-элемент управления, так как нам не требуется обратная передача на сервер) будет использоваться для активации динамического заполнения:</span><span class="sxs-lookup"><span data-stu-id="6add9-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="6add9-121">Наконец, нам нужен элемент управления `DynamicPopulateExtender` для подключения к ним.</span><span class="sxs-lookup"><span data-stu-id="6add9-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="6add9-122">Будут установлены следующие атрибуты (помимо очевидных, `ID` и `runat`=`"server"`):</span><span class="sxs-lookup"><span data-stu-id="6add9-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="6add9-123">`TargetControlID`, куда помещается результат вызова веб-службы</span><span class="sxs-lookup"><span data-stu-id="6add9-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="6add9-124">`ServicePath` путь к веб-службе (пропустите, если вы хотите использовать метод страницы)</span><span class="sxs-lookup"><span data-stu-id="6add9-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="6add9-125">`ServiceMethod` имя веб-метода или метода страницы</span><span class="sxs-lookup"><span data-stu-id="6add9-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="6add9-126">`ContextKey` сведения о контексте для отправки веб-службе</span><span class="sxs-lookup"><span data-stu-id="6add9-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="6add9-127">элемент `PopulateTriggerControlID`, который активирует вызов веб-службы</span><span class="sxs-lookup"><span data-stu-id="6add9-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="6add9-128">`ClearContentsDuringUpdate`, следует ли очищать целевой элемент во время вызова веб-службы</span><span class="sxs-lookup"><span data-stu-id="6add9-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="6add9-129">Как видите, элементу управления требуются некоторые сведения, но размещение всех данных в нем довольно прямолинейно.</span><span class="sxs-lookup"><span data-stu-id="6add9-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="6add9-130">Ниже приведена разметка для элемента управления `DynamicPopulateExtender` в текущем сценарии.</span><span class="sxs-lookup"><span data-stu-id="6add9-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="6add9-131">Запустите страницу ASP.NET в браузере и нажмите кнопку. Вы получите текущую дату в формате "месяц-день-год".</span><span class="sxs-lookup"><span data-stu-id="6add9-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>

<span data-ttu-id="6add9-132">[![нажатии кнопки получает дату с сервера](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6add9-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="6add9-133">При нажатии кнопки извлекается дата с сервера ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-populating-a-control-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="6add9-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6add9-134">Дальше</span><span class="sxs-lookup"><span data-stu-id="6add9-134">Next</span></span>](dynamically-populating-a-control-using-javascript-code-cs.md)
