---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: Часть 8. окончательные страницы, обработка исключений и заключение | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 8 добавляется страница контактов, страница About и исключение...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474342"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="dae9e-104">Часть 8. Последние страницы, обработка исключений и заключение</span><span class="sxs-lookup"><span data-stu-id="dae9e-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="dae9e-105">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="dae9e-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="dae9e-106">В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET.</span><span class="sxs-lookup"><span data-stu-id="dae9e-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="dae9e-107">Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.</span><span class="sxs-lookup"><span data-stu-id="dae9e-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="dae9e-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="dae9e-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="dae9e-109">В части 8 добавляется страница контактов, сведения о странице и обработке исключений.</span><span class="sxs-lookup"><span data-stu-id="dae9e-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="dae9e-110">Это заключение серии.</span><span class="sxs-lookup"><span data-stu-id="dae9e-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a><span data-ttu-id="dae9e-111">Страница "Контакты" (отправка электронной почты с ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="dae9e-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="dae9e-112">Создание новой страницы с именем Контактус. aspx</span><span class="sxs-lookup"><span data-stu-id="dae9e-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="dae9e-113">С помощью конструктора создайте следующую форму, затратив особую заметку для включения Тулкитскриптманажер и элемента управления редактора из Ажаксконтролтулкит.</span><span class="sxs-lookup"><span data-stu-id="dae9e-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="dae9e-114">.</span><span class="sxs-lookup"><span data-stu-id="dae9e-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="dae9e-115">Дважды щелкните кнопку "Отправить", чтобы создать обработчик событий щелчка в файле кода программной части и реализовать метод отправки контактных данных в виде сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="dae9e-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="dae9e-116">Этот код требует, чтобы файл Web. config содержал запись в разделе конфигурации, в которой указан SMTP-сервер, используемый для отправки почты.</span><span class="sxs-lookup"><span data-stu-id="dae9e-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a><span data-ttu-id="dae9e-117">Сведения о странице</span><span class="sxs-lookup"><span data-stu-id="dae9e-117">About Page</span></span>

<span data-ttu-id="dae9e-118">Создайте страницу с именем AboutUs. aspx и добавьте любое нужное содержимое.</span><span class="sxs-lookup"><span data-stu-id="dae9e-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a><span data-ttu-id="dae9e-119">Глобальный обработчик исключений</span><span class="sxs-lookup"><span data-stu-id="dae9e-119">Global Exception Handler</span></span>

<span data-ttu-id="dae9e-120">Наконец, в рамках приложения мы выдавали исключения, и существуют непредвиденные обстоятельства, которые могут вызвать необработанные исключения в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="dae9e-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="dae9e-121">Никогда не нужно, чтобы необработанное исключение отображалось посетителю веб-узла.</span><span class="sxs-lookup"><span data-stu-id="dae9e-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="dae9e-122">Помимо плохой необработанных исключений пользователь может быть проблемой безопасности.</span><span class="sxs-lookup"><span data-stu-id="dae9e-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="dae9e-123">Для решения этой проблемы будет реализован глобальный обработчик исключений.</span><span class="sxs-lookup"><span data-stu-id="dae9e-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="dae9e-124">Для этого откройте файл Global. asax и обратите внимание на следующий предварительно созданный обработчик событий.</span><span class="sxs-lookup"><span data-stu-id="dae9e-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="dae9e-125">Добавьте код для реализации приложения\_обработчик ошибок следующим образом.</span><span class="sxs-lookup"><span data-stu-id="dae9e-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="dae9e-126">Затем добавьте страницу с именем Error. aspx в решение и добавьте этот фрагмент кода разметки.</span><span class="sxs-lookup"><span data-stu-id="dae9e-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="dae9e-127">Теперь в обработчике событий "страница\_загрузки" извлекаются сообщения об ошибках из объекта запроса.</span><span class="sxs-lookup"><span data-stu-id="dae9e-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a><span data-ttu-id="dae9e-128">Завершен</span><span class="sxs-lookup"><span data-stu-id="dae9e-128">Conclusion</span></span>

<span data-ttu-id="dae9e-129">Мы увидели, что ASP.NET WebForms упрощает создание сложного веб-сайта с доступом к базе данных, членством, AJAX и т. д.</span><span class="sxs-lookup"><span data-stu-id="dae9e-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="dae9e-130">очень быстро.</span><span class="sxs-lookup"><span data-stu-id="dae9e-130">pretty quickly.</span></span>

<span data-ttu-id="dae9e-131">Надеюсь, в этом учебнике вы предоставили вам средства, необходимые для начала создания собственных приложений ASP.NET WebForms.</span><span class="sxs-lookup"><span data-stu-id="dae9e-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="dae9e-132">Назад</span><span class="sxs-lookup"><span data-stu-id="dae9e-132">Previous</span></span>](tailspin-spyworks-part-7.md)
