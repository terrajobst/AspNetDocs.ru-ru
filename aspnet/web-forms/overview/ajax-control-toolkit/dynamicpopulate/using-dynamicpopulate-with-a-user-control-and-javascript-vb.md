---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: Использование DynamicPopulate с пользовательским элементом управления и JavaScript (VB) | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет результирующее значение целевым элементом управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497304"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="7e9b5-103">Использование DynamicPopulate с пользовательским элементом управления и кодом JavaScript (VB)</span><span class="sxs-lookup"><span data-stu-id="7e9b5-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>

<span data-ttu-id="7e9b5-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7e9b5-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7e9b5-105">[Скачать код](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7e9b5-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="7e9b5-106">Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="7e9b5-107">Можно также активировать заполнение с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="7e9b5-108">Однако особое внимание необходимо предпринять, когда расширитель находится в пользовательском элементе управления.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-108">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="overview"></a><span data-ttu-id="7e9b5-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="7e9b5-109">Overview</span></span>

<span data-ttu-id="7e9b5-110">Элемент управления `DynamicPopulate` в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="7e9b5-111">Можно также активировать заполнение с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="7e9b5-112">Однако особое внимание необходимо предпринять, когда расширитель находится в пользовательском элементе управления.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="7e9b5-113">Шаги</span><span class="sxs-lookup"><span data-stu-id="7e9b5-113">Steps</span></span>

<span data-ttu-id="7e9b5-114">Во-первых, вам понадобится ASP.NET Web Service, который реализует метод, вызываемый элементом управления `DynamicPopulateExtender`.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="7e9b5-115">Веб-служба реализует метод `getDate()`, который принимает один аргумент типа String, именуемый `contextKey`, поскольку элемент управления `DynamicPopulate` отправляет один фрагмент сведений о контексте при каждом вызове веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="7e9b5-116">Ниже приведен код (файлы `DynamicPopulate.vb.asmx`), который извлекает текущую дату в одном из трех форматов:</span><span class="sxs-lookup"><span data-stu-id="7e9b5-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="7e9b5-117">На следующем шаге создайте новый пользовательский элемент управления (`.ascx` файл), обозначенный следующим объявлением в первой строке:</span><span class="sxs-lookup"><span data-stu-id="7e9b5-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="7e9b5-118">Для вывода данных, поступающих с сервера, будет использоваться элемент &gt; `label`&lt;.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="7e9b5-119">Кроме того, в файле пользовательского элемента управления будут использоваться три переключателя, каждая из которых представляет один из трех возможных форматов даты, поддерживаемых веб-службой.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="7e9b5-120">Когда пользователь щелкает один из переключателей, браузер выполнит код JavaScript, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7e9b5-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="7e9b5-121">Этот код обращается к `DynamicPopulateExtender` (не беспокойтесь о странном ИДЕНТИФИКАТОРе, он будет рассмотрен позже) и активирует динамическое заполнение данными.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="7e9b5-122">В контексте текущего переключателя `this.value` ссылается на его значение, которое `format1`, `format2` или `format3` именно то, что предполагает веб-метод.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="7e9b5-123">Единственным элементом пользовательского элемента управления пока является элемент управления `DynamicPopulateExtender`, который связывает переключатели с веб-службой.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="7e9b5-124">Опять же, вы можете отметить странный идентификатор, используемый в элементе управления: `mcd1$myDate` вместо `myDate`.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="7e9b5-125">Ранее код JavaScript использовал `mcd1_dpe1` для доступа к `DynamicPopulateExtender` вместо `dpe1`. Такая стратегия именования является особой требованием при использовании `DynamicPopulateExtender` в пользовательском элементе управления.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="7e9b5-126">Кроме того, необходимо внедрить пользовательский элемент управления, чтобы сделать его все работать.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="7e9b5-127">Создайте новую страницу ASP.NET и зарегистрируйте префикс тега для только что реализованного пользовательского элемента управления:</span><span class="sxs-lookup"><span data-stu-id="7e9b5-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="7e9b5-128">Затем включите элемент управления `ScriptManager` ASP.NET AJAX на новой странице:</span><span class="sxs-lookup"><span data-stu-id="7e9b5-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="7e9b5-129">Наконец, добавьте пользовательский элемент управления на страницу.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="7e9b5-130">Необходимо задать только его атрибут `ID` (и `runat="server"`, конечно), но также необходимо задать конкретное имя: `mcd1` так как это префикс, используемый в пользовательском элементе управления для доступа к нему с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="7e9b5-131">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="7e9b5-131">And that's it!</span></span> <span data-ttu-id="7e9b5-132">Страница ведет себя ожидаемым образом: пользователь щелкает один из переключателей, элемент управления в наборе инструментов вызывает веб-службу и отображает текущую дату в нужном формате.</span><span class="sxs-lookup"><span data-stu-id="7e9b5-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>

<span data-ttu-id="7e9b5-133">[![переключатели находятся в пользовательском элементе управления](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7e9b5-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="7e9b5-134">Переключатели находятся в пользовательском элементе управления ([щелкните, чтобы просмотреть изображение с полным размером](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="7e9b5-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7e9b5-135">Назад</span><span class="sxs-lookup"><span data-stu-id="7e9b5-135">Previous</span></span>](dynamically-populating-a-control-using-javascript-code-vb.md)
