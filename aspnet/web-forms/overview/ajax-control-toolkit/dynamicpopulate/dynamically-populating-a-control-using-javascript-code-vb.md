---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: Динамическое заполнение элемента управления с помощью кода JavaScript (VB) | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет результирующее значение целевым элементом управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b2bd5b1571ccebc9baa501b29743aecdb4543fb2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497382"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a><span data-ttu-id="96834-103">Динамическое заполнение элемента управления с помощью кода JavaScript (VB)</span><span class="sxs-lookup"><span data-stu-id="96834-103">Dynamically Populating a Control Using JavaScript Code (VB)</span></span>

<span data-ttu-id="96834-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="96834-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="96834-105">[Скачать код](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="96834-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)</span></span>

> <span data-ttu-id="96834-106">Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="96834-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="96834-107">Можно также активировать заполнение с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="96834-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="96834-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="96834-108">Overview</span></span>

<span data-ttu-id="96834-109">Элемент управления `DynamicPopulate` в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="96834-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="96834-110">Можно также активировать заполнение с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="96834-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="96834-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="96834-111">Steps</span></span>

<span data-ttu-id="96834-112">Во-первых, вам понадобится ASP.NET Web Service, который реализует метод, вызываемый элементом управления `DynamicPopulateExtender`.</span><span class="sxs-lookup"><span data-stu-id="96834-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="96834-113">Веб-служба реализует метод `getDate()`, который принимает один аргумент типа String, именуемый `contextKey`, поскольку элемент управления `DynamicPopulate` отправляет один фрагмент сведений о контексте при каждом вызове веб-службы.</span><span class="sxs-lookup"><span data-stu-id="96834-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="96834-114">Ниже приведен код (файл `DynamicPopulate.vb.asmx`), который извлекает текущую дату в одном из трех форматов:</span><span class="sxs-lookup"><span data-stu-id="96834-114">Here is the code (file `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

<span data-ttu-id="96834-115">На следующем шаге создайте новый сайт ASP.NET и начните с элемента управления ScriptManager ASP.NET AJAX:</span><span class="sxs-lookup"><span data-stu-id="96834-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

<span data-ttu-id="96834-116">Затем добавьте элемент управления Label (например, с помощью элемента управления HTML с тем же именем или `<asp:Label />` веб-элемента управления), который позже покажет результат вызова веб-службы.</span><span class="sxs-lookup"><span data-stu-id="96834-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

<span data-ttu-id="96834-117">Затем включите элемент управления `DynamicPopulateExtender` и укажите сведения о веб-службе, целевой элемент управления, но не имя элемента управления, запускающего заполнение. это будет сделано позже с помощью пользовательского JavaScript!</span><span class="sxs-lookup"><span data-stu-id="96834-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

<span data-ttu-id="96834-118">Теперь к части JavaScript.</span><span class="sxs-lookup"><span data-stu-id="96834-118">Now to the JavaScript part.</span></span> <span data-ttu-id="96834-119">Функция `$find()`, определенная библиотекой AJAX ASP.NET, возвращает ссылку на объекты на стороне сервера из набора средств ASP.NET AJAX Control Toolkit, например `DynamicPopulateExtender`.</span><span class="sxs-lookup"><span data-stu-id="96834-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="96834-120">В текущем файле `$find("dpe")` возвращает ссылку на один элемент управления `DynamicPopulateExtender` на странице.</span><span class="sxs-lookup"><span data-stu-id="96834-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="96834-121">Он предоставляет метод, именуемый `populate()`, который запускает процесс динамического заполнения.</span><span class="sxs-lookup"><span data-stu-id="96834-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="96834-122">Методу `populate()` требуется один аргумент: ключ контекста, который будет использоваться в качестве аргумента для веб-метода `getDate()`.</span><span class="sxs-lookup"><span data-stu-id="96834-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="96834-123">Например, `$find("dpe").populate("format1")` будет заполнять метку текущей датой в формате "месяц-день-год".</span><span class="sxs-lookup"><span data-stu-id="96834-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="96834-124">Чтобы сделать пример более гибким, пользователь может выбрать один из нескольких форматов даты.</span><span class="sxs-lookup"><span data-stu-id="96834-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="96834-125">Для каждого из них отображается переключатель.</span><span class="sxs-lookup"><span data-stu-id="96834-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="96834-126">Когда пользователь щелкнет переключатель, код JavaScript динамически заполняет метку выбранным форматом даты.</span><span class="sxs-lookup"><span data-stu-id="96834-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="96834-127">Ниже перечислены эти переключатели.</span><span class="sxs-lookup"><span data-stu-id="96834-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

<span data-ttu-id="96834-128">Обратите внимание на то, что в контексте переключателя выражение JavaScript `this.value` относится к значению текущей кнопки, то есть именно та же информация, с которой может работать метод `getDate()`.</span><span class="sxs-lookup"><span data-stu-id="96834-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>

<span data-ttu-id="96834-129">[![нажатии кнопки получает дату с сервера в указанном формате.](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="96834-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="96834-130">При нажатии кнопки извлекается дата с сервера в указанном формате ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="96834-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="96834-131">[Назад](dynamically-populating-a-control-vb.md)
> [Вперед](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)</span><span class="sxs-lookup"><span data-stu-id="96834-131">[Previous](dynamically-populating-a-control-vb.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)</span></span>
